
## Create a two-step authentication with Twilio

Increase security in access to your web services by building a simple two-step authentication with Twilio’s SMS APIs to help you

## Resources

- Python 2.7+
- Flask 0.10.0:
  flask.pocoo.org/
- Flask Github:
  github.com/mitsuhiko/flask
- A Twilio account:
  twilio.com
- Twilio's Python REST API Helper Library:
  github.com/twilio/twilio-python/zipball/master
- MySQLDB:
  mysql-python.sourceforge.net

Telephony is one of the most versatile technologies in our households. Despite being invented over 100 years ago, we still use the same basic infrastructure that once only carried the voices of people to deliver a rich multitude of media content at incredible speeds. As is often the case with wonderful things, they can often be complex too – and yet phones are more important now to our daily lives than ever. So, what can we do to leverage some of that versatile technology? Well, for starters we can use an API. Twilio has created a RESTful API that removes a great deal of that complexity of telephony so that we can write apps and services that are able to deliver and receive both phone calls and SMS using various endpoints and services. Neat! In this tutorial, we’re going to look at using Twilio to help us create the basic flow for a two-step authentication system for logging into a service. We’re also going to be using Flask to help us create our routes and generate our pages, but little of Flask’s detail will be covered here.

## 01 Get a Twilio account and phone number

Signing up to Twilio is pretty easy. First, head over to http://twilio.com and click the ‘Signup’ button. At this point, the sign-up process doesn’t really differ from any other service, but after you’ve entered an email address and password you’ll be asked for a phone number. Given the nature of Twilio’s API, it makes sense for them to ask whether we’re human, and having them text us is a good way to confirm that. Hey, it’s a two-step authentication, which is exactly what we’re working towards. You can enter any number you have access to, be it a landline or mobile, to confirm who you are, but at this point we suggest you authenticate using a phone that can accept SMS (instead of a landline). Having entered your number, you’ll receive a text to authenticate your phone – enter it and you’ll be presented with a Twilio phone number. This is your Twilio phone number and you’ll be using it to send and receive our authentication texts.

![](img/3b256f430f51c98f1315671f6e4eec19_111_0.png)

The Twilio interface is kept nice and simple – no unnecessary complications here

## 02 Add credit

Just like a mobile phone operator, Twilio is not a free service – although it is very inexpensive. In order to continue, we’ll need to add a card and some funds to our newly created Twilio account. On the main page of the dashboard, you’ll see a big blue dialog asking to upgrade your trial account; click through and follow the instructions to add a card and the amount of credit you would like to use. The minimum amount of $20 (around £10 GBP) will be more than plenty for this and other projects. Once that’s done, you’re almost ready to start sending text messages – but first head back over to the Twilio dashboard and copy your account SID and auth token down somewhere, you’ll need those a little later.

## 03 Install the Twilio Helper Library and MySQLDB

The Twilio helper library is a fantastic piece of code that lets you jump straight into sending and handling text messages in no time at all. There are a couple of ways to install the library: you can use either PIP or Easy_Install, like so

```
$ pip install twilio
$ easy_install twilio
```

Or you can download the source code for the helper library and run the 'setup.py' file. It really is as simple as that. Now, for storing the verification tokens we're going to use a MySQL database. To get Python talking to our SQL server, we'll use the Python module MySQLdb, the package for which you can grab like so...

```
apt-get install python-mysqldb
```

In the tutorial resources we have included an SQL dump with the table structure. Import it into a database of your choosing. Assuming everything so far has gone swimmingly, you can create a new project folder/environment and add a new file 'server.py'.

## 04 Server setup

Open the 'server.py' file for editing. The first thing we're going to do is import the libraries we need for our authentication flow, create the endpoints for our server and assign some of the variables needed to run our Flask server. (Fig 01)

You may have noticed the account_sid and auth_token variable we've set after the import statements. We'll use these with our Twilio client so we can interact with Twilio and our mobile phones. These settings can be found on the Twilio account dashboard, right below the header. We've also connected to our SQL database, so make sure your SQL server is running before you fire up the app, otherwise you'll have an error thrown. Save, now if you run your 'server.py' file, you should be able to access the index page of your server at 127.0.0.1:5000/.

## 05 Server logic

If you've hit all of your server endpoints already, so far all you will see are the strings we returned at the end of endpoint declarations. These are not all that good-looking, so let's add some Flask templates to pretty things up a little. The focus of this tutorial is not on the intricacies of Flask and as such, included on the DVD is a folder called 'templates' and another called 'static'; copy them both to the root of your current project folder and amend

```
import MySQLdb
from flask import Flask, redirect, request, session, render_template
from twilio.rest import TwilioRestClient as twilio
import string, random, time

db = MySQLdb.connect(host="127.0.0.1", user="SQLUSER", password="SQLPASS", db="two-step", port=3306)

expirationLength = 300

account_sid = "YOUR ACCOUNT SID"
auth_token = "YOUR ACCOUNT AUTH TOKEN"
client = twilio(account_sid, auth_token)

@app.route('/')
def index():
    return "index page"

@app.route('/login', methods=['GET'])
def login():
    return "login page"

@app.route('/check-user', methods=['POST'])
def checkUser():
    return "check user page"

@app.route('/logout')
def logout():
    return "logout page"

@app.route('/verify', methods=['GET'])
def twoStep():
    return "verify page"

@app.route('/check-code', methods=['POST'])
def checkCode():
    return "check code page"

if __name__ == '__main__':
    app.secret_key = 'R4nDOMCRypt0gr4ph1cK3y0R6535S1ON'
    app.run(host='0.0.0.0', debug=True)
```

your endpoints as in Fig 02. If you revisit the pages again, things might seem a little out of whack at the moment, but don't worry about that for the time being. It's mostly because we've not put together the server logic to help the templates figure out what to do.

Let's deal with the '/' path first. All we're doing here is checking the state of our session cookies and effecting how the index.html page renders according to that state. If the user isn't logged in, we'll give them a link to the login page, if the user is logged in but hasn't verified, then we'll give them a link to the code verification page. Before we deliver the template we need to check that our session has its particular variables set, otherwise we'll end up getting KeyErrors.

```
@app.route('/')
def index():
    checkSessionState()
    return render_template('index.html')

def checkSessionState():
```
