# The Legality of Wardriving

According to the Federal Bureau of Investigation (FBI), it is not illegal to scan access points; however, once a theft of service, a denial of service (DoS), or a theft of information occurs, it becomes a federal violation through 18USC 1030 (www.usdoj.gov/criminal/cybercrime/1030_new.html). While this is good, general information, any questions about the legality of a specific act in the U.S. should be posed directly to either the local FBI field office, a cyber-crime attorney, or the U.S. Attorney’s office. This information only applies to the U.S. Wardrivers are encouraged to investigate the local laws where they live to ensure that they aren’t inadvertently violating them. Understanding the distinction between “scanning” and identifying wireless access points, and actually using the access point, is the same as understanding the difference between Wardriving (a legal activity) and theft, (an illegal activity).

# Introduction to Wardriving with Linux

Linux is the most robust operating system for wardriving. Unlike Windows, Linux offers the ability to place your wireless card in monitor (rfmon) mode, which allows you to perform passive scanning to detect access points that are not broadcasting the Service Set Identifier (SSID) beacon. These are commonly referred to as *cloaked*, or *hidden* access points. This capability, along with the large amount of open source and freeware wireless programs that have been developed for Linux, has helped make Linux one of the most popular operating systems used by both wardrivers and penetration testers.

# Preparing Your System to Wardrive

Before you can wardrive using Linux, you need to ensure that your operating system is properly configured to utilize the tools that are available. Specifically, you need a kernel that supports monitor mode and your specific Wireless Local Area Network (WLAN) card. After kernel configuration is complete, you need to install the proper wardriving tools and tailor their configurations to your preferences.

# Preparing the Kernel

Configuring Linux to Wardrive used to be a very difficult process that involved both kernel configuration and driver patching. That is no longer the case. As of the