# Chapter 3 • DEPLOYING YOUR SYSTEMS

Over 100Mb Ethernet or Gigabit Ethernet, it is the fastest method of installation available.

# Using Install Images

Some administrators advocate the use of install images, which are images of an operating system installation that can be written directly to a disk. Install images offer a very fast way to copy an operating system to a new server and their use is common in Windows desktop environments. This isn't recommended for servers (Windows or Unix) due to the vastly different hardware and software requirements of each server. For each server configuration, you would have to maintain a separate install image that could be several gigabytes in size.

Automation is the greatest benefit of network installations. However, complete automation of this process may not be right for your site, depending on the level of customization you need. For example, if you are bringing in a consultant in a week to install an Oracle database and you are unaware of the space needed for the application and the data, you may want to hold off on setting up those files until the consultant arrives. But you can still perform other parts of the installation that do not affect Oracle.

If you run into these situations, you may want to consider creating a base configuration that acts as the common denominator, installing software and configurations that are common to all of your servers. From the base configuration, you can add software and make custom changes that are appropriate for each individual machine (such as installing Oracle on a database server).

If you have variation in your server hardware, most network installation systems will allow you to create custom configurations based on the hardware, IP address, and other characteristics of each server on which you are installing the operating system. For example, you could allocate 8GB to the / partition on a server with one 20GB disk, but only 4GB on a server with one 10GB disk. Both Jumpstart and Kickstart allow you to create custom configurations, as you will see in the following sections.

That said, network installations may not be for you. Organizations with very few servers may be better off using CD-ROMs, since there is no economy of scale achieved implementing this system for just three or four servers. Additionally, sites that do not acquire new hardware often will generally not install operating systems very often. The initial load involves too many machines for you and your staff to handle in a reasonable amount of time, it may not be the time and effort to set up the network installation infrastructure for a one-time use.

# Using Solaris Jumpstart

One of the most powerful installation packages is Jumpstart for Solaris. Jumpstart is particularly attractive because Sun's support for network booting in its firmware. After the support infrastructure is set up, you can install Solaris on a freshly loaded machine by plugging in a power cable, a network cable, and turning on the machine; no CD-ROM or other media is necessary.