# Tweets about Tesla Stock

Sabrina Yang


## Abstract

The purpose of this project is to analyze and predict Tesla’s stock price movement based on sentiment analysis of tweets involving the company and its ticker. Tweet sentiment can be directionally positive or negative, and in various magnitudes. By understanding the relationship between tweets and sentiment, we will be able to understand better how Tesla’s stock price might move in subsequent days/hours. On Twitter, one tweet posted from a single Twitter account can be retweeted many times to share info and influence many people. The number of followers that the Twitter account has can also be a measure of the influence of the tweets since the more followers the account has, the more influential the tweets can impact market sentiment and potentially stock price. I explored tweet data in short term periods and performed unsupervised learning including topic modeling on the tweets, in order to interpret the results and how they may relate to stock price movements.


## Design
The project’s design will center around unsupervised learning. I will also perform topic modeling and sentiment analysis as part of the analytical framework. Together, these tools will allow me to gather insights around tweets and the overall impact on stock price.


## Data
1. Tweets

It is gathered from [Twitter](https://twitter.com) during 07/11- 07/19. Due to Twitter’s API restriction, I was only able to get data in this short timeframe. For each date, I collected 2000 tweets and the raw dataset has a total 18,019 tweets with the features ['date', 'username', 'description', 'location', 'following', 'followers','totaltweets', 'retweetcount', 'text', 'hashtags'].
This project can observe short-term activities only. 



2. Tesla Stock Price data


It is gathered from [Yahoo Finance](https://finance.yahoo.com/quote/TSLA/). It has columns 
 _['High', 'Low', 'Open', 'Close', 'Volume', 'Adj Close']_
 and for rows it has the certain dates of data I need to match my tweets data. 
  



## Methodology

*Data Collection*

1.  Tweets data: use Twitter API Tweepy to grab tweets and its details
2.	Tesla Stock Price chart: use pandas web.DataReader to read data from Yahoo Finance website.  

*Text Preprocessing*

1.	remove digits, punctations, urls
2.	stem and tokenize - PorterStemmer
3.	add some necessary words into stopwords list 
(_['tsla','tesla', 'just', 'hi', 'thi', 'week', 'like', 'think', 'aaaannnddd', 'aaaand', 'aaa','wa','look', 'day', 'stock', 'today', 'ha','gt', 'whi', 'minut', 'time']_)
and remove stopwords by TfidfVectorizer and generate tweet_word_matrix

*Topic Modeling*

1. use Non-Negative Matrix Factorization(NMF) to generate tweet_topic_matrix. The reason I chose this method over LSA is because tweets are relatively short documents.
2.	The first time I set n_components=15 to make 15 topics on dataset
3.	After the next step of Filter Out Noises, I did it again to get 8 topics for my final result. 


*Filter Out Noises*

1.	The purpose is to clean advertisement tweets
2.	Use _str.contains()_ to filter out the tweets contain Chatroom, Sign Up, Daily Alert, etc.
3.	After filtering, the dataset still has 9400 tweets so it’s still a decent amounts.

*Unsupervised Learning*

1.	Kmeans Clustering (used the elbow method to find the best k = 8) on tweet-topic-matrix
2.	do clustering plot by TSNE instead of PCA and  TruncatedSVD is because the topics number is 8 which is a relatively high number so TSNE is more suitable for this dimensionality reduction.
3.	t-SNE(T- distributed Stochastic Neighbor Embedding):
t-SNE is also a method to reduce the dimension. One of the most major differences between PCA and t-SNE is it preserves only local similarities whereas PA preserves large pairwise distance maximize variance.


## Tools

1. Twitter API 
- Tweepy

2. Sklearn  
- from sklearn.feature_extraction.text import TfidfVectorizer, ENGLISH_STOP_WORDS  
- from sklearn.decomposition import NMF
- from sklearn.cluster import KMeans
- from sklearn.manifold import TSNE

3. NLTK 
- from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer

4. Numpy

5. Pandas
- import pandas_datareader.data as web

6. Plotting
- import matplotlib.pyplot as plt
%matplotlib inline
- from mpl_toolkits.mplot3d import Axes3D



## Summary

### 1. Topic Modeling Results (15 topics)

- topic_0 : Ads - promoting trading alert chatroom 
- topic_1 : FUD (Fear ,Uncertainty,  Doubt)  # insolvency = bankrupty   # crash, panic
- topic_2 : Ads - stock app promotion
- topic_3 : Ads - stock option trading investment advice
- topic_4:  Bitcoin - how much Tesla made from bitcoin investment
- topic_5:  # fintwit  # wallstreetbet # trends  # top stocks: aapl, spce(Virgin Galactic), mrna
- topic_6:  Ads - free option trade, sign up
- topic_7:  Ads - daily alert
- topic_8:  Car - Tesla FSD Subscription, drive
- topic_9:  STOCK - technical analysis and price charts  
- topic_10: Ads - stock alert for discord
- topic_11: STOCK - trade ideas, stock watchlist
- topic_12: Elon Musk tweets activities, solarcity, cybertruck, court (Tesla bought Solarcity recently)
- topic_13: STOCK - TSLA stock personal trading ideas - Short > Long 
- topic_14: STOCK - TSLA stock personal opinions and feelings - buy dip


some of topics are noises, ( daily alert, promotions, chatrooms) but some are useful:

    - elon musk's tweets
    - tech chart patterns
    - retail traders about tesla news


### 2. Top Modeling Results after filtering/cleaning noises (8 topics)


- topic_0: STOCK - Personal trading ideas, but still ads for chatroom and stock tickers
- topic_1: FUD  (Fear ,Uncertainty,  Doubt)                                                   
- topic_2: Bitcoin -  how much Tesla made from bitcoin investment
- topic_3: # fintwit # wallstreetbet # trends  # top stocks: aapl, spce(Virgin Galactic), mrna
- topic_4: Car - tesla FSD subscription, drive, Elon Musk, News, STOCK - Short > Long(0.01)
- topic_5: STOCK - technical analysis and price charts: bullish > bearish (0.08)
- topic_6: STOCK - influencer account promote meme stock - amc, gme,  Stock Watchlist (CCIV, PLTR, SOFI)
- topic_7 :STOCK - Option contract, trading idea, still some ads, promoting group, learning resources like Youtube link


### 3. Sentiment Analysis & Stock Price

Sentiment analysis was performed for 2 key words: $TSLA and Tesla. The result was different for both as users discuss $TSLA for stock related tweets while Tesla was used more for discussing the company, the car, and Elon Musk.

For $TSLA, as the sentiment compound score decreased (i.e., more negative in sentiment than prior days), stock price also fell. However, once both sentiment and stock price dropped to lower levels, sentiment became volatile. This makes sense as a drop in Tesla’s stock price tend to bring in the twitter crowd that tries to boost the market by tweeting positive tweets.

**$TSLA**
<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/date_stock_sentiment-two-scales.png" >



For Tesla, the correlation between sentiment and stock price was more difficult to discern. Initially, as sentiment rose, Tesla’s stock price dropped. However, towards the end of the period, sentiment dropped and Tesla’s stock price rose. It is likely that since twitter users use the word “Tesla” to discuss the car and other aspects of the company, the correlation with its stock price is lower than would be for the ticker $TSLA.

**Tesla**
<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/Tesla_date_stock_sentiment-two-scales.png" >
 
 
### 4. Kmeans Clustering & plot by using TSNE

k = 8 so here shows 8 different clusters by colors as plotting by this dimensionality reduction method called TSNE on 2 dimensions.
<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/Kmeans_cluster_TSNE_plot.png">
