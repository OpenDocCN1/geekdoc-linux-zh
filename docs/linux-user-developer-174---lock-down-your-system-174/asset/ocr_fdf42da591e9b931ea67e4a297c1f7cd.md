```
```
A - Serial Device       : /dev/ttyS0
C - Callin Program
D - Callout Program
E - Bps/Par/Bits       : 115200 8N1
F - Hardware Flow Control : No
G - Software Flow Control : No

Change which setting?
```
```

Arch Linux ARM. It is developed and maintained by us and makes it easy to construct custom packages and solutions. It adopts the Arch Linux way of doing things, but with much-needed extras. Don't get me wrong, there's a lot of great things about Arch Linux, but it can be overly complicated when it really doesn't need to be. So it was our aim to make it more accessible and considerably expand on its feature set.

The Guinnux rescue file system allows users to boot into flash should the embedded system fail, and allows for simple system recovery – we've had a lot of positive feedback about this so far. The system can be recovered without having to re-flash an image – a useful addition that saves more than just time! In fact, it is essential for enterprise deployments to recover and more surprisingly, it's a feature that is often left out of many other enterprise-based distributions.

Other features myself and the team have been working on include adapting the boot loader so users are able to boot kernels from any external file system. This allows for Keystone to distribute and upgrade kernel packages from anywhere and at any time, without interrupting service. Users can also find a ton of extra information about Guinnux over on our official Wiki page: http://wiki.guinnux.org/doku.php.

# What makes Guinnux truly unique compared to other embedded Linux distributions?

Guinnux is the first embedded GNU/Linux distribution that emulates the proven workflow of Enterprise Linux solutions. We've looked to blend all that is great with enterprise distributions – of which there's a lot – with the core stabilities and improvements that we've introduced in Guinnux.

Users will also find Guinnux as a headless enterprise embedded Linux distribution, but [it] still provides a mature and stable development environment for all our users. We've also looked to offer a comprehensive networking and protocol compatibility suite, something that many of our...

![](bbox=[0.41, 0.37, 0.92, 0.655])

# Getting acquainted with the Guinnux Starter Kit

The Guinnux Starter Kit aims to be a one-stop shop for everybody who could possibly need to start developing with Guinnux. It serves as an entry point for the evaluation of both the runtime and development environments that Guinnux offers its users. The kit itself consists of a ARM9-based development board, a 5V external power supply and a microSD card for use with the board. This development board includes a number of I/O interfaces, such as RS232 Serial, USB 1.1 Host, 10MB LAN and room for a 10 expansion connector as well. Other specifications include 64MB SDRAM and battery-backed RTC.

The latest version of Guinnux comes pre-programmed onto the board, with the accompanying ext4 root file system boot and loaded onto the microSD card. Extra binary and system images are available for download from the official Guinnux site. By standard, the root file system contains every single core utility to remotely access and customise the Guinnux development board, so expect to things like the DPKG Package Manager and the openSSH server among others. Interested parties can get their hands on the Guinnux Start Kit over at **www.kaes.net**.