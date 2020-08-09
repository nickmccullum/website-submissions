# Building a Twitter Bot in Python with Tweepy

Have you ever imagined having an automated assistant to respond to tweets, and even post different tweets that are useful, fun, and even exciting for your followers to see? That is exactly what we will be covering in this tutorial today. Although this might seem like a difficult task at the beginning, once you get started with it, you will know how easy and intuitive it is.

Let’s get started.

 ## What is Tweepy
    

In the simplest terms, Tweepy is a library for the Python language for accessing the application programming interface (API) provided by Twitter. Being such a simple and great tool to use, Tweepy allows easy integration of Twitter tools through the official API in your programs. Tweepy can be easily used to create bots and tools to automate as well as prompt everything you manually do on Twitter.

Applications of this can be used for both fun activities and very illegitimate activities such as spamming and harassing people. Since Twitter does not let any illegitimate acts slide easily, if one is planning to engage in anything illicit, it might come with lots of unpleasant consequences. Therefore, one should be extremely thoughtful about what you are about to do with the knowledge that you gain today from this tutorial. It should solely be used for research and non-harmful purposes and we are not liable for any legal consequences or damages that might arise from any unlawful practices or applications.

Let’s go ahead and install Tweepy using pip.

`pip install tweepy`

  

Once it is installed, open up a new Jupyter Notebook or a script and see if Tweepy imports without any issues.

`import tweepy`

  

If it works fine, you are good to go. Let’s now look at the rest of the requirements the preparation of this tutorial needs to fulfill.

## Requirements
    

In this Tweepy tutorial, it is not just sufficient to have the Tweepy library installed and simply code and get a Twitter bot to run. We need access to an active Twitter account with the developer mode enabled. We will directly be working on this real-time without the use of any sandboxes. We require the Twitter developer account to create the credentials such as both consumer key and secret as well as both the access token and access token secret for us.

Twitter developer account gives access to the Twitter API which opens up application layer and transport layer endpoints to perform various tasks such as tweeting, favoriting, retweeting, liking, direct messaging, and even things like finding what is trending and all. If you were to build a program from the scratch, you would have to go through all the trouble of writing codes to deal with all the low-level functionalities such as encoding and decoding your data, configuring requests, configuring authentication, configuring timeouts just to use the above endpoints Twitter provides. This is what we are alleviating by using Tweepy and focusing solely on the bot we are developing instead.

Having a Twitter account does not necessarily give access to a developer account and we are required to explicitly apply for a developer account. Even when we apply, sometimes it takes days for our account to be approved. Therefore, as the most immediate task is to get the Twitter developer account set, let’s get to it.

## Setting Up Twitter Developer Account
    

