
## Communicate securely

Use your phone in Incognito mode.

The key to securing your phone against any sort of surveillance is end-to-end encryption. There are an increasing number of apps and services that let you encrypt the data on your device before it is sent off and then decrypted at the recipient’s device. Encryption doesn’t prevent the caching of data but safeguards it against any kind of snooping by making it unintelligible to anyone without the correct decryption keys.

Begin your lockdown efforts by obfuscating your web browsing activities. Just like any desktop web browser, you can install a variety of add-ons to your Android browser.

Some of the popular Privacy-inducing add-ons are the Proxy-on add-on which you can use to customise the user-agent on the browser and hide the fact that you are on a mobile device.

Then there’s the self-destructing cookies add-on which will automatically delete all cookies when you close a site. For more comprehensive control you can use the CleanQuit add-on which removes all information about the previous session including the browsing & download history and site preferences.

If you want anonymity, you should switch to the Orweb browser (http://bit.ly/1eiYkJ) which is preconfigured to help you browse the web anonymously. It’s also loaded with plugins to disguise your device, gives you control over cookies, prevents loading of Flash content and keeps no browsing history. It requires the Orbot plugin, and Orbot is Tor for Android. (See p34 for more details about the Tor Project). On initial launch, Orbot runs through a quick setup wizard. If you have a rooted phone, you can turn on transparent proxying, which allows all network apps to automatically run through the Tor network.

To sign and encrypt email messages on your mobile device you need the Android Privacy Guard (APG) app, which is an open source implementation of OpenPGP. You’ll also need the K-9 email app, which integrates seamlessly with APG.

To use these apps, first launch K-9 and configure it to connect to your email server. Then launch APG and tap the menu button, which brings up the option to manage private keys and public keys. You can export these keys from the desktop and import them into APG. Once the keys are imported, K-9 will display the option to sign and encrypt messages when you write a new email. Conversely it will let you decrypt emails when you receive a new encrypted message.

Similarly, if you wish to encrypt instant messages, you’ll need the open source ChatSecure app. The app uses the OTR protocol to enable secure chat sessions over XMPP accounts. Using the app you can have secure chats with your friends over popular networks including Google Talk and Facebook on any OTR compatible client including Pidgin, Adium, and Jitsi.

## Old School usage

Another famed form of text-based communication is SMS. Although on a steady decline due to the falling prices of mobile internet many people still use texting as their primary means of communication.

You can encrypt SMS messages with the open source TextSecure app, which can encrypt SMS stored locally on the phone. However, to send encrypted messages over the air, the recipient must also have TextSecure or they’ll receive unencrypted messages. When you run the app first time, it gives you the option to create encrypted versions of all local messages. Although it doesn’t touch the existing unencrypted SMS, it’s advisable to delete them after creating encrypted versions.

Before you can send messages you’ll have to create a secure connection with the recipient’s device by exchanging keys. TextSecure will send a message to the recipient, whose TextSecure app will automatically respond with a message to establish a secure connection. From then on you send and receive encrypted messages. Surprisingly, a lot of us still use the smartphone to make actual calls and there are apps and services that will establish secure channels to thwart any attempts to intercept your conversation.

> “Surprisingly, a lot of us still use the smartphone to make actual calls.”

You can use the free RedPhone app, which makes encrypted calls over the internet.

There’s also SilentPhone, which is developed by Phil Zimmerman who gave us OpenPGP for securing email and ZRTP protocol for securing VoIP calls. The SilentPhone app works on multiple mobile platforms but comes with a $10 (about £6) subscription fee.

Both these solutions work as advertised and create encrypted calls. However, their major limitation is that they require the person at the other end of the line to be using the same app. The Ostel project is working on solving this problem. They’ve created a standard known as Open Source Telephony Network (OSTN) that uses free and open source protocols to create end-to-end encrypted voice communication channels.

The best thing about this is that you can connect with any user that’s using an app that supports the OSTN standard. There’s the CSipSimple app for Android, Acrobits for iPhone users, PrivateGSM for BlackBerry users and the cross-platform Jitsi desktop app for Linux, Windows and Mac users.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_31_0.png)

You can use the Jitsi app for making encrypted video calls.

## Choose volume location

- Local
- Dropbox
- External SD
- Google Drive

The EncDroid Android app lets you create EncFS encrypted folders and syncs them.
