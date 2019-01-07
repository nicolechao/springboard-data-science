# 2nd Capstone Project


## Problem: Sentiment Analysis on Movie Reviews with Tweets

![Home](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%202/Images/Homepage.png)

In this project we analyze sentiment on recent movie-related tweets on a scale of five values: negative, somewhat negative, neutral, somewhat positive, positive.

Twitter is an well-known American online news and social networking service on which users post and interact with messages known as "tweets". In 2012, more than 100 million users posted 340 million tweets a day and the service handled an average of 1.6 billion search queries per day. 

As tweets refelct the real-time popular opinion, by scraping tweets from twitter website and analyzing sentiment on movie reviews with tweets, it can be used for movie theater to predict how good the movie is and whether they should continue playing it or add more number of showings. It can also be used for movie producer to decide what kind of movie will be more popular and optimize their revenue.


## Potential Clients
As mentioned in previous session, by analyzing sentiment on movie reviews with tweets, it can be used for both movie theater and move producer to optimize their revenue.


## Data
* We scraped data using Selenium and Twitter search URL on movie-related tweets. More details in project report.


## Approach
1. Apply data wrangling, exploratory data analysis on the scraped data set.
2. Apply VADER to generate sentiment scores as our labels.
3. Apply deep learning models, including LSTM, mLSTM, CNN and TCN for this supervised classification problem. 


## Used Packages
1. Web Scraping: selenium
2. Data Wrangling and Visualization: pandas, numpy, matplotlib, seaborn
3. Natural Language Processing: re, nltk, wordcloud, gensim
4. Machine Learning and Deep Learning: sklearn, keras

## Deliverables
1. Code
 - [Data scraping](https://github.com/nicolechao/springboard-data-science/tree/master/Capstone%202/Data%20Scraping)
 - [Data wrangling](https://github.com/nicolechao/springboard-data-science/tree/master/Capstone%202/Data%20Wrangling)
 - [Exploratory data analysis](https://github.com/nicolechao/springboard-data-science/tree/master/Capstone%202/Exploratory%20Data%20Analysis)
 - [Deep learning modeling](https://github.com/nicolechao/springboard-data-science/tree/master/Capstone%202/Modeling) 
2. [Milestone Report](https://github.com/nicolechao/springboard-data-science/tree/master/Capstone%202/Milestone%20Report)
3. [Project Report](https://github.com/nicolechao/springboard-data-science/tree/master/Capstone%202/Project%20Report)
