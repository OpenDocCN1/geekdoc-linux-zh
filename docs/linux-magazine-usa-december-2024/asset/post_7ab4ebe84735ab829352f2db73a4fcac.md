
![](img/d6d2a4cd4a2f445e8c9e8079857e2469_4_0.png)

## 16 Coding with AI

Futurists predict a day when computers will write the computer programs. Are we there already? This month we separate fact from hype to examine some of the popular AI-based coding tools and explore what they can (and can't) do well.

## Make Space

- **56 Embedded Rust**
  Rust, a potential successor to C/C++, claims to solve some memory safety issues while maintaining high performance. We look at Rust on embedded systems, where memory safety, concurrency, and security are equally important.

- **64 Off-Grid File Sharing**
  A battery-powered WiFi hotspot can provide useful services like file sharing even when you're off the grid. A Pi Zero 2 W as the hotspot with ownCloud installed does the trick.

- @linux-magazine.com
- @linux_pro
- @linuxpromagazine
- Linux Magazine
- @linuxmagazine

## LINUXVOICE

- **71 Welcome**
  This month in Linux Voice.

- **73 Doghouse – Stakeholders**
  The stakeholder approach of open source broadens the pool of who can access, influence, and benefit from information technologies.

- **74 Anki**
  Flashcards are a fast and effective way to memorize pertinent facts for your next exam. Anki takes this time-honored trick in a direction you never could have imagined with the days of those classic 3x5 cards.

- **82 FOSSPicks**
  Nate explores some top FOSS tools, including the latest Gnome desktop, a slick 3D model viewer, LibreQuake, a neat currency converter, and much more.

- **88 Tutorial – Legacy Video Games**
  People born in the late '80s and early '90s often have a sizeable collection of old video games gathering dust at home. Systems capable of executing these are, however, becoming scarce. This article explores the options for archiving old PC games and running them on modern systems.

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_4_1.png)

### TWO TERRIFIC DISTROS
### DOUBLE-SIDED DVD!
**SEE PAGE 6 FOR DETAILS**

### Kubuntu 24.10 and Kali Linux 2024.3
### Two Terrific Distros on a Double-Sided DVD!

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_5_0.png)

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_5_1.png)

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_5_2.png)

### Kubuntu 24.10
#### “Orcular Oriole”
**64-bit**

### Kali Linux 2024.3
**64-bit**

Kubuntu 24.10, codenamed Orcular Oriole, is the newest release of the popular KDE-based Ubuntu flavor known as Kubuntu. The latest edition, which ships with Linux kernel 6.11, will receive nine months of full support until the next long-term support release in April 2025.

The new Kubuntu comes with the KDE Plasma 6.1 desktop, KDE Frameworks 5.116 and 6.6.0, and “many updated KDE Get applications.” The latest release is the next step in the developers' quest to replace the ancient X11 graphics system with the more recent Wayland compositor. In the new edition, Wayland is the default, although X11 is still available as an option.

Plasma 6.1 comes with a new option for easy remote access to other Plasma desktops. Also included are enhanced capabilities for screen locking and desktop customization. A new experimental feature called “permissions prompting” offers “fine-grained control over Snap applications permissions.”

Based on Debian, Kali Linux is a security-directed distribution. It is a popular choice for forensics, penetration testing, and reverse engineering. Kali Linux 2024.3 is the third release of the year.

The focus of Kali Linux 2024.3 is the update and optimization of programming tools, including the documentation. However, the release notes also highlight what is not included because the update and optimization are taking weeks to complete. An important feature still to come is Python 3.12, whose exclusion has also blocked other packages (for details, see https://www.kali.org/blog/kali-linux-2024-3-release/). If a temporarily excluded package interests you, check the weekly updates to see if it is now available.

# Inside
AlmaLinux

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_6_0.png)

Download this free focus guide and get an introduction to AlmaLinux OS, a forever-free, community-based enterprise Linux distribution.

https://bit.ly/AlmaLinux-focus-guide

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_6_1.png)

# NEWS
Updates on technologies, trends, and tools

# THIS MONTH'S NEWS

- 08
  - The Gnome Foundation Struggling to Stay Afloat
  - Thousands of Linux Servers Infected with Stealth Malware Since 2021
  - More Online

- 09
  - Halcyon Creates Anti-Ransomware Protection for Linux
  - Valve and Arch Linux Announce Collaboration
  - More Online

- 10
  - OSL and LPI Form Strategic Alliance
  - AlmaLinux Unveils New Hardware Certification Process

- 11
  - Wind River Introduces eLxR Pro Linux Solution
  - Juno Tab 3 Launches with Ubuntu 24.04

# The Gnome Foundation Struggling to Stay Afloat

