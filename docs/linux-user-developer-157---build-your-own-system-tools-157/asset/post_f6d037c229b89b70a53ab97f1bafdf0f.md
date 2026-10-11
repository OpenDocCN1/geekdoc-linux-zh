
## Access Twitter with Python

Twitter can be a great communication channel to enable your Raspberry Pi project to talk to the world.

![](img/e7f197876caa0b235fb5da2d16a578ea_77_0.png)

**Joey Bernard** is a true renaissance man, splitting his time between building furniture, helping researchers with scientific computing problems and writing Android apps.

### Why Python?

It's the official language of the Raspberry Pi. Read the docs at python.org/doc.

> In the previous issue, we looked at how to turn your Raspberry Pi into an RSS feed reader and how to enable your Raspberry Pi to post an RSS feed for others to read.

In this issue, we will continue along the same lines and look at how to add the ability to have your Raspberry Pi post tweets for the rest of the world to follow what is happening.

The first step is to find some way to talk to Twitter. Twitter provides a full API that defines how you can send and read tweets. We could work with raw sockets; manually form and send messages, then process the returned results.

However, this completely defeats the whole point of Python and the premise of code reuse. Instead, we will use the module python-twitter. There are several other options available too, in case you wish to look for a module that uses a different code style that better matches your own. They should all have the same functionality, so feel free to explore and experiment. For these examples, you can install the module with `pip install python-twitter`. This works fine for Python 2.x, but Python 3 support is something that is in progress, so you may need to pick a different module if you want to use Python 3.

If you need the latest features, you can always grab the source code from GitHub and build it.

Once you have the module installed, you can import it within your code with `import twitter`. The class `twitter.API` provides the main interface to enable you to interact with the Twitter API. When you create a new instance of the class, you need to provide your credentials in order to authenticate to Twitter and be allowed to work with your account. Twitter now uses OAuth as the main way to handle authentication, and this means that you need to generate an access token that your code can use to identify itself with Twitter. There is an entire section within its developer documentation that covers the steps required to get your token, located at goo.gl/99oAfA. The first step is that you need to register your code as an application that is authorised to talk with Twitter.

You handle this by going to apps.twitter.com and creating a new app. This gives you the consumer key and consumer secret that identifies your code as being permitted to connect to Twitter. The second step is to create an authentication token for your account that will tell Twitter that this app is authorised to connect to your account, read it and post to it. You should end up with two separate keys and secrets that you can now use to create an instance of the API class. The code looks like:

```python
import twitter
api = twitter.API(consumer_key="consumer_key",
                  consumer_secret="consumer_secret",
                  access_token="access_token",
                  access_token_secret="access_token_secret")
```

...where the relevant keys and secrets are the ones that you have generated above. You can check to see whether your credentials worked by calling the function `api.VerifyCredentials()`. This will either give you an error or give you a breakdown of the account information.

Once you have an authenticated connection to Twitter, your Raspberry Pi project can start to talk to the world at large. The most basic method is `PostUpdate()`. With this function, you can send in a status update message, with a maximum of 140 characters. If your message is longer than that, you can use the function `PostUpdates()`, which will post multiple status updates until the entire message is posted.

If you want to, you can include other details with the message. This includes options like your current longitude and latitude, or a place ID, to identify where a particular update came from. This might be handy on a mobile monitoring project of some kind where you want to know where a particular update came from. You can also post an update as a response to some other message, by including the `in_reply_to_status_id=` option in the function call.

If you don't want to use public status updates for your messages, you can use the function `PostDirectMessage()` to send a text message to a particular account. You can use either the `user_id` or the `screen_name` to identify the recipient of your direct message. While this is a bit more private than a public update, it is by no means secure, so don't send any compromising information using this method.

If you want to, you can also send multimedia files as Twitter updates. The function `PostMedia()` can take either a local file name or a HTTP URL to do a multimedia tweet. You can send image files like JPEG, GIF or PNG. You can also include an associated text message for the tweet, as well as location information if you want to geolocate the tweet and image.

Once you finish any of these posting functions, you get a status object returned that gives you details of your status. There are two dozen elements giving you items, such as whether it has been favourited, when it was created and the hashtags associated.

The Twitter API also enables you to read updates and direct messages from other users. This means that you can use this same communication channel to be able to send commands to your Raspberry Pi project.

The function `GetDirectMessages()` can get up to the last 20 direct messages sent to your Raspberry Pi's Twitter account. Luckily, you don't have to do this every time. You can use the option `since_id=x` to tell Twitter to only send those direct messages that are newer than message ID x.

If you are only interested in getting the last Y messages, you can instead use the option `count=Y`. This function returns a sequence of DirectMessage object instances. This structure contains the message ID, the creation date, recipient and sender information, as well as the actual message's text. This way, you can send commands within the text message so that your project can do different tasks after it has been deployed.

With the examples we have here, you should be able to have your project tweet what is going on out in the world.

### Managing interactions

![](img/e7f197876caa0b235fb5da2d16a578ea_78_0.png)

You might be interested in having more complex control over the Twitter account for your Raspberry Pi project. The Twitter Python module provides full access to the Twitter API, so you can make changes to the relationships between this account and other Twitter users.

- You can follow another user with the function `CreateFriendship()`.
- If you change your mind, you can always unfollow a user with the function `DestroyFriendship()`.

What might be of more interest, however, is to check out how many people are following you. Or, more specifically, how many people are following your Raspberry Pi project. You can get a sequence of Twitter users who are following your project with the function `GetFollowers()`. The default maximum number of returned followers is 200. So, if your project becomes really popular, you will need to use the function `GetFollowersPaged()` to get all of the followers in groups of 200. You can control pages returned with the option `cursor=X`. The defaults also return the statuses for all of these users, which you may not necessarily want to have to process. If so, you can use the option `skip_status=true`.

You can also get the number of times you’ve been friends with the function `GetFriends()`. In this case, the default number of results returned is 20. You can increase this with the option `count=X` up to a maximum of 200. If you have more than 200 friends, you can get paged results here too. You can control which page of results to return with the `cursor` option, just as above.

If you want to get a broader look at who is checking out your project, you can use the function `GetMentions()` to see who is mentioning the user account for your project. You get the last 20 mentions by default, but you can request up to 200.

Another measure of your reach into the public sphere is how many retweets you get. You can find out by using the function `GetRetweetsOfMe()`. The default number returned is 20, but you can ask for up to 100 of the latest retweets.

With these extra functions, you can actually have your Raspberry Pi project interacting with the world in general and monitor its own ability to communicate with the public. This might be handy for citizen science projects.

### Full code listing

```python
import twitter

# The first step is to connect to Twitter
api = twitter.Api(consumer_key='consumer_key',
                  consumer_secret='consumer_secret',
                  access_token='access_token',
                  access_token_secret='access_token_secret')

# You can post status updates
update_status = api.PostUpdate('I am now connected!')

# You can geotag updates with lat/long
update_status = api.PostUpdate('I am here: ', latitude=45.949874,
                               longitude=-66.642347)

# Posting images taken from your RP1
update_status = api.PostMedia('This is my picture', 'image1.png')

# Get the last 10 mentions and retweets
mentions = api.GetMentions(count=10)
retweets = api.GetRetweetsOfMe(count=10)

# Finding out how many followers you have
followers = api.GetFollowers()
follower_cnt = len(followers)
```

![](img/e7f197876caa0b235fb5da2d16a578ea_78_1.png)

*Above* Consider setting up a fresh Twitter account specifically for your project
