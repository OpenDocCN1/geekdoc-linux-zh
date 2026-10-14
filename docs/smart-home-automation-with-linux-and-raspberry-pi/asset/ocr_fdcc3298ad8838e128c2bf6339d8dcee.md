The software hack involves most of the same steps, with the few added complications explained in detail at [www.xbox-linux.org/wiki/Software_Method_HOWTO](http://www.xbox-linux.org/wiki/Software_Method_HOWTO) (or [http://web.archive.org/web/200100728124622/](http://web.archive.org/web/200100728124622/) if the site is offline). Naturally, being software, the Linux install disappears on each reboot—your data remains, but you must reinstate the hack to boot Linux in order to access it.

There was once The Xbox Chocolate Project, where Xbox Linux users would help would-be users modify their machines. It is still going, but fewer volunteers are available. Asking at your local Linux User Group (aka LUG; see [www.linux.org/groups](http://www.linux.org/groups) for your local group) might be another idea.

The reason for hacking an Xbox is up to you. If you just want to make it play DVDs, then the Microsoft DVD Playback Kit is a better option, and it comes with its own IR remote control. As a set-top box, it might be a little noisy compared to the other solutions I’ve mentioned (and will mention) by today’s standards. But as a secondary (or even primary) file server, web server, or even desktop machine, it has extremely positive geek credentials.

# Xbox Media Center

Despite the name, there are more versions of Xbox Media Center (XBMC) running on non-Xbox platforms than there are on the Xbox, including versions for the Raspberry Pi and a Live CD, all available from [www.xbmc.org](http://www.xbmc.org)! This is because the software can only be compiled using the Xbox development kit (XDK), which is made available only to licensed developers. And because Microsoft isn’t happy with Linux developers writing open source software on its console, this is not available to hobbyists in any form. Consequently, the only native versions of XBMC running in the wild are those compiled by licensed developers and those versions that have leaked out from those developers. The legality of such versions is seriously suspect. In either case, you will still need a modified Xbox to run the code, as you would with Xbox Linux.

> **Note** If you do have access to the Xbox software, then you can use the IR remote control that is supplied with the Microsoft DVD Playback Kit with XBMC.

As software, XBMC contains a lot of top-end functionality and is still in active development. This includes an initiative to reduce the boot time, making it appear more like a set-top box and less like a computer running software—one goal to which all home automation devices should aspire.

Its functionality includes the ability to play back media of almost every format (coming from hard disks, optical media, network shares, online streams and feeds, and DAAP for iTunes), display photographs, run Python-written plug-ins (for weather reports and the like), and play games. It is also able to support the media with data services from IMDb (the Amazon-owned Internet Movie Database) and FreeDB (for CD track listings). For many, the main XBMC lack is concerns its skinnability, allowing anyone with a minimum of knowledge to create custom interfaces for the software.

Despite its prominence, there are several forks of XBMC: Boxee, with integration into social networking applications; MediaPortal, a Windows-centric version with PVR handling; Plex, which focuses on the Mac OS X and associated Apple platform-oriented functionality (such as the iTunes app store); and Voddler, which supports media streaming from its (commercial) video-on-demand site.

# Hardware Hacks

The hacks in this category will involve changes you can make either to existing hardware or to new hardware you can easily build that controls, or is controlled by, an existing computer.

# Linksys NSLU2

The existing NSLU2 unit (aka the Slug) requires no hardware hacks to make it run any of the custom Linux firmwares covered earlier. However, you can improve the unit with various hacks.