The Gnome Foundation has announced changes are underway due to some serious financial issues [https://foundation.gnome.org/2024/10/07/Update-from-the-board-2024-10/]. Their current budget was approved on October 1, and they have been forced to make some very tough decisions to ensure long-term sustainability.

Those decisions include layoffs, most notably Caroline Henrickson, Creative Director, and, Melissa Wu, Director of Community Development. The foundation also indicated that, unless more funds are secured, they will have to make serious changes in how they market, fundraise, and even attend events.

One area that did not see cuts is Gnome's two major conferences; Gnome Asia and GUADec. Fortunately, these events are backed by corporate sponsorship, so they have been spared (for the time being). The Gnome Foundation internship programs and the group's participation in Google Summer of Code are also not impacted by the current cuts.

Part of the reason for these cuts is that the Gnome Foundation had been living off a surplus of funds, but those funds dwindled until, in April 2024, Robert McQueen (Gnome Foundation president) announced that the surplus was gone.

At the time of writing, the Gnome Foundation is currently searching for a new executive director.

The Gnome Foundation is asking for community support by way of volunteering, idea sharing, and donations ([https://www.gnome.org/donate/]).

# Thousands of Linux Servers Infected with Stealth Malware Since 2021

A strain of malware has been exploiting misconfigurations on Linux servers since 2021 and has been found to be quite challenging to remove. The malware has been dubbed perfect and, as you might expect, mines cryptocurrency.

The developers of this malware are as of yet unknown. They have created a malicious piece of software that uses processes and file names that are either identical or very similar to those already found in Linux environments.

To keep itself hidden, perfect uses several tricks, one of which is to install many of its components as rootkits, which by nature are harder to detect. Perfect also stops all easily detected activities when a user logs in, uses a Unix socket over Tor for communication, deletes the installation binary after the service is up and running, manipulates the pcap\_loop process by way of hooking to obfuscate the malware, and suppresses error messages to avoid warnings during execution.

In regards to perfect, Assaf Morag, a researcher for Aqua Security, said, "The main impact of the attack is resource hijacking. In all cases, we observed a monero cryptominer (XMRI)G) executed and exhausting the server's CPU resources. The cryptominer is also packed and encrypted. Once unpacked and decrypted it communicates with cryptomining pools." Morag continues, "To detect PerCti malware you look for unusual spikes in CPU usage, or system slowdown if the rootkit has been deployed on your server. These may indicate cryptomining activities, especially during idle times." (https://www.aquasec.com/blog/perfect-a-stealth-mlware-targeting-millions-of-linux-servers/).

To mitigate against perCiti, you should make sure all Linux servers are patched for all known vulnerabilities, set noexec on /tmp and /dev/shm, disable unused services, implement strict privilege management, isolate critical servers from the Internet or use firewalls to restrict outbound communication, and deploy runtime protection.

# Halcyon Creates Anti-Ransomware Protection for Linux

Halcyon's goal is to defeat ransomware, and on October 1, the company announced the general availability of Halcyon Linux. This new product offers protection against ransomware attacks targeting Linux systems.

According to Cyntel, Linux ransomware attacks increased by 75 percent in 2023 and are expected to continue to climb as more bad actors target Linux deployments (https://www.cynet.com/ransomware/linux-ransomware-attack-anatomy-examples-and-protection/).

The Cyntel report states, "While Linux ransomware only represents a small share of cyberattacks, there are several reasons to be concerned. As a Linux user, you must not overlook ransomware even if it is not yet common on Linux-based systems. While Windows is the favorite for desktops, Linux dominates the market for supercomputers and servers. The Linux computing market is projected to grow to $22 billion by 2029."

To combat that, Halcyon Linux is powered via the Halcyon Anti-Ransomware Platform and secures Linux-based systems with real-time visibility and detections, integrated ransomware response, data exfiltration prevention, efficient performance, cross-platform coverage, and 24/7/365 security analyst monitoring.

Jon Miller, CEO and co-founder of Halcyon says of the new solution, "The fact that Linux systems usually are always on and available means they provide the perfect beachhead for establishing persistence and moving laterally in a targeted network, and they can be leveraged for data theft where the exfiltration is easily masked by normal network traffic."

Miller continues, "As more ransomware operators are developing the capability to target Linux systems alongside Windows, it is imperative that organizations have the ability to keep pace with the expanded threat."

At the moment, there is no indication about the pricing of the new platform, but you can request a solutions brief at https://www.halcyon.ai/anti-ransomware/linux and a demo at https://www.halcyon.ai/get-a-demo.

# Valve and Arch Linux Announce Collaboration

Arch Linux recently announced that it would be part of a collaboration with Steam for two major projects. The projects in question are a build service infrastructure and a secure signing enclave.

According to the Arch news release, "This opportunity allows us to address some of the biggest outstanding challenges we have been facing for a while. The collaboration will speed up the progress that would otherwise take much longer for us to achieve and will ultimately unblock us from finally pursuing some of our planned endeavors. We are incredibly grateful for Valve (https://www.valvesoftware.com/en/) to make this possible and for their explicit commitment to help and support Arch Linux."

The secure signing enclave is intended for the Arch team to use to sign packages with a single signing key, instead of the current process (one person key per package).

# MORE ONLINE

- Linux Magazine
  www.linux-magazine.com

- ADMIN HPC
  https://www.admin-magazine.com/HPC/
  TUI Tools for Containers
  • Jeff Layton
  Text-based user interface tools for a development container.

- ADMIN Online
  http://www.admin-magazine.com/
  A Feature-Rich Drop-In Replacement for Microsoft Exchange
  • Markus Fellner
  Grommunio is a completely open source and fully compatible drop-in replacement for Microsoft Exchange that uncouples your company from Microsoft's cloud strategy and its severe security and data protection issues.

- Manage Software Apps Publicly and Privately
  • Kevin Wittmer
  The WinGet client for the Windows Package Manager improves the software installation experience for administrators, developers, and users and provides a way to create and share software in the WinGet package format for publishing to public and private repos.

- RFID Technologies and Risks
  • Tam Hanna
  We look at various approaches to RFID asset tracking, provide an understanding of the technologies and challenges involved, and cover some of the potential attack vectors.

- Artificial Admin
  • Martin Löschwitz
  AIOps brings artificial intelligence tools into everyday administrative work, with AI-supported automation of some admin responsibilities.
