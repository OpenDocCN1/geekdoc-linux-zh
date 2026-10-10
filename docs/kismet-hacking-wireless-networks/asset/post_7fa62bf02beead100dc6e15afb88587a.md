
## Summary

In today’s world of everyone using wireless networks, there will almost always be other networks in the area of yours. This means that you probably only want to monitor threats directed at your network. In this case, you probably only want to monitor the channel you are operating your access points on, so as to avoid unnecessary data collection and possibly violating any number of laws regarding privacy and data interception. As well, if you decide to channel hop, it’s likely you’ll miss a lot of data, which can be a problem if you are looking to monitor usage by users or by an intruder. If you want to monitor for performance reasons, channel hopping may be a good idea, so you can get a view of the wireless landscape of other networks in the area.

Filters will be your friend as well. If you’re monitoring your network and all the traffic going over it, filters can be used to limit the amount of data collected to just the minimum necessary and the unusual, otherwise things will become very big, very quickly.

The level of complexity is up to your imagination, but for the purposes of this book, we focus on Kismet’s strength as a cheap and effective way to monitor your small network in an office.

# Chapter 8
## Kismet Drones

**Solutions in this chapter:**

- Drone Installation
- PC Drone Setup
- Summary

## Introduction

This chapter hopes to show you the various ways that Kismet drones can be used and integrated into your network monitoring. Kismet has a neat trick in terms of sources. The server doesn't need to be on the same system as the source feeding it. Kismet just receives packets and parses them into a human readable view; it doesn't care where that data comes from. Kismet supports an installation of remote, dumb sensors called drones. Drones sniff data from the air and send it down to the server. Kismet can handle several of these and they don't need to be powerful systems. This part of the book will focus on building drones and integrating them with Kismet server.

## Drone Installation

A drone is a fairly dumb device. It needs nothing more than a compatible network device that can support monitor mode. In addition, it needs something resembling a CPU that can run a very basic Linux and the drone software. Finally, it needs a backhaul method to get the captured data to the server.

You can run a Kismet drone on any type of system you like, from full, modern PC to small embedded computers and everything in between. Kismet is built with x86 systems in mind, but ARM, MIPS and other processors are possible to use as well.

In this chapter we will show you both ends of the spectrum in terms of difficulty and cost.

### Linksys WRT54G

The WRT54GL is the latest version of the WRT54G family of routers that have been a great deal of fun for hardware hackers over the last few years. They contain a MIPS processor, a wireless chipset, and wired Ethernet connections, everything we need.

As hackable and available as they are, WRT54G's are limited. The main problems with them is that they have a small memory footprint, and a proprietary Broadcom chip set that limits what we can do to what the manufacturer's driver let's us do, and an open source software development cycle that isn't always up to date.

That being said, their redeeming value of being dirt cheap and well documented means that we can squeeze a lot of capabilities out of these units if you don't want to spend money to get extra features of other hardware, or if those other features are not necessary.

## Notes from the Underground

### A Word About Cross Compiling

In some cases it’s not possible to compile software on the device it’s going to run on. Small embedded systems often have no space for a full compiler, libraries, sources, and so forth, which are needed to build software. The 2 megabytes of memory and 200Mhz processor makes it so we can’t compile Kismet directly (natively) on the WRT54GL. Cross-compiling is often necessary to build the software in these cases. Cross-compiling is basically building software on one architecture for another. In the case of the WRT54GL, you can build software on your x86 desktop for the MIPS processor.

Cross-compiling can be more a case of voodoo than an art. Setting up toolchains for other architectures is not something for the timid, or even some of the experienced users out there. A great deal of time and research was spent to try and document building your own cross-compiler to build drones for the WRT54GL, however, it was nearly impossible to document all the variables required. In addition, the ever-changing sources for OpenWRT, Kismet, and all the other software needed means it would require an entire book on it’s own to talk about cross-compiling. For the most part though, with drones, you can easily be back several revisions of Kismet and not break anything, since the fields coming across the wire have not changed across versions.

