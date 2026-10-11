# Make a Python Twitter client

Create a simple Twitter client to make and monitor tweets

![](bbox=[0.79, 0.095, 0.92, 0.125])

![](bbox=[0.06, 0.16, 0.6, 0.36])

# 01 Accountability

To create a Twitter app, you need a Twitter account. Sign into your account, or create a separate one if you want to split up personal and development accounts on the service. Once that's done, go to dev.twitter.com and log in using your desired account.

![](bbox=[0.07, 0.445, 0.33, 0.55])

![](bbox=[0.37, 0.385, 0.62, 0.48])

# 02 New beginnings

Go to 'My applications' and click 'Create a new application'. Here you'll need to enter the app's name, a short description and a website where more details about yourself and/or the app can be found. Names of apps are not allowed to use the word Twitter in them.

![](bbox=[0.07, 0.645, 0.33, 0.8])

# 03 Privileges

After this has been created, you'll be brought to the details page of the app. Before we go any further, click on Settings and select Read, Write and Access Direct Messages under Application Type so that we can use it properly as a Twitter client.

# 04 Access token

We can now create an access token for the application to work with your Twitter account. Go back to the details once the read and write permissions have been changed, and scroll down to the bottom. Click 'Create my access token' to retrieve it.

# 05 Install Pip

We'll install the latest version of python-twitter from our website. To do this, first install pip, as we're using Python, available in repos as python-pip. As we're using Debian, this looks like:

```
$ sudo apt-get install python-pip
```

...which allows us to set up Python modules.

![](bbox=[0.37, 0.66, 0.63, 0.79])

# 06 Install Twython

Now that we have Pip installed, we can go ahead and install Twython. To do this, continue in your terminal and put:

```
$ sudo pip install twython
```

This will get the Twython module, and all the OAuth packages you need to log into your account with tokens we created.

![](bbox=[0.66, 0.385, 0.94, 0.48])

> We need to create a Python file to hold all our authentication details. Start by importing Twython

# 07 Authentication file

We need to create a Python file to hold all our authentication details. Start up IDLE, or a text editor of your choice, and start by importing Twython with:

```
from twython import Twython
```

Make sure you have the keys we created earlier handy to add in the next parts. If the output is long, type it to go to the next screen.

![](bbox=[0.66, 0.625, 0.94, 0.735])

# 08 App keys

Add the following to your code:

```
APP_KEY = 'YOUR_CONSUMER_KEY'
APP_SECRET = 'YOUR_CONSUMER_SECRET'
...replacing YOUR_APP_KEY and YOUR_APP_SECRET with your own consumer key and consumer secret respectively.
```