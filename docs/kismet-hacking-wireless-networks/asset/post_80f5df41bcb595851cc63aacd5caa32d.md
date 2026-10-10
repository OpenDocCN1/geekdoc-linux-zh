
## Note

This setting also allows you to set the channels for your regulatory domain. By default, it is set up for the North American regulator domain, which is for channels 1–11, but not all users are in the North American regulatory domain and can use more or less channels. This is also where you can hack things a bit. If your card supports all 14 channels, or more than your regulatory domain allows, you can specify all the possible channels, even the ones not technically allowed in your regulatory domain. Check your local laws before doing this, however.

Since we are not transmitting in Kismet, it shouldn’t be a problem (check your local laws) to listen to see if someone has set up a rogue AP on channels not normally used or allowed, to try and avoid detection. Please don’t abuse this as the regulations are there for a reason.

```
# Combo cards like Atheros use both 'a' and 'b/g' channels. Of course, you
# can also explicitly override a given source. You can use the script
# extras/listchan.pl to extract all the channels your card supports.
defaultchannels=IEEE80211ab1:1,6,11,2,7,3,8,4,9,5,10,36,40,44,48,52,56,60,64
```

You can also specify channels to be covered by a/b/g combo cards if you happen to have one. The *listchan.pl* script in the extras directory of the install package will poll your card(s) to see what channels are supported. A useful thing to see if your card is capable of more than you thought it was.

```
# Fine-tuning channel hopping control:
# The sourcechannels option can be used to set the channel hopping for
# specific interfaces, and to control what interfaces share a list of
# channels for split hopping. This can also be used to easily lock
# one card on a single channel while hopping with other cards.
# Any card without a sourcechannel definition will use the standard hopping
# list.
#
sourcechannels=sourcename(,sourcename):ch1,ch2,ch3,...,chN
#
# ie, for us channels on the source ‘prism2source’ (same as normal channel
# hopping behavior):
# sourcechannels=prism2source:1,6,11,2,7,3,8,4,9,5,10
```

This parameter is where you can fine-tune the channel hopping. In the *defaultchannels* parameter, we specified what channels were available; now we can specify which ones we specifically want to listen on and what order to sequence through.

## Notes from the Underground

### Hack

There is a very cool hack possible here. For b/g networks, channels 1, 6, and 11 are statistically the most popular since they don't overlap. If we have one card, it makes no sense to spend only 8/11th's of our time on channels less likely to have something on them. You can specify channels more than once and the sequence will loop back to the beginning when done. So if you specify channels 1, 6, and 11 more than once, you'll end up spending more time there overall and even out your distribution of channels.

```
sourcechannels=prism2source:1,6,11,2,7,1,6,11,3,8,1,6,11,4,9,1,6,11,5,10
```

With the above line we are spending 6/10th's of our time checking the most popular channels. You can tweak this distribution to your liking, but it has been tested and tends to work for high-speed scanning such as highway speed wardriving. You can also specify additional channels such as 12–14 if your card supports it and add those to the mix.

You can do the same for 802.11a channels. Either adding them to the mix of b/g channels if you have an a/b/g card or just the 802.11a channels if you have a single mode card.

```
# Given two capture sources, "prism2a" and "prism2b", we want prism2a to stay
# on channel 6 and prism2b to hop normally. By not setting a sourcechannels
# line for prism2b, it will use the standard hopping.
# sourcechannels=prism2a:6
```

If you don't specify a sourcechannels parameter and channelhop=true, the system will automatically hop through the default channels. If you have multiple sources, you can have a specific sourcechannels for one device and have it monitor a few specific channels, while the other one checks the remainder. This is effective with wardriving. One source spends all it's time checking 1, 6, and 11 where there are most likely going to be signals, and the other can check the remaining channels.

You can also use this to break up the workload across multiple sources. One card can do the lower channels, the other the higher channels, and be able to sequence through everything much faster than a single card.

![](img/d6ac176c353d2b7687c1186a140180a1_131_0.png)

![](img/d6ac176c353d2b7687c1186a140180a1_131_1.png)

```
# To assign the same custom hop channel to multiple sources, or to split the
# same custom hop channel over two sources (if splitchannels is true), list
# them all on the same sourcechannels line:
# sourcechannels=prism2a,prism2b,prism2c;1,6,11
```

You can also nest multiple sources in an assigned *sourcechannel*. If *channelsplit=true*, Kismet will cycle through the channels, and make sure that no two sources are on the same channel at the same time, maximizing the time spent on high-usage channels, and making sure not to overlap scanned channels. In the config file example, three sources would cycle through each of three channels without overlapping.

```
# Port to serve GUI data
tcpport=2501
```

Here you can specify what TCP port the server will serve clients on. There should be no real reason to change this setting. If you feel the need to change this, make sure to make the appropriate change in the *kismet_ui.conf* file.

```
# People allowed to connect, comma separated IP addresses or network/mask
# blocks. Netmasks can be expressed as dotted quad (/255.255.255.0) or as
# numbers (/24)
allowedhosts=127.0.0.1
```

This is where remote monitoring can be set up. By default, for security reasons, only the host running the server can connect a client (localhost). If you want to use the Kismet client on another system and connect to a remote server, you need to specify the network address of the host that will be connecting to the server. This is accomplished by appending it to the existing line with a comma and no space.
`allowedhosts=127.0.0.1,192.168.0.34,10.0.50.45`

You can also specify valid netblocks; *allowedhosts=127.0.0.1,192.168.0.0/24* or *allowedhosts=127.0.0.1,192.168.0.0/255.255.255.0* will allow the entire 192.168.0.x netblock to connect.

It is best to limit what hosts can connect. If you’re monitoring your corporate network and you let anyone connect, you could end up giving access to your data dumps to an attacker, since Kismet does not do any authentication beyond this.

```
# Address to bind to. Should be an address already configured already on
# this host, reverts to INADDR_ANY if specified incorrectly.
bindaddress=127.0.0.1
```

The Kismet server can be bound to specific addresses on a multi-homed system. By default, Kismet will bind to all addresses configured and listen on all interfaces. If you want to limit it to only one address, specify it here.

```
# Maximum number of concurrent GUI's
maxclients=5
```

This specifies exactly what it says; the maximum number of clients that can connect to a server. The more clients, the more work the server has to do, so it’s best not to allow too many or run too many.

```
# Do we have a GPS?
gps=true
```

This is a pretty self-explanatory parameter. If you want to use a GPS, you need to set this to true in order to use it. If it’s set to false, you can save a little memory on really slim systems.

```
# Host:port that GPSD is running on. This can be localhost OR remote!
gpshost=localhost:2947
```

Kismet uses GPSD for getting GPS coordinates into Kismet and in turn into your logs. GPSD interfaces with your serial/Universal Serial Bus (USB) port and takes the incoming NMEA data and puts it out over a TCP port. Kismet connects to that port and puts the data into the server.

Specify where GPSD is running and on what port. Most configurations have GPSD running on the same system as `kismet_server`, so it would be set to “`gpshost=localhost:2947`” or “`gpshost=127.0.0.1:2947`” depending on if name resolution is working or not.

> **Note**
> 
> If for some reason you have GPSD on another machine on the same network as the `kismet_server` and GPSD is available on it, you can specify that system’s address instead. Note: If you get your GPS data from a source other than one attached to the system running `kismet_server`, then all your locations will seem to be from the location at the remote system, skewing your results. This is also true if you are running remote drones. If your GPS location is not at the location of your sensor, then your GPS data will not be correct.
