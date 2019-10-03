### Text Analytics Brainstorming

[Twitter Public Database](https://www.docnow.io/catalog/)  
[Where To Get Twitter Data For Academic Research](https://gwu-libraries.github.io/sfm-ui/posts/2017-09-14-twitter-data)
(It seems like a lot of available data is only for Tweet IDs, so we will need to use Tweepy in Python to manually look up all of them?)  
[7-zip for opening GZIP File Extensions](https://www.7-zip.org/)  
[Looking up Tweets manually by their IDs (without using an API)](https://www.bram.us/2017/11/22/accessing-a-tweet-using-only-its-id-and-without-the-twitter-api/)

1) mine all of Trump's tweets, see what his most commonly used words are, favorite subjects, etc.  
Could also see if his language patterns/preferred topics have changed over time. 

2) tweets directed *to* Trump.

3) [Notre Dame Cathedral Fire](https://digital.library.unt.edu/ark:/67531/metadc1477117/m1/)

4) ~~[Fake News Tweets](https://archive.org/details/fakenews-tweets)~~

#### Tweepy Code for Looking Up Tweets by their IDs ([stackoverflow thread](https://stackoverflow.com/questions/44581647/retrieving-a-list-of-tweets-using-tweet-id-in-tweepy))
```
import tweepy


def lookup_tweets(tweet_IDs, api):
    full_tweets = []
    tweet_count = len(tweet_IDs)
    try:
        for i in range((tweet_count / 100) + 1):
            # Catch the last group if it is less than 100 tweets
            end_loc = min((i + 1) * 100, tweet_count)
            full_tweets.extend(
                api.statuses_lookup(id=tweet_IDs[i * 100:end_loc])
            )
        return full_tweets
    except tweepy.TweepError:
        print 'Something went wrong, quitting...'

consumer_key = 'XXX'
consumer_secret = 'XXX'
access_token = 'XXX'
access_token_secret = 'XXX'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth, wait_on_rate_limit=True, wait_on_rate_limit_notify=True)

# do whatever it is to get por.TweetID - the list of all IDs to look up

results = lookup_tweets(por.TweetID, api)

for tweet in results:
    if tweet:
        print tweet.text
```
### Update | 10/2/19   
![Evidently,  you need to submit an application and be approved before using Twitter's API...](https://github.com/rjweisne/Fall2HW/blob/master/wait%20for%20twitter%20API.PNG)
