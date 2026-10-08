Signal level:49/153 Noise level:13/153
Encryption key:off
Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 18 Mb/s
24 Mb/s; 36 Mb/s; 54 Mb/s

In this case, the information provided by the iwlist command was very useful in identifying available wireless access points, their names, and whether they were configured for authentication/encryption. The iwlist command can also query specific wireless configuration details—see the online man page for iwlist (using the command man iwlist) for more information.

# Installing and Using Windows Networking Drivers

Driver support is one of the few areas in which Linux lags behind Microsoft Windows. I hope that making this statement doesn't offend Linux Torvalds to give me a call and demand the return of my official Linux Bigot decoder ring, but it's a fact. The reason that there are not Linux drivers for every piece of random hardware is not because of any problem or limitation in Linux, but rather device manufacturers target their largest potential when writing device drivers for their hardware, and, at the moment, the main market for PC hardware-is Microsoft Windows systems.

Clover folks in the open source community are writing new drivers every day, and each new Linux kernel supports more hardware than ever. However great that is, it doesn't help when you need to use a specific Windows device today. Luckily, a Linux kernel and related utilities, called ndiswrapper, enables you to use the Microsoft drivers for much of the networking hardware that is not yet supported by Linux. How cool is that? Thanks to the ndiswrapper package, you can use Windows' drivers on your superior Ubuntu systems until a native Linux driver becomes available.

One obvious question is, "Why not just buy hardware that works with Linux in the first place?" To be honest, with my general approach, there are some very good reasons for wanting (or needing) to use hardware that is Windows-only. The most significant of these are the following:

+   - You already have a wireless network adapter that is not yet supported by Linux. Why buy another adapter if you don't have to?

+   - Dual-boot laptops often include built-in hardware that is not supported by Linux. Similarly, if you are given a laptop as part of your job along with PCMCIA or USB network adapters that are not supported by Linux, using the Windows drivers with Ubuntu enables you to use a real operating system for work without requiring to spend any money.

+   - Some wireless protocols, most specifically 802.11a, are poorly supported under Linux but are still used by many businesses. Because 802.11a is also largely extinct, I doubt