
## Figure 1.10 Kismet Help Interface

![](img/d6ac176c353d2b7687c1186a140180a1_44_0.png)

## Using a Graphical Front End

In addition to the standard Kismet interface, you can also use a graphical front end with Kismet. Gkismet (http://gkismet.sourceforge.net) is a front-end interface that works with Kismet. Once you have downloaded, compiled, and installed gkismet, you need to start the Kismet server:

```
# /usr/bin/kismet_server
```

Next, start gkismet:

```
# /usr/bin/gkismet
```

This opens the gkismet interface and prompts for the *kismet_server* information (see Figure 1.11). In most cases, you will be connecting to *localhost* (127.0.0.1) on default port 2501.

## Figure 1.11 Connecting to the Kismet Server

![](img/d6ac176c353d2b7687c1186a140180a1_45_0.png)

Once you have entered your server information, gkismet connects to the Kismet server and you receive a display of the access points Kismet has discovered (see Figure 1.12).

## Figure 1.12 Gkismet in Action

![](img/d6ac176c353d2b7687c1186a140180a1_45_1.png)

There are several advantages to using a graphical front end. For instance, the card power is displayed on the main screen. This can be very beneficial for direction finding and walking down rogue access points. Additionally, you can easily examine the information on each access point by double-clicking on the access point you want information on.

Additionally, the sort options can be accessed by right-clicking on the SSID of the access point and choosing how you want the information sorted.

## Summary

In this chapter we have explored some of the history of how wireless technology evolved into what it is today. Wireless technology has been around a long time, considering the decades of development in radio and cellular telephone technology. These technologies have been quietly developing in the background while PDAs, Palm Pilots, and other handheld wireless devices have been gaining notoriety. Other uses such as GPS and satellite communications to the home have also been developing for mainstream applications. These applications offer consumers many advantages over wireline counterparts, including flexibility, mobility, and increased efficiency and timeliness.

Kismet is a very powerful tool for both wardriving and penetration testing. One of the biggest advantages of using Kismet is the ability to use monitor or rfmon mode. This allows you to identify wireless networks that are not broadcasting the SSID in the beacon frame and sets Kismet apart from its Windows counterpart NetStumbler.

It is important to understand the many features of Kismet in order to maximize its effectiveness. You can edit the kismet.conf file to customize Kismet to your specific needs. The Kismet panel interface provides many different user options for sorting and viewing information about the networks you discover. Additionally, graphical front end programs like gkismet can make viewing data a bit easier on the eyes.

Kismet is also a great tool for a penetration tester that needs to perform WLAN discovery to identify a target network. Although not always 100% accurate, Kismet can be used to identify the type of encryption used on a network. For complete accuracy you can open your Kismet.dump file, which is a pcap formatted packet capture with a packet analyzer like Ethereal or Wireshark to get an accurate reading of the encryption level. Once you have identified your target and the encryption level there are several open source tools available to continue the penetration test. Tools like SirMacSloot can spoof the MAC address and bypass MAC Address filtering. The Aircrack suite provides a rich set of tools for collecting packets, injecting packets and cracking WEP. CoWPAtty is a great tool for breaking WPA-PSK when used with a good dictionary file.

Performing a penetration test on a wireless network is often a way to get an initial foothold into the network. While always remembering to stay within scope, you can then begin your normal penetration test process for the internal network with your entry vector into the wireless network providing you with an excellent jumping off point.

# Chapter 2

# Basic Installation

Solutions in this chapter:

- Introduction
- Kismet Prerequisites
- Kismet installation
- Compiling and installing Kismet on a Linux laptop
- Choosing a wireless card driver
- Wireless card driver compiling and installation
- Editing the Kismet configuration file for a basic Kismet installation
- Run Kismet

## Introduction

This chapter will introduce you to the basic installation of Kismet. A basic installation is one in which the server and the client portions of Kismet are on the same laptop. This is the installation that most people will be interested in, at least initially. Advanced installations for separate servers and clients, as well as remote and drone machines, will be covered in Chapters 7 and 8.

Here we’ll be focusing on a “typical Kismet install” on a “typical Linux system.” For those who don’t know, Linux (formally known “GNU/Linux”) is a UNIX-like operating system (OS), created in 1991 by Linus Torvalds. Kismet can be installed on most “Unix-like” OS, including Linux, Debian, Berkeley Software Distribution (BSD), Apple OSX/Darwin, and Linux virtual machines running under Microsoft Windows. However, since Linux is the “native” operating system for Kismet, and is what most users will be using for running Kismet, it’s going to be the basis for our initial “typical Kismet install.”

While Kismet will run on almost any personal computer in which Linux is installed, it is assumed here that most people who are using a basic Kismet setup will be doing so on a wireless networking-enabled laptop. Therefore, throughout this chapter the terms “computer,”“personal computer,”“PC,” and “laptop” are used interchangeably.

Also, as Linux systems tend to be almost as idiosyncratic as their owners, the word “typical” is used here with a grain of salt. The installation covered here will be as generic as possible, but please understand that variations in how Linux has been installed on your laptop may render some of the following information useless. It will be impossible to cover all possible departures from the norm, although we will try to cover some common variations.

Going into this chapter, you will need to have some Linux distribution (or “distro” in Linux jargon) already installed on you laptop, and at least a passing familiarity with Linux’s command-line interface (CLI) and how to do things in Linux such as downloading files.

![](img/d6ac176c353d2b7687c1186a140180a1_49_0.png)

## Notes from the Underground

### Live Distros

If you are brand new to Linux and the idea of learning a new OS seems overwhelming, you can still try Kismet and Linux without a huge investment of time, effort, or money. Many variations of complete Linux distributions, known as “Live Distros,” are available on bootable read-only Compact Disks (CD-ROMS). To try a live distro, you simply download the CD-ROM image (called an International Organization for Standardization [ISO] file) from a creator’s Web site, and burn it to a blank CD-ROM. When the computer is then booted off the new CD-ROM, it will start up in Linux. Most Live distros are based on standard distros such as Slackware.

To return to your original operating system, simply remove the CD-ROM and boot off the hard disk as you would normally.

One of the most popular live distros is Knoppix, available from www.knop-pix.de and www.knopper.net. Knoppix runs with a Graphic User Interface (GUI) to make it easier for the novice Linux user to navigate. It has Kismet pre-installed along with a number of drivers for many popular cards.

Another popular live distro is Backtrack (www.remote-exploit.org). Backtrack is designed to be used by Information Security (InfoSec) professionals for system and network security audits, and as such has a plethora of security tools in addition to Kismet. It also has a number of popular wireless card drivers pre-installed. As of this writing, Backtrack 2 has been out for well over a year, and Backtrack 3 is in Beta Release.

Running Kismet in Backtrack is covered in detail in Chapter 10.

To keep the beginning as simple as possible, we’ll discuss the basic installation of Kismet and its use with a common wireless card, but we aren’t going to discuss things like antennas or using Kismet with a Global Positioning System (GPS) receiver until the next chapter. We will be installing Kismet as the user “root” for this initial installation. In Unix-type systems such as Linux, “root” is the administrator-level user.

## Kismet Prerequisites

Depending on how you installed Linux on your machine, you may need some additional software before you install Kismet. Kismet is written in the C++ computer
