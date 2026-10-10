# Notes from the Underground

# Live Distros

If you are brand new to Linux and the idea of learning a new OS seems overwhelming, you can still try Kismet and Linux without a huge investment of time, effort, or money. Many variations of complete Linux distributions, known as “Live Distros,” are available on bootable read-only Compact Disks (CD-ROMS). To try a live distro, you simply download the CD-ROM image (called an International Organization for Standardization [ISO] file) from a creator’s Web site, and burn it to a blank CD-ROM. When the computer is then booted off the new CD-ROM, it will start up in Linux. Most Live distros are based on standard distros such as Slackware.

To return to your original operating system, simply remove the CD-ROM and boot off the hard disk as you would normally.

One of the most popular live distros is Knoppix, available from www.knop-pix.de and www.knopper.net. Knoppix runs with a Graphic User Interface (GUI) to make it easier for the novice Linux user to navigate. It has Kismet pre-installed along with a number of drivers for many popular cards.

Another popular live distro is Backtrack (www.remote-exploit.org). Backtrack is designed to be used by Information Security (InfoSec) professionals for system and network security audits, and as such has a plethora of security tools in addition to Kismet. It also has a number of popular wireless card drivers pre-installed. As of this writing, Backtrack 2 has been out for well over a year, and Backtrack 3 is in Beta Release.

Running Kismet in Backtrack is covered in detail in Chapter 10.

To keep the beginning as simple as possible, we’ll discuss the basic installation of Kismet and its use with a common wireless card, but we aren’t going to discuss things like antennas or using Kismet with a Global Positioning System (GPS) receiver until the next chapter. We will be installing Kismet as the user “root” for this initial installation. In Unix-type systems such as Linus, “root” is the administrator-level user.

# Kismet Prerequisites

Depending on how you installed Linux on your machine, you may need some additional software before you install Kismet. Kismet is written in the C++ computer