# Project 3 : Web APIs & NLP 

### Table of Contents:
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Conclusion](#Conclusion)
- [Recommendation](#Recommendation)
- [Datasets](#Datasets)
---
### Problem Statement

Given a joke from a user, can we use a predictive modeling technique to determine whether a joke is a “dad joke” or a regular “joke” using subreddits r/dadjokes & r/jokes as a basis? Metrics used for determination will be accuracy score.


### Executive Summary

In order to begin any portion of this project, we first needed to figure out a method of approach in order to obtain the correct dataset to work with.  From outside research, we were introducced to an open source data scraping API, "pushshift.io", an API created and maintained by Jason Michael Baumgartner that allows the user to obtain a dictionary of subreddit data then converts it to a usable dataframe.  Using the pushshift API, we were able to access 85 reddit specific parameters that we can select from to data scrape.  In our case, we scraped the 'title' & 'selftext' features to combine in order to create our evaluation metrics.  

Following the use of pushshift API, we conducted a pre-eda where we crreated a new column to combine the texts in 'title' & 'selftext' columns.  Then, we removed the blanks, duplicates, HTML tags, non-letters, webpage links, and download pages to do an initial cleaning of our dataset.  Afterwards, We tokenized our text into a list of words using regular expression for main usage as well as lemmatization for our Multinomial Naive Bayes modeling.  

Using our tokenized words, we plotted to visualize the word frequency by subreddit to observe if there are any particular trends with certain words being used decisively more often in one subreddit vs. another.  Dissapointingly enough, we observed many words of multiple frequency yet none of the words seemed to have direct indication of whether the word belonged specifically to one subreddit or another.  Some of the most common words found were found in both subreddits and/or were too generic (such as 'im', 'said','dont','know').  A preliminary assumption we can deduce from this is that these can be used as stopwords that we can incorporate in our models.  Also, we decided to see if there are any trends in bigram words as well so went ahead and repeated the above process for the list of bigram words from which we noticed no other particular trend.

We've also created a venn-diagram of the top 15 most frequent words from each of the subreddits to visualize if there were any other patterns or discrepancies we can notice and our findings were similar to above results.  One key observation that we made was that the word 'wife' actually appeared more often in the 'jokes' subreddit when we would normaly presume any words related to 'dad' or 'wife' would be more apparent in the 'dadjokes' subreddit.

As far as our model selection goes, we decided to use a Logistic (Binomial) Regression using CountVectorizer which is used to predict the probability of a certain class or event in a binomial outcome scenario.  We also used a Multinomial Naive-Bayes modeling technique on lemmatized wordset which could be used to classify vectors based on probabilies of the training variables.  Using the models mentioned, we used a gridcv and pipelines to iterate and determine the best model parameters to obtain the most proficient model to use for our predictions.

We also created a confusion matrix to visualzie and determine the results of our findings for each of the models as well.


### Conclusion

Compared to our baseline prediction of 52% (towards r/dadjokes), our models did outperform by a slight amount.  Our logistic Regression using CountVectorizer yielded a train/test scores of 90%/58% when using TfidfVectorizer yielded a train/test scores of 88%/57%.  Both vectorizers yielded a pretty close result (especially vs the test set) which were only ~5% above the baseline score.  As for our Multinomial Naive-Bayes model, it yielded a train/test result of 81%/56% which indicates that it performed slightly below the logistic regression models even though it still performed above the baseline score of 52% by approximately ~4%.

  


### Recommendation

In the end, if we were to select our best model, it would be our logistic regression model that used CountVectorizer with an accuracy score of 58% on the testing set.  However, we definitely need to investigate our case using more dataset (we only observed 2500 posts per reddit on a 5 month history).  Also, we need to see if we can accomodate our temporary limitations, which we view it as limitations that can be solved, such as evaluating repetition of texts in a single post.  There are also long term limitations such as "Are jokes too general as a topic to classify?" "What type of users are primarily apparent in r/jokes vs. r/dadjokes.

We cannot conclusively say we have model that can predict the nature of 'jokes' yet but it does seem like something that is possible if we were to have additional data sources to surpass our limitations.


### Datasets

- [dadjokes dataset](./dataset/dadjokes.csv)
- [jokes dataset](./dataset/jokes.csv)

These datasets are scraped data from r/dadjokes & r/jokes using pushshift.io API.




