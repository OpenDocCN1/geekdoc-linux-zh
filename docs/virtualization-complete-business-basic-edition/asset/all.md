![](images/calibre_cover.jpg)

Virtualization Complete

Business Basic Edition

Proxmox-freeNAS-Zentyal-pfSense 

By Lee R. Surber

Book Description

The Ultimate Step By Step Field Guide For Proxmox In The Real World...!!!

Learn the secrets of building a bulletproof virtual IT infrastructure.  This 4-In-1 collection leverages the power and cost effectiveness of open source Linux, delivering a complete solution in easy step-by-step format.  All the software components of this system are time tested in production and were chosen because they are simply the BEST at what they do. This field guide is easy enough for Linux beginners yet advanced enough for IT professionals!   Select your system model, then, deploy it quickly with full diagrams and ALL the necessary command line entries provided for you!

*   > > Leverage the bare metal Proxmox hypervisor to deploy a completely modular high performance foundation!

*   > > Replace costly Cisco components with easily moveable virtual pfSense managed endpoints.

*   > > Learn how to install high performance, redundant, semi-virtual freeNAS fileservers running the self-healing ZFS file system.

*   > > Replace Microsoft active directory with robust Zentyal primary and backup directory servers.

*   > > Additional content covers directory based VPN authentication, IDS, Rsync, iSCSI, NFS, LVM, ZFS snapshot backups, hardware pass-through, 10 min. disaster recovery, best practices, and much more!

*   > > Take complete control of your entire server rack through web-based management over secure VPN.

Virtualization Complete is the ONLY collection available to offer such a comprehensive working business solution!

Copyright

Linux Solutions(LRS-TEK)

Virtualization Complete

Business Basic Edition

Proxmox-freeNAS-Zentyal-pfSense 

Copyright © 2016 By Lee R. Surber Linux Solutions(LRS-TEK) 

All rights reserved.  No part of this publication may be reproduced, distributed, or transmitted in any form or by any means, or stored in a database or retrieval system, without the prior written permission of the publisher. 

Linux Solutions(LRS-TEK) 

3000 CR 615 

Alvarado,  TX  76009 

Email:  lee.surber@linuxsolutions.us 

