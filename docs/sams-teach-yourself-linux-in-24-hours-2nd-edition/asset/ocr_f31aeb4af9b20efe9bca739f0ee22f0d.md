# Installing and Configuring AOL Instant Messenger

AOL's Instant Messenger, or IM, is a fun and easy-to-use X11 client for chatting with friends over the Internet. The service is free, and you don't have to pay for the software. This client constantly checks and then instantly notifies you when a friend logs in the service. You can then send an instant message!

You have to first register at AOL's Web site and then download and install IM. Navigate to http://www.aol.com/aim/home.html. and sign up for the service by selecting a screen name and a password and entering your email address (you receive a confirmation message by email from AOL). Next, go to the download section, and select the Java version. It takes you about 20 minutes to download the five-megabyte file called aim_linux.sh (a self-extracting shell script).

After downloading, start the installation like this:

```
# sh aim_linux.sh
```

```
AOL Instant Messenger(TM) Registration Agreement
Your use of AOL Instant Messenger(TM) service ("Service") constitutes your acceptance, and agreement with America Online, Inc. ("AOL"), as follows: You represent and warrant that you are eighteen years or older. You understand and agree that your use of the Service does not constitute membership in the AOL service. You agree that you will not use the Service to publish, post, distribute or disseminate any defamatory, obscene, or other unlawful material or information. You further agree that you will not use the Service to transmit unsolicited commercial messages or use the Buddy Info screens to collect or harvest personal information about users of the Service to transmit unsolicited commercial messages. You will not decompile, reengineer or otherwise copy the Service.
...
```

After several screens of information, you're asked this question:

Do you accept the license? (y/n)

Type a y. The script then reports the following:

Uncompressing and Installing AOL Instant Messenger.

IM is installed in your home directory in a directory named aim. Start your PPP connection to your ISP, and then launch aim like this:

```
# aim/aim&
```