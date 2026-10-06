# Chapter 9 ♦ Running Debian GNU/Linux 305

low-demand applications. Intel PRO/100 and PRO/1000 adapters are supported in Linux and will work well in high-demand applications, as will cards based on the "tulip" chipsets and most 3com network cards.

Many newer systems include software-based modems that are not supported by the manufacturer under Linux. If you require a dial-up connection for Internet access, see Chapter 5 and check out http://tildp.org/HOWTO/Modem-HOWTO-2.html before you start the installation process.

Many other devices, as sound and video capture cards, can also be used under Linux. For more information about hardware compatibility, see the Hardware Compatibility HOWTO at http://tildp.org/HOWTO/Hardware-HOWTO/

# Workstations

In most cases, workstation users will want to run the X Window System (X11). The ability to run X11 depends on compatibility with the video chipset on your video card or motherboard. Debian 3.1 includes version 4.3.0 of the XFree86 X System. You can find a list of video chipsets supported in this release at http://xfree86.org/4.3/0.

# Servers

A Linux installation generally consists of only the minimum set of packages required to provide the service for which it was designed. In particular, this means that servers do not usually have a graphical interface installed.

Server hardware is generally more expensive than workstation hardware, although you can still run smaller servers on less-expensive desktop hardware. If you are planning to store important data on your server, you will want to look into a RAID array storage. A number of inexpensive ATA RAID controllers work well under Linux.

> More information about ATA RAID compatibility is available at the following sites: http://linuxmia.com/faq/Hardware/sata.html and http://biblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Hardware-HOWTO#IDERA.

Higher-end servers will of, require more expensive hardware. In applications such as mail servers where you will have a lot of disk activity, plan splitting the disk-intensive tasks across multiple arrays. When it comes to CPU and RAM, more of both is good, but most applications benefit more from extra RAM than they do from multiple CPUs.