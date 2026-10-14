Playback on the client side is a simple matter of installing a network-friendly media player, such as VLC. When your browser first encounters an unknown type (such as mp3 or m3u), it will ask for a suitable application to launch. If possible, you want to set this up so that each new song is queued in the media playlist, instead of launching a separate instance of the player. This is known as *enqueuing*.

Some browsers (such as Firefox) are often supplied with media plug-ins that take control of all media and attempt to play the media in the browser itself. This is generally undesirable, so try using the File Types menu option, you can remove this association and apply it manually.

An alternative package with similar scope is smb2www. As the name suggests, this provides access to all your Samba-related shares from across the Web. This has the advantage of being incredibly flexible and eliminates the need for specific symlinks to each folder you want to share but at the expense of opening a lot of your personal network to the outside world. Although I have this installed, I keep it switched off by default and switch it on (by entering through an SSH session) only when needed, that is, when I need to access a Windows machine that doesn’t allow remote connection. When your server is often under a heavy load, that is, when it's used as a media server, then smb2www has the benefit of not requiring a reboot after changing its configuration. The new configuration is available immediately after editing the file:

```
vi /etc/smb2www/smb2www.conf
```

or using the following:

```
dpkg-reconfigure smb2www
```

# SMS

The lowest common denominator in bidirectional wireless communication is undoubtedly the Short Message Service (SMS), or text message. This protocol exists as part of the mobile phone network infrastructure, making it zero cost for the provider and therefore low cost to the consumer, with many networks providing free text messages as part of their monthly package deals. Despite the rise of mobile Internet, the SMS remains a well-used protocol, especially among the young, for communication. To make use of SMS within your home, you can use one of two approaches to send and receive messages. The first and most obvious way is to perform all the processing with a secondary mobile phone connected to the computer. There is also the second method whereby a telecoms company provides you with a pseudomobile number that acts in same way as a physical phone, except you use it with an API rather than a keypad. In some cases this API is as simple as an SMTP gateway. In both cases, there are command-line tools to handle the telecoms data, so the method you choose comes down to financial preference.

> **Note** Some hardware devices will control power lines on receipt of a mobile phone call (like the GSM Remote Control Switch; see [www.gsm-auto.com](http://www.gsm-auto.com)), but their functionality is limited and often more expensive than the home-brew equivalent.

# Processing with a Phone

This is the quickest way to experiment with a SMS-controlled home because most people have (at least) one old phone at home or one from a partner that can be borrowed for testing. Even without an existing device, the cost of a simple pay-as-you-go device is not that great. You will also need a valid subscriber identity module (SIM) card and a connecting cable to your computer. A number of phone shops (and even supermarkets) sell SIM cards containing very low credit and are ideal starting points if you don’t have a second card of your own.