

```python
# Dependencies
%matplotlib inline
import tweepy
import json
import pandas as pd
import time
import numpy as np
from datetime import datetime
import matplotlib.pyplot as plt
import seaborn as sns


# Import and Initialize Sentiment Analyzer
from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer
analyzer = SentimentIntensityAnalyzer()

# Twitter API Keys
consumer_key = "JMK1jCxlewvpZm7KuNOKdBOx1"
consumer_secret = "5BL3WwK5iu7SAioFy8mZbDzJN8AQeyjtPxKRfhlz5xZ7fgP6fQ"
access_token = "201086971-yqXToCo50DaFkBpJHJfxoZ6yiZDn8FiMb0x657WH"
access_token_secret = "c5y47MU7xRqWhDWJ03XJyoJBqJnEuDm28K6sboL59D5VM"

# Setup Tweepy API Authentication
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth, parser=tweepy.parsers.JSONParser())

# Target User Accounts
news_sources = ["BBCWorld", "CBSNews", "CNN", "FoxNews", "NYT"]
```


```python
tweet_data = {
    "tweet_source": [],
    "tweet_text": [],
    "tweet_date": [],
    "tweet_vader_score": [],
    "tweet_neg_score": [],
    "tweet_pos_score": [],
    "tweet_neu_score": []
}

# Loop through each user
for news_agency in news_sources:

    # Loop through 5 pages of tweets (total 100 tweets)
    for x in range(5):

        # Get all tweets from home feed
        public_tweets = api.user_timeline(news_agency, page=x)

        # Loop through all tweets
        for tweet in public_tweets:

            # Run Vader Analysis on each tweet
            ps = analyzer.polarity_scores(tweet['text'])
            compound = ps["compound"]
            pos = ps['pos']
            neu = ps['neu']
            neg = ps['neg']
            # source
            # text
            # date
            #compound = analyzer.polarity_scores(tweet["text"])["compound"]
            #pos = analyzer.polarity_scores(tweet["text"])["pos"]
           # neu = analyzer.polarity_scores(tweet["text"])["neu"]
           # neg = analyzer.polarity_scores(tweet["text"])["neg"]

            # Add each value to the appropriate array
            #tweet_text
            
            #tweet_date
            
            #tweet_vader_score
            #tweet_neg_score
            #tweet_pos_score
            #tweet_neu_score
            tweet_data["tweet_vader_score"].append(compound)
            tweet_data["tweet_pos_score"].append(pos)
            tweet_data["tweet_neu_score"].append(neu)
            tweet_data["tweet_neg_score"].append(neg)
            
             # All data is grabbed from the JSON returned by Twitter
            tweet_data["tweet_source"].append(tweet["user"]["name"])
            tweet_data["tweet_text"].append(tweet["text"])
            tweet_data["tweet_date"].append(tweet["created_at"])
 

```


```python
# turn tweet dictionary into dataframe based on the keys
tweet_df = pd.DataFrame(tweet_data, columns=["tweet_source", 
                                             "tweet_text", 
                                             "tweet_date",
                                             "tweet_vader_score",
                                             "tweet_pos_score",
                                             "tweet_neu_score",
                                             "tweet_neg_score"])
tweet_df.head()


# Export to CSV
tweet_df.to_csv('Data.csv', header = True, index = False)
#file_name = str(time.strftime("%m-%d-%y")) + "-tweets.csv"
#tweet_df.to_csv("analysis/" + file_name, encoding="utf-8")


```


```python
# for the tweet_date column, turn the dates into datetime using pd.to_datetime(date_string)
tweet_df["tweet_date"] = pd.to_datetime(tweet_df["tweet_date"])

# sort the dataframe by date
tweet_df.sort_values("tweet_date", inplace=True)
tweet_df.reset_index(drop=True, inplace=True)
```


```python
# create a scatter plot of sentiment (see solutions)

# Build scatter plot for tracking tweet polarity by tweet history
# Note how a few data munging tricks were used to obtain (-100 -> 0 tick marks)
plt.scatter(np.arange(-len(tweet_df[tweet_df["tweet_source"] == "BBC News (World)"]), 0, 1), 
            tweet_df[tweet_df["tweet_source"] == "BBC News (World)"]["tweet_vader_score"],
            edgecolor="black", linewidths=1, marker="o", color="skyblue", s=75,
            alpha=0.8, label="BBC")

plt.scatter(np.arange(-len(tweet_df[tweet_df["tweet_source"] == "CBS News"]), 0, 1), 
            tweet_df[tweet_df["tweet_source"] == "CBS News"]["tweet_vader_score"],
            edgecolor="black", linewidths=1, marker="o", color="green", s=75,
            alpha=0.8, label="CBS")

plt.scatter(np.arange(-len(tweet_df[tweet_df["tweet_source"] == "CNN"]), 0, 1), 
            tweet_df[tweet_df["tweet_source"] == "CNN"]["tweet_vader_score"],
            edgecolor="black", linewidths=1, marker="o", color="red", s=75,
            alpha=0.8, label="CNN")

plt.scatter(np.arange(-len(tweet_df[tweet_df["tweet_source"] == "Fox News"]), 0, 1), 
            tweet_df[tweet_df["tweet_source"] == "Fox News"]["tweet_vader_score"],
            edgecolor="black", linewidths=1, marker="o", color="b", s=75,
            alpha=0.8, label="Fox")

plt.scatter(np.arange(-len(tweet_df[tweet_df["tweet_source"] == "The New York Times"]), 0, 1), 
            tweet_df[tweet_df["tweet_source"] == "The New York Times"]["tweet_vader_score"],
            edgecolor="black", linewidths=1, marker="o", color="gold", s=75,
            alpha=0.8, label="New York Times")

# Incorporate the other graph properties
plt.title("Sentiment Analysis of Media Tweets (%s)" % time.strftime("%x"))
plt.ylabel("Tweet Polarity")
plt.xlabel("Tweets Ago")
plt.xlim([-105, 5])
plt.xticks([-100, -80, -60, -40, -20, 0], [100, 80, 60, 40, 20, 0])
plt.ylim([-1.05, 1.05])
plt.grid(True)

# Create a legend
lgnd = plt.legend(fontsize="small", mode="Expanded", 
                  numpoints=1, scatterpoints=1, 
                  loc="upper left", bbox_to_anchor=(1,1), title="Media Sources", 
                  labelspacing=0.5)



# Show plot
plt.show()
```


