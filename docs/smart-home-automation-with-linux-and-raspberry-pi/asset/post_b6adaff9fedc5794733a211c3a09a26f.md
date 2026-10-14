
## Media Access

One common piece of functionality is to provide access to your music collection from outside home, such as from the office. Several Apache modules are available to handle this; one of them is mod_musicindex (http://freshmeat.net/projects/musicindex/, also available in the libapache2-mod-musicindex package). Although capable of being used to list general-purpose directories (as it does for its own online documentation), it is capable of rendering music-specific icons to let you download and/or stream this music anywhere in the world and create playlists interactively for the current folder and all the subdirectories underneath it.

To prepare an online portal for your music, first create a directory inside your web directory:

```bash
mkdir music
```

Then create an .htaccess file inside, granting permissions to whichever users you see fit. These permissions apply to this directory and every one underneath it, unless superseded by another .htaccess file. Because your music collection is likely to be stored outside of the web root, you must add a symlink to it.

```bash
ln -s /net/media/mp3 mp3
```

This also highlights the reason you created a separate media directory in the root—it eliminates the need for web-specific files polluting the directory structure of our nonweb media file hierarchy. You can then add the appropriate configuration lines to your virtual site configuration file, such as 001-homecontrol:

```apache
<Directory /var/www/sites/homecontrol/media>
    Options Indexes FollowSymLinks MultiViews
    MusicIndex On +Stream +Download +Search -Rss -Tarball
    MusicSortOrder filename album disc track artist title filetype
    MusicFields title artist album length bitrate
    MusicPageTitle Media Jukebox
    MusicDefaultCss musicindex.css
</Directory>
```

Then reload the Apache configuration in the usual way. This provides a functional but less than beautiful page, such as that shown in Figure 5-2.

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_191_0.png)

*Figure 5-2. An example of music index and your music being available anywhere*

Playback on the client side is a simple matter of installing a network-friendly media player, such as VLC. When your browser first encounters an unknown type (such as mp3 or m3u), it will ask for a suitable application to launch. If possible, you want to set this up so that each new song is queued in the media playlist, instead of launching a separate instance of the player. This is known as *enqueuing*.

Some browsers (such as Firefox) are often supplied with media plug-ins that take control of all media and attempt to play the media in the browser itself. This is generally undesirable, so try using the File Types menu option; you can remove this association and apply it manually.

An alternative package with similar scope is smb2www. As the name suggests, this provides access to all your Samba-related shares from across the Web. This has the advantage of being incredibly flexible and eliminates the need for specific symlinks to each folder you want to share but at the expense of opening a lot of your personal network to the outside world. Although I have this installed, I keep it switched off by default and switch it on (by entering through an SSH session) only when needed, that is, when I need to access a Windows machine that doesn’t allow remote connection. When your server is often under a heavy load, that is, when it's used as a media server, then smb2www has the benefit of not requiring a reboot after changing its configuration. The new configuration is available immediately after editing the file:

```
vi /etc/smb2www/smb2www.conf
```

or using the following:

```
dpkg-reconfigure smb2www
```

## SMS

The lowest common denominator in bidirectional wireless communication is undoubtedly the Short Message Service (SMS), or text message. This protocol exists as part of the mobile phone network infrastructure, making it zero cost for the provider and therefore low cost to the consumer, with many networks providing free text messages as part of their monthly package deals. Despite the rise of mobile Internet, the SMS remains a well-used protocol, especially among the young, for communication. To make use of SMS within your home, you can use one of two approaches to send and receive messages. The first and most obvious way is to perform all the processing with a secondary mobile phone connected to the computer. There is also the second method whereby a telecoms company provides you with a pseudo-mobile number that acts in the same way as a physical phone, except you use it with an API rather than a keypad. In some cases this API is as simple as an SMTP gateway. In both cases, there are command-line tools to handle the telecoms data, so the method you choose comes down to financial preference.

> **Note** Some hardware devices will control power lines on receipt of a mobile phone call (like the GSM Remote Control Switch; see [www.gsm-auto.com](http://www.gsm-auto.com)), but their functionality is limited and often more expensive than the home-brew equivalent.

### Processing with a Phone

This is the quickest way to experiment with a SMS-controlled home because most people have (at least) one old phone at home or one from a partner that can be borrowed for testing. Even without an existing device, the cost of a simple pay-as-you-go device is not that great. You will also need a valid subscriber identity module (SIM) card and a connecting cable to your computer. A number of phone shops (and even supermarkets) sell SIM cards containing very low credit and are ideal starting points if you don’t have a second card of your own.

Most mobile phone packages come in one of two varieties, each with particular merits in the HA field.

- Contract deals are cheap to begin with, because the cost of a (new) phone is subsidized but expensive to maintain. Unless you convert all your e-mail to text messages, it is unlikely you will ever make full use of the “free SMS for life” deals to make it worth the money you pay out every month on the subscription.
- Pay-as-you-go deals provide a comparatively cheap barrier to entry, as the bulk of the cost is up front; running costs are virtually nil. This is more true if you have a surplus phone from, say, a previous upgrade. The price of individual messages will be higher (than free!), but because most HA installations send very few messages, this is a worthwhile tradeoff. If your software goes haywire and issues too many messages, however, you will quickly exhaust your credit, causing further (and potentially more vital) communications to be lost.

> **Note** The quality or age of the phone isn’t important because it will be permanently plugged into a PC at home and unlikely to suffer the abuse of daily life.

The specific make of phone will depend on the software used. There are a couple of open source projects here, with most supporting the majority of functionality present on the Nokia devices, along with some Sony Ericsson handsets. Our basic requirements from a software point of view are that you should be able to send and receive messages to our phone. Access to the phone’s address book is useful but not necessary, as that can be better represented in software. It should also work as a command-line tool.

Gnokii ([www.gnokii.org](http://www.gnokii.org)) has been the leading software in this field for a while, and its technology has spawned several forks over the years. Its name represents the fact that the majority of supported devices are Nokia-based, although devices do work with a standard cable. (See [http://wiki.gnokii.org/index.php/Config](http://wiki.gnokii.org/index.php/Config) for a list of known good devices.) For others, you may have more luck using the Bluetooth driver.

The setup, provided you have a compatible phone, involves a simple configuration file such as the following:

```text
[global]
port = /dev/ttyACM0
model = AT
connection = serial
```

where the port can be determined by dmesg after plugging in your phone, although some others are chosen according to the make and model of your phone. (Determine this from the web site at [http://wiki.gnokii.org/index.php/Config](http://wiki.gnokii.org/index.php/Config).) Once it’s plugged in, you can issue the following to determine that the connection is working:

```text
gnokii --identify
```

Even though the phone might be able to communicate with Gnokii, the available functionality can vary. So, don’t make critical changes to your phone (such as writing data into the address book) without a suitable backup.

The easiest functionality to test and demonstrate is that of sending a text message. This is also the most widely supported.

```text
echo "This is a test message" | gnokii --sendsms myphonenumber
```
