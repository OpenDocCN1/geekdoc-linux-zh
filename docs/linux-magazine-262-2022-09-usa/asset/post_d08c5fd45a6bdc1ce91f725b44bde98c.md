
## 16 Beyond 5G

Behind the scenes, the cellular phone network has always been the preserve of highly specialized and proprietary equipment, but some recent innovations could be changing that. This month we explore the Open RAN specification, which could one day allow more of the mobile phone network to operate on off-the-shelf hardware.

### IN-DEPTH

- **56 Programming Snapshot – Go Geolocation Game**
A geolocation guessing game based on the popular Wordle evaluates a player’s guesses based on the distance from and direction to the target location.

### MakerSpace

- **66 Home Laser**
With the FLUX Beamo laser and a Raspberry Pi Board B10001, you can execute your own laser cutting projects on a wide range of materials.

- **72 Home Assistant with MQTT**
Automating your four walls does not require commercial solutions. With a little skill, you can develop your own projects on a low budget.

### LINUXVOICE

- **77 Welcome**
This month in Linux Voice.

- **78 Doghouse – Chess**
Maddog considers the history of chess as a metaphor on how to grow the desktop Linux user base.

- **79 Present Slide Creator**
The Golang package present may be the key to making attractive slide presentations with less work and hassle.

- **84 FOSSPicks**
This month Graham looks at Lorian, FreeCAD 0.20, CLAP, Gophide, GameShell, Jellyfin, Vita3K, and more!

- **90 Tutorial – Manuskript**
The Manuskript editor is all you need to jump start your next writing project.

![](img/b40e8bf6cf651f8eebf36f5265123095_4_0.png)

**TWO TERRIFIC DISTROS**
**DOUBLE-SIDED DVD!**
SEE PAGE 6 FOR DETAILS

## openSUSE Leap 15.4 and MX Linux 21.1
Two Terrific Distros on a Double-Sided DVD!

![](img/b40e8bf6cf651f8eebf36f5265123095_5_0.png)

![](img/b40e8bf6cf651f8eebf36f5265123095_5_1.png)

### openSUSE Leap 15.4
64-bit

### MX Linux 21.1
64-bit

Leap 15.4 is the latest stable release of openSUSE, the popular and well-established community-based distribution. Leap 15.5 is not scheduled to replace it until June 2023.

Because the 15.4 release is built upon a mature platform, most of its features are updates, and often behind the scenes. Several changes are enhancements and improvements to sudo and visudo, and backports and bug fixes to systemd. In addition, the release has major updates to AppArmor, as well as to productivity tools such as Firefox and LibreOffice.

Perhaps the most noticeable change is the introduction of DNF, the package manager which has largely replaced Yum in other RPM distros such as Fedora. While Yum remains in openSUSE, the 15.4 release can be configured to use DNF. In addition, the 15.4 release also introduces Microdnf, a subset of DNF that can be used to speed up package installation when the whole of DNF is not required.

Like all openSUSE releases, Leap 15.4 is a general-purpose release, suitable for all levels of users.

What do you get when the lightweight antiX distribution collaborates with the once-prominent MEPIS community? Answer: A Debian derivative that has been first in page hits on DistroWatch for three years and shows few signs of slipping.

Install MX Linux, and the reasons for its popularity become obvious immediately. The antiX core makes for a speedy system, and many will approve of MX Linux’s minimal reliance on systemd. Newcomers can appreciate the clear and detailed documentation, especially in the installer, and the orienting Welcome screen and tour of the desktop. For more experienced users, the desktop contains a series of tools rarely if ever matched in other distributions. These original tools include graphic interfaces for editing Bash, the boot manager, repositories, the firewall, and advanced backup techniques. Less spectacularly but equally usefully, MX Linux also includes a USB formatter, a Live USB creator, and a Samba configurator – as well as many other tools for tasks that are done from the command line in other distributions. For more information, see this issue’s Distro Walk.

Defective discs will be replaced.
Please send an email to subs@linux-magazine.com.

Although this Linux Magazine disc has been tested and is to the best of our knowledge free of malicious software and defects, Linux Magazine cannot be held responsible and is not liable for any disruption, loss, or damage to data and computer systems related to the use of this disc.

## Take Your First Steps In Web Development!

![](img/b40e8bf6cf651f8eebf36f5265123095_6_0.png)

### Web Development Essentials

Modern software applications are commonly developed for the Web. Linux Professional Institute's new Web Development Essentials program supports you in your first steps in software development. It includes learning materials suitable for both training and self-study. Upon passing the Web Development Essentials exam, you receive a certificate to prove your skills.

LPI Learning Materials are available at [learning.lpi.org](http://learning.lpi.org). Find out more about the program and the exam at [lpi.org/wde](http://lpi.org/wde)

![](img/b40e8bf6cf651f8eebf36f5265123095_6_1.png)

## NEWS

Updates on technologies, trends, and tools

### THIS MONTH'S NEWS

- **08**
    - Rocky Linux 9 Has Arrived
    - Slimbook Upgrades CPUs in Executive Linux Ultrabook
- **09**
    - Fedora Linux Is Coming to the Raspberry Pi 4
    - KaOS 2022.06 Now Available with KDE Plasma 5.25
    - More Online
- **10**
    - Manjaro 21.3.0 Now Available
    - SpiralLinux: a New Linux Distribution Focused on Simplicity

### Rocky Linux 9 Has Arrived

Rocky Linux 9 is now available and is a landmark release for several reasons. First off, there has been a surge in Rocky Linux deployments, putting it ahead of CentOS Stream and AlmaLinux. But more than that, Rocky Linux includes several security enhancements and networking features to help make it a best-in-class open source operating system for businesses of all sizes.

In the new release, you'll find SHA-1 message digest for cryptographic purposes has been deprecated (as the cryptographic hash functions are no longer considered secure). In addition, you'll find OpenSSL 3.0.1 (which includes provider concept, a new versioning scheme, an improved HTTP/HTTPS client, support for new protocols/formats/algorithms, and more), OpenSSH version 8.7p1 (which includes the replacement of the SCP/RCP protocol with the more predictable SFTP protocol), SELinux performance improvements, and the automatic configuration of security compliance settings for PCI-DSS, HIPAA, DISA, and more.

![](img/b40e8bf6cf651f8eebf36f5265123095_7_0.png)

As for the networking improvements, you'll find that MultiPath TCP Daemon can now be used instead of iproute2 for the configuration of MultiPath TCP endpoints. Also, NetworkManager now uses key files to store connection profiles (but still supports ifcfg). Iptables-nft and ipset are deprecated and have been replaced by the nftables framework. Finally, network-scripts has been removed in favor of NetworkManager to configure network connections.

One other major move forward for Rocky Linux is that this version was built with a community-developed, open source, cloud-native system, called Peridot. This Golang project was developed to assure new versions of Rocky Linux can be released within one week after each RHEL version. By migrating to this system, anyone can reproduce Rocky Linux from scratch, ensuring that the distribution will always be available. The source for the Peridot build system can be found on GitHub (https://github.com/rocky-linux/peridot-release).

For more information about the new Rocky Linux release, be sure to read the complete release notes (https://github.com/rocky-linux/documentation/blob/6d86674106232d3c0ab72da734de6eede4e46549/docs/release_notes/9.0.md).

### Slimbook Upgrades CPUs in Executive Linux Ultrabook

Slimbook, well known for producing KDE Plasma-powered laptops, has given their Executive series a bit of a refresh by making them available with the Intel 12th Gen Alder Lake CPU. This new iteration adds considerably more power
