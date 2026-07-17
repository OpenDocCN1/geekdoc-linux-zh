![](image_rsrc722.jpg)

Front Cover

![A close up of a logo Description automatically generated](image_rsrc723.jpg)

Copyright

First published on Amazon.com by Morgan Partridge in 2024

This edition was published in 2024 by Morgan Partridge

Copyright © 2024 Morgan Partridge

The moral right of the author has been asserted.

All rights reserved.

No part of this publication may be reproduced, stored in a retrieval system, or transmit in any form or by any means, without the prior permission in writing of the author, nor otherwise circulated in any form of binding or cover other than that in which it is published and without a similar condition including this condition being imposed on the subsequent purchaser.

Disclaimer

The information contained in "Mastering Linux Mint 22" (the "Book") is for general information purposes only. The author and the publisher have made every effort to ensure the accuracy and completeness of the information within this Book as of the date of publication.

However, software, technology, and the field of information technology are constantly evolving. Therefore, the author and publisher make no representations or warranties of any kind, express or implied, about the completeness, accuracy, reliability, suitability, or availability of the content of the Book for any purpose. Any reliance placed on such information is, therefore, strictly at the reader's own risk.

Neither the publisher nor the author shall be held liable or responsible to any person or entity with respect to any loss or incidental or consequential damages caused, or alleged to have been caused, directly or indirectly, by the information or programs contained herein.

This Book is not intended as a substitute for the advice of an appropriately qualified and licensed professional or technician. If professional assistance is required, the services of a competent professional should be sought.

Every effort has been made to make this Book as complete and as accurate as possible, but no warranty or fitness is implied. The information is provided on an "as is" basis.

The author and publisher have no responsibility or liability to any person or entity concerning any liability, loss, or risk, personal or otherwise, which is incurred as a consequence, directly or indirectly, of the use and application of any of the content of this Book.

Acknowledgments

To my family without whom none of this would have been possible.

Linus Torvalds is the creator of Linux and holder of the Linux trademark and is acknowledged as such, and he does not support or sponsor this self-help learning book.

Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries

Linux Mark Institute and the community, for developing and maintaining Linux Mint.

Blizzard for developing and publishing World of Warcraft that I really love and enjoy.

WINE or Wine Is Not An Emulator for the compatibility layer.

Lutris making it far more accessible to Install and play games and software.

Gabe Newell and Valve for developing and publishing the Steam Store.