![png](output_4_0.png)



```python
# group the sources by sentiment from teh tweet dataframe
# Average all polarities by news source
tweet_df_polarity = tweet_df.groupby(["tweet_source"]).mean()["tweet_vader_score"]

# View the polarities
pd.DataFrame(tweet_df_polarity)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_vader_score</th>
    </tr>
    <tr>
      <th>tweet_source</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BBC News (World)</th>
      <td>-0.069848</td>
    </tr>
    <tr>
      <th>CBS News</th>
      <td>-0.064404</td>
    </tr>
    <tr>
      <th>CNN</th>
      <td>-0.034501</td>
    </tr>
    <tr>
      <th>Fox News</th>
      <td>0.010526</td>
    </tr>
    <tr>
      <th>NYT</th>
      <td>0.013152</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Store all polarities in a tuple
# plt.bar(np.arange(-len(tweet_df[tweet_df["tweet_source"] == "BBC News (World)"]), 0, 1), 
#             tweet_df[tweet_df["tweet_source"] == "BBC News (World)"]["tweet_vader_score"],
#             edgecolor="black", width=1, marker="o", color="skyblue", s=75,
#             alpha=0.8, label="BBC")
```


```python
# Store all polarities in a tuple
tweets_polarity = (tweet_df_polarity["BBC News (World)"], 
                    tweet_df_polarity["CBS News"], 
                    tweet_df_polarity["CNN"], 
                    tweet_df_polarity["Fox News"],
                    tweet_df_polarity["NYT"])

```


```python
tweets_polarity
```




    (-0.069848, -0.064404, -0.034501, 0.010526000000000002, 0.013152000000000006)




```python
# Generate bars for each news source
fig, ax = plt.subplots()
ind = np.arange(len(tweets_polarity))  

width = 1
rect1 = ax.bar(ind[0], tweets_polarity[0], width, color="skyblue")
rect2 = ax.bar(ind[1], tweets_polarity[1], width, color="green")
rect3 = ax.bar(ind[2], tweets_polarity[2], width, color="red")
rect4 = ax.bar(ind[3], tweets_polarity[3], width, color='blue')
rect5 = ax.bar(ind[4], tweets_polarity[4], width, color='gold')

autolabelneg(rect1)
autolabelneg(rect2)
autolabelneg(rect3)
autolabelpos(rect4)
autolabelpos(rect5)

# Orient widths, add labels, tick marks, etc. 
ax.set_ylabel("Tweet Polarity")
ax.set_title("Overall Media Sentiment based on Twitter (%s) " % (time.strftime("%x")))
ax.set_xticks(ind + 0.5)
ax.set_xticklabels(("BBC", "CBS", "CNN", "Fox", "NYT"))
ax.set_autoscaley_on(True)
ax.grid(False)


# Generate labels for each news source
def autolabelpos(rects):
    # attach some text labels
    for rect in rects:
        height = rect.get_height()
        ax.text(rect.get_x() + rect.get_width()/2., 1*height,
                '+%.2f' % float(height),
                ha='center', va='bottom')

def autolabelneg(rects):
    # attach some text labels
    for rect in rects:
        height = rect.get_height()
        ax.text(rect.get_x() + rect.get_width()/2., -1*height-0.015,
                '-%.2f' % float(height),
                ha='center', va='bottom')
        
        
plt.show()
```


![png](output_9_0.png)



```python
# Generate labels for each news source
def autolabelpos(rects):
    # attach some text labels
    for rect in rects:
        height = rect.get_height()
        ax.text(rect.get_x() + rect.get_width()/2., 1*height,
                '+%.2f' % float(height),
                ha='center', va='bottom')

def autolabelneg(rects):
    # attach some text labels
    for rect in rects:
        height = rect.get_height()
        ax.text(rect.get_x() + rect.get_width()/2., -1*height-0.015,
                '-%.2f' % float(height),
                ha='center', va='bottom')
```


```python

        

```
