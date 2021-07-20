# Project 5 NLP : Tweets about Telsa Stock

# Project Proposal


## Question


The idea of this project is to monitor Telsa stock price movement on Tweets sentimental analysis over Twitter on a short term period. 

If we can pick up today’s tweets sentiment analysis directions (positive or negative) for Tesla to see what people talk about Telsa and how people react on its performance as related news or market trend, it can affect the way the stock moves tomorrow. 

On Twitter, one tweet posted from a single Twitter account can be retweeted many times to share info and influence even more people. The number of followers that the Twitter account has can also be measure of the influence of the tweets since more followers the account has, more influential the tweets can impact the crowd and potentially on stock price.

The main idea is to explore the tweets data for short term period range to do unsupervised learning like topic modeling on the tweets and interpret the topics to see how these relate to Telsa stock price moves.


## Data


#### Twitter
-  Resource: collected by [Twitter](https://twitter.com) API Tweepy.

-  Date Range: start from 07/12   
               07/05 -07/13 (since the current API only let user collect the past 6-9 days data so it will be my research date period)

	__Features including:__
	
<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/tweets_raw.png">


#### Tesla Stock Price
-  Resource: downloaded from [Yahoo Finance](https://finance.yahoo.com)

-  Date Range: 07/06 – 07/14 (since our hypothesis is today’s tweets will affect tomorrow stock price so we want to look into the daily stock price data on the next day of each tweets date to monitor the movement)



	__Features including:__
	- Variables: 

		Date, Open, High, Low, Close, Adj Close, Volumne 
	






## Tools
1. Tweepy (Twitter API)
2. Tokenizer
3. sklearn
	- Feature Extraction
    * from sklearn.feature_extraction.text import TfidfVectorizer, ENGLISH_STOP_WORDS
    - Topic Modeling
    * from sklearn.decomposition import NMF, TruncatedSVD, LatentDirichletAllocation
4. NLTK VADER (sentiment analysis)
5. Classification (stock moves up or down)





## MVP Goal:

✨Clean the raw text and make Tweet/Topic Matrix for topic modeling to show what the topic clusters are.✨