The OpenDyslexic font in the Dyslexic-friendly edition this book is written in was made by Abbie Gonzalez at [https://antijingoist.gumroad.com/l/OpenDyslexic](https://antijingoist.gumroad.com/l/OpenDyslexic) and [https://opendyslexic.org/](https://opendyslexic.org/).

Table Of Contents

Table of Contents

[Front Cover](#part0001.xhtml)

[Copyright](#part0002.xhtml)

[Disclaimer](#part0003.xhtml)

[Acknowledgments](#part0004.xhtml)

[Table Of Contents](#part0005.xhtml)

[Introduction](#part0006.xhtml)

[What Is Linux Mint 22?](#part0007.xhtml)

[Install Test Machine Details](#part0008.xhtml)

[System Requirements](#part0009.xhtml)

[Minimum](#part0010.xhtml)

[Processor:](#part0010.xhtml_a5MY)

[Graphics:](#part0010.xhtml_a5MZ)

[Memory:](#part0010.xhtml_a5N0)

[Storage:](#part0010.xhtml_a5N1)

[Recommended](#part0011.xhtml)

[Processor:](#part0011.xhtml_a5N3)

[Graphics:](#part0011.xhtml_a5N4)

[Memory:](#part0011.xhtml_a5N5)

[Storage:](#part0011.xhtml_a5N6)

[System Requirements Explanation](#part0012.xhtml)

[Linux Mint 22 Pre-Install](#part0013.xhtml)

[Downloading the Linux Mint 22 ISO](#part0013.xhtml_a5N9)

[Selecting Installation Media](#part0014.xhtml)

[DVD-R/RW Discs](#part0018.xhtml)

[Comparing USB and DVD Booting for Linux Mint 22 Installation with Ventoy](#part0022.xhtml)

[Using Ventoy USB Drive:](#part0022.xhtml_a5ND)

[Using a DVD Disc:](#part0023.xhtml)

[Linux Mint 22 Install Guide](#part0024.xhtml)

[Keyboard Layout](#part0025.xhtml)

[Multimedia Codecs](#part0026.xhtml)

[Installation Options](#part0027.xhtml)

[Install Alongside & Erase Disk](#part0028.xhtml)

[Something Else](#part0029.xhtml)

[Finalizing Partition Changes](#part0034.xhtml)

[Timezone](#part0035.xhtml)

[Creating User Profile](#part0036.xhtml)

[Completing Install Process](#part0037.xhtml)

[Setting Linux Mint 22 To Boot](#part0038.xhtml)

[Linux Mint 22 First Login](#part0039.xhtml)

[Brief Idiosyncrasies Overview](#part0040.xhtml)

[Password Entering & Confirmation](#part0040.xhtml_a5NW)

[Installing and Updating Packages Using Mobile Home Broadband](#part0041.xhtml)

[Wayland GDM3 Graphical Glitches on NVIDIA Graphics Cards](#part0042.xhtml)

[Resolve Missing Packages for a .deb File](#part0043.xhtml)

[Snap .desktop Shortcut Transfer to System-Wide Applications](#part0044.xhtml)

[System Briefly Hangs When Install Battle.net Through Wine-Staging](#part0045.xhtml)

[World of Warcraft Hangs Building Shaders](#part0046.xhtml)

[First Time Logging In To Linux Mint 22](#part0047.xhtml)

[Wayland Compositor NVIDIA Glitches](#part0047.xhtml_a5P4)

[For Other Graphics Cards](#part0048.xhtml)

[Adding a User to the Sudoers File](#part0049.xhtml)

[Suspending Root Account in Linux Mint 22](#part0050.xhtml)

[Modifying /usr/sbin/nologin:](#part0050.xhtml_a5P8)

[Modifying /etc/ssh/sshd_config:](#part0051.xhtml)

[Modifying /etc/shadow:](#part0052.xhtml)

[Linux Mint 22 Repositories](#part0053.xhtml)

[Enabling Linux Mint 22  Repositories](#part0054.xhtml)

[Updating Linux Mint 22](#part0055.xhtml)

[Updating Linux Mint Through Update Manager (GUI)](#part0056.xhtml)

[Updating Linux Mint Through the Command Line](#part0057.xhtml)

[Automating Updates On Linux Mint 22](#part0058.xhtml)

[Disabling Update Notifications](#part0059.xhtml)

[Updating Kernel In Linux Mint 22](#part0060.xhtml)

[Linux Mint 22 Software Sources](#part0061.xhtml)

[Linux Mint 22 Software Manager](#part0062.xhtml)

[APT](#part0062.xhtml_a5PN)

[Setting Software Install as .deb Default](#part0063.xhtml)

[Setting GDebi as Default for .deb](#part0064.xhtml)

[Flatpak](#part0065.xhtml)

[Flatpak Command Line Examples](#part0065.xhtml_a5PT)

[Flathub](#part0066.xhtml)

[Snap](#part0067.xhtml)

[Snap Store](#part0068.xhtml)

[AppImages](#part0069.xhtml)

[pip](#part0070.xhtml)

[Node.js & npm](#part0071.xhtml)

[NVM](#part0072.xhtml)

[NVM Usage Examples](#part0073.xhtml)

[pnpm](#part0074.xhtml)

[Homebrew](#part0075.xhtml)

[Software Security Solutions](#part0076.xhtml)

[UFW (User Friendly Firewall)](#part0077.xhtml)

[UFW TCP & UDP Ports for Online Productivity Services & Gaming](#part0078.xhtml)

[UFW - Single Port Rules](#part0079.xhtml)

[UFW - Multi-Port Rules](#part0080.xhtml)

[UFW - Range Port Rules](#part0081.xhtml)

[UFW - Multi-Port & Range Port Rules](#part0082.xhtml)

[Removing UFW Port Rules](#part0083.xhtml)

[GUFW](#part0084.xhtml)

[GUFW Single Port Rules](#part0085.xhtml)

[GUFW Multi-Port Rules](#part0086.xhtml)

[GUFW Range Port Rules](#part0087.xhtml)

[GUFW Multi-Port Rules & Range Port Rules](#part0088.xhtml)

[GUFW Add Rule From Report](#part0089.xhtml)

[GUFW Remove Port Rules](#part0090.xhtml)

[ClamAV](#part0091.xhtml)

[clamd.conf Command Line & GUI Setup](#part0092.xhtml)

[Automatic ClamAV Updates and Daily Scans](#part0093.xhtml)

[ClamTk](#part0094.xhtml)

[Chkrootkit](#part0095.xhtml)

[Chkrootkit Daily Scans](#part0096.xhtml)

[Rkhunter](#part0097.xhtml)

[Rkhunter Daily Update & Scans](#part0098.xhtml)

[Firejail](#part0099.xhtml)

[Firetools](#part0100.xhtml)

[OSSEC](#part0101.xhtml)

[OSSEC Systemd Service](#part0102.xhtml)

[Alternative DNS Services](#part0103.xhtml)

[Google DNS](#part0104.xhtml)

[Cloudflare DNS](#part0105.xhtml)

[Quad9 DNS](#part0106.xhtml)

[Control D DNS](#part0107.xhtml)

[Ultimate Hosts Blacklist DNS](#part0108.xhtml)

[DNS.WATCH DNS](#part0109.xhtml)

[Hosts](#part0110.xhtml)

[Hosts.deny](#part0111.xhtml)

[Superhosts.deny](#part0112.xhtml)

[Air Gapping](#part0113.xhtml)

[Unplugging Wired & Wireless Network Connections](#part0114.xhtml)

[Removing Unnecessary USB & PS/2 Devices](#part0115.xhtml)

[Get a Technical Professional to Help Remove Internal Network Adapters](#part0116.xhtml)

[Analog Media](#part0117.xhtml)

[Anti EMF Paint](#part0118.xhtml)

[EMF Shielding Fabric](#part0119.xhtml)

[3.5 MM Speakers](#part0120.xhtml)

[USB Keyboard & Mouse](#part0121.xhtml)

[Carrier Pigeons](#part0122.xhtml)

[Learning Ancient Languages](#part0123.xhtml)

[Manual Compiling](#part0124.xhtml)

[Duct Tape For Covering The Webcam & Microphone](#part0125.xhtml)

[Virtual Private Networks](#part0126.xhtml)

[Proton VPN](#part0127.xhtml)

[NordVPN](#part0128.xhtml)

[Private Internet Access](#part0129.xhtml)

[Drivers](#part0130.xhtml)

[NVIDIA](#part0131.xhtml)

[AMD](#part0132.xhtml)

[Radeontop](#part0133.xhtml)

[AMDGPU Fan Configuration Guide](#part0134.xhtml)

[Printer Driver All](#part0135.xhtml)

[Office Suites](#part0136.xhtml)

[LibreOffice](#part0137.xhtml)

[Apache OpenOffice](#part0138.xhtml)

[Apache OpenOffice Desktop Shortcut](#part0139.xhtml)

[Calligra Suite](#part0140.xhtml)

[OnlyOffice](#part0141.xhtml)

[Softmaker FreeOffice](#part0142.xhtml)

[WPS Office](#part0143.xhtml)

[Email Clients](#part0144.xhtml)

[Thunderbird](#part0145.xhtml)

[Betterbird](#part0146.xhtml)

[Mailspring](#part0147.xhtml)

[Image Editing Software](#part0148.xhtml)

[Gnu Image Manipulation Program (GIMP)](#part0149.xhtml)

[Blender](#part0150.xhtml)

[Pinta](#part0151.xhtml)

[Krita](#part0152.xhtml)

[Inkscape](#part0153.xhtml)

[Darktable](#part0154.xhtml)

[Tuxpaint](#part0155.xhtml)

[Audio Editing Software](#part0156.xhtml)

[Audacity](#part0157.xhtml)

[Ardour](#part0158.xhtml)

[MIXXX](#part0159.xhtml)

[Video Editing Software](#part0160.xhtml)

[OpenShot](#part0161.xhtml)

[Kdenlive](#part0162.xhtml)

[Shotcut](#part0163.xhtml)

[Pitivi](#part0164.xhtml)

[Integrated Development Environments (IDE’s)](#part0165.xhtml)

[Visual Studio Code](#part0166.xhtml)

[VSCodium](#part0167.xhtml)

[Atom](#part0168.xhtml)

[Geany](#part0169.xhtml)

[Bluefish](#part0170.xhtml)

[Live Streaming Software](#part0171.xhtml)

[OBS Studio](#part0172.xhtml)

[Owncast](#part0173.xhtml)

[Personal Data Privacy](#part0174.xhtml)

[Searx](#part0175.xhtml)

[OpenStego](#part0176.xhtml)

[Tor Browser Launcher](#part0177.xhtml)

[I2pd](#part0178.xhtml)

[Hyphanet](#part0179.xhtml)

[ZeroNet](#part0180.xhtml)

[Web Browsers](#part0181.xhtml)

[Chromium](#part0182.xhtml)

[Ungoogled-Chromium](#part0183.xhtml)

[Google Chrome](#part0184.xhtml)

[Microsoft Edge](#part0185.xhtml)

[Thorium](#part0186.xhtml)

[Vivaldi](#part0187.xhtml)

[Brave](#part0188.xhtml)

[Firefox](#part0189.xhtml)

[Firefox ESR](#part0190.xhtml)

[Waterfox](#part0191.xhtml)

[LibreWolf](#part0192.xhtml)

[Pale Moon](#part0193.xhtml)

[Mullvad Browser](#part0194.xhtml)

[Basilisk](#part0195.xhtml)

[Password Managers](#part0196.xhtml)

[LastPass](#part0197.xhtml)

[Bitwarden](#part0198.xhtml)

[KeePassXC](#part0199.xhtml)

[Buttercup](#part0200.xhtml)

[Media Players](#part0201.xhtml)

[VLC](#part0202.xhtml)

[SMPlayer](#part0203.xhtml)

[Haruna](#part0204.xhtml)

[Dragon Player](#part0205.xhtml)

[System Utilities](#part0206.xhtml)

[QDirStat](#part0207.xhtml)

[Psensor](#part0208.xhtml)

[Stacer](#part0209.xhtml)

[Bleachbit](#part0210.xhtml)

[SoundConverter](#part0211.xhtml)

[Converseen](#part0212.xhtml)

[GParted](#part0213.xhtml)

[Hardinfo](#part0214.xhtml)

[Gpustat](#part0215.xhtml)

[Czkawka](#part0216.xhtml)

[Instant Messaging](#part0217.xhtml)

[Discord](#part0218.xhtml)

[Skype](#part0219.xhtml)

[Session](#part0220.xhtml)

[Pidgin](#part0221.xhtml)

[Ferdium](#part0222.xhtml)

[Signal](#part0223.xhtml)

[Telegram](#part0224.xhtml)

[Remote Working](#part0225.xhtml)

[Zoom](#part0226.xhtml)

[Slack](#part0227.xhtml)

[Citrix Workspace](#part0228.xhtml)

[Cloud Office Suites](#part0229.xhtml)

[Google Docs Editors Suite](#part0230.xhtml)

[Microsoft 365](#part0231.xhtml)

[Zoho Office Suite](#part0232.xhtml)

[AI Content Generation](#part0233.xhtml)

[Easy Diffusion](#part0234.xhtml)

[oobabooga (Text Generation GUI)](#part0235.xhtml)

[Negative Prompts for Stable Diffusion](#part0236.xhtml)

[Stable Diffusion Web UI](#part0237.xhtml)

[System Settings](#part0238.xhtml)

[Night Light (GNOME)](#part0239.xhtml)

[Night Light (Cinnamon & Redshift)](#part0240.xhtml)

[PipeWire Sound Crackle & Popping Fixes](#part0241.xhtml)

[Linux Mint 22 System Variables](#part0242.xhtml)

[Setting Image As Background In Gnome & Cinnamon](#part0243.xhtml)

[mount_options.conf](#part0244.xhtml)

[Adding Startup Applications In Cinnamon](#part0245.xhtml)

[Adding Startup Applications In GNOME](#part0246.xhtml)

[Auto Mount Partitions Using GNOME Disks](#part0247.xhtml)

[Cinnamon Screenshot Keybindings](#part0248.xhtml)

[GNOME Overview & Windows Keybinds](#part0249.xhtml)

[GNOME Screenshot Keybinds](#part0250.xhtml)

[Default Systemd Timeout](#part0251.xhtml)

[Making Files And Folders Immutable](#part0252.xhtml)

[ffmpegthumbnailer](#part0253.xhtml)

[Removing .desktop files](#part0254.xhtml)

[Power Settings](#part0255.xhtml)

[GNOME Extensions](#part0256.xhtml)

[GNOME Shell Extension Manager](#part0257.xhtml)

[GNOME Shell Integration](#part0258.xhtml)

[User Themes](#part0259.xhtml)

[ArcMenu](#part0260.xhtml)

[Dash to Panel](#part0261.xhtml)

[Desktop Icons (NG)](#part0262.xhtml)

[Tray Icons: Reloaded](#part0263.xhtml)

[Cinnamon Applets](#part0264.xhtml)

[Grouped Window List](#part0265.xhtml)

[Cinnamon Windows Alt-Tab Switcher](#part0266.xhtml)

[Cinnamon Menu Applet](#part0267.xhtml)

[Cinnamon Calendar Applet](#part0268.xhtml)

[Desktop Environments](#part0269.xhtml)

[GNOME](#part0270.xhtml)

[Tasksel](#part0271.xhtml)

[KDE Plasma](#part0272.xhtml)

[LXDE](#part0273.xhtml)

[XFCE](#part0274.xhtml)

[Programming Languages](#part0275.xhtml)

[Zig](#part0276.xhtml)

[Go](#part0277.xhtml)

[Rust](#part0278.xhtml)

[Lua](#part0279.xhtml)

[OpenJava](#part0280.xhtml)

[Imageboards](#part0281.xhtml)

[YChanEx](#part0282.xhtml)

[Ebook Readers](#part0283.xhtml)

[Calibre](#part0284.xhtml)

[Bookworm](#part0285.xhtml)

[Virtualization](#part0286.xhtml)

[Oracle VirtualBox](#part0287.xhtml)

[Virt-manager](#part0288.xhtml)

[Gaming](#part0289.xhtml)

[Wine-Staging](#part0290.xhtml)

[Lutris](#part0291.xhtml)

[ProtonUp-Qt](#part0292.xhtml)

[Steam](#part0293.xhtml)

[DXVK](#part0294.xhtml)

[Vkd3d-proton](#part0295.xhtml)

[World of Warcraft](#part0296.xhtml)

[Battle.net](#part0297.xhtml)

[Possible Fix for Lutris World of Warcraft Black Screen In-Game Store Issue](#part0298.xhtml)

[Possible Fix for WINE-Staging World of Warcraft Black Screen In-Game Store Issue](#part0299.xhtml)

[Possible Fix for DirectX 12 Graphics Error](#part0300.xhtml)

[Retail World of Warcraft Vanilla AddOn Suite](#part0301.xhtml)

[Linux Mint 22 Command Reference](#part0302.xhtml)

[Essential System Commands for File and Directory Management](#part0302.xhtml_a5Y7)

[List Directory Contents](#part0302.xhtml_a5Y8)

[Change Directory](#part0302.xhtml_a5Y9)

[Go Up One Directory Tier](#part0302.xhtml_a5YA)

[List All Non-hidden Files and Folders](#part0302.xhtml_a5YB)

[List All Files and Folders Including Hidden](#part0302.xhtml_a5YC)

[Make a Directory](#part0302.xhtml_a5YD)

[Remove Files](#part0302.xhtml_a5YE)

[Remove Files and Folders Recursively](#part0302.xhtml_a5YF)

[Copy a File to a Destination](#part0302.xhtml_a5YG)

[Copy a Folder to a Destination](#part0302.xhtml_a5YH)

[Move a File or Folder to a Destination](#part0302.xhtml_a5YJ)

[Rename a File or Folder](#part0302.xhtml_a5YK)

[Display File Contents](#part0302.xhtml_a5YM)

[List Parent Directory Contents](#part0302.xhtml_a5YN)

[Mastering APT: Advanced Package Management Techniques](#part0303.xhtml)

[Update Package Lists](#part0303.xhtml_a5YR)

[Upgrade Installed Packages](#part0303.xhtml_a5YS)

[Full Upgrade Installed Packages](#part0303.xhtml_a5YT)

[Package Search](#part0303.xhtml_a5YU)

[Show Package Information](#part0303.xhtml_a5YV)

[Install Packages](#part0303.xhtml_a5YW)

[Remove Packages](#part0303.xhtml_a5YX)

[Purge Packages](#part0303.xhtml_a5YY)

[Auto Remove Packages](#part0303.xhtml_a5YZ)

[List Installed Packages](#part0303.xhtml_a5Z0)

[Add Repository](#part0303.xhtml_a5Z1)

[Remove Repository](#part0303.xhtml_a5Z2)

[Edit Sources File](#part0303.xhtml_a5Z3)

[Fix Broken Dependencies](#part0303.xhtml_a5Z4)

[Retrieve Source Code for a Package](#part0303.xhtml_a5Z5)

[Upgrading the System](#part0303.xhtml_a5Z6)

[Clean Packages](#part0303.xhtml_a5Z7)

[Auto Clean Packages](#part0303.xhtml_a5Z8)

[Hold APT Packages](#part0303.xhtml_a5Z9)

[Unhold APT Packages](#part0303.xhtml_a5ZA)

[Show Held Packages](#part0303.xhtml_a5ZB)

[Package Verification](#part0303.xhtml_a5ZC)

[Mastering Flatpak: Installation, Management, and Beyond](#part0304.xhtml)

[Flatpak Installation](#part0304.xhtml_a5ZE)

[Listing Installed Flatpaks](#part0304.xhtml_a5ZF)

[Updating Flatpaks](#part0304.xhtml_a5ZG)

[Running a Flatpak](#part0304.xhtml_a5ZH)

[Uninstalling Flatpak](#part0304.xhtml_a5ZJ)

[Flatpak Remote Repository List](#part0304.xhtml_a5ZK)

[Adding a Flatpak Remote Repository](#part0304.xhtml_a5ZM)

[Removing a Flatpak Remote Repository](#part0304.xhtml_a5ZN)

[Snap Operations: A Comprehensive Guide to Installing, Managing, and Exploring Snap Applications](#part0305.xhtml)

[Installing a Snap](#part0305.xhtml_a5ZR)

[Listing Installed Snaps](#part0305.xhtml_a5ZS)

[Updating Snaps](#part0305.xhtml_a5ZT)

[Running a Snap](#part0305.xhtml_a5ZU)

[Removing a Snap](#part0305.xhtml_a5ZV)

[Searching for Snaps](#part0305.xhtml_a5ZW)

[Listing Snap Information](#part0305.xhtml_a5ZX)

[Viewing Snap Connections](#part0305.xhtml_a5ZY)

[Mastering File Ownership Modification](#part0306.xhtml)

[File Ownership Modification](#part0306.xhtml_a600)

[Ownership Modification with Recursion](#part0306.xhtml_a601)

[Ownership Modification with Group Specification](#part0306.xhtml_a602)

[Silent Ownership Modification](#part0306.xhtml_a603)

[Verbose Ownership Modification](#part0306.xhtml_a604)

[Interactive Ownership Modification](#part0306.xhtml_a605)

[Ownership Modification with Timestamp Preservation](#part0306.xhtml_a606)

[Mastering File Permissions: A Comprehensive Guide to Managing Access and Security Settings](#part0307.xhtml)

[Change File Permissions](#part0307.xhtml_a608)

[Change Permissions Recursively](#part0307.xhtml_a609)

[Change File Permissions Numerically](#part0307.xhtml_a60A)

[Change Numerical Permissions Recursively](#part0307.xhtml_a60B)

[Change Permissions with Details](#part0307.xhtml_a60C)

[Change Permissions with Confirmation](#part0307.xhtml_a60D)

[Change Permissions with Reference](#part0307.xhtml_a60E)

[Exploring dpkg: A Comprehensive Guide to Package Management](#part0308.xhtml)

[Install .deb Package](#part0308.xhtml_a60G)

[Remove .deb Installed Package](#part0308.xhtml_a60H)

[Remove .deb Package with Config Files](#part0308.xhtml_a60J)

[List Installed Packages](#part0309.xhtml)

[List Files Installed by Package](#part0309.xhtml_a60M)

[Check Package Dependencies](#part0309.xhtml_a60N)

[Reconfigure Installed Package](#part0309.xhtml_a60P)

[Fix Installs Broken by Installed Packages](#part0309.xhtml_a60R)

[Efficient File Retrieval with wget](#part0310.xhtml)

[File Download](#part0310.xhtml_a60T)

[Change Output Filename](#part0310.xhtml_a60U)

[Background File Download](#part0310.xhtml_a60V)

Introduction

Unlock the full potential of Linux Mint 22 with "Mastering Linux Mint 22" This comprehensive guide takes you through every step of the process, from understanding system requirements and pre-installation preparations to mastering advanced features and troubleshooting.

Discover detailed instructions on installing Linux Mint 22, whether using USB or DVD media, and learn how to configure your system for optimal performance. Get insights into resolving common issues, managing software sources, and securing your system with advanced firewall rules and antivirus setups.

Explore a wide array of software options, including office suites, email clients, image and audio editing tools, and development environments. Dive into privacy-focused web browsing, efficient system utilities, and powerful virtualization techniques.

Whether you are a beginner or an experienced user, this book provides everything you need to make the most out of Linux Mint 22\. From first-time setup to daily use, "Mastering Linux Mint 22" is your essential companion for a smooth and productive Linux experience. Get your copy now and start mastering Linux Mint 22 today!

What Is Linux Mint 22?

Linux Mint is a community-driven Linux distribution based on Ubuntu and Debian, comes with a variety of free and open-source applications, and can offer full multimedia support if you include proprietary software like codecs; unlike standard Ubuntu, Linux Mint uses the Cinnamon interface in its most popular edition, featuring a customizable and traditional layout where users can drag applets, create panels, and download new applets, making it highly flexible and user-friendly.

Install Test Machine Details

| Hardware |
| Processor | AMD Ryzen 7 5800X3D 8-Core |
| Graphics | NVIDIA Gigabyte RTX 3060 12GB |
| Memory | 64GB RAM |
| Storage | 3TB SSD with DRAM Cache |
| Display | 1080p Resolution Monitor |
|  |  |

As stated in the above table, the hardware used on the install test machine, which was used to experiment for this book, featured the following:

*   An AMD Ryzen 7 5800X3D CPU with 8 cores and 16 threads.

*   An NVIDIA Gigabyte RTX 3060 12 GB for graphical workloads, chosen for its performance with AI tasks, as discussed in the AI content section later on.

*   64GB of DDR4 RAM from Corsair.

*   Storage included two 1TB QVO Samsung SSDs and a 1TB Netac NVMe SSD.

*   A 21.5” KOORUI monitor with 1080p resolution for display.

System Requirements

| Hardware | Minimum | Recommended |
| Processor | 9th Gen Intel Core or 1st Gen AMD Ryzen Hex or Octa-Core CPU (64-bit) | 10th Gen Intel Core or 2nd Gen AMD Ryzen Hex or Octa-Core CPU (64-bit) |
| Graphics | NVIDIA GTX 1060 6GB or equivalent AMD or Intel graphics card | NVIDIA RTX 2060 6GB or equivalent AMD or Intel graphics card |
| Memory | 16GB RAM | 32GB RAM |
| Storage | 256GB SSD with DRAM Cache | 2X 256GB SSD with DRAM Cache |
| Display | 1080p Resolution Monitor |  |

Minimum

### Processor:

For a decent setup, use at least a 9th Gen Intel Core or 1st Gen AMD Ryzen Hex or Octa-Core CPU (64-bit).

### Graphics:

For graphics, an NVIDIA GTX 1060 6GB or an equivalent AMD or Intel graphics card is needed for acceptable 3D gaming performance.

### Memory:

In terms of memory, 16 GB of DRAM (preferably DDR4) is the minimum recommended. This allows you to run a 3D application, browse the web, and watch videos or streams on YouTube and Twitch simultaneously. With only 8GB of RAM, performance can suffer with just one game and a couple of tabs open.

### Storage:

For storage, a 256GB SSD with a DRAM cache (not SLC) is recommended. A Samsung 850 Evo or better is preferable. Some 3D applications have issues loading textures properly on cacheless or SLC SSDs. Additionally, 256GB provides enough space for the Linux Mint 22 operating system and a large 3D application install.

Recommended

### Processor:

For the best performance, go with at least 10th Gen Intel 6 or 8 Core CPU or a 2nd Gen AMD Ryzen Hex or Octa-Core CPU (64-bit). These provide significant boosts over previous generations.

### Graphics:

At least an RTX 2060 is viable, though I’d personally go for a 3060 RTX 12 GB. The first generation of RTX offers ray tracing, which is becoming more supported on Linux. It's now available in World of Warcraft if you set the right environment variable in the ‘/etc/bash.bashrc’ file, as explained in the ‘Environment Variables’ section of the ‘System Settings’ chapter.

### Memory:

For memory, 32GB RAM is excellent to start with. It lets you run many applications and browser tabs simultaneously. You can even load a local Stable Diffusion AI model and generate images while playing a video game.

### Storage:

Using at least two 256 GB SSDs with a DRAM cache is ideal for a better setup, based on my experience using a Samsung 850 EVO 250GB SSD for World of Warcraft on Ubuntu 20.04\. Based on this I believe that one drive can hold all your Linux Mint 22 data, while the other stores media files, video games, and 3D applications. This way, read/write operations on one drive won’t slow down the other. This setup helps avoid unresponsiveness when transferring large files, unzipping folders with many files, or updating the computer.

System Requirements Explanation

I based both the minimum and recommended system requirements on my experience with various Linux-based operating systems like Ubuntu 20.04 LTS, Linux Mint 22, and Fedora 37\. I also considered the official Linux Mint 22 and World of Warcraft system requirements. You can find more information at the following links:

Linux Mint 22:

[https://blog.linuxmint.com/?p=4731](https://blog.linuxmint.com/?p=4731)

World of Warcraft System Requirements:

[https://eu.battle.net/support/en/article/76459](https://eu.battle.net/support/en/article/76459)

Linux Mint 22 Pre-Install

Downloading the Linux Mint 22 ISO

To Download the Linux Mint 22 ISO file, start by going to the following web address:

[https://www.linuxmint.com/download.php](https://www.linuxmint.com/download.php)

Under, ‘Cinnamon Edition’, Click the download button next to ‘New Features’, then Click a Mirror to download the latest version of the Linux Mint 22 ISO (‘linuxmint-22.0-cinnamon-64bit.iso’ at the time of writing).

Selecting Installation Media

#### USB Drives: Type A and C

Type A USB (3.0) drives are slower but cheaper and more compatible with both old and new devices. They’re easy to use because they fit most ports. On the other hand, Type C USB ports, which can reach speeds up to 10Gbps (double that of Type A), are found on newer computers. Older computers need an extra adapter for Type C, which adds to the cost. Personally, I prefer Type A USB (3.0) drives. They’re more affordable and convenient for me since my USB C port is hard to reach and I lack additional Type C ports.

#### Ventoy

Ventoy, a free and open-source tool, revolutionizes bootable USB drives! Simply copy .iso, .wim, .img, .vhd(x), or .efi files directly onto the drive – no reformatting needed. Ventoy's magic lies in its ability to boot these files directly, whether on a USB stick, hard drive, SSD, or SD card.  It even works with multiple ISO images, letting you choose from a handy boot menu. Legacy BIOS, UEFI, MBR, GPT – Ventoy handles them all, even massive ISO files over 4GB. Windows, Linux, Unix, VMware – the list of supported operating systems is extensive, making Ventoy the ultimate versatile boot solution!

Installing Ventoy And Copying Over The Linux Mint 22 ISO

For Linux Systems:

1.  Visit Ventoy’s GitHub page at: [https://github.com/ventoy/Ventoy/releases](https://github.com/ventoy/Ventoy/releases).
2.  Download the latest file, like ‘ventoy-1.0.98-linux.tar.gz’.
3.  Locate and extract this file in your file explorer.
4.  Open the folder named ‘ventoy-1.0.98’.
5.  Find the file ‘VentoyGUI.x86_64’ inside.
6.  Launch a terminal.
7.  Navigate to the folder with cd ~/Downloads/ventoy-1.0.98.
8.  Check the contents with dir.
9.  Start VentoyGUI with sudo ./VentoyGUI.x86_64.
10.  Select your USB drive in Ventoy.
11.  Save any important USB files elsewhere.
12.  Hit ‘Install’ and approve the action.
13.  Update Ventoy when prompted.
14.  Move the Linux Mint 22 ISO to the Ventoy partition (avoid the EFI partition).

Remember to back up your data.

For Windows Systems:

To set up Ventoy for Linux Mint 22, follow these easy steps:

1.  Go to the Ventoy releases page on GitHub at: [https://github.com/ventoy/Ventoy/releases](https://github.com/ventoy/Ventoy/releases)
2.  Download the ‘ventoy-1.0.98-windows.zip’ for Windows.
3.  Find the ‘ventoy-1.0.98-windows.zip’ file you downloaded.
4.  Open the zip and look for the ‘ventoy-1.0.98’ folder.
5.  Inside, run the ‘Ventoy2Disk’ program.
6.  Click the refresh icon in Ventoy2Disk.
7.  Pick your USB drive from the ‘Device’ list.
8.  Install or update Ventoy on your USB.
9.  Move the Linux Mint 22 ISO file to the Ventoy partition, but not the EFI one.

That’s it! Your USB is now ready for the Linux Mint 22 installation on either Linux or Windows.

DVD-R/RW Discs

DVD-R/RW discs offer a nostalgic charm and are great for archival storage, as they’re less prone to data loss from electromagnetic interference. However, they’re fragile and the storage capacity is limited compared to USB drives. Type A and Type C USBs boast faster data transfer speeds and a sturdier build, making them ideal for frequent use and portability. The downside? They can be pricier and more susceptible to data corruption from viruses or hardware failure. In essence, DVDs are your go-to for long-term storage on a budget, while USBs shine for efficiency and durability in everyday tasks.

#### Brasero

Brasero is a user-friendly GNOME application for burning CDs and DVDs, offering a variety of features for easy and quick disc creation. It supports editing disc contents, multisession, and Joliet extensions, and can write images to the hard drive. For audio CDs, it handles a wide range of formats and allows detailed editing of track silences. Additionally, Brasero can copy discs, save projects, erase rewritable media, and preview multimedia files. Its interface is customizable and supports drag-and-drop actions, ensuring a smooth disc-burning experience.

Installing Brasero And Burning The Linux Mint 22 ISO

To set up Brasero and burn the Linux Mint 22 ISO, follow these steps:

For Debian and Ubuntu:

*   Open the terminal.
*   Type sudo apt install brasero and press Enter.

For Red Hat and Fedora:

*   Open the terminal.
*   Type sudo dnf install brasero and press Enter.

For Gentoo:

*   Open the terminal.
*   Type sudo emerge brasero and press Enter.

For CentOS 8 and older:

*   Open the terminal.
*   Type sudo yum install brasero and press Enter.

For openSUSE:

*   Open the terminal.
*   Type sudo zypper install brasero and press Enter.

For Arch Linux:

*   Open the terminal.
*   Type sudo pacman -S brasero and press Enter.

Next, grab a blank DVD+R disc (4.7GB) and make sure your DVD writer is compatible. Launch Brasero from your applications menu or by typing brasero in the terminal. In Brasero:

*   Choose “Burn image”.
*   Find and select the “linuxmint-22.0-cinnamon-64bit.iso” file.
*   Insert your disc into the drive.
*   Hit “Burn” to begin the process.

CDBurnerXP

CDBurnerXP is a handy tool for burning CDs, DVDs, and Blu-rays, supporting many formats for robust data storage. It crafts audio CDs, bootable media, and spans data over discs. Features include instant burning, verifying data, and saving projects. It also erases, copies, and fetches disc info, creates ISOs, supports LightScribe, and updates in multiple languages.

Installing CDBurnerXP And Burning The Linux Mint 22 ISO

Download and Install CDBurnerXP:

*   Go to the CDBurnerXP website.

[https://www.cdburnerxp.se/](https://www.cdburnerxp.se/)

*   Click on ‘CDBurnerXP’ to find the software.
*   Download the file named ‘cdbxp_setup_4.5.8.7128_x64_minimal.exe’.
*   Open the downloaded file and follow the on-screen instructions.

Burn the Linux Mint 22 ISO:

Insert a blank DVD-R/RW disc into your DVD writer.

Open CDBurnerXP from the Start Menu.

Choose ‘Burn ISO image’ and click ‘Browse’ to select your Linux Mint 22 ISO file.

Tick options like ‘Verify data’ and ‘Finalize disc’.

Press ‘Burn disc’ to begin.

If you run into any problems, the CDBurnerXP site has resources and a support team to help. Enjoy your Linux Mint 22 experience!

Comparing USB and DVD Booting for Linux Mint 22 Installation with Ventoy

To boot and install Linux Mint 22, you can use a Ventoy USB drive or a DVD disc. Each method has different steps:

### Using Ventoy USB Drive:

1.  Boot with Ventoy USB:

    *   Start your PC and boot from the Ventoy USB. Select the USB as the boot device in the BIOS or boot menu.
2.  Select Linux Mint 22 ISO:

    *   Ventoy will display a list of ISOs on the USB. Use the arrow keys to pick the Linux Mint 22 ISO and press ENTER.
3.  Choose Grub Mode:

    *   After selecting Linux Mint 22 ISO, pick the grub mode and press ENTER.
4.  Start Graphical Installer:

    *   Choose the Graphical Installer and press ENTER to begin installing Linux Mint 22.

Using a DVD Disc:

1.  Insert the DVD:

    *   Put the Linux Mint 22 DVD in your drive and restart your PC.
2.  Boot from DVD:

    *   Your PC should boot from the DVD if it’s set as the primary boot device.
3.  Start Installer:

    *   GRUB Installer Select Screen appears, so choose the, Linux Mint 22 option.
    *   The Linux Mint 22 installer starts immediately, without extra menus compared to Ventoy.

These differences help you decide the best way to install Linux Mint 22, based on what you're comfortable with.

Linux Mint 22 Install Guide

Installing Linux Mint 21.3 with the ubiquity-based installer involves selecting your keyboard layout, deciding whether to include multimedia codecs, choosing the type of installation, configuring your timezone, creating a user account, and finally rebooting your computer after installation is complete.

Keyboard Layout

To start installing Linux Mint, double-click on the 'Install Linux Mint' option. When asked to select a keyboard layout, choose the appropriate layout from the left side of the screen, such as 'English (UK)'. Then, pick the corresponding keyboard sub-layout on the right side, also 'English (UK)'. After selecting the correct keyboard layout and sub-layout, click on the 'Continue' button to proceed with the installation.

Multimedia Codecs

To install multimedia codecs, select the checkbox labeled 'Install multimedia codecs' and then click on the 'Continue' button.

Installation Options

In the ubiquity-based Linux Mint 22 Installer, there are three installation options available. The first option, "Install alongside existing operating system," allows you to install Linux Mint 22 alongside another operating system on the same disk without requiring any data removal or partition modification; this is quick and convenient.

The second option, "Erase disk and install Linux Mint," will completely remove all data on the disk and install Linux Mint 22 'Wilma' with predetermined partition sizes; this option is suitable for those who want a fresh installation without preserving any existing data.

The third option, "Something else," provides more advanced features for disk management; it allows you to create, resize, and modify partitions on the selected disk, giving you more control over the partitioning process, including the ability to specify volume sizes and types, and is recommended for users who have a deeper understanding of disk management and want to create a customized and functional system.

While the first two options offer easier installation processes, the "Something else" option provides a more comprehensive understanding of disk management, partitioning, and volume configurations necessary for creating a fully functional Linux Mint 22 'Wilma' system.

Install Alongside & Erase Disk

To complete the installation, click on the "Install Now" button, carefully review any changes to your disks during the installation, and once you have reviewed the changes, click on the "Continue" button to proceed.

Something Else

To set up specific partitions on a 1TB NVME SSD, create a new partition table and ensure the EFI partition is at least 512 MB, allocate 71680 MB for the SWAP partition, and use the remaining free space for the root filesystem partition formatted as an Ext4 journaling file system and mounted at /; review the disk changes and proceed with the installation.

New Partition Table

To create a new partition table, click the '+' symbol to add a new partition, select the disk you wish to partition, and if the selected disk does not have a partition table, click 'New Partition Table', then 'Continue' and choose 'free space' on the disk.

EFI Partition

To set up the EFI partition, click '+' to create a new partition, enter '1024' MB in the 'Size' field, toggle the switches for 'Primary' and 'Beginning of this space' to on, select 'EFI' in the 'Use as' field, and click 'OK' to confirm.

SWAP Partition

To configure the SWAP partition, click '+' to add another partition, enter '71680' MB in the 'Size' field, toggle the switches for 'Primary' and 'Beginning of this space' to on, select 'swap area' in the 'Use as' field, and click 'OK' to confirm.

Root (/) Filesystem Partition:

To create the Root Filesystem partition, click '+' to add a new partition, use the remainder of the free space for 'Size', toggle the switches for 'Primary' and 'Beginning of this space' to on, select 'Ext4 journaling file system' in the 'Use as' field, enter '/' in the 'Mount point' field, and click 'OK' to confirm.

Finalizing Partition Changes

To finalize the installation, click 'Install Now', review the disk changes to ensure they are correct, and then click 'Continue' to proceed with the installation; by following these steps, you can effectively partition your 1TB NVME SSD for optimal performance and organization.

Timezone

To set the timezone, select the desired location on the map or enter the name of the city in the box below the world map, then click on the "Continue" button to proceed.

Creating User Profile

To create a user profile, enter your name in the box labeled "Your name," and the box next to "Your computer's name" will automatically fill in; enter a username in the box labeled "Pick a username," select a secure and memorable password in the box labeled "Choose a password," activate the switch next to "Require my password to log in," and finally, click on the "Continue/Install" button to proceed.

Completing Install Process

Wait patiently until the installation is complete, then click on the "Restart Now" button, and after the restart, remove the USB drive before the motherboard BIOS logo becomes visible.

Setting Linux Mint 22 To Boot

To select a boot entry on an MSI MAG B550 TOMAHAWK motherboard, remove the USB drive and press the designated key (F10 or other) to access the motherboard BIOS. Press the key once, repeatedly, or steadily before the motherboard BIOS logo becomes visible to enter the BIOS.

Once inside the BIOS, navigate to the boot menu options. Locate the USB drive within the boot queue and move it towards the end of the list to ensure the system prioritizes other boot options before attempting to boot from the USB drive.

Switch to Advanced Mode within the BIOS settings. In Advanced Mode, find and select the Settings option, then locate and select the Boot option from the Settings menu.

Within the Boot menu, search for the UEFI Hard Disk Drive Priorities and select the first entry. Use the arrow keys to navigate and highlight the Ubuntu option, then press the ENTER key to confirm the selection of Ubuntu as the desired boot entry.

Save the changes made in the BIOS settings and exit the BIOS to allow the system to restart.

Linux Mint 22 First Login

Begin by selecting the username established during the installation phase and enter the corresponding password, then click on the "Let's go!" button.

Next, locate the switch between the sunrise and sunset symbols to enable dark mode by moving the switch to the right. Find and untick the box next to "Show this dialogue at startup," then click on the ✕ symbol to close the dialogue.

To shut down the Update Manager, navigate to the taskbar, right-click on the Update Manager icon, and select "Quit" to conclude the process. 

Brief Idiosyncrasies Overview

Password Entering & Confirmation

When using commands that need special permissions, like 'su -', 'sudo apt update', or 'sudo snap install', you must enter your password. This is the password set during installation or updated in your account settings. It's a simple step for security!

Example:

example@example:~$ sudo apt update
[sudo] password for example: ********

Installing and Updating Packages Using Mobile Home Broadband

When updating Linux Mint 22 with a mobile home broadband connection, I often can't get all necessary packages in one go. This usually requires redoing the installation and update steps. This issue seems specific to mobile broadband and doesn't occur with ADSL, ADSL 2, FTTC, or FTTP.

Wayland GDM3 Graphical Glitches on NVIDIA Graphics Cards

Using MSI NVIDIA 1060 6GB and Gigabyte NVIDIA RTX 3060 12GB graphics cards, I encountered graphical issues at the gdm3 login screen. This is due to limited compatibility between the default Wayland compositor and NVIDIA cards. The solution is simple: click the cog icon at the screen's bottom right and select "GNOME on Xorg" before logging in. This ensures a glitch-free login experience, as Xorg is more compatible with NVIDIA graphics cards.

Resolve Missing Packages for a .deb File

To install .deb files easily, use:

sudo apt install ./example.deb

This finds and installs any necessary packages for your .deb file.

Snap .desktop Shortcut Transfer to System-Wide Applications

Sometimes, .desktop shortcuts for applications installed through Snap may not be accessible through the application menu or the /usr/share/applications folder.

To make snap applications accessible, follow these steps:

cd /var/lib/snapd/desktop/applications

sudo cp discord_discord.desktop /usr/share/applications

These commands navigate to the directory where the snap .desktop shortcuts are installed and copy them to the system-wide applications folder, ensuring they are accessible through the application menu.

System Briefly Hangs When Install Battle.net Through Wine-Staging

When installing battle.net for the first time through the relevant battle.net setup exe file, the system can hang for a while (sometimes quite a while) before returning to a responsive nature, on the other hand when I install battle.net through Wine and it hangs, I just wait a short while for the hang and then restart the system, before starting the installation process again and it works fine for me from then on.

World of Warcraft Hangs Building Shaders

On occasion World of Warcraft can briefly hang under Linux Mint 22 for the first few times running it (which has been my experience), with my belief being it is the shaders being built, WoW not being made to be run under Wine on Linux Mint 22 or some rumored error with the MSAA options, through I am unsure about the latter due to certain stuttering occurring in World of Warcraft in Windows 11 despite MSAA being turned on or off.

First Time Logging In To Linux Mint 22

Wayland Compositor NVIDIA Glitches

If you have an NVIDIA graphics card and experience graphical glitches, there's a simple fix. After entering your system login, click the cog icon at the bottom right. Choose "GNOME on Xorg" before logging in. Do this for the first login and for subsequent logins. This solution is detailed in the "Wayland GDM3 Graphical Glitches on NVIDIA Graphics Cards" section of the "Brief Idiosyncrasies Overview" chapter.

For Other Graphics Cards

For those using graphics cards other than NVIDIA, logging in is straightforward. Enter the password for the user account you created during setup. This simple step gets you into your system smoothly and quickly.

Adding a User to the Sudoers File

To add a user to the sudoers file, follow these steps:

Open a terminal and switch to the root user:

su -

Add the user to the sudo group:

sudo usermod -aG sudo username

Replace "username" with the desired username.

Exit the root user session:

exit

Reboot the system:

sudo reboot

These steps will grant the user sudo privileges.

Suspending Root Account in Linux Mint 22

Modifying /usr/sbin/nologin:

Open the terminal and execute:

sudo apt install gedit

sudo gedit /etc/passwd

Locate the line starting with:

root:x:0:0:root:/root:/bin/bash

Modify this line to:

root:x:0:0:root:/root:/usr/sbin/nologin

Save the changes by clicking "Save" and then close the editor by clicking the "✕" button, or use CTRL + S and then close the editor.

Modifying /etc/ssh/sshd_config:

Open the terminal and run:

sudo gedit /etc/ssh/sshd_config

Scroll to the end of the sshd_config file.

Add the line:

PermitRootLogin no

If the PermitRootLogin line is already present, change it from:

PermitRootLogin yes

to:

PermitRootLogin no

Save the changes by clicking "Save" and then close the editor by clicking the "✕" button, or use CTRL + S and then close the editor.

Modifying /etc/shadow:

Open the terminal and execute:

sudo gedit /etc/shadow

Locate the line starting with root:.

Add a "!" in front of root:, changing it to:

!root:

Save the changes by clicking "Save" and then close the editor by clicking the "✕" button, or use CTRL + S and then close the editor.

Linux Mint 22 Repositories

In Linux Mint 22, you can manage software sources in two ways. First, use the Software & Updates tool to remove the CD-ROM source, which sometimes blocks updates. Then, you can add more sources to get new software. If you prefer the hands-on approach, open the terminal, edit the sources list with gedit, and disable the CD-ROM line. Add any extra lines you need for more software options. After editing, always refresh your sources to apply the changes.

Enabling Linux Mint 22  Repositories

Visit the official Linux Mint website at [https://linuxmint.com/](https://linuxmint.com/) for all things Linux Mint.

Setting Up Repositories via Sources.list:

Run the following commands in the terminal:

sudo gedit /etc/apt/sources.list

Amend with the following lines:

deb http://archive.ubuntu.com/ubuntu/ noble main restricted universe multiverse

deb-src http://archive.ubuntu.com/ubuntu/ noble main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu/ noble-updates main restricted universe multiverse

deb-src http://archive.ubuntu.com/ubuntu/ noble-updates main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu/ noble-security main restricted universe multiverse

deb-src http://archive.ubuntu.com/ubuntu/ noble-security main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu/ noble-backports main restricted universe multiverse

deb-src http://archive.ubuntu.com/ubuntu/ noble-backports main restricted universe multiverse

Save your changes by clicking “Save” or using the menu options.

Setting Up Repositories via Command Line From The Terminal:

Run the following commands in the terminal:

sudo apt update

sudo apt upgrade

sudo add-apt-repository main universe restricted multiverse

sudo apt update

sudo apt upgrade

Updating Linux Mint 22

Updating Linux Mint 22, known as ‘Wilma’, can be accomplished through two primary methods. The first method is user-friendly, utilizing the graphical interface of the Update Manager. Here, you can simply click a few buttons to initiate the update process. Alternatively, for those comfortable with command-line operations, a series of commands can be executed in the terminal to achieve the same result.

Beyond manual updates, Linux Mint offers the convenience of automatic updates upon system shutdown. This feature is enabled by installing and configuring the unattended-upgrades package. Once set up, this package ensures your system remains up-to-date automatically, eliminating the need for manual intervention.

If you find the frequency of update notifications intrusive, Linux Mint provides a solution for this as well. You can partially disable these notifications by adjusting the settings of the Update Manager in the Startup Applications. This customization allows you to control the level and frequency of update notifications according to your preference.

For users interested in more advanced customization, such as changing or updating the Linux Mint kernel, guidance is available through the official repositories provided by the Linux Mark Institute. These repositories offer the necessary resources and instructions for safely updating and changing the kernel, ensuring compatibility and stability for your system.

In summary, Linux Mint 21.3 offers a flexible and user-friendly approach to system updates, whether you prefer a graphical interface, command-line methods, automatic updates, or custom kernel modifications. Each option is designed to cater to different user needs and preferences, ensuring a smooth and secure operating experience.

Updating Linux Mint Through Update Manager (GUI)

1.  Launch Update Manager: Open the Update Manager from the application menu.
2.  Continue Prompt: Click on "Continue" when prompted.
3.  Local Mirror Option: Next to "Do you want to switch to a local mirror," click on "Yes."
4.  Close Prompt: Close the prompt by clicking on the "X" button.
5.  Refresh Package List: Click on "Refresh" to update the package list.
6.  Select Update: Choose an update, such as "vim."
7.  Read Description: Click on the "Description" tab to read the software package's description.
8.  Review Packages: Switch to the "Packages" tab to review the installed packages affected by the update and the total update size in KB.
9.  Check Changelog: Go to the "Changelog" tab to see the update's changes.
10.  Select Update for Installation: Tick the box next to the update you want to carry out.
11.  Install Updates: Click on "Install Updates" to begin the installation.
12.  Wait for Application: Wait for the changes to be applied.
13.  Refresh Again: Click on "Refresh" again.

Close Update Manager: Close the Update Manager by clicking on the "X" button.

Updating Linux Mint Through the Command Line

To update your system using the terminal:

Run the following commands:

sudo apt update

sudo apt upgrade

To issue an upgrade command with pre-approved confirmation, run:

sudo apt update && sudo apt upgrade -y

Automating Updates On Linux Mint 22

To set up unattended updates in Linux Mint 22, follow these steps:

1.  Open the terminal and run:

sudo apt update

sudo apt install unattended-upgrades

sudo nano /etc/apt/apt.conf.d/50unattended-upgrades

2.  Edit the 50unattended-upgrades file with the following contents:

Unattended-Upgrade::Origins-Pattern {

"origin=Debian,codename=${distro_codename},label=Debian";
   "origin=Debian,codename=${distro_codename},label=Debian-Security";

"origin=Debian,codename=${distro_codename}-security,label=Debian-Security";
};

Unattended-Upgrade::InstallOnShutdown "true";

Unattended-Upgrade::Remove-Unused-Dependencies "true";

Unattended-Upgrade::OnlyOnACPower "true";

3.  Save by pressing CTRL + S, then exit by pressing CTRL + X.
4.  Run the following command:

sudo nano /etc/apt/apt.conf.d/10periodic

5.  Edit the 10periodic file with the following contents:

APT::Periodic::Update-Package-Lists "1";

APT::Periodic::Download-Upgradeable-Packages "1";

APT::Periodic::AutocleanInterval "7";

APT::Periodic::Unattended-Upgrade "1";

6.  Save by pressing CTRL + S, then exit by pressing CTRL + X.
7.  Run the following commands:

cd /etc/systemd

sudo nano logind.conf

8.  Edit the logind.conf file with the following content:

InhibitDelayMaxSec=1800

9.  Save by pressing CTRL + S, then exit by pressing CTRL + X.
10.  Finally, run these commands to enable and start unattended upgrades:

sudo systemctl enable unattended-upgrades

sudo systemctl start unattended-upgrades

sudo systemctl status unattended-upgrades

These steps will install, configure, start, and check the status of automatic updates on Linux Mint 22.

Disabling Update Notifications

1.  Open Startup Applications: Access this from the application menu.
2.  Disable Update Manager: Find "Update Manager" and turn off its switch.
3.  Close Window: Click on the "X" button to close.

Updating Kernel In Linux Mint 22

For more information about the Linux kernel in general consult the official website at [https://www.kernel.org/](https://www.kernel.org/).

Updating Linux Mint Kernel via GUI:

1.  Access Update Manager: Open it from the application menu.
2.  View Kernels: Click on "View" and then select "Kernels."
3.  Select Kernel: Choose the highest kernel number available.
4.  Install Kernel: Click on "Install."

Complete Installation: After installation, click on "Close."

Linux Mint 22 Software Sources

Linux Mint 22 Software Sources aim to provide users with access to a wide range of software without needing virtualization tools. This ensures that users can install and run software easily, without relying on applications that emulate filesystems from other Linux distributions like Arch, Ubuntu, or openSUSE Tumbleweed, such as distrobox and BoxBuddy.

The Linux Mint Software Manager lets you easily manage apps. It’s a user-friendly GUI that comes pre-installed. With access to many open-source and proprietary apps, you can install, update, and remove software quickly. Its clean, intuitive interface is great for Linux newbies, and its powerful search feature makes finding apps a breeze.

APT stands for Advanced Package Tool, a powerful utility for managing software on Debian and its derivatives. It installs, updates, and removes software packages. APT uses repositories, which are directories of software. You can use APT with sudo to gain superuser privileges for more control.

Setting Software Install as the default for .rpm files allows you to easily open and install them with a double-click, making it much more user-friendly than using the command line.

Setting GDebi as the default for .deb files details how to set GDebi as the default application. Unlike Software Install, GDebi automatically fetches the required packages, avoiding the need to run sudo dpkg -i and sudo apt install -f commands.

Flatpak covers the installation of the Flatpak protocol on Linux Mint 22, including the addition of the Flatpak plugin for GNOME Software. This makes browsing and installing Flatpak applications easier without using a web browser. It also includes basic Flatpak command line operations like adding, listing, and removing applications.

Flathub explains how to add the Flatpak Flathub repository to Linux Mint 22, providing access to a vast repository of Flatpak applications. With the Flatpak plugin for GNOME Software, users can easily browse and install these applications.

Snap demonstrates how to install the Snap protocol on Linux Mint 22, providing command line access to Canonical’s Snapstore, which includes thousands of applications like Discord, Steam, and Visual Studio Code. It also details managing snaps, including installation, removal, .desktop shortcut creation, and total removal from the system. Additionally, it shows how to install the graphical Snap Store.

.AppImages explains how to make .AppImage files executable using the Nautilus file manager in GNOME 46 the default desktop environment of Linux Mint 22\. It also provides an example of creating a .desktop shortcut for the Curseforge .AppImage and an overview of the fields in a .desktop file.

AppImageLauncher provides an in-depth look at obtaining and installing the latest compatible .rpm file for AppImageLauncher.

pip describes how to install pip, the package manager that connects to the Python Packaging Index (PyPI), allowing users to install software from PyPI through the command line.

Node.js & npm details installing Node.js (a JavaScript runtime) and npm (Node Package Manager) using the APT command line.

NVM shows how to install the Node Version Manager (NVM), allowing users to install and use different versions of Node.js and npm individually. It provides practical examples of using specific versions through NVM.

pnpm illustrates how to install pnpm (Performant npm), a different package manager for Node.js. It explains installing pnpm using curl and sh commands in the terminal and emphasizes its role in centralizing packages in a global repository.

Linux Mint 22 Software Manager

To install applications using the Software Manager, follow these steps:

1.  Click on the desired application in the Software Manager.
2.  Click the 'Install' button.

Alternatively, you can use the search bar to find a program by typing its name, for example, 'vlc,' and then clicking on the application and 'Install.'

You can also choose different software sources for an application by:

1.  Browsing through the front page or category pages.
2.  Using the search bar to find the application, such as 'SMPlayer.'
3.  Clicking on the application.
4.  Pressing the drop-down box below the 'Install' button.

Available options may include Linux Mint, Ubuntu, and Flatpak (Flathub). Once you've selected your desired source from the options presented, click 'Install.'

To remove installed applications using the Software Manager:

1.  Go to the 'Installed' tab in the Software Manager.
2.  Locate the application you wish to uninstall or remove.
3.  Click 'Uninstall' next to the application.

APT

Visit the official APT website at [https://wiki.debian.org/Apt](https://wiki.debian.org/Apt) for more information.

1.  Update Package Lists and Repositories:

◦         To update the APT package lists and repositories, run the following command:

▪         sudo apt update

2.  Upgrade APT Packages:

◦         Upgrade APT packages by running the following command:

▪         sudo apt update && sudo apt upgrade -y

3.  Remove APT Packages:

◦         To remove or uninstall APT packages, use the following command:

▪         sudo apt remove package-name

4.  Purge APT Packages:

◦         Purge APT packages entirely by running the following command:

▪         sudo apt purge package-name

5.  Remove 3rd Party Repository .list Files:

◦         To remove individual .list files from 3rd party repositories, navigate to the directory containing these files:

▪         cd /etc/apt/sources.list.d

◦         Then, remove the specific .list file (e.g., xanmod.list) and update APT sources:

▪         sudo rm -r file-name && sudo apt update

6.  Remove Leftover Packages:

◦         To remove leftover packages, run the following command:

sudo apt autoremove

Setting Software Install as .deb Default

Open the Files application from the application menu.

Press CTRL + L to activate the location entry in the file path entry box.

Type ~/Downloads and press Enter to navigate to the Downloads directory.

Select a .rpm file, for example, google-chrome-stable_current_amd64.deb.

Right-click on the .deb file and choose "Open With".

Select "Software Install".

Move the switch next to "Always use for this file type" (rpm package) to the right.

Click "Open

Setting GDebi as Default for .deb

1.  Open the terminal and run:

sudo apt install gdebi

2.  Open the Files application from the application menu.
3.  Press CTRL + L to activate the location entry in the file path entry box.
4.  Type ~/Downloads and press Enter to navigate to the Downloads directory.
5.  Select a .deb file, for example, openstego_0.8.6-1_all.deb.
6.  Right-click on the .deb file and choose "Open With".
7.  Select "GDebi Package Installer".
8.  Move the switch next to "Always use for this file type" (Debian package) to the right.
9.  Click "Open".

Flatpak

Visit the official Flatpak website at [https://www.flatpak.org/](https://www.flatpak.org/) for more information.

Installing Flatpak via APT in the Terminal

sudo apt update

sudo apt install flatpak

sudo apt install gnome-software-plugin-flatpak

### Flatpak Command Line Examples

To install a Flatpak app, run:

flatpak install flathub ch.tigerjython.TigerJython2

To remove a Flatpak app, run:

flatpak remove ch.tigerjython.TigerJython2

To delete Flatpak repositories, run:

flatpak remotes

flatpak remote-delete flathub

To remove Flatpak from Linux Mint 22 ‘Wilma’, run:

sudo apt purge flatpak gnome-software-plugin-flatpak

Flathub

Visit the official Flathub website at [https://flathub.org/](https://flathub.org/) for more information.

To add the Flathub repository, run the following command in the terminal:

flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

Snap

Visit the official Snap website at [https://snapcraft.io/](https://snapcraft.io/) for more information.

To install Snap, run the following commands in the terminal:

1.  Move the existing 'nosnap.pref' file to a backup location in your 'Documents' directory with the following commands:

◦         sudo mv /etc/apt/preferences.d/nosnap.pref ~/Documents/nosnap.backup

2.  Update your package list to ensure you have the latest information:

◦         sudo apt update

3.  Install Snapd by executing the following command:

◦         sudo apt install snapd

Once Snap is installed, you can work with Snap packages as follows:

◦         To install Snap packages, you can use the Snap Store graphical interface or the command line.

◦         For instance, to install Discord, use the following command:

▪         sudo snap install discord

◦ To uninstall Snap packages, you have the option to use the Snap Store's graphical interface or the command line.

◦         For example, to remove Chromium, execute the following command:

▪         sudo snap remove chromium

Snap Store

Visit the official Snap Store website at [https://snapcraft.io/](https://snapcraft.io/) for more information.

To install Snap, run the following commands in the terminal:

sudo snap install core

sudo snap install snap-store

AppImages

Visit the official .AppImage website at [https://appimage.org/](https://appimage.org/) for more information.

Set .AppImage as Executable in a GUI:

Open the Files application from the application menu.

Activate Location Entry by pressing CTRL + L.

Enter ~/ to access the home directory and press Enter.

Right-click on an empty space and select "New Folder".

Type "Applications" and click Create.

Drag and drop Bazecor-1.4.0-rc.4-x64.AppImage from the ~/Downloads directory to the ~/Applications directory.

Navigate to ~/Applications.

Right-click Bazecor-1.4.0-rc.4-x64.AppImage and select "Properties".

In the Properties window, enable the "Executable as Program" option by moving the switch to the right.

Double-click Bazecor-1.4.0-rc.4-x64.AppImage to run it.

To make the file immutable (optional), run the following command in the terminal while in the ~/Applications directory:

sudo chattr +i -RV Bazecor-1.4.0-rc.4-x64.AppImage

pip

Visit the official pip website at [https://pypi.org/project/pip/](https://pypi.org/project/pip/) for more information.

To install pip, run the following commands in the terminal:

sudo apt update

sudo apt install pip

To check the installed pip version, run:

pip3 --version

Node.js & npm

Visit the official Node.js and npm websites at [https://nodejs.org/](https://nodejs.org/) and [https://www.npmjs.com/](https://www.npmjs.com/) for more information.

To install Node.js and npm, run the following command in the terminal:

sudo apt install nodejs npm

NVM

Visit the official NVM website at [https://github.com/nvm-sh/nvm/](https://github.com/nvm-sh/nvm/) for more information.

To install NVM, run the following commands in the terminal:

sudo apt  update

sudo apt  install curl wget

To check the installed versions of curl and wget run:

curl --version

wget --version

If using curl, run:

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

If using wget, run:

wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

To add NVM to the profile file, run:

export NVM_DIR="$HOME/.nvm"

[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

NVM Usage Examples

To install a specific version of Node.js and npm on a user level, run:

nvm install 16

To use a specific version of Node.js and npm on a user level, run:

nvm use 16

pnpm

Visit the official pnpm website at [https://pnpm.io/](https://pnpm.io/) for more information.

To install pnpm, run the following commands in the terminal:

sudo apt update

If using curl, run:

curl -fsSL https://get.pnpm.io/install.sh | sh -

If using wget, run:

wget -qO- https://get.pnpm.io/install.sh | sh -

Once command has been executed:

Follow the in-terminal directions.

Homebrew

Visit the official Homebrew website at [https://brew.sh/](https://brew.sh/) for more information.

To install Homebrew, run the following commands in the terminal:

sudo apt update

sudo apt install git

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
(echo; echo 'eval

Follow the directions given in the terminal.

To install a recommended application ‘Homebrew’ run:

brew install gcc

Software Security Solutions

Software Security Solutions stresses the need to protect both software and hardware on personal computers running Linux Mint 22\. It’s vital to ensure your system is secure. They focus on providing top-notch security measures, emphasizing the importance of safeguarding your digital environment. With their expertise, users can trust that their computing systems are well-protected. Linux Mint 22, known for its robustness, pairs well with these security practices. Users can enjoy a seamless, secure computing experience without worrying about threats.

UFW (User Friendly Firewall) UFW provides a user-friendly command line interface for the iptables firewall included with the Linux 6.8 kernel in Linux Mint 22\. It explains how to install and configure UFW using the apt command line, including port forwarding for various online services and games. Detailed instructions are provided for setting up custom UFW rules, adding and deleting port rules, and listing them by number.

GUFW (Graphical User Friendly Firewall) GUFW is the graphical interface for UFW, making it even easier to manage the iptables firewall. It allows you to add, edit, and remove single, range, and multi-port rules through a simple graphical interface.

ClamAV and ClamTk ClamAV is a command line utility for scanning files manually, on a schedule, or on access. ClamTk provides a graphical interface for ClamAV, making it easier to configure, check scan history, and manage quarantined files. You can also scan directories by right-clicking with ClamTk.

chkrootkit chkrootkit is a command line utility that scans for rootkits on the system. It displays results in the terminal or logs them to a file via a cron job. While it cannot remove rootkits, it helps identify them for further action.

rkhunter rkhunter is another command line tool for scanning and removing rootkits. It can be configured for daily updates and scans, automatically handling rootkits and suspect files.

Firejail and Firetools Firejail is a command line tool for sandboxing applications, isolating them from the rest of the system. Firetools provides a graphical interface for configuring and launching sandboxed applications, making it easier to use Firejail.

OSSEC (Open Source HIDS SECurity) OSSEC is an open-source Host-Based Intrusion Detection System (HIDS). It explains how to install OSSEC, create a systemd service for it, and monitor processes and software packages on workstations and servers.

DNS Over TLS This section covers installing and setting up DNS Over TLS to protect against MITM (Man In The Middle) attacks. It encrypts DNS requests using TLS 128-bit encryption, ensuring secure communication with a no-log DNS server like Quad9 with Malware Blocking and DNSSEC.

Alternative DNS Services Provides information on no-log DNS services such as Google DNS, Cloudflare DNS, Quad9 DNS, CONTROL D DNS, Ultimate Hosts Blacklist DNS, and DNS.WATCH, including their names, official web addresses, and IPv4 and IPv6 addresses.

Hosts Explains how to locate, obtain, and install a custom hosts file to map hostnames to IP addresses. It includes steps for backing up the existing hosts file and setting proper ownership and permissions.

hosts.deny Details how to use the hosts.deny file to block connections from specific IP addresses, hostnames, or domains. It covers backing up the existing file and installing a custom hosts.deny file with the correct permissions.

superhosts.deny Similar to hosts.deny, superhosts.deny is a more extensive version for blocking connections from a broader range of IP addresses, hostnames, or domains. It explains how to back up, obtain, and install a custom superhosts.deny file with the correct ownership and permissions.

UFW (User Friendly Firewall)

Visit the official UFW (User Friendly Firewall) website at [https://help.ubuntu.com/community/UFW](https://help.ubuntu.com/community/UFW) for more information.

To install UFW (User Friendly Firewall), run the following commands in the terminal:

sudo apt purge ufw

cd /etc

sudo rm -r ufw

cd

sudo apt update && sudo apt upgrade

sudo apt install ufw

UFW TCP & UDP Ports for Online Productivity Services & Gaming

#### TCP Ports:

53, 80, 433, 443, 1119, 1120, 1716, 1935, 2099, 3074, 3075, 3216, 3478, 3479, 3569, 3724, 4000, 5060, 5062, 5222, 5223, 6012, 6112-6114, 6250, 8080, 8088, 8094, 8097, 9946, 9988, 14000-14024, 17502-17504, 18000-18120, 22990, 27900, 29810, 29900, 42124-42130, 20000-20100, 25000-25099, 27014-27050, 30000-30099, 42100-42200, 6112-6119, 6113-6119, 7777-7780, 8393-8400, 9960-9969

#### UDP Ports:

67, 68, 80, 443, 546, 631, 1119, 1120, 1716, 3074, 3126, 3478, 3659, 3724, 4000, 5060, 5062, 6012, 6112-6114, 6120, 6250, 8080, 8088, 8125, 9565, 9570, 18000, 27036, 29900, 10000-19999, 1024-1124, 1119-1120, 12000-64000, 14000-14016, 21000-26000, 22990-23006, 25000-25099, 25200-25300, 27000-27031, 30000-30099, 3074-3083, 3478-3479, 37000-40000, 4379-4380, 5000-5500, 6112-6119, 9000-9999

I compiled these lists of TCP and UDP ports by researching the help sections and forums of major gaming companies like Blizzard, Activision, Microsoft, Electronic Arts, Riot, and Amazon.

UFW - Single Port Rules

To allow single port rules in UFW, run the following commands in the terminal:

#### TCP Ports:

sudo ufw allow 80/tcp

#### UDP Ports:

sudo ufw allow 80/udp

UFW - Multi-Port Rules

To allow multiple ports in UFW, run the following commands in the terminal:

#### TCP Ports:

sudo ufw allow 80,443/tcp

#### UDP Ports:

sudo ufw allow 80,443/udp

UFW - Range Port Rules

To allow a range of ports in UFW, run the following commands in the terminal:

#### TCP Ports:

sudo ufw allow 1119:1120/tcp

#### UDP Ports:

sudo ufw allow 1119:1120/udp

UFW - Multi-Port & Range Port Rules

To allow multiple ports and port ranges in UFW, run the following commands in the terminal:

#### TCP Ports:

sudo ufw allow 80,443,1119:1120/tcp

#### UDP Ports:

sudo ufw allow 80,443,1119:1120/udp

#### UFW Ports Status

To check the status of UFW ports, run:

sudo ufw status

Removing UFW Port Rules

To remove UFW port rules, run the following commands in the terminal:

1.  List all current UFW rules by their order:

sudo ufw status numbered

2.  Delete a specific UFW rule by its number (replace 33 with the actual rule number you want to delete):

sudo ufw delete 33

3.  Verify that the rule has been deleted by listing all UFW rules again:

sudo ufw status numbered

GUFW

Visit the official GUFW website at [https://costales.github.io/projects/gufw/](https://costales.github.io/projects/gufw/) for more information.

Installing GUFW via GNOME Software:

1.  Open GNOME Software and search for GUFW.
2.  Click on "Firewall Configuration".
3.  In the Source Selection Box, choose "System Package".
4.  Click "Install".

Installing GUFW via APT in the Terminal:

To install GUFW using APT, run the following commands:

sudo apt update && sudo apt upgrade

sudo apt install gufw

GUFW Single Port Rules

To set up a single port rule in GUFW, follow these steps:

Open GUFW from the application menu, identified as "Firewall Configuration."

In the "Profile" box, select "Home."

Activate the firewall by toggling the "Status" switch to the right.

For "Incoming" traffic, choose "Deny" from the dropdown box.

For "Outgoing" traffic, select "Allow."

Navigate to the "Rules" section and click the "+" button to add a new rule.

Go to the "Simple" tab.

In the "Name" box, enter "HTTP."

From the "Policy" dropdown, select "Allow."

Under "Direction," choose "In" for incoming traffic.

For the protocol, select "Both" for both TCP and UDP, "TCP" for only TCP, or "UDP" for only UDP.

In the "Port" box, enter "80."

Click "Add" to apply the rule.

This method allows you to efficiently manage port rules in GUFW, ensuring your firewall settings are correctly configured for your needs.

GUFW Multi-Port Rules

To configure rules for multiple ports in GUFW, follow these steps:

Open GUFW from the application menu, ensuring you select "Firewall Configuration."

Navigate to the "Rules" section and click the "+" button to add a new rule.

Select the "Simple" tab within the rule creation window.

In the "Name" field, enter a descriptive name, such as "HTTP/HTTPS."

Choose "Allow" from the "Policy" dropdown menu to permit traffic.

Set the "Direction" to "In" for incoming rules.

For the "Protocol," select "Both" if both TCP and UDP are needed, "TCP" for TCP only, or "UDP" for UDP only, based on your requirements.

In the "Port" field, input the ports you wish to allow, separated by a comma, for example, "80,443."

Click "Add" to finalize and apply the rule.

This method enables you to set up firewall rules for multiple ports in GUFW, streamlining the management of network traffic for your system.

GUFW Range Port Rules

To implement range port rules in GUFW, follow these steps:

Open GUFW from your application menu, selecting "Firewall Configuration."

Navigate to the "Rules" section and press the "+" button to create a new rule.

Switch to the "Simple" tab in the rule creation window.

Enter a name for your rule in the "Name" field, like "HTTP Range."

Select "Allow" from the "Policy" dropdown to permit traffic.

Choose "In" from the "Direction" dropdown for incoming traffic.

Select "TCP" if you're setting up TCP ports, or "UDP" for UDP ports, based on your needs.

In the "Port" field, specify the range of ports you wish to open, for instance, "1112:1114."

Click "Add" to apply and save your new range port rule.

This method allows you to efficiently manage port ranges within GUFW, providing precise control over your network traffic permissions.

GUFW Multi-Port Rules & Range Port Rules

To configure rules for multiple ports and port ranges in GUFW, follow these steps:

Launch GUFW from your application menu, selecting "Firewall Configuration."

Navigate to the "Rules" section and click the "+" button to add a new rule.

Select the "Simple" tab in the rule creation window.

In the "Name" field, enter a descriptive name like "HTTP."

Choose "Allow" from the "Policy" dropdown menu to enable traffic.

Set the "Direction" to "In" for incoming rules.

For the protocol, choose "TCP" for TCP ports or "UDP" for UDP ports, based on your requirement.

In the "Port" field, input the ports and ranges you need to open, for example, "1111,22:24."

Click "Add" to apply the rule.

This approach allows you to easily manage both individual ports and ranges within GUFW, ensuring your firewall configurations are precise and tailored to your network's needs.

GUFW Add Rule From Report

To add a firewall rule based on a report in GUFW, follow these steps:

Open GUFW from your application menu, selecting "Firewall Configuration."

Navigate to the "Report" section.

Choose a rule number from the list provided.

Click the "+" button to initiate adding the rule.

Confirm by clicking "Add."

This method allows you to efficiently implement firewall rules directly from GUFW reports, streamlining the management of your network security settings.

GUFW Remove Port Rules

To delete a port rule in GUFW, follow these steps:

Open GUFW from your application menu, selecting "Firewall Configuration."

Navigate to the "Rules" tab.

Highlight the rule you intend to remove by selecting its number.

Click the "-" button to delete the rule.

Please double-check that you have selected the correct rule before deleting, as GUFW does not prompt for confirmation upon removal.

ClamAV

Visit the official ClamAV website at [https://www.clamav.net/](https://www.clamav.net/) for more information.

Installing ClamAV via APT in the Terminal:

sudo apt update

sudo apt install clamav clamav-daemon

clamd.conf Command Line & GUI Setup

To configure clamd with the command line and GUI, follow these steps:

Open the clamd configuration file by executing in the terminal:

sudo gedit /etc/clamav/clamd.conf

Update the clamd.conf file starting from the OnAccessMaxFileSize line:

OnAccessMaxFileSize 101M

ScanOnAccess yes

OnAccessIncludePath /

OnAccessExcludePath /home/.wine /mnt

OnAccessPrevention yes

Save your changes by clicking "Save".

Create the clamav directory:

sudo mkdir /run/clamav

Set the directory permissions to allow reading, writing, and execution:

sudo chmod 777 -R /run/clamav

Start the clamd service:

sudo clamd

After starting clamd, secure the directory by changing permissions back:

sudo chmod 755 -R /run/clamav/

Automatic ClamAV Updates and Daily Scans

To set up automatic updates and scans with ClamAV, follow these steps in the terminal:

Open the crontab file for editing:

sudo crontab -e

Choose the editor number for nano when prompted.

Add the following lines to the crontab file to configure the scheduled tasks:

For updating the ClamAV database daily at 11:00 PM:

2 3 * * * /usr/bin/freshclam

For performing a daily scan at midnight targeting specific directories, logging the process, and removing any detected infected files:

0 0 * * * /usr/bin/clamscan --log --infected --remove -r /home /usr /etc /bin /sbin

Save your changes by pressing CTRL + S and exit by pressing CTRL + X.

This setup ensures your ClamAV database is regularly updated, and your system is scanned daily for any threats, enhancing your security measures.

ClamTk

Visit the official ClamTk website at [https://github.com/dave-theunsub/clamtk](https://github.com/dave-theunsub/clamtk) for more information.

Installing ClamTk via DEB/FLATPAK Package through GNOME Software:

1.  Open GNOME Software and search for ClamTk.
2.  Click on ClamTk, then on the Source Selection Box.
3.  Choose DEB or FLATPAK and click Install.

Installing ClamTk via APT in the Terminal:

To install ClamTk, type these commands:

sudo apt update && sudo apt upgrade

sudo apt install clamtk

Installing ClamTk via FLATPAK in the Terminal:

To install via FLATPAK, type this command:

flatpak install flathub com.gitlab.davem.ClamTk

Chkrootkit

Visit the official chkrootkit website at [https://www.chkrootkit.org/](https://www.chkrootkit.org/) for more information.

Installing Chkrootkit via APT in the Terminal:

To install Chkrootkit, type these commands:

sudo apt update

sudo apt install chkrootkit

Chkrootkit Daily Scans

To schedule daily chkrootkit scans, open your terminal and run:

sudo crontab -e

In the crontab file, insert the following line:

2 22 * * * /usr/sbin/chkrootkit -x -q -r / >> /var/log/chkrootkit.log 2>&1

This command configures a daily scan at 10:02 PM, quietly logging the results to /var/log/chkrootkit.log. Save your changes by pressing CTRL + S, then exit with CTRL + X.

Rkhunter

Visit the official Rkhunter website at [https://sourceforge.net/projects/rkhunter/](https://sourceforge.net/projects/rkhunter/) for more information.

Installing Rkhunter via APT in the Terminal:

To install Rkhunter, type these commands:

sudo apt update

sudo apt install rkhunter

If a dialog box appears concerning postfix, choose the "No Configuration" option and proceed.

Rkhunter Daily Update & Scans

To set up daily updates and scans with rkhunter, open your terminal and type:

sudo crontab -e

In the crontab file, add the following line:

2 21 * * * /usr/local/bin/rkhunter --cronjob --update --quiet --remove

This schedules rkhunter to update and run a quiet scan daily at 9:02 PM, maintaining your system's security without intrusive notifications. Save your modifications by pressing CTRL + S and exit using CTRL + X.

Firejail

Visit the official Firejail website at [https://firejail.wordpress.com/](https://firejail.wordpress.com/) for all things Firejail.

Installing Firejail via APT in the Terminal:

Type these commands:

sudo apt update

sudo apt install firejail

Firetools

Visit the official Firetools website at [https://github.com/netblue30/firetools](https://github.com/netblue30/firetools) for more information about Firetools.

Installing Firetools via DEB package through GNOME Software:

1.  Open GNOME Software and search for Firetools.
2.  Click on Firetools, then on the Source Selection Box.
3.  Choose System Package or FLATPAK and hit Install.

Installing Firetools via APT in the Terminal:

Type these commands:

sudo apt update && sudo apt upgrade

sudo apt install firejail firetools

OSSEC

Visit the official OSSEC website at [https://www.ossec.net/](https://www.ossec.net/) for all things OSSEC.

Installing OSSEC via APT in the Terminal:

To install OSSEC, open your terminal and execute the following command to install the necessary dependencies:

sudo apt-get install make gcc libc6-dev libssl-dev zlib1g-dev libpcre2-dev libevent-dev build-essential zlib1g-dev libpcre2-dev libsqlite3-dev libssl-dev libevent-dev libsystemd-dev curl wget git libxslt-dev python3-dev python3-babel python3-venv python3-pip

Next, install the version 16 of Node.js & Npm using your Node Version Manager (NVM):

nvm install 16

Next, set your Node Version Manager (NVM) to use version 16:

nvm use 16

Download OSSEC version 3.7.0 using wget:

wget https://github.com/ossec/ossec-hids/archive/refs/tags/3.7.0.tar.gz

Extract the downloaded archive:

tar -xzvf 3.7.0.tar.gz

Navigate into the OSSEC directory:

cd ossec-hids-3.7.0

Initiate the installation script:

sudo ./install.sh

During the installation, follow these instructions:

Select English by typing en and press Enter.

Choose the local installation type by typing local and specify the installation path as /var/ossec.

Respond with n for the first question and y for the subsequent ones to accept the defaults, apart from the email and adding additional IPs to the whitelist. You can skip the email notification and the additional whitelist IPs features if you prefer.

Confirm your choices by pressing Enter at the end.

OSSEC Systemd Service

Begin by opening your terminal and entering the following command to edit the OSSEC service file:

sudo gedit /etc/systemd/system/ossec.service

In the ossec.service file, insert the following configuration:

[Unit]

Description=OSSEC service

After=network.target

[Service]

Type=simple

ExecStart=/var/ossec/bin/ossec-control start

ExecStop=/var/ossec/bin/ossec-control stop

TimeoutStartSec=0

Restart=on-failure

StartLimitInterval=0

[Install]

WantedBy=multi-user.target

Save your changes and close the editor.

Next, execute these commands in the terminal to enable, start, and check the status of the OSSEC service:

sudo systemctl enable ossec.service

sudo systemctl start ossec.service

sudo systemctl status ossec.service

Alternative DNS Services

Google DNS

Google DNS is available at:

[https://developers.google.com/speed/public-dns](https://developers.google.com/speed/public-dns)

The IPv4 addresses are 8.8.8.8 and 8.8.4.4.

The IPv6 addresses are 2001:4860:4860::8888 and 2001:4860:4860::8844.

Cloudflare DNS

Cloudflare DNS can be accessed at:

[https://www.cloudflare.com/en-gb/learning/dns/what-is-1.1.1.1/](https://www.cloudflare.com/en-gb/learning/dns/what-is-1.1.1.1/)

The IPv4 addresses are 1.1.1.1 and 1.0.0.1.

The IPv6 addresses are 2606:4700:4700::1111 and 2606:4700:4700::1001.

Quad9 DNS

Quad9 DNS is accessible at:

[https://www.quad9.net/service/service-addresses-and-features](https://www.quad9.net/service/service-addresses-and-features)

The IPv4 addresses are 9.9.9.11 and 149.112.112.11.

The IPv6 addresses are 2620:fe::11 and 2620:fe::fe:11.

Control D DNS

Control D DNS is available at:

[https://controld.com/free-dns](https://controld.com/free-dns)

The IPv4 addresses are 76.76.2.0 and 76.76.10.0.

The IPv6 addresses are 2606:1a40:: and 2606:1a40:1::.

Ultimate Hosts Blacklist DNS

Ultimate Hosts Blacklist DNS can be found at:

[https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist#dns-server](https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist#dns-server)

The IPv4 addresses are 88.198.70.38 and 88.198.70.39.

The IPv6 addresses are 2a01:4f8:140:5021::38 and 2a01:4f8:140:5021::39.

DNS.WATCH DNS

DNS.WATCH is accessible at:

[https://dns.watch](https://dns.watch)

The IPv4 addresses are 84.200.69.80 and 84.200.70.40.

The IPv6 addresses are 2001:1608:10:25::1c04:b12f and 2001:1608:10:25::9249:d69b.

Hosts

To set up a custom hosts file using both command line and GUI methods, follow these steps:

Visit the website:

[https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist?tab=readme-ov-file#raw-file-sources](https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist?tab=readme-ov-file#raw-file-sources)

Find the 'hosts' row, right-click on 'Download,' and select 'Save link as.' Then, click 'Save.'

Next, execute these commands in your terminal:

Navigate to the etc directory:

cd /etc

Rename the existing hosts file for backup:

sudo mv hosts hosts_backup

Move to your Downloads folder:

cd ~/Downloads

Copy the downloaded hosts file to /etc:

sudo cp hosts /etc

Return to the etc directory:

cd /etc

Change the ownership of the hosts file to root:

sudo chown -R root hosts

Set the correct permissions for the file:

sudo chmod 755 hosts

Hosts.deny

To configure a custom hosts.deny file using both command line and GUI approaches, follow these straightforward instructions:

Navigate to this URL:

[https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist?tab=readme-ov-file#raw-file-sources](https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist?tab=readme-ov-file#raw-file-sources)  

Locate the 'hosts.deny' entry, right-click on 'Download', choose 'Save link as', and then click 'Save'.

Next, proceed with these terminal commands:

Change directory to /etc:

cd /etc

Rename your current hosts.deny for backup purposes:

sudo mv hosts.deny hosts_backup.deny

Move to your Downloads folder:

cd ~/Downloads

Copy the downloaded hosts.deny to /etc:

sudo cp hosts.deny /etc

Navigate back to the /etc directory:

cd /etc

Update the file ownership to root:

sudo chown -R root hosts.deny

Set the proper file permissions:

sudo chmod 755 hosts.deny

Superhosts.deny

To set up a custom superhosts.deny file through both command line and graphical user interface, simply follow these steps:

First, visit this website:

[https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist?tab=readme-ov-file#raw-file-sources](https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist?tab=readme-ov-file#raw-file-sources).  

Look for the entry labeled 'superhosts.deny', right-click on 'Download', select 'Save link as', and confirm by clicking 'Save'.

Then, execute the following commands in your terminal:

Change your current directory to /etc:

cd /etc

Back up your existing superhosts.deny file:

sudo mv superhosts.deny superhosts_backup.deny

Head over to your Downloads folder:

cd ~/Downloads

Copy the downloaded superhosts.deny file to /etc:

sudo cp superhosts.deny /etc

Return to the /etc directory:

cd /etc

Update the file's ownership to root:

sudo chown -R root superhosts.deny

Apply the appropriate file permissions:

sudo chmod 755 superhosts.deny

Following these instructions will help you successfully update your superhosts.deny file, enhancing your system's security by controlling access more efficiently. Always remember to keep backups and set correct permissions to maintain your system's integrity.

Air Gapping

Air gapping isolates secure networks from others, like the internet, to prevent unauthorized access. Despite physical separation, innovative attacks like acoustic malware, AirHopper, BitWhisper, GSMem, and NFCdrip have breached these gaps using sound, thermal changes, FM signals, cellular frequencies, and NFC radio. Malware like ProjectSauron also exploits USB devices to siphon data from such networks, proving that even air-gapped systems can be vulnerable to creative cyber threats.

Cutting off all network connections, both wired (Ethernet) and wireless (Wi-Fi, Bluetooth, cellular), makes a device invisible to the network and securely isolated from potential cyber threats. This ensures it cannot be accessed or compromised via traditional network means, providing a strong layer of security for sensitive information.

Isolating a computer from the internet and other devices is crucial for preventing unauthorized data access. Systems can record metadata when devices like USBs or PS/2 peripherals are connected through logs or registries, potentially compromising security. Removing unnecessary USB and PS/2 devices reduces the risk of tracking and data sniffing, enhancing the effectiveness of air gapping in safeguarding sensitive information.

Enhancing computer security by removing internal network adapters involves a meticulous process akin to motherboard surgery. A specialized technician might remove or disable networking components to sever wired and wireless connections, ensuring the device is isolated from external networks. While effective, this method demands rare skills, making it potentially expensive. Alternatively, sourcing non-working laptops from platforms like eBay, specifically those with defunct networking capabilities, offers a budget-friendly solution for achieving a similar level of security.

Isolating data by storing it on analog media, like tapes, enhances security. This method, highlighted by innovative uses of VHS and cassette tapes for storing various files, capitalizes on analog's longevity and resilience against digital threats. With equipment often found on eBay and mainstream LTO drives on Amazon, this approach offers a secure, nostalgic way to preserve data, merging past tech with modern data protection needs.

Using anti-EMF paint on computer cases shields against radio waves, potentially blocking unauthorized access to electronics. Experts recommend three layers of this paint to cut down EMF exposure by up to 60db. This method is inspired by concerns over electronic snooping, as dramatized in media like "Last Of The Summer Wine." While effective, applying anti-EMF paint requires a significant investment, with costs for materials and professional labor reaching beyond $300\. Despite the expense, the ease of purchasing paint online from retailers like Amazon offers a convenient solution for those prioritizing privacy.

Wrapping computer components in EMF shielding fabric prevents unwanted electromagnetic interference, enhancing system protection. Before applying this fabric, it's advisable to apply three coats of anti-EMF paint as a primer. The fabric, tailored to fit by a craftsman, can either be glued or self-adhered to the system's parts. Notably, EMF shielding fabric, depending on its type, density, and length, offers a cost-effective alternative to anti-EMF paint.

Using 3.5mm speakers enhances security by isolating audio systems from data breaches, as these speakers, powered by standard mains and connected via a 3.5mm jack, transmit sound without data, unlike USB. Opting for models with detachable, shielded power cables further guards against interference. This setup, while simple, significantly reduces the risk of cyber threats, making it a smart choice for secure audio needs.

Isolating a computer or network physically from the internet and unsecured devices makes it immune to cyber attacks. Preferring USB over PS/2 due to reliability and steering clear of wireless options for security, one finds solace in trusted, durable USB devices like the Steelseries APEX 3 TKL keyboard and Rival 3 mouse, which offer robustness without the frills of wireless interception risks. This strategy ensures a secure computing environment, free from the vulnerabilities wireless peripherals may introduce.

Using carrier pigeons for message delivery provides the ultimate privacy, as these avian messengers bypass electronic surveillance, ensuring messages can't be intercepted by digital means. Starting at $300, carrier pigeons offer a secure, albeit old-fashioned, method of communication, accessible through specialized farms or services like PigeonGram, which combines pigeon delivery with postal service for those in the USA seeking a blend of tradition and convenience in their confidential communications.

Learning ancient languages like Sumerian or Old Chinese offers unique privacy, as these tongues are scarcely understood today. This method not only enriches one's cultural roots but ensures secure communication among a select few, leveraging the scarcity of fluent speakers. With ample resources available, learning these languages becomes a gateway to private, enriched dialogue, blending heritage preservation with the joy of acquiring a rare skill, all within a modest budget.

Manually compiling software allows for tailored optimization to one's system by adjusting source codes and flags. This process not only enhances hardware-software synergy but also enables customization, like in GNOME, where one can omit certain dependencies for a streamlined setup. It also unlocks experimental features, such as GPU acceleration in Chromium, offering a quieter, efficient system. By compiling manually, users gain a bespoke version of software, finely tuned to their needs without the bloat of unused features.

A practical way to safeguard privacy is to follow the example of Tech Giant Mark Zuckerberg, who uses duct tape to cover his webcam and microphone. This approach, costing as little as $5, is accessible and straightforward, endorsing the shift towards external HD webcams and mics for enhanced quality and security. It's a practical step for anyone valuing privacy in the digital age.

Unplugging Wired & Wireless Network Connections

Disconnecting both wired and wireless network connections, such as Wireless 6E, Ethernet, and Optical Fibre, eliminates any direct link between your computer and the network. This is crucial to prevent hackers from accessing your system through these connections.

To enhance your security and peace of mind, consider purchasing dummy network and USB plugs.

These can be found on Amazon at the following links:

[https://www.amazon.co.uk/s?k=dummy+network+plugs](https://www.amazon.co.uk/s?k=dummy+network+plugs)

[https://www.amazon.co.uk/s?k=dummy+usb+plugs](https://www.amazon.co.uk/s?k=dummy+usb+plugs)

These plugs not only occupy unused ports, protecting against dust and potentially prolonging the life of your computer's components, but they also make it less appealing for anyone trying to tamper with your system.

Regularly check what is connected to your computer. This simple habit ensures that no unauthorized devices have been attached to your system by someone with harmful intentions.

Removing Unnecessary USB & PS/2 Devices

Removing unnecessary USB and PS/2 devices is a wise move. Keep only essential devices like the keyboard, mouse, webcam, headset, and microphone connected. Avoid using USB hubs, as they can damage the motherboard and case USB ports. High-quality USB hubs can also be quite expensive.

After disconnecting non-essential devices, use dummy USB and PS/2 plugs to fill the empty ports.

These can be found on Amazon at the following links:

[https://www.amazon.co.uk/s?k=usb+dust+cap](https://www.amazon.co.uk/s?k=usb+dust+cap)

[https://www.amazon.co.uk/s?k=ps%2F2+port+dust+cap](https://www.amazon.co.uk/s?k=ps%2F2+port+dust+cap)

These plugs provide an extra layer of security, protect your system from dust, and help extend the lifespan of its components.

Additionally, it's wise to check your USB and PS/2 ports twice daily. This precaution ensures that no malicious devices have been connected while you were busy or away.

Get a Technical Professional to Help Remove Internal Network Adapters

To eliminate both wired and wireless connectivity from a computer, consult a skilled technician who can precisely modify the motherboard by removing or disabling networking components without affecting other functionalities. Given the expertise required, this approach might be costly.

An economical alternative is to look for used laptops on eBay, specifically those listed as non-working due to faulty networking capabilities. This strategy offers a practical solution for achieving device isolation.

Start your search at:

[https://www.ebay.co.uk/](https://www.ebay.co.uk/)

Analog Media

Using analog media like tapes for storing data offers a unique and enjoyable method that can preserve information for 5 to 10 years or more, depending on storage conditions and usage frequency. Recent YouTube videos using Danmere and Datosonix merchandise have highlighted creative storage solutions using VHS and cassette tapes to store photos, videos, and games.

These older devices and media can often be found on eBay at:

[https://www.ebay.co.uk/](https://www.ebay.co.uk/)

Additionally, more widely used LTO tape drives and their necessary media are available on Amazon at:

[https://www.amazon.co.uk/s?k=tape+drive](https://www.amazon.co.uk/s?k=tape+drive)

These options showcase a blend of nostalgic and modern data storage methods, appealing to various interests and needs.

Anti EMF Paint

Using Anti EMF Paint is a practical step for those concerned about privacy, as it can significantly reduce the vulnerability of computer components to radio waves. Experts recommend applying at least three layers of this paint, including a primer, to block nearly 60 decibels of electromagnetic frequency (EMF) radiation.

More information, backed by studies, can be found at:

[https://emfacademy.com/emf-paint/](https://emfacademy.com/emf-paint/)

Privacy enthusiasts might find this especially relevant, recalling scenarios like the "Father Of The Bride" episode from "Last Of The Summer Wine," where Seymour remotely disrupts electronics without physical access. This illustrates a real-world concern: potent antennas could, in theory, interfere with or access your personal computer's electronic components.

The financial aspect is noteworthy. Applying three coats of Anti EMF Paint to a computer case can cost upwards of $300 for materials alone. If you decide to paint it yourself, the cost might be lower, but for a professional finish, hiring an experienced painter is advisable. Though more expensive, this ensures a quality application and leverages the painter's expertise with such specialized materials.

For those looking to purchase Anti EMF Paint, options abound online. Retailers like Amazon and eBay offer a broad selection, catering to various preferences and needs. Amazon provides the convenience of easy shopping and delivery, making it a preferred choice for many.

You can explore the options here:

[https://www.amazon.co.uk/s?k=Anti+EMF+paint](https://www.amazon.co.uk/s?k=Anti+EMF+paint)

In summary, while the initial investment in Anti EMF Paint and professional application may seem high, the privacy and protection benefits it offers make it a consideration worth exploring.

EMF Shielding Fabric

EMF Shielding Fabric can help protect a personal computer by wrapping its components in special fabric, preventing external radio waves from interfering with the system. It's advisable to apply three coats of Anti EMF Paint, including a primer, before using the fabric. A fabric craftsman can cut the EMF Shielding Fabric to measure, and it can be attached either with superglue or using its self-adhesive properties.

One of the advantages of EMF Shielding Fabric is its cost-effectiveness compared to Anti EMF Paint. Depending on the type, density, and length, it is generally cheaper, starting at about $50 for a good quality sheet on Amazon.

You can find options here:

[https://www.amazon.co.uk/s?k=EMF+Shielding+Fabric](https://www.amazon.co.uk/s?k=EMF+Shielding+Fabric)

3.5 MM Speakers

Using 3.5mm speakers connected to a PC with a standard mains power cable and jack offers enhanced security compared to USB speakers. The 3.5mm setup transmits only audio without data, reducing the risk of data breaches. For added protection, consider speakers with a detachable power cord that can be replaced with one that has superior electromagnetic shielding and possibly a layer of Anti EMF Paint to safeguard against power disruptions or surveillance.

You can find ideal mains-powered PC speakers with a 3.5mm jack here:

[https://www.amazon.co.uk/s?k=mains+powered+pc+speakers+3.5mm+jack](https://www.amazon.co.uk/s?k=mains+powered+pc+speakers+3.5mm+jack)

Although it's possible to power speakers solely through the 3.5mm cable, this typically results in lower sound quality. However, the trade-off in power savings might be worthwhile.

For a balance of sound quality and efficiency, consider these earphones I use regularly:

[https://www.amazon.co.uk/gp/product/B00CBU0IV8](https://www.amazon.co.uk/gp/product/B00CBU0IV8)

USB Keyboard & Mouse

I like USB keyboards and mice more than PS/2 ones. PS/2 ones have problems with connecting and powering on old motherboards. Wireless keyboards are not safe because hackers can steal your data. Projection keyboards are cool but expensive. I use the steelseries APEX 3 TKL keyboard and the steelseries Rival 3 mouse every day. They are strong and work well.

You can buy them on Amazon at

[https://www.amazon.co.uk/s?k=steelseries+keyboard+and+mouse](https://www.amazon.co.uk/s?k=steelseries+keyboard+and+mouse)

They are good for people who want secure and reliable devices.

Carrier Pigeons

Using carrier pigeons for message delivery might sound amusing, but it's very secure. Unlike digital communications, messages sent this way stay private, free from government surveillance and electronic databases. Carrier pigeons cost between $300 and $1,000, depending on breed, breeder, training, and health.

You can find them at:

[https://www.pigeonfarms.com/](https://www.pigeonfarms.com/)  

[https://racinghomer.com/](https://racinghomer.com/)

For those in the USA who find the cost too high, PigeonGram offers a clever solution. This service lets you send messages via pigeon from one loft to another, and the final message is delivered to the recipient's address through USPS, complete with tracking.

Learn more at:

[https://www.pigeongram.com/](https://www.pigeongram.com/)

This mix of ancient and modern methods provides a unique, secure way to communicate.

Learning Ancient Languages

Learning ancient languages like Sumerian, Luwian, or Old Chinese offers both privacy and intellectual growth. By mastering these forgotten tongues, you connect with the heritage and culture of their original speakers and gain a unique way to communicate, understood by very few today. This can be appealing for those seeking a more private form of expression.

There are many resources available for anyone interested in these languages, through websites such as:

[https://www.amazon.co.uk/s?k=sumerian+language](https://www.amazon.co.uk/s?k=sumerian+language)

[https://www.amazon.co.uk/s?k=luwian+language](https://www.amazon.co.uk/s?k=luwian+language)

[https://www.amazon.co.uk/s?k=old+chinese+language](https://www.amazon.co.uk/s?k=old+chinese+language)

offer a variety of materials, with prices ranging from $20 to over $200\. This investment supports the preservation of ancient languages and enriches the learner's life with history and culture.

Manual Compiling

Manually compiling software is important but can be time-consuming for systems that aren't connected to the internet. It means looking at the source code and choosing specific settings to ensure the software works well with your hardware and setup. This lets you customize things, like building a desktop environment such as GNOME without certain features like the Software & Updates GUI, and turning off update notifications by default. This way, you won't have to keep using command-line instructions or editing files in Ubuntu every time you reinstall your system.

Sometimes, software has special or experimental features not available in the official versions. For instance, when you compile Chromium from source, you can enable GPU-acceleration features that aren't usually turned on. This can make your system quieter and more stable. Compiling software yourself allows you to make it fit your needs better, improving both performance and user experience.

Duct Tape For Covering The Webcam & Microphone

Using duct tape to cover your webcam and microphone is a simple and effective way to protect your privacy. Even Facebook's Mark Zuckerberg uses this method, showing its practicality for everyone. Duct tape is cheap and versatile, costing around $5\. This ensures privacy and encourages using external HD webcams and microphones for better quality. These alternatives are easy to find and affordable, offering a big improvement over built-in laptop cameras and mics.

For a selection of duct tape, visit:

[https://www.amazon.co.uk/s?k=thick+duct+tape](https://www.amazon.co.uk/s?k=thick+duct+tape)

For high-quality webcams and microphones, check out:

[https://www.amazon.co.uk/s?k=hd+webcam+and+microphone](https://www.amazon.co.uk/s?k=hd+webcam+and+microphone)

Virtual Private Networks

A Virtual Private Network (VPN) connects devices securely to networks over the Internet. It allows remote access to private networks and links different networks, including offices spread across locations. VPNs boost security, reduce costs compared to dedicated lines, and improve remote work flexibility. They use tunneling protocols to create secure virtual connections, serving both individual remote access and business site-to-site needs. Configurations range from connecting a single computer to an entire network or linking multiple organizations. VPNs cater to various security levels and network topologies, supporting uses from cloud computing to branch office connectivity.

Proton VPN, based in Switzerland, offers secure and private internet browsing on multiple platforms without logging user activity. Available in free and paid versions, it ensures high-speed, encrypted connections for safety over public networks and access to restricted content globally. It emphasizes ease of use, reliability, and a no-logs policy. Proton VPN supports up to 10 devices, integrates with Tor, and features unique security enhancements like Secure Core and Perfect Forward Secrecy. Created by the makers of Proton Mail, it aims to make the internet safer and more accessible for everyone.

NordVPN provides comprehensive online security, protecting your daily activities wherever you are. Beyond VPN services, it includes Threat Protection to block malware and ads, Meshnet for private network creation, Dark Web Monitor for compromised account alerts, and Dedicated IP for a consistent online identity. NordVPN offers encryption, a kill switch for dropped connections, split tunneling for selective app protection, Double VPN for extra encryption, and SmartDNS for easy streaming. It ensures privacy with no user tracking, global coverage, fast connections, and support for multiple devices. It's user-friendly, with browser extensions and 24/7 customer support, making digital protection accessible to everyone.

Private Internet Access (PIA) is a trusted VPN provider since 2010, known for its vast network of over 10,000 servers and a solid zero-logging policy. Owned by Kape Technologies, PIA supports various platforms and offers unlimited connections, making it popular among privacy-conscious users. Key features include robust torrenting capabilities, a command line tool for scripting, and strong privacy and security credentials verified by independent audits and court validations.

Proton VPN

Visit the official Proton VPN website at [https://protonvpn.com/](https://protonvpn.com/) for everything related to Proton VPN.

Installing Proton VPN via .deb from the GUI:

1.  Go to [https://protonvpn.com/support/official-ubuntu-vpn-setup/](https://protonvpn.com/support/official-ubuntu-vpn-setup/).
2.  Click "Download the Proton VPN DEB package" to download Proton VPN.
3.  Open the directory Files and navigate to: ~/Downloads.
4.  Double-click protonvpn-stable-release_1.0.3-3_all.deb.
5.  Click "Install".

NordVPN

Visit the official NordVPN website at [https://nordvpn.com/](https://nordvpn.com/) for everything related to NordVPN.

Installing NordVPN via APT in the Terminal:

Type these commands:

sudo apt update

sh <(curl -sSf https://downloads.nordcdn.com/apps/linux/install.sh)

Private Internet Access

Visit the official Private Internet Access website at [https://www.privateinternetaccess.com/](https://www.privateinternetaccess.com/) for everything related to Private Internet Access.

Installing Private Internet Access via .run from the GUI & Terminal:

1.  Go to:

[https://www.privateinternetaccess.com/download/linux-vpn](https://www.privateinternetaccess.com/download/linux-vpn%20)

2.  Click "Download VPN for Linux" to download Private Internet Access.
3.  Open the directory Files and navigate to: ~/Downloads.
4.  Right-click an empty space in the directory.
5.  Click "Open In Terminal".
6.  Run the following commands in the terminal:

sudo chmod +x pia-linux-3.5.7-08120.run

sudo ./pia-linux-3.5.7-08120.run

Drivers

Drivers are essential for computers, acting as a bridge between the operating system and devices like printers or keyboards. They come in two types: generic for basic functions and specific for particular devices, needing manual installation. Drivers ensure smooth interaction between devices and software, facilitating tasks from web browsing to playing media. Outdated or incorrect drivers can cause performance issues or system failures. Installation typically happens via manufacturer websites, with updates ensuring compatibility and security. Without drivers, computers can't access hardware, leading to operational failures. Signed drivers offer extra security by verifying authenticity. Keeping drivers updated is crucial for smooth functioning, with version compatibility varying by Windows versions. Device Manager can help check if drivers are working properly.

NVIDIA drivers connect your computer to its NVIDIA graphics processor, crucial for maximizing hardware performance with the latest games and apps. Certified drivers from NVIDIA's official site enhance frame rates, resolution, and 3D graphics while reducing crashes. Available for download from NVIDIA or PC manufacturers, these drivers fix common issues like display errors and slow performance.

AMD drivers ensure smooth communication between your AMD hardware, like graphics cards, and your computer's operating system. They're key for optimal performance and compatibility with games and applications. Check for the latest AMD drivers by visiting AMD's support section. Updates can be manual or automatic via AMD's update software, improving performance, stability, and security while fixing bugs. Regular updates are recommended for the best experience.

Radeontop monitors GPU utilization for AMD graphics cards, starting from the R600 series. It provides real-time data on overall GPU activity and specific block usage, useful for optimizing performance. You can select among multiple GPUs, dump data to a file, and adjust the output's frequency and style. While it primarily supports open drivers, it's also compatible with AMD Catalyst, albeit with some limitations. Its accessibility to /dev/dri/cardN or /dev/mem paths requires root privileges, ensuring detailed insights into both OpenCL and OpenGL workloads, making it an essential utility for graphics professionals and enthusiasts.

Printer drivers allow your computer to communicate with your printer, translating digital data into a format the printer understands. This includes page layout, paper type, and print quality settings, ensuring accurate document printing. Printer drivers know your printer's capabilities and handle technical details, making printing seamless from any application. They support various operating systems and offer features like stapling and booklet making. With drivers for many brands like Brother, Epson, HP, and Canon, they ensure compatibility and enhance printing options, streamlining the process from digital to physical form.

NVIDIA

Visit the official NVIDIA website at [https://www.nvidia.com/](https://www.nvidia.com/) for everything related to NVIDIA.

Installing NVIDIA via APT in the Terminal:

Type these commands:

Update your package lists:

sudo apt update

Add the i386 architecture for compatibility:

sudo dpkg --add-architecture i386

sudo apt update

Install the NVIDIA driver and Vulkan libraries:

sudo apt install nvidia-driver-550 libvulkan1 libvulkan1:i386

Installing NVIDIA via NVIDIA Developer APT Repository in the Terminal:

Update your package lists:

sudo apt update

Add the i386 architecture for compatibility:

sudo dpkg --add-architecture i386

sudo apt update

Import the NVIDIA GPG key:

curl -fSsL https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/3bf863cc.pub | sudo gpg --dearmor | sudo tee /usr/share/keyrings/nvidia-drivers.gpg > /dev/null 2>&1

Add the NVIDIA repository to your system:

echo 'deb [signed-by=/usr/share/keyrings/nvidia-drivers.gpg] https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/ /' | sudo tee /etc/apt/sources.list.d/nvidia-drivers.list

Update your package lists again:

sudo apt update

Finally, install the NVIDIA driver along with Vulkan support:

sudo apt update

sudo apt install nvidia-driver libvulkan1 libvulkan1:i386

AMD

Visit the official AMD website at [https://www.amd.com/en.html](https://www.amd.com/en.html)  for everything related to AMD.

The latest stable open-source AMD drivers are included by default with Linux Mint 22 and the latest unstable drivers are available through the OIBAF ppa.

Installing OIBAF AMD Drivers via APT in the Terminal:

Type these commands:

Update your package lists:

sudo apt update

Add the i386 architecture for compatibility:

sudo dpkg --add-architecture i386

sudo apt update

Add the OIBAF ppa:

sudo add-apt-repository ppa:oibaf/graphics-drivers

sudo apt update

Install the OIBAF AMD drivers and related libraries:

sudo apt update && sudo apt upgrade

Radeontop

Visit the official Radeontop website at [https://github.com/clbr/radeontop](https://github.com/clbr/radeontop)  for everything related to Radeontop.

For a SYSTEM Package through Software Manager:

1.  Open Software Manager and search for Radeontop.
2.  Click on Radeontop, then on the source selection box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing Radeontop via APT in the Terminal:

Update your package lists:

sudo apt update

Install Radeontop:

sudo apt install radeontop

AMDGPU Fan Configuration Guide

Open Terminal:

Type:

sudo gedit /etc/amdgpu-fan.yml

Hit Enter.

Edit Configuration:

Replace content with:

speed_matrix:
  - [0, 0]
  - [30, 15]
  - [50, 30]
  - [70, 70]
  - [90, 100]

Save Changes:

Click "Save."

Or, navigate to "File" > "Save."

Alternatively, use the ☰ menu to select "Save As," then confirm by clicking "Save."

Close Editor:

Exit gedit to complete your setup.

Printer Driver All

Visit the official Printer Driver All website at [https://packages.ubuntu.com/jammy/printer-driver-all](https://packages.ubuntu.com/jammy/printer-driver-all) for everything related to Printer Driver All.

Installing Printer Driver All via APT in the Terminal:

First, update your package list:

sudo apt update

Then, install the driver:

sudo apt install printer-driver-all

Office Suites

Office suites are crucial for productivity, combining word processors, spreadsheets, and presentation programs in one interface. Traditionally offline like Microsoft Office, many now offer online functionality, such as Google Docs. Popular choices include Microsoft Office for Windows and Mac, as well as open-source options like LibreOffice and OpenOffice. Apple's iWork is tailored for Mac users, providing tools for documents, spreadsheets, and presentations. These suites improve efficiency and document management, showcasing technology's role in workplace productivity.

LibreOffice, a free and open-source suite, includes tools for word processing, spreadsheets, and presentations, supporting many file formats, including Microsoft Office. Originating from OpenOffice in 2010, it is available in 115 languages for Windows, macOS, and Linux, with mobile versions by Collabora. Known for collaboration and accessibility, it is a favorite among many users, including Linux distributions. With a strong development community, it offers feature-rich applications like Writer, Calc, and Impress, serving over 200 million users worldwide.

Apache OpenOffice, another open-source suite, provides word processing, spreadsheets, and presentations, supporting formats like ODF. It evolved from OpenOffice.org and IBM's Lotus Symphony and is available for Linux, macOS, and Windows under the Apache-2.0 license. Despite challenges in maintaining contributors and timely updates, it remains significant in productivity software, demonstrating the dynamics of open-source projects.

Calligra Suite, developed by KDE, is a versatile office and graphic art suite for desktops, tablets, and smartphones. It includes word processing, spreadsheets, presentations, vector graphics, and database editing tools. Calligra Words focuses on document creation with an intuitive design, while Calligra Sheets handles spreadsheets with ease. Other components like KEXI, Karbon, Plan, and Stage enhance the suite's functionality, with Gemini providing a flexible interface for 2-in-1 devices.

OnlyOffice, formerly TeamLab, is a free office suite with online editors for texts, spreadsheets, presentations, forms, and PDFs. It supports various formats like DOCX and XLSX, ensuring compatibility with Microsoft Office. Available as SaaS or for private networks, it features tab-based editing, extensive styling tools, numerous spreadsheet functions, presentation enhancements, and comprehensive PDF editing capabilities.

SoftMaker FreeOffice is a free office suite for Windows, Mac, and Linux, offering word processing, spreadsheets, and presentation tools compatible with Microsoft Office formats like DOCX, XLSX, and PPTX. It caters to both business and personal use, with a customizable interface, touch mode for touchscreen devices, and numerous features for creating documents and presentations. Its compatibility with Microsoft Office ensures seamless file sharing.

WPS Office includes WPS Writer, Presentation, and Spreadsheet, and is a popular Microsoft Office alternative for Linux, supporting formats like DOCX, XLSX, and PPTX. It enhances productivity with text processing, data analysis, and presentation creation tools, including a versatile PDF toolkit. The free version offers extensive functionalities, with a professional version available by subscription. With over 494 million monthly users, WPS Office has improved significantly since its 2016 release, developed by a volunteer community for Linux.

LibreOffice

Visit the official LibreOffice website at [https://www.libreoffice.org/](https://www.libreoffice.org/) for everything related to LibreOffice.

Installing LibreOffice via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open GNOME Software and search for LibreOffice.
2.  Click on LibreOffice, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing LibreOffice via APT in the Terminal:

sudo apt install libreoffice

Installing LibreOffice via FLATPAK in the Terminal:

flatpak install flathub org.libreoffice.LibreOffice

Installing LibreOffice via SNAP in the Terminal:

sudo snap install libreoffice

Apache OpenOffice

Visit the official Apache OpenOffice website at [https://www.openoffice.org/](https://www.openoffice.org/) for all things Apache OpenOffice.

Navigate to the release page at:

[https://github.com/area-of-dev/OpenOffice.AppImage/releases](https://github.com/area-of-dev/OpenOffice.AppImage/releases)

Click on "The Assets" tab to view the files and select the latest version of the OpenOffice.AppImage file.

Download the file to your ~/Downloads folder.

Locate the OpenOffice.AppImage file in your Downloads folder, right-click on it, and select "Properties." In the Properties menu, go to the "Permissions" tab and check the box to "Set as executable."

Double-click the OpenOffice.AppImage file to start the installation.

### Apache OpenOffice Desktop Shortcut

Open your terminal and navigate to the applications directory with:

cd /usr/share/applications

Open a new .desktop file for editing by running:

sudo gedit openoffice1.desktop

In the openoffice1.desktop file, enter:

[Desktop Entry]

Name=Apache OpenOffice

Comment=Apache OpenOffice

Exec=./Downloads/OpenOffice.AppImage

Icon=application

Terminal=false

Type=Application

Categories=Utility;Office;

Click "Save" to save your progress. After saving, close the editor.

Calligra Suite

Visit the official Calligra Suite website at [https://calligra.org/](https://calligra.org/) for everything related to Calligra Suite.

Installing Calligra Suite via SYSTEM PACKAGE/FLATPAK Package through GNOME Software:

1.  Open GNOME Software and search for Calligra.
2.  Click on Calligra, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing LibreOffice via APT in the Terminal:

sudo apt install calligra

OnlyOffice

Visit the official OnlyOffice website at [https://www.onlyoffice.com/en/](https://www.onlyoffice.com/en/) for all things OnlyOffice.

Installing OnlyOffice via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for OnlyOffice.
2.  Click on OnlyOffice, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing OnlyOffice via FLATPAK in the Terminal:

flatpak install flathub org.onlyoffice.desktopeditors

Installing OnlyOffice via SNAP in the Terminal:

sudo snap install onlyoffice-desktopeditors

Softmaker FreeOffice  

Visit the official Softmaker FreeOffice website at [https://www.freeoffice.com/en/](https://www.freeoffice.com/en/) for everything related to Softmaker FreeOffice.

Navigate to the release page at:

[https://www.freeoffice.com/en/download/applications](https://www.freeoffice.com/en/download/applications)

Click "Download" and then click on the .rpm package for DEB-based systems to download Softmaker FreeOffice.

Go to your ~/Downloads folder, double-click on softmaker-freeoffice-2021-1068_amd64.deb, and click "Install."

WPS Office

Visit the official WPS Office website at [https://www.wps.com/](https://www.wps.com/) for everything related to WPS Office.

Navigate to the release page at:

[https://www.wps.com/office/linux/](https://www.wps.com/office/linux/)

Click on the Rpm Package to download WPS Office.

Go to your ~/Downloads folder, double-click on wps-office_11.1.0.11719.XA_amd64.deb and click "Install."

Email Clients

Email clients are software that help manage emails by allowing you to view, send, and organize messages efficiently. They work offline, integrate calendars, and improve usability over web services. Customization options boost efficiency and security, simplifying email management.

Mozilla Thunderbird is a free, open-source email client that also functions as a personal information manager. It offers calendar, contact book, RSS feed reader, chat, and news functionalities. Supported across various platforms, it’s managed by MZLA Technologies Corporation, a Mozilla Foundation subsidiary. Community-driven, Thunderbird integrates email, newsgroup, news feed, and instant messaging with personal information management features. It supports multiple email protocols and offers advanced security with OpenPGP and S/MIME encryption, meeting industry standards. Notably, the French military uses it for its security features.

Betterbird enhances Thunderbird with exclusive features, bug fixes, and early updates. It introduces multi-line views, vertical tabs, account colors, and improved attachment management. With advanced search capabilities, Betterbird offers a smoother email experience. It installs easily alongside Thunderbird, fixing issues the latter hasn't addressed for a more reliable email experience.

Geary, an open-source email client, is designed for simplicity and efficiency. Initially developed by the Yorba Foundation and now part of GNOME, it supports major email services and IMAP servers. It organizes mail by conversations and includes features like an HTML mail composer, desktop notifications, and secure password storage via GNOME Keyring.

Mailspring is a versatile email client for Mac, Linux, and Windows. It supports multiple accounts, including IMAP and Office 365, with features like touch gestures, advanced shortcuts, and fast search. It includes undo send, a unified inbox, read receipts, and link tracking. Mailspring's advanced search, signature editor, and multilingual email translation enhance productivity. It also offers themes, layouts, and extensive localization for effective and personalized email management.

Thunderbird

Visit the official Thunderbird website at [https://www.thunderbird.net/en-GB/](https://www.thunderbird.net/en-GB/) for everything related to Thunderbird.

Installing Thunderbird via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Thunderbird.
2.  Click on Thunderbird, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Thunderbird via APT in the Terminal:

sudo apt install thunderbird

Installing Thunderbird via FLATPAK in the Terminal:

flatpak install flathub org.mozilla.Thunderbird

Installing Thunderbird via SNAP in the Terminal:

sudo snap install thunderbird

Betterbird

Visit the official Betterbird website at [https://www.betterbird.eu/](https://www.betterbird.eu/) for everything about Betterbird.

Installing Betterbird via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Betterbird.
2.  Click on Betterbird, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Thunderbird via FLATPAK in the Terminal:

flatpak install flathub eu.betterbird.Betterbird

Mailspring

Visit the official Mailspring website at [https://www.getmailspring.com/](https://www.getmailspring.com/) for everything about Mailspring.

Installing Mailspring via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Mailspring.
2.  Click on Mailspring, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Mailspring via FLATPAK in the Terminal:

flatpak install flathub com.getmailspring.Mailspring

Installing Mailspring via SNAP in the Terminal:

sudo snap install mailspring

Image Editing Software

Image editing software allows you to manipulate digital photos through cropping, retouching, and color adjustments. It includes tools for vector, raster, and 3D modeling, enhancing or creating images from scratch. Mainly used for 2D edits, it supports tasks like resizing and applying filters to adjust attributes or add effects, and also facilitates format conversion.

GIMP, the GNU Image Manipulation Program, is a free tool for photo editing and image composition. It offers features like painting tools, layer support, and advanced manipulation with full alpha channel support. Expandable with plugins and scripts, GIMP runs on various platforms and supports many file formats, making it suitable for both simple and complex editing needs.

Blender is a free, open-source 3D creation suite for modeling, animation, VFX, and video editing. It runs on Linux, macOS, and Windows, catering to both professionals and hobbyists. With comprehensive tools, Blender supports a wide range of media productions, from game assets to films. Its interface, powered by OpenGL, ensures a uniform experience across devices, while its active community offers extensive support and learning resources.

Pinta is an open-source, cross-platform image editor similar to Paint.NET but with more features. It provides a robust toolkit for bitmap image editing, including drawing tools, filters, color adjustments, and multiple layers for complex edits. Designed for ease of use, it includes unlimited undo history, multilingual support, and a customizable workspace, making it a user-friendly yet powerful editing solution.

Krita is a versatile, free open-source graphics editor for digital artists and animators. It offers tools for 2D animation and art creation on Linux, Windows, and macOS. Krita features an OpenGL-accelerated canvas, advanced brush engines with over 100 preloaded brushes, non-destructive layers, vector support, and customizable interfaces. It includes brush stabilizers for smooth strokes, built-in vector tools for comics, and a resource manager for sharing or importing brushes, making it a powerful tool for creators seeking flexibility and precision.

Inkscape is a free, open-source vector graphics editor that runs on various platforms including Windows, macOS, and Unix-like systems. It excels in creating sharp, scalable illustrations like cartoons, logos, and diagrams without pixel limits, thanks to its vector-based approach. Supporting SVG as its primary format, Inkscape handles many file types and offers tools for intricate designs with shapes, text, colors, and gradients, all while allowing for transforming and editing images directly from raster sources to vector art.

Darktable is a free, open-source photography app and raw developer focused on non-destructive post-production. It optimizes workflows, handling many images efficiently across various platforms. With features like real-time adjustments, GPU acceleration, and support for numerous image formats, Darktable enhances image editing through modules for color correction, effects, and organization. It supports non-destructive editing, ICC profiles, and Lua scripting for customization, with a UI that includes lighttable and darkroom modes for easy navigation and editing, plus tethering and map views for comprehensive image management.

Tux Paint is a free, open-source drawing software designed for children ages 3 to 12\. Created by Bill Kendrick in 2002, it offers a simple interface filled with fun effects and drawing tools to spark creativity in kids. Supporting multiple platforms like Windows, macOS, and Android, Tux Paint is accessible worldwide. With its mascot Tux guiding users, children can explore art through various tools and effects, while teachers and parents can customize the experience with additional content. Ideal for fostering computer literacy and artistic skills, Tux Paint is celebrated for its ease of use and inclusive design.

Gnu Image Manipulation Program (GIMP)

Visit the official GIMP website at [https://www.gimp.org/](https://www.gimp.org/) for everything related to GIMP.

Installing Gnu Image Manipulation Program (GIMP) via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Gnu Image Manipulation Program (GIMP).
2.  Click on Gnu Image Manipulation Program (GIMP), then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Gnu Image Manipulation Program (GIMP) via APT in the Terminal:

sudo apt install gimp

Installing Gnu Image Manipulation Program (GIMP) via FLATPAK in the Terminal:

flatpak install flathub org.gimp.GIMP

Installing Gnu Image Manipulation Program (GIMP) via SNAP in the Terminal:

sudo snap install gimp

Blender

Visit the official Blender website at [https://www.blender.org/](https://www.blender.org/) for everything about Blender.

Installing Blender via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Blender.
2.  Click on Blender, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Blender via APT in the Terminal:

sudo apt install blender

Installing Blender via FLATPAK in the Terminal:

flatpak install flathub org.blender.Blender

Installing Blender via SNAP in the Terminal:

sudo snap install blender --classic

Pinta

Visit the official Pinta website at [https://www.pinta-project.com/](https://www.pinta-project.com/) for everything about Pinta.

Installing Pinta via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Pinta.
2.  Click on Pinta, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Pinta via APT in the Terminal:

sudo apt install pinta

Installing Pinta via FLATPAK in the Terminal:

flatpak install flathub com.github.PintaProject.Pinta

Installing Pinta via SNAP in the Terminal:

sudo snap install pinta

Krita

Visit the official Krita website at [https://krita.org/en/](https://krita.org/en/) for everything about Krita.

Installing Krita via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Krita.
2.  Click on Krita, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Krita via APT in the Terminal:

sudo apt install krita

Installing Krita via FLATPAK in the Terminal:

flatpak install flathub org.kde.krita

Installing Krita via SNAP in the Terminal:

sudo snap install krita

Inkscape

Visit the official Inkscape website at [https://inkscape.org/](https://inkscape.org/) for everything about Inkscape.

Installing Inkscape via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Inkscape.
2.  Click on Inkscape, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Inkscape via APT in the Terminal:

sudo apt install inkscape

Installing Inkscape via FLATPAK in the Terminal:

flatpak install flathub org.inkscape.Inkscape

Installing Inkscape via SNAP in the Terminal:

sudo snap install inkscape

Darktable

Visit the official Darktable website at [https://www.darktable.org/](https://www.darktable.org/) for everything about Darktable.

Installing Darktable via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Darktable.
2.  Click on Darktable, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Darktable via APT in the Terminal:

sudo apt install darktable

Installing Darktable via FLATPAK in the Terminal:

flatpak install flathub org.darktable.Darktable

Installing Darktable via SNAP in the Terminal:

sudo snap install darktable

Tuxpaint

Visit the official Tuxpaint website at [https://tuxpaint.org/](https://tuxpaint.org/) for everything about Tuxpaint.

Installing Tuxpaint via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Tuxpaint.
2.  Click on Tuxpaint, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Tuxpaint via FLATPAK in the Terminal:

flatpak install flathub org.tuxpaint.Tuxpaint

Audio Editing Software

Audio editing software lets you edit and create audio, import and export files, record sounds, and adjust timing and volume. It also allows mixing tracks, applying effects like reverb and equalization, and converting between file formats. Digital audio workstations offer comprehensive music production suites with user-friendly interfaces, enabling non-linear editing and both real-time and offline processing for professional sound quality.

Audacity is a free, open-source audio editor and recorder for Windows, macOS, Linux, and Unix-like systems. With over 1142 million downloads since 2015, it's popular for its compatibility with major systems, support for various audio formats, and ability to work with plugins like VST3\. Licensed under GPL-2.0-or-later, Audacity also offers deep audio analysis tools for visualizing frequencies, making it ideal for audio editing and recording.

Ardour is a digital audio workstation for recording, editing, and mastering on Linux, macOS, and Windows. Created by Paul Davis, it offers limitless capabilities based on your hardware, including latency correction, various monitoring options, and plug-in effects. Ardour supports infinite tracks, buses, and flexible routing. Its editing features include drag, trim, split, and time-stretch with high precision. Ardour excels in mastering, integrates with JACK for advanced processing, and supports audio CD file export.

Mixxx is free, open-source DJ software for creatively mixing digital music files, suitable for all DJ levels. It features BPM and key detection for track matching, syncs up to four songs, supports various DJ controllers, and allows custom mappings. Add flair with sound effects and chain them for creativity. Use timecode vinyl for a classic feel. Developed by a dedicated community, Mixxx is perfect for DJs eager to mix digitally without cost.

Audacity

Visit the official Audacity website at [https://www.audacityteam.org/](https://www.audacityteam.org/) for everything about Audacity.

Installing Audacity via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Audacity.
2.  Click on Audacity, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Audacity via APT in the Terminal:

sudo apt install audacity

Installing Audacity via FLATPAK in the Terminal:

flatpak install flathub org.audacityteam.Audacity

Installing Audacity via SNAP in the Terminal:

sudo snap install audacity

Ardour

Visit the official Ardour website at [https://ardour.org/](https://ardour.org/) for everything about Ardour.

Installing Ardour via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Ardour.
2.  Click on Ardour, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Ardour via APT in the Terminal:

sudo apt install ardour

Installing Ardour via FLATPAK in the Terminal:

flatpak install flathub org.ardour.Ardour

MIXXX

Visit the official Mixxx website at [https://mixxx.org/](https://mixxx.org/) for everything about Mixxx.

Installing MIXXX via RPM/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for MIXXX.
2.  Click on MIXXX, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing MIXXX via FLATPAK in the Terminal:

flatpak install flathub org.mixxx.Mixxx

Installing MIXXX via SNAP in the Terminal:

sudo snap install mixxx-community

Video Editing Software

Video editing software is an essential tool for manipulating video clips, adding music, and adjusting timing. It is crucial for creating films, TV shows, ads, and video essays, making the editing process accessible on personal computers. This software supports cutting videos into parts, overlaying soundtracks, and exporting the final product as a video file. From professionals to hobbyists, it allows users to refine their videography work, enabling a wide range of styles and applications.

OpenShot, a free and open-source video editor for Linux, macOS, Windows, and ChromeOS, was launched in 2008 by Jonathan Thomas. It provides cross-platform editing and supports various formats through FFmpeg. OpenShot allows for unlimited tracks and layers, accommodating complex projects. Key features include curve-based keyframe animations for smooth transitions, drag-and-drop functionality for ease of use, and clip resizing to fit different aspects of the project. Additionally, it offers video transitions, compositing, 3D titles with Blender, advanced timeline controls, frame accuracy, speed changes, audio mixing, and digital effects like chroma key for green screen effects.

Kdenlive, another open-source video editor, began in 2003\. It supports multi-track editing and uses FFmpeg for extensive format support. Its interface and shortcuts are customizable to enhance user experience. Kdenlive includes a titler for creating captions and titles, numerous effects, and transitions to add a professional touch. It offers proxy editing for efficient workflow, automatic backups to prevent data loss, online resources for additional support, timeline previews for real-time editing, keyframeable effects for dynamic changes, and themable interfaces for personalization. Developed by a small, dedicated team, Kdenlive is suitable for both basic and professional video editing tasks.

Shotcut, a free, open-source video editor for FreeBSD, Linux, macOS, and Windows, was created in 2011 by Dan Dennedy. It supports a wide range of formats via FFmpeg and offers multi-track editing. Shotcut features GPU-accelerated processing for faster rendering, video and audio filters for enhanced effects, and supports webcam and audio capture for direct recording. It can handle network stream playback and provides advanced editing tools like color grading for adjusting the tone and mood of videos, keyframes for animating effects, motion tracking for following subjects, and supports hardware inputs like Blackmagic Design for professional monitoring. Shotcut's versatility includes options for batch encoding, ensuring consistent output, and integrity checks for maintaining quality, making it ideal for both beginners and professionals.

Pitivi, a free, open-source video editor for Linux, offers an intuitive and efficient editing experience for both novices and professionals. It supports unlimited video and audio tracks, allowing for complex projects. Pitivi includes full undo/redo functionality to correct mistakes easily, keyframeable effects for dynamic changes, and imports various formats via GStreamer for broad compatibility. Designed following GNOME guidelines, Pitivi ensures ease of use with features like frame stepping for precise edits, trimming for removing unwanted sections, and sound mixing for balancing audio. It is community-driven, emphasizing usability and multimedia innovation to provide a robust editing platform.

OpenShot

Visit the official OpenShot website at [https://www.openshot.org/](https://www.openshot.org/) for everything about OpenShot.

Installing OpenShot via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for OpenShot.
2.  Click on OpenShot, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing OpenShot via APT in the Terminal:

sudo apt install openshot-qt

Installing OpenShot via FLATPAK in the Terminal:

flatpak install flathub org.openshot.OpenShot

Installing OpenShot via SNAP in the Terminal:

sudo snap install openshot-community

Kdenlive

Visit the official Kdenlive website at [https://kdenlive.org/en/](https://kdenlive.org/en/) for everything about Kdenlive.

Installing Kdenlive via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Kdenlive.
2.  Click on Kdenlive, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Kdenlive via APT in the Terminal:

sudo apt install kdenlive

Installing Kdenlive via FLATPAK in the Terminal:

flatpak install flathub org.kde.kdenlive

Installing Kdenlive via SNAP in the Terminal:

sudo snap install kdenlive

Shotcut

Visit the official Shotcut website at [https://www.shotcut.org/](https://www.shotcut.org/) for everything about Shotcut.

Installing Shotcut via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Shotcut.
2.  Click on Shotcut, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Shotcut via FLATPAK in the Terminal:

flatpak install flathub org.kde.Shotcut

Installing Shotcut via SNAP in the Terminal:

sudo snap install shotcut

Pitivi

Visit the official Pitivi website at [https://www.pitivi.org/](https://www.pitivi.org/) for everything about Pitivi.

Installing Pitivi via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Pitivi.
2.  Click on Pitivi, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Pitivi via APT in the Terminal:

sudo apt install pitivi

Installing Pitivi via FLATPAK in the Terminal:

flatpak install flathub org.pitivi.Pitivi

Integrated Development Environments (IDE’s)

Integrated Development Environments (IDEs) are software tools that streamline software development by combining a code editor, debugger, and build automation tools. Popular IDEs like IntelliJ IDEA and Eclipse often include compilers or interpreters, simplifying the development process. They also integrate version control and GUI construction tools, enhancing productivity with a unified interface. IDEs support various programming languages, with some tailored for specific ones. Modern IDEs are usually graphical, although text-based versions existed in the past.

Visual Studio Code, created by Microsoft, is a versatile source-code editor available for Windows, Linux, and macOS. It offers debugging, syntax highlighting, and intelligent code completion, supporting many programming languages. Customization is possible through themes, shortcuts, and extensions from a central repository. Despite collecting usage data, its open-source nature ensures transparency. It operates without a traditional project system, allowing directories to be opened and saved as workspaces, supporting extensive language extensions.

VSCodium is a community-driven, open-source version of Microsoft's VS Code editor, free from telemetry and branding. It retains the same functionality while respecting user privacy and freedom by removing tracking features. VSCodium simplifies access to VS Code's benefits without needing to compile from source, providing binaries under the MIT license. It addresses concerns over software freedom and privacy, ensuring an up-to-date, clean version of VS Code is available to all.

Atom was a free, open-source text and source code editor by GitHub for macOS, Linux, and Windows. Launched in 2015, it was celebrated for its customization capabilities using HTML, CSS, and JavaScript. Built on the Electron framework, it supported plugins in JavaScript and embedded Git control. Despite its retirement, Atom's legacy as a versatile and user-friendly editor for developers endures.

Geany is a free, open-source, lightweight text editor with basic IDE features, designed for speed with minimal dependencies. It supports many programming and markup languages, offering syntax highlighting, code folding, auto-completion, and project management. Geany works across operating systems, including BSD, Linux, macOS, Solaris, and Windows, though its Windows version lacks certain Unix-based tools unless added by the user. Unlike traditional Unix editors, Geany resembles Windows editors like Notepad++, using Scintilla and GTK for its interface.

Bluefish is a powerful editor for programmers and web developers, supporting various programming and markup languages. It’s open-source under the GNU GPL license, running on multiple platforms like Linux, macOS, and Windows. Bluefish excels with its speed, lightweight design, and ability to handle numerous documents efficiently. It offers project support, multi-threaded remote file editing, powerful search and replace, rapid coding snippets, and integration with external programs. Additionally, it features customizable language support, in-line spell checking, auto-recovery, and site management tools, making it a comprehensive tool for coding and web development.

Visual Studio Code

To explore everything about Visual Studio Code, visit their official website at [https://code.visualstudio.com/](https://code.visualstudio.com/).

Installing Visual Studio Code via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Visual Studio Code.
2.  Click on Visual Studio Code, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Visual Studio Code via APT in the Terminal:

sudo apt install wget gpg apt-transport-https

wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg

sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg

echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null

sudo apt update && sudo apt install code

Installing Visual Studio Code via FLATPAK in the Terminal:

flatpak install flathub com.visualstudio.code

Installing Visual Studio Code via SNAP in the Terminal:

sudo snap install code --classic

Installing Visual Studio Code via .deb in the GUI:

Navigate to the release page at:

[https://code.visualstudio.com/download](https://code.visualstudio.com/download)

Scroll down to the section featuring Tux the penguin.

Click on the ".deb" download link to retrieve the Debian package file.

After downloading, navigate to your Downloads directory:

Locate the downloaded Debian package file, which should be named something like " code_1.90.1-1718141439_amd64.deb."

Double-click on the .deb package file to initiate the installation process.

Follow the on-screen instructions and click "Install" when prompted.

VSCodium

Visit the official VSCodium website at [https://vscodium.com/](https://vscodium.com/) for everything VSCodium.

Installing VSCodium via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for VSCodium.
2.  Click on VSCodium, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing VSCodium via APT in the Terminal:

wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg \

| gpg --dearmor \

| sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg

echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' \

| sudo tee /etc/apt/sources.list.d/vscodium.list

sudo apt update && sudo apt install codium

Installing VSCodium via FLATPAK in the Terminal:

flatpak install flathub com.vscodium.codium

Installing VSCodium via SNAP in the Terminal:

sudo snap install codium --classic

Installing VSCodium via .deb in the GUI:

Navigate to the release page at:

[https://github.com/VSCodium/vscodium/releases](https://github.com/VSCodium/vscodium/releases)

Scroll down to the section featuring the latest release.

Click on the "amd64.deb" download link to retrieve the Debian package file.

After downloading, navigate to your Downloads directory:

Locate the downloaded Debian package file, which should be named something like " codium_1.90.1.24165_amd64.deb."

Double-click on the .deb package file to initiate the installation process.

Follow the on-screen instructions and click "Install" when prompted.

Atom

Visit the official Atom website at [https://atom-editor.cc/](https://atom-editor.cc/) for all things Atom.

Installing Atom via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Atom.
2.  Click on Atom, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Atom via FLATPAK in the Terminal:

flatpak install flathub io.atom.Atom

Installing Atom via .deb in the GUI:

Navigate to the release page at:

[https://github.com/atom/atom/releases/tag/v1.60.0](https://github.com/atom/atom/releases/tag/v1.60.0)

Scroll down to the section featuring the latest release.

Click on the "amd64.deb" download link to retrieve the Debian package file.

After downloading, navigate to your Downloads directory:

Locate the downloaded Debian package file, which should be named something like "atom-amd64.deb."

Double-click on the .deb package file to initiate the installation process.

Follow the on-screen instructions and click "Install" when prompted.

Geany

Visit the official Geany website at [https://geany.org/](https://geany.org/) for everything Geany.

Installing Geany via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Geany.
2.  Click on Geany, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Geany via APT in the Terminal:

sudo apt install geany

Installing Geany via FLATPAK in the Terminal:

flatpak install flathub org.geany.Geany

Installing Geany via SNAP in the Terminal:

sudo snap install geany --channel=latest/edge

Bluefish

Visit the official Bluefish website at [https://bluefish.openoffice.nl/index.html](https://bluefish.openoffice.nl/index.html) for all things Bluefish.

Installing Bluefish via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Bluefish.
2.  Click on Bluefish, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Bluefish via APT in the Terminal:

sudo apt install bluefish

Installing Bluefish via FLATPAK in the Terminal:

flatpak install flathub nl.openoffice.bluefish

Live Streaming Software

Live streaming software allows you to broadcast live video and audio online, capturing content from cameras, microphones, or screens. Unlike downloading, which saves files to a device, streaming plays media in real-time without local storage, using data packets for smooth playback. This saves space and provides instant access to videos and music, making it a popular choice for online entertainment and live sharing.

OBS Studio is a free, open-source streaming and screencasting software for Windows and macOS. It supports various video encoding methods and integrates with platforms like YouTube and Twitch. Users can mix audio, switch scenes seamlessly, and customize transitions. Its user-friendly interface includes a multi-scene canvas, audio mixer, and simple settings for easy setup. OBS also supports plugins and scripts for enhanced functionality, catering to both beginners and advanced users seeking professional-quality productions.

Owncast is a self-hosted, customizable live streaming and chat platform, offering full control over your content and community. It integrates with popular broadcasting software and features built-in chat for viewer engagement, custom emotes, and chat bots. Designed for streamers seeking independence from large platforms, it provides a tracking-free experience. Compatible with Linux and macOS servers, it requires minimal setup to start streaming. Owncast also connects to the Fediverse, expanding audience reach. It’s perfect for those wanting custom, ad-free streaming without the constraints of mainstream services.

OBS Studio

Visit the official OBS Studio website at [https://obsproject.com/](https://obsproject.com/) for everything OBS Studio.

Installing OBS Studio via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for OBS Studio.
2.  Click on OBS Studio, then on the Source Selection Box.
3.  Choose RPM or FLATPAK and click Install.

Installing OBS Studio via APT in the Terminal:

sudo apt install obs-studio

Installing OBS Studio via FLATPAK in the Terminal:

flatpak install flathub com.obsproject.Studio

Installing OBS Studio via SNAP in the Terminal:

sudo snap install obs-studio

Owncast

Visit the official Owncast website at [https://owncast.online/](https://owncast.online/) for everything related to Owncast.

Installing OBS Studio via APT in the Terminal:

sudo apt update

curl -s https://owncast.online/install.sh | bash

Personal Data Privacy

Personal data privacy is a fundamental right that involves controlling how personal details like name, location, or online behavior are shared. As digital interactions increase, protecting this information becomes crucial to maintain trust online. Misuse can lead to fraud, unwanted marketing, or restricted free expression, making data protection laws essential for safeguarding privacy against breaches and misuse. It's about ensuring responsible use of our information, upholding freedom and security in a connected world.

Searx is a free, open-source metasearch engine that prioritizes user privacy by not sharing IP addresses or search histories. It blocks tracking cookies and uses HTTP POST for queries to enhance privacy. Inspired by Seeks, Searx offers direct links to sites with options for cached or proxied views. It supports searches across various domains and allows users to run private instances or use public ones, including Tor services. Searx fetches results from over 80 engines, with customizable settings saved in a cookie. It also supports special search operators for tailored queries.

OpenStego is a free, Java-based steganography tool that hides data within images and offers watermarking to protect copyrights, working across various platforms. It supports encryption for extra security, making it a comprehensive solution for concealing messages or verifying ownership without altering the appearance of digital files.

Tor, short for The Onion Router, is free software that enables anonymous communication by directing Internet traffic through a global network of volunteer relays. Initially developed for secure U.S. intelligence communication, Tor now serves millions, masking users' locations and internet use from surveillance. Though intended for privacy and freedom, Tor's use spans from lawful activities to illicit trade and information leaks, sparking debate over its implications on privacy versus security.

i2pd is a C++ tool for accessing I2P, an encrypted network ensuring anonymous communication by hiding users' IP addresses. Unlike Java I2P, i2pd focuses solely on routing, requires no Java, and offers better performance with lower resource use. It supports various applications, from file-sharing to messaging, all while maintaining anonymity and security online.

Searx

Visit the official Searx website at [https://github.com/searx/searx](https://github.com/searx/searx) for all things Searx.

Installing Searx via APT in the Terminal:

First, update your package lists:

sudo apt update

Next, install necessary packages:

sudo apt install git rsync make gcc libc6-dev libssl-dev zlib1g-dev libpcre2-dev libevent-dev build-essential zlib1g-dev libpcre2-dev libsqlite3-dev libssl-dev libevent-dev libsystemd-dev curl wget git libxslt-dev python3-dev python3-babel python3-venv python3-pip

Install and use Node Version Manager (NVM) with Node.js version 16:

nvm install 16

nvm use 16

Prepare the Searx environment:

cd ~/

git clone https://github.com/searx/searx.git

cd searx

python3 -m venv venv source venv/bin/activate

Open requirements.txt and replace any werkzeug entry with:

werkzeug==2.2.2

Then save your changes.

Install the Python requirements:

pip install -r requirements.txt

Copy the default settings file and customize:

cp searx/settings.yml searx/settings_custom.yml

gedit searx/settings.yml

Edit settings.yml to your preference, including changing the secret key.

Enable advanced search in preferences.py by setting advanced_search to True:

gedit searx/preferences.py

Find settings['ui'].get('advanced_search', False) and change False to True. Save all changes and exit the editor.

Deactivate the virtual environment:

deactivate

Start Searx with:

sh -c '/home/username/searx/venv/bin/python /home/username/searx/searx/webapp.py'

Replace username with your actual username. This guide ensures Searx is installed and configured for personal use, enhancing privacy and control over your search data.

To create a desktop shortcut for Searx, open your terminal and navigate to the applications directory:

cd /usr/share/applications

Then, open a new file named searx1.desktop with your preferred text editor:

sudo gedit searx1.desktop

In the searx1.desktop file, input the following content, replacing username with your actual system username:

[Desktop Entry]

Type=Application

Name=Searx

Comment=Searx - Privacy-respecting, open-source metasearch engine

Exec=sh -c '/home/username/searx/venv/bin/python /home/username/searx/searx/webapp.py'

Icon=terminal

Terminal=false

Categories=Network;WebBrowser;

After entering the details, save your progress. Finally, exit the editor. This setup provides a convenient shortcut to launch Searx directly from your desktop.

OpenStego

Visit the official OpenStego website at [https://www.openstego.com/](https://www.openstego.com/) for all things OpenStego.

Installing OpenStego via DEB Package In The GUI:

Navigate to the release page at:

[https://github.com/syvaidya/openstego/releases](https://github.com/syvaidya/openstego/releases).

Click the latest openstego_.deb to download OpenStego.

Go to your Downloads folder.

Double-click openstego_0.8.6-1_all.deb.

Click Install.

Tor Browser Launcher

Visit the official Tor Browser Launcher website at [https://www.torproject.org/](https://www.torproject.org/) for all things Tor Browser Launcher.

Installing Tor Browser Launcher via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Tor Browser Launcher.
2.  Click on Tor Browser Launcher, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Tor Browser Launcher via APT in the Terminal:

sudo apt install torbrowser-launcher

Installing Tor Browser Launcher via FLATPAK in the Terminal:

flatpak install flathub org.torproject.torbrowser-launcher

I2pd

Visit the official I2pd website at [https://i2pd.website/](https://i2pd.website/) for all things I2pd.

Installing I2pd via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for I2pd.
2.  Click on I2pd, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing I2pd via FLATPAK in the Terminal:

flatpak install flathub website.i2pd.i2pd

Installing I2pd via SNAP in the Terminal:

sudo snap install i2pd

Hyphanet

Visit the official Hyphanet website at [https://www.hyphanet.org/](https://www.hyphanet.org/) for all things Hyphanet.

Installing Hyphanet via APT and Java in the Terminal and GUI

sudo apt update

Navigate to the release page at:

[https://www.hyphanet.org/pages/download.html](https://www.hyphanet.org/pages/download.html)

Click on "Download Hyphanet for GNU/Linux & POSIX."

Open your terminal and install the necessary dependencies with this command:

sudo apt install default-jre default-jdk libcanberra-gtk-module libcanberra-gtk3-module libcanberra-gtk-module:i386 libcanberra-gtk* xapp* gtk2-engines-murrine

Navigate to the Downloads folder:

cd ~/Downloads

Execute the installer with Java:

java -jar new_installer_offline_1497.jar

In the language selection menu, select "English" (or your preferred language). Click "OK," then click "Next."

Choose your installation path and click "Next." Confirm the creation of the target directory by clicking "OK."

Ensure the "Base" option is selected, then click "Next" three times. Select to create shortcuts in the Start Menu and additional shortcuts for the desktop.

Choose to apply these settings for the "current user" by toggling the switch next to it. Click "Next," then click "Done" to complete the installation.

ZeroNet

Visit the official ZeroNet website at [https://zeronet.io/](https://zeronet.io/) for all things ZeroNet.

Installing ZeroNet via APT in the Terminal:

sudo apt update && sudo apt upgrade

wget https://github.com/HelloZeroNet/ZeroNet-linux/archive/dist-linux64/ZeroNet-py3-linux64.tar.gz

tar xvpfz ZeroNet-py3-linux64.tar.gz

cd ZeroNet-linux-dist-linux64/ ./ZeroNet.sh

To create a .desktop shortcut for ZeroNet, open the terminal and navigate to the applications directory:

cd /usr/share/applications

Create a new file with:

sudo gedit zeronet1.desktop

In the text editor, fill in the file with the following details:

[Desktop Entry]

Name=ZeroNet

Comment=Access decentralized websites

Exec=./Downloads/ZeroNet-linux-dist-linux64/ZeroNet.sh

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

Replace /path/to/ with the actual path where ZeroNet is located on your system. Save your changes by clicking "Save," or go to "File" > "Save," or click the ☰ icon, select "Save As," and then click "Save." Close the editor once done.

Web Browsers

Web browsers are tools that let us visit websites by fetching content from the web or local storage to display on our devices. Whether on computers or mobile phones, browsers like Google Chrome and Safari connect to web servers when we enter a URL, allowing us to explore pages securely via HTTPS. They're different from search engines, serving to render web pages, store cookies for personalization and tracking, and use caches to speed up revisits. Privacy features help manage these cookies, ensuring a safer browsing experience.

Chromium, an open-source browser project by Google, aims for a safer, faster web. Unlike Chrome, it’s fully open-source, missing some features like automatic updates and certain codecs. It’s the foundation for many browsers, including Chrome and Edge, focusing on security through its multi-process architecture and contributions from various tech giants.

Ungoogled-Chromium is a version of Chromium modified to eliminate Google web service dependencies while maintaining the original experience. It enhances privacy and control, requiring manual activation of certain features. It blocks internal Google requests and borrows tweaks from projects like Inox and Bromite for a privacy-focused browsing experience.

Google Chrome, launched in 2008, is a popular web browser by Google. Built on free software from Apple WebKit and Mozilla Firefox, it’s available on multiple platforms, including Windows, Linux, macOS, iOS, and Android. Known for strong performance, it features a minimalistic interface and unique tools like the omnibox for URL and search, and a comprehensive Chrome Web Store for extensions and themes.

Microsoft Edge, launched by Microsoft in 2015, evolved from its original EdgeHTML base to a Chromium foundation in 2020\. This change enhanced compatibility and performance across devices. Edge features PDF reading, WebAssembly support, and an Internet Explorer mode for compatibility. It integrates seamlessly with Microsoft’s services, offering voice control, search functionality, and a clutter-free Reading Mode.

Thorium Browser is a high-performance variant of Chromium, optimized for modern CPUs. It mirrors Google Chrome’s functionality but introduces enhancements and patches for improved speed and privacy. It excludes Google’s telemetry and integrates alternative search engines by default, catering to a more tech-savvy audience.

Vivaldi, launched in 2015 by Vivaldi Technologies, targets tech enthusiasts and former Opera users seeking rich features and customization. It offers unique UI customization, built-in ad and tracker blockers, email support, and innovative tab management, supporting Chrome and Firefox extensions.

Brave is a free, open-source browser focused on privacy, blocking most ads and trackers by default. It rewards users with Basic Attention Tokens (BAT) for viewing optional ads. Brave includes a built-in VPN, a crypto wallet, and its own search engine, prioritizing user consent and privacy.

Firefox, developed by Mozilla, is a free, open-source web browser known for speed, privacy features, and flexibility. It supports multiple platforms and uses the Gecko engine for web standards compliance. Features include tabbed browsing, private browsing, and various developer tools. Firefox remains popular for its commitment to user privacy and web standards.

Firefox ESR is designed for organizations needing stable web deployment without frequent updates. It focuses on security and stability fixes, not the latest features, offering unmatched data protection and flexible deployment, making it ideal for businesses and universities.

Waterfox, a Firefox fork, focuses on ethics, user privacy, and performance. It supports Firefox add-ons and emphasizes privacy by disabling telemetry. Waterfox ensures a safe browsing experience without compromising speed or functionality.

LibreWolf is an independent Firefox variant focused on privacy, security, and freedom. It enhances protection against tracking and fingerprinting, excludes telemetry, and includes pre-installed uBlock Origin for ad-free browsing.

Pale Moon is a free, open-source browser optimized for modern processors. Built on its own Goanna engine, it focuses on efficiency, customization, and privacy, supporting classic plugins and extensive customization.

Mullvad Browser, developed with the Tor Project, enhances online privacy. It defaults to private browsing, leaves no cookies or history behind, and combats fingerprinting. It’s fine-tuned for privacy, minimizing tracking and fingerprinting.

Basilisk, based on the Goanna engine and UXP platform, offers a stable, change-resistant browsing experience. It supports modern web standards and various plugins, providing a familiar browsing experience.

Chromium

Visit the official Chromium website at [https://www.chromium.org/chromium-projects/](https://www.chromium.org/chromium-projects/) for all things Chromium.

Installing Chromium via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Chromium.
2.  Click on Chromium, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Chromium via APT in the Terminal:

sudo apt install chromium

Installing Chromium via FLATPAK in the Terminal:

flatpak install flathub org.chromium.Chromium

Installing Chromium via SNAP in the Terminal:

sudo snap install chromium

Ungoogled-Chromium

Visit the official Ungoogled-Chromium website at [https://github.com/ungoogled-software/ungoogled-chromium](https://github.com/ungoogled-software/ungoogled-chromium) for all things Ungoogled-Chromium.

Installing Ungoogled-Chromium via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Ungoogled-Chromium.
2.  Click on Ungoogled-Chromium, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Ungoogled-Chromium via FLATPAK in the Terminal:

flatpak install flathub io.github.ungoogled_software.ungoogled_chromium

Google Chrome

Visit the official Google Chrome website at [https://www.google.com/intl/en_uk/chrome/](https://www.google.com/intl/en_uk/chrome/) for all things Google Chrome.

Installing Google Chrome via APT in the Terminal:

sudo apt update && sudo apt upgrade

wget -qO - https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor | sudo tee /etc/apt/keyrings/google-chrome.gpg

sudo sh -c 'echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/google-chrome.gpg] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list'

sudo apt update

sudo apt install google-chrome-stable

Installing Google Chrome via .deb in the GUI:

Navigate to the release page at:

[https://www.google.com/chrome/](https://www.google.com/chrome/)

Click "Download Chrome."

Click the circle next to "64 bit .deb (For Debian/Ubuntu)."

Click "Accept and Install" to download Chrome.

Go to your Downloads folder.

Double-click google-chrome-stable_current_amd64.deb.

Click "Install."

Microsoft Edge

Visit the official Microsoft Edge website at [https://www.microsoft.com/en-us/edge](https://www.microsoft.com/en-us/edge) for all things Microsoft Edge.

Installing Microsoft Edge via APT in the Terminal:

curl -sSL -O https://packages.microsoft.com/config/<distribution>/<version>/packages-microsoft-prod.deb

sudo dpkg -i packages-microsoft-prod.deb

rm packages-microsoft-prod.deb

sudo apt update

sudo apt install microsoft-edge-stable

[Filename will vary depending on the version of the Microsoft edge browser used].

Installing Microsoft Edge via .deb in the GUI:

Navigate to the release page at:

[https://www.microsoft.com/en-us/edge/download?form=MA13FJ](https://www.microsoft.com/en-us/edge/download?form=MA13FJ).

Click "Accept and download" to download Microsoft Edge.

Go to your Downloads folder.

Double-click microsoft-edge-stable_125.0.2535.92-1_amd64.deb.

Click "Install."

Thorium

Visit the official Thorium website at [https://thorium.rocks/](https://thorium.rocks/) for all things Thorium.

Installing Thorium via .rpm in the GUI:

Navigate to the release page at:

[https://github.com/Alex313031/thorium/releases](https://github.com/Alex313031/thorium/releases)

Click the latest thorium-browser_AVX2.rpm to download Thorium.

Go to your Downloads folder.

Double-click thorium-browser_124.0.6367.218_AVX2.deb.

Click "Install."

Vivaldi

Visit the official Vivaldi website at [https://vivaldi.com/](https://vivaldi.com/) for all things Vivaldi.

Installing Vivaldi via APT in the Terminal:

sudo apt update

sudo apt install wget

wget -qO- https://repo.vivaldi.com/archive/linux_signing_key.pub | gpg --dearmor | sudo dd of=/usr/share/keyrings/vivaldi-browser.gpg

echo "deb [signed-by=/usr/share/keyrings/vivaldi-browser.gpg arch=$(dpkg --print-architecture)] https://repo.vivaldi.com/archive/deb/ stable main" | sudo dd of=/etc/apt/sources.list.d/vivaldi-archive.list

sudo apt update && sudo apt install vivaldi-stable

Installing Vivaldi via .deb in the GUI:

Navigate to the release page at:

[https://vivaldi.com/download/?platform=linux](https://vivaldi.com/download/?platform=linux)

Click "Vivaldi for Linux DEB" to download Vivaldi.

Go to your Downloads folder.

Double-click vivaldi-stable_6.7.3329.41-1_amd64.deb.

Click "Install."

Brave

Visit the official Brave website at [https://brave.com/](https://brave.com/) for all things Brave.

Installing Brave via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Brave.
2.  Click on Brave, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Brave via APT in the Terminal:

sudo apt update && sudo apt upgrade

sudo apt install curl

sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update && sudo apt install brave-browser

Installing Brave via FLATPAK in the Terminal:

flatpak install flathub com.brave.Browser

Installing Brave via SNAP in the Terminal:

sudo snap install brave

Firefox

Visit the official Firefox website at [https://www.mozilla.org/en-GB/firefox/new/](https://www.mozilla.org/en-GB/firefox/new/) for all things Firefox.

Installing Firefox via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Firefox.
2.  Click on Firefox, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Firefox via APT in the Terminal:

sudo apt install firefox

Installing Firefox via FLATPAK in the Terminal:

flatpak install flathub org.mozilla.firefox

Installing Firefox via SNAP in the Terminal:

sudo snap install firefox

Firefox ESR

Visit the official Firefox ESR website at [https://www.mozilla.org/en-GB/firefox/enterprise/](https://www.mozilla.org/en-GB/firefox/enterprise/) for all things Firefox ESR.

Installing Firefox via .tar.xz in the GUI:

Navigate to the release page at:

[https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr](https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr)

Click "Which browser would you like to download?" and select "Firefox Extended Support Release."

Click "Select your preferred installer" and choose "Linux 64-bit."

Click "Select your preferred language" and select "English (British)."

Click "Download Now" to download Firefox ESR.

Go to your Downloads folder.

Double-click firefox-115.11.0esr.tar.bz2.

Select firefox and click "Extract."

Go to ~/Downloads/firefox.

Double-click firefox.

To create a desktop shortcut for Firefox ESR, open the terminal and enter the following commands:

cd /usr/share/applications

sudo gedit firefoxesr1.desktop

Update the firefoxesr1.desktop file with the following content:

[Desktop Entry]

Name=Firefox ESR

Comment=Firefox ESR

Exec=./Downloads/firefox/firefox

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

To save your changes, click "Save," or go to "File" and select "Save," or click the ☰ icon, choose "Save As," and then click "Save." Once done, exit the editor. Ensure the Exec= path correctly points to the Firefox ESR executable's location on your system.

Waterfox

Visit the official Waterfox website at [https://www.waterfox.net/](https://www.waterfox.net/) for all things Waterfox.

Installing Waterfox via FLATPAK Package through Software Manager:

1.  Open GNOME Software and search for Waterfox.
2.  Click on Waterfox, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Waterfox via FLATPAK in the Terminal:

flatpak install flathub org.mozilla.Waterfox

Installing Firefox via .tar.xz in the GUI:

Navigate to the release page at:

[https://www.waterfox.net/download/](https://www.waterfox.net/download/)

In the same row as Linux, click "Download" to download Waterfox.

Go to your Downloads folder.

Double-click waterfox-G6.0.16.tar.bz2.

Select waterfox and click "Extract."

Go to ~/Downloads/waterfox.

Double-click waterfox.

To create a desktop shortcut for Waterfox, open the terminal and enter the following commands:

cd /usr/share/applications

sudo gedit Waterfox1.desktop

Update the Waterfox1.desktop file with the following content:

[Desktop Entry]

Name=Waterfox

Comment=Waterfox

Exec=./Downloads/waterfox/waterfox

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

To save your changes, click "Save," or go to "File" and select "Save," or click the ☰ icon, choose "Save As," and then click "Save." Once done, exit the editor. Ensure the Exec= path correctly points to the Waterfox executable's location on your system.

LibreWolf

Visit the official LibreWolf website at [https://librewolf.net](https://librewolf.net/) for all things LibreWolf.

Installing LibreWolf via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for LibreWolf.
2.  Click on LibreWolf, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Firefox via APT in the Terminal:

sudo apt update && sudo apt install -y wget gnupg lsb-release apt-transport-https ca-certificates

distro=$(if echo " una bookworm vanessa focal jammy bullseye vera uma " | grep -q " $(lsb_release -sc) "; then lsb_release -sc; else echo focal; fi)

wget -O- https://deb.librewolf.net/keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/librewolf.gpg

sudo tee /etc/apt/sources.list.d/librewolf.sources << EOF > /dev/null

Types: deb

URIs: https://deb.librewolf.net

Suites: $distro

Components: main

Architectures: amd64

Signed-By: /usr/share/keyrings/librewolf.gpg

EOF

sudo apt update && sudo apt install librewolf

Installing Firefox via FLATPAK in the Terminal:

flatpak install flathub io.gitlab.librewolf-community

Pale Moon

Visit the official Pale Moon website at [https://www.palemoon.org/](https://www.palemoon.org/) for all things Pale Moon.

Installing Pale Moon via .tar.xz in the GUI:

Navigate to the release page at:

[https://www.palemoon.org/download.shtml](https://www.palemoon.org/download.shtml)

In the same row as Linux 64-bit GTK3, click "Download tarball" to download Pale Moon.

Go to your Downloads folder.

Double-click palemoon-33.1.1.linux-x86_64-gtk3.tar.xz.

Select palemoon and click "Extract."

Go to ~/Downloads/palemoon.

Double-click palemoon.

To create a desktop shortcut for Pale Moon, open the terminal and enter the following commands:

cd /usr/share/applications

sudo gedit palemoon1.desktop

Update the palemoon1.desktop file with the following content:

[Desktop Entry]

Name=Pale Moon

Comment=Pale Moon

Exec=./Downloads/palemoon/palemoon

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

To save your changes, click "Save," or go to "File" and select "Save," or click the ☰ icon, choose "Save As," and then click "Save." Once done, exit the editor. Ensure the Exec= path correctly points to the Pale Moon executable's location on your system.

Mullvad Browser

Visit the official Mullvad Browser website at [https://mullvad.net/en/browser](https://mullvad.net/en/browser) for all things Mullvad Browser.

Installing Mullvad Browser via .tar.xz in the GUI:

Navigate to the release page at:

[https://mullvad.net/en/download/browser/linux](https://mullvad.net/en/download/browser/linux)

Click the Linux tab.

Click "Download" to download Mullvad Browser.

Go to your Downloads folder.

Double-click mullvad-browser-linux-x86_64-13.0.16.tar.xz.

Select mullvad-browser and click "Extract."

Go to ~/Downloads/mullvad-browser/Browser.

Double-click mullvadbrowser.real.

To create a desktop shortcut for Mullvad Browser, open the terminal and enter the following commands:

cd /usr/share/applications

sudo gedit mullvad-browser1.desktop

Update the mullvad-browser1.desktop file with the following content:

[Desktop Entry]

Name=Mullvad Browser

Comment=Mullvad Browser

Exec=./Downloads/mullvad-browser/Browser/mullvadbrowser.real

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

To save your changes, click "Save," or go to "File" and select "Save," or click the ☰ icon, choose "Save As," and then click "Save." Once done, exit the editor. Ensure the Exec= path correctly points to the Mullvad Browser executable's location on your system.

Basilisk

Visit the official Basilisk website at [https://www.basilisk-browser.org/](https://www.basilisk-browser.org/) for all things Basilisk.

Installing Basilisk via .tar.xz in the GUI:

Navigate to the release page at:

[https://www.basilisk-browser.org/download.shtml](https://www.basilisk-browser.org/download.shtml)

Under United States, in the same row as Linux x86_64 tarball, click x86 64-bit GTK3 to download Basilisk.

Go to your Downloads folder.

Double-click basilisk-20240510185247.linux-x86_64-gtk3.tar.

Select basilisk and click "Extract."

Go to ~/Downloads/basilisk.

Double-click basilisk.

To create a desktop shortcut for Basilisk, open the terminal and enter the following commands:

cd /usr/share/applications

sudo gedit basilisk1.desktop

Update the basilisk1.desktop file with the following content:

[Desktop Entry]

Name=Basilisk

Comment=Basilisk

Exec=./Downloads/basilisk/basilisk

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

To save your changes, click "Save," or go to "File" and select "Save," or click the ☰ icon, choose "Save As," and then click "Save." Once done, exit the editor. Ensure the Exec= path correctly points to the Basilisk executable's location on your system.

Password Managers

Password managers are secure apps that store all your login details in one place, eliminating the need to remember each one. They are crucial in today's digital world, offering convenience and boosting security by generating strong passwords and protecting against identity theft. With features like encryption and cloud storage, they are an excellent choice for managing personal and work accounts across different devices. While free versions are available, investing in a paid service ensures maximum security and features, making it a valuable tool for protecting your digital life.

LastPass, managed by GoTo, is a robust password manager designed to securely store and handle passwords. It offers a web interface, browser extensions, and mobile apps, ensuring easy access and synchronization of passwords across devices. With AES-256 encryption, LastPass protects user data, offering features like automated form filling, password generation, and secure note storage. It supports two-factor authentication with options like the LastPass Authenticator, enhancing security. Available for major browsers and smartphones, LastPass facilitates seamless password management, even offline, and includes a user-set password hint for emergency access.

Bitwarden is a versatile, open-source password manager that combines security with ease of use, providing encrypted storage for credentials and sensitive data across multiple platforms. It supports various devices with apps for desktops, browsers, and mobiles, plus a CLI tool, ensuring your data is safe yet accessible anywhere. With features like two-factor authentication, passwordless entry, and secure sharing, it caters to everyone from individuals to businesses. Its commitment to privacy is underscored by zero-knowledge encryption and options for cloud or self-hosting. Beyond passwords, it manages notes, cards, and more.

KeePassXC is a free, open-source password manager that started as a KeePassX community fork, offering a secure place to store passwords across platforms like Windows, macOS, Linux, and BSD. It supports KeePass 2.x (.kdbx) formats, imports older databases, and adds extra security with key files and YubiKey. Praised by the EFF for its privacy, KeePassXC features encryption, no cloud reliance, and cross-platform compatibility, keeping your data under your control. Its browser extensions enhance user experience by autofilling passwords.

Buttercup is a free, open-source password manager that provides secure 256-bit AES encryption for your credentials. It's designed for simplicity, making it easy to store and find your login details. Available for all major desktop platforms and mobile devices, it supports seamless integration across devices. With features like auto-lock, customizable entries, and a built-in trash, managing passwords is straightforward. Buttercup also offers a Chrome extension, enhancing its utility.

LastPass

Visit the official LastPass website at [https://www.lastpass.com/](https://www.lastpass.com/) for everything related to LastPass.

Installing LastPass via .sh in the Terminal and GUI:

Navigate to the release page at:

[https://lastpass.com/lplinux.php](https://lastpass.com/lplinux.php)

Click to download the Latest Linux Release.

Navigate to ~/Downloads.

Double-click lplinux.tar.bz2.

Select "Extract" and extract the files into ~/Downloads.

Open Terminal in ~/Downloads by right-clicking on an empty space and selecting "Open in Terminal."

Enter the following command in the terminal:

chmod +x install_lastpass.sh

Run the script by entering:

./install_lastpass.sh

Bitwarden

Visit the official Bitwarden website at [https://bitwarden.com/](https://bitwarden.com/) for all things Bitwarden.

Installing Bitwarden via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Bitwarden.
2.  Click on Bitwarden, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Bitwarden via FLATPAK in the Terminal:

flatpak install flathub com.bitwarden.desktop

Installing Bitwarden via SNAP in the Terminal:

sudo snap install bitwarden

KeePassXC

Visit the official KeePassXC website at [https://keepassxc.org/](https://keepassxc.org/) for all things KeePassXC.

Installing KeePassXC via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for KeePassXC.
2.  Click on KeePassXC, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing KeePassXC via APT in the Terminal:

sudo apt install keepassxc

Installing KeePassXC via FLATPAK in the Terminal:

flatpak install flathub org.keepassxc.KeePassXC

Installing KeePassXC via SNAP in the Terminal:

sudo snap install keepassxc

Buttercup

Visit the official Buttercup website at [https://buttercup.pw/](https://buttercup.pw/) for all things Buttercup.

Installing Buttercup via AppImage in the GUI:

Navigate to the release page at:

[https://buttercup.pw/](https://buttercup.pw/)

Click "Linux (AppImage)" to download Buttercup.

Download the file to your ~/Downloads folder.

Locate the Buttercup-linux-x86_64.AppImage file in your Downloads folder, right-click on it, and select "Properties."

In the Properties menu, go to the "Permissions" tab and check the box to "Set as executable."

Double-click the Buttercup-linux-x86_64.AppImage file to start the installation process.

To create a Buttercup AppImage .desktop shortcut, follow these steps in your terminal:

Navigate to the applications directory with the command:

cd /usr/share/applications

Open a new .desktop file for editing by running:

sudo gedit buttercup1.desktop

In the buttercup1.desktop file, enter the following details:

[Desktop Entry]

Name=Buttercup

Comment=Buttercup

Exec=./Applications/Buttercup.AppImage

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

To save your progress, click "Save." Alternatively, you can click "File," then "Save," or click the ☰ icon, select "Save As," and finally click "Save." After saving, close the editor.

Media Players

Media players, both software and hardware, play audio and video files from sources like storage devices, discs, or the internet. They may need codecs for some formats, can stream online content, and vary in DVD and Blu-ray support. The choice of player can impact media quality, and using multiple players for different formats is common. Unlike media servers that store and share files, players are not designed for editing but often support subtitles, updates, and skins. Open-source players offer extensive format support and customization. Playlists help organize media, and some players can convert file formats or stream internet radio. Lightweight players use minimal resources, ideal for less powerful systems.

VLC is a versatile, free, and open-source media player for desktops and mobile devices like Android and iOS. Developed by the VideoLAN project, it plays various audio, video, and streaming formats, including DVDs. It streams media and transcodes files, with built-in codecs from the libavcodec library. VLC supports encrypted DVD playback on Linux and macOS through libdvdcss and is available on major app stores, though its legal status varies by region due to DVD decryption.

Parole Media Player, designed for the Xfce desktop, uses the GStreamer framework to play various media types, including local files, DVDs, and streams. It’s lightweight, extensible with plugins, and efficient with minimal resource use. It supports drag-and-drop playlists and basic playback controls but lacks advanced configuration options and struggles with corrupted files and high-resolution displays, making it less versatile than players like mpv or VLC.

SMPlayer, free and open-source for Windows and Linux, offers a seamless experience with built-in codecs for any video and audio format. It remembers playback settings per file, ensuring you resume with the same settings. As a GUI for MPlayer, it supports YouTube playback, subtitle downloads, and offers a range of skins and advanced features without needing external codecs. Available in over 30 languages, SMPlayer makes media playback easy and customizable across platforms.

Haruna, an open-source video player for KDE Plasma, offers features like online video playback via youtube-dl, YouTube playlist support, auto-playlists, and customizable shortcuts. Its intuitive design and compatibility with various video formats make it a top choice for Linux users. With auto-skipping chapters and adjustable subtitle settings, Haruna enhances viewing experiences. Available on Flathub and Ubuntu repos, it’s a must-try for those seeking a comprehensive media player.

Dragon Player, a multimedia player for the KDE desktop, focuses on simplicity, providing a straightforward experience without excessive features. Developed from Codeine for KDE 3 and now for KDE SC 4, it uses Phonon for multimedia framework support. Its features include a clean interface, video resumption, subtitle support, adjustable video display settings, and CD/DVD playback. Free and open-source, Dragon Player is ideal for those who value ease of use over complexity.

VLC

Visit the official VLC website at [https://www.videolan.org/](https://www.videolan.org/) for all things VLC.

Installing VLC via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for VLC.
2.  Click on VLC, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing VLC via APT in the Terminal:

sudo apt install vlc

Installing VLC via FLATPAK in the Terminal:

flatpak install flathub org.videolan.VLC

Installing VLC via SNAP in the Terminal:

sudo snap install vlc

SMPlayer

Visit the official SMPlayer website at [https://www.smplayer.info/](https://www.smplayer.info/) for all things SMPlayer.

Installing SMPlayer via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for SMPlayer.
2.  Click on SMPlayer, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing SMPlayer via APT in the Terminal:

sudo apt install smplayer

Installing SMPlayer via FLATPAK in the Terminal:

flatpak install flathub info.smplayer.SMPlayer

Installing SMPlayer via SNAP in the Terminal:

sudo snap install smplayer

Haruna

Visit the official Haruna website at [https://apps.kde.org/en-gb/haruna/](https://apps.kde.org/en-gb/haruna/) for all things Haruna.

Installing Haruna via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Haruna.
2.  Click on Haruna, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Haruna via APT in the Terminal:

sudo apt install haruna

Installing Haruna via FLATPAK in the Terminal:

flatpak install flathub org.kde.haruna

Installing Haruna via SNAP in the Terminal:

sudo snap install haruna

Dragon Player

Visit the official Dragon Player website at [https://apps.kde.org/en-gb/dragonplayer/](https://apps.kde.org/en-gb/dragonplayer/) for all things Dragon Player.

Installing Dragon Player via SYSTEM PACKAGE Package through Software Manager:

1.  Open Software Manager and search for Dragon Player.
2.  Click on Dragon Player, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing Dragon Player via APT in the Terminal:

sudo apt install dragon

Installing Dragon Player via SNAP in the Terminal:

sudo snap install dragon

System Utilities

System utilities are software programs that help manage and optimize a computer’s system or application software. They work behind the scenes, performing tasks like backing up data, compressing disks, and managing files. These utilities can be part of the operating system or installed separately to enhance or replace default tools. They play a crucial role in ensuring security, optimizing performance, and keeping computers running smoothly. Some examples include anti-virus programs, disk defragmenters, debuggers, diagnostic programs, and network utilities. They are essential for both regular users and IT professionals, requiring different levels of user privileges based on their impact on the system.

QDirStat is a graphical tool for managing disk space, offering a dual view of directories and files with a traditional tree and a colorful treemap. It introduces features like multi-selection, custom cleanup actions, and detailed error reporting. It's user-friendly and versatile, making it easy to identify and manage files by their types.

Psensor is a GTK+ based software for monitoring hardware temperatures and CPU fan speeds in real-time. It can also monitor remote servers and display Linux CPU usage. Psensor automatically detects supported hardware, presenting data as text and detailed graphs. It includes configurable alarms and alerts for critical temperature and fan speed issues.

Stacer is an open-source system optimizer and application monitor for Linux. It allows users to manage startup apps, clean unnecessary files, handle system services and processes, and uninstall applications. Stacer also offers real-time resource usage monitoring and an APT repository manager for easy package repository edits.

BleachBit is a tool for freeing up disk space and protecting privacy on Linux and Windows. It cleans out unnecessary files and can shred files to prevent recovery. BleachBit supports a wide range of applications and includes advanced features like vacuuming Firefox to boost speed, making it essential for maintaining system performance and security.

SoundConverter is an audio file converter for the GNOME Desktop, supporting formats like Ogg Vorbis, AAC, MP3, and FLAC. It offers fast, multithreaded conversion and can extract audio from video files. Users can easily rename files and organize folders based on tags, streamlining audio conversion tasks.

Converseen is a versatile image processor for Windows, Linux, macOS, and FreeBSD. It supports over 100 formats, allowing for conversions, resizing, rotation, and flipping of images. Users can also transform PDF documents into images and rename files in bulk. Converseen is user-friendly and practical for any image processing need.

GParted is a free application for managing disk partitions with GNU Parted. It simplifies tasks like creating, resizing, moving, and copying partitions, making it useful for setting up new operating systems and reorganizing disk space. GParted supports various file systems and storage devices, catering to both novice and advanced users.

HardInfo2 is a system profiler and benchmark tool for Linux, providing detailed insights into hardware and software components. It offers extensive reports in HTML or plain text and allows benchmark comparisons. HardInfo2 organizes data in an accessible format, making it easy to diagnose and analyze system performance and hardware specifications.

gpustat is a command-line utility for monitoring NVIDIA Graphics Devices. It offers real-time GPU status querying with features like a built-in watch mode, detailed GPU properties, running process names, and power usage. It's a valuable tool for those needing detailed insights into their NVIDIA GPU's performance.

Czkawka, named after the Polish word for "hiccup," is a fast and free application designed to declutter your computer by removing unnecessary files. Built in Rust, it stands out for its speed, using advanced algorithms and multithreading to perform tasks efficiently. This open-source tool is ad-free and available on Linux, Windows, macOS, and FreeBSD. It offers both CLI and GUI frontends, with the GUI using GTK 4 or Slint frameworks to suit different user preferences. Czkawka ensures privacy by not accessing the internet or collecting data. It supports multiple languages and has various tools for finding duplicates, empty folders, large files, and more. It can also search for similar images, videos, and music, and identify invalid symbolic links, broken files, and mismatches between file content and extensions.

QDirStat

Visit the official QDirStat website at [https://github.com/shundhammer/qdirstat](https://github.com/shundhammer/qdirstat) for all things QDirStat.

Installing QDirStat via SYSTEM PACKAGE Package through Software Manager:

1.  Open Software Manager and search for QDirStat.
2.  Click on QDirStat, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing QDirStat via APT in the Terminal:

sudo apt install qdirstat

Psensor

Visit the official Psensor website at [https://github.com/chinf/psensor](https://github.com/chinf/psensor) for all things Psensor.

Installing Psensor via SYSTEM PACKAGE Package through Software Manager:

1.  Open Software Manager and search for Psensor.
2.  Click on Psensor, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing Psensor via APT in the Terminal:

sudo apt install psensor

sudo sensors-detect

sensors

Stacer

Visit the official Stacer website at [https://oguzhaninan.github.io/Stacer-Web/](https://oguzhaninan.github.io/Stacer-Web/) for all things Stacer.

Installing Stacer via SYSTEM PACKAGE Package through Software Manager:

1.  Open Software Manager and search for Stacer.
2.  Click on Stacer, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing Stacer via APT in the Terminal:

sudo apt install stacer

Bleachbit

Visit the official Bleachbit website at [https://www.bleachbit.org/](https://www.bleachbit.org/) for all things Bleachbit.

Installing Bleachbit via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Bleachbit.
2.  Click on Bleachbit, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Bleachbit via APT in the Terminal:

sudo apt install bleachbit

Installing Bleachbit via FLATPAK in the Terminal:

flatpak install flathub org.bleachbit.BleachBit

SoundConverter

Visit the official SoundConverter website at [https://soundconverter.org/](https://soundconverter.org/) for all things SoundConverter.

Installing SoundConverter via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for SoundConverter.
2.  Click on SoundConverter, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing SoundConverter via APT in the Terminal:

sudo apt install soundconverter

Installing SoundConverter via FLATPAK in the Terminal:

flatpak install flathub org.soundconverter.SoundConverter

Converseen

Visit the official Converseen website at [https://converseen.fasterland.net/](https://converseen.fasterland.net/) for all things Converseen.

Installing Converseen via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Converseen.
2.  Click on Converseen, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Converseen via APT in the Terminal:

sudo apt install converseen

Installing Converseen via FLATPAK in the Terminal:

flatpak install flathub net.fasterland.converseen

Installing Converseen via SNAP in the Terminal:

sudo snap install converseen

GParted

Visit the official GParted website at [https://gparted.org/index.php](https://gparted.org/index.php) for all things GParted.

Installing GParted via SYSTEM PACKAGE Package through Software Manager:

1.  Open Software Manager and search for GParted.
2.  Click on GParted, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing GParted via APT in the Terminal:

sudo apt install gparted

Hardinfo

Visit the official Hardinfo website at [https://github.com/lpereira/hardinfo](https://github.com/lpereira/hardinfo) for all things Hardinfo.

Installing Hardinfo via SYSTEM PACKAGE Package through Software Manager:

1.  Open Software Manager and search for Hardinfo.
2.  Click on Hardinfo, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing Hardinfo via APT in the Terminal:

sudo apt install hardinfo

Gpustat

Visit the official Gpustat website at [https://github.com/wookayin/gpustat](https://github.com/wookayin/gpustat) for all things Gpustat.

Installing Gpustat via APT in the Terminal:

sudo apt install gpustat

gpustat

Czkawka

Visit the official Czkawka website at [https://github.com/qarmin/czkawka](https://github.com/qarmin/czkawka) for all things Czkawka.

Installing Czkawka via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Czkawka.
2.  Click on Czkawka, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing Czkawka via FLATPAK in the Terminal:

flatpak install flathub com.github.qarmin.czkawka

Installing Czkawka via SNAP in the Terminal:

sudo snap install czkawka

Instant Messaging

Instant messaging software allows users to communicate instantly through text over networks. Unlike emails, conversations happen in real-time, often with features like emojis, voice, video chat, and file sharing. It's useful for quick exchanges but relies on central servers, raising privacy concerns. Some services include chat rooms and mobile messaging, enhancing connectivity. However, users face potential service suspensions and privacy issues.

Discord is a social platform for instant messaging, voice, and video calls. It supports communities through servers where users chat, share media, and hang out. With apps for major platforms, it’s popular among gamers and various interest groups. Discord offers private and group communication tools, low-latency technology for seamless interaction, and custom moderation features. It blends everyday conversation ease with the excitement of larger communities, making digital gatherings easy and inclusive. More info at [https://discord.com](https://discord.com/).

Skype, from Microsoft, offers free video, voice calls, and messaging. It works on various devices and is free for basic features, with paid options for phone calls and SMS. Skype connects the business world, enhancing collaboration. It provides instant messaging, voice chat, and more, with unique IDs for users. Though it doesn’t support emergency calls, it offers features like background blur for video chats. Recently, Skype integrated the Bing AI chatbot. More info at [https://skype.com](https://skype.com/).

Session is a privacy-focused messaging app by The Oxen Project. It’s available on macOS, Windows, Linux, iOS, and Android, using a blockchain network for secure communication without phone numbers or emails. Instead, users have a unique 66-digit ID. Despite lacking two-factor authentication and evolving protocols, its encryption is independently verified. Session offers a secure way to exchange messages, voice notes, and media. More info at [https://getsession.org](https://getsession.org/).

Pidgin is a free, open-source messaging client supporting many protocols. It allows users to connect to various services through one interface. Known for robust encryption with the Off-the-Record Messaging plugin, it’s popular among privacy enthusiasts and included in Tails OS. Pidgin has a user-friendly GTK+ interface, works on multiple operating systems, and supports extensibility through plugins for added functionality. More info at [https://pidgin.im](https://pidgin.im/).

Ferdium is a desktop app consolidating favorite services into one platform for easy access. It supports multiple accounts of the same service, offers workspaces to separate personal and professional life, and includes a Todo panel. Adding custom services is easy, ensuring flexibility. Ferdium prioritizes privacy, offers cloud sync across devices, and hibernates unused services to save resources. Originating from Franz, it enhances the experience with additional features and compatibility with Franz accounts. More info at [https://ferdium.org](https://ferdium.org/).

Signal is a secure messaging app with state-of-the-art encryption. It offers free text, voice messages, photos, videos, and calls without fees, even long distances. Signal includes encrypted stickers and group chats, with no ads, trackers, or ties to major tech companies. As a nonprofit supported by donations, it stands for privacy and accessibility. More info at [https://signal.org](https://signal.org/).

Telegram is a messaging app blending communication and social networking. Launched in 2013, it supports messaging, media sharing, and voice or video calls with end-to-end encryption. Users enjoy features like stories, large groups, and channels for broadcasts. Telegram’s open API allows custom bots and mini-apps, enriching user interaction. Available on major platforms, it stands out for security, user-friendly interface, and rich functionality. More info at [https://telegram.org](https://telegram.org/).

Discord

Visit the official Discord website at [https://discord.com/](https://discord.com/) for all things Discord.

Installing Discord via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Discord.
2.  Click on Discord, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Discord via FLATPAK in the Terminal:

flatpak install flathub com.discordapp.Discord

Installing Discord via SNAP in the Terminal:

sudo snap install discord

Skype

Visit the official Skype website at [https://www.skype.com/en/](https://www.skype.com/en/) for all things Skype.

Installing Skype via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Skype.
2.  Click on Skype, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Skype via APT in the Terminal:

sudo apt update

sudo apt install software-properties-common apt-transport-https curl ca-certificates

curl -fsSL https://repo.skype.com/data/SKYPE-GPG-KEY | sudo gpg --dearmor | sudo tee /usr/share/keyrings/skype.gpg > /dev/null

echo deb [arch=amd64 signed-by=/usr/share/keyrings/skype.gpg] https://repo.skype.com/deb stable main | sudo tee /etc/apt/sources.list.d/skype.list

sudo apt update

sudo apt install skypeforlinux

Installing Skype via FLATPAK in the Terminal:

flatpak install flathub com.skype.Client

Installing Skype via SNAP in the Terminal:

sudo snap install skype

Installing Skype via .deb in the GUI:

Navigate to the release page at:

[https://repo.skype.com/SYSTEM PACKAGE/pool/main/s/skypeforlinux/](https://repo.skype.com/rpm/pool/main/s/skypeforlinux/)

Click the latest skypeforlinux_amd64.deb to download Skype.

Go to your Downloads folder.

Double-click skypeforlinux__amd64.deb.

Click Install.

Session

Visit the official Session website at [https://getsession.org/](https://getsession.org/) for all things Session.

Installing Session via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Session.
2.  Click on Session, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Session via FLATPAK in the Terminal:

flatpak install flathub network.loki.Session

Pidgin

Visit the official Pidgin website at [https://www.pidgin.im/](https://www.pidgin.im/) for all things Pidgin.

Installing Pidgin via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Pidgin.
2.  Click on Pidgin, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE OR FLATPAK and click Install.

Installing Pidgin via APT in the Terminal:

sudo apt install pidgin

Installing Pidgin via FLATPAK in the Terminal:

flatpak install flathub im.pidgin.Pidgin

Ferdium

Visit the official Ferdium website at [https://ferdium.org/](https://ferdium.org/) for all things Ferdium.

Installing Ferdium via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Ferdium.
2.  Click on Ferdium, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Ferdium via FLATPAK in the Terminal:

flatpak install flathub org.ferdium.Ferdium

Installing Ferdium via SNAP in the Terminal:

sudo snap install ferdium

Signal

Visit the official Signal website at [https://signal.org/](https://signal.org/) for all things Signal.

Installing Signal via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Signal.
2.  Click on Signal, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Signal via FLATPAK in the Terminal:

flatpak install flathub org.signal.Signal

Installing Signal via SNAP in the Terminal:

sudo snap install signal-desktop

Telegram

Visit the official Telegram website at [https://telegram.org/](https://telegram.org/) for all things Telegram.

Installing Telegram via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Telegram.
2.  Click on Telegram, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Telegram via FLATPAK in the Terminal:

flatpak install flathub org.telegram.desktop

Installing Telegram via SNAP in the Terminal:

sudo snap install telegram-desktop

Remote Working

Remote working software enables employees to collaborate, communicate, and manage tasks from anywhere, reducing the need for physical offices. This technology, evolving since the 1970s and booming with the internet and cloud computing, supports work-from-home and hybrid models. It offers cost savings, flexibility, and access to a wider talent pool, but challenges include reduced face-to-face interaction and potential feelings of isolation.

Zoom, a video conferencing app, gained popularity during COVID-19 by connecting millions through video, audio, and chat in virtual meetings. It is free to download and offers both paid and free plans. The free plan supports meetings with up to 100 people for 40 minutes. Users can share screens, files, and chat privately. No account is needed to join meetings, but one is required to host. Its ease of use and ability to gather large groups, even on the free version, make it a preferred choice for many. Visit the official website at [https://zoom.us/](https://zoom.us/).

Slack is a business messaging app that enhances team communication and collaboration. It offers dedicated channels for seamless information sharing and interaction within and across teams, regardless of location or time zone. Slack supports flexible, asynchronous work, allowing access to information and colleagues when needed. It fosters inclusivity by giving everyone equal access to shared, searchable info, speeding up decision-making. Integrating generative AI and various apps, Slack simplifies workflows. Whether through messaging, audio, video, or live huddles, Slack adapts to diverse work preferences, uniting teams big and small in a secure environment. Visit the official website at [https://slack.com/](https://slack.com/).

Citrix Workspace app offers secure and instant access to all essential resources for user productivity, integrating virtual desktops, apps, and web services with features like single sign-on. It's a versatile client for both cloud and on-prem environments, succeeding Citrix Receiver with technologies like HDX for a high-definition experience across all major OS and browsers. This app ensures secure, efficient management of apps and desktops, enhancing user experience with advanced search and seamless internet browsing. Visit the official website at [https://www.citrix.com/](https://www.citrix.com/).

Zoom

Visit the official Zoom website at [https://zoom.us/](https://zoom.us/) for all things Zoom.

Installing Zoom via APT in the Terminal:

sudo apt update

sudo apt install gdebi libglib2.0-0 libxcb-shape0 libxcb-shm0 libxcb-xfixes0 libxcb-randr0 libxcb-image0 libfontconfig1 libgl1-mesa-glx libxi6 libsm6 libxrender1 libpulse0 libxcomposite1 libxslt1.1 libsqlite3-0 libxcb-keysyms1 libxcb-xtest0 ibus libegl1-mesa libxcb-cursor0

Navigate to the release page at:

[https://zoom.us/download?os=linux](https://zoom.us/download?os=linux)

Click the box in the same row as Linux Type.

Select Debian.

Click the box in the same row as OS Architecture.

Select 64-bit.

Click Download to download Zoom.

Go to your Downloads folder.

Double-click zoom_amd64.deb.

Click Install.

Slack

Visit the official Slack website at [https://slack.com/intl/en-gb/](https://slack.com/intl/en-gb/) for all things Slack.

Installing Slack via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Slack.
2.  Click on Slack, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing Slack via FLATPAK in the Terminal:

flatpak install flathub com.slack.Slack

Installing Slack via SNAP in the Terminal:

sudo snap install slack

Citrix Workspace

Visit the official Citrix Workspace website at [https://www.citrix.com/products/receiver.html](https://www.citrix.com/products/receiver.html) for all things Citrix Workspace.

Installing Citrix Workspace via .deb in the GUI:

Navigate to the release page at

[https://www.citrix.com/downloads/workspace-app/](https://www.citrix.com/downloads/workspace-app/).

Click Workspace app for Linux.

Click Citrix Workspace app for Linux.

Click Debian Packages.

Click Full Packages (Self-Service Support).

Click Download File under Citrix Workspace app for Linux (x86_64) to download Citrix Workspace.

Go to your Downloads folder.

Double-click icaclient_24.5.0.76_amd64.deb.

Click Install.

Cloud Office Suites

Cloud office suites are online tools that enhance business agility by offering on-the-go access to collaboration and productivity applications. This shift to the cloud, supported by devices like Linux desktops, empowers a remote workforce to connect and share information in real time, making it a top choice for enterprises aiming for flexibility and efficiency.

The Google Docs Editors Suite, part of Google Drive, offers web-based productivity tools including Docs, Sheets, Slides, Drawings, Forms, Sites, and Keep. Accessible online or via mobile, it enables real-time collaboration with features like revision history, machine learning enhancements, and support for various formats. This suite streamlines document creation and sharing, fostering efficient teamwork and communication. Visit the official website at [https://www.google.com/drive/](https://www.google.com/drive/).

Microsoft 365 is a suite from Microsoft that blends productivity tools, collaboration features, and cloud services. It includes familiar applications like Word, Excel, and PowerPoint, alongside Outlook.com, OneDrive, and Microsoft Teams. Designed for both individual and enterprise use, it offers programs for Windows, macOS, and mobile devices, plus web versions. Microsoft 365 also features enterprise solutions like Exchange Server and SharePoint, and subscription plans that provide access to desktop software, hosted email, and intranet services, ensuring a comprehensive solution for users' needs. Visit the official website at [https://www.microsoft.com/microsoft-365](https://www.microsoft.com/microsoft-365).

Zoho Office Suite is a comprehensive, web-based suite designed for modern teamwork and productivity. It combines a wide range of applications including word processing, spreadsheets, presentations, databases, note-taking, and more, integrated with advanced tools for CRM, project management, and invoicing. This platform encourages collaboration by supporting work from anywhere, offering seamless sharing, and ensuring mobility with cloud-based document management. Zoho Office Suite also ensures compatibility with Microsoft Office files and connectivity with other popular apps, making it a versatile tool for businesses looking to boost productivity and foster teamwork across various working styles. Visit the official website at [https://www.zoho.com/office-suite/](https://www.zoho.com/office-suite/).

Google Docs Editors Suite

Visit the official Google Docs Editors Suite website at [https://www.google.co.uk/docs/about/](https://www.google.co.uk/docs/about/) for all things Google Docs Editors Suite.

Accessing Google Docs Editors Suite via Browser in the GUI:

Navigate to the web page at:

[https://www.google.co.uk/docs/about/](https://www.google.co.uk/docs/about/)

Sign in to access Google Docs Editors Suite.

Microsoft 365

Visit the official Microsoft 365 website at [https://www.microsoft.com/en-gb/microsoft-365/](https://www.microsoft.com/en-gb/microsoft-365/) for all things Microsoft 365.

Accessing Microsoft 365 via Browser in the GUI:

Navigate to the web page at:

[https://www.microsoft.com/en-gb/microsoft-365/](https://www.microsoft.com/en-gb/microsoft-365/)

Sign in to access Microsoft 365.

Zoho Office Suite

Visit the official Zoho Office Suite website at [https://www.zoho.com/officesuite/](https://www.zoho.com/officesuite/) for all things Zoho Office Suite.

Accessing Zoho Office Suite via Browser in the GUI:

[https://www.zoho.com/officesuite/](https://www.zoho.com/officesuite/)

Sign in to access Zoho Office Suite.

AI Content Generation

AI content generation uses advanced AI technologies like transformers and large language models to create text, images, and more. This technology is changing how we produce and interact with media, despite initial issues like bias and inaccuracy. Its potential is transforming business and creative processes, marking a new era of digital innovation.

Easy Diffusion simplifies the use of Stable Diffusion with a one-click install for all platforms. It requires no technical setup and features a user-friendly interface. It supports ControlNet, SDXL, multiple LoRAs, easy embeddings, seamless tiling, inpainting, faster processing, reduced VRAM usage, WebP format, undo actions, new samplers, and improved upscaling. This makes advanced text-to-image AI accessible to everyone.

oobabooga is a versatile Gradio web UI for interacting with large language models, including Transformers, GPTQ, and Llama. It has three interface modes—default, notebook, and chat—and supports multiple backends like ExLlamaV2 and AutoGPTQ. Users can switch between models via a dropdown menu and enhance their experience with extensions for voice input/output, translation, and more. It supports chatting with custom characters, precise chat templates, and integrates the Transformers library for efficient model loading and CPU inference. Additionally, it features an OpenAI-compatible API server, making it a comprehensive tool for text generation tasks.

A negative prompt in Stable Diffusion lets users specify unwanted elements in an image, like "blurry" or "duplicate," helping the model avoid these. This technique improves image quality by refining details and accuracy without complex instructions.

Upscayl is a free, open-source AI tool for upscaling images, enhancing low-resolution photos using deep learning. Created by TGS963 and Nayam Amarshe, it works on various platforms and can magnify images up to 4x without losing detail. It sharpens images, enhances quality, and reduces artifacts using advanced AI techniques. Its easy interface and quick processing make it suitable for casual users and professionals needing high-quality image enlargements.

Stable Diffusion Web UI simplifies using Stable Diffusion, featuring easy installation, image generation and modification through text, and modes like outpainting and inpainting. It includes functions like attention adjustment for precise results, loopback for iterative processing, and various upscaling options for better image quality. Users can train custom embeddings, use AI-enhanced tools for face and image restoration, and explore creative controls like style applications and prompt editing. It supports efficient operation on modest hardware, integrates with popular extensions, and offers an intuitive interface with progress tracking and live previews.

Easy Diffusion

Visit the official Easy Diffusion website at [https://easydiffusion.github.io/](https://easydiffusion.github.io/) for more information.

Installing Easy Diffusion via APT in the Terminal:

sudo apt update

Navigate to the release page at:

[https://github.com/easydiffusion/easydiffusion/releases](https://github.com/easydiffusion/easydiffusion/releases)

Download the latest Easy-Diffusion-Linux.zip.

Go to ~/Downloads and double-click Easy-Diffusion-Linux.zip.

Select easy-diffusion and click Extract.

Navigate to ~/Downloads/easy-diffusion.

Right-click an empty space and open in Terminal.

Run the command:

./start.sh.

To create a desktop shortcut for Easy Diffusion:

Open the terminal and enter:

cd /usr/share/applications

Run:

sudo gedit easy-diffusion1.desktop.

Update the file with:

[Desktop Entry]

Name=Easy Diffusion

Comment=Easy Diffusion

Exec=./Downloads/easy-diffusion/start.sh

Icon=terminal

Terminal=true

Type=Application

Categories=Utility;Game;

Save and exit the editor.

oobabooga (Text Generation GUI)

Visit the official oobabooga (Text Generation GUI) website at [https://github.com/oobabooga/text-generation-webui](https://github.com/oobabooga/text-generation-webui) for more information.

Installing oobabooga (Text Generation GUI) via .sh in the Terminal:

Navigate to the release page at:

[https://github.com/oobabooga/text-generation-webui](https://github.com/oobabooga/text-generation-webui)

Download text-generation-webui-main.zip.

Go to ~/Downloads and double-click text-generation-webui-main.zip.

Select text-generation-webui-main and click Extract.

Navigate to ~/Downloads/text-generation-webui-main.

Right-click an empty space and open in Terminal.

Run the commands:

./start_linux.sh

./update_linux.sh

To create a desktop shortcut for oobabooga:

Open the terminal and enter:

cd /usr/share/applications.

Run:

sudo gedit oobabooga1.desktop.

Update the file with:

[Desktop Entry]

Name=oobabooga (Text Generation GUI)

Comment=oobabooga (Text Generation GUI)

Exec=./Downloads/text-generation-webui-main/update_linux.sh

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

Save and exit the editor.

Negative Prompts for Stable Diffusion

Use the following negative prompts to avoid unwanted elements in images:

(((((extra fingers))))), (((((poorly drawn hands))))), (((((poorly drawn face))))), (((((mutation))))),  (((((deformed))))), (((((bad proportions))))), (((((extra limbs))))), (((((glitchy))))), (((((extra hands))))),  (((((mangled fingers))))), (((((portrait))))), (((((text))))), (((((words))))), (((((copyright))))), (((((realism))))), (((((2girl))))), (((((3girl))))), (((((4girl))))), (((((helmet))))), (((((multiple_breasts))))), (((((flowers))))), (((((blur))))), (((((terrible))))), (((((awful))))), (((((copyright))))), ((((((trademark)))))), (((((watermark))))),

(((((censorship))))), (((((censored))))), (((((deformed face))))), (((((bad anatomy))))), (((((deformed face))))), (((((ugly))))), (((((deformed hands))))), (((((blurry))))), (((((multiple_breasts))))), (((((multiple_nipples))))), (((((jpeg artifacts))))), (((((signature))))), (((((username))))), (((((blurry))))), (((((monochrome))))), (((((asymmetrical breasts))))), (((((cropped))))), (((((worst quality))))),

(((((low quality))))), (((((normal quality))))), (((((extra digit))))), (((((fewer digits))))), (((((lowres))))), (((((artist name))))), (((((poorly draw))))), (((((messy drawing))))), (((((extra ears))))), (((((broken legs))))), (((((puffy nipples))))), (((((disfigured))))),

(((((long neck))))), (((((out of frame))))), (((((crossed eyes))))), (((((bad hands))))), (((((error))))), (((((missing fingers))))), (((((normal quality))))), (((((mutated))))), (((((broken legs))))), (((((hands inside body))))), (((((extra leg))))), (((((third leg))))), (((((amputee))))), (((((extra breasts))))), (((((fused hands))))), (((((claws))))), (((((more than 2 nipples))))), (((((lineart))))), (((((simple background))))), (((((floating limbs))))), (((((disconnected limbs))))), (((((out of focus))))), (((((conjoined))))), (((((blended))))),

(((((fused))))), (((((pathetic))))), (((((sloppy))))), (((((liquid collarbone))))), (((((disappearing arms))))), (((((missing breasts))))), (((((short arm))))), (((((missing arms))))), (((((more than 2 legs))))), (((((extra arms))))), (((((fused fingers))))), (((((malformed hands))))), (((((missing hand))))), (((((missing hands))))), (((((one hand with more than 5 fingers))))), (((((one hand with less than 5 fingers)))), (((((one hand with less than 5 digit))))), (((((fused digit))))), (((((bad digit))))), (((((liquid digit))))), (((((bad gloves))))), (((((poorly drawn gloves))))), (((((fused gloves))))), (((((more than 1 left hand))))) , (((((more than 1 right hand))))), (((((asymmetrical body))))), (((((missing extremities))))), (((((walleyed))))), (((((eye bags))))), (((((duplicate))))), (((((dehydrated))))), (((((cloned face))))), (((((malformed limbs))))), (((((blind))))), (((((dead eyes))))), (((((out of shot))))), (((((logo))))), (((((writing)))))

Stable Diffusion Web UI

Visit the official Stable Diffusion Web UI website at [https://github.com/AUTOMATIC1111/stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui) for more information.

Installing Stable Diffusion Web UI via .sh in the Terminal:

Navigate to the release page at:

[https://github.com/AUTOMATIC1111/stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

Download the latest Source code (zip).

Go to ~/Downloads and double-click stable-diffusion-webui-1.9.4.zip.

Select stable-diffusion-webui-1.9.4 and click Extract.

Navigate to ~/Downloads/stable-diffusion-webui-1.9.4.

Right-click an empty space and open in Terminal.

Run the command:

./webui.sh.

To create a desktop shortcut for Stable Diffusion Web UI:

Open the terminal and enter:

cd /usr/share/applications.

Run:

sudo gedit stablediffusionwebui1.desktop.

Update the file with:

[Desktop Entry]

Name=Stable Diffusion Web UI

Comment=Stable Diffusion Web UI

Exec=./Downloads/stable-diffusion-webui-1.9.4/webui.sh

Icon=terminal

Terminal=true

Type=Application

Categories=Utility;Game;

Save and exit the editor.

System Settings

System settings on Linux Mint 22 provide a complete overview of your computer's hardware, software, and configuration details. Whether you are troubleshooting, upgrading, or curious about specifics like RAM, processor speed, or operating system version, accessing these settings through terminal commands or graphical interfaces like System Monitor and System Settings gives valuable insights. These tools allow performance adjustments, security configurations, and driver updates, enhancing your understanding and optimization of the system's capabilities.

Night Light in the GNOME desktop environment reduces blue light emission from screens, making it easier on the eyes during late hours. Found under display settings, this feature can be toggled on or off and allows adjusting the screen's color temperature to minimize strain. Automatically set to activate from sunset to sunrise, it's perfect for evening work or relaxation, with options to disable it temporarily for activities like watching movies. This tool enhances user comfort and well-being during nighttime computer use.

Redshift on the Cinnamon desktop environment adjusts your screen's color temperature according to the time of day, reducing eye strain and potential insomnia. This tool transitions between warmer colors at night (2000–4000 K) and cooler hues during the day (5500–6500 K) to match natural lighting, aiding your eyes' gradual adaptation. Configurable for continuous or fixed settings, Redshift requires your location to accurately track the sun's elevation, supporting multiple monitors on Linux and BSD systems. This application simulates the ambient light of your environment for more comfortable screen time.

PipeWire is designed to enhance Linux's handling of audio and video by offering a low-latency, graph-based processing engine. It supports various multimedia use cases, previously managed by PulseAudio and JACK, and includes a robust security model to facilitate audio and video device interaction by containerized applications like Flatpak. As part of Linux's evolving application development ecosystem, alongside Wayland and Flatpak, PipeWire aims to be a foundational component, enabling minimal-latency capture and playback, real-time processing, and seamless integration across PulseAudio, JACK, ALSA, and GStreamer applications with support for sandboxed environments.

Linux Mint 22 system variables, or environment variables, are dynamic named values used to store information and control the behavior of command-line applications and system operations. These variables consist of a name and a value, formatted as KEY=value, with no spaces around the "=" symbol. Values containing spaces must be enclosed in quotes, and multiple values can be assigned using a colon (":") separator. Variable names are case-sensitive and conventionally uppercase. Environment variables are globally accessible and inherited by child processes, unlike shell variables, which are local to the current shell instance. They offer a versatile tool for customizing Linux Mint 22’s system and application behaviors.

Setting an image as the background in Cinnamon lets you personalize your desktop by choosing any image or color. Right-click on the desktop, select "Change desktop background," and add a new wallpaper through the Desktop Background Preferences dialog. You can also adjust its appearance to fit or fill the screen. For a solid color, pick "No Wallpaper" and choose a color. Changes are instant, and for system-wide settings, admins can use dconf to set defaults, lock configurations, and add extra backgrounds for all users, ensuring a unified look or branding across devices.

Mount_options.conf is a UDisks feature for sysadmins, enabling the customization of mount options for various filesystems to ensure security and data consistency. Introduced in UDisks 2.9.0, it allows system-wide overrides via configuration files or udev rules, specifically for dynamic mountpoints like removable media, prioritizing safe and reliable access without compromising the system. It distinguishes between filesystem types and drivers, refining control over data management, preventing unauthorized access, and data loss, making it a critical tool for secure and efficient storage handling.

In Linux Mint 22’s Cinnamon desktop, "Startup Applications" let you manage programs that launch at boot. Press the Super key, search for it, and tweak your boot process for efficiency. Be cautious when disabling defaults as they are often crucial. Add new apps with ease or adjust existing ones, including launch delays, ensuring a smoother start with control over what runs and when, without overwhelming your system.

Auto mount volumes on startup in Linux Mint 22 ensures your drives connect automatically when the system boots. Using the GNOME Disks utility, a part of many Linux distros, you can easily set this up. Launch Disks, select your drive, then a partition, and adjust the mount options to enable mounting at system startup. This tool simplifies adding entries to the /etc/fstab file, making partitions available system-wide without manually editing config files. Just restart your machine, and your selected partitions will auto-mount, streamlining your setup for immediate access.

In Linux Mint 22, keybinds and screenshots are essential for capturing your screen's contents, crucial for sharing insights, solving problems, or preserving memories. They confirm your experiences, archive information, and enhance documents with visual context. Tools like Screenshot make screenshots invaluable for efficient communication and documentation in various tasks.

The default systemd timeout, typically set at 90 seconds, governs how long systemd waits for a service to start or stop before considering the operation failed. This timeout mechanism ensures system responsiveness by preventing indefinitely hanging services. However, for more flexibility, systemd allows adjusting this timeout according to specific needs, enabling services to have customized timeout settings that can deviate from the default.

Immutable files and folders are digital assets that cannot be modified or deleted once created. This characteristic ensures data integrity and security, especially in environments where preserving historical accuracy and preventing unauthorized changes are crucial. While the concept seems rigid, it's a safeguard against data tampering and loss, offering reliability and peace in knowing that critical information remains untouched.

FFmpegthumbnailer is a lightweight tool designed to quickly generate video thumbnails, enhancing file management efficiency. Utilizing the powerful ffmpeg library, it decodes video frames, with its capabilities tied to ffmpeg's configuration. Renowned for its speed and minimal resource usage, FFmpegthumbnailer is essential for file managers, streamlining the process of creating visually informative thumbnails for video files, aiding in quicker identification and access to video content.

Linux .desktop files are simple text files that provide essential information to the desktop environment about software applications. They define how a program is launched, its name, and the icon it uses. These files make it easier for users to interact with applications through graphical interfaces by enabling the creation of shortcuts.

In Linux Mint 22, power settings let users manage how their computer uses energy, crucial for extending battery life and efficiency. These settings include options for screen brightness, sleep mode, and the behavior when the laptop lid is closed. Users can easily customize these preferences via the system settings panel, ensuring their device operates optimally while conserving power.

Night Light (GNOME)

Visit the official Night Light (GNOME) website at [https://foundation.gnome.org/](https://foundation.gnome.org/) for all things Night Light (GNOME).

Setting Up Night Light (GNOME) via the GUI:

Open the application menu and select "Settings."

Navigate to the "Displays" tab on the left sidebar, then click on "Night Light."

Toggle the switch next to "Night Light" to enable it.

In the "Schedule" row, click the dropdown box and choose "Manual Schedule."

Set the active period from 21:00 to 06:00.

Adjust the color temperature slider to a position just slightly below the midpoint between the third and fourth white lines.

Night Light (Cinnamon & Redshift)

Visit the official Night Light (Cinnamon & Redshift) websites at [https://github.com/linuxmint/cinnamon](https://github.com/linuxmint/cinnamon) and [https://github.com/jonls/redshift](https://github.com/jonls/redshift) for all things Night Light (Cinnamon & Redshift).

Installing and Setting Up Night Light (Cinnamon & Redshift) via the Terminal and GUI:

sudo apt install redshift redshift-gtk wayland*

Navigate to your config directory with:

cd ~/.config

Edit the Redshift configuration by typing:

nano redshift.conf

Input the following settings:

[redshift]

temp-night=2250

transition=1

brightness=1.0

gamma=1.0

[location]

adjustment-method=vidmode

location-provider=manual

Save changes with CTRL + S and exit with CTRL + X.

PipeWire Sound Crackle & Popping Fixes

Visit the official PipeWire website at [https://pipewire.org/](https://pipewire.org/) for all things PipeWire.

To fix potential sound issues like crackling or popping with PipeWire via Command Line and GUI:

Disable audio power saving:

echo "options snd_hda_intel power_save=0" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf

echo "options snd_hda_intel power_save_controller=N" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf

Verify the changes:

cat /sys/module/snd_hda_intel/parameters/power_save

cat /sys/module/snd_hda_intel/parameters/power_save_controller

Edit the PipeWire configuration to optimize performance:

sudo gedit /usr/share/pipewire/pipewire.conf

Adjust the quantum settings:

Change #default.clock.quantum = 1024 to default.clock.quantum = 2048.

Modify default.clock.min-quantum = 16 to default.clock.min-quantum = 2048.

Update #default.clock.max-quantum = 2048 to default.clock.max-quantum = 4096.

Save changes and restart PipeWire services:

systemctl --user restart pipewire.service pipewire-pulse.service pipewire-media-session.service

systemctl --user restart pipewire-multi.service

Enhance audio priority by editing:

sudo gedit /etc/security/limits.conf

Add:

@audio   -  nice     -20

Save and exit.

Remove potential conflicts by purging speech-dispatcher:

sudo apt remove speech-dispatcher

Ensure all changes are consistent across PipeWire configurations. Save and back up necessary files, then restart your computer.

Linux Mint 22 System Variables

Setting Up Linux Mint 22 System Variables via the Command Line and GUI:

Edit the system-wide Bash configuration file:

sudo gedit /etc/bash.bashrc

Add the following settings:

# Environment Variables

#export STAGING_WRITECOPY='1'

#export DXVK_ENABLE_NVAPI='1'

#export WINEESYNC='1'

#export WINEDEBUG='-all'

#export __GL_SHADER_DISK_CACHE_SKIP_CLEANUP='1'

#export __GL_THREADED_OPTIMIZATION='1'

#export STAGING_SHARED_MEMORY='1'

#export WINE_SIMULATE_WRITECOPY='1'

#export DXVK_STATE_CACHE_PATH='/home/username/.wine/drive_c/Program Files (x86)/Battle.net'

#export __GL_SHADER_CACHE='/home/username/.wine/drive_c/Program Files (x86)/Battle.net'

#export VKD3D_SHADER_CACHE_PATH='/home/username/.wine/drive_c/Program Files (x86)/Battle.net'

#export VKD3D_CONFIG='dxr'

#export exclude_processes='Agent.exe "Battle.net Helper.exe'

Replace username with your actual username where applicable. Save changes by clicking "Save" or through the File menu.

Setting Image As Background In Gnome & Cinnamon

Visit the official Cinnamon website at [https://github.com/linuxmint/cinnamon](https://github.com/linuxmint/cinnamon) for all things Cinnamon.

To set an image as the background:

Right-click on the image file and select "Set as Background."

mount_options.conf

Visit the official udisks website at [https://www.freedesktop.org/wiki/Software/udisks/](https://www.freedesktop.org/wiki/Software/udisks/) for all things udisks.

To set up mount_options.conf via Command Line and GUI:

sudo apt update

sudo gedit /etc/udisks2/mount_options.conf

Add the following content:

[defaults]

ntfs_defaults=uid=$UID,gid=$GID

ntfs_allow=uid=$UID,gid=$GID,nls,umask,dmask,fmask,nohidden,sys_immutable,discard,force,sparse,showmeta,prealloc,no_acs_rules,acl,noatime

Save progress by clicking "Save," or through the File menu.

Adding Startup Applications In Cinnamon

To add startup applications via GUI in Linux Mint 22:

Open the Application Menu using the Super key. Navigate to "Startup Applications," click the + button, and select "Choose Application."

Type the name of the application you want to load at startup, select it, and click "Add."

For adding a custom command:

Open "Startup Applications" from the Application Menu with the Super key.

Click the + button and choose "Custom Command."

Enter a name for the command, the command itself (e.g., "discord" to launch Discord), a detailed comment, and set a startup delay if needed.

Click "Save."

To add startup applications via Command Line:

Open the terminal. Navigate to the directory containing application shortcuts with:

cd /usr/share/applications

List all files with:

dir

Identify the .desktop file for the application (e.g., firefox.desktop).

Copy this file to the autostart folder with:

sudo cp firefox.desktop /etc/xdg/autostart

Adding Startup Applications In GNOME

To add startup applications in GNOME via GUI:

Open the application menu with the Super key and launch "Tweaks."

Navigate to the "Startup Applications" tab and click the "+" button.

Type in the name of the application you want to start automatically and select "Add."

Auto Mount Partitions Using GNOME Disks

Visit the official GNOME Disks website at [https://apps.gnome.org/en-GB/DiskUtility/](https://apps.gnome.org/en-GB/DiskUtility/) for all things GNOME Disks.

Auto Mounting Partitions via the GUI:

Launch Disks from the application menu.

Select the disk holding the volumes you want to mount.

Choose the specific volume on that disk, and click the cogwheel icon.

Select "Edit Mount Options."

Toggle the switch next to "User Session Defaults" to the left.

Confirm your changes by clicking "OK."

Cinnamon Screenshot Keybindings

Changing flashspot color attribute via the Command Line and GUI:

Open the "Files" application and press "CTRL + L" to enable "Location Entry" mode.

Type "/usr/share/themes/" and navigate to the "Mint-Y-Dark-Red" folder.

Inside, go to the "cinnamon" directory.

Right-click on an empty space and choose "open in terminal."

Execute:

sudo gedit cinnamon.css

Search for the "flashspot" element and change its value to "#00FFFFFF".

Save changes and exit.

Press "ALT + F2" to open the cinnamon run command box, type "r", and hit enter to restart cinnamon.

To create a "Screenshots" folder via GUI:

Open the "Files" application and navigate to the "~/Pictures" directory.

Right-click on an empty space and select the option to create a new folder.

Rename it to "Screenshots."

To take a focused window screenshot via GUI:

Open "Settings" from the application menu.

Navigate to "Keyboard" and select "Shortcuts." Click on "Add custom shortcut."

Name it "Focused Window Screenshot" and input:

bash -c "cd ~/Pictures/Screenshots && gnome-screenshot -w -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png"

Add the command and assign it a keyboard binding, such as "F10".

To take a fullscreen screenshot via GUI:

Open "Settings" from the application menu. Navigate to "Keyboard" and select "Shortcuts."

Click on "Add custom shortcut."

Name it "Fullscreen Screenshot" and input:

bash -c "cd ~/Pictures/Screenshots && gnome-screenshot -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png"

Add the command and assign it a keyboard binding, such as "F11".

GNOME Overview & Windows Keybinds

To change the "Show the Overview" keybind via GUI:

Open the application menu and select "Settings." Navigate to the "Keyboard" tab and select "View and Customize Shortcuts."

Search for "Show the overview."

Press "Super + TAB" to set the new keybind.

To change the "Switch Windows" keybind via GUI:

Open the application menu and select "Settings."

Navigate to the "Keyboard" tab and select "View and Customize Shortcuts."

Search for "Switch windows." Press "ALT + TAB" to set the new keybind.

GNOME Screenshot Keybinds

To change the "Take a Screenshot" keybind via GUI:

Open the application menu and select "Settings."

Navigate to the "Keyboard" tab and select "View and Customize Shortcuts."

Search for "Take a screenshot."

Press "F10" to set the new keybind.

To change the "Take a Screenshot of a Window" keybind via GUI:

Open the application menu and select "Settings."

Navigate to the "Keyboard" tab and select "View and Customize Shortcuts."

Search for "Take a screenshot of a window."

Press "F11" to set the new keybind.

To change the "Take a Screenshot of a Window Interactively" keybind via GUI:

Open the application menu and select "Settings."

Navigate to the "Keyboard" tab and select "View and Customize Shortcuts."

Search for "Take a screenshot of a window interactively."

Press "F9" to set the new keybind.

Default Systemd Timeout

Visit the official Systemd website at [https://systemd.io/](https://systemd.io/) for all things Systemd.

To set up the default Systemd timeout via Command Line and GUI:

sudo apt update

cd /etc/systemd/

sudo gedit system.conf

Change:

#DefaultTimeoutStartSec=90s

To:

DefaultTimeoutStartSec=30s

Save progress by clicking "Save," or through the File menu.

Run:

sudo systemctl daemon-reload

Making Files And Folders Immutable

Visit the official Immutable Files and Folders website at [https://www.linux.org/docs/man1/chattr.html](https://www.linux.org/docs/man1/chattr.html)  for all things Immutable Files and Folders.

To make files and folders immutable via Command Line:

sudo apt update

cd ~/Downloads

sudo chattr +i -RV CurseForge-1.251.0-17831.AppImage

ffmpegthumbnailer

Visit the official ffmpegthumbnailer website at [https://github.com/dirkvdb/ffmpegthumbnailer](https://github.com/dirkvdb/ffmpegthumbnailer) for all things ffmpegthumbnailer.

Installing ffmpegthumbnailer via APT in the Terminal:

sudo apt update

sudo apt install ffmpeg ffmpegthumbnailer gstreamer1.0-libav

rm -r ~/.cache/thumbnails/

Removing .desktop files

Visit the official .desktop files website at [https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) for all things .desktop files.

Removing .desktop files via the Terminal:

cd /usr/share/applications

dir

sudo cp uget-gtk.desktop uget-gtk1.desktop

sudo rm -r uget-gtk.desktop

sudo update-desktop-database

Power Settings

To adjust power settings via GUI:

Open "Settings" from the application menu.

Navigate to the "Power" section.

Set "Screen Blank" to "5 Minutes."

Turn off "Automatic Suspend" by selecting "Off."

GNOME Extensions

GNOME Shell extensions, developed by third parties, enhance the GNOME interface by allowing customizations like window management tweaks or app launching modifications. You can find and manage these extensions on a dedicated website, and they come with unique identifiers (UUID) for secure installation. While they offer versatile enhancements, from minor to major interface changes, users should be cautious. Extensions integrate deeply with the OS, potentially leading to system issues or security risks. However, they undergo thorough reviews for safety before being available for download, ensuring a balance between innovation and security. Visit the official GNOME website at [https://foundation.gnome.org/](https://foundation.gnome.org/) for more information.

The GNOME Shell Extension Manager simplifies the installation and management of GNOME extensions. This tool allows users to browse, install, remove, enable, or disable extensions directly from the extensions.gnome.org website, without needing a web browser. It's particularly useful on Ubuntu 21.10 and later, where the default Firefox cannot install extensions due to its Snap format. With support for in-app updates from GNOME 43 onwards and the ability to manage installed extensions, including system ones, it offers a streamlined experience. Available via Flathub as a Flatpak, it stands as an essential tool for enhancing the GNOME desktop environment. Visit the official website at [https://extensions.gnome.org/](https://extensions.gnome.org/) for more details.

The GNOME Shell Integration Chrome Extension and Firefox Addon facilitate seamless interaction between the GNOME desktop environment and the respective web browsers. They enable users to install, manage, and apply GNOME Shell extensions directly from their browser, without needing to use the terminal or other tools. This integration simplifies the customization and enhancement of the GNOME desktop experience, making it more accessible to users who prefer graphical interfaces over command-line operations. More information can be found at [https://extensions.gnome.org/extension/19/user-themes/](https://extensions.gnome.org/extension/19/user-themes/).

The User Themes extension for the GNOME Desktop Environment on Linux Mint 22 enables users to customize the appearance of the GNOME Shell. By default, GNOME Tweaks cannot alter the GNOME Shell theme. Installing this extension overcomes that limitation, offering more personalization options directly within this environment.

ArcMenu is a top GNOME Shell extension offering a traditional app menu experience with a variety of layouts, from simple to exotic. It features built-in GNOME search, quick system shortcuts access, and stylish updates like adjustable search box border radius. The latest version includes bug fixes and improvements like separate icon size settings for categories and applications, and a Windows 11-style power button submenu. Find more at [https://extensions.gnome.org/extension/1228/arcmenu/](https://extensions.gnome.org/extension/1228/arcmenu/).

Dash to Panel is a versatile GNOME Shell extension that transforms the dash into a unified main panel, merging application launchers and the system tray for a streamlined experience akin to KDE Plasma and Windows 7+. It eliminates the need for a separate dock, granting effortless access to running and favorited apps. Highly customizable, it allows users to adjust the panel’s appearance, behavior, and functionality, including running indicators, window previews, and intellihide. Features like customizable running indicators, live previews on hover, keyboard shortcuts for launching apps, and multi-monitor support enhance usability, making your workspace feel personalized and efficient. Learn more at [https://extensions.gnome.org/extension/1160/dash-to-panel/](https://extensions.gnome.org/extension/1160/dash-to-panel/).

Desktop Icons (NG) is an enhancement for GNOME Shell, acting as a revamped version of the official Desktop Icons extension. It introduces features like intuitive drag-and-drop across the desktop, applications, and Nautilus windows, plus a versatile "Open with..." option for multiple files. It ensures the full names of icons are visible upon hover or click, even if they're too long, and maintains compositor stability under heavy desktop activity. More details are available at [https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/](https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/).

Tray Icons: Reloaded is a GNOME Shell extension that revitalizes your desktop by returning Tray Icons to the top panel, enriched with new features. It introduces an overflow mode with a '3 dots' icon for excess items, customizable tray positioning, icon limits, and sizes. Users can fine-tune icon color saturation, contrast, and brightness, alongside adjustable tray, icon margins, and padding. Find more information at [https://extensions.gnome.org/extension/2890/tray-icons-reloaded/](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/).

GNOME Shell Extension Manager

Visit the official GNOME Shell Extension Manager website at [https://github.com/mjakeman/extension-manager](https://github.com/mjakeman/extension-manager) for all things GNOME Shell Extension Manager.

Installing GNOME Shell Extension Manager via FLATPAK Package through Software Manager:

1.  Open Software Manager and search for GNOME Shell Extension Manager.
2.  Click on GNOME Shell Extension Manager, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing GNOME Shell Extension Manager via APT in the Terminal:

sudo apt update

sudo apt install gnome-shell-extension-manager

Installing GNOME Shell Extension Manager via FLATPAK in the Terminal:

flatpak install flathub com.mattjakeman.ExtensionManager

GNOME Shell Integration

For all things GNOME Shell Integration visit the official GNOME Shell Integration websites at:

[https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep](https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep)

[https://addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/](https://addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/)

Installing the GNOME Shell Integration Chrome Extension via GUI:

Navigate to the release page at:

[https://chromewebstore.google.com/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep](https://chromewebstore.google.com/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep)

Click "Add to Chrome," then confirm by clicking "Add extension."

Installing the GNOME Shell Integration Firefox Add-on via GUI:

Navigate to the release page at:

[https://addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/](https://addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/)

Click "Add to Firefox," then confirm by clicking "Add."

Make sure to check "Allow this extension to run in Private Windows" to ensure availability across all sessions.

User Themes

Visit the official User Themes website at [https://gitlab.gnome.org/GNOME/gnome-shell-extensions](https://gitlab.gnome.org/GNOME/gnome-shell-extensions) for all things User Themes.

Installing the User Themes GNOME Extension via GUI:

Navigate to the release page at:

[https://extensions.gnome.org/extension/19/user-themes/](https://extensions.gnome.org/extension/19/user-themes/)

Click "Install" and confirm to add User Themes.

ArcMenu

Visit the official ArcMenu website at [https://gitlab.com/arcmenu/ArcMenu](https://gitlab.com/arcmenu/ArcMenu) for all things ArcMenu.

Installing the ArcMenu GNOME Extension via GUI:

Navigate to the release page at:

[https://extensions.gnome.org/extension/3628/arcmenu/](https://extensions.gnome.org/extension/3628/arcmenu/)

Click "Install" and confirm to add ArcMenu.

Dash to Panel

Visit the official Dash to Panel website at [https://github.com/home-sweet-gnome/dash-to-panel](https://github.com/home-sweet-gnome/dash-to-panel) for all things Dash to Panel.

Installing the Dash to Panel GNOME Extension via GUI:

Navigate to the release page at:

[https://extensions.gnome.org/extension/1160/dash-to-panel/](https://extensions.gnome.org/extension/1160/dash-to-panel/)

Click "Install" and confirm to add Dash to Panel.

Adjusting the Dash to Panel Tray Font Size via GUI:

Right-click on "Dash to Panel" to open its context menu.

Select "Dash to Panel Settings." In the settings window, navigate to the "Fine-Tune" tab.

Adjust the "Tray Font Size" slider to 21px.

Desktop Icons (NG)

Visit the official Desktop Icons (NG) website at [https://gitlab.com/rastersoft/desktop-icons-ng](https://gitlab.com/rastersoft/desktop-icons-ng) for all things Desktop Icons (NG).

Installing the Desktop Icons (NG) GNOME Extension via GUI:

Navigate to the release page at:

[https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/](https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/)

Click "Install" and confirm to add Desktop Icons (NG).

Tray Icons: Reloaded

Visit the official Tray Icons: Reloaded website at [https://github.com/MartinPL/Tray-Icons-Reloaded](https://github.com/MartinPL/Tray-Icons-Reloaded) for all things Tray Icons: Reloaded.

Installing the Tray Icons: Reloaded GNOME Extension via GUI:

Navigate to the release page at:

[https://extensions.gnome.org/extension/2890/tray-icons-reloaded/](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)

Click "Install" and confirm to add Tray Icons: Reloaded.

Cinnamon Applets

Cinnamon applets enhance your Linux Mint 22 experience by offering useful tools like the "Force Quit" applet, which allows you to close unresponsive windows with a click. To create an applet, assign a unique ID, create a folder with a "metadata.json" file for applet information, and an "applet.js" file for the code. Applets reside in either your local or system-wide Cinnamon applets directory. With a straightforward API, applets can adapt to various panel orientations and sizes, ensuring functionality across multiple instances. Visit the official Cinnamon website at [https://github.com/linuxmint/cinnamon](https://github.com/linuxmint/cinnamon) for more details.

The Grouped Window List applet in Cinnamon organizes open windows by application in the panel, similar to taskbar functionalities in other operating systems. It simplifies navigation between multiple instances of the same application by grouping them under a single icon, offering previews on hover, and allowing for quick switching or window management. This applet enhances efficiency and workspace organization, making it easier to manage open applications and maintain a clutter-free desktop environment. Learn more at [https://cinnamon-spices.linuxmint.com/applets/view/27](https://cinnamon-spices.linuxmint.com/applets/view/27).

The Cinnamon Windows Alt-Tab Switcher offers various styles like icons, thumbnails, or a combination, making it easier to navigate with larger icons and detailed previews. Users can adjust icon sizes and styles from the system settings. The Cinnamon-Alt-Tab-Enhanced project adds features like support across multiple workspaces, larger thumbnail views, and comprehensive keyboard and mouse support, enhancing the user experience. Find more information at [https://github.com/linuxmint/cinnamon-screensaver](https://github.com/linuxmint/cinnamon-screensaver).

The Cinnamon Menu Applet simplifies accessing installed applications on your system. Users can easily launch applications by typing their names or aliases, provided there's a corresponding .desktop file. This applet also organizes applications into categories, making navigation and discovery more intuitive. It bridges the gap between user convenience and system functionality, ensuring that finding and running any application is a smooth and straightforward process. More details can be found at [https://github.com/linuxmint/Cinnamon](https://github.com/linuxmint/Cinnamon).

The Calendar Applet for the Cinnamon Desktop Environment offers a time display similar to Windows XP, a highly regarded operating system by Microsoft. This feature allows users to mimic the appearance and ambiance of Windows XP, avoiding its programming limitations. Additionally, it supports the 12-hour format, contrasting with the military-style 24-hour format, providing a user-friendly approach to timekeeping. Visit [https://github.com/linuxmint/cinnamon-spices-applets](https://github.com/linuxmint/cinnamon-spices-applets) for more information.

Grouped Window List

To set up the Grouped Window List via the graphical user interface, start by launching Firefox from the application menu.

Once open, minimize the program.

Right-click on the Firefox icon on the panel and select "Configure."

Navigate to the "Panel" tab.

In the "Button label" option, click the box and choose "Window Title."

Cinnamon Windows Alt-Tab Switcher

To set up the Cinnamon Windows Alt-Tab Switcher with a graphical user interface, follow these steps.

Open the application menu and run the Windows command.

Navigate to the Alt-Tab section and find the "Alt-Tab switcher style" option.

Click the checkbox next to it and select "Thumbnails only" from the dropdown menu.

Cinnamon Menu Applet

To set up the Cinnamon Menu Applet via the graphical user interface, right-click the menu button and select "Configure."

Navigate to the "Panel" tab. Enable the "Use a custom icon and label" option by sliding the switch to the right.

In the "Text" field, press CTRL + A to select all text, then press DEL to clear it.

Enter " Start" as the new label. For the icon, click the box in the same row.

In the search box, press CTRL + A to select all text, then press DEL to clear it.

Type "start-here" into the search, select the "start-here" icon when it appears, and click "Select" to finalize your choice.

Cinnamon Calendar Applet

To set a custom date format in the Cinnamon Calendar Applet via the GUI, right-click the Calendar applet, typically found at the bottom right corner of your screen.

Choose "Configure" from the menu.

Locate the "Use a custom date format" option and slide its switch to the right.

In the "Date format" field, press CTRL + A to select all text, then type "%I:%M %p".

Press Enter to apply your changes.

This will customize your calendar display to show time in a 12-hour format, making it more intuitive to read.

Desktop Environments

Desktop environments use a graphical interface to make computer interaction easier, featuring icons, windows, and toolbars. They originated on PCs and now unify software appearance and functionality, helping users access files without dealing with the underlying OS complexities. Popular examples include KDE and GNOME, offering customizable user experiences across various systems. These environments range from traditional setups to innovative 3D desktops, showing the versatility and evolution of user interfaces.

GNOME is a free, open-source desktop environment for Linux and Unix-like systems. It aims to make computing simple and efficient. Developed by a global community, including Red Hat, GNOME is the default for many Linux distributions. It offers an intuitive, elegant interface, focusing on ease of use and productivity, with features like the Activities Overview for easy task access and seamless integration with online accounts. GNOME aims to be a polished, comprehensive suite for users, enhancing the Linux experience with a user-friendly GUI and essential applications, rivaling Windows and macOS interfaces.

KDE Plasma 5, launched on July 15, 2014, is the fifth iteration of KDE's desktop environment. It evolved from Plasma 4 with a fresh "Breeze" theme, QML-based graphical interface, and better device convergence. It boosts performance through OpenGL acceleration, offers customizable widgets, and includes KRunner for versatile searches. With features like encrypted vaults, session management, and improved HiDPI support, Plasma 5 enhances the user experience on Linux. It supports X Window and Wayland, with continuous updates enriching its functionality until succeeded by Plasma 6 in 2024.

LXDE, the Lightweight X11 Desktop Environment, is a free, efficient desktop environment designed for older or less powerful computers. Crafted in C using the GTK 2 toolkit, it thrives on Unix-like systems, promoting speed and low energy consumption. It supports rolling releases, features Openbox as its default window manager (with options like Fluxbox, IceWM), and includes a mix of GPL and LGPL code. Key components include the PCMan File Manager, LXPanel, and LXTerminal, making LXDE versatile for everyday computing needs without the bulk.

XFCE, pronounced as four individual letters, is a free, open-source desktop environment for Linux and Unix-like systems. It emphasizes speed and efficiency, being light on resources without sacrificing visual appeal or ease of use. The latest XFCE 4.18 version introduces notable enhancements, focusing on user-visible improvements. It includes a new file input widget to avoid invalid filenames, a versatile shortcut editor, and performance boosts in thumbnail handling.

GNOME

Visit the official GNOME website at [https://foundation.gnome.org/](https://foundation.gnome.org/) for all things GNOME.

Installing GNOME via APT in the Terminal:

sudo apt update

sudo apt install gnome

Installing GNOME via Tasksel in the Terminal:

Type tasksel.

Use the arrow keys to find GNOME and press the SPACEBAR to select it, marking it with an asterisk.

Navigate to "Ok" using the arrow keys and press Enter to begin the installation.

Tasksel

Visit the official Tasksel website at [https://github.com/ParrotSec/tasksel](https://github.com/ParrotSec/tasksel) for all things Tasksel.

Installing Tasksel via APT in the Terminal:

sudo apt update

sudo apt install tasksel

KDE Plasma

Visit the official KDE Plasma website at [https://kde.org/plasma-desktop/](https://kde.org/plasma-desktop/) for all things KDE Plasma.

Installing KDE Plasma via APT in the Terminal:

sudo apt update

sudo apt install kde-full

Installing KDE Plasma via Tasksel in the Terminal:

Type tasksel.

Use the arrow keys to find KDE Plasma and press the SPACEBAR to select it, marking it with an asterisk.

Navigate to "Ok" using the arrow keys and press Enter to begin the installation.

LXDE

Visit the official LXDE website at [https://www.lxde.org/](https://www.lxde.org/) for all things LXDE.

Installing LXDE via APT in the Terminal:

sudo apt update

sudo apt install lxde

Installing LXDE via Tasksel in the Terminal:

Type tasksel.

Use the arrow keys to find LXDE and press the SPACEBAR to select it, marking it with an asterisk.

Navigate to "Ok" using the arrow keys and press Enter to begin the installation.

XFCE

Visit the official XFCE website at [https://www.xfce.org/](https://www.xfce.org/) for all things XFCE.

Installing XFCE via APT in the Terminal:

sudo apt update

sudo apt install xfce

Installing XFCE via Tasksel in the Terminal:

Type tasksel.

Use the arrow keys to find XFCE and press the SPACEBAR to select it, marking it with an asterisk.

Navigate to "Ok" using the arrow keys and press Enter to begin the installation.

Programming Languages

Programming languages are systems for writing software, balancing form (syntax) and meaning (semantics) with features like types and error handling. Influenced by computer architecture, they have evolved from hardware-specific to more abstract forms, enhancing simplicity. Ranging from imperative to object-oriented types, they cater to various needs while balancing benefits and trade-offs, like simplicity versus performance. This evolution is reflected in the dynamic study and classification within computer science, making programming a vibrant field.

Zig, created by Andrew Kelley, is a compact, statically typed compiled language aimed at system programming, positioning itself as a modern successor to C. Striving for simplicity and efficiency, Zig avoids macros and preprocessors, embracing flow control, easy function calls, and direct library imports. It borrows from newer languages through compile-time generics and a hint of reflection, enhancing flexibility. Zig prioritizes safety without demanding runtime checks, offering option types and a built-in testing framework to manage manual memory without garbage collection, distinguishing itself from peers like Go, Rust, and Carbon.

Go, crafted by Robert Griesemer, Rob Pike, and Ken Thompson at Google, is a high-level, statically typed language similar to C but with added memory safety, garbage collection, and concurrency. It thrives on simplicity and security, making it ideal for scalable systems. Supported by Google, Go (or Golang) boasts a robust standard library, built-in concurrency, and a vibrant ecosystem. Its main implementations include the "gc" compiler for diverse platforms and WebAssembly, and gccgo or gollvm through gofrontend. GopherJS even brings Go to the web by compiling it to JavaScript.

Rust, created by Graydon Hoare in 2006 and later backed by Mozilla, is a versatile programming language known for its emphasis on performance, type safety, and concurrency without needing a garbage collector. Its unique "borrow checker" helps manage memory and data races effectively. Adopted by tech giants like Amazon and Google, and even integrated into Linux kernel development, Rust stands out for its quick uptake and impact on systems programming, blending ideas from functional programming for robust, efficient software creation.

Lua is a versatile programming language born in Brazil in 1993, known for its efficiency and lightness. Ideal for embedded use, it runs on a cross-platform interpreter and offers a simple C API for integration. It excels in scripting, configuration, and rapid prototyping thanks to its dynamic typing, automatic memory management, and support for multiple programming paradigms. Lua's development by PUC-Rio emphasizes speed, portability, and ease of embedding. Its name, meaning "Moon" in Portuguese, underscores its unique identity. Free and open-source, Lua stands out for its performance, small footprint, and adaptability across platforms and devices.

OpenJDK is a free, open-source version of the Java Platform, Standard Edition, initiated by Sun Microsystems in 2006 and licensed under GPL-2.0 with a special exception for linking. It’s where enthusiasts and developers converge to advance Java SE and its related projects, offering the latest OpenJDK JDK 21 binaries for various operating systems. Engage in the vibrant OpenJDK Community to explore, download, or contribute to projects like Amber, Loom, Panama, Valhalla, and the future of Java. For practical Java applications, dev.java is your go-to. Whether you’re learning, downloading, or contributing, OpenJDK embodies collaboration and innovation in Java's evolution.

Zig

Visit the official Zig website at [https://ziglang.org/](https://ziglang.org/) for all things Zig.

Installing Zig via SNAP in the Terminal:

sudo snap install zig --beta --classic

Go

Visit the official Go website at [https://go.dev/](https://go.dev/) for all things Go.

Installing Go via GUI & Command Line in the Terminal:

Navigate to the release page at:

[https://go.dev/dl/](https://go.dev/dl/)

Click The Latest go.linux-amd64.tar.gz to Download Go.

Run the following commands in the terminal:

cd ~/Downloads

tar -xvf go1.22.4.linux-amd64.tar.gz

sudo chown -R root go

sudo mv go /usr/local

Rust

Visit the official Rust website at [https://www.rust-lang.org/](https://www.rust-lang.org/) for all things Rust.

Installing Rust via curl in the Terminal:

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh source "$HOME/.cargo/env"

Lua

Visit the official Lua website at [https://www.lua.org/home.html](https://www.lua.org/home.html) for all things Lua.

Installing Lua via APT in the Terminal:

sudo apt update

sudo apt install build-essential libreadline-dev wget cd

mkdir lua_build

cd lua_build

wget https://www.lua.org/ftp/lua-5.4.6.tar.gz

tar -xvf lua-5.4.6.tar.gz cd lua-5.4.6

make linux test

sudo make install

OpenJava

Visit the official OpenJava website at [https://openjdk.org/](https://openjdk.org/) for all things OpenJava.

Installing OpenJava via APT in the Terminal:

sudo apt update && sudo apt upgrade

sudo apt install default-jre default-jdk

Imageboards

Imageboards are online forums where images take precedence over text, originating from Japan. They allow users to engage in diverse discussions by posting pictures, functioning like bulletin boards but focusing more on temporary content. Users can post anonymously and often use tripcodes—hashed passwords—for identity without storing personal data. Unlike online galleries, content on imageboards primarily comes from external sources. Platforms like 4chan offer "secure" tripcodes to enhance anonymity, making these forums unique for their combination of visual content and anonymous interaction.

YChanEx is a tool designed to download threads and images from imageboards like 4chan and 8chan. It works on Windows with .NET 4.5 and on Linux via WINE, featuring a unique "ychanex:" browser protocol for easy downloads. Still in development, it supports various imageboards and includes features like proxy support, brotli decompression, and thread history. Recent updates have improved reliability and the user interface, with more enhancements planned. YChanEx aims to simplify the archiving of imageboard content, making it easier to preserve discussions and images from these forums.

YChanEx

Visit the official YChanEx website at [https://github.com/murrty/YChanEx](https://github.com/murrty/YChanEx) for all things YChanEx.

Installing YChanEx via APT in the Terminal & GUI:

Update the package manager metadata:

sudo apt update

Enable the 32-bit architecture support:

sudo dpkg --add-architecture i386

sudo apt update

Download and add the WineHQ repository key:

sudo mkdir -p /etc/apt/keyrings

sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key

sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources

Install WineHQ:

sudo apt update

sudo apt install winehq-staging

Navigate to the releases page:

[https://github.com/murrty/YChanEx/releases/tag/2.0](https://github.com/murrty/YChanEx/releases/tag/2.0)

Download the Latest YChanEx.exe.

Go to ~/Downloads and double-click YChanEx.exe [Right Click and set WINE as default if this does not work].

To create a .desktop shortcut for YChanEx, follow these steps in your terminal:

Navigate to the applications directory with the command:

cd /usr/share/applications

Open a new .desktop file for editing by running:

sudo gedit ychanex1.desktop

In the ychanex1.desktop file, enter the following details:

[Desktop Entry]

Name=YChanEx

Comment=YChanEx

Exec=/bin/bash -c "cd ~/Downloads && wine YChanEx.exe”

Icon=terminal

Terminal=false

Type=Application

Categories=Utility;Game;

To save your progress, click "Save." Alternatively, you can click "File," then "Save," or click the ☰ icon, select "Save As," and finally click "Save." After saving, close the editor.

Ebook Readers

Ebook software transforms your device into a digital book, allowing you to read on computers, tablets, or phones. It supports various formats like EPUB, PDF, and Word, each offering unique features and compatibility. Understanding these formats helps you choose the right one for your reading preferences, ensuring a smooth and enjoyable experience across different devices.

Calibre is a free, open-source e-book suite that enables users to organize, display, edit, create, and convert e-books across multiple formats. It supports syncing with many e-readers. You can edit EPUB and AZW3 formats directly, while others require conversion. Calibre offers a wide range of plugins, supports metadata management, and allows e-book importing, including wireless sync. Although it doesn't natively remove DRM, plugins are available to enable this functionality. From version 6.0, full-text search enhances its library capabilities, with content conversion facilitated by Python-based recipes.

Bookworm is a versatile, free eBook reader for Windows that supports formats like PDF, EPUB, MOBI, and more. It's designed for accessibility, offering plain text and fully formatted views. Features include text-to-speech, OCR for scanned documents, and Wikipedia integration for quick term lookups. Users can easily navigate documents, make annotations, and even extract articles from web pages. Whether using a screen reader or enjoying the read-aloud function, Bookworm enhances the reading experience for everyone.

Calibre

Visit the official Calibre website at [https://calibre-ebook.com/](https://calibre-ebook.com/) for all things Calibre.

Installing Calibre via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Calibre.
2.  Click on Calibre, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Calibre via APT in the Terminal:

sudo apt install calibre

Installing Calibre via FLATPAK in the Terminal:

flatpak install flathub com.calibre_ebook.calibre

Installing Calibre via Binary install in the Terminal:

sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin

Bookworm

Visit the official Bookworm website at [https://getbookworm.com/](https://getbookworm.com/) for all things Bookworm.

Installing Bookworm via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Bookworm.
2.  Click on Bookworm, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Bookworm via APT in the Terminal:

sudo apt install bookworm

Installing Bookworm via FLATPAK in the Terminal:

flatpak install flathub com.github.babluboy.bookworm

Virtualization

Virtualization software, known as a hypervisor, enables one computer to function as multiple virtual machines, allowing different operating systems to run simultaneously on a single PC. This technology optimizes resource use, simplifies backups, and allows seamless operation of various OSs and outdated applications. It enhances security by isolating potential threats from malware and browser vulnerabilities. Beyond personal use, virtualization supports Infrastructure as a Service (IaaS), increasing scalability and efficiency for businesses, reducing costs, and improving disaster recovery and testing. It embodies flexible, efficient computing, making more possible with less.

Oracle VirtualBox is a versatile virtualization tool suitable for both enterprise and personal use, supporting various operating systems like Windows, Linux, and macOS. It offers extensive features for high performance, accommodating numerous guest operating systems, including different Windows versions and Linux distributions. As open-source software under the GPL v3, VirtualBox invites community contributions while maintaining professional quality, backed by Oracle. Regular updates expand its supported systems and features, and it includes resources like pre-built VMs for developers.

Virt-manager, primarily developed by Red Hat, is a desktop tool for managing virtual machines (VMs) via libvirt. It allows users to create, edit, start, and stop VMs, and view their performance and console. It supports KVM, Xen, QEMU, LXC containers, and FreeBSD's bhyve hypervisor since 2014\. The suite includes tools like virt-install for easy VM setup, virt-viewer for VM display interaction, virt-clone for cloning VMs, virt-xml for editing VM configurations, and virt-bootstrap for setting up root file systems for libvirt-based containers.

Oracle VirtualBox

Visit the official Oracle VirtualBox website at [https://www.virtualbox.org/](https://www.virtualbox.org/) for all things Oracle VirtualBox.

Installing Oracle VirtualBox via APT in the Terminal:

sudo apt update && sudo apt upgrade

cd

wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | rpm --import -

sudo apt update

sudo apt install virtualbox-7.0

Installing Oracle VirtualBox via DEB in the GUI:

Navigate to the release page:

[https://www.virtualbox.org/wiki/Linux_Downloads](https://www.virtualbox.org/wiki/Linux_Downloads)

Click the link for the latest Ubuntu 24.04 package to download Oracle VirtualBox.

Go to your Downloads folder:

Double-click on virtualbox-7.0_7.0.18-162988~Ubuntu~noble_amd64.deb.

Click "Install" to complete the installation.

Adding User to the vboxusers Group:

Switch to the root user:

su -

Add your username to the vboxusers group (replace "username" with the actual username):

sudo usermod -aG vboxusers username

Exit the root user:

exit

Reboot your system to apply the changes:

sudo reboot

Virt-manager

Visit the official Virt-manager website at [https://virt-manager.org/](https://virt-manager.org/) for all things Virt-manager.

Installing Virt-manager via SYSTEM PACKAGE Package through Software Manager:

1.  Open Software Manager and search for Virt-manager.
2.  Click on Virt-manager, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE and click Install.

Installing Virt-manager via APT in the Terminal:

sudo apt install virt-manager

Gaming

Gaming on Linux Mint 22 offers an exciting shift from traditional gaming platforms, tapping into Linux Mint 22’s robust and stable environment. Leveraging tools like Steam Proton and Lutris, you can smoothly run a wide array of games, from indie titles to AAA releases, on a platform traditionally seen as less suitable for gaming. This evolution highlights a vibrant community effort to make Linux a gamer-friendly OS, showing significant improvements in performance and hardware support. While challenges like driver compatibility remain, the progress is undeniable, offering a refreshing alternative to Windows gaming with a focus on open-source principles and user control.

Wine-Staging, available at [https://www.winehq.org/](https://www.winehq.org/), is a testing ground for Wine, incorporating bug fixes and features not yet in the development branch. It speeds up access to experimental features for users and developers. Wine-Staging acts as a patchset for Wine’s development version, allowing maintainers to selectively include patches. A dedicated team reviews and maintains these patches from bug reports to improve Wine's performance, particularly for games and applications. Differentiations include winehq-staging for testing, winehq-stable for stable versions, winehq-devel for development headers, and wine-development for additional debugging tools.

Lutris is a free, open-source game manager for Linux that integrates with platforms like Steam, GOG, Humble Bundle, and the Epic Games Store. It simplifies playing games across various hardware and software, supporting over 20 emulators and community scripts for Wine, ensuring smooth operation of both old and new games. Developed by Mathieu Comandon and the community, Lutris promotes video game preservation, allowing users to build an open-source game console with their PC. It’s a stable platform powered by Linux and Vulkan, keeping your game collection alive and accessible.

ProtonUp-Qt, found at [https://github.com/DavidoTek/ProtonUp-Qt](https://github.com/DavidoTek/ProtonUp-Qt), is a GUI tool that simplifies installing and managing GE-Proton, Luxtorpeda, and Wine-GE for games on Steam, Heroic, and Lutris on Linux and Steam Deck. It enhances compatibility, offering solutions when Valve’s Proton falls short or when playing upgraded versions of classic games. The latest update, 2.9.1, includes a Steam Shortcut Editor, switches to Ph42oN’s Dxvk-Async, and improves Wine-GE handling, along with UI/UX enhancements and configuration improvements for a smoother gaming setup.

Steam is the leading digital platform for PC games, providing automatic game updates, third-party title distribution, matchmaking, and social features. It offers Steamworks for developers, supports macOS, Linux, and mobile platforms, and sells other digital content and hardware like the Valve Index. Dominating the market with a 75% share in 2013, by 2021, Steam had over 34,000 games and 132 million users, leading to innovations like the Steam Deck.

DXVK is a Vulkan-based layer that translates Direct3D 9/10/11 for 3D applications on Linux via Wine, enhancing gaming by bridging DirectX and Vulkan, reducing overhead, and boosting performance. This innovation marks a pivotal shift for Linux gaming, offering comparable, if not superior, experiences to Windows and making Linux a stronger contender for gamers.

VKD3D designed to fully implement the Direct3D 12 API over Vulkan, mainly for Proton's Direct3D 12 support. It prioritizes performance and game compatibility, utilizing modern Vulkan features, although this means older systems might not be supported. The latest version, 2.12, introduces NVIDIA Reflex support, enhancements like the D3D12 render pass API, and various fixes and workarounds for game-specific issues. It also includes performance improvements on NVIDIA GPUs and debug tools for developers, making it a vital tool for gaming on platforms that support Vulkan.

Wine-Staging

Visit the official Wine-Staging website at [https://wiki.winehq.org/Wine-Staging](https://wiki.winehq.org/Wine-Staging) for all things Wine-Staging.

Update the package manager metadata:

sudo apt update

Enable the 32-bit architecture support:

sudo dpkg --add-architecture i386

sudo apt update

Download and add the WineHQ repository key:

sudo mkdir -p /etc/apt/keyrings

sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key

sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources

Install WineHQ-Staging:

sudo apt update

sudo apt install winehq-staging gamemode winbind protobuf-compiler libprotobuf-dev libopusfile0 winetricks

Lutris

Visit the official Lutris website at [https://lutris.net/](https://lutris.net/) for all things Lutris.

Installing Lutris via SYSTEM PACKAGE/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Lutris.
2.  Click on Lutris, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Lutris via APT in the Terminal:

sudo apt install lutris

Installing Lutris via FLATPAK in the Terminal:

flatpak install flathub net.lutris.Lutris

ProtonUp-Qt

Visit the official ProtonUp-Qt website at [https://davidotek.github.io/protonup-qt/](https://davidotek.github.io/protonup-qt/) for all things ProtonUp-Qt.

Installing ProtonUp-Qt via RPM/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for ProtonUp-Qt.
2.  Click on ProtonUp-Qt, then on the Source Selection Box.
3.  Choose FLATPAK and click Install.

Installing ProtonUp-Qt via FLATPAK in the Terminal:

flatpak install flathub net.davidotek.pupgui2

Steam

Visit the official Steam website at [https://store.steampowered.com/](https://store.steampowered.com/) for all things Steam.

Installing Steam via RPM/FLATPAK Package through Software Manager:

1.  Open Software Manager and search for Steam.
2.  Click on Steam, then on the Source Selection Box.
3.  Choose SYSTEM PACKAGE or FLATPAK and click Install.

Installing Steam via APT in the Terminal:

sudo apt update

sudo apt install steam

Installing Steam via FLATPAK in the Terminal:

flatpak install flathub com.valvesoftware.Steam

Installing Steam via SNAP in the Terminal:

sudo snap install steam

DXVK

Visit the official DXVK website at [https://github.com/doitsujin/dxvk](https://github.com/doitsujin/dxvk) for all things DXVK.

Install DXVK via .sh in the Terminal and GUI:

Navigate to the release page at:

[https://github.com/doitsujin/dxvk/releases](https://github.com/doitsujin/dxvk/releases)

Download the latest dxvk-tar.gz.

Go to ~/Downloads, double-click dxvk-2.3.1.tar.gz, select dxvk-2.3.1, and click Extract.

Right-click an empty space and select "Open in Terminal."

Run these commands:

cd ~/Downloads/dxvk-2.3.1

cp x64/*.dll ~/.wine/drive_c/windows/system32

cp x32/*.dll ~/.wine/drive_c/windows/syswow64

winecfg

Configure Wine:

Click Libraries.

Select 'dxgi' and click 'Edit'.

Toggle the switch next to 'Native' to 'Builtin' and click 'OK'.

Repeat for 'd3d9', 'd3d11', and 'd3d10core'.

Click 'Apply' and 'OK'.

Vkd3d-proton

Visit the official Vkd3d-proton website at [https://github.com/HansKristian-Work/vkd3d-proton](https://github.com/HansKristian-Work/vkd3d-proton) for all things Vkd3d-proton.

Install Vkd3d-proton via .sh in the Terminal and GUI:

Navigate to the release page at:

[https://github.com/HansKristian-Work/vkd3d-proton/releases](https://github.com/HansKristian-Work/vkd3d-proton/releases)

Download the latest vkd3d-proton.

Go to ~/Downloads, double-click vkd3d-proton, select vkd3d-proton-2.12, and click Extract.

Right-click an empty space and select "Open in Terminal."

Run these commands:

cd ~/Downloads/vkd3d-proton-2.12

./setup_vkd3d_proton.sh install

winecfg

Configure Wine:

Click Libraries.

Add and configure d3d12core and `d3d12 to native to builtin

World of Warcraft

World of Warcraft is a captivating online game that invites players to explore the vast lands of Azeroth. With new expansions like THE WAR WITHIN, it offers underground worlds, allied races, and ancient evils to conquer. Classic versions and updates like Dragonflight revitalize gameplay with dungeons and unique challenges. Whether starting anew, returning, or embracing the hardcore, WoW promises endless adventure with friends, rewards through play, and a community of fellow adventurers. Join now to partake in epic quests, battles, and a living, evolving world. Visit the official World of Warcraft website at [https://worldofwarcraft.com/](https://worldofwarcraft.com/).

The Battle.net Client is a desktop app designed to streamline your gaming experience by managing all Battle.net games in one place. It allows you to install, update, and launch your games conveniently, offering access to the Battle.net Shop and game news. Replacing previous game launchers, it serves as a portal to both current and future games. With a single sign-on feature, logging in once gives you access to all your games, keeping you logged in for up to 30 days if you choose. The client also supports background patching for games, with options to pause or disable auto-updates, ensuring you're always ready to play without hassle. For any issues, there's direct support and troubleshooting advice available. Visit the official Battle.net website at [https://battle.net/](https://battle.net/).

The Lutris World of Warcraft black screen in-game store issue arises when players running World of Warcraft through Lutris encounter a black screen upon accessing the in-game store, preventing them from viewing or purchasing items. This problem can also occur at the checkout stage after selecting an item. This section offers practical solutions to address and resolve this bug, aiming to restore the game's store functionality and enhance the gaming experience.

The WINE-Staging World of Warcraft black screen in-game store issue arises when players, running World of Warcraft through WINE-Staging, encounter a black screen upon accessing the in-game store, preventing them from viewing or purchasing items. This problem can also occur at the checkout stage after selecting an item. This section offers practical solutions to address and resolve this bug, aiming to restore the game's store functionality and enhance the gaming experience. Visit the official Wine-Staging website at [https://wiki.winehq.org/Wine-Staging](https://wiki.winehq.org/Wine-Staging) for more information.

The DirectX 12 error in World of Warcraft can often be fixed by updating Nvidia graphics drivers from version 525 to 545\. This issue usually happens when the game is set to use DirectX 12 instead of DirectX 11\. You can fix this by changing the settings in both the Battle.net Client and World of Warcraft itself.

The Retail World of Warcraft Vanilla AddOn Suite is a carefully selected collection of mods designed to give players a blend of Shadowlands' modern flair and the nostalgic feel of WoW's vanilla era. It enriches the game with quality-of-life features inspired by early RPGs, including UI enhancements from Accountant Classic to XToLevel, aiming to improve your play experience by combining the best of both worlds. This suite covers everything from stat tracking to quest management, ensuring a smoother, more enjoyable journey through Azeroth.

CurseForge is a gaming hub where players download mods and add-ons for games like World of Warcraft, Minecraft, and StarCraft II. It’s also a creative platform offering templates for crafting new mods, rewarding authors with points for downloads. The CurseForge app enhances addon management, streamlining updates with quick, responsive features, and auto-updating options. By supporting mod authors, who receive 70% of app revenue, users directly contribute to their favorite creators’ success, with options to use a free, ad-supported version or subscribe to remove ads and further support the community. Visit the official CurseForge website at [https://www.curseforge.com/](https://www.curseforge.com/).

Running Battle.net from the command line involves setting up WINE-Staging on Linux Mint 22’s Cinnamon, installing essential packages, and configuring graphical API translation layers. To achieve this, one must first install prerequisite packages to ensure compatibility and optimal performance. The most effective way to launch the Battle.net Client is through the command line, which can then be integrated into Linux Mint 22’s startup options via the Custom command feature. Visit the official Battle.net website at [https://battle.net/](https://battle.net/) for more details.

Battle.net

Visit the official Battle.net website at [https://eu.shop.battle.net/en-gb?from=root](https://eu.shop.battle.net/en-gb?from=root) for all things Battle.net.

[Requires WINE-Staging to be installed]

Installing Battle.net via .exe in the Terminal and GUI:

Navigate to the release page at:

[https://download.battle.net/en-gb/?product=bnetdesk](https://download.battle.net/en-gb/?product=bnetdesk)

Click "Try Again" to download Battle.net.

Go to ~/Downloads.

Right-click an empty space.

Click "Open in Terminal."

Run the following commands:

sudo apt update && sudo apt upgrade

gamemoderun wine Battle.net-Setup.exe --disable-software-rasterizer

Follow the on-screen instructions.

Possible Fix for Lutris World of Warcraft Black Screen In-Game Store Issue

Visit the official World of Warcraft and Lutris websites at:

[https://worldofwarcraft.blizzard.com/](https://worldofwarcraft.blizzard.com/)

[https://lutris.net/](https://lutris.net/)

Fix via Command Line & GUI:

Open Lutris from your application menu.

Select Blizzard Battle.net and click the upward arrow next to the wine glass icon, then choose "Wine Configuration."

In the Wine Configuration window, find the "Windows Version" dropdown and select either Windows 11 or Windows 10.

Navigate to the "Graphics" tab and enable "CSMT for improved graphic performance" and "VAAPI as backend for DXVA2 GPU Decoding."

Move to the "Drives" tab, press the add button, and assign a new drive letter.

Locate and select the World of Warcraft directory, which includes the retail, classic, and classic_era folders. Click "OK."

Click "Apply" to apply these settings and confirm by clicking "OK" again.

Ensure that the WINEESYNC variable is not set and that no esync instances are running.

If issues persist, consider updating your graphics drivers to the latest version available, such as the 555 drivers from NVIDIA.

Possible Fix for WINE-Staging World of Warcraft Black Screen In-Game Store Issue

Visit the official World of Warcraft and WINE-Staging websites at:

[https://worldofwarcraft.blizzard.com/](https://worldofwarcraft.blizzard.com/)

[https://wiki.winehq.org/Wine-Staging](https://wiki.winehq.org/Wine-Staging)

Fix via Command Line & GUI:

Run the following command in the terminal:

winecfg

Select Blizzard Battle.net and click the upward arrow next to the wine glass icon, then choose "Wine Configuration."

In the Wine Configuration window, find the "Windows Version" dropdown and select either Windows 11 or Windows 10.

Navigate to the "Graphics" tab and enable "CSMT for improved graphic performance" and "VAAPI as backend for DXVA2 GPU Decoding."

Move to the "Drives" tab, press the add button, and assign a new drive letter.

Locate and select the World of Warcraft directory, which includes the retail, classic, and classic_era folders. Click "OK."

Click "Apply" to apply these settings and confirm by clicking "OK" again.

Ensure that the WINEESYNC variable is not set and that no esync instances are running. If issues persist, consider updating your graphics drivers to the latest version available, such as the 555 drivers from NVIDIA.

Possible Fix for DirectX 12 Graphics Error

Visit the official DirectX website at [https://www.microsoft.com/en-gb/download/details.aspx?id=35](https://www.microsoft.com/en-gb/download/details.aspx?id=35)  for all things DirectX.

Fix via GUI:

Open Battle.net from the application menu.

Click the gear icon next to the large blue "Play" or "Update" button.

Choose "Game Settings" and locate the section for the version of World of Warcraft you wish to play.

Check "Additional command line arguments" and enter "-d3d11" in the adjacent box. Click "Done."

Launch World of Warcraft, access the "Options" menu, select the "Graphics" tab under "System," and scroll to "Graphics API" under "Advanced." Ensure DirectX 11 is selected.

If not, choose DirectX 11 from the dropdown next to "Graphics API" and restart World of Warcraft to apply the changes.

Retail World of Warcraft Vanilla AddOn Suite

Below is a catalog of AddOns meticulously compiled to replicate a user interface reminiscent of both Shadowlands and the classic era/vanilla version of World of Warcraft. These modifications incorporate several quality-of-life (QOL) enhancements inspired by RPG titles predating or concurrent with the original release of World of Warcraft Vanilla.

Accountant Classic

Cheugy_Mission_Reports

ClassicFCT

ClassicFrames

ClassicGuildFrame

ClassicLevelUp

ClassicQuestText

ClassicUI

ClassicalFps

ClockHider

CovenantMissionHelper

CTMOD

DejaCharacterStats

ExtraQuestButton

GarrisonCommander

IcyVeinsStatPriority

Misspelled

MyRolePlay

NeatPlates

NPCRPGossip

Notes

OldCastbars

OrderHallCommander

PixelPerfectAlign

QuestCompletist

Storyline

UnlimitedMapPinDistance

VenturePlan

WarPlan

XToLevel

This collection of AddOns has been meticulously curated to enhance your gaming experience, mirroring the aesthetics and functionality of both Shadowlands and the classic/vanilla World of Warcraft era, while also drawing inspiration from quality-of-life improvements found in RPGs that predate or coincide with the original World of Warcraft Vanilla release.

Linux Mint 22 Command Reference

Essential System Commands for File and Directory Management

### List Directory Contents

Command: sudo ls directory

Description: Lists the contents of the specified directory.

### Change Directory

Command: cd directory

Description: Changes the current working directory to the specified directory.

### Go Up One Directory Tier

Command: cd ..

Description: Changes the current working directory to the parent directory, moving up one level in the directory hierarchy.

### List All Non-hidden Files and Folders

Command: dir

Description: Lists all non-hidden files and folders in the current working directory.

### List All Files and Folders Including Hidden

Command: ls -a

Description: Lists all files and folders in the current directory, including hidden ones.

### Make a Directory

Command: sudo mkdir directory

Description: Creates a new directory inside the current working directory.

### Remove Files

Command: sudo rm filename

Description: Deletes the specified file from the filesystem.

### Remove Files and Folders Recursively

Command: sudo rm -r directory

Description: Deletes the specified directory and its contents, including all files and subdirectories.

### Copy a File to a Destination

Command: sudo cp filename destination

Description: Copies the specified file to the specified destination.

### Copy a Folder to a Destination

Command: sudo cp -R folder destination

Description: Copies the specified folder and its contents to the specified destination.

### Move a File or Folder to a Destination

Command: sudo mv filename destination

Description: Moves the specified file or folder to the specified destination.

### Rename a File or Folder

Command: sudo mv filename newfilename

Description: Renames the specified file or folder to the new specified name.

### Display File Contents

Command: sudo cat filename

Description: Displays the contents of the specified file on the terminal.

### List Parent Directory Contents

Command: ls ..

Description: Lists the contents of the parent directory of the current working directory.

Mastering APT: Advanced Package Management Techniques

### Update Package Lists

Command: sudo apt update

Description: Updates the local package database by retrieving the latest information from the software repositories.

### Upgrade Installed Packages

Command: sudo apt upgrade

Description: Upgrades all installed applications to their latest available versions from the repositories, handling any required dependencies.

### Full Upgrade Installed Packages

Command: sudo apt full-upgrade

Description: Performs a full upgrade of all packages on the system to their latest versions, which may involve removing packages if necessary.

### Package Search

Command: sudo apt search package

Description: Searches for packages that match a specified keyword.

### Show Package Information

Command: sudo apt show package

Description: Provides detailed information about a specific package.

### Install Packages

Command: sudo apt install package

Description: Installs a package from the software repositories, including any required dependencies.

### Remove Packages

Command: sudo apt remove package

Description: Removes a package from the system while preserving any configuration files associated with it.

### Purge Packages

Command: sudo apt purge package

Description: Removes a package from the system, including its configuration files.

### Auto Remove Packages

Command: sudo apt autoremove

Description: Removes any unused packages and their dependencies from the system.

### List Installed Packages

Command: sudo apt list

Description: Displays a list of all packages currently installed on the system.

### Add Repository

Command: sudo add-apt-repository repository

Description: Adds a new software repository to the system.

### Remove Repository

Command: sudo add-apt-repository -r repository

Description: Removes a previously added repository from the system.

### Edit Sources File

Command: sudo apt edit-sources

Description: Opens the sources.list file in the default text editor for manual editing of software repository sources.

### Fix Broken Dependencies

Command: sudo apt install -f

Description: Attempts to resolve and fix any broken package dependencies by installing missing or conflicting packages.

### Retrieve Source Code for a Package

Command: sudo apt source package

Description: Downloads the source code of a package from the repository.

### Upgrading the System

Command: sudo do-release-upgrade

Description: Initiates a distribution upgrade process to move the operating system to a newer version.

### Clean Packages

Command: sudo apt clean

Description: Clears the local package cache to free up disk space.

### Auto Clean Packages

Command: sudo apt autoclean

Description: Automatically cleans the local package cache by removing unnecessary files.

### Hold APT Packages

Command: sudo apt mark-hold package

Description: Prevents a package from being updated during upgrades.

### Unhold APT Packages

Command: sudo apt mark-unhold package

Description: Removes the hold on a package, allowing it to be updated during upgrades.

### Show Held Packages

Command: sudo apt-mark showhold

Description: Displays a list of all packages that are currently held on the system.

### Package Verification

Command: sudo apt-key verify

Description: Verifies the integrity and authenticity of package repository keys.

Mastering Flatpak: Installation, Management, and Beyond

### Flatpak Installation

Command: flatpak install flatpak

Description: Installs a Flatpak from a remote repository.

### Listing Installed Flatpaks

Command: flatpak list

Description: Provides an overview of all the Flatpak applications currently installed on your system.

### Updating Flatpaks

Command: flatpak update

Description: Upgrades all installed Flatpaks to the latest versions.

### Running a Flatpak

Command: flatpak run flatpak

Description: Launches an installed Flatpak application.

### Uninstalling Flatpak

Command: flatpak uninstall flatpak

Description: Removes a specified Flatpak package from your system.

### Flatpak Remote Repository List

Command: flatpak remote-list

Description: Lists the names of Flatpak remote repositories that have been added to your system.

### Adding a Flatpak Remote Repository

Command: flatpak remote-add --if-not-exists name url

Description: Adds a new Flatpak remote repository to your system.

### Removing a Flatpak Remote Repository

Command: flatpak remote-delete name

Description: Removes a specified Flatpak remote repository from your system's configuration.

Snap Operations: A Comprehensive Guide to Installing, Managing, and Exploring Snap Applications

### Installing a Snap

Command: sudo snap install <snap>

Description: Installs a snap application from the Snapcraft database.

### Listing Installed Snaps

Command: sudo snap list

Description: Lists installed snaps on the system.

### Updating Snaps

Command: sudo snap refresh

Description: Upgrades all snaps to the latest versions.

### Running a Snap

Command: snap run <snap>

Description: Runs an installed snap.

### Removing a Snap

Command: sudo snap remove <snap>

Description: Removes an installed snap from the system.

### Searching for Snaps

Command: sudo snap find <search_term>

Description: Searches the Snapcraft database for snaps matching the search term.

### Listing Snap Information

Command: sudo snap info <snap>

Description: Provides detailed information about an installed snap.

### Viewing Snap Connections

Command: sudo snap connections <snap>

Description: Displays the connections made by an installed snap.

Mastering File Ownership Modification

### File Ownership Modification

Command: sudo chown user filename

Description: Changes the ownership of a file or folder to the specified user.

### Ownership Modification with Recursion

Command: sudo chown -R user filename

Description: Recursively changes the owner of a file or folder and its contents to the specified user.

### Ownership Modification with Group Specification

Command: sudo chown user:group filename

Description: Alters both the owner and group associated with a file or folder.

### Silent Ownership Modification

Command: sudo chown -f user filename

Description: Modifies ownership while suppressing error messages if the operation does not succeed.

### Verbose Ownership Modification

Command: sudo chown -v user filename

Description: Changes ownership while providing detailed information about the process.

### Interactive Ownership Modification

Command: sudo chown -i user filename

Description: Requests confirmation when changing ownership of a file or folder.

### Ownership Modification with Timestamp Preservation

Command: sudo chown --preserve-timestamps user filename

Description: Modifies file ownership while preserving timestamps associated with the file.

Mastering File Permissions: A Comprehensive Guide to Managing Access and Security Settings

### Change File Permissions

Command: sudo chmod permissions filename

Description: Modifies the permissions on a file or folder to control access and security settings.

### Change Permissions Recursively

Command: sudo chmod -R permissions filename

Description: Recursively modifies the permissions for a file or folder and its contents.

### Change File Permissions Numerically

Command: sudo chmod numbers filename

Description: Adjusts the permissions for a file or folder using a numeric code (e.g., 755).

### Change Numerical Permissions Recursively

Command: sudo chmod -R numbers filename

Description: Recursively updates the permissions of a file or folder and its sub-items using a numeric code.

### Change Permissions with Details

Command: sudo chmod -v permissions filename

Description: Alters ownership of a file or folder while providing detailed information about the permission changes made.

### Change Permissions with Confirmation

Command: sudo chmod -i permissions filename

Description: Changes ownership of a file or folder while requesting confirmation for each individual permission modification.

### Change Permissions with Reference

Command: sudo chmod --reference=reference-file filename

Description: Sets the ownership of a file or folder to match the permissions of a specified reference file.

Exploring dpkg: A Comprehensive Guide to Package Management

### Install .deb Package

Command: sudo dpkg -i file.deb

Description: Installs a specified .deb file on your system.

### Remove .deb Installed Package

Command: sudo dpkg -r package_name

Description: Uninstalls an installed .deb package while preserving its configuration files.

### Remove .deb Package with Config Files

Command: sudo dpkg -P package_name

Description: Completely removes an installed .deb package, including its configuration files.

### List Installed Packages

Command: sudo dpkg -l

Description: Lists all packages installed on the host system, along with version and description information.

### List Files Installed by Package

Command: sudo dpkg -L package_name

Description: Provides a comprehensive list of files installed by a specified package.

### Check Package Dependencies

Command: sudo dpkg -I package_name.deb

Description: Verifies and lists the dependencies required by a .deb package.

### Reconfigure Installed Package

Command: sudo dpkg-reconfigure package_name

Description: Allows you to modify the configuration settings of an already installed package.

### Fix Installs Broken by Installed Packages

Command: sudo dpkg --configure -a

Description: Repairs broken package installations by re-configuring packages that were not properly installed or configured.

Efficient File Retrieval with wget

### File Download

Command: wget url

Description: Downloads a file from the specified URL.

### Change Output Filename

Command: wget -o filename url

Description: Modifies the filename for the file to be downloaded.

### Background File Download

Command: wget -b url

Description: Downloads a file while permitting uninterrupted use of the command line.