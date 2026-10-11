
## OpenWRT gets native IPv6

### Barrier Breaker release includes shiny new features

Popular embedded distribution OpenWRT has announced a new release which adds fully native support for the Internet Protocol version 6 (IPv6) via DHCP for the first time.

Commonly used to replace the stock software on off-the-shelf router hardware, previous OpenWRT packages have been slowly introducing support for IPv6, starting with the ability to route IPv6 traffic over more common IPv4 connections.

Dubbed “Barrier Breaker”, OpenWRT 14.07 enhances the IPv6 stack with the introduction of DHCPv6, allowing an OpenWRT-based router to receive both IPv4 and IPv6 addresses from a wide-area network provider.

Additional new features include source-constrained routing, router advertisements, and multihoming with local prefix allocations.

Additional tweaks in the latest release include better wireless configuration through netifd, support for dynamic firewall rules and zones, a UCI data validation layer, filesystem tweaks including snapshots and rollbacks, and draft support for self-managing home networks using the HNCP standard.

A new package feed has also been created, due to organisers’ displeasure with the quality of existing feeds.

The Barrier Breaker release uses the 3.10 Linux kernel, with the project leaders stating their intentions to release a Chaos Calmer build before the end of the year with either 3.14 or a newer long-term support (LTS) kernel version.

## EFF launches router OS

### Privacy-focused package unveiled at HOPE X

The Electronic Frontier Foundation has released what it describes as a “hacker alpha” of its planned operating system for routers, part of the privacy group’s Open Wireless Movement.

Linux-based, the Open Wireless Router software has been developed in conjunction with Fight for the Future, Mozilla, Free Press and other privacy advocate groups with the view of providing a simple and easy-to-use means for internet users to help increase their privacy.

The software will, in its final stage, include bandwidth-controlled public and encrypted private wireless networks, offer anonymisation and encryption features, be hardened against attack and feature an auto-update mechanism over a secured connection.

The EFF also promises to include advanced network queueing functionality for reduced latency in time-sensitive applications. This, coupled with the bandwidth controls on the public network side, is hoped to encourage users to open their internet connections to public use without the need for a network key or other authentication measures.

Building on the Caro/WRT project, the early-version alpha currently supports only the Netgear WNDR3800 router. “This release is a work in progress”, the team behind it warned at the unveiling, “and is intended only for developers and people willing to deal with the bleeding edge.”

## THE FREE SOFTWARE COLUMN

### Sense of community

While companies are keen to profit from free and open source software, Richard isn't sure they are looking closely at what makes communities work

![](img/daaca9116bc2b1db669c224de81abc7c_9_0.png)

> **Richard Hittlesey** *writes* about art, music, digital rights, Linux and free software for a variety of publications

As Richard Stallman is careful to explain, open source and free software are two very different concepts (www.gnu.org/philosophy/open-source-misses-the-point.html). While the 'Open Source Initiative' began as a marketing exercise in 1999 to sell free software to corporate enterprises, and open source advocates tended to claim it for themselves, the success of free and open source software in the corporate world was guaranteed by the rise of GNU/Linux, licensed under a copyleft licence.

Free software can be described as 'open source', and much open source software is also 'free software', but these terms are not interchangeable. What distinguishes free software from 'open source' is the concept of the Four Freedoms and the notion of copyleft (read more at www.gnu.org/philosophy/free-sw.html). Copyleft licences, such as the GPL, allow third parties to take the code, repackage it, and pass it on in any form they wish, but ensure reciprocity by obliging those who distribute the code to pass on any changes under the same licence, thus preventing forks and preserving the free and open source nature of the code.

The nature and effect of copyleft was important both to the success of GNU/Linux and its adoption by the former Unix companies, who had had their fingers burnt with the fracturing of Unix and open standards during the Eighties and Nineties. If they had learnt anything from the Unix wars, it was that proprietary operating systems, even if they are your own, cost money and create hurdles for other parts of your business. Unix had been touted as the universal operating system, and each of the Unix companies poured huge resources into developing proprietary versions of the same operating system at the expense of the hardware, service and userland software that were their core businesses.

The arrival of GNU/Linux opened up new possibilities. GNU/Linux was 'owned' by everybody and was licensed under the GPL. Once more than one company had formed a commitment to Linux it became obvious that there was a mutual advantage in contributing back to the project, and they did. The framework that made this possible was the GPL.

The GPL protected the code against forks, and encouraged commodisation, and commodisation reduced costs and benefited everybody. A more permissive licence wouldn't have given this protection and, inevitably, forks would have ensued. The release of core chunks of corporate code accelerated the development of Linux and ensured its success in the enterprise, enhanced by its portability across a wide range of hardware. Dozens of companies contributed to the Linux kernel and gained access to the benefits of the contributions of all the others. This effect has made it possible to port anything to anything at a vastly reduced cost, because the costs are shared. Portability may or may not have been a factor in the original adoption of GNU/Linux, but has worked to the long-term advantage of its many participants, and free and open source software has grown in popularity as a result, with some beneficial consequences. GNU/Linux has fulfilled the promise of Unix without the waste of resources that ensued from the countless incompatible and proprietary variants of Unix.

The contribution of the GPL and copyleft to this success isn't always given due recognition, and there are reasons for this. Companies are still looking for ways that they can monetise the contributions of others without giving back the code, so tend to promote 'open source' or ideas such as 'open core' or copyright assignment, hoping to win the participation of developers without the obligation to return their changes – often so that subsets of the code can be submerged into proprietary offerings.

Advocates of 'open source' in industry too often dismiss copyleft as an unnecessary embellishment, or find a way to subvert its original purpose, but projects do not thrive when there are ambivalences and ambiguities around the leadership and ownership of the code, as was illustrated by the fallout among the various projects that Oracle inherited from Sun Microsystems. Similarly, devices such as dual licensing, copyright assignment and Community Licence Agreements (CLAs), which subvert the common purpose of developers, can strip away the clarity of a project's purpose and act as a disincentive to the sense of community that is the lifeblood of an 'open source' project.

The Linux 'community' of the Nineties, and offshoots like Debian, grew around a piece of software and a licence that promoted reciprocity. They were almost entirely voluntary and spontaneous. The software and the licence were the glue. The sense of community and fun, and the ensuring feeling that anything was possible, were the drivers. It is perhaps a shame that while companies are keen to profit from free and open source software, they do not always look more closely at what makes these communities work.
