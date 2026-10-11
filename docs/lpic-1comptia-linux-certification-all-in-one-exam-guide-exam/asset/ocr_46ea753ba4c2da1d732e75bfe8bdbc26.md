I know this because I had it happen to me once. I configured my system to use a sync rate that was too fast for an older CRT monitor I was using. It worked OK for a couple of weeks. However, one evening my monitor started hissing, sparking, and smoking. I pushed it too fast for too long and burned it up. Always check your video board and monitor documentation to obtain the correct specs?

Before you begin, you should pull out your video board and monitor documentation and identify the following information:

+   • Who’s the manufacturer of the video board?
+   * What model number is the video board?
+   * How much memory is installed on the video board?
+   * What’s the board’s maximum resolution?
+   * What’s the board’s maximum color depth?
+   * What chipset is installed on the board?
+   * What’s the maximum horizontal and vertical sync rate supported by your monitor?

With this information in hand, you need to check the HCL for your distribution and make sure your video board and monitor are supported. Trust me, having this information in hand before you begin will save you a lot of trouble. Be warned, however, that you will find many times that never video boards are not listed in the HCL. Does this mean it’s not supported and won’t work? Maybe, maybe not. Here’s what you can do:

+   • See if an older driver will support your newer video board until a newer driver is released. Most X server implementations will include a set of generic drivers that will support most video boards at some level. It won’t look great, but you can at least get your system up and running.
+   * Check the video board manufacturer’s web site and see if they have released a driver for their board that isn’t included with your X server implementation.

Once you have this information gathered, you’re ready to start configuring your X server. This can be done in two ways:

+   * Editing the X configuration file
+   * Using an X configuration utility

Let’s look at the X configuration file first.

# ## Editing the X Configuration File

Just like everything else in Linux, your X configuration is stored in a text file in the /etc directory.

![](bbox=[0.16, 0.93, 0.28, 0.97])

**NOTE A good friend of mine coined an appropriate axiom: “Everything in Linux is a file.” All of your system and service configurations are stored in files. You even access hardware devices through a file.**