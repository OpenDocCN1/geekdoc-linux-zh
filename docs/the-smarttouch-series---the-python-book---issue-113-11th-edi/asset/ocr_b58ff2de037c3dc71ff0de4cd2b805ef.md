# Creating dynamic templates
with Flask, Jinja2 and Twitter

Create a dynamic webpage with Twitter and Flask’s rendering engine, Jinja2

# Resources

+   - Python 2.7+
- Flask 0.10.0: flask.pocco.org
- Flask GitHub: github.com/mitsuhiko/flask
- A Twitter account
- Your favourite text editor
- Code downloaded from FileSilo

![](bbox=[0.37, 0.345, 0.9, 0.57])

The template uses a loop to generate a list of Twitter tweets

Python and Flask are a great combination when you’re looking to handle the Twitter OAuth process and build requests to obtain tokens. We’ve used Twitter here because of the large amount of easily digestible data available on it. However, since Twitter adheres to the standards set out by OAuth 1.0, the code we’ve used to sign and build requests can be modified to work with any third-party API using the same standard without a great deal of work. For years PHP has been a mainstay of template generation, but now with well-documented frameworks such as Flask, Sinatra and Handlebars, the ability to use powerful scripting languages greatly improves our ability to make great web services. Here, we’re going to use Python, Flask and its templating engine to display tweets. Flask comes with the super-nifty Jinja2 templating engine, If you’re familiar with Node.js or front-end JavaScript, the syntax will look very similar to the Handlebars rendering engine.

But, before we dive into that, we need to organise some of the example code that we’re using for this.

# 01 Rearranging our code

Server code can get messy and unmaintainable quickly, so the first thing we’re going to do is move our helper functions to another file and import them into our project, much like you would a module. This way, it will be clear which functions are our server logic and endpoints and which are generic Python functions. Open the TwitterAuthentication file downloaded from FileSilo (stored under Twitter OAuth files) and locate the getParameters, sign_request and create_oauth_headers functions. Cut and paste them into a new file called helpers.py in the root of your project folder. At the top of this file we want to import some libraries.

```
import urllib, collections, hmac, binascii, time, random, string

from hashlib import sha1
```

Now we can head back over to server.py and import the helper functions back into our project. We do this by simply calling import helpers. Because Python is smart, it will look in the current directory for a helpers.py file before it looks for a system module. Now every function included in helpers.py is accessible to our project. All we need to do is call them as prepped our the methods we called before with helper.function_name and it will execute. For sign_request, we’ll need to pass our oauth_secret and consumer_secret for each request rather than accessing it from the session. Adjust the function declaration like so:

```
def sign_request(parameters, method,
baseURL, consumer_secret, oauth_
secret):
```

# 02 server.py modules

With a lot of the modules needed in this project having been moved to helpers.py, we can now remove most of them from server.py. If we amend our first import statement to be...

```
import urllib2, time, random, json
```

...our project will continue to function as it did