Let’s first login to Twitter with your existing account or if you do not have one, create a new one. Make sure that you verify it with a mobile number as well since this is essential in the next step. Now, let’s visit [https://developer.twitter.com/](https://developer.twitter.com/) and apply for a developer account. The process is pretty intuitive and therefore, you should not have any issue with it.

  

![](https://lh6.googleusercontent.com/-DpTFIgVknXBE2iy9BzTwNeX5l76oUQt7aexHX_HSH6HM6amLxgRvcVNUvYrpUkjKb5-1OBu0Gp_J1_9ad5H58rsvJVW6qWspGCVBSyyCWU4sj7BIVacC0f_Ze2pXNKkuXBP4go)

  

You will be prompted with questions such as why are you using this and what are you planning to do with it, mentioning your genuine intentions. You can say that you are intending to build a bot as a learning exercise and therefore, you need the developer account.

![](https://lh6.googleusercontent.com/FmnbJ7JL0tsMXR5pc7hKrn1N19mCckIRuuz8HkzPuAzGlM4l6VJx_SlIC9BSmKgiOuZ-oB_t0sci27-kvM8Xo9RUGMw4INCPQM-bfhdhzjqbdx2Fx1v0m5korMTjlk1Ms3btIAQ)

  

![](https://lh6.googleusercontent.com/TZrlU2T3NGglsCK5IWPdN8WC6xNfF5WlCd0ZKoqG-1feo7SQ0zfauhHMsgs2ucTE3hGpEo2AvPZdM7UfVO4fLmUOIirFH_nPdRYbW7e-eXeqlCXsZQ2tlcrDos8B9a0_z4ooHNY)

  

Once you have applied for the developer account, it will take one or two days for it to be approved (worst case, might take around a week). We urge you to keep reading this whether or not you have the account as it will allow you to get a better grip on everything that we do here. So, let’s continue with the tutorial.

The Twitter API exposes these endpoints after providing authentication with OAuth, the most popular open protocol for authentication. Once we have our Twitter developer account accepted, we are to configure the authentication details.

Let’s navigate to the ‘Apps’ option from the top menu bar and then click ‘Create An App’. Provide the details and then finally click ‘Create’. The process is pretty intuitive, so you should be alright. Once it’s done, go to ‘Permissions’ and see whether your new app has both reading as well as writing permissions. If it seems like it does not, go ahead, edit it, and get permission for both reading and writing. Next, navigate to ‘Keys and Tokens’ and get your credentials. Copy the consumer key, consumer secret, access token, and access token secret. Consumer key is also known as the API key and if your account says that instead, do not worry about it.

It should also be kept in mind that certain rate limits have been imposed by the Twitter API about how often you are able to use those HTTPS endpoints within your app. Therefore, this should always be considered when designing and developing your next Twitter bot or Twitter app.

Before we do some coding, let us now use the credentials we stored earlier and see if we can connect to the Twitter endpoints. Open your favorite Python IDE (even Notepad or Gedit would do) and test the connectivity.
```python
import tweepy
API_KEY = ‘Paste your api/consumer key here’
API_SECRET = ‘Paste your api/consumer secret here’
ACCESS_TOKEN = ‘paste your access token here’
ACCESS_TOKEN_SECRET = ‘paste your access token secret here’
auth = tweepy.OAuthHandler( API_KEY, API_SECRET )
auth.set_access_token( ACCESS_KEY, ACCESS_TOKEN_SECRET )
twitter_api = tweepy.API( auth )
print( twitter_api.verify_credentials() )
```
  

In the above code, set the API_KEY, API_SECRET, ACCESS_TOKEN, and ACCESS_TOKEN_SECRET to the codes you generated and copied earlier. If this executes well without any errors and prints true, you are good to go.

Let’s now get ourselves familiar with the jargon of Tweepy and Twitter.

## Tweepy: Jargon
    

It is our understanding that what Tweepy really does is provide a medium to easily access Twitter API endpoints by encapsulating the low-level functions and adding high-level and relevant functionalities on top. Tweepy has been evolving alongside Twitter’s new updates. However, the vocabulary and the jargon is still what it used to be when Tweepy started. For instance, now what is called a tweet on Twitter used to be status. Tweepy still used that term even today. In Tweepy, there are ‘friendships’. This is the equivalent term for followers on Twitter. Moreover, what we call likes on Twitter are called favorites on Tweepy. There are a few more but for now, these would be sufficient and as you practice with Tweepy more, you will get accustomed to the jargon of Tweepy.

Let us now get the bigger picture of Tweepy and see what kind of functionalities it offers.

## Tweepy: Functionalities
    

There are five main functionalities Tweepy facilitates. We will talk about them one by one.

-   #### OAuth Handling
    

We already have an idea about what OAuth is. Tweepy has the class OAuthHandler to deal with the underlying mechanics of the OAuth. We can create OAuthHandler objects and use it for API calls. For instance, in a previous section, we have created an OAuthHandler object called auth with the API key and API secret we generated.

-   #### API
    

There is an API class in Tweepy that facilitates accessing the available HTTPS endpoints in the Twitter APi. In the previous code, we have created a twitter_api object using the OAuthHandler we created and verified the credentials we generated. API class also offers functions to perform tasks such related to user timelines, followers, tweets, accounts, blocking users, trends, streaming to name a few. We will later go over these one by one when we are coding.

-   #### Models
    

There are model classes in Tweepy to conveniently use the responses from the https endpoints to our benefit. These responses are inherently being encapsulated by the Tweepy model classes and therefore, we only have to worry about the functionality of the intended task instead of low-level functions. There are model classes such as user, friendship, status, and searchresults. We will look at these later as well.

-   #### Cursors
    

Almost all the time, Twitter https endpoints return results by a sequence of assigned numbers of pages. This is where the Tweepy cursor comes in. It nicely makes the whole process of traversing and fetching items far easier. There is a cursor class in Tweepy to facilitate this task.

-   #### Streams
    

Streams in Tweepy are used for the task of acquiring much larger volumes of data such as tweets. It nicely handles the session creation, authentication, connection, as well as the closing. We can also use streaming to watch for tweets in real-time matching specific guidelines or criteria.

Now that we know about both the jargon and the functionalities of Tweepy, we are ready to roll with the codes.

## Tweepy: The Twitter Bot
    

There is no proper and methodical way to learn Tweepy. You just have to get on with it and learn what you can do with it. Therefore, we will learn it by following common use cases and examples. Make sure that you always have the code from the earlier section and configured the variables, keys, and secrets. Let’s start.

-   #### Say Hi to all your followers
    
```python
my_followers = twitter_api.followers()
for user in my_followers:
	twitter_api.update_status('Hi @' + user.screen_name)
	time.sleep(5000)
```
  

Let’s go over the codes line by line. What we’re doing here is acquiring the followers of my account using the twitter_api object. We are saving it to a my_followers object and in the next line, we are iterating through it and updating our status (which means we are tweeting) with a five second time interval. We are doing this in order to avoid getting banned due to accessing the endpoints without a break.

Almost forgot, congratulations! You just made your first bot.

-   #### Get Tweets on Your Timeline
    
```python
my_timeline = twitter_api.home_timeline( count = 10 )
for tweet in my_timeline:
	print( tweet.user.name + 'tweeted' + tweet.text )
```
  

What we are doing here is getting the timeline from my account for looping through it to get the most 10 recent tweets.

-   #### Get User Details
    
```python
some_user = twitter_api.get_user( "elonmusk" )
print( some_user.name )
print( some_user.description )
print( some_user.location )
```
  
  

If we know the username, we can use the get_user function from the API class to get their details. If we want to view their followers, it can be done as follows.
```python
for follower in some_user.followers():
	print( follower.name )
```
  

-   #### Update Profile Description
    
```python
twitter_api.update_profile(description="I am a bot")
```

  

The API class also provides functions to update your personal details easily from your Python code.

-   #### Liking Tweets
    
```python
my_timeline = twitter_api.home_timeline()
tweet = my_timeline[0]
twitter_api.create_favorite( tweet.id )
```
  

We can get the first tweet of our timeline and then like it by using the create_favorite function provided by the API class.

-   #### Blocking Users
    

`twitter_api.create_block( twitterusername )`

  

We can easily block someone by using the above function.

-   #### Get Blocked List
    
```python
for blocked_user in twitter_api.blocks():
	print(blocked_user.name)
```
  

This will print all the users we have blocked on Twitter from our account.

-   #### Search for Tweets
    
```python
for tweet in twitter_api.search( q="Space", lang="en", rpp=5 ):
	print( tweet.user.name + 'said' + tweet.text )
```
  

In this, we are searching for the 5 most recent tweets that contain the word Space. This does go beyond your list of followers and acquire publicly shared tweets as well.

-   #### Get Name Mentions on Tweets
    
```python
mentioned_tweets = twitter_api.mentions_timeline()
for tweet in mentioned_ tweets:
	print( tweet.user.name + 'said' + tweet.text )
```
  

What we are doing here is getting the tweets that our username has been mentioned.

## Conclusion
    

In this tutorial, we acquired good foundation knowledge on how to interact Twitter with a bot. Not only this takes your presence on Twitter to the next level but also ensures that your followers are always entertained and hooked with your account. It can be used for a range of things like automated tweeting as well as for analytics.

We used Tweepy to realize this on a higher-level allowing ourselves to focus on the actual code instead of the infrastructure. We also did a few examples to get ourselves familiar with Tweepy and more functions can be found on [the official documentation](https://tweepy.readthedocs.io/). Feel free to play around and keep practicing. However, keep it in mind not to use this for any illicit activities or to spam users. You may be banned from Twitter but the legal consequence could stretch way more than that.
