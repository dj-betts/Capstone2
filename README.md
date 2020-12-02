-**Bias detection** 
- *Features:* NLP of articles posted on twitter and facebook.  I want to focus on certain type of words that tend to be highly biased, for example "absolutes"  (i.e. 'totally', 'finally', 'all', 'every') for language that is more "nuanced" (i.e. idk. not those words?). OR I could pull all articles from a newspapers and analyze articles from op-ed, editorial, and new desks.
- *Target1:* predicitng if an article is "fake" based on words used
- *Target2:* measure the bias of an article based on the words with some threshold of bias vs. opinion. it to NLP of podcasts and youtube channels.
- *Target3:* model that correctly guesses whether an article is from an op-ed section or not. These are all a similar idea.
- *Resources:* Twitter or Facebook API w/ articles flagged as "fake". NYTimes op-ed vs news desk.
- *Obstacles:* It feels like a big project and I'm not sure if it's in my skill set. 


11/23: scraped january 2019 op-ed and news articles. research nytime staff. got metadata into series. made metadata keys function. multi articles metadata into df. pipline finished. 3 hours for one month. eda on meata data. concat oped and news into one df.

11/24: start building pipline for url request

11/29: january 2019 articles pulled

11/30: initial eda on january 2019 w/ articles. try to flatten text of articles. trim text of articles. multinomial naive baise w/ .89 accuracy. built pipeline for api to full df in 3 functions. 11 minutes/month was the fastest. 

12/1: downloaded rest of 2019 throughout the day. realized my .89 accuracy was because my model was guessing everying was 'news' because of imbalanced classed (10:1). read in the morning. created a notebook for building a dataset out of the full 2019 file. finally got to full data set.

Vectorizer:
TfidfVectorizer(stop_words='english')

Imbalanced-learn: 
RandomUnderSampler(random_state=0)

Models: 
MultinomialNB()
accuracy = 0.7840579710144927
recall = 0.9838095238095238
precision = 0.7060833902939166

RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.9478260869565217
recall = 0.9257142857142857
precision = 0.9700598802395209

### Next steps:
- genie importance plot to find most influencial words (feature engineering?)

- ROC curves (decision rules notes)

- limiting the bag of words. 

- currently len(feature_names) = 219112 (len(feature_names) = 235420 if strip_accents='ascii'
- **think about what it would do to limit the bag of words?
- **high demensionality 
- ** feature engineering - two ways. mathematically  & domain knowledge-ically.
* mathematically
* domain knowledge-ically


- need better visuals of data. word legnths. common words. word cloud?... heatmap of geni importance plot?

- depending on genie importance plot add stop words. work more w/ the vectorizer. 

### Blocks:
- my github is a mess. do i need to look into gitignore? 
- organizaing workflow
- how do i keep my models/vectorizers straight? what is random state?
- 







# notes

## from article (https://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/)

1. collect more data
2. try changing performace matric
    - confusion matrix: A breakdown of predictions into a table showing correct predictions (the diagonal) and the types of incorrect predictions made (what classes incorrect predictions were assigned).
    
    - precision: A measure of a classifiers exactness.
    
    - recall: A measure of a classifiers completeness
    
    - F1 Score (or F-score): A weighted average of precision and recall.


    * Kappa (or [Cohen’s kappa](https://en.wikipedia.org/wiki/Cohen%27s_kappa)): Classification accuracy normalized by the imbalance of the classes in the data.
    
    * ROC Curves: Like precision and recall, accuracy is divided into sensitivity and specificity and models can be chosen based on the balance thresholds of these values.
    
3. resample data

    - Consider testing under-sampling when you have an a lot data (tens- or hundreds of thousands of instances or more)
    - Consider testing over-sampling when you don’t have a lot of data (tens of thousands of records or less)
    - Consider testing random and non-random (e.g. stratified) sampling schemes.
    - Consider testing different resampled ratios (e.g. you don’t have to target a 1:1 ratio in a binary classification problem, try other ratios)
    
    
4. Try generating synthetic samples
     
    - #### ?? You could sample them empirically within your dataset or you could use a method like Naive Bayes that can sample each attribute independently when run in reverse. **You will have more and different data, but the non-linear relationships between the attributes may not be preserved.** ??

5. Try differente algorithms
    - decision trees often perform well on imbalanced datasets. 
    - C4.5, C5.0, CART and Random Forest
    - [For some example R code using decision trees, see my post titled](http://machinelearningmastery.com/non-linear-classification-in-r-with-decision-trees/)
    - [For an example of using CART in Python and scikit-learn](http://machinelearningmastery.com/get-your-hands-dirty-with-scikit-learn-now/)
    
6. Try penalized models
7. Try a Different Perspective
8. Try getting creative

## curse of dimensionality

The common theme of these problems is that when the dimensionality increases, the volume of the space increases so fast that the available data become sparse.



