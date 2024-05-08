# -NYTimes-Fox-News-Climate-Change-Topic-Modelling-BERTopic

## Dataset & Preparation
The Dataset includes articles from the Nytimes & Fox News over a one year period, and studies and contrasts them based on the use of Climate Change Articles. It details the process of identifying and counting articles related to climate change from NYTimes and Fox News, using specific climate-related terms and a function to determine if an article is related to climate change. This includes filtering duplicates, selecting English language articles, merging title and body columns, and creating a new column for the source URI.  The proportion of climate change articles to total articles by source, resulting in percentages for both NYTimes and Fox News in terms of climate change article calcualtions.


## Bar Chart Visualization 
It filters and counts climate change-related articles, comparing the proportion of such articles to the total number of articles over time.
![Bar](./images_png/bar.png)

## Extreme Weather Visualization
Looking at cases where the name entity is extreme weather.

![Extreme Weather 1](./images_png/ex1_weather.png)
---
![Extreme Weather 2](./images_png/ex_weather.png)

## Bertopic

![NYTimes DTM](./images_png/nytimes_dtm.png)
![Fox News DTM](./images_png/foxnews_dtm.png)
---
![InterTopic NYTimes](./images_png/intertopic_nytimes.png)
![InterTopic Fox](./images_png/intertopic_fox.png)
---
![NYTimes Bar](./images_png/nytimes_bar.png)
![Fox News Bar](./images_png/foxnews_bar.png)
---
![NYTimes Heatmap](./images_png/nytimes_heatmap.png)
![Fox News Heatmap](./images_png/foxnews_heatmap.png)
---
![NYTimes Doc](./images_png/nytimes_doc.png)
![Fox News Doc](./images_png/foxnews_doc.png)
---
