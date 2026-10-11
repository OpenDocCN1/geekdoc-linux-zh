# # SMS

![](bbox=[0.07, 0.11, 0.93, 0.43])

# 03 **The dashboard**

Once registered and logged in, visit the dashboard page, which will display your AccountSid and your Auth Token. These are both required to use the Twilio REST. Keep these secure and private, but be sure to make a note of them as you will need them for your Python program later.

# 04 **Install the software**

Boot up your Raspberry Pi and connect it to the Internet. Before you install the Twilio software, it is worth updating and upgrading your Pi. In the LX Terminal, type `sudo apt-get update`, then `sudo apt-get upgrade`. Once complete, type `sudo easy_install twilio` or `sudo pip install twilio` to install the software. (If you need to install pip, type `sudo apt-get install python-pip` python-dev, press Enter, then type `sudo pip install -U pip`.)

# 05 **Twilio authentication**

Now you are ready to create the SMS program that will send the text message to your mobile phone. Open your Python editor and import the Twilio REST libraries (line one, below). Next, add your AccountSid and Auth Token, replacing the X with yours, as you will find on your dashboard:

```
```
from twilio.rest import TwilioRestClient
account_sid = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
# Enter Yours
auth_token = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
# Enter Yours
client = TwilioRestClient(account_sid, auth_token)
```
```

# 06 **Create your message**

You will probably want to be able to change your text messages rather than send the same one. Create a new variable in your program called *message*. This will prompt you to enter the phrase that you want to send to the mobile phone. When the program runs, this is the message that will be sent:

```
```
message = raw_input("Please enter your message")
```
```

# Twilio provides a wide range of API codes and reference documents to create other communication programs

# 07 **Add your numbers**

To send the message, you need to add the code line below and your two phone numbers. The first number is your mobile phone number, which is registered and validated with Twilio (Step 2). The second number is your Twilio account number, which can be retrieved from your dashboard page under ‘Call the Sandbox number’. Change the Sandbox number to your country location and remember to add the international country code.

> *Above You will be able to find your AccountSid and your Auth Token on the Twilio dashboard*

```
```
message = client.messages.
create(to="+44YOURNUMBER",
from_="+44YOUTWILIONUMBER", body=message)
```
```

# 08 **Send the message**

Now send your message. The code below is not required, but useful to indicate your message has been sent. Add the lines and save your program. Ensure your Raspberry Pi is connected to the Internet and that your mobile is on, then run your program. You have just texted from your Raspberry Pi!

```
```
print message.sid
print "Your message is being sent"
print "Check your phone!"
```
```

# 09 **Other API and codes**

Twilio provides a wide range of API codes and reference documents to create other communication programs, such as making phone calls, recording a call, and retrieving data including caller IDs and call duration. The API also complements a wide range of languages, including Ruby, PHP, Java and Node.js (twilio.com/api/).

# REST

REST stands for Representational State Transfer. (It is sometimes spelled “REST”), it relies on a stateless, client-server, cacheable communications protocol – and in virtually all cases, the HTTP protocol is used. REST is an architecture style for designing networked applications.