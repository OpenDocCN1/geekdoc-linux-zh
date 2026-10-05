# Chapter 16 Network Hardware

WAPs are usually dedicated appliances that consist of one or more radios and some form of embedded network operating system, often a stripped-down version of Linux. A single WAP can provide a connection point for multiple clients, but not for an unlimited number of clients. A good rule of thumb is to serve no more than eight simultaneous clients from a single enterprise-grade WAP. Any device that communicates through a wireless standard supported by your WAPs can act as a client.

The common wireless standards used are IEEE 802.11g and 802.11n operates in the 2.4 GHz frequency band and provides LAN-like access to up to 54 Mb/s. Operating range varies from 100 meters to 400 kilometers, depending on equipment and terrain.

802.11n delivers up to 600 Mb/s of bandwidth and can use the 5 GHz frequency band and the 2.4 GHz band (though 5 GHz is recommended for deployment). Typical operating range is approximately double of 802.11g.

Today, 802.11g (and its grandfather, 802.11b) are commonplace. The transceivers are inexpensive and built into most laptops. Add-in cards are widely cheaply available for desktop PCs,

You can configure a Linux box to act as an a/b/ access point if you have the right hardware and driver. Since most PC-based wireless cards are still designed for Microsoft Windows, which may not come from the factory with Linux drivers.

An extent-alone 802.11b/g base station for the home or small office is Apple’s AirPort Express, a wall-like device that is expensive ($99) and highly functional.¹ Another option is to consider running a stripped version of Linux (such as OpenWRT) on a commercial WAS. Openwrt.org for information and a list of compatible hardware.

Literally dozens of vendors are having wireless access points. You can buy them at Home Depot and even at the grocery store. Predictably, the adage that "you pay for it" applies. Cheap access points (in the $50 range) are likely to perform poorly when handling large file transfers or more than one active client.

Debugging a wireless network is something of a black art. You must consider a range of variables when dealing with problems. If you are deploying a wireless network at an enterprise scale, you'll probably need to invest in a wireless network analyzer. We highly recommend the analysis products made by AirMagnet.

+   6. The 600 Mb/s bandwidth of 802.11n is largely theoretical. In practice, in the neighborhood of 400 Mb/s is a more realistic expectation for an optimized configuration. The environment and the capabilities and hardware of the client devices explain most of the difference between theoretical and real-life throughput. When it comes to wireless, your mileage may

+   7. In it, it will also connect to your stereo to play music wirelessly from your PC or laptop.