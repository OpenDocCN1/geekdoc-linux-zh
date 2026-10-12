
# Send an SMS from your Raspberry Pi

Create a program that combines Twilio and simple Python code to enable you to send an SMS from your Pi to a mobile phone.

What you'll need...

- Raspberry Pi
- Twilio account

![](img/f11b7dbb71886af07ef87126037ebe98_73_0.png)

Text messaging, or SMS (Short Message Service), has become a staple of everyday communication. What began life as a 40 pence message service is now offered by most tariff providers as an unlimited service used worldwidely. Twilio, a cloud communications company, enables you to send SMS messages for free from your Raspberry Pi to a mobile phone using just six lines of code.

> “Create other communication programs, such as making phone calls, recording a call, and retrieving data”

![](img/f11b7dbb71886af07ef87126037ebe98_73_1.png)

### Set up your Twilio account

- The first step of this project is to register for a Twilio account and Twilio number. This is free and will enable you to send an SMS to a registered, verified phone. Once signed up, you will receive a verification code via SMS to the registered phone. When prompted, enter this onto the Twilio site to authenticate your account and phone. Go to twilio.com/try-twilio and create your account now.

### Register numbers

- Your Twilio account is just a trial account, unless you pay the upgrade fee, which means you can only send and receive communications from a validated phone number. Enter the phone number of the contact who you want to verify, ensuring that you select the correct country code. Twilio will send you a verification code and you will need to enter it into the website form and press submit.

### The dashboard

- Once registered and logged in on Twilio, visit the page, which will display your AccountSID and your Auth Token. These are both required to use the Twilio REST API. Keep these secure and private, but be sure to make a note of them as you will need them for your Python program later.

![](img/f11b7dbb71886af07ef87126037ebe98_74_0.png)

### Install the software

- Now boot up your Raspberry Pi and connect it to the internet. Before you install the Twilio software, it is worth updating and upgrading your Pi. In the LXDE Terminal, type `sudo apt-get update`, then `sudo apt-get upgrade`. Once complete, type `sudo easy_install twilio` or `sudo pip install twilio` to install the software. If you need to install pip, type `sudo apt-get install python-pip`, `python-dev`, press Enter, then type `sudo pip install -U pip`.

### Twilio authentication

- Now you are ready to create the SMS program that will send the text message to your mobile phone. Open your Python editor and import the Twilio REST libraries (line one, below). Next, add your AccountSID and Auth Token, replacing the X’s with yours, as you will find on your dashboard.

```python
from twilio.rest import TwilioRestClient

account_sid = "XXXXXXXXXXXXXXXX"
auth_token = "XXXXXXXXXXXXXXXX"
```

### Create your message

- You will probably want to be able to change your text messages rather than send the same one. Create a new variable in your program called `message`. This will prompt you to enter the phrase that you want to send to the mobile phone. When the program runs, this is the message that will be sent.

```python
message = raw_input("Please enter your message")
```

### Add your numbers

- To send the message, you need to add the code line below and your two phone numbers. The first number is your mobile phone number, which is registered and validated with Twilio (Step 2). The second number is your Twilio account number, which can be retrieved from your dashboard page under ‘Call the Sandbox’ number. Change the Sandbox number to your country location and remember to add the international country code.

```python
client = TwilioRestClient(account_sid, auth_token)
message = client.messages.create(to="4479XXXXXXXXXX", from_="444XXXXXXXXX", body=message)
```

### Send the message

- Now send your message. The code below is not required, but is useful to indicate your message has been sent. Add the lines and save your program. Ensure your Raspberry Pi is connected to the internet and that your mobile is on, then run your program. You have just texted from your Raspberry Pi!

```python
print message.sid
print "Your message is being sent" 
print "Check your phone" 
```

### Other APIs and codes

- You can also create other communication programs, such as making phone calls, recording a call, and texting data including caller IDs and call duration. The API has also completed a wide range of programming languages, including Ruby, PHP, Java and Node.js (twilio.com/api) to name a few.

# Make a Pi 2 HTPC

### What you’ll need…

- OpenELEC openelec.tv
- HDMI cable
- USB IR receiver
- IR remote
- Case
- Dedicated power supply
- Optional USB storage

> Finally create a more powerful and capable HTPC using the Raspberry Pi 2 and the excellent OpenELEC project.

We know people who just have a Raspberry Pi for XBMC, now called Kodi. It’s a great idea and a great use for the Pi – it works just well enough that you can easily play media locally or over the network. The biggest issue came with GUI response on the original Model Bs, and a lack of USB ports for connecting up everything that you want. While optimisation over the last few years has helped, the leap to Raspberry Pi 2 has basically solved all of these problems by giving you much more powerful hardware to play with. So if you’re looking to upgrade or finally take the plunge, this handy guide will help you create the perfect Raspberry Pi 2 HTPC.

![](img/f11b7dbb71886af07ef87126037ebe98_75_0.png)

### Choose the software

**01** In the past, Pi HTPCs were just a choice between RaspBMC and OpenELEC. However, RaspBMC is on a bit of a hiatus and OpenELEC is your best bet for getting the most up-to-date software. There’s not a massive difference between the two, as they both run XBMC.

### Get the software

**02** Head over to openelec.tv and look for the Download section. There’s a specific Raspberry Pi section which is split into original (ARMv6) and Pi 2 (ARMv7). Grab the image file from this page for the Pi 2.

### Install to card

**03** Open up the terminal and use `fdisk -l` to determine where your SD card is located on your system. Something like `/dev/sdb` or `/dev/mmcblk0` will be ideal. Navigate to the image using `cd` and install it with `dd` using:

```bash
$ dd bs=1M if=OpenELEC-RPi2-arm-5.0.5.img of=/dev/mmcblk0
```

### First boot

**04** Plug in your Raspberry Pi, either to your TV or to another screen just to begin with, and turn it on. OpenELEC will resize the SD card partitions and write a few extra programs before finally booting into Kodi.

### Configure Kodi

**05** Go through the basic wizard to get through the interface – if you are connecting via wireless you will need to go to OpenELEC in the System menu and activate the wireless receiver before selecting your network and then entering your password.

![](img/f11b7dbb71886af07ef87126037ebe98_76_0.png)

### Add network shares

**06** You can attach a portable hard drive or USB stick to the Pi for storage, but it is really to stream over the network. Go to File manager under System and Add source. Go to Browse and choose your network protocol to browse the network or alternatively, add it manually.

![](img/f11b7dbb71886af07ef87126037ebe98_76_1.png)

> “It’s a great use for the Pi – it works just well enough that you can easily play media locally or over the network”

![](img/f11b7dbb71886af07ef87126037ebe98_76_2.png)

### Case and placement

**07** Placement of your Raspberry Pi is important. As it’s going to be out all the time, we highly recommend getting a case for it – the Pibox cases from Pimoroni are quite well suited for this type of use as they are sturdy and can be attached to the rear of some TVs.

### IR sensors and controllers

**08** Kodi can be controlled with a number of different things – including USB game controllers and compatible IR sensors. We’ve used FLIRC in the past, but if you have your Pi behind the TV, you’ll need a sensor on a wire that can stretch to a useful position.

### Future updates

**09** OpenELEC has the excellent ability to update itself without needing you to reinstall it every few months, meaning you won’t need to do much maintenance at all. Now you can sit back and enjoy your media much easier than before.
