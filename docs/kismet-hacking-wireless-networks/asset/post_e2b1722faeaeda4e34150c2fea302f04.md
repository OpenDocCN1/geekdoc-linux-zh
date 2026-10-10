
you can take your time, since drones are typically stationary and we don’t have to worry about velocity making detection a problem.

```
# By setting the dwell time for channel hopping we override the channelvelocity
# setting above and dwell on each channel for the given number of seconds.
#channeldwell=10
```

This setting overrides the channel velocity setting and specifies that, rather than a certain number of channels per second, Kismet should spend a certain amount of time on each channel. This is a more useful setting for static installations and drones. This way you can thoroughly inspect each channel. It’s up to you to determine which works for you to make the most of your time and coverage. Increments of 1 second can be adjusted.

```
# Do we split channels between cards on the same spectrum? This means if
# multiple 802.11b capture sources are defined, they will be offset to cover
# the most possible spectrum at a given time. This also controls splitting
# fine-tuned sourcechannels lines which cover multiple interfaces (see below)
#splitchannels=true
```

Channel splitting enables Kismet to cover more spectrum at any given time when multiple sources are in use. If you have two cards, both hopping, Kismet will make sure that they are both always on different channels at any given time. If card 1 is on channel 5, card 2 is on a channel other than 5, maximizing the covered spectrum. This is especially useful for situations of several cards where having all of them on one channel makes little or no sense. If you are using several drones or other situations where you need blanket coverage of a channel across several locations, consider disabling this.

```
# Basic channel hopping control:
# These define the channels the cards hop through for various frequency ranges
# supported by Kismet. More finegrain control is available via the
# "sourcechannels" configuration option.
# Don't change the IEEE80211<x> identifiers or channel hopping won't work.
# Users outside the US might want to use this list:
# defaultchannels=IEEE80211b:1,7,13,2,8,3,14,9,4,10,5,11,6,12
```

```
defaultchannels=IEEE80211b:1,6,11,2,7,3,8,4,9,5,10
# 802.11g uses the same channels as 802.11b...
```

```
defaultchannels=IEEE80211g:1,6,11,2,7,3,8,4,9,5,10
# 802.11a channels are non-overlapping so sequential is fine. You may want to
# adjust the list depending on the channels your card actually supports.
# defaultchannels=IEEE80211a:36,40,44,48,52,56,60,64,100,104,108,112,116,120,124,
128,132,136,140,149,153,157,161,184,188,192,196,200,204,208,212,216
defaultchannels=IEEE80211a:36,40,44,48,52,56,60,64
```

Here you can specify what channels, by default, the drone should hop through. More fine control is available in the *sourcechannels=* line later on; we are just specifying the channels that are possible here.

This setting also allows you to set the channels for your regulatory domain. By default, it is set up for the North American regulator domain, which is for channels 1–11, but not all users are in the North American regulatory domain and can use more or less channels. This is also where you can hack things a bit. If your card supports all 14 channels, or more than your regulatory domain allows, you can specify all the possible channels, even the ones not technically allowed in your regulatory domain. Check your local laws before doing this, however.

Since we are not transmitting in Kismet, it shouldn't be a problem (check your local laws) to listen to see if someone has set up a rogue access point on channels not normally used or allowed, to try and avoid detection. Please don't abuse this as the regulations are there for a reason.

```
# Combo cards like Atheros use both 'a' and 'b/g' channels. Of course, you
# can also explicitly override a given source. You can use the script
# extras/listchan.pl to extract all the channels your card supports.
defaultchannels=IEEE80211ab:1,6,11,2,7,3,8,4,9,5,10,36,40,44,48,52,56,60,64
```

You can also specify channels to be covered by *a/b/g* combo cards if you happen to have one. The *listchan.pl* script in the extras directory of the install package will poll your card(s) to see what channels are supported. A useful thing to see if your card is capable of more than you thought it was.

```
# Fine-tuning channel hopping control:
# The sourcechannels option can be used to set the channel hopping for
# specific interfaces, and to control what interfaces share a list of
# channels for split hopping. This can also be used to easily lock
# one card on a single channel while hopping with other cards.
# Any card without a sourcechannel definition will use the standard hopping
# list.
# sourcechannels=sourcename[,sourcename]:ch1,ch2,ch3,...chN
# ie, for us channels on the source `prism2source' (same as normal channel
# hopping behavior):
# sourcechannels=prism2source:1,6,11,2,7,3,8,4,9,5,10
```

This parameter is where you can fine-tune the channel hopping. In the *default-channels* parameter, we specified what channels were available. Now we can specify which ones we specifically want to listen on and what order to sequence through.

### Note

There is a very cool hack possible here. For b/g networks, channels 1, 6, and 11 are statistically the most popular since they don't overlap. If we have one card, it makes no sense to spend only 8/11th's of our time on channels less likely to have something on them. You can specify channels more than once and the sequence will loop back to the beginning when done. So if you specify 1, 6, and 11 more than once, you'll end up spending more time there overall and even out your distribution of time/channels.

```
sourcechannels=prism2source:1,6,11,2,7,1,6,11,3,8,1,6,11,4,9,1,6,11,5,10
```

With the above line we are spending 6/10th's of our time checking the most popular channels. You can tweak this distribution to your liking, but it has been tested and tends to work for high speed scanning such as highway speed war-driving. You can also specify additional channels such as 12-14 if your card supports it and add those to the mix.

You can do the same for 802.11a channels. Either adding them to the mix of b/g channels if you have an a/b/g card or just the 802.11a channels if you have a single mode card.

![](img/d6ac176c353d2b7687c1186a140180a1_223_0.png)

```
# Given two capture sources, "prism2a" and "prism2b", we want prism2a to stay
# on channel 6 and prism2b to hop normally. By not setting a sourcechannels
# line for prism2b, it will use the standard hopping.
# sourcechannels=prism2a:6
```

If you don't specify a *sourcechannels* parameter and *channelhop=true*, the system will automatically hop through the default channels. If you have multiple sources, you can have a specific *sourcechannels* for one device and have it monitor a few specific channels while the other one checks the remainder. This is effective with wardriving. One source spends all it's time checking 1, 6, and 11 where there are most likely going to be signals, and the other can check the remaining channels.
You can also use this to break up the workload across multiple sources. One card can do the lower channels, the other the higher channels, and be able to sequence through everything much faster than a single card.

```
# To assign the same custom hop channel to multiple sources, or to split the
# same custom hop channel over two sources (if splitchannels is true), list
# them all on the same sourcechannels line:
# sourcechannels=prism2a,prism2b,prism2c:1,6,11
```

You can also nest multiple sources in an assigned *sourcechannel*. If *channelsplit=true*, Kismet will cycle through the channels, and make sure that no two sources are on the same channel at the same time, maximizing the time spent on high-usage channels, and making sure not to overlap scanned channels. In the config file example, three sources would cycle through each of three channels without overlapping.

Like the server and client, you can specify command-line switches for the drone that override the options in the *kismet_drone.conf* file.

- `-I, --initial-channel <n:c>` Initial channel to monitor on (default: 6)
    Format capname:channel

This switch sets what channel the enabled sources should start on. If channel hopping is disabled, this will be the channel that is monitored.

- `-x, --force-channel-hop` Forcibly enable the channel hopper

If channel hopping is disabled in the config file, -x (lower case x) will force it to be enabled.

- `-X, --force-no-channel-hop` Forcibly disable the channel hopper
