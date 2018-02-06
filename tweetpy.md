# data-mining-2017-2018

https://developer.twitter.com/en/docs/tweets/search/api-reference/get-search-tweets.html
https://www.digitalcitizen.life/command-prompt-how-use-basic-commands
https://apps.twitter.com/
http://tweepy.readthedocs.io/en/v3.5.0/

```
# c: cd 

#python

#python twitter.py

## pip install tweepy
## pip install csv
## pip install pandas

import tweepy
import csv
import pandas as pd

####input your credentials here
consumer_key = 'kX3iBW5z4QAJb93wzQix5j1rD'
consumer_secret = '9wn1t2aIG0MSmXhNkBF8pbjR9ll1zmJJ6xZqzaVa83H0f2Dvsw'
access_token = '429399439-zzGXG5XfwkymwQdstBr1F5CudAWlgIN4unYKTW2q'
access_token_secret = 'VUgDORB8IlL7Pq9ZBWTnISF4EcAdcs5t5aOwi347E9IqT'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth,wait_on_rate_limit=True)

# Open/Create a file to append data
csvFile = open('tweets.csv', 'a')

#Use csv Writer
csvWriter = csv.writer(csvFile)

for tweet in tweepy.Cursor(api.search,q="#OTFinal",count=1000,
                           lang="en",
                           since="2018-02-01").items():
    print (tweet.created_at, tweet.text)
    csvWriter.writerow([tweet.created_at, tweet.text.encode('utf-8')])

```
