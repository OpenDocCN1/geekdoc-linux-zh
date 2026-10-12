# Projects

Code your own Twitter bot

# What you'll need...

+   - Internet connectivity
+   - Latest version of Raspbian
+   www.raspberrypi.org/ downloads

![](bbox=[0.05, 0.26, 0.28, 0.48])

# Code your own
Twitter bot

Create your very own Twitter bot that can retweet chunks of wisdom from others

Twitter is a useful way of sharing information with the world and it's our favourite method of giving our views quickly and conveniently. Many millions of people use the microblogging platform from their computers, mobile devices and possibly even have it on their televisions.

You don't need to keep pressing that retweet button, though. With a sprinkling of Python, you can have your Raspberry Pi do it for you. Here's how to create your own Twitter bot...

# Installing the
required software

**01** Log into the Raspbian system with the username *Pi* and the password *raspberry*. Get the latest package lists using the command `sudo apt-get update`. Then install the Python Package installer using `sudo apt-get install python-pip`.

Once you've done that, run `sudo pip install tweepy` to install the Twitter library we'll be using.

# Registering your 'app' with
Twitter

**02** We need to authenticate with Twitter using OAuth. Before this, you need to go to https://dev.twitter.com/apps and sign in with the account you'd like your Pi to tweet from. Click the 'Create a new application' button. We called our application 'LUD Pi Bot' and set the website to www.linuxuser.co.uk.

# Full code listing

```
```python
#!/usr/bin/env python2

# A Twitter Bot for the Raspberry Pi that retweets any content from
import sys
import time
from datetime import datetime
from tweepy import Tweepy

class bot:
    def __init__(self, c_key, c_secret, a_token, a_secret):
        # Create a Twython API instance
        self.api = Tweepy(c_key, c_secret, a_token, a_secret)

        # Make sure we are authenticated correctly
        try:
            self.api.verify_credentials()
        except:
            sys.exit("Authentication Failed")

        last_run = datetime.now()

    @staticmethod
```
```