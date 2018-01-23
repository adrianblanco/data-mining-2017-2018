# data-mining-2017-2018

https://apps.twitter.com/

```
install.packages("twitteR")
install.packages("httr")
library("twitteR")
library("httr")

install.packages(base64enc)
library("base64enc")

api_key <- "tysYZPggiK2cIgjTKtKMLbQ6n"
api_secret <- "fSdfE69Xpa20YnFscwuVvy8bsuMgAEtAk50T82DA2Alpb8ZJWO"
access_token <- "429399439-HdMCrSn8EEkuojbllsHf7hpNaPvr3SMsqYiC01be"
access_token_secret <- "3KONOi67BjViOKUyudEPgmP4gYb5mvdI39JsMXkSz5QdQ"
setup_twitter_oauth(api_key,api_secret,access_token,access_token_secret)

mariano_tweets <- userTimeline("marianorajoy", n = 200)
mariano_tweets

tweetsc.df <- twListToDF(mariano_tweets)

hashtag<-searchTwitter("#OTGala12", n=100, since='2018-01-23')
hashtag
```
