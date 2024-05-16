# -NYTimes-Fox-News-Climate-Change-Topic-Modelling-BERTopic


## Dataset & Preparation
The Dataset includes articles from the Nytimes & Fox News over a one year period, and studies and contrasts them based on the use of Climate Change Articles. It details the process of identifying and counting articles related to climate change from NYTimes and Fox News, using specific climate-related terms and a function to determine if an article is related to climate change. This includes filtering duplicates, selecting English language articles, merging title and body columns, and creating a new column for the source URI.  The proportion of climate change articles to total articles by source, resulting in percentages for both NYTimes and Fox News in terms of climate change article calcualtions.


## Bar Chart Visualization 
It filters and counts climate change-related articles, comparing the proportion of such articles to the total number of articles over time.
![Bar](./images_png/bar.png)

## Extreme Weather Visualization
Looking at cases where the name entity is extreme weather.

![Extreme Weather 2](./images_png/ex_weather.png)

## Bertopic 

BERTopic is a topic modeling technique that leverages the BERT (Bidirectional Encoder Representations from Transformers) language model to generate dense vector representations of documents. Here’s why it’s considered effective:

- Contextual Understanding: BERTopic uses BERT’s deep learning architecture, which captures the context of words in a document, leading to more meaningful topic representations.
- Dynamic Topic Reduction: It can reduce the number of topics after the initial model has been trained, allowing for fine-tuning and better topic quality.
- Hierarchical Topics: BERTopic can find a hierarchy of topics, providing a structured overview of the topics discovered.
- Class Probability: It calculates the probability of a document belonging to a topic, which can be useful for topic classification tasks.

```python
from sentence_transformers import SentenceTransformer
from bertopic import BERTopic
from sklearn.feature_extraction.text import CountVectorizer
from umap import UMAP
import pandas as pd

# Initialize SentenceTransformer model
sentence_model = SentenceTransformer("all-distilroberta-v1")

# Define English stop words
stop_words = 'english'

# Preprocess documents using CountVectorizer with stop words removal
count_vectorizer = CountVectorizer(stop_words=stop_words)
nytimes_vectorized = count_vectorizer.fit_transform(nytimes_docs['text'])
foxnews_vectorized = count_vectorizer.transform(foxnews_docs['text'])

# Convert sparse matrix to list of strings
nytimes_texts = [' '.join(row.split()) for row in nytimes_docs['text']]
foxnews_texts = [' '.join(row.split()) for row in foxnews_docs['text']]

# Create and train a BERTopic model for NYTimes documents
nytimes_model = BERTopic(calculate_probabilities=True, verbose=True, embedding_model=sentence_model)
nytimes_topics, _ = nytimes_model.fit_transform(nytimes_texts)

# Update topics to remove stop words
nytimes_model.update_topics(nytimes_texts, vectorizer_model=count_vectorizer)

# Generate topic representations over time for NYTimes documents (without top_n_topics)
nytimes_topics_over_time = nytimes_model.topics_over_time(
    nytimes_texts,  # Pass the list of strings instead of the DataFrame
    nytimes_docs['date'].tolist(),
    nr_bins=20
)

# Visualize ALL the topics over time for NYTimes documents
nytimes_model.visualize_topics_over_time(nytimes_topics_over_time)

# Create and train a BERTopic model for FoxNews documents
foxnews_model = BERTopic(calculate_probabilities=True, verbose=True, embedding_model=sentence_model)
foxnews_topics, _ = foxnews_model.fit_transform(foxnews_texts)

# Update topics to remove stop words
foxnews_model.update_topics(foxnews_texts, vectorizer_model=count_vectorizer)

# Generate topic representations over time for FoxNews documents (without top_n_topics)
foxnews_topics_over_time = foxnews_model.topics_over_time(
    foxnews_texts,  # Pass the list of strings instead of the DataFrame
    foxnews_docs['date'].tolist(),
    nr_bins=20
)

# Visualize ALL the topics over time for FoxNews documents
foxnews_model.visualize_topics_over_time(foxnews_topics_over_time)
```

- SentenceTransformer: A pre-trained model from the sentence_transformers library is initialized. The model used here is "all-distilroberta-v1", which is a distilled version of the RoBERTa model optimized for sentence-level tasks.
- CountVectorizer: This is a method from the sklearn.feature_extraction.text library that converts a collection of text documents into a matrix of token counts. It’s used here with English stop words removed to preprocess the documents.
- BERTopic: An instance of the BERTopic class is created for both NYTimes and FoxNews documents. The calculate_probabilities parameter is set to True to calculate the probabilities of topics per document, and verbose is set to True to print out progress logs. The embedding_model parameter is set to the SentenceTransformer model initialized earlier.
- fit_transform: The BERTopic model is trained on the preprocessed texts from NYTimes and FoxNews documents. This method assigns a topic to each document and returns the topics.
- update_topics: After the initial training, the topics are updated to remove common stop words, refining the topic representation.
- topics_over_time: This function calculates how topics have evolved over time by binning the documents into a specified number of bins (nr_bins=20) based on their dates.
- visualize_topics_over_time: This method generates a visualization of how topics have changed over time, providing insights into the temporal dynamics of the topics.

https://colab.research.google.com/github/StephenJudeD/-NYTimes-Fox-News-Climate-Change-Topic-Modelling-BERTopic/blob/main/bertopic_nytimes_fox_v1.ipynb

### Topics over time
![NYTimes DTM](./images_png/nytimes_dtm.png)
![Fox News DTM](./images_png/foxnews_dtm.png)
### Intertopic Distribution
![InterTopic NYTimes](./images_png/intertopic_nytimes.png)
![InterTopic Fox](./images_png/intertopic_fox.png)
### Bar Chart
![NYTimes Bar](./images_png/nytimes_bar.png)
![Fox News Bar](./images_png/foxnews_bar.png)
### Heatmap
![NYTimes Heatmap](./images_png/nytimes_heatmap.png)
![Fox News Heatmap](./images_png/foxnews_heatmap.png)
### Documents
![NYTimes Doc](./images_png/nytimes_doc.png)
![Fox News Doc](./images_png/foxnews_doc.png)
---
