# Create a two-step authentication with Twilio

Increase security in access to your web services by building a simple two-step authentication with Twilio’s SMS APIs to help you

# Resources

+   - Python 2.7+
+   - Flask 0.10.0:
+     flask.pocoo.org/
+   - Flask Github:
+     github.com/mitsuhiko/flask
+   - A Twilio account:
+     twilio.com
+   - Twilio's Python REST API Helper Library:
+     github.com/twilio/twilio-python/zipball/master
+   - MySQLDB:
+     mysql-python.sourceforge.net

Telephony is one of the most versatile technologies in our households. Despite being invented over 100 years ago, we still use the same basic infrastructure that once only carried the voices of people to deliver a rich multitude of media content at incredible speeds. As is often the case with wonderful things, they can often be complex too – and yet phones are more important now to our daily lives than ever. So, what can we do to leverage some of that versatile technology? Well, for starters we can use an API. Twilio has created a RESTful API that removes a great deal of that complexity of telephony so that we can write apps and services that are able to deliver and receive both phone calls and SMS using various endpoints and services. Neat! In this tutorial, we’re going to look at using Twilio to help us create the basic flow for a two-step authentication system for logging into a service. We’re also going to be using Flask to help us create our routes and generate our pages, but little of Flask’s detail will be covered here.

# 01 Get a Twilio account and phone number

Signing up to Twilio is pretty easy. First, head over to http://twilio.com and click the ‘Signup’ button. At this point, the sign-up process doesn’t really differ from any other service, but after you’ve entered an email address and password you’ll be asked for a phone number. Given the nature of Twilio’s API, it makes sense for them to ask whether we’re human, and having them text us is a good way to confirm that. Hey, it’s a two-step authentication, which is exactly what we’re working towards. You can enter any number you have access to, be it a landline or mobile, to confirm who you are, but at this point we suggest you authenticate using a phone that can accept SMS (instead of a landline). Having entered your number, you’ll receive a text to authenticate your phone – enter it and you’ll be presented with a Twilio phone number. This is your Twilio phone number and you’ll be using it to send and receive our authentication texts.

![](bbox=[0.1, 0.7, 0.56, 0.9])

The Twilio interface is kept nice and simple – no unnecessary complications here

# 02 Add credit

Just like a mobile phone operator, Twilio is not a free service – although it is very inexpensive. In order to continue, we’ll need to add a card and some funds to our newly created Twilio account. On the main page of the dashboard, you’ll see a big blue dialog asking to upgrade your trial account; click through and follow the instructions to add a card and the amount of credit you would like to use. The minimum amount of $20 (around £10 GBP) will be more than plenty for this and other projects. Once that’s done, you’re almost ready to start sending text messages – but first head back over to the Twilio dashboard and copy your account SID and auth token down somewhere, you’ll need those a little later.