It is highly recommended that if you are using Kismet on architectures other than x86, let the developers of whatever Linux distribution you will be using on the device cross-compile it and package it for you. It will save you from dealing with the same headaches and stress the authors went through.

The OpenWRT Buildroot system is an exception. If everything lines up, the build root takes care of setting up the toolchains necessary, and all the source files for building your own firmware and packages.

In short, if you can compile on the system you are going to be running a Kismet drone on, it’s best that you do. If you can’t, the developers for your target platform may have a packaged solution that’s easier to set up than manually trying to build your own cross-compiler.

## Installation

Installation and configuration of a Kismet drone on a WRT seems to be a lot of steps, but it’s very easy once you get through your first one. These instructions are adapted from instructions available online from the authors, which have proven very reliable.

> **NOTE**
>
> A whole book could be written about the linksys WRT54GL and its many versions. In fact, there is one from Syngress, “Linksys WRT54G Ultimate Hacking” by Paul Asadoorian and Larry Pesce. A great read if you want to know more about the hardware underlying these systems.

The first step should be to get your hands on a compatible WRT54. The best bet is the WRT54GL. The L designates that this version runs Linux and is compatible for our needs. The OpenWRT wiki has a huge amount of information on specific models and compatibility and should be your first stop.

> **NOTE**
>
> Early WRT versions all ran Linux. When linksys released version 5 of the ubiquitous router, they changed from a Linux-based firmware to a vvxworks proprietary firmware and also changed the amount of memory and a few other specifications. The backlash was significant enough that linksys released the wrt54gl models with the original amount of memory and running Linux in order to keep feeding the tinkerer market. (See http://wiki.openwrt.org/OpenWrtDocs/Hardware.)
>
> OpenWRT has two versions available: Whiterussian and Kamikaze. Whiterussian is the older, stable version, while Kamikaze is the new development version. In the first part of the chapter, we will use Whiterussian as an example even though it is no longer being developed. The second part will be about Kamikaze. The reason Whiterussian is included is first, because it’s stable. Kamikaze is a moving target and tricky to write about, because they haven’t sorted out all the issues that may affect a drone. In the process of writing, several bugs and problems were found and corrected in the development version, so Kamikaze will work but needs the additional step of building your own OpenWRT package with a cross-compiler.

First, we need to get the router set up so we can talk to it. This usually starts with plugging it into your network or to your computer through a crossover cable. A crossover cable is best since you probably don't want to introduce a new Dynamic Host Configuration Protocol (DHCP) server onto your network until you have a chance to turn that off.

Configure the router's address, Domain Name System (DNS), and gateway, so that the router can talk to the rest of the world and we can load packages later. This can be done after OpenWRT is loaded, but we will use the GUI Linksys here to make life easier.

## Whiterrussian

Download the “OpenWRT Whiterrussian” release from http://downloads.openwrt.org/whiterrussian/newest/default/. OpenWRT uses the jffs or the squashfs file system. Both are writable, so added files and changes are retained through power cycles, meaning that your drone files are not erased on reboot. You can also store scripts for running all the commands, to start up the drone on the router or just have it start up the drone on boot. The squashfs system makes it easier to keep from messing up the system, since the base files are read-only. So unless you have a pressing need for the jffs file system, you probably want to get the squashfs image from the download site.

Select the right firmware for your router type according to the Whiterrussian README on the openwrt site (http://downloads.openwrt.org/whiterrussian/newest/00-README). If you select the wrong one, you might turn your router into a useless electronic brick, so make sure to get the right one.

Connect to the Web control panel on the router (presuming you have not removed the Linksys firmware yet or are using another with a Web utility). Using the Upgrade firmware button under Administration | Upgrade Firmware, violate your warranty by loading the .bin file you downloaded from the openwrt.org Web site.

> It is advisable to set the BOOT_WAIT parameter on your router before you flash. In case you turn your router into a brick, this gives you a few seconds to try and upload a fresh firmware on powerup. If not, it gets ugly. The OpenWRT Users guide has instructions for doing this on the default
