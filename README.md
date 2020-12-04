# proposal-ish
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


Vectorizer: len(feature_names) = 221213
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

**12/2: trimmed extra starting/finishing paragraphs leftover from beautiful soup**

Models: 
Vectorizer: len(feature_names) = 237438 by function:trim_fat, strip_accents='ascii'
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.9241545893719807
recall = 0.878095238095238
precision = 0.9695057833859095

Vectorizer: len(feature_names) = 231896 **triming** most all except (~3000) articles
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.9478260869565217
recall = 0.9095238095238095
precision = 0.9865702479338843

Vectorizer: (feature_names) = 5000
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.9497584541062802
recall = 0.900952380952381
**precision = 1.0 (rate of correct predictions of op-ed articles out of all predictions.never guessed op-ed)**
(tn, fp, fn, tp)=(1020, 0, 104, 946)
**what's happening here? it's not guessing that anything is op-ed...?**

accuracy = (tp + tn) / (tn + fn + tp + fp)
recall = (tp) / (tp + fn)
precision = (tp) / (tp + fp)

STRUGGLED with NLTK at 10pm. realized after stemming and lemmatizing that hadn't removed punctuation. by this point I ralized how nltk worked, through list comprehensions, i think?

[Stemming and Lemmatization](https://medium.com/towards-artificial-intelligence/how-and-why-to-implement-stemming-and-lemmatization-from-nltk-5f0cc69d2af)

Stemming:
-types: Porter's algorithm. the Snowball algorithm.
"Stemming also reduces the accuracy of a model."
"Snowball Stemmer is an improved version of the Porter stemmer. This method is highly precise over large data-sets."

Lemmatization:
"The accuracy of the NLP model is comparatively high in this method."
"The root word is known as a lemma."

*Porter and Snoball stemming methods convert some words to non-dictionary words. Such conversion of words restricts the use of porter and snowball stemming methods to search engines, n-gram context, and text classification problems. 

*Lemmatization can be used in paragraph/document summarization, word/sentence prediction, sentiment analysis, and others.

*Lemmatization is mandatory for critical projects and projects where sentence structure matter like language applications. Stemming or Lemmatization do affect precision and recall. Stemming reduces precision performance, and increases recall performance.*

Models:
Vectorizer: SnowballStemmer('english'). stop_words=None?. features = 263722
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.9289855072463769
recall = 0.9057142857142857
precision = 0.9519519519519519
(tn, fp, fn, tp) = 972 48 99 951

Vectorizer: SnowballStemmer('english'). stop_words='english'. max_features = 10000
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.9516908212560387
recall = 0.9095238095238095
precision = 0.9947916666666666
1015 5 95 955

Vectorizer: SnowballStemmer('english'). stop_words='english'. max_features = None
*did fit seperate from transform
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.9304347826086956
recall = 0.8942857142857142
precision = 0.9660493827160493
tn=987, fp=33, fn=111, tp=939)

@       0.022 +/- 0.003
facebook0.022 +/- 0.003
twitter 0.006 +/- 0.001
york    0.006 +/- 0.002
)       0.005 +/- 0.002
follow  0.004 +/- 0.001
said    0.003 +/- 0.001
polici  0.001 +/- 0.000
data    0.000 +/- 0.000
econom  0.000 +/- 0.000
tuesday 0.000 +/- 0.000
elect   0.000 +/- 0.000
mean    0.000 +/- 0.000

### finally decided to delete the tail w/ the extra paragraph from beautiful soup
sum(none_df.type_of_material == "Op-Ed") = 182
sum(none_df.type_of_material == "News") = 3838


Vectorizer:  
SnowballStemmer('english'). stop_words='english'. max_features = None
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.7842344618494189
recall = 0.6722772277227723
precision = 0.8761290322580645
tn=873, fp=96, fn=331, tp=679)
234816


TfidfVectorizer(max_df=0.9, min_df=0.15,
                tokenizer=<function snowball_tokenize at 0x7fcec1177f80>)
2020-12-03 20:33:43.177976
accuracy = 0.9196563921172309
recall = 0.9574257425742574
precision = 0.8928901200369345
tn=853, fp=116, fn=43, tp=967)
num_features = 540
<class 'numpy.ndarray'>
CPU times: user 14.6 ms, sys: 3.48 ms, total: 18.1 ms
Wall time: 15.7 ms



### punctuation work
Vectorizer:  
SnowballStemmer('english'). stop_words='english'. max_features = None
RandomForestClassifier(max_depth=2, random_state=0)
accuracy = 0.8388074785245073
recall = 0.7663366336633664
precision = 0.9031505250875146
tn=886, fp=83, fn=236, tp=774)
254169
2

## trimmed OG dataset by removing 
for the year of 2019 that leaves 28213 'news' articles and '2043' op-ed articles

### still need to move df.type_of_material == news.section_name == 'Opinion' to "Op-Ed"






#### what is this random forest doing?

1. takes all X and y which is my text and classifiers as vectors(tfidf)
2. take a random number of 8278 instances (tfidf vector) and uses a random number of 219112 features to make best decision.
3. bags/bootstraps that model
4. does it again a bunch of times


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

# 1. refine dataset OR optimize vectorizer

### Blocks:

- my github is a mess. do i need to look into gitignore? 
- organizaing workflow
- how do i keep my models/vectorizers straight? what is random state?
- can't get 2018 json request to work. LocationParseError: Failed to parse: <Response [200]>


### Questions:
- are random forest inexpensve to run?



## notes

### notes on NYTimes staff:

- [NYTIMES staff](https://en.wikipedia.org/wiki/List_of_The_New_York_Times_employees)
- [The New York Times Editorial Board](https://www.nytimes.com/interactive/2018/opinion/editorialboard.html)
- [Kathleen Kingsbury](https://en.wikipedia.org/wiki/Kathleen_Kingsbury) acting Editorial Page Editor June 7, 2020 - the November election" at The New York Times, replacing James Bennet.


- [James Bennet](https://en.wikipedia.org/wiki/James_Bennet_(journalist) editorial page editor May 2016-June 2020
records to 05/2016

### from article (https://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/)

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

### curse of dimensionality

The common theme of these problems is that when the dimensionality increases, the volume of the space increases so fast that the available data become sparse.


### lead's notes

- geni importance plot
- difference in article length for op-ed vs news
~~- top 20 words for each class~~
~~- min and max df~~
~~- stem and lemmetize~~
~~- max features trim
~~- min/max df freq trim


