## 2nd Capstone Project

# Sentiment Analysis on Movie Reviews with Tweets

#### Yueh-Tung (Nicole) Chao


![Home](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%202/Images/Homepage.png)


## Problem
In this project we analyze sentiment on recent movie-related tweets on a scale of five values: negative, somewhat negative, neutral, somewhat positive, positive.

Twitter is an well-known American online news and social networking service on which users post and interact with messages known as "tweets". In 2012, more than 100 million users posted 340 million tweets a day and the service handled an average of 1.6 billion search queries per day. 

As tweets refelct the real-time popular opinion, by scraping tweets from twitter website and analyzing sentiment on movie reviews with tweets, it can be used for movie theater to predict how good the movie is and whether they should continue playing it or add more number of showings. It can also be used for movie producer to decide what kind of movie will be more popular and optimize their revenue.


## Client
As mentioned in previous session, by analyzing sentiment on movie reviews with tweets, it can be used for both movie theater and move producer to optimize their revenue.


## Data Set / Data 
We scraped data using Selenium and Twitter search URL on movie-related tweets. To be more specific, given the following link, we can give the search URL keyword, start-date & end-date for searching,

```
https://twitter.com/search?q=<keyword>%20since%3A<start_date>%20until%3A<end_date>&amp;amp;amp;amp;amp;amp;lang=tr%22
```

and it would return a page of tweets which fit these constraints.


Here's an example where we would like to search 'Mission Impossible' from 2018-06-01 to 2018-09-11.

```
https://twitter.com/search?q=missionimpossible%20since%3A2018-06-01%20until%3A2018-09-11&amp;amp;amp;amp;amp;amp;lang=tr%22
```

and then we can get tweets about 'Mission Impossible' posted between 2018-06-01 and 2018-09-11. Snapshot as followed:

![MI6](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%202/Images/MissionImpossible.png)

Ny repeating the above process for recent movies, we collected about **15002** data points.


## Data Wrangling
After scraping the data, we conduct the following steps to clean up data.

1. Drop duplicate data points.
2. Remove '\n' which represents newline in tweets.
3. Remove URLs in tweets using regular expression.

After applying the above steps, there are **14696** data points left.


## Initial Findings
During exploratory data analysis, we ask the following questions:

1. How to identify useful tweets?
2. With all the useful tweets, which movie occurs most?
3. Usually how many tokens are there in a tweets?

and ask follow-up questions if needed.

Initial findings are:

1. We identify useful tweets using predefined keywords.
 - After searching predfined keywords and remove data points without these keywords, there are 7628 tweets.
2. Then we check which movies occur most in tweets. The most common two are Jurassic World & Crazy Rich Asians considering our searching start-date is 2018-06-01 to 2018-09-11.
![MostCommon](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%202/Images/MostCommon.png)
3. We also analyze length of a tweets. After removing unwanted tokens, stop words & applying lemmatization, most of the tweets have about 4 ~ 11 useful words.
![WordCountHist](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%202/Images/WordCountHistogram.png)
4. We tried to identify topic using both bad-of-words & TF-IDF. Looks like TD-IDF can at least generate more meaningful topic than bag-of-words.
5. We inspect tweets outliers which are really short or long. An observation is short tweets are pretty straight forward on sentiments while long ones seem not.

## Other Potential Data Sets
More data can be scraped give predefined keywords using Twitter Search URL.