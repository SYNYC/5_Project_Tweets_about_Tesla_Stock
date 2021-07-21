# MVP
##### Sabrina Yang

After collecting $TSLA tweets from 07/12 - 07/19 (total 18019 tweets), I cut down to 10096 tweets after deleting duplicates rows/tweets.

## 1. Topic Modelings - NMF

Since tweets are considered as relatively short documents, I chose NMF as my method on analyzing the interpretable topic models. Here’s what I found:


- topic_0 : advertisement - promoting trading alert chatroom 
- topic_1 : FUD (Fear ,Uncertainty,  Doubt)  # insolvency = bankrupty   # crash, panic
- topic_2 : advertisement - stock app promotion
- topic_3 : advertisement - stock option trading investment advice
- topic_4:  how much Tesla made from bitcoin investment
- topic_5:  car, FSD Subscription  (ha = have: car ownership)
- topic_6:  # fintwit  # wallstreetbet # trends  # top stocks: aapl, spce(Virgin Galactic), mrna
- topic_7:  advertisement - daily alert
- topic_8:  advertisement - sign up 
- topic_9:  stock technical analysis and price charts  
- topic_10: advertisement - stock alert for discord
- topic_11: meme stock - influencers account trade ideas - promoting certain stocks - amc, gme
- topic_12: elon musk tweets activity, solarcity, cybertruck, trial, court  (Tesla bought Solarcity recently)
- topic_13: TSLA stock personal opinions and feelings
- topic_14: TSLA stock personal trading ideas - Short > Long ("Short" shows up more frequent than "Long", means the market is more bearish at that moment)

**What do the topics tell you about the overall structure of the data?**
-  some of topics are noises ( daily alert, promotions, advertisements) but some are useful 

    - elon musk's tweets
    - tech chart patterns
    - retail traders about tesla news



## 2. Sentiment Analysis Score - Vader


The reason I chose NLTK Vader for this part is because Vader has better sense to pick up social media sentiments than other packages. It comes as 4 scores: negative, neutral, positive and compound. For this case, I will focus on compound score to make a scatterplot based on daily average sentiment score.(why did I take compound score, not other scores to analyze? Since neutral tweets do not reflect a positive or negative mood and serve therefore no purpose to this analysis) 

- a. Daily Sentiment Compound Score 
<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/date_sentiment.png">

  
- b. Daily $TSLA price and Sentiment Compound Score
    - Can't see any significant correlation pattern but the sentiment did fall down when the stock price dropped for the first 2 days(7/12-7/14).
    - Sentiment climbed up and down repeatly from 7/15 to 7/19 even though the stock didn't recover during last week.
    - In the end of this observation timeframe, the sentiment hyper somehow boost the confidence of stock holders and we saw the price recovery on 7/20.
<img src="https://github.com/SYNYC/5_Project_Tweets_about_Tesla_Stock/blob/main/charts/date_stock_sentiment-two-scales.png">


**Next step:**
1. look into elon musk's tweets content

2. do more data cleaning on advertisement tweets to decrease the noises and redo the topic modeling to get clearer topics. 
   - _update_: cut down to 9712 tweets after this cleaning

3. do Kmeans clustering for topic-matrix df for topic purpose

4. Check other related tweets than my current keyword "$TSLA" search, for example, check "Tesla" tweets.

