# Classifying "Op-Ed" vs "News"

## Background:
##### Format matters. As the modern consumer is bombarded with news and opinion from multiple sources via multiple formats it is becoming increasingly difficult for a consumer to distinguish what they should take as fact from what they should, by design, read as an opinion. I was interested in building a model that classified stories written for the "Op-Ed" desk and those written for the "News" desk, the two formats that coexist in every newsroom, print or broadcast.

## Objectives:

##### 1. Build a classification model that predicts "Op-Ed" from "News" pieces using NLP on the body of the articles themselves.


## The Data:

##### In 2019, the New York Times published 41,748 articles, not all of them were published in print. I obtained metadata from each article via the TImes Archive API, and scrapped each URL for the body of each article. In total, my final corpus of documents was 26,472 News articles and 2,012 Op-Ed articles. 

![Number of Op-Ed and News articles](img/num_opednews_2019.png)

---

## Model Performance: 

![Confusion Matrix](img/conf_matx.png)

## Analysis:

###### Important features: Many features are political and are causing the model to predict based on topic, not sentiment. 

![Important Features](img/important_feat_bar.png)



## Next Steps:

##### 1. Engineer data sets that control for the topic to discover features that differentiate bias in a specific topic. (eg. classifying political Op-Ed from news stories about politics. Connect model results to EDA.
##### 2. Optimize RF
##### 3. Build a [XGBoost](https://xgboost.readthedocs.io/en/latest/#)
##### 5. Flask app interactivity. 

![normalize for true](img/norm_true.png)
![normalize for pred](img/norm_pred.png)