Visit our website at [www.linuxsolutions.us](http://www.linuxsolutions.us/) 

eBook 1st Edition 

TABLE OF CONTENTS

[Book Description](#index_split_001.html_filepos611) 

[Copyright](#index_split_002.html_filepos3388) 

[.1-Introduction](#index_split_004.html_filepos17397) 

[.2-Before You Begin](#index_split_005.html_filepos26625) 

[.3-Best Practices](#index_split_006.html_filepos28974) 

> > [.3.1-Hybrid Servers](#index_split_006.html_filepos29940)

> > [.3.2-Disaster Recovery](#index_split_006.html_filepos32478)

> > [.3.3-KVM Preferred](#index_split_006.html_filepos34013)

> > [.3.4-Small Footprint Virtualization](#index_split_006.html_filepos34714)

> > [.3.5-Clustering](#index_split_006.html_filepos36343)

> > [.3.6-Maximize Performance](#index_split_006.html_filepos36999)

> > [.3.7-System Diagrams](#index_split_006.html_filepos39206)

[Book 1:  Proxmox VE](#index_split_007.html_filepos50528) 

> [1.1-Introduction To Proxmox](#index_split_007.html_filepos50660)

> [1.2-Installing Proxmox](#index_split_008.html_filepos52406)

> [1.3-Initial Login](#index_split_009.html_filepos59739)

> [1.4-Network Adapters](#index_split_010.html_filepos61979)

> [1.5-Adding LVM Storage](#index_split_011.html_filepos65541)

> [1.6-Configure LVM Storage](#index_split_012.html_filepos70296)

> [1.7-Configure NFS Storage](#index_split_013.html_filepos71958)

> [1.8-Configure iSCSI Storage](#index_split_014.html_filepos74171)

> [1.9-Creating VM Configurations](#index_split_015.html_filepos77013)

> [1.10-VM Backup & Restore](#index_split_016.html_filepos86999)

> [1.11-VM Hardware](#index_split_017.html_filepos92928)

> [1.12-Adding Pass-Through Disks](#index_split_018.html_filepos97235)

> [1.13-Troubleshooting Proxmox](#index_split_019.html_filepos105352)

> [1.14-Upgrading Proxmox](#index_split_020.html_filepos106161)

[Book 2:  pfSense](#index_split_021.html_filepos107409) 

> [2.1-Introduction To pfSense](#index_split_021.html_filepos107538)

> [2.2-Installing pfSense](#index_split_022.html_filepos110101)

> [2.3-Assigning Network Interfaces](#index_split_023.html_filepos112286)

> [2.3-Assigning IP Addresses](#index_split_024.html_filepos115257)

> [2.4-Reset Admin Password](#index_split_025.html_filepos118919)

> [2.5-Web Configuration Wizard](#index_split_026.html_filepos119701)

> [2.6-Changing Themes](#index_split_027.html_filepos125254)

> [2.7-Configure DHCP Server](#index_split_028.html_filepos126560)

> > [2.7.1-WINS, DNS, Gateway, and Domain](#index_split_028.html_filepos128086)

> > [2.7.2-DHCP Client Reservations](#index_split_028.html_filepos129335)

> [2.8-Firewall Settings](#index_split_029.html_filepos130789)

> > [2.8.1-LAN Rules](#index_split_029.html_filepos131340)

> > [2.8.2-WAN Rules](#index_split_029.html_filepos132607)

> [2.9-OpenVPN](#index_split_030.html_filepos133813)

> > [2.9.1-OpenVPN Client Export Utility](#index_split_030.html_filepos134546)

> > [2.9.2-OpenVPN Setup Wizard](#index_split_030.html_filepos135208)

> > [2.9.3-OpenVPN Client Connectors](#index_split_030.html_filepos139013)

> > [2.9.4-Authenticate Zentyal Domain Users](#index_split_030.html_filepos140300)

> [2.10-Snort IDS](#index_split_031.html_filepos143634)

> > [2.10.1-Install Snort Package](#index_split_031.html_filepos144780)

> > [2.10.2-Snort Global Settings](#index_split_031.html_filepos145641)

> > [2.10.3-Snort Interfaces](#index_split_031.html_filepos146037)

> > [2.10.4-Updating Threat Rules](#index_split_031.html_filepos148165)

> > [2.10.5-Threat Rule Categories](#index_split_031.html_filepos148542)

> > [2.10.6-Add Alerts To Suppression List](#index_split_031.html_filepos149705)

> > [2.10.7-Block Offenders At Source](#index_split_031.html_filepos150555)

> [2.11-Configuration Backups](#index_split_032.html_filepos151614)

[Book 3:  freeNAS](#index_split_033.html_filepos153134) 

> [3.1-Traditional Storage Fails](#index_split_033.html_filepos153263)

> [3.2-freeNAS & ZFS](#index_split_034.html_filepos158684)

> [3.3-Installing freeNAS](#index_split_035.html_filepos159656)

> [3.4-Add freeNAS Pass-Through Disks](#index_split_036.html_filepos163763)

> [3.5-Set Storage For No Backup](#index_split_037.html_filepos165198)

> [3.6-Start freeNAS Through The Console](#index_split_038.html_filepos166572)

> [3.7-Initial Login](#index_split_039.html_filepos167436)

> [3.8-freeNAS Navigation](#index_split_040.html_filepos168229)

> [3.9-Network Configuration](#index_split_041.html_filepos168671)

> [3.10-Users And Groups](#index_split_042.html_filepos170783)

> > [3.10.1-Adding A New User](#index_split_042.html_filepos170894)

> > [3.10.2-Adding A New Group](#index_split_042.html_filepos172510)

> [3.11-Add A ZFS Volume](#index_split_043.html_filepos173178)

> [3.12-Detach And Move Volumes](#index_split_044.html_filepos174244)

> [3.13-ZFS Datasets](#index_split_045.html_filepos176971)

> [3.14-ZFS Permissions](#index_split_046.html_filepos180713)

> [3.15-freeNAS Services](#index_split_047.html_filepos182750)

> > [3.15.1-CIFS(Windows Sharing) Service](#index_split_047.html_filepos183226)

> > [3.15.2-NFS(Linux Sharing) Service](#index_split_047.html_filepos184498)

> > [3.15.3-iSCSI Target Service](#index_split_047.html_filepos185721)

> > [3.15.4-Rsync(Backup) Service](#index_split_047.html_filepos187083)

> > [3.15.5-SSH(Secure Shell) Service](#index_split_047.html_filepos188051)

> [3.16-Add Network Shares](#index_split_048.html_filepos189275)

> > [3.16.1-NFS Shares](#index_split_048.html_filepos189388)

> > [3.16.2-Windows Shares](#index_split_048.html_filepos191389)

> > [3.16.3-iSCSI Target Shares](#index_split_048.html_filepos192766)

> [3.17-ZFS Snapshot Backups](#index_split_049.html_filepos200154)

> [3.18-Restore A Snapshot In Windows](#index_split_050.html_filepos203397)

> [3.19-Rsync Replication](#index_split_051.html_filepos204679)

> > [3.19.1-Add The Rsync Push Task](#index_split_051.html_filepos206034)

> > [3.19.2-Add The Rsync Module](#index_split_051.html_filepos210666)

> > [3.19.3-Tips On Using Rsync](#index_split_051.html_filepos212722)

> [3.20-Domain Membership](#index_split_052.html_filepos214725)

> > [3.20.1-Domain Permissions](#index_split_052.html_filepos218609)

> [3.21-Configuration Backups](#index_split_053.html_filepos219629)

[Book 4:  Zentyal Domain Controller](#index_split_054.html_filepos220923) 

> [4.1-Introduction To Zentyal](#index_split_054.html_filepos221070)

> [4.2-Installing Zentyal](#index_split_055.html_filepos222574)

> [4.3-Initial Login](#index_split_056.html_filepos227249)

> [4.4-Initial Setup](#index_split_057.html_filepos228620)

> [4.5-Navigating Zentyal](#index_split_058.html_filepos231647)

> [4.6-Adding Users](#index_split_059.html_filepos232445)

> [4.7-Adding Groups](#index_split_060.html_filepos233639)

> [4.8-Additional Domain Controller](#index_split_061.html_filepos234836)

> [4.9-Shut Down & Reboot](#index_split_062.html_filepos236034)

> [4.10-Upgrading Zentyal](#index_split_063.html_filepos236462)

> [4.11-Joining Zentyal Domains](#index_split_064.html_filepos237316)

> > [4.11.1-Workgroup Authentication](#index_split_064.html_filepos239120)

> > [4.11.2-Join The Domain In Windows](#index_split_064.html_filepos242382)

> [4.12-Configuration Backups](#index_split_065.html_filepos244007)

[.4-Final Thoughts And Thanks](#index_split_066.html_filepos245971) 

[.5-Additional Resources](#index_split_067.html_filepos247862) 

.1-Introduction

After a decade of research and experimentation this book will reveal the secrets of building a bulletproof virtual IT infrastructure.  It leverages the power and cost effectiveness of open source Linux, delivering a complete solution in easy step-by-step format.  Full system diagrams have also been included to help visualize your system!  All the software components of this system are time tested in production and were chosen because they are simply the BEST at what they do.  Ideally suited to the business environment, this is the ONLY book available today that offers such a complete working solution!

.1.1-Who is this book designed for?

When writing this book I wanted to keep it simple enough for Linux beginners yet advanced enough conceptually that IT professionals would still find benefit.  With all command line entries included and easy to read diagrams, THIS IS the field guide I had always hoped for when starting years ago in virtual infrastructure!

.1.2-What you will learn!

There are so many cookbook methods about virtualization today that you can quickly become overwhelmed.  It's all too easy to end up with an overly complex system that ultimately performs poorly.  The focus of this book is to keep installation and setup as simple as possible while still maintaining a very high level of performance and reliability.  Upon completion you can be assured of the following:

*   > > You will understand installation and setup of a multi-machine Linux powered virtual infrastructure.

*   > > You will learn how to install a virtual managed endpoint/router supporting 30 second migration between servers.

*   > > You will learn how to configure world class intrusion detection that blocks offenders immediately.  This also includes threats from smart phones and thumb drives!

*   > > You will learn how to install virtual  Linux based primary and backup domain controllers.  These controllers are fully compatible with Microsoft Active Directory.

*   > > You will learn how to configure a VPN tunnel on your new virtual router.

*   > > You will learn how to setup domain authentication for your virtual VPN server.

*   > > You will learn how to install semi-virtualized hybrid fileservers using a simple hardware pass-through method.

*   > > You will learn how to configure fileserver redundancy leveraging the power of Rsync.

*   > > You will learn how to configure the self healing ZFS file system for sustained I/O rates between 30 and 60 Megabytes/sec using Gigabit adapters.

*   > > You will learn how to leverage ZFS snapshot backups avoiding the need for expensive backup software.

*   > > You will learn how EASY IT Administration really can be!

.1.3-Key features!

Most people do not want or welcome change unless the benefits are overwhelmingly positive!  You can be assured of the following:

*   > > You will maintain full Microsoft compatibility.

*   > > You can use existing hardware in most cases.

*   > > You will have even greater software compatibility.

*   > > You will NEVER have to pay for licensing again.

*   > > You can simplify management and reduce IT staff.

*   > > You will have more security to protect against intrusion and attack.

*   > > You will have mobile connectivity with your office.

*   > > You will have complete web-based remote control of all your systems.

*   > > You will have instant backups available.

*   > > You will save 90% over traditional system costs.

.1.4-How easy is it to install?

Every component in my system is based off an ISO CD/DVD Distribution!  Linux gurus may want to roll their own system but it really isn't needed.  This approach simplifies system setup and reduces the knowledge required to  get it all up and running!

.1.5-What Linux distributions are used in this system?

The following Linux distributions are what I have chosen after years of research and testing:

*   > > Proxmox VE - for virtualization platform

*   > > pfSense - for routing, firewalling, NAT, intrusion detection, and VPN

*   > > Zentyal Server - for Samba based active directory

*   > > freeNAS - for file storage using the robust ZFS file system

.1.6-I don't know Linux!  It's too complicated!

Linux is complex!  Even professionals need to reference documentation!  For that reason I have included all the command line entries you will ever need.  This truly is a step-by-step field guide!  One of the key concepts here is to keep it simple!  Virtualized machines can be recovered in minutes if something goes wrong.  There is no need for complex raid devices or network configurations! You can feel relaxed that you will have an extremely reliable high performance system when completed!

.2-Before You Begin

*   > > You will need a copy of PuTTY installed on your workstation for some SSH session command line post-install changes.  Putty can be downloaded here:  [PuTTY console](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)

*   > > You will need computers capable of running Proxmox.  I recommend the best multi-core machines you can spare with at least 16-32Gb of Ram.  The more cores and RAM the better.  You will also want multiple gigabit network adapters and multiple hard drives for storage.  2 to 6 Terabytes of storage per Proxmox server would be nice.

*   > > You will need one or more unmanaged Gigabit network switches for reliable high speed networking.

*   > > Since you will be installing NAS storage on these machines make sure you have enough hard disks installed.  Example:  1 x 500Gb disk for Proxmox, 1 x 500Gb disk for VM images, and 2 x 2Tb drives for NAS hardware pass-through.

*   > > If you want to take advantage of VPN you will need an internet connection.  Most residential providers use sticky IP connections, captive portal, and layer 2 hardware authorization.  This essentially means you have a cheap static IP address and didn't even know it.  If your IP changes....simply edit your DNS zone record to the new IP.

NOTE:  I recommend detaching all hard disks and network adapters with the exception of the Proxmox OS drive and the primary network interface.  You will re-enable these additional drives and network adapters  after the install.

.3-Best Practices

While writing this book I had to make a decision where to put this section.  I feel so strongly about my chosen methods that I decided to cover it right here in the beginning.  No need to worry if you don't fully grasp some of these methods right now!  As you progress they will be re-introduced and further explained, where they will make much more sense!

Over the years, as advancements came, I tested and deployed.  I've tried HA, clustering, iSCSI backed storage, QCow vs Raw vs vmdk disk, OpenVz vs KVM, virtio drivers, and the list goes on!  Along the way I learned some hard lessons!  So, this section is dedicated to tips and tricks that will make your deployments super simple and maximize the use of your hardware.  Here we go!

.3.1-Hybrid Servers

Take advantage of modern hardware by building hybrid platforms.  Essentially, you create a virtualization host with a built in bare metal NAS server.  You install the NAS just like any other VM with its OS residing on a virtual disk.  The actual storage drives will reside on a physical LVM array assigned through a technique known as hardware pass-through.  This method provides very respectable data read/write performance!  I have tested sustained throughput rates in the range of 30-60 Megabytes/sec using Gigabit adapters.

The biggest advantage is that your data is NOT stored in a virtual disk file!  Even if you destroy the VM the data remains safe!  This approach maximizes the use of your hardware resource and makes management, maintenance, and disaster recovery MUCH easier!

For example:  The following scenarios should help understand cost and benefit!

*   > > Scenario 1:  Let's assume you have 2 Proxmox servers, 2 brand(x) NAS/SANs, and 1 brand(x)Router.  You have consumed 5 positions in your rack and you cannot use 3 of those positions for anything else.  If a NAS or Router goes down due to hardware failure you WILL be down for 6-24hrs at the minimum unless you have an exact duplicate laying around.

*   > > Scenario 2:  Let's assume you have 5 Proxmox servers un-clustered.  You have consumed 5 positions in your rack and each position can host anything!  Some or all of these could be hybridized using hardware pass-through for NAS drives and extra network adapters for routing.  If any machine went down you simply transfer the hot-swap storage drives for the NAS to the next Proxmox server, map a couple network adapter Mac addresses for the Router, restore your virtual machine images, and you're back running in 15 minutes or less!   It is also important to note that this method does NOT cripple Proxmox in any way with respect to other VM's you wish to install providing you have enough disk and network resources.

.3.2-Disaster Recovery

If any of your Proxmox servers go down the single most important item to recover will ALWAYS be your VM image backups.  Think of them as Master Recovery Images!   Without these you are lost so it is important to have as many copies as possible!  My preferred method is to select a NAS(virtualized or standalone) to use as my primary VM image backup server.  This server will host the NFS image backup share to Proxmox.  This share is manually replicated(only once during setup) to all other NAS servers in the system and synchronized on schedule using Rsync.  If a  machine goes down I can replace it, re-install Proxmox, re-install any NAS drives , re-map my NFS backups, and restore the VM images.  Once again, you're back running in 15 minutes or less!  This method has served me very well and is rock solid time tested!

KEEP A COPY ON THUMB-DRIVE:  Another highly recommended tip is to copy your VM image backups to a thumb-drive or DVD then store them in a fireproof safe.  You can easily map a read-only samba share of your VM image backups to be accessible from any windows machine or android phone.  Using the small footprint method  described below ensures your entire VM image backup archive will easily fit on a modern 64-128GB USB thumb-drive.

.3.3-KVM Preferred

Proxmox allows for 2 types of virtualization, KVM and OpenVZ.  The key difference between the two, is that KVM is fully virtualized, where OpenVZ is partially virtualized.  While OpenVZ does yield performance benefits over KVM, it loses in every other way.   My choice is to only use KVM!  I will always choose compatibility and easy disaster recovery over performance!  If you require more performance get better hardware!  You can easily build a water-cooled over-clocked rocket with 8 or more cpu cores and 32Gb or more RAM on the cheap today!

.3.4-Small Footprint Virtualization

My preferred approach is what I term small footprint virtualization.  Let's assume you have a 2008 Windows Server with a need for 500GB capacity.  There are 2 installation approaches that will work!

*   > > Scenario 1:  You could create a VM with virtual disks totaling 500GB.  With this method you're looking at large image backups that take a long time to complete!  Should you need to move or recover using a backup image it will also take a long time to restore!

*   > > Scenario 2:  With small footprint virtualization you create a VM with as small a virtual disk as allowable, then use a network backed resource such as iSCSI from within the guest to map the additional capacity requirement.  This method allows for super fast backup and restore at the expense of some performance.

In production environments the flexibility of small footprint virtualization exceeds any minor performance hits.  It allows you to backup and restore a VM with large capacity mappings to another physical machine quickly.  This comes in very handy if you need to pull a machine down for maintenance.

.3.5-Clustering

In this book I do not cover clustering because it does NOT fit the simplicity model.  Clustering is great for managing a large number of servers from a single interface but does add complexity to the system!  It also relies heavily on network backed storage which reduces overall VM performance levels compared to dedicated hardware installs.  When a cluster breaks you may want to plan on an all-nighter!  Keeping your Proxmox servers un-clustered still allows for most recoveries and moves within minutes!

.3.6-Maximize Performance

Another preferred approach I will share based on experience should be a no-brainer.  Any VM will perform better if it has dedicated disk and network hardware.  If you can spare the extra disks and network adapters it is highly recommended!

I think a good general rule is to allow no more than 2 VM guests per physical device.  One being a low throughput guest while the other can be high throughput.  For example: a domain controller only handling authentication can easily share a disk and network adapter with a multi-domain email server.  A multi-domain web server may not share resources well under load with a file server.

SSD DRIVES:  I have had very good luck running up to 6 small footprint VM installs on just one SSD drive.  Each one of these had dedicated network adapters!

AVOID NETWORK BACKED STORAGE IN PRODUCTION:  This storage type is typically used by large enterprise with hundreds of servers where internet speed is the limiting factor and intermittent performance dynamics are expected.  It relies on various protocols such as GlusterFS, RBD, iSCSI, and NFS.  The iSCSI protocol is by far the most common and versatile of these for small to medium sized deployments.  While iSCSI does work and is useful for testing environments, the performance is NOT on par with installs to local dedicated hardware.  Over a 10 year period I tried EVERY conceivable configuration in an environment with VERY respectable resources!  My conclusion:  If you MUST install a network backed VM it's because you failed to build your system with enough storage or you don't have enough Proxmox servers available!  If you're going to map iSCSI targets do it from within a guest VM running on dedicated hardware!  You will have respectable performance and you will GAIN hugely in backup and recovery management.

.3.7-System Diagrams

(Option-1)  Optimal Hardware Benefit

The drawing below shows a system with 3 hybrid Proxmox servers. It is designed to maximize resources by making use of ALL available physical machines!  EVERY virtual machine is installed on dedicated disk and network hardware for best production performance.  VM installation to network backed storage(iSCSI and NFS) can still be used for temporary lower performance requirements.

![](images/00074.jpg)  

freeNAS-1 Role In (Option-1) System

In this system freeNAS-1 is setup as the primary NAS fileserver.  It will host traditional Windows(CIFS), Linux(NFS), media, and ftp to your network clients.  It will also host data related(NO BACKUP DRIVES) iSCSI targets to be mapped from within guest operating systems.  All shares are manually replicated during setup to freeNAS-2 and freeNAS-3 where they are automatically synchronized once per hour using Rsync.

freeNAS-3 Role In (Option-1) System

In this  system freeNAS-3 is setup to serve special Proxmox NFS shares for Templates, Containers, ISO, and VM Image Backups.  It will provide load balancing by hosting shares for network client backups. This also includes backup related(NO DATA DRIVES) iSCSI targets to be mapped from within guest operating systems.  freeNAS-3 can host iSCSI and NFS targets for Proxmox VM images but should be avoided due to weaker performance.  All shares are manually replicated during setup to freeNAS-1 and freeNAS-2 where they are automatically synchronized once per hour using Rsync.  freeNAS-3 is only available to network clients for backup purposes.

IMPORTANT:  There is a caveat!  Since freeNAS-3 is virtualized it will not be able to backup its own VM image!  You MUST backup this VM image to a different NFS share hosted by freeNAS1(nfs.netbackups2) then use Rsync once again to automatically synchronize the dataset to all other nodes.  NOTE:  nfs.netbackups2 will ONLY be used for freeNAS-3 VM Image Backups while ALL other VM Image Backups will be sent to the nfs.netbackups share.

freeNAS-2 Role In (Option-1) System

freeNAS-2 does not host anything and is not available to network clients.  It receives Rsync backups on schedule from freeNAS-1 and freeNAS-3 for disaster recovery usage.  It could also be used to load balance by serving read only shares for files that don't change much.

With a little Rsync magic, all NAS servers end up containing the same datasets.  The end result is a fully virtualized web administered business solution with 3 mirrored NAS servers, active directory, domain control, DHCP, DNS, firewall, intrusion detection, and VPN capability!

(Option-2)  Optimized For Network Backed Storage

The drawing below shows a system with 2 hybrid Proxmox servers and 1 standalone NAS. It is designed to maximize network backed storage performance by making use of a standalone freeNAS server.  Network backed storage is commonly used in larger clustered systems.  It makes use of the iSCSI and NFS protocols enabling Proxmox to leverage remote storage.  EVERY virtual machine should still be installed on dedicated disk and network hardware for best production performance.  This system offers very acceptable performance when installing VM's on iSCSI or NFS targets.  It also provides excellent image backup performance at the expense of using an entire slot in your server rack.  There is once again a caveat here!  If the standalone freeNAS-3 goes down do to hardware failure you may be down for 6hrs or more unless you have identical hardware to replace it with.

![](images/00059.jpg)  

freeNAS-1 Role In (Option-2) System

In this system freeNAS-1 is still setup as the primary NAS fileserver.  It will host traditional Windows(CIFS), Linux(NFS), media, and ftp to your network clients.  It will also host data related(NO BACKUP DRIVES) iSCSI targets to be mapped from within guest operating systems.  These shares are manually replicated during setup to freeNAS-2 and freeNAS-3 where they are synchronized once per hour using Rsync.

freeNAS-3 Role In (Option-2) System

In this system freeNAS-3 is setup to serve special Proxmox NFS shares for Templates, Containers, ISO, and VM Image Backups.  It will provide load balancing by hosting shares for network client backups. This also includes backup related(NO DATA DRIVES) iSCSI targets to be mapped from within guest operating systems.  All shares are manually replicated during setup to freeNAS-1 and freeNAS-2 where they are automatically synchronized once per hour using Rsync.  freeNAS-3 is only available to network clients for backup purposes.

Main Difference:  With bare-metal performance it can now be used to host iSCSI targets for Proxmox VM images.  Using iSCSI multipath drivers with high quality network hardware yields very acceptable performance in critical testing environments.

freeNAS-2 Role In (Option-2) System

In this system freeNAS-2 does not host anything and is not available to network clients.  It receives Rsync backups on schedule from freeNAS-1 and freeNAS-3 for disaster recovery usage.  It could also be used to load balance by serving read only shares for files that don't change much.

With a little Rsync magic, all NAS servers end up containing the same datasets.  The end result is a semi virtualized web administered business solution with 3 mirrored NAS servers, active directory, domain control, DHCP, DNS, firewall, intrusion detection, and VPN capability!

(Option-3)  Easy Offline Router Migration

The drawing below shows a system with 3 hybrid Proxmox servers. With the addition of a simple 5 port switch and some well thought planning it is possible to move the pfSense router between Proxmox1 and Proxmox2.  The system is designed to maximize resources by making use of ALL available physical machines!  EVERY virtual machine is installed on dedicated disk and network hardware for best production performance.  VM installation to network backed storage(iSCSI and NFS) can still be used for temporary lower performance requirements.

![](images/00066.jpg)  

freeNAS-1 Role In (Option-3) System

In this system freeNAS-1 is setup as the primary NAS fileserver.  It will host traditional Windows(CIFS), Linux(NFS), media, and ftp to your network clients.  It will also host data related(NO BACKUP DRIVES) iSCSI targets to be mapped from within guest operating systems.  All shares are manually replicated during setup to freeNAS-2 and freeNAS-3 where they are automatically synchronized once per hour using Rsync.

freeNAS-3 Role In (Option-3) System

In this  system freeNAS-3 is setup to serve special Proxmox NFS shares for Templates, Containers, ISO, and VM Image Backups.  It will provide load balancing by hosting shares for network client backups. This also includes backup related(NO DATA DRIVES) iSCSI targets to be mapped from within guest operating systems.  freeNAS-3 can host iSCSI and NFS targets for Proxmox VM images but should be avoided due to weaker performance.  All shares are manually replicated during setup to freeNAS-1 and freeNAS-2 where they are automatically synchronized once per hour using Rsync.  freeNAS-3 is only available to network clients for backup purposes.

IMPORTANT:  There is a caveat!  Since freeNAS-3 is virtualized it will not be able to backup its own VM image!  You MUST backup this VM image to a different NFS share hosted by freeNAS-1(nfs.netbackups2) then use Rsync once again to automatically synchronize the dataset to all other nodes.  NOTE:  nfs.netbackups2 will ONLY be used for freeNAS-3 VM Image Backups while ALL other VM Image Backups will be sent to the nfs.netbackups share.

freeNAS-2 Role In (Option-3) System

freeNAS-2 does not host anything and is not available to network clients.  It receives Rsync backups on schedule from freeNAS-1 and freeNAS-3 for disaster recovery usage.  It could also be used to load balance by serving read only shares for files that don't change much.

With a little Rsync magic, all NAS servers end up containing the same datasets.  The end result is a fully virtualized web administered business solution with 3 mirrored NAS servers, active directory, domain control, DHCP, DNS, firewall, intrusion detection, and VPN capability!

Book 1:  Proxmox VE

1.1-Introduction To Proxmox

With an active community and rock solid distribution Proxmox shines!  You can download it in CD/DVD ISO format from the Proxmox website here:  [Proxmox VE](http://proxmox.com/en/downloads)   For the purpose of this book I have used Proxmox VE 3.4\.  Once you have it downloaded , burn it to disk,  insert it, and follow the simple installation routine.  For those who aren't familiar Proxmox is a complete open source virtualization management platform.  It offers  enterprise class features such as  HA, clustering, live migration, web management, and hardware  pass-through capability.  It also is capable of running on the newest ZFS file system and allows both KVM and Open VZ container virtualization types.

With advancements in modern hardware there is really no reason NOT to virtualize.  It makes management and maintenance simple while affording greater compatibility lending to longer software/hardware life cycles.

If you rely on Windows XP 32 bit for some over-priced software package you're no longer going to have to upgrade do to hardware failure on the physical machine.  Simply virtualize that machine from backup!

NOTE:  Proxmox is a powerful platform and it's feature-set cannot be completely covered in this book.  This guide was designed as a step-by-step to get you up and running quickly.  I highly recommend tapping the wealth of online resources available for a more thorough understanding.

1.2-Installing Proxmox

Insert the Proxmox disk and boot the machine.  You will be greeted by the following window.

To continue: Press Enter 

![](images/00084.jpg)  

EULA

The next screen (shown below) contains the END USER LICENSE AGREEMENT (EULA).  I know you will carefully read this from beginning to end!  When finished reading:

To continue: Click I Agree 

![](images/00081.jpg)  

Configuring The Hard Disk

This step assumes a simple install with one drive and no raid.  My personal preference here is to only have one disk attached to the motherboard for a fresh install.  Just detach all disks with exception of the one used for the OS. This avoids any possible MBR issues if you ever need to remove disks due to failure.  It's easy to get confused if you have multiple hard disks installed in any machine.  For this reason I like to include a hard disk ID map.  This can be as simple as a sticky note or magic marker ID's on each disk.

NOTE:  It has been long advised by the Proxmox developers to only install to a single disk partitioned and managed by LVM.  Raid has not been supported until recently.  My personal opinion is that raid really doesn't matter.  A properly maintained system will always be pulled from service before a catastrophic  disk failure happens.  There are ALWAYS warning signs!  From an engineering perspective a parity array such as RAID(1, 5, 6, or 10) introduces extended duty cycles and heat buildup thus shortening motor life.  A striping array such as RAID-0 reduces duty cycles and heat buildup thus increasing motor life.  It also provides increased throughput as a bonus!  It is the only RAID I use for these stated reasons!

Back to the install!  By clicking the options button below you will notice that  Proxmox now allows for ZFS raid configuration.  As mentioned above I do not use this but it is an option if you desire.  If you are following my instructions, which you should be, we will be performing a default installation to the primary target disk (/dev/sda) so close the options dialog if you opened it.

To continue: Click Next 

![](images/00249.jpg)  

Choose Your Location And Time

Next you will setup your default location and time zone.

To continue: Click Next 

![](images/00029.jpg)  

Root Password And Email Address

Now you will set your root password and email address.  Make sure to use a strong root password!

To continue: Click Next 

![](images/00018.jpg)  

Network Configuration

Next you will setup your network.  Your settings should look something like this(where x can be substituted for any number between 0 and 255):

FQDN: proxmox1.yourdomain.com

IP Address:  192.168.x.2

Netmask: 255.255.255.0

Gateway: 192.168.x.254

DNS: 192.168.x.254

NOTE:  We choose 192.168.x.254 for both gateway and DNS because it lies outside the DHCP address range defaults(192.168.x.100-192.168.x.200) on most routers.  For specific rules on private IP addressing do an internet search for RFC 1918 guidelines.  I highly recommend using pfSense for a managed endpoint/routing platform!  I have used it for 7 years virtualized without incident!  It will handle all DHCP, DNS, NAT, VPN, and Intrusion Detection.  You can download it here:  [pfSense router](https://www.pfsense.org/download/) 

To continue: Click Next 

![](images/00369.jpg) 

Installation Successful

To continue: Click Reboot 

![](images/00353.jpg) 

PLEASE NOTE:  When Proxmox reboots take note of the address for logging in to the web interface.  It should match the address set in the previous network configuration screen.

Example:  https://192.168.10.2:8006

![](images/00198.jpg)  

At this point you need to login as root using the password you provided during installation and issue a shutdown.  The command is shown below.  Only type the word poweroff followed by the Enter key.

# poweroff

HIGHLY RECOMMENDED:  Once the machine powers down you will install any additional network adapters and hard disks.  I recommend labeling the network adapters used in the system with MAC/Hardware address.  If you are not familiar with MAC/hardware addresses they usually look something like this  92:26:b9:c2:42:15 and should be clearly identified on your device.  You need the ability to identify each network port externally using its MAC.  I personally write the last 4 digits of the MAC on each adapter bracket with magic marker for easy identification.

I have found that some USB network adapters do work well and will be pre-labeled with ID and serial.  I use these for low bandwidth connections such as the pfSense router.

When finished start the machine for the next step in the setup.

1.3-Initial Login

Now the you have completed the install it is time to login.  Open your favorite web browser (I use Mozilla Firefox) then enter the ip address you chose during installation.

Please Note:  Proxmox uses secure port 8006 by default

Your entry should look something like this:

https://192.168.10.2:8006

You will then see a secure connection warning as pictured below.  Click I Understand the Risks 

![](images/00355.jpg)  

Next:  Click Add Exception as pictured below

![](images/00001.jpg)  

Then: Click Confirm Security Exception as pictured below

![](images/00026.jpg)  

Now login as user: root with the password you set during install

![](images/00088.jpg)  

Proxmox VE is a community edition but you can elect a subscription account that entitles full support.  This is not necessary but you will see the subscription reminder(shown below) each time you log in.  I find Proxmox to be an excellent software and really don't mind seeing a popup reminder!  After all!  It is free!

![](images/00327.jpg)  

You will now see the web management interface(shown below).  This is where you will create and configure your virtual machines.

![](images/00114.jpg)  

1.4-Network Adapters

Now you need to configure your network adapters so they can be used for any VM's (virtual machines) you create.  Notice that the network tab is not shown in the default view (datacenter view).  You must be in node view to see the network tab.  In the case pictured below the node is called proxmox5.

Click the node (pictured below)

![](images/00328.jpg)  

Click the Network tab (pictured below)

![](images/00299.jpg)  

Click Create >> Linux Bridge (pictured below)

![](images/00091.jpg)  

You will now see the Linux Bridge Dialog (pictured below).  For each network adapter you will create a bridge.  You can see (for this guide) I have filled the form using industry standard naming convention and have kept a 1:1 relationship between eth(x) and vmbr(x) ports.  For the first time user I would suggest following this rule but you could easily map vmbr1 >> eth2 instead.  There will be only 1 default internet Gateway which is pre-configured during install and used by vmbr0 so leave this field blank.

NOTE:  For the IP address field make sure to use a subnet that will NOT be used in your system (such as 10.10.x.x).  Also make sure to use an appropriate Subnet mask for your chosen IP address range.  IF you are unfamiliar with network addressing Google CIDR for more information.  The complexities of network engineering are beyond the scope of this step by step guide but there is a wealth of knowledge to be found on the internet.

When finished click Create 

![](images/00213.jpg) 

NOTE:  Repeat the above steps for each adapter you wish to use on your new Proxmox server.  For Example: vmbr2 >> eth2  @ 10.10.30.2/255.255.255.0

Changes will not take effect until the system is rebooted.

Restart now using the button in the upper right hand corner of the node view (you should already be in node view).

![](images/00301.jpg)  

When the system finishes rebooting it should refresh the screen automatically.  You can validate that your virtual interfaces are ready if the yes value in the active column appears(pictured below).  Once again, repeat this process for all network adapters you intend to use.  You can see here that I have 3 physical adapters but only 2 are configured and ready.

![](images/00349.jpg)  

1.5-Adding LVM Storage

Before you can add LVM storage you will need to install PuTTY.  PuTTY is a great open source console which allows SSH (Secure shell) access to other computers.  It can be downloaded here:  [PuTTY console](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) 

Once installed, open it, check SSH connection, type the ip address of your Proxmox server then click Open.

![](images/00102.jpg)  

Click Yes to the PuTTY Security Alert (pictured below)

![](images/00002.jpg)  

Login as user: root with the password you set when installing Proxmox

Now type the following command:

# cat /proc/partitions

![](images/00077.jpg)  

This command will generate a list of hard disk devices as pictured below.  We are interested in a new device that does not look to be in service.  The ONLY possible device as seen below is /dev/sdb because it contains no partitions at all.  Now we have enough information to setup a logical device with this disk.

![](images/00137.jpg)  

Now that you know which disk to use you can create a physical volume with the following command:

# pvcreate /dev/sdb

![](images/00209.jpg)  

You will now see the volume confirmation as pictured below

![](images/00335.jpg)  

Now that a physical volume exist you can create a volume group called lvstorage (or some other name of your choice).

To create the volume group issue the following command:

# vgcreate lvstorage /dev/sdb

![](images/00336.jpg)  

You will now see the volume group confirmation as pictured below

![](images/00319.jpg)  

You are now finished in the command console and may close the PuTTY program.

I highly recommend learning as much about Linux LVM as possible.  It is my preference to use LVM for everything!  It boots using UUID serialization which makes it bullet-proof-bootable and allows for easy removal of drives for relocation to other machines.  You can also create striping or mirrored volumes and it supports snapshots, resizing, moving, etc....  It is light weight and fits our simplicity model perfectly!

About LMV

LVM storage is characterized by three components, which are, physical volumes, volume groups, and logical volumes.  A volume group is made up of 1 or more physical volumes.  A PV (physical volume) is nothing more than a hard drive.  The primary storage component is the logical volume.  A volume group can be sliced up into many logical volumes.  For example:  You have 3 x 500GB physical disks making up your VG (volume group).  These are /dev/sda,b,and c respectively.  The total capacity of this group will be 1.5TB which you may name vg_500gbint.  I like to use a name that tells what device sizes I am using and whether they are internal or external devices.  You could then create 2 x 750GB LV's (logical volumes) or 15 x 100GB LV's from your 1.5TB VG.

You may wish to name your LV's something like lv1_vg500gbint indicating it as the first logical volume associated with the volume group named vg_500gbint.

1.6-Configure LVM Storage

Now that you have added a logical volume group at the command line it is time to configure how it is used in Proxmox.  One thing to note is that(in this guide) LVM storage through the web interface will only be used for VM images.  This special storage area is where all your virtual machines will keep their assigned hard drives.

To get started make sure your in datacenter view then click the Storage tab(pictured below). Next click Add >> LVM(pictured below).

![](images/00068.jpg)  

You should now see the LVM dialog box(pictured below).  The lvstorage group you created using PuTTY can now be selected.  Type a unique name for the ID field(pictured below).

When finished: Click Add.

NOTE:  Often times I choose a name that indicates the storage type such as LV_vg80gbint.

![](images/00125.jpg)  

You should now see your new LVM storage in the tree view(pictured below).  Clicking on the summary tab shows the available size of your new storage(pictured below).

![](images/00330.jpg)  

1.7-Configure NFS Storage

NFS is perhaps the most diverse of all storage types you will use.  It is a network based storage so you will need a NAS configured on your local subnet in order to use it.  NFS can be used for image, backup, template, ISO, and container storage in Proxmox.  I have extensively tested all types of storage in Proxmox over the years.  As previously mentioned, my storage of choice for local images is LVM based!  Well, my preference for network backed storage is NFS!  It offers performance rivaling that of iSCSI without any of the complexities.

In this section I will demonstrate the configuration of an existing NFS share to be used for VM backup archives.  In production you will probably want(at least) an additional share for CD/DVD ISO files.  Backups and ISO's are the ones I tend to need the most!

To get started make sure your in datacenter view then click the Storage tab(pictured below).

Next click Add >> NFS(pictured below).

![](images/00207.jpg)  

You should now see the NFS dialog box(pictured below).  Type the IP address of your NAS storage.  Type a unique name for the ID field(pictured below).  Choose the appropriate NFS Export from the dropdown list.  You can also select how many backup archives are allowed per VM.

When finished: click Add.

NOTE:  Often times I choose a name that indicates the storage type such as NFS_NetBackups.

![](images/00216.jpg)  

You should now see your new NFS storage in the tree view(pictured below).

![](images/00307.jpg)  

1.8-Configure iSCSI Storage

The 3rd and final storage option for Proxmox that we will cover in this book is iSCSI.  This storage type is typically used by large enterprise with hundreds of servers where internet speed is the limiting factor and intermittent performance dynamics are expected.  Because it is network backed storage, VM performance suffers compared to dedicated hardware installs.  For this reason I do not recommend using it for any critical production application.

Although it does have network imposed limitations it is very flexible and when used with high quality hardware can yield very reasonable performance.  Where iSCSI shines is in a large testing environment where you need temporary storage space allocations on a frequent basis.  Because it fools the operating system into thinking it has extra local disks the possibilities are endless.  For example:  It could easily be used to configure an LVM based mirrored array that is mapped to a specific directory then mounted and used for VM images, containers, templates, etc.  To learn how iSCSI targets are setup in freeNAS click here: [3.16.3-iSCSI Target Shares](#index_split_048.html_filepos192766) 

To map an iSCSI target make sure your in Datacenter >>Storage then click Add>>iSCSI(shown below).

![](images/00122.jpg)  

You will then see the following dialog.  Enter the ID and Portal information then select the Target from the dropdown list(shown below).  If you do not wish to configure the target as an LVM disk for mounting make sure the option Use LUN's directly is checked.

![](images/00124.jpg)  

To proceed:  click the Add button(shown below).

![](images/00103.jpg)  

When the target has been successfully added it will appear as a new storage device(pictured below).

![](images/00254.jpg)  

You should now be able to view the content information by selecting it from the node tree(shown below).

![](images/00106.jpg)  

1.9-Creating VM Configurations

Now that you have Proxmox configured you can create your first VM(virtual machine)!  Let's get a pfSense router configuration setup!

To begin: click Create VM in the upper right corner.

![](images/00020.jpg)  

Now assign an ID and Name your new VM.

To continue: Click Next 

![](images/00264.jpg)  

Next, select the OS type.  pfSense is BSD based so choose (other).

To continue: Click Next 

![](images/00255.jpg)  

The next step assumes that you have an ISO storage setup and working with the latest pfSense-LiveCD.  For this guide I am using version 2.2.4 Release.  If you don't have any ISO storage you can click local in the node tree view then upload your CD/DVD image.  Alternatively, you can burn the ISO to disk then select Use physical CD/DVD Drive(pictured below).

To continue: Click Next 

![](images/00151.jpg)  

Next, you will configure hard disk parameters.  For this pfSense install use IDE device type with 8GB disk.  You can choose local or the lvstorage you configured earlier in this guide.

NOTE:  After extensive testing my preferred disk configuration is ALWAYS to use IDE Bus, Raw disk Format, and Default Cache settings.

When finished: Click Next 

![](images/00241.jpg)  

Now select how many CPU cores to use for processing.  Do NOT set more cores than you have available or your VM will not boot!  For CPU type I recommend KVM.  In some cases your VM may fail to boot.  If that's the case select QEMU instead.

SPECIAL CASE:  The BSD based pfSense is one of those cases where you MUST select a QEMU CPU type.

NOTE:  If your VM won't boot it can usually be traced back to an improper CPU type.  Also, you will usually select 64 bit unless you have a 32 bit need.

When finished: Click Next 

![](images/00164.jpg)  

You will now need to configure memory.  The two modes are fixed and auto.  I tend to use auto the most because it shares memory and will NOT allow over-allocation.  I suggest running pfSense with the memory configuration as shown below.

NOTE:  It is possible to assign so much fixed memory that the Proxmox OS is deprived of memory resource!

To continue: Click Next 

![](images/00024.jpg)  

Next you will setup the network bridge.  We will set the pfSense LAN adapter to vmbr0\.  This is safe with a router because the only traffic passing through is internet, which is low bandwidth relative to the network adapters maximum capacity.  For adapter model select Intel E1000\.  I strongly recommend it!

NOTE:  Normally you will NOT want to use vmbr0 for VM's because it is the default adapter for the user interface!  You can use it!  Just try to avoid doing so unless the VM is low bandwidth.

To continue: Click Next 

![](images/00362.jpg)  

Finally you will confirm the configuration.

To continue: Click Finish 

![](images/00243.jpg)  

At this point you should be able to see your new VM configuration in the node tree as pictured below.  You can click the various tabs at the top for additional configuration options.  You can also edit individual items within the configuration by clicking on them and selecting edit

![](images/00196.jpg)  

Since your pfSense router only has one network adapter we will need to add another.  The new adapter is needed for your WAN(Internet) connection.  It is important  that you know the correct Mac/Hardware address for this to work.  If you followed the directions to this point you should have labeled the adapters making it easy to match the Mac/Hardware addresses by looking at the back of the machine.

Let's continue: Click Add >> Network Device 

![](images/00180.jpg)  

Now add a new network bridge(shown below).  For this example I have chosen vmbr1 but that can be changed very easily whenever you want.

![](images/00035.jpg)  

Now you will see your newly added adapter in the hardware list(pictured below).

MAC address NOTE: The hardware address you see is an alias and not the actual hardware address!  That's why you labeled them!

![](images/00095.jpg)  

Now let's double check the association between vmbr1 and eth1\.  We just want to make certain that vmbr1 doesn't point to eth4 instead.  To check the association go to the network tab in node view(pictured below).  You can clearly see associations between all the adapters.  We still don't know the real Mac address though!

![](images/00242.jpg)  

To find out which adapter to plug your internet into will require an additional step.  I know this may seem complicated but it's really not that bad once you wrap your head around it.  You will use a special Linux command called ifconfig.

# ifconfig eth1

Let's find that Mac now!

Open up your PuTTY program and login as root like you did when we setup the storage.

Now type the command below followed by the Enter key.

# ifconfig eth1

The results will show the actual Mac/Hardware address as picture below.

![](images/00015.jpg)  

Now that you have the real HW address you can match the labeled adapter and plug in your internet.

NOTE:  Because of this special Mac matching requirement for the WAN ports you won't be able to share these adapters with other VM's .  The solution is in planning which Proxmox servers will be used for router instances then add extra network adapters to only those machines.  That's a small price to pay for the ability to easily move your internet gateway.

It's also possible to use a small 5 port switch to allow offline migration of your routing gateway.  Just select another Proxmox server you want to use for a pfSense cold copy(off-state), repeat the address matching procedure on that machine, and plug into the 5 port switch along with your live pfSense and your incoming internet.

In summary:  your incoming internet connection plugs into the 5 port switch and each pfSense VM WAN port also plugs into that switch.  Please see [(Option-3) Easy Offline Router Migration](#index_split_006.html_filepos46754)  for more information.

DMZ and WAN2:  I don't suggest installing these extra adapters until after the initial pfSense installation is completed.  You will need at least one more virtual adapter for DMZ if following this complete guide.  When that time comes just refer back to this section and repeat the process for adding a new network adapter.

Now that your configuration is complete you need to know how to boot it.  Simply select the VM in the node tree and click the start button in the upper right hand corner.  Alternatively, if installing an OS you may wish to select the console so you can respond to prompts.  Just click the start option in the console(pictured below).  Once your VM starts up it will look like any other operating system booting.  To follow the install of pfSense click here: [Book 2: pfSense](#index_split_021.html_filepos107409) 

![](images/00348.jpg)  

1.10-VM Backup & Restore

Please take advantage of the following information as mentioned earlier in [.3-Best Practices](#index_split_006.html_filepos28974). 

Disaster Recovery Simplified

If any of your Proxmox servers go down the single most important item to recover will ALWAYS be your VM image backups.  Think of them as Master Recovery Images!   Without these you are lost so it is important to have as many copies as possible!

My preferred method is to select a NAS(virtualized or standalone) to use as my primary VM image backup server.  This server will host the NFS image backup share to Proxmox.  This share is manually replicated(only once during setup) to all other NAS servers in the system and synchronized on schedule using Rsync.

If a  machine goes down I can replace it, re-install Proxmox, re-install any NAS drives , re-map my NFS backups, and restore the VM images.  Once again, you're back running in 15 minutes or less!  This method has served me very well and is rock solid time tested!

NOTE:  There is a caveat!  If the NAS serving your VM image backups is virtualized such as [(Option-3) Easy Offline Router Migration](#index_split_006.html_filepos46754) it will not be able to backup its own VM image!  The simple work around for this is to create another NFS netbackups share on a different freeNAS node called netbackups2\.  Once again, we will use Rsync to automatically synchronize this dataset across all freeNAS nodes.  Please refer to the [.3.7-System Diagrams](#index_split_006.html_filepos39206) to gain more insight on system architecture and flow. 

KEEP A COPY ON THUMB-DRIVE:  Another highly recommended tip is to copy your VM image backups to a thumb-drive or DVD then store them in a fireproof safe.  You can easily map a read-only samba share of your VM image backups to be accessible from any windows machine or android phone.  Using the small footprint method described in [.3-Best Practices](#index_split_006.html_filepos28974) ensures your entire VM image backup archive will easily fit on a modern 64-128GB USB thumb-drive.

How To Backup Your VM

Proxmox provides you with a convenient backup interface.  Simply select the VM you wish to backup from the node tree view and click the Backup tab.  Choose your backup location at the far right followed by the Backup Now button(pictured below).

![](images/00295.jpg)  

You will then be presented with the backup dialog(pictured below).

Choose your options then click Backup.

![](images/00220.jpg)  

The progress dialog will appear showing the current status of the job(pictured below).  That's it!

![](images/00049.jpg) 

NOTE:  Image backups are NEVER enough.  You will still want to perform traditional backups from within the guest.  IMPORTANT:  I highly recommend that you do NOT try to backup VM image disks that are much larger than 80Gb or that use device pass-through(explained in ).

For example:  The freeNAS VM build covered in [Book 3: freeNAS](#index_split_033.html_filepos153134) with a 6TB pass-through storage drive should be configured using RSync and configuration backups from within the freeNAS guest.

I like to think of Proxmox image backups as a Master Recovery Image.  Your backup frequency should be very low from within Proxmox(maybe 1 backup every few months). 

How To Restore Your VM

To restore a VM select your backup location in the node view tree.  For this example I have selected NFS_netbackups(pictured below).  Once selected you should see the list of archives under the content tab.  Now, choose the archive that you wish to restore(shown below).

![](images/00271.jpg)  

Once you have selected an archive click on Restore(pictured below).

![](images/00229.jpg)  

You should now see the Restore VM dialog(pictured below) where you can assign a new VM ID and select the Storage location.

When finish click the Restore button(shown below).

![](images/00284.jpg)  

Once the process begins you will see the task viewer where you can watch the status of your restore(pictured below).

![](images/00099.jpg)  

1.11-VM Hardware

Network Adapters

At some point you may want to add or edit your VM hardware.  Proxmox offers a wide range of options including adding, editing, and removing both disk and network adapters.  It also allows for moving, throttling, and resizing of disks.  You already added a network adapter earlier in this chapter for use with the pfSense router configuration so the hardware tab should not be strange.  Once again, for reference to this hardware section we'll add a network adapter as pictured below.

Let's continue: Click Add >> Network Device 

![](images/00062.jpg)  

Now add a new network bridge(shown below).  For this example I have chosen vmbr1 but that can be changed very easily whenever you want.

![](images/00031.jpg)  

Now you will see your newly added adapter in the hardware list(pictured below).

MAC address NOTE: The hardware address you see is an alias and not the actual hardware address!

![](images/00250.jpg)  

You can change the Mac address, Model, or Bridge of any selected adapter simply by clicking the edit button under the hardware tab.  Figures (1-3) below show the edit network dialog.

fig.1.

![](images/00027.jpg)  

fig.2

![](images/00324.jpg)  

fig.3

![](images/00263.jpg)  

Hard Disk

Adding a new disk is equally simple.  Let's create a new 32Gb IDE drive for a Zentyal Domain Controller(shown below).  Click Add >> Hard Disk(pictured below)

![](images/00222.jpg)  

You will see the Add: Hard Disk dialog(pictured below).  Notice the default Bus is VIRTIO.  VIRTIO is a high performance driver but may not be compatible with your installation.  For the most compatible least troublesome Bus I recommend IDE.  Also notice the default Format is Qcow2\.  I ALWAYS use Raw format!  It is the highest performing and most compatible Format.  Also, stick with Cache default to avoid data loss!

![](images/00333.jpg)  

Figures (4-6) show the various dropdowns in the Hard Disk dialog.  Notice:  Incorrectly selected items will appear in red until the proper value is chosen.

fig.4

![](images/00262.jpg)  

fig.5

![](images/00023.jpg)  

fig.6

![](images/00266.jpg)  

Once added your new disk will appear red until the VM is power-cycled(pictured below).

> ![](images/00261.jpg)

1.12-Adding Pass-Through Disks

As mentioned in the [.3-Best Practices](#index_split_006.html_filepos28974) section, I use hybrid servers.  Essentially, you are creating a Proxmox virtualization host with a built in NAS server.  You install the NAS just like any other VM with its OS residing on a virtual disk.  However, the actual storage drives will reside on physical LVM storage assigned through a technique known as hardware pass-through.

This method allows for a very small backup footprint because your only backing up the NAS operating system and NOT the data.  It also provides moderately better disk throughput for data read/write cycles.  I have tested sustained throughput rates in the range of 30-60 Megabytes/sec using Gigabit adapters.  Bonding your adapters does yield better performance but I like to keep it simple!

The biggest advantage is that your data is NOT stored in a virtual disk file!  Even if you destroy the VM the data remains safe!

Now that you have an understanding let's add a 6TB striped volume to a new install of freeNAS.  As you can see the freeNAS install only has one 8GB IDE disk where the OS resides(pictured below).

![](images/00108.jpg)  

Let's open PuTTY and login as root on your Proxmox server.  Then we need to find our disks using the following command(pictured below):

# cat /proc/partitions

![](images/00109.jpg)  

As you can see, the largest disks(picture above) are /dev/sdb and /dev/sdc.

Also notice that there are /dev/sdb1 and /dev/sdc1 as well.  This indicates a single partition exists on each disk.  The partition sizes indicate that all available space is not being used.  We need to change that!  To edit /dev/sdb type the following command:

# fdisk /dev/sdb

You will now see something like this(pictured below):

![](images/00158.jpg)  

Now press: m >> Enter 

You will see the help screen(shown below).  We are interested in an creating empty DOS partition table.

![](images/00219.jpg)  

Now press: o >> Enter 

Followed by: w >> Enter 

This series of commands will create a new empty DOS partition table and write changes to disk.

Next we need to repeat these steps for /dev/sdc.  Do NOT worry about the lack of partitions!  The beauty of this method is that LVM doesn't care!

Let's verify our disks again to ensure the partitions are gone using the following command:

# cat /proc/partitions

![](images/00240.jpg)  

As you can see(above), /dev/sdb and /dev/sdc can now be used to full capacity.

We will now create LVM physical volumes(PV's) using the following commands:

# pvcreate /dev/sdb

# pvcreate /dev/sdc

OR

# pvcreate /dev/sd[b,c]

![](images/00226.jpg)  

The output above shows successful creation.

Next, we will create a volume group(VG) containing both disks with the following command:

# vgcreate freenas4 /dev/sd[b,c]

![](images/00360.jpg)  

The output above shows our VG created successfully.

For the final step we will create a striped logical volume(LV) using all available space.  LVM Striping is equivalent to RAID-0 for maximum disk throughput.

Type the following command to create the stripe:

# lvcreate -l 100%FREE -i2 -n 6tbstore freenas4

where: i2(number of stripe members), n(name)

![](images/00089.jpg)  

The above output shows our LV stripe successfully created.

As I mentioned earlier, Linux LVM is extremely powerful and flexible.  I would highly recommend learning it well.  Below are 3 more very useful LVM commands:

# pvscan

This command lists ALL known physical volumes(pictured below).

![](images/00087.jpg)  

# vgscan

This command lists ALL known volume groups(pictured below).

![](images/00073.jpg)  

# lvscan

This command lists ALL known logical volumes(pictured below).

![](images/00224.jpg)  

You can see the newly created 6TB striped volume above.  Now we're ready to assign this volume to the freeNAS-4 VM.  You will notice the ID number of freeNAS-4 is 800 and IDE1 or IDE3 is available(pictured below).

![](images/00108.jpg)  

To assign the new disk we will issue the special QEMU command as follows:

# qm set 800 -ide1 /dev/freenas4/6tbstore

The command entered into PuTTY looks like this(pictured below).

![](images/00132.jpg)  

The result of this command is evident by the new IDE1 drive shown in the freeNAS-4 hardware window(pictured below).  NOTE:  You will need to refresh the tab page before the new disk will appear.

![](images/00111.jpg)  

The freeNAS-4 VM(above) could now be booted and the new 6TB disk configured as a ZFS stripe.

PLEASE REMEMBER:  It is important to note that freeNAS-4 is now tied to the Proxmox3 server by its hardware pass-through disk.  It cannot be moved to another physical machine unless the physical disks are removed.  The other VM's(pictured above) can be moved to another physical machine easily using a simple backup/restore.  They are NOT tied in any way to the Proxmox3 server.

1.13-Troubleshooting Proxmox

Troubleshooting Proxmox is easy!  There isn't any!  You may occasionally have a VM locked.  Simply issue the following command:

# qm unlock [vm-ID]

Example:  # qm unlock 800

where 800 is the vm- ID number(pictured above) in node tree view

You may also have a new VM configuration fail to boot.  Changing the CPU type from KVM to QEMU or from QEMU to KVM usually works.

Finally:  Some operating systems may require you to partition and format the VM disk before they will boot.

1.14-Upgrading Proxmox

When it comes to updates and upgrades to Proxmox I have found the KISS(keep it simple stupid) method works the best.  DO NOT under ANY circumstance try to update or upgrade a perfectly functional install!  Linux is not like Windows!  When things go wrong they tend to go wrong in a VERY bad way!

There are ways of updating using apt and aptitude commands but I DO NOT recommend this and it would take a whole chapter just to cover.  You will spend less time if you simply backup your VM's, restore them to different nodes, then re-install the Proxmox node in question with the latest distribution release. 

With the DVD it takes 10-15 minutes to install and configure!  Through command line upgrade it can take 45-60 minutes IF everything goes right!  That's a BIG IF!  When you're the only IT Administrator with 200 machines/users to babysit you tend to avoid the IF scenarios and go with the sure shot every time! 

Book 2:  pfSense

2.1-Introduction To pfSense

About 1 year after placing Proxmox in production at work I got a call.  I was told that one client decided to change encryption on our VPN tunnel to something more secure.  I soon realized that our existing equipment could NOT be upgraded so I began searching for alternatives.  That's when I decided on pfSense!

My first install was bare metal and worked just fine.  It wasn't long before I began pondering the idea of a virtualized routing platform.  The great debate was whether virtualized routers were up to the task from a security standpoint.  I just couldn't let the idea rest unless I tried it!  Well, I must say, that 7 years later I'm glad I decided to virtualize.

The security question was soon put to the test after experiencing some issues with an ATT gateway.  I ended up spending the whole day on the phone with ATT starting at level-1 and eventually making it to TOP level-6 support.  This is where the network engineers spend their days!  To make a long story short, ATT Network Engineers could NOT test my gateways without pfSense being disabled.

Over the years Snort IDS running on pfSense has caught numerous offenders and killed the connections immediately.  Whenever I install new software it's packet sniffed with Wireshark before ever going into production!  Furthermore, network monitors such as Nagios Core provide a wealth of information to keep IT Administrators informed.  With proper firewall rules and Layer-2 hardware filtering it is EXTREMELY unlikely that you will be hacked!

NOTE:  pfSense is a powerful platform and it's feature-set cannot be completely covered in this book.  This guide was designed as a step-by-step to get you up and running quickly.  I highly recommend tapping the wealth of online resources available for a more thorough understanding.

Ok!  Enough said!  Before installation can begin you must create the VM configuration.  I recommend a 8Gb IDE virtual disk with 4Gb of Ram for this install.  If you need to review those steps again click here: [1.9-Creating VM Configuration](#index_split_015.html_filepos77013) 

2.2-Installing pfSense

Now, power on the pfSense VM making sure that you have the CD or disk image loaded.

You should see the following screens:

![](images/00359.jpg)  

Now, when you see the prompt(shown below) press the (I) key.  If you don't catch it in time just reset the VM.

![](images/00013.jpg)  

Next you will see the configuration console(pictured below).  Use your arrow down to Accept These Settings followed by the Enter key.

![](images/00300.jpg)  

Now, choose the Quick/Easy Install (pictured below)

![](images/00065.jpg)  

Hit OK (pictured below)

![](images/00270.jpg)  

You will want to select the Standard Kernel (pictured below) for our install.

![](images/00010.jpg)  

Next, select Reboot (pictured below).

![](images/00016.jpg)  

When the system reboots you will notice the DEFAULT credentials are:

Username: admin 

Password: pfsense 

![](images/00265.jpg)  

2.3-Assigning Network Interfaces

Next, you will setup the network!  Since pfSense is a BSD based distribution your network interfaces are named differently.  If you have used e1000 Gigabit they will show up as em(x).  If you have used Realtek adapters they will be named re(x).  Please pay close attention now!  This is the only tricky part to the install!

Notice in the picture below that em1 has been assigned an IP Address and is defaulted to the LAN interface.  This is NOT correct!  The ONLY possible way a DHCP address could have been assigned is if the em1 interface (pictured below) was actually connected to the Internet Router.  We need to flip these interfaces around so the LAN becomes em0.

NOTE:  I find it easiest to ALWAYS set the LAN to the first interface which is ALWAYS going to be em0 or re0.

To assign em0 to the LAN select option 1 then press ENTER 

![](images/00326.jpg)  

You will see the following prompt(pictured below).  Type n for NO then press  ENTER.  We do NOT want VLAN.  Also notice the interface mac addresses.  These should match those in your Proxmox vm configuration.

![](images/00367.jpg)  

Next, you will be prompted for the WAN interface name.  Type em1 then press ENTER.

![](images/00171.jpg)  

pfSense will now ask for the LAN interface name(pictured below).  Type em0 then press ENTER.

![](images/00245.jpg)  

Since we will NOT setup an optional  interface(opt1) right now simply press the ENTER key which indicates NO SELECTION(pictured below).

![](images/00223.jpg)  

Your interfaces will now be assigned(shown below).  Type y then press ENTER.

![](images/00225.jpg)  

2.3-Assigning IP Addresses

Now you will need to set the IP address of the LAN adapter  This will be the address the web interface runs on.  It will also serve as the default gateway and DNS server on your local network.  NOTE:  I prefer to set this address as the last in the subnet(x.x.x.254).

To proceed:  select option 2 then press ENTER 

![](images/00117.jpg)  

Next, type the number of the interface you wish to configure.  In our case we want the LAN adapter which is number 2 in the list(pictured below).

To proceed:  Type 2 then press ENTER 

![](images/00317.jpg)  

You will now be prompted for the new LAN IPv4 address.  For the purpose of the tutorial I have used 192.168.0.254(pictured below).

To proceed:  Type the LAN IP you will use then press ENTER 

![](images/00144.jpg)  

Next you will be asked to provide a Subnet mask bit count in CIDR notation.  This will almost ALWAYS be 24 for a local network.

To proceed:  Type 24 then press ENTER 

![](images/00177.jpg)  

The next few prompts can be skipped by pressing ENTER which indicates NO SELECTION(pictured below).

To proceed:  press ENTER 

![](images/00318.jpg)  

You will NOT need IPv6 configured(pictured below) on your LAN so this step can be skipped.

To proceed:  press ENTER 

![](images/00082.jpg)  

To make the console configuration as simple as possible we will NOT enable DHCP on the LAN at this time(pictured below).  That will be setup using the web interface.

To proceed:  Type n then press ENTER 

![](images/00267.jpg)  

You will now be prompted to revert the web interface(pictured below) from secure(https) to non-secure(http).  You may wish to leave it set to secure.

To proceed:  Type n then press ENTER 

![](images/00351.jpg)  

The configuration should now be complete.

To proceed:  press ENTER 

![](images/00003.jpg)  

2.4-Reset Admin Password

At some point you may wish to default the Admin credentials.  The menu option is number 3(pictured below).

![](images/00078.jpg)  

If you select option 3 and press y indicating YES the credentials will be reset.  The defaults  are:

Username: admin 

Password: pfsense 

![](images/00075.jpg)  

2.5-Web Configuration Wizard

You are now ready to open your web browser to the LAN address you just set(https://192.168.0.254) for a first login.  For the purpose of this tutorial I have used Mozilla Firefox.

To continue(pictured below): click I Understand the Risks 

![](images/00257.jpg)  

Next(pictured below):  click Add Exception 

![](images/00178.jpg)  

Now(pictured below):  click Confirm Security Exception 

![](images/00228.jpg)  

To proceed:  login(pictured below) using the default password: pfsense

![](images/00256.jpg)  

Once logged in the wizard will start(pictured below).  Simply follow the prompts.

To proceed: click Next 

![](images/00160.jpg)  

pfSense now offers Gold Subscription signup(pictured below).  This is NOT required in any way to use the software.

To proceed:  click Next 

![](images/00110.jpg)  

You will now be prompted to enter some basic information about your router(pictured below).  To specify a .com domain other than localdomain or YOURWEBS you MUST have a registrar such as Go Daddy.

For example:  I have a registered YOURWEBS.US domain so I can enter that below.  If I didn't have that domain registered I could still use YOURWEBS leaving off the .US suffix.  This will work just fine with my local Zentyal domain controller install.  Regardless what name you choose, the domain entry should match that of the Zentyal controller we'll be setting up later in the book.  My preference here is to register a domain that will NOT be used by the public but that still resolves to my WAN IP address.

You may also wish to use Google DNS servers(8.8.8.8 and 8.8.4.4) as alternates instead of your ISP.  This option can sometimes solve name resolution issues.

To proceed:  click Next 

![](images/00048.jpg)  

Now enter your Time server(recommend default) and Timezone information(pictured below).

To proceed:  click Next 

![](images/00119.jpg)  

Since the WAN was already configured earlier this is redundant.  It should almost ALWAYS be configured for DHCP (pictured below) with most ISP's today.

![](images/00057.jpg)  

Scrolling down to the bottom of the screen reveals the following options(pictured below).  You want both of these checked for WAN interfaces.

To proceed:  click Next 

![](images/00182.jpg)  

Since we have already configured the LAN interface this step is again redundant.  The values(pictured below) should match those you entered during the console stage of installation.

To proceed:  click Next 

![](images/00170.jpg)  

Next you will change the default Admin Password(pictured below) to a more secure one(make sure to do this).

To proceed:  click Next 

![](images/00090.jpg)  

Now, pfSense will reload the configuration changes(pictured below).

To proceed:  click Reload 

![](images/00086.jpg)  

Congratulations!  You are done with the initial setup.

To proceed:  click the here link as pictured below 

![](images/00185.jpg)  

2.6-Changing Themes

The default theme and dashboard will look something like the picture shown below.  Notice that everything is left justified.  My preference is to change this to center justified for easier navigation and mobile phone compatibility.

![](images/00116.jpg)  

Let's change the default theme to NERVECENTER by selecting System>General Setup as shown below.

![](images/00008.jpg)  

Now scroll to the bottom and select the NERVCENTER theme from the dropdown list(pictured below).  Don't forget to save the changes!

![](images/00323.jpg)  

Your new NERVCENTER theme should look something like this(pictured below).

![](images/00115.jpg)  

2.7-Configure DHCP Server

The next step is to enable the DHCP server on the LAN.  This will assign IP addresses to any machine connected locally.

To proceed:  click Services>DHCP Server  as pictured below.

![](images/00025.jpg)  

You should see the following window(shown below).  Check the box:  Enable DHCP server on LAN interface 

![](images/00315.jpg)  

Once the service box is checked you will need to set a range(pictured below).  My preference is to use a range (x.x.x.100-x.x.x.200).  This allows for static reservation addressing before and after the range which is very useful.  Also notice the Deny unknown clients switch(pictured below).  I prefer to keep this unchecked until all entries are added to the system.  Once everything is verified and working you can check this box and save changes.  This will prevent unauthorized hardware from obtaining addresses on your system(very useful and highly recommended).

![](images/00347.jpg)  

2.7.1-WINS, DNS, Gateway, and Domain

When a client connects to the DHCP server it receives all the information from the following entries.  In this example we will be installing Zentyal to act as a directory server for the YOURWEBS.US domain.  The WINS servers entries below are the addresses of ZentyalDC1 and ZentyalDC2 respectively.  The DNS and Gateway entries are the pfSense LAN interface IP.

![](images/00290.jpg)  

The picture below shows another security switch that I prefer to keep turned off until everything is verified to be working.  By Enabling Static ARP Entries pfSense will prevent ANY hardware NOT listed from communicating with the LAN adapter.  This is yet another powerful tool to help keep your network secure(strongly recommended)!

![](images/00190.jpg)  

2.7.2-DHCP Client Reservations

If you scroll to the bottom of the page you will see the Static mappings table.  The one pictured below is pre-populated to give you an idea what the table will look like after making a few entries.  I strongly recommend entering EVERY hardware address in your network here with full descriptions(as shown below).  Not only is it necessary if you wish to enable static ARP entries(shown above), but it comes in handy if you need to quickly look up the IP address of any machine on your network.

To make an entry:  click the + button on the right side(shown below).

![](images/00344.jpg)  

Next you should see the DHCP entry form(shown below).  I have included a sample entry for reference(shown below).  After making an entry be sure to save your changes.  NOTE:  There is really NO need to make WINS, DNS, Gateway, or any other entries here.  By default the pfSense interface IP will control ALL clients automatically.

![](images/00194.jpg)  

2.8-Firewall Settings

The last thing you'll need to do is setup a couple firewall rules.  We will allow ALL traffic between LAN clients and allow ALL LAN clients out on the WAN.  First we'll add the LAN to LAN rule.

To proceed:  click Firewall>Rules as shown below

![](images/00143.jpg)  

2.8.1-LAN Rules

You should see tabs with the names of your network interfaces.  Some of my tabs(pictured below) have different names.  I have simply renamed them!  For Example:  I have renamed my WAN interface to JAB.  The only interfaces we're going to concern with for this book are LAN and WAN.  The list pictured below is pre-populated to give you an idea what the table will look like after making our LAN Rule entry.

![](images/00246.jpg)  

To add our new LAN to LAN rule click the + button on the right side(pictured below).

![](images/00080.jpg)  

The picture below shows the completed LAN to LAN rule.  Duplicate this rule remembering to save the changes when finished.

![](images/00235.jpg)  

2.8.2-WAN Rules

Next we'll setup a rule allowing all LAN outbound on the WAN.  Remember, I have renamed my WAN interface to JAB(pictured below)!  The entry on your system will be made under the WAN tab.  The list pictured below is pre-populated to give you an idea what the table will look like after making our WAN Rule entry.

![](images/00325.jpg)  

To add our new LAN to ANY rule click the + button on the right side(pictured below).

![](images/00329.jpg)  

The picture below shows the completed LAN to ANY rule on the WAN interface.  Duplicate this rule remembering to save the changes when finished.

![](images/00342.jpg)  

2.9-OpenVPN

VPN is a tunneling protocol which allows secure remote access to your system.  Once connected to the VPN tunnel clients can work as though they were onsite.  In order for VPN to work you must have a static IP address and all remote machines must have a client connector installed.  Configuring VPN manually can be quite challenging, even to professionals, but the pfSense developers have included a fantastic wizard to get you up and running with minimal effort.  NOTE:  even with the wizard this will be a lengthy chapter so better get your coffee and pay close attention!  Let's get started!

2.9.1-OpenVPN Client Export Utility

To begin:  click System>Packages(shown below).

![](images/00156.jpg)  

If you do not see OpenVPN Client Export Utility under Installed Packages download and install it under the Available Packages tab(pictured below).

![](images/00251.jpg)  

2.9.2-OpenVPN Setup Wizard

Once the OpenVPN Client Export Utility is installed go to the main dashboard screen then click VPN>OpenVPN(pictured below).

![](images/00146.jpg)  

Next, click the Wizards tab(pictured below).

![](images/00030.jpg)  

For now, select Local User Access from the dropdown then click the Next button(shown below).

![](images/00021.jpg)  

You will now need to establish a Certificate Authority (CA).  Complete the form as shown below then click Add new CA.

![](images/00054.jpg)  

Next, you will need to create a New Server Certificate.  Keep the Key length at 1024 bits for best results.  When finished click Create new Certificate(pictured below).

![](images/00181.jpg)  

In the General Information section below I have left Protocol and Port values at default.  The Interface should normally be WAN but I have renamed mine to JAB in this server.  This helps for identification purposes when you have several WAN connections all hosting VPN tunnels.

![](images/00274.jpg)  

The Cryptographic Settings(shown below) should also be left at default unless you know what you are doing.

![](images/00208.jpg)  

For Tunnel Settings(shown below) I have allowed 1 client in the 10.10.10.0/24 Tunnel Network.  This client will have access to the 192.168.0.0/24 Local Network.

![](images/00221.jpg)  

In Client Settings(pictured below) I have allowed Dynamic IP and Address Pool.  I have also assigned the pfSense IP address as the DNS Server and supplied YOURWEBS.US as a Default Domain.  When finished click Next(shown below).

![](images/00334.jpg)  

The wizard will now setup firewall rules.  To proceed:  click Next(shown below).

![](images/00101.jpg)  

The wizard is now done configuring you VPN.  To proceed:  click Next(shown below).

![](images/00211.jpg)  

When finished you will see your server configuration as shown below.

![](images/00238.jpg)  

2.9.3-OpenVPN Client Connectors

The client export connectors MUST be installed in order for any client to connect to your new VPN server.  You should be able to use the default settings(pictured below) for your connector packages.

![](images/00309.jpg)  

At the bottom of the page you will find hyperlinks for all the Client Install Packages in the Exports column on the right(shown below).  Simply click the link for the package you wish to download.

![](images/00163.jpg)  

When the download dialog appears(pictured below) save the file to disk for installation on your client machines.  Please Note:  When installing connectors on Windows clients make sure to run the setup as Administrator!

![](images/00302.jpg)  

2.9.4-Authenticate Zentyal Domain Users

Now that we have a VPN server let's configure it so Domain users can authenticate and use it!  To do this you first need to have Zentyal installed as covered in [Book 4: Zentyal Domain Controller](#index_split_054.html_filepos220923) 

With Zentyal installed let's proceed by clicking System>User Manager(shown below).

![](images/00272.jpg)  

Next, click the Servers tab(shown below).  Notice:  the list below is already pre-populated with ZentyalDC1 for your reference.  Your installation should only show the Local Database at this point.

To add a new server click the + Button(shown below).

![](images/00337.jpg)  

Next, you will need to enter your Zentyal Domain Controller information(shown below).  NOTICE:  The Base DN syntax must be entered exactly.  If your domain is xyz.com then the Base DN should be DC=xyz,DC=com or it will NOT work.  This information can also be found in the Zentyal management interface under Users and Computers>LDAP Settings.  Also, notice I have selected Microsoft AD as the Initial Template(pictured below).  When finished click Save.

![](images/00278.jpg)  

Now we'll test the new Authentication Server.  Select the server under the Settings tab the click Save and Test(shown below).

![](images/00310.jpg)  

The test should run successfully as shown below.  If not, re-check your settings and try again.  When finished click Close(pictured below).

![](images/00064.jpg)  

To maintain the highest level of security we only want Zentyal Authenticating VPN Users.  Make sure to change Authentication Server back to Local Database after the test(shown below).

![](images/00308.jpg)  

The final step is to enable the Zentyal server as a Backend for authentication in the OpenVPN server.  To do this click VPN>OpenVPN then edit the server making sure the new Zentyal Server is highlighted as shown below.  When finished don't forget to save the changes!

![](images/00268.jpg)  

2.10-Snort IDS

A critical component of any modern business network is intrusion detection or IDS.  When it comes to IDS Snort is the most popular package used today!  The concept behind IDS is to monitor transmission protocols for uncharacteristic behavior and then kill the connection when this behavior is detected.  This is precisely the way Antivirus and Malware providers find new threats and create updates to counter those threats.

Most IDS systems are setup to monitor external connections by default.  My recommendation is to monitor your internal connections instead.  This method catches malicious code that can be brought in through portable devices such as smart-phones and USB thumb drives.

NOTE:  Snort can be rather complicated to setup for those unfamiliar with it.  This will be a quick run-through do to the many configuration options, so please make sure to duplicate my settings exactly!  Let's get Snort working now!

2.10.1-Install Snort Package

To begin:  click System>Packages(shown below).

![](images/00156.jpg)  

If you do not see Snort under Installed Packages download and install it under the Available Packages tab(pictured below).

![](images/00251.jpg)  

Once the package is installed click Services>Snort(pictured below).

![](images/00135.jpg)  

2.10.2-Snort Global Settings

Under the Global Settings tab(shown below) make sure ONLY Emerging Threats is checked.  Duplicate all other settings.

![](images/00291.jpg)  

2.10.3-Snort Interfaces

Under the Snort Interfaces tab add an interface by clicking the + button(shown below).  Notice:  I have included a  pre-populated interface for reference.

![](images/00298.jpg)  

For this example we will add the LAN interface(shown below), which will catch alerts caused by infected USB thumb drives and smart-phones.

![](images/00275.jpg)  

For Alert Settings duplicate my options for normal operation.  IMPORTANT:  during initial learning you will want to UNCHECK Block Offenders.  This is only temporary until you have monitored normal traffic and added any false alerts to the suppression list.

![](images/00046.jpg)  

For Detection Performance Settings duplicate my settings(shown below).

![](images/00303.jpg)  

Leave all whitelist settings at default(shown below).

![](images/00183.jpg)  

The suppression filter(shown below) will be auto-generated after initial monitoring and adding of the first suppression entry.

![](images/00042.jpg)  

Now that you are finished setting up the LAN interface click Save(shown below).

![](images/00312.jpg)  

2.10.4-Updating Threat Rules

Under the Updates tab(shown below) simply click the Update button in the middle of the page.

![](images/00234.jpg)  

2.10.5-Threat Rule Categories

Threat rule categories are specific to the selected interface.  Since we have configured the LAN interface for monitoring you must edit that specific interface by clicking the edit(e) button on the right under the Snort Interfaces tab.  Next, click the LAN Categories tab and select ONLY the rules shown below.  Selecting other rules will FLOOD you with unnecessary alerts and should only be experimented with after you become familiar with Snort.

![](images/00260.jpg)  

![](images/00149.jpg)  

![](images/00155.jpg)  

![](images/00365.jpg)  

2.10.6-Add Alerts To Suppression List

Once snort is running you WILL start seeing alerts as seen in the list below.  You can add low-risk alerts to the suppression list by clicking the plus(+) button in the SID column(shown below).  HINT:  Use common sense when building your suppression list!

![](images/00288.jpg)  

Once you have suppressed any alert the suppression list should be auto-generated as shown below.

![](images/00313.jpg)  

2.10.7-Block Offenders At Source

Once you have monitored your normal network traffic and established a suppression list it's time to let Snort work.  You can now go back to the Snort Interface settings and enable offenders to be blocked at the source.  Remember, this is the option I recommended you leave unchecked until you had a chance to monitor traffic.

IMPORTANT:  Snort is very powerful and it WILL block traffic!  It may even block You!  If this happens login to pfSense from another computer, temporarily disable blocking, and make sure to run a virus or malware scan on the blocked machine just to be safe!  When setup and used properly this system ROCKS!

![](images/00282.jpg)  

2.11-Configuration Backups

Besides using VM image backups it is also wise to keep a copy of the pfSense configuration.  The configuration backup is especially important when developers rewrite the build in a way that breaks certain packages on update.  In these instances your VM image backup will only get you back to the version you were using.  I have had this happen only 1 time in the last 7 years, so don't worry too much!

To access the configuration backup page:  click Diagnostics>Backup/Restore(pictured below).

![](images/00145.jpg) 

You should see the Backup/Restore dialog as shown below.  Now, click the Download configuration button.

![](images/00314.jpg)  

When the download dialog appears(shown below) save your configuration to disk.  HINT:  I like to keep a copy of this on thumb drive!

![](images/00004.jpg)  

Restoring your pfSense should be self-explanatory!  Simply use the Restore configuration option instead!

Book 3:  freeNAS

3.1-Traditional Storage Fails

For years I relied on traditional storage servers usually configured with either RAID(1, 5, 6, or 10).  My preferred file system was XFS because it was cutting edge and relatively trouble free.  The problem was that a file server consumes the entire hardware resource of that machine even when there is no demand.  Furthermore, you need multiple machines dedicated to storage in order to maintain data redundancy.

Another observation was that RAID is NOT perfect!  If you select hardware RAID and the controller dies have fun getting the system back up in a timely manner!  If you select software RAID and the file system degrades you'll take a huge performance hit while it rebuilds.

Large arrays can easily take 24hrs to complete this process.  During this time the IT Department gets flooded with calls about poor system performance!  To make matters worse, the automatic backup starts running it's nightly incremental causing performance to plummet!  There had to be a better way!

What Makes A Good Storage System

How do you define a good storage system?  First, I asked myself what was MOST important?  Well, that's not easy to answer after being in the field and experiencing problems!  There are several key elements involved!

For me, they are:

*   > > The data storage platform MUST be reliable and compatible for years

*   > > Complete system disaster recovery MUST be simple and fast

*   > > The storage input/output MUST be fast

*   > > Daily end-users restore requests must be simple and fast

*   > > Data MUST be redundantly stored

*   > > Data corruption MUST be minimized

If I cannot meet ALL of these expectations then the storage platform choice is wrong!  According to these needs traditional RAID(1, 5, 6, or 10) storage simply could not work!  This requires an explanation!

Duty Cycles

When engineers design electronic components they commonly provide a Duty Cycle Rating.  This special rating helps determine how long a component can perform under load before heat buildup starts irreversibly degrading components.  Now, let's apply this concept to a hard disk array!

When a parity array such as RAID(1, 5, 6, or 10) is written to it must synchronize the data cache without interruption or it WILL degrade.  If it degrades, it WILL rebuild!  If it rebuilds, it introduces extended duty cycle and heat buildup.  This heat buildup irreversibly degrades components leading to eventual failure.

A striping array such as RAID-0 never synchronizes or degrades.  This reduces duty cycle and heat buildup thus increasing component life.  It also provides increased throughput as a bonus!

Simplicity & Redundancy

RAID-0(striping array) fits the performance demand perfectly.  It can NEVER degrade!  It either works or it doesn't!  What about simplicity and redundancy?

So here's the magic!  We build our system using ONLY non-parity striping arrays then use RSync to replicate the data over several NAS machines.  This gives the performance of RAID-0 while maintaining data redundancy.

This method provides data input/output rates that beat ANY RAID-10 storage.  Furthermore, when virtualized, ALL platform compatibility issues for on the fly upgrades are gone.  Best of all, Linux LVM provides a simple method of creating UUID serialized stripe volumes.  This means bullet-proof booting and easy physical migrations to other machines.

It seems that all the requirements are satisfied except end-user restore requests and minimizing data corruption.  Waite, there's freeNAS with ZFS!

3.2-freeNAS & ZFS

The final requirements are satisfied with the addition of the self-healing ZFS file system.  The best purpose built distribution for this is freeNAS.  When setup according to this book you can expect very respectable performance when compared to bare metal file servers.  freeNAS is very complete with active directory integration, snapshot backups, and a super built-in RSync script for hands free duplication across nodes.  Let's get on with the installation!

NOTE:  freeNAS is a powerful platform and it's feature-set cannot be completely covered in this book.  This guide was designed as a step-by-step to get you up and running quickly.  I highly recommend tapping the wealth of online resources available for a more thorough understanding.

3.3-Installing freeNAS

Before installation can begin you must create the VM configuration.  I recommend a 8Gb IDE virtual disk with 8Gb of Ram for this install.  If you need to review those steps again click here: [1.9-Creating VM Configuration](#index_split_015.html_filepos77013) 

Now, power on the freeNAS VM making sure that you have the CD or disk image loaded.  For this book I have used freeNAS version 9.2.1.5-RELEASE -x64.iso.  If you do not have freeNAS you can download the latest release here:  [http://www.freenas.org/download-freenas-release.html](http://www.freenas.org/download-freenas-release.html) 

NOTE:  The download section also allows you to choose other releases toward the bottom of the page.  I would recommend using the exact version I have used for this book!  It has proven VERY reliable and if it's NOT BROKEN don't try to fix it!

Once powered up you should see the following screens:

To proceed:  press ENTER (indicating OK)

![](images/00098.jpg)  

Next, you will be prompted for the installation hard disk(pictured below).  Since we only have one disk this is easy!

To proceed:  press ENTER (indicating OK)

![](images/00363.jpg)  

freeNAS is now ready to begin the install(pictured below).

To proceed:  press ENTER (indicating Yes)

![](images/00047.jpg)  

When the install is completed you will be prompted to remove the CD and reboot(pictured below).

To proceed:  press ENTER (indicating OK)

![](images/00350.jpg)  

In order to remove the CD you will need to select list item 4-shutdown(pictured below).

To proceed:  press ENTER (indicating OK)

![](images/00366.jpg)  

Now you can close the console and go to the VM hardware tab(pictured below).  Select the CD then click Edit 

![](images/00305.jpg)  

To prevent the freeNAS VM from using the CD drive again simply check Do not use any media(pictured below).

To proceed:  click OK 

![](images/00165.jpg)  

Next, you need to copy the network interface Mac\hardware address(highlighted below) so that it can be entered into the pfSense router, which should already be installed.

![](images/00354.jpg)  

Now, open your pfSense web management interface and make the appropriate entry in the DHCP static mappings(pictured below).  Don't forget to save your changes.

![](images/00322.jpg)  

3.4-Add freeNAS Pass-Through Disks

At this point there is no storage drive for freeNAS to use for shares.  We will now add the LVM striped volume that was created in Chapter 1.12 as a pass-through hard disk.  You may wish to revisit that chapter!   

To begin, open the PuTTY program and login as root on your Proxmox server(pictured below).

![](images/00192.jpg)  

To assign the new disk we will issue the special QEMU command as follows:

# qm set 800 -ide1 /dev/freenas4/6tbstore

The command entered into PuTTY looks like this(pictured below).

![](images/00356.jpg)  

The result of this command is evident by the new IDE1 drive shown in the freeNAS-4 hardware window(pictured below).  NOTE:  You will need to refresh the tab page before the new disk will appear.

![](images/00200.jpg)  

3.5-Set Storage For No Backup

IMPORTANT:  It is extremely important that we ONLY backup the freeNAS primary disk(ide0) and NOT the 6TB storage drive.  If this were to happen it would seriously degrade your system performance!  Your backups should be configured using RSync from within the freeNAS guest.  This behavior can easily be avoided by editing the disk properties as shown below.

![](images/00055.jpg) 

Notice the disk properties(pictured below) indicate that secondary disk(ide1) will NOT be included in backups.

![](images/00052.jpg) 

The freeNAS-4 VM(above) can now be booted and the new 6TB disk configured as a ZFS stripe.

PLEASE REMEMBER:  It is important to note that freeNAS-4 is now tied to the Proxmox3 server by its hardware pass-through disk.  It cannot be moved to another physical machine unless the physical disks are removed.

3.6-Start freeNAS Through The Console

Now, start your new freeNAS VM by opening the Proxmox console in the upper right hand corner.  When the console appears click the Start Button(pictured below).

![](images/00195.jpg)  

We are only using the console window startup to ensure the VM starts properly and is assigned the appropriate IP address through DHCP.  Notice the bottom of the console display indicates our web interface address to be http://192.168.0.22 

![](images/00189.jpg)  

3.7-Initial Login

Now, you can open the web browser and enter the address of the freeNAS VM.  I use and recommend Mozilla Firefox.

The first screen you see will be the root user password change dialog(shown below).  Make your password strong!

![](images/00051.jpg)  

Once the password is set you should see the full web management interface(pictured below).

![](images/00287.jpg)  

3.8-freeNAS Navigation

Navigation is pretty straight forward!  You will find a series of tabs at the top of the main screen.  There is also a tree in the left column(pictured below).

![](images/00187.jpg)  

3.9-Network Configuration

During installation freeNAS defaults to accept DHCP with its hostname set to freenas.  DHCP is NOT desired when you run servers of any kind.  Furthermore, with multiple freenas machines running on your network they cannot all have the same name!  Let's change that now!

Under the Network>Global Configuration tab(pictured below) you can change your Hostname, Domain, Gateway, and Nameserver information.  In this case I have set the Gateway and Nameserver to the IP address of the pfSense Router running on Proxmox.  Don't forget to save your changes!

![](images/00096.jpg)  

Now, let's click on the Network Summary (shown below) tab to verify our network interface name and address.  This will be needed to setup a static address mapping.

![](images/00097.jpg)  

Next, click Interfaces>Add Interface(pictured below).

![](images/00041.jpg)  

When the interface dialog appears(shown below) enter the appropriate Interface Name and IP Address.  The Netmask will almost ALWAYS be (255.255.255.0).  This is the most commonly used Netmask for home or business reservation ranges.

![](images/00269.jpg)  

When finished you should see the new entry listed under Interfaces(shown below).

![](images/00292.jpg)  

3.10-Users And Groups

3.10.1-Adding A New User

If you do not have a domain running locally you will need to add users to your server or servers.  At the far right of the main interface you will find the Account button(pictured below).

To proceed:  click Account 

![](images/00159.jpg)  

You should then see the default Users and Groups page.  You can easily navigate using the tabs at the top of the page.

To add a member:  click Add User(shown below)

![](images/00161.jpg)  

The Add User dialog should then appear(shown below).  Enter the new User information as required.  I have included sample data for reference.

![](images/00071.jpg)  

At the bottom of the entry form there is a section allowing you to choose Auxiliary groups for the new user.  Let's add John Smith to the ftp group!  To do so simply double click the appropriate group from the Available column(pictured below).

![](images/00280.jpg)  

3.10.2-Adding A New Group

To add a new group is equally simple.

To add a member:  click Add Group(shown below)

![](images/00127.jpg)  

The Add Group dialog should then appear(shown below).  Enter the new Group information as required.

![](images/00248.jpg)  

3.11-Add A ZFS Volume

The freeNAS web interface makes it quite easy to add storage.  To access the Volume Manager make sure you are working under the Storage tab at the top of the screen(pictured below).

To proceed: click ZFS Volume Manager 

![](images/00276.jpg)  

To add your new volume, type a unique name, then select the available disk(pictured below). 

To proceed: click Add Volume 

![](images/00197.jpg)  

The new volume should then appear as active(shown below).

![](images/00107.jpg)  

3.12-Detach And Move Volumes

If for some reason you need to move the freeNAS VM to another physical Proxmox machine the best method is to detach the volume cleanly.  At the bottom of the page you will see a set of control buttons(pictured below).

To proceed:  click Detach Volume 

![](images/00121.jpg)  

freeNAS will then ask if you wish to destroy the data(pictured below)!  MAKE SURE YOU DO NOT CHECK THIS BOX OR YOUR DATA WILL BE GONE! 

To proceed:  click Yes 

![](images/00022.jpg)  

Once the volume is removed it should NOT be viewable under active volumes.   Now you will want to shut down the freeNAS VM.  I suggest making an additional VM image backup through the Proxmox interface.  Make sure the backup is stored where it can be easily retrieved!  Now you can safely power down the physical Proxmox machine and move the freeNAS data disks to your new Proxmox server.

Once you are finished moving the data disks you'll need to restore the freeNAS VM backup image made prior to the move.  The next step will be to re-add the hard disk pass-through on the new Proxmox server.  If you forgot how go here:   

Once you've completed the above steps power on the freeNAS VM, login, and click Auto Import Volume(pictured below).

![](images/00083.jpg)  

You will now see the volume import wizard.  In step 1 select No: Skip to import then click OK(shown below).

![](images/00227.jpg)  

In step 2  select the volume you wish to import then click OK(shown below).

![](images/00173.jpg)  

You should now see the volume showing active after a successful import(shown below).

![](images/00133.jpg)  

3.13-ZFS Datasets

Now that we have created a volume it's time to refine it.   The Dataset can be thought of similar to a folder in MS Windows.  Better yet!  A virtual folder with special properties!

To create a new Dataset:  click Create ZFS Dataset(shown below)

![](images/00357.jpg)  

The default view in freeNAS is Basic Mode so after you name the new dataset click the Advanced Mode button(shown below).

![](images/00039.jpg)  

Advanced Mode offers refinements such as compression, share type, quota, reservation, and deduplication.  Notice that I have set a 100 Gigabyte quota for this dataset(pictured below).

To proceed:  click Add Dataset 

![](images/00210.jpg)  

You will now see your new dataset in the Active Volumes list(shown below).  Notice the Size and Available column information comes from the quota set previously.

![](images/00104.jpg)  

The above example shows a dataset name that I would NOT normally use.   We will now destroy the dataset for reference.

To proceed:  click Destroy Dataset(pictured below)

![](images/00140.jpg)  

freeNAS developers wisely decided to give every opportunity to opt out of destructive actions.  Notice the dialog with a Red background(pictured below).

![](images/00037.jpg)  

I have provided a pre-populated volume with dataset naming conventions that I prefer to use.  The ds prefix simply indicates that I am working with a dataset under the volume named pool0\.  Notice that it is possible to nest the datasets within other datasets(pictured below).

![](images/00253.jpg)  

You can edit an existing dataset at any time.  Let's look at the properties of the dataset named ds.filestore/protected (pictured below).

![](images/00067.jpg)  

To view the dataset properties click Edit ZFS Options(shown below).

![](images/00147.jpg)  

If you need additional space for this dataset change both quota values according to your needs(shown below).

![](images/00017.jpg)  

Pay close attention NOT to exceed the size of the parent dataset(shown below)!

![](images/00033.jpg)  

3.14-ZFS Permissions

Generally, when you create a dataset you will need to set appropriate permissions for users.  For the purpose of this example we will setup public permissions, which are wide open.  No need to worry though, you can also restrict a public share by IP address under the Shares tab.  I can say with confidence, even with public permissions set on your shares, so long as pfSense is setup according to this book, using hardware filtering, that you are quite secure!

Let's set permissions on the ds.backups dataset now(pictured below).

![](images/00244.jpg)  

To proceed:  click Change Permissions(pictured below)

![](images/00138.jpg)  

You should now see the Permissions dialog(pictured below).  To enable public access to this dataset I have checked every box under Mode for Owner, Group, and Other.  The recursive check box means that ALL datasets nested under this one will have permissions changed as well.  ACL can be left defaulted to Unix even if configured under a domain.  If you need specific user or group privileges they can be selected using the dropdown box.

NOTE:  If you have trouble connecting to a share this is where you start your troubleshooting.  Resetting permissions as shown below will guarantee access to the dataset.

![](images/00014.jpg)  

3.15-freeNAS Services

Your server can be setup to host a variety of services which can be found under the Services tab(pictured below).  In this book we will be primarily concerned with CIFS, iSCSI, NFS, Rsync, and SSH.

![](images/00316.jpg)  

3.15.1-CIFS(Windows Sharing) Service

First we'll look at CIFS(otherwise known as SAMBA).  This service is the backbone of Windows compatible networks and will be your primary file sharing protocol.  Let's look at the configuration options for CIFS now.

To proceed:  click the wrench icon(shown below)

![](images/00006.jpg)  

The default configuration options(pictured below) will allow sharing of files in a Windows network as a computer named freenas within the Workgroup named WORKGROUP.  You will need to change these names according to your needs!  For example:  My domain name is called yourwebs.us and my workgroup is called YOURWEBS.  Because I have more than one freeNAS server running I use names such as freeNAS-1, freeNAS-2, freeNAS-3, etc.

![](images/00233.jpg)  

3.15.2-NFS(Linux Sharing) Service

Next, we'll look at NFS.  This service is the original Linux based file sharing protocol.  Today you can install services on windows to connect to NFS shares.  I prefer to keep my NFS shares locked down to only Linux machines.  If you need windows access just enable a temporary CIFS share that only you have permissions for.  Let's look at the configuration options for NFS now.

To proceed:  click the wrench icon(shown below)

![](images/00044.jpg)  

The only configuration option that you will ever need to change is the Bind IP Address(shown below).  It is possible to bind NFS to a different IP than that used for CIFS shares.  For best performance I recommend having 2 network adapters, one for CIFS and the other for NFS and Rsync.

![](images/00005.jpg)  

3.15.3-iSCSI Target Service

Next, we'll look at iSCSI Global options.  iSCSI is a powerful networking protocol and can be a little challenging to beginners.  It allows serialized shares to be created in such a way that the guest operating system is fooled into believing it has multiple physical drives.  Let's look at the Global Configuration options for iSCSI now.

To proceed:  click the wrench icon(shown below)

![](images/00206.jpg)  

You should now see the Target Global Configuration screen as shown below.  The only thing on this screen that you should touch would be the Base Name.  For example:  you may want to change org.example (pictured below) to something like us.freenas1.yourwebs 

CAUTION:  Be careful when changing the Base Name or your server might not be visible for mapping.  If this happens revert back to default:  iqn.2011-03.org.example.istgt 

![](images/00361.jpg)  

3.15.4-Rsync(Backup) Service

Now, we'll look at Rsync configuration options.  Rsync is a powerful backup utility which is widely used in the Linux community.  It is light weight and very good at what it does!  freeNAS provides excellent scripting for Rsync backups!  We'll cover that later!  Let's look at the configuration options for Rsync now.

To proceed:  click the wrench icon(shown below)

![](images/00153.jpg)  

The configuration for the Rsync service is simple.  There really isn't any!  Keep the default TCP port value(pictured below).

![](images/00112.jpg)  

3.15.5-SSH(Secure Shell) Service

Finally, we'll look at SSH configuration options.  SSH stands for secure shell.  It allows remote logins via a console program such as the PuTTY program used earlier in the book.  Let's look at the configuration options for SSH now.

To proceed:  click the wrench icon(shown below)

![](images/00304.jpg)  

Make sure to match ALL checkboxes that I have checked(pictured below).  No further configuration is needed.

![](images/00202.jpg)  

Now that we've covered the important service configuration options make sure they're all enabled by clicking each of the service switches(shown below).  They should turn blue when enabled!

![](images/00184.jpg)  

3.16-Add Network Shares

3.16.1-NFS Shares

As mentioned earlier in the book, I prefer to use NFS shares for Proxmox backups.  We will now create a share called netbackups which will be used for Proxmox VM image backups.

To proceed click Sharing>NFS(pictured below)

![](images/00259.jpg)  

Next, click Add NFS Share(pictured below).

![](images/00129.jpg)  

When the dialog appears type in the appropriate information(pictured below).  Notice that I have Authorized 3 Proxmox server IP addresses.  This will restrict access and is strongly suggested!  Under Maproot User select root.  This may NOT be the most secure but is guaranteed to work and keeps things simple.  Also notice that I have browsed and selected a nested dataset under ds.backup named netbackups.

If you have not created a dataset yet go back a do so now.  Otherwise, click close after your dataset selection(pictured below).

![](images/00212.jpg)  

Now, carefully review your entries then click OK to proceed(pictured below).

![](images/00252.jpg)  

You should now see the new NFS netbackups share in the list(pictured below).

![](images/00343.jpg)  

3.16.2-Windows Shares

Setting up a Windows share is very similar to NFS.  We will now create a share called netbackups which can be used to access Proxmox VM image backups from Windows.

To proceed:  click Add CIFS Share(pictured below).

![](images/00069.jpg)  

Start by typing an appropriate Name and selecting the dataset Path as shown below!

![](images/00123.jpg)  

Now, enter a comment if you wish and set all other options according to your needs.  Notice that I have set this share to Read Only and Browsable to Network Clients(shown below).

![](images/00011.jpg)  

Once finished, your new Windows share will be visible in the list(pictured below).

![](images/00281.jpg)  

3.16.3-iSCSI Target Shares

I have elected to save iSCSI for last because it takes the most time to configure.  Please pay attention closely!  To setup an iSCSI target you'll first need to add a dataset to be mapped.  For this example I have created a 40Gb dataset named example.trgt012 nested within the ds.iscsitrgts dataset(pictured below).  This naming convention helps me identify the intended type of share I'm working with.

![](images/00188.jpg)  

Once you have created a dataset go to the Services tab as shown below.

To proceed:  click the wrench icon(shown below)

![](images/00206.jpg)  

Next go straight to the Portals tab then click Add Portal(shown below)

![](images/00293.jpg)  

When the dialog screen appears(shown below) you will notice the default IP Address is set to 0.0.0.0 implying that ANY interface will be used.  This setting is fine!  You may also wish to add a comment.

To proceed:  click OK 

![](images/00118.jpg)  

Next, we'll setup Initiators!  To proceed:  click Add Initiator(shown below)

![](images/00345.jpg)  

You should now see the Add Initiator dialog(pictured below).  Since you are in a Layer 2 hardware protected network it is safe to keep the default settings.

To proceed:  click OK (shown below)

![](images/00056.jpg)  

Now we'll setup Access Groups!

To proceed:  click Add Authorized Access(shown below)

![](images/00063.jpg)  

When the dialog appears as shown below enter the appropriate information.  For this example I have set the User as a network client named win7pro and the Peer User as my active directory Username:  lsurber 

NOTE:  The Secret and Peer Secret cannot be the same!  I choose an arbitrary Secret while using my active directory password for the Peer Secret.

To proceed:  click OK(shown below)

![](images/00179.jpg)  

Next up is Targets!  To proceed:  click Add Target(shown below)

![](images/00105.jpg)  

You should now see the Target Dialog screen shown below.  My preference is to use the name of the dataset(example.trgt012) as the Target Name.  Now, select the Portal Group ID and the Initiator Group ID establish earlier.  You could also choose an Authentication Group number.  I have left this set to none for this example.

To proceed:  click OK(pictured below)

![](images/00148.jpg)  

You should now see your newly created Target as shown below.

![](images/00061.jpg)  

Next we'll configure the Extent!

To proceed:  click Add Extent(pictured below)

![](images/00139.jpg)  

Once again, I have chosen to use the dataset name for the Extent Name and set the Extent size to 40g.  This matches the quota I set for the dataset when it was created.  My preference and recommendation is to use the File Extent Type.  Now choose the appropriate Path to the extent.  NOTICE:  I have selected  the nested dataset example.trgt012 for the path. 

After selecting your path:  click Close(shown below)

![](images/00009.jpg)  

To proceed:  click OK(shown below)

![](images/00045.jpg)  

I have purposely created this common error for your reference(shown below).  NOTICE:  because this is a File Extent Type you cannot simply select the dataset as the Path to the extent.  Also, notice the correct Extent size syntax was wrong!  It should have been 40GB.

![](images/00134.jpg)  

To correct the Path to the extent I will simply add /trgt012 to the end of the selected dataset.  You may be starting to understand why naming is important!

With everything corrected click OK(shown below)

![](images/00100.jpg)  

Finally, we can Associate the Target with the Extent!

To proceed:  click Add Target/Extent 

![](images/00358.jpg)  

When the dialog appears simply select the Target and Extent to associate from the dropdowns.  You can leave LUN ID set to Auto.

To proceed:  click OK(shown below)

![](images/00162.jpg)  

When the target has been successfully added to the system it will appear as shown below.  Congratulations!

![](images/00218.jpg)  

3.17-ZFS Snapshot Backups

Probably, the BEST feature of the ZFS file system is copy on write.  This feature allows backups to be restored almost instantly from snapshot archives.  When setup and used properly you will NEVER need another form of backup software... EVER!!!  I STRONGLY suggest using my best practices method.  It involves running 2, 3, or 4 freeNAS servers all with the same datasets.

Any dataset hosting live data will be considered a primary dataset.  Each primary dataset  will need to be manually replicated (once during setup) to all other freeNAS nodes.  The primary  datasets(hosting live data) will be configured as Rsync push tasks on the node hosting the live shares.  The backup  datasets(backup data only) will be configured as Rsync modules on any node NOT hosting live shares .  With this method all datasets are replicated over every freeNAS node automatically.

ZFS snapshots can then be setup on each node using a different schedule.  The primary datasets  can  be set to hourly or daily snapshots while the rest are set to weekly, monthly, etc.  With enough storage overhead it is entirely possible to set it and forget it while it maintains backups for a year or more.  Let's setup a snapshot task now!

To proceed:  click Add Periodic Snapshot(shown below)

![](images/00340.jpg)  

For this snapshot task I am selecting the ds.backups dataset(pictured below).

![](images/00040.jpg)  

Once again, the Recursive switch means that ALL nested datasets under ds.backups will be included in the snapshot.  All other options should be self-explanatory(pictured below).

![](images/00036.jpg)  

Once saved, your snapshot task will appear in the list(pictured below).

![](images/00060.jpg)  

Notice that the new snapshot task was run almost immediately and can be accessed under the ZFS Snapshots tab(shown below).  At this point, users of Windows 7 or higher could now right click a CIFS file share on this dataset and mount or restore a file from the snapshot. 

![](images/00070.jpg)  

3.18-Restore A Snapshot In Windows

As an IT Administrator, it is very common to have end users calling on a daily basis saying they accidentally deleted their files.  ZFS snapshots make this daily task easy to deal with on systems running Windows 7 or higher!  Let's look at snapshot restore options on a Windows 7 machine(pictured below)!

![](images/00321.jpg)  

Let's assume a user deleted a file from the mapped Z drive(shown above).  To see available snapshots simply right click the drive then choose Properties(picture below).

![](images/00166.jpg)  

When the dialog appears select the Previous Versions tab(pictured below).  You will then have the option to Open, Copy, or Restore any files over the range of snapshots in your schedule.

![](images/00283.jpg)  

3.19-Rsync Replication

As mentioned previously, Rsync is a powerful backup utility widely used in the Linux community.  It's poor man's High- Availability without a fence device!  In many ways it's better!  Of course, you won't have millisecond failover and true HA, but you will have several copies of data that can be accessed very quickly(5-10 minutes) if needed.  The biggest BONUS here is price!  A true hardware fenced High-Availability storage farm will cost you between $20000 and $100000 US Currency!

In order to setup Rsync for first run make sure you have created identical datasets on every freeNAS node.  So, if you have 3 servers planned, then you will have 3 sets of identical datasets for the Rsync backups.  The primary  datasets(hosting live data) will be configured as Rsync push tasks on the node hosting the live shares.  The backup  datasets(backup data only) will be configured as Rsync modules on any node NOT hosting live shares .  With this method all datasets are replicated over every freeNAS node automatically.

3.19.1-Add The Rsync Push Task

Let's add an Rsync task for the primary dataset named netbackups!  This dataset contains important live data and is where Proxmox stores ALL of the VM image backups in a system configured like [(Option-2) Optimized For Network Backed Storage](#index_split_006.html_filepos42952)!

To proceed:  click System>Rsync Tasks>Add Rsync Task(shown below)

![](images/00157.jpg)  

You should now see the task dialog box. Click Browse and select the appropriate dataset(as shown below).

![](images/00199.jpg)  

Notice(below) that I have chosen the netbackups dataset which is nested under ds.backups!  Please NOTE that when Rsync runs it will backup the entire netbackups dataset folder.  This is IMPORTANT to remember when setting up the backup datasets on other  nodes.

> ![](images/00113.jpg)

Next you will need to enter the Remote Host IP address and Remote Module Name.  Notice, I have chosen freenas5.netbackups as the module name(pictured below).  This identifies freenas5 as the remote node and netbackups as the dataset folder I am backing up.  Now, if I want to replicate netbackups to another server(freenas-2), the module names will uniquely identify each replication.

Leave Rsync mode set to module and Direction set to Push.  You may wish to enter a description that will indicate the frequency of the backups.

![](images/00120.jpg)  

Next, select the desired frequency of the backup by adjusting the sliders(fig. 1-3 below).  NOTE:  Every 15 minutes may be too frequent for good performance!  This is just an example!  I generally use 1 hour for files that change frequently and 1 day for static files.

fig. 1

![](images/00258.jpg)  

fig. 2

![](images/00332.jpg)  

fig. 3

![](images/00247.jpg)  

You may also choose a specific month(shown Below)

![](images/00167.jpg)  

Or, choose a specific day of the week(shown below).

![](images/00169.jpg)  

The default User is set to root(shown below).  I would NOT change this unless you know what you're doing.

![](images/00230.jpg)  

I like to use the options set as shown below.

![](images/00142.jpg)  

![](images/00050.jpg)  

![](images/00131.jpg)  

The screenshot below shows what a working Rsync Tasks table looks like.  These tasks are configured on a fileserver named freeNAS-1 hosting live data.  All datasets are pushed to Remote Modules on nodes freeNAS-2 and freeNAS-4 every hour.

![](images/00092.jpg)  

3.19.2-Add The Rsync Module

Let's setup an Rsync Module for a backup dataset on one of the other freeNAS nodes to synchronize the netbackups dataset now!

To proceed:  click Services>Rsync (shown below)

![](images/00130.jpg)  

Now, click Add Rync Module(shown below)

![](images/00136.jpg)  

You should now see the module dialog box(pictured below).  Enter the Module name from the Rsync push task you previously configured(freenas5.netbackups).  You may wish to use the same Comment from the Rsync push task.  Leave the Access Mode set to Read/Write and User set to root. 

NOTICE:  I have added the IP address of the primary freeNAS push task node in the Hosts allow field to limit access.

MOST IMPORTANT:  It is critical the Path be set to /mnt/pool0/ds.backups and NOT /mnt/pool0/ds.backups/netbackups or you will end up with a nested copy that looks something like this /mnt/pool0/ds.backups/netbackups/netbackups.

![](images/00152.jpg)  

The screenshot below shows what a working Rsync Modules table looks like.  These Modules are configured on a machine named freeNAS-4\.  All datasets are pushed from freeNAS-1 every hour.

![](images/00079.jpg)  

3.19.3-Tips On Using Rsync

Setting up Tasks and Modules can be confusing at first so be patient and think about what you're doing.

*   > > Remember that when configuring Rsync in Push mode(used in this book) live datasets will have a Task and backup datasets will have a Module.

*   > > Avoid having live datasets on every freeNAS node.  You should have at least 1 freeNAS node where NO live data is hosted.  This normally means there will be NO Rsync Push Tasks on that machine.

*   > > Double check every Task and Module you create.  This will help prevent overwriting important live data.

*   > > When setting up a new freeNAS server with a large amount of data only add a few modules at a time.  You would experience a big performance hit if several Terabytes of data tried to synchronize all at once.

*   > > Use good naming practices to avoid confusion.

*   > > Use dedicated network adapters and an isolated subnet to dramatically improve performance.  You may also want to limit adapter throughput OR use 100 Base virtual adapters for these dedicated links.

3.20-Domain Membership

A domain directory consists of a central database and allows MUCH easier management of Users, Groups, and Network Services.  Most domains are managed by Microsoft active directory running on a Windows server.  In this book I have included an open source alternative which leverages the powerful Samba4 platform running on Zentyal Small Business Server.

Although freeNAS is capable of acting as a Domain Controller, I prefer to use Zentyal because it keeps things modular and it can be readily setup for Master/Slave control.  This method is preferred because it adds redundancy to the central database!

Let's add this freeNAS server to a Zentyal controlled domain.  In the tradition of keeping things simple and compatible I will use the older NT4 database style(shown below).

To configure Domain Directory Service click System>General then select NT4 from the dropdown list(shown below).  Don't forget to save the setting!

![](images/00346.jpg)  

Next, go to Services>Directory Services and click the wrench icon(pictured below)

![](images/00128.jpg)  

You should now see the Directory Service dialog(shown below).  Enter the Domain Controller IP address instead of the host name.  This is the address of the Zentyal server.  NOTE:   This address should also be entered in your pfSense DHCP static reservation list.

PAY ATTENTION HERE:  With the NT4 based directory you DO NOT need to enter .com, .org, .us, etc domain suffixes.  Also, your Workgroup Name is limited to 15 characters.  I have entered YOURWEBS in the Workgroup Name even though the domain name I will be controlling is YOURWEBS.US(pictured below).

![](images/00007.jpg)  

Earlier we setup CIFS(Windows) shares on your new freeNAS server.  When configuring the machine for domain membership the CIFS Workgroup settings should match those for Directory Services.

Double check your settings now by going to Services>CIFS then clicking the wrench icon.  I have included my settings for your reference(pictured below).  Remember to save your changes!

![](images/00294.jpg)  

Now you can enable the Directory Service by clicking on the switch as shown below.  It should turn blue when enabled.

![](images/00285.jpg)  

The final step is to Rebuild the cache.  Go to System>Settings>Advanced then click Rebuild LDAP/AD Cache at the bottom of the page(shown below).  NOTE:  sometimes it is necessary to reboot the server for all changes to become active.

![](images/00217.jpg)  

3.20.1-Domain Permissions

With the server now being an active domain member you should now see additional Users and Groups in your dataset Permissions dialog.  To demonstrate this I have included the permissions dialog for the netbackups dataset we created earlier.  Notice the additional Users at the bottom of the dropdown list(pictured below).

![](images/00215.jpg)  

As an example I have changed the owner permissions on the netbackups dataset(pictured below).  With these new permissions, ONLY domain administrators would have access to the dataset.

![](images/00331.jpg)  

3.21-Configuration Backups

Besides using VM image backups it is also wise to keep a copy of the freeNAS configuration.  The configuration backup is especially important when developers rewrite the build in a way that breaks certain packages on update.  In these instances your VM image backup will only get you back to the version you were using.  I have NOT had this happen with freeNAS, so don't worry too much!

To access the configuration backup page:  click System>Settings>General followed by Save Config(pictured below).

![](images/00012.jpg)  

Save the configuration file to disk when the download dialog appears(shown below).  HINT:  I recommend keeping a copy of this on thumb drive!

![](images/00204.jpg)  

Restoring your freeNAS configuration should be self-explanatory!  Simply use the Upload Config option instead!

Book 4:  Zentyal Domain Controller

4.1-Introduction To Zentyal

Zentyal started in 2004 as an Open Source project.  It has a very loyal global community and is actively developed.  Zentyal Small Business Server CE is actually a fully fledged business solution.  The latest versions leverage the powerful Samba 4 package which effectively emulates a Microsoft Domain Controller.  It comes as a complete standalone distribution in CD\DVD ISO format which makes installation a breeze!  This makes Zentyal a no brainer for inclusion as a modular building block in our 4 in 1 system.

In our system we will use it as an Active Directory Domain Controller.  In this book I am using the Zentyal 4.0 64 bit version.  You can download this exact version at Sourceforge here:  [zentyal-4.0-amd64.iso](http://sourceforge.net/projects/zentyal/files/Old%20versions/zentyal-4.0-amd64.iso/download)  NOTE:  The latest version is now called Zentyal Server Development Edition.  The interface remains largely the same but I would still recommend matching the version I have use to avoid any issues.  If you are comfortable with the latest version it can be downloaded directly from the Zentyal home page here:  [Zentyal Server Development Edition](http://www.zentyal.org/server/) 

4.2-Installing Zentyal

The installation process for Zentyal is similar to most other operating systems.  Before installation can begin you must create the VM configuration.  I recommend a 12Gb IDE virtual disk with 8Gb of Ram for this install.  If you need to review those steps again click here: [1.9-Creating VM Configuration](#index_split_015.html_filepos77013).  You may also want to add a DHCP client reservation in pfSense before you begin the actual install.

Once the machine is started you will see the language selection screen(pictured below).

To proceed:  press ENTER 

![](images/00320.jpg)  

Next, you will see the mode selection screen(shown below).

To proceed:  press ENTER 

![](images/00085.jpg)  

The default language is set to English(pictured below).  Notice: the navigation map for moving, selecting, and activating is located at the bottom of the screen.

To proceed:  press ENTER 

![](images/00368.jpg)  

Now, select your location(pictured below).

To proceed:  press ENTER 

![](images/00239.jpg)  

Optionally, you may choose to detect your keyboard layout(shown below).  We will not auto-detect our keyboard.

To proceed:  select No then press ENTER 

![](images/00043.jpg)  

Next, select the country of origin for your keyboard(pictured below).

To proceed:  press ENTER 

![](images/00038.jpg)  

Now, select the proper layout for your keyboard(shown below).

To proceed:  press ENTER 

![](images/00076.jpg)  

Now, you will be prompted to set a hostname.  If you already assigned a static DHCP reservation your hostname should appear(pictured below).

To proceed:  Select Continue then press ENTER 

![](images/00338.jpg)  

Next, choose a username for account administration(shown below).

To proceed:  Select Continue then press ENTER 

![](images/00072.jpg)  

Make sure you choose a strong password to help protect your system(pictured below).

To proceed:  Select Continue then press ENTER 

![](images/00364.jpg)  

Zentyal should auto-detect your time zone.  If it does not then follow the prompt to correct your settings.

To proceed:  Select Yes then press ENTER 

![](images/00289.jpg)  

When the installation is ready to complete you will be prompted to remove the CD.  NOTE:  Since this is a VM installation you will do this through the Proxmox interface.

To proceed:  Select Continue then press ENTER 

![](images/00352.jpg)  

4.3-Initial Login

Once Zentyal completes the installation stage it needs to be configured.  Enter the IP address for Zentyal in your web browser.  This is a secure site so your entry should look something like this:  https://192.168.0.76:8443  For the purpose of this tutorial I have used Mozilla Firefox.

To continue(pictured below): click I Understand the Risks 

![](images/00168.jpg)  

Next:  Click Add Exception as pictured below

![](images/00154.jpg)  

Then: Click Confirm Security Exception as pictured below

![](images/00028.jpg)  

You may now login to Zentyal using the credentials established during the installation(pictured below).

![](images/00311.jpg)  

4.4-Initial Setup

When you are ready to start the initial setup of Zentyal press the green Continue button(shown below).

![](images/00277.jpg)  

For our installation we are only using Zentyal as a Domain Controller.  When Domain Controller and File Sharing is selected a green check will appear(shown below).

To proceed:  click INSTALL 

![](images/00175.jpg)  

Confirm the package selection by clicking CONTINUE as shown below.

![](images/00286.jpg)  

Next, the wizard will prompt to configure network interfaces(shown below).

Select Internal for eth0 then click NEXT 

![](images/00141.jpg)  

Since Zentyal is a critical server you will always want a static IP address.

Select Static from the dropdown then click NEXT to continue(shown below).

![](images/00094.jpg)  

Next, enter the appropriate address information(shown below).  This should already be populated if you made a DHCP reservation in pfSense.

To proceed:  click NEXT 

![](images/00093.jpg)  

You will now need to enter the server type and domain name information.  For the purpose of this tutorial I have selected a Standalone server that authenticates YOURWEBS.US users(shown below).  NOTE:  This can easily be changed to Additional domain controller even after the installation is complete.  I have included instructions in [4.8-Additional Domain Controller](#index_split_061.html_filepos234836) for those who need both PDC and BDC.

To proceed:  click FINISH 

![](images/00186.jpg)  

The Zentyal installation is now complete.

To proceed:  click GO TO THE DASHBOARD (pictured below)

![](images/00150.jpg)  

4.5-Navigating Zentyal

The first screen that appears after final setup or login is the Zentyal Dashboard(pictured below).  All further configuration will take place using this interface.

![](images/00191.jpg)  

On the left side of the screen you will find the navigation tree(pictured below).  When you click on any category in the list it will auto-expand to show additional sub-categories if there are any.

![](images/00053.jpg)  

4.6-Adding Users

Adding a user in Zentyal is relatively straight forward.  On the left side of the screen click the Users and Computers list item.  You should now see the Users and Computers module screen(shown below).  Notice that in our example the top level item shows the YOURWEBS.US domain and all associated items under that domain.  To add a new user select the Users folder(shown in blue below).  This action will cause the + button at the bottom of the page to turn green(pictured below).  Clicking the green + button will open the Add User dialog.

![](images/00176.jpg)  

When the Add User dialog appears fill the form with the appropriate information then click ADD(shown below).

![](images/00339.jpg)  

4.7-Adding Groups

Adding a group is very much the same as adding a user.  On the left side of the screen click the Users and Computers list item.  You should now see the Users and Computers module screen(shown below).  Notice that in our example the top level item shows the YOURWEBS.US domain and all associated items under that domain.  To add a new group select the Groups folder(shown in blue below).  This action will cause the + button at the bottom of the page to turn green(pictured below).  Clicking the green + button will open the Add Group dialog.

![](images/00297.jpg)  

When the Add Group dialog appears fill the form with the appropriate information then click ADD(shown below).

![](images/00341.jpg)  

4.8-Additional Domain Controller

During installation Zentyal was configured as a Standalone server named ZentyalDC2.  This was done purposefully to demonstrate how to change the role from Standalone to Additional domain controller.  Let's assume there was already a Zentyal domain controller named ZentyalDC1 configured as a Standalone server for the yourwebs.us domain.

To change the ZentyalDC2 role:  Click Domain>Settings then select Additional domain controller from the dropdown.  Enter the information for the ZentyalDC1.yourwebs.us controller as shown below.  IMPORTANT:  The IP address MUST be that of ZentyalDC1 and NOT that of the pfSense router which acts as the DNS server for yourwebs.us.  Don't forget to save your changes when finished!

![](images/00296.jpg)  

4.9-Shut Down & Reboot

If you should need to shutdown or restart your server that's easy!  The control can be found under System in the navigation tree(shown below).

![](images/00174.jpg)  

4.10-Upgrading Zentyal

On the main screen you will be alerted when there are upgrades available(shown below).  I would strongly recommend against upgrades unless it is absolutely necessary.  My preference with Linux based software is to find versions that work and stick with them until a better solution comes along.  If it isn't broken don't try to fix it!  This really does hold true!  In the case of our Zentyal installation it is only being used to hold users in a database.  Furthermore, it is virtualized and because of this, will remain compatible for as long as you wish to use it.

![](images/00203.jpg)  

4.11-Joining Zentyal Domains

Now that Zentyal is configured for domain control all network clients should be able to access it.  The keyword here is access NOT join!  This is important to understand when administering a domain!  The common misconception is that you must join a domain to have privilege and that is simply NOT the case.  In fact, sometimes it may be preferred to simply remain in a WORKGROUP while still having user access to shares that are delegated under a domain.  A good example:  It is very common for some software to require Administrative privilege to run.  Some very expensive high level CAD software not only require privileges but must be run as Administrator!

Avoiding The IT Dictatorship

When you elect to join clients to a domain it becomes restrictive and increasingly difficult to manage user preferences.  Not all users have the same requirements or preferences.  This can make the IT Administrators role very challenging!  They must maintain the security and integrity of the system while at the same time not alienating the end users.  Using your domain control authority to be overly restrictive can create a hostile workplace where co-workers despise the IT Staff!  A properly implemented IDS system running on a layer 2 hardware filtered network will crush just about attack!  This allows Administrators to relax user account settings while still maintaining strong network security.

4.11.1-Workgroup Authentication

As mentioned above, it is sometimes preferred to remain in a WORGROUP while still authenticating against a domain.  This is by far the simplest system to implement and affords a wide range of flexibility to Admins.  Let's take a look at how this works.  For the purpose of this book I have a domain named YOURWEBS.US which we have setup Zentyal to be a domain controller for.  In the System Properties>Computer Name dialog(pictured below) the client workstation is named win7pro and the WORKGROUP is set to YOURWEBS.  Essentially, just by dropping the domain suffix(.US) off the end enables our system to browse network resources that are domain controlled.  If you need to change your workgroup name click the Change button(shown below) to match the domain name setup in your system. 

![](images/00032.jpg)  

The following dialog appears when you click the Change button above.  Simply type your new Workgroup name where you see YOURWEBS(pictured below) then click OK 

![](images/00201.jpg)  

In Chapter 3.20 we joined our freeNAS-4 fileserver to the YOURWEBS.US so we are already able to take advantage of network share access control.  If you need to review freeNAS domain permissions click here:  [3.20-Domain Membership](#index_split_052.html_filepos214725)  Let's map a network share from freeNAS-4 using YOURWEBS.US domain credentials as shown below.

![](images/00058.jpg)  

Opening FreeNAS-4 reveals it's share.  Simply right click the share then select Map network drive(pictured below).

![](images/00172.jpg)  

When mapping from a WORKGROUP client it is important to check the box Connect using different credentials(shown below).

![](images/00237.jpg)  

You should then be prompted for the credentials as shown below.  Notice that the username MUST be formatted to include the domain without any suffix when connecting from a WORKGROUP client.  The entry should look something like this: YOURDOMAIN\username 

![](images/00019.jpg)  

After credentials have been accepted you should see your new share mapping(shown below).

![](images/00205.jpg)  

4.11.2-Join The Domain In Windows

To join a network client to the domain is referred to as binding and will severely restrict user preferences.  To achieve the bind click the Change button(shown below).

![](images/00032.jpg)  

Next, select the Domain option(shown below).

![](images/00201.jpg)  

Type the domain name without any suffix(shown below).

![](images/00034.jpg)  

Finally, type the full domain Administrator credentials when prompted.  Notice that the username MUST be formatted to include the full domain when binding a client.  The entry should look something like this: YOURDOMAIN.XYZ\username 

![](images/00273.jpg)  

When the client machine is successfully bound you will see the welcome dialog after which you will be prompted to reboot.

![](images/00193.jpg)  

4.12-Configuration Backups

Besides using VM image backups it is also wise to keep a copy of the Zentyal configuration.  The configuration backup is especially important when developers rewrite the build in a way that breaks certain packages on update.  In these instances your VM image backup will only get you back to the version you were using.  I have NOT had this happen with Zentyal, so don't worry too much!

To access the configuration backup page:  click System>Configuration Backup(pictured below).

![](images/00126.jpg)  

Next, select Local then click the BACKUP button(pictured below).

![](images/00306.jpg)  

You should now see your new configuration backup in the Backups' list(shown below).

![](images/00236.jpg)  

Download your new configuration by clicking the Download Configuration button(shown below).

![](images/00214.jpg)  

Save your configuration to disk when the download begins.  HINT:  I recommend keeping a copy of this file on thumb drive!

![](images/00279.jpg)  

Restoring your Zentyal configuration should be self-explanatory!  Simply use the RESTORE option instead!

.4-Final Thoughts And Thanks

It doesn't seem too long ago that being an IT Administrator could be hugely stressful.  So much so, that I can remember times when I questioned whether or not to remain in the field!  I can honestly say that virtualization has changed things for the better!  The ease of management and maintenance that it provides has brought back that flame that inspired me so many years ago.  I don't think there's a day that passes where I am not awe-inspired with how well this system works!  It's like the terminator!  Please keep in mind, that none of this would be possible if it were not for the hard work and dedication of the open source development community!  So, please!  Support the community where you can!

In closing, I would like to thank all those who have purchased and read this book.  Many thousands of hours went into production testing and research before I felt confident that this system was the system!  I hope that it has been instrumental in building your personal or business based infrastructure.  Once you are bitten by the virtualization bug it's seemingly impossible to turn back!  For this reason I will continue with future projects focused on an even more complete business solution.  Of notable mention, would be my plans to incorporate PBX, multi-domain email, and multi-domain webhosting servers into this already robust system.  So, thanks again and stay tuned for more upcoming Virtualization Complete releases such as BUSINESS PLUS, BUSINESS PRO, BUSINESS ADVANCED, and perhaps ENTERPRISE!

.5-Additional Resources

[www.proxmox.com](http://www.proxmox.com/):  Proxmox home page.

[www.pfsense.org](https://www.pfsense.org/):  pfSense home page.

[www.freenas.org](http://www.freenas.org/):  freeNAS home page.

[www.zentyal.com](http://www.zentyal.com/):  Zentyal home page.

[www.distrowatch.com](http://distrowatch.com/):  One of the best open source distribution databases on the web.

Table of Contents

*   [Book Description](#index_split_001.html_filepos611)
*   [Copyright](#index_split_002.html_filepos3388)
*   [.1-Introduction](#index_split_004.html_filepos17397)
*   [.2-Before You Begin](#index_split_005.html_filepos26625)
*   [.3-Best Practices](#index_split_006.html_filepos28974)
*   [Book 1:  Proxmox VE](#index_split_007.html_filepos50528)
    *   [1.1-Introduction To Proxmox](#index_split_007.html_filepos50660)
    *   [1.2-Installing Proxmox](#index_split_008.html_filepos52406)
    *   [1.3-Initial Login](#index_split_009.html_filepos59739)
    *   [1.4-Network Adapters](#index_split_010.html_filepos61979)
    *   [1.5-Adding LVM Storage](#index_split_011.html_filepos65541)
    *   [1.6-Configure LVM Storage](#index_split_012.html_filepos70296)
    *   [1.7-Configure NFS Storage](#index_split_013.html_filepos71958)
    *   [1.8-Configure iSCSI Storage](#index_split_014.html_filepos74171)
    *   [1.9-Creating VM Configurations](#index_split_015.html_filepos77013)
    *   [1.10-VM Backup & Restore](#index_split_016.html_filepos86999)
    *   [1.11-VM Hardware](#index_split_017.html_filepos92928)
    *   [1.12-Adding Pass-Through Disks](#index_split_018.html_filepos97235)
    *   [1.13-Troubleshooting Proxmox](#index_split_019.html_filepos105352)
    *   [1.14-Upgrading Proxmox](#index_split_020.html_filepos106161)
*   [Book 2:  pfSense](#index_split_021.html_filepos107409)
    *   [2.1-Introduction To pfSense](#index_split_021.html_filepos107538)
    *   [2.2-Installing pfSense](#index_split_022.html_filepos110101)
    *   [2.3-Assigning Network Interfaces](#index_split_023.html_filepos112286)
    *   [2.3-Assigning IP Addresses](#index_split_024.html_filepos115257)
    *   [2.4-Reset Admin Password](#index_split_025.html_filepos118919)
    *   [2.5-Web Configuration Wizard](#index_split_026.html_filepos119701)
    *   [2.6-Changing Themes](#index_split_027.html_filepos125254)
    *   [2.7-Configure DHCP Server](#index_split_028.html_filepos126560)
        *   [2.7.1-WINS, DNS, Gateway, and Domain](#index_split_028.html_filepos128086)
        *   [2.7.2-DHCP Client Reservations](#index_split_028.html_filepos129335)
    *   [2.8-Firewall Settings](#index_split_029.html_filepos130789)
        *   [2.8.1-LAN Rules](#index_split_029.html_filepos131340)
        *   [2.8.2-WAN Rules](#index_split_029.html_filepos132607)
    *   [2.9-OpenVPN](#index_split_030.html_filepos133813)
        *   [2.9.1-OpenVPN Client Export Utility](#index_split_030.html_filepos134546)
        *   [2.9.2-OpenVPN Setup Wizard](#index_split_030.html_filepos135208)
        *   [2.9.3-OpenVPN Client Connectors](#index_split_030.html_filepos139013)
        *   [2.9.4-Authenticate Zentyal Domain Users](#index_split_030.html_filepos140300)
    *   [2.10-Snort IDS](#index_split_031.html_filepos143634)
        *   [2.10.1-Install Snort Package](#index_split_031.html_filepos144780)
        *   [2.10.2-Snort Global Settings](#index_split_031.html_filepos145641)
        *   [2.10.3-Snort Interfaces](#index_split_031.html_filepos146037)
        *   [2.10.4-Updating Threat Rules](#index_split_031.html_filepos148165)
        *   [2.10.5-Threat Rule Categories](#index_split_031.html_filepos148542)
        *   [2.10.6-Add Alerts To Suppression List](#index_split_031.html_filepos149705)
        *   [2.10.7-Block Offenders At Source](#index_split_031.html_filepos150555)
    *   [2.11-Configuration Backups](#index_split_032.html_filepos151614)
*   [Book 3:  freeNAS](#index_split_033.html_filepos153134)
    *   [3.1-Traditional Storage Fails](#index_split_033.html_filepos153263)
    *   [3.2-freeNAS & ZFS](#index_split_034.html_filepos158684)
    *   [3.3-Installing freeNAS](#index_split_035.html_filepos159656)
    *   [3.4-Add freeNAS Pass-Through Disks](#index_split_036.html_filepos163763)
    *   [3.5-Set Storage For No Backup](#index_split_037.html_filepos165198)
    *   [3.6-Start freeNAS Through The Console](#index_split_038.html_filepos166572)
    *   [3.7-Initial Login](#index_split_039.html_filepos167436)
    *   [3.8-freeNAS Navigation](#index_split_040.html_filepos168229)
    *   [3.9-Network Configuration](#index_split_041.html_filepos168671)
    *   [3.10-Users And Groups](#index_split_042.html_filepos170783)
        *   [3.10.1-Adding A New User](#index_split_042.html_filepos170894)
        *   [3.10.2-Adding A New Group](#index_split_042.html_filepos172510)
    *   [3.11-Add A ZFS Volume](#index_split_043.html_filepos173178)
    *   [3.12-Detach And Move Volumes](#index_split_044.html_filepos174244)
    *   [3.13-ZFS Datasets](#index_split_045.html_filepos176971)
    *   [3.14-ZFS Permissions](#index_split_046.html_filepos180713)
    *   [3.15-freeNAS Services](#index_split_047.html_filepos182750)
        *   [3.15.1-CIFS(Windows Sharing) Service](#index_split_047.html_filepos183226)
        *   [3.15.2-NFS(Linux Sharing) Service](#index_split_047.html_filepos184498)
        *   [3.15.3-iSCSI Target Service](#index_split_047.html_filepos185721)
        *   [3.15.4-Rsync(Backup) Service](#index_split_047.html_filepos187083)
        *   [3.15.5-SSH(Secure Shell) Service](#index_split_047.html_filepos188051)
    *   [3.16-Add Network Shares](#index_split_048.html_filepos189275)
        *   [3.16.1-NFS Shares](#index_split_048.html_filepos189388)
        *   [3.16.2-Windows Shares](#index_split_048.html_filepos191389)
        *   [3.16.3-iSCSI Target Shares](#index_split_048.html_filepos192766)
    *   [3.17-ZFS Snapshot Backups](#index_split_049.html_filepos200154)
    *   [3.18-Restore A Snapshot In Windows](#index_split_050.html_filepos203397)
    *   [3.19-Rsync Replication](#index_split_051.html_filepos204679)
        *   [3.19.1-Add The Rsync Push Task](#index_split_051.html_filepos206034)
        *   [3.19.2-Add The Rsync Module](#index_split_051.html_filepos210666)
        *   [3.19.3-Tips On Using Rsync](#index_split_051.html_filepos212722)
    *   [3.20-Domain Membership](#index_split_052.html_filepos214725)
        *   [3.20.1-Domain Permissions](#index_split_052.html_filepos218609)
    *   [3.21-Configuration Backups](#index_split_053.html_filepos219629)
*   [Book 4:  Zentyal Domain Controller](#index_split_054.html_filepos220923)
    *   [4.1-Introduction To Zentyal](#index_split_054.html_filepos221070)
    *   [4.2-Installing Zentyal](#index_split_055.html_filepos222574)
    *   [4.3-Initial Login](#index_split_056.html_filepos227249)
    *   [4.4-Initial Setup](#index_split_057.html_filepos228620)
    *   [4.5-Navigating Zentyal](#index_split_058.html_filepos231647)
    *   [4.6-Adding Users](#index_split_059.html_filepos232445)
    *   [4.7-Adding Groups](#index_split_060.html_filepos233639)
    *   [4.8-Additional Domain Controller](#index_split_061.html_filepos234836)
    *   [4.9-Shut Down & Reboot](#index_split_062.html_filepos236034)
    *   [4.10-Upgrading Zentyal](#index_split_063.html_filepos236462)
    *   [4.11-Joining Zentyal Domains](#index_split_064.html_filepos237316)
        *   [4.11.1-Workgroup Authentication](#index_split_064.html_filepos239120)
        *   [4.11.2-Join The Domain In Windows](#index_split_064.html_filepos242382)
    *   [4.12-Configuration Backups](#index_split_065.html_filepos244007)
*   [.4-Final Thoughts And Thanks](#index_split_066.html_filepos245971)
*   [.5-Additional Resources](#index_split_067.html_filepos247862)

Table of Contents

[Book Description](#index_split_001.html_filepos611)

[Copyright](#index_split_002.html_filepos3388)

[.1-Introduction](#index_split_004.html_filepos17397)

[.2-Before You Begin](#index_split_005.html_filepos26625)

[.3-Best Practices](#index_split_006.html_filepos28974)

[Book 1:  Proxmox VE](#index_split_007.html_filepos50528)

> > [1.1-Introduction To Proxmox](#index_split_007.html_filepos50660)

> > [1.2-Installing Proxmox](#index_split_008.html_filepos52406)

> > [1.3-Initial Login](#index_split_009.html_filepos59739)

> > [1.4-Network Adapters](#index_split_010.html_filepos61979)

> > [1.5-Adding LVM Storage](#index_split_011.html_filepos65541)

> > [1.6-Configure LVM Storage](#index_split_012.html_filepos70296)

> > [1.7-Configure NFS Storage](#index_split_013.html_filepos71958)

> > [1.8-Configure iSCSI Storage](#index_split_014.html_filepos74171)

> > [1.9-Creating VM Configurations](#index_split_015.html_filepos77013)

> > [1.10-VM Backup & Restore](#index_split_016.html_filepos86999)

> > [1.11-VM Hardware](#index_split_017.html_filepos92928)

> > [1.12-Adding Pass-Through Disks](#index_split_018.html_filepos97235)

> > [1.13-Troubleshooting Proxmox](#index_split_019.html_filepos105352)

> > [1.14-Upgrading Proxmox](#index_split_020.html_filepos106161)

[Book 2:  pfSense](#index_split_021.html_filepos107409)

> > [2.1-Introduction To pfSense](#index_split_021.html_filepos107538)

> > [2.2-Installing pfSense](#index_split_022.html_filepos110101)

> > [2.3-Assigning Network Interfaces](#index_split_023.html_filepos112286)

> > [2.3-Assigning IP Addresses](#index_split_024.html_filepos115257)

> > [2.4-Reset Admin Password](#index_split_025.html_filepos118919)

> > [2.5-Web Configuration Wizard](#index_split_026.html_filepos119701)

> > [2.6-Changing Themes](#index_split_027.html_filepos125254)

> > [2.7-Configure DHCP Server](#index_split_028.html_filepos126560)

> > > > > > [2.7.1-WINS, DNS, Gateway, and Domain](#index_split_028.html_filepos128086)

> > > > > > [2.7.2-DHCP Client Reservations](#index_split_028.html_filepos129335)

> > [2.8-Firewall Settings](#index_split_029.html_filepos130789)

> > > > > > [2.8.1-LAN Rules](#index_split_029.html_filepos131340)

> > > > > > [2.8.2-WAN Rules](#index_split_029.html_filepos132607)

> > [2.9-OpenVPN](#index_split_030.html_filepos133813)

> > > > > > [2.9.1-OpenVPN Client Export Utility](#index_split_030.html_filepos134546)

> > > > > > [2.9.2-OpenVPN Setup Wizard](#index_split_030.html_filepos135208)

> > > > > > [2.9.3-OpenVPN Client Connectors](#index_split_030.html_filepos139013)

> > > > > > [2.9.4-Authenticate Zentyal Domain Users](#index_split_030.html_filepos140300)

> > [2.10-Snort IDS](#index_split_031.html_filepos143634)

> > > > > > [2.10.1-Install Snort Package](#index_split_031.html_filepos144780)

> > > > > > [2.10.2-Snort Global Settings](#index_split_031.html_filepos145641)

> > > > > > [2.10.3-Snort Interfaces](#index_split_031.html_filepos146037)

> > > > > > [2.10.4-Updating Threat Rules](#index_split_031.html_filepos148165)

> > > > > > [2.10.5-Threat Rule Categories](#index_split_031.html_filepos148542)

> > > > > > [2.10.6-Add Alerts To Suppression List](#index_split_031.html_filepos149705)

> > > > > > [2.10.7-Block Offenders At Source](#index_split_031.html_filepos150555)

> > [2.11-Configuration Backups](#index_split_032.html_filepos151614)

[Book 3:  freeNAS](#index_split_033.html_filepos153134)

> > [3.1-Traditional Storage Fails](#index_split_033.html_filepos153263)

> > [3.2-freeNAS & ZFS](#index_split_034.html_filepos158684)

> > [3.3-Installing freeNAS](#index_split_035.html_filepos159656)

> > [3.4-Add freeNAS Pass-Through Disks](#index_split_036.html_filepos163763)

> > [3.5-Set Storage For No Backup](#index_split_037.html_filepos165198)

> > [3.6-Start freeNAS Through The Console](#index_split_038.html_filepos166572)

> > [3.7-Initial Login](#index_split_039.html_filepos167436)

> > [3.8-freeNAS Navigation](#index_split_040.html_filepos168229)

> > [3.9-Network Configuration](#index_split_041.html_filepos168671)

> > [3.10-Users And Groups](#index_split_042.html_filepos170783)

> > > > > > [3.10.1-Adding A New User](#index_split_042.html_filepos170894)

> > > > > > [3.10.2-Adding A New Group](#index_split_042.html_filepos172510)

> > [3.11-Add A ZFS Volume](#index_split_043.html_filepos173178)

> > [3.12-Detach And Move Volumes](#index_split_044.html_filepos174244)

> > [3.13-ZFS Datasets](#index_split_045.html_filepos176971)

> > [3.14-ZFS Permissions](#index_split_046.html_filepos180713)

> > [3.15-freeNAS Services](#index_split_047.html_filepos182750)

> > > > > > [3.15.1-CIFS(Windows Sharing) Service](#index_split_047.html_filepos183226)

> > > > > > [3.15.2-NFS(Linux Sharing) Service](#index_split_047.html_filepos184498)

> > > > > > [3.15.3-iSCSI Target Service](#index_split_047.html_filepos185721)

> > > > > > [3.15.4-Rsync(Backup) Service](#index_split_047.html_filepos187083)

> > > > > > [3.15.5-SSH(Secure Shell) Service](#index_split_047.html_filepos188051)

> > [3.16-Add Network Shares](#index_split_048.html_filepos189275)

> > > > > > [3.16.1-NFS Shares](#index_split_048.html_filepos189388)

> > > > > > [3.16.2-Windows Shares](#index_split_048.html_filepos191389)

> > > > > > [3.16.3-iSCSI Target Shares](#index_split_048.html_filepos192766)

> > [3.17-ZFS Snapshot Backups](#index_split_049.html_filepos200154)

> > [3.18-Restore A Snapshot In Windows](#index_split_050.html_filepos203397)

> > [3.19-Rsync Replication](#index_split_051.html_filepos204679)

> > > > > > [3.19.1-Add The Rsync Push Task](#index_split_051.html_filepos206034)

> > > > > > [3.19.2-Add The Rsync Module](#index_split_051.html_filepos210666)

> > > > > > [3.19.3-Tips On Using Rsync](#index_split_051.html_filepos212722)

> > [3.20-Domain Membership](#index_split_052.html_filepos214725)

> > > > > > [3.20.1-Domain Permissions](#index_split_052.html_filepos218609)

> > [3.21-Configuration Backups](#index_split_053.html_filepos219629)

[Book 4:  Zentyal Domain Controller](#index_split_054.html_filepos220923)

> > [4.1-Introduction To Zentyal](#index_split_054.html_filepos221070)

> > [4.2-Installing Zentyal](#index_split_055.html_filepos222574)

> > [4.3-Initial Login](#index_split_056.html_filepos227249)

> > [4.4-Initial Setup](#index_split_057.html_filepos228620)

> > [4.5-Navigating Zentyal](#index_split_058.html_filepos231647)

> > [4.6-Adding Users](#index_split_059.html_filepos232445)

> > [4.7-Adding Groups](#index_split_060.html_filepos233639)

> > [4.8-Additional Domain Controller](#index_split_061.html_filepos234836)

> > [4.9-Shut Down & Reboot](#index_split_062.html_filepos236034)

> > [4.10-Upgrading Zentyal](#index_split_063.html_filepos236462)

> > [4.11-Joining Zentyal Domains](#index_split_064.html_filepos237316)

> > > > > > [4.11.1-Workgroup Authentication](#index_split_064.html_filepos239120)

> > > > > > [4.11.2-Join The Domain In Windows](#index_split_064.html_filepos242382)

> > [4.12-Configuration Backups](#index_split_065.html_filepos244007)

[.4-Final Thoughts And Thanks](#index_split_066.html_filepos245971)

[.5-Additional Resources](#index_split_067.html_filepos247862)