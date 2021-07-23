# Tweets about Tesla Stock

Sabrina Yang


## Abstract

The purpose of this project is to help lending institutions to determine which borrowers to lend to. In order to achieve this, I built a model to predict whether a borrower would repay their loan or not. Lenders will loan a principal amount out to borrowers and also charge interest. Once the principal is paid back in full at the end of the loan, the lender will make a significant profit. This is why they would prefer not to risk losing even a single dollar as this can greatly affect their profit. There are many variables and features associated with loans, which can be found on Lending Club’s website. However, I determined that 28 features are most likely to have the largest impact on the model and have analyzed these as such. By building a model that incorporates these features, the lender would be able to quickly discern which borrowers are most likely to repay or not repay their loans. 

## Design
The question of whether a client will pay or not can be solved by using supervised learning as a classification tool. Doing a hard prediction will help me predict whether the client will pay or not. The lending institution is concerned about losing any principal at all and so would rather not lend than to lose any money at all. So in this project, recall will be more focused than precision. As such, I took the F2 score as my critical examination tool.


## Data
1. Tweets
It is gathered from [Twitter](https://twitter.com) from 07/11- 07/19. Due to API restriction, I was only able to get this timeframe data and each date I collected for 2000 tweets, and the raw dataset has total18019 tweets info with the features included 
_['date', 'username', 'description', 'location', 'following', 'followers','totaltweets', 'retweetcount', 'text', 'hashtags']_
This project can observe short term activities only. 



2. Tesla Stock Price chart
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
2.	Use str.contains() to filter out the tweets contain Chatroom, Sign Up, Daily Alert, etc.
3.	After filtering, the dataset still has 9400 tweets so it’s still a decent amounts.

*Unsupervised Learning*

1.	Kmeans Clustering (used the elbow method to find the best k = 8) on tweet-topic-matrix
2.	do clustering plot by TSNE since the topics number is 8 and it’s a relatively high number so TSNE is more suitable.


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

### 1. Topic Modeling Results

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


### 2. Top Modeling Results after filtering/cleaning noises


- topic_0: STOCK - Personal trading ideas, but still ads for chatroom and stock tickers
- topic_1: FUD  (Fear ,Uncertainty,  Doubt)                                                   
- topic_2: Bitcoin -  how much Tesla made from bitcoin investment
- topic_3: # fintwit # wallstreetbet # trends  # top stocks: aapl, spce(Virgin Galactic), mrna
- topic_4: Car - tesla FSD subscription, drive, Elon Musk, News, STOCK - Short > Long(0.01)
- topic_5: STOCK - technical analysis and price charts: bullish > bearish (0.08)
- topic_6: STOCK - influencer account promote meme stock - amc, gme,  Stock Watchlist (CCIV, PLTR, SOFI)
- topic_7 :STOCK - Option contract, trading idea, still some ads, promoting group, learning resources like Youtube link


### 3. Sentiment Analysis & Stock Price


<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/date_stock_sentiment-two-scales.png" >

### 4. Kmeans Clustering – plot by TSNE

<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/Kmeans_cluster_TSNE_plot.png">
