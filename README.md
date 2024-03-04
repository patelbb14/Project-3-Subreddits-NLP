# UnresolvedMysteries vs FanTheories Subreddits

## Project 3: Web APIs & NLP

### Problem Statement

You are a data scientist at Reddit and a co-worker is about to quit their job as they are not happy. As a parting gift, the co-worker goes through some of the subreddits and messes them up by taking some of the posts from one subreddit and placing them in another. The objective of this project is to build a classification model that will be able to sort these subreddits into the correct subreddit. We will focus on two subreddits : UnresolvedMysteries and FanTheories. 

---

### Datasets


#### Data Dictionary

Used the following source to find subreddits that were text based only. 
https://www.reddit.com/r/AskReddit/comments/cigqig/what_are_some_good_text_based_subreddits_to/?onetap_auto=true

The subreddits chosen were 'UnresolvedMysteries' and 'FanTheories'. Below is the data dictionary of the data that was used for this project.

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**created_utc**|*float64*|'UnresolvedMysteries' and 'FanTheories' Subreddits| Time post was created in UTC
|**title**|*object*|'UnresolvedMysteries' and 'FanTheories' Subreddits| Title of post
|**self_text**|*object* |'UnresolvedMysteries' and 'FanTheories' Subreddits| Text of post
|**subreddit**|*object* |'UnresolvedMysteries' and 'FanTheories' Subreddits| What subreddit the post is from
|**score**|*int64* |'UnresolvedMysteries' and 'FanTheories' Subreddits| Aggregate sum of upvotes and downvotes (no negatives)
|**num_comments**|*int64* |'UnresolvedMysteries' and 'FanTheories' Subreddits| The number of comments


---

### Executive Summary

You are a data scientist at Reddit and a co-worker is about to quit their job as they are not happy. As a parting gift, the co-worker goes through some of the subreddits and messes them up by taking some of the posts from one subreddit and placing them in another. The objective of this project is to build a classification model that will be able to sort these subreddits into the correct subreddit. We will focus on two subreddits : UnresolvedMysteries and FanTheories. 

In order to classify posts correctly, some initial data cleaning and EDA were done such as dropping null value rows, looking at top 15 words, looking at top 15 bigrams, looking at top 15 trigrams, and doing sentiment analysis on score. NLP parsing was also required before beginning to model using both Count Vectorizer and TFIDF (Term Frequency Inverse Document Frequency) Vectorizer. Six different classification models were tested using various parameter search methods.


---

### Conclusions & Recommendations

| Num | Vectorizer | Model | Best Score | Train Score |Test Score (Accuracy)| Best Parameters |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | CountVectorizer | Multinomial Naïve Bayes |0.9873|0.9969|0.9788|{'cvec__max_features': None, 'cvec__min_df': 2, 'cvec__ngram_range': (2, 2)} |
| 2 | TfidfVectorizer | Multinomial Naïve Bayes |0.9873|0.9975|0.9797|{'tvec__max_features': None, 'tvec__min_df': 2, 'tvec__ngram_range': (2, 2)} |
| 3 | CountVectorizer | Random Forest Classifier |0.9735|1.0|0.9755|{'rf__max_depth': None, 'rf__min_samples_leaf': 1, 'rf__n_estimators': 150} |
| 4 | TfidfVectorizer | Random Forest Classifier |0.9740|1.0|0.9772|{'rf__max_depth': None, 'rf__min_samples_leaf': 1, 'rf__n_estimators': 500} |


All the models above outperformed the baseline accuracy score of 0.510049. Since the focus was on getting as many correct predictions as possible, the Multinomial Naïve Bayes with TfidfVectorizer (the second model on the table above) overall had the best predictive performance on the classification problem. However, we can see the the Multinomial Naïve Bayes with CountVectorizer also has very close results.

For next steps, moving forward, we could potentially include more relevant and similar subreddits into our research, and label all these as binary classification of 0 whereas UnresolvedMysteries remains as 1. This may expand our modeling capacity. In addition, image posts were not taken into account when picking the subreddits. In addition, we can also look at the title of posts and see how well that would be in predicting the correct subreddits.

The model works well but does not achieve a 100% accuracy. To handle this, a Misplaced Subreddit Post button could be a good idea to use so that users can reach out and let us know that the post seems to be in the wrong subreddit.

