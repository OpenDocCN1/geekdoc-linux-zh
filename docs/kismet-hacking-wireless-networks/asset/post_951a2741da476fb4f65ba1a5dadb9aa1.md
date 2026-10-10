
## TIP

For one reason or another, some people have had trouble running Kismet with the most recent version of *GPSD*. To fix some of those problems, a Kismet and Netstumbler forums user named Dutch, released an older, scaled down version of *GPSD*, appropriately titled *gpsdold*. Those who have used this version (including this author) have reported no problems. Dutch’s version of *gpsdold* can be found at http://www.netstumbler.org/158973-post-1600.html. Download and install to /usr/bin, and then use in the same way you’d use *GPSD*.

## Wardriving with Kismet

If you’ve made it this far, congratulate yourself: you’ve downloaded BackTrack, burned it to a CD, booted up the live distro, and properly configured Kismet to work with your particular wireless card and GPS receiver. Now it’s time to go wardriving.

### Tools & Traps...

### Optional but Useful Items for Your Wardriving Setup

In addition to your current setup, if your wireless card supports it, you may want to consider an external antenna. A simple 5 dBi omni-directional antenna designed for 2.4 GHz will significantly aid in the discovery of networks (an external antenna outside the car is eminently preferable to an internal antenna inside a wireless card sitting inside a metal car!). Most antennas will also require a pigtail, which is a short adapter cable that connects the antenna coaxial cable to the antenna jack on your wireless card. For special cases, you may want to consider a cantenna or other form of directional antenna. The folks at http://wardrivingworld.com and http://www.fab-corp.com are highly respected among wardrivers and will go out of their way to ensure you get the right equipment for your setup.

An additional consideration, especially for longer drives, is a power inverter. This device (which typically costs about $25–30) will plug into your cigarette lighter (or other vehicle power socket) and convert the vehicle’s DC power to AC for your laptop.

## Wardriving

We said that it was time to begin wardriving, but there are a few important tips to consider before you start (see also “Notes from the Underground”):

- Be sure that your wardriving setup does not physically impair your ability to drive, or block your line of sight. This may seem like common sense, but the more complex your wardriving setup, the more potential exists for exotic things that could get in your way of seeing. Don’t let antennas, cables, or the laptop itself prevent you from being a responsible driver.

- Once you start Kismet and configure everything to run (see Figure 10.6), close your laptop lid. Again, this is a matter of common sense, because an open laptop is an invitation for distraction. Closing the lid removes the invitation to constantly peek at the screen. And believe me, if the screen is open, you’ll peek at it.

![](img/d6ac176c353d2b7687c1186a140180a1_250_0.png)

- Law enforcement officers will tell you that many more people talk themselves into tickets than the other way around. Should you be stopped by law enforcement, it is not necessary to fabricate some far-fetched story about what you're doing, or make false claims about the secret project you're working on and how they don't have a need to know. Wardriving is legal, so telling the truth is the easiest and simplest explanation.

## Notes from the Underground...

## RenderMan's Stumbler Ethics

1. Do Not Connect! At no time should you ever connect to any APs that are not your own. Disable client managers and Transmission Control Protocol (TCP)/Internet Protocol (IP) stacks to be sure. Simply associating can be interpreted as computer trespass by law enforcement.

2. Obey traffic laws. It's your community too, and the traffic laws are there for everyone's safety including your own. Doing doughnuts at 3:00 A.M. gets unwanted attention from the authorities anyways.

3. Obey private property and no-trespassing signs. Don't trespass in order to scan an area. That's what the directional antenna is for. You wouldn't want people trespassing on your property would you?

4. Don't use your data for personal gain. Share the data with like-minded people, show it to people who can change things for the better, use it for education, but don't try and make any money or status off your data. It's just wrong to expect these people to reward you for pointing out their own stupidity.

5. Be like the hiker motto of "take only pictures, leave only footprints." Detecting SSIDs and moving on is legal; anything else is irresponsible to yourself and your community.

6. Speak intelligently to others. When telling others about wardriving and wireless security, don't get sensationalistic. Horror stories and FUD are not very helpful to the acceptance of wardrivers. Speak factually and carefully. Point out problems, but also point out solutions.

7. If/when speaking to media, remember you are representing the community. Your words reflect on the rest of us. Do not do anything illegal no matter how much they ask. They may get pissed off, but at least you have demonstrated the integrity that this hobby requires. http://www.renderlab.net/projects/wardrive/ethics.html

## Tools & Traps...

## GPS Location Data

Users are often confused about the GPS data that Kismet provides. A common question is: how does Kismet geo-locate an access point? Or, Are the GPS coordinates the actual location of the access point? While Kismet does take a number of signal readings at different locations, the real answer to the question is that it doesn't actually geo-locate anything; and the GPS coordinates are not the actual location of the AP.

The GPS receiver marks your location when you detect an AP. So while you're driving down the street and detect an AP in a house off the street, Kismet sees the AP as being in the street at the location where you were when you detected the AP (a quick look at street level maps at WiGLE.net will confirm this). When Kismet has more than one set of GPS coordinates, the displayed location is the set of coordinates where Kismet reported the strongest signal. In an ideal world, this would seem to provide you with a fairly accurate "abeam" location: as you detect an AP, the signal will be weak, and growing stronger until you pass abeam the AP, and then becoming weaker again until it is no longer detected. However, the harsh reality of obstructions and multi-path reflection will tend to skew these results. Still, all things considered, Kismet does a pretty darn good job.

Before you shut down your laptop, remember to save your log files to a USB thumb drive (or other external source) if you didn’t already run Kismet from it. Remember, when running a live CD, the log files are saved to a temporary RAM disk, which will not be saved when you power off your laptop.

## Managing Your Results

You’ve returned home from your first wardrive, and have collected hundreds (or perhaps even thousands) of networks. Now, what exactly are you going to do with this data? Hopefully, as we explained in the previous section, you had an objective in mind. If you were wardriving as part of a penetration test, you might want to parse out only those networks in the vicinity of your target location. Or, you might be interested in compiling statistics on the networks you collected: channel usage, encryption, and so forth. Either way, consider uploading your data to WiGLE.net.

### WiGLE

WiGLE.net (Wireless Geographic Logging Engine) is an online database that holds in excess of 15 million logged wireless networks, most with geographic coordinates. WiGLE gives you access to Service Set Identifier (SSID) and manufacturer statistics, octet and channel usage statistics, and a browsable Web map of the world. By creating an account, you can upload and track your logged networks, and be credited with networks that you found first.

### Obtaining BackTrack

- You can download directly or via torrent from http://www.remote-exploit.org/backtrack_download.html.
- Be sure to check the MD5 hash to ensure your download is free from tampering or errors.
- Burn the BackTrack ISO at slower speeds (4x–8x) for better results.

### Configuring Kismet

- Be sure to use a supported card (see http://www.kismetwireless.net/documentation.shtml for details).
