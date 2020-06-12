# Identifying Potential Customers Based on Reddit Posts
---
#### Julia Kelman: [GitHub](https://github.com/JulKelman)  
  
  
## Problem Statement
---
We are a company who created a new product meant to help individuals with Autism Spectrum Disorder (ASD). We want to market online and as a result need to be able to identify users who are part of our target population based on their online content (reddit/facebook/blog posts for example).  
The autism community has a great online presence with many facebook groups and blogs dedicated to supporting individuals with this disorder. However, many of those groups are not restricted to people with ASD. Indeed, other disorders such as Obsessive Compulsive Disorder (OCD) share many symptoms with autism [source](https://www.webmd.com/brain/autism/autism-similar-conditions). As a result, online resources are often geared towards both of those populations.  
To start, our company will focus on identifying potential customers on one major blog for a support group for individuals with ASD and individuals with OCD.   
Since our product is specific to individuals with ASD, we need to be able to differentiate between people with ASD and OCD based on what they post on this online platform.  
We plan to solve this problem by using submissions on an Autism reddit page and an OCD reddit page to build a classification model able to classify a user as having either ASD or OCD based on their post with the highest level of accuracy possible.   
This model could then be used to identify potential customers on blogs for people with autism or OCD. 


## Executive Summary 
---
Our goal is to build a model able to classify a submission as either part of the ASD subreddit or the OCD subreddit. In order to do so, 1653 posts from the [ASD subreddit page](https://www.reddit.com/r/autism/) and 2209 posts from the [OCD subreddit page](https://www.reddit.com/r/OCD/) were gathered using an API and the steps outlined in the [Data Gathering Notebook](https://git.generalassemb.ly/julia-kelman/project_3/blob/master/code/Gathering%20Data%20Notebook.ipynb). Our final dataframe contained 3862 submissions posted by individual users between November 2019 and March 2020. For each of those submissions, 9 variables were provided. For a detailed list and description of those variables refer to the [data dictionary](#Data-Dictionary).   
The dataframe was cleaned making sure to deal with any null values, and the submission text was cleaned to remove any non-text information. The words were then stemmed in order to improve our model's accuracy. Exploratory analysis included analysis of the comments, scores, and most frequent words. Data visualisation tools were used to identify trends and valuable insights from those analysis. Five models were then tested: baseline, logistic regression, kNN, naive bayes, and SVM, each with either a Count Vectorizer or TFIDF Vectorizer.   
The model with the highest test accuracy was selected, evaluated, and conclusions and recommendations were derived to optimize the identification of potential customers. 

## Project Table of Contents:
---
- Reddit Data Import
    - Data Dictionary
- Data Cleaning
- Exploratory Data Analysis
    - Comments Analysis
    - Score Analysis
    - Timestamps Analysis
    - Most Frequent Words Analysis
    - Creating Custom Stopwords List
- Model Preparation
- Modeling
    - Baseline Model
    - Logistic Regression
        - Logistic Regression + CountVectorizer
        - Logistic Regression + TFIDFVectorizer
    - kNN
        - kNN + CountVectorizer
        - kNN + TFIDFVectorizer
    - Naive Bayes
        - Multinomial Naive Bayes + CountVectorizer  
        - Gaussian NB + TFIDFVectorizer
    - SVM
        - SVM + CountVectorizer
        - SVM + TFIDFVectorizer
- Model Selection
- Model Evaluation
    - Confusion Matrix
    - Understanding Misclassifications
    - Coefficients Interpretation
- Conclusion & Recommendations
- References

## Project Files 
---
 [Reddit Data](https://github.com/JulKelman/Classifying-Reddit-Submissions/tree/master/Data)   

## Data Dictionary 
---
|Feature|Type|Description|
|:---|:---:|:---|
|title|object|Submission post title.| 
|selftext|object|Main content/body of the submission post.|
|subreddit|object|Subreddit page the post belonged to (ASD or OCD).| 
|created_utc|int|Created Universal Time (utc) when the submission was originally posted.|
|author|object|Submission post author (more specificially their reddit name).|
|num_comments|int|Number of comments for each submission post.|
|score|int|Number of upvotes minus number of downvotes a submission post received.|
|is_self|boolean|Wether or not a submission is a self post.|
|timestamp|object|Date the submission was posted (derived from the created_utc feature).|


## Conclusions and Recommendations 
--- 
We identified a Logistic Regression model with TFIDF Vectorizer and custom stopwords as the model giving us the highest predictive power. This model classifies wether a post is part of the ASD subreddit or the OCD subreddit with 93% accuracy. As a result, this model would allow us to identify potential customers with autism based on their submissions on online resource blogs geared towards individuals with ASD and OCD.
In 3.8% of cases we’re spending advertising money on the wrong users. In 2.8% of cases we’re missing out on potential customers. There is a tradeoff between those 2 types of errors.
In the future, we can modify our model to minimize one type or the other based on recommendations from the marketing team. For instance, if the marketing budget is low, we may want to minimize the number of users we misclassify as having ASD when they actually have OCD (leading to unecessary advertising spendings). On the other hand, if we have a big marketing budget, we may want to minimize the number of users we misclassify as having OCD when they actually have ASD (making sure we are reaching out to every potential customers). 

## References
--- 
[Autism Reddit](https://www.reddit.com/r/autism/)  
[OCD Reddit](https://www.reddit.com/r/OCD/)  
[OCD resembles ASD](https://www.webmd.com/brain/autism/autism-similar-conditions)  
[Sheryl Paul Book](https://www.amazon.com/gp/product/B07FDQVKZ9/ref=dbs_a_def_rwt_hsch_vapi_tkin_p1_i0) 
