![](1260462080.jpg)

![Image](1260462080.jpg)

![Cover Image](title.jpg)

Copyright © 2024 by McGraw Hill. All rights reserved. Except as permitted under the Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of publisher, with the exception that the program listings may be entered, stored, and executed in a computer system, but they may not be reproduced for publication.

ISBN: 978-1-26-046208-1
MHID:      1-26-046208-0

The material in this eBook also appears in the print version of this title: ISBN: 978-1-26-046207-4, MHID: 1-26-046207-2.

eBook conversion by codeMantra
Version 1.0

All trademarks are trademarks of their respective owners. Rather than put a trademark symbol after every occurrence of a trademarked name, we use names in an editorial fashion only, and to the benefit of the trademark owner, with no intention of infringement of the trademark. Where such designations appear in this book, they have been printed with initial caps.

McGraw Hill eBooks are available at special quantity discounts to use as premiums and sales promotions or for use in corporate training programs. To contact a representative, please visit the Contact Us page at [www.mhprofessional.com](http://www.mhprofessional.com).

Information has been obtained by McGraw Hill from sources believed to be reliable. However, because of the possibility of human or mechanical error by our sources, McGraw Hill, or others, McGraw Hill does not guarantee the accuracy, adequacy, or completeness of any information and is not responsible for any errors or omissions or the results obtained from the use of such information.

TERMS OF USE

This is a copyrighted work and McGraw Hill (“McGraw Hill”) and its licensors reserve all rights in and to the work. Use of this work is subject to these terms. Except as permitted under the Copyright Act of 1976 and the right to store and retrieve one copy of the work, you may not decompile, disassemble, reverse engineer, reproduce, modify, create derivative works based upon, transmit, distribute, disseminate, sell, publish or sublicense the work or any part of it without McGraw Hill’s prior consent. You may use the work for your own noncommercial and personal use; any other use of the work is strictly prohibited. Your right to use the work may be terminated if you fail to comply with these terms.

THE WORK IS PROVIDED “AS IS.” McGRAW HILL AND ITS LICENSORS MAKE NO GUARANTEES OR WARRANTIES AS TO THE ACCURACY, ADEQUACY OR COMPLETENESS OF OR RESULTS TO BE OBTAINED FROM USING THE WORK, INCLUDING ANY INFORMATION THAT CAN BE ACCESSED THROUGH THE WORK VIA HYPERLINK OR OTHERWISE, AND EXPRESSLY DISCLAIM ANY WARRANTY, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO IMPLIED WARRANTIES OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE.

McGraw Hill and its licensors do not warrant or guarantee that the functions contained in the work will meet your requirements or that its operation will be uninterrupted or error free. Neither McGraw Hill nor its licensors shall be liable to you or anyone else for any inaccuracy, error or omission, regardless of cause, in the work or for any damages resulting therefrom. McGraw Hill has no responsibility for the content of any information accessed through the work. Under no circumstances shall McGraw Hill and/or its licensors be liable for any indirect, incidental, special, punitive, consequential or similar damages that result from the use of or inability to use the work, even if any of them has been advised of the possibility of such damages. This limitation of liability shall apply to any claim or cause whatsoever whether such claim or cause arises in contract, tort or otherwise.

*For the young widows and widowers: may they find the courage to face their fears, to navigate their way through the pain, and to find hope for a brighter future.*

## ABOUT THE AUTHORS

**Michael Jang** (RHCE, LPIC-2, UCP, LCP, Linux+, MCP) is currently a Lead Technical Writer for Forescout. His experience with computers goes back to the days of jumbled punch cards. He has written other books on Linux certification, including *LPIC-1 in Depth*, *Mike Meyers’ Linux+ Certification Passport*, and *Sair GNU/Linux Installation and Configuration Exam Cram*. His other Linux books include *Linux Annoyances for Geeks*, *Linux Patch Management*, and *Security Strategies in Linux Platforms and Applications.* He has also written or contributed to books on Microsoft operating systems, including *MCSE Guide to Microsoft Windows 98* and *Mastering Windows XP Professional, Second Edition*.

**Alessandro Orsaria** (RHCE, RHCA, CCIE x 2) is an IT professional with more than 20 years’ experience in the industry. He has authored articles for technical Linux magazines and is currently employed by a proprietary trading firm. Alessandro is Red Hat RHCE and RHCA certified and has achieved two Cisco CCIE certifications in Routing & Switching and Datacenter. He holds an MBA from Imperial College of London and a degree in physics.

### About the Technical Editor

Sam Doran is a Principal Software Engineer at Red Hat. He served in the U.S. Air Force as an aircraft mechanic and is a proud alumnus of the Virginia Tech Corps of Cadets. Prior to joining Red Hat, he worked for the U.S. government as well as private industry in jobs ranging from site reliability engineering to information security. He has used RHEL professionally since 2003 as well as a number of other Linux distributions.

## CONTENTS AT A GLANCE

[1     Prepare for the Red Hat RHCSA Certification](#ch01.xhtml)

[2     Fundamental Command-Line Skills](#ch02.xhtml)

[3     Managing Basic Networking](#ch03.xhtml)

[4     Software Management](#ch04.xhtml)

[5     systemd and the Boot Process](#ch05.xhtml)

[6     User Administration](#ch06.xhtml)

[7     Storage and Filesystem Administration](#ch07.xhtml)

[8     Linux Security](#ch08.xhtml)

[9     System Administration Tasks](#ch09.xhtml)

[10   An Introduction to Containers](#ch10.xhtml)

[A    Prepare a System for the Sample Exams](#app01.xhtml)

[B    Solutions to RHCSA Sample Exam 1](#app02.xhtml)

[C    Solutions to RHCSA Sample Exam 2](#app03.xhtml)

[D    About the Online Content](#app04.xhtml)

[Index](#index.xhtml)

## Contents

*[Acknowledgments](#ack.xhtml)*

*[Preface](#preface.xhtml)*

*[Introduction](#intro.xhtml)*

*[RHCSA Exam Readiness Checklist](#intro.xhtml_fm01)*

[1     Prepare for the Red Hat RHCSA Certification](#ch01.xhtml)

[The RHCSA Exam](#ch01.xhtml_lev1)

[The Exam Experience](#ch01.xhtml_lev1sec1)

[Evolving Requirements](#ch01.xhtml_lev1sec2)

[Basic Hardware Requirements](#ch01.xhtml_lev2)

[Hardware Compatibility](#ch01.xhtml_lev1sec3)

[Architectures](#ch01.xhtml_lev1sec4)

[RAM Requirements](#ch01.xhtml_lev1sec5)

[Storage Options](#ch01.xhtml_lev1sec6)

[Networking](#ch01.xhtml_lev1sec7)

[Virtual Machine Options](#ch01.xhtml_lev1sec8)

[Get Red Hat Enterprise Linux](#ch01.xhtml_lev3)

[Get a Subscription at No Cost](#ch01.xhtml_lev1sec9)

[Purchase a Subscription](#ch01.xhtml_lev1sec10)

[Third-Party Rebuilds](#ch01.xhtml_lev1sec11)

[Check the Download](#ch01.xhtml_lev1sec12)

[**Exercise 1-1:** Get Red Hat Enterprise Linux](#ch01.xhtml_exer1-1)

[An Environment for Practice Labs](#ch01.xhtml_lev4)

[System Roles](#ch01.xhtml_lev1sec13)

[Getting VMware Workstation Player](#ch01.xhtml_lev1sec14)

[Virtual Networks on a Hypervisor](#ch01.xhtml_lev1sec15)

[Configure a Virtual Machine on VMware Workstation Player](#ch01.xhtml_lev1sec16)

[RHEL 9 Installation](#ch01.xhtml_lev5)

[Boot Media](#ch01.xhtml_lev1sec17)

[Basic Installation Steps](#ch01.xhtml_lev1sec18)

[The Installation Perspective on Partitions](#ch01.xhtml_lev1sec19)

[Partition Creation Exercise](#ch01.xhtml_lev1sec20)

[**Exercise 1-2:** Partitioning During Installation](#ch01.xhtml_exer1-2)

[Wow, Look at All That Software!](#ch01.xhtml_lev1sec21)

[Baseline Packages](#ch01.xhtml_lev1sec22)

[During the Installation](#ch01.xhtml_lev1sec23)

[Initial Setup](#ch01.xhtml_lev1sec24)

[Certification Summary](#ch01.xhtml_lev1sec25)

![Images](tick-a.jpg) [Two-Minute Drill](#ch01.xhtml_lev1sec26)

Q&A [Self Test](#ch01.xhtml_lev1sec27)

[Lab Questions](#ch01.xhtml_lev1sec28)

[Self Test Answers](#ch01.xhtml_lev1sec29)

[Lab Answers](#ch01.xhtml_lev1sec30)

[2     Fundamental Command-Line Skills](#ch02.xhtml)

[Shells](#ch02.xhtml_lev6)

[Other Shells](#ch02.xhtml_lev1sec31)

[Virtual Consoles](#ch02.xhtml_lev1sec32)

[GUI Shell Interfaces](#ch02.xhtml_lev1sec33)

[Differences Between Regular and Administrative Users](#ch02.xhtml_lev1sec34)

[Standard Streams and Command Redirection](#ch02.xhtml_lev1sec35)

[Standard Command-Line Tools](#ch02.xhtml_lev7)

[File and Directory Concepts](#ch02.xhtml_lev1sec36)

[File Lists and ls](#ch02.xhtml_lev1sec37)

[File-Creation Commands](#ch02.xhtml_lev1sec38)

[Wildcards](#ch02.xhtml_lev1sec39)

[File Searches](#ch02.xhtml_lev1sec40)

[File Permissions](#ch02.xhtml_lev8)

[File Permissions and Ownership](#ch02.xhtml_lev1sec41)

[Commands to Change Permissions and Ownership](#ch02.xhtml_lev1sec42)

[A Basic Introduction of User and Group Concepts](#ch02.xhtml_lev1sec43)

[Managing Text Files](#ch02.xhtml_lev9)

[Commands to Read Text Streams](#ch02.xhtml_lev1sec44)

[Commands to Process Text Streams](#ch02.xhtml_lev1sec45)

[Edit Text Files at the Console](#ch02.xhtml_lev1sec46)

[**Exercise 2-1:** Using vi to Create a New User](#ch02.xhtml_exer2-1)

[If You Don’t Like vi](#ch02.xhtml_lev1sec47)

[Edit Text Files in the GUI](#ch02.xhtml_lev1sec48)

[Accessing the Documentation](#ch02.xhtml_lev10)

[When You Need Help](#ch02.xhtml_lev1sec49)

[A Variety of man Pages](#ch02.xhtml_lev1sec50)

[The info Manuals](#ch02.xhtml_lev1sec51)

[Detailed Documentation in /usr/share/doc](#ch02.xhtml_lev1sec52)

[Certification Summary](#ch02.xhtml_lev1sec53)

![Images](tick-a.jpg) [Two-Minute Drill](#ch02.xhtml_lev1sec54)

Q&A [Self Test](#ch02.xhtml_lev1sec55)

[Lab Questions](#ch02.xhtml_lev1sec56)

[Self Test Answers](#ch02.xhtml_lev1sec57)

[Lab Answers](#ch02.xhtml_lev1sec58)

[3     Managing Basic Networking](#ch03.xhtml)

[A Networking Primer](#ch03.xhtml_lev11)

[IPv4 Networks](#ch03.xhtml_lev1sec59)

[Networks and Routing](#ch03.xhtml_lev1sec60)

[Tools and Commands](#ch03.xhtml_lev1sec61)

[Network Configuration and Troubleshooting](#ch03.xhtml_lev12)

[Network Configuration Services](#ch03.xhtml_lev1sec62)

[Network Configuration Tools](#ch03.xhtml_lev1sec63)

[**Exercise 3-1:** Configure IPv4 Settings on a Network Interface](#ch03.xhtml_exer3-1)

[Configure Name Resolution](#ch03.xhtml_lev1sec64)

[Hostname Configuration Files](#ch03.xhtml_lev1sec65)

[An Introduction to IPv6](#ch03.xhtml_lev13)

[Basic IPv6 Addressing](#ch03.xhtml_lev1sec66)

[Troubleshooting Tools](#ch03.xhtml_lev1sec67)

[Configure IPv6 Addresses](#ch03.xhtml_lev1sec68)

[Administration with Secure Shell and Secure Copy](#ch03.xhtml_lev14)

[Command-Line Access](#ch03.xhtml_lev1sec69)

[More SSH Command-Line Tools](#ch03.xhtml_lev1sec70)

[Graphical Secure Shell Access](#ch03.xhtml_lev1sec71)

[Certification Summary](#ch03.xhtml_lev1sec72)

![Images](tick-a.jpg) [Two-Minute Drill](#ch03.xhtml_lev1sec73)

Q&A [Self Test](#ch03.xhtml_lev1sec74)

[Lab Questions](#ch03.xhtml_lev1sec75)

[Self Test Answers](#ch03.xhtml_lev1sec76)

[Lab Answers](#ch03.xhtml_lev1sec77)

[4     Software Management](#ch04.xhtml)

[The RPM Package Manager](#ch04.xhtml_lev15)

[What Is a Package?](#ch04.xhtml_lev1sec78)

[What Is the RPM Database?](#ch04.xhtml_lev1sec79)

[What Is a Repository?](#ch04.xhtml_lev1sec80)

[Install an RPM Package](#ch04.xhtml_lev1sec81)

[Uninstall an RPM Package](#ch04.xhtml_lev1sec82)

[Install RPMs from Remote Systems](#ch04.xhtml_lev1sec83)

[RPM Installation Security](#ch04.xhtml_lev1sec84)

[Updating the Kernel](#ch04.xhtml_lev1sec85)

[More RPM Commands](#ch04.xhtml_lev16)

[Package Queries](#ch04.xhtml_lev1sec86)

[Package Signatures](#ch04.xhtml_lev1sec87)

[File Verification](#ch04.xhtml_lev1sec88)

[**Exercise 4-1:** Practice with rpm Commands](#ch04.xhtml_exer4-1)

[Dependencies and the dnf Command](#ch04.xhtml_lev17)

[An Example of Dependency Hell](#ch04.xhtml_lev1sec89)

[Relief from Dependency Hell](#ch04.xhtml_lev1sec90)

[Red Hat Subscription Management](#ch04.xhtml_lev1sec91)

[**Exercise 4-2:** Subscribe a System to Red Hat Subscription Management](#ch04.xhtml_exer4-2)

[Basic dnf Configuration](#ch04.xhtml_lev1sec92)

[**Exercise 4-3:** Create a dnf Repository from the RHEL 9 DVD](#ch04.xhtml_exer4-3)

[Third-Party Repositories](#ch04.xhtml_lev1sec93)

[**Exercise 4-4:** Configure Access to the EPEL Repository](#ch04.xhtml_exer4-4)

[Basic dnf Commands](#ch04.xhtml_lev1sec94)

[Installation Mode](#ch04.xhtml_lev1sec95)

[Security and dnf](#ch04.xhtml_lev1sec96)

[Updates and Security Fixes](#ch04.xhtml_lev1sec97)

[Package Groups and dnf](#ch04.xhtml_lev1sec98)

[More dnf Commands](#ch04.xhtml_lev1sec99)

[Module Streams (*)](#ch04.xhtml_lev18)

[Certification Summary](#ch04.xhtml_lev1sec100)

![Images](tick-a.jpg) [Two-Minute Drill](#ch04.xhtml_lev1sec101)

Q&A [Self Test](#ch04.xhtml_lev1sec102)

[Lab Questions](#ch04.xhtml_lev1sec103)

[Self Test Answers](#ch04.xhtml_lev1sec104)

[Lab Answers](#ch04.xhtml_lev1sec105)

[5     systemd and the Boot Process](#ch05.xhtml)

[The Boot Process](#ch05.xhtml_lev19)

[Basic System Configuration](#ch05.xhtml_lev1sec106)

[Startup Menus](#ch05.xhtml_lev1sec107)

[Access to Linux Bootloaders](#ch05.xhtml_lev1sec108)

[Bootloaders and GRUB 2](#ch05.xhtml_lev20)

[GRUB, the GRand Unified Bootloader](#ch05.xhtml_lev1sec109)

[**Exercise 5-1:** Boot into a Different Target](#ch05.xhtml_exer5-1)

[**Exercise 5-2:** Recover the Root Password](#ch05.xhtml_exer5-2)

[Modify the System Bootloader](#ch05.xhtml_lev1sec110)

[How to Update GRUB 2](#ch05.xhtml_lev1sec111)

[The GRUB 2 Command Line](#ch05.xhtml_lev1sec112)

[**Exercise 5-3:** Using the GRUB 2 Command Line](#ch05.xhtml_exer5-3)

[An Option for Booting from GRUB 2: Rescue Mode](#ch05.xhtml_lev1sec113)

[Between GRUB 2 and Login](#ch05.xhtml_lev21)

[Kernels and the Initial RAM Disk](#ch05.xhtml_lev1sec114)

[The First Process, Targets, and Units](#ch05.xhtml_lev1sec115)

[Switch Between Targets](#ch05.xhtml_lev1sec116)

[Reboot and Shut Down a System Normally](#ch05.xhtml_lev1sec117)

[systemd Replaces Upstart and SysVinit](#ch05.xhtml_lev1sec118)

[systemd Units](#ch05.xhtml_lev1sec119)

[Virtual Consoles and Login Screens](#ch05.xhtml_lev1sec120)

[Control by Target](#ch05.xhtml_lev22)

[Functionality by Target](#ch05.xhtml_lev1sec121)

[The Innards of systemd Units](#ch05.xhtml_lev1sec122)

[Service Configuration](#ch05.xhtml_lev1sec123)

[Time Synchronization](#ch05.xhtml_lev23)

[Time Zone Configuration](#ch05.xhtml_lev1sec124)

[Sync the Time with chronyd](#ch05.xhtml_lev1sec125)

[Certification Summary](#ch05.xhtml_lev1sec126)

![Images](tick-a.jpg) [Two-Minute Drill](#ch05.xhtml_lev1sec127)

Q&A [Self Test](#ch05.xhtml_lev1sec128)

[Lab Questions](#ch05.xhtml_lev1sec129)

[Self Test Answers](#ch05.xhtml_lev1sec130)

[Lab Answers](#ch05.xhtml_lev1sec131)

[6     User Administration](#ch06.xhtml)

[User Account Management](#ch06.xhtml_lev24)

[Different Kinds of Users](#ch06.xhtml_lev1sec132)

[The Shadow Password Suite](#ch06.xhtml_lev1sec133)

[Command-Line Tools](#ch06.xhtml_lev1sec134)

[**Exercise 6-1:** Add a User with Cockpit Web Console](#ch06.xhtml_exer6-1)

[**Exercise 6-2:** Real and Fake Shells](#ch06.xhtml_exer6-2)

[Modify an Account](#ch06.xhtml_lev1sec135)

[Administrative Control](#ch06.xhtml_lev25)

[The Ability to Log In](#ch06.xhtml_lev1sec136)

[The su Command](#ch06.xhtml_lev1sec137)

[Limit Access to su](#ch06.xhtml_lev1sec138)

[The sg Command](#ch06.xhtml_lev1sec139)

[Superuser Access with the sudo Command](#ch06.xhtml_lev1sec140)

[User and Shell Configuration](#ch06.xhtml_lev26)

[Home Directories and /etc/skel](#ch06.xhtml_lev1sec141)

[**Exercise 6-3:** Another Way to Secure a System](#ch06.xhtml_exer6-3)

[Shell Configuration Files in User Home Directories](#ch06.xhtml_lev1sec142)

[Login, Logout, and User Switching](#ch06.xhtml_lev1sec143)

[Special Groups](#ch06.xhtml_lev27)

[Standard and Red Hat Groups](#ch06.xhtml_lev1sec144)

[Shared Directories](#ch06.xhtml_lev1sec145)

[**Exercise 6-4:** Control Group Ownership with the SGID Bit](#ch06.xhtml_exer6-4)

[Certification Summary](#ch06.xhtml_lev1sec146)

![Images](tick-a.jpg) [Two-Minute Drill](#ch06.xhtml_lev1sec147)

Q&A [Self Test](#ch06.xhtml_lev1sec148)

[Lab Questions](#ch06.xhtml_lev1sec149)

[Self Test Answers](#ch06.xhtml_lev1sec150)

[Lab Answers](#ch06.xhtml_lev1sec151)

[7     Storage and Filesystem Administration](#ch07.xhtml)

[Storage Management and Partitions](#ch07.xhtml_lev28)

[Current System State](#ch07.xhtml_lev1sec152)

[The fdisk Utility](#ch07.xhtml_lev1sec153)

[The gdisk Utility](#ch07.xhtml_lev1sec154)

[The parted Utility](#ch07.xhtml_lev1sec155)

[Using parted: Starting, Getting Help, and Quitting](#ch07.xhtml_lev1sec156)

[Graphical Options](#ch07.xhtml_lev1sec157)

[**Exercise 7-1:** Work with fdisk and parted](#ch07.xhtml_exer7-1)

[Filesystem Formats](#ch07.xhtml_lev29)

[Standard Filesystems](#ch07.xhtml_lev1sec158)

[Journaling Filesystems](#ch07.xhtml_lev1sec159)

[Filesystem Format Commands](#ch07.xhtml_lev1sec160)

[Swap Volumes](#ch07.xhtml_lev1sec161)

[Filesystem Check Commands](#ch07.xhtml_lev1sec162)

[**Exercise 7-2:** Format, Check, and Mount Different Filesystems](#ch07.xhtml_exer7-2)

[Basic Linux Filesystems and Directories](#ch07.xhtml_lev30)

[Separate Linux Filesystems](#ch07.xhtml_lev1sec163)

[Directories That Can Be Mounted Separately](#ch07.xhtml_lev1sec164)

[Logical Volume Manager (LVM)](#ch07.xhtml_lev31)

[Definitions in LVM](#ch07.xhtml_lev1sec165)

[Create a Physical Volume](#ch07.xhtml_lev1sec166)

[Create a Volume Group](#ch07.xhtml_lev1sec167)

[Create a Logical Volume](#ch07.xhtml_lev1sec168)

[Make Use of a Logical Volume](#ch07.xhtml_lev1sec169)

[More LVM Commands](#ch07.xhtml_lev1sec170)

[Remove a Logical Volume](#ch07.xhtml_lev1sec171)

[Resize Logical Volumes](#ch07.xhtml_lev1sec172)

[Filesystem Management](#ch07.xhtml_lev32)

[The /etc/fstab File](#ch07.xhtml_lev1sec173)

[Universally Unique Identifiers in /etc/fstab](#ch07.xhtml_lev1sec174)

[The mount Command](#ch07.xhtml_lev1sec175)

[More Filesystem Mount Options](#ch07.xhtml_lev1sec176)

[Virtual Filesystems](#ch07.xhtml_lev1sec177)

[Add Your Own Filesystems to /etc/fstab](#ch07.xhtml_lev1sec178)

[Removable Media and /etc/fstab](#ch07.xhtml_lev1sec179)

[Network Filesystems](#ch07.xhtml_lev1sec180)

[The Automounter](#ch07.xhtml_lev33)

[Mounting via the Automounter](#ch07.xhtml_lev1sec181)

[**Exercise 7-3:** Configure the Automounter](#ch07.xhtml_exer7-3)

[Certification Summary](#ch07.xhtml_lev1sec182)

![Images](tick-a.jpg) [Two-Minute Drill](#ch07.xhtml_lev1sec183)

Q&A [Self Test](#ch07.xhtml_lev1sec184)

[Lab Questions](#ch07.xhtml_lev1sec185)

[Self Test Answers](#ch07.xhtml_lev1sec186)

[Lab Answers](#ch07.xhtml_lev1sec187)

[8     Linux Security](#ch08.xhtml)

[Basic Firewall Control](#ch08.xhtml_lev34)

[Standard Ports](#ch08.xhtml_lev1sec188)

[The firewalld Service](#ch08.xhtml_lev1sec189)

[**Exercise 8-1:** Adjust Firewall Settings](#ch08.xhtml_exer8-1)

[**Exercise 8-2:** Firewall Configuration with the Cockpit Web Console](#ch08.xhtml_exer8-2)

[Securing SSH with Key-Based Authentication](#ch08.xhtml_lev35)

[SSH Configuration Commands](#ch08.xhtml_lev1sec190)

[SSH Client Configuration Files](#ch08.xhtml_lev1sec191)

[Basic Encrypted Communication](#ch08.xhtml_lev1sec192)

[Set Up a Private/Public Pair for Key-Based Authentication](#ch08.xhtml_lev1sec193)

[A Security-Enhanced Linux Primer](#ch08.xhtml_lev36)

[Basic Features of SELinux](#ch08.xhtml_lev1sec194)

[SELinux Status](#ch08.xhtml_lev1sec195)

[SELinux Configuration at the Command Line](#ch08.xhtml_lev1sec196)

[Configure Basic SELinux Settings](#ch08.xhtml_lev1sec197)

[Configure Regular Users for SELinux](#ch08.xhtml_lev1sec198)

[Manage SELinux Boolean Settings](#ch08.xhtml_lev1sec199)

[List and Identify SELinux File Contexts](#ch08.xhtml_lev1sec200)

[Restore SELinux File Contexts](#ch08.xhtml_lev1sec201)

[**Exercise 8-3:** Configure a New Directory with Appropriate SELinux Contexts](#ch08.xhtml_exer8-3)

[SELinux Port Labeling](#ch08.xhtml_lev1sec202)

[Identify SELinux Process Contexts](#ch08.xhtml_lev1sec203)

[Diagnose and Address SELinux Policy Violations](#ch08.xhtml_lev1sec204)

[The GUI SELinux Administration Tool](#ch08.xhtml_lev1sec205)

[Certification Summary](#ch08.xhtml_lev1sec206)

![Images](tick-a.jpg) [Two-Minute Drill](#ch08.xhtml_lev1sec207)

Q&A [Self Test](#ch08.xhtml_lev1sec208)

[Lab Questions](#ch08.xhtml_lev1sec209)

[Self Test Answers](#ch08.xhtml_lev1sec210)

[Lab Answers](#ch08.xhtml_lev1sec211)

[9     System Administration Tasks](#ch09.xhtml)

[Resource Management and System Tuning](#ch09.xhtml_lev37)

[System Resource Management Commands](#ch09.xhtml_lev1sec212)

[System Tuning Profiles](#ch09.xhtml_lev1sec213)

[Archives and Compression](#ch09.xhtml_lev38)

[gzip and bzip2](#ch09.xhtml_lev1sec214)

[tar](#ch09.xhtml_lev1sec215)

[star](#ch09.xhtml_lev1sec216)

[Running Tasks on a Schedule: cron and at](#ch09.xhtml_lev39)

[The System crontab and Components](#ch09.xhtml_lev1sec217)

[Hourly cron Jobs](#ch09.xhtml_lev1sec218)

[Regular anacron Jobs](#ch09.xhtml_lev1sec219)

[Setting Up cron for Users](#ch09.xhtml_lev1sec220)

[**Exercise 9-1:** Create a cron Job](#ch09.xhtml_exer9-1)

[Running a Job with the at System](#ch09.xhtml_lev1sec221)

[Secure cron and at](#ch09.xhtml_lev1sec222)

[Bash Scripts](#ch09.xhtml_lev40)

[A “Hello, World” Script](#ch09.xhtml_lev1sec223)

[Bash Variables](#ch09.xhtml_lev1sec224)

[Bash Control Structures](#ch09.xhtml_lev1sec225)

[**Exercise 9-2:** Create a Script](#ch09.xhtml_exer9-2)

[Local Log Files](#ch09.xhtml_lev41)

[System Log Configuration File](#ch09.xhtml_lev1sec226)

[Log File Management](#ch09.xhtml_lev1sec227)

[A Variety of Log Files](#ch09.xhtml_lev1sec228)

[Service-Specific Logs](#ch09.xhtml_lev1sec229)

[**Exercise 9-3:** Learn the Log Files](#ch09.xhtml_exer9-3)

[View systemd Journal Log Entries](#ch09.xhtml_lev1sec230)

[Certification Summary](#ch09.xhtml_lev1sec231)

![Images](tick-a.jpg) [Two-Minute Drill](#ch09.xhtml_lev1sec232)

Q&A [Self Test](#ch09.xhtml_lev1sec233)

[Lab Questions](#ch09.xhtml_lev1sec234)

[Self Test Answers](#ch09.xhtml_lev1sec235)

[Lab Answers](#ch09.xhtml_lev1sec236)

[10   An Introduction to Containers](#ch10.xhtml)

[Fundamentals of Container Technology](#ch10.xhtml_lev42)

[The Rise of Container Technologies](#ch10.xhtml_lev1sec237)

[Virtualization and Containers](#ch10.xhtml_lev1sec238)

[Understanding Container Architecture](#ch10.xhtml_lev1sec239)

[Docker and Podman](#ch10.xhtml_lev1sec240)

[Getting Started with Containers](#ch10.xhtml_lev43)

[Installing Container Tools](#ch10.xhtml_lev1sec241)

[Running Your First Container](#ch10.xhtml_lev1sec242)

[Rootless and Rootful Containers](#ch10.xhtml_lev1sec243)

[Building and Using Container Images](#ch10.xhtml_lev44)

[Image Registries](#ch10.xhtml_lev1sec244)

[Building Container Images: A Primer](#ch10.xhtml_lev1sec245)

[**Exercise 10-1:** Building and Running a Container Image](#ch10.xhtml_exer10-1)

[**Exercise 10-2:** Uploading an Image to Quay.io](#ch10.xhtml_exer10-2)

[Managing Containers](#ch10.xhtml_lev45)

[Podman Commands](#ch10.xhtml_lev1sec246)

[Running a Container as a SystemD Service](#ch10.xhtml_lev1sec247)

[**Exercise 10-3:** Running a Container as a Service](#ch10.xhtml_exer10-3)

[Persistent Storage](#ch10.xhtml_lev1sec248)

[**Exercise 10-4:** Attaching Persistent Storage to a Container](#ch10.xhtml_exer10-4)

[Certification Summary](#ch10.xhtml_lev1sec249)

![Images](tick-a.jpg) [Two-Minute Drill](#ch10.xhtml_lev1sec250)

Q&A [Self Test](#ch10.xhtml_lev1sec251)

[Lab Questions](#ch10.xhtml_lev1sec252)

[Self Test Answers](#ch10.xhtml_lev1sec253)

[Lab Answers](#ch10.xhtml_lev1sec254)

[**A   Prepare a System for the Sample Exams**](#app01.xhtml)

[Sample Exam System Requirements](#app01.xhtml_lev46)

[**B   Solutions to RHCSA Sample Exam 1**](#app02.xhtml)

[RHCSA Sample Exam 1 Discussion](#app02.xhtml_lev47)

[**C   Solutions to RHCSA Sample Exam 2**](#app03.xhtml)

[RHCSA Sample Exam 2 Discussion](#app03.xhtml_lev48)

[**D   About the Online Content**](#app04.xhtml)

[Single User License Terms and Conditions](#app04.xhtml_lev49)

[Downloadable Book Resources](#app04.xhtml_lev50)

[Lab Files](#app04.xhtml_lev1sec255)

[Appendix A: Prepare a System for the Sample Exams](#app04.xhtml_lev1sec256)

[Sample Exams](#app04.xhtml_lev1sec257)

[Technical Support](#app04.xhtml_lev51)

**[Index](#index.xhtml)**

## ACKNOWLEDGMENTS

I’d like to thank Ed Tittel, who gave me my first chance to write for publication, as well as Tim Green, for helping me write what BookAuthority has named the best Red Hat Linux book of all time! I’d also like to thank various mentors over the years: Penny Yao, Susan Tacker, Mark Craig, and Carole Jelen for supporting my work. I’d also like to thank Alessandro Orsaria for taking on the work required to update this book. We would not have the last two editions without him. I’d like to pay tribute to my dog, Katie, who was this man’s best friend for 15 years. Most importantly, I’d like to thank my sweet wife, Donna; you are the love of my life.

—Mike Jang

My profound appreciation extends to Mike Jang and Tim Green, whose confidence in my abilities enabled me to contribute to the eighth edition of this book. I also wish to extend my gratitude to the editorial team of McGraw Hill, whose stellar efforts have been indispensable. To Emiliano and Julia, whose unwavering support was my beacon during the arduous process of creating this work, I offer my deepest thanks and love. A final thought goes to Maria, for her constant support in all that I have done.

—Alessandro Orsaria

## PREFACE

Linux is booming, and Red Hat is leading this growth with the help of skilled Red Hat Certified Systems Administrators (RHCSA).

Linux, which is free, became popular because it offered companies a cheaper alternative to the more costly Unix systems. But Linux has more to offer than just cost savings. Thanks to the Linux community, this operating system works well with many kinds of hardware. Today, you can use Linux on everything from laptops and mobile devices to servers and mainframes. This makes Linux a versatile option for many different situations.

Linux is also known for its strong security. Because it is open source, any security problems can be quickly found and fixed by the community. Linux also has strong rules about permissions and access, which makes it tough for harmful software to break in. Regular updates also help keep Linux safe and secure.

Linux also provides good support for virtualization, which lets users create and manage virtual machines (VMs) efficiently. With tools like Kernel-based Virtual Machine (KVM) and Xen, Linux allows users to run more than one operating system at the same time on a single machine. This is really useful in server environments, where virtualization makes things like software deployment and resource management easier.

On top of this, Linux is the go-to platform for container technologies like Docker and Kubernetes. Containers create isolated environments for applications, making them easier to move and run on different systems. Linux’s built-in features, such as namespaces and cgroups, are the backbone of containerization. These features make it easier to manage resources, isolate processes, and scale up. By bringing together Linux and containerization, software development and deployment have become faster and more efficient.

Having discussed the diverse capabilities and advantages of Linux, it’s essential to recognize the challenges that come with mastering it. Red Hat exams, for instance, are tough, and not many first-time test-takers pass the RHCSA exam. But don’t let that scare you. While passing isn’t guaranteed, this book is designed to help you prepare for and hopefully pass the RHCSA exam. The skills described in this book can also help you in your job as a Linux administrator. However, this book isn’t a replacement for the Red Hat prep courses, which we’ll talk about soon.

To prepare for the RHCSA exam, you should have a laptop or computer with at least 8GB of RAM so that you can run a couple of virtual machines. It doesn’t matter whether your computer runs Linux, Windows, or macOS; you simply need to be able to create two VMs. In this book, we use VMware Workstation Player as our hypervisor, but you can choose another option like KVM, especially if you’re running Linux on your computer. You could also use cloud instances for the labs and exercises in this book, although some cloud providers’ version of Red Hat Enterprise Linux might be slightly different from the standard one. You might also be unable to do some tasks, like installing the operating system from an ISO image. For these reasons, we recommend installing VMware Workstation Player, as explained in [Chapter 1](#ch01.xhtml), or another hypervisor of your choice.

### Getting Red Hat Enterprise Linux

Red Hat exams, including the RHCSA, test your proficiency with Red Hat Enterprise Linux. You might believe that you need to buy a subscription to RHEL to meet the exam objectives, such as installing software packages and updates via Red Hat Subscription Management (RHSM). However, Red Hat currently provides a no-cost Developer Subscription for Individuals if you join the Red Hat Developer program. This subscription includes access to Red Hat Enterprise Linux and a variety of other technologies. Joining the program, which you can do for free at [https://developers.redhat.com/register](https://developers.redhat.com/register), is the only requirement. [Chapter 1](#ch01.xhtml) provides detailed instructions on how to join and install Red Hat Enterprise Linux.

Alternatively, you can choose to install one of the many derivatives of Red Hat Enterprise Linux. These derivatives are built from the RHEL source code, which is mostly released under the Linux General Public License (GPL) or other open-source licenses. These licenses grant anyone the right to construct Red Hat Enterprise Linux from the released Red Hat source code. However, if you’re comfortable with the terms and conditions of the Red Hat Developer program, there’s no clear advantage to using a derivative distribution for RHCSA exam preparation.

Red Hat also provides several Enterprise Linux subscriptions. While not required for RHCSA exam prep, familiarity with these can be beneficial if you plan to (or already) work with Red Hat Enterprise Linux systems:

![Images](square.jpg)   RHEL Server provides varying levels of support for three different CPU architectures, with costs based on the number of CPU sockets and supported virtual guests.

![Images](square.jpg)   RHEL Workstation includes varying levels of support ideal for workstation use.

![Images](square.jpg)   RHEL Developer Suite offers download access to RHEL 9 and several additional software packages, intended solely for development.

![Images](square.jpg)   RHEL add-ons enhance functionality in areas such as high availability, resilient storage, and load balancing, among others.

This book was developed using RHEL 9.1 Server. While RHEL’s source code is open source, access to the binary packages requires a subscription. This can be free of charge if you select the Red Hat Developer Subscription for Individuals.

Enterprise-level operating systems like RHEL 9 offer the benefit of stability. When an enterprise upgrades to RHEL 9, they can trust that configuration revisions will be a one-time affair, with security updates and bug fixes handled automatically. Red Hat strives to ensure enterprises won’t need to overhaul their systems for minor releases, such as RHEL 9.1\. A necessity to reconfigure for minor updates would escalate costs.

Minor releases also should not impact Red Hat exam objectives. While RHEL 9.2 introduces bug fixes, security updates, and new features, it doesn’t alter the defaults of any configuration files detailed in this book.

We expect future minor releases, such as RHEL 9.3, RHEL 9.4, and beyond, to follow this pattern. Our close monitoring of RHEL releases over the past ten years suggests no significant exam objective changes based solely on a minor release. Still, you should routinely check the exam objectives listed on the Red Hat website to ensure they align with the content of this study guide.

### In This Book

[Chapter 1](#ch01.xhtml) of this book is designed to assist you in preparing a study system for the RHCSA exam and offers detailed insight into the exam experience.

Except for [Chapter 1](#ch01.xhtml), every chapter begins by outlining the objectives pertinent to that chapter’s material. Following this, the topics are dissected and explained. We have chosen to present the topics in an order that we believe will be most beneficial to the majority of candidates, which doesn’t necessarily follow the sequence of the exam objectives. However, if you are already well-versed with Linux, feel free to skip over certain sections or entire chapters during your initial reading.

Toward the end of each chapter, we’ve included a Self Test, a series of questions, along with their answers. While Red Hat exams don’t typically involve multiple-choice questions, these types of questions can still be a valuable tool in assessing your understanding and retention of the chapter material. Furthermore, the short-answer questions format emphasizes the practical experience necessary for the exam.

Following this Self Test is a “Lab Questions” section that directs you to the companion website to access the lab exercises for the chapter. The solutions to the lab exercises are included in the book, at the end of each chapter. Please see Appendix D, “About the Online Content.”

Remember, Red Hat exams are hands-on. Therefore, practice is key. You should repeatedly exercise your skills until you reach a level of confidence where you can complete tasks without the assistance of this book. The Red Hat RHCSA exam is designed to test candidate qualifications as Linux systems administrators. If you pass the exam, it’s not because you’ve memorized a canned set of answers—it’s because you have a set of Linux administrative skills and know how to use them under pressure, whether it be during an exam or in a real-world situation.

While this book is organized to serve as an in-depth review for the RHCSA exam for both experienced Linux and Unix professionals, it is not intended as a substitute for Red Hat courses—or, more important, real-world experience. Nevertheless, each chapter covers a major aspect of the exam, with an emphasis on the “why” as well as the “how to” of working with and supporting RHEL as a systems administrator or engineer.

### Conventions and Abbreviations

Although logging in to the root user account is a risky practice on production systems, it is the fastest way to administer RHEL during the exam. The command prompt assumes use of that account. When logged in to the root account, you’ll see a command-line prompt similar to the following:

`[root@server1 root]#`

As the length of this prompt would lead to a number of broken and wrapped code lines throughout this book, we’ve normally abbreviated the root account prompt as

`#`

Be careful. The hash mark (#) is also used as a comment character in Linux scripts and programs. When logged in as a regular user, you will see a slightly different prompt; for user michael, it would typically look like the following:

`[michael@server1 michael]$`

Similarly, we’ve abbreviated this as

`$`

There are a number of command lines and blocks of code interspersed throughout the chapters. Commands embedded within regular text, such as **ls -l**, are shown in bold. User entries and some variables in regular text are also shown in bold.

Sometimes commands exceed the available length of a line. Take this example:

`# virt-install -n outsider1.example.org -r 1024 --disk`

`path=/var/lib/libvirt/images/outsider1.example.org.img,size=16`

`-l ftp://192.168.122.1/pub/inst -x ks=ftp://192.168.122.1/pub/ks1.cfg`

Unless this command is carefully formatted, line breaks might appear in unfortunate places, such as between the two dashes in front of the **--disk** switch. One way to address this is with the backslash (\), which “escapes” the meaning of the carriage return that follows. (The backslash can also “escape” the meaning of a space, making it easier to work with multiple-word filenames.) Therefore, while the following command appears as if it is on four different lines, the backslashes mean that Linux reads it as one single command:

`# virt-install -n outsider1.example.org -r 1024 --disk \`

`> path=/var/lib/libvirt/images/outsider1.example.org.img,size=16 \`

`> -l ftp://192.168.122.1/pub/inst \`

`> -x ks=ftp://192.168.122.1/pub/ks1.cfg`

In some code snippets, we could not use the backslash character to split the output on more than one line. In those cases, we used a continuation arrow, as shown next:

![Images](f0xxv-01.jpg)

Sometimes, you’ll need to actually type in a command or a response to a question at a command line. In that case, you’ll see an instruction such as “Type **y**.” Alternatively, some menus require a keypress; for instance, you may be asked to press *p* to access a password prompt. In that case, the letter *p* is not added to the screen when you press that key. In addition, the *a*, despite its appearances, is in lowercase. In contrast, *A* is the uppercase version of that letter.

One area where some publishers have trouble is with the double-dash. Some publishing programs change the double-dash to an em dash (—). But that can be a problem. The double-dash is common in many Linux commands. For example, the following command lists all packages currently installed on the local system:

`# rpm --query --all`

When we ran this command on our RHEL 9 systems, it listed over 1000 packages.

In contrast, the following command lists all files in all packages on the local system:

`# rpm --query -all`

When we ran this command on our RHEL 9 system, it listed over 150,000 files, a rather different result. So pay attention to the dashes, and rest assured that the team who produced this book took care to make sure that double-dashes are shown as is!

### Exam Readiness Checklist

At the end of the Introduction, you will find an Exam Readiness Checklist. This table has been constructed to allow you to cross-reference the official RHCSA exam objectives with the objectives as they are presented and covered in this book. The checklist also allows you to gauge your level of expertise on each objective at the outset of your studies. This should allow you to check your progress and make sure you spend the time you need on more difficult or unfamiliar sections. The checklist lists all the objectives exactly as Red Hat presents them ([www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam?section=objectives](http://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam?section=objectives)) and cross-references the corresponding coverage in this book, including chapter and page references. Additionally, the table features a column of blank boxes next to each objective. Readers can check these boxes when they feel confident that they are prepared for that specific exam objective.

### In Every Chapter

For this series, we’ve created a set of chapter components that calls your attention to important items, reinforces important points, and provides helpful exam-taking hints. Take a look at what you’ll find in every chapter:

![Images](square.jpg)   Every chapter begins with the **Certification Objectives—**the skills you need to master in order to pass the section on the exam associated with the chapter topic. The Objective headings identify the objectives within the chapter, so you’ll always know an objective when you see it.

![Images](square.jpg)   **Exam Watch** notes call attention to information about, and potential pitfalls in, the exam. These helpful hints are written by authors who have taken the exams and received their certification—who better to tell you what to worry about? They know what you’re about to go through!

![Images](exam.jpg)

**This book’s coverage of the RHCSA exam objectives can be found in the RHCSA Exam Readiness Checklist at the end of this front matter.**

![Images](square.jpg)   **Practice Exercises** are interspersed throughout the chapters. These are step-by-step exercises that allow you to get the hands-on experience you need in order to pass the exams. They help you master skills that are likely to be an area of focus on the exam. Don’t just read through the exercises; they are hands-on practice that you should be comfortable completing. Learning by doing is an effective way to increase your competency with a product. Remember, the Red Hat exams are entirely “hands on”; there are no multiple-choice questions on these exams.

![Images](square.jpg)   **On the Job** notes describe the issues that come up most often in real-world settings. They provide a valuable perspective on certification- and product-related topics. They point out common mistakes and address questions that have arisen from on-the-job discussions and experience.

![Images](job.jpg)

![Images](square.jpg)   **Inside the Exam** sidebars highlight some of the most common and confusing problems that students encounter when taking a live exam. Designed to anticipate what the exam will emphasize, they will help ensure you know what you need to know to pass the exam. You can get a leg up on how to respond to those difficult-to-understand labs by focusing extra attention on these sidebars.

![Images](square.jpg)   **Scenario & Solution** sections lay out potential problems and solutions in a quick-to-read format.

![Images](square.jpg)   The **Certification Summary** is a succinct review of the chapter and a restatement of salient skills regarding the exam.

![Images](right.jpg)

![Images](square.jpg)   The **Two-Minute Drill** at the end of every chapter is a checklist of the main points of the chapter. It can be used for last-minute review.

![Images](QA.jpg)

![Images](square.jpg)   The **Self Test** offers questions designed to help test the practical knowledge associated with the certification exams. The answers to these questions, as well as explanations of the answers, can be found at the end of each chapter. By taking the Self Test after completing each chapter, you’ll reinforce what you’ve learned from that chapter. This book does not include multiple-choice questions because Red Hat does not include any such questions on its exams.

![Images](square.jpg)   The **Lab Questions** at the end of the Self Test section offer a unique and challenging question format that requires the reader to understand multiple chapter concepts to answer correctly. These questions are more complex and more comprehensive than the other questions because they test your ability to take all the knowledge you have gained from reading the chapter and apply it to complicated, real-world situations. Starting with [Chapter 2](#ch02.xhtml), all lab questions are available only from the companion website that accompanies this book, consistent with the electronic format associated with the Red Hat exams. Remember, the Red Hat exams contain *only* lab-type questions. If you can answer these questions, you have proven that you know the subject!

### Additional Resources

If you would like to pursue further reading beyond this book, perhaps the best way to do so is with Red Hat documentation. Much of what we’ve learned about RHEL 9 comes from the documents available at [https://access.redhat.com/documentation/en/red_hat_enterprise_linux/9](https://access.redhat.com/documentation/en/red_hat_enterprise_linux/9). For your purposes, the following may be the most important of these guides:

![Images](square.jpg)   **Performing a Standard RHEL 9 Installation** Although Red Hat exams are given on preconfigured systems, every Linux administrator should be able to install the operating system from scratch.

![Images](square.jpg)   **Configuring Basic System Settings** This system administrator guide includes essential skills that you should be able to master in your job.

![Images](square.jpg)   **Managing Software with the DNF Tool** This guide could serve as an additional resource that expands upon the software installation procedures detailed in [Chapter 4](#ch04.xhtml).

![Images](square.jpg)   **Using SELinux** SELinux often poses a challenging topic for many candidates. This guide details various strategies that can aid in bolstering your SELinux policy’s security.

![Images](square.jpg)   **Configuring and Managing Networking** Despite a majority of this guide’s chapters being beyond the scope of the RHCSA exam, the initial chapters establish a strong foundation on network configuration.

### Some Pointers

Once you’ve finished reading this book, set aside some time to do a thorough review. You might want to return to the book several times and make use of all the methods it offers for reviewing the material:

![Images](square.jpg)   *Reread all the Exam Watch notes.* Remember that these notes are written by authors who have taken the exam and passed. They know what you should expect—and what you should be on the lookout for.

![Images](square.jpg)   *Review all the Scenario & Solution sections* for quick problem solving.

![Images](square.jpg)   *Retake the Self Tests.* Focus on the labs, as there are no multiple-choice questions on the Red Hat exams. We’ve included questions just to test your mastery of the practical material in each chapter.

![Images](square.jpg)   *Complete the exercises.* Did you do the exercises when you read through each chapter? If not, do them! These exercises are designed to cover exam topics, and there’s no better way to get to know this material than by practicing. Be sure you understand why you are performing each step in each exercise. If there is something you are not clear on, reread that section in the chapter.

## INTRODUCTION

### The Red Hat Exam Challenge

This section covers the reasons for pursuing industry-recognized certification, explains the importance of the RHCSA certification, and prepares you for taking the actual examination. It gives you a few pointers on how to prepare, what to expect, and what to do on exam day.

This book covers every published exam objective at the time of writing. For the latest objectives, see [www.redhat.com/en/services/certification/rhcsa](http://www.redhat.com/en/services/certification/rhcsa). Red Hat has also published a syllabus for each of its prep courses for these exams, described shortly. While the published exam objectives are accurate, the prep course syllabi provide additional information. Each Red Hat prep course provides an excellent grounding in systems administration, network administration, security, and more. To that end, this book also includes coverage based on the public syllabi of Red Hat courses RH124 and RH134, described later.

Nevertheless, this book is not intended to be a substitute for any Red Hat course.

#### Leaping Ahead of the Competition!

Red Hat’s RHCSA certification exam is a hands-on exam. As such, it is respected throughout the industry as a sign of genuine practical knowledge. If you pass, you will be head and shoulders above the candidate who has passed only a “standard” multiple-choice certification exam.

Red Hat has offered its hands-on exams since 1999\. They’ve evolved over the years. As detailed in [Chapter 1](#ch01.xhtml), the RHCSA is a three-hour exam. The requirements are detailed in the Exam Readiness Checklist later in this Introduction.

#### Why a Hands-On Exam?

Most certifications today are based on multiple-choice exams. These types of exams are relatively inexpensive to set up and easy to proctor. Unfortunately, many people without real-world skills are good at taking multiple-choice exams. In some cases, the answers to these multiple-choice exams are already available online. This results in problems on the job with “certified” engineers who have an image as “paper tigers” and do not have any real-world skills.

INSIDE THE EXAM

The RHCSA exam is a Red Hat exam. Knowledge of Unix or a Linux distribution such as Ubuntu is certainly helpful, as well as real-world experience with Linux and containers. However, it is important to know how to set up, configure, install, and perform tasks using Red Hat Enterprise Linux.

In response, Red Hat wanted to develop a certification program that matters. In our opinion, they have succeeded with the RHCSA, the RHCE, and their other advanced certifications.

Linux administrators sometimes have to install Linux on a computer or virtual machine. In fact, the RHCSA includes several objectives on this subject. Depending on the configuration, they may need to install Linux from a central source through a network. Installing Linux is not enough to make it useful. Administrators need to know how to configure Linux: add users, install and configure services, set up firewalls, and more.

### Red Hat Certification Program

Red Hat offers several courses that can help you prepare for the RHCSA exam. Most of these courses are four or five days long. In some cases, the courses are offered electronically.

These aren’t the only Red Hat courses available; there are a number of others related to the Red Hat Certified Engineer (RHCE), Red Hat Certified Architect (RHCA), Red Hat Certified OpenShift Administrator, and several Certificates of Expertise in specific areas such as server hardening and performance tuning. But focus on passing the RHCSA exam first; the RHCSA is a prerequisite for more advanced certifications such as the RHCE and RHCA.

#### Should You Take an RHCSA Course?

This book is *not* intended as a substitute for any particular Red Hat RHCSA prep course. However, the topics in this book are based in part on the topics listed in course outlines provided at [www.redhat.com/en/services/training/all-courses-exams](http://www.redhat.com/en/services/training/all-courses-exams). By design, these topics may help Linux users qualify as real-world administrators and can also be used as such. Red Hat can change these topics and course outlines at any time, so monitor [www.redhat.com](http://www.redhat.com) for the latest updates. [Table 1](#intro.xhtml_tab1) describes those courses associated with the RHCSA exam.

The courses given by Red Hat are excellent. The Red Hat instructors who teach these courses are highly skilled. If you have the resources, it is the best way to prepare for the RHCSA exam. If you feel the need for classroom instruction, read this book and then take the appropriate course.

TABLE 1 Red Hat RHCSA-Related Courses

![Images](f0xxxi-01.jpg)

If you’re not sure you’re ready for the course or book, read [Chapter 1](#ch01.xhtml). It includes a rapid overview of the requirements associated with the RHCSA certification. If you find the material in [Chapter 1](#ch01.xhtml) to be overwhelming, consider one of the books noted near the start of the chapter or one of the other lower-level Red Hat courses. In addition, [Chapter 1](#ch01.xhtml) includes a lab that prompts you to examine the requirements of the Linux Professional Institute for its Level 1 certification (LPIC-1). Linux geeks like yourself who are ready to study for the Red Hat exams often take the LPIC-1 exams first.

Alternatively, you may already be familiar with the material in this book. You may have the breadth and depth of knowledge required to pass the RHCSA exam. In that case, use this book as a refresher to help you focus on the skills and techniques needed to pass the exam.

### Signing Up for the RHCSA Course and/or Exam

Red Hat provides convenient web-based registration systems for the courses and tests. To sign up for any of the Red Hat courses or exams, navigate to [www.redhat.com](http://www.redhat.com), click the link for Training & Services | All Courses and Exams, and select the desired course or exam. As shown back in [Table 1](#intro.xhtml_tab1), exams may be taken independently from a course. For example, the RHCSA exam is associated with exam codes EX200\. Exams may also be taken as part of an online or instructor-led course. Alternatively, contact Red Hat Enrollment Central at [training@redhat.com](mailto:training@redhat.com) or (866) 626-2994.

Discounts may be available for a limited time for candidates who have been previously certified as an RHCSA. Current discounts are shown at [https://www.redhat.com/en/services/training/specials/](https://www.redhat.com/en/services/training/specials/).

### RHCSA Exam Readiness Checklist

![Images](fxxxii-01.jpg)

![Images](fxxxiii-01.jpg)

![Images](fxxxiv-01.jpg)

![Images](fxxxv-01.jpg)

## Chapter 1

## Prepare for the Red Hat RHCSA Certification

CERTIFICATION OBJECTIVES

[1.01     The RHCSA Exam](#ch01.xhtml_ch1obj01)

[1.02     Basic Hardware Requirements](#ch01.xhtml_ch1obj02)

[1.03     Get Red Hat Enterprise Linux](#ch01.xhtml_ch1obj03)

[1.04     An Environment for Practice Labs](#ch01.xhtml_ch1obj04)

[1.05     RHEL 9 Installation](#ch01.xhtml_ch1obj05)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

The Red Hat exams are an advanced challenge. This book covers the Red Hat Certified System Administrator (RHCSA) exam, a practical lab test that evaluates an individual’s proficiency in Red Hat Enterprise Linux. Successfully passing it not only boosts one’s professional appeal but also demonstrates their mastery of Linux. The RHCSA certification also is the foundation for those who want to earn the Red Hat Certified Engineer (RHCE) and serves as the initial step toward more advanced Red Hat certifications. Red Hat offers several courses to help prepare for these exams, as described in the front matter and in this chapter.

The focus of this chapter is installation, to create a lab environment as a test bed for the lab exercises in subsequent chapters. We assume that you have a PC available, either a desktop or a laptop, running Linux or a Windows operating system. On your PC, you will install two virtual machines (VMs) running Red Hat Enterprise Linux 9 (RHEL 9). Alternatively, you can use a “rebuild” distribution such as AlmaLinux, as it’s built from the same source code as RHEL 9\. We discuss the only relevant differences in [Chapter 4](#ch04.xhtml).

Today, containers have become a key part of IT systems because of their unique ability to neatly pack up an application in its own box with everything it needs to run. This makes moving and running applications much easier and quicker. Plus, with containers, you can easily add or reduce resources based on the demand for your app, a feature known as *scalability*. Because containers play such a big role in modern IT operations, the RHCSA exam now includes a whole section about them. We’ll go into all the details in [Chapter 10](#ch10.xhtml) of this book.

If you are new to Linux or Unix, this book may not be enough for you. Red Hat suggests that RHCSA candidates have one to three years of experience with the bash shell, user administration, system monitoring, basic networking, software updates, and more. In this book it’s not possible to provide sufficient detail, at least in a way that can be understood by newcomers to Linux and other Unix-based operating systems. Nevertheless, we tried to keep the topics easy to follow even for the reader who has very little experience with Linux. If after reading the first chapters of this book you find gaps in your knowledge, you can refer to one of the following guides:

![Images](square.jpg)   *Linux Administration: A Beginner’s Guide, Eighth Edition*, by Wale Soyinka (McGraw Hill, 2020), provides a step-by-step guide to Linux.

![Images](square.jpg)   *LPIC-1 in Depth* by Michael Jang (Course Technology PTR, 2009) covers the certification many Linux professionals qualify for prior to working for the RHCSA. The book dates back to 2009, but the fundamentals of Linux are still the same.

Before installing RHEL 9, you need to ensure that your system has the right hardware. The installation of RHEL 9 is supported on systems with 64-bit CPUs. In addition, to set up a lab environment with virtual machines, you need a CPU that supports hardware virtualization. Details are discussed in this chapter. As such, while the RHCSA exam is, by and large, not a hardware exam, some basic hardware knowledge is a fundamental requirement for any Linux administrator. As for the operating system itself, you can purchase a subscription to RHEL, or you can use a “rebuild” distribution such as AlmaLinux, where the operating system software is compiled by the open-source community from source code publicly released by Red Hat.

If you’re experienced with other Unix-type operating systems such as Solaris, AIX, and HP-UX, prepare to leave some defaults at the door. There are even significant differences between the Ubuntu and Red Hat distributions. When Red Hat developed its Linux distribution, the company made some choices that differed from other Unix implementations. When one of the authors of this *Study Guide* took one of Red Hat’s System Administration courses, some students with these backgrounds had difficulties with the course and the RHCSA exam.

For the purposes of this book, we’ll be running most commands as the Linux administrative user, root. Logging in as the root user is normally discouraged for security reasons. Also, if you make a mistake on the command line as the root user, you could potentially harm your system very seriously. However, since the RHCSA is a time-based exam, you may find that running commands as the root user is appropriate, because it is quicker and requires less typing than using a normal user account for administrative purposes. Just remember that out of the exam room, this is not recommended.

INSIDE THE EXAM

**OS Installation and Virtualization**

This chapter does not cover any RHCSA exam objectives. While the previous versions of the RHCSA exam included skills related to the installation of Red Hat Enterprise Linux and to the management of virtual guests, the current version of the RHCSA exam does not.

For RHEL 9, the installation process of RHEL is relatively simple. Automated installations (using Kickstart) and virtualization management are now covered in other certification exams: specifically, in the Red Hat Certified Specialist in Deployment and System Management exam (EX403) and in the Red Hat Certified Specialist in Virtualization exam (EX318).

Nevertheless, to set up the lab environment that we will use in the rest of the book, you will need to go through the installation of RHEL and the basic configuration of virtual machines.

These procedures will not be tested in the RHCSA exam, but are essential skills that you must be very familiar with.

**Using Other Versions of Red Hat**

For the purposes of this chapter, you can install RHEL 9 using a no-cost developer subscription provided by the Red Hat Developer Program. You can also use AlmaLinux. However, whereas RHEL 9 is based in part on the work done by many open-source contributors, it’s also based on the Fedora Linux 34 release. Don’t use Fedora to study for the Red Hat exams. If you use Fedora, some configuration settings and commands may differ from RHEL 9\. Later versions of Fedora are likely to have features not found in RHEL 9.

### CERTIFICATION OBJECTIVE 1.01

### The RHCSA Exam

Red Hat first started giving certification exams in 1999\. Since that time, its exams have evolved. The former Red Hat Certification Technician (RHCT) was a complete subset of the RHCE.

In addition, Red Hat has focused the exams more on hands-on configuration. Multiple-choice questions were removed from the exam in 2003\. Later, in 2009, Red Hat simplified the exam by removing the requirement to install Linux on a “bare-metal” system.

Then, the RHCSA certification was introduced as a replacement for the RHCT certification to better align with industry demands and to reflect the evolving role of a Linux system administrator.

Today, the RHCSA exam tests your ability to configure live physical and virtual systems for networking, security, custom filesystems, package updates, user management, and more. In essence, the RHCSA exam covers those skills required to configure and administer a Linux system in the enterprise.

![Images](job.jpg)

**For those keen on progressing their Red Hat credentials, the RHCE certification is the next logical step. The RHCE exam tests your ability to manage multiple systems using Ansible and evaluates your expertise in system automation and administration. Achieving this certification augments one’s professional standing and underscores their expertise in Linux.**

#### The Exam Experience

Red Hat’s certification tests are hands-on exams. As a result of this, they are respected throughout the industry as a sign of genuine practical knowledge. When you pass a Red Hat exam, you will stand head and shoulders above the candidate who has passed only a “standard” multiple-choice certification exam.

When the RHCSA exam starts, you’ll be faced with a live RHEL 9 system. You’ll be given actual configuration problems associated with the items listed in the RHCSA EX200 exam objectives, shown at the following (click the Objectives tab):

![Images](exam.jpg)

**An overview of this book’s coverage of the items listed in the RHCSA exam objectives can be found in the introduction for this book.**

[https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam](https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam)

Naturally, this book is dedicated to helping you gain the skills described on those web pages.

The RHCSA exam lasts three hours. Any changes that you make must survive a reboot. When you’ve completed the given tasks, the person grading the exam will check if the system is configured to meet the requirements. For example, if you are told to “create, delete, and modify local user accounts,” it doesn’t matter whether you modify the associated configuration files with the editor or by using other command-line tools. As long as you don’t cheat, it’s the results that count.

While you won’t have Internet access during the exam, you will have access to online documentation such as man and info pages, as well as documentation in the /usr/share/doc/ directories, assuming appropriate packages are installed.

In addition, Red Hat provides the exams in electronic format. Although the basic instructions may be in a local language such as English, the RHCSA exam is available in several different languages. If you prefer to take the exam in a language other than English, you should contact Red Hat training to be sure the exam is available in that language at [training@redhat.com](mailto:training@redhat.com) or 1-866-626-2994.

Red Hat also has prep courses for the RHCSA exam. The outlines for those courses are available from [https://www.redhat.com](https://www.redhat.com). Although this book is not intended as a substitute for such courses, it is consistent with their outlines. This book covers the objectives associated with the RHCSA exam.

![Images](exam.jpg)

**Red Hat provides “pre-assessment” tests for its exam prep courses. These tests are available at [https://rhtapps.redhat.com/assessment](https://rhtapps.redhat.com/assessment)**

#### Evolving Requirements

Red Hat regularly updates the RHCSA exam to keep up with the changing landscape of Linux system administration and technology trends. This ensures that certified professionals remain current and relevant in their skills and knowledge.

Future changes to the RHCSA exam may be based on topics covered in the Red Hat RHCSA Rapid Track course, RH199/RH200\. So if you are not planning to take the RHCSA exam within the next few months, watch the outline for that course. It may, in effect, be a preview of where Red Hat wants to take the RHCSA exam in the future.

### CERTIFICATION OBJECTIVE 1.02

### Basic Hardware Requirements

Now it is time to explore in detail the hardware that a computer requires to support Red Hat Enterprise Linux. Although some manufacturers include their own Linux hardware drivers, most Linux hardware support comes from third parties, starting with the work of volunteers. Fortunately, there is a vast community of Linux developers, many of whom produce drivers for Linux and distribute them freely on the Internet. If a certain piece of hardware is popular, you can be certain that Linux support for that piece of hardware will pop up somewhere on the Internet and will be incorporated into various Linux distributions, including Red Hat Enterprise Linux.

#### Hardware Compatibility

RHEL 9 can be installed only on 64-bit systems. Fortunately, all PCs and servers sold today are 64-bit systems. Even the lowly Intel i3 CPU can handle 64-bit operating systems. There are even 64-bit versions of the Intel Atom CPU, common on netbook systems and tablets. Similar comparisons can be made for CPUs from Advanced Micro Devices.

Be careful when purchasing a new computer to use with Linux. Although Linux hardware compatibility has come a long way the last few years, and you should have little problem installing it on most modern servers or PCs, you shouldn’t assume Linux will install or run flawlessly on *any* computer, especially if the system in question is a state-of-the-art laptop computer. Laptops are sometimes designed with proprietary configurations that work with Linux only after some reverse engineering.

If you want hardware compatible with and supported by Red Hat, consult the hardware compatibility list at [https://catalog.redhat.com/hardware](https://catalog.redhat.com/hardware).

![Images](exam.jpg)

**While it is important to know how Linux interacts with your hardware, the RHCSA exam is not a hardware exam.**

#### Architectures

The architecture of a server or PC defines the components it uses as well as the way those components are connected. In other words, the architecture describes much more than just the CPU. It includes standards for other hardware such as memory, data paths such as computer buses, general system design, and more. All software is written for a specific computer architecture.

Although RHEL 9 has been built for a variety of architectures, you can focus on the Intel/AMD 64-bit or x86_64 architecture for the RHCSA exam. As of this writing, this exam is offered only on computers with such CPUs, so you need not worry about special architecture-specific issues such as specialty bootloaders or custom proprietary drivers. Nevertheless, customized Red Hat distributions are available for a variety of platforms.

You can install RHEL 9 on systems with a wide variety of CPUs. Red Hat supports four different basic 64-bit CPU architectures:

![Images](square.jpg)   Intel/AMD64 (x86_64)

![Images](square.jpg)   64-bit ARM

![Images](square.jpg)   IBM Power Systems, Little Endian

![Images](square.jpg)   IBM System Z

To identify the architecture of a running RHEL system, run the following command:

`# uname -p`

To practice with the labs in this book, you need to configure virtual machines. Be sure to choose a system that supports hardware-assisted virtualization, along with Basic Input/Output System (BIOS) or Unified Extensible Firmware Interface (UEFI) menu options that allow you to activate hardware-assisted virtualization. All new PCs will meet these requirements today. However, if you are running an old system, look at the processor specifications on the vendor’s website.

#### RAM Requirements

Although it’s possible to run RHEL 9 on less, the RAM requirements are driven by the needs of the Red Hat installer. For basic Intel/AMD-based 64-bit architectures, Red Hat officially requires 1.5GiB of RAM.

Of course, actual memory requirements depend on the load from every program that may be run simultaneously on a system. That can also include the memory requirements of any virtual machine that you might run on a physical RHEL 9 system. There is no practical maximum RAM because, theoretically, you could run 64TB of RAM on RHEL 9\. But that’s just theory. The maximum RAM supported and tested on RHEL 9 for 64-bit Intel/AMD-based systems is 48TB, which is still twice than the 24TB supported on RHEL 8.

![Images](job.jpg)

**If you’re setting up Linux as a server, RAM requirements increase with the number of applications that may need to run simultaneously. The same may be true if you’re running several different VMs on a single system. However, administrators typically “overcommit” RAM on VMs configured with different functionality. VMs can also transparently share memory pages to further improve efficiency.**

#### Storage Options

Before a computer can load Linux, the BIOS or UEFI firmware has to recognize the active primary partition on the disk drive. This partition should include the Linux boot files. The BIOS or UEFI can then set up and initialize that disk drive, and then load Linux boot files from that active primary partition. You should know the following about disk drives and Linux:

![Images](square.jpg)   The number of drives that can be installed on modern computers has increased. On commodity hardware it’s relatively easy to get 16 or 24 Serial Advanced Technology Attachment (SATA) or Serial Attached SCSI (SAS) internal drives on a system. Moreover, the use of Non-Volatile Memory Express (NVMe) drives is steadily growing, particularly in applications requiring high performance.

![Images](square.jpg)   You need both a UEFI firmware and a GPT-partitioned disk to boot from a drive larger than 2TB. UEFI is a firmware interface that is meant to replace the traditional BIOS, and today is available on many PCs on the market. The GUID Partition Table (GPT) is a partitioning format that supports drives larger than 2TB, but you also require a UEFI firmware (rather than a traditional BIOS firmware) to boot from such device.

![Images](square.jpg)   You can install RHEL 9 on a storage area network (SAN) volume. RHEL 9 supports more than 10,000 storage device paths.

#### Networking

As Linux was originally designed as a clone of Unix, it retains the advantages of Unix as a network operating system. However, not every network component works with Linux. As an example, several manufacturers of wireless network devices have not built Linux drivers. In most such cases, Linux developers have been working endlessly to develop appropriate drivers and to get those drivers incorporated into the major distributions, including RHEL.

#### Virtual Machine Options

Virtualization makes it relatively easy to set up a large number of systems, so it can help you configure machines, each dedicated to a specific service. To that end, virtualization can be classified into different categories. Some solutions can belong to more than one category. As an example, VMware ESXi is a bare-metal, hypervisor-based virtualization solution that supports hardware-assisted virtualization and provides optional paravirtual drivers to be installed on the guest OS.

![Images](square.jpg)   **Application level vs. VM level** Software tools such as Wine (originally an acronym for Wine Is Not an Emulator) support the installation of a single application. In this case, Wine allows an application built for Microsoft Windows to be running on Linux. On the other end, VM-level virtualization emulates a number of complete computer systems for the installation of separate guest OSs.

![Images](square.jpg)   **Hosted vs. bare-metal hypervisor** Applications such as VMware Player and VirtualBox are hosted hypervisors (“type-2” hypervisors) because they run on a conventional OS such as Microsoft Windows 11\. Conversely, bare-metal virtualization systems, such as VMware ESXi and Citrix Hypervisor (“type-1” hypervisors), include a minimal OS dedicated to VM operations.

![Images](square.jpg)   **Paravirtualization vs. full virtualization** Full virtualization allows a guest OS to run unmodified on a hypervisor, whereas paravirtualization requires specialized drivers to be installed in the guest OS.

The KVM (Kernel-based Virtual Machine) solution that comes with RHEL 9 is known as a hypervisor—a VM monitor that supports the running of multiple operating systems concurrently on the same CPU.

![Images](job.jpg)

**KVM replaced Xen as the default hypervisor starting in RHEL 5 and has replaced Xen in many open-source distributions. Citrix Hypervisor (formerly XenServer) is owned by Citrix.**

Another virtualization approach that is very popular today is Linux containers, such as those provided by Docker or Podman. This solution is not hypervisor-based but rather relies on the process and filesystem isolation techniques available in the Linux kernel (that is, cgroups and namespaces) to run multiple isolated Linux systems on the same physical host. Kubernetes (and OpenShift, which is based on it) provides an orchestration platform for the management and deployment of containers.

### CERTIFICATION OBJECTIVE 1.03

### Get Red Hat Enterprise Linux

The RHCSA exam is based on your knowledge of RHEL. To get an official copy of RHEL, you typically need a subscription. However, for development purposes Red Hat also offers a subscription at no cost as part of the Red Hat Developer Program. As an alternative, third-party rebuilds such as AlmaLinux are available. AlmaLinux uses the same source code as RHEL and, except for the trademarks and the connection to the Red Hat Customer Portal, is essentially functionally identical to RHEL.

Once you get a subscription, you’ll be able to download RHEL 9 from the Red Hat Customer Portal at [https://access.redhat.com/downloads](https://access.redhat.com/downloads). Downloads are available for the operating system in a format appropriate for a DVD. There’s also a download available for a network boot ISO image. You’ll even be able to download files with the source code for associated packages. These downloads are in ISO image format, with an **.iso** extension. Such files can be burned to appropriate media, using standard tools such as balenaEtcher, K3b, Brasero, and even corresponding tools on Microsoft systems. Alternatively, you can set up a VM where the virtual CD/DVD drive hardware points directly to the ISO file.

![Images](exam.jpg)

**Although it is important to know how to get RHEL, that skill is not a part of the objectives for the RHCSA exam.**

#### Get a Subscription at No Cost

Red Hat currently offers a RHEL subscription at no cost, if you enroll in the Red Hat Developer Program at [https://developers.redhat.com](https://developers.redhat.com). If you want to learn RHEL and use it for development purposes, this is certainly the most affordable option. However, keep in mind that you may not be allowed to use this subscription on production systems. The Red Hat Developer subscription offers self-service support through resources such as knowledge base articles and discussion groups on the Red Hat Customer Portal.

#### Purchase a Subscription

Different subscriptions are available for workstations, servers, and development machines. You may want to purchase a subscription if you want to be able to contact Red Hat Support.

A variety of server subscriptions are available, the price of each depending on the number of CPU sockets and virtual guests and on the support level. A system associated with a standard RHEL subscription is limited to two CPU sockets and two virtual nodes. Each socket can have a multicore CPU. Significant discounts for academic users are available.

Red Hat also offers a Red Hat Enterprise Linux Workstation subscription, currently priced at $299 per year in the United States. This subscription provides full support from Red Hat and download access to RHEL and several types of add-on software.

#### Third-Party Rebuilds

To comply with the Linux General Public License (GPL), Red Hat releases the source code for just about every RHEL package. However, the GPL only requires Red Hat to make the source code available to its customers. Red Hat does not have to make the binary packages compiled from that source code publicly available.

![Images](job.jpg)

**The description in this book of the GPL, trademark law, and Red Hat legal agreement for subscription services is not a legal opinion and is not intended as legal advice.**

Under trademark law, Red Hat can prevent others from releasing software with its trademarks, such as the Red Hat logo. Nevertheless, the GPL gives anyone the right to compile that source code. If they make any modifications, all they need to do is release their changes under the same license. And some “third parties” have taken this opportunity to remove the trademarks from the released source code and have compiled that software into their own rebuilds, functionally equivalent to RHEL.

The RHEL source code is available at the Red Hat Customer Portal. However, the building of a distribution, even from source code, is a tricky process. But once complete, the rebuild has the same functionality as RHEL. However, rebuild distributions don’t have a connection to and can’t get updates from the Red Hat Customer Portal. Installing packages from Red Hat Subscription Management (RHSM) is part of the RHCSA exam objectives, so you will not be able to practice this skill if you use a rebuild distribution. Nevertheless, this is the only limitation.

![Images](exam.jpg)

**In the current RHCSA exam objectives, RHSM is referred to by its previous name, the “Red Hat Network.” While there’s a possibility of Red Hat making updates to this in the future, for the RHCSA exam’s scope, both RHSM and the “Red Hat Network” represent the same service, which offers access software packages and updates provided by Red Hat.**

CentOS Linux, once the most prominent RHEL rebuild, was discontinued in 2021\. It was replaced by CentOS Stream, a Linux distribution designed to function as a midstream bridge between Fedora Linux’s upstream development and RHEL’s downstream development. As such, it’s not a rebuild of RHEL but rather an upstream development platform for it.

Among the third-party rebuilds, AlmaLinux continues to be a viable option. For more information, see [https://almalinux.org](https://almalinux.org).

#### Check the Download

For downloads from its website, Red Hat provides checksums based on the 256-bit Secure Hash Algorithm (SHA256). You can check these ISO files against the given checksum numbers with the **sha256sum** command. For example, the following command calculates the SHA256 checksum for the RHEL 9.1 DVD file:

`# sha256sum rhel-baseos-9.1-x86_64-dvd.iso`

At the time of writing, the most recent version of RHEL available was 9.1\. Throughout this book, we’ve tailored the examples and exercises to align with RHEL 9.1 specifics. However, readers should find it straightforward to modify and apply these examples to newer releases of RHEL 9\. It’s essential to stay updated and adaptable, recognizing that the core principles typically remain consistent across minor version updates.

EXERCISE 1-1

**Get Red Hat Enterprise Linux**

In this exercise, you will enroll in the Red Hat Developer Program and download a RHEL 9 ISO image. You can skip this exercise if you already have a RHEL subscription, or if you wish to use AlmaLinux or another RHEL derivative distribution to practice for the Red Hat exams.

1.   Point your browser to [https://developers.redhat.com](https://developers.redhat.com). Click Log In in the upper-right corner, then click Register in the same location.

2.   Complete the registration form and click Create My Account to activate your account.

3.   Go to [https://developers.redhat.com/products/rhel/download](https://developers.redhat.com/products/rhel/download) and download the latest Server DVD ISO image for RHEL 9, x86_64 architecture.

4.   Calculate the SHA256 checksum of the RHEL 9 Server DVD ISO file. If you are on a Linux machine, type this command (the filename may differ slightly for a release of RHEL other than 9.1):

`# sha256sum rhel-baseos-9.1-x86_64-dvd.iso`

On Windows, start PowerShell and run

`# Get-FileHash rhel-baseos-9.1-x86_64-dvd.iso`

5.   Go to [https://access.redhat.com/downloads](https://access.redhat.com/downloads) and click Red Hat Enterprise Linux. You can also get the DVD ISO image from this page, but the most important thing is that here you will find the SHA checksum of the DVD ISO file that you have previously downloaded. Compare the SHA256 checksum with the one that you calculated in Step 4 and check that the two values are the same. If not, you may have had an issue during the download of the file.

6.   Go to [https://access.redhat.com/management/products](https://access.redhat.com/management/products). You should see a Red Hat Developer Subscription for Individuals in your active subscriptions. Click it and have a look at the products included with your Developer Subscription. In the list, you should recognize Red Hat Enterprise Linux for x86_64\. There will be lots of products listed, but we won’t cover all of those in this book.

### CERTIFICATION OBJECTIVE 1.04

### An Environment for Practice Labs

Red Hat provides “pre-installed systems” for its exams, with questions presented “electronically.” So you won’t start from scratch, but you’ll still need to set up practice systems.

In other words, when seated for an exam, you’ll see an installed copy of RHEL 9 on the test system, with questions in some electronic format. No public information is available on the format of the questions.

The installation requirements described in this section are suited to the creation of an environment for practice labs. That environment may also work as a baseline for other RHEL systems. On many real networks, new virtual systems are created or cloned from that baseline. Those new systems are then dedicated for a single service.

For the purposes of our lab environment, we will use VMware Workstation Player virtualization software to set up some RHEL virtual machines for testing. We chose VMware Workstation Player because it is freely available, and you can install it on a desktop PC or laptop, whether you have a Windows or Linux system running on it. Of course, if you already have a physical system running Linux, you may choose to use KVM, the Red Hat virtualization hypervisor. Or you can install other virtualization products, such as VirtualBox. However, we cannot cover every possible scenario in this book, so we’ll assume you will be using VMware Workstation Player.

The baseline for the RHEL 9 systems configured in this chapter is relatively simple. You will need about 20GiB of disk space. Part of that space will be organized as shown in [Table 1-1](#ch01.xhtml_ch1tab1). Some of the space will be configured as regular partitions. The remaining space on the disk drive will be left empty for potential configuration during the lab exercises as logical volumes.

TABLE 1-1 Filesystem Mount Points

![Images](f0013-01.jpg)

![Images](job.jpg)

**The notation MiB indicates a mebibyte, which is equivalent to 1024KiB (1024 “kibibytes”), or 1024 × 1024 = 1,048,576 bytes. Similarly, a GiB is a gibibyte and is the same as 1024MiB, and so on. However, in the notation of the International System of Units, MB indicates a megabyte, which is equivalent to 1000KB (1000 kilobytes), or 1000 × 1000 = 1,000,000 bytes. You may have noticed that operating systems usually show a disk size in GiB (or TiB), while disk vendors advertise their disk sizes in GB (or TB). Can you guess why? Which is larger?**

The 20GiB virtual hard disk is the recommended size to provide enough room for the labs that you will complete in later chapters. If space is limited on your system, you might go as low as 10GiB, which is the minimum disk size supported by RHEL 9, or even lower. Swap space in Linux is used as an extension of local RAM, especially when that resource runs short, and is not strictly necessary.

The baseline minimum installation of RHEL 9 does not include a GUI. Although it is fairly easy to install the package groups associated with the GUI after installation is complete, that process requires the installation of several hundred megabytes’ worth of packages. And that takes time. Since Red Hat provides a pre-installed system to reduce the time required for the exam, it is reasonable to suggest that the system provided by Red Hat includes the GUI. And the default GUI for Red Hat systems is the GNOME Desktop Environment.

![Images](job.jpg)

**GNOME was initially an acronym within an acronym. It stood for the GNU Network Object Model Environment. GNU is itself a recursive acronym because it stands for GNU’s Not Unix. Linux is filled with similar recursive acronyms, such as PHP: Hypertext Preprocessor (PHP).**

The amount of RAM to allocate is more complex, especially on a VM. For the purposes of this book, we’ve configured VMs with 2GiB of RAM to comfortably enable GUI-based illustrations of the RHEL installation process. However, 1.5GiB of RAM is the minimum required, and you could run RHEL 9 with even less. Since different VMs rarely use all the RAM simultaneously, it’s possible to “overcommit” RAM; for example, it may be possible to set up two VMs, with 2GiB of RAM each, on a physical host system with less than 4GiB of physical RAM. Some RAM on the VMs will remain unused, available to the physical host system.

#### System Roles

In this chapter, you will set up two RHEL 9 virtual machines. The installation of the first system will be explained in the next Certification Objective section, “RHEL 9 Installation,” while you will install the second system in Lab 1 at the end of the chapter.

[Table 1-2](#ch01.xhtml_ch1tab2) lists the roles appropriate for each of the two systems that you will install.

TABLE 1-2 Roles for Test Systems

![Images](f0014-01.jpg)

#### Getting VMware Workstation Player

To get VMware Workstation Player, navigate to the official VMware website, specifically to [https://www.vmware.com/products/workstation-player.html](https://www.vmware.com/products/workstation-player.html). Click the Download For Free link, and then click Go To Downloads. Following that, you’ll be presented with two download options, one for Linux and one for Windows. Click the Download Now button for the one that fits your operating system.

Once the software is downloaded, locate the installation file in your Downloads folder or wherever your browser defaults to save files. The installation file generally ends with .exe for Windows or .bundle for Linux. To start the installation process, double-click the file.

For Windows, an installation wizard opens to guide you through the process. Click Next and follow the onscreen instructions, accepting the End-User License Agreement and choosing the location of installation (if not the default).

On Linux, open the terminal, navigate to the directory containing the .bundle file, and use the command **sudo sh ./VMware-Player-<version_number>.bundle** to start the installation process. Follow the prompts, accepting the license agreement and choosing the relevant options.

Upon successful installation, you can launch VMware Workstation Player. To do this, either navigate to the program through your system’s start menu or type **VMware Workstation Player** into your system’s search bar and press ENTER.

When you open VMware Workstation Player, a window appears that is similar to what is shown in [Figure 1-1](#ch01.xhtml_ch1fig1). This is your main control panel for managing and interacting with your virtual machines. From here, you can create new VMs, open existing ones, change settings, and much more.

FIGURE 1-1 VMware Workstation Player

![Images](F01-01.jpg)

#### Virtual Networks on a Hypervisor

The free version of VMware Workstation Player offers three types of networks that you can configure for your virtual machines:

![Images](square.jpg)   **Bridged** This mode bridges your physical network adapter and your virtual machine’s adapter, allowing the VM to appear as a separate device on the same network that your host machine is connected to. It means that the VM will get an IP address within the same subnet as your host machine.

![Images](square.jpg)   **Network Address Translation (NAT)** In NAT mode, your VM shares the IP address of your host machine. The VMware hypervisor software acts as a network router for the VM and manages a private network connection between the host machine and the VM. The VMs connected via NAT mode will be able to access the Internet but won’t be directly accessible from the external network, as they’ll be on a separate subnet.

![Images](square.jpg)   **Host-only** With a host-only network, your VM can only communicate with the host machine. It will not have any access to the external network, the Internet. This is useful when you want to isolate the VM from your network for security or testing purposes.

In our lab environment, we will be using the NAT mode for our Linux VMs. This configuration provides the VMs with Internet access while keeping them isolated from the outside, making it an ideal balance for our purposes.

VMware Workstation Player automatically allocates a subnet for NAT mode. To determine the subnet used by VMware for NAT, follow this procedure on a Windows system, as shown in [Figure 1-2](#ch01.xhtml_ch1fig2):

FIGURE 1-2 The VMnet8 adapter properties

![Images](F01-02.jpg)

1.   Open Control Panel and click Network And Internet (in Category view).

2.   Click Network And Sharing Center.

3.   On the left side of the Network And Sharing Center window, click Change Adapter Settings. This opens a screen with all of your network connections.

4.   Locate the VMware Network Adapter VMnet8\. This adapter is used for the NAT network in VMware Workstation Player.

5.   Right-click the name of the adapter and select Properties.

6.   In the Properties window, click Internet Protocol Version 4 (TCP/IPv4) and then click the Properties button.

7.   The next window displays the IP address and subnet mask for the VMnet8 adapter.

If you have installed VMware Workstation Player on Linux, open a terminal and type the command **ip address show vmnet8**. This will display the IP address and subnet mask for the vmnet8 adapter.

![Images](job.jpg)

**VMware Workstation Player will take care to avoid IP address conflicts with existing hardware on the local network, such as with routers and wireless access points. For example, if your wireless access point uses the subnet 192.168.56.0/24, the VMware software will not use this range.**

If you need help with networking, refer to [Chapter 3](#ch03.xhtml). For now, all you need to know is that VMware Workstation Player has created a network subnet for NAT mode on your physical host. This subnet is not visible to the external world, and the VMs that you create will be attached to it so that they will run and communicate on this isolated network segment.

The NAT subnet can be changed according to your preferences or requirements, but this is not necessary. Throughout this book, we’ll be working under the assumption that the subnet is set to 172.16.0.0/24. However, it is essential to remember that your own system’s configuration might differ from this.

For instance, suppose that the subnet created by VMware Workstation Player on your machine happens to be 192.168.219.0/24\. In such a case, the corresponding IP address you would assign to server1 would then be 192.168.219.100 rather than 172.16.0.100\. Here, you’ll notice that the final octet is the same, whereas the first three octets reflect the NAT subnet address. So, the key takeaway is to ensure that the first three octets that you assign to your VM’s IP address match those of your NAT subnet.

#### Configure a Virtual Machine on VMware Workstation Player

Return to the main window of VMware Workstation Player. With the following steps, you’ll set up the VM that will host the server1.example.com system introduced in [Table 1-2](#ch01.xhtml_ch1tab2):

1.   Click File | Create a New Virtual Machine to open the New Virtual Machine Wizard.

![Images](I01-01.jpg)

2.   Select “I will install the operating system later” and click Next.

3.   Set the guest operating system to Linux, version Red Hat Enterprise Linux 9 64-bit.

4.   Type a name for the new VM; to match the discussion in the remainder of this book, you should name this VM **server1**. Click Next. In the next screen, set the disk size to 20GB.

![Images](I01-02.jpg)

5.   Click Next, then Finish. The virtual machine is created and is shown in VMware Workstation Player in a “Powered Off” state.

![Images](I01-03.jpg)

6.   Now you need to point VMware Workstation Player to your installation media. Select the newly created VM and click Edit Virtual Machine Settings. In the new window that opens, select CD/DVD (SATA) and ensure that the option Connect At Power On is selected. Then, click the Browse button and browse until you find the path of the RHEL 9 ISO image that you have previously downloaded. This image will be mounted as if it were a DVD inserted in the drive of the machine. Then, click Save to return to VMware Workstation Player.

![Images](I01-04.jpg)

7.   Click Start. The VM should power on and boot from the RHEL 9 DVD image that you have attached to it.

8.   To power off the virtual machine, from the Virtual Machine menu select Power | Power Off Guest.

![Images](job.jpg)

**If you click your mouse pointer inside the virtual machine display window of VMware Workstation Player, this will cause the VM to capture the host mouse pointer and keyboard so that you can use the mouse and type inside the VM. Press CTRL-ALT to release it and restore control to the main operating system.**

### CERTIFICATION OBJECTIVE 1.05

### RHEL 9 Installation

Even most new Linux users can install RHEL 9 from a CD/DVD. Although this section addresses some of the options associated with installation, it is focused on the creation of the first of the two systems listed in [Table 1-2](#ch01.xhtml_ch1tab2).

In addition, the installation process is an opportunity to learn more about RHEL 9, not only boot media, but the logical volumes that can be configured after installation is complete. However, because pre-installed physical systems are now the norm for Red Hat exams, detailed discussions of logical volumes have been consolidated in [Chapter 7](#ch07.xhtml).

The steps described in this section assume that you have downloaded the RHEL 9 DVD image, as explained earlier in the chapter, and followed the steps in the previous section to create a VM in VMware Workstation Player.

#### Boot Media

When you are installing RHEL 9, the simplest option is to boot it from the RHEL 9 DVD. But that’s not the only available installation option. In essence, five methods are available to start the RHEL 9 installation process:

![Images](square.jpg)   Boot from a RHEL 9 Binary DVD.

![Images](square.jpg)   Boot from a USB drive containing the RHEL 9 Binary DVD image.

![Images](square.jpg)   Boot from a minimal RHEL Boot CD.

![Images](square.jpg)   Boot from a USB key containing a minimal RHEL Boot CD image.

![Images](square.jpg)   Boot from a Kickstart server using a PXE network boot card.

The last three options generally assume that you’re going to install RHEL over a network and that package repositories will be available on a web server, FTP server, or NFS share. The installation and boot media are available from the Red Hat Customer Portal for users with a subscription. They are also available from servers associated with “rebuild” distributions.

If you followed the steps in the previous section, you can boot the server1.example.com VM from the installation DVD. After a few seconds, a RHEL installation screen should appear, as illustrated in [Figure 1-3](#ch01.xhtml_ch1fig3), with at least the following three options:

FIGURE 1-3 The installation boot screen

![Images](F01-03.jpg)

![Images](square.jpg)   Install Red Hat Enterprise Linux 9.1

![Images](square.jpg)   Test this media & install Red Hat Enterprise Linux 9.1

![Images](square.jpg)   Troubleshooting

The first option should work for most users. If you want to check the integrity of the installation media before starting the installation process, select the second option.

Two modes are associated with the Red Hat installation program (also known as “Anaconda”): text mode and graphical mode. Although the graphical mode is the recommended method, you would be automatically redirected to text mode if the installation program does not properly detect your video card. Fortunately, this will not be the case on VMware Workstation Player, because the hosted hypervisor will emulate a video card that is supported by Linux.

You can also force installation in text mode if you wish. To do so, highlight the Install Red Hat Enterprise Linux 9.1 option and press the TAB key. When you do, the following options are revealed on that screen, on one line:

![Images](f0023-02.jpg)

To force installation in text mode, add **inst.text** to the end of this line.

#### Basic Installation Steps

The basic RHEL installation is straightforward and should already be well understood by any Red Hat certification candidate.

The sequence of steps for the installation process varies depending on whether you’re installing in text mode or graphical mode. The sequence also may vary if you’re using a rebuild distribution of RHEL 9. So be flexible when reading the following instructions:

1.   Boot your computer from the RHEL DVD. Three options are normally shown, as illustrated in [Figure 1-3](#ch01.xhtml_ch1fig3). Select the first option and press ENTER.

2.   Select a language to use during the installation process, as shown in [Figure 1-4](#ch01.xhtml_ch1fig4). English is the default; over 50 options are available.

FIGURE 1-4 Select a language for installation.

![Images](F01-04.jpg)

3.   The next screen is the Installation Summary screen, shown in [Figure 1-5](#ch01.xhtml_ch1fig5). From this interface you can review and edit all installation settings. One item in the Installation Summary screen is marked with a “warning” symbol. This indicates that you must configure the corresponding section before being able to proceed with the installation.

FIGURE 1-5 The Installation Summary screen

![Images](F01-05.jpg)

4.   From the Installation Summary screen, review the date and time zone of the local system, and make appropriate changes if necessary.

5.   Similarly, you can review the keyboard configuration and the language settings if needed.

6.   The next option in the Installation Summary screen relates to the installation source. Because you are installing from a DVD image, leave this setting as “Local media.”

7.   Review the Network & Host Name settings in the Installation Summary screen, as shown in [Figure 1-6](#ch01.xhtml_ch1fig6). The left panel lists the network interfaces detected by the installation program. Select the Ethernet interface, and move the switch at the top-right corner to the ON position.

FIGURE 1-6 The Network & Host Name configuration screen

![Images](F01-06.jpg)

8.   Click the Configure button and select the IPv4 Settings tab to choose how you want IP addressing to be configured. You will see the window shown in [Figure 1-7](#ch01.xhtml_ch1fig7). In the Method field, set the configuration method to Manual to manually enter a static IP address. Then, click Add and enter the settings shown in [Figure 1-7](#ch01.xhtml_ch1fig7). Save your configuration.

FIGURE 1-7 IPv4 network settings

![Images](F01-07.jpg)

9.   In the Host Name field shown at the bottom left in [Figure 1-6](#ch01.xhtml_ch1fig6), set **server1.example.com** as the hostname for the system and click Apply. Once you have completed your configuration changes, click the Done button.

10.   Click the Installation Destination item from the Installation Summary screen, and you will see the screen shown in [Figure 1-8](#ch01.xhtml_ch1fig8). From this screen, you can determine how space on configured disk drives, local and remote, is used. Here, you can choose between automatically and manually configured partitioning. For automatic partitioning, you can select the check box “I would like to make additional space available” if you want to reconfigure space from other existing partitions. Optionally, you can select “Encrypt my data.” For the purposes of this installation, select Custom and click Done to continue.

FIGURE 1-8 The Installation Destination screen

![Images](F01-08.jpg)

#### The Installation Perspective on Partitions

Disk partitions are a way to slice a disk drive into multiple regions. Once a partition is created, you can configure Linux to mount a partition on a directory, or “mount point.” For example, a partition can be mounted on the top of the Linux filesystem, which is the root partition (or “/”), or it can be mounted under a different directory, such as /home.

To define a partition, you may need some background on naming conventions, the configuration of different filesystems, and uses of swap space and logical volumes. This is just an overview. Detailed information is available in [Chapter 7](#ch07.xhtml).

##### Naming Conventions

Linux has a simple naming standard for disk partitions: three letters followed by a number. The first letter identifies the type of drive (*s* is for SATA or SAS, and *v* is for virtual disks on KVM-based VMs). The second letter is *d* for disk, and the third letter represents the relative position of that disk, starting with *a*. For example, the first SATA drive is sda, followed by sdb, sdc, and sdd. (NVMe drives, such as that detected in [Figure 1-8](#ch01.xhtml_ch1fig8), are named nvme*X*n*Y*, where *X* indicates the index or number of the NVMe controller, and n*Y* refers to the namespace or logical unit within the NVMe controller.)

The number that follows the three letters is based on the relative position of the partition. Two partitioning schemes are available on modern PCs: the traditional Master Boot Record (MBR) and the newer GUID Partition Table (GPT) scheme.

In the MBR scheme, partitions can be one of three types: primary, extended, or logical. Primary partitions can contain the boot files for an operating system. Disk drives can also be configured with one extended partition, which can then contain a number of logical partitions.

Disk drives are limited to four primary partitions. When four partitions are not enough, an extended partition can be substituted for the last primary partition. That extended partition can then be subdivided into logical partitions. So when planning a partition layout, make sure that the extended partition is big enough. Although it’s possible to create more, you should not create more than 12 logical partitions on any individual SATA, SAS, or virtual disk drive.

The GPT partitioning scheme does not have such limitations and, on RHEL 9, by default can support up to 128 partitions. This number can be increased further if necessary, although such a scenario is quite rare and not commonly used.

Each partition is associated with a Linux device file. At least that is straightforward; for example, the device filename associated with the third partition on the first SATA drive is /dev/sda3\. (For NVMe drives, the third partition on /dev/nvme0n1 would be indicated as /dev/nvme0n1p3.)

A volume is a generic name for a formatted segment of space that can be used to contain data. Volumes can be partitions or those logical volumes associated with Logical Volume Management (LVM). A filesystem exists inside a volume and provides the ability to store files. Filesystems handle the conversion of blocks on the volumes to files. For example, Red Hat uses the XFS filesystem as the default format for its volumes. The standard way to access data in Linux is to first mount that filesystem onto a directory. For instance, when the /dev/sda1 partition is formatted to the XFS filesystem, it can then be mounted on a directory such as /boot. It is common to say something like, “The /dev/sda1 filesystem is mounted on the /boot mount point.” You will review these concepts in more depth in [Chapter 7](#ch07.xhtml).

##### Separate Filesystem Volumes

Normally, you should create several volumes for RHEL 9\. Even in the default configuration, RHEL is configured with at least three volumes—a top-level root directory (/), a /boot directory, and Linux swap space. Additional volumes may be suitable for directories such as /home, /opt, /tmp, and /var. They’re also suitable for any custom directories such as for websites, dedicated groups of users, and more.

Although it’s important to configure the /boot directory on a regular partition, other directories can readily be configured on logical volumes.

Dividing the space from available disk drives in this manner keeps system, application, and user files isolated from each other. This helps protect the disk space used by system services and various applications. Files cannot grow across volumes. For example, a user’s home directory with lots of files can’t crowd out space needed by a system service.

While there are many advantages to creating more volumes, it isn’t always the best solution. When disk space is limited, the number of partitions should be kept to a minimum. For example, if you have a 12GiB disk drive and want to install 5GiB of packages, having dedicated /var and /home volumes could lead to a situation where disk space runs out far too quickly.

##### Linux Swap Space

Linux swap space is normally configured either on a dedicated partition or on a logical volume. Such space is used to extend the amount of effective RAM on a system as virtual memory for currently running programs. But normally you should not just buy extra RAM and eliminate swap space. Linux moves infrequently used programs and data to swap space even if you have gigabytes of free RAM.

The way Red Hat recommends to assign swap space is based on the amount of RAM on a system. For systems of up to 2GiB, the recommended swap space size is twice the amount of installed RAM. For systems between 2GiB and 8GiB, it’s equal to the amount of RAM. Above 8GiB, it’s half the amount of RAM. But those are not “hard and fast” rules. Workstations with several gigabytes of RAM frequently use very little swap space. However, certain application workloads may need a big swap partition, such as applications that use large tmpfs filesystems (tmpfs is a temporary filesystem stored in RAM that relies on swap space as a backing store if the server is under memory pressure). In any case, the default installation configures swap space, not in a dedicated partition, but as a logical volume.

##### Basic Information on Logical Volumes

The creation of a logical volume from a partition requires the following steps. Details on these concepts, as well as the actual commands required to execute these steps, are described in [Chapter 7](#ch07.xhtml). Some of these steps are run automatically if you create a logical volume during the installation process.

![Images](square.jpg)   Label a partition as a Linux LVM volume.

![Images](square.jpg)   Initialize the labeled partition as a physical volume.

![Images](square.jpg)   Combine one or more physical volumes as a volume group.

![Images](square.jpg)   Subdivide a volume group into logical volumes.

![Images](square.jpg)   Format a logical volume to a Linux filesystem or swap space.

![Images](square.jpg)   Mount a formatted logical volume on a directory or as swap space.

#### Partition Creation Exercise

Now we return to the installation process. If you followed the steps described so far in this chapter, you should see the Manual Partitioning screen shown in [Figure 1-9](#ch01.xhtml_ch1fig9).

FIGURE 1-9 The Manual Partitioning screen

![Images](F01-09.jpg)

At this screen, the drop-down menu gives you the opportunity to configure filesystems on standard partitions, on LVM volumes, and on thin-provisioned LVM volumes. The /boot mount point will be always configured on a standard partition, regardless of the partition scheme settings you have selected in this screen.

1.   Select Standard Partition from the partitioning scheme drop-down menu. LVM will be discussed in [Chapter 7](#ch07.xhtml).

2.   Configure standard mount points as described earlier in [Table 1-1](#ch01.xhtml_ch1tab1). Larger partitions are acceptable if you have the space. At the bottom left of the screen, the + button supports the creation of a new mount point, as shown in [Figure 1-10](#ch01.xhtml_ch1fig10).

FIGURE 1-10 Adding a mount point

![Images](F01-10.jpg)

3.   Back in the Manual Partitioning screen, you should now see the settings shown in [Figure 1-11](#ch01.xhtml_ch1fig11). This window supports a number of choices:

FIGURE 1-11 Configuration for the /boot partition

![Images](F01-11.jpg)

![Images](square.jpg)   **Mount Point** This is the directory (such as /boot) whose files will be stored on the partition.

![Images](square.jpg)   **Desired Capacity** Indicate the desired capacity of the partition; in this case, the partitions to be configured for this baseline system are defined in [Table 1-1](#ch01.xhtml_ch1tab1).

![Images](square.jpg)   **Device Type** This is the device type, which you previously set to Standard Partition from the partitioning scheme menu.

![Images](square.jpg)   **File System** Select the filesystem type; in this case, the default xfs filesystem is selected.

![Images](square.jpg)   **Label** You can provide an optional label.

Now it’s time for an exercise. First, we examine how to create and configure partitions during the installation process. We’ll also look at how to allocate a filesystem to a partition or a logical volume.

EXERCISE 1-2

**Partitioning During Installation**

This exercise is based on the assumption that you have followed the installation steps in the previous section of this chapter. It is easy to recover from mistakes because you can click the Reload Storage Configuration button to discard any configuration changes. This exercise starts with the Manual Partitioning screen shown in [Figure 1-9](#ch01.xhtml_ch1fig9) and continues with the screens shown in [Figures 1-10](#ch01.xhtml_ch1fig10) and [1-11](#ch01.xhtml_ch1fig11).

1.   If you have made any configuration changes to the partitioning layout, click the Reload Storage Configuration button (the rotating arrow button at the bottom left in [Figure 1-9](#ch01.xhtml_ch1fig9)) to discard all of them.

3.   Select the LVM partitioning scheme from the drop-down menu on the left of [Figure 1-9](#ch01.xhtml_ch1fig9).

3.   At the bottom left of the screen, click the + button to add a new mount point.

4.   Set up an appropriate mount point, such as /boot, set the capacity to 1GiB, and click the Add Mount Point button.

5.   Note that despite your having selected the LVM partitioning scheme, the /boot mount point has been created on a standard partition. This is because the Anaconda installer forces the /boot volume to be on a standard partition.

6.   Click the File System drop-down menu and review the available options. You will see several filesystem types, such as xfs, vfat, ext4, and so on.

7.   Create an additional volume for the swap space. Under Mount Point, select “swap” and set the size to 1GiB.

8.   Leave the swap space on a standard partition. Ensure that the swap partition is selected and change the Device Type setting from LVM to Standard Partition.

9.   Create an additional mount point for the root filesystem, using the steps just described. Select / in the Mount Point input box and set the size to 15GiB. Note how the Available Space and Total Space figures shown at the bottom left of the window have changed.

10.   Repeat the preceding step to create a mount point for the /home filesystem and set the size to 1GiB.

Now that the exercise is complete, the partition configuration should reflect at least the minimums shown in [Table 1-1](#ch01.xhtml_ch1tab1). One version is shown in [Figure 1-12](#ch01.xhtml_ch1fig12). If a mistake is made, highlight a partition and edit its configuration settings. Do not be concerned with small errors; modest variations in size are not relevant in practice—and the Red Hat exams reflect what happens in practice.

FIGURE 1-12 Sample partition configuration

![Images](F01-12.jpg)

To complete this part of the process, click Done. You will see a Summary of Changes screen. This is your last chance to cancel before proceeding. Assuming you’re satisfied, click Accept Changes to continue.

#### Wow, Look at All That Software!

Over 6600 software packages are available just from the RHEL 9 installation DVD. That figure does not include a number of packages available only through other subscription channels on the Red Hat Customer Portal. With so many packages, it’s important to organize them into groups. Click Software Selection from the Installation Summary screen (shown earlier in [Figure 1-5](#ch01.xhtml_ch1fig5)). You’ll see the options shown in [Figure 1-13](#ch01.xhtml_ch1fig13), which allow you to configure the local system to a desired functionality. The selection depends on your objective. If you’re installing on a production physical system to set up KVM-based virtualization, select Virtualization Host. If you’re setting up virtual guests (or other dedicated physical servers), select Server with GUI. During a Red Hat exam, you’ll be installing most additional software after basic operating system installation is complete. Other options are listed in [Table 1-3](#ch01.xhtml_ch1tab3).

FIGURE 1-13 Software Selection screen

![Images](F01-13.jpg)

TABLE 1-3 Installation Software Categories

![Images](f0035-01.jpg)

For a truly secure baseline in a production environment, consider the minimal installation. Fewer packages mean fewer vulnerabilities. You can then add just the packages needed for the desired functionality. Any software that isn’t installed can’t be exploited by a “black hat” hacker.

![Images](job.jpg)

**In the security world, the term “white hat” hackers refers to good people who break into systems for nonmalicious reasons, such as for a security penetration test. The term “black hat” hackers refers to people who want to break into other systems with evil intent.**

#### Baseline Packages

In this section, you’ll get a basic overview of what’s available during the RHEL 9 installation process. During the exams, you may refer to one of these package groups with the Red Hat Add/Remove Software tool. You can also find a list of available package groups with the **dnf group list** command. More information is available in [Chapter 4](#ch04.xhtml).

Red Hat package groups are organized logically. It’s important to choose only the package groups you need. Fewer installed packages means more room for personal files, as well as the log files needed to monitor systems.

For the purposes of this installation, select Server with GUI from the Software Selection screen shown in [Figure 1-13](#ch01.xhtml_ch1fig13). Click the Root Password option and enter a password for the root administrative user twice. Later during the installation, you can create a regular user for the system. Finally, click Done and then click Begin Installation. Anaconda then proceeds to the installation process.

#### During the Installation

After the installation of the software packages is initiated, you will see the screen shown in [Figure 1-14](#ch01.xhtml_ch1fig14).

FIGURE 1-14 Installing the RPM packages

![Images](F01-14.jpg)

When the installation is complete, you’ll see a final message to that effect, with an option to reboot the system. Don’t forget to remove the installation DVD image; otherwise, the system may boot again from the DVD media. To do so, select the Virtual Machine menu, click Removable Devices, and under CD/DVD click Disconnect.

#### Initial Setup

Upon completion of the installation process, when RHEL 9 boots to the graphical user interface for the first time, the Initial Setup screen will appear, as shown in [Figure 1-15](#ch01.xhtml_ch1fig15). Follow these steps:

FIGURE 1-15 The Initial Setup screen

![Images](F01-15.jpg)

1.   At the Initial Setup screen, you can enable or disable location services and connect your online accounts, such as Google or Microsoft. Click Skip to go to the next screen.

2.   Create a regular user account by providing a username and password of your choice.

3.   Click Start Using Enterprise Linux.

4.   On a RHEL 9 system, you’re offered to take a tour of the system. If you are new to RHEL 9, click Take Tour.

5.   You’re prompted to connect the system to the Red Hat Subscription Management. To register, you’ll need a Red Hat account with an available subscription, which you should have obtained in Exercise 1-1\. However, you will complete the registration of the system in [Chapter 4](#ch04.xhtml).

#### CERTIFICATION SUMMARY

The RHCSA exam is not for beginners. It’s a hands-on, practical test that assesses your abilities on a live RHEL system through problem-solving and system configuration tasks. The examination primarily focuses on evaluation of your core system administration skills, simulating real-world scenarios.

RHEL 9 supports different architectures. For the RHCSA exam, you need a system with an Intel/AMD 64-bit CPU (also known as x86_64 architecture).

This chapter helped you to obtain and install a basic RHEL system, with the packages and settings suitable for the remainder of this book. With a subscription to the Red Hat Customer Portal, you can download RHEL installation ISO files from the associated account. Since RHEL software is released under open-source licenses, third parties such as AlmaLinux OS Foundation have used that source code to build a new Linux distribution without Red Hat trademarks. You can also use AlmaLinux to study for the RHCSA exam.

This chapter also helped you to create and configure an installation of RHEL 9 to practice the skills you’ll learn in subsequent chapters. You’ll configure a second system in upcoming Lab 1\. Although many users don’t have spare physical computers to dedicate to their studies, VMs make it possible to set up these systems on a single physical computer.

Because the installation of RHEL 9 is relatively easy even for newer Linux users, not every detail was covered in this chapter. After installation comes the Initial Setup screen. However, this varies depending on whether you’ve installed a GUI.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 1](#ch01.xhtml).

##### The RHCSA Exam

![Images](squ1.jpg)   The RHCSA exam is a separate exam from the RHCE exam.

![Images](squ1.jpg)   Red Hat exams are all “hands-on”; there are no multiple-choice questions.

##### Basic Hardware Requirements

![Images](squ1.jpg)   Although RHEL 9 can be installed on several different platforms, you’ll need hardware with 64-bit CPUs and hardware-assisted virtualization for the RHCSA exam.

![Images](squ1.jpg)   Red Hat supports RHEL 9 installations on systems with at least 1.5GiB of RAM. Less is possible, especially on systems without a GUI.

![Images](squ1.jpg)   RHEL 9 can be installed on a local drive or a variety of storage network devices.

##### Get Red Hat Enterprise Linux

![Images](squ1.jpg)   The RHCSA exam uses Red Hat Enterprise Linux.

![Images](squ1.jpg)   Production and development subscriptions of RHEL 9 are available.

![Images](squ1.jpg)   Since Red Hat releases the source code for RHEL 9, third parties are free to “rebuild” the distribution from the Red Hat source code (except for the trademarks).

![Images](squ1.jpg)   A rebuild of RHEL 9 is functionally identical to the original, except for access to Red Hat Customer Portal to download software packages.

![Images](squ1.jpg)   Reputable third-party rebuilds are available, such as AlmaLinux.

##### An Environment for Practice Labs

![Images](squ1.jpg)   Red Hat states that exams are presented on “pre-installed systems” with questions presented “electronically.”

![Images](squ1.jpg)   The native RHEL 9 VM solution is KVM. In this book, we use VMware Workstation Player, because it is open source and freely available for Linux and Windows operating systems.

![Images](squ1.jpg)   It’s useful to set up multiple VMs to simulate network communications.

##### RHEL 9 Installation

![Images](squ1.jpg)   You can start the installation process from a variety of boot media.

![Images](squ1.jpg)   RHEL 9 can be installed from DVD, from a local drive, from an NFS directory, from a web server, or from an FTP server.

![Images](squ1.jpg)   RHEL 9 should be configured on separate volumes for at least the top-level root directory (/), the /boot directory, and Linux swap space.

![Images](squ1.jpg)   RHEL 9 includes installation package groups in a number of categories.

![Images](squ1.jpg)   The first post-installation steps involve the Initial Setup screen.

#### Q SELF TEST

The following questions will help you measure your understanding of the material presented in this chapter. Because there are no multiple-choice questions on the Red Hat exams, there are no multiple-choice questions in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams.

##### The RHCSA Exam

**[1.](#ch01.xhtml_ch1ques1)**   How many multiple-choice questions are there on the RHCSA exam?

**[2.](#ch01.xhtml_ch1ques2)**   How much time is allocated for installation during the RHCSA exam?

##### Basic Hardware Requirements

**[3.](#ch01.xhtml_ch1ques3)**   Assuming Intel-based PC hardware, what’s the default virtualization technology for RHEL 9?

**[4.](#ch01.xhtml_ch1ques4)**   Which Intel/AMD CPU architectures can be used on RHEL 9?

##### Get Red Hat Enterprise Linux

**[5.](#ch01.xhtml_ch1ques5)**   Name one third-party distribution based on RHEL 9 source code.

##### An Environment for Practice Labs

**[6.](#ch01.xhtml_ch1ques6)**   Is VMware Workstation Player a type-1 or type-2 hypervisor?

##### RHEL 9 Installation

**[7.](#ch01.xhtml_ch1ques7)**   Name two different options for installation media that will boot the RHEL 9 installation program.

**[8.](#ch01.xhtml_ch1ques8)**   Name two types of volumes that can be configured and formatted during the RHEL 9 installation process to store data.

**[9.](#ch01.xhtml_ch1ques9)**   What are the different types of base environments available in the Software Selection screen that is accessed from the Installation Summary screen?

**[10.](#ch01.xhtml_ch1ques10)**   What application is started during the first boot of a new RHEL 9 system?

#### LAB QUESTIONS

The first lab is fairly elementary, aimed to complete the installation of the environment for practice labs that you have started in this chapter. The second lab suggests that you look at the requirements associated with the Linux Professional Institute for a different perspective on system administration.

##### Lab 1

In this lab, you will install the tester1.example.com system described earlier in [Table 1-2](#ch01.xhtml_ch1tab2). To do so, follow the steps you performed earlier to install server1.example.com in the “Configure a Virtual Machine on VMware Workstation Player” and “RHEL 9 Installation” sections.

Select a text-based installation and perform a minimal installation.

##### Lab 2

The Red Hat exams are an advanced challenge. In this lab, you’ll examine the Red Hat exam prerequisites from a slightly different perspective. If you’re uncertain about your readiness for the RHCSA exam, the Linux Professional Institute (LPI) has Level 1 exams that test basic skills in more detail. In addition, they cover a number of related commands that we believe are implied prerequisites for the Red Hat certifications.

To that end, examine the detailed objectives associated with LPIC-1 exams 101 and 102\. Links to those objectives are available at [https://www.lpi.org/our-certifications/lpic-1-overview](https://www.lpi.org/our-certifications/lpic-1-overview). If you’re comfortable with most of the files, terms, and utilities listed in the objectives for those exams, you’re ready to start your studies for the Red Hat exams.

#### A SELF TEST ANSWERS

##### The RHCSA Exam

**[1.](#ch01.xhtml_r_ch1ques1)**   There are no multiple-choice questions on any Red Hat exams. It has been more than a decade since the Red Hat exams had a multiple-choice component. The Red Hat exams are entirely “hands-on” experiences.

**[2.](#ch01.xhtml_r_ch1ques2)**   There is no correct answer to this question. Although the Red Hat exams are now presented on pre-installed systems, keep in mind that requirements may change at any time.

##### Basic Hardware Requirements

**[3.](#ch01.xhtml_r_ch1ques3)**   The default virtualization technology for RHEL 9 is KVM. Although there are many excellent virtualization products available, KVM is the default option supported by Red Hat on RHEL 9.

**[4.](#ch01.xhtml_r_ch1ques4)**   To install RHEL 9, you need a system with one or more 64-bit CPUs.

##### Get Red Hat Enterprise Linux

**[5.](#ch01.xhtml_r_ch1ques5)**   AlmaLinux is one of the distributions built on RHEL 9\. CentOS Linux was discontinued in 2021.

##### An Environment for Practice Labs

**[6.](#ch01.xhtml_r_ch1ques6)**   VMware Workstation Player is a type-2 (or “hosted”) hypervisor, because it runs on a conventional operating system such as Linux, macOS, or Windows.

##### RHEL 9 Installation

**[7.](#ch01.xhtml_r_ch1ques7)**   Options for installation boot media for RHEL 9 include a DVD, and a USB drive.

**[8.](#ch01.xhtml_r_ch1ques8)**   You can configure and format regular partitions and logical volumes during the installation process to store data.

**[9.](#ch01.xhtml_r_ch1ques9)**   The base environments are Server with GUI, Server, Minimal Install, Workstation, Custom Operating System, and Virtualization Host.

**[10.](#ch01.xhtml_r_ch1ques10)**   Initial Setup is started during the first boot.

#### LAB ANSWERS

##### Lab 1

This lab assumes you’ve downloaded the DVD ISO image for RHEL 9, as explained in the section “Get Red Hat Enterprise Linux” in this chapter. Follow the same steps you performed to create a virtual machine for the server1.example.com system in “Configure a Virtual Machine on VMware Workstation Player,” but set the system name to tester1.example.com. Next, install RHEL 9 by following the instructions in the “RHEL 9 Installation” section. Refer to the partitioning scheme in [Table 1-1](#ch01.xhtml_ch1tab1) and be sure to configure the network settings provided in [Table 1-2](#ch01.xhtml_ch1tab2).

Once you have completed the installation, you will have a tester1.example.com virtual machine identical to server1.example.com, except for the hostname and IP address settings.

##### Lab 2

This lab may seem odd given that it references the requirements for a different Linux certification. However, many Linux administrators take the exams of the Linux Professional Institute seriously. LPI creates excellent certifications. Many Linux administrators study for the LPIC Level 1 certification. Passing the LPIC-1 101 and 102 exams provides an excellent foundation for the RHCSA exam.

If you feel the need to get more of a grounding in Linux, refer to either or both of the books described at the beginning of this chapter.

The Red Hat exams are an advanced challenge. Some of the requirements for the RHCSA exam may seem intimidating. It’s okay if some of them seem beyond your capabilities at the moment, because that is the reason you are reading this book. However, if you’re uncomfortable with basic command-line tools such as **ls**, **cd**, and **cp**, you might need more of a grounding in Linux first. Most candidates are successfully able to fill in the gaps in their knowledge with some self-study and practice.

## Chapter 2

## Fundamental Command-Line Skills

CERTIFICATION OBJECTIVES

[2.01     Shells](#ch02.xhtml_ch2obj01)

[2.02     Standard Command-Line Tools](#ch02.xhtml_ch2obj02)

[2.03     File Permissions](#ch02.xhtml_ch2obj03)

[2.04     Managing Text Files](#ch02.xhtml_ch2obj04)

[2.05     Accessing the Documentation](#ch02.xhtml_ch2obj05)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

The Red Hat exams are an advanced challenge. This chapter covers RHCSA requirements related to essential Linux command-line tools. Many of these requirements specify basic command-line tools associated with entry-level certifications such as those offered by the Linux Professional Institute.

While command-line skills are no longer official prerequisites, they are required to achieve the exam objectives. As most candidates for the RHCSA exam should already be familiar with these command-line tools, this chapter covers the related topics with minimum detail. If after reading this chapter you feel the need for more guidance about these topics, the excellent beginning Linux books described in [Chapter 1](#ch01.xhtml) can help.

Linux gurus should recognize that we’ve “oversimplified” a number of explanations to keep this chapter as short as possible. However, because most IT professionals are specialists, you may feel a bit uncertain about a few topics in this chapter. That is okay. In fact, it’s natural that many experienced Linux administrators don’t frequently use every command. Many candidates are successfully able to fill in the gaps in their knowledge with some self-study and practice.

INSIDE THE EXAM

**Shells**

The related RHCSA exam objective is pretty generic:

![Images](square.jpg)   Access a shell prompt and issue commands with correct syntax

The default shell for Linux is bash, the “Bourne-again shell.” In fact, the original release of the RHCSA objectives specified the use of bash. Whatever shell you prefer, you need to know how to get to a shell prompt and run regular commands from that prompt. Some basic commands are described in some of the other objectives. It’s fairly easy to open a shell prompt from a console and within the GUI.

**Pipelines and Redirection**

Data into and out of a shell is often thought of in Linux as a stream of information. One basic Linux skill is the ability to redirect

such streams. As described in the RHCSA requirements, that’s the ability to

![Images](square.jpg)   Use input/output redirection (>, >>, |, 2>, etc.)

The operators in parentheses can redirect the streams from command output, command error, data files, and more.

**File and Directory Management**

Now that you have access to a command line, file and directory management is next. With related commands, you can navigate around the Linux directory tree, as well as perform all the tasks suggested in the related objectives:

![Images](square.jpg)   Create, delete, copy, and move files and directories

![Images](square.jpg)   Create hard and soft links

**File Permissions**

Security in Linux starts with the permissions given to files. As “everything is a file” in Linux, assigning file permissions is an excellent start to implementing security. In any case, the related exam objectives, once understood, are fairly straightforward:

![Images](square.jpg)   List, set, and change standard ugo/rwx permissions

![Images](square.jpg)   Diagnose and correct file permissions problems

![Images](square.jpg)   Manage default file permissions

Standard permissions for Linux files are defined for users, groups, and others, which leads to the *ugo* concept. Those permissions are read, write, and execute, or *rwx.*

**The Analysis of Text Output**

Most Linux configuration files are text files. It is important to understand and analyze the flow of text as it is sent to the terminal or “piped” through different commands. Tools such as the **grep** command can help you focus on needed information. In this chapter, you will examine how to meet the following objective:

![Images](square.jpg)   Use grep and regular expressions to analyze text

**The Use of Text Editors**

To configure Linux, you need to know how to edit text files. And for those newer to Linux, that requires a different paradigm. Although word processors such as OpenOffice.org Writer and Microsoft Word can save files in text format, a mistake with a key configuration file can render a Linux system unbootable, and these editors can inject hidden data or otherwise cause problems when used for simple text editing. Therefore, you need to know how to handle the following objective with standard non-GUI utilities:

![Images](square.jpg)   Create and edit text files

**The Variety of Local Documentation**

Internet access is not available during the Red Hat exams, but that’s okay. Google is not your only friend. Linux has some excellent documentation installed with most packages. Command manuals are also available. The following objective is straightforward; it describes the commands and directory associated with most Linux online documentation:

![Images](square.jpg)   Locate, read, and use system documentation including man, info, and files in /usr/share/doc

### CERTIFICATION OBJECTIVE 2.01

### Shells

A *shell* is a user interface. A text-based shell is also used as a command-line interpreter. In Linux, the shell is the interpreter that allows you to interact with the operating system using various commands. With the right file permissions, you can set up commands in scripts to run as needed, even at a certain time. Linux shells can process commands in various sequences, depending on how you manage the input and output of each command. The way commands are interpreted is in part determined by variables and parameters associated with each shell.

As previously introduced, the default shell in Linux is bash, so the focus of commands in this book is based on how they’re used in bash. However, a number of other shells are available that are popular with many users. As long as the appropriate RPMs are installed, users can start any of these shells. If desired, you can change the default shell for individual users in the /etc/passwd file.

#### Other Shells

Users can choose between four command-line shells in RHEL 9\. Although bash is the default, longtime Linux and Unix users may prefer something else. This is a partial list of the most common shells:

![Images](square.jpg)   **bash** The default Bourne-again shell, based on the command-line interpreter originally developed by Stephen Bourne

![Images](square.jpg)   **ksh** The Korn shell, developed by David Korn at Bell Labs in the 1980s, to incorporate the best features of the Bourne-again and C shells

![Images](square.jpg)   **tcsh** An enhanced version of the Unix C shell

![Images](square.jpg)   **zsh** A sophisticated shell, similar to the Korn shell

These shells are located in the /bin directory. If a user prefers one of these options as their default shell, it’s easy to change. The most direct method is to change the default shell in the /etc/passwd file. For example, the line that applies to one of the authors’ regular accounts is

`michael:x:1000:1000:Michael Jang:/home/michael:/bin/bash`

As an example, to change the default shell to ksh, change /bin/bash to /bin/ksh. You also need to install the corresponding RPM package for the Korn shell. Package management will be covered in [Chapter 4](#ch04.xhtml).

#### Virtual Consoles

If you have access to the console of a RHEL system, you can use six virtual consoles (or “virtual terminals”) to open six independent login sessions. However, only one virtual console is activated by default. The other login prompts are launched dynamically when you switch to an unused terminal. Virtual consoles are defined by the logind.conf file in the /etc/systemd directory. If you look at that file, you’ll see an option named NAutoVTs, which defines the maximum number of virtual consoles that can be activated. Virtual consoles are associated with device files /dev/tty1 through /dev/tty6\. When a GUI is configured, it takes /dev/tty1.

Normally, to change between virtual consoles, press ALT and the function key associated with that terminal. For example, the ALT-F3 key combination moves to the third terminal. However, in the RHEL GUI, the ALT-F*n* key combinations are used to provide other functionalities, such as to start the Run Application tool via ALT-F3. Therefore, you’ll need to press CTRL-ALT-F*n* to move to the *n*th virtual console from the GUI.

![Images](exam.jpg)

**Even though it should be trivial for most Linux users, a part of one RHCSA objective is to “access a shell prompt.” You should now know how to set up access to different shell prompts.**

At a text console login, you’d see the following prompt, which depends a bit on the release of RHEL, the version number of the kernel, and the system hostname:

![Images](f0047-01.jpg)

The graphical login, which requires the installation of the GNOME Display Manager (GDM), is more intuitive, as shown in [Figure 2-1](#ch02.xhtml_ch2fig1).

FIGURE 2-1 A first GUI login console

![Images](F02-01.jpg)

#### GUI Shell Interfaces

Once you are logged in to the GUI, access to the bash shell is easy. If you’re in the default GNOME desktop environment, choose Activities | Terminal. Traditionally, administrators have worked from the console. But in many cases, working on the command line from the GUI can be helpful, especially because you can place windows side by side. A right-click on a GUI terminal screen supports opening of additional terminals in different windows or in tabs. It also supports copy and paste as needed.

The screenshots of the command line taken for this book are from the GUI-based command line using a “Light” theme, in part because dark text on a white screen is easier to read. To change the theme of your GNOME terminal, choose Edit | Preferences and click the General tab, as shown in [Figure 2-2](#ch02.xhtml_ch2fig2).

FIGURE 2-2 Option to change the GNOME terminal theme

![Images](F02-02.jpg)

#### Differences Between Regular and Administrative Users

What you can do at the command line depends on the privileges associated with the login account. Two basic prompts are available. The following is an example of what you might see when logged in as a regular user:

`[michael@server1 ~]$`

Note how it includes the username, the hostname of the local system, the current directory, and a $ prompt. The $ prompt is the standard for regular users. As noted in the introduction to the book, examples of commands run from a regular user account just show the following:

`$`

In contrast, take a look at a prompt for the root administrative user on the same system. It should look familiar. Except for the name of the account, the only consistent difference is the prompt.

`[root@server1 ~]#`

In this book, examples of commands run from the root administrative account just show the following:

`#`

Besides ownership and permissions, other differences between regular and administrative accounts are discussed in [Chapter 6](#ch06.xhtml).

#### Standard Streams and Command Redirection

Linux uses three basic data streams. Data goes in, data comes out, and errors are sent in a different direction. These streams are known as standard input (*stdin*), standard output (*stdout*), and standard error (*stderr*). Every process has the stdin, stdout, and stderr configured to a device. Normally, input comes from the keyboard, whereas standard output and standard error go out to the screen terminal. In the following example, when you run **cat /etc/fstab**, the contents of the /etc/fstab file are sent to the screen as standard output (as are any errors):

`# cat /etc/fstab`

You can redirect each of these streams to or from a file. For example, if you have a program named database and a datafile with a lot of data, the contents of that datafile can be sent to the database program with a left redirection arrow (<). As shown here, datafile is taken as standard input:

`# database < datafile`

Standard input can come from another command as well. For example, if you need to scroll through the boot messages, you can combine the **dmesg** and **less** commands with a pipe:

`# dmesg | less`

![Images](job.jpg)

**The sequence of commands separated by a pipe symbol is a *pipeline*.**

The output from **dmesg** is redirected as standard input to **less**, which then allows you to scroll through that output as if it were a separate file.

Standard output is just as easy to redirect. For example, the following command uses the right redirection arrow (**>**) to send the standard output of the **ls** command, which lists the contents of the current directory, to the file named filelist.txt:

`# ls > filelist.txt`

![Images](exam.jpg)

**Command redirection symbols such as >, >>, 2>, and | are associated with the “input/output redirection” objective in the RHCSA exam objectives.**

The file filelist.txt will be created if it does not exist. If it does exist, its contents will be overwritten. You can add standard output to the end of an existing file with a double redirection arrow with a command such as **ls >> filelist.txt**.

If you want to save the error messages of a program into a file, redirect the error stream from it with a command such as the following:

`# program 2> err-list.txt`

Sometimes you may want to discard all errors. This can be achieved by redirecting the error stream to the special device file /dev/null:

`# program 2> /dev/null`

Another useful redirection operator is the ampersand and right arrow (&>), which sends both the standard output and error to a file or device. An example is shown here:

`# program &> output-and-error.txt`

Another way to achieve the same result is shown next:

`# program > output-and-error.txt 2>&1`

Here, the first operator (>) sends the standard output to the file indicated, while the next operator (2>&1) sends the standard error stream to the same file as standard output.

[Table 2-1](#ch02.xhtml_ch2tab1) summarizes the redirection operators that we have described so far.

TABLE 2-1 Redirection Operators

![Images](f0051-01.jpg)

### CERTIFICATION OBJECTIVE 2.02

### Standard Command-Line Tools

While newer Linux users may prefer to use the GUI, the most efficient way to administer Linux is from the command-line interface. Although excellent GUI tools are available, the look and feel of those tools varies widely by distribution. In contrast, if you know the standard command-line tools, you’ll be able to find your way around every Linux distribution.

Remember, in any bash session you can go through the history of previous commands, using the UP- and DOWN-ARROW keys, and use CTRL-R to make a search. You can also take advantage of text completion, which allows you to use the TAB key almost as a wildcard to complete a command, a filename, or a variable (if the text begins with the **$** character).

![Images](exam.jpg)

**This section covers only the most basic of commands available in Linux. It describes only a few capabilities of each command. Nevertheless, it allows you to “issue commands with correct syntax,” as described in the RHCSA objectives.**

Almost all Linux commands include options (or “switches”) and arguments. Command options allow you to change the behavior of a command and are usually prepended by one or two dashes (such as **ls -a** or **ls --all**). Arguments specify files, devices, or other targets that a command should act on. Only a few commands are covered in this chapter. If you’re less familiar with some of them, use the documentation. Study the command options. Try them out! Only with practice, practice, and more practice can you really understand the power behind some of these commands.

Two basic groups of commands are used to manage Linux files. One group helps you get around Linux files and directories. The other group actually does something creative with the files. Those commands will be covered in the next sections, but first we’ll review some basic filesystem concepts.

#### File and Directory Concepts

As noted previously, everything in Linux can be reduced to a file. Directories are special types of files that serve as containers for other files. To navigate and find important files, you need some basic commands and concepts to tell you where you are and how to move from directory to directory. One of the most important commands is **pwd**, which prints the current directory; a variable that always points to a user’s home directory is the tilde (~); and the concept that describes where you are in the Linux directory tree is the path. Closely related are the directories searched when a command is typed in, which is based on the environment variable known as the PATH. Once these concepts are understood, you can navigate between directories with the **cd** (short for “change directory”) command.

##### pwd

At the command-line interface, the current directory may be either the top-level root (/) directory or a subdirectory. The **pwd** command identifies the current directory. Try it out. It’ll give you a directory name relative to the / directory. With this information in hand, you can move to a different directory if needed. Incidentally, **pwd** is short for “print working directory” (which has nothing to do with modern printers, but respects the days when output was printed on a teletype). For example, when the user michael runs that command in his home directory, he gets the following output:

`/home/michael`

##### The Tilde (~)

Upon a standard login, every Linux user is taken to a home directory. The tilde (~) can be used to represent the home directory of any currently active user. For example, when user john logs in, he’s taken to his home directory, /home/john. In contrast, the home directory of the root administrative user is /root.

Thus, the effect of the **cd ~** command depends on your home directory. For example, if you’ve logged in as user mj, the **cd ~** command navigates to the /home/mj directory. If you’ve logged in as the root user, this command navigates to the /root directory. You can list the contents of your home directory from anywhere in the directory tree with the **ls ~** command. The **cd** and **ls** commands are described shortly. When you log in as the root administrative user and run the **ls** command, you should see the following filename being listed:

`anaconda-ks.cfg`

Incidentally, this file describes what happened during the installation process, the packages that were installed, and the users and groups added to the local system. The **anaconda-ks.cfg** command is also important for automated Kickstart installations, but this is outside the scope of the RHCSA exam.

##### Directory Paths

You need to know two path concepts when working with Linux directories: absolute paths and relative paths. An absolute path describes the complete directory structure in terms of the top-level directory, root (/). A relative path is based on the current directory. Relative paths do not start with a slash. However, they may initiate with “./”. The dot symbol signifies the current directory in this context.

The difference between an absolute path and a relative one is important. Commands referencing a wrong directory by using a relative path may lead to unintended consequences. For example, say you’re in the top-level root directory /, and you have backed up the /home directory using its relative path to the root, home (notice the lack of a leading slash). If you happen to be in the /home directory when restoring that backup, the files for user michael, for example, would be restored to the /home/home/michael directory.

In contrast, if the /home directory was backed up using the absolute path /home (notice the leading slash), the current working directory doesn’t matter when you are restoring these files. That backup will be restored to the correct directories.

##### PATH Environment Variable

PATH is a special environment variable that a shell, such as bash, will search for executable commands. PATH contains a list of directories that are searched for the command that the user just typed at the command prompt. Strictly speaking, it is best to use the full path to a command, such as **/bin/ls** instead of **ls**. In practice, this is tedious, which is why the PATH environment variable was created. The only place absolute paths are recommended is in shell scripts or when the PATH is unknown or inconsistent across various machines. There is normally no need to use absolute paths when entering commands in an interactive shell, unless the command happens to be in a directory that is not in your PATH.

To determine the PATH for the current user account, run the **echo $PATH** command. You should see a series of directories in the output. The differences between the PATH for a regular user and one for a root user are shown next::

![Images](f0053-01.jpg)

The directories in the PATH for regular users and the root administrative user are slightly different. But the differences matter because the directories are searched in order. For example, the **useradd** command is available from the /usr/sbin directory. As you can see from the default PATH for regular and root users, the command is not in the PATH of regular users, since /usr/sbin is not in the list.

The PATH is determined globally by current settings in the /etc/profile file or by scripts in the /etc/profile.d directory.

As well as the global settings, the PATH for individual users can be customized with an appropriate entry in that user’s home directory, in the hidden files named ~/.bash_profile or ~/.profile.

##### cd

It’s easy to change directories in Linux. Just use **cd** and cite the absolute path of the desired directory. If you use the relative path, just remember that the destination depends on the current working directory.

By default, the **cd** command with no arguments navigates to your home directory. The tilde is not required for that command. Another common shortcut is two consecutive dots (..) to represent the directory that is one level up in the hierarchy. Thus, **cd ..** moves to the parent directory of the current working directory.

#### File Lists and ls

Now that you’ve reviewed those commands that can navigate from one directory to another, it’s time to see what files exist in a directory—and that’s the province of the **ls** command.

The Linux **ls** command (short for “list”), with the right switches, can be quite powerful. The right kind of **ls** can tell you everything about a file, such as last modification time, last access time, and size. It can help you organize the listing of files in just about any desired order. Important variations on this command include **ls -a** to reveal hidden files (which are files whose names begin with a dot, “.”), **ls -l** for long listings, **ls -t** for a list sorted by modification time, and **ls -i** for inode numbers (inodes are internal data structures in a filesystem that store information about a file). Other useful command options are **-r**, to reverse the listing order, and **-R**, to list the contents of all subdirectories recursively.

You can combine switches; we often use the **ls -ltR** command to display a recursive long listing with the most recently changed files last. The **-d** switch, when combined with others, can give you more information on the current directory, or on a directory that you have passed as an argument to the **ls** command.

One important feature that returns SELinux contexts is the **ls -Z** command. Take a look at the output in [Figure 2-3](#ch02.xhtml_ch2fig3). The system_u, object_r, var_t, and s0 output demonstrates the current SELinux contexts of the noted files. During the RHCSA exam (and RHCE as well), you’ll be expected to configure a system with SELinux enabled. Starting with [Chapter 8](#ch08.xhtml), this book covers how SELinux can be configured for every service that’s installed.

FIGURE 2-3 Current SELinux contexts

![Images](F02-03.jpg)

#### File-Creation Commands

Two commands are used to create new files: **touch** and **cp**. Alternatively, you can let a text editor such as vi create a new file. Although the **ln**, **mv**, and **rm** commands don’t create files, they do manage them in related ways.

##### touch

Perhaps the simplest way to create a new empty file is with the **touch** command. For example, the **touch abc** command creates an empty file named abc in the local directory. The **touch** command is also used to change the time of the last modification of a file. For example, try the following three commands:

![Images](f0055-02.jpg)

Note the timestamps listed with the output of each **ls -l** command, and compare them with the current date and time returned by **date**. After you run the **touch** command, the timestamp of /etc/passwd is updated to the current date and time.

##### cp

The **cp** (copy) command allows you to take the contents of one file and place a copy with the same or different name in the directory of your choice. For example, the **cp *file1 file2*** command takes the contents of *file1* and saves the contents in *file2* in the current directory. One of the dangers of **cp** is that it can easily overwrite files in different directories, without prompting you to make sure that’s what you really wanted to do.

Another usage of the **cp** command is with multiple file sources to be copied into a single destination directory. In this case the syntax is **cp *file1 file2 ... dir***.

The **cp** command, with the **-a** switch, supports recursive changes and preserves all file attributes, such as permissions, ownerships, and timestamps. For example, the following command copies all subdirectories of the noted directory, along with associated files, into /mnt/backup:

`# cp -a /home/michael/. /mnt/backup/`

##### mv

Although there is a “rename” command in Linux, you can use **mv** (short for “move”). The **mv** command puts a different label on a file. For example, the **mv *file1 file2*** command changes the name of *file1* to *file2*. Unless you’re moving the file to a different filesystem, everything about the file, including the inode number, remains the same.

The **mv** command can also be used to move files and directories into the directory specified as the last argument. The following example creates two files named “a” and “b” in the current directory and then moves them into the /tmp directory:

![Images](f0056-02.jpg)

##### ln

Linked files allow users to refer to the same file using different names. When linked files are devices, they may represent more common names, such as /dev/cdrom. File links can be hard or soft.

Hard links are directory entries (or “dentries”) that point to the same inode. They must be created within the same filesystem. You could delete a hard-linked file in one directory, and it would still exist in the other directory (files are only deleted when the number of dentry records pointing to them hits 0, which is tracked via a counter per file). For example, the following command creates a hard link from the actual Samba configuration file to smb.conf in the /root directory:

`# ln /etc/samba/smb.conf /root/smb.conf`

On the other hand, a soft link serves as a redirect; when you open a file created with a soft link, the link redirects you to the original file. If you delete the original file, the file is lost. Although the soft link is still there, it has nowhere to go. The following command is an example of how you can create a soft-linked file:

`# ln -s /etc/samba/smb.conf /root/smb.conf`

##### rm

The **rm** command is somewhat dangerous. At the Linux command line, there is no trash bin. So if you delete a file with the **rm** command, it’s at best difficult to recover that file.

The **rm** command is powerful. For example, let’s assume that you downloaded the source files for the Linux kernel in the /root/rpmbuild/BUILD/kernel-5.14.0-162.el9_1 directory. Several thousand files are included in that directory. If you don’t need those files anymore, obviously it’s not practical to delete them one by one. Therefore, the **rm** command includes some powerful switches. The following command removes all of those files in one go:

`# rm -rf /root/rpmbuild/BUILD/kernel-5.14.0-162.6.1.el9_1`

The **-r** switch works recursively, and the **-f** switch overrides any safety precautions, such as the **-i** switch (which prompts for confirmation) shown in the output to the **alias** command for the root administrative user. It’s still quite a dangerous command. For example, a simple typing mistake such as putting a space between the first forward slash and the directory name, as shown here, would first delete every file starting with the top-level root directory (/) before looking for the root/rpmbuild/BUILD/kernel-5.14.0-162.6.1.el9 subdirectory:

`# rm -rf / root/rpmbuild/BUILD/kernel-5.14.0-162.6.1.el9_1`

This would delete every file on the system, and you would have to restore all its contents from backup.

##### Directory Creation and Deletion

The **mkdir** and **rmdir** commands are used to create and delete directories. The ways these commands are used depend on the already-discussed concepts of absolute and relative paths. For example, the following command creates the test subdirectory to the current directory. If you’re currently in the /home/michael directory, the full path would be /home/michael/test.

`# mkdir test`

Alternatively, the following command creates the /test directory:

`# mkdir /test`

If desired, you can use the following command to create a series of directories:

`# mkdir -p test1/test2/test3`

That command is equivalent to the following commands:

![Images](f0058-01.jpg)

Conversely, the **rmdir** command deletes a directory only if it’s empty. If you’re cleaning up after the previous **mkdir** commands, the **-p** switch is useful there as well. The following command deletes the noted directory and subdirectories, as long as all of the directories are otherwise empty:

![Images](f0058-02.jpg)

##### alias

The **alias** command can be used to simplify a few commands. For the root administrative user, the default aliases provide a bit of safety. To see the aliases for the current user, run the **alias** command. The following output shows some of the default Red Hat aliases for the root user:

![Images](f0058-03.jpg)

Some of these aliases help protect key files from mistakes. The **-i** switch prompts the user for confirmation before a file is deleted or overwritten with the **cp**, **mv**, or **rm** command. Just be aware, the **-f** switch supersedes the **-i** switch for the noted commands.

#### Wildcards

Sometimes you may not know the exact name of the file or the exact search term. That is when a wildcard is handy, especially with the commands described throughout the book. Three basic wildcards are shown in [Table 2-2](#ch02.xhtml_ch2tab2).

TABLE 2-2 Wildcards in the Shell

![Images](f0059-01.jpg)

![Images](job.jpg)

**The use of wildcards is sometimes known in the Linux world as *globbing*.**

#### File Searches

Most users who study Linux for a while become familiar with key files. For example, named.conf is the key configuration file for the standard DNS (Domain Name Service) servers, based on the Berkeley Internet Name Domain (BIND). But not many people remember that a sample named.conf file, with all kinds of useful configuration hints, can be found in the /usr/share/doc/bind/sample/etc directory.

To that end, there are two basic commands for file searches: **find** and **locate**.

##### find

The **find** command searches through directories and subdirectories for a desired file. For example, if you wanted to find the directory with the named.conf DNS sample configuration file, you could use the following command, which would start the search in the root directory:

`# find / -name named.conf`

But the speed of that search depends on the memory and disk speed available on the local system. Alternatively, if you know that this file is located in the /usr subdirectory tree, you could start in that directory with the following command:

`# find /usr -name named.conf`

That command should now find the desired file more quickly.

##### locate

If this is all too time-consuming, RHEL allows you to set up a database of installed files and directories. Searches with the **locate** command are almost instantaneous—and **locate** searches don’t require the full filename. The drawback is that the **locate** command database is normally updated only once each day.

![Images](exam.jpg)

**When you take Red Hat exams, you can run** updatedb **early on to find needed files more quickly later on without delay.**

### CERTIFICATION OBJECTIVE 2.03

### File Permissions

The basic security of a Linux computer is based on file permissions. Default file permissions are defined by the **umask** command. Special permissions can be configured to give all users and/or groups additional privileges. These are known as the set user ID (SUID), set group ID (SGID), and sticky permission bits. Ownership is based on the default user and group IDs of the person who created a file. The management of permissions and ownership involves commands such as **chmod**, **chown**, and **chgrp**. Before exploring these commands, it’s important to understand the permissions and ownership associated with a file.

#### File Permissions and Ownership

Linux file permissions and ownership are straightforward. As suggested by the related RHCSA objective, they’re read, write, and execute, classified by the user, the group, and all other users. However, the effect of permissions on directories is more subtle. [Table 2-3](#ch02.xhtml_ch2tab3) shows the exact meaning of each permission bit.

TABLE 2-3 Permissions on Files and Directories

![Images](f0060-01.jpg)

Consider the following output from **ls -l /sbin/fdisk**:

`-rwxr-xr-x. 1 root root 175376 Sep 21 10:45 /sbin/fdisk`

The permissions are shown on the left side of the listing. Ten characters are shown. The first character determines whether it’s a regular file or a special file. In this example, the first character is a dash (-), which indicates that this is a regular file. The remaining nine characters must be read in groups of three, and each group applies, respectively, to the file owner (user), the group owner, and everyone else on that Linux system. The letters are straightforward: *r* = read, *w* = write, *x* = execute. These permissions are described in [Table 2-4](#ch02.xhtml_ch2tab4).

TABLE 2-4 Description of File Permissions

![Images](f0061-01.jpg)

Hence, in the previous example, the root user has rwx permissions to the /sbin/fdisk file, while the root group and everyone else have only rx permissions. It’s common for the user and group owners of a file to have the same name. In this case, the root user is a member of the root group. But they don’t have to have the same name. For example, directories designed for collaboration between users may be owned by a special group. As explained in [Chapter 6](#ch06.xhtml), that involves groups with several regular users as members.

Keep in mind that permissions granted to the group take precedence over permissions granted to all other users. Similarly, permissions granted to the owner take precedence over all other permissions categories. Thus, in the following example, although everyone else has full permissions to the file, the members of the group “mike” have not been granted any permissions, and as such they won’t be able to read, modify, or execute the file:

![Images](f0061-03.jpg)

There’s a relatively new element with permissions—and it’s subtle. Notice the dot after the last x in the output to the **ls -l setup.sh** command? It specifies that the file has an SELinux security context. If you’ve configured ACL permissions on a file, that dot is replaced by a plus sign (+). But that symbol doesn’t override SELinux control.

You need to consider another type of permission: the special permission bits. These include the SUID and SGID bits and another special permission known as the *sticky bit*. The effects of the special permission bits on files and directories are shown in [Table 2-5](#ch02.xhtml_ch2tab5).

TABLE 2-5 Special Permission Bits

![Images](f0062-01.jpg)

An example of the SUID bit is associated with the **passwd** command in the /usr/bin directory. Executing the **ls -l** command on that file leads to the following output:

![Images](f0062-02.jpg)

The **s** in the execute bit for the user owner of the file is the SUID bit. It means the file can be executed by other users with the authority of the file owner, the root administrative user. But that doesn’t mean that any user can change other users’ passwords. Access to the **passwd** command is further regulated by Pluggable Authentication Modules (PAM), although this is out of scope of the RHSCA exam. The SUID permission is required because the user’s password is stored in /etc/shadow, and that file can be accessed only by the root user.

An example of the SGID bit can be found with the **locate** command, also in the /usr/bin directory. Executing the **ls -l** command on that file displays the following output:

![Images](f0062-03.jpg)

The **s** in the execute bit for the group owner of the file (group nobody) is the SGID bit. The **locate** command has the SGID bit set because it keeps track of all the files in the system in the database /var/lib/mlocate/mlocate.db, which is readable only by the root and slocate users.

Finally, an example of the sticky bit can be found in the permissions of the /tmp directory. It means that users can copy their files to that directory, but no one else can remove those files, apart from their respective owners (which is the “sticky”). The **ls -ld** command on that directory shows the following output:

![Images](f0062-04.jpg)

The **t** in the execute bit for other users is the sticky bit. Note that without the sticky bit, everyone will be able to remove everyone else’s files in /tmp because write permissions have been granted to all users on that directory.

##### The Loophole in Write Permissions

It’s easy to remove write permissions from a file. For example, if you wanted to make the license.txt file read-only, the following command removes write permissions from that file:

![Images](f0063-01.jpg)

You may notice that, under certain conditions, if a change is made in the vi text editor, the user who owns that file can override a lack of write permissions with the bang character, which looks like an exclamation point (!). In other words, while in the vi editor, the user who owns the file can run the following command to override the lack of write permissions:

`w!`

Although this may seem surprising, in practice the **w!** command of the vi editor is not bypassing the Linux file permission system. The **w!** command overwrites a file—that is, it deletes the existing file and creates a new one with the same name. As you can see from [Table 2-3](#ch02.xhtml_ch2tab3), the permission bit that grants the privilege to create and delete files is the write permission on the parent directory, not the write permission on the file itself. Hence, if a user has write permission on a directory, she can overwrite the files in it, regardless of the write permission bits set on files.

#### Commands to Change Permissions and Ownership

Key commands that can help you manage the permissions and ownership of a file are **chmod**, **chown**, and **chgrp**. In the following subsections, you’ll examine how to use those commands to change permissions along with the user and group that owns a specific file, or even a series of files.

One tip that can help you change the permissions on a series of files is to use the **-R** command option. It is the recursive switch for all three of these commands. In other words, if you specify the **-R** switch with any of the noted commands on a directory, it applies the changes recursively. The changes are applied to all files in that directory, including all subdirectories. *Recursion* means that the changes are also applied to files in each subdirectory, and so on.

##### The chmod Command

The **chmod** command uses the numeric value of permissions associated with the owner, group, and others. In Linux, permissions are assigned the following numeric values: *r* = 4, *w* = 2, and *x* = 1\. In numerical format, permissions are represented by an octal number, where each digit is associated with a different group of permissions. For example, the permission number 640 means that the owner is assigned permission 6 (4 + 2, read and write), whereas the group has permission 4 (read) and everyone else has no permissions. The **chown** and **chgrp** commands adjust the user and group owners associated with the cited file.

The **chmod** command is flexible. You don’t always have to use numbers. For example, the following command sets execute permissions for the user owner of the script.sh file:

`# chmod u+x script.sh`

Note how the **u** and the **x** follow the ugo/rwx format specified in the associated RHCSA objective. To interpret, this command adds (with the plus sign) for the user owner of the file (with the **u**) execute permissions (with the **x**).

These symbols can be combined. For example, the following command disables (with the minus sign) write permissions (with the **w**) for the group owner (with the **g**) and all other users (with the **o**) on the local file named document.txt:

`# chmod go-w document.txt`

Rather than adding or removing permissions with the + and − operators, you can set the exact mode of a permission group using the equal operator (=). As an example, the following command changes the group permissions of the file named document.txt to read and write and clears the execute permission if it was set:

`# chmod g=rw document.txt`

While you can use all three group permission types in the **chmod** command, it’s not necessary. The following command makes the script.sh file executable by all users:

`# chmod +x script.sh`

For the SUID, SGID, and sticky bits, some special options are available. If you choose to use numeric bits, those special bits are assigned numeric values as well, where SUID = 4, SGID = 2, and sticky bit = 1\. However, to define the special bits you need one more digit in the octal representation. For example, the following command configures the SUID bit (with the first 4 digits in permission mode). It includes rwx permissions for the user owner (with the 7), rw permissions for the group owner (with the 6), and r permissions for other users (with the last 4) on the file named testfile:

`# chmod 4764 testfile`

If you’d rather use the ugo/rwx format, the following command activates the SGID bit for the local testscript file:

`# chmod g+s testscript`

And the following command turns on the sticky bit for the /test directory:

`# chmod o+t /test`

For the **chmod** command, changes don’t have to be made by the root administrative user. The user owner of a file is allowed to change the permissions associated with her files.

##### The chown Command

The **chown** command can be used to modify the user who owns a file. For example, take a look at the ownership for the first figure that we created for this chapter, based on the **ls -l** command:

`-rw-r--r--. 1 michael examprep 855502 Oct 25 14:07 F02-01.tif`

The user owner of this file is michael; the group owner of this file is examprep. The following **chown** command changes the user owner to user elizabeth, but must be executed as root:

`# chown elizabeth F02-01.tif`

You can do more with **chown**; for example, the following command changes both the user and group owner of the noted file to user donna and group supervisors, assuming that user and group already exist:

`# chown donna.supervisors F02-01.tif`

Only the root administrative user can change the user owner of a file, whereas group ownership can be modified by root and also by the user who owns the file.

##### The chgrp Command

You can change the group owner of a file with the **chgrp** command. For example, the following command changes the group owner of the noted F02-01.tif file to the group named project (assuming it exists):

`# chgrp project F02-01.tif`

##### Special File Attributes

In addition to regular rwx/ugo permissions, files also have attributes. Such attributes can help you control what anyone can do with different files. Whereas the **lsattr** command lists current file attributes, the **chattr** command can help you change those attributes. For example, the following command protects /etc/fstab from accidental deletion, even by the root administrative user:

`# chattr +i /etc/fstab`

With that attribute, if you try to delete the file as the root administrative user, you’ll get the following response:

![Images](f0065-06.jpg)

The **lsattr** command shows an active “immutable” attribute on /etc/fstab:

![Images](f0066-02.jpg)

Of course, the root administrative user can unset that attribute with the following command. Nevertheless, the initial refusal to delete the file should at least give pause to that administrator before changes are made.

`# chattr -i /etc/fstab`

Several key attributes are described in [Table 2-6](#ch02.xhtml_ch2tab6). Other attributes, such as **c** (compressed), **s** (secure deletion), and **u** (undeletable), don’t work for files stored in the ext4 and XFS filesystems.

TABLE 2-6 File Attributes

![Images](f0066-01.jpg)

#### A Basic Introduction of User and Group Concepts

Linux, like Unix, is configured with users and groups. Everyone who uses Linux is set up with a username, even if it’s just “guest.” There’s even a standard user named “nobody.” Take a look at /etc/passwd. An excerpt from this file is shown in [Figure 2-4](#ch02.xhtml_ch2fig4).

FIGURE 2-4 The /etc/passwd file

![Images](F02-04.jpg)

As shown, all kinds of usernames are listed in the /etc/passwd file. Even a number of Linux services such as mail, news, ftp, and apache have their own usernames. In any case, the /etc/passwd file follows a specific format, described in more detail in [Chapter 6](#ch06.xhtml). For purposes of this discussion, note that the only regular users shown in this file are alex and michael; their user IDs (UID) and group IDs (GID) are, respectively, 1000 and 1001; and their home directories match their usernames. The next user gets UID and GID 1002, and so on.

This matching of UIDs and GIDs is based on the Red Hat user private group scheme. Now run the **ls -l /home** command. The output should be similar to the following:

![Images](f0066-04.jpg)

Pay attention to the permissions. Based on the rwx/ugo concepts described earlier in this chapter, only the named user owner has access to the files in his or her home directory.

##### The umask

Every time you create a new file, the default permissions are based on the value of umask. When you type the **umask** command, the command returns a four-digit octal number such as 0002\. If a bit of the umask is set, then the corresponding permission is disabled in newly created files and directories. To find the relevant permission bits, you need to subtract the umask value from the number 777 (or 666 for a file). As an example, a umask of 0245 would cause newly created directories to have 0532 octal permissions (0777 – 0245 = 0532), which is equivalent to the following permission string:

`r-x-wx-w-.`

In the past, the value of umask affected the value of all permissions on a file. For example, if the value of umask was 000, the default permissions for any file created by that user were once 777 – 000 = 777, which corresponds to read, write, and execute permissions for all users. They’re now 666, since regular new files can no longer get executable permissions when they are created. Directories, on the other hand, require executable permissions so that any file contained therein can be accessed.

##### The Default umask

With that in mind, the default umask is driven by the /etc/profile and /etc/bashrc files, specifically the following stanza, which drives a value for umask depending on the value of the UID:

![Images](f0068-01.jpg)

In other words, the umask for user accounts with UIDs of 200 and above is 002\. In contrast, the umask for UIDs below 200 is 022\. In RHEL 9, service users such as adm, postfix, and apache have lower UIDs; this affects primarily the permissions of the log files created for such services. Of course, the root administrative user has the lowest UID of 0\. By default, files created for such users have 644 permissions (666 – 022 = 644); directories created for such users have 755 permissions (777 – 022 = 755).

In contrast, regular users have a UID of 1000 and above. Files created by such users normally have 664 permissions. Directories created by such users normally have 775 permissions. Users can override the default settings by appending a **umask** command in their ~/.bashrc or ~/.bash_profile.

### CERTIFICATION OBJECTIVE 2.04

### Managing Text Files

Linux and Unix are typically managed through a series of text files. Linux administrators do not normally use graphical editors to manage these configuration files. Editors such as OpenOffice.org Writer or Microsoft Word normally either save files in a binary format or change the encoding of plain-text files. Unless text files are preserved in their original format, changes that are made can render a Linux system unbootable.

Linux commands have been set up to manage text files as streams of data. You’ve seen tools such as redirection arrows and pipes. However, that data can be overwhelming without tools that can sort through that data. Even before files are edited, it’s important to know how to read these files at the command-line interface.

#### Commands to Read Text Streams

Previously, you reviewed commands such as **cd**, **ls**, and **pwd** that can help you get around Linux filesystems. With commands such as **find** and **locate**, you reviewed how to identify the location of desired files.

Now it’s time to start reading and processing the content of files. Most Linux configuration files are text files. Linux editors are text editors. Linux commands are designed to read text files. To identify the types of files in the current directory, try the **file *** command.

##### cat

The most basic command for reading files is **cat**. The **cat *filename*** command scrolls the text within the *filename* file. It also works with multiple filenames; it concatenates the filenames that you might list as one continuous output to your screen. You can redirect the output to the file of your choice, as described in the earlier section “Standard Streams and Command Redirection.”

##### less and more

Larger files demand command utilities that can help you scroll through the file text at your leisure. These utilities are known as *pagers*, and the most common are **more** and **less**. With the **more *filename*** command, you can scroll through the text of a file, from start to finish, one screen at a time. With the **less *filename*** command, you can scroll in both directions through the same text with the PAGE UP, PAGE DOWN, and arrow keys. Both commands support vi-style searches.

As the **less** and **more** commands do not change files, they’re an excellent way to scroll through and search for items in a large text file such as an error log. For example, to search through the basic /var/log/messages file, run the following command:

`# less /var/log/messages`

You’ll then be able to scroll up and down the log file for important information. You can use the forward slash and question mark to search forward or backward through the file. For example, once you’ve run the command just shown, you’ll be taken to a screen similar to that shown in [Figure 2-5](#ch02.xhtml_ch2fig5).

FIGURE 2-5 The less pager and /var/log/messages

![Images](F02-05.jpg)

To search forward in the file for the term “error,” type the following in the pager:

`/error`

To search in the reverse direction, substitute a **?** for the **/**.

The **zless** variant of the **less** command has one more feature unavailable to commands such as **more** and **cat**: it can read text files compressed in gzip format, normally shown with the .gz extension. For example, the man pages associated with many standard commands that are run in the shell can be found in the /usr/share/man/man1 directory. All of the files in this directory are compressed in .gz format. Nevertheless, the **zless** command can read those files.

And that points to the operation of the **man** command. In other words, these two commands are functionally equivalent:

![Images](f0069-03.jpg)

##### head and tail

The **head** and **tail** commands are separate tools that work in essentially the same way. By default, the **head *filename*** command looks at the first 10 lines of a file; the **tail *filename*** command looks at the last 10 lines of a file. You can specify the number of lines shown with the **-n *xy*** switch. For example, the **tail -n 15 /etc/passwd** command lists the last 15 lines of the /etc/passwd file.

The **tail** command can be especially useful for problems in progress. For example, if there’s an ongoing problem with failed login attempts, the following command monitors the noted file and displays new lines on the screen as new log entries are recorded:

`# tail -f /var/log/secure`

#### Commands to Process Text Streams

A text stream is the movement of data. For example, the **cat *filename*** command streams the data from the *filename* file to the terminal. When these files get large, it’s convenient to have commands that can filter and otherwise process these streams of text.

Linux includes simple commands to help you search, check, or sort the contents of a file. In addition, there are special files that contain others; some of these container files are known colloquially as “tarballs.” We will explore tarballs in [Chapter 9](#ch09.xhtml).

![Images](job.jpg)

**Tarballs are a common way to distribute Linux packages. Packages are normally distributed in a compressed format, with a .tar.gz or .tgz file extension, consolidated as a package in a single file.**

##### sort

You can sort the contents of a file in a number of ways. By default, the **sort** command sorts the contents in alphabetical order, depending on the first letter in each line. For example, the **sort /etc/passwd** command would sort all users (including those associated with specific services and such) by username.

##### grep

The **grep** command uses a search term to look through a file. It returns the full line that contains the search term. For example, **grep 'Michael Jang' /etc/passwd** looks for the name of this user in the /etc/passwd file.

You can use regular expressions within a **grep** command. Regular expressions provide a powerful way to specify complex search patterns. Some of the characters that have a special meaning inside a regular expression are shown in [Table 2-7](#ch02.xhtml_ch2tab7). If you want a metacharacter to lose its special meaning and be taken literally, precede it by a blackslash (\).

TABLE 2-7 Special Characters in Regular Expressions

![Images](f0071-01.jpg)

The **grep** command supports some useful switches. To make the search case-insensitive, you can pass the **-i** option to the command line. The **-E** option enables the use of extended regular expression syntax. Another interesting switch is **-v**, which reverses the matching logic—that is, it tells **grep** to select only the lines that do *not* match a regular expression.

As an example, suppose you want to select only the lines from /etc/nsswitch.conf that are not blank and do not contain a comment (that is, they do not start with the # character). This can be achieved by running the following command:

`# grep -v '^$' /etc/nsswitch.conf | grep -v '^#'`

Note how the first **grep** command selects all the lines that are not blank (the regular expression that matches a blank line is **^$**—that is, start of line and immediate end of line). Then, the output is piped to a second **grep** command, which excludes all the lines that start with a hash character.

The same result can be obtained with a single instance of **grep** and the **-e** switch, which allows you to specify multiple search patterns on the same command:

`# grep -v -e '^$' -e '^#' /etc/nsswitch.conf`

For more information on regular expressions, type **man 7 regex**.

##### diff

One useful option to find the difference between files is the **diff** command. If you’ve just used a tool such as the Network Manager Connection Editor described in [Chapter 3](#ch03.xhtml), it’ll modify a file such as eth0.nmconnection in the /etc/NetworkManager/system-connections directory.

If you’ve backed up that eth0.nmconnection file, the **diff** command can identify the differences between the two files. For example, the following command identifies the differences between the eth0.nmconnection file in the /root and the /etc/NetworkManager/system-connections directories:

![Images](f0072-03.jpg)

The -u option in the **diff** command represents the “unified format.” This format not only highlights the differences between files but also displays several surrounding lines for context. This contextual view facilitates a clearer understanding of the variations in relation to the adjacent content.

##### wc

The **wc** command, short for “word count,” can return the number of lines, words, and characters in a file. The **wc** options are straightforward; for example, **wc -l *filename*** returns the number of lines in that file.

##### sed

The **sed** command, short for “stream editor,” allows you to search for and change specified words or even text streams in a file. For example, the following command exchanges the first instance of the word “Windows” with “Linux” in each line of the file opsys and writes the result to the file newopsys:

`# sed 's/Windows/Linux/' opsys > newopsys`

However, this may not be enough. If there’s more than one instance of “Windows” in a line in the opsys file, it does not change the second instance of that word. But you can fix this by adding a “global” suffix:

`# sed 's/Windows/Linux/g' opsys > newopsys`

The following example would make sure that all Samba shares configured with the **writable = yes** directive are reversed:

`# sed 's/writable = yes/writable = no/g' /etc/samba/smb.conf > ~/smb.conf`

Of course, you should then review the results in the /root/smb.conf file before overwriting the original /etc/samba/smb.conf file.

##### awk

The **awk** command, named for its developers (Aho, Weinberger, and Kernighan), rather than a command, is more of a full programming language. It can identify lines with a keyword and read out the text from a specified column in that line. A common example is with the /etc/passwd file. For example, the following command will read out the fourth field in /etc/passwd (the group ID) of every user with a listing of “mike”:

`# awk -F : '/mike/ {print $4}' /etc/passwd`

#### Edit Text Files at the Console

The original version of the RHCSA objectives specified the use of the Vim editor. Strictly speaking, it doesn’t matter what text editor you use to edit text files. However, we believe that you need to know how to use the Vim editor, and apparently most system administrators agree. The Vim editor is short for “vi, improved.” When installed, the Vim editor can be started with the **vi** command. Hereafter, we refer to that text editor as vi.

We think every administrator needs at least a basic knowledge of vi. Although emacs would also be a valid choice, vi may help you save a broken system. If you ever have to restore a critical configuration file using emergency boot media, vi may be the only editor you’ll have available.

While RHEL 9 also includes access to the more intuitive nano editor, a knowledge of vi commands can help you in searching and editing key sections of text files more quickly. Although the RHEL boot media supports more console-based editors, vi is one of the most feature-rich and efficient editors available on Linux.

You should know how to use the two basic modes of vi: command and insert. When you use vi to open a file, it opens in command mode. Some of the commands start insert mode. Opening a file is easy: just use the **vi *filename*** command.

The following is only the briefest of introductions to the vi editor. For more information, there are several books available on the topic, as well as a tutorial that you can start through the **vimtutor** command.

##### vi Command Mode

In command mode, you can do everything to a text file except edit it. The options in command mode are broad and varied, and they are the subject of a number of book-length texts. In summary, options in vi command mode fall into seven categories:

![Images](square.jpg)   **Open** To open a file in the vi editor from the command-line interface, run the **vi *filename*** command.

![Images](square.jpg)   **Search** For a forward search, start with a backslash (**/**), followed by the search term. Remember, Linux is case sensitive, so if you’re searching for “Michael” in /etc/passwd, use the **/Michael** command. For a reverse search, start with a question mark (**?**).

![Images](square.jpg)   **Close** To leave vi, use the **:q** command.

![Images](square.jpg)   **Abandon** If you want to abandon any changes, use the **:q!** command.

![Images](square.jpg)   **Write** To save your changes, use the **w** command. You can combine commands; for example, **:wq** writes the file and exits vi.

![Images](square.jpg)   **Edit** You can use a number of commands to edit files through vi, such as **x**, which deletes the currently highlighted character; **dw**, which deletes the currently highlighted word; and **dd**, which deletes the current line. Remember, **yy** copies the current line into a buffer, **p** places text from a buffer, and **u** restores text from a previous change.

![Images](square.jpg)   **Insert** A number of commands allow you to start insert mode, including **i** to start inserting text at the current position of the editor and **o** to open up a new line immediately below the current position of the cursor. To exit insert mode, press the ESC key.

##### Basic Text Editing

In modern Linux systems, editing files with vi is easy. Just use the normal navigation keys (arrow keys, PAGE UP, and PAGE DOWN), and then one of the basic commands such as **i** or **o** to start vi’s insert mode, and type your changes directly into the file.

When you’re finished with insert mode, press the ESC key to return to command mode. You can then save your changes, or abandon them and exit vi.

[Table 2-8](#ch02.xhtml_ch2tab8) summarizes the Vim commands that we have encountered in this section.

TABLE 2-8 Vim Commands

![Images](f0075-01.jpg)

![Images](job.jpg)

**If you find Vim too cryptic, type** vimtutor**. This is a short, interactive tutorial that will take you about 25–30 minutes to complete. If, after completing the tutorial, you still don’t like Vim, consider an alternative editor, as explained in the next section.**

![Images](job.jpg)

**There are several specialized variations of the** vi **command:** vipw **edits /etc/passwd,** vigw **edits /etc/group, and** visudo **edits /etc/sudoers. The benefit of these commands is that they set appropriate locks to prevent file corruption.**

EXERCISE 2-1

**Using vi to Create a New User**

In this exercise, you’ll create a new user by editing the /etc/passwd file with the vi text editor. Although there are other ways to create new Linux users, which we will cover in more detail in [Chapter 6](#ch06.xhtml), this exercise helps you verify your skills with vi and at the command-line interface.

1.   Open a Linux command-line interface. Log in as the root user and type the **vipw** command. This command uses the vi editor to open /etc/passwd.

2.   Navigate to the end of the file. There are several ways to do this in command mode, including the DOWN ARROW key, the PAGE DOWN key, and the **G** command.

3.   Identify a line associated with a regular user. If you’ve just created a new user, it should be the last line in the file. If a regular user does not yet exist, identify the first line, which should be associated with the root administrative user, with the number 0 in the third and fourth columns.

4.   Make one copy of this line. If you’re already comfortable with vi, you should know that you can copy an entire line to the buffer with the **yy** command. This “yanks” the line into the buffer. You can then restore or insert that line as many times as desired with the **p** command.

5.   Change the username, user ID, group ID, user comment, and home directory for the new user. For detailed information on each entry, see [Chapter 6](#ch06.xhtml). For example, in the following illustration, this corresponds to tweedle, 1001, 1001, Tweedle Dee, and /home/tweedle. Make sure the username also corresponds to the home directory.

![Images](f0076-01.jpg)

6.   Return to command mode by pressing the ESC key. Save the file with the **:w** command, and then exit with the **:q** command. (You can combine the two commands in vi; the next time you make a change and want to save and exit, run the **:wq** command.)

7.   You should see the following message:

![Images](f0076-02.jpg)

That message can be ignored because the next step adds appropriate information to the /etc/shadow file. However, you don’t need to modify /etc/shadow directly.

8.   As the root user, run the **passwd *newuser*** command. Assign the password of your choice to the new user. For this example, the new user is tweedle.

9.   The process is not yet complete; every user needs a group. To that end, run the **vigr** command. Repeat the earlier steps that copied an appropriate line from near the end of the file. Note that group names and group ID numbers normally are identical to their usernames and user ID numbers.

10.   All you need to change for the new entry is the group name and group ID number. Based on the information shown in the previous illustration, this would be a group name of tweedle and a group number of 1001.

11.   Repeat the aforementioned **:wq** command to close vi and save the change.

12.   Pay attention to the following message:

![Images](f0077-01.jpg)

13.   As suggested, run the **vigr -s** command to open the /etc/gshadow file. You’ll note that there’s less information in this file. Once a copy is made of an appropriate line, all you’ll need to do is change the group name.

14.   Repeat the aforementioned **:wq** command to close vi and save the change. Actually, you’ll get a message that suggests that the file is read-only. You’d have to run **:wq!** in this case to write to this “read-only” file, overriding current settings.

15.   Additional steps are required to properly set up the new user related to that user’s home directory and standard files from the /etc/skel directory. However, if you completed this exercise correctly, you should be able to log in with the new username. For more information on users, see [Chapter 6](#ch06.xhtml).

#### If You Don’t Like vi

If you absolutely hate vi, you can use nano, a small and friendly editor. By default, when you run commands such as **edquota** and **crontab**, they open configuration files using the vi editor. To change the default editor used by system commands to nano, run

`# export EDITOR=/bin/nano`

To change the default editor for all users, add the preceding line to the /etc/environment configuration file:

`# echo 'export EDITOR=/bin/nano' >> /etc/environment`

Because the nano editor is fairly intuitive, as shown in [Figure 2-6](#ch02.xhtml_ch2fig6), instructions will not be provided in this book. The full manual is available at [https://www.nano-editor.org](https://www.nano-editor.org).

FIGURE 2-6 The /etc/nsswitch.conf file opened with the nano editor

![Images](F02-06.jpg)

Similar changes can be made if you prefer a different editor, such as emacs.

#### Edit Text Files in the GUI

No question, the Red Hat exams have become friendlier for users of the GUI. The gedit text editor was even included for a short time in the RHCSA objectives. More traditional Linux administrators may have been horrified. (The gedit editor has since been deleted from the objectives.)

Once gedit is installed, you can start it by choosing Activities | Show Applications | Text Editor. Because it is an intuitive GUI text editor, its use is trivial. Don’t obsess about editors; they are just tools on exams and in real life.

However, if you’re editing configuration files on remote systems, it’s possible that you won’t have access to gedit on that system, especially if the GUI hasn’t been installed there. You could start gedit and forward the application display to the GUI on your local machine using a feature called X forwarding. But many administrators set up VMs without the GUI to save disk space and system resources.

### CERTIFICATION OBJECTIVE 2.05

### Accessing the Documentation

Although there’s no Internet access allowed during Red Hat exams, there is a lot of documentation available already installed on a RHEL 9 system. It starts with the man pages, which document the options and settings associated with most commands and many configuration files. It continues with the info documents. Although fewer commands and files have such documents, when available, they do provide even more information.

Many packages include extensive documentation in the /usr/share/doc directory. Just apply the **ls** command to that directory. Every subdirectory there includes information about the capabilities of each associated package.

#### When You Need Help

The first thing we usually do when we need help with a command is to run it by itself. If more information is required, the command prompts with a request for more information, including a variety of options. As an example, look at the output to the following command:

`$ dnf`

If that approach doesn’t work, generally some amount of help is available with the **-h** or the **--help** switch. Sometimes a mistake leads to some hints; the output to the following command suggests legal options to the **cd** command:

![Images](f0079-02.jpg)

Sometimes the **-h** switch is more helpful; take a look at the output to the **fdisk -h** command. But the **-h** option doesn’t always show a help message; in that case, the **--help** switch may serve that purpose. Look at [Figure 2-7](#ch02.xhtml_ch2fig7) as an example, which displays the output to the **ls --help** command.

FIGURE 2-7 Help with the ls command

![Images](F02-07.jpg)

#### A Variety of man Pages

Few people can remember every switch to every command. That’s one reason why command documentation is so important. Most Linux commands are documented in a format known as the man page. If you run the **man** command by itself, RHEL returns the following message:

`What manual page do you want?`

For example, say you need to set up a logical volume but have forgotten the switches associated with the **lvextend** command. To browse the man page for that command, run **man lvextend**. As with many other commands, there’s an EXAMPLES section, like that shown in [Figure 2-8](#ch02.xhtml_ch2fig8). If you’ve run the **lvextend** command before, that section may help jog your memory.

FIGURE 2-8 Examples from the lvextend man page

![Images](F02-08.jpg)

Such man pages are available for most configuration files and commands. However, there may be more. So what if you’re not sure about the name of the man page? In that case, the **whatis** and **apropos** commands can help. For example, to find the man pages with “nfs” in the title, run the following command:

`# whatis nfs`

If you want to find the man pages with nfs in the description, the following command can identify related commands:

`# apropos nfs`

However, if you’ve just installed a service such as httpd, associated with the Apache web server, commands such as **whatis httpd** and **apropos apachectl** probably won’t provide any information. These commands work from a database in the /var/cache/man directory. You can update that database by starting the man-db-cache-update service. The following command updates the database of man pages:

`# mandb`

If you encounter a situation, such as during a Red Hat exam, where the associated man page is not installed, there are at least three possible reasons. The associated functional software package may not be installed. The RPM package named man-pages may also not be installed. In some cases, there is a package specifically dedicated to documentation that must be installed separately. For example, there’s an httpd-manual package installed separately from the Apache web server.

In some cases, multiple man pages are available. Take a look at the following output to the **whatis smbpasswd** command:

![Images](f0081-02.jpg)

The numbers (5) and (8) are associated with different sections of man pages. If you’re interested in details, they’re shown in the output to the **man man** command. The man page shown by default is the man page associated with the **smbpasswd** command. In this case, if you want the man page for the smbpasswd encrypted password file, run the following command:

`$ man 5 smbpasswd`

To exit from a man page, press **q**.

#### The info Manuals

The list of available info manuals is somewhat limited. However, the coverage of some topics (for example, the bash shell) is usually more extensive than a corresponding man page. For a full list of info documents, run the **ls /usr/share/info** command. When an info manual is not available, a request defaults to the associated man page.

To learn more about the bash shell, run the **pinfo bash** command. **pinfo** has a user interface similar to the Lynx web browser and it is a more user-friendly alternative to the traditional **info** command. As shown in [Figure 2-9](#ch02.xhtml_ch2fig9), info manuals are organized into sections. To access a section, move the cursor to the asterisked entry and press ENTER.

FIGURE 2-9 A sample info manual

![Images](F02-09.jpg)

To exit from an info page, press **q**.

#### Detailed Documentation in /usr/share/doc

The list of documentation available in the /usr/share/doc directory seems impressive. But the quality of the documentation depends on the work of its developers. The subdirectories include the name and version number of the installed package. Some of these subdirectories include just one file, normally named COPYING, which specifies the license under which the given software was released.

Sometimes, the documentation directory includes useful examples. For example, the sudo/ subdirectory includes sample configuration files and directives for administrative control, which can be helpful when you’re configuring administrators with different privileges.

The documentation may include entire manuals in HTML format. For an example, if you install the pam-docs package, the pam/ subdirectory includes an entire online manual for the Pluggable Authentication Modules (PAM) system.

#### CERTIFICATION SUMMARY

The focus of this chapter is on the basic command-line tools, which were formerly associated with Red Hat exam prerequisites. Those prerequisites have now been incorporated into the main body of the RHCSA objectives.

The command line is the interface of a shell, an interpreter that allows you to interact with the operating system using various commands. Although no shell is specified in the objectives, the default shell in most Linux distributions, including RHEL 9, is bash. You can start a command-line prompt at one of the default consoles or at a terminal in the GUI.

At the bash prompt, you can manage the files and directories through which Linux is configured and organized. Linux configuration files are predominantly in text format, allowing for configuration, search, and modification using various commands. It’s essential to manage file ownership and permissions with the **chown** and **chmod** commands, ensuring appropriate users and groups have access to files and directories. Text files can be analyzed as streams of data that can be interpreted and processed. To edit a text file, you need a text editor such as Vim, nano, or gedit.

Linux documentation is extensive. It starts with command switches such as **-h** and **--help**, which provide hints on what goes with a command. It continues with man and info pages. Many packages include extensive documentation files in the /usr/share/info directory. In many, perhaps most, cases, you do not need Internet access to find the hints needed.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 2](#ch02.xhtml).

##### Shells

![Images](squ1.jpg)   The default Linux shell is bash.

![Images](squ1.jpg)   Six command-line virtual consoles are available by default; if the GUI is installed, it takes over the first virtual console.

![Images](squ1.jpg)   You can open multiple command-line terminals in the GUI.

![Images](squ1.jpg)   Shells work with three data streams: stdin, stdout, and stderr.

![Images](squ1.jpg)   Command redirection allows you to manage streams of data with operators such as >, >>, <, |, and 2>.

##### Standard Command-Line Tools

![Images](squ1.jpg)   Everything in Linux can be reduced to a file.

![Images](squ1.jpg)   Commands such as **pwd** and **cd** can help navigate directories.

![Images](squ1.jpg)   Concepts such as directory paths, the PATH, and the tilde (~) can help you understand and use commands at the shell.

![Images](squ1.jpg)   Basic commands allow you to find needed files and read file contents. These commands include **ls**, **find**, and **locate**.

![Images](squ1.jpg)   File creation and deletion commands include **touch**, **cp**, **ln**, **mv**, and **rm**; corresponding directory creation and deletion commands are **mkdir** and **rmdir**.

![Images](squ1.jpg)   Commands can be customized with the **alias** command.

##### File Permissions

![Images](squ1.jpg)   Standard Linux file permissions are read, write, and execute, which may vary for the user owner, the group owner, and other users.

![Images](squ1.jpg)   Special permissions include the SUID, SGID, and sticky bits.

![Images](squ1.jpg)   Default user permissions are based on the value of the umask.

![Images](squ1.jpg)   Ownership and permissions can be changed with the **chown**, **chgrp**, and **chmod** commands.

![Images](squ1.jpg)   Special file attributes can be listed with the **lsattr** command and modified by the **chattr** command.

##### Managing Text Files

![Images](squ1.jpg)   Linux is managed through a series of text configuration files.

![Images](squ1.jpg)   Text files can be read as streams of data with commands such as **cat**, **less**, **more**, **head**, and **tail**.

![Images](squ1.jpg)   New files can be created, copied, moved, linked, and deleted with the **touch**, **cp**, **mv**, **ln**, and **rm** commands. Commands can be customized with the **alias** command.

![Images](squ1.jpg)   File filters such as the **sort**, **grep**, **wc**, **sed**, and **awk** commands support the processing of text streams.

![Images](squ1.jpg)   Understanding text editors is a critical skill. An earlier version of the RHCSA objectives specified the use of Vim and gedit.

##### Accessing the Documentation

![Images](squ1.jpg)   If you need a hint for a command, try it by itself; alternatively, try the **-h** and **--help** switches.

![Images](squ1.jpg)   Command man pages often include examples; **whatis** and **apropos** can search for man pages on different topics.

![Images](squ1.jpg)   If an info manual is available for a command or file, you’ll find it in the /usr/share/info directory.

![Images](squ1.jpg)   Many packages include extensive documentation and examples in the /usr/share/doc directory.

#### Q SELF TEST

The following questions will help you measure your understanding of the material presented in this chapter. As there are no multiple-choice questions on the Red Hat exams, there are no multiple-choice questions in this book. These questions exclusively test your understanding of the chapter. Getting results, not memorizing trivia, is what counts on the Red Hat exams.

##### Shells

**[1.](#ch02.xhtml_ch2ques1)**   What is the name of the default shell in RHEL 9?

**[2.](#ch02.xhtml_ch2ques2)**   From the GUI, what key combination moves to virtual console 3?

##### Standard Command-Line Tools

**[3.](#ch02.xhtml_ch2ques3)**   What single command creates the /abc/def/ghi/jkl series of directories?

**[4.](#ch02.xhtml_ch2ques4)**   What symbol represents the home directory of the current user?

**[5.](#ch02.xhtml_ch2ques5)**   What command lists all the files whose name starts with the letters ab, contains one extra character, and is followed by one of the digits 1, 2, or 3?

**[6.](#ch02.xhtml_ch2ques6)**   What command lists all the files whose name ends with .conf in the /etc directory?

##### File Permissions

**[7.](#ch02.xhtml_ch2ques7)**   What single command changes the user owner to professor and group owner to assistants for the local file named question2.txt?

##### Managing Text Files

**[8.](#ch02.xhtml_ch2ques8)**   What command lists the last 10 lines of the /var/log/messages file?

**[9.](#ch02.xhtml_ch2ques9)**   What command returns lines with the term Linux from the /var/log/messages file?

**[10.](#ch02.xhtml_ch2ques10)**   What sequence of commands extracts all the lines in /etc/passwd that contain the string /bin/bash and sorts them alphabetically?

**[11.](#ch02.xhtml_ch2ques11)**   What sequence of commands returns all the users whose default shell is bash?

##### Accessing the Documentation

**[12.](#ch02.xhtml_ch2ques12)**   What command searches the database of man pages for manuals that reference the **passwd** command and configuration file?

**[13.](#ch02.xhtml_ch2ques13)**   If there are man pages for the hypothetical **abcde** command and file, in sections 5 and 8, what command is sure to call up the man pages from section 5?

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for each lab follow the Self Test answers.

#### A SELF TEST ANSWERS

##### Shells

**[1.](#ch02.xhtml_r_ch2ques1)**   The default shell in RHEL 9 is bash, also known as the Bourne-again shell.

**[2.](#ch02.xhtml_r_ch2ques2)**   From the GUI, the key combination that moves to virtual console 3 is CTRL-ALT-F3.

##### Standard Command-Line Tools

**[3.](#ch02.xhtml_r_ch2ques3)**   The single command that creates the /abc/def/ghi/jkl series of directories is **mkdir -p /abc/def/ghi/jkl**.

**[4.](#ch02.xhtml_r_ch2ques4)**   The symbol that represents the home directory of the current user is the tilde (~).

**[5.](#ch02.xhtml_r_ch2ques5)**   The command **ls ab?[123]** lists all the files whose name starts with ab, contains one extra character, and is followed by one of the digits 1, 2, or 3.

**[6.](#ch02.xhtml_r_ch2ques6)**   The command **find /etc -name '*.conf'** lists all the files whose name ends with .conf in the /etc directory.

##### File Permissions

**[7.](#ch02.xhtml_r_ch2ques7)**   The single command that changes the user owner to professor and group owner to assistants for the noted file is

`# chown professor.assistants question2.txt`

It’s acceptable to substitute a colon (:) for the dot (.).

##### Managing Text Files

**[8.](#ch02.xhtml_r_ch2ques8)**   The command that lists the last 10 lines of the /var/log/messages file is **tail -n 10 /var/log/messages**. Because 10 lines is the default, **tail /var/log/messages** is also a valid solution.

**[9.](#ch02.xhtml_r_ch2ques9)**   The command that returns lines with the term Linux from the /var/log/messages file is **grep Linux /var/log/messages**. Other variations are acceptable, such as **cat /var/log/messages | grep Linux.**

**[10.](#ch02.xhtml_r_ch2ques10)**   The command **grep /bin/bash /etc/passwd | sort** extracts all the lines in /etc/passwd that contain the string /bin/bash and sorts them alphabetically.

**[11.](#ch02.xhtml_r_ch2ques11)**   There are many ways to answer this question. A possible solution is

`# awk -F: '{print $1" "$7}' /etc/passwd | grep /bin/bash | awk '{print $1}'`

The first **awk** command in the pipeline extracts the first and seventh fields (the username and shell) from each line of /etc/passwd. The result is piped to **grep**, which keeps only the lines that contain /bin/bash. Finally, the last **awk** command selects the first field (the username) from the output. The overall result is that this pipeline returns all the users whose default shell is bash.

##### Accessing the Documentation

**[12.](#ch02.xhtml_r_ch2ques12)**   The command that searches the database of man pages for manuals that reference the **passwd** command and configuration file is **whatis passwd**. The **apropos** and **man -k** commands go further because they list man pages with the text “passwd” in the command or the description.

**[13.](#ch02.xhtml_r_ch2ques13)**   The command that calls up the man page from section 5 for the hypothetical **abcde** command and file is **man 5 abcde**.

#### LAB ANSWERS

##### Lab 1

This lab is tricky, because it requires you to practice with a bash feature not explained in the chapter. As suggested, type **man bash** and search for the string “brace expansion” (type **/** followed by the search string, then press the N key until you find the relevant section).

**1.**   Create the directory book in your home directory:

`$ mkdir ~/book`

Confirm that the directory exists:

`$ ls -l ~`

**2.**   Change to the new directory and create the files:

![Images](f0088-02.jpg)

The preceding **touch** command is the quickest way to create all the requested files with one operation. Note that the command also creates a Ch00.txt file, which is not requested, so you need to remove it.

**3.**   Remove the book directory and all its contents with the following command:

`$ rm -rf ~/book`

##### Lab 2

You can create the rhcsa directory and lab.txt file with the following commands:

![Images](f0088-04.jpg)

Next, display the contents of the lab.txt file and count the characters in it:

![Images](f0088-05.jpg)

If you didn’t know that **-m** is the **wc** command option to display the number of characters in a file, recall that you can type **man wc** to find that information. To create the archive directory and complete the other tasks in the lab, run

![Images](f0088-06.jpg)

##### Lab 3

First, create a file that contains a list of filenames in the /etc directory whose names end with “conf”:

![Images](f0088-07.jpg)

Note that a normal user would not have permissions to see all the files within the /etc directory. For this reason, you can run the previous command as the root user.

Finally, count the number of lines in the file and display all lines that contain the string “security”:

![Images](f0088-08.jpg)

##### Lab 4

The required commands are shown next:

![Images](f0089-01.jpg)

As you can see, this command line consists of a pipe of two commands:

**1.**   The **awk** command prints the third and first fields for each line of the /etc/passwd file, where fields are separated by a colon (:) character.

**2.**   The output of the **awk** command is redirected to the input of the **grep** command, which selects all lines that start with two digits followed by a space character.

##### Lab 5

This lab reinforces the practical understanding of Linux file and directory permissions.

**1.**   Start by creating the directory and the file:

![Images](f0089-02.jpg)

**2.**   Set the ownership for main.log:

![Images](f0089-03.jpg)

**3.**   Adjust permissions for main.log: here, we want the root user to read and write (rw-), the nobody group to have no permissions (---), and others to only read (r--):

![Images](f0089-04.jpg)

**4.**   Set permissions for /var/log/rhcsa directory: we want the root user to have full access (rwx), the owner group to have no permissions (---), and others to access but not list (--x):

![Images](f0089-05.jpg)

**5.**   To verify your changes, you can use the ls command:

![Images](f0089-06.jpg)

**6.**   As a regular user, try to read the file and list the contents of the directory. The first command should execute successfully, while the second will produce an error:

![Images](f0089-07.jpg)

##### Lab 6

This lab gives you the opportunity to practice with Vim. As explained in this chapter, if you do not like Vim, there are alternatives. However, after completing the tutorial, you should be comfortable enough to use Vim for day-to-day operations and, hopefully, you should be able to appreciate its speed and efficiency.

## Chapter 3

## Managing Basic Networking

CERTIFICATION OBJECTIVES

[3.01     A Networking Primer](#ch03.xhtml_ch3obj01)

[3.02     Network Configuration and Troubleshooting](#ch03.xhtml_ch3obj02)

[3.03     An Introduction to IPv6](#ch03.xhtml_ch3obj03)

[3.04     Administration with Secure Shell and Secure Copy](#ch03.xhtml_ch3obj04)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

The RHCSA exam requires that you know how to configure network interfaces and configure hostname resolution. In other words, you need to be prepared to configure IPv4 and IPv6 settings on a network device and to configure your system as a Domain Name Service (DNS) client so that it can resolve hostnames.

Chapter 1 covered the basics of the installation process, and [Chapter 2](#ch02.xhtml) covered basic command-line tools and file editors. The next step is the network configuration, which is covered in this chapter. Once a system is connected to the network, you can connect to it remotely, install packages from a repository, and configure network services.

After you complete the installation of the systems for your test lab, you’ll want to be able to administer them remotely. Understanding SSH connections for remote administration is not only an RHCSA requirement but also an essential skill in the real world.

INSIDE THE EXAM

**IPv4 and IPv6**

Although excellent GUI tools are available to help you manage network services, you should have a strong understanding of command-line tools and configuration files. Command-line tools can help you understand and manage network services directly or through related configuration files. The associated objectives are

![Images](square.jpg)   Configure IPv4 and IPv6 addresses

![Images](square.jpg)   Configure network services to start automatically at boot

![Images](square.jpg)   Start, stop, and check the status of network services

Of course, these objectives require a basic understanding of IP networking.

**Configuration of Name Resolution**

Name resolution depends on databases of hostnames or fully qualified domain names (FQDNs) such as server1.example.com and IP addresses such as 172.16.0.100\. The sources from which Linux obtains name resolution information are usually the local /etc/hosts database of hostnames and IP addresses, as well as available databases of DNS servers. That is what you need to learn for the following RHCSA objective:

![Images](square.jpg)   Configure hostname resolution

While network troubleshooting is no longer a part of the entry-level Red Hat exam, the way you address problems with respect to network configuration and hostname resolution can help you better understand how networks operate.

**Access Remote Systems and Transfer Files Securely**

The RHCSA objectives state that you need to know how to

![Images](square.jpg)   Access remote systems using SSH

![Images](square.jpg)   Securely transfer files between systems

If systems administrators had to be in physical contact with every system, half of their lives would be spent en route from system to system. With tools such as Secure Shell (SSH), administrators can do their work remotely and transfer files securely. Although SSH is automatically installed in a standard configuration in RHEL 9, custom configuration options such as key-based authentication are covered later in the book.

### CERTIFICATION OBJECTIVE 3.01

### A Networking Primer

TCP/IP is a series of protocols organized in layers, known as a protocol suite. It was developed for Unix and eventually adopted as the standard for communication on the Internet. IP addresses identify a network interface in an IP network, and IP addressing is one of the most important concepts of TCP/IP. A number of TCP/IP tools and configurations are available to help you manage a network.

As with the explanations of command-line skills in [Chapter 2](#ch02.xhtml), the description of TCP/IP networking in this section is an oversimplification intended to prepare you for the RHCSA exam, rather than a detailed introduction to TCP/IP networking. If you find this section overwhelming or incomplete, refer to Jang’s and Soyinka’s books listed in the introduction to [Chapter 1](#ch01.xhtml). Linux is built for networking, and there is no practical way to pass any Red Hat exam unless you understand networking in some detail.

Although the focus of current enterprise networks is still on IP version 4 addressing, some organizations have mandated a move toward IP version 6 (IPv6) networks. The focus of this section is on IPv4, whereas IPv6 is covered in a separate section later in this chapter. However, most of the configuration files and tools that are used for IPv4 also apply to IPv6.

#### IPv4 Networks

Every network interface that communicates on a network needs its own IP address. Some addresses are assigned permanently to a network interface; these are known as *static* IP addresses. Others are leased from a Dynamic Host Configuration Protocol (DHCP) server for a limited amount of time; these are known as *dynamic* IP addresses.

IPv4 addresses are 32-bit binary numbers and are usually expressed in “dot-decimal” notation (such as 172.16.0.100), with each decimal octet representing 8 bits. An IP address is made up of two parts: a network (or *subnet*) address and a host part. Until the publication of RFC 1517 in 1993 by the Internet Engineering Task Force ([https://www.ietf.org](https://www.ietf.org)), IP addresses were categorized into different classes, which defined the size of the network and the host part of the address.

Today, IP addresses are usually analyzed using a classless logic. That means that the subnet mask, rather than the address class, is used to determine the network and host parts of an IP address. The old classful addressing scheme introduced by RFC 791 is shown in [Table 3-1](#ch03.xhtml_ch3tab1). Some concepts of RFC 791 still remain in practice today; as an example, the IP range 224.0.0.0–239.255.255.255 is used for multicast addresses.

TABLE 3-1 IP Address Classes

![Images](f0094-01.jpg)

In addition, a number of private IP addresses are not to be assigned to any computer that is directly connected to the Internet. The most common private network ranges are defined in RFC 1918 and are associated with network addresses 10.0.0.0–10.255.255.255, 172.16.0.0–172.31.255.255, and 192.168.0.0–192.168.255.255\. In addition, network addresses 127.0.0.0 through 127.255.255.255 are reserved for loopback communication on a local host.

#### Networks and Routing

As discussed in the previous section, an IP address has two parts: a network part and a host identifier. To determine the network part and the host part, IP addresses are associated with a *subnet mask* (also known as a *netmask* or *prefix*). This is a 32-bit number made of a sequence of binary ones followed by zeros.

The subnet mask can be represented in the same dot-decimal notation used for IPv4 addresses. For example, 255.255.255.0 is a subnet mask made of 24 binary ones and 8 zeros. An alternative notation is known as Classless Inter-Domain Routing (CIDR) notation and consists of a slash character (/) followed by a number that indicates the amount of one bits in the netmask. As an example, the subnet mask 255.255.255.0 can be written as /24 in CIDR notation.

Given an IP address and a subnet mask, all you have to do to determine the network portion of the IP address is provide a logical AND between the IP address and the netmask. For example, given the IP address 172.16.0.100 with netmask /24, the first three bytes of the address (172.16.0) represent the network part, whereas the last byte (100) is the host identifier.

Three key IP components define a network:

![Images](square.jpg)   **Network address** Always the first IP address in a range

![Images](square.jpg)   **Broadcast address** Always the last address in the same range

![Images](square.jpg)   **Subnet mask** Helps your computer define the network portion and the host portion of an IP address

You can assign IP addresses between the network and broadcast addresses (not including these addresses) to any computer on the network. As an example, suppose you are defining the range of addresses for a private network. Start with the private network address 192.168.56.0 and a subnet mask of 255.255.255.0\. Based on this information, the broadcast address is 192.168.56.255, and the range of IP addresses that you can assign on that particular network is 192.168.56.1 through 192.168.56.254\. That subnet mask is also defined by the number of associated bits, 24\. In other words, the given network can be represented by 192.168.56.0/24.

IP addresses are assigned to network interfaces. A host with multiple network interfaces that forwards traffic across different networks is called a *router*. IP hosts separated by other groups of IP hosts by a router must be located in different networks.

Related to networking and routing is the concept of the *default gateway*. It’s a host that defines the junction between the local network and all other networks that your machine does not know how to reach. Although the gateway IP address is part of the local network, that address is assigned to a router, which may have an IP address on a different network, such as the public Internet. The default gateway IP address is normally configured in the routing table for the local system, as defined by the **ip route** command described in the following section.

#### Tools and Commands

Numerous tools are available to manage the TCP/IP protocol suite on your Linux computer. In older versions of Red Hat Enterprise Linux, some of the most important network management commands were **ifconfig**, **arp**, **netstat**, and **route**. Those commands have been deprecated, in favor of the **ip** tool, which supports more advanced features. [Table 3-2](#ch03.xhtml_ch3tab2) provides a list of the deprecated commands along with their equivalent **ip** commands.

TABLE 3-2 The ifconfig, arp, and netstat Commands with Their Equivalent ip Commands

![Images](f0095-01.jpg)

![Images](exam.jpg)

**Even though they are considered “obsolete,” the** ifconfig, arp, **and** netstat **commands are still popular among system engineers. There is no need for you to learn them for the RHCSA exam. However, if you are a longtime Linux user and feel more comfortable with** ifconfig, arp, **and** netstat **installed, you can find them in the *net-tools* RPM package, which is installed by default as part of the Server with GUI installation (software installation is covered in [Chapter 4](#ch04.xhtml)).**

##### A Note on Interface Names

By default, Red Hat Enterprise Linux 9 names network interfaces based on their physical location, such as enoX for onboard Ethernet interfaces and enpXsY for PCI slots. Some naming examples are given in [Table 3-3](#ch03.xhtml_ch3tab3). (RHEL 9 uses the traditional enumeration method of eth0, eth1, etc., only as a fallback choice.) Hence, you may find the first onboard network interface to be named *eno1*, while an interface located on PCI bus 3, slot 0, would be named *enp3s0*.

TABLE 3-3 Ethernet Interface Name Examples

![Images](f0096-01.jpg)

In the examples in this chapter, the network interface in our test system is named eth0\. On your RHEL systems, the name may differ. Don’t obsess over interface names! It’s just a name and does not affect the functionality of any network configuration commands. The old eth*X* naming had the drawback that it was not always consistent, because it was dependent on the order in which network interfaces were detected at boot. The new naming convention in RHEL 9 helps to solve this problem by referring to the physical location of the interface in its name, such as the PCI slot.

##### ping and traceroute

The **ping** and **traceroute** commands are often used to diagnose and troubleshoot network problems. The **ping** command allows you to test connectivity. It can be applied to an IP address on the local system, on the local network, or on a different network, such as on the Internet. For the purpose of this section, assume your IP address is 192.168.56.100 and the default gateway address on the local network is 192.168.56.1\. If you’re having problems connecting to a host, try the following **ping** commands in order. The first step is to test the integrity of TCP/IP on your computer:

`# ping 127.0.0.1`

Normally, **ping** works continuously on Linux; you’ll need to press CTRL-C to stop this command. If you need to verify a proper connection to a LAN, **ping** the IP address of the local network interface:

`# ping 192.168.56.100`

If that works, **ping** the address of another computer on your network. Then start tracing the route to the Internet. **ping** the address for the network gateway (in this case, 192.168.56.1). If possible, **ping** the address of the network’s connection to the Internet, which would be on the other side of the gateway. It may be the public IP address of your router on the Internet. Finally, **ping** the address of a computer that you know is active on the Internet.

You can substitute hostnames such as [www.google.com](http://www.google.com) for an IP address. If the hostname doesn’t work, there is likely a problem with the database of hostnames and IP addresses, more commonly known as a Domain Name System (DNS). It could also indicate a problem with the /etc/hosts configuration file.

The **traceroute** command is provided by the traceroute RPM package (see [Chapter 4](#ch04.xhtml) for information on installing software). **traceroute** automates the process just described by tracking the route path to a destination. For example, the following command finds the path to the IP address 192.168.20.5:

![Images](f0097-03.jpg)

Look at the **-n** option in this command. This tells **traceroute** to display IP addresses rather than hostnames. The command also shows the round-trip time (RTT) to reach each hop along the path. By default, three different probes are sent for each hop.

Please note that some **traceroute** command options require root privileges. Another command that serves the same purpose and is not subjected to this limitation is **tracepath**.

![Images](job.jpg)

**By default,** traceroute **relies on UDP probe packets with an increasing time-to-live (TTL) value in the IP header in order to find the route path to a given destination. Sometimes, a firewall along the path may block UDP packets. In that case, you may try to run** traceroute **with the** -I **or** -T **option to enable ICMP or TCP probe packets, respectively.**

##### Review Current Network Adapters with ip

The **ip** command can display the current state of active network adapters. It also can be used to assign network addresses and more. Run the **ip link show** command to review the link status of the active network adapters on the system. Optionally, include the **-s** switch **(ip -s link show)** if you want to display statistics about network performance.

To review IP address information, try the **ip address show** command, which gives the same output of **ip link show**, but it also includes IP addresses and their properties. The **ip address show eth0** command listed next reflects the current configuration of the Ethernet network adapter:

![Images](f0098-01.jpg)

The **ip** command is flexible. For example, the **ip a s** command is functionally equivalent to **ip addr show** or **ip address show**.

##### Configure a Network Adapter with ip

You can also use **ip** to assign IP address information. For example, the following command adds the noted IP address and network mask to the eth0 network adapter:

![Images](f0098-02.jpg)

The first argument, **172.16.0.50/24**, specifies the new IP address and netmask. The next argument, **dev eth0**, tells you which device is being configured. To make sure the change worked, run the **ip addr show eth0** command again.

With the right options, the **ip** command can modify additional network settings. Some of these options are shown in [Table 3-4](#ch03.xhtml_ch3tab4).

TABLE 3-4 ip Command Options

![Images](f0099-01.jpg)

However, you’ll want to make sure the changes survive a reboot, whether it be for the RHCSA exam or for a server that you want to administer remotely. The **ip** command is useful for troubleshooting or to temporarily configure an IP address for troubleshooting a network problem. It is not the appropriate tool to make changes that persist after a system reboot, because any changes made with the **ip** command are, by definition, temporary. To configure permanent changes to the network configuration, use **nmcli** or manually modify the configuration files in the /etc/NetworkManager/system-connections directory, described shortly.

##### Activate and Deactivate Network Adapters

It’s possible to use the **ip** command to activate and deactivate network adapters. For example, the following commands deactivate and reactivate the first Ethernet adapter:

![Images](f0099-02.jpg)

##### ip as a Diagnostic Tool

The Address Resolution Protocol (ARP) associates the hardware address of a network interface (MAC) with an IP address. The **ip neigh** command displays a table of hardware and IP addresses on the local computer. This command can help detect problems such as duplicate addresses on the network. Such problems may happen with improperly configured systems or cloned virtual machines. If needed, you can use the **ip neigh** command to set or modify ARP table entries manually. As hardware addresses are not routable, an ARP table is limited to the local network. Here’s sample output from the command, showing all ARP entries in the local database:

![Images](f0099-03.jpg)

The first column in the output lists known IP addresses on the LAN, followed by the interface to which the neighbor is attached and its link layer address (MAC address). The last entry shows whether or not the neighbor’s hardware address is reachable. A STALE entry may indicate that its ARP cache timeout has expired since a packet was last seen from that host. If the ARP table is empty, no recent connections exist to other systems on the local network.

##### Routing Tables with ip route

The **ip** command is versatile. One important version of this command, **ip route**, displays routing tables. It’s functionally equivalent to the deprecated **route** command. When run with the **-r** switch (**ip -r route**), this command looks to /etc/hosts files and DNS servers to display hostnames rather than numeric IP addresses.

The routing table for the local system normally includes a reference to the default gateway address. For example, look at the following output to the **ip route** command:

![Images](f0100-01.jpg)

The deprecated **netstat -nr** command should display the same table. For this routing table, the gateway IP address is 172.16.0.2\. Any network packets with a destination other than the 172.16.0.0/24 network range are sent through the gateway address (in other words, the layer 2 address for this gateway is looked up and put in the frame as the destination MAC address). The system at the gateway address, usually a router, forwards that packet to the next router according to its routing table until it gets to a router that is directly connected to the destination.

##### Display Network Connections with ss

The **ss** command replaces the deprecated **netstat** tool to display network connections. With the right combination of command switches, it can show listening and nonlistening TCP and UDP sockets. One command we like to use is

`# ss -tuna4`

which shows all (**-a**) network sockets using IPv4 (**-4**) and both the TCP (**-t**) and UDP (**-u**) protocols in numeric (**-n**) format. If the **-p** switch is specified, **ss** also shows the process ID (PID) of the process using each socket. [Figure 3-1](#ch03.xhtml_ch3fig1) illustrates a sample output.

FIGURE 3-1 Output from the ss -tuna4 command

![Images](F03-01.jpg)

At the end of the output, note the peer address of 192.168.122.1:47068\. The 47068 port number is just the source port on the remote server. The corresponding local address of 192.168.122.100:22 specifies a port number of 22 (the local SSH service) for a connection from 192.168.122.1\. You may also see a second entry with the same port number, which identifies the associated SSH daemon listening for connections. Other lines in this output identify other listening services.

### CERTIFICATION OBJECTIVE 3.02

### Network Configuration and Troubleshooting

Now that you’ve reviewed the basics of IP addressing and associated commands, it’s time to look at the configuration files. These configuration files determine whether networking is started during the boot process. If networking is activated, these files also determine whether addresses and routes are configured statically as documented or dynamically with a DHCP client.

Basic network configuration only confirms that systems can communicate through their IP addresses. But that is not enough. Whether you’re pointing to systems such as server1.example.com or URLs such as [www.mheducation.com](http://www.mheducation.com), network configuration is not enough if hostname resolution is not working.

![Images](job.jpg)

**Some of the most common causes of network problems are physical in nature. This section assumes you’ve checked all network connections. On a VM, that means making sure the virtual network interface wasn’t accidentally deleted or deactivated on the VM or on the physical host.**

#### Network Configuration Services

If there’s trouble with a network configuration, one thing to check is the current status of the network. To do so, run the following command:

`# systemctl status NetworkManager`

RHEL 9 uses a service known as Network Manager to monitor and manage network settings. Using the **nmcli** command-line tool, you can interact with Network Manager and display the current status of network devices:

`# nmcli dev status`

The command should list configured and active devices. If a key device such as eth0 is not listed as connected, your network connection is probably down or the device is not configured. Key configuration files are located in the /etc/NetworkManager/system-connections directory.

Sometimes mistakes happen. If you’ve deactivated an adapter or just lost a wireless connection, try something simple: restart networking. The following command restarts networking with current configuration files:

`# systemctl restart NetworkManager`

If a simple restart of networking services doesn’t work, then it’s time to get into the files. The /etc/NetworkManager/system-connections directory is where Red Hat Enterprise Linux stores and retrieves networking information. With available Red Hat configuration tools, you don’t have to touch these files, but it’s good to know they’re there. Each installed network adapter, such as ens3, gets its own *name*.nmconnection configuration file, where *name* is the name of the device or the name of the connection. For example, eth0 is given file eth0.nmconnection. This file includes the IP address information required to identify this adapter on a network.

What you see in the *.nmconnection files depends on how an Ethernet network adapter was configured. For example, look at the situation where networking was set up only for the purposes of installation. If you did not configure networking when setting the hostname during the GUI installation process, the network interface would have retrieved its IP settings from a DHCP server.

Generally, the network options configured through a DHCP server include the IP address, the network mask, the gateway address for access to external networks, and the IP address of any DNS servers for that network.

When a network interface is configured to get its IP settings from a DHCP server, the corresponding nmconnection file would contain at least the following directives:

![Images](f0102-02.jpg)

Network Manager includes **nmcli** to control the status of the service and apply network configuration changes. Rather than modifying the configuration via **nmcli**, you can change a device configuration file directly. For that purpose, the configuration file shown in [Figure 3-2](#ch03.xhtml_ch3fig2) provides a guide.

FIGURE 3-2 A manual configuration of eth0

![Images](F03-02.jpg)

Most of these directives are straightforward. They define a configuration for an Ethernet network interface with name eth0, using a defined IP address, a netmask, a default gateway, and a DNS server.

After saving the file, you still have to notify Network Manager of the changes. This is achieved by running the following commands (**con** is short for **connection**):

![Images](f0102-03.jpg)

Shortly, you’ll see how to use Network Manager’s command-line tool to modify the configuration of a network device.

#### Network Configuration Tools

Red Hat includes several tools that can be used to configure network devices in RHEL 9\. The first is the Network Manager command-line tool, **nmcli**, introduced in the prior section. If you prefer a text-based graphical tool, you can start **nmtui** from a virtual terminal. As an alternative, the Network Manager Connection Editor is a GTK+ 3 application that you can start from a GNOME terminal with the **nm-connection-editor** command.

All the tools mentioned interact with the Network Manager system service.

##### The nmcli Configuration Tool

Network Manager can store different profiles, also known as *connections*, for the same network interface. This allows you to switch from one profile to another. For example, you may have a home profile and a work profile for a laptop Ethernet adapter and switch between the two depending on the network to which you are attached.

You can display all the configured connections in Network Manager by running the following command:

![Images](f0103-02.jpg)

To show how **nmcli** can be used to set up a different connection profile, the following command creates a new connection for eth0:

![Images](f0103-03.jpg)

Then, a static IP address and default gateway can be configured, as shown here:

![Images](f0103-04.jpg)

You can run **nmcli con show *connection-id*** to display the current settings for a connection. You can also modify additional properties from **nmcli**. For example, to add a DNS server to the eth-work connection, run

![Images](f0104-01.jpg)

Finally, to switch to the new connection profile, run

![Images](f0104-02.jpg)

You can prevent a connection from starting automatically at boot with the following command:

![Images](f0104-03.jpg)

##### The nmtui Configuration Tool

As suggested by the name, this tool provides a text-based user interface and can be started from a command-line terminal. Just run the **nmtui** command. With a console tool, you’d need to press TAB to switch between options and press the SPACEBAR or the ENTER key to select the highlighted option.

Press the DOWN ARROW key until Quit is highlighted, and then press ENTER. For now, make a backup of the file from the /etc/NetworkManager/system-connections directory. Based on the **diff** command, [Figure 3-3](#ch03.xhtml_ch3fig3) compares the contents of an eth0 interface that uses the DHCP protocol, as configured during the installation process, with an interface that uses static IP addressing, configured with the **nmtui** tool.

FIGURE 3-3 The differences between static and dynamic network configuration

![Images](F03-03.jpg)

The directives shown in [Figure 3-3](#ch03.xhtml_ch3fig3) are described in [Table 3-5](#ch03.xhtml_ch3tab5), along with some other configuration directives that you may find in the system-connections directory.

TABLE 3-5 Network Configuration Directives in the /etc/NetworkManager/system-connections Directory

![Images](f0105-01.jpg)

EXERCISE 3-1

**Configure IPv4 Settings on a Network Interface**

In this exercise, you’ll configure the first Ethernet network interface with the Network Manager text-based user interface tool. All you need is a command-line interface. Take the following steps:

1.   Back up a copy of the current configuration file for the Ethernet interface. This would be the *.nmconnection file in the /etc/NetworkManager/system-connections directory (the filename may vary, depending on the interface name). (Hint: use the **cp** command, not the **mv** command.)

2.   Run the **nmtui** command.

3.   In the menu that appears, Edit a Connection should be highlighted. If necessary, press the ARROW or TAB key until it is. Then press ENTER.

4.   In the screen that appears, make sure the first Ethernet network interface is highlighted and press ENTER.

5.   In the Edit Connection window shown here, the Automatic option may be selected under IPv4 Configuration. If so, highlight it and press ENTER; then select Manual.

![Images](I03-01.jpg)

6.   If the IPv4 settings are not shown, highlight the Show option at the right of IPv4 Configuration and press enter. This expands the current IPv4 settings.

7.   Enter the IP address information for the system. The settings shown in the window are based on the settings described in [Chapter 1](#ch01.xhtml) for the server1.example.com system. When complete, highlight OK and press ENTER.

8.   You’re taken back to the device screen. Make sure Quit is highlighted and press ENTER.

9.   Check the result with the **ip addr show** and **ip route** commands. The configuration of the network interface and the associated routing table should reflect the new settings.

10.   To restore the original configuration, restore the *.nmconnection file to the /etc/NetworkManager/system-connections directory and run **nmcli conn reload**.

##### Network Manager Connection Editor

Now you’ll work with the default graphical network management tool for RHEL 9, the Network Manager Connection Editor tool. When connecting to different networks, Network Manager is designed to make that switching between, say, a wireless and an Ethernet connection as seamless as possible. But that’s something more applicable to portable systems as opposed to servers. For the scope of the RHCSA exam, all you need to know is how to configure a network interface with that tool.

The Network Manager Connection Editor is not really new, because it has been in use in Fedora for several years. It only runs in the GUI. To start it, run the **nm-connection-editor** command. This opens the Network Connections tool shown in [Figure 3-4](#ch03.xhtml_ch3fig4).

FIGURE 3-4 Network Manager Connection Editor

![Images](F03-04.jpg)

As you can see from the figure, the tool lists the connection profile for the first Ethernet network interface. It also supports the configuration of other types of networks, including wireless, mobile broadband cards (such as those used to connect to 4G and 5G networks), and Digital Subscriber Line (DSL) connections. On a regular server, the focus is on reliable connections, and that is still based on a standard wired Ethernet device.

Highlight the connection profile of the first Ethernet device (eth0) and click the gear icon; then click the IPv4 Settings tab, as shown in [Figure 3-5](#ch03.xhtml_ch3fig5). Unless previously configured, the default Method setting assumes that the network interface will receive its configuration settings automatically from a DHCP server.

FIGURE 3-5 Editing an Ethernet connection in the Network Manager Connection Editor

![Images](F03-05.jpg)

Click the Method drop-down text box. Although Connection Editor supports the configuration of a network interface in several different ways, the only one of interest in this case is Manual. Select that option, and the Additional Static Addresses section of the window should no longer be blanked out. Now add the IP address information for the system. Based on the server1.example.com system described in [Chapter 1](#ch01.xhtml), here are the appropriate options:

![Images](square.jpg)   **Address** 172.16.0.100

![Images](square.jpg)   **Netmask** 255.255.255.0 (24 in CIDR notation is an acceptable equivalent in this field)

![Images](square.jpg)   **Gateway** 172.16.0.2

![Images](square.jpg)   **Additional DNS Servers** 172.16.0.2

![Images](square.jpg)   **Additional Search Domains** [example.com](http://example.com)

![Images](square.jpg)   **DHCP Client ID**

![Images](square.jpg)   **Require IPv4 Addressing for This Connection to Complete** Deselected

If properly entered, the configuration associated with the first Ethernet interface is titled with the connection name listed in [Figure 3-5](#ch03.xhtml_ch3fig5). For that configuration, the settings are saved in the eth0.nmconnection file in the /etc/NetworkManager/system-connections directory.

#### Configure Name Resolution

The final piece in network configuration is typically name resolution. In other words, does the local system have the information required to translate domain names such as [mheducation.com](http://mheducation.com) to IP addresses such as 52.7.41.60?

Name resolution was easy when Unix was first being developed. When the predecessor to the Internet was first put into use, the worldwide computer network had four hosts, one computer at each of four different universities. It was easy to set up a static file with a list of each of their names and corresponding addresses. That file has evolved into what is known in Linux as /etc/hosts.

But now the Internet is more complex. Although you could try to set up a database of every domain name and IP address on the Internet in the /etc/hosts file, that would take almost forever and would not be a scalable solution. That’s why most users set up connections to DNS servers. On RHEL 9, that’s still documented in the /etc/resolv.conf configuration file.

On smaller networks, some administrators set up the /etc/hosts file as a database for the name of each system and IP address on the local network. If desired, administrators could even set up a few IP addresses of domains on the Internet, although this setup would break if any of those Internet domains made DNS changes on their own.

But if you’ve configured a connection to a DNS server and systems in /etc/hosts, what’s searched first? That’s the purpose of the /etc/nsswitch.conf configuration file, which specifies the search order for various name-service databases, including hostnames.

#### Hostname Configuration Files

RHEL 9 includes at least four hostname configuration files of interest: /etc/hostname, /etc/hosts, /etc/resolv.conf, and /etc/nsswitch.conf. These four files, taken together, contain the local hostname, the local database of hostnames and IP addresses, the IP address of one or more DNS servers, and the order in which these databases are searched.

##### /etc/nsswitch.conf

The /etc/nsswitch.conf file specifies database search priorities for everything from authentication to name services. As the name server switch file, it includes the following entry, which determines what database is searched first:

`hosts: files dns myhostname`

When a system gets a request to search for a hostname such as tester1.[example.com](http://example.com), the preceding directive means the /etc/hosts file is searched first. If that name is not found in /etc/hosts, the next step is to search available configured DNS servers, normally using those configured in the /etc/resolv.conf file. If the name is still not found, the system looks at its hostname.

The resolver library also uses information in the /etc/host.conf file. The entry in this file is simply

`multi on`

which tells the system to return all IP addresses in /etc/hosts that are mapped to the same hostname, instead of returning only the first entry.

##### /etc/hosts

The /etc/hosts file is a static database of hostnames/FQDNs and IP addresses. It’s suitable for small, relatively static networks. However, using it for networks where there are frequent changes can be a pain. Every time a system is added or removed, you’ll have to change this file—not only on the local system but also on every other system on that network.

The /etc/hosts file is well suited to the local virtual machines created in [Chapter 1](#ch01.xhtml). A simple version of the file might include the following entries:

![Images](f0110-02.jpg)

In some cases, you may want to set up multiple entries for an IP address. For example, the following entries could be added to specify the IP addresses for web and FTP servers:

![Images](f0110-03.jpg)

##### /etc/resolv.conf

The standard file for documenting the location of DNS servers is still /etc/resolv.conf. Typically, it’ll have one or two entries, similar to the following:

![Images](f0110-04.jpg)

The **search** directive appends the [example.com](http://example.com) domain name to searches for simple hostnames. The **nameserver** directive specifies the IP address of the configured DNS server. If in doubt about whether the DNS server is operational, run one of the following commands:

![Images](f0110-05.jpg)

In the preceding commands, substitute the IP address associated with the DNS server that you want to test, which could be one of the servers listed in the **nameserver** directive in your /etc/resolv.conf file. You can specify up to three **nameserver** directives in this file.

![Images](job.jpg)

**It may not be wise to edit the /etc/resolv.conf file directly. If you have configured DNS servers with another tool such as** nmcli, **Network Manager will overwrite any changes you make when directly editing that file unless you override this behavior with** ignore-auto-dns **in the connection file.**

##### /etc/hostname

During the boot process, the network service looks to the /etc/hostname file to define the value of the local hostname. The hostname should be set as an FQDN such as tester1.example.com. As suggested earlier, it’s a simple file, where the hostname is documented with a directive such as the following:

`tester1.example.com`

Of course, you can modify the value of the hostname with the **hostname *newname*** command. However, this change is only temporary and is not reflected in the /etc/hostname file. To make the change persistent, use the **hostnamectl set-hostname *newname*** command.

### CERTIFICATION OBJECTIVE 3.03

### An Introduction to IPv6

One of the special challenges of the RHCSA exam is IPv6 networking. While most current networks are configured with IPv4 addresses, several regions have run out of public IPv4 addresses.

Internet Protocol Version 6 (IPv6) was introduced in the late 1990s as a replacement for IPv4\. It turns out that the 4 billion (2^(32)) IPv4 addresses are not enough. IPv6 supports many more addresses, potentially up to 2^(128), or 3.4 × 10^(38) (340 undecillion) addresses.

#### Basic IPv6 Addressing

The first section of this chapter introduced the “dot-decimal” notation for IPv4 addresses, where each decimal octet represents 8 bits of the 32-bit address (for example, 192.168.56.100). IPv6 addresses are made of 128 bits and are set up in hexadecimal notation, also known as base 16\. In other words, an IPv6 address may include the following “digits”:

`0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, b, c, d, e, f`

An IPv6 address is normally organized in eight groups of four hexadecimal numbers each, called “nibbles” since each character represents half a byte, in the following format:

`2001:0db8:3dab:0001:0000:0000:0000:0072`

You can simplify IPv6 addressing further:

![Images](square.jpg)   Remove any leading zeros in a nibble. For example, you can write 0db8 as db8, 0072 as 72, 0000 as 0, and so on.

![Images](square.jpg)   Replace any sequence of 0000 nibbles with a pair of colons (::). As an example, you can abbreviate 0000:0000:0000 with a pair of colons. However, to avoid ambiguity, you can apply this rule only once in an IPv6 address.

Hence, you can rewrite the previous address in a much more compact form:

`2001:db8:3dab:1::72`

Similar to IPv4, IPv6 addresses are made of two parts: a host and a network address. The host portion of an IPv6 address is known as the *interface identifier*. In IPv6, subnet masks are typically specified in prefix notation (such as /48).

As an example, assume that the IPv6 address 2001:db8:3dab:1::72 has a network prefix of /64\. In other words, the network part of that IPv6 address includes the first 64 bits of that address. In this case, that network prefix is 2001:db8:3dab:1\. The interface identifier includes the last 64 bits, shown as the hexadecimal number 72.

IPv6 addresses are classified in several categories. First, there are three address formats:

![Images](square.jpg)   **Unicast** A unicast address is associated with a single network adapter.

![Images](square.jpg)   **Anycast** An anycast address can be assigned to multiple hosts simultaneously. It can be used for load balancing and redundancy. Anycast addresses are organized in the same way as unicast addresses.

![Images](square.jpg)   **Multicast** A multicast address is used to send a message to multiple destinations simultaneously.

With that diversity of address formats, IPv4-style broadcast addresses aren’t needed. If you want to send a message to multiple systems, use IPv6 multicast addresses.

IPv6 addresses are also organized in several different ranges, as described in [Table 3-6](#ch03.xhtml_ch3tab6). The default route in IPv4 (0.0.0.0/0) is shown as ::/0 in IPv6.

TABLE 3-6 IPv6 Address Types

![Images](f0113-01.jpg)

The link-local address range requires explanation. Every interface in an IPv6 network is automatically configured with a link-local address. These addresses are not routable; as such, communication is limited to the local network segment. Link-local addresses are needed for various IPv6 operations.

Even if you haven’t configured IPv6 in your servers, each network interface is automatically assigned a link-local address, as shown in the following output:

![Images](f0113-02.jpg)

To identify a link-local address, look for an address that starts with fe80\. Note the “scope link” entry. As you can see, interface eth0 has the following IPv6 link-local address: fe80::20c:29ff:fe0c:30d4/64.

#### Troubleshooting Tools

Most of the network tools introduced in this chapter work seamlessly with both IPv4 and IPv6 addresses. There are two notable exceptions: the **ping** and **tracepath** commands. For IPv6 networking, you would use the **ping6** and **tracepath6** commands.

The **ping6** command works in a similar way to **ping**. Even before you configure an IPv6 address, you can run the **ping6** command on the Linux system hosting your server1.example.com virtual machine:

![Images](f0113-03.jpg)

Since link-local addresses are not routable, you must specify the outbound interface (**-I**) in the **ping6** command when you ping a remote link-local address.

#### Configure IPv6 Addresses

As with IPv4 networking, you can configure an IPv6 address with the Network Manager command-line tool **nmcli**, the text-based graphical tool **nmtui**, or the Network Manager Connection Editor.

Start the Network Manager Connection Editor from the GUI with the **nm-connection-editor** command. Select the connection profile of the first Ethernet device (eth0 in our system), click the gear icon, then click the IPv6 Settings tab, shown in [Figure 3-6](#ch03.xhtml_ch3fig6).

FIGURE 3-6 Editing an IPv6 address in the Network Manager Connection Editor

![Images](F03-06.jpg)

Click the Method drop-down text box and select Manual. You can now add IP address information for the system. For example, on server1.example.com we added the following settings:

![Images](square.jpg)   **Address** 2001:db8:3dab::2

![Images](square.jpg)   **Prefix** 64

![Images](square.jpg)   **Gateway** 2001:db8:3dab::1

Similarly, we have associated the IPv6 address 2001:db8:3dab:1 with the vmnet8 interface on our physical system. You can verify the configuration with the following command:

![Images](f0115-01.jpg)

The configuration is saved in the eth0.nmconnection file in the /etc/NetworkManager/system-connections directory. Open that file. You will notice that the Network Manager Connection Editor added the following configuration lines:

![Images](f0115-02.jpg)

The **addr-gen-mode** directive is used to auto-generate an IPv6 address derived from the hardware address of the network interface and requires **method** to be set to **auto** to be effective. The next variables, **address1** and **gateway**, set the IP addresses of the interface and the default gateway, respectively.

### CERTIFICATION OBJECTIVE 3.04

### Administration with Secure Shell and Secure Copy

Red Hat Enterprise Linux installs the Secure Shell (SSH) packages by default. The RHCSA requirement with respect to SSH is simple: you need to know how to use it to access remote systems. In addition, you need to know how to securely transfer files between systems. Therefore, this section examines how to use the **ssh** and **scp** commands to access remote systems and transfer files.

As suggested earlier, the stage is already set by the default installation of SSH on standard installations of RHEL 9\. Although firewalls are enabled by default, the standard RHEL 9 firewall leaves TCP port 22 open for SSH access. Related configuration files are stored in the /etc/ssh directory.

The Secure Shell daemon is secure because it encrypts messages. In other words, malicious users who are listening to traffic on a network can’t read the data sent between SSH clients and servers. And that’s important on a public network such as the Internet. RHEL incorporates SSH version 2, which supports multiple key-exchange methods and is incompatible with the older SSH version 1\. Client commands such as **ssh**, **scp**, and **sftp** are covered in this section, while key-based authentication for SSH is covered in [Chapter 8](#ch08.xhtml).

#### Command-Line Access

To access a remote system with **ssh**, you need a username and password on that remote system. By default, direct **ssh**-based access to the root account is not enabled. For example, the following command opens a shell on the noted server1 system and authenticates with the username michael:

![Images](f0116-01.jpg)

![Images](job.jpg)

**If you get an error such as “Name or service not known” when you attempt to access a remote host via** ssh, **that indicates that the system cannot resolve the hostname to an IP address. You will configure name resolution in one of this chapter’s labs. In the meantime, to log in to server1.example.com via** ssh, **use the IP address that you configured in [Chapter 1](#ch01.xhtml).**

The following command works in the same way:

![Images](f0116-02.jpg)

Without the username, the **ssh** command assumes that you’re logging in remotely as the username on the local system. For example, if you were to run the command

![Images](f0116-03.jpg)

from the user michael account, the **ssh** command would assume that you’re trying to log in to the server1.example.com system as user michael.

The first time the **ssh** command is run between systems, it presents something similar to the following message:

![Images](f0116-04.jpg)

Once connected via **ssh**, you can do anything on the remote system that’s supported by your user privileges on that machine. For example, you can even shut down the remote system gracefully with the **poweroff** command if you have privileges to do so. After executing that command, you’ll typically have a couple of seconds to exit the remote system with the **exit** command.

#### More SSH Command-Line Tools

If you prefer to access the remote system with an FTP-like client, the **sftp** command is for you. Although the **-l** switch doesn’t have the same meaning of the **ssh** command, it still can be used to log in to the account of any user on the remote system. Whereas regular FTP communication proceeds in clear text, communication with the **sftp** command can be used to transfer files in encrypted format.

Alternatively, if you just want to transfer files over an encrypted connection, the **scp** command can help. For example, we created some of the screenshots for this book on the test VMs configured in [Chapter 1](#ch01.xhtml). To transmit one of those screenshots to one of our systems, we used a command similar to the following, which copied the F02-07.tif file from the local directory to the remote system with the noted hostname, in the /home/michael/RHbook/Chapter2 directory:

![Images](f0117-01.jpg)

Unless key-based authentication has been configured (as discussed in [Chapter 8](#ch08.xhtml)), the command prompts for the password of the user michael on the system named server1\. Once the password is confirmed, the **scp** command transfers the F02-07.tif file in encrypted format to the noted directory on the remote system named server1.

#### Graphical Secure Shell Access

You can use the **ssh** command to forward the output of a GUI application over a network. As strange as it sounds, it works if the local system runs an X server while you call remote GUI client applications from remote systems.

By default, both the SSH server and client configuration files are set up to support X11 communication over a network. All you need to do is connect to the remote system with the **-X** switch (or **-Y** to use trusted X11 forwarding, which bypasses some security extension controls). For example, you could use the command sequence shown in [Figure 3-7](#ch03.xhtml_ch3fig7) to monitor the remote system.

FIGURE 3-7 Remote GUI access via SSH

![Images](F03-07.jpg)

![Images](f0118-02.jpg)

![Images](f0119-01.jpg)

#### CERTIFICATION SUMMARY

Linux is inherently a network operating system. Network devices such as eth0 can be configured with both IPv4 and IPv6 addresses. Network review and configuration commands include **ip link show** and **ip addr show**. Additional related commands include **ss**, **ping**, and **tracepath**. Individual devices are configured in the /etc/NetworkManager/system-connections directory. Network devices can also be configured with the **nmcli** and **nmtui** commands at the console and the Network Manager Connection Editor.

Configuring hostname and name resolution is an essential skill. If you have not set a hostname at installation, run the **hostnamectl** command. While the RHCSA objectives do not cover the configuration of a DNS server, you must know how to configure a DNS client. The **nmcli** and **nmtui** commands and the Network Manager Connection Editor that you used to configure network interfaces also enable you to specify the IP address of a DNS server.

Once the network is configured, you do not need to access a system from its console, but you can access it remotely. The SSH service can help set up remote encrypted sessions between Linux systems. The RHCSA exam requires that you know how to use an SSH client and to securely transfer files between systems. You can use the **ssh** command to log in to remote systems; use the **ssh -Y** command to access trusted remote GUI applications; and use the **scp** command to copy files remotely over an encrypted connection.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 3](#ch03.xhtml).

##### A Networking Primer

![Images](squ1.jpg)   IPv4 addresses have 32 bits. There are five classes of IPv4 addresses and three different sets of private IPv4 addresses suitable for setting up TCP/IP on a private LAN.

![Images](squ1.jpg)   The subnet mask (also known as netmask or prefix) is used to find the network and host parts of an IP address.

![Images](squ1.jpg)   Tools such as **ping**, **traceroute**, **tracepath**, **ip**, and **ss** can help you diagnose problems on the LAN.

![Images](squ1.jpg)   Name resolution configuration files such as /etc/resolv.conf determine how a system finds the right IP address; the /etc/resolv.conf file may be configured from a DHCP server by Network Manager.

##### Network Configuration and Troubleshooting

![Images](squ1.jpg)   Individual network devices are configured in the /etc/NetworkManager/system-connections directory.

![Images](squ1.jpg)   Network configuration tools include the console-based **nmcli** and **nmtui** commands and the Network Manager Connection Editor.

![Images](squ1.jpg)   Name resolution configuration files include /etc/nsswitch.conf, /etc/hosts, and /etc/resolv.conf.

##### An Introduction to IPv6

![Images](squ1.jpg)   IPv6 addresses have 128 bits organized in groups of four nibbles (16 bits).

![Images](squ1.jpg)   The three different types of IPv6 addresses are unicast, anycast, and multicast.

![Images](squ1.jpg)   IPv6 addresses can be limited to local network segments (link-local) or routable.

##### Administration with Secure Shell and Secure Copy

![Images](squ1.jpg)   SSH is installed by default on RHEL 9\. It’s even accessible through default firewalls.

![Images](squ1.jpg)   The **ssh** command can be used to access remote systems securely. It can even enable access to remote GUI utilities.

![Images](squ1.jpg)   Related commands include **sftp** and **scp**.

#### Q SELF TEST

The following questions will help you measure your understanding of the material presented in this chapter. Because there are no multiple-choice questions on the Red Hat exams, there are no multiple-choice questions in this book. These questions exclusively test your understanding of the chapter. Getting results, not memorizing trivia, is what counts on the Red Hat exams.

##### A Networking Primer

**[1.](#ch03.xhtml_ch3ques1)**   In IPv4 addressing, with a network address of 192.168.100.0 and a broadcast address of 192.168.100.255, what is the range of assignable IP addresses?

**[2.](#ch03.xhtml_ch3ques2)**   Given the addresses described in Question 1, what **ip** command assigns the IPv4 address 192.168.100.100 to network device eth0?

**[3.](#ch03.xhtml_ch3ques3)**   What tools are available in RHEL 9 to configure the settings on a network device so that they persist after a system reboot?

**[4.](#ch03.xhtml_ch3ques4)**   What **nmcli** command creates a connection profile named “home” for the network interface eth0, with IP address 192.168.100.20/24, default gateway 192.168.100.254, and DNS server 192.168.100.254?

**[5.](#ch03.xhtml_ch3ques5)**   After configuring the connection profile as described in Question 4, what command brings up the new connection profile?

##### Network Configuration and Troubleshooting

**[6.](#ch03.xhtml_ch3ques6)**   What is the full path to the configuration file with the hostname of the local system?

**[7.](#ch03.xhtml_ch3ques7)**   What is the default full path to the configuration file associated with the connection profile of the eth0 Ethernet adapter for the local system?

##### An Introduction to IPv6

**[8.](#ch03.xhtml_ch3ques8)**   What is the shortest representation of the 2001:0db8:00aa:0000:04ba:0000:0000:00cd IPv6 address?

**[9.](#ch03.xhtml_ch3ques9)**   What command can you use to ping an IPv6 address?

##### Administration with Secure Shell and Secure Copy

**[10.](#ch03.xhtml_ch3ques10)**   What **ssh** command switch enables access to remote GUI utilities via X11 forwarding?

**[11.](#ch03.xhtml_ch3ques11)**   What command initiates a secure copy of the file /etc/hosts from the system server1.example.com to the /tmp directory on the local host?

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for each lab follow the Self Test answers.

#### A SELF TEST ANSWERS

##### A Networking Primer

**[1.](#ch03.xhtml_r_ch3ques1)**   The range of assignable IP addresses in the noted IPv4 network is 192.168.100.1 through 192.168.100.254.

**[2.](#ch03.xhtml_r_ch3ques2)**   Given the addresses described in Question 1, the **ip** command that assigns IPv4 address 192.168.100.100 to network device eth0 is **ip addr add 192.168.100.100/24 dev eth0**. Note that the settings configured with this command do not persist after a system reboot.

**[3.](#ch03.xhtml_r_ch3ques3)**   You can configure the settings on a network device so that they persist after a reboot using either **nmcli**, **nmtui**, or the Network Manager Connection Editor.

**[4.](#ch03.xhtml_r_ch3ques4)**   The following **nmcli** command creates a connection profile named “home” for the network interface eth0, with IP address 192.168.100.20/24, default gateway 192.168.100.254, and DNS server 192.168.100.254:

![Images](f0122-01.jpg)

**[5.](#ch03.xhtml_r_ch3ques5)**   The following command brings up the network profile:

![Images](f0122-02.jpg)

##### Network Configuration and Troubleshooting

**[6.](#ch03.xhtml_r_ch3ques6)**   The full path to the configuration file with the hostname of the local system is /etc/hostname.

**[7.](#ch03.xhtml_r_ch3ques7)**   The default full path to the configuration file associated with the connection profile of the eth0 Ethernet adapter for the local system is /etc/NetworkManager/system-connections/eth0.nmconnection. If you use different connection profiles in Network Manager, you would find a file for each connection profile within the /etc/NetworkManager/system-connections directory.

##### An Introduction to IPv6

**[8.](#ch03.xhtml_r_ch3ques8)**   The shortest representation of the 2001:0db8:00aa:0000:04ba:0000:0000:00cd IPv6 address is 2001:db8:aa:0:4ba::cd.

**[9.](#ch03.xhtml_r_ch3ques9)**   You can use the **ping6** command to ping an IPv6 address. If this is a link-local address, you need to specify the outbound interface with the **-I** switch.

##### Administration with Secure Shell and Secure Copy

**[10.](#ch03.xhtml_r_ch3ques10)**   The **ssh** command switch that enables access to trusted remote GUI utilities via X11 forwarding is **-Y**. The **-X** switch is also an acceptable answer.

**[11.](#ch03.xhtml_r_ch3ques11)**   The required command to securely copy /etc/hosts from server1 to /tmp on the local host is **scp server1.example.com:/etc/hosts /tmp/**.

#### LAB ANSWERS

##### Lab 1

This lab sets up an invalid IP address configuration for all connections present on the system.

**1.**   Test connections to local and remote systems, such as the hostname or FQDN for the local system and the IP address of the nameserver in /etc/resolv.conf:

![Images](f0123-01.jpg)

**2.**   Check the link status and IP settings:

![Images](f0123-02.jpg)

**3.**   Review applicable network configuration files. Can you identify the problem yet?

![Images](f0123-03.jpg)

**4.**   If you can’t identify the problem, open the Network Manager Connection Editor and review the information in the IPv4 settings of the connection profile:

![Images](f0123-04.jpg)

**5.**   The network configuration was altered by setting the wrong IP address and removing the default gateway settings. Open the Network Manager Connection Editor and manually restore the original configuration.

**6.**   If you still have problems, restore the configuration from the backup files:

![Images](f0123-05.jpg)

##### Lab 2

This lab deactivates all active network connection profiles on the system and reconfigures them to not connect after a reboot.

**1.**   Test connections to local and remote systems, such as the hostname or FQDN for the local system and the IP address of the nameserver in /etc/resolv.conf:

![Images](f0124-01.jpg)

**2.**   Check the link status and IP settings:

![Images](f0124-02.jpg)

You should see that the network interface has no IP settings.

**3.**   Open the Network Manager Connection Editor and check the connection IP settings:

![Images](f0124-03.jpg)

**4.**   List the active connections. The output of the commands should be blank:

![Images](f0124-04.jpg)

**5.**   Using Network Manager Connection Editor, edit the connection profile and ensure that in the General tab the option “Connect automatically with priority” is selected. This should restore network connectivity.

**6.**   If you still have problems, restore the configuration from the backup files:

![Images](f0124-05.jpg)

##### Lab 3

This lab removes the DNS client configuration. You should find that IP connectivity works fine but name resolution fails.

**1.**   Try pinging [www.google.com](http://www.google.com). The command should fail.

![Images](f0124-06.jpg)

**2.**   This indicates an issue with network resolution. If you check the contents of /etc/resolv.conf, you will find that the file is empty:

![Images](f0124-07.jpg)

**3.**   Open the Network Manager Connection Editor and manually restore the original configuration by editing the DNS server and search domains settings in the IPv4 Settings tab.

**4.**   If you still have problems, restore the configuration from the backup files:

![Images](f0124-08.jpg)

##### Lab 4

In this lab, you set up the /etc/hosts file on each of the systems described in [Chapter 1](#ch01.xhtml). Except for the local system settings added by Network Manager, the data in /etc/hosts on the two systems may be identical. Specifically, that file should include the following entries:

![Images](f0125-01.jpg)

Your IP addresses may differ, depending on the virtual network set up by your hypervisor, as discussed in [Chapter 1](#ch01.xhtml).

Duplication with data inserted by Network Manager is not a problem, as long as the data is consistent. In fact, it’s possible to set up multiple names for an IP address; for example, if you set up a web server on the 172.16.0.50 system, you could add the following entry to /etc/hosts:

![Images](f0125-02.jpg)

Once you have completed the configuration, try pinging tester1.example.com from server1.example.com (and vice versa). Name resolution in /etc/hosts should work:

![Images](f0125-03.jpg)

##### Labs 5 and 6

These labs are guided exercises to let you become familiar with **nmtui** and the Network Manager Connection Editor. You should be able to follow all the steps and make configuration changes.

**1.**   Once you have modified the IP configuration, test connectivity between the two virtual machines using the **ping** command (your IP address may differ):

![Images](f0125-04.jpg)

**2.**   As a bonus task, try configuring IPv6 addresses on your test systems. For instance, configure the IPv6 address fd00::1/64 on server1.example.com and fd00::2/64 on tester1.example.com, and ensure that you can ping each other’s IP address with **ping6** from each host:

![Images](f0125-05.jpg)

**3.**   If something goes wrong, you can restore the original configuration from the backup files:

![Images](f0125-06.jpg)

## Chapter 4

## Software Management

CERTIFICATION OBJECTIVES

[4.01     The RPM Package Manager](#ch04.xhtml_ch4obj01)

[4.02     More RPM Commands](#ch04.xhtml_ch4obj02)

[4.03     Dependencies and the dnf Command](#ch04.xhtml_ch4obj03)

[4.04     Module Streams (*)](#ch04.xhtml_ch4obj04)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

After installation is complete, systems are secured, filesystems are configured, and other initial setup tasks are completed, you still have work to do. Almost certainly before your system is in the state you desire, you will be required to install or remove packages. To make sure the right updates are installed, you need to know how to get a system working with Red Hat Subscription Management (RHSM) or the repository associated with a rebuild distribution.

To accomplish these tasks, you need to understand how to use the **rpm** and **dnf** commands in detail. Although these are “just” two commands, they are rich in detail. Entire books have been dedicated to the **rpm** command, such as the *Red Hat RPM Guide* by Eric Foster-Johnson. For many, that degree of in-depth knowledge of the **rpm** command is no longer necessary, given the capabilities of the **dnf** command and the additional package management tools provided in RHEL 9.

INSIDE THE EXAM

**Administrative Skills**

As the management of RPM packages is a fundamental skill for Red Hat administrators, you should expect to use the *rpm*, *dnf*, and related commands on the RHCSA exam. The RHCSA objectives include one specific requirement addressed in this chapter:

![Images](square.jpg)   Install and update software packages from Red Hat Network, a remote repository, or from the local filesystem

The RHCSA exam for RHEL 8 also included the following objective:

![Images](square.jpg)   Work with package module streams

Although this objective is no longer included in the RHCSA exam objectives for RHEL 9, working with package module streams is still an important topic and might be restored in future revisions of the exam objectives. For this reason, we have included an optional section in this chapter to explain how module streams work. However, feel free to skip this section or return to it later, assuming that it still is not relevant for your exam preparation after this book is published.

Another closely related objective requires knowledge of the **tar** archiving utility, which is covered in [Chapter 9](#ch09.xhtml). Before Red Hat introduced RPM packages, tar archives were the standard method for distributing software.

Now let’s break down these skills a bit. First, we will introduce the **rpm** command. This is a very powerful software management tool, but lacks two important features that are provided by **dnf**: the management and installation of dependencies, which is software that is required by another software package; and the ability to work with repositories, which are collections of software packages accessible on a local filesystem or over the network. To work with **dnf**, you will configure access to Red Hat Subscription Management (RHSM) to download software packages. You can also use the same **dnf** commands to install and update packages from a remote third-party repository. Since RHEL 8, Red Hat also offers a new concept to support the distribution of different versions of the same application: this is the purpose of module streams.

### CERTIFICATION OBJECTIVE 4.01

### The RPM Package Manager

One of the major duties of a system administrator is software management. This includes installing new applications, updating services, and patching kernels. Without the right tools, it can be difficult to figure out what software is on a system, what is the latest update, and what applications depend on other software. Worse, you may install a new software package only to find it has overwritten a crucial file from a currently installed package.

![Images](job.jpg)

**As previously indicated, since RHEL 8, Red Hat introduced a new default package manager,** dnf**, also known as “Dandified YUM” or DNF. The** yum **command, which was the default package manager in RHEL 7, is simply a symbolic link to** dnf **in RHEL 9\. However, you do not need to know all the differences between** dnf **and** yum **to pass the RHCSA exam. For more information about the changes between** dnf **and** yum**, go to [https://dnf.readthedocs.io](https://dnf.readthedocs.io).**

RPM is a recursive acronym for RPM Package Manager (formerly Red Hat Package Manager). RPM was designed to alleviate the software management problems just discussed. With RPM, software is managed in discrete *packages*. An RPM package includes the software with instructions for adding, removing, and upgrading those files. When properly used, the RPM tool can back up key configuration files before proceeding with upgrades and removals. It can also help you identify the currently installed version of any RPM-based application.

RPMs and the **rpm** command are very focused on individual packages, which in many cases is far from ideal and is why **rpm** has been supplemented with the **dnf** command. With a connection to a repository such as that available from RHSM you’ll be able to use **dnf** to satisfy dependencies automatically.

#### What Is a Package?

In the generic sense, an RPM package is a container of files. It includes the group of files associated with a specific program or application, which normally contains binary files, installation scripts, and configuration and documentation files. It also includes instructions on how and where these files should be installed and uninstalled.

An RPM package name usually consists of the version, the release, and the architecture for which it was built. For example, the fictional penguin-3.4.5-26.el9.x86_64.rpm package is version 3.4.5, release 26.el9\. The x86_64 indicates that it is suitable for computers built to the AMD/Intel 64-bit architecture.

![Images](job.jpg)

**Many RPM packages include software compiled for a specific CPU type (for example, x86_64). You can identify the CPU type for the system with the** uname -i **or** uname -p **command. More information about your processor can be found in /proc/cpuinfo.**

#### What Is the RPM Database?

At the heart of this system is the RPM database, which is stored locally on each machine in the /var/lib/rpm directory. Among other things, this database tracks the version and location of every file in each RPM. The RPM database also maintains an MD5 checksum of each file. With the checksum, you can use the **rpm -V *package*** command to determine whether any file from that RPM package has changed. The RPM database makes it easy to add, remove, and upgrade individual packages because it’s configured to know which files to handle and where to put them.

RPM also manages conflicts between packages. For example, assume you have a package that installs a configuration file, and you want to update from an older to a newer version of the software. Call the original configuration file /etc/*someconfig*.conf. You’ve already installed package X. If you then try to install a more recent version of package X, the RPM package can be configured to preserve the original configuration file and install the new one as /etc/*someconfig*.conf.rpmnew.

Alternatively, the RPM creator can build the RPM in such a way that it will back up the original /etc/*someconfig*.conf file (with a filename such as /etc/*someconfig*.conf.rpmsave) before upgrading package X and then replace the configuration file with a new version. This may occur if the format of the old configuration file is incompatible with the new release of the software.

![Images](job.jpg)

**Although RPM upgrades are supposed to preserve or save existing configuration files, there are no guarantees, especially if the RPM is created by someone other than Red Hat. It’s best to back up all applicable configuration files before upgrading any associated RPM package.**

#### What Is a Repository?

RPM packages are frequently organized into repositories. Generally, such repositories include groups of packages with different functions. For example, the Red Hat Customer Portal gives access to the following RHEL 9 Server repositories:

![Images](square.jpg)   **BaseOS** The main repository, which includes the packages associated with the core RHEL 9 system, along with updates

![Images](square.jpg)   **AppStream** A large group of open-source applications, which includes databases and run-time languages

Each repository includes a database of packages in a repodata/ subdirectory. That database includes information on each package and allows installation requests to include all dependencies. If you have a subscription to RHSM, access to the Red Hat repositories is enabled in the product-id.conf and subscription-manager.conf files, in the /etc/dnf/plugins directory. Those files are discussed later in this chapter.

![Images](job.jpg)

**A dependency is a package that needs to be installed to make sure all the features of a target package work as designed.**

#### Install an RPM Package

There are three basic commands that *may* install an RPM. They won’t work if the RPM to install requires any dependencies. For example, if you haven’t installed the SELinux policy DBUS (policycoreutils-dbus) and development tool package (policycoreutils-devel) and try to install the SELinux configuration GUI (policycoreutils-gui), you’ll get the following message (version numbers may vary):

![Images](f0131-01.jpg)

One way to test this is to mount the RHEL 9 DVD with the **mount /dev/cdrom /media** command. Next, find the noted policycoreutils-gui package in the AppStream/Packages/ subdirectory. Alternatively, you could download that package directly from the Red Hat Customer Portal or a configured repository with the **dnf download policycoreutils-gui** command. This and other **dnf** commands are discussed later in this chapter. Be aware that some Linux GUI desktop environments automatically mount a CD/DVD media that is inserted into an associated drive. If so, you’ll see the mount directory in the output to the **mount** command.

When dependency messages are shown, **rpm** does not install the given package. Note the dependency messages: policycoreutils-gui requires the policycoreutils-dbus and policycoreutils-devel packages of the same version number.

![Images](job.jpg)

**Sure, you can use the** --nodeps **option to make** rpm **ignore dependencies, but that can lead to other problems, unless you install those dependencies as soon as possible. The best option is to use an appropriate** dnf **command, described later in this chapter. In this case, a** dnf install policycoreutils-gui **command would automatically install the other dependent RPM as well.**

If you’re not stopped by dependencies, the following three basic commands can install RPM packages:

![Images](f0132-01.jpg)

The **rpm -i** option installs the package, if it isn’t already installed. The **rpm -U** option upgrades any existing package or installs it if an earlier version isn’t already installed. The **rpm -F** option upgrades only existing packages. It does not install a package if it wasn’t previously installed.

We like to add the **-vh** options with the **rpm** command. These options add verbose mode and use hash marks that can help monitor the progress of the installation. So when we use **rpm** to install a package, we run the following command:

![Images](f0132-02.jpg)

There’s one more thing associated with a properly designed RPM package. When unpacking a package, the **rpm** command checks to see whether it would overwrite any configuration files. The **rpm** command tries to make intelligent decisions about what to do in this situation. As suggested earlier, if the **rpm** command chooses to replace an existing configuration file, it provides a warning (in most cases) similar to this:

![Images](f0132-03.jpg)

The **rpm** command normally works in the same fashion when a package is erased with the **-e** switch. If a configuration file has been changed, it’s also saved with an .rpmsave extension in the same directory.

It’s up to you to look at both files and determine what modifications, if any, need to be made. Of course, as not every RPM package is perfect, there’s always a risk that such an update would overwrite that critical customized configuration file. In that case, backups are important.

In general, the **rpm** commands to upgrade a package work only if the package being installed is of a newer version. Sometimes, an older version of a package is desirable. As long as there are no security issues with the older package, administrators may be more comfortable with slightly older releases. Bugs that may be a problem on a newer package may not exist in an older version of that package. So if you want to “downgrade” a package with the **rpm -i**, **-U**, or **-F** command, the **--force** switch can help.

![Images](job.jpg)

**If you’ve already customized a package and then upgraded it with** rpm**, check if there is a saved configuration file ending with an .rpmnew extension. Use it as a guide to change the settings in the new configuration file. But remember, with upgrades, there may be additional required changes. Therefore, you should test the result for every conceivable production environment.**

#### Uninstall an RPM Package

The **rpm -e** command uninstalls a package. But first, RPM checks a few things. It performs a dependency check to make sure no other packages need what you’re trying to uninstall. If dependent packages are found, **rpm -e** fails with an error message identifying these packages. With properly configured RPMs, if you have modified related configuration files, RPM makes a copy of the file, adds an .rpmsave extension to the end of the filename, and then erases the original. It can then proceed with the uninstallation. When the process is complete, it removes the package from the database.

![Images](job.jpg)

**Be very careful about which packages you remove from a system. Like many other Linux utilities,** rpm **may silently let you shoot yourself in the foot. For example, if you were to remove the packages that include the running kernel, it could render that system unusable at the next boot.**

#### Install RPMs from Remote Systems

With the RPM system, you can even specify package locations similar to an Internet address, in URL format. For example, if you want to apply the **rpm** command to the foo.rpm package on the /pub directory of the ftp.rpmdownloads.com FTP server, you can install this package with a command such as the following:

![Images](f0133-01.jpg)

Assuming you have a network connection to that remote server, this particular **rpm** command logs on to the FTP server anonymously and downloads the file. Unfortunately, an attempt to use wildcards in the package name with this command leads to an error message associated with “file not found.” The complete package name is required, which can be an annoyance.

If the FTP server requires a username and password, you can include them in the following format:

![Images](f0133-02.jpg)

where *username* and *password* are the username and password you need to log on to this system, and *port*, if required, specifies a nonstandard port used on the remote FTP server.

Based on the preceding example, if the username is **mjang** and the password is **Ila451MS**, you could install an RPM directly from a remote server with the following command:

![Images](f0133-03.jpg)

#### RPM Installation Security

Security can be a concern, especially with RPM packages downloaded over the Internet. If a “black hat” hacker were to somehow be able to modify the content of a third-party repository, how would you know that packages from those sources were genuine? The key is GNU Privacy Guard (GPG), which is the open-source implementation of Pretty Good Privacy (PGP). If an RPM file is signed using a private GPG key, the integrity of the package can be verified with the corresponding public GPG key. A valid signature also ensures that the package has been signed by an authorized party and does not come from a malicious hacker.

If you haven’t imported or installed the Red Hat public GPG keys, you might have noticed something similar to the following message when packages are installed:

![Images](f0134-01.jpg)

If you’re concerned about security, this warning should raise alarm bells. During the RHEL 9 installation process, GPG keys are stored in the /etc/pki/rpm-gpg directory. Take a look at the contents of this directory. You’ll find files such as RPM-GPG-KEY-redhat-release. To actually use the key to verify packages, it has to be imported—and the command to import the GPG key is fairly simple:

![Images](f0134-02.jpg)

If there’s no output, the **rpm** command probably successfully imported the GPG key. The GPG key is now included in the RPM database, which can be verified with the **rpm -qa gpg-pubkey** command.

In the /etc/pki/rpm-gpg directory, there are normally two GPG keys available, as described in [Table 4-1](#ch04.xhtml_ch4tab1).

TABLE 4-1 GPG Keys to Verify Software Updates

![Images](f0134-03.jpg)

Later in this chapter, you’ll see how GPG keys are imported automatically from remote repositories when new packages are installed.

#### Updating the Kernel

Kernel updates incorporate new features, address security issues, and generally help Linux systems work better. However, kernel updates can go wrong and prevent systems booting or cause applications to break; this is particularly common if specialized packages that depend on an existing version of a kernel have been installed.

If you are aware of any software that relies on a custom kernel module, don’t upgrade a kernel if you’re not ready to repeat every step taken to customize software with the existing kernel, whether that be obtaining new closed-source kernel modules from the vendor for the new version, rebuilding specialized modules for the new kernel, or performing other manual work. For example, the drivers for a few wireless network cards and printers without in-tree open-source drivers may be tied to a specific version of a kernel. Some virtual machine software components (not including KVM) may be installed against a specific version of a kernel.

If you see an available update for a kernel RPM, the temptation is to run the **rpm -U *newkernel*** command. Don’t do it! It overwrites your existing kernel, and if the updated kernel doesn’t work with the system, you’re out of luck. (Well, not completely out of luck, but if you reboot and have problems, you’ll have to use rescue mode, discussed in [Chapter 5](#ch05.xhtml), to boot the system and reinstall the existing kernel. In the days when there were separate Troubleshooting and System Maintenance sections on the RHCE exam, that might have made for an interesting test scenario.) The best option for upgrading to a new kernel is to install it, specifically with a command such as this:

![Images](f0135-01.jpg)

If you’re connected to an appropriate repository, the following command works equally well:

![Images](f0135-02.jpg)

This installs the new kernel, along with related files, side by side with the current working kernel. One example of the result is shown in [Figure 4-1](#ch04.xhtml_ch4fig1), in the output to the **ls /boot** command.

FIGURE 4-1 New and existing kernel files in the /boot directory

![Images](F04-01.jpg)

![Images](job.jpg)

**It is also safe to install a new kernel by running** dnf update kernel**. In fact, by default,** dnf **is configured to always install a kernel package and leave any old kernel in place. This applies to a maximum of three kernels installed at the same time.**

[Table 4-2](#ch04.xhtml_ch4tab2) briefly describes the different files for the various parts of the boot process in the /boot directory.

TABLE 4-2 Files in the /boot Directory

![Images](f0136-01.jpg)

The installation of a new kernel adds options to boot the new kernel in the GRUB configuration file (/boot/grub2/grub.cfg), without erasing existing options. By default, the system will boot with the newly installed kernel. Therefore, if that kernel does not work, you can restart the system, access the GRUB menu, and then boot from the older, previously working kernel.

### CERTIFICATION OBJECTIVE 4.02

### More RPM Commands

The **rpm** command is rich with details. All this book can do is cover some of the basic ways **rpm** can help you manage RHEL. You’ve already read about how **rpm** can install and upgrade packages in various ways. Queries can help you identify what’s installed in detail. Verification tools can help you check the integrity of packages and individual files. You can use related tools to help identify the purpose of different RPMs and to compile a full list of RPMs already installed.

#### Package Queries

The simplest **rpm** query verifies whether a specific package is installed. The following command verifies the installation of the systemd package (the version number may vary):

![Images](f0137-02.jpg)

You can do more with **rpm** queries, as described in [Table 4-3](#ch04.xhtml_ch4tab3). Note how queries can be performed either with -**q** or **--query**; full-word switches such as **--query** are usually associated with a double-dash.

TABLE 4-3 rpm --query Options

![Images](f0137-01.jpg)

If you want to query an RPM package file rather than the local RPM database, all you have to do is add the **-p** switch and specify the path or URL of the package file. As an example, the following command lists all files of the RPM package epel-release-latest-9.noarch.rpm:

![Images](f0137-03.jpg)

#### Package Signatures

RPM uses several methods for checking the integrity of a package. You’ve seen how to import the GPG key. Some of the available methods are shown when you verify a package with the **rpm --checksig *pkg.rpm*** command. (The **-K** switch is equivalent to **--checksig**.) For example, if you’ve downloaded a package from a third party such as the hypothetical pkg-1.2.3-4.noarch.rpm package and want to check it against the imported GPG keys, run the following command (**-v** makes the output verbose):

![Images](f0138-01.jpg)

If successful, you’ll see output similar to the following:

![Images](f0138-02.jpg)

This guarantees that the package is authentic and the RPM file was not modified by a third party. You may already recognize the algorithms used to verify package integrity:

![Images](square.jpg)   **rsa** Named for its creators, Rivest, Shamir, and Adleman, it’s a public key encryption algorithm.

![Images](square.jpg)   **sha1** Secure Hash Algorithm-1, a cryptographic hash function that produces a 160-bit hash value.

![Images](square.jpg)   **sha256** A cryptographic hash function that produces a 256-bit hash value.

![Images](square.jpg)   **md5** Message Digest 5, a cryptographic hash function that produces a 128-bit hash value.

#### File Verification

The verification of an installed package compares information about that package with information from the RPM database on a system. The **--verify** (or **-V**) switch checks the size, MD5 checksum, permissions, type, owner, and group of each file in the package. Verification can be done in a number of ways. Here are a few examples:

![Images](square.jpg)   Verify all files. Naturally, this may take a long time on your system. (Of course, the **rpm -Va** command performs the same function.)

`# rpm --verify –a`

![Images](square.jpg)   Verify all files within a package against a downloaded RPM.

`# rpm --verify -p vsftpd-3.0.3-49.el9.x86_64.rpm`

![Images](square.jpg)   Verify a file associated with a particular package.

`# rpm --verify --file /bin/ls`

If the integrity of the files or packages is verified, you will see no output. Any output means that a file or package is different from the original. There’s no need to panic if certain changes appear; after all, administrators do edit configuration files. There are nine tests. If there has been a change, the output is a string of up to eight failure code characters, each of which tells you what happened during each test.

If you see a dot (.), that test passed. The following example shows /bin/vi with an incorrect group ID assignment:

![Images](f0139-02.jpg)

[Table 4-4](#ch04.xhtml_ch4tab4) lists the failure codes and their meanings.

TABLE 4-4 rpm --verify Codes

![Images](f0139-01.jpg)

Now here’s an interesting experiment: When you have one version of a package installed, use the **rpm --verify -p** command with a second version of the same package. Finding such a package should not be too difficult because Red Hat updates packages for feature updates, security patches, and, yes, bug fixes frequently. For example, when we wrote this book for RHEL 9, we had access to both sssd-client-2.7.3-4.el9.x86_64.rpm and sssd-client-2.8.2-2.el9.x86_64.rpm. When the latter version was installed, we ran the command

![Images](f0139-03.jpg)

and got a whole list of changed files, as shown in [Figure 4-2](#ch04.xhtml_ch4fig2). This command provides information on what was changed between different versions of the sssd-client package.

FIGURE 4-2 Verifying changes between packages

![Images](F04-02.jpg)

EXERCISE 4-1

*Practice with rpm Commands*

In this exercise, you’ll practice with some of the **rpm** command options that we have described so far.

1.   In VMware Workstation (or the hosted hypervisor application that you are using), select your server1 VM and click Edit Virtual Machine Settings.

2.   Mount the RHEL 9 ISO file that you downloaded in [Chapter 1](#ch01.xhtml). To do so, in the Settings window select CD/DVD (SATA) and click Use ISO Image. Browse and select the path of the RHEL 9 ISO image. Ensure that the option Connected is selected.

3.   Log in to the system and type the **df** command. If the DVD was automounted, you should see an entry in the **df** output that shows that the DVD is available at a directory path such as /run/media/*yourusername*/RHEL-9-1-0-BaseOS-x86_64\. If for some reason you do not see the DVD being mounted, you can mount it manually by entering the following command (as root):

`# mount /dev/cdrom /media`

4.   Change the directory to the directory where the DVD is mounted by entering either

![Images](f0141-01.jpg)

or, if you mounted the DVD manually,

![Images](f0141-02.jpg)

5.   List the content of this directory. You should notice that there are two directories, BaseOS and AppStream, which include the RPM packages of the BaseOS and AppStream repositories.

![Images](f0141-03.jpg)

6.   Change to the BaseOS/Packages/ directory and list its contents:

![Images](f0141-04.jpg)

7.   Find information about the RPM package tmux (the exact version of the package may differ, depending on which version of the RHEL 9 DVD you have mounted):

![Images](f0141-05.jpg)

8.   Check if the tmux package is installed by entering the following command. In a typical Red Hat installation, you should find that this package is not present.

![Images](f0141-06.jpg)

9.   Install the tmux RPM package:

![Images](f0141-07.jpg)

10.   List the files that have been created after the installation of the tmux package:

![Images](f0141-08.jpg)

### CERTIFICATION OBJECTIVE 4.03

### Dependencies and the dnf Command

The **dnf** command makes it easy to add and remove software packages to and from a system. It maintains a database regarding the proper way to add, upgrade, and remove packages. This makes it relatively simple to add and remove software with a single command. That single command overcame what was known as “dependency hell.”

The **dnf** command extends the capabilities of **yum**, which was originally developed for an old Linux distribution now discontinued, Yellow Dog Linux. The name of the command is based on the Yellowdog Updater, Modified (YUM). Given the trouble associated with dependency hell, Linux users were motivated to find a solution. The **yum** command was adapted for Red Hat distributions with the help of developers from Duke University.

The configuration of **dnf** depends on package libraries known as repositories. Red Hat repositories are available through Red Hat Subscription Management, while repositories of third-party rebuild distributions use their own publicly available servers. In either case, it’s important to know the workings of the **dnf** command as well as how it installs and updates individual packages and package groups.

#### An Example of Dependency Hell

To understand more about the need for the **dnf** command, examine [Figure 4-3](#ch04.xhtml_ch4fig3). This **rpm** command tries to install the **gcc** compiler, but fails because some dependencies are missing. Although how to use a compiler is not an exam requirement, the associated package dependencies will illustrate the need for **dnf**.

FIGURE 4-3 Excerpt of the packages required to install the gcc RPM

![Images](F04-03.jpg)

You could try to use the **rpm** command to install each of these packages. To do so, take the following steps:

1.   Include the RHEL 9 DVD. Insert it into its drive, or make sure it’s included in the configuration for the target virtual machine.

2.   Unless it’s already mounted, mount that DVD with the following command. Of course, a different empty directory can be substituted for /media.

`# mount /dev/cdrom /media`

3.   Navigate to the directory where the DVD is mounted (that is, /media or some subdirectory of /media).

4.   The RPM packages on the RHEL 9 DVD can be found in the BaseOS/Packages/ and AppStream/Packages/ subdirectories of the DVD. Navigate to the AppStream/Packages directory of the DVD.

5.   Enter the **rpm -ivh** *command, and then type in the names of the packages listed in [Figure 4-3](#ch04.xhtml_ch4fig3). It may be easiest to use command completion for this purpose; for example, if you were to type in*

`# rpm -ivh glibc-devel-`

you could then press the TAB key twice and review available packages that start with **glibc-devel-**. You could then enter additional letters and press the TAB key again to complete the name of the package.

6.   After a bit of work, you’d end up with something similar to the command and results shown in [Figure 4-4](#ch04.xhtml_ch4fig4). What actually appears depends on the current revision level of each package, as well as what’s already installed on the local system.

FIGURE 4-4 These packages have dependencies.

![Images](F04-04.jpg)

7.   The next step is to try to include the missing dependencies in the list of packages to be installed. When we try this step, it leads to the command and results shown in [Figure 4-5](#ch04.xhtml_ch4fig5).

FIGURE 4-5 There are even more dependencies.

![Images](F04-05.jpg)

At this point, we do not have more dependencies to install, but for some RPM packages there could be even more levels of dependent packages to include. This pain is known as dependency hell.

#### Relief from Dependency Hell

Before **yum** and **dnf**, some attempts to use the **rpm** command were stopped by the dependencies described earlier. Sure, you could install those dependent packages with the same command, but what if those dependencies themselves have dependencies? That perhaps is the biggest advantage of the **yum** and **dnf** commands.

Before **yum**, RHEL incorporated dependency resolution into the update process. Through RHEL 4, this was done with **up2date**. Red Hat incorporated **yum** starting with RHEL 5\. Since RHEL 8, **yum** is a symbolic link to **dnf**, the next-generation package manager, which supports all the **yum** command options and more.

With **dnf**, all you need to do to install the packages listed in [Figure 4-4](#ch04.xhtml_ch4fig4) is run the following command:

`# dnf install gcc`

If so prompted, accept the request to install additional dependent packages, and then all of the noted dependencies are installed automatically. (Yes, the **-y** switch would perform the same function.) If updates are available from connected repositories, the latest available version of each package is installed. The **dnf** command is described in more detail later in this chapter.

But if you’re running RHEL 9 without a connection to Red Hat Subscription Management, nothing happens. Shortly, you’ll see how to do so.

A number of third-party repositories are available for RHEL. They include several popular applications that are not supported by Red Hat. For example, one of the authors of this book uses an external repository to install packages associated with his laptop wireless network card.

Although the owners of these repositories work closely with some Red Hat developers, there are some reports where dependencies required from one repository are unavailable from other repositories, leading to a different form of “dependency hell.” However, the more popular third-party repositories are excellent; we have never encountered dependency hell when using these repositories.

![Images](job.jpg)

**There are two main reasons why Red Hat does not include most proven and popular packages available from third-party repositories. Some are not released under open-source licenses, and others are packages that Red Hat simply chooses not to support.**

#### Red Hat Subscription Management

Relief from dependency hell depends on the proper configuration of **dnf**. You need to know not only how to configure **dnf** to connect to repositories over the Internet but also how to configure **dnf** to connect to repositories on a local network.

The RHCSA exam objectives require candidates to be able to “install and update software packages from Red Hat Network.” As previously mentioned, while the Red Hat Network has been succeeded by Red Hat Subscription Management, the exam objective continues to refer to this service by its legacy name. Access to Red Hat Subscription Management is provided over the Internet or over a local Red Hat Satellite server.

Perhaps the key benefit of Red Hat Satellite (or an alternative such as Spacewalk or Katello) is the ability to store software packages on a local system on the network. Once an appropriate connection is configured from the client systems, Satellite Server can even run remote commands on any schedule. If you’re administering a whole bunch of systems, Red Hat Satellite supports configuration of systems in groups. For example, if there are 10 systems configured as RHEL 9–based web servers, you can configure those systems as a single group. You can then schedule a single command that’s applied to all of those systems remotely. For more information on Red Hat Satellite, see the latest version of the documentation, available from [https://access.redhat.com/products/](https://access.redhat.com/products/). However, this is out of scope for the RHCSA exam.

If you have enrolled in the Red Hat Developer Program, as explained in [Chapter 1](#ch01.xhtml), you are entitled to use a Red Hat Developer subscription. Exercise 4-2 explains how to subscribe your system to the RHSM.

EXERCISE 4-2

**Subscribe a System to Red Hat Subscription Management**

1.   If you haven’t done so already, join the Red Hat Developer Program and register at [https://developers.redhat.com](https://developers.redhat.com). If you do not have an account, create a new one.

2.   Point the browser to [https://access.redhat.com/management/subscriptions/](https://access.redhat.com/management/subscriptions/). You should see a Red Hat Developer Subscription for Individuals in your inventory. This subscription allows you to register a RHEL system and download updates from RHSM.

3.   Log in to the server1.example.com system that you installed in [Chapter 1](#ch01.xhtml). Run the following command to register this system with RHSM. You will be prompted to type your Red Hat account username and password. If the system is already registered, use the **--force** command option to re-register the machine.

`# subscription-manager register`

4.   Subscribe the system to a Red Hat product. In the following command, the --auto option finds the most appropriate subscription (which will be the Red Hat Developer subscription, if you don’t have any others):

`# subscription-manager attach --auto`

5.   Alternatively, list all available subscriptions. Take note of the pool IDs.

`# subscription-manager list --available`

Then, use the pool ID that you have retrieved from the last command to attach a system to a subscription:

![Images](f0145-04.jpg)

6.   Review current settings. Run the following command to list the subscriptions attached to the system:

![Images](f0146-01.jpg)

The command output should be similar to that shown here:

![Images](f0146-02.jpg)

7.   Show all available repositories available for the system:

![Images](f0146-03.jpg)

8.   Show the repositories currently enabled:

`# subscription-manager repos --list-enabled`

The command output should be similar to the following:

![Images](f0146-04.jpg)

9.   You can enable additional repositories with the following command:

![Images](f0146-05.jpg)

10.   Confirm with the following **dnf** command that the system is subscribed to the BaseOS and AppStream repositories:

![Images](f0147-01.jpg)

The command output should be similar to the following:

![Images](f0147-02.jpg)

11.   The system is now ready for the installation of new packages. Try running the following command to install a software package:

![Images](f0147-03.jpg)

The result should be similar to what’s shown below. As you see, in this example the **dnf** command not only downloads and installs the wireshark RPM but also installs the dependent packages to make sure that all software dependencies are satisfied.

![Images](f0147-04.jpg)

#### Basic dnf Configuration

Now that you are subscribed to repositories on the RHSM, you have to understand how **dnf** is configured in some detail. It starts with the /etc/dnf/dnf.conf configuration file and continues with files in the /etc/dnf and /etc/yum.repos.d directories. As you can see, even though **dnf** is the current tool, directory names still feature the term **yum**. To get the full list of **dnf** configuration directives and their current values, run the following command:

![Images](f0148-01.jpg)

##### The Basic dnf Configuration File: dnf.conf

This section analyzes the default version of the /etc/dnf/dnf.conf file, line by line. Although you won’t make changes to this file in most cases, you need to understand at least the standard directives in this file if something goes wrong. The following lines are straight excerpts from the default version of this file. The first directive is a header; the **[main]** header suggests that all directives that follow apply globally to **dnf**:

`[main]`

The **gpgcheck** boolean directive makes sure the **dnf** command actually checks the GPG signature of downloaded packages:

`gpgcheck=1`

The **installonly_limit** directive specifies how many of the packages listed in the **installonlypkgs** option (usually the kernel) can be installed at the same time:

`installonly_limit=3`

The **clean_requirements_on_remove** boolean directive instructs **dnf** to go through each package dependency when removing packages. If this configuration option is set to True, any dependencies that are not required by other packages will also be removed.

`clean_requirements_on_remove=True`

If enabled, the **best** directive tells **dnf** to always try to install the highest version available of a package during an upgrade:

`best=True`

##### Configuration Files in the /etc/dnf/plugins Directory

The default files in the /etc/dnf/plugins directory configure a connection between **dnf** and the Red Hat Portal or a local Satellite server. If you’re studying from a RHEL rebuild distribution such as AlmaLinux, you’ll see a different set of files in this directory. This is a Red Hat book, however, so the focus will be on the two basic files in the RHEL 9 installation.

**Spacewalk Plugin**   If you have a subscription to the RHSM via an old version of Red Hat Satellite Server, the spacewalkplugin.conf file in this directory is especially important. The directives, shown next, enable the plugin and check GPG signatures of RPM packages:

![Images](f0149-01.jpg)

**Red Hat Subscription Management Plugins**  The subscription-manager.conf and product-id.conf files are designed to connect the **dnf** system to the Red Hat Portal using Subscription Management. As discussed in this chapter, Subscription Management is used to subscribe a system to RHSM for system updates. The file subscription-manager.conf is straightforward. The first directive enables the plugin. The last directive, if set to 1, disables all repositories that are not managed by Subscription Management. This is useful when the system runs Fedora and you do not want to use the default system repositories because the system is managed by Red Hat Satellite or Katello.

![Images](f0149-02.jpg)

##### Configuration Files in the /etc/yum.repos.d Directory

The configuration files in the /etc/yum.repos.d directory are designed to connect systems to actual **dnf** repositories. If you’re running a rebuild distribution such as AlmaLinux, you’ll see files with the .repo extension in this directory, which configure access to public repositories on the Internet. If you’re running RHEL 9 and registered the system with Red Hat Subscription Management, you’ll see a redhat.repo file, which lists all the repositories available for the system on the Red Hat Portal.

A couple of elements in common for configuration files in the /etc/yum.repos.d directory are the file extension (.repo) and the documentation, available with the **man dnf.conf** command.

A properly configured .repo file in the /etc/yum.repos.d directory can be a terrific convenience to enable the installation of groups of packages with the **dnf** command. As the /etc/yum.repos.d directory might be empty on a new RHEL 9 system, you should know how to create that file from scratch, using data for the installation server and information available in the dnf.conf man page.

**Understand the Default redhat.repo Configuration File**  If you have subscribed the system to Red Hat Subscription Management, you should see a redhat.repo file in the /etc/yum.repos.d directory, with content similar to that shown in [Figure 4-6](#ch04.xhtml_ch4fig6). Although it includes a number of different repositories, you can learn from the pattern of directives configured for each repository.

FIGURE 4-6 Several repositories configured in one file

![Images](F04-06.jpg)

There are several stanzas in the redhat.repo file, one for each Red Hat repository. For example, the first stanza shown in [Figure 4-6](#ch04.xhtml_ch4fig6) defines the configuration settings for the BaseOS repository. The first line, in brackets, provides a name for the repository. In this case, **[rhel-9-for-x86_64-baseos-rpms]** just stands for the name of the base repository used by RHEL 9\. It doesn’t represent the directory where the associated packages are installed.

Although the name of the repository follows, it’s just for documentation purposes and does not affect how packages or package databases are read or downloaded. In fact, the inclusion of the **name** directive is optional.

![Images](f0150-02.jpg)

The **baseurl** directive specifies the URL that contains the actual repository of packages. It commonly works with either the HTTP/HTTPS or FTP protocol. It can even work with local directories or mounted Network File System shares.

![Images](f0150-03.jpg)

The **enabled** directive specifies if a repository is enabled or not:

![Images](f0150-04.jpg)

When you run the **dnf repolist** command, the name of all the enabled repositories will be shown in output similar to the following.

![Images](f0151-01.jpg)

If you want to disable checking the GPG signatures of each package to be downloaded (a bad idea!), the following command puts that wish into effect:

![Images](f0151-02.jpg)

Of course, if you enable **gpgcheck**, any GPG check requires a GPG key; the following directive specifies one key from the local /etc/pki/rpm-gpg directory for that purpose:

![Images](f0151-03.jpg)

**Create Your Own /etc/yum.repos.d Configuration File**  You need to learn how to create a local configuration file in the /etc/yum.repos.d directory, to allow the installation of packages from repositories other than the Red Hat ones. To do so, you’ll need to set up a text file with a .repo extension in the /etc/yum.repos.d directory. That file needs only three lines.

On RHEL 9, especially during an exam, the /etc/yum.repos.d directory may be empty. So you may not have access to an existing configuration file to use as a template. The man page of the dnf.conf file may look overwhelming if you need to find information during the RHCSA exam.

Fortunately, the **dnf config-manager** command allows you to easily configure a repository. To configure a new repository, the only thing you need is to pass to **dnf config-manager** the URL of the repo:

![Images](f0151-04.jpg)

This command will create a file named myrepo.example.com.repo with the same content as shown in [Figure 4-7](#ch04.xhtml_ch4fig7).

FIGURE 4-7 Excerpt from a .repo file

![Images](F04-07.jpg)

Next, you can open the file and customize the settings. The identifier for the repository is shown in brackets. Unless specified by the RHCSA exam, it doesn’t matter what single word you put between the brackets as the identifier.

Alternatively, you can create the .repo file manually. For example, create a new file named whatever.repo in the /etc/yum.repos.d directory. (To some extent, the filename of the .repo file does not matter, as long as it has a .repo extension in the /etc/yum.repos.d directory.) In that file, add the following identifier:

![Images](f0152-01.jpg)

Next comes the **name** directive for the repository. This should be human readable and does not affect the functionality of the repository. To demonstrate, we add the following directive:

![Images](f0152-02.jpg)

![Images](exam.jpg)

**You should learn how to create a working .repo file in the /etc/yum.repos.d directory during Red Hat exams. It can be a big timesaver when you need to install additional packages.**

Finally, there’s the **baseurl** directive, which can be configured to point to an installation server. The RHCSA requirements imply that you need to know how to install software from the Red Hat Network. They also suggest that you need to know how to install and update packages from a remote repository. To meet this objective, you need to know the URL of that remote server or repository. It’s reasonable to expect that URL to be provided during the exam.

For example, in a classroom environment, a **baseurl** directive may look like this:

`baseurl=http://192.168.122.1/inst`

Next, add the following line:

`gpgcheck=0`

That’s all you need. Of course, security is important in real life, and for this reason you should enable **gpgcheck** and specify where the GPG key is found with the **gpgkey** directive. But if your focus is on the exam, the best advice is often to keep things as simple as possible.

EXERCISE 4-3

**Create a dnf Repository from the RHEL 9 DVD**

This exercise requires access to the RHEL 9 DVD. You’ll be using the tester1.example.com system that you installed in [Chapter 1](#ch01.xhtml). Because this system is not subscribed to the Red Hat Subscription Management (if it is, run **subscription-manager unregister**), you will create a **dnf** repository to install packages locally from the RHEL 9 DVD.

1.   In VMWare Workstation (or your hosted hypervisor), select your tester1 VM and click Settings.

2.   Mount the RHEL 9 ISO file that you downloaded in [Chapter 1](#ch01.xhtml). To do so, in the Settings window select CD/DVD (SATA) and click Use ISO Image. Browse and select the path of the RHEL 9 ISO image. Ensure that the option Connected is selected.

3.   Log in to the system and type the **df** command. If the DVD was automounted, you should see an entry in the **df** output that shows that the DVD is available at a directory path such as /run/media/*yourusername*/RHEL-9-1-0-BaseOS-x86_64\. If for some reason you do not see the DVD being mounted, you can mount it manually by entering the following command (as root):

`# mount /dev/cdrom /media`

In this exercise we assume that the DVD is mounted to /run/media/*yourusername*/RHEL-9-1-0-BaseOS-x86_64\. Change your commands accordingly if this is not the case.

4.   Navigate to the /etc/yum.repos.d directory.

5.   Open a new file in a text editor and name it (for example) **rhel9.repo**.

6.   Edit the rhel9.repo file. Create a new stanza of directives. Use an appropriate stanza title such as **[rhel]**.

7.   Specify BaseOS as a **name** directive for the repository.

8.   Include a **baseurl** directive set to **file:///run/media/*yourusername*/RHEL-9-1-0-BaseOS-x86_64/BaseOS**/.

9.   Include an **enabled=1** directive.

10.   Add **gpgkey=0**.

11.   Save and close the file.

12.   Run the **dnf clean all** and **dnf update** commands.

13.   Next, try the following command:

`# dnf install tmux`

14.   If successful, you should see the following output:

![Images](f0153-03.jpg)

You’ve now set up a repository on the local DVD.

15.   Restore the original configuration by deleting the rhel9.repo file from the /etc/yum.repos.d directory.

#### Third-Party Repositories

Other groups of third-party developers create packages for RHEL 9. They include packages for some popular software not supported by Red Hat. The website for one of these third parties can be found at [https://docs.fedoraproject.org/en-US/epel/](https://docs.fedoraproject.org/en-US/epel/).

To add third-party repositories to a system, you’d create a custom .repo file in the /etc/yum.repos.d directory.

Some repositories, such as EPEL (Extra Packages for Enterprise Linux), simplify the configuration by providing an RPM package that includes a .repo configuration file and a GPG key to verify the packages. To configure the repository, all you have to do is install that RPM file:

![Images](f0154-01.jpg)

If you want to disable any repository in the /etc/yum.repos.d directory, add the following directive to the applicable repository file:

![Images](f0154-02.jpg)

EXERCISE 4-4

**Configure Access to the EPEL Repository**

In this exercise, you will configure access to the EPEL repository. Rather than installing the epel-release-latest-9.noarch.rpm package, as just described, you will configure the repository manually. This will provide you a great opportunity to practice with the configuration of a repository.

1.   Log in to the server1.example.com system.

2.   Run the following command:

![Images](f0154-03.jpg)

3.   The command has created a file named epel.repo in the /etc/yum.repos.d/ directory.

4.   Install the calc RPM package, which comes from the EPEL repository:

![Images](f0154-04.jpg)

#### Basic dnf Commands

If you want to learn more about the intricacies of the **dnf** command, run the command by itself. You’ll see the following output scroll by, probably far too fast. Of course, you can pipe the output to the **less** command pager with the **dnf | less** command.

![Images](f0155-01.jpg)

You’ll examine how a few of these commands and options work in the following sections. Although you might not have Internet access during a Red Hat exam, you may have a network connection to a locally configured repository, which you should be ready to configure via the appropriate file in the /etc/yum.repos.d directory, as described earlier. As well as during the exam, **dnf** is an excellent tool for administering Red Hat systems.

Start with a simple command: **dnf list**. It’ll return a list of all packages, whether they’re installed or available, along with their version numbers and repositories. **dnf list | grep *packagename*** tells you what version of a package you will get with a **dnf install**. If you want to show all the configured repositories, you can do this with **dnf repolist all**. More information about a specific package can be obtained via the **dnf info** command. For example, the following command is functionally equivalent to **rpm -qi samba**:

`# dnf info samba`

The **rpm -qi** command works if the queried package is already installed, because it retrieves information directly from the RPM database on the local system. Conversely, the **dnf info** command is not subject to that limitation, because it retrieves information from the upstream software repositories. It queries the repository metadata and displays information about the specified package.

#### Installation Mode

There are two basic installation commands. If you haven’t installed a package before, or you want to update it to the latest stable version, run the **dnf install *packagename*** command. You don’t need to specify the version or release number. Only the package name is required. For example, if you’re checking for the latest version of the Samba RPM, the following command will update it or add it if it isn’t already installed on the target system:

`# dnf install samba`

If you just want to keep the packages on a system up to date, run the **dnf update *packagename*** command. For example, if you already have the Samba RPM installed, the following command makes sure it’s updated to the latest version:

`# dnf update samba`

If you haven’t installed Samba, this command doesn’t add it to your installed packages. In that way, the **dnf update** command is analogous to the **rpm -F** command.

Of course, the **dnf** command is not complete without options that can remove a package. The first one is straightforward because it uninstalls the Samba package along with any dependencies:

`# dnf remove samba`

The **dnf update** command by itself is powerful; if you want to make sure that all installed packages are updated to the latest stable versions, run the following command:

`# dnf update`

The **dnf update** command may take some time as it communicates with the Red Hat Portal or other repositories. It may need to download the current database of packages with all dependencies. It then finds all packages with available updates and adds them to the list of packages to be updated. It finds all dependent packages if they’re not already included in the list of updates.

What if you just want a list of available updates? The **dnf list updates** command can help there. It’s functionally equivalent to the **dnf check-update** command.

But what if you aren’t quite sure what to install? For example, if you want to install the Evince document reader and think the operational command includes the term “evince,” then the **dnf provides "*/*evince**"** command can help.

Alternatively, to search for all instances of files with the .repo extension, run the following command:

`# dnf provides "*/*.repo"`

It lists all instances of the packages with files that end with the .repo extension, with the associated RPM package. The wildcard is required because the **provides** option requires the full path to the file. It accepts partial filenames; for example, the **dnf provides "/etc/systemd/*"** command returns the RPM associated with files in the /etc/systemd directory. Once the needed package is known, you can proceed with the **dnf install *packagename*** command.

![Images](job.jpg)

**In many cases, problems with** dnf **can be solved with the** dnf clean all **command. If there are recent updates to Red Hat packages (or third-party repositories), this command flushes the current cache of metadata, allowing you to synchronize metadata with configured repositories, without having to wait the default 24 hours before the cache is automatically flushed.**

#### Security and dnf

GPG digital signatures can verify the integrity and authenticity of **dnf** updates. It’s the same system described earlier in this chapter for RPM packages. As an example, look at the output the first time a new package is installed over a network on RHEL 9:

`# dnf install samba`

After packages are downloaded, you’ll see something similar to the following messages:

![Images](f0157-02.jpg)

If you’re simultaneously downloading packages from other repositories, additional GPG keys may be presented for approval. As suggested by the last line, **N** is the default response; you actually have to type in **y** to proceed with the download and installation—not only of the GPG key but also of the package in question.

You may notice that the GPG key used is from the same directory of keys associated with the **rpm** command earlier in this chapter.

#### Updates and Security Fixes

Red Hat maintains a public list of errata, classified by RHEL release, at [https://access.redhat.com/errata-search/](https://access.redhat.com/errata-search/). If you have a RHEL subscription, affected packages are normally made available through the Red Hat Portal; for RHSM-connected machines, all you need to do is run the **dnf update** command periodically. This list is useful for those third parties who use RHEL source code, such as AlmaLinux and even Oracle Linux; typically RHEL rebuilds provide similar errata shortly after Red Hat.

#### Package Groups and dnf

The **dnf** command can do more. It can install and remove packages in groups. With the following command, you can identify available package groups from configured repositories:

`# dnf group list`

Note how the groups are divided into installed and available groups. Some of the groups listed may be of particular interest, such as “Virtualization Host,” which installs the KVM hypervisor. To find out more about this group, run the following command. The output is shown in [Figure 4-8](#ch04.xhtml_ch4fig8).

FIGURE 4-8 Packages in the Virtualization Host group

![Images](F04-08.jpg)

`# dnf group info "Virtualization Host"`

There are two types of groups in **dnf**: regular groups, which include standard RPM packages, and environment groups, which are made of other groups. “Virtualization Host” in [Figure 4-8](#ch04.xhtml_ch4fig8) is identified as an “Environment Group” and is in fact a collection of regular groups.

To list all groups, you can type

`# dnf group list hidden`

Let’s get some information about one of the regular groups:

`# dnf group info "Remote Desktop Clients"`

Note how the packages are all listed as “Optional Packages,” as shown in [Figure 4-9](#ch04.xhtml_ch4fig9).

FIGURE 4-9 Packages in the Remote Desktop Clients group

![Images](F04-09.jpg)

In other words, they’re not normally installed with the package group. Thus, suppose you were to run the following command:

`# dnf group install "Remote Desktop Clients"`

Nothing would be installed. Optional packages from this package group can be installed with the following command option:

`# dnf group install --with-optional "Remote Desktop Clients"`

But Optional Packages is not the only category. The following command lists all packages in the “Printing Client” package group. The output is shown in [Figure 4-10](#ch04.xhtml_ch4fig10).

FIGURE 4-10 Packages in the Printing Client group

![Images](F04-10.jpg)

`# dnf group info "Printing Client"`

Packages in the Printing Client group are classified in two other categories. Mandatory packages are always installed with the package group. Default packages are normally installed with the package group; however, specific packages from this group can be excluded with the **-x** switch. For example, the following command installs the three mandatory and seven default packages:

`# dnf group install "Printing Client"`

In contrast, the following command excludes the paps and the gutenprint-cups packages from the list of those to be installed:

`# dnf group install "Printing Client" -x paps -x gutenprint-cups`

The options to the **dnf** command are not complete unless there’s a command that can reverse the process. As suggested by the name, the **dnf group remove** command uninstalls all packages from the noted package group:

`# dnf group remove "Printing Client"`

Exclusions are not possible with the **dnf group remove** command. If you don’t want to remove all packages listed in the output to the command, it may be best to remove target packages individually.

#### More dnf Commands

A number of additional **dnf**-related commands are available. Two of them may be of particular interest to those studying for the Red Hat exams: **dnf config-manager** and **dnf download** can, respectively, display all current configuration settings and download individual RPM packages. One more related command is **createrepo**, which can help you set up a local repository.

##### View All Directives with dnf config-manager

To some extent, the directives listed in the dnf.conf and related configuration files provide only a small snapshot of available directives. To review the full list of directives, run the **dnf config-manager --dump** command. Pipe it to the **less** command as a pager. It includes nearly 100 lines. The excerpt from the **[main]** section shown in [Figure 4-11](#ch04.xhtml_ch4fig11) includes settings that apply to all the configured repositories.

FIGURE 4-11 A partial list of dnf directives

![Images](F04-11.jpg)

Some of the directives do not have any default values, such as **exclude**; some don’t really matter, such as the color directives. Some of the most significant directives are shown in [Table 4-5](#ch04.xhtml_ch4tab5). It is not a comprehensive list. If you’re interested in a directive not shown, it’s defined in the man page for the dnf.conf file.

TABLE 4-5 Configuration Parameters from yum-config-manager

![Images](f0161-01.jpg)

##### Package Downloads with dnf download

As suggested by the name, the **dnf download** command can be used to download packages from **yum**-based repositories. It’s a fairly simple command. For example, the following command reviews the contents of configured repositories for a package named cups:

`# dnf download cups`

Either the RPM package is downloaded to the local directory or the command returns the following error messages:

`No package cups available.`

Sometimes, more specifics are required. If there are multiple versions of a package stored on a repository, the default is to download the latest version of that package. That may not always be what you want. For example, if you want to use a specific version of the RHEL 9 kernel, use the following command:

`# dnf download kernel-5.14.0-284.11.1.el9_2`

##### Create Your Own Repository with createrepo

An earlier version of the exam objectives for RHEL 6 suggested that you should know how to “create a private yum repository.” Although that objective has since been removed, it’s a necessary job skill for a Red Hat system engineer.

Custom repositories can provide additional control. Enterprises that want to control the packages installed on their Linux systems can create their own customized repository. Although this can be based on the standard repositories developed for a distribution, it can include additional packages such as custom software unique to an organization. Just as easily, it can omit packages that may violate organizational policies such as games. Limits on the choices for certain functions such as browsers can minimize related support requirements.

To create a customized repository, you need to collect desired packages in a specific directory. The **createrepo** command can process all packages in that directory. The database is created in XML files in a repodata/ subdirectory. An example of this package database already exists in the BaseOS/repodata/ subdirectory of the RHEL 9 DVD.

The Red Hat Portal enables support of customized repositories with related products, such as Red Hat Satellite Server. For more information on repository management, see *Linux Patch Management*, written by Michael Jang and published by Prentice Hall.

### CERTIFICATION OBJECTIVE 4.04

### Module Streams (*)

Suppose you need to install a service, or an application runtime, such as Apache, Perl, or NodeJS, and you need a specific release of that software. With **rpm** or **dnf**, you can specify in the command line the exact version of the package that you want to install. Assuming that this is available in your software repositories, everything will work, until you run **dnf update**. What if a newer major release of that package is available? The package manager will automatically update it to the latest release.

Here’s where *modularity* comes in handy. With module streams, a vendor can distribute multiple releases of the same application, and a system administrator can pin to a specific release when installing the software.

As an example, suppose that you need to install NodeJS 18\. As of this writing, RHEL 9 software repositories include both NodeJS 16 and NodeJS 18\. A command such as **dnf install nodejs** would install version 16\. You could specify the exact version of the package to install, such as **dnf install nodejs-16.***, but the next time that you run **dnf update**, NodeJS may be upgraded to a new major version, if available, which is not what you want.

**NOTE: * Please note that this section will not be on the exam, but contains useful information.**

Fortunately, Red Hat distributes NodeJS 18 as module streams. This way, you can pin to the release that you need and still get patches for that release, but you will never be upgraded to the latest major release when you run **dnf update**.

Some of the more experienced readers may have noticed that module streams try to solve the same problem addressed by software collections in RHEL 7\. In fact, software collections provide the ability to distribute multiple versions of the same application and to install them in a separate root tree. However, there is a major difference with module streams: while software collections allow installation of multiple releases of the same application *concurrently*, module streams only permit installation of one version of an application on a system.

##### Getting Information About Module Streams

As described earlier in this chapter, RHEL 9 comes with two repositories: BaseOS and AppStream. While BaseOS includes the core operating system software, AppStream contains user-level applications, some of which are packaged as modules.

The **dnf module** command has been introduced in RHEL 9 to manage module streams. To familiarize yourself with some of the concepts of modules, list all modules with the **dnf module list** command. An excerpt of the output is shown in [Figure 4-12](#ch04.xhtml_ch4fig12).

FIGURE 4-12 Listing module streams

![Images](F04-12.jpg)

The first column in [Figure 4-12](#ch04.xhtml_ch4fig12), Name, displays the module name, such as nodejs. The second column, Stream, shows the module stream, which is the specific version of that application that we can install.

The next column, Profiles, includes, for each module stream, a list of available profiles. This is a way of grouping RPM packages within module streams. For example, the postgresql 15 module stream has two profiles, client and server. That means that we can choose to install PostgreSQL for a server installation or for a client by specifying the profile that we wish to install.

Note that some profiles are marked as default, **[d]**. That means that if we do not pass the name of a profile at installation, by default **dnf** will install the server RPM packages for the default profile.

To get the list of RPM packages that are installed by the PostgreSQL module, type

`# dnf module info postgresql`

You can even be more specific by indicating the module name and the stream, separated by a colon:

`# dnf module info nodejs:18`

The **--profile** command option shows the RPM packages that will be installed on each profile:

`# dnf module info --profile nodejs:18`

##### Installing and Removing Module Streams

At the bottom of [Figure 4-12](#ch04.xhtml_ch4fig12), you can see that a stream or a profile can be marked as default, **[d]**, enabled, **[e**], disabled, **[x]**, or installed, **[i]**. We have already seen that “default” can refer to which profile of a module stream is installed by default, if none is specified. It can also refer to a stream if a module has more than one, or to indicate which stream will be installed if none is specified.

To install a module stream, the corresponding module stream must be enabled first. This can be done by running the **dnf module enable** command. For example, to enable the nodejs 18 stream, run

`# dnf module enable nodejs:18`

Next, install the module:

`# dnf module install nodejs`

However, the **dnf module install** command automatically enables a module, so you can replace the previous two commands with the following one:

`# dnf module install nodejs:18`

Optionally, you can specify a profile (for example, the “minimal” profile) with this syntax:

`# dnf module install nodejs:18/minimal`

Removing a module requires one command:

`# dnf module remove nodejs:18`

Next, you can “reset” the stream, which disables the stream and resets the configuration to the default settings:

`# dnf module reset nodejs`

#### CERTIFICATION SUMMARY

This chapter focuses on the management of RPM packages. With different command options, you also saw how the **rpm** tool installs, removes, and upgrade packages, as well as how it works locally and remotely. When presented with a new version of a kernel, it’s important to never replace the existing kernel with **rpm**. A properly configured installation of a later kernel version does not overwrite the existing kernel, but brings the kernels together, side by side. You’ll then be able to boot into either kernel.

With the **rpm** command, you also learned how to query packages, to examine to which package a file belongs, to validate a package signature, and to find the current list of installed RPMs. You also saw the difficulties associated with dependencies that drove users to the **dnf** command.

The **dnf** command is much more powerful than the **rpm** command. When there are dependencies, it installs those packages simultaneously. You learned how to configure Red Hat and other repositories to work with the **dnf** command. You should now be able to configure your own repositories and subscribe a system to the Red Hat Portal using the **subscription-manager** command. As you saw, the **dnf** command can also install or remove package groups.

Module streams provide a way to distribute multiple versions of the same application, and to pin to a specific release when installing it. The **dnf module** command can be used to list, install, and uninstall module streams.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 4](#ch04.xhtml).

##### The RPM Package Manager

![Images](squ1.jpg)   The RPM database tracks where each file in a package is located, its version number, and much more.

![Images](squ1.jpg)   The **rpm -i** command installs RPM packages.

![Images](squ1.jpg)   The **rpm -e** command uninstalls RPM packages.

![Images](squ1.jpg)   The **rpm** command can even install RPMs directly from remote servers.

![Images](squ1.jpg)   RPM package verification is supported by the GPG keys in the /etc/pki/rpm-gpg directory.

![Images](squ1.jpg)   Kernel RPMs should always be installed, never upgraded.

![Images](squ1.jpg)   The upgrade mode of RPM replaces the old version of the package with the new one.

##### More RPM Commands

![Images](squ1.jpg)   The **rpm -q** command determines whether packages are installed on a system; with additional switches, it can list more about a package and identify the package for a specific file.

![Images](squ1.jpg)   Package signatures can be checked with the **rpm --checksig** (or **-K**) command.

![Images](squ1.jpg)   The **rpm -V** command can identify files that have changed from the original installation of the package before the RPM is installed.

![Images](squ1.jpg)   The **rpm -qa** command lists all currently installed packages.

##### Dependencies and the dnf Command

![Images](squ1.jpg)   By including additional required packages, the **dnf** command can help avoid “dependency hell.”

![Images](squ1.jpg)   The behavior of the **dnf** command is configured in the /etc/dnf/dnf.conf file, plugins in the /etc/dnf/plugins directory, and repositories configured in the /etc/yum.repos.d directory.

![Images](squ1.jpg)   Red Hat organizes packages in two main repositories for RHEL 9, BaseOS and AppStream.

![Images](squ1.jpg)   Repositories for rebuild distributions and from third parties are accessible online.

![Images](squ1.jpg)   The **dnf** command can install, erase, and update packages. It also can be used to search in different ways.

![Images](squ1.jpg)   The **dnf** command uses GPG signatures to validate RPM packages.

![Images](squ1.jpg)   The **dnf** command can install, remove, and list package groups.

![Images](squ1.jpg)   Module streams are a way to distribute multiple versions of the same application in a single repository.

![Images](squ1.jpg)   A stream is a collection of RPM packages that are required by a specific version of an application.

#### Q SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams. There may be more than one answer to many of these questions.

##### The RPM Package Manager

**[1.](#ch04.xhtml_ch4ques1)**   What command would you use to install the penguin-3.26.x86_64.rpm package, with verbose messages in case of errors? The package is on the current directory.

**[2.](#ch04.xhtml_ch4ques2)**   What command would you use to upgrade the penguin RPM with the penguin-3.27.x86_64.rpm package? The package is on the ftp.remotemj02.abc server.

**[3.](#ch04.xhtml_ch4ques3)**   If you’ve downloaded a later version of the Linux kernel to the local directory and the package filename is kernel-5.14.0-284.11.1.el9_2.x86_64.rpm, what’s the best command to make it a part of your system?

**[4.](#ch04.xhtml_ch4ques4)**   What directory contains RPM GPG keys on an installed system?

##### More RPM Commands

**[5.](#ch04.xhtml_ch4ques5)**   What command lists all currently installed RPMs?

**[6.](#ch04.xhtml_ch4ques6)**   What command lists all the files in the package penguin-3.26.x86_64.rpm?

**[7.](#ch04.xhtml_ch4ques7)**   If you’ve downloaded from a third party an RPM called third.i686.rpm, how can you validate the associated package signature?

##### Dependencies and the dnf Command

**[8.](#ch04.xhtml_ch4ques8)**   What is the full path to the directory where **dnf** repositories are normally configured?

**[9.](#ch04.xhtml_ch4ques9)**   What command from the console starts the process of registration to Red Hat Subscription Management?

**[10.](#ch04.xhtml_ch4ques10)**   What command searches **dnf** repositories for the package associated with the /etc/passwd file?

**[11.](#ch04.xhtml_ch4ques11)**   What directive specifies a **dnf** repository URL in a .repo file?

**[12.](#ch04.xhtml_ch4ques12)**   How do you enable and install the module nodejs, stream version 18, profile development?

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for the labs follow the Self Test answers.

#### A SELF TEST ANSWERS

**The RPM Package Manager**

**[1.](#ch04.xhtml_r_ch4ques1)**   The command that installs the penguin-3.26.x86_64.rpm package, with verbose messages in case of errors, is

`# rpm -iv penguin-3.26.x86_64.rpm`

Additional switches that don’t change the functionality of the command, such as **-h** for hash marks, are acceptable. This applies to subsequent questions as well.

**[2.](#ch04.xhtml_r_ch4ques2)**   The command that upgrades the aforementioned penguin RPM with the penguin-3.27.x86_64.rpm package from the ftp.remotemj02.abc server is

`# rpm -Uv ftp://ftp.remotemj02.abc/penguin-3.27.x86_64.rpm`

**[3.](#ch04.xhtml_r_ch4ques3)**   If you’ve downloaded a later version of the Linux kernel to the local directory and the package filename is kernel-5.14.0-284.11.1.el9_2.x86_64.rpm, the best way to make it a part of your system is to install it—and not upgrade the current kernel. Kernel upgrades overwrite existing kernels. Kernel installations allow kernels to exist side by side; if the new kernel doesn’t work, you can still boot into the working kernel. As the desired package is already downloaded, you’d use a command similar to the following:

`# rpm -iv kernel-5.14.0-284.11.1.el9_2.x86_64.rpm`

Variations of the **rpm** command, such as **rpm -i** and **rpm -ivh**, are acceptable. However, variations that upgrade, with the **-U** or **-F** switch, are incorrect.

**[4.](#ch04.xhtml_r_ch4ques4)**   The directory with RPM GPG keys on an installed system is /etc/pki/rpm-gpg.

##### More RPM Commands

**[5.](#ch04.xhtml_r_ch4ques5)**   The command that lists all installed RPMs is

`# rpm -qa`

**[6.](#ch04.xhtml_r_ch4ques6)**   The command that lists all the files in the package penguin-3.26.x86_64.rpm is

`# rpm -ql penguin-3.26.x86_64.rpm`

**[7.](#ch04.xhtml_r_ch4ques7)**   If you’ve downloaded from a third party an RPM called third.i686.rpm, you’ll first need to download and install the RPM-GPG-KEY file associated with that repository. You can then validate the associated package signature with a command like the following (note the uppercase -K; --checksig is equivalent to -K):

`# rpm -K third.i386.rpm`

##### Dependencies and the dnf Command

**[8.](#ch04.xhtml_r_ch4ques8)**   The **dnf** command repositories are normally configured in files in the /etc/yum.repos.d directory. Technically, **yum** command repositories can also be configured directly in the /etc/dnf/dnf.conf file.

**[9.](#ch04.xhtml_r_ch4ques9)**   The **subscription-manager** command starts the process of registering a system to Red Hat Subscription Management.

**[10.](#ch04.xhtml_r_ch4ques10)**   The **dnf provides /etc/passwd** command identifies packages associated with that file.

**[11.](#ch04.xhtml_r_ch4ques11)**   The **baseurl** directive specifies the URL of a **dnf** repository.

**[12.](#ch04.xhtml_r_ch4ques12)**   To install the module nodejs, stream version 18, profile development, run the following command:

`# dnf module install nodejs:18/development`

Note that this command automatically enables the stream, so you do not need to run **dnf module enable** first.

#### LAB ANSWERS

##### Lab 1

**1.**   Run the following command to create a list of all the packages installed on the system and save it to the /root/pkgs.txt file:

`# rpm -qa > /root/pkgs.txt`

**2.**   To answer this question, you can count the lines of the /root/pkgs.txt file or run the following command:

`# rpm -qa | wc -l`

**3.**   To identify which package the file /etc/sestatus.conf belongs to, run

`# rpm -qf /etc/sestatus.conf`

**4.**   You should notice that zlib is already installed (**rpm -q zlib**). To find information and the list of files provided by the zlib RPM package, run

`# rpm -qil zlib`

**5.**   This question is slightly different from the previous one, in that the tmux package is not installed by default. Assuming that the RHEL 9 DVD is mounted at /run/media/*yourusername*/RHEL-9-1-0-BaseOS-x86_64, run the following commands to answer the question:

![Images](f0170-03.jpg)

##### Lab 2

Create a file named /etc/yum.repos.d/sql.repo with the following content:

![Images](f0170-04.jpg)

Run the following commands to search for and install the package:

![Images](f0170-05.jpg)

##### Lab 3

One way to check all the files in the /usr/sbin directory is to run the following command:

![Images](f0170-06.jpg)

If successful, the command should provide the following output, indicating that the timestamp of the file is different from that of the original file:

![Images](f0170-07.jpg)

To reinstall the package, type

![Images](f0170-08.jpg)

The **dnf remove openssh-server** command followed by **dnf install openssh-server** would achieve the same result.

##### Lab 4

This lab is intended to help you examine what the **dnf update** command can do. As you can see from the update.txt file created in this lab, the messages display how **dnf** searches for all newer packages from configured repositories or the Red Hat Portal, downloads their metadata, and uses them to check for dependencies that also need to be downloaded and installed.

##### Lab 5

To find information about the “Graphical Administration Tools” group, type

![Images](f0171-01.jpg)

You should find that this group consists of five optional packages.

To install the wireshark package, type

![Images](f0171-02.jpg)

**Lab 6**

First, list the existing postgresql module streams:

![Images](f0171-03.jpg)

You will find that there is one stream, version 15.

To install PostgreSQL from the 15 stream and the client profile, run

![Images](f0171-04.jpg)

Note that this command will automatically enable the stream, so it is not necessary to run **dnf module enable** first.

Finally, confirm that the stream is enabled and installed:

![Images](f0171-05.jpg)

## Chapter 5

## systemd and the Boot Process

CERTIFICATION OBJECTIVES

[5.01     The Boot Process](#ch05.xhtml_ch5obj01)

[5.02     Bootloaders and GRUB 2](#ch05.xhtml_ch5obj02)

[5.03     Between GRUB 2 and Login](#ch05.xhtml_ch5obj03)

[5.04     Control by Target](#ch05.xhtml_ch5obj04)

[5.05     Time Synchronization](#ch05.xhtml_ch5obj05)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

This chapter is focused on what happens from the moment a system is powered up to the time a login prompt is available. This is called the boot process. When the system powers on, the BIOS/UEFI firmware searches for a bootable device. Assuming this is a local hard drive, the GUID Partition Table (GPT) or Master Boot Record (MBR) of that device points to the GRUB 2 bootloader. Once an option to boot RHEL 9 is selected in GRUB 2, the bootloader loads a special file, initramfs, and gives control to the Linux kernel, which then starts **systemd**, the first Linux process. The **systemd** process then initializes the system and activates appropriate system units. When Linux boots into a specific target, it starts a series of “units,” including the SSH daemon and the service associated with the Network Time Protocol (NTP). You can customize this process.

INSIDE THE EXAM

**Understanding the Boot Process**

Objectives related to the boot process have been consolidated into the RHCSA exam. Perhaps the most basic skill related to the boot process is an understanding of the commands that start and stop the boot process, such as **systemctl poweroff** and **systemctl reboot**:

![Images](square.jpg)   Boot, reboot, and shut down a system normally

In this chapter, you’ll be introduced to systemd targets, which replace the traditional runlevels in RHEL 6 and other older Linux distributions. From the standard RHEL 9 boot menu, you need to know how to

![Images](square.jpg)   Boot systems into different targets manually

Closely related to this objective is this one:

![Images](square.jpg)   Interrupt the boot process in order to gain access to a system

You should be able to gain access to a system to recover a lost root password or to troubleshoot issues during the boot process.

Also, you must know how to automatically boot the system into different “targets,” such as nongraphical multi-user mode or a GUI desktop:

![Images](square.jpg)   Configure systems to boot into a specific target automatically

As Linux is a network operating system, and as most users can’t do much without network services, it’s important to know how to

![Images](square.jpg)   Start and stop services and configure services to start automatically at boot

You’ll also learn how to

![Images](square.jpg)   Modify the system bootloader

Closely related to these objectives, and part of the boot process, are objectives related to how filesystems are mounted, as covered in [Chapter 7](#ch07.xhtml).

**The Network Time Service**

This chapter covers the configuration of a client that syncs the time using NTP. The corresponding exam objective is

![Images](square.jpg)   Configure time service clients

### CERTIFICATION OBJECTIVE 5.01

### The Boot Process

Although not officially a Red Hat exam prerequisite or requirement, a basic understanding of the BIOS and the UEFI firmware is a fundamental skill for all serious computer users. The Unified Extensible Firmware Interface (UEFI) is a newer standard and has replaced the Basic Input/Output System (BIOS) on many modern systems. But for our purposes, their functionalities are the same.

Because of the variety of BIOS/UEFI firmware available, this discussion is general. It’s not possible to provide any sort of step-by-step instructions for modifying the wide array of available BIOS/UEFI menus. In any case, such instructions are not directly relevant either to the administration of Linux or to any of the Red Hat exams. However, these skills can help you boot from different Linux installation media, access default virtualization settings, and more.

#### Basic System Configuration

When a computer is powered up, the first thing that starts is the BIOS/UEFI firmware. Based on settings stored in stable, read-only memory, the BIOS/UEFI system performs a series of diagnostics to detect and connect the CPU and key controllers. This is known as the Power On Self Test (POST). If you hear beeps during this process, there may be a hardware problem such as an improperly connected drive controller. The BIOS/UEFI system then looks for attached devices such as the graphics card. After the graphics hardware is detected, you may see a screen similar to [Figure 5-1](#ch05.xhtml_ch5fig1), which displays other hardware as detected, tested, and verified.

FIGURE 5-1 The BIOS Initialization menu

![Images](F05-01.jpg)

If your system has a UEFI menu, it may include a Trusted Platform Module (TPM). Although TPM technology is built to enhance security on a system, it has caused controversy within the open-source community due to privacy and vendor lock-in issues. Many open-source professionals worked to minimize any such problems through the Open Trusted Computing (OpenTC) group of the European Union. RHEL 9 can take advantage of TPM hardware features to enhance system security.

Once complete, the BIOS/UEFI passes control to the boot device, typically the first drive. The first stage of the GRUB 2 bootloader is normally copied to the MBR or GPT. It serves as a pointer to the other information from the GRUB 2 menu. At that point, you should see a bootloader screen.

#### Startup Menus

Generally, one of the reasons to access the BIOS/UEFI firmware menu is to boot from different media, such as a CD or USB key. In many cases, you can bypass this process.

Sometimes, all you see after POST is a blank screen. The BIOS/UEFI is often configured in this way. In that case, you’ll need to do some guessing based on your experience on how to access the boot or BIOS menu.

In many cases, boot menus are directly accessible by pressing a key such as ESC, DEL, F1, F2, or F12. Such boot menus may have entries similar to the following:

![Images](f0176-01.jpg)

From that or similar menus, you should be able to select the desired boot device using the ARROW and ENTER keys.

#### Access to Linux Bootloaders

As noted in [Chapter 1](#ch01.xhtml), the standard Linux bootloader is GRUB 2, and the first part of it (known as stage 1) is installed in the MBR or GUID table of the default drive. Normally, the BIOS should automatically start the bootloader, with a message similar to

![Images](f0176-02.jpg)

If you press a key before those five seconds are complete, GRUB 2 will present a menu similar to that shown in [Figure 5-2](#ch05.xhtml_ch5fig2).

FIGURE 5-2 The GRUB 2 menu

![Images](F05-02.jpg)

If the system includes more than one Linux kernel, or more than one operating system, there may be multiple choices available, which you can highlight with the UP ARROW and DOWN ARROW keys. To boot Linux from the highlighted option, press ENTER.

On old PCs (pre-21st century), some BIOSes could not find your bootloader unless it was located within the first 1024 cylinders of the hard disk. For that reason, the partition where the /boot directory is configured is normally the first available primary partition.

RHEL 9 supports the traditional MBR partitioning layout and the newer GPT format. Whereas the MBR partitioning scheme supports a maximum size of 2TB per disk, GPT does not have such limitation. However, to boot RHEL from a disk with a GPT partition layout, you need a system with the UEFI firmware interface rather than a traditional BIOS firmware. You should check with your hardware vendor if UEFI is supported by your system.

### CERTIFICATION OBJECTIVE 5.02

### Bootloaders and GRUB 2

The standard bootloader associated with Red Hat Enterprise Linux is GRUB 2, the GRand Unified Bootloader version 2\. As suggested by the Red Hat exam requirements, for the RHCSA exam you need to know how to use the GRUB 2 menu to boot into different targets and diagnose and correct boot failures arising from bootloader errors. In GRUB version 1, which was the default in RHEL 6, the associated configuration file was relatively easy to understand and customize. However, although the GRUB 2 menu is similar to what’s seen on RHEL 6, the steps required to configure that bootloader are quite different, as you’ll see later in this chapter.

#### GRUB, the GRand Unified Bootloader

Red Hat has implemented GRUB 2 as the only bootloader for its Linux distributions. It’s normally configured to boot into a configured default kernel. GRUB 2 finds the configuration in the /boot directory and displays a menu, which will look similar to [Figure 5-2](#ch05.xhtml_ch5fig2). You can use the GRUB 2 menu to boot any operating system detected during the Linux installation process, or any other operating system added to appropriate configuration files.

GRUB 2 is flexible. Not only can the configuration be easily generated from the CLI, but also it can be edited directly from the GRUB 2 menu. From the menu shown in [Figure 5-2](#ch05.xhtml_ch5fig2), you can press E to temporarily edit the selected item, or press C to open a GRUB 2 command prompt. This section is focused on booting into different systemd targets.

##### Boot into an Emergency Shell

To pass a parameter to the kernel through GRUB 2, press E at the first GRUB 2 menu. This allows you to edit the boot parameters sent to the kernel. Locate the line that starts with the directive **linux**. Scroll down with the DOWN ARROW key if necessary. You might then see a configuration line similar to the following:

![Images](f0178-01.jpg)

Yeah, that’s a lot of stuff, which will be explained later in this chapter. What matters for the RHCSA exam is that you understand how to add more kernel parameters to the end of this line. For example, if you add the string **systemd.unit=emergency.target** to the end of this line and press CTRL-X, Linux starts in a mode of operation called *emergency target*, which runs a rescue shell.

From the emergency target, type the root password and then type **exit**. The system will go into the default target, which normally is either the multi-user target or the graphical target. If you have made changes or repairs to any partitions, the next step is to reboot the computer with the **systemctl reboot** command. At some point during a Red Hat exam, you should test the changes that you’ve made with a reboot.

![Images](job.jpg)

**On RHEL 9, the** shutdown, reboot, **and** halt **commands are symbolic links to** systemctl. **They have the same effect as the** systemctl poweroff, systemctl reboot, **and** systemctl halt **commands, respectively.**

![Images](exam.jpg)

**Changes must survive a reboot during the RHCSA exam, so you’ll want to restart your system at least once to verify each of the requirements is met even after a reboot.**

To a certain extent, the concept of the systemd targets is similar to that of runlevels in older Linux distributions and is detailed later in this chapter. For now, all you need to know is that when RHEL 9 is configured to boot into a GUI, it’s configured to boot into the graphical target by default. That target can be changed by appending a **systemd.unit=*name*.target** string to the end of the kernel command line.

If you need direct access into a recovery shell, add the string **systemd.unit=rescue.target** to the end of the kernel command line. In rare cases, some systems are so troubled, they don’t boot into the rescue target. In that case, you can boot the system into the emergency target by appending the string **systemd.unit=emergency.target** to the kernel command line. The difference between rescue and emergency targets is that the former mounts the filesystems in read-write mode, while the latter does not mount any filesystems, apart from the root filesystem in read-only mode.

The emergency and rescue targets require the root password to log in and get full root administrative privileges. If you have lost the root password, you will need to add the string **rd.break** to the end of the kernel command line and follow the procedure illustrated later in Exercise 5-2\. As that supports full administrative privileges, including changes to the root administrative password, you may want to password-protect the GRUB 2 menu. Somebody who can change the boot order can achieve the same thing with a bootable USB drive, so it is also important to protect your BIOS or UEFI firmware to ensure the system only boots the local disk without a password. However, this is out of the scope of the RHCSA exam.

Now you should understand how to boot into different targets during the boot process. [Table 5-1](#ch05.xhtml_ch5tab1) summarizes the boot options described so far.

TABLE 5-1 How to Start an Emergency Shell

![Images](f0179-01.jpg)

![Images](exam.jpg)

**Red Hat exams are “closed book.” Although you are allowed to use all documentation that can be found on your RHEL installation, during recovery or emergency procedures you may not have access to man pages or other documentation resources. Therefore, it is extremely important that you practice the exercises in this chapter without the help of any documentation. You should memorize the steps to boot into an emergency shell or to recover a root password; otherwise, you may be in trouble, not just during the RHCSA exam, but also in real life when performing your job duties as a Linux sysadmin.**

EXERCISE 5-1

**Boot into a Different Target**

One key skill is knowing how to boot into a different systemd target. This exercise assumes you’ve configured RHEL 9 per [Chapter 1](#ch01.xhtml), which sets the graphical target as the default. Run the **ls -l /etc/systemd/system/default.target** command to verify. If the current system reflects the defaults, this file should be a symbolic link to the graphical.target file within the directory /usr/lib/systemd/system. As an alternative, run the following command:

`# systemctl get-default`

It should return the string “graphical.target.” Now you can start the exercise.

1.   Reboot your system using the **reboot** command.

2.   When you see the following message, make sure to press any key to access the GRUB 2 menu:

`The selected entry will be started automatically in 5s.`

3.   Press E to edit the current menu entry.

4.   Scroll down with the DOWN ARROW key to locate the line starting with **linux**. First, delete the kernel options **rhgb quiet**. Then, at the end of the line, type **systemd.unit=multi-user.target** and press CTRL-X to boot this kernel.

5.   Watch the boot messages. What kind of login screen do you see?

6.   Log in to this system. You can use any existing user account.

7.   Run the **reboot** command to restart this system.

8.   Repeat Steps 2 through 4, but boot this system into the rescue target by passing the option **systemd.unit=rescue.target** to the kernel.

9.   Watch the boot messages. What kind of login screen do you see? Which filesystems are mounted?

10.   Repeat Steps 2 through 4, but boot this system into the emergency target by passing the option **systemd.unit=emergency.target** to the kernel.

11.   Watch the boot messages. What kind of login screen do you see? Do you have to log in at all? Which filesystems are mounted?

12.   Repeat Steps 2 through 4, but this time append **rd.break** to the kernel command line.

13.   Watch the boot messages. What kind of login screen do you see? Do you have to log in at all? Is the root filesystem mounted from the hard drive?

14.   Type **reboot** to log out and restart the system.

EXERCISE 5-2

**Recover the Root Password**

If you boot a RHEL 9 system into the rescue or emergency target, you are prompted for the root password. But what if you have forgotten the password? This exercise shows the steps required to reset a lost password for the root user. During the password-recovery process, you probably won’t have access to documentation. Hence, you should practice the following procedure until you are fully prepared to use it in a crisis:

1.   Use the following command to change the root password to a random string. This command hides the random password from you:

`# openssl rand -base64 15 | passwd --stdin root`

2.   Log out from your session. Try to log in again as the root user. You shouldn’t be able to log in to the system with the old known root password.

3.   Reboot the server.

4.   When you see the following message, press a key to access the GRUB 2 menu:

`The selected entry will be started automatically in 5s.`

5.   Press E to edit the current menu entry.

6.   Scroll down with the DOWN ARROW key to locate the line starting with **linux**. Press CTRL-E or END to move to the end of the line, and then type the string **rd.break**.

7.   Press CTRL-X to boot the system.

8.   The **rd.break** directive interrupts the boot sequence before the root filesystem is properly mounted. Confirm this by running **ls /sysroot**. If you know the contents of the root filesystem, the output should look familiar.

9.   Remount the root /sysroot filesystem as read-write and change the root directory to /sysroot (you will learn more about the **mount** command in [Chapter 7](#ch07.xhtml)):

![Images](f0182-01.jpg)

10.   Change the root password:

`# passwd`

11.   Because SELinux is not running, the **passwd** command does not preserve the context of the /etc/passwd file. To ensure that the /etc/passwd file is labeled with the correct SELinux context, instruct Linux to relabel all files at the next boot with the following command:

`# touch /.autorelabel`

12.   Type **exit** to close the chroot jail, and then type **exit** again to reboot the system.

13.   It may take a few minutes for SELinux to relabel all files. Once you get a login prompt, confirm that you are able to log in as the root user.

#### Modify the System Bootloader

The RHCSA specifically requires that you need to know how to “modify the system bootloader.” That means you need to know how to configure GRUB 2 in detail. The configuration is available in the file /etc/grub2.cfg, which is a symbolic link that points to /boot/grub2/grub.cfg on systems configured in BIOS mode, or /boot/efi/EFI/redhat/grub.cfg for servers that use an UEFI boot manager. See [Figure 5-3](#ch05.xhtml_ch5fig3) to see an excerpt of the grub.cfg file. In the rest of this chapter, we will assume that you run a traditional BIOS-based system or a UEFI-capable system in BIOS mode. We’ll refer to /boot/grub2/grub.cfg as the standard path of the configuration file.

FIGURE 5-3 An excerpt of the grub.cfg file

![Images](F05-03.jpg)

Although the number of options and directives in the grub.cfg file may seem overwhelming, don’t panic. You never need to touch this file directly. The right approach is to generate a new version of this file with the **grub2-mkconfig** tool, based on the /etc/default/grub configuration file and on the scripts in the /etc/grub.d/ directory. The /etc/default/grub file is much simpler to understand, safer, and more convenient to edit than grub.cfg. Once you have made a modification to /etc/default/grub, generate the new GRUB configuration file by running

![Images](f0183-02.jpg)

![Images](job.jpg)

**Do not manually edit the /boot/grub2/grub.cfg file. Use** grub2-mkconfig **and the /etc/default/grub file to make modifications to grub.cfg.**

The following is a detailed analysis of a typical version of the /etc/default/grub file:

![Images](f0183-03.jpg)

In the first line, the GRUB_TIMEOUT variable specifies the time in seconds before GRUB 2 automatically boots the default operating system. You can interrupt the countdown by pressing any key on the keyboard. If this variable is set to 0, GRUB 2 will not display a list of bootable kernels, unless you press and hold an alphanumeric key during the BIOS initial screen.

The value of the GRUB_DISTRIBUTOR variable returns “Red Hat Enterprise Linux” on a standard RHEL installation, and is displayed before each kernel-bootable entry. You can modify this entry to any string of your choice if you wish.

The next variable is GRUB_DEFAULT and is related to the default kernel that GRUB 2 loads at boot. The value “saved” instructs GRUB 2 to look at the saved_entry variable in the file /boot/grub2/grubenv. This variable is updated with the name of the latest kernel every time that a new kernel is installed.

You can update the saved_entry variable and instruct GRUB 2 to boot a different default kernel via the **grub2-set-default** command. As an example,

`# grub2-set-default 1`

sets the second menu entry as the default kernel. This may be slightly confusing because GRUB 2 starts counting from 0\. Hence, **grub2-set-default 0** points to the first available menu. Similarly, the command **grub2-set-default 1** points to the second kernel entry, and so on.

The next configuration line in /etc/default/grub defines the variable GRUB_DISABLE_SUBMENU. This is set to “true” by default to disable any submenu entries at boot. Then follows the variable GRUB_TERMINAL_OUTPUT, which tells GRUB 2 to use a text console as the default output terminal. The last two variables defined in the file are GRUB_DISABLE_RECOVERY, which disables the generation of recovery menu entries, and GRUB_ENABLE_BLSCFG, which tells GRUB 2 to use a special file format, the Boot Loader Specification (BLS).

The variable GRUB_CMDLINE_LINUX is more interesting. It specifies the options to pass to the Linux kernel. For example, **rd.lvm.lv** tells the name of the logical volumes where the root filesystem and swap partition are located. The **crashkernel** option is used to reserve some memory for **kdump**, which is invoked to capture a kernel core dump if the system crashes. Finally, at the end of the line, the **rhgb quiet** directives enable the Red Hat graphical boot and hide the boot messages by default. If you want to enable verbose boot messages, remove the **quiet** option from this line.

#### How to Update GRUB 2

If you need to reinstall the GRUB 2 bootloader, just run the **grub2-install** command. If it doesn’t automatically write the GRUB 2 pointer to the MBR, or if multiple hard drives are available, you may need to include the hard drive device, such as /dev/vda. It’s also possible to set up GRUB 2 on a portable drive; just specify the device with the command.

When the GRUB 2 configuration file is generated using **grub2-mkconfig**, no additional commands are required. The pointer from the MBR automatically reads the current version of the /boot/grub2/grub.cfg file.

#### The GRUB 2 Command Line

An error in grub.cfg can result in an unbootable system. For example, if GRUB 2 identifies the wrong volume as the root partition (/), Linux will hang during the boot process. Other configuration errors in /boot/grub2/grub.cfg can lead to a kernel panic during the boot process.

Now that you’ve analyzed the GRUB 2 configuration file, you can probably visualize some of the effects of errors in this file. If some of the filenames or partitions are wrong, GRUB 2 won’t be able to find critical files such as the Linux kernel. If the GRUB 2 configuration file is completely missing, you’ll see a prompt similar to this:

`grub>`

You can access a GRUB 2 command line by pressing the C key when the menu is displayed. To see a list of available commands, press the TAB key at the grub> prompt, or type the **help** command.

Command completion is also available. For example, if you don’t remember the name of the kernel file, type **linux /** and then press the TAB key to review the available files in the /boot directory.

You should be able to find all detected hard drives on a standard PC from the BIOS/UEFI menus with the **ls** command. As an example, let’s find the /boot partition and grub.cfg file on this particular system. By default, the /boot directory is mounted on a separate partition. First, run **ls** at the grub> command line:

![Images](f0185-02.jpg)

The string **hd0** denotes the first hard drive, whereas **msdos1** is the first partition, created with the MBR format (msdos). If a server was partitioned using the newer GPT partition format, GRUB 2 would identify the first partition as **gpt1** rather than **msdos1**. Similarly, **hd0,msdos2** denotes the second partition on the first hard drive.

Next, use that information to find the grub.cfg file:

![Images](f0185-03.jpg)

If the file is not on the noted partition, you’ll see an “error: file ‘/grub2/grub.cfg’ not found” error message. You may also see “error: unknown filesystem” if the noted partition does not contain a valid filesystem.

We know that the /boot directory is on **(hd0,msdos1)**. To confirm the location of grub.cfg, run the following command:

![Images](f0185-04.jpg)

You should see the contents of the grub.cfg file in the output. Press a key to scroll through the content of the file until you are back to the GRUB 2 command line.

There’s one more way to identify the partition with the /boot directory. Run the **search.file** command to find grub.cfg:

![Images](f0186-01.jpg)

GRUB 2 should return the partition with the /boot directory. In this case, it’s the first partition on the first hard drive:

![Images](f0186-02.jpg)

Now you can use these commands from the GRUB 2 configuration file to boot Linux from the grub> prompt. If the top-level root filesystem is located on a partition, you may even confirm the contents of the /etc/fstab file with a command like the following:

![Images](f0186-03.jpg)

If the root filesystem resides on an LVM volume, the preceding command might return an “error: unknown filesystem” message. If you encounter this problem, load the LVM module using the following command:

![Images](f0186-04.jpg)

Now, the **ls** command should also include logical volumes in its output:

![Images](f0186-05.jpg)

Finally, to print the content of /etc/fstab, run the following command:

![Images](f0186-06.jpg)

EXERCISE 5-3

**Using the GRUB 2 Command Line**

In this exercise, you’ll boot RHEL 9 manually. Follow these steps:

1.   Boot the system. When you see the following line at the top of the screen, press any key to access the GRUB 2 menu:

`The selected entry will be started automatically in 5s.`

2.   Press c for a GRUB-based command-line interface. You should see the grub> prompt.

3.   Load the LVM module:

`grub> insmod lvm`

4.   List all partitions and logical volumes:

`grub> ls`

5.   Identify the root partition. This may be named something like “lvm/rhel-root.” You may need to use some trial and error to find out (for example, by trying to display the /etc/fstab file from all the device names previously listed by GRUB 2).

`grub> cat (lvm/rhel-root)/etc/fstab`

6.   Set the root variable to the device that you have identified as that containing the root filesystem:

`grub> set root=(lvm/rhel-root)`

7.   Enter the **linux** command, which specifies the kernel and root directory partition. Yes, this is a long line; however, you can use command completion (press the TAB key) to make it faster. In addition, the only important parts of the line are the kernel file and the location of the top-level root directory.

![Images](f0187-04.jpg)

8.   Enter the **initrd** command, which specifies the initial RAM disk command and file location. Again, you can use the TAB key for filename completion.

![Images](f0187-05.jpg)

9.   Now enter the **boot** command. If this command is successful, Linux should now boot the selected kernel and initial RAM disk just as if you selected that option from the GRUB 2 configuration menu.

#### An Option for Booting from GRUB 2: Rescue Mode

The troubleshooting objectives associated with a previous version of the RHCSA exam prep guide suggested that you needed to be able to recover from a complete boot failure, such as if the GRUB 2 configuration file were corrupt or missing. In other words, if you’ve tried to boot directly from the grub> prompt described earlier and failed, you might need to resort to the option known as rescue mode. That requires access to the installation DVD or the network boot disk.

![Images](exam.jpg)

**The RHCSA objectives no longer include a requirement associated with rescue mode. However, because the rescue of unbootable systems is an important skill, it may be included in future versions of the exam.**

To that end, boot from one of those media options. You should see the installation screen with the following options:

![Images](f0188-01.jpg)

Select the Troubleshooting option and press uenter. You will see a second screen with the following options:

![Images](f0188-02.jpg)

Select the Rescue a Red Hat Enterprise Linux system option and press ENTER. Rescue mode runs a stable minimal version of the RHEL 9 operating system on the local machine. It’s in essence a text-only version of the “Live DVD” media available on other Linux distributions such as Knoppix or Ubuntu distributions.

![Images](job.jpg)

**For RHEL 9, it’s best to use RHEL 9 rescue media. Such media uses a kernel compiled by Red Hat, customized for supported hardware. Nevertheless, options such as Knoppix are also good.**

You can use the rescue environment to recover unbootable systems. In most cases, the next step you see is shown in [Figure 5-4](#ch05.xhtml_ch5fig4).

FIGURE 5-4 Options for the rescue environment

![Images](F05-04.jpg)

The *Continue* option, as shown in [Figure 5-5](#ch05.xhtml_ch5fig5), mounts all detected volumes as subdirectories of the /mnt/sysroot directory. The *Read-Only Mount* option mounts detected volumes in read-only mode. The *Skip to Shell* option moves straight to a command-line interface. Select Continue. After confirmation, you’ll be presented with a shell prompt.

FIGURE 5-5 Mounting the root filesystem in the rescue environment

![Images](F05-05.jpg)

From the shell prompt, enter the **chroot /mnt/sysroot** command. As the regular top-level root directory for the system is mounted on the /mnt/sysroot directory, the **chroot** command changes the root directory, as if the /mnt/sysroot filesystem was mounted under /.

Do practice what you’ve learned about GRUB 2 in this section. It could help you recover from a real-world problem—and Red Hat does say that their exams are filled with “real-world tasks.” However, don’t assume that you have access to a CD or a DVD during a Red Hat exam. If a rescue media is not available, that should mean that there’s at least one alternative method you can use to address the problem.

### CERTIFICATION OBJECTIVE 5.03

### Between GRUB 2 and Login

This section provides a basic overview of the boot process after the GRUB 2 bootloader finds the kernel. If you understand this process, you can diagnose a wide variety of boot problems. The messages associated with the kernel provide a step-by-step view of the process.

The loading of Linux depends on a temporary filesystem, known as the initial RAM disk. Once the boot process is complete, control is given to systemd, known as the first process. This section will describe the contents of systemd in detail, through the configuration of units and targets.

![Images](job.jpg)

**Most Linux distributions, including RHEL 9, have replaced Upstart and SysVinit with the systemd service manager.**

In this section, you’ll also review the commands that allow you to reboot and shut down a system normally.

![Images](job.jpg)

**In systemd, the Unix philosophy that “everything is a file” can be paraphrased as “everything is a unit.” Units are the basic building blocks of systemd.**

#### Kernels and the Initial RAM Disk

After you select a kernel from the GRUB 2 configuration menu, Linux hands over boot responsibilities to the kernel with the help of the initial RAM disk, also known by its filename in the /boot directory, initramfs. As suggested by its name, it is actually a filesystem, but it is saved in a file rather than on a disk partition.

During the boot process, Linux loads that temporary filesystem into your RAM. Linux then loads hardware drivers and starts the first process, **systemd**.

Next, **systemd** activates all the system units for the initrd.target and mounts the root filesystem under /sysroot. Finally, **systemd** restarts itself in the new root directory and activates all units for the default target (we will look in more detail at units and targets in the next section).

To learn more, disable the **quiet** directive for the desired kernel in the GRUB configuration file. Boot your system. Watch as the messages pass quickly through the screen. After logging in, you can review these messages by running the **dmesg** command.

You can find more log information in the systemd journal. Display its contents with the **journalctl** command. What you see depends on the hardware and configuration of the local system. Key messages include the following:

![Images](square.jpg)   The version of the kernel

![Images](square.jpg)   SELinux status, if active. By default, SELinux first starts in permissive mode, until the configured policy (enforcing) is loaded near the end of the boot process.

![Images](square.jpg)   The amount of recognized RAM (which does not necessarily match the actual amount of installed RAM)

![Images](square.jpg)   CPUs

![Images](square.jpg)   Kernel command line, specifying the logical volume or root filesystem

![Images](square.jpg)   Freeing of memory associated with the initial RAM disk (initramfs)

![Images](square.jpg)   Hard drives and partitions (as defined by their device filenames, such as /dev/sda or /dev/vda1)

![Images](square.jpg)   Active filesystems

![Images](square.jpg)   Swap partitions

The log file is filled with excellent information. If the system is loading the wrong kernel, you’ll see evidence of that here. If Linux isn’t using a partition that you’ve configured, you’ll also see it here (indirectly). If SELinux isn’t loading properly, you’ll see it in messages toward the end of the file.

![Images](exam.jpg)

**Remember that the Red Hat exams are not hardware exams. If you identify a problem with a key hardware component, such as a network card (which cannot be solved by some Linux command), inform your instructor/exam proctor. Don’t be surprised, however, if she responds that it’s not a hardware problem.**

#### The First Process, Targets, and Units

The Linux kernel continues the boot process by calling the first process, **systemd**. In RHEL 9, the legacy **init** process is configured with a symbolic link to **systemd**.

Units are the basic building blocks of systemd. The most common are *service units*, which have a **.service** extension and activate a system service. To show a list of all service units, type the following command:

`# systemctl list-units --type=service --all`

The **--all** flag includes all units, not just the active ones. There are other types of units, such as mount and automount units, which manage mount points; path units, which activate a service when there is a change on a filesystem path (such as a spool directory); socket units, which start a service only when a client connection is made (if you have used the **xinetd** daemon, this is similar to how **xinetd** starts services on demand); and many, many more.

A special type of unit is a *target unit*, which is used to group together other system units and to transition the system into a different state. To list all target units, type the following command:

`# systemctl list-units --type=target --all`

The most important target units are described in [Table 5-2](#ch05.xhtml_ch5tab2).

TABLE 5-2 The systemd Target Units

![Images](f0191-03.jpg)

In systemd, targets serve the same function as runlevels in previous RHEL distributions. In RHEL 6, seven runlevels, 0 through 6, were available. Linux services were organized by runlevel. Each runlevel was associated with a level of functionality.

For example, in runlevel 1, only one user was allowed to log in to that Linux system. X11 mode, also known as runlevel 5, was used to start Linux with a GUI login screen, if appropriate packages were installed. [Table 5-3](#ch05.xhtml_ch5tab3) compares systemd targets and the runlevels defined in RHEL 6.

TABLE 5-3 RHEL 6 Runlevels and RHEL 9 systemd Targets

![Images](f0192-01.jpg)

Run the following command:

![Images](f0192-02.jpg)

Note the symbolic links in the output. See how files such as runlevel0.target, runlevel1.target, and so on are linked to systemd targets such as poweroff.target and rescue.target? These links provide backward compatibility with the old SysV runlevels. You can even refer to graphical.target as runlevel5.target and multi-user.target as runlevel3.target.

Targets are controlled by units, organized in unit files. Although the default target is defined in /etc/systemd/system, you can override the default during the boot process from the GRUB 2 menu.

Each target may be associated with several systemd units. Each unit can start or stop Linux services such as printing (**cupsd**), scheduling (**crond**), the Apache web server (**httpd**), the Samba file server (**smbd**), and more. When configured, the boot process starts and stops the systemd units of your choice. These units are known as dependencies. To list all dependencies of the default graphical.target unit, run the following command:

![Images](f0192-03.jpg)

The default target is specified as a symbolic link from the /etc/systemd/system/default.target file to either multi-user.target or graphical.target. You can also use the **systemctl** command to retrieve the current default target or to change the current settings, as shown here:

![Images](f0192-04.jpg)

As you can see from this output, the **systemctl set-default multi-user.target** command creates a symbolic link named /etc/systemd/system/default.target, which points to the corresponding multi-user.target configuration file.

#### Switch Between Targets

Now that you’ve examined the different targets available on RHEL 9, it’s time to explore how to switch between targets. On earlier versions of RHEL, this is functionally equivalent to switching runlevels. First, establish the default target with the following command:

![Images](f0193-01.jpg)

RHEL 9 normally boots to either graphical.target or multi-user.target. After logging in as the administrative user, you can move to a different target with the **systemctl isolate** command. For example, the following command moves the system to the multi-user target:

![Images](f0193-02.jpg)

After that command is complete, rerun the **systemctl get-default** command. The output confirms that the default target has not changed:

![Images](f0193-03.jpg)

Now try something else. What do you think happens when the following command is executed?

![Images](f0193-04.jpg)

#### Reboot and Shut Down a System Normally

The commands required to reboot and shut down a system are straightforward. As just suggested in the previous section, the following commands provide one way to shut down and reboot a system, respectively:

![Images](f0193-05.jpg)

For legacy purposes, Red Hat has created symbolic links from the following commands to **systemctl**. These commands work just as they did in earlier versions of RHEL.

![Images](f0193-06.jpg)

#### systemd Replaces Upstart and SysVinit

The **systemd** process is the first process started at boot. It takes charge of activating all services. It replaces the traditional **init** daemon and the Upstart system, which is also a substitute for **init** and was the default **init** daemon on RHEL 6\. The design and philosophy of Upstart are very similar to the old SysVinit system, which relies on init scripts to activate services, and on the concept of runlevels, which was introduced in the previous sections.

In contrast, systemd introduces a lot of new tools and can do much more, while maintaining compatibility with SysVinit. The design of systemd is based on optimal efficiency. First, at boot, systemd activates only the services that are strictly required, whereas others are started on demand. As an example, systemd starts the CUPS printing service only when a print job is sent to the /var/spool/cups queue. In addition, systemd parallelizes the initialization of services.

As a result, the boot process under systemd is faster. To display the time required to boot your system, run the following command:

![Images](f0194-01.jpg)

This output shows the time required to initialize the kernel, plus the time to load the initial RAM disk (initrd) and the time to activate systemd units (userspace). The total time is 5.332 seconds. But there’s more. You can display a detailed account of the time required to activate each systemd unit by running **systemd-analyze blame**. An example is shown in [Figure 5-6](#ch05.xhtml_ch5fig6).

FIGURE 5-6 Initialization time of systemd units

![Images](F05-06.jpg)

The numbers in [Figure 5-6](#ch05.xhtml_ch5fig6) don’t equal the total userspace time reported by **systemd-analyze time**. That happens because systemd starts multiple services simultaneously.

But there’s even more. Although an in-depth knowledge of all the features of systemd is outside of the scope of the RHCSA exam, systems administrators can take advantage of some of its capabilities.

Some Linux developers have argued that systemd does too much and breaks the Unix philosophy of writing programs that “do one thing and do it well.” However, as of today, systemd has been adopted by most of the major Linux distributions.

##### Logging

The **systemd** process includes a powerful logging system. You can display all collected logs with the **journalctl** command. By default, the journal log files are temporarily stored in RAM in a ring buffer in the /run/log/journal directory. To get Linux to write journal log files persistently on disk, run the following commands:

![Images](f0195-01.jpg)

Once persistent logging is enabled, you can show log messages from a specific boot with the **-b** switch: **journalctl -b 0** displays the log messages since the last boot, **journalctl -b 1** from the boot before the last one, and so on. You don’t have to switch through different log files because **journactl** automatically aggregates available data from the current and all rotated log files.

You can also filter log messages based on their priority using the **-p** command option. As an example, **journalctl -p warning** displays all messages with a priority level of “warning” or higher. Log messages of a “warning” priority level are displayed in yellow, whereas messages with priority levels of “err” and higher are shown in red.

##### Control Groups

Control groups (or cgroups) are a feature of the Linux kernel to group processes together and control or limit their resource usage (such as CPU, memory, and so on). In systemd, cgroups are primarily used to track processes and to ensure that all processes that belong to a service are terminated when a service is stopped.

Under the traditional SysVinit system, it is difficult to identify the service associated with a process. In fact, services often start multiple processes. When you stop a SysVinit service, that service may not be able to terminate all dependent (child) processes. You’re stuck with either stopping all dependent processes manually (with the **ps** and **kill** commands) or accepting a system with orphaned processes in an unknown state until the next reboot.

To address this limitation, systemd labels processes associated with a service using cgroups. In this way, systemd uses cgroups to kill all processes in a group, if required.

The command **systemd-cgls** displays the cgroup hierarchy in a tree format, as shown in [Figure 5-7](#ch05.xhtml_ch5fig7). From the excerpt in [Figure 5-7](#ch05.xhtml_ch5fig7), you can identify cgroups such as Network Manager and rsyslog.service, along with the processes they have spawned. Note the one-to-one correspondence between cgroups and systemd service units.

FIGURE 5-7 The cgroup hierarchy

![Images](F05-07.jpg)

##### Dependencies

The traditional SysVinit system starts services sequentially. In contrast, systemd can activate services in parallel by keeping track of all dependencies between units. The **systemctl list-dependencies** command displays a tree with all dependencies between units.

You can show the dependencies for any available unit. Dependent units must be started first. For example, the following command shows the units that must be started before the **rsyslog** service:

`# systemctl list-dependencies rsyslog.service`

An excerpt of the command output is shown in [Figure 5-8](#ch05.xhtml_ch5fig8).

FIGURE 5-8 Dependencies between systemd units

![Images](F05-08.jpg)

#### systemd Units

The **systemd** process uses various configuration files to start other processes. You can find these configuration files in the following directories: /etc/systemd/system and /usr/lib/systemd/system.

The default configuration files are stored in /usr/lib/systemd/system. Custom files, stored in /etc/systemd/system, supersede these files. Don’t change files in the /usr/lib/systemd/system directory. Any software updates may overwrite those files.

We have already discussed *service* and *target* units, but there are more. [Table 5-4](#ch05.xhtml_ch5tab4) gives a brief description of all available unit types.

TABLE 5-4 The systemd Unit Types

![Images](f0198-01.jpg)

Examine the contents of the /usr/lib/systemd/system directory. Each file contains the configuration of a systemd unit whose type matches the filename extension. As an example, the file graphical.target defines the configuration for the graphical login target unit, whereas the file rsyslog.service includes the configuration for the rsyslog service unit.

You can list all active systemd units using the following command:

`# systemctl list-units`

The **list-units** keyword is optional because it is the default. If you want to include inactive, maintenance, and failed units, add the **--all** command switch. An excerpt of the output of the command is shown in [Figure 5-9](#ch05.xhtml_ch5fig9).

FIGURE 5-9 systemd units

![Images](F05-09.jpg)

The first column lists the unit name, while the second column (not shown in [Figure 5-9](#ch05.xhtml_ch5fig9)) tells whether or not the unit was properly loaded. The third column displays the state of the unit: active, inactive, failed, or maintenance. The next column includes more detail. Finally, the last column shows a brief description of the unit.

Whereas the **systemctl list-units** command gives a run-time snapshot of the state of each unit, the following command shows whether a unit is enabled or disabled at startup:

`# systemctl list-unit-files`

An example of the output is shown in [Figure 5-10](#ch05.xhtml_ch5fig10). As you can see, units can be “enabled” or “disabled.” There is also another state, named “static,” which means that a unit is enabled and it cannot be manually disabled.

FIGURE 5-10 Installed unit files

![Images](F05-10.jpg)

#### Virtual Consoles and Login Screens

The login terminals in Linux are virtual terminals. Most Linux systems, including RHEL 9, are configured with six standard command-line virtual terminals. These consoles are numbered from 1 to 6\. When configured with a GUI and a login manager, RHEL 9 substitutes the graphical login screen for the first and second virtual consoles.

What does that all mean? In Linux, you can switch between virtual consoles with an ALT-function key combination. For example, ALT-F2 brings you to the second virtual console. You can switch between adjacent virtual terminals by pressing ALT-RIGHT ARROW or ALT-LEFT ARROW. For example, to move from virtual console 2 to 3, press ALT-RIGHT ARROW. If you’re in a GUI, add the CTRL key. So in RHEL 9, if the GUI is installed, you’d press CTRL-ALT-F3 to get to the third virtual console.

When you log in to a regular virtual console, Linux returns a command-line shell. The default shell for a user is defined in the /etc/passwd file described in [Chapter 6](#ch06.xhtml). When you log in to a GUI, Linux returns the configured GUI desktop.

### CERTIFICATION OBJECTIVE 5.04

### Control by Target

With systemd, Red Hat Enterprise Linux service management is customized by target. Since systemd includes links to runlevels for backward compatibility with SysVinit, you can still refer to the runlevels listed in [Table 5-3](#ch05.xhtml_ch5tab3) with commands such as **init** and **telinit**. However, you should get familiar with targets because this is the standard method of activating services at boot.

Linux is highly customizable. Therefore, it makes sense that the systemd units that start in each target can be customized. Although GUI tools are available to customize systemd units, configuring them from the command-line interface is generally a lot faster.

#### Functionality by Target

As described earlier, the basic functionality of each target is listed in the configuration files in the directories /etc/systemd/systemd and /usr/lib/systemd/system. For example, let’s start with the default target, which in a RHEL 9 system with graphical login is

![Images](f0200-01.jpg)

The system knows that graphical.target is the default thanks to a symbolic link from the /etc/systemd/system/default.target file to the graphical.target file in /usr/lib/system/system. Take a look at one of those files. An excerpt is shown here:

![Images](f0200-02.jpg)

![Images](job.jpg)

**You may also use the** systemctl cat *unitname* **command to display the content of a system unit file.**

This means that a target can include another target. In this case, graphical.target is a superset of multi-user.target. After all systemd units in multi-user.target have started, graphical.target activates display-manager.service, as indicated by the Wants directive in the graphical.target configuration file.

Other services started by graphical.target may be listed in the graphical.target.wants subdirectory in /etc/systemd/system or /usr/lib/systemd/system. In a default RHEL 9 installation, we see the following file:

![Images](f0201-01.jpg)

#### The Innards of systemd Units

The systemd units are activated whenever a system moves to a different target. Therefore, the units associated with the default target are executed during the boot process. Appropriate units are also started when you change targets; for example, when you run the **systemctl isolate multi-user.target** command from the graphical.target, Linux stops all service units that were started by the graphical target.

But you can control systemd units directly. For example, examine the content of the file rsyslog.service from the /usr/lib/systemd/system directory, as shown in [Figure 5-11](#ch05.xhtml_ch5fig11).

FIGURE 5-11 The configuration file of the rsyslog service unit

![Images](F05-11.jpg)

The configuration starts with the Unit section, which contains a description of the service. Then comes the service configuration, which includes the type of the service, a pointer to a file with some environment variables that configure the service behavior, the main executable to run to activate the service, and a directive that sends all standard output from the service to /dev/null.

Finally, the WantedBy directive tells us that this service will be activated at boot when the system enters into the multi-user target.

Now, run the following command:

`# systemctl status rsyslog.service`

If you specify a unit name without an extension, by default systemd assumes that it is a service unit. Hence, a short version of the previous command is

`# systemctl status rsyslog`

This command should return an output similar to that shown in [Figure 5-12](#ch05.xhtml_ch5fig12), including the status of the service unit, its main process ID, and up to the 10 most recent log lines. If some of the log lines are truncated, use the **-l** switch to display them in full.

FIGURE 5-12 Displaying the status of a service

![Images](F05-12.jpg)

You can stop a service by running a command such as this:

`# systemctl stop rsyslog.service`

Alternatively, the **systemctl** command can be used with the options shown in [Table 5-5](#ch05.xhtml_ch5tab5); for example, the following command reloads the SSH configuration file without stopping or starting the service:

TABLE 5-5 systemctl Service Control Commands

![Images](f0203-01.jpg)

`# systemctl reload sshd.service`

#### Service Configuration

The **systemctl** command gives you a simple way to enable a service for the default target. First, try the following command:

![Images](f0203-02.jpg)

This gives an output similar to [Figure 5-10](#ch05.xhtml_ch5fig10), but limited to service units. You’ll see the whole list of installed services in the system, along with their activation status at boot.

The **systemctl** command can do more. With that command, you can change the boot state of a particular service. For example, in a system with the Postfix e-mail server installed, the following command checks if the Postfix service is configured to start at boot:

![Images](f0203-03.jpg)

An equivalent command is

![Images](f0203-04.jpg)

This indicates that the Postfix e-mail server is configured to start in the default target. If you want to make sure the Postfix service does not start in the default target, execute the following command:

![Images](f0203-05.jpg)

Run the **systemctl list-unit-files** command again to confirm the change. To turn it back on for the default target, run the same command, substituting **enable** for **disable**, as shown here:

![Images](f0204-01.jpg)

When you enable a service, the **systemctl enable** command creates a symbolic link in the directory /etc/systemd/system/multi-user.target.wants that points to the corresponding unit configuration file in /usr/lib/systemd/system. If you wish, you can enable or disable services manually by creating symbolic links in the appropriate systemd directories. However, using **systemctl** is the preferred way because it is less error-prone.

When a service is disabled, you can still start and stop it manually via the **systemctl start** and **stop** commands. This means that the **systemctl disable** command does not prevent a user from accidentally starting a service by mistake. If you want to disable a service unit at boot and ensure that it cannot be started anymore, you should use the **mask** command, as illustrated here:

![Images](f0204-02.jpg)

As shown, this command creates a symbolic link in /etc/systemd/system named postfix.service, which points to /dev/null. A configuration file in /etc/systemd/system always takes precedence over a corresponding file in /usr/lib/systemd/system. Hence, the result is that the default postfix.service file in /usr/lib/systemd/system is “masked” by the symbolic link in /etc/systemd/system to /dev/null.

### CERTIFICATION OBJECTIVE 5.05

### Time Synchronization

The configuration of a Network Time Protocol (NTP) client is straightforward. This section provides an overview of the configuration files and the associated command tools.

There are good reasons to keep different systems running on the same clock. For example, a web server and a client logging in different times would make troubleshooting extremely difficult. Several services rely on accurate timestamps. As an example, a time drift of more than five minutes would cause a Kerberos client to fail authentication.

The time synchronization daemon included with RHEL 9 is **chronyd**. This replaces **ntpd**, which was included with RHEL releases up to version 7\. **chronyd** has some unique features compared to **ntpd** and keeps accurate time in a variety of conditions, whether it is installed on systems that are always connected to the network, such as servers, or on virtual or mobile systems. Before we describe the configuration of **chronyd**, we will explain how to configure the time zone.

#### Time Zone Configuration

Every system, real or virtual, has an internal clock. The installation process on RHEL 9 normally sets the hardware clock to local time rather than UTC. However, UTC (which is essentially identical to Greenwich Mean Time, or GMT) is usually the best setting for servers to avoid issues when switching to daylight saving time.

Every RHEL 9 system includes a time zone configured in the /etc/localtime file. This is a symbolic link that points to one of the time zones files in /usr/share/zoneinfo. As an example, /etc/localtime should point to /usr/share/zoneinfo/America/Los_Angeles if you are based in California.

Rather than manually setting a symbolic link to a time zone file, you can use the **timedatectl** utility. If you run the command alone with no arguments, it will show a summary of the current time settings, including the current time, time zone, and NTP status. Some sample output is shown in [Figure 5-13](#ch05.xhtml_ch5fig13).

FIGURE 5-13 Date and time settings

![Images](F05-13.jpg)

You can display a list of the available time zones by running the following command:

`# timedatectl list-timezones`

Then, to switch to a different time zone, run **timedatectl** with the **set-timezone** command. Here’s an example:

`# timedatectl set-timezone America/Los_Angeles`

#### Sync the Time with chronyd

The default **chronyd** configuration file, /etc/chrony.conf, is set up to connect to a pool of public servers from the NTP pool project. When used collectively, the **chronyd** daemon minimizes time errors.

`pool 2.rhel.pool.ntp.org iburst`

Some versions of RHEL, such as those deployed in cloud environments, may use different NTP servers. The **iburst** configuration option shown here speeds the initial synchronization when the **chronyd** service is started.

To configure **chronyd** to synchronize with a different NTP server, just modify the **server** directives in /etc/chrony.conf and restart **chronyd**:

`# systemctl restart chronyd`

Don’t forget to configure **chronyd** to start automatically at boot:

`# systemctl enable chronyd`

You can display information about the current time sources using the **chronyc sources -v** command. An example is shown in [Figure 5-14](#ch05.xhtml_ch5fig14).

FIGURE 5-14 NTP server statistics

![Images](F05-14.jpg)

![Images](exam.jpg)

**A quick way to enable and start** chronyd **using the default configuration is by running the command** timedatectl set-ntp true.

#### CERTIFICATION SUMMARY

This chapter covered the basic boot process of a RHEL system. It starts with the hardware POST and continues with the BIOS or UEFI system. Once boot media is found, the process moves to the first stage of the GRUB 2 bootloader. The GRUB 2 menu allows you to select and customize the kernel to be booted.

Once you’ve selected an option, GRUB 2 hands control to the kernel. The kernel loads a temporary filesystem known as the initial RAM disk. Then essential drivers and filesystems are loaded, and the kernel executes the first process, also known as **systemd**.

Linux services are controlled by systemd targets, which group together other systemd units. The default target is configured as a symbolic link in the directory /etc/systemd/system, and the unit configuration files are stored in this directory and in /usr/lib/systemd/system. The status of those systemd units can be configured and queried using the **systemctl** command. The systemd targets are linked to other targets and to unit configuration files. **systemctl** can also be used to start, stop, restart, reload systemd units, and more.

You may need to set up local systems as NTP clients. The default NTP service in RHEL 9 is **chronyd**.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 5](#ch05.xhtml).

##### The Boot Process

![Images](squ1.jpg)   Although not strictly a part of the exam, it’s important to know the basics of the BIOS and the UEFI.

![Images](squ1.jpg)   You can change the boot sequence from the BIOS/UEFI menu.

![Images](squ1.jpg)   Once the BIOS/UEFI detects the designated boot drive(s), it hands control to GRUB 2 via the Master Boot Record (MBR) or GUID Partition Table (GPT) of the appropriate drive.

##### Bootloaders and GRUB 2

![Images](squ1.jpg)   RHEL 9 uses GRUB 2.

![Images](squ1.jpg)   The GRUB 2 configuration file is organized into sections.

![Images](squ1.jpg)   From the GRUB 2 menu, you can boot into a systemd target other than the default.

![Images](squ1.jpg)   You can even boot from a GRUB 2 menu into a rescue shell that provides root administrative access without an account password.

![Images](squ1.jpg)   The GRUB 2 configuration file specifies a kernel, a root directory volume, and an initial RAM disk for each operating system.

![Images](squ1.jpg)   If the GRUB 2 configuration file is missing, you may be able to boot from the grub> prompt with information on the /boot directory partition, the Linux kernel file, the top-level root directory, and the initial RAM disk file.

##### Between GRUB 2 and Login

![Images](squ1.jpg)   You can analyze boot messages through the **journalctl** command.

![Images](squ1.jpg)   Default system targets are configured as a symbolic link from the /etc/systemd/system directory.

![Images](squ1.jpg)   The **systemd** process has replaced Upstart and SysVinit, which were part of older RHEL distributions. **systemd** has configuration files in the /etc/systemd/system and /usr/lib/systemd/system directories.

![Images](squ1.jpg)   Once the kernel boots, it hands control to systemd, also known as the first process.

##### Control by Target

![Images](squ1.jpg)   The default target configured in /etc/systemd/system activates systemd units in the /usr/lib/systemd/system directory.

![Images](squ1.jpg)   Target units can include other targets and units to be activated.

![Images](squ1.jpg)   You can use **systemctl** to control a service with the **start**, **stop**, **restart**, **reload**, and other commands.

![Images](squ1.jpg)   The services that start in each target can also be controlled with **systemctl** and the **enable/disable** commands.

##### Time Synchronization

![Images](squ1.jpg)   The **timedatectl** tool can be used to check the current time, date, time zone, and NTP service status.

![Images](squ1.jpg)   The default NTP service in RHEL 9 is **chronyd**. It keeps time in sync with servers configured in the /etc/chrony.conf file.

#### Q SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams. There may be more than one answer for many of these questions.

##### The Boot Process

**[1.](#ch05.xhtml_ch5ques1)**   On what part of the boot hard drive is the first stage of the GRUB 2 bootloader typically located?

##### Bootloaders and GRUB 2

**[2.](#ch05.xhtml_ch5ques2)**   When you see the GRUB 2 configuration menu, what command would you use to modify the configuration?

**[3.](#ch05.xhtml_ch5ques3)**   What string would you add to the **linux** command line to boot into the emergency target?

**[4.](#ch05.xhtml_ch5ques4)**   If you see the **set root=(hd0,msdos1)** directive in the GRUB 2 configuration file, on what partition is the /boot directory? Assume the GRUB 2 configuration file is properly configured.

##### Between GRUB 2 and Login

**[5.](#ch05.xhtml_ch5ques5)**   What temporary filesystem is loaded directly from the GRUB 2 menu?

**[6.](#ch05.xhtml_ch5ques6)**   What one-word command can you use to read systemd log messages?

**[7.](#ch05.xhtml_ch5ques7)**   In what directories can you find the configuration files associated with the first process?

**[8.](#ch05.xhtml_ch5ques8)**   How do you switch from the graphical target to the multi-user target?

##### Control by Target

**[9.](#ch05.xhtml_ch5ques9)**   What command lists the default target?

**[10.](#ch05.xhtml_ch5ques10)**   Name three commands that can be typically run from **systemctl** to control the status of systemd units.

**[11.](#ch05.xhtml_ch5ques11)**   What command lists the state of all systemd units currently available on the local system, including those that are not active?

##### Time Synchronization

**[12.](#ch05.xhtml_ch5ques12)**   What command lists the current time, time zone, and status of the time synchronization service?

**[13.](#ch05.xhtml_ch5ques13)**   Which configuration file is used by **chronyd**?

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for the labs follow the Self Test answers.

#### A SELF TEST ANSWERS

##### The Boot Process

**[1.](#ch05.xhtml_r_ch5ques1)**   For the BIOS/UEFI to hand control over to Linux, it needs to identify the Master Boot Record (MBR) or the GUID Partition Table (GPT) of the boot hard drive.

##### Bootloaders and GRUB 2

**[2.](#ch05.xhtml_r_ch5ques2)**   From the GRUB 2 menu, the command that modifies the configuration is **e**, which stands for “edit.”

**[3.](#ch05.xhtml_r_ch5ques3)**   To boot into the emergency target from the GRUB 2 **linux** command line, you’d append the string **systemd.unit=emergency.target**.

**[4.](#ch05.xhtml_r_ch5ques4)**   The **set root=(hd0,msdos1)** directive implies that the /boot directory is on the first partition on the first hard drive.

##### Between GRUB 2 and Login

**[5.](#ch05.xhtml_r_ch5ques5)**   The temporary filesystem loaded from the GRUB 2 menu is the initial RAM disk filesystem, also known by its filename, initramfs.

**[6.](#ch05.xhtml_r_ch5ques6)**   The one-word command that you can use to read systemd log messages is **journalctl**.

**[7.](#ch05.xhtml_r_ch5ques7)**   The configuration files associated with the first process are located in the /etc/systemd/system and /usr/lib/systemd/system directories.

**[8.](#ch05.xhtml_r_ch5ques8)**   The command to switch from the graphical target to the multi-user target is **systemctl isolate multi-user.target**.

##### Control by Target

**[9.](#ch05.xhtml_r_ch5ques9)**   The command that lists the default target is **systemctl get-default**.

**[10.](#ch05.xhtml_r_ch5ques10)**   Typical commands that can be run from **systemctl** include **start**, **stop**, **restart**, **reload**, **enable**, **disable**, and more.

**[11.](#ch05.xhtml_r_ch5ques11)**   The **systemctl list-units --all** command (or just **systemctl --all**) lists the state of all units, including inactive ones.

##### Time Synchronization

**[12.](#ch05.xhtml_r_ch5ques12)**   The **timedatectl** command lists the current time, time zone, and status of the time synchronization service.

**[13.](#ch05.xhtml_r_ch5ques13)**   The **chronyd** configuration file is /etc/chrony.conf.

#### LAB ANSWERS

Yes, there are many Linux systems that run for years at a time without a reboot. But reboots are sometimes required, such as when newer kernels are installed. So when configuring a Linux system, make sure any changes survive a reboot. On a Red Hat exam, you won’t get credit unless your changes survive a reboot.

##### Lab 1

If successful, this lab will show you how to change the default target, along with the relative importance of the options in the GRUB bootloader. Remember, you can modify the default target via the **systemctl** command:

`# systemctl set-default multi-user.target`

or manually by modifying the /etc/systemd/system/default.target symbolic link:

![Images](f0212-01.jpg)

To confirm that the changes worked, run

![Images](f0212-02.jpg)

Then, you can set again the graphical target to be the default by running

![Images](f0212-03.jpg)

##### Lab 2

This lab is the same as Exercise 5-2\. Practice with the root password recovery procedure until you are familiar with all the steps and you don’t need to rely on the documentation. Remember, Red Hat exams are “closed book.”

##### Lab 3

After completing this lab, you should have modified the variables GRUB_TIMEOUT and GRUB_CMDLINE_LINUX in /etc/default/grub, as shown here:

![Images](f0212-04.jpg)

Note that the **quiet** keyword has been removed from GRUB_CMDLINE_LINUX to enable verbose messages at boot.

Then, run the **grub2-mkconfig** command to generate a new GRUB configuration file:

![Images](f0212-05.jpg)

To really test the result, reboot the system. What happens? Finally, revert your changes.

##### Lab 4

The initial command executed in this lab moved the grub.cfg configuration file to the /root directory. If you understand GRUB 2 well, you should have been able to boot the system from the grub> prompt.

Otherwise, follow the steps in Exercise 5-3 to boot the system. You should have run the following commands to the grub> prompt (some details may vary, such as the version of the kernel installed):

![Images](f0213-01.jpg)

Next, restore the original grub.cfg file:

![Images](f0213-02.jpg)

Alternatively, generate a new grub.cfg configuration file with the **grub2-mkconfig** command. If unsuccessful, you can recover the grub.cfg file by booting into the rescue target described in this chapter. From the rescue mode command-line prompt, you should be able to restore the original configuration with the following commands:

![Images](f0213-03.jpg)

##### Lab 5

One way to accomplish the tasks in this lab is with the following steps:

**1.**   Run the following:

![Images](f0213-04.jpg)

**2.**   Edit the /etc/chrony.conf file and change the pool directive to

![Images](f0213-05.jpg)

Then, restart the **chronyd** daemon:

![Images](f0213-06.jpg)

**3.**   To confirm your changes, run **timedatectl** to check the current time zone. Then, check that the **chornyd** daemon is running and syncing the time from [time.google.com](http://time.google.com):

![Images](f0213-07.jpg)

##### Lab 6

To complete this lab, log in to tester1.example.com:

**1.**   Run the following commands to enable persistent journal logs on disk:

![Images](f0214-01.jpg)

**2.**   Reboot the system and save the journal log messages from the boot before the last one to the file /root/journal-beforelast.log:

![Images](f0214-02.jpg)

##### Lab 7

On tester1.example.com, follow these steps to complete the lab:

**1.**   Confirm the current status of the kdump and rhcd services:

![Images](f0214-03.jpg)

**2.**   Stop **kdump** and configure the service so that it does not start at boot:

![Images](f0214-04.jpg)

**3.**   Configure **rhcd** to start at boot:

![Images](f0214-05.jpg)

**4.**   Reboot the system and check the status of the services. You can list more than one service on the same command line:

![Images](f0214-06.jpg)

## Chapter 6

## User Administration

CERTIFICATION OBJECTIVES

[6.01     User Account Management](#ch06.xhtml_ch6obj01)

[6.02     Administrative Control](#ch06.xhtml_ch6obj02)

[6.03     User and Shell Configuration](#ch06.xhtml_ch6obj03)

[6.04     Special Groups](#ch06.xhtml_ch6obj04)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

Fundamental to Linux administration is the management of users and groups. In this chapter, you’ll examine different ways to manage the variety of users and groups available to Linux. Important skills in this area range from the simple login to user account management, group membership, and group collaboration. The configuration of administrative privileges for Linux users can help the master administrator distribute responsibilities to others.

You’ll see how to manage these tasks from the command line, with the help of the files of the shadow password suite. You’ll also use tools such as the Cockpit web console to set up some of these tasks. As you should expect, Red Hat GUI tools can’t do it all, which emphasizes the importance of understanding user management from the command line.

INSIDE THE EXAM

This chapter addresses several RHCSA objectives. Briefly explained, these objectives include the following:

![Images](square.jpg)   Log in and switch users in multiuser targets

That means you need to know how to log in with regular accounts when RHEL 9 is running in the multiuser or graphical targets. To switch users, you need to know how to switch to a different account using the **su** command.

![Images](square.jpg)   Create, delete, and modify local user accounts

![Images](square.jpg)   Change passwords and adjust password aging for local user accounts

![Images](square.jpg)   Create, delete, and modify local groups and group memberships

You could use commands such as **useradd**, **usermod**, **groupadd**, **groupmod**, and **chage** as well as Cockpit to accomplish these tasks. While this chapter explains how you can use both types of tools, there is no guarantee that Cockpit will be available during an exam.

![Images](square.jpg)   Configure superuser access

You must be able to assign root privileges using the /etc/sudoers file and the wheel group.

![Images](square.jpg)   Create and configure set-GID directories for collaboration

This objective refers to how to set one or more directories for collaboration among a group of users.

### CERTIFICATION OBJECTIVE 6.01

### User Account Management

You need to know how to create and configure users. This means knowing how to configure and modify accounts, work with passwords, and organize users in groups. You also need to know how to configure the environment associated with each user account: in configuration files and in user settings.

If you’ve installed RHEL 9 following the instructions in [Chapter 1](#ch01.xhtml), the default Red Hat installation should include a regular user account in addition to the root administrative account. Although no regular user accounts except root are required, it’s important to set up some regular user accounts. Even if you’re going to be the only user on the system, do create at least one non-administrative account for day-to-day work. Then you can use the root account only when it’s necessary to administer the system. You can add accounts to Red Hat Enterprise Linux systems using various utilities, including direct editing of password configuration files (the manual method), the **useradd** command (the command-line method), and the Cockpit web console (the graphical method).

#### Different Kinds of Users

There are three basic types of Linux user accounts: superuser (root), regular, and system. The superuser root account is automatically created when Linux is installed, and it has administrative privileges for all services on a Linux system. A “black hat” hacker who has a chance to take control of this account can take full control of that system.

For the times when you do log in as an administrator, RHEL builds in safeguards for root users. Log in as the root user, and then run the **alias** command. You’ll see entries such as the following:

`alias rm='rm -i'`

Due to this particular alias, when the root user runs the **rm** command, the shell actually executes the **rm -i** command, which prompts for confirmation before the **rm** command deletes a file. Note that the **-f** option in **rm**, such as **rm -f *filename***, supersedes this safety setting.

Regular users have the necessary privileges to perform standard tasks on a Linux computer. They can access programs such as bash, a database, or a web browser. They can store files in their own home directories. Since regular users do not normally have administrative privileges, they cannot accidentally delete critical operating system configuration files. You can assign a regular account to most users, safe in the knowledge that they can’t disrupt a system with the privileges they have on that account.

Services such as Apache, mail, and printing have their own individual system accounts. These accounts exist to allow each of these services to interact with Linux systems, and are not allowed to log in interactively on a system. Normally, you won’t need to change any system account, but if you see that someone is running a command shell through one of these accounts, be wary. Someone may have broken into your system.

![Images](job.jpg)

**To review recent logins, run the** last | less **command. If the login is from a remote location, it will be associated with a specific IP address outside your network.**

To show the identity of a user, type the **id** command followed by the username, or just **id** to show the identity of the current user. An example of the information displayed by the **id** command is shown next:

![Images](f0217-02.jpg)

Ignore the last line in the output, which defines the SELinux context. The **id** command shows the numeric user ID (UID) of the user along with its name inside parentheses. Every user belongs to a primary group, which is displayed with its group ID (GID) and name. The command shows all the groups the user is part of, with their GIDs and name.

#### The Shadow Password Suite

When Unix was first developed back in the 1970s, security was not a serious concern. Everything required for user and group management was contained in the /etc/passwd and /etc/group files. As suggested by the name, passwords were originally in the /etc/passwd file. The problem is that file is “world readable.” Anyone with a copy of that file, before the shadow password suite was introduced, would have a copy of the encrypted password for every user. Even though passwords are not saved in clear text, they may be vulnerable to brute-force attacks. For example, a dictionary attack can usually decipher a password in a few seconds, if the password is based on a common dictionary word. That was the main motivation behind the development of the shadow password suite, which moves more sensitive information to other files that are readable only by the root administrative user.

The four configuration files of the shadow password suite are /etc/passwd, /etc/group, /etc/shadow, and /etc/gshadow. Default settings for user accounts are stored in the /etc/login.defs file.

##### The /etc/passwd File

The /etc/passwd file contains basic information about every user. Open that file in a text editor and browse around a bit. At the top of the file, the first line defines the root login account (the superuser). Other users in this file may relate to services such as mail, ftp, and sshd. There may be regular users designed for logging in to the system. An excerpt of the /etc/passwd file is shown in [Figure 6-1](#ch06.xhtml_ch6fig1).

FIGURE 6-1 The /etc/passwd file

![Images](F06-01.jpg)

There are seven columns of information in the /etc/passwd file, delineated by colons. Each column in /etc/passwd includes specific information. For example, the user account defined by the following line has seven fields, described in [Table 6-1](#ch01.xhtml_ch1tab1):

TABLE 6-1 The Anatomy of /etc/passwd

![Images](f0219-02.jpg)

`mj:x:1000:1000:Michael Jang:/home/mj:/bin/bash`

The RHEL 9 version of /etc/passwd includes more secure features for user accounts when compared to some other Linux distributions. The only accounts with a real login shell are user accounts. Service accounts such as mail or nobody are assigned the false /sbin/nologin shell.

##### The /etc/group File

Every Linux user is assigned to a *primary group*, which is the group corresponding to the GID defined in /etc/passwd. By default, in RHEL 9 every user gets his own private group, with the same name as their username. A user may also be a member of other groups, which are usually referred to as *supplementary groups* to distinguish them from a user’s primary group.

The main purpose of a primary group is to assign a group owner to a new file. All files are owned by the UID and primary group GID of the user who created them.

Open /etc/group in a text editor. Browse around a bit. The first line in this file specifies information for the root administrative user’s group. Some groups have a special purpose. For example, being a member of the wheel group gives the privilege to run administrative commands via sudo, as explained later in the chapter. An excerpt of the /etc/group file is shown in [Figure 6-2](#ch06.xhtml_ch6fig2).

FIGURE 6-2 The /etc/group file

![Images](F06-02.jpg)

There are four columns of information in the /etc/group file, delineated by colons. As an example, the group defined in the following line has four fields, described in [Table 6-2](#ch06.xhtml_ch6tab2):

TABLE 6-2 The Anatomy of /etc/group

![Images](f0221-01.jpg)

`reviewers:x:2000:mj,ao,sd`

##### The /etc/shadow File

The /etc/shadow file is a supplement to /etc/passwd. It contains eight columns of information, and the first column contains the same list of usernames as documented in /etc/passwd. As long as there’s an *x* in the second column of each /etc/passwd entry, Linux knows to look at /etc/shadow for more information. Open that file in a text editor and browse around a bit. You’ll see the same pattern of information, starting with the root administrative user. An excerpt of the /etc/shadow file is shown in [Figure 6-3](#ch06.xhtml_ch6fig3).

FIGURE 6-3 The /etc/shadow file

![Images](F06-03.jpg)

As shown in [Table 6-3](#ch06.xhtml_ch6tab3), /etc/shadow includes the encrypted password in the second column, and the remaining information relates to the way passwords are managed. The first two characters of the second column specify the encryption hash for the password. If you see a $1, the password is hashed to the Message Digest 5 (MD5) algorithm, the standard through RHEL 5\. If you see a $6, the password is protected with the 512-bit Secure Hash Algorithm (SHA-512), the standard since RHEL 6.

TABLE 6-3 The Anatomy of /etc/shadow

![Images](f0222-01.jpg)

Note that some users in [Figure 6-3](#ch06.xhtml_ch6fig3) have * or !! characters in the password field. That means that the user will not be able to use a password to log in. This is a standard configuration for system user accounts.

![Images](exam.jpg)

**If you do not remember the meaning of a field in the files described in this section, open the corresponding man page. Note that** man passwd **shows the man page of the** passwd **command, while** man 5 passwd **is the correct command to display the man page for the /etc/passwd file.**

##### The /etc/gshadow File

The /etc/gshadow file is the group configuration file in the shadow password suite. It includes the group administrators, which can add other group members using the **gpasswd** command. If desired, you can even configure a hashed password. Once a password is set, the group administrators can add or remove members to the group by using the **gpasswd** command and typing the required password. An excerpt of the /etc/gshadow file is shown in [Figure 6-4](#ch06.xhtml_ch6fig4). For example, the group defined by the following line has four fields, described in [Table 6-4](#ch06.xhtml_ch6tab4):

FIGURE 6-4 The /etc/gshadow file

![Images](F06-04.jpg)

TABLE 6-4 The Anatomy of /etc/gshadow

![Images](f0223-02.jpg)

`reviewers:!:mj:mj,ao,sd`

##### The /etc/login.defs File

The /etc/login.defs file provides the baseline for a number of parameters in the shadow password suite. This section provides a brief analysis of some of the active directives in the default version of this file. As you’ll see, the configuration options go somewhat beyond authentication. Keep in mind that if you change any settings, those are effective only for new users, not for existing ones.

The first configuration parameter in the /etc/login.defs file specifies the directory where mailboxes are located:

`MAIL_DIR /var/spool/mail`

In the file, there are three directives related to default password aging information. The directives are explained in the comments inside the file and in [Table 6-5](#ch06.xhtml_ch6tab5).

TABLE 6-5 /etc/login.defs Password-Aging Configuration Parameters

![Images](f0224-01.jpg)

As suggested earlier, user ID (UID) and group ID (GID) numbers for regular users and groups start at 1000\. Since Linux supports UID and GID numbers above 4 billion (actually, up to 2^(32) – 1), the maximum UID and GID numbers of 60000, as defined in the /etc/login.defs file, may seem strange. However, this leaves higher numbers available for other user databases, such as those associated with OpenLDAP or Microsoft Active Directory. In the following lines, **UID_MIN** specifies the minimum UID to assign when a new regular user is created, **UID_MAX** specifies the maximum UID, and so on:

![Images](f0224-03.jpg)

Similarly, the **useradd** and **groupadd** commands with the **-r** switch create a system user or system group, respectively, whose ID is chosen within the following range:

![Images](f0224-04.jpg)

Normally, when the **useradd** command is run to create a new user, it automatically creates home directories as well, which is confirmed by the following directive:

![Images](f0224-05.jpg)

As described later in this chapter, other files set the value of the umask. But if those other files did not exist, this directive would govern the default umask for regular users:

![Images](f0224-06.jpg)

The following directive is critical in the implementation of the *user private group scheme*. In this configuration scheme, users are made members of their own private group, normally with the same UID and GID numbers. The following directive means that the umask group bits will be the same as the owner bits for non-root users. Additionally, the group will be deleted if all the users in that group are also deleted.

![Images](f0225-01.jpg)

Finally, the following directive was used to determine the algorithm used to encrypt passwords, by default SHA 512:

![Images](f0225-02.jpg)

![Images](exam.jpg)

**The tools discussed in this section can help you create, delete, and modify local user accounts.**

#### Command-Line Tools

There are two basic ways to add users through the command-line interface. As the root user, you can add users directly by editing the /etc/passwd file in a text editor such as vi. To this end, both **vipw** and **vigr** were described in [Chapter 2](#ch02.xhtml). Alternatively, you can use text commands customized for the purpose.

##### Add Users Directly

Open the /etc/passwd file in the text editor of your choice. As described in [Chapter 2](#ch02.xhtml), you can do so with the **vipw** command. However, if you add users by directly editing the files of the shadow password suite, you’ll have to do two more things:

![Images](square.jpg)   *Add a user home directory.* For example, for user donna, you’d have to add the /home/donna home directory, making sure that user donna and group donna both have ownership of that directory.

![Images](square.jpg)   *Populate the user home directory.* The default option is to copy the files from the /etc/skel directory, discussed later in this chapter. You’d also have to make sure that user donna and group donna have ownership of those files copied to the /home/donna directory.

##### Add Users to a Group Directly

Every Linux user is assigned to a group, at least his own private group. The GID number listed in the /etc/group file for a user’s primary group must match that shown for that user in the /etc/passwd file. The user is usually the only member of that group.

Of course, users can be members of other groups as well. For example, to create a group named project, you could add the entries to the /etc/group and /etc/gshadow files. One way to do so in a text editor is with the **vigr** command. As an example, the following entry might be appropriate for a group named project:

`project:x:60001:`

The number 60001 is used, as that is beyond the limit of the **GID_MAX** directive from the /etc/login.defs file described earlier. But that’s just an arbitrary limit used by the **groupadd** command. There’s no prohibition against a higher number, as long as it does not duplicate existing GIDs. However, it is convenient when the UID and GID numbers of regular users match.

Of course, for a group to be useful, you’d have to add users already configured in the /etc/passwd file at the end of the line. The following example assumes these users already exist:

`project:x:60001:michael,elizabeth,stephanie,tim`

You’d also have to add this group to the /etc/gshadow file. You could do so directly with the **vigr -s** command. Alternatively, to set up a group administrator with a password, you could run the **gpasswd** command. For example, the **gpasswd project** command would set up a password for administering the group, as described later in this chapter. It would automatically add the encrypted password with the given group name to the /etc/gshadow file.

##### Add Users at the Command Line

Alternatively, you can simplify this process with the **useradd** command. The **useradd michael** command would add user michael to the /etc/passwd file. In addition, the **useradd** command creates the /home/michael home directory, adds the standard files from the /etc/skel directory, and assigns the default shell, /bin/bash. The **useradd** command is the recommended way to add users on RHEL. It includes a number of command options. The most common are shown in [Table 6-6](#ch06.xhtml_ch6tab6).

TABLE 6-6 useradd Command Options

![Images](f0227-01.jpg)

##### Assign a Password

Once a new user is created, you can use the **passwd *username*** command to assign a password to that user. For example, the **passwd pm** command prompts you to assign a new password to user pm. For security reasons, RHEL is configured to avoid passwords that are based on dictionary words, shorter than eight characters, too simple, based on palindromes, and other, similar criteria. Nevertheless, such passwords are legal and accepted if the **passwd** command is run by the root user.

##### Add or Delete a Group at the Command Line

When it’s appropriate to add a special group to the shadow password suite, you may want to use the **groupadd** command. Generally, you’ll want to use it with the **-g** option. For example, the following command would set up a special project group with a GID of 60001:

`# groupadd -g 60001 project`

If you don’t use the **-g** option, the **groupadd** command takes the next available GID number. For example, if two regular users are configured on a system, they each have UID and GID numbers of 1000 and 1001, respectively. If you’ve run the **groupadd project** command without specifying a GID number, the project group is assigned a GID of 1002\. The next regular user that’s created would get a UID of 1002 and a GID of 1003, which could lead to confusion.

Fortunately, the command to delete a group is simpler. If the project group has completed its work, you can delete that group from the shadow password suite database with the following command:

`# groupdel project`

##### Delete a User

The removal of a user account is a straightforward process. The easiest way to delete a user account is with the **userdel** command. By default, this command does not delete that user’s home directory, so administrators can transfer files from that user, perhaps to an employee who has taken over the tasks of the deleted user. Alternatively, the **userdel -r *username*** command deletes that user’s home directory along with all of the files stored in that home directory.

![Images](exam.jpg)

**If you know both the CLI and GUI methods to perform a task, use the CLI method. It almost always saves time.**

This is a lot faster than the GUI method, for which you open the Cockpit web console, select the user, and then click Delete. Although it’s probably easier for a less experienced user to remember the GUI method, text commands can save you time.

EXERCISE 6-1

**Add a User with Cockpit Web Console**

One alternative to user management commands such as **useradd** and **usermod** is the Red Hat Cockpit web console.

1.   Install the cockpit RPM package if it is not present:

`# rpm -q cockpit || dnf install cockpit`

2.   Permit the Cockpit service through the firewall:

![Images](f0228-02.jpg)

3.   Start the Cockpit service:

`# systemctl enable --now cockpit.socket`

4.   Open Firefox and point to the URL [https://localhost:9090](https://localhost:9090). Accept the server’s certificate, log in with the root account credentials, select the Accounts page, and click Create New Account. This opens a new window, as shown here:

![Images](I06-01.jpg)

5.   Complete the form. All entries are required, except Full Name. The entries are fairly self-explanatory. The password should be at least eight characters and should ideally contain a mix of upper- and lowercase letters, numbers, and punctuation to keep it more secure from the standard password-cracking programs.

6.   Enter the identical password in the Confirm field and click Create when you are done.

7.   Select the account that you have just created. You will see the screen shown below. Select the Server Administrator check box to give the user administrative privileges.

![Images](I06-02.jpg)

8.   Repeat the process as desired for any additional new users that may be required. Make sure to create at least one new user prior to running Exercise 6-2.

EXERCISE 6-2

**Real and Fake Shells**

Do not run this exercise unless a regular user has already been created on the local system. If desired, run Exercise 6-1 first, as that allows you to create a new regular user on the target system.

1.   Open the /etc/passwd file. Find a current regular user with a UID of 1000 or above.

2.   Identify the default shell. It’s specified in the last column, normally /bin/bash for regular users.

3.   Change the default shell to /sbin/nologin, and save the changes to the /etc/passwd file.

4.   Open a different virtual console. Press the CTRL-ALT-F2 keys to open a different console. (If you’re already in the second virtual console, substitute F3, F4, F5, or F6 for F2.)

5.   Try logging in as the modified user. What happens?

6.   Return to the original console. If it’s the GUI, it should be accessible with the CTRL-ALT-F1 key combination. If that is not possible (such as when the GUI is not installed), you should still be able to log in as the root administrative user.

7.   Reopen the /etc/passwd file. Restore the /bin/bash shell to the target regular user.

#### Modify an Account

As a Linux administrator, you may want to modify an existing user account. While the Cockpit web console is straightforward to use and convenient to create or delete users, command-line interface options offer more features.

We’ve described some of these commands, such as **useradd**, **userdel**, **groupadd**, and **groupdel**. A few other key user administration commands are **usermod**, **groupmod**, and **chage**.

##### usermod

The **usermod** command modifies various settings in /etc/passwd. In addition, it allows you to change the settings in /etc/shadow, such as the expiration date for an account, or to add a user to a supplementary group in /etc/group. For example, the following command sets the account associated with user test1 to expire on June 8, 2023:

`# usermod -e 2023-06-08 test1`

The following command makes user test1 a member of a group named accounting:

`# usermod -G accounting test1`

The **usermod** command is closely related to the **useradd** command; in fact, the **usermod** command supports all of the **useradd** command options listed earlier in [Table 6-6](#ch06.xhtml_ch6tab6). The **usermod** command includes several additional options, some of which are listed in [Table 6-7](#ch06.xhtml_ch6tab7).

TABLE 6-7 usermod Command Options

![Images](f0231-01.jpg)

When a user password is locked, an exclamation mark (!) is added before the user’s encrypted password in /etc/shadow.

##### groupmod

The **groupmod** command is relatively simple. It has two practical uses. The following command changes the GID number of the group named project (in this case, to 60002):

`# groupmod -g 60002 project`

In contrast, the following command changes the name of the group named project to secret:

`# groupmod -n secret project`

![Images](exam.jpg)

**The** chage **command is an excellent way to address the RHCSA objective to “adjust password aging for local user accounts.”**

##### chage

The **chage** command is primarily used to manage aging information for a password, by modifying the corresponding fields in the /etc/shadow file. While some of the parameters can also be set with the **useradd** and **usermod** commands, most of the command options are different, as described in [Table 6-8](#ch06.xhtml_ch6tab8).

TABLE 6-8 chage Command Options

![Images](f0232-01.jpg)

### CERTIFICATION OBJECTIVE 6.02

### Administrative Control

It’s important for administrators to execute most actions as regular users because the root administrative user has full privileges on a system. Limits on regular users can help protect Linux systems from accidents. Regular users who have the root administrative password can temporarily take root privileges with the **su** command. The **su** command can also allow a user to become another user, provided that the correct password for the target user is specified.

Both the **su** and **sudo** commands allow running commands as another user, as well as opening a shell as another user. For administrative tasks, **sudo** offers more flexibility, because the configuration can tell exactly which commands a user is allowed to run. With **sudo** and the help of the /etc/sudoers file, it’s possible to set up dedicated administrators with partial or complete root administrative privileges or to execute a command as another user.

#### The Ability to Log In

The file /etc/security/access.conf regulates access by all users. Although this topic is not explicitly listed in the RHCSA exam objectives, it is an important skill that you should master as a system administrator.

By default, in RHEL 9 the file /etc/security/access.conf does not have any effect. To enable access.conf, add the following line to /etc/pam.d/password-auth and /etc/pam.d/system-auth:

`account required pam_access.so`

The default version of this file is completely commented out, but the comments provide useful examples. The first example shows how to disallow (with the -) logins to the first virtual console (tty1) to *all* users but root:

`-:ALL EXCEPT root:tty1`

Scroll down further in the file. The following lines (with the +) show how to allow the root user to access the system from three specific remote IP addresses and from the localhost address:

![Images](f0233-03.jpg)

If you’re protecting a system from outside networks, this type of limitation on direct root administrative access makes sense. As long as the **su** or **sudo** command allows it, users who log in remotely as regular users can still elevate their privileges accordingly.

Be aware that the directives in this file are considered in order. So, if directives that allow access (with the +) come first, then the following directive denies access to all other users from all other local and remote logins:

`-:ALL:ALL`

#### The su Command

In some cases, such as Red Hat exams, it’s appropriate to log in as the root administrative user. But in real production systems, it’s best to log in as a regular user. As a regular user, you can temporarily open a shell with root administrative privileges with the **su** command. Normally, that command prompts for the password of the root administrative user. After you’ve completed administrative tasks, it’s best to log out of the root administrative account; the **exit** command would return to the regular account of that user.

The **su -l** command is slightly different because it opens a *login shell* for the root administrative account. That means **su -l** changes the current directory to the root user’s home directory, /root, and sets the user’s environment as if the root user had logged in directly.

If you have the password of a second user, you can use the **su -l *username*** command to log in directly to that account. For example, if you wanted to switch to user dickens’ account, you’d run the **su -l dickens** command. When you enter her password successfully, the command takes you to the /home/dickens directory.

Finally, the **su -c** command can be used to assume administrative privileges for one command. For example, the following command can be used to modify the first virtual drive on a system (assuming the root administrative password is successfully entered in response to the prompt):

`$ su -c '/sbin/fdisk /dev/sda'`

#### Limit Access to su

As discussed earlier, the ability to log in directly as the root administrative user can be regulated. Further limitations on administrative access are possible. For example, you can limit the users who are allowed to run the **su** command. This requires two basic steps.

First, you’ll need to list the users who should have access to the **su** command. Make them a part of the wheel group. By default, here is what this line in /etc/group looks like:

`wheel:x:10:`

You can add selected users to the end of this line directly with the **usermod -G wheel *username*** command or with the Cockpit web console.

Second, this requires a change to the configuration of Pluggable Authentication Modules (PAM). While PAM is not an RHCE objective, there’s a commented directive available in the /etc/pam.d/su file ready for this purpose:

![Images](f0234-03.jpg)

If this line is activated, only users who are members of the wheel group are allowed to use the **su** command.

#### The sg Command

With the **sg** command, you can execute a command as another group. Assume you’re a member of the project group. Then the command **sg project -c *command*** allows you to run commands with the identity of the group named project. For example, the following command copies the important.doc file to the noted directory:

`$ sg project -c 'cp important.doc /home/project'`

The file important.doc in the directory /home/project is owned by the group project, because the **cp** command was run under the project group.

#### Superuser Access with the sudo Command

You can limit access to the **sudo** command. Regular users who are authorized in /etc/sudoers can access administrative commands with their own password. Unlike **su**, typically the **sudo** command requires you to type your own user account’s password, rather than the password of the user that you are trying to access.

To access /etc/sudoers run the **visudo** command. The **visudo** command locks the /etc/sudoers file against simultaneous edits and checks the syntax of the file before exiting. The following directive is active in the default version of the file. This allows the root user to run any command as any user:

![Images](f0235-01.jpg)

The **root** keyword indicates that this configuration applies to the root user. Thanks to this configuration, the root user can run any command (due to the last ALL on the line), from any host (thanks to the first ALL), as any user (the second ALL).

Other users can be given administrative access. For example, if you want to allow user boris full administrative access, add the following directive to /etc/sudoers:

![Images](f0235-02.jpg)

In this case, all boris needs to do to run an administrative command is to preface it with the **sudo** command. For example, if boris runs the following command, he’s prompted for his own regular user password before the noted service is started:

![Images](f0235-03.jpg)

Alternatively, you can allow special users administrative access without a password. As suggested by the comments in the file, the following directive in /etc/sudoers would allow all users who are members of the wheel group to run administrative commands without a password:

![Images](f0235-04.jpg)

But you don’t have to allow full administrative access. For example, if you want to allow users who are members of the %users group to shut down the local system, activate the following directive:

![Images](f0235-05.jpg)

In many Linux configuration files, the % sign in front of a directive specifies a group. For example, another directive shown in comments specifies a group of commands that can be run by users who are members of the %sys group:

![Images](f0235-06.jpg)

Each of the directives can be associated with a set of commands. For example, users in the sys group, who are allowed to run PROCESSES directives, can run the commands associated with the following configuration line:

![Images](f0235-07.jpg)

In a similar fashion, you could set up an admin group of users who are allowed to run these commands with the following directive:

![Images](f0236-01.jpg)

This assumes that groups such as admin exist in the /etc/group and /etc/gshadow files.

### CERTIFICATION OBJECTIVE 6.03

### User and Shell Configuration

Each user on any Red Hat Enterprise Linux system has an *environment* when logged on to the system. The environment defines directories where Linux looks for programs to run, the look of the login prompt, the terminal type, and more. This section explains how you can configure the default environment for local users. All system-wide shell configuration files are kept in the /etc directory. These files are bashrc, profile, and the scripts in the /etc/profile.d directory. These files and scripts are supplemented by hidden files in each user’s home directory, as just described. Let’s take a look at these files.

#### Home Directories and /etc/skel

When a new user is created with standard commands such as **useradd** or with the Cockpit web console, a default set of configuration files is copied to the user’s home directory from the /etc/skel directory.

##### Home Directory

The home directory is where a user starts when logging in to a RHEL system. The home directory for most users is /home/*username*, where *username* is the user’s login name. Every user should normally have write permission in his own home directory, so each user is free to read and write his own files.

##### /etc/skel

The /etc/skel directory contains default environment files for new accounts. The **useradd** command copies these files to the home directory for new users. The contents of /etc/skel may vary. While the standard files in this directory are hidden, administrators are free to add more files for new users. Standard files from one copy of /etc/skel are described in [Table 6-9](#ch06.xhtml_ch6tab9).

TABLE 6-9 Standard Files in the /etc/skel Directory

![Images](f0237-01.jpg)

![Images](exam.jpg)

**Linux includes many hidden files that start with a dot (.). To list these files, run the** ls -a **command. For example, if you want to list all the files in the /etc/skel directory, run the** ls -a /etc/skel **command.**

If you’ve installed more than a standard set of software packages on RHEL, additional configuration files and subdirectories may appear in the /etc/skel directory. For example, the installation of certain packages may include configuration files associated with emacs and the Z shell (zsh) in this directory.

As the system administrator, you can edit these files or place custom files in /etc/skel. When new users are created, these files are copied to the new users’ home directories.

![Images](job.jpg)

**/etc/profile and ~/.bash_profile are executed before starting an interactive shell, while /etc/bashrc and ~/.bashrc are run for both interactive and noninteractive shells (such as scripts).**

##### /etc/bashrc

The /etc/bashrc file is used for aliases and functions on a system-wide basis. Open this file in the text editor of your choice. Read each line in this file. Even if you don’t understand the script commands, you can see that this file sets the following bash shell parameters for each user:

![Images](square.jpg)   It assigns a value of **umask**, which sets the default permissions for newly created files. It supports one set of permissions for root and system users (with user IDs below 200) and another for regular users.

![Images](square.jpg)   It assigns and defines a prompt, which is what you see just before the cursor at the command prompt.

![Images](square.jpg)   It includes settings from *.sh files in the /etc/profile.d/ directory.

The settings here are supplemented by the .bashrc file in each user’s home directory and, for login shells, by the /etc/profile, .bash_profile, and .bash_logout files.

##### /etc/profile and /etc/profile.d

The /etc/profile file is used for system-wide environments and startup files, and is sourced when bash is invoked as an interactive shell.

The first part of the file sets the PATH for searching for commands. Additional directories are added to the PATH with the **pathmunge** function. Then it exports the PATH, USER, LOGNAME, MAIL, HOSTNAME, HISTSIZE, and HISTCONTROL variables and finally runs the scripts in the /etc/profile.d directory. You can check the current value of any of these variables with the **echo $*variable*** command.

##### /etc/profile.d

The /etc/profile.d directory is designed to contain scripts to be executed in a login or interactive shell (that is, not in a script or a command that is run as **bash -c *command***). If you performed a “Server with GUI” installation, the following is a partial listing of the files; those with .sh extensions apply to the default bash shell:

![Images](f0238-01.jpg)

In most cases, there are two versions of a script, customized for different shell environments. Look at the files in the /etc/profile.d script directory. You can see that any script in this directory that ends with .sh is included as part of the configuration sourced by /etc/profile. Scripts with other extensions, such as .csh, relate to the C shell.

EXERCISE 6-3

**Another Way to Secure a System**

One more way to help secure a system is to change the default permissions for new files and directories. In this exercise, you’ll reconfigure a system to remove access permissions for default files from other users or groups.

1.   Back up the current version of the /etc/bashrc and /etc/login.defs.

2.   Open the /etc/bashrc file in a text editor. Two lines in the file set the umask. One of the two lines is selected, depending on the **if** statement above them. See if you can determine which value of umask is assigned to a regular user.

3.   The **if** statement tests to see whether the username and group name are the same and that the UID is greater than 199\. In other words, the umask value of 002 is given to non-login shells run by regular users. A umask value of 022 is given to system users.

4.   Change the first **umask** statement to exclude all permissions for groups and others. In other words, replace the umask of 002 with a umask of 077.

5.   Save and exit the file.

6.   In the /etc/login.defs file, find the UMASK directive and change its value to 077\. This umask value is used by a login shell.

7.   Log in as a regular, nonprivileged user. Use the **touch** command to make a new empty file. Use **ls -l** to verify the permissions on that file.

8.   Open a non-login shell (i.e., type **bash**). Again, use the **touch** command to make a new empty file and use **ls -l** to verify the permissions on that new file.

You have just changed the default umask for login and non-login shells. While this is an excellent option for security, it would affect the steps used in other chapters. Therefore, the final step is important.

9.   Restore the original versions of /etc/bashrc and /etc/profile from the backup created in Step 1.

#### Shell Configuration Files in User Home Directories

As described earlier, each user gets a copy of all files from the /etc/skel directory, typically when the account is created. Most of them are hidden, revealed only with commands such as **ls -a**. As users start working with their accounts, more configuration files may be added to their home directories. Some users may work primarily with the default bash shell, whereas others will have additional configuration files related to their GUI desktop environments, such as GNOME.

The default Linux shell is bash, and until recently it was specifically included as the only shell described in associated Red Hat exam objectives. Although bash is no longer specifically included in the objectives, it is the default for RHEL 9.

#### Login, Logout, and User Switching

While this may seem like a “no-brainer” topic for Linux users with even a couple of days of experience, one of the RHCSA topics is “Log in and switch users in multiuser targets.” It includes concepts from different chapters. As discussed in [Chapter 5](#ch05.xhtml), the multi-user targets are multi-user.target and graphical.target. Virtual terminals are available at all of these targets. In the RHEL 9.1 release, a text login prompt appears as follows:

![Images](f0240-01.jpg)

The hostname, as well as the versions of RHEL 9 and the kernel, will vary. But that’s irrelevant to actual logins; all you need to do is type in a username, press ENTER, and type in a password when prompted.

Logouts from the command line are even simpler; the **exit**, **logout**, and CTRL-D commands all perform logouts from the command line. Of course, once you’ve logged out from a system, the login prompt just shown will appear.

As discussed earlier in this chapter, there’s a different way to switch user accounts. For example, to switch from the current account to user donna’s account, run the following command:

`$ su -l donna`

The same **exit**, **logout**, and CTRL-D commands can be used to exit from user donna’s account. Of course, users can log in to and log out of the GUI. Although the steps vary a bit by desktop environment, they are as simple as the steps required to log in to and log out of any other operating system.

### CERTIFICATION OBJECTIVE 6.04

### Special Groups

In the past, many Linux distributions would typically assign all users to the same primary group, making it easier for them to share files. However, this approach had a security downside: if permissions weren’t carefully configured, all members of that primary group could access each other’s files and directories. This was often undesirable, as users might not want to share their data with everyone in the group. Red Hat has addressed this issue by assigning unique group ID (GID) numbers to each user, enhancing both security and user privacy.

As previously mentioned, this is known as the user private group scheme. Users get exclusive access to their own primary groups and don’t have to worry about other users reading the files in their directories.

#### Standard and Red Hat Groups

In RHEL, each user gets her own special private group by default. As noted earlier, UIDs and GIDs normally start at 1000, are assigned matching numbers, and proceed in ascending order. In addition, you can set up special groups of dedicated users, ideally with higher GIDs. For example, an administrator might configure a group for the accounting department, perhaps with a GID of 70000.

#### Shared Directories

Most people work in groups, and they may want to share files. However, there may be good reasons for people in those groups to keep their information hidden from others. To support such groups, you can set up a shared directory, with access limited to the members of the group.

Assume you want to set up a shared directory, /home/accshared, for a group of accountants. To that end, you can set up a shared directory with the following basic steps:

1.   Create the shared directory:

`# mkdir /home/accshared`

2.   Create a group for the accountants. Call it accgrp. Give it a group ID that doesn’t interfere with existing group or user IDs. One way to do this is to add a line such as the following to the /etc/group file. Substitute the desired usernames.

![Images](f0241-02.jpg)

3.   Set up appropriate ownership for the new shared directory. The following commands prevent any specific user from taking control of the directory and assign group ownership to accgrp:

![Images](f0241-03.jpg)

Any user who is a member of the accgrp group can now create files in and copy files to the /home/accshared directory. Any files generated within or copied to that directory will be owned by the accgrp group.

This is made possible by the 2770 permissions assigned to the /home/accshared directory. Let’s break that down into its component parts. The first digit (2) is the *set group ID bit*, also known as the *SGID bit*. When an SGID bit is set on a directory, any files created in that directory automatically have their group ownership set to be the same as the group owner of the directory. In addition, group ownership of files copied from other directories is reassigned (in this case, to the group named accgrp). There is a second way to set the SGID bit for the /home/accshared directory:

`chmod g+s /home/accshared`

The remaining digits are basic knowledge for any experienced Linux or Unix user. The 770 sets read, write, and execute permissions for the user and group that own the directory. Other users get no permissions to that directory.

Recall from [Chapter 2](#ch02.xhtml) that the read permission on a directory allows the user to list its contents, while the write permission gives the ability to create new files in it. The execute permission on a directory is perhaps the most misunderstood, because there is nothing to execute: it just gives permission to access the contents of the directory (i.e., **cd** into it).

EXERCISE 6-4

**Control Group Ownership with the SGID Bit**

In this exercise, you will create new files in a directory designed to be shared by a group of users. You’ll also see the difference in what happens before and after the SGID bit is set.

1.   Add users called test1, test2, and test3\. Specify passwords when prompted. Check the /etc/passwd and /etc/group files to verify that each user’s private group was created.

![Images](f0242-01.jpg)

2.   Edit the /etc/group file and add a group called tg1\. Make the test1 and test2 accounts members of this group. You could add the following line to /etc/group directly:

`tg1:x:99999:test1,test2`

Before you proceed, make sure the group ID assigned to group tg1 (in this case, 99999) is not already in use. Make sure to add the following line to /etc/gshadow. A group password is not required.

`tg1:!::test1,test2`

3.   Create a directory intended for use by the tg1 group:

![Images](f0242-03.jpg)

4.   Change the user and group ownership of the shared directory:

![Images](f0242-04.jpg)

5.   Log in as user test1\. Navigate to the /home/test1 directory. Run the **umask** command to confirm that files created from this account will have the appropriate permissions. (The output of the **umask** command for regular users such as test1 should be 0022.) If there’s a problem with the home directory or the umask output, you may have made an error earlier in this chapter with user settings. If so, check the **umask** settings in /etc/profile and /etc/bashrc, and repeat Steps 1–5.

6.   Run the **cd /home/testshared** command. What happens?

7.   Now as the root user, set group write permissions on the testshared directory:

`# chmod 770 /home/testshared`

8.   As user test1, navigate back to the /home/testshared directory, and then try to create a file in the new directory. So far, so good.

![Images](f0243-02.jpg)

9.   As the root user, remove all permissions for other users on new files in the /home/testshared directory:

`# chmod o-rwx /home/testshared/*`

10.   Now with the following command, check the ownership on the new file. Do you think other users in the tg1 group can access this file? If in doubt, log in as user test2 and see for yourself.

`$ ls -l`

11.   From the root account, set the SGID bit on the directory:

`# chmod g+s /home/testshared`

(Yes, if you are efficiency minded, you may know that the **chmod 2770 /home/testshared** command combines the effect of this and the previous **chmod** commands.)

12.   Switch back to the test1 account, navigate back to the /home/testshared directory, and create another file. Remove permissions for other users on the newly created file. Check the ownership on the newly created file. Do you think that user test2 can now access this file? (To see for yourself, try it from the test2 account.)

![Images](f0243-06.jpg)

13.   Now log in as the test2 account. Go into the /home/testshared directory. Try accessing the testb.txt file. Create a different file and then use ls -l to check permissions and ownership again. (To see that it worked, try accessing this file from the test1 account.)

14.   Switch to the test3 account and check whether that user can or cannot create files in this directory and whether that user can or cannot view the files in this directory. As expected, the user cannot access the /home/testshared directory because it is not part of the tg1 group.

#### CERTIFICATION SUMMARY

You can manage users and groups with the files of the shadow password suite. These files can be modified directly, with the help of commands such as **useradd** and **groupadd** or the Cockpit web console. The way users are configured is based on the /etc/login.defs file. Any variables or system-wide settings are defined in /etc/bashrc, /etc/profile, and the files in /etc/profile.d/. They can be modified by the .bashrc and .bash_profile files in user home directories.

There are several ways to limit the use of administrative privileges. The ability to log in can be regulated by the file /etc/security/access.conf. Access to the **su** command can be limited with the help of PAM. Partial and complete administrative privileges can be configured for the **sudo** command in the /etc/sudoers file.

By default, Red Hat Enterprise Linux assigns unique user and group ID numbers to each new user. This user private group scheme supports the configuration of special groups for a specific set of users. The users in the group can share and modify each other’s files in a dedicated directory, courtesy of the SGID bit.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 6](#ch06.xhtml).

##### User Account Management

![Images](squ1.jpg)   After installation, a system may have only a single login account: root. For everyday operation, it’s best to create one or more regular accounts.

![Images](squ1.jpg)   The shadow password suite is configured in the /etc/passwd, /etc/shadow, /etc/group, and /etc/gshadow files.

![Images](squ1.jpg)   Administrators can add user and group accounts by directly editing the files of the shadow password suite or with commands such as **useradd** and **groupadd**. The way user accounts are configured is defined by the /etc/login.defs file.

![Images](squ1.jpg)   Accounts can be added with the Cockpit web console.

##### Administrative Control

![Images](squ1.jpg)   Logins can be regulated by the /etc/security/access.conf file.

![Images](squ1.jpg)   Access to the **su** command can be restricted through the /etc/pam.d/su file.

![Images](squ1.jpg)   Custom administrative privileges can be configured in the /etc/sudoers file.

##### User and Shell Configuration

![Images](squ1.jpg)   The home directory for new login accounts is populated from the /etc/skel directory.

![Images](squ1.jpg)   Each user has an environment when logged on to the system, based on /etc/bashrc, /etc/profile, and the scripts in /etc/profile.d/.

![Images](squ1.jpg)   All users have hidden shell configuration files in their home directories, such as .bash_profile and .bashrc.

##### Special Groups

![Images](squ1.jpg)   Red Hat’s user private group scheme configures users with their own unique user and group ID numbers.

![Images](squ1.jpg)   With appropriate SGID permissions, you can configure a shared directory for a specific group of users.

![Images](squ1.jpg)   Setting the SGID bit is easy: run the **chmod g+s** command on the shared directory.

#### Q SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams. There may be more than one answer to many of these questions.

##### User Account Management

**[1.](#ch06.xhtml_ch6ques1)**   What’s the standard minimum user ID number for regular users on Red Hat distributions?

**[2.](#ch06.xhtml_ch6ques2)**   What command creates the user mike with /sbin/nologin as a shell?

##### Administrative Control

**[3.](#ch06.xhtml_ch6ques3)**   What file restricts users’ access?

**[4.](#ch06.xhtml_ch6ques4)**   Which file controls the commands that a user can run with the privileges of root or of another user?

**[5.](#ch06.xhtml_ch6ques5)**   When a regular user uses the **sudo** command to run an administrative command, what password is required?

##### User and Shell Configuration

**[6.](#ch06.xhtml_ch6ques6)**   If you want to add files to every new user account, what directory should you use?

**[7.](#ch06.xhtml_ch6ques7)**   What are the system-wide configuration files associated with the bash shell?

##### Special Groups

**[8.](#ch06.xhtml_ch6ques8)**   What command would set the SGID bit on the /home/developer directory?

**[9.](#ch06.xhtml_ch6ques9)**   What command would set up ownership of the developer group on the /home/developer directory?

**[10.](#ch06.xhtml_ch6ques10)**   What command would add user alpha to the developer group? (This question assumes the alpha user and the developer group already exist and that alpha may belong to groups other than his primary group.)

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for these labs follow the Self Test answers.

#### A SELF TEST ANSWERS

##### User Account Management

**[1.](#ch06.xhtml_r_ch6ques1)**   The minimum user ID number for regular users on Red Hat distributions is 1000.

**[2.](#ch06.xhtml_r_ch6ques2)**   The command **useradd -s /sbin/nologin** creates the user mike with /sbin/nologin as a shell.

##### Administrative Control

**[3.](#ch06.xhtml_r_ch6ques3)**   The file that restricts users’ access is /etc/security/access.conf.

**[4.](#ch06.xhtml_r_ch6ques4)**   The file that controls which commands a user can run with the privileges of root or of another user is /etc/sudoers.

**[5.](#ch06.xhtml_r_ch6ques5)**   When a regular user uses the **sudo** command to run an administrative command, the regular password of that user is required, unless the NOPASSWD directive was specified in /etc/sudoers.

##### User and Shell Configuration

**[6.](#ch06.xhtml_r_ch6ques6)**   To automatically add files to every new user account, you should use the /etc/skel directory.

**[7.](#ch06.xhtml_r_ch6ques7)**   The system-wide configuration files associated with the bash shell are /etc/bashrc, /etc/profile, and the scripts in /etc/profile.d/.

##### Special Groups

**[8.](#ch06.xhtml_r_ch6ques8)**   The command that would set the SGID bit on the /home/developer directory is **chmod g+s /home/developer**. Numeric options such as **chmod 2770 /home/developer** may not be correct, as they go beyond just setting the SGID bit.

**[9.](#ch06.xhtml_r_ch6ques9)**   The command that sets up ownership of the developer group on the /home/developer directory is **chown :developer /home/developer**. Another command (not covered in this chapter) that achieves the same result is **chgrp developer /home/developer**.

**[10.](#ch06.xhtml_r_ch6ques10)**   The command that adds user alpha to the developer group is **usermod -aG developer alpha**. Note that the **-a** command option is required to prevent the user being removed from other supplementary groups not listed in the **usermod** command.

#### LAB ANSWERS

##### Lab 1

While there are several methods available to create new users and groups, they should all come to the same result. In the following steps, you will use the **useradd** and **groupadd** commands to complete the lab tasks.

**1.**   Create the user newguy and make newguy a member of the users group (note that the users group already exists in /etc/group, so there is no need to create this group):

`# useradd -G users newguy`

**2.**   Create the user intern:

`# useradd intern`

**3.**   Set the password of both users to changeme:

![Images](f0247-03.jpg)

**4.**   Create a new group named peons with GID 12345, and make both users members of that group:

![Images](f0247-04.jpg)

Note the **-a** command option with **usermod**. This is required because newguy is a member of the users group. If you don’t pass the **-a** option (append), newguy will be removed from the users group. Alternatively, you can specify all the supplementary groups that newguy is a member of:

![Images](f0248-01.jpg)

##### Lab 2

**1.**   First, create the new user senioradm and assign a password:

![Images](f0248-02.jpg)

**2.**   With respect to **sudo** privileges, you should add the following line in the /etc/sudoers file:

![Images](f0248-03.jpg)

As an alternative to editing the sudoers file (preferably with **visudo**), you could create a new file in the /etc/sudoers.d/ directory and add the new configuration there.

Another valid solution is to make the user a member of the wheel group. In fact, the members of the wheel group can run any command via **sudo**, as configured in this line of /etc/sudoers:

![Images](f0248-04.jpg)

**3.**   To test the result, log in as the senioradm user and run an administrative command, prefaced by **sudo**. For example, try the following command:

![Images](f0248-05.jpg)

Unless you’ve run the **sudo** command in the last few minutes, this action will prompt for a password. Enter the password created for user senioradm. It should list all the firewall zones and their configuration.

##### Lab 3

**1.**   Create the new user junioradm and assign a password:

![Images](f0248-06.jpg)

**2.**   With respect to **sudo** privileges, you should add the following line in the /etc/sudoers file:

![Images](f0248-07.jpg)

As an alternative to editing the sudoers file (preferably with **visudo**), you could create a new file in the /etc/sudoers.d/ directory and add the new configuration there.

**3.**   Run the **fdisk** command via **sudo**:

![Images](f0248-08.jpg)

If successful, you should see a list of partitions for connected drives in the output.

**4.**   Try to run the same command without **sudo**, and notice the difference:

![Images](f0249-01.jpg)

You should get some permission errors.

##### Lab 4

**1.**   This lab specifies “new users,” which implies that you should add the directory to /etc/skel, rather than copying to the home directory of every single user:

![Images](f0249-02.jpg)

**2.**   Test the result by adding a new user named infouser with the **useradd** command:

![Images](f0249-03.jpg)

**3.**   You should find that a /home/infouser directory has been created, with the content of /usr/share/doc/bash in it:

![Images](f0249-04.jpg)

##### Lab 5

**1.**   Create the user account:

![Images](f0249-05.jpg)

**2.**   Run the following command to check when the password for this user account expires:

![Images](f0249-06.jpg)

**3.**   Set the last day that the password was changed to 0 since January 1, 1970\. This will force a password change at the next logon.

![Images](f0249-07.jpg)

**4.**   Set the minimum number of days between password changes and the maximum number of days during which a password is valid for user mike:

![Images](f0249-08.jpg)

**5.**   Again, confirm the new settings for user mike.

**6.**   For the last lab requirement, edit the file /etc/login.defs and set PASS_MAX_DAYS to 30 days:

![Images](f0249-09.jpg)

##### Lab 6

**1.**   Create the testlock user account and lock the password:

![Images](f0250-01.jpg)

In /etc/shadow, you should see an extra single exclamation mark (!) prepended to the password field of user testlock.

**2.**   Test if you can log in as user testlock from a terminal. If you can, open a shell by running **su** as a normal user or as root. From tester1, check if you can open an SSH session as user testlock.

**3.**   Unlock the user’s password and disable the user account by, for instance, setting the expiration date of the account to January 1, 2000:

![Images](f0250-02.jpg)

**4.**   Repeat Step 2.

**5.**   Reenable the user account by setting an empty expiring date, and set user testlock’s login shell to /sbin//nologin:

![Images](f0250-03.jpg)

**6.**   Repeat Step 2.

You should have found that when the user’s password is locked and when the account is disabled, you cannot log in from a terminal or via SSH. Access via **su** is permitted only as root. Therefore, the two methods may seem equivalent. However, when the user’s password is locked, you can still log in to the user account via a password-less authentication method—for example, with SSH key authentication (which is covered in [Chapter 8](#ch08.xhtml)).

Conversely, setting the user’s shell to /sbin/nologin disables SSH access (with password and key authentication), as well as access from a terminal or via **su**. However, the user may still be able to authenticate through a web application, if present, or via other programs that rely on password authentication.

In conclusion, which is the most secure method to disable a user account and ensure that access to the system is disabled? If you do not want to delete the user account, use all of them: lock the user’s password, disable the account, and set the login shell to /sbin/nologin.

##### Lab 7

**1.**   Create user accounts for mike, rick, terri, and maryam by using the **useradd** command:

![Images](f0251-01.jpg)

**2.**   Set up a group for these users. Configure a group ID outside the range of regular users in /etc/group with a line such as this:

![Images](f0251-02.jpg)

**3.**   Create the /home/galley directory. Give it proper ownership and permissions with the following commands:

![Images](f0251-03.jpg)

## Chapter 7

## Storage and Filesystem Administration

CERTIFICATION OBJECTIVES

[7.01     Storage Management and Partitions](#ch07.xhtml_ch7obj01)

[7.02     Filesystem Formats](#ch07.xhtml_ch7obj02)

[7.03     Basic Linux Filesystems and Directories](#ch07.xhtml_ch7obj03)

[7.04     Logical Volume Manager (LVM)](#ch07.xhtml_ch7obj04)

[7.05     Filesystem Management](#ch07.xhtml_ch7obj05)

[7.06     The Automounter](#ch07.xhtml_ch7obj06)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

Linux installation is easy, at least for anyone serious about Red Hat certification. Perhaps the most difficult part during the installation of a system is partitioning and formatting your disk drives. However, most administrators have to maintain existing systems. Hence, disk and filesystem management does not end after the installation of a system.

Critical skills related to storage management include adding new partitions, creating logical volumes, mounting and expanding filesystems, and more. In many cases, you’ll want to make sure these filesystems are mounted automatically during the boot process, and that requires a detailed knowledge of the /etc/fstab configuration file.

INSIDE THE EXAM

Some of the RHCSA objectives listed in this chapter overlap and may be covered in multiple sections. The objectives all relate in some way to filesystem management and should be considered as a whole in this chapter.

**Partition Management**

As in the real world, it is the results that matter. It doesn’t matter whether you use **fdisk** or **parted** to create an MBR-style partition. However, you should know that the Red Hat implementation of **fdisk** now supports GPT partitions, just as **gdisk** and **parted** do. Make sure that appropriate partitions meet the requirements of the exam.

The current RHCSA objectives include the following related requirements:

![Images](square.jpg)   List, create, delete partitions on MBR and GPT disks

![Images](square.jpg)   Add new partitions and logical volumes, and swap to a system non-destructively

**Logical Volumes**

The Logical Volume Manager (LVM) provides a level of abstraction to group and manage partitions and disks in special entities called *volume groups*. On top of a volume group you can create logical volumes, which can be formatted with a filesystem like normal disk partitions. The following RHCSA objectives describe the skills required:

![Images](square.jpg)   Create and remove physical volumes

![Images](square.jpg)   Assign physical volumes to volume groups

![Images](square.jpg)   Create and delete logical volumes

Of course, a logical volume isn’t fulfilling its full potential unless you can increase its size, as suggested by the following objective:

![Images](square.jpg)   Extend existing logical volumes

**Filesystem Management**

Partitions and logical volumes must be formatted before they’re ready to store files. To that end, you need to know how to meet the following RHCSA objectives:

![Images](square.jpg)   Create, mount, unmount, and use vfat, ext4, and xfs file systems

![Images](square.jpg)   Configure systems to mount file systems at boot by universally unique ID (UUID) or label

![Images](square.jpg)   Mount and unmount network file systems using NFS

**The Automounter**

The automounter service, known as autofs, is a tool that initiates automatic mounting of filesystems when they're accessed and dismounts them after they've been inactive for a certain duration. This functionality proves invaluable for network-based file systems, detachable storage mediums, and other assets that aren't required to be constantly mounted.

The associated RHCSA objective is

![Images](square.jpg)   Configure autofs

### CERTIFICATION OBJECTIVE 7.01

### Storage Management and Partitions

While it’s easier to create partitions and logical volumes during the installation process, not every administrator has that privilege. Therefore, you must learn how to create and manage partitions on installed systems. Once configured, a partition or a logical volume can be referred to generically as a *volume*. In Linux, three tools still predominate for administrators who need to create and manage partitions: **fdisk**, **gdisk**, and **parted**. While these tools are primarily applied to local hard disks, they can also be used for other media such as drives attached over a network.

#### Current System State

Before using the **fdisk**, **gdisk**, or **parted** utility to create or modify a partition, do check currently available free space along with currently mounted filesystems. The **df** and **mount** commands make it easy. The example shown in [Figure 7-1](#ch07.xhtml_ch7fig1) illustrates how the **df** command displays the total, used, and available free space on all currently mounted filesystems.

FIGURE 7-1 Disk space usage shown by the df command

![Images](F07-01.jpg)

![Images](job.jpg)

**The terms *filesystem* and *file system* are interchangeable. Both are used in official Linux documentation.**

Note the numbers under the “1K-blocks” column. In this case (except for the temporary filesystems, tmpfs, and devtmpfs), they add up to about 17GiB of allocated space. If the hard drive is larger, unallocated space may be used for another partition. Partitions can be combined with others to configure additional space in volume groups and logical volumes, and that can be useful when you need to expand the space available to appropriate filesystems, such as /home, /tmp, and /var.

![Images](job.jpg)

**Because tmpfs and devtmpfs are temporary filesystems stored in RAM, their contents are removed after a system reboot.**

To print the partition sizes in a more readable format, you can use the **-h** command option, as shown in [Figure 7-2](#ch07.xhtml_ch7fig2). The **-H** command option displays output similar to that of **-h**, but whereas **-H** prints the volume sizes in international units such as KB, MB, and GB, **-h** prints the sizes in KiB (kibibyte), MiB (mebibyte), and GiB (gibibyte).

FIGURE 7-2 Output of the df command in human-readable format

![Images](F07-02.jpg)

This difference in notation was briefly explained in [Chapter 1](#ch01.xhtml). In international units, multiples are expressed in powers of ten. Hence, 1KB = 1000 bytes, 1MB = 1,000,000 bytes, and so on. Conversely, the KiB, MiB, and GiB notation uses powers of two. Therefore, 1KiB = 1024 bytes, 1MiB = 1,048,576 bytes, and so on.

![Images](exam.jpg)

**You must recognize which units of measure to use depending on the context. For example, if you are asked to create a partition of 1GB, that means 1 billion bytes. However, if you are required to create a partition of 1GiB, that is equivalent to 1024 × 1024 × 1024 bytes, or equivalently 1024 × 1024KiB, or 1024MiB, or 1GiB.**

The second command, **mount**, lists the format and mount options for each filesystem. Examine the following output of the partition represented by device /dev/mapper/rhel-home. Note that it is mounted on the /home directory with the xfs file type. The purpose of this filesystem is to separate the home directories of regular users in a dedicated volume.

![Images](f0256-02.jpg)

If the output of the **mount** command confuses you, consider the **findmnt** command, which prints all mounted filesystems in a tree-like format, as shown in [Figure 7-3](#ch07.xhtml_ch7fig3).

FIGURE 7-3 Output of the findmnt command

![Images](F07-03.jpg)

In the output, note the presence of “special filesystems” such as proc and sysfs, which we cover later in this chapter.

#### The fdisk Utility

The **fdisk** utility is common to many operating systems. macOS has a fully featured version of **fdisk**. Older versions of Microsoft Windows have a simplified version of **fdisk**.

Although the Linux implementation of **fdisk** includes a wide variety of commands, you need to know only the few discussed here.

**fdisk** works with partitions created using the traditional Master Boot Record (MBR) partitioning scheme. On newer systems that run UEFI firmware rather than a traditional BIOS, you may see a different partitioning standard: the GUID Partition Table (GPT). Although in earlier releases of RHEL 8 **fdisk** support for GPT was considered experimental, today **fdisk** can handle GPT partitions. Nevertheless, in this chapter, we will demonstrate how to use **gdisk** and **parted** to manage them.

##### Start fdisk: Help and More

The following screen output lists commands that show how to start **fdisk**, how to get help, and how to quit the program. The /dev/sda drive is associated with the first drive on a Linux system, but the name may be different on your machine, such as /dev/nvme0n1 if you have an NVMe drive. As other systems may be configured with different hard drive device files, you may need to check the output from the **df** and **fdisk -l** commands for clues.

![Images](job.jpg)

**An NVMe drive is a type of solid-state drive (SSD) that uses the Non-Volatile Memory Express interface protocol to connect to a computer’s motherboard. NVMe is designed to take advantage of the high-speed capabilities of solid-state storage.**

When you start **fdisk**, type **m** to list basic **fdisk** commands:

![Images](f0258-01.jpg)

A wide variety of commands are associated with **fdisk**—and more if you run the **x** command to access **fdisk**’s extra functionality.

##### Using fdisk: A New Drive with No Partitions

After a new drive is installed on Linux, that drive normally isn’t configured with partitions. The **fdisk** utility can be used to configure partitions on physical or virtual disks attached to the system. For example, the baseline virtual system for this book includes one drive, which may be named /dev/nvme0n1, /dev/sda, or /dev/vda on your system.

![Images](job.jpg)

**SATA, PATA, and SAS SCSI drives are all represented by device files such as /dev/sda, /dev/sdb, and so on.**

If a newly added drive hasn’t been used by the RHEL installation program (or some other disk management program), **fdisk** will return the following message the first time it tries to access the drive:

![Images](f0259-01.jpg)

In other words, even if you don’t create a partition, **fdisk** will automatically write a DOS disk label to the drive if you save your changes.

If you need more than four partitions on the new physical disk, configure the first three partitions as primary partitions, and then configure the fourth partition as an extended partition. That extended partition should typically be large enough to fill the rest of the disk; all logical partitions must fit in that space.

##### Using fdisk: In a Nutshell

At the **fdisk** command-line prompt, start with the print command (**p**) to examine the partition table. This allows you to review the current entries in the partition table. Assuming free space is available, you can then create a new (**n**) partition.

Generally, partitions are either primary (**p**) or logical (**l**). If it doesn’t already exist, you can also create an extended partition (**e**) to contain logical partitions. Remember that in a drive formatted with the MBR scheme, you can have up to four primary partitions, which would correspond to numbers 1 through 4\. One of the primary partitions can be configured as an extended partition. The remaining partitions are logical partitions, numbered 5 and above. With an extended partition, you can create a maximum of 12 logical partitions on a drive.

If free space is available, **fdisk** normally starts the new partition at the first available sector or cylinder. The actual size of the partition depends on disk geometry.

##### Using fdisk: Create a Partition

The following screen output sample shows the steps used to create a new (**n**) partition (**p**), make it bootable (**a**), and then finally write (**w**) the partition information to the disk. (Note that although you may specify a 500MiB partition, the geometry of the disk may not allow that precise size.)

![Images](f0260-01.jpg)

Note how the number of sectors matches the binary representation of 500MiB. Repeat the commands to create any other partitions you might need.

When partitions are added or changed, you generally don’t have to reboot to get Linux to read the new partition table, unless another partition on that drive has been formatted and mounted. If so, an attempt to write the partition table with the **w** command fails temporarily with the following message:

![Images](f0260-02.jpg)

If you run **partprobe /dev/sdb**, the kernel will read the new partition table and you’ll be able to use the newly created partition.

##### Using fdisk: Many Partition Types

One feature of special interest is based on the **t** command to change the partition system identifier. If you need space for logical volumes or even swap space, the **t** command is important. After pressing **t**, you’re prompted to enter the partition number (if there’s more than one configured). You can then list available partition types with the **L** command, as shown here. (If there’s only one partition on the drive, it is selected automatically.)

![Images](f0261-01.jpg)

The list of available partition identifiers, as shown in [Figure 7-4](#ch07.xhtml_ch7fig4), is impressive. Note how it’s not limited to Linux partitions. However, as this book covers Linux, [Table 7-1](#ch07.xhtml_ch7tab1) lists associated partition types.

FIGURE 7-4 Linux partition types in fdisk

![Images](F07-04.jpg)

TABLE 7-1 Linux Partition Types in fdisk

![Images](f0262-01.jpg)

Unless you’re making a change, type in identifier **83**. You’ll be returned to the **fdisk** command prompt.

##### Using fdisk: Delete a Partition

The following example removes the only configured partition. The sample output screen first starts **fdisk**. Then you can print (**p**) the current partition table, delete (**d**) the partition by number (**1** in this case), write (**w**) the changes to the disk, and quit (**q**) from the program. Needless to say, *do not perform this action on any partition where you need the data*.

Assuming only one partition exists on this drive, it is selected automatically after you run the **d** command.

![Images](f0262-02.jpg)

This is the last chance to change your mind before deleting the current partition. To avoid writing the change, exit from **fdisk** with the **q** command. If you’re pleased with the changes that you’ve made and want to make them permanent, proceed with the **w** command:

![Images](f0262-03.jpg)

You should now have an empty hard drive.

![Images](job.jpg)

**If you remove a partition, the partition table on disk is modified to reflect the change, but the actual data on the partition isn’t removed. This means that if you re-create the partition using the same layout (same start/end sectors), your data will still be there. It’s worth trying this procedure in case you accidentally delete a partition by mistake.**

##### Using fdisk: Create a Swap Partition

Now that you know how to create partitions with **fdisk**, just one additional step is required to set up that partition for swap space. Once you have a swap partition of the desired size, run the **t** command to select a partition, and then run the **l** command to show the partition ID types listed in [Figure 7-4](#ch07.xhtml_ch7fig4).

In this case, at the following prompt, type in **82** for a Linux swap partition:

![Images](f0263-01.jpg)

For example, you could run the following sequence of commands to set up a new swap partition on the second hard drive. The details of what you see depend on the partitions you may have created. It’ll be a 900MiB swap space on the first primary partition (/dev/sdb1).

![Images](f0263-02.jpg)

The **fdisk** utility doesn’t actually write the changes to disk until you run the write (**w**) command. Alternatively, you can cancel these changes with the quit (**q**) command. If you don’t see any error messages, the changes are written to disk. As described later in this chapter, additional work is required to configure RHEL to use that newly created swap partition.

#### The gdisk Utility

As illustrated in the previous section, the MBR partitioning scheme supports a maximum of 15 partitions for data (3 primary and 12 logical), plus an extended partition, which is simply a “container” for logical partitions. In contrast, the GPT partitioning scheme can hold up to 128 partitions.

Another limitation of MBR is the disk size. The MBR scheme uses 32-bit logical addresses, which support disk drives up to 2TB. On the other hand, the GPT format relies on 64-bit addresses, which support drives of up to 8 million terabytes!

Although you could use **fdisk** and select the **g** command to switch to a GPT partition table format, the **gdisk** utility was specifically designed for GPT partitions. If you’re familiar with **fdisk**, **gdisk** should seem familiar too. When you start **gdisk** on a disk with an MBR partition table, you will see the following warning:

![Images](f0264-01.jpg)

As suggested by the message, type **q** to exit; otherwise, you may lose any data on your drive. In this case, **gdisk** warned us that our disk was formatted using the MBR partition table, and hence we should rather use **fdisk** to modify the partition layout.

Once started, **gdisk** works in a similar way to **fdisk**. Type the question mark (**?**) to get a list of commands:

![Images](f0264-02.jpg)

![Images](f0265-01.jpg)

The next screen output shows the steps used to create a new 500MiB partition (**n**) on an empty disk device /dev/sdc:

![Images](f0265-02.jpg)

As with **fdisk**, the **gdisk** tool doesn’t write the changes to disk until you type the write (**w**) command. At any time, you can quit the utility without saving any changes with the quit (**q**) command.

#### The parted Utility

The **parted** command is included in GNU Parted and is becoming increasingly popular. It’s an excellent tool developed by the Free Software Foundation. As with **fdisk**, you can use it to create, check, and destroy partitions, but it can do more. You can also use it to resize and copy partitions, as well as the filesystems contained therein. It’s the foundation for multiple GUI-based partition management tools, including GParted and QtParted. For more information, see [www.gnu.org/software/parted](http://www.gnu.org/software/parted).

![Images](job.jpg)

**In some ways, using the** parted **utility may be riskier than using** fdisk**. For example, one of the authors of this book accidentally ran the** mklabel **command from the (parted) prompt on an existing RHEL system. It deleted all existing partitions. Changes were written immediately while** parted **was still running. Fortunately, there was a backup of this virtual system and it could be restored with little trouble.**

During our discussion of **parted**, we’ll proceed from section to section, assuming that **parted** is still open with the following prompt:

`(parted)`

#### Using parted: Starting, Getting Help, and Quitting

The screen output shown in [Figure 7-5](#ch07.xhtml_ch7fig5) lists commands that show how to start the **parted** utility, how to get help, and how to quit the program. In this case, the /dev/sdb drive is associated with the second disk on a Linux system. Your computer may have a different drive name; you can check the output from the **df** and **fdisk -l** commands for clues.

FIGURE 7-5 The parted command options

![Images](F07-05.jpg)

As you can see in [Figure 7-5](#ch07.xhtml_ch7fig5), when **parted** is run, it opens its own command-line prompt. Enter **help** for a list of available commands.

A wide variety of commands are available at the **parted** interface. When compared to **fdisk** and **gdisk**, **parted** can do more in some ways, as you will see in the next sections.

##### Using parted: In a Nutshell

At the **parted** command-line prompt, start with the **print** command to list the current partition table. Assuming sufficient unallocated space is available, you can then make a new (**mkpart**) partition. For more information about **parted** command options, use the **help** command; for example, the following command provides more information about **mkpart**:

![Images](f0267-01.jpg)

If that’s too much information, just run the command. You’ll be prompted for the necessary information.

##### Using parted: A New PC (or Hard Drive) with No Partitions

The first step with any truly new hard drive is to create a partition table. For example, after you add a new hard drive to your virtual RHEL system, just about any command you run in **parted** leads to the following message:

![Images](f0267-02.jpg)

Before you can do anything else with this drive, you need to create a label. As shown from the list of available commands, you can do so with the **mklabel** command. If you type **msdos**, the MBR-style partition scheme will be used. To use the GTP format, type **gpt** at the command prompt:

![Images](f0267-03.jpg)

##### Using parted: Create a New Partition

Now you can create a new partition in **parted** with the **mkpart** command. Naturally, if you have selected the MBR partition scheme, you need to specify the partition type:

![Images](f0267-04.jpg)

For **parted**, we used 1MiB to start the partition at sector 2048\. Although we could have used “0MiB” as the starting point, that would have generated a warning because the partition would have not been properly aligned at the 1MiB boundary for best performance. Note also that we ended the partition at 501MiB, so that its size is exactly 500MiB. Now review the results with the **print** command:

![Images](f0268-01.jpg)

Note that **parted** displays the sizes in the International System of Units; that is, in kB, MB, GB, and so on. To change the default units, run the **unit** command:

![Images](f0268-02.jpg)

![Images](job.jpg)

**The GUI-based tool GParted does support formatting to a wider variety of filesystem formats, even though it is just a “front end” to** parted**. It is available from the EPEL repository, described in [Chapter 4](#ch04.xhtml).**

##### Using parted: Delete a Partition

It’s easy to delete a partition in **parted**. From the (parted) prompt, use the **rm** command to delete the target partition by number.

Of course, before deleting any partition, you should do the following:

![Images](square.jpg)   Save any data you need from that partition.

![Images](square.jpg)   Unmount the partition.

![Images](square.jpg)   Make sure the partition isn’t configured in /etc/fstab, so that Linux doesn’t try to mount it the next time you boot.

![Images](square.jpg)   After starting **parted**, run the **print** command to identify the partition you want to delete, as well as its ID number.

For example, to delete partition /dev/sdb10 from the (parted) prompt, run the following command:

![Images](f0268-03.jpg)

##### Using parted: Create a Swap Partition

Now repeat the process to create a swap partition. If necessary, delete the previously created partition to make room. Make the start of the new partition 1MiB after the end of the previous partition. You can still use the same commands, just substitute the **linux-swap** filesystem type as appropriate:

![Images](f0269-01.jpg)

Review the result with the **print** command:

![Images](f0269-02.jpg)

Now exit from **parted**. To use the swap partition, you need to run **mkswap** and **swapon**:

![Images](f0269-03.jpg)

Now you can format the new regular Linux partition with the **mkfs.xfs** command:

![Images](f0269-04.jpg)

We’ll cover these commands in detail later in this chapter.

##### Using parted: Set Up a Different Partition Type

When a partition is created in **parted**, you can change its type with the **set** command. If you have a hard drive with unused partitions, open it with the **parted** command. For example, the following command opens the second virtual hard drive:

![Images](f0269-05.jpg)

Run the **print** command. The Flags column for existing partitions should be empty. Now you’ll set that flag with the **set** command. From the commands shown here, the flags are set to use that first partition of the second drive as an LVM partition:

![Images](f0270-01.jpg)

Now review the result with the **print** command:

![Images](f0270-02.jpg)

You can use similar steps to configure a partition or a component of a RAID array. It’s also a flag; just substitute **raid** for **lvm** in response to the Flag to Invert prompt just shown. If you’re following along with a RHEL 9 system, first confirm the result. Exit from **parted** and then run the following commands:

![Images](f0270-03.jpg)

You’ll see the **lvm** flag as shown previously from the **parted** command; you’ll see the following confirmation in the output to the **fdisk** command:

![Images](f0270-04.jpg)

If you’ve set up the baseline virtual system described in [Chapter 1](#ch01.xhtml), this is an excellent opportunity to set up partitions as components of LVM volumes. Now that you have the tools, it does not matter whether you use **fdisk**, **gdisk**, or **parted** for this purpose. You can choose to use all the free space. Just be sure to create a partition on more than one hard disk for this purpose to help illustrate the power of logical volumes.

#### Graphical Options

As suggested earlier, excellent graphical front ends are available for disk partitions. The GParted and QtParted options are based on **parted** and are designed for the GNOME and KDE desktop environments, respectively. As they are not available from the Red Hat Network, they are not supported by Red Hat and therefore won’t be available for any Red Hat exams.

One graphical option available for RHEL 9 is known simply as Disk Utility, available from the gnome-disk-utility package. Once appropriate packages are installed, you can open Disk Utility from the command-line interface with the **gnome-disks** command.

The Disk Utility screen shown in [Figure 7-6](#ch07.xhtml_ch7fig6) depicts the baseline virtual machine created in [Chapter 1](#ch01.xhtml); it lists the virtual hard drive, device /dev/nvme0n1, as well as its root and home partitions and the DVD drive.

FIGURE 7-6 The Disk Utility

![Images](F07-06.jpg)

The functionality includes some of the following clickable options from the Settings menu (“gear” icon):

![Images](square.jpg)   **Format Partition** On a drive, sets the MBR- or GPT-style partition formats. On a partition, formats a partition for a number of filesystem formats.

![Images](square.jpg)   **Edit Partition** Sets the partition type, such as Linux swap or Linux LVM.

![Images](square.jpg)   **Edit Filesystem** Sets the filesystem label; labels were commonly used on RHEL 5.

![Images](square.jpg)   **Edit Mount Options** Configures the filesystem mount options, such as mount points and filesystem type.

![Images](square.jpg)   **Create Partition Image** Creates an image file with the content of a drive or partition.

![Images](square.jpg)   **Restore Partition Image** Restores the content of a drive from a partition image.

![Images](square.jpg)   **Benchmark Partition** Allows measurements of read and write performance.

![Images](square.jpg)   **Unmount the Filesystem** Unmounts a filesystem. (This option appears as the “stop” icon.)

![Images](square.jpg)   **Delete Partition** Deletes a partition. (This option appears as the “minus” icon.)

![Images](square.jpg)   **Create Partition** Creates a new partition. (This option appears as the “plus” icon.)

Not all of these options appear in [Figure 7-6](#ch07.xhtml_ch7fig6); for example, the Create Partition option does not appear unless you’ve selected a “free” area of the target hard drive. In addition, you may note that the functionality of the Disk Utility goes beyond mere partitioning.

EXERCISE 7-1

**Work with fdisk and parted**

In this exercise, you’ll work with both the **fdisk** and **parted** utilities. You will work with a new empty drive. For the purpose of this exercise, **fdisk** and **parted** will be used on drive /dev/nvme0n2\. Do save the result of this work. You’ll use it for exercises that follow later in this chapter.

1.   Shut down server1.example.com.

2.   In VMware Workstation Player, select the server1.example.com VM and click Edit Virtual Machine Settings. In the new window that opens, select Add | Hard Disk and click Next.

3.   In the next screen, select NVMe as the Virtual Disk Type and click Next.

4.   In the next screen, leave selected the default setting Create A New Virtual Disk and click Next.

![Images](I07-02.jpg)

5.   A new screen to specify the disk capacity will appear. Select 8.000 in the Maximum Disk Size field to create a new 8GB hard drive, and click Next.

6.   In the next screen, leave the default settings and click Finish, then click Save.

7.   Power on server1.example.com and open a terminal as the root user.

8.   Run the **fdisk -l /dev/nvme0n2** command to review the current status of the /dev/nvme0n2 drive (if your first disk drive has a different device name, substitute with the correct name, such as /dev/sdb or /dev/vdb).

9.   Run the **fdisk /dev/nvme0n2** command.

10.   Run the **p** command to display any previously configured partitions. The drive should be empty.

11.   Create a new partition with the **n** command. Create a primary partition with the **p** command and enter **1** for the partition number.

12.   When presented with a request similar to the following, accept the default of 2048 sectors. It is common to start the first partition at 1MiB (= 2048 sectors) to align the partition with the disk geometry:

`First sector (2048-16777215, default 2048):` **`2048`**

13.   When presented with a request similar to the following, type +2G to create a partition of size 2GiB:

![Images](f0274-01.jpg)

14.   Run the **p** command again to review the result. Run the **w** command to write the result to disk.

15.   Review the result on the /dev/nvme0n2 disk with the **parted /dev/nvme0n2 print** command.

16.   Run **parted** in interactive mode with the **parted /dev/nvme0n2** command.

17.   From the (parted) prompt, run the **print** command to review the current status of partitions.

18.   Type **unit MiB**, then run **print** again. How has the output changed?

19.   Create a new partition with the **mkpart** command. Follow the prompts. Enter **primary** as the partition type and **xfs** as a filesystem type; start the partition at **2049MiB** and end it at **4097MiB**, to create a partition of 2048MiB (4097MiB – 2049MiB = 2048MiB). Run the **print** command to confirm the new partition, and identify the partition number.

20.   Run the **quit** command to exit from **parted**.

21.   Run the **fdisk -l /dev/nvme0n2** command to review the result.

![Images](exam.jpg)

**During the RHCSA exam, you may need to perform simple calculations to find where a partition should end. If your math is rusty, use the** bc **calculator or a Python command line to do math operations.**

### CERTIFICATION OBJECTIVE 7.02

### Filesystem Formats

The number of filesystem types may exceed the number of operating systems. While RHEL can work with many of these formats, the default is XFS. Although many users enable other filesystems such as Btrfs, Red Hat may not support them.

Linux supports a rich variety of filesystems. Except for some old filesystems such as ext2, most filesystems incorporate features such as journal-based transactions, large storage support, delayed allocation, and complex algorithms to optimize read and write performance. In the following sections we split filesystems into two broad categories: standard and journaling. While this is an oversimplification, it is sufficient to categorize the filesystems that are important to Linux.

The filesystems described in this book are just a subset of those that can be configured on a RHEL system. The Linux kernel makes it possible to set up more.

#### Standard Filesystems

Linux is a clone of Unix. The Linux filesystems were developed to mimic the functionality of Unix filesystems available at the time. The first versions of the Linux operating systems used the Extended Filesystem (ext). In the twentieth century, the default filesystem on Red Hat Linux was the Second Extended Filesystem (ext2). Starting with RHEL 5, Red Hat moved to the Third Extended Filesystem (ext3). For RHEL 6, Red Hat progressed to the Fourth Extended Filesystem (ext4). Both ext3 and ext4 are journaling filesystems. Starting with RHEL 7, Red Hat changed the default filesystem to XFS, a highly scalable journaling filesystem initially developed by Silicon Graphics in 1993.

The size of current filesystems has increased the importance of journaling because such filesystems are more resilient to failure. So in general, the non-journaling filesystems described in [Table 7-2](#ch07.xhtml_ch7tab2) are legacy filesystems. Of course, filesystems such as ISO 9660 and swap are still in common use.

TABLE 7-2 Some Standard Filesystems

![Images](f0275-01.jpg)

#### Journaling Filesystems

Journaling filesystems have two main advantages. First, a filesystem check is very fast. Second, if a crash occurs, a journaling filesystem has a log (also known as a journal) that can be used to restore the metadata for the files on the relevant partition.

For RHEL 9, the default filesystem is XFS, a highly scalable, journal-based filesystem. This isn’t the only journaling filesystem option available, however. [Table 7-3](#ch07.xhtml_ch7tab3) lists a few of the options commonly used for RHEL. From this list, Red Hat officially supports only ext3, ext4, and XFS. At the time of writing, Btrfs is no longer supported by Red Hat.

TABLE 7-3 Some Journaling Filesystems

![Images](f0276-01.jpg)

The Red Hat move to XFS is a testament to its use as a server operating system. For example, volumes formatted to XFS can theoretically be as large as 8 exabytes (EB). That’s a serious increase over the maximum size of an ext3 volume: 16 terabytes (TB).

XFS supports a large number of concurrent operations, guarantees space for files, guarantees faster checks, and more. As XFS has been a part of the Linux kernel since 2004, it is proven technology.

#### Filesystem Format Commands

Several commands can help you create a Linux filesystem. They’re all based on the **mkfs** command, which works as a front end to filesystem-specific commands such as **mkfs.ext3**, **mkfs.ext4**, and **mkfs.xfs**.

If you want to reformat an existing partition or logical volume, take the following precautions:

![Images](square.jpg)   Back up any existing data on the partition.

![Images](square.jpg)   Unmount the partition.

There are two ways to format a volume. (As noted earlier in this chapter, *volume* is a generic name that can describe a partition or a logical volume.) For example, if you’ve just created a partition on /dev/sdb5, you can format it to the XFS filesystem by using one of the following commands:

![Images](f0277-01.jpg)

You can format partitions, logical volumes, and RAID arrays to other filesystems. Some of the options available in RHEL 9 include the following:

![Images](square.jpg)   **mkfs.ext2** formats a volume to the ext2 filesystem.

![Images](square.jpg)   **mkfs.ext3** formats a volume to the RHEL 5 default ext3 filesystem.

![Images](square.jpg)   **mkfs.ext4** formats a volume to the RHEL 6 default ext4 filesystem.

![Images](square.jpg)   **mkfs.fat** (or **mkfs.vfat**, **mkfs.msdos**, **mkdosfs**) formats a partition to the Microsoft-compatible FAT filesystem; it does not create bootable filesystems. (All these commands are the same because they are symbolic links to mkfs.fat.)

![Images](square.jpg)   **mkfs.xfs** formats a volume to the RHEL 9 default XFS filesystem.

![Images](square.jpg)   **mkswap** sets up a Linux swap area.

These commands assume you’ve configured an appropriate partition in the first place; for example, before the **mkswap** command can be properly applied to a partition, the Linux swap partition ID type must be configured for that partition. If you’ve created a logical volume, as described later in this chapter, similar rules apply.

#### Swap Volumes

Although Linux can use swap files, the swap space is generally configured in properly formatted partitions or logical volumes. To see the swap space currently configured, run the **cat /proc/swaps** command.

As suggested in the previous section, swap volumes are formatted with the **mkswap** command. But that’s not enough. Swap volumes must also be activated with the **swapon** command. If the new swap volume is recognized, you’ll see it in both the /proc/swaps file and the output to the **top** command. Second, you’ll need to make sure to configure the new swap volume in the /etc/fstab file, as described later in this chapter.

#### Filesystem Check Commands

The **xfs_repair** command (or **fsck** for other filesystems) analyzes the specified XFS filesystem and performs repairs as required. Assume, for example, you’re having problems with files in the /var directory, which happens to be mounted on /dev/sda7. If you want to run **xfs_repair**, unmount that filesystem first. In some cases, you may need to go into rescue mode before you can unmount a filesystem. To unmount, analyze, and then remount the filesystem noted in this section, run the following commands:

![Images](f0278-01.jpg)

The **fsck** command serves as a “front end,” depending on the filesystem format. For example, if you’re formatting an ext2, ext3, or ext4 filesystem, **fsck** by itself automatically calls the **e2fsck** command. In fact, the **fsck.ext2**, **fsck.ext3**, **fsck.ext4**, and **e2fsck** files are all different names for the same command! They have the same inode number. You can confirm this by applying the **ls -i** command to all four files, which are part of the /sbin directory.

EXERCISE 7-2

**Format, Check, and Mount Different Filesystems**

In this exercise, you’ll work with the file format and checking commands **mkfs** and **fsck** and then review the results with the **mount** command. This exercise assumes you’ve completed Exercise 7-1, or at least have unmounted Linux partitions with no data.

1.   Review the current status of partitions on the drive discussed in Exercise 7-1 with the **parted /dev/nvme0n2 print** command. If your first disk drive has a different device name, substitute with the correct name, such as /dev/sdb or /dev/vdb.

2.   Format the partition created by the first drive with the **mkfs.ext2 /dev/nvme0n2p1** command (similarly, if your drive has a different name such as /dev/sdb, the first partition is /dev/sdb1). Review the current status of the volume with the **dumpe2fs -h /dev/nvme0n2p1 | grep features** command. What features do you see in the output? Save the output temporarily. One way to do so is to open a new command-line console. Check the system with the **fsck.ext2 /dev/nvme0n2p1** command.

3.   Mount the newly formatted partition with the **mount /dev/nvme0n2p1 /mnt** command. Review the output with the **mount** command by itself. If the mount and format worked, you’ll see the following output:

`/dev/nvme0n2p1 on /mnt type ext2 (rw,relatime,seclabel)`

4.   Unmount the formatted partition with the **umount /mnt** command.

5.   Run the **mkfs.ext4 /dev/nvme0n2p1** command. You will get a warning that a filesystem is already present on /dev/nvme0n2p1\. Type **y** to format the partition and rerun the **dumpe2fs** command from the previous step. What’s the difference between the output now and the output when the partition was formatted to the ext2 filesystem?

6.   Repeat Steps 3 and 4\. What’s the difference in the output to the **mount** command?

7.   Now on the other partition created in Exercise 7-1, apply the **mkfs.xfs /dev/nvme0n2p2** command. Run the **xfs_info /dev/nvme0n2p2** command. What information is displayed? Execute **man xfs_info** for a description of this command.

8.   Mount the newly formatted partition on the **/mnt** directory and then run the **mount** command by itself. Can you confirm the filesystem type of the /dev/nvme0n2p2 partition from the output of the **mount** command?

### CERTIFICATION OBJECTIVE 7.03

### Basic Linux Filesystems and Directories

“Everything in Linux is a file.” Partitions are associated with *filesystem device nodes* such as /dev/sda1\. Hardware components are associated with node files such as /dev/cdrom. Detected devices are documented as files in the /sys directory. The Filesystem Hierarchy Standard (FHS) is the official way to organize files in Unix and Linux directories. As with the other sections, this introduction provides only the most basic overview of the FHS. More information is available from the official FHS home page at [http://refspecs.linuxfoundation.org/fhs.shtml](http://refspecs.linuxfoundation.org/fhs.shtml).

![Images](job.jpg)

**In Linux, the word *filesystem* has different meanings. It can refer to the FHS or to a filesystem format such as ext3\. A filesystem mount point such as /var represents the directory on which a filesystem can be mounted.**

#### Separate Linux Filesystems

Several major directories are associated with all modern Unix/Linux operating systems. Files, drivers, kernels, logs, programs, utilities, and more are organized in these directories. The way these components are organized on storage media is known as a filesystem. The FHS makes it easier for Linux distributions to adhere to a common directory structure.

Every filesystem starts with the top-level root directory, also known by its symbol, the single forward slash (/). All the other directories shown in [Table 7-4](#ch07.xhtml_ch7tab4) are subdirectories of the root directory. Unless they are mounted separately, you can also find their files on the same partition as the root directory. You may not see some of the directories shown in the table if associated packages have not been installed. Not all directories shown are officially part of the FHS. More importantly, not all listed directories can or should be mounted separately.

TABLE 7-4 Basic Filesystem Hierarchy Standard Directories

![Images](f0280-01.jpg)

![Images](f0281-01.jpg)

The directory on which a filesystem is mounted is known as a *mount point*. While the root directory (/) is the top-level directory in the FHS, the root user’s home directory (/root) is just a subdirectory.

#### Directories That Can Be Mounted Separately

If space is available, several directories listed in [Table 7-4](#ch07.xhtml_ch7tab4) are excellent candidates to be mounted separately. As discussed in [Chapter 1](#ch01.xhtml), it’s typical to mount directories such as /, /boot, /home, /opt, /tmp, and /var on separate volumes. Sometimes, it makes sense to mount lower-level subdirectories on separate volumes, such as /var/ftp for an FTP server or /var/www for a web server.

But first, several directories should always be maintained as part of the top-level root directory filesystem. These directories include /dev, /etc, and /bin. Files within these directories are essential to the smooth operation of Linux as an operating system. Although the same argument can be made for the /boot directory, it is a special case. The storage of the Linux kernel, initial RAM disk, and bootloader files in this directory can help protect the core of the operating system when there are other problems.

Files in the /proc and /sys directories are filled only during the boot process and disappear when a system is shut down, and as such they are stored in a special in-memory virtual filesystem.

Some directories listed in [Table 7-4](#ch07.xhtml_ch7tab4) are designed for use only as mount points. In other words, they should normally be empty. If you store files on those directories, they won’t be accessible if, say, a network share is mounted on them. Typical network mount points include the /media, /mnt, /net, and /smb directories.

### CERTIFICATION OBJECTIVE 7.04

### Logical Volume Manager (LVM)

Logical Volume Manager (also known as LVM) creates an abstraction layer between physical devices, such as disks and partitions, and volumes that are formatted with a filesystem.

LVM can simplify disk management. As an example, assume that the /home filesystem is configured on its own logical volume. If extra space is available on the volume group associated with /home, you can easily resize the filesystem. If no space is available, you can make more room by adding a new physical disk and allocate its storage capacity to the volume group. On LVM, volume groups are like storage pools, and they aggregate together the capacity of multiple storage devices. Logical volumes reside on volume groups and can span multiple physical disks.

#### Definitions in LVM

To work with LVM, you need to understand how partitions configured for that purpose are used. First, with the **fdisk**, **gdisk**, and **parted** utilities, you need to create partitions configured to the LVM partition type. You can also use an entire disk device.

Once those partitions or disk devices are available, they need to be set up as physical volumes (PVs). That process initializes a disk or partition for use by LVM. Then, you create volume groups (VGs) from one or more physical volumes. Volume groups organize the physical storage in a collection of manageable disk chunks known as physical extents (PEs). With the right commands, you can then organize those PEs into logical volumes (LVs). Logical volumes are made of logical extents (LEs), which map to the underlining PEs. You can then format and mount the LVs. For those who are new to LVM, it may be important to break out each definition:

![Images](square.jpg)   **Physical volume (PV)** A PV is a partition or a disk drive initialized to be used by LVM.

![Images](square.jpg)   **Physical extent (PE)** A PE is a small uniform segment of disk space. PVs are split into PEs.

![Images](square.jpg)   **Volume group (VG)** A VG is a storage pool, made of one or more PVs.

![Images](square.jpg)   **Logical extent (LE)** Every PE is associated with an LE, and these PEs can be combined into a logical volume.

![Images](square.jpg)   **Logical volume (LV)** An LV is a part of a VG and is made of LEs. An LV can be formatted with a filesystem and then mounted on the directory of your choice.

You’ll see this process broken down in the following sections. In essence, to create an LV system, you need to create a new PV using a command such as **pvcreate**, assign the space from one or more PVs to a VG with a command such as **vgcreate**, and allocate the space from some part of available VGs to an LV with a command such as **lvcreate**.

To add space to an existing logical volume, you need to add free space from an existing VG with a command such as **lvextend**. If you don’t have any spare space on the VG, you’ll need to add to it with unassigned PV space with a command such as **vgextend**. If all of your PVs are taken, you may need to create a new PV from an unassigned partition or hard drive with the **pvcreate** command.

#### Create a Physical Volume

The first step is to start with a physical partition or a hard disk drive. Based on the discussion earlier in this chapter, you should be able to set up partitions to match the Linux LVM identifier. Then, to set up a new PV on a properly configured partition, such as /dev/sda1, apply the **pvcreate** command to that partition:

`# pvcreate /dev/sda1`

If there is more than one partition to be configured as a PV, the associated device files can all be listed in the same command:

`# pvcreate /dev/sda1 /dev/sda2 /dev/sdb1 /dev/sdb2`

#### Create a Volume Group

From one or more PVs, you can create a volume group. In the following command, substitute the name of your choice for *volumegroup*:

`# vgcreate` *`volumegroup`* `/dev/sda1 /dev/sda2`

You can include additional PVs in any VG. Assuming there are existing PVs based on /dev/sdb1 and /dev/sdb2 partitions, you can add to the *volumegroup* VG with the following command:

`# vgextend` *`volumegroup`* `/dev/sdb1 /dev/sdb2`

However, a new VG isn’t enough since you can’t format or mount a filesystem on it. So you need to create an LV for this purpose.

#### Create a Logical Volume

The following command creates an LV. You can add as many chunks of disk space, in PEs, as you need.

`# lvcreate -l` *`number_of_PEs volumegroup`* `-n logicalvolume`

This creates a device named /dev/*volumegroup/logicalvolume.* You can format this device as if it were a regular disk partition and then mount that new logical volume on a directory.

But this isn’t useful if you don’t know how much space is associated with each PE. You can use the **vgdisplay** command to display the size of the PEs, or specify the size with the **-s** option of the **vgcreate** command when you initialize the VG. Alternatively, you can use the **-L** switch to set a size in MiB, GiB, or another unit of measure. For example, the following command creates an LV named flex of 200MiB:

`# lvcreate -L 200M` *`volumegroup`* `-n flex`

But that’s not the last step, as described next.

#### Make Use of a Logical Volume

You may not get full credit unless the logical volume gets formatted and mounted when the system is rebooted. This process is described later in this chapter in the discussion of the /etc/fstab configuration file.

#### More LVM Commands

A wide variety of LVM commands related to PVs, LVs, and VGs are available. Generally, they are **pv***, **lv***, and **vg*** in the /usr/sbin directory. Physical volume commands include those listed in [Table 7-5](#ch07.xhtml_ch7tab5).

TABLE 7-5 Physical Volume Management Commands

![Images](f0284-02.jpg)

As you assign PVs to VGs, you may need commands to control and configure the VGs. [Table 7-6](#ch07.xhtml_ch7tab6) includes an overview of most related volume group commands.

TABLE 7-6 Volume Group Commands

![Images](f0285-01.jpg)

As you assign PVs to VGs and then subdivide VGs into LVs, you may need commands to control and configure the LVs. [Table 7-7](#ch07.xhtml_ch7tab7) includes an overview of related LVM commands.

TABLE 7-7 Logical Volume Commands

![Images](f0286-01.jpg)

Try the **vgscan** command. You can verify configured VGs with the **vgdisplay** command. For example, [Figure 7-7](#ch07.xhtml_ch7fig7) illustrates the configuration of VG rhel.

FIGURE 7-7 Configuration of a volume group

![Images](F07-07.jpg)

Although a number of **lvm*** commands are installed, just four of them are active: **lvm**, **lvmconfig**, **lvmdiskscan**, and **lvmdump**. Other **lvm*** commands are obsolete. The **lvm** command moves to an lvm> prompt. It’s rather interesting, as the **help** command at that prompt provides a nearly full list of available LVM commands.

The **lvmconfig** command can modify the default settings in the related configuration file, /etc/lvm/lvm.conf. The **lvmdiskscan** command scans all available drives for LVM-configured physical volumes. Finally, the **lvmdump** command sets up a configuration report with diagnostic information.

#### Remove a Logical Volume

The removal of an existing LV is straightforward, with the **lvremove** command. This assumes that any directories previously mounted on LVs have been unmounted. At that point, the basic steps are simple:

1.   Save any data in directories that are mounted on the LV.

2.   Unmount the filesystem associated with the LV. As an example, you can use a command similar to the following:

`# umount /dev/vg_01/lv_01`

3.   Apply the **lvremove** command to the LV with a command such as this:

`# lvremove /dev/vg_01/lv_01`

4.   You should now have the LEs from this LV free for use in other LVs.

#### Resize Logical Volumes

If you need to increase the size of an existing LV, you can add the space from a newly created PV to it. All it takes is appropriate use of the **vgextend** and **lvextend** commands. For example, to add the PEs to the VG associated with a /home directory mounted on an LV, take the following basic steps:

1.   Back up any data existing on the /home directory. (This is a standard precaution that isn’t necessary if everything goes right. You might even skip this step on the Red Hat exams. But do you really want to risk user data in practice?)

2.   Extend the VG to include new partitions configured to the appropriate type. For example, to add /dev/sdd1 to the vg_00 VG, run the following command:

`# vgextend vg_00 /dev/sdd1`

3.   Make sure the new partitions are included in the VG with the following command:

`# vgdisplay vg_00`

4.   Now you can extend the space given to the current LV. For example, to extend the LV to 2000MiB, run the following command:

`# lvextend -L 2000M /dev/vg_00/lv_00`

5.   The **lvextend** command can increase the space allocated to an LV in KiB, MiB, GiB, or even TiB. For example, you could specify a 2GiB LV with the following command:

`# lvextend -L 2G /dev/vg_00/lv_00`

6.   If you prefer to specify the extra space to be added rather than the total space, you can use the syntax in the following example, which adds 1GiB to the logical volume:

`# lvextend -L +1G /dev/vg_00/lv_00`

7.   Resize the formatted volume with the **xfs_growfs** command (or with **resize2fs**, if it is an ext2/ext3/ext4 filesystem). If you’re using the entire extended LV, the command is simple:

`# xfs_growfs /dev/vg_00/lv_00`

8.   Alternatively, you can reformat the LV, using commands described earlier, so the filesystem can take full advantage of the new space—and then restore data from the backup. (If you’ve already successfully resized an LV, *don’t* reformat it. It isn’t necessary and would destroy existing data!)

`# mkfs.xfs -f /dev/vg_00/lv_00`

9.   In either case, you’d finish the process by checking the new filesystem size with the **df** command:

`# df -h`

### CERTIFICATION OBJECTIVE 7.05

### Filesystem Management

Before you can access the files in a filesystem, that filesystem must be mounted on a mount point. Linux normally automates this process using the /etc/fstab configuration file. When Linux goes through the boot process, directories specified in /etc/fstab are mounted on configured volumes, with the help of the **mount** command. Of course, you can run that command with any or all appropriate options, so that’s an excellent place to start this section.

The remainder of this section focuses on options for /etc/fstab. While it starts with the default using the baseline configuration for a standard virtual machine, it includes options to customize that file for local, remote, and removable filesystems.

#### The /etc/fstab File

To look at the contents of the /etc/fstab file, run the **cat /etc/fstab** command. As shown in the example in [Figure 7-8](#ch07.xhtml_ch7fig8), different filesystems are configured on each line.

FIGURE 7-8 Sample /etc/fstab

![Images](F07-08.jpg)

In RHEL 9 the default is to use universally unique IDs (UUIDs) to mount non-LVM filesystems. As you’ll see in the next section, UUIDs can represent a partition, a logical volume, or an entire disk drive. In all cases, volumes should be formatted to the filesystem noted on each line and are mounted on the directory listed in the second column. The advantage of UUIDs and logical volume devices is that they are unique, whereas device names such as /dev/sdb2 may change after a reboot, depending on the order in which the disks are initialized.

But to some extent, UUIDs are beside the point. As shown in [Figure 7-8](#ch07.xhtml_ch7fig8), six fields are associated with each filesystem, described from left to right in [Table 7-8](#ch07.xhtml_ch7tab8). Each field is separated by one or more spaces. You can verify how partitions are actually mounted in the /etc/mtab file, as shown in [Figure 7-9](#ch07.xhtml_ch7fig9). Note the differences, especially the use of the device file in place of UUIDs, and the presence of virtual filesystems such as tmpfs and sysfs, which are discussed later in this chapter.

TABLE 7-8 Description of /etc/fstab by Column, Left to Right

![Images](f0290-01.jpg)

FIGURE 7-9 Sample /etc/mtab

![Images](F07-09.jpg)

When adding a new partition, you could just add the device file associated with the partition or logical volume to the first column.

#### Universally Unique Identifiers in /etc/fstab

In /etc/fstab, note the presence of UUIDs. Every formatted volume has a UUID, a unique 128-bit number. Each UUID represents either a partition, a logical volume, or a RAID array.

To identify the UUID for available volumes, run the **blkid** command with the name of the device as an argument. The output will give the UUID of the device. As an example, to retrieve the UUID of the root LV in the rhel VG, run the following command:

![Images](f0290-02.jpg)

Alternatively, you could use the **xfs_admin** and **dumpe2fs** commands for the XFS and ext2/ext3/ext4 filesystems, respectively; for example, the following command identifies the UUID associated with the noted LV:

![Images](f0290-03.jpg)

As UUIDs are not limited to LVs, you should be able to get equivalent information for a partition from a command such as the following:

![Images](f0291-01.jpg)

Of course, the same is true if you have a configured and formatted ext volume, with a command such as the following:

![Images](f0291-02.jpg)

#### The mount Command

The **mount** command can be used to attach local and network partitions to specified directories. Mount points are not fixed; you can mount a CD drive or even a shared network directory to any empty directory if appropriate ownership and permissions are set. Closely related is the **umount** (not unmount) command, which unmounts selected volumes from associated directories.

First, try the **mount** command by itself. It’ll display all currently mounted filesystems, along with important mount options. For example, the following output suggests that the /dev/mapper/rhel-root volume is mounted on the top-level root directory in read-write mode and formatted to the xfs filesystem:

![Images](f0291-03.jpg)

As suggested earlier, the **mount** command is closely related to the /etc/fstab file. If you’ve unmounted a directory and have made changes to the /etc/fstab file, the easiest way to mount all filesystems currently configured in the /etc/fstab file is with the following command:

![Images](f0291-04.jpg)

However, if a filesystem is already mounted, this command doesn’t change its status, no matter what has been done to the /etc/fstab file. But if the system is subsequently rebooted, the options configured in /etc/fstab are used automatically.

If you’re not sure about a possible change to the /etc/fstab file, it’s possible to test it out with the **mount** command. For example, the following command remounts the volume associated with the /boot directory in read-only mode:

![Images](f0291-05.jpg)

You can confirm the result by rerunning the **mount** command. The following output should reflect the result on the /boot directory:

![Images](f0291-06.jpg)

If you’ve read this book from the beginning, you’ve already seen the **mount** command at work, and even the ISO files associated with downloaded CD/DVD images. To review, the following command mounts the noted RHEL 9 ISO file on the /mnt directory:

![Images](f0292-01.jpg)

#### More Filesystem Mount Options

Many **mount** command options are appropriate for the /etc/fstab file. One option most commonly seen in that file is **defaults**. Although that is the appropriate mount option for most /etc/fstab filesystems, there are other options, such as those listed in [Table 7-9](#ch07.xhtml_ch7tab9). If you want to use multiple options, separate them by commas. Don’t use spaces between options. The list in [Table 7-9](#ch07.xhtml_ch7tab9) is not comprehensive. You can find out more from the mount man page, available with the **man mount** command.

TABLE 7-9 Options for the mount Command and /etc/fstab

![Images](f0292-02.jpg)

#### Virtual Filesystems

This section describes some of the virtual filesystems used by RHEL 9 and listed in /etc/mtab. Here are the most common:

![Images](square.jpg)   **tmpfs** This filesystem is stored in RAM. Data is erased after a system reboot.

![Images](square.jpg)   **devpts** This filesystem relates to pseudo-terminal devices.

![Images](square.jpg)   **sysfs** This filesystem provides dynamic information about system devices. Explore the associated /sys directory. You’ll find a wide variety of information related to the devices and drivers attached to the local system.

![Images](square.jpg)   **proc** This filesystem is especially useful because it provides dynamically configurable options for changing the behavior of the kernel.

![Images](square.jpg)   **cgroup2** This filesystem is associated with the control group feature of the Linux kernel, which allows you to set limits on system resource usage for a process or a group of processes.

#### Add Your Own Filesystems to /etc/fstab

If you need to set up a special directory, it sometimes makes sense to set it up on a separate volume. While it’s nice to follow the standard format of the /etc/fstab file, it is an extra effort. On the RHCSA exam, read carefully the instructions to determine if a new directory needs to be a mount point of a partition.

So, in most cases, it’s sufficient to set up a new volume in /etc/fstab with the associated device file, such as a /dev/sda6 partition, a UUID, or an LVM device such as /dev/mapper/NewVol-NewLV or /dev/NewVol/NewLV. Make sure the device file reflects the new volume you’ve created, the intended mount directory, and the filesystem format you’ve applied (such as xfs).

#### Removable Media and /etc/fstab

In general, removable media should not be mounted automatically during the boot process. Although that’s possible in the /etc/fstab configuration file with an option such as **noauto**, in general, setting up removable media in /etc/fstab is not standard in RHEL.

To read removable media such as smartcards and CD/DVDs, RHEL partially automates the mounting of such media in the GNOME Desktop Environment. Although the details of this process are not part of the RHCSA exam objectives, the process is based on configuration files in the /usr/lib/udev/rules.d directory. If RHEL detects your hardware, click Activities | Files; in the menu that appears, select the entry for the removable media.

If that doesn’t work for some reason, you can use the **mount** command directly. For example, the following command mounts a CD/DVD in a drive:

![Images](f0294-01.jpg)

The **-t** switch specifies the type of filesystem (iso9660). The device file /dev/sr0 represents the first CD/DVD drive; /mnt is the directory through which you can access the files from the CD/DVD after mounting. But /dev/sr0? How is anyone supposed to remember that?

Fortunately, Linux addresses this in a couple of ways. First, it sets up links from more sensibly named files such as /dev/cdrom, which you can confirm with the **ls -l /dev/cdrom** command. Second, it provides the **blkid** command. Try it. If removable media (other than a CD/DVD) is connected, you’ll see it in the output to the command, including the associated device file.

Just remember that it is important to unmount removable media such as USB keys before removing them. Otherwise, the data you thought was written to the disk might still be in the unwritten RAM cache. In that case, you would lose that data.

Given these examples of how removable media can be mounted, you should have a better idea of how such media can be configured in the /etc/fstab configuration file. The standard **defaults** option is inappropriate in most cases because it mounts a system in read-write mode (even for read-only DVDs), attempts to mount automatically during the boot process, and limits access to the root administrative user. But that can be changed with the right options. For example, to configure a CD drive that can be mounted by regular users, you could add the following line to /etc/fstab:

![Images](f0294-02.jpg)

This line sets up a mount in read-only mode, does not try to mount it automatically during the boot process, and supports access by regular users.

As desired, similar options are possible for removable media such as USB keys, but that can be more problematic with multiple USB keys; for example, one may be detected as /dev/sdc once, and then later detected as /dev/sdd, if there’s a second USB key installed. However, if properly configured, each USB key should have a unique UUID. There’s another option: rather than using static mounts for removable devices, you can rely on the automounter, as we will illustrate later in this chapter.

#### Network Filesystems

The /etc/fstab file can be used to automate mounts from network filesystems. The two major sharing services of interest are NFS and Samba. This section provides only a brief overview as to how such filesystems can be configured in the /etc/fstab file; to get some practice with the configurations described in this section, see the labs at the end of the chapter.

In general, network shares are subjected to more reliability issues than direct-attached storage. The settings in the /etc/fstab file should account for that. So if there’s a problem in the network connection or perhaps a problem such as a power failure on the remote NFS server, you can specify how you want the client to behave.

A connection to a shared NFS directory is based on its hostname or IP address, along with the full path to the directory on the server. So to connect to a remote NFS server on system *server1* that shares the /pub directory, you could mount that share with the following command (assuming the /share directory exists):

![Images](f0295-01.jpg)

Some common mount options are shown in the following /etc/fstab entry:

![Images](f0295-02.jpg)

The **rsize** and **wsize** variables determine the maximum size (in bytes) of the data to be read and written in each request. Normally, these should not be required, because the client and server should be able to negotiate the largest values that they both support. The **hard** directive specifies that the client will retry failed NFS requests indefinitely, blocking client requests potentially until the NFS server becomes available. Conversely, the **soft** option will cause the client to fail after a predefined number of retransmissions, but at the cost of risking the integrity of the data. If the connection is to an NFS version 4 server, substitute **nfs4** for **nfs** in the third column.

You can configure some NFS client and server settings in /etc/nfs.conf. An excerpt of this file is shown in [Figure 7-10](#ch07.xhtml_ch7fig10). For example, to enable only NFSv4 and disable v2 and v3, set the following configuration parameters in /etc/nfs.conf:

FIGURE 7-10 Sample /etc/nfs.conf

![Images](F07-10.jpg)

![Images](f0295-03.jpg)

### CERTIFICATION OBJECTIVE 7.06

### The Automounter

With network mounts and portable media, problems may come up if connections are lost or media is removed. During the server configuration process, you could be mounting filesystems from a number of remote systems. You may also want temporary access to removable media such as USB keys. The automount daemon, also known as the automounter or **autofs**, can help. It can automatically mount a specific filesystem as needed. It can unmount a filesystem automatically after a fixed period of time.

#### Mounting via the Automounter

Once a partition is mounted manually with the **mount** command or via /etc/fstab, it stays mounted until you unmount it or shut down the system. The permanence of the mount can cause problems. For example, if you’ve mounted a USB key and then physically removed the key, Linux may not have had a chance to write the file to the disk. Data would be lost. The same issue applies to Secure Digital (SD) cards or other hot-swappable removable drives.

Another issue: mounted NFS filesystems may cause problems if the remote host fails or the connection is lost. Systems may slow down or even hang as the local system looks for the mounted directory.

This is where the automounter can help. It relies on the **autofs** daemon to mount configured directories as needed on a temporary basis. In RHEL, the relevant configuration files are auto.master, auto.misc, auto.net, and auto.smb, all in the /etc directory. If you use the automounter, keep the /misc and /net directories free. Red Hat configures automounts on these directories by default, and they won’t work if local files or directories are stored there. The following subsections will cover each of these files.

![Images](job.jpg)

**You won’t even see the /misc and/or /net directories unless you properly configured /etc/auto.master and the** autofs **daemon is running.**

##### /etc/auto.master

The standard /etc/auto.master file includes a series of directives, with four uncommented lines by default. The first refers to the /etc/auto.misc file as the configuration file for the /misc directory. The **/net -hosts** directive allows you to specify the host to automount a network directory, as specified in /etc/auto.net.

![Images](f0296-01.jpg)

In any case, these directives point to configuration files for each service. Shared directories from each service are automatically mounted on demand on the given directory (/misc and /net).

You can set up the automounter on other directories. One popular option is to set up the automounter on the /home directory. In this way, you can configure user home directories on remote servers mounted on demand.

![Images](f0297-01.jpg)

This works only if a /home directory doesn’t already exist on the local system. As the RHCSA exam requires the configuration of a number of regular users, your systems should include a /home directory for regular users. In that case, you could substitute a different directory, leading to a line such as the following:

![Images](f0297-02.jpg)

Just remember, for any system accessed over a network, you’ll need to be sure that the firewall allows traffic associated with the given service.

##### /etc/auto.misc

Red Hat conveniently provides standard automount directives in comments in the /etc/auto.misc file. It’s helpful to analyze this file in detail. We use the default RHEL version of this file. The first four lines are comments, which we skip. The first directive is

![Images](f0297-03.jpg)

In RHEL, this directive is active by default, assuming you’ve activated the **autofs** service. In other words, if you have a CD in the /dev/cdrom drive, you can access its files through the automounter with the **ls /misc/cd** command, even as a regular user. The automounter accesses it using the ISO 9660 filesystem. It’s mounted read-only (**ro**), set owner user ID permissions are not allowed (**nosuid**), and device files on this filesystem are not used (**nodev**).

A number of other directives are commented out, ready for use. Of course, you would have to delete the comment character (#) before using any of these configuration lines, and you’d have to adjust names and device files accordingly; for example, /dev/hda1 is no longer used as a device name on the latest Linux systems.

As suggested by one of the comments, “The following entries are samples to pique your imagination.” The first of these commented lines allows you to set up a /misc/linux mount point from a shared NFS directory, /pub/linux, from the ftp.example.org host:

![Images](f0297-04.jpg)

The next line assumes that a filesystem is stored on the /dev/hda1 partition. With this directive, you can automount the filesystem in /misc/boot.

![Images](f0297-05.jpg)

The following three lines apply to a floppy disk drive. Don’t laugh; virtual floppies are fairly easy to create and configure on most virtual machine systems. The first directive, set to an “auto” filesystem type, searches through /etc/filesystems to try to match what’s on your floppy. The next two directives assume that the floppy is formatted to the ext2 filesystem.

![Images](f0298-01.jpg)

The next line points to the first partition on the third SCSI drive. The **jaz** at the beginning suggests this is suitable for an old Iomega-type Jaz drive.

![Images](f0298-02.jpg)

Finally, the last command is based on an older system where the automounter is applied to a legacy PATA drive. Of course, the /dev/hdd device file is no longer used, so substitute accordingly. But **removable** at the beginning suggests this is also suitable for removable hard drives. Of course, you’d likely have to change the filesystem format to something like XFS. As suggested earlier in this chapter, the **blkid** command can help identify available device files from removable systems such as USB keys and portable drives.

![Images](f0298-03.jpg)

In general, you’ll need to modify these lines for available hardware.

##### /etc/auto.net

With the /etc/auto.net configuration script, you can review and read shared NFS directories. It works with the hostnames or IP addresses of NFS servers. By default, executable permissions are enabled on this file.

Assuming the automounter is active and can connect to an NFS server with an IP address of 172.16.0.100, you can review shared NFS directories on that system with the following command:

![Images](f0298-04.jpg)

This output indicates that the /srv/ftp directory on the 172.16.0.100 system is shared via NFS. Based on the directives in /etc/auto.master, you could access this share (assuming appropriate firewall and SELinux settings) with the following command:

![Images](f0298-05.jpg)

##### /etc/auto.smb

One of the problems associated with the configuration of a shared Samba or CIFS directory is that it works, at least in its standard configuration, only with public directories. In other words, if you activate the /etc/auto.smb file, it’ll only work with directories shared without a username or a password.

If you accept these unsecure conditions, it’s possible to set up the /etc/auto.smb file in the same way as the /etc/auto.net file. First, you’d have to add it to the /etc/auto.master file in a similar fashion, with the following directive:

![Images](f0299-01.jpg)

You’d then need to specifically restart the automounter service with the following command:

![Images](f0299-02.jpg)

You’d then be able to review shared directories with the following command; substitute a hostname or IP address if desired. Of course, this won’t work unless the Samba server is activated on the noted server1.example.com system and the firewall is configured to allow access through associated TCP/IP ports.

![Images](f0299-03.jpg)

##### Activate the Automounter

Once appropriate files have been configured, you can start, restart, or reload the automounter. As it is governed by the **autofs** daemon, you can stop, start, restart, or reload that service with one of the following commands:

![Images](f0299-04.jpg)

With the default command in the /etc/auto.misc file, you should now be able to mount a CD on the /misc/cd directory automatically, just by accessing the configured directory. Once you have a CD in the drive, the following command should work:

![Images](f0299-05.jpg)

EXERCISE 7-3

**Configure the Automounter**

In this exercise, you’ll test the automounter. You’ll need a DVD ISO image, such as the RHEL 9 DVD. First, however, you need to make sure that the **autofs** daemon is in operation, modify the appropriate configuration files, and then restart **autofs**. You can then test the automounter in this lab.

1.   Check that the autofs RPM package is installed on server1.example.com. If not, run

`# dnf install autofs`

2.   From the command-line interface, run the following command to make sure the **autofs** daemon is running:

`# systemctl start autofs`

3.   Review the /etc/auto.master configuration file in a text editor. The defaults are sufficient to activate the configuration options in /etc/auto.misc and /etc/auto.net.

4.   Check the /etc/auto.misc configuration file in a text editor. Make sure it includes the following line (which should already be there by default). Save and exit from /etc/auto.misc.

![Images](f0300-03.jpg)

5.   Reload the **autofs** daemon. Since it’s already running, all you need to do is make sure it rereads associated configuration files.

![Images](f0300-04.jpg)

6.   The automounter service is now active. Insert a CD or DVD into an appropriate drive and run the following command. If successful, it should display the contents of the CD or DVD:

![Images](f0300-05.jpg)

7.   Run the **ls /misc** command immediately. You should see the CD directory in the output.

8.   Wait at least five minutes and then repeat the previous command. What do you see?

![Images](f0301-01.jpg)

#### CERTIFICATION SUMMARY

As a Linux administrator, you should know how to create and manage new filesystem volumes. To create a new filesystem, you need to know how to create, manage, and format partitions as well as how to set up those partitions for logical volumes.

RHEL 9 also supports the configuration of logical volumes. The process may seem a bit intricate, as it requires the configuration of a partition as a physical volume. One or more PVs can then be configured as a volume group. Logical volumes can then be configured from desired portions of a VG. Associated commands are **pv***, **vg***, and **lv***; those and others can be accessed from the lvm> prompt.

Linux supports the format of partitions and logical volumes to a wide variety of filesystems. Although the default is XFS, Linux supports several regular and journaling filesystems types, including filesystems available on Microsoft and other operating systems.

Once configured, partitions and logical volumes, whether encrypted or not, can be added to the /etc/fstab file. That configuration is read during the boot process and can also be used by the **mount** command. If desired, removable filesystems and shared network directories can also be configured in /etc/fstab.

The /etc/fstab file is not the only option to set up mounts. You can automate this process for regular users with the automounter. Properly configured, it allows users to access shared network directories, removable media, and more through paths defined in /etc/auto.master.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 7](#ch07.xhtml).

##### Storage Management and Partitions

![Images](squ1.jpg)   **fdisk**, **gdisk**, and **parted** can be used to configure partitions for filesystems and logical volumes.

![Images](squ1.jpg)   Disks can use the traditional MBR-style partitioning scheme, which supports primary, extended, and logical partitions, or the GPT scheme, which supports up to 128 partitions.

##### Filesystem Formats

![Images](squ1.jpg)   Linux tools can be used to configure and format volumes to a number of different filesystems.

![Images](squ1.jpg)   Examples of standard filesystems include MS-DOS and ext2.

![Images](squ1.jpg)   Journaling filesystems, which include logs that can restore metadata, are more resilient; the default RHEL 9 filesystem is XFS.

![Images](squ1.jpg)   RHEL 9 supports a variety of **mkfs.*** filesystem format-check commands and **fsck.*** filesystem-check commands.

##### Basic Linux Filesystems and Directories

![Images](squ1.jpg)   Linux files and filesystems are organized into directories based on the FHS.

![Images](squ1.jpg)   Some Linux directories are well suited to configuration on separate filesystems.

##### Logical Volume Manager (LVM)

![Images](squ1.jpg)   LVM is based on physical volumes, logical volumes, and volume groups.

![Images](squ1.jpg)   You can create and add LVM systems with a wide variety of commands, starting with **pv***, **lv***, and **vg***.

![Images](squ1.jpg)   The space from new partitions configured as PVs can be allocated to existing volume groups with the **vgextend** command; they can be added to LVs with the **lvcreate** and **lvextend** commands.

![Images](squ1.jpg)   Extra space on a partition can be used to extend an existing XFS filesystem with the **xfs_growfs** command.

##### Filesystem Management

![Images](squ1.jpg)   Standard filesystems are mounted as defined in /etc/fstab.

![Images](squ1.jpg)   Filesystem volumes are usually identified by their UUIDs; for a list, run the **blkid** command.

![Images](squ1.jpg)   The **mount** command can either use the settings in /etc/fstab or mount filesystem volumes directly.

![Images](squ1.jpg)   It’s also possible to configure mounts of shared filesystems from NFS and Samba servers in /etc/fstab.

##### The Automounter

![Images](squ1.jpg)   With the automounter, you can configure automatic mounts of removable media and shared network drives.

![Images](squ1.jpg)   Key automounter configuration files are auto.master and auto.misc, in the /etc directory.

#### Q SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. Getting results, not memorizing trivia, is what counts on the Red Hat exams. There may be more than one correct answer to many of these questions.

##### Storage Management and Partitions

**[1.](#ch07.xhtml_ch7ques1)**   What **fdisk** command option lists configured partitions from all attached hard drives?

**[2.](#ch07.xhtml_ch7ques2)**   After a swap partition has been created, what command activates it?

##### Filesystem Formats

**[3.](#ch07.xhtml_ch7ques3)**   What is the primary advantage of a journaling filesystem such as XFS?

**[4.](#ch07.xhtml_ch7ques4)**   What command formats /dev/sdb3 to the default Red Hat filesystem format?

##### Basic Linux Filesystems and Directories

**[5.](#ch07.xhtml_ch7ques5)**   What filesystem is mounted on a directory separate from the top-level root directory in the default RHEL 9 installation?

**[6.](#ch07.xhtml_ch7ques6)**   Name two directories just below / that are not suitable for mounting separately from the volume with the top-level root directory.

##### Logical Volume Manager (LVM)

**[7.](#ch07.xhtml_ch7ques7)**   Once you’ve created a new partition and set it to the Logical Volume Manager type, what command adds it as a PV?

**[8.](#ch07.xhtml_ch7ques8)**   Once you’ve added more space to an LV, what command would expand the underlining XFS filesystem to fill the new space?

##### Filesystem Management

**[9.](#ch07.xhtml_ch7ques9)**   To change the mount options for a local filesystem, what file would you edit?

**[10.](#ch07.xhtml_ch7ques10)**   What would you add to the /etc/fstab file to set up access to the ext4 filesystem /dev/sda6, mounted on the /usr directory as read-only with other default options? Assume you can’t find the UUID of /dev/sda6\. Also assume a dump value of 1 and a filesystem check order of 2.

##### The Automounter

**[11.](#ch07.xhtml_ch7ques11)**   If you’ve started the **autofs** daemon and want to read the list of shared NFS directories from the server1.example.com computer, what automounter-related command would you use?

**[12.](#ch07.xhtml_ch7ques12)**   Name the configuration files associated with the default installation of the automounter on RHEL 9.

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for each lab follow the Self Test answers.

#### A SELF TEST ANSWERS

##### Storage Management and Partitions

**[1.](#ch07.xhtml_r_ch7ques1)**   The **fdisk** command option that lists configured partitions from all attached hard drives is **fdisk -l**.

**[2.](#ch07.xhtml_r_ch7ques2)**   After creating a swap partition, you can use the **mkswap *devicename*** and **swapon *devicename*** commands to initialize and activate the volume; just substitute the device file associated with the volume (such as /dev/sda1 or /dev/VolGroup00/LogVol03) for ***devicename***.

##### Filesystem Formats

**[3.](#ch07.xhtml_r_ch7ques3)**   The primary advantage of a journaling filesystem such as XFS is faster data recovery.

**[4.](#ch07.xhtml_r_ch7ques4)**   The command that formats /dev/sdb3 to the default Red Hat filesystem format is **mkfs.xfs /dev/sdb3**. The **mkfs -t xfs /dev/sdb3** command is also an acceptable answer.

##### Basic Linux Filesystems and Directories

**[5.](#ch07.xhtml_r_ch7ques5)**   The /boot filesystem is mounted separately from /.

**[6.](#ch07.xhtml_r_ch7ques6)**   There are many correct answers to this question; some of the directories not suitable for mounting separately from / include /bin, /dev, and /etc. (In contrast, several directories are essentially shown as placeholders for mounting, including /media and /mnt.)

##### Logical Volume Manager (LVM)

**[7.](#ch07.xhtml_r_ch7ques7)**   Once you’ve created a new partition and set it to the Logical Volume Manager file type, the command that adds it as a PV is **pvcreate**. For example, if the new partition is /dev/sdb2, the command is **pvcreate /dev/sdb2**.

**[8.](#ch07.xhtml_r_ch7ques8)**   Once you’ve added more space to an LV, the command that would expand the underlining XFS filesystem to fill the new space is **xfs_growfs**.

##### Filesystem Management

**[9.](#ch07.xhtml_r_ch7ques9)**   To change the mount options for a local filesystem, edit /etc/fstab.

**[10.](#ch07.xhtml_r_ch7ques10)**   Since the UUID is unknown, you’ll need to use the device file for the volume (in this case, /dev/sda6). Thus, the line to be added to /etc/fstab is

![Images](f0305-01.jpg)

##### The Automounter

**[11.](#ch07.xhtml_r_ch7ques11)**   If you’ve started the **autofs** daemon and want to read the list of shared NFS directories from the first.example.com computer, the automounter-related command you’d use to list those directories is **/etc/auto.net server1.example.com**.

**[12.](#ch07.xhtml_r_ch7ques12)**   The configuration files associated with the default installation of the automounter include auto.master and auto.misc, all in the /etc directory.

#### LAB ANSWERS

##### Lab 1

This lab assumes that the new drive is available as /dev/sdb. Substitute accordingly if the device has a different name.

**1.**   Run **parted /dev/sdb**. Create the new partition with the following command:

![Images](f0306-01.jpg)

Note that the filesystem starts at 1MiB. What happens if you enter 0MiB?

**2.**   Type **print** to show the partition table on the drive. Exit from **parted** by typing **q**.

**3.**   Format the new filesystem:

`# mkfs.xfs /dev/sdb1`

**4.**   Create the directory mount point:

`# mkdir /test1`

**5.**   Find the UUID of the device:

`# blkid /dev/sdb1`

**6.**   Add the following line to /etc/fstab (substitute the UUID with the one that you obtained from the **blkid** command):

`UUID="629e809f-2e6d-474c-bc2d-a96121cd1e21" /test1 xfs defaults 0 0`

**7.**   Run **mount -a** to mount the filesystem. Confirm that the filesystem is mounted with the **df** command.

**8.**   To test that the configuration persists after a reboot, create some files in the /test1 directory. Reboot the system and list the content of /test1\. Do you see the files that you have created?

**9.**   The second part of the lab is similar, but requires you to use **fdisk** rather than **parted**. Run **fdisk /dev/sdb**. Create a new (**n**) primary (**p**) partition whose number is **2**. Accept the default for the first sector and enter **+1G** for the last sector. Tag the partition (**t**) with code **82**. Show the partition table (**p**), save the changes (**w**), and exit (**q**).

**10.**   Format and activate the new swap partition:

![Images](f0307-01.jpg)

**11.**   Find the UUID of the device:

![Images](f0307-02.jpg)

**12.**   You should be able to confirm the configuration of a new swap partition in the output to the **cat /proc/swaps** command. You should also be able to verify the result in the **Swap** line associated with the **top** command, as well as in the output of the **free -h** command.

**13.**   Add the following line to /etc/fstab (substitute the UUID with the one that you obtained from the **blkid** command):

![Images](f0307-03.jpg)

**14.**   Remember, when taking the exam, all changes should survive a reboot. For the purpose of this lab, reboot the system to confirm this. However, reboots take time; if you have multiple tasks during an exam, you may want to wait until completing as much as possible before rebooting a system.

##### Lab 2

This lab assumes that you have spare space on the /dev/sdb drive to create the new partition and physical volume. Even if you’ve configured the exact spare partitions described in this lab and followed exact instructions, it’s quite possible that your LV won’t be exactly 900MiB. Some of that variance comes from the differences between units of measure that rely on base 2 or base 10 numbers. Don’t panic; that variance is normal. The same proviso applies to Lab 3 as well.

**1.**   Create the new partition for the PV. Run **fdisk /dev/sdb**. Create a new (**n**) primary (**p**) partition. Accept the default for the first sector and enter **+1G** for the last sector. Tag the partition (**t**) with code **8e**. Show the partition table (**p**), save the changes (**w**), and exit (**q**).

**2.**   Create the physical volume:

![Images](f0307-04.jpg)

**3.**   Create the volume group:

![Images](f0307-05.jpg)

**4.**   Create and format the logical volume:

![Images](f0307-06.jpg)

**5.**   To verify the UUID of the newly formatted volume, run the following command:

![Images](f0308-01.jpg)

**6.**   Add the following line to /etc/fstab (substitute the UUID with the one that you obtained from the **blkid** command):

![Images](f0308-02.jpg)

**7.**   Create the /test2 directory:

![Images](f0308-03.jpg)

**8.**   If the /etc/fstab file is properly configured, you should be able to run the **mount -a** command. Then the **df** command should show the logical volume mounted on the /test2 directory.

**9.**   As with Lab 1, all changes should survive a reboot. At some point, you’ll want to reboot the local system to check for success or failure of this and other labs.

##### Lab 3

Based on the information from Lab 2, you should already know what the size of the current LV is. The associated **df** command should confirm the result; the **df -m** command, with its output in MB, could help.

The key commands in this lab are **lvextend** and **xfs_growfs**. While there are a number of excellent command options available, all you really need with either command is the device file for the LV:

![Images](f0308-04.jpg)

As with Lab 2, the result can be confirmed after appropriate **mount** and **df** commands. However, to ensure that no data has been lost during the process, you could create some test files before resizing the LV and the filesystem.

##### Lab 4

There are several steps associated with this lab:

**1.**   Ensure that all the partitions and volumes created in the previous labs have been unmounted, eliminated from /etc/fstab, and removed (with **{lv,vg,pv}remove**).

**2.**   You don’t need to partition the /dev/sdb and /dev/sdc drives. It is sufficient to initialize the entire drives as PVs, using the **pvcreate /dev/sdb** and **pvcreate /dev/sdc** commands.

**3.**   Run the **vgcreate -s 2M vg01 /dev/sdb /dev/sdc** command to create the VG.

**4.**   Create the LV with the **lvcreate -l 800 -n lv01 vg01** command.

**5.**   Format the filesystem with the **mkfs.ext4 /dev/vg01/lv01** command.

**6.**   Add the correct entry to /etc/fstab.

**7.**   Create the mount point (**mkdir /test4**).

If the /etc/fstab file is properly configured, you should be able to run the **mount -a** command. Then you should see /dev/mapper/vg01-lv01 mounted on the /test4 directory.

##### Lab 5

The configuration of the automounter on a shared NFS directory is easier than it looks. Before you begin, make sure the shared NFS directory is available from the remote computer with the **showmount -e *remote_ipaddr*** command, where *remote_ipaddr* is the IP address of the remote NFS server. If that doesn’t work, you may have skipped a step described in the lab.

As for the automounter configuration, there are two approaches. You could modify the following commented sample NFS configuration directive. Of course, you’d have to at least change ftp.example
.org to the name or IP address of the NFS server and /pub/linux to /tmp (or whatever is the name of the directory being shared).

![Images](f0309-01.jpg)

Alternatively, you could just directly take advantage of the **/etc/auto.net** script. For example, if the remote NFS server is on IP address 172.16.0.100, run the following command:

![Images](f0309-02.jpg)

You should see the /tmp directory shared in the output. If so, you’ll be able to access it more directly with the following command:

![Images](f0309-03.jpg)

If you really want to learn how to use the automounter, try modifying the aforementioned directive in the /etc/auto.misc configuration file. Assuming the automounter is already running, you can make sure the automounter rereads the applicable configuration files with the **systemctl reload autofs** command.

If you use the same first directive in the aforementioned line, you’ll be able to use the automounter to access the same directory with the **ls /misc/linux** command.

## Chapter 8

## Linux Security

CERTIFICATION OBJECTIVES

[8.01     Basic Firewall Control](#ch08.xhtml_ch8obj01)

[8.02     Securing SSH with Key-Based Authentication](#ch08.xhtml_ch8obj02)

[8.03     A Security-Enhanced Linux Primer](#ch08.xhtml_ch8obj03)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

Linux security has been based on a concept known as discretionary access control (DAC). In the DAC model, access to “objects,” such as file and directories, is discretionary because it is controlled by the owner of the objects. Hence, the standard permissions and ownership associated with files and directories is an implementation of DAC.

Then, the U.S. National Security Agency (NSA) developed SELinux, which is an implementation of a different kind of security architecture, known as mandatory access control (MAC). MAC differs significantly from DAC. Red Hat expects you to work with SELinux enabled during exams. In this chapter, you will examine how to set enforcing and permissive modes, change file contexts, use boolean settings, and diagnose SELinux policy violations.

Also in the realm of security, the firewall is a crucial component. In this chapter, you’ll examine **firewalld**, which provides support for different trust zones. You will learn how to allow or block services through **firewalld** using the **firewall-config** graphical utility and the **firewall-cmd** command-line tool.

A service that is installed on most Linux systems is SSH. As it is a very common service for logging in to a machine, it is also a crucial service for security. So this chapter also describes how you can improve security by using key-based authentication for SSH.

If you’re starting with the default installation created during the installation process, you may need to install additional packages during this chapter. For example, if the GUI-based firewall configuration tool is missing, you’ll need to install it with the following command:

`# dnf install firewall-config`

For more information on the package installation process, see [Chapter 4](#ch04.xhtml).

INSIDE THE EXAM

**Basic Firewall Control**

**firewalld** is a feature-rich, zone-based stateful firewall that you can use to block or accept traffic to remote network services. The related RHCSA objectives are

![Images](square.jpg)   Configure firewall settings using firewall-cmd/firewalld

![Images](square.jpg)   Restrict network access using firewall-cmd/firewall

**The Secure Shell Server**

As suggested in the introduction, the SSH service is given special focus in this chapter because, as a common service for logging in to a machine, securing it is crucial. The related RHCSA objective is

![Images](square.jpg)   Configure key-based authentication for SSH

With key-based authentication, you’ll be able to log in to remote systems by using private/public key pairs. Password transmission over the network would no longer be required. The 1024 or more bits associated with such authentication keys are a lot harder to guess than a standard password.

**Security-Enhanced Linux**

There’s no way around it. On the Red Hat exams, you’re expected to work with SELinux. It’s not clear whether you can even pass the Red Hat exams unless you configure at least some services with SELinux in mind. To help exam candidates understand what’s needed, Red Hat has broken down SELinux-related objectives. The first objective is fundamental to SELinux, as it relates to the three modes available for SELinux on a system (enforcing/permissive/disabled):

![Images](square.jpg)   Set enforcing and permissive modes for SELinux

The next objective requires that you understand the SELinux contexts defined for different files and processes. Although the associated commands are straightforward, the available contexts are as broad as the number of services available on Linux:

![Images](square.jpg)   List and identify SELinux file and process contexts

As you experiment with different SELinux contexts, you’ll likely make mistakes. You may not remember the default contexts associated with important directories. But with the right commands, you don’t have to remember everything; as suggested by the following objective, it’s relatively easy to restore the default:

![Images](square.jpg)   Restore default file contexts

SELinux uses contexts not just for files and processes but also for network ports. By editing port labels, you can allow a service to run on a nonstandard port, or you can restrict the ports that a service is able to listen to. The related exam objective is

![Images](square.jpg)   Manage SELinux port labels

The next objective may seem complex at first glance, but it isn’t, because the boolean settings associated with SELinux have descriptive names. In essence, this means that to run a certain service under SELinux, all you need to do is turn on one or more boolean settings (rather than having to modify the SELinux policy rules directly).

![Images](square.jpg)   Use boolean settings to modify system SELinux settings

Once SELinux is operational, you should monitor the system for policy violations. A violation may be the result of a misconfiguration or an unauthorized intrusion attempt. Hence, to get the most out of SELinux, you should know how to audit for policy violations and be able to address common problems. The related RHCSA objective is

![Images](square.jpg)   Diagnose and address routine SELinux policy violations

### CERTIFICATION OBJECTIVE 8.01

### Basic Firewall Control

Traditionally, firewalls were configured only between LANs and outside networks such as the Internet. But as security threats increase, there’s an increasing need for firewalls on every system. RHEL 9 includes a firewall in every default configuration.

The Linux kernel comes with a powerful framework, the Netfilter system, which enables other kernel modules to offer functionalities such as packet filtering, network address translation (NAT), and load balancing. In previous RHEL releases, the **iptables** command was the main tool used to interact with the Netfilter system to provide packet filtering and NAT.

Today, the functionality of Netfilter has been extended by Nftables, a new packet classification system. Before you send a message over an IP network, the message is broken down into smaller units called *packets*. Additional information, including the type of data, the source address, and destination address, is added to each packet. The packets are reassembled when they reach the destination computer. An Nftables rule examines these fields in each packet to determine whether to allow the packet to pass.

In RHEL 9, the old **iptables** tool is now deprecated in favor of **firewalld**. You can interact with **firewalld** using the graphical utility **firewall-config** or the command-line client **firewall-cmd**. While **iptables** relied on the Netfilter system within the Linux kernel to filter packets, **firewalld** uses the more advanced feature provided by Nftables. In addition, whereas **iptables** was based on the concept of “chain of filter rules” to block or forward traffic, **firewalld** is “zone based,” as you will see in the following sections.

For the RHCSA exam, you need to understand how to configure a firewall to either block or allow network communication through one or more ports using **firewall-cmd**. We will also explain how to use the **firewall-config** GUI tool and the Cockpit web console to achieve the same result.

#### Standard Ports

Linux communicates over a network, primarily using the TCP/IP protocol suite. Different services use certain ports and protocols by default, as defined in the /etc/services file. It may be useful to know some of these ports by heart, such as those described in [Table 8-1](#ch08.xhtml_ch8tab1). Be aware, some of these ports may communicate using the Transmission Control Protocol (TCP), the User Datagram Protocol (UDP), or even the Stream Control Transmission Protocol (SCTP). For example, as noted in the following excerpts from the /etc/services file, the FTP service has been assigned the TCP and UDP ports listed here:

TABLE 8-1 Common TCP/IP Ports

![Images](f0315-01.jpg)

![Images](f0314-01.jpg)

However, you’ll see shortly that the Red Hat firewall configuration tools open only TCP communications for FTP services. This is because the default policy of the Internet Assigned Number Authority (IANA) is to register port numbers for both TCP and UDP, even if a service only supports the TCP protocol.

#### The firewalld Service

You can automate the process of configuring a firewall. For that purpose, in RHEL 9 **firewalld** comes with both a console and a GUI configuration tool. Although the look and feel of the two applications differs, you can use both tools to configure access to trusted services. Before starting the **firewalld** configuration tool, check that **firewalld** is running and automatically starts during the boot process:

![Images](f0315-02.jpg)

One of the features of **firewalld** is *zone-based* firewalling. In a zone-based firewall, networks and interfaces are grouped into zones, with each zone configured with a different level of trust. The zones defined in **firewalld** are listed in [Table 8-2](#ch08.xhtml_ch8tab2), along with their default behavior for outgoing and incoming connections.

TABLE 8-2 Zones in firewalld

![Images](f0316-01.jpg)

![Images](job.jpg)

**A zone is made up of a group of source network addresses and interfaces, plus the rules to process the packets that match those source addresses and network interfaces.**

![Images](job.jpg)

**On some systems, you may see a zone named “libvirt.” This is not one of the default zones defined in firewalld, but it is created by libvirt to manage interfaces such as virbr0, which is used to allow communication between virtual guests and the host.**

##### The GUI firewall-config Tool

You can start the graphical **firewalld** configuration tool from a GUI-based command line with the **firewall-config** command. The result is shown in [Figure 8-1](#ch08.xhtml_ch8fig1).

FIGURE 8-1 The graphical firewall-config tool

![Images](F08-01.jpg)

As shown in the figure, the main window includes different menus and tabs. In the top-left area, you can find which interface is linked to which zone. Next to it, there is a drop-down Configuration menu, where you can set the firewall to Runtime or Permanent mode. If it’s set to Runtime, the changes applied by **firewall-config** take effect immediately but will not survive a server reboot. Alternatively, select Permanent mode to make your changes survive a server reboot. At any time, you can click Options | Reload Firewalld to make a new firewall configuration immediately effective.

![Images](exam.jpg)

**If** firewall-config **is not installed, run the** dnf install firewall-config **command.**

![Images](job.jpg)

**You can only modify definitions of zones and services in Permanent mode.**

The Zones tab includes all the zones previously listed in [Table 8-2](#ch08.xhtml_ch8tab2). When an incoming packet hits the firewall, its source address is checked for a match with the network addresses that belong to the existing zones. If no match is found, the incoming interface of the packet is checked to verify whether it belongs to a zone. Once a correspondence is found, the packet is processed according to the rules of the zone it has been matched to.

In the main **firewall-config** window, the public zone is displayed in a bold font to indicate that this zone is the *default zone*. The default zone has a special meaning: any new network interface added to the system is automatically assigned to the default zone. In addition, the rules of the default zone are processed for all incoming packets that do not match any of the other zones. You can set a different zone to be the default by clicking Options | Change Default Zone.

To allow or deny incoming traffic through the firewall, select a zone and add or remove a checkmark in the zone’s Services tab for the service you want to grant or block. As an alternative, you can also specify a protocol and port from the Ports tab.

In **firewalld**, a service is defined as a group of one of more protocols and ports. A service can also include a Netfilter helper module to support filtering for those applications that dynamically open multiple connections.

A variety of network services are already defined in the Services window. The most common are described in [Table 8-3](#ch08.xhtml_ch8tab3).

TABLE 8-3 Common TCP/IP Ports

![Images](f0318-01.jpg)

If you switch the **firewall-config** tool into Permanent mode, you can add new zones and services or edit existing ones. To manage services, click the Services tab, select a service, and click the corresponding icon at the bottom of the pane to remove, add, or edit the service. If desired, you can also configure custom ports for an existing service by selecting the service’s port in the right pane and then clicking the Add or Edit button to open the Port and Protocol dialog box, as shown in [Figure 8-2](#ch08.xhtml_ch8fig2).

FIGURE 8-2 Adding custom ports to a service in the firewall-config tool

![Images](F08-02.jpg)

##### The Console firewall-cmd Configuration Tool

The **firewall-cmd** configuration tool has the same features and services as the corresponding GUI tool. In fact, both the graphical **firewall-config** tool and the CLI **firewall-cmd** tool are just client front ends that communicate to **firewalld**.

As with the GUI tool, **firewall-cmd** can display all the available zones and switch to a different default zone. The following example changes the default zone from the public zone to the internal zone:

![Images](f0319-02.jpg)

The option **--list-all** is particularly useful. It lists all the configured interfaces and services allowed through a zone, as illustrated next:

![Images](f0319-03.jpg)

![Images](f0320-01.jpg)

As with many of the **firewall-cmd** command options, the default zone is assumed if no zone is specified with the **--zone** command switch. You can add and remove ports and services from a zone with the **--add-port**, **--add-service**, **--remove-port**, and **--remove-service** switches, respectively. The next example enables the http service for traffic hitting the dmz zone:

![Images](f0320-02.jpg)

By default, all configuration changes made by **firewall-cmd** do not survive a server reboot. To make a change that survives a reboot, add the **--permanent** switch to **firewall-cmd**. Then, run **firewall-cmd --reload** to implement the change immediately.

![Images](exam.jpg)

**You want firewall changes that survive after a reboot. To do so with the** firewall-cmd **command, use the** --permanent **switch.**

EXERCISE 8-1

**Adjust Firewall Settings**

In this exercise, you’ll adjust firewalls from the command-line interface and review the results with the **nmap** and **telnet** commands. Although it does not matter how you address a problem on a Red Hat exam, in this exercise you’ll see what happens when adding a new service via the **firewall-cmd** tool. Of course, it’s possible to use the graphical **firewall-config** tool to perform the same tasks. This assumes a system with the default **firewalld** configuration described in this chapter.

Note that the Telnet application protocol is unencrypted and therefore is not considered secure. Nevertheless, this example uses the Telnet service to illustrate how to modify firewall settings. In the real world, use SSH rather than Telnet.

1.   Check if the **nmap** command is present. If not, run

![Images](f0321-01.jpg)

2.   Review current active services on the local system with the **nmap localhost** command. Note the IP address of the local system with the **ip addr** command. If the local system is server1.example.com, that IP address should be 172.16.0.100.

3.   Make sure **firewalld** is currently operational with the **systemctl status firewalld** command.

4.   Go to a different system. You can do so from a different virtual machine, or you can access it remotely with the **ssh** command. If the tester1.example.com system is running, you can log in to that system with the **ssh 172.16.0.50** command.

5.   Use the **nmap** command from tester1 to review what is seen through the firewall; for the noted server1.example.com system, the right command would be **nmap 172.16.0.100**. If the IP address found from Step 2 is different, substitute accordingly.

6.   Return to the original system. Run the following commands to install and start the Telnet service:

![Images](f0321-02.jpg)

7.   Run the following command to show the current settings for the default zone:

![Images](f0321-03.jpg)

8.   Allow telnet traffic through the default zone, and include the **--permanent** switch to make the change persistent:

![Images](f0321-04.jpg)

9.   Apply the previous change to the run-time configuration of the firewall:

![Images](f0321-05.jpg)

10.   Navigate back to the tester1.example.com system as was done in Step 4.

11.   Repeat Step 5\. What do you see? You should find the Telnet service in the output of the **nmap** command, indicating that the firewall is now permitting connections for this application.

12.   Finally, revert the changes:

![Images](f0321-06.jpg)

EXERCISE 8-2

**Firewall Configuration with the Cockpit Web Console**

So far, we have seen two methods to modify the firewall configuration: the CLI utility **firewall-cmd** and the GUI tool **firewall-config**. In this exercise, we will explore how to achieve the same configuration of Exercise 8-1, but with the Red Hat Cockpit web console.

You should not be surprised that Red Hat Enterprise Linux offers many ways to achieve the same result. During the RHCSA exam, it is the result that matters, not which tool you use to achieve a configuration. Therefore, you should familiarize yourself with all the methods available to complete a task, and choose the one that most suits you.

1.   Install the cockpit RPM package if it is not present:

![Images](f0322-01.jpg)

2.   Permit the Cockpit service through the firewall:

![Images](f0322-02.jpg)

3.   Start the Cockpit service:

![Images](f0322-03.jpg)

4.   Open Firefox and point to the URL [https://localhost:9090](https://localhost:9090). Accept the server’s certificate and log in with the root account credentials.

5.   Click the Networking option in the navigation menu on the left. Then click the Edit Rules And Zones link, as shown next:

![Images](I08-01.jpg)

6.   Click Add Services to add a service to the zone indicated:

![Images](I08-02.jpg)

7.   Select the Telnet service from the list and click Add Services:

![Images](I08-03.jpg)

8.   The Telnet service was added to both the permanent and runtime configurations. To confirm, run

![Images](f0324-01.jpg)

### CERTIFICATION OBJECTIVE 8.02

### Securing SSH with Key-Based Authentication

[Chapter 3](#ch03.xhtml) addressed SSH client programs, including **ssh**, **scp**, and **sftp**. The focus of this section is on securing SSH access with key-based authentication.

As SSH is an important tool for administering systems remotely, it’s important to understand the basics of how it encrypts communication between a client and the SSH server. Then you’ll see how to create a public/private key pair so connections won’t even put user passwords at risk. But first, it may be helpful to review some basic information about SSH configuration commands and files.

#### SSH Configuration Commands

There are a few SSH-oriented utilities you need to know about:

![Images](square.jpg)   **sshd** The daemon service; this must be running to receive inbound Secure Shell client requests.

![Images](square.jpg)   **ssh-agent** A program to hold private keys used for Digital Signature Algorithm (DSA), Elliptic Curve DSA (ECDSA), and Rivest, Shamir, Adleman (RSA) authentication. The idea is that the **ssh-agent** command is started in the beginning of an X session or a login session, and other programs are started as clients to the **ssh-agent** program.

![Images](square.jpg)   **ssh-add** Adds private key identities to the authentication agent, **ssh-agent**.

![Images](square.jpg)   **ssh** A secure way to log in to a remote machine, similar to Telnet but with encrypted communications. The basic use of this command was discussed in [Chapter 3](#ch03.xhtml). To make this work with key-based authentication, you need a private key on the client and a public key on the server. Take the public key file, such as id_rsa.pub, created later in this section, copy it to the server, and place it in the home directory of an authorized user in the ~/.ssh/authorized_keys file.

![Images](square.jpg)   **ssh-keygen** A utility that creates private/public key pairs for SSH authentication. The **ssh-keygen -t *keytype*** command creates a key pair based on the DSA, ECDSA, or RSA protocol.

![Images](square.jpg)   **ssh-copy-id** A script that copies a public key to a target remote system.

#### SSH Client Configuration Files

Systems configured with SSH include configuration files in two different directories. For the local system, basic SSH configuration files are stored in the /etc/ssh directory. But just as important are the configuration files in each user’s home directory in the ~/.ssh/ subdirectory. Those files configure how the given user is allowed to connect to remote systems.

When DSA, ECDSA, and RSA keys are included, the user ~/.ssh/ subdirectory includes the following files:

![Images](square.jpg)   **authorized_keys** Includes a list of public keys from remote users. Users with public encryption keys in this file can connect to remote systems. The system users and names are listed at the end of each public key copied to this file.

![Images](square.jpg)   **id_dsa** Includes the local private key based on the DSA algorithm.

![Images](square.jpg)   **id_dsa.pub** Includes the local public key for the user based on the DSA algorithm.

![Images](square.jpg)   **id_ecdsa** Includes the local private key based on the ECDSA algorithm.

![Images](square.jpg)   **id_ecdsa.pub** Includes the local public key for the user based on the ECDSA algorithm.

![Images](square.jpg)   **id_rsa** Includes the local private key based on the RSA algorithm.

![Images](square.jpg)   **id_rsa.pub** Includes the local public key for the user based on the RSA algorithm.

![Images](square.jpg)   **known_hosts** Contains the public host keys from remote systems. The first time a user logs in to a system, the user is prompted to accept the public key of the remote server. On RHEL 9, the ECDSA protocol is used by default to encrypt traffic. The corresponding public key on the remote server is stored on the /etc/ssh/ssh_host_ecdsa_key.pub file and is added by the client to its local ~/.ssh/known_hosts file.

#### Basic Encrypted Communication

Basic encryption in computer networking normally requires a private key and a public key. The principle is the same as GNU Privacy Guard (GPG) communications, discussed in [Chapter 4](#ch04.xhtml). A private key is stored by the owner, and a public key is sent to a third party. When the key pair is properly configured, a user can encrypt a message using their private key, while a third party can decrypt a message with the corresponding public key. This also works in reverse: a third party can encrypt a message using the public key of the receiver, while the receiver can decrypt the message with their private key. In the SSH protocol, the server shares its public key for authentication, and a symmetric session key is mutually established through a key exchange algorithm. This key is used to secure the communication channel.

Encryption keys are based on random numbers. The numbers are so large (typically 2048 bits for RSA keys or more) that the chance someone will break into the server system, at least with a PC, is practically impossible. Private and public encryption keys are based on a matched set of these random numbers.

##### Private Keys

The private key must be secure. Key-based authentication relies on a private key that is accessible only to the user owner of that key in the ~/.ssh subdirectory of that user’s home directory. To authenticate a user, the server sends to the client a “challenge,” which is a request to perform an encryption operation that requires the knowledge of the private key. Once the server receives a response to its challenge from the client, it will be able to decrypt the message and prove that the user’s identity is genuine.

##### Public Keys

The public key is just that, publicly available. Public keys are designed to be copied to appropriate users’ ~/.ssh/ subdirectories in a file named authorized_keys.

The example shown in [Figure 8-3](#ch08.xhtml_ch8fig3) lists the directories and files associated with SSH usage.

FIGURE 8-3 Keys in a user’s .ssh/ subdirectory

![Images](F08-03.jpg)

![Images](exam.jpg)

**Most of the common issues with SSH key-based authentication are related to file permissions. As shown in [Figure 8-3](#ch08.xhtml_ch8fig3), the permissions for private keys are set to 600 (rw-------) and for public keys are set to 644 (rw-r--r--). In addition, the permissions of the ~/.ssh directory should be 700 (rwx------).**

A key is like a password used to encrypt communications data. But it’s not a standard password by any means. Imagine trying to remember the 1024-bit number expressed in hexadecimal format shown here:

![Images](f0326-01.jpg)

The private key is similar, *but you must keep it private*, or this whole system fails. Keeping it private means no one should have access to the key other than its owner. If your PC is public, secure your private key with a passphrase (password). The procedure to set up a passphrase is described next. Don’t forget the passphrase, or you’ll have to create a new key pair and again copy your public key to all the target systems.

#### Set Up a Private/Public Pair for Key-Based Authentication

The **ssh-keygen** command is used to set up a public/private key pair. Although it creates an RSA key by default, it also can be used to create a DSA key or ECDSA key. For example, some users may need DSA keys to comply with certain U.S. government standards. An example of the command sequence is shown in [Figure 8-4](#ch08.xhtml_ch8fig4).

FIGURE 8-4 Command to generate an SSH key pair

![Images](F08-04.jpg)

As shown in the figure, the command prompts for an optional passphrase to protect the private key. When the identical passphrase is confirmed, the private key is saved in the id_rsa file, and the corresponding public key is stored in the id_rsa.pub file. Both files for user michael are stored in the /home/michael/.ssh directory.

If desired, you can set up RSA keys with a larger number of bits. In our testing, we were able to set up key pairs with up to 8192 bits fairly quickly, even on a virtual machine system with just one virtual CPU. The command that starts the process is

`$ ssh-keygen -b 8192`

Alternatively, if a DSA key is needed, the following command can help. Only 1024-bit DSA keys are allowed. The process after this command is the same as shown in [Figure 8-4](#ch08.xhtml_ch8fig4).

`$ ssh-keygen -t dsa`

The next step is to transmit the public key to a remote system. It might be one of the servers you administer. If you’re willing to transmit that public key over the network (once per connection), the following command can work:

![Images](f0328-01.jpg)

Strictly speaking, the **ssh-copy-id** command without the **-i** option defaults to transmitting the most recently created public key. The preceding command automatically appends the noted local RSA key to the end of the *remote* ~/.ssh/authorized_keys file. In this case, that file can be found in the /home/michael directory. Of course, you may choose to substitute the IP address for the hostname.

![Images](job.jpg)

**Sometimes, after copying a key to a remote system, you may get an “agent admitted failure to sign using the key” error followed by a password prompt when you try to log in. To fix this problem, log out of the console or the GUI and log back in. In most cases, the** ssh **command will prompt for the passphrase.**

You should then be able to immediately connect to that remote system. In the preceding case, the appropriate command is either one of the following:

![Images](f0328-02.jpg)

When run on a console, the **ssh** command uses the following prompt for the passphrase:

`Enter passphrase for key '/home/michael/.ssh/id_rsa'`

When run in a GUI-based command line, it prompts with a window similar to that shown in [Figure 8-5](#ch08.xhtml_ch8fig5).

FIGURE 8-5 Prompt for a passphrase

![Images](F08-05.jpg)

### CERTIFICATION OBJECTIVE 8.03

### A Security-Enhanced Linux Primer

Security-Enhanced Linux (SELinux) was developed by the U.S. National Security Agency to provide a level of mandatory access control for Linux. It goes beyond the discretionary access control associated with file permissions. In essence, SELinux enforces security rules within the kernel of the operating system. It limits the damage if there is a security breach. For example, if the system account associated with an FTP service is compromised, SELinux makes it more difficult to use that account to compromise other services.

#### Basic Features of SELinux

The SELinux security model is based on subjects, objects, and actions. A *subject* is a process, such as a running command or an application such as the Apache web server in operation. An *object* is a file, a device, a socket, or in general any resource that can be accessed by a subject. An *action* is what may be done by the subject to the object.

SELinux assigns different contexts to objects. A *context* is just a label, which is used by the SELinux security policy to determine whether a subject’s action on an object is allowed or not. For example, the Apache web server process can take objects such as web page files and display them for the clients of the world to see. That action is normally allowed in the RHEL 9 implementation of SELinux, as long as the object files have appropriate SELinux contexts.

The contexts associated with SELinux are fine-grained. In other words, if a “black hat” hacker breaks in and takes over your web server, SELinux contexts prevent that intruder from using that breach to break into other services.

To see the context of a particular file, run the **ls -Z** command. As an example, review what this command does in [Figure 8-6](#ch08.xhtml_ch8fig6), as it displays security contexts in the / directory.

FIGURE 8-6 SELinux security contexts of different files

![Images](F08-06.jpg)

As noted at the beginning of this chapter, six objectives relate to SELinux on the RHCSA exam. You’ll explore how to meet these objectives in the following sections.

#### SELinux Status

As suggested in the RHCSA objectives, you need to know how to “set enforcing and permissive modes for SELinux.” There are three available modes for SELinux: *enforcing*, *permissive*, and *disabled*. The enforcing and disabled modes are self-explanatory. SELinux in permissive mode means that any SELinux rules that are violated are logged, but the violation does not stop any action.

If you want to change the default SELinux mode, change the **SELINUX** directive in the /etc/selinux/config file, as illustrated in [Table 8-4](#ch08.xhtml_ch8tab4). The next time you reboot, the changes are applied to the system.

TABLE 8-4 Standard Directives in /etc/selinux/config

![Images](f0330-02.jpg)

If SELinux is configured in enforcing mode, it protects systems in one of two ways: in *targeted* mode or in *mls* mode. The default is the targeted policy, which allows you to customize what is protected by SELinux in a fine-grained manner. In contrast, MLS goes a step further, using the Bell–LaPadula model developed for the U.S. Department of Defense. That model supports layers of security between levels c0 and c3\. Although the c3 level is listed as “Top Secret,” the range of available levels goes all the way up to c1023\. Such fine-grained levels of secrecy have yet to be fully developed. If you want to explore MLS, install the selinux-policy-mls RPM.

![Images](job.jpg)

**If you just want to experiment with SELinux, configure it in permissive mode. It’ll log any violations without stopping anything. It’s easy to set up with the SELinux Administration tool, or you can set** SELINUX=permissive **in /etc/selinux/config. If the** auditd **service is running, violations are logged in the audit.log file in the /var/log/audit directory. Just remember, Red Hat likely wants candidates to configure SELinux in enforcing mode during the exams.**

#### SELinux Configuration at the Command Line

SELinux is today a mature piece of software, and it has become much more useful with the releases of RHEL 7 and RHEL 8\. Nevertheless, given the complexity associated with SELinux, it may be more efficient for system engineers who are not very familiar with it to use the SELinux Administration tool to configure SELinux settings.

The following sections show how you can configure and manage SELinux from the command-line interface. However, because it’s easier to demonstrate the full capabilities of SELinux using GUI tools, a detailed discussion of such capabilities will follow later in this chapter.

#### Configure Basic SELinux Settings

There are some essential commands that can be used to review and configure basic SELinux settings. To see the current status of SELinux, run the **getenforce** command; it returns one of three self-explanatory options: enforcing, permissive, or disabled. The **sestatus** command provides more information, with output similar to the following:

![Images](f0331-01.jpg)

You can change the current SELinux status with the **setenforce** command; the options are straightforward:

![Images](f0331-02.jpg)

This changes the /sys/fs/selinux/enforce boolean. For booleans, you could substitute 1 and 0, respectively, for enforcing and permissive. To make this change permanent, you’ll have to modify the **SELINUX** variable in the /etc/selinux/config file. However, changes to detailed SELinux booleans require different commands.

Alternatively, if SELinux is disabled for some reason, the output would be

![Images](f0332-01.jpg)

![Images](exam.jpg)

**If SELinux is disabled, it may take a few minutes to reboot a system after setting SELinux in enforcing mode. However, the process is less time-consuming than it was for the previous RHEL releases.**

In that case, the **setenforce** command does not work. Instead, you have to set **SELINUX=enforcing** in the /etc/selinux/config file. And that requires a system reboot to “relabel” all files, where SELinux labels are applied to each file on the local system.

#### Configure Regular Users for SELinux

To review the status of current SELinux users, run the **semanage login -l** command. Based on the default installation of RHEL 9, it leads to the following output:

![Images](f0332-02.jpg)

In other words, regular “default” users have the same SELinux user context of the root administrative user. To confirm, run the **id -Z** command as a regular user. Without changes, it leads to the following output, which suggests that the user is not confined by any SELinux settings:

![Images](f0332-03.jpg)

The preceding string defines what is called a *label* in SELinux jargon. A label is made up of several context strings, separated by a column: a user context (which ends with **_u**), a role context (which ends with **_r**), a type context (which ends with **_t**), a sensitivity context, and a category set. The rules of the targeted policy, which is the default SELinux policy in RHEL 9, are mostly associated with the type (**_t**) context.

Although it may not be an exam requirement, regular users can be confined by SELinux. When user accounts are compromised, and they will be compromised, you want any damage that might be caused limited by SELinux rules. The following example specifies a confinement rule that adds (**-a**) regular user michael, specifying (**-s**) the user_u context for confinement:

![Images](f0332-04.jpg)

The user_u role does not have the ability to run the **su** and **sudo** commands, described in [Chapter 6](#ch06.xhtml). If desired, you can reverse the process with the **semanage login -d michael** command. The available user contexts listed in the latest Red Hat documentation are shown in [Table 8-5](#ch08.xhtml_ch8tab5).

TABLE 8-5 Options for SELinux User Roles

![Images](f0333-01.jpg)

When a user role is changed, it doesn’t take effect until the next login. For example, if we were to change the role for user michael to user_u in a GUI-based command line, the change would not take effect until we logged out and logged back in to the GUI. If you were to try this on your system, you would no longer be able to start any administrative configuration tools, and you would not have access to the **sudo** and **su** commands.

On some networks, you may want to change the role of future users to user_u. If you don’t want regular users tinkering with administrative tools, you could make that change for future default users with the following command:

![Images](f0333-02.jpg)

This command modifies (**-m**) the targeted policy store (**-S**), with SELinux user (**-s**) user_u, with the MLS s0 range (**-r**) for the default user. Here, “__default__” includes two underscore characters on each side of the word. As long as user_u is in effect for the default SELinux user, regular users won’t have access to use administrative tools or commands such as **su** and **sudo**. The following command reverses the process:

![Images](f0333-03.jpg)

![Images](job.jpg)

**The MLS policy adds complexity to SELinux. The targeted default policy with appropriate booleans and file contexts normally provides more than adequate security.**

The full MLS range is required (s0-s0:c0.c1023) because the unconfined_u user is not normally limited by MLS restrictions.

#### Manage SELinux Boolean Settings

Most SELinux settings are boolean—in other words, they’re activated and deactivated by setting them to 1 or 0, respectively. Once set, the booleans can be retrieved from the /sys/fs/selinux/booleans directory. One simple example is **selinuxuser_ping**, which is normally set to 1, which allows users to run the **ping** and **traceroute** commands. Many of these SELinux settings are associated with specific services.

These settings can be read with the **getsebool** command and modified with the **setsebool** command. For example, the following output from the **getsebool user_exec_content** command confirms that SELinux allows users to execute scripts either in their home directories or from the /tmp directory:

![Images](f0334-01.jpg)

This boolean can be disabled either temporarily or in a way that survives a reboot. One method for doing so is with the **setsebool** command. For example, the following command disables the noted boolean until the system is rebooted:

![Images](f0334-02.jpg)

You can choose to substitute **0** for **off** in the command. As this is a boolean setting, the effect is the same: the flag is switched off. However, the **-P** switch is required to make the change to the boolean setting survive a system reboot. Be aware that the changes don’t take effect until the next time the affected user actually logs in to the associated system.

A full list of available booleans is available in the output to the **getsebool -a** command.

For more information on each boolean, run the **semanage boolean -l** command. The output includes descriptions of all available booleans, and it can be searched with the help of the **grep** command.

#### List and Identify SELinux File Contexts

If you’ve enabled SELinux, the **ls -Z** command lists current SELinux file contexts, as shown earlier in [Figure 8-6](#ch08.xhtml_ch8fig6). As an example, take the relevant output for the anaconda-ks.cfg file from the /root directory:

![Images](f0334-03.jpg)

The output specifies four elements of SELinux security: the user, role, type, and MLS level for the noted file. Generally, the SELinux user associated with a file is system_u or unconfined_u, and this generally does not affect access. In most cases, files are associated with object_r, an object role for the file. It’s certainly possible that future versions of the SELinux targeted policy will include more fine-grained options for the user and role.

The key file context is the type, in this case, admin_home_t. If you configure a service such as FTP and HTTP, the files served by the FTP or HTTP service must have appropriate SELinux contexts. You can change the type of files and directories with the **chcon** command.

For example, to configure a nonstandard directory for an FTP server, make sure the context matches the default FTP directory. Consider the following command:

![Images](f0335-01.jpg)

The contexts are the system user (system_u) and object role (object_r) for type sharing with the public (public_content_t). If you create another directory for FTP service, you’ll need to assign the same security contexts to that directory. For example, if you create an /ftp directory as the root user and run the **ls -Zd /ftp** command, you’ll see the contexts associated with the /ftp directory as shown:

![Images](f0335-02.jpg)

To change the context, use the **chcon** command. If there are subdirectories, you’ll want to make sure changes are made recursively with the **-R** switch. In this case, to change the user and type contexts to match /var/ftp, run the following command:

![Images](f0335-03.jpg)

If you want to support uploads to your FTP server, you’ll have to assign a different type context, specifically public_content_rw_t. That corresponds to the following command:

![Images](f0335-04.jpg)

You can also use a different variation on the **chcon** command. The following command uses user, role, and context from the /var/ftp directory and applies the changes recursively:

![Images](f0335-05.jpg)

But wait, what happens if a filesystem gets relabeled? The changes made with **chcon** won’t survive a filesystem relabeling because all file contexts will be reset to the default values defined in the SELinux policy. Hence, we need a way to modify the rules that define the default file context for each file. This subject will be covered in the next section.

![Images](job.jpg)

**Using** restorecon **is the preferred way to change file contexts because it sets the contexts to the values configured in the SELinux policy. The** chcon **command can modify file contexts to any value passed as an argument, but the change may not survive a filesystem relabeling if a context differs from the default value defined in the SELinux policy. Hence, to avoid mistakes, you should modify contexts in the SELinux policy with** semanage fcontext **and use** restorecon **to change file contexts.**

#### Restore SELinux File Contexts

Default contexts are configured in /etc/selinux/targeted/contexts/files/file_contexts. If you make a mistake and want to restore the original SELinux settings for a file, the **restorecon** command restores those settings based on the file_contexts configuration file. However, the defaults in a directory may vary. For example, the following command (with the **-F** switch forcing a change to all contexts rather than just the type context) leads to a different set of contexts for the /ftp directory:

![Images](f0336-01.jpg)

You may notice that the user context is different from when the /ftp directory was created. That’s due to the first line in the aforementioned file_contexts file, which applies the noted contexts:

![Images](f0336-02.jpg)

You may also list all default file contexts rules in file_contexts with the **semanage fcontext -l** command. See [Figure 8-7](#ch08.xhtml_ch8fig7) for an excerpt of the output.

FIGURE 8-7 SELinux context definitions

![Images](F08-07.jpg)

As you can see, SELinux context definitions use regular expressions, such as the following:

![Images](f0336-03.jpg)

The preceding regular expression matches the **/** character, followed by an arbitrary number of characters (the **.***). The **?** character means that the entire regular expression within parentheses can be matched zero or one time. Hence, the overall result is to match a **/** followed by an arbitrary number of characters, or nothing. This regular expression is widely used to match a directory and all the files in it.

As an example, a regular expression that matches the /ftp directory and all files in it is given by the following:

![Images](f0336-04.jpg)

Using this regular expression, you can define an SELinux policy rule that assigns to the /ftp directory and all files in it a default type context. You can do so with the **semanage fcontext -a** command. For example, the following command assigns a default type context of public_content_t to the /ftp directory and all the files in it:

![Images](f0337-01.jpg)

Once you have defined a new default policy context for a filesystem path, you can run the **restorecon** command to set the contexts to the corresponding default policy values. The following command restores the context recursively (**-R**) to the public_content_t value defined previously:

![Images](f0337-02.jpg)

EXERCISE 8-3

**Configure a New Directory with Appropriate SELinux Contexts**

In this exercise, you’ll set up a new directory, /ftp, with SELinux contexts that match the standard directory for FTP servers. This exercise demonstrates how to do this with the **chcon** command and shows the effect of using the **restorecon** and **semanage** commands.

1.   Create the /ftp directory. Use the **ls -Zd /ftp** command to identify the SELinux contexts on that directory. Contrast that with the contexts on the /var/ftp directory.

2.   Change the contexts on the /ftp directory to match those on the /var/ftp directory. The most efficient method is with the following command:

`# chcon -R --reference /var/ftp /ftp`

While the **-R** switch is not required, we include it to help you get used to the idea of changing contexts recursively.

3.   Run the **ls -Zd /ftp** command to review the changed contexts on that directory. It should now match the contexts on the /var/ftp directory.

4.   Run the following command to see what happens when SELinux is relabeled:

`# restorecon -Rv /ftp`

What did this command do to the contexts of the /ftp directory?

5.   To make changes to the /ftp directory permanent, you need help from the **semanage** command, with the **fcontext** argument. As there is no analog to the **chcon --reference** command switch, the following command specifies the user role and file type, based on the default settings for the /var/ftp directory:

`# semanage fcontext -a -s system_u -t public_content_t "/ftp(/.*)?"`

6.   Review the results. First, the **semanage** command does not change the current SELinux contexts of the /ftp directory. Next, review the contents of file_contexts
.local in the /etc/selinux/targeted/contexts/files directory. It should reflect the **semanage** command just executed.

7.   Rerun the **restorecon** command from Step 4\. Does it change the SELinux contexts of the /ftp directory now?

#### SELinux Port Labeling

The SELinux policy controls every action that a process can execute on a certain object, such as a file, a device, or a network socket. Opening a TCP socket and listening to a network port is one of those actions you can control and restrict via the SELinux policy.

If one of the services covered in the previous section is configured to listen to a nonstandard port, by default the SELinux targeted policy will deny this action. In fact, SELinux uses labels to control access not only to files or devices but also to network ports.

You can list all SELinux port labels by running the **semanage** command:

`# semanage port -l`

Filtering for a certain string can help in identifying which ports a service is allowed to listen to. As shown in the following example, the SSH service is restricted to listening to port 22:

![Images](f0338-02.jpg)

Similarly, the http_port_t label regulates the ports that Apache can listen to, whereas http_cache_port_t identifies the ports allowed by web proxies:

![Images](f0338-03.jpg)

If you need to change a label to allow a service to listen to a nonstandard port, use the **semanage** command. In the following example, the SELinux policy is modified to allow Apache to listen to port 444:

![Images](f0338-04.jpg)

#### Identify SELinux Process Contexts

As you will see in [Chapter 9](#ch09.xhtml), the **ps** command lists currently running processes. In an SELinux system, there are contexts for each running process. To see those contexts for all processes currently in operation, run the **ps -eZ** command, which lists every (**-e**) process SELinux context (**-Z**). [Figure 8-8](#ch08.xhtml_ch8fig8) includes a varied excerpt from the output of that command on our system.

FIGURE 8-8 SELinux security contexts of different processes

![Images](F08-08.jpg)

Although the user and role don’t change often, the process type varies widely, frequently matching the purpose of the running process. For example, from the figure you can see how the Avahi daemon (avahi-daemon) is matched by the avahi_t SELinux type. You should be able to identify how at least some of the other SELinux types match the associated service.

In other words, although there is a large variety of SELinux types, they’re consistent with the name of the running process.

#### Diagnose and Address SELinux Policy Violations

If SELinux is running in enforcing mode and a problem arises, and you’re sure there are no problems with the target service or application, don’t disable SELinux! Red Hat has made it easier to manage and troubleshoot. According to Red Hat, the top two causes of SELinux-related problems are contexts and boolean settings.

##### SELinux Audits

Problems with SELinux should be documented in the associated log file, audit.log, in the /var/log/audit directory. The file may be confusing, especially the first time you read it. A number of tools are available to help decipher this log.

First, the audit search (**ausearch**) command can help filter for specific types of problems. For example, the following command lists all SELinux events associated with the use of the **sudo** command:

`# ausearch -m avc -c sudo`

Such events are known as Access Vector Cache (**-m avc**) messages; the **-c** allows you to specify the name commonly used in the log, such as httpd or su. If you’ve experimented with the user_u SELinux user described earlier in this chapter, there should be several related messages available from the audit.log file.

Even for most administrators, the output is still a lot of gobbledygook. However, it should include identifying information such as the audited user ID (shown as auid), which can help you identify the offending user. Perhaps the user needs such access, or perhaps that user’s account has been compromised. In any case, the alert may cause you to pay more attention to that account.

In contrast, the **sealert -a /var/log/audit/audit.log** command may provide more clarity.

##### SELinux Boolean Issues

After deactivating the user_exec_content boolean described earlier, we created a simple script named script1 for a user governed by the user_u label. After making that script executable, we tried running it with the **/home/examprep/script1** command. Even though that user had ownership of the file, with executable permissions set, that attempt led to the following message:

`-bash: /home/examprep/script1: Permission denied`

That led to the log excerpt from /var/log/messages shown in [Figure 8-9](#ch08.xhtml_ch8fig9). Note that the message explicitly cites the command required to address the problem. As an administrator, you need to decide whether such users should be given the ability to execute their own scripts. If so, then the noted command would address the problem.

FIGURE 8-9 An SELinux alert and a solution

![Images](F08-09.jpg)

#### The GUI SELinux Administration Tool

If you’ve taken the time to learn SELinux from the command line, this section should be just a review. For many users, the easiest way to change SELinux settings is with the SELinux Administration tool, which you can start with the **system-config-selinux** command. If the command is not available, install the tool by running

`# dnf install policycoreutils-gui`

As shown in [Figure 8-10](#ch08.xhtml_ch8fig10), the tool shows a basic view of the status of SELinux on the local system, reflecting some of the information shown in the output to the **sestatus** command.

FIGURE 8-10 SELinux status in the Administration tool

![Images](F08-10.jpg)

As you can see, there are options labeled System Default Enforcing Mode and Current Enforcing Mode, which you can set to Enforcing, Permissive, or Disabled. Generally, you don’t need to activate the Relabel On Next Reboot option unless you’ve changed the default policy type.

Three of the categories shown in the left pane of the SELinux Administration tool window are described in the following sections. The other categories are out of scope of the RHCSA exam.

##### SELinux Boolean Settings

In the SELinux Administration tool, click Boolean in the left panel, as shown in [Figure 8-11](#ch08.xhtml_ch8fig11). Scroll through available modules. As you can see, an SELinux policy can be modified in a number of different categories, some related to administrative functions, others to specific services. A select number of these options are shown in [Figure 8-11](#ch08.xhtml_ch8fig11). Any changes you make are reflected in boolean variables in the /sys/fs/selinux/booleans directory. Module categories of interest for the RHCSA exam include cron, mount, virt, and that catch-all category: unknown. A list of selected booleans is included in [Table 8-6](#ch08.xhtml_ch8tab6). The booleans appear in the order shown in the SELinux Administration tool.

FIGURE 8-11 Booleans in the SELinux Administration tool

![Images](F08-11.jpg)

TABLE 8-6 Selected SELinux Boolean Options

![Images](f0343-01.jpg)

##### File Labeling

Clicking File Labeling in the left panel of the SELinux Administration tool enables you to change the default labels associated with files, some of which are described earlier in this chapter (and in other chapters discussing SELinux contexts). Some of the options are shown in [Figure 8-12](#ch08.xhtml_ch8fig12). Any changes to this screen are written to the file_contexts.local file in the /etc/selinux/targeted/contexts/files directory.

FIGURE 8-12 File types in the SELinux Administration tool

![Images](F08-12.jpg)

##### Network Port

The Network Port section of the SELinux Administration tool associates standard ports with services.

![Images](f0344-01.jpg)

#### CERTIFICATION SUMMARY

This chapter focused on the basics of RHCSA-level security. On any Linux system, security starts with the ownership and permissions associated with a file. Firewalls can prevent communication on all but the desired ports. Standard ports for most services are defined in the /etc/services file. However, some services may not use all of the protocols defined in that file. The default RHEL 9 firewall supports access only to a local SSH server.

The **ssh-keygen** command creates passphrase-protected key pairs, which can be used to authenticate to an SSH server without transmitting a user’s password over the network.

SELinux provides another layer of protection using mandatory access control. With a variety of available objects and file types, SELinux controls can help ensure that a breach in one service doesn’t lead to trouble with other services.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 8](#ch08.xhtml).

##### Basic Firewall Control

![Images](squ1.jpg)   **firewalld** is based on the Netfilter kernel system and on Nftables.

![Images](squ1.jpg)   You can find some of the common ports and protocols in /etc/services.

![Images](squ1.jpg)   The default RHEL 9 firewall supports remote access to the local SSH server.

![Images](squ1.jpg)   The RHEL 9 firewall can be configured with the GUI **firewall-config** tool or the CLI **firewall-cmd** tool.

##### Securing SSH with Key-Based Authentication

![Images](squ1.jpg)   SSH key authentication commands include **ssh-keygen** and **ssh-copy-id**.

![Images](squ1.jpg)   User home directories include their own .ssh subdirectory of configuration files, with private and public SSH keys.

![Images](squ1.jpg)   Private/public key pairs can be configured with passphrases using the **ssh-keygen** command.

![Images](squ1.jpg)   Public keys can be transmitted to users’ home directories on remote systems with the **ssh-copy-id** command.

##### A Security-Enhanced Linux Primer

![Images](squ1.jpg)   SELinux may be configured in enforcing, permissive, or disabled mode, with targeted or MLS policies, with the help of the **setenforce** command. Default boot settings are stored in the /etc/selinux/config file.

![Images](squ1.jpg)   SELinux labels contain different contexts, such as user, roles, types, and MLS levels.

![Images](squ1.jpg)   SELinux booleans can be managed with the **setsebool** command; permanent changes require the **-P** switch.

![Images](squ1.jpg)   SELinux contexts can be changed with the **chcon** command and restored to defaults with the **restorecon** command.

![Images](squ1.jpg)   The **sealert** command can be used to interpret problems documented in the audit.log file in the /var/log/audit directory.

#### Q SELF TEST

The following questions will help you measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. Getting results, not memorizing trivia, is what counts on the Red Hat exams. There may be more than one right answer to many of these questions.

##### Basic Firewall Control

**[1.](#ch08.xhtml_ch8ques1)**   What TCP/IP port number is associated with the HTTPS service?

**[2.](#ch08.xhtml_ch8ques2)**   What is the full **firewall-cmd** command to permanently allow incoming HTTPS traffic for the default **firewalld** zone?

**[3.](#ch08.xhtml_ch8ques3)**   How do you reload firewall rules without restarting the **firewalld** service?

##### Securing SSH with Key-Based Authentication

**[4.](#ch08.xhtml_ch8ques4)**   What command configures a private/public key pair using DSA?

**[5.](#ch08.xhtml_ch8ques5)**   What subdirectory of a user home directory contains the authorized_keys file?

##### A Security-Enhanced Linux Primer

**[6.](#ch08.xhtml_ch8ques6)**   What command configures SELinux in enforcing mode?

**[7.](#ch08.xhtml_ch8ques7)**   What command lists all boolean settings for SELinux?

**[8.](#ch08.xhtml_ch8ques8)**   What command adds TCP port 4443 to the http_port_t label?

**[9.](#ch08.xhtml_ch8ques9)**   How do you restore default SELinux security contexts to a file?

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for the labs follow the Self Test answers.

#### A SELF TEST ANSWERS

##### Basic Firewall Control

**[1.](#ch08.xhtml_r_ch8ques1)**   The TCP/IP port number associated with the HTTPS service is 443.

**[2.](#ch08.xhtml_r_ch8ques2)**   The **firewall-cmd** command that permanently allows incoming HTTPS traffic for the default **firewalld** zone is

`# firewall-cmd --permanent --add-service=https`

**[3.](#ch08.xhtml_r_ch8ques3)**   Use **firewall-cmd --reload** to reload the firewall rules without restarting the service.

##### Securing SSH with Key-Based Authentication

**[4.](#ch08.xhtml_r_ch8ques4)**   The command that configures a private/public key pair using DSA is

`ssh-keygen -t dsa`

**[5.](#ch08.xhtml_r_ch8ques5)**   Every user with public keys stored in the authorized_keys file can find that file in the .ssh/ subdirectory of the user’s home directory.

##### A Security-Enhanced Linux Primer

**[6.](#ch08.xhtml_r_ch8ques6)**   The command that configures SELinux in enforcing mode is

`# setenforce enforcing`

**[7.](#ch08.xhtml_r_ch8ques7)**   The command that lists all boolean settings for SELinux is

`# semanage boolean -l`

**[8.](#ch08.xhtml_r_ch8ques8)**   The command that adds TCP port 4443 to the http_port_t label is

`# semanage port -a -t http_port_t -p tcp 4443`

**[9.](#ch08.xhtml_r_ch8ques9)**   Run **restorecon -v /path/to/file** to restore the default SELinux security context for the specified file.

#### LAB ANSWERS

##### Lab 1

This lab is designed to raise awareness of the time and effort required to disable and re-enable SELinux in enforcing mode. If you switch between disabled and permissive mode, the time and effort required should be about the same. If you have to reconfigure SELinux in enforcing mode, you may lose precious time during a Red Hat exam because nothing else can be done while the system is being rebooted and relabeled.

##### Lab 2

In this lab you learn how to configure a firewall for a web server.

**1.**   On server1.example.com, confirm that SELinux is running in enforcing mode with the following command:

`# systemctl status firewalld`

**2.**   Install the httpd RPM package:

`# dnf install -y httpd`

**3.**   Start and enable the httpd service to start at boot:

`# systemctl start --now httpd`

On server1.example.com, open Firefox and point the browser to the URL http://localhost. You should see the default web page. Try opening the same page from tester1.example.com, using the IP address of the web server (i.e., [http://172.16.0.100](http://172.16.0.100)). What output do you get?

**4.**   Check the current firewall zone and set the zone to dmz:

![Images](f0348-04.jpg)

**5.**   Add the http service to the current default zone:

![Images](f0348-05.jpg)

**6.**   From tester1.example.com, point the Firefox browser to [http://172.16.0.100](http://172.16.0.100) (substitute accordingly if the IP address of your server1.example.com machine differs). You should see the default test page of the web server.

**7.**   Remember that during Red Hat exams, all changes must survive a system reboot. Reboot your system and check if you can still access the web server’s test page. If not, you may have forgotten to enable Apache to start at boot or to make your firewall changes permanent.

##### Lab 3

In this lab you run the web server on TCP port 81 rather than on port 80\. To do so, you will have to update the http service on the firewall to allow port 81 in addition to the default port 80.

**1.**   Open the /etc/httpd/conf/httpd.conf file and change the **Listen 80** directive to **Listen 81**.

**2.**   Restart the httpd service:

`# systemctl restart httpd`

**3.**   The test web page should be visible from the local server1 machine after you point the browser to [http://localhost:81](http://localhost:81).

**4.**   From another system such as tester1, you should not be able to load the page.

**5.**   From the GNOME terminal, run **firewall-config** on server1\. Select Permanent from the Configuration drop-down menu. Then, select the Services tab, scroll until you find the http service, click Add, and enter **81** for the port number in the window. Choose Options | Reload Firewalld to reload the configuration. If you performed all the changes correctly, you should be able to load the test web page from tester1.

**6.**   Next, reboot server1:

`# reboot`

##### Lab 4

This lab is similar to Lab 3, but because you’ll be running the web server on a nonstandard port, you will need to configure SELinux to label the new port.

**1.**   Open the /etc/httpd/conf/httpd.conf file and change the **Listen** directive to **Listen 82**.

**2.**   Restart the httpd service:

`# systemctl restart httpd`

After restarting the web service, you should see an error. The error message suggests to run the **journalctl -xeu httpd.service** command. If you do so and check the logs, you will find that the server cannot bind to TCP port 82\. A similar error should also appear in /var/log/messages, but in this case you should also notice that the error is caused by SELinux. This is because TCP port 82 is not included in the list of ports for the http_port_t type:

`# semanage port -l | grep http_port_t`

To fix this, run the following command:

`# semanage port -a -t http_port_t -p tcp 82`

Then, start the httpd service. This time, you should not see any errors:

`# systemctl start httpd`

**3.**   From the GNOME terminal, run **firewall-config** on server1\. Select Permanent from the Configuration drop-down menu. Then, select the Services tab, scroll until you find the http service, click Add, and enter **82** for the port number in the window. Choose Options | Reload Firewalld to reload the configuration.

**4.**   If you performed all the changes correctly, you should be able to load the test web page from tester1.

##### Lab 5

This lab assumes that you have completed the configuration of the Apache web server that you have set up from the previous labs.

**1.**   Open the /etc/httpd/conf/httpd.conf file and change the **Listen** directive to **Listen 80**.

**2.**   Restart the httpd service:

`# systemctl restart httpd`

**3.**   Create the new web page as suggested in the lab instructions:

`# echo "Hello world!" > /var/www/html/index.html`

**4.**   If successful, you should see the new test web page from a browser running on tester1.example.com and pointing to the URL http://172.16.0.100 (substitute for the IP address of server1, if different).

**5.**   Create the directory /html:

`# mkdir /html`

**6.**   You should have modified the **DocumentRoot** directive and added a new stanza to the /etc/httpd/conf/httpd.conf file, which should look as shown next:

![Images](f0350-05.jpg)

**7.**   Create the new web page as suggested in the lab instructions:

![Images](f0350-06.jpg)

**8.**   Restart the httpd service:

`# systemctl restart httpd`

**9.**   You should not be able to display the new test page from a browser. If you look in /var/log/messages, you should find an error from SELinux stating that SELinux is preventing /usr/sbin/httpd from getattr access on the file /html/index.html. This is because the file does not have the right SELinux contexts. You can set the correct context by copying that of /var/www/html as a reference:

![Images](f0351-01.jpg)

This will fix the issue, but the change will not survive a relabeling of the filesystem. To make the change persistent, check the file context on the /var/www/html directory (**ls -dZ /var/www/html**), and define a new file context rule to apply the same context to /html, as shown next:

![Images](f0351-02.jpg)

##### Lab 6

**1.**   On tester1.example.com, create the user bob:

![Images](f0351-03.jpg)

**2.**   On tester1, generate a new SSH key pair for user bob:

![Images](f0351-04.jpg)

**3.**   On server1.example.com, create the user alice:

![Images](f0351-05.jpg)

**4.**   On tester1 as user bob, copy the public SSH key to user alice’s home directory on server1 (substitute the IP address with that of your instance of server1, if different):

`$ ssh-copy-id alice@172.16.0.100`

**5.**   Finally, bob on tester1 should be able to SSH to alice@172.16.0.100 without being prompted for a password (substitute the IP address with that of your instance of server1, if different).

## Chapter 9

## System Administration Tasks

CERTIFICATION OBJECTIVES

[9.01     Resource Management and System Tuning](#ch09.xhtml_ch9obj01)

[9.02     Archives and Compression](#ch09.xhtml_ch9obj02)

[9.03     Running Tasks on a Schedule: cron and at](#ch09.xhtml_ch9obj03)

[9.04     Bash Scripts](#ch09.xhtml_ch9obj04)

[9.05     Local Log Files](#ch09.xhtml_ch9obj05)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

This chapter covers functional system administration tasks not already covered in other chapters. The chapter starts with a discussion of process management and continues with system tuning. It then covers the creation and management of archive files.

In addition, this chapter helps you automate repetitive system administration tasks. Some of these tasks happen when you want to have a “life,” others when you’d rather be asleep. In this chapter, you’ll learn how to schedule both one-time and periodic execution of jobs. This is made possible with the **cron** and **at** daemons. In this case, “at” is not a preposition, but a service that monitors a system for one-time scheduled jobs. In a similar fashion, cron is a service that monitors a system for regularly scheduled jobs.

Bash scripting is also highlighted as an indispensable tool for automation, enabling you to create complex workflows and automate multi-step tasks efficiently.

When you’re troubleshooting, system logging often provides the clues you need to solve a lot of problems. The focus in this chapter is local logging.

INSIDE THE EXAM

**Resource Management and System Tuning**

Administrators work on Linux systems in a number of ways. In this chapter, you’ll learn various methods for meeting the following RHCSA objectives. The first of these objectives involves identifying resource-intensive processes and taking corrective actions, such as adjusting process scheduling or setting a system tuning profile:

![Images](square.jpg)   Identify CPU/memory-intensive processes and kill processes

These other objectives are more closely related to system administration:

![Images](square.jpg)   Adjust process scheduling

![Images](square.jpg)   Manage tuning profiles

**Archives and Compression**

Commands such as **tar** and **gzip** are often used for system backups. Therefore, they are essential tools for a system administrator. The corresponding RCHSA objective is

![Images](square.jpg)   Archive, compress, unpack, and uncompress files using **tar**, **star**, **gzip**, and **bzip2**

**Running Tasks on a Schedule: cron and at**

By default, every RHEL 9 system comes with preconfigured jobs that run on a schedule to perform essential maintenance tasks. System administrators can manage those jobs and configure new ones using the **at** and **cron** commands, as listed in the following exam objective:

![Images](square.jpg)   Schedule tasks using **at** and **cron**

**Bash Scripts**

The automation of system administration tasks is perhaps the most important skill for a system administrator. That means that you should be able to create shell scripts. And because the default shell of RHEL 9 is the Bourne-again shell (or bash), that means that you need to know how to write scripts using bash. There are four RHCSA objectives related to this skill:

![Images](square.jpg)   Conditionally execute code (use of: **if**, **test**, **[]**, etc.)

![Images](square.jpg)   Use Looping constructs (**for**, etc.) to process file, command line input

![Images](square.jpg)   Process script inputs ($1, $2, etc.)

![Images](square.jpg)   Processing output of shell commands within a script

**Local Log Files**

Finally, you will look at where to find information logged by the systemd journal and rsyslog. The related RHCSA objectives are

![Images](square.jpg)   Locate and interpret system log files and journals

![Images](square.jpg)   Preserve system journals

### CERTIFICATION OBJECTIVE 9.01

### Resource Management and System Tuning

Several system administration commands in the RHCSA objectives are not covered in previous chapters. They’re associated with process management and system tuning. Process management commands allow you to see what processes are running, to check the resources they’re using, and to kill or restart those processes. System tuning profiles apply special configuration settings to optimize a system’s performance for a specific usage, such as a desktop or a database server.

#### System Resource Management Commands

Linux includes a variety of commands that can help you identify those processes that are running on a system. The most basic of those commands is **ps**, which provides a snapshot of currently running processes. Those processes can be ranked with the **top** command, which can display running Linux tasks in order of their resource usage. With **top**, you can identify those processes that are using the most CPU and RAM memory. Commands that can adjust process priority include **nice** and **renice**. Sometimes it’s not enough to adjust process priority, at which point it may be appropriate to send a signal to a process with commands such as **kill** and **killall**. If you need to monitor system usage, the **sar** and **iostat** commands can also be helpful.

![Images](exam.jpg)

**The objectives related to system resource management are to “identify CPU/memory-intensive processes and kill processes” and to “adjust process scheduling.”**

##### Process Management with the ps Command

It’s important to know what’s running on a Linux computer. To help with that task, the **ps** command has a number of useful switches. When you’re trying to diagnose a problem, one common practice is to start with the complete list of running processes and then look for a specific program. For example, if the Firefox web browser were unresponsive and using most of CPU cycles, you’d want to kill any associated processes. The **ps aux | grep [f]irefox** command could then help you identify the process(es) that you need to kill. Note the square brackets around “f”: these prevent the **grep** command itself from appearing in the results when searching for the **firefox** process. It’s a technique used to exclude the **grep** process from the output.

![Images](job.jpg)

**The** pgrep **command is also useful because it combines the features of** ps **and** grep. **In this case, the** pgrep -a firefox **command is functionally equivalent to** ps aux | grep firefox.

The **ps** command by itself is usually not enough. All it does is identify those processes running in the current terminal. This command typically returns just the process associated with the current shell and the **ps** command process itself.

To identify those processes associated with a username, the **ps -u *username*** command can help. Sometimes there are specific users who may be problematic for various reasons. So if you’re suspicious of user mjang, the following command can help you review every process currently associated with that user:

`$ ps -u mjang`

As an administrator, you may choose to focus on a specific account for various reasons, such as activity revealed by the **top** command, described in the next section. Alternatively, you may want to audit all currently running processes with a command such as the following:

`$ ps aux`

The **ps aux** command gives a more complete database of currently running processes, in order of their PIDs. The **a** option lists all running processes, the **u** option displays the output in a user-oriented format, and the **x** option lifts the standard limitation that listed processes must be associated with a terminal or console. One example is shown in [Figure 9-1](#ch09.xhtml_ch9fig1). While the output can include hundreds of processes and more, the output can be redirected for further analysis with commands such as **grep**. The output columns shown in [Figure 9-1](#ch09.xhtml_ch9fig1) are described in [Table 9-1](#ch09.xhtml_ch9tab1).

FIGURE 9-1 Output from the ps aux command

![Images](F09-01.jpg)

TABLE 9-1 Columns of Output from ps aux

![Images](f0358-01.jpg)

Incidentally, you may note that the **ps aux** command does not include the familiar dash in front of the **aux** switches. In this case, the command works with and without the dash (although slightly differently). Valid command options with the dash are also known as UNIX or POSIX style; in contrast, options without the dash are known as BSD style. The following alternative includes current environment variables for each process:

`$ ps eux`

Processes can be organized in a tree format. Specifically, the first process, with a PID of 1, is systemd. That process is the base of the tree, which may be shown with the **pstree** command. In a few cases, it’s not possible to use a standard **kill** command to kill a process. In such cases, look for the “parent” of the process in the tree. You can identify the parent of a process, known as the PPID, with the following command:

`$ ps axl`

The **l** switch displays the output in long format and is not compatible with the **u** switch. You can view the PID and PPIDs of all running processes as shown in [Figure 9-2](#ch09.xhtml_ch9fig2).

FIGURE 9-2 Output from the ps axl command

![Images](F09-02.jpg)

With the **-Z** switch (that’s an uppercase Z), the **ps** command can also identify the SELinux contexts associated with a process. For example, the **ps -efZ** command includes the SELinux contexts of each process at the start of the output. If you’ve read [Chapter 8](#ch08.xhtml), the contexts should already seem familiar. For example, consider the context of the vsFTP server process in the following excerpt:

![Images](f0359-01.jpg)

Contrast that with the context of the **vsftpd** executable. The actual vsFTP process runs under the system_r role, while the executable has role object_r:

![Images](f0359-02.jpg)

As you can see, context types are also different. The **vsftpd** process runs with context type ftpd_t, while, the **vsftpd** executable has context type ftpd_exec_t. The role of different daemons and their corresponding executable files should match and contrast in a similar fashion.

##### View Loads with the top Task Browser

The **top** command sorts active processes first by their CPU load and RAM memory usage. Take a look at [Figure 9-3](#ch09.xhtml_ch9fig3). It provides an overview of the current system status, starting with the current uptime, number of connected users, active and sleeping tasks, CPU load, and more. The output is, in effect, a task browser.

FIGURE 9-3 Output from the top command

![Images](F09-03.jpg)

The default sort field is CPU usage. In other words, the process that’s taking the most CPU resources is listed first. You can change the sort field with the help of the left and right directional (<, >) keys. Most of the columns are the same as shown in [Figure 9-2](#ch09.xhtml_ch9fig2), as detailed in [Table 9-1](#ch09.xhtml_ch9tab1). The additional columns are described in [Table 9-2](#ch09.xhtml_ch9tab2).

TABLE 9-2 Additional Columns of Output from top

![Images](f0360-01.jpg)

One problem with the **top** and **ps** commands is that they display the status of processes on a system as a snapshot in time. That may not be enough. Processes may load a system for just a blip of time, or even periodic blips in time. One way to find more information about the overall load on a system is with two commands from the sysstat package: **sar** and **iostat**. That system activity information is logged courtesy of the **sa1** and **sa2** commands, which will be described shortly.

##### System Activity Reports with the sar Command

The **sar** command is provided by the sysstat RPM package. After installing the sysstat package, start the sysstat service and enable the service to start at boot:

![Images](f0360-02.jpg)

Note that the last command enables not only the sysstat service but also two dependent units, sysstat-collect.timer and sysstat-summary.timer.

In essence, **sar** can be used to provide a system activity report. For example, [Figure 9-4](#ch09.xhtml_ch9fig4) shows the output of the **sar** command. As you can see, the output shows various CPU measures at different points in time. The default settings measure CPU load at 10-minute intervals. This system has two logical CPUs, which are measured individually and as a whole. The high %idle numbers shown in the figure are a good sign that the CPU is not being overloaded; however, the figure shows the load for less than an hour.

FIGURE 9-4 Output from the sar command

![Images](F09-04.jpg)

The 10-minute intervals associated with the **sar** command output are driven by the sysstat-collect.timer systemd unit, in the /usr/lib/systemd/system directory. The output from those reports is collected in log files in the /var/log/sa directory. The filenames are associated with the numeric day of the month; for example, system activity report status for the 15th of the month can be found in the sa15 file in the noted directory. However, such reports are normally stored at least for the last 28 days, based on the following default in the /etc/sysconfig/sysstat file:

`HISTORY=28`

##### Variations on sar with sa1 and sa2

The **sa1** and **sa2** commands are often used to collect system activity report data. In the system-collect.service system unit, the **sa1** command is used to gather system activity data every 10 minutes. In the system-summary.service unit, the **sa2** command writes a daily report in the /var/log/sa directory.

##### CPU and Storage Device Statistics with iostat

In contrast to **sar**, the **iostat** command reports more general input/output statistics for the system, not only for the CPU but also for connected storage devices, such as local drives and mounted shared NFS directories. The example shown in [Figure 9-5](#ch09.xhtml_ch9fig5) displays information for the CPU and the storage devices since system startup on server1.example.com.

FIGURE 9-5 CPU and storage device statistics

![Images](F09-05.jpg)

Both the **sar** and **iostat** commands can capture statistics at regular intervals. As an example, the following command shows CPU and storage device statistics every five seconds and stops after a minute (12 reports):

`# iostat 5 12`

##### nice and renice

The **nice** and **renice** commands can be used to manage the priority of different processes. Whereas the **nice** command is used to start a process with a different priority, the **renice** command is used to change the priority of a currently running process.

Process priorities in Linux specify numbers that seem counterintuitive. The range of available nice numbers can vary from –20 to 19\. The default nice number of a process is inherited from the parent and is usually 0\. A process given a priority of 19 will have to wait until the system is almost completely free before taking any resources. In contrast, a process given a priority of –20 takes precedence over all other processes. In practice, this is true for almost all processes because “real-time” tasks take precedence over the lowest nice value of –20\. But this is outside of the scope of the RHCSA exam, so ignore the existence of real-time processes for now, and for the sake of this discussion assume that all normal processes can be assigned a nice value from –20 to 19.

The **nice** command prefaces other commands. For example, if you have an intensive script to be run at night, you might choose to start it with a command like the following:

`# nice -n 19 ./intensivescript`

Note that only the root user can assign nice priorities less than 0. The preceding command starts the noted script with the lowest possible priority.

Sometimes a program is just taking up too many resources. If you don’t want to kill a process, you can lower its priority with the **renice** command. Normally, the easiest way to identify a process that’s taking up too many resources is with the **top** command. Identify the PID that’s taking up too many resources. That PID number is in the left-hand column of the output.

If the PID of your target process is 1234, the following command would change the nice number of that process to 10, which gives that process a lower priority than the default of 0:

`# renice -n 10 1234`

If you want to decrease the nice level of a process, you must run **renice** as root. Even though the output of the command refers to the “priority,” it really is just listing the old and new “nice” numbers for the process:

`1234: old priority 0, new priority, 10`

The new nice number is shown in the output to the **top** command, under the NI column.

##### Process-Killing Commands

Sometimes, it’s not enough to reprioritize a process. Some processes can just overwhelm a system. In most cases, you can stop such difficult processes with the **kill** and **killall** commands. In many cases, you can kill a process directly from the **top** task browser.

If there’s a situation where a process is taking up a lot of memory or CPU, it’s probably slowing down everything else running on that system. As shown in [Figure 9-6](#ch09.xhtml_ch9fig6), Firefox has loaded the CPU of the noted system pretty heavily. If it were unresponsive, we’d press **k** from the **top** task browser.

FIGURE 9-6 The top task browser with heavy Firefox load

![Images](F09-06.jpg)

As shown in [Figure 9-6](#ch09.xhtml_ch9fig6), the **k** command reveals the PID To Signal/Kill: prompt, where we enter the PID of the Firefox process or accept the default of 4537, which appears to be Firefox. It applies the default signal (SIGTERM) to the process with that PID number.

Of course, you could apply the **kill** command directly to a PID number. For example, the following command is equivalent to the steps just described in the **top** task browser:

`# kill 4537`

The **kill** command can be run by the owner of a process from his account. Thus, user alex could run the **kill 4537** command from his regular account because he has administrative privileges over processes associated with his username.

Despite its name, the **kill** command can send a wide variety of signals to different processes. For a full list, run the **kill -l** command or type **man 7 signal**. [Table 9-3](#ch09.xhtml_ch9tab3) lists some of the most common signals.

TABLE 9-3 A List of Common POSIX Signals

![Images](f0364-01.jpg)

Before the advent of systemd and scripts in the /etc/init.d directory, the **kill -1** command was used to send a configuration reload signal to service daemons. For example, if the PID number of the main process associated with the Apache web server is 2059, the following command is functionally equivalent to the **systemctl reload httpd** command:

`# kill -1 2059`

Without the **-1** switch (and that’s a dash number 1), the **kill** command, under normal circumstances, would terminate the given process. In this case, it would terminate the Apache web server. But sometimes, processes get stuck. In some such cases, the **kill** command does not work by itself. The process continues running. In that case, you can try two things.

First, you could try the **kill -15** command, which sends the SIGTERM signal, attempting to kill the process cleanly. If the process will not exit cleanly, **kill -9** can be used to stop a process “uncleanly” by sending a SIGKILL signal. If it is successful, other related processes may still remain in operation.

Sometimes, a number of processes are running under the same name. For example, the Apache web server starts several processes that run simultaneously. It’s at best inefficient to kill just one process; the following command would kill all currently running server processes, assuming no other issues:

`# killall httpd`

#### System Tuning Profiles

The Linux kernel has hundreds of settings that can be tuned to improve a system’s performance. Some of those parameters are configurable via the **sysctl** command and the /etc/sysctl.conf file, others from the /sys filesystem, or by adding special boot options to the Linux kernel.

Covering all the possible tunable settings would require a book on its own. Luckily, RHEL 9 comes with **tuned**, a daemon that simplifies the daunting and complex process to optimize a system for best performance.

The tuned service should be installed and enabled by default on every RHEL 9 system. If the package is not present, run

`# dnf -y install tuned`

You can enable and start the service with the following commands:

![Images](f0365-02.jpg)

##### Listing tuned Profiles

The configuration of **tuned** is based on predefined profiles. Of course, you can add and define your own profiles, but this is out of the scope of the RHCSA exam.

To interact and configure the tuned service, use the **tuned-adm** command. For example, **tuned-adm list** shows a list of all available profiles; the output is shown in [Figure 9-7](#ch09.xhtml_ch9fig7).

FIGURE 9-7 tuned profiles

![Images](F09-07.jpg)

As you can see, ten different profiles are available. The output also shows that the currently active profile on the system is virtual-guest. You could obtain the same information by running

![Images](f0365-03.jpg)

[Table 9-4](#ch09.xhtml_ch9tab4) describes the purpose of each profile. Note that the list of profiles in your system might be slightly different, because Red Hat continuously reviews and introduces new profiles across new versions of RHEL.

TABLE 9-3 Default tuned Profiles

![Images](f0366-01.jpg)

##### Switching tuned Profiles

Switching to a different profile is achieved by the **tuned-adm profile** command. For example, to change to the throughput-performance profile, run

`# tuned-adm profile throughput-performance`

The new tuning optimizations are applied immediately, and the changes are persistent after a system reboot. To confirm the current profile, run

![Images](f0367-01.jpg)

After installation, the **tuned** daemon determines the best profile for your system and selects that one as the default. If you have switched to another profile and don’t remember which one was the default profile that **tuned** selected, you can run

![Images](f0367-02.jpg)

### CERTIFICATION OBJECTIVE 9.02

### Archives and Compression

Linux includes a variety of commands to archive groups of files. Some archives can be reprocessed into packages such as RPMs. Other archives are just used as backups. In either case, archives can be a terrific convenience, especially when compressed. This section explores the archive and compression commands specifically cited in the RHCSA objectives. These “essential tools” include the **gzip**, **bzip2**, **tar**, and **star** commands.

#### gzip and bzip2

The **gzip** and **bzip2** commands are functionally similar as they compress and decompress files, just using different algorithms. The **gzip** command uses the DEFLATE algorithm, whereas the **bzip2** command uses the Burrows-Wheeler block sorting algorithm. While they both work well, the **bzip2** command has a better compression ratio. For example, either of the two following commands could be used to compress a big document file named big.doc:

![Images](f0367-03.jpg)

This adds a .gz or a .bz2 suffix to the file, compressed to the associated algorithms. With the **-d** switch, you can use the same commands to reverse the process:

![Images](f0367-04.jpg)

As an alternative, the **gunzip** and **bunzip2** commands can be used for the same purpose.

#### tar

The **tar** command was originally developed for archiving data to tape drives. However, it’s commonly used today for collecting a series of files, especially from a directory, in a single archive file. For example, the following command backs up the information from the /home directory in the home.tar.gz file:

`# tar czvf home.tar.gz /home`

Like the **ps** command, this is one of the few commands that does not require a dash in front of the switch. This particular command creates (**c**) an archive, compresses (**z**) it, in verbose (**v**) mode, with the filename (**f**) that follows. Alternatively, you can extract (**x**) from that file with the following command:

`# tar xzvf home.tar.gz`

The compression specified (**z**) is associated with the **gzip** command; if you wanted to use **bzip2** compression, substitute the **j** switch. The **tar** command can store and extract access control list settings or SELinux attributes with the **--selinux** option.

If you have a tar archive created without the **--selinux** option, you can compensate. You can use commands such as **restorecon**, as described in [Chapter 8](#ch08.xhtml), to restore the SELinux contexts of an archive.

#### star

The **star** command gained some popularity because it was the first to introduce support for archiving files in an SELinux system. As the **star** command is not normally installed, you’ll need to install it; one method is with the following command:

`# dnf install star`

Unfortunately, the **star** command doesn’t quite work in the same fashion as **tar**. If you ever have to use the **star** command, do practice the command. For example, the following command would create an archive, with all SELinux contexts, from the current /home directory:

`# star -xattr -H=exustar -c -f=home.star /home/`

The **-xattr** switch saves the extended attributes associated with SELinux. The **-H=exustar** switch records the archive using the exustar format, which allows you to store ACLs if the **-acl** option is specified. The **-c** creates a new archive file. The **-f** specifies the name of the archive file.

Once the archive is created, it can be unpacked with the following command, which extracts the archive:

`# star -x -f=home.star`

If desired, the archive can be compressed with the aforementioned **gzip** or **bzip2** command, or from **star** with the **-z** or **-bz** command-line option. The **star -x** command can detect and restore files from archives configured with various compression schemes. For example, based on a **gzip**-compressed archive, the **star** command unpacks that archive, as noted by the following log information message:

![Images](f0369-01.jpg)

### CERTIFICATION OBJECTIVE 9.03

### Running Tasks on a Schedule: cron and at

The cron system is essentially a smart alarm clock. When the alarm sounds, Linux runs the commands of your choice automatically. You can set the alarm clock to run at all sorts of regular time intervals. Many cron jobs are scheduled to run during the middle of the night, when user activity is lower. Of course, that timing can be adjusted. Alternatively, the **at** system allows users to run the commands of their choice, once, at a specified time in the future.

![Images](exam.jpg)

**Because** cron **always checks for configuration changes, you do not have to restart cron every time a change has been made.**

RHEL 9 installs the **cron** daemon by default and incorporates the anacron system in cron. The **cron** daemon starts jobs on a regular schedule. The anacron system helps the **cron** daemon work on systems that are powered off, such as desktops or laptops. This ensures that important jobs are always run, even if a system was powered off for a period of time.

The cron system is configured to check the /var/spool/cron directory for jobs by user. In addition, it incorporates jobs defined in the /etc/anacrontab file, based on the 0anacron script in the /etc/cron.hourly directory. It also checks for scheduled jobs for the computer described in the /etc/crontab file and in the /etc/cron.d directory.

#### The System crontab and Components

The /etc/crontab file is set up in a specific format. Each line can be blank, a comment (which begins with #), a variable, or a configuration line. Naturally, blank lines and comments are ignored. In some Linux distributions, that file includes a schedule of jobs. In RHEL 9, the default crontab file just includes the format for other related configuration files.

Users run regular commands. Anyone who runs a new process, whether it be you or a daemon, inherits an “environment” that is made of various environment variables. To see the environment variables for the current user, run the **env** command. If that user is your account, some of the standard variables in RHEL include **HOME**, which should match your home directory, **SHELL**, which should match the default shell, and **LOGNAME** as the username.

Other variables can be set in the /etc/crontab and other cron files (in /etc/cron.d, /etc/cron.daily, and so on):

`Variable=Value`

Some variables are already set for you. For example, **MAIL** is **/**var/spool/mail/michael if your username is michael, **LANG** is en_US.UTF-8, and **PATH** is where the shell looks for commands. You can set these variables to different values in various cron configuration files. For example, the default /etc/crontab file includes the following variables:

![Images](f0370-02.jpg)

Note that the **PATH** variable in a cron configuration file may be different from the **PATH** variable associated with a shell. In fact, the two variables are independent. Therefore, you’ll want to specify the exact path of every command in each cron configuration file if it isn’t in the crontab **PATH**.

![Images](job.jpg)

**The** MAILTO **variable can help you administer several Linux systems. The** cron **daemon sends by e-mail any output that a job sends to** stdout **or** stderr**. Just add a line such as MAILTO=me@example.net to route all the output of cron jobs to that e-mail address.**

The format of a line in /etc/crontab is now detailed in comments, as shown in [Figure 9-8](#ch09.xhtml_ch9fig8). Each of these columns is explained in more detail in [Table 9-5](#ch09.xhtml_ch9tab5).

FIGURE 9-8 The format of a crontab

![Images](F09-08.jpg)

TABLE 9-5 Columns in a cron Configuration File

![Images](f0371-01.jpg)

If you see an asterisk in any column, the **cron** daemon runs that command for all possible values of that column. For example, an * in the minute field means that the command is run every minute during the specified hour(s). Consider the example shown here:

![Images](f0370-03.jpg)

This line runs the **ls** command every April 3 at 5:01 A.M. The asterisk in the day of week column simply means that it does not matter what day of the week it is; **crontab** still runs the **ls** command at the specified time.

The entries associated with the **cron** daemon are flexible. For example, a 7–10 entry in the hour field would run the specified command at 7:00 A.M., 8:00 A.M., 9:00 A.M., and 10:00 A.M. A list of entries in the minute field, such as 0,5,10,15,20,25,30,35,40,45,50,55, would run the specified command every five minutes. But that’s a lot of numbers. The entry */5 in the minute field would lead to the same result. The **cron** daemon also recognizes abbreviations for months and the day of the week.

The actual command is the sixth field. You can set up new lines with a percent (**%**) symbol. All the text after the first percent sign is sent to the command as standard input. This is useful for formatting standard input. The following is an example of a cron file:

![Images](f0371-02.jpg)

#### Hourly cron Jobs

Now it’s time for some sample cron files. The files and scripts discussed are limited to those seen on the server1.example.com system. A number of different packages add their own cron jobs. Certain jobs associated with the **cron** daemon are run every hour, based on the 0hourly script in the /etc/cron.d directory. This file includes the same variables as the /etc/crontab file just described. For hourly jobs, it includes one line:

![Images](f0372-01.jpg)

Given the information provided in the preceding section, you should be able to read this line. The **run-parts** command loads each script in the directory that follows; the scripts in that directory are executed as the root user. Of course, the first five columns specify the time; the scripts are run at one minute past the hour, every hour, every day, every month, on each day of the week.

The script of interest in the /etc/cron.hourly directory is 0anacron, which reviews the contents of the /var/spool/anacron/cron.daily file to see if the **anacron** command has been run in the current day. If not, and if the system is not running on battery (for example, on a laptop disconnected from main power), the **/usr/sbin/anacron -s** command is executed, which runs scripts defined in the /etc/anacrontab configuration file.

#### Regular anacron Jobs

The 0anacron script in the /etc/cron.hourly directory described earlier executes the **anacron** command after a system has been powered up. That command executes three scripts defined in the /etc/anacrontab file. This includes three environment variables that should seem familiar:

![Images](f0372-02.jpg)

The **SHELL** directive may appear a bit different, but the **ls -l /bin/sh** command should confirm a symbolic link to the **/bin/bash** command, which starts the default bash shell. The following directive means that scripts are run at a random time of up to 45 minutes after the scheduled time:

`RANDOM_DELAY=45`

With the following directive, anacron jobs are run only between the hours of 3 A.M. and 10:59 P.M.

`START_HOURS_RANGE=3-22`

While the format of /etc/anacrontab is similar to the format listed in a script for a regular cron job, there are differences. The order of data in each line is specified by the following comment:

![Images](f0373-01.jpg)

The period in days is 1, 7, or @monthly, because the number of days in a month varies. The delay in minutes is associated with the **RANDOM_DELAY** directive. Since the /etc/anacrontab file is executed through the /etc/cron.d/0hourly script, the clock starts one minute after the hour, after the system has been started. The delay in minutes comes before the **RANDOM_DELAY** directive.

In other words, based on the following line, the scripts in the /etc/cron.daily directory may be run anywhere from 5 to 50 minutes after the **anacron** command is run, or 6 to 51 minutes after the hour:

![Images](f0373-02.jpg)

For more examples, review some of the scripts in the /etc/cron.daily directory. A key script you may want to investigate is **logrotate**, which is used to archive or remove old log files.

#### Setting Up cron for Users

Each user can use the **crontab** command to create and manage cron jobs for their own accounts. Four switches are associated with the **crontab** command:

![Images](square.jpg)   **-u *user*** Allows the root user to edit the crontab of another specific user.

![Images](square.jpg)   **-l** Lists the current entries in the crontab file.

![Images](square.jpg)   **-r** Removes cron entries.

![Images](square.jpg)   **-e** Edits an existing **crontab** entry. By default, **crontab** uses vi, unless a different editor is specified via the **EDITOR** environment variable.

To set up cron entries on your own account, start with the **crontab -e** command. Normally, it opens a file in the vi editor, where you can add appropriate variables and commands, similar to what you’ve seen in other cron job files.

Once the cron job is saved, you can confirm the change with either the **crontab -l** command or, as the root user, by reading the contents of a file in the /var/spool/cron directory associated with a username. All current cron jobs for a user can be removed with the **crontab -r** command.

EXERCISE 9-1

**Create a cron Job**

In this exercise, you will modify your crontab to read a text file at 1:05 P.M. every Monday in the month of January. To do this, use the following steps:

1.   Log in as a regular user.

2.   Create a ~/bin directory. Add a file called taxrem.sh, which reads a text file from your home directory. A command such as the following in the taxrem.sh file should suffice:

![Images](f0374-01.jpg)

Make sure to add appropriate lines to the reminder.txt file in your home directory, such as “Don’t forget to do your taxes!” Make sure the taxrem file is executable with the **chmod +x ~/bin/taxrem.sh** command.

3.   Open the crontab for your account with the **crontab -e** command.

4.   Add an appropriate command to the crontab. Based on the conditions described, it would read as follows:

![Images](f0374-02.jpg)

5.   Don’t forget directives such as **MAILTO=user@example.com** at the start of the crontab.

6.   Save and exit. Run **crontab -l** and confirm the existence of the user cron file in the /var/spool/cron directory. That file should have the same name as the user.

#### Running a Job with the at System

Like **cron**, the **at** daemon supports job processing. However, you can set an **at** job to be run once. Jobs in the cron system must be set to run on a regular basis. The **at** daemon works in a way similar to the print process; jobs are spooled in the /var/spool/at directory and run at the specified time.

You can use the **at** daemon to run the command or script of your choice. For the purpose of this section, assume that user michael has created a script named 797.sh in his home directory to process some airplane sales database.

From the command line, you can run the **at *time*** command to start a job to be run at a specified time*.* Here, *time* can be now; in a specified number of minutes, hours, or days; or at the time of your choice. Several examples are illustrated in [Table 9-6](#ch09.xhtml_ch9tab6).

TABLE 9-6 Examples of the at Command

![Images](f0375-01.jpg)

You can use one of the sample commands shown in [Table 9-6](#ch09.xhtml_ch9tab6) to open an **at** job. It opens a different command-line interface, where you can specify the command of your choice. For this example, assume you’re about to leave work and want to start the job in an hour. From the conditions specified, run the following commands:

![Images](f0375-02.jpg)

The CTRL-D command exits the **at** shell and returns to the original command-line interface. As an alternative, you can use input redirection, as follows:

![Images](f0375-03.jpg)

The **atq** command, as shown next, checks the status of the current **at** jobs. All jobs that are pending are listed in the output to the **atq** command.

![Images](f0375-04.jpg)

If there’s a problem with the job, you can remove it with the **atrm** command. For example, you can remove the noted job, labeled job 1, with the following command:

![Images](f0375-05.jpg)

#### Secure cron and at

You may not want everyone to be able to run a job in the middle of the night. You may also want to restrict this privilege for security reasons.

Users can be configured in /etc/cron.allow and /etc/cron.deny files. If neither of these files exists, **cron** usage is restricted to the root administrative user. If the /etc/cron.allow file exists, only users named in that file are allowed to use **cron**. If there is no /etc/cron.allow file, only users named in **/**etc/cron.deny can’t use **cron**.

These files are formatted as one line per user; if you include the following entries in /etc/cron.deny, and the /etc/cron.allow file does not exist, users elizabeth and nancy aren’t allowed to set up their own cron scripts:

![Images](f0376-01.jpg)

However, if the /etc/cron.allow file does exist with the same list of users, it takes precedence. In that case, both users elizabeth and nancy are allowed to set up their own cron scripts. The range of possibilities is summarized in [Table 9-7](#ch09.xhtml_ch9tab7).

TABLE 9-7 Security Effects of cron.allow and cron.deny

![Images](f0376-02.jpg)

User security for the **at** system is almost identical. The corresponding security configuration files are /etc/at.allow and /etc/at.deny. The range of possibilities is summarized in [Table 9-8](#ch09.xhtml_ch9tab8).

TABLE 9-8 Security Effects of at.allow and at.deny

![Images](f0376-03.jpg)

If you’re paranoid about security, it may be appropriate to include only desired users in the /etc/cron.allow and /etc/at.allow files. Otherwise, a security breach in a service account may allow a “black hat” hacker to run a **cron** or **at** script from the associated account.

### CERTIFICATION OBJECTIVE 9.04

### Bash Scripts

As discussed earlier in this chapter, RHEL 9 includes some system maintenance scripts, scheduled by the **cron** daemon. Those scripts are located in various files in the /etc/cron.* directories. We will analyze some of those scripts to introduce the basics of the bash shell, and cover some of the loop and condition structures. You’ll then have the skills you need to create simple shell scripts. Bash, an acronym for Bourne-again shell, is a Unix shell and command language developed by Brian Fox for the GNU Project as a free replacement for the original Bourne shell (sh) distributed with Unix. It provides a command-line interface for controlling and interacting with your RHEL operating system, and also allows you to create scripts to automate a complex series of commands.

#### A “Hello, World” Script

A key part of any bash script is the *shebang*. The shebang is the string **#!/bin/bash**, which is a special kind of comment that tells the operating system which interpreter should be used to execute the script. It must be the first line of your script. To write a simple “Hello, World” bash script, create a file (such as my_script.sh) with your favorite editor, and copy the following content:

![Images](f0377-01.jpg)

In the script, **#!/bin/bash** indicates that the script should be run using the bash shell, while **echo "Hello, World"** prints the string “Hello, World!” to the terminal.

On RHEL 9, the **/bin/sh** path is symbolically linked to **/bin/bash**. This means that using **/bin/sh** or **/bin/bash** will lead to the same result, and they can be used interchangeably.

![Images](job.jpg)

**Some Unix systems and Linux distributions (not RHEL) link the** /bin/sh **command to a shell other than bash. Unless** #!/bin/bash **is specified in the script, it may not be transferable to other distributions.**

To run the script, you first need to make it executable. You can do this with the **chmod** command:

`$ chmod +x my_script.sh`

Then, you can execute the script like so:

`$ ./my_script.sh`

If you try to run a script that is not executable, you would get the following error:

![Images](f0378-01.jpg)

Hence, if you get an error such as the preceding one, add the execute permission to the script file:

`# chmod +x /usr/local/bin/myscript`

Every bash script or command returns an exit value when it finishes running. This is a numerical value that represents whether the script completed successfully or encountered an error. By convention, an exit value of 0 indicates success, while any other value indicates an error. You can set the exit value of a script with the **exit** command. For example, **exit 0** indicates success, while **exit 1** indicates an error. If no **exit** command is provided, the exit value of the script will be the exit value of the last command in the script.

#### Bash Variables

You can use variables in bash to store data. Although it’s sometimes common to write variable names in uppercase letters in bash, keep in mind that you cannot start a variable name with a number.

The following example illustrates how you can assign a variable from the command line:

`# today=4`

Take care when assigning a variable to not add spaces around the equal (=) character. To display the value of a variable, use the **echo** command and add a dollar sign in front of the variable:

![Images](f0378-04.jpg)

You can also add braces around the variable name to avoid ambiguous expressions. For example, without braces, the following command would retrieve the value of the variable **$todayth** rather than the value of **$today**:

![Images](f0378-05.jpg)

You can use variables as part of arithmetic expressions. In bash, arithmetic expressions are enclosed in the **$((*expression*))** syntax. Here’s an example:

![Images](f0378-06.jpg)

But there’s more. Variables can also store the output of a command. There are two ways to do so: using the **$(*command*)** syntax and with backticks, **`*command*`**. Here’s an example of each:

![Images](f0379-01.jpg)

##### The Scope of Variables

In the previous example, we have seen that the variables that we declare in bash can be passed as arguments to other commands. But are those variables available to other scripts? For example, create a script with the following lines:

![Images](f0379-02.jpg)

Save the content to a file (for example, testvar), make it executable, assign a value to myvar, and then run the script:

![Images](f0379-03.jpg)

The script’s output is empty, so the value of myvar was not available to the script. To use shell variables with any command, you need to export those variables as *environment variables*, as shown next:

![Images](f0379-04.jpg)

Then, if you run the script again, you will find that the value of the myvar variable is now passed to the script:

![Images](f0379-05.jpg)

Environment variables are usually declared in either the ~/.bashrc file or ~/.bash_profile file on a user’s home directory, or in the corresponding global files, /etc/basrhc or /etc/profile. An example is the LANG environment variable, which tells programs which language and local setting to use.

Environment variables are useful to define variables that should be globally available to all programs. However, they are not very practical if you want to pass to a program parameters that change often. For that purpose, you can use command arguments, or positional parameters.

##### Parameters in Bash

In bash, a *parameter* is something that can store a value. Hence, a variable is a parameter. It is in fact a type of parameter denoted by a name. However, there are also two other types of parameters:

![Images](square.jpg)   **Special parameters** These parameters are represented by special characters, each with a specific meaning. For example, the special parameter $? stores the exit code of the last command executed.

![Images](square.jpg)   **Positional parameters** A series of parameters, $0 to $9, that store the command-line arguments.

Some of the most common special and positional parameters are listed in [Table 9-9](#ch09.xhtml_ch9tab9). We will cover positional parameters in more detail later in the chapter.

TABLE 9-9 Special and Positional Bash Parameters

![Images](f0380-01.jpg)

##### Parameters Expansion

A parameter’s value can be manipulated using some string substitution techniques known as *parameter expansion*. To illustrate these concepts, define a variable as shown next:

`# ch9=/home/mike/studyguide/ch9/ch9.gz`

The first parameter expansion construct is **${*parameter*:-*word*}**. This gives the value of **${*parameter*}** if the parameter is defined; otherwise, ***word*** is substituted:

![Images](f0380-03.jpg)

Another useful parameter expansion construct is **${*parameter*/*pattern*/*string*}**. This replaces the longest match of ***pattern*** with ***string***. As an example, suppose that you want to change the .gz extension to .tar.gz for the filename stored in the variable ch9:

![Images](f0380-04.jpg)

You can remove a matching suffix pattern with the parameter expansion sequences **${*parameter*#*word*}** and **${*parameter*##*word*}**. These remove, respectively, the shortest or longest occurrence of ***word***, starting the search from the beginning of the value of ***parameter***. An example is shown next:

![Images](f0381-02.jpg)

Similarly, the parameter expansion sequences **${*parameter*%*wor*d}** and **${*parameter*%%*word*}** remove the shortest or longest occurrence of ***word***, but starting the search from the end of the value of ***parameter***. This is exemplified here:

![Images](f0381-03.jpg)

A summary of the parameter expansion sequences is shown in [Table 9-10](#ch09.xhtml_ch9tab10).

TABLE 9-10 Parameter Expansion

![Images](f0381-01.jpg)

#### Bash Control Structures

Scripts are filled with various command constructs. Some groups of commands are executed only if a condition is met. Others are organized in a loop, which continues to run as long as a condition is satisfied. These command constructs are also known as *conditional and control structures.* Common commands include **for**, **if**, and **test**. The end of a loop may be labeled with a keyword such as **done** or **fi**. Some commands only exist in the context of others, which will be described in the subsections that follow.

##### Test Operators and Conditional Constructs

The **if** operator is primarily used to check if a condition is met, such as if a file exists. For example, the following command checks if the /etc/sysconfig/network file exists and is a regular file:

![Images](f0382-01.jpg)

The exclamation mark (**!**) is the “not” operator and negates the result of the test. The **-f** checks to see if the filename that follows is a currently existing regular file. Test operators are very common in bash shell scripts. Some of these operators are listed in [Table 9-11](#ch09.xhtml_ch9tab11).

TABLE 9-11 Test Operators for Bash Scripts

![Images](f0382-02.jpg)

INSIDE THE EXAM

**man test** is an excellent documentation resource to find all test operators in **bash**.

The **if** operator normally is associated with a **then** operator, and possibly an **else** operator, and the command is ended by an **fi** instruction. For example, consider the following hypothetical block:

![Images](f0383-01.jpg)

In this code, if the /etc/fstab file exists (courtesy of the **-e**), the command associated with the **then** operator is run. If that file is missing, the noted message is displayed.

##### An Example: The 0anacron Script

We summarized the intent of the 0anacron script earlier in this chapter, but we’ll analyze it in detail here. You can find the script in the /etc/cron.hourly directory. A copy of the script is shown in [Figure 9-9](#ch09.xhtml_ch9fig9).

FIGURE 9-9 The 0anacron script

![Images](F09-09.jpg)

The script starts with a shebang line, which tells Linux that this is a bash script. Then, there is the following **if** block:

![Images](f0383-02.jpg)

The **test** operator is sometimes used as a conditional within the **if**. For example, the line

![Images](f0384-01.jpg)

is functionally equivalent to

![Images](f0384-02.jpg)

This **if** block verifies whether the file /var/spool/anacron/cron.daily exists and is readable. If the test is successful, the content of the cron.daily file is saved into the **day** variable. In fact, the cron.daily file contains the last date (in YYYYMMDD format) that **anacron** was run.

The next lines contain another **if** block:

![Images](f0384-03.jpg)

This code compares two strings: the current date, as returned by the **date** command in YYYYMMDD format (note the backticks to substitute the output of the **date** command as the first operand in the test comparison), and the content of the **day** variable. As a good practice, the name of the **day** variable is enclosed in double quotes to prevent any special characters within the quoted string, apart from the dollar sign, to be interpreted by bash.

If the two dates are equal, the script exits immediately with a value of 0, indicating no errors. In other words, if **anacron** was already run today, the content of the /var/spool/anacron/cron.daily file would include today’s date. In this case, the script won’t run a second time and will exit with a value of 0.

The next section of code contains a **for** loop, which is explained in the next section. For now, it is sufficient to say that each of the following blocks of code will be executed for every power supply file in the directory /sys/class/power_supply:

![Images](f0384-04.jpg)

The purpose of the code in the **for** loop is to check whether the system runs on battery power or not. If the system is running on battery, the script does not run the **anacron** command, because this is I/O intensive and may drain too much power from the battery.

The first **if** conditional checks whether the type of the current power supply is Mains and the “online” file exists for the power supply. The **2>/dev/null** part is to suppress error messages by redirecting them to null.

Then, the second **if** conditional checks whether the current power supply is online (if the content of the “online” file is 1). If the condition is satisfied, that is, if the current power supply is online, then the **online** variable is set to 1 and the **for** loop is terminated (**break**) immediately; otherwise, it is set to 0.

Note the test expression:

![Images](f0385-01.jpg)

This gets the content of the file $psupply/online, suppressing any errors, appends the value “x” to it, and then compares this value with the string “1x”. Why append the “x” string? This is an old shell scripting trick to prevent errors if the content of the file is empty. To do so, “x” is appended to make the output a valid string.

Next, the script checks the value of the **online** variable. If it is 0 (that is, the system is not on AC power), the script terminates immediately with an exit value of 0\. Otherwise, the script runs the **anacron** command:

![Images](f0385-02.jpg)

In turn, **anacron** will read a list of jobs from /etc/anacrontab and execute them in sequential (**-s**) order.

##### Control Structures: The for Loop

The **for** loop executes a block of commands for all the items specified in a list. It’s fairly simple and has different forms. In the following example, the command in the **for** loop is executed three times, for each value of the variable **n** in the list 1, 2, 3:

![Images](f0385-03.jpg)

The output of the previous snippet of code is

![Images](f0385-04.jpg)

A more complex example is shown next. The **for** loop is executed for all the users in the system, as returned by the **getent passwd** command:

![Images](f0385-05.jpg)

In the first line, the **getent passwd** command returns all the users in the system. This may include users defined locally in /etc/passwd, as well as users defined in a central directory service such as LDAP. The output of the command is truncated to the first column (**-f 1**), defined by a separator character (**-d ":"**). This gives a list of usernames that the **for** loop can cycle through and assign to the **username** variable at each iteration.

Then, the previous code snippet executes the **groups** command, with each username as an argument. This command returns the groups that a user is part of, in the following format:

![Images](f0386-01.jpg)

The **cut -f 1 -d ":"** command extracts all the output after the column separator, and the result is saved in the **usergroups** variable. Finally, the result is displayed by the **echo** command.

##### Positional Parameters

You can use positional parameters to pass information to a script, in the same fashion that you would do with arguments in normal commands. In a bash script, the first command argument is saved in the special variable **$1**, the second in **$2**, and so forth. The total number of arguments is saved in the **$#** special variable. As an example, consider the following script:

![Images](f0386-02.jpg)

Save the code in a file named args.sh and make it executable with the **chmod +x args.sh** command. Then, run the program as shown:

![Images](f0386-03.jpg)

You should see the following output:

![Images](f0386-04.jpg)

In Exercise 9-2, you will have a chance to put these lessons into practice.

EXERCISE 9-2

**Create a Script**

In this exercise, you’ll create a script named get-shell.sh. The script takes a username as the first argument and displays the default shell of the indicated user, using the following format:

![Images](f0386-05.jpg)

If no argument is provided, the script must display the default shell of the current user. If more than one argument is given, the script must print the following error message and exit with a value of 1:

![Images](f0387-01.jpg)

If the user given as an argument does not exist, the script must display the following error message and exit with a value of 2:

![Images](f0387-02.jpg)

1.   Create a file named get-shell.sh and assign execute permissions to that file:

![Images](f0387-03.jpg)

2.   Open the file with your favorite editor. Start the script with the following line:

![Images](f0387-04.jpg)

3.   Add the following lines that check if the number of arguments (**$#**) is greater than one. If so, print an error message and exit with a value of 1:

![Images](f0387-05.jpg)

4.   Add the lines that follow. If no arguments have been passed, the script saves the name of the current user (**$USER**) in the **username** variable. Otherwise, the **username** variable takes the value of the first argument (**$1**). To express this logic, use the **if-then-else** construct:

![Images](f0387-06.jpg)

5.   Retrieve the user’s information. You can query the user database with the **getent passwd** command. This command returns user information from the local /etc/passwd file and from any configured directory systems:

![Images](f0387-07.jpg)

6.   Check the exit value of the previous command. Any nonzero exit value means that an error has occurred. If so, exit the program immediately with an exit status of 2:

![Images](f0387-08.jpg)

7.   Extract the user’s shell from the **userinfo** variable. This is the seventh field (**-f 7**) of /etc/passwd, where each field is separated by a column character (**-d ":"**):

![Images](f0388-01.jpg)

8.   Print the result. As a good practice, exit with a value of 0 to indicate that no errors have occurred:

![Images](f0388-02.jpg)

9.   Save your changes. Execute the script with different arguments to test every possible condition:

![Images](f0388-03.jpg)

### CERTIFICATION OBJECTIVE 9.05

### Local Log Files

An important part of maintaining a secure system is monitoring those activities that take place on the system. If you know what usually happens, such as understanding when users log in to a system, you can use log files to spot unusual activity. Red Hat Enterprise Linux comes with system-monitoring utilities that can help identify the culprit if there is a problem.

RHEL 9 comes with two logging systems: a traditional logging service, rsyslog, and an enhanced logging daemon known as **systemd-journald**. We briefly discussed systemd logging in [Chapter 5](#ch05.xhtml). Thanks to its architecture, systemd can intercept and save all boot and syslog messages, along with the output that services send to standard error and to standard output. This is much more than what a traditional syslog server can do. By default, systemd journal logs are stored temporarily (in a RAM tmpfs filesystem) in the /run/log/journal directory.

The rsyslog daemon includes the functionality of the kernel and system logging services used through RHEL 9\. You can use the log files thus generated to track activities on a system. The way rsyslog logs output to files is based on the configuration defined in the /etc/rsyslog.conf file and on the files in the /etc/rsyslog.d directory.

In many cases, services such as SELinux, Apache, and Samba have their own log files, defined within their own configuration files. Details are addressed in the chapters associated with those services.

#### System Log Configuration File

You can configure what is logged through the /etc/rsyslog.conf configuration file. As shown in [Figure 9-10](#ch09.xhtml_ch9fig10), it includes a set of rules for different facilities: **authpriv**, **cron**, **kern**, **mail**, **news**, **user**, and **uucp**.

FIGURE 9-10 The rsyslog.conf configuration file

![Images](F09-10.jpg)

Each facility is also associated with several different levels of logging, known as the priority. In ascending order, log priorities are **debug**, **info**, **notice**, **warn**, **err**, **crit**, **alert**, **emerg**. There’s also a generic **none** priority that logs no messages of the specific facility; for example, an **authpriv.none** directive would omit all authentication messages.

For each facility and priority, log information is sent to a specific log file. For example, consider the following line from /etc/syslog.conf:

![Images](f0389-01.jpg)

This line sends log information from all of the given facilities to the /var/log/messages file. This includes all facility messages of **info** level and higher, except for log messages related to the **mail**, **authpriv** (authentication), and **cron** facilities.

You can use the asterisk as a wildcard in /etc/syslog.conf. For example, a line that starts with ***.*** tells **rsyslogd** to log everything. A line that starts with **authpriv.*** means you want to log all messages from the **authpriv** facility.

By default, **rsyslogd** logs all messages of a given priority or higher. In other words, a **cron.err** line will include all log messages from the **cron** daemon at the **err**, **crit**, **alert**, and **emerg** levels.

Most messages from **rsyslogd** are written to files in the /var/log directory. You should scan these logs on a regular basis and look for patterns that could indicate a security breach. It’s also possible to set up cron jobs to look for such patterns.

#### Log File Management

Logs can easily become very large and difficult to read. By default, the **logrotate** utility creates a new log file on a weekly basis, using the directives in the /etc/logrotate.conf file, which also pulls in directives from files in the /etc/logrotate.d directory. As shown in [Figure 9-11](#ch09.xhtml_ch9fig11), the directives in the file are straightforward and well explained by the comments.

FIGURE 9-11 Log rotation configured in /etc/logrotate.conf

![Images](F09-11.jpg)

Specifically, the default settings rotate log files on a weekly basis, storing the past four weeks of logs. New log files are created during the rotation, and older files have the date of rotation as a suffix.

#### A Variety of Log Files

Various log files and their functionality are described in [Table 9-12](#ch09.xhtml_ch9tab12). These files are created based on the previously described configuration of the /etc/rsyslog.conf file and of service configuration files in the /etc/rsyslog.d directory. Some of the log files (such as those in /var/log/httpd) are created directly by applications. All files shown are in the /var/log directory. If you haven’t installed, activated, or used the noted service, the associated log file may not appear. In contrast, you may see log files not shown here based on additional installed services.

TABLE 9-12 Standard Red Hat Log Files

![Images](f0391-01.jpg)

#### Service-Specific Logs

As suggested earlier, a number of services control their own log files. The log files for the vsFTP server, for example, are configured in the vsftpd.conf file in the /etc/vsftpd directory. As noted from that file, the following directive enables the logging of both uploads and downloads in the /var/log/xferlog file:

`xferlog_enable=YES`

The logging of other services may be more complex. For example, separate log files are configured for access and errors in the Apache web server in the /var/log/httpd directory.

EXERCISE 9-3

**Learn the Log Files**

In this exercise, you’ll inspect the log files on a local system to try to identify different problems.

1.   Restart the Linux computer. Log in from SSH as the root user. Use the wrong password once.

2.   Log in properly with the correct password as the root user.

3.   In a console, navigate to the /var/log directory and open the file named “secure.” Navigate to the “Failed password” message closest to the end of the file. Review what happened. Close the file.

4.   Review other logs in the /var/log directory. Use [Table 9-12](#ch09.xhtml_ch9tab12) for guidance. Look for messages associated with hardware. What log files are they in? Does that make sense?

5.   Most, but not all, log files are text files. Try reading the lastlog file in the /var/log directory as a text file. What happens? Try the **lastlog** command. Are you now reading the contents of the /var/log/lastlog file? Can you confirm this from the associated man page?

#### View systemd Journal Log Entries

Aside from initializing the system and managing services, systemd also implements a powerful logging system. In [Chapter 5](#ch05.xhtml) we briefly introduced **journalctl** and explained how to enable persistent logging. In this section, we will review some of the basic functionalities of the **journalctl** command and show how to perform advanced searches.

By default, logs are stored in a ring buffer using a binary format inside the directory /run/log/journal, and they do not persist a system reboot. If you prefer to write journal log files persistently on disk, edit the /etc/systemd/journald.conf file and look for the Storage configuration option:

`#Storage=auto`

This parameter can be set to **volatile**, **persistent**, or **auto**. If set to **volatile**, journal logs are temporarily stored in /run/log/journal. Conversely, **persistent** stores the journal logs in /var/log/journal (and creates this directory if it does not exist). The **auto** setting uses persistent storage if /var/log/journal exists, and otherwise fails back to volatile mode. If you modify the Storage parameter, you’ll have to restart the **systemd-journald** service.

Hence, to enable persistent storage, uncomment the Storage entry and set its value to **persistent**:

`Storage=persistent`

Then, restart the **systemd-journald** service with the following command:

`# systemctl restart systemd-journald`

One of the main advantages of the systemd journal over rsyslog is that it can store not just kernel and syslog messages but also any other output that services send to their standard output or standard error. You don’t need to know where a daemon sends its logs because everything is captured by systemd and logged into the journal. The journal is indexed so that it can be easily searched using different options.

By default, the **journalctl** command shows all the messages in the journal in a paged format chronologically. It displays messages of **warning** severity in yellow, and it shows err, crit alert and **emerg**, **alert**, **crit** and **err** lines in red. A useful command switch is **-f**, which works in a similar way to the **tail -f** command by displaying the last 10 log entries and continuously printing any new log entries as they are appended to the journal.

You can filter the output of **journalctl** in several ways. You can use the **-p** switch to display messages whose priority is the same or higher than the one specified. As an example, the following command shows only entries of priority **err** or above:

`# journalctl -p err`

The command switches **--since** and **--until** can restrict the output to a specified time range. The next examples should be self-explanatory:

![Images](f0393-05.jpg)

You can also filter the output by looking at the most recent journal entries via the **-n** option. For example, you can run the next command to show the last 20 lines in the journal:

`# journalctl -n 20`

But there’s more. Each entry in the systemd journal has a set of metadata that you can display with the **-o verbose** switch. [Figure 9-12](#ch09.xhtml_ch9fig12) shows how a journal entry looks when enabling verbose output.

FIGURE 9-12 A journal entry with metadata

![Images](F09-12.jpg)

The **journalctl** command can filter the output using any of the fields listed in [Figure 9-12](#ch09.xhtml_ch9fig12). For example, the following command shows all log entries associated with user ID 1000:

`# journalctl _UID=1000`

Similarly, the next example displays all journal entries related to the **nslcd** daemon:

`# journalctl _COMM=nslcd`

You can also specify multiple conditions on the same line. As you get more practice with the **journalctl** command, you will find that the systemd journal is very robust and flexible, and can be queried using a myriad of different options.

![Images](f0395-01.jpg)

#### CERTIFICATION SUMMARY

RHEL 9 includes a variety of system administration commands that can help you monitor and manage the resources used on a system. These commands include **ps**, **top**, **kill**, **nice**, and **renice**. In addition, you can optimize the system for a specific workload by applying a **tuned** performance profile.

File archives are a common way to back up or distribute filesystem contents in a single file. Special command options are required to back up files with specialized attributes such as those based on ACLs and SELinux.

The **cron** and **at** daemons can help you manage what jobs are run on a system on a schedule. With related configuration files, access to these daemons can be limited to certain users. While cron configuration files follow a specific format documented in /etc/crontab, those configuration directives have been integrated with the anacron system that supports job management on systems that are powered off on a regular basis.

Linux administrators need to configure scripts on a regular basis. Normally, bash scripts start with the **#!/bin/bash** line, which sets up the interpreter. Scripts can run Linux commands, along with conditional and control structures such as **for**, **if**, and **test**.

RHEL 9 includes two logging systems—the systemd journal and the rsyslog daemon—that are configured primarily for local logging. Log entries are normally collected by systemd in the /run/log/journal directory (or /var/log/journal if the systemd service is configured to write logs persistently on disk), whereas rsyslog stores log files permanently in the /var/log directory. The rsyslog daemon also supports the creation of a logging server that can collect log file information from a variety of systems.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 9](#ch09.xhtml).

##### Resource Management and System Tuning

![Images](squ1.jpg)   The **ps** command can identify currently running processes.

![Images](squ1.jpg)   The **top** command starts a task browser that can identify processes utilizing excessive resources on the system.

![Images](squ1.jpg)   The **sar** and related commands provide system activity reports.

![Images](squ1.jpg)   The **iostat** command can provide CPU and storage device statistics.

![Images](squ1.jpg)   The **nice** and **renice** commands can be used to reprioritize processes.

![Images](squ1.jpg)   The **kill** and **killall** commands can be used to send signals to currently running processes.

![Images](squ1.jpg)   You can list performance profiles and apply one to a system with the **tuned-adm** command.

##### Archives and Compression

![Images](squ1.jpg)   Archives can be created, extracted, and compressed with the **gzip**, **bzip2**, **tar**, and **star** commands.

##### Running Tasks on a Schedule: cron and at

![Images](squ1.jpg)   The cron system allows users to schedule jobs so they run at given intervals.

![Images](squ1.jpg)   The at system allows users to configure jobs to run once at a scheduled time.

![Images](squ1.jpg)   The **crontab** command is used to work with cron files. Use **crontab -e** to edit, **crontab -l** to list, and **crontab -r** to delete cron files.

![Images](squ1.jpg)   The /etc/cron.allow and /etc/cron.deny files are used to control access to the cron job scheduler; the /etc/at.allow and /etc/at.deny files are used to control access to the **at** job scheduler in a similar fashion.

##### Bash Scripts

![Images](squ1.jpg)   Standard administrative scripts can provide a model for custom scripts to automate system maintenance tasks.

![Images](squ1.jpg)   Bash scripts start with the **#!/bin/sh** or **#!/bin/bash** shebang line.

![Images](squ1.jpg)   Variables can store data and are available to other scripts or commands if exported as environment variables.

![Images](squ1.jpg)   Parameters include $?, which returns the exit value of the last command, and $1 to $9, which are the command-line arguments passed to a script.

![Images](squ1.jpg)   Simple loop and control structures are executed with commands such as **for**, **if**, and **test**.

##### Local Log Files

![Images](squ1.jpg)   RHEL includes the rsyslog daemon, which monitors a system for kernel messages as well as other process activity, as configured in /etc/rsyslog.conf.

![Images](squ1.jpg)   You can use log files generated in the /var/log directory to track activities on a system.

![Images](squ1.jpg)   Other log files may be created and configured through service configuration files.

![Images](squ1.jpg)   Log files may be rotated on a regular basis, as configured in the /etc/logrotate.conf file.

![Images](squ1.jpg)   The systemd journal logs all boot, kernel, and service messages in a ring buffer inside the /run/log/journal directory. Alternatively, it can store logs persistently in /var/log/journal.

![Images](squ1.jpg)   The **journalctl** command is used to display and filter journal entries.

#### Q SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams.

##### Resource Management and System Tuning

**[1.](#ch09.xhtml_ch8ques1)**   What command identifies all running processes in the current terminal console?

**[2.](#ch09.xhtml_ch8ques2)**   What is the highest priority number you can set for a process with the **nice** command?

**[3.](#ch09.xhtml_ch8ques3)**   How can you list all **tuned** profiles?

##### Archives and Compression

**[4.](#ch09.xhtml_ch8ques4)**   What **tar** command option can be used to archive the files of an existing directory while saving its SELinux contexts?

**[5.](#ch09.xhtml_ch8ques5)**   You want to create an archive of the /etc directory. What command do you need to run to create a compressed bzip2 archive of that directory? Assume that archive is named /tmp/etc.tar.bz2.

##### Running Tasks on a Schedule: cron and at

**[6.](#ch09.xhtml_ch8ques6)**   You want to schedule a maintenance job, maintenance.pl, to run from your home directory on the first of every month at 4:00 A.M. You’ve run the **crontab -e** command to open your personal crontab file. Assume you’ve added appropriate **PATH** and **SHELL** directives. What directive would you add to run the specified job at the specified time?

**[7.](#ch09.xhtml_ch8ques7)**   Suppose you see the following entry in the output to the **crontab -l** command:

`42 4 1 * * root run-parts /etc/cron.monthly`

When is the next time Linux will run the jobs in the /etc/cron.monthly directory?

**[8.](#ch09.xhtml_ch8ques8)**   What file is used to configure log file rotation?

##### Bash Scripts

**[9.](#ch09.xhtml_ch8ques9)**   What exit code is associated with success in a script?

**[10.](#ch09.xhtml_ch8ques10)**   If the HOME variable contains the value /*path*/*user*, where *user* is the username stored in the USER variable and *path* is an arbitrary path, how do you use parameter expansion to refer to the /*path* value?

**[11.](#ch09.xhtml_ch8ques11)**   Write a bash **test** command to check if a file exists and is executable.

**[12.](#ch09.xhtml_ch8ques12)**   Write a bash **for** statement to cycle through all the users in a system.

##### Local Log Files

**[13.](#ch09.xhtml_ch8ques13)**   What entry in the /etc/rsyslog.conf file would notify logged-in users whenever there is a critical problem with the kernel?

**[14.](#ch09.xhtml_ch8ques14)**   There are several files in the /var/log directory related to what happened during the installation process. What is the first word shared by the name of these log files?

**[15.](#ch09.xhtml_ch8ques15)**   What command displays all systemd journal entries with a priority equal to alert or higher?

**[16.](#ch09.xhtml_ch8ques16)**   How you can show the systemd journal entries related to the **httpd** daemon logged since the 16th of March 2023?

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for each lab follow the Self Test answers.

#### A SELF TEST ANSWERS

##### Resource Management and System Tuning

**[1.](#ch09.xhtml_r_ch8ques1)**   This is a bit of a trick question because the **ps** command by itself identifies any currently running processes in the current terminal.

**[2.](#ch09.xhtml_r_ch8ques2)**   The highest priority number that can be used with the **nice** command is –20. Remember, priority numbers for processes are counterintuitive: lower values mean higher priorities, and higher values mean lower priorities.

**[3.](#ch09.xhtml_r_ch8ques3)**   The **tuned-adm list** command lists all **tuned** profiles.

##### Archives and Compression

**[4.](#ch09.xhtml_r_ch8ques4)**   The **tar** command option that preserves SELinux contexts in an archive is **--selinux**.

**[5.](#ch09.xhtml_r_ch8ques5)**   The command that creates a compressed bzip2 archive of the /etc directory is

`# tar cvfj /tmp/etc.tar.bz2 /etc`

##### Running Tasks on a Schedule: cron and at

**[6.](#ch09.xhtml_r_ch8ques6)**   The directive that runs the maintenance.pl script from a home directory at the noted time is

`0 4 1 * * ~/maintenance.pl`

**[7.](#ch09.xhtml_r_ch8ques7)**   Based on the noted entry in **/**etc/crontab, the next time Linux will run the jobs in the /etc/cron.monthly directory is on the first of the upcoming month, at 4:42 A.M.

**[8.](#ch09.xhtml_r_ch8ques8)**   The configuration file associated with the rotation of log files over time is /etc/logrotate.conf. Additional service-specific configuration files can be created in the /etc/logrotate.d directory.

##### Bash Scripts

**[9.](#ch09.xhtml_r_ch8ques9)**   The exit code associated with success in a script is 0.

**[10.](#ch09.xhtml_r_ch8ques10)**   If the HOME variable contains the value /*path*/*user*, where *user* is the username stored in the USER variable and *path* is an arbitrary path, you can refer to the /*path* value as **${HOME%%/${USER}}** or **${HOME%/${USER}}**.

**[11.](#ch09.xhtml_r_ch8ques11)**   A bash **test** command to check if a file exists and is executable can be written as follows:

`test -x /path/to/file`

**[12.](#ch09.xhtml_r_ch8ques12)**   A **for** statement to cycle through all the usernames in a system can be written as follows:

`for username in $(getent passwd | cut -f 1 -d ":")`

##### Local Log Files

**[13.](#ch09.xhtml_r_ch8ques13)**   There’s a commented entry in the /etc/rsyslog.conf file that meets the requirements of the question. Just activate it and change the priority to **crit** to notify you (and everyone) whenever a serious problem with the kernel logs occurs:

![Images](f0400-03.jpg)

Of course, that means there are other acceptable ways to meet the requirements of the question.

**[14.](#ch09.xhtml_r_ch8ques14)**   The log files in /var/log that are most relevant to the installation process start with **anaconda**.

**[15.](#ch09.xhtml_r_ch8ques15)**   The command that displays all systemd journal entries with a priority equal to alert or higher is **journalctl -p alert**.

**[16.](#ch09.xhtml_r_ch8ques16)**   To show all systemd journal entries related to the **httpd** daemon and logged since the 16th of March 2023, run the command **journalctl _COMM=httpd --since 2023-03-16**.

#### LAB ANSWERS

##### Lab 1

Install tuned and enable the service with the following commands:

![Images](f0400-04.jpg)

Note that running **systemctl enable tuned** is not necessary, because when the package is installed, it already enables the service to start at boot (confirm this with **systemctl is-enable tuned**).

Next, find the active profile and switch to the balanced profile:

![Images](f0400-05.jpg)

After rebooting the system, **tuned-adm active** will show that the current active profile is “balanced.”

Finally, switch back to the default profile. If you forgot which one it was, type **tuned-adm recommend**.

##### Lab 2

One way to modify the login messages as noted is with the following steps (there is at least one other method, related to the /etc/cron.d directory):

**1.**   Log in as the root user.

**2.**   Run the **crontab -e** command.

**3.**   Add the appropriate environment variables, at least the following:

`SHELL=/bin/bash`

**4.**   Add the following commands to the file to overwrite /etc/motd at the appropriate times:

![Images](f0401-02.jpg)

**5.**   Save the file. As long as the **cron** daemon is active (which it is by default), the next user who logs in to the console after one of the specified times should see the message upon a successful login. If you want to test the result immediately, the **date** command can help. For example, the command

`# date 06120659`

sets a date of June 12, at 6:59 A.M., just before the **cron** daemon should execute the first command in the list. (Of course, you’ll want to substitute today’s date and wait one minute before logging in to this system from another console.)

##### Lab 3

To set up an **at** job to start five minutes from now, start with the **at** command. It’ll take you to an at> prompt.

Currently installed RPMs are shown in the output to the **rpm -qa** command. Since there is no **PATH** defined at the at> prompt, you should include the full path. So, one way to create a list of currently installed RPMs in the /root/rpms.txt file in a one-time job starting five minutes from now is with the following commands:

![Images](f0401-04.jpg)

Within five minutes, you should see an rpms.txt file in the home directory of the root user, /root. If five minutes is too long to wait (as it might be during the RHCSA exam), proceed to Lab 4 and come back to this problem afterward. Don’t forget to set up the other **at** job to be run in 24 hours.

##### Lab 4

One way to set up the cron job specified in the lab requirements is detailed here:

**1.**   Log in as the root user.

**2.**   The lab requirements don’t allow you to use the **crontab -e** command to edit the root crontab file. Hence, create a system crontab in the /etc/cron.d directory, using the following command:

![Images](f0402-01.jpg)

**3.**   Type the following line to set up the cron job:

![Images](f0402-02.jpg)

**4.**   Don’t forget to escape the % characters in the crontab entry; otherwise, they will be interpreted as newlines.

**5.**   Type the EOF sequence:

![Images](f0402-03.jpg)

**6.**   To test the job, modify the crontab entry so that it runs a few minutes from now. Then, change the directory to /tmp and extract the generated archive using the following command:

![Images](f0402-04.jpg)

**7.**   Confirm that SELinux contexts have been preserved by running the following command:

![Images](f0402-05.jpg)

##### Lab 5

Success in this lab should be straightforward. The simplest way to set up the script is to start with the fundamental requirements and then add the other functionalities. For example, the following script saves the current date in MMDDHHSS format in the **$TODAY** variable. Then, it runs the **tar** command to back up the directory passed as the first argument into the backup-MMDDHHSS.tar file within the directory given as the second argument.

![Images](f0402-06.jpg)

The next step is to add the other non-core functionalities. You will need a test to check whether the number of arguments is not equal to two:

![Images](f0402-07.jpg)

You will also need to add another test to confirm that the arguments passed to the script are regular directories:

![Images](f0403-01.jpg)

In addition, another test is required to check if the second argument is a directory. If the test fails, the script must create the directory:

![Images](f0403-02.jpg)

Note that if the second argument is a file but not a directory, the script will return an error. However, this is not an error condition that the exercise asks you to take into consideration.

If you put together all the blocks of code, you will have a working script. Test the script with different arguments to verify that all the exception conditions are recognized and successfully processed.

##### Lab 6

There are no secret solutions in this lab; the intent is to get you to review the contents of key log files to understand what should be there.

When you review the anaconda.* files in /var/log and compare them to other files, you may gain some insight on how to diagnose installation problems. The failed login should be readily apparent in the /var/log/secure file. You may be able to get hints in the output to the **utmpdump btmp** command.

When you review the /var/log/cron file, you’ll see when standard cron jobs were run. Most of the file should be filled (by default) by the standard hourly job, **run-parts /etc/cron.hourly**, from the /etc/cron.d/0hourly configuration file. If you’ve rebooted, you may see the anacron service, and you should be able to search for the job of the same name.

While **dmesg** includes the version of the currently booted kernel, it may be the same kernel as the one associated with /var/log/anaconda/syslog if you haven’t upgraded kernels. At the end of /var/log/dmesg, you can find the filesystems mounted to the XFS format, as well as currently mounted swap partitions. For example, the following lists the partitions from a KVM-based virtual drive:

![Images](f0403-03.jpg)

As you’ve hopefully discovered, the /var/log/maillog file does not include any information on mail clients, only servers.

## Chapter 10

## An Introduction to Containers

CERTIFICATION OBJECTIVES

[10.01     Fundamentals of Container Technology](#ch10.xhtml_ch10obj01)

[10.02     Getting Started with Containers](#ch10.xhtml_ch10obj02)

[10.03     Building and Using Container Images](#ch10.xhtml_ch10obj03)

[10.04     Managing Containers](#ch10.xhtml_ch10obj04)

[![Images](tick1.jpg)     Two-Minute Drill](#ch01.xhtml_lev1sec1)

[**Q&A**   Self Test](#ch01.xhtml_lev1sec1)

The world of IT is in a constant state of evolution, with new technologies emerging and reshaping how we approach tasks and solve problems. One such transformative technology is the use of containers, a fundamental component in today’s DevOps architectures and cloud deployments. This evolution is evident in the RHCSA exam for RHEL 9, the latest exam objectives for which introduce the ability to manage containers as a significant new area of knowledge and competency.

Functionally, containers bear a resemblance to virtual machines (VMs) insofar as they both provide isolated environments with their own network interfaces, filesystems, and resource controls. However, the fundamental difference lies in the fact that containers do not maintain their own operating system. This results in containers being significantly lightweight and faster to start. Furthermore, they can accommodate more applications on a given host than traditional VMs, making them an efficient and resource-friendly option.

This chapter starts with a broad overview by discussing general concepts about containers and drawing comparisons to VMs to highlight their unique benefits. After establishing that fundamental understanding, the chapter guides you through deploying your first containers. You’ll then explore the workings of container images and registries and how they contribute to the overall container ecosystem.

Next, you’ll learn about container management, exploring commands in more detail and how to run containers as a service, an important skill for container deployments. The final section of the chapter delves into the crucial aspect of attaching persistent storage to a container, ensuring data longevity and resilience. This knowledge will provide you with an understanding of how to integrate containers into broader IT systems effectively, an essential skill in modern DevOps and cloud deployments. Let’s embark on this journey to master the art of containers!

INSIDE THE EXAM

**Fundamentals of Container Technology**

This initial section, while not directly linked to specific exam objectives, establishes the vital groundwork for understanding the pivotal concept of containers. Here, we delve into the reasons behind the rise of containers as potent tools in streamlining the development lifecycle, minimizing operational costs, and mitigating complexities. By drawing analogies and differences between containers and VMs, this section offers a comprehensive introduction to container technology.

**Getting Started with Containers**

Exam objectives emphasize both foundational and advanced aspects of Podman, an open-source tool for developing, managing, and running containers on Red Hat Enterprise Linux. Launching the first container introduces essential Podman commands, laying the groundwork for more detailed exploration in subsequent topics.

The relevant RHCSA exam objectives addressed here include

![Images](square.jpg)   Perform basic container management such as running, starting, stopping, and listing running containers

![Images](square.jpg)   Run a service inside a container

**Building and Using Container Images**

Retrieving container images from remote registries and building container images are essential skills in the world of containers.

The RHCSA exam objectives covered in this section are

![Images](square.jpg)   Find and retrieve container images from a remote registry

![Images](square.jpg)   Inspect container images

![Images](square.jpg)   Build a container from a Containerfile

**Managing Containers**

The RHCSA exam objectives also focus on advanced Podman commands, extending beyond a thorough review of those previously introduced. The configuration of containers to start automatically as a system service is a critical aspect of automated deployments, which is also covered in the exam.

Due to their ephemeral nature, containers lose their content once they are removed. Hence, configuring persistent storage is crucial when running containerized services, especially for databases. This section provides an understanding of how to achieve this.

The associated RHCSA exam objectives are

![Images](square.jpg)   Perform container management using commands such as **podman** and **skopeo**

![Images](square.jpg)   Configure a container to start automatically as a systemd service

![Images](square.jpg)   Attach persistent storage to a container

### CERTIFICATION OBJECTIVE 10.01

### Fundamentals of Container Technology

This section provides a comprehensive overview of why containers have become indispensable tools for streamlining the development lifecycle, reducing operational costs, and simplifying complex IT environments. Using comparisons and contrasts with VMs, the section clarifies the unique advantages and functionalities of containers.

#### The Rise of Container Technologies

In the world of software development and IT operations, there’s always been a tricky balance to maintain: developers are always eager to release new features or improvements quickly, while IT operations teams need to make sure that the systems they manage stay stable and reliable. This balancing act between quick changes and stable operations led to the creation of a method called *DevOps*.

DevOps is a way of working that brings together developers and operations teams. It’s all about making the process of creating and releasing software faster and more efficient, without causing problems in the systems where the software runs. However, even with the best DevOps practices, there can be challenges. Some of these include making sure the software behaves the same way in different systems, getting teams with different goals to work well together, and figuring out how to safely release new software features quickly.

Containers can help solve some of these DevOps challenges. With containers, developers can pack up an application and everything it needs to run (like software libraries) into one neat package. This means the application can run the same way in different places, whether it’s on a developer’s personal computer or on a large computer system in a data center.

You can think of containers as little boxes that keep applications safe and separate from each other, similar to virtual machines. But, unlike VMs, which need a separate operating system to run, containers share the operating system of the machine they’re running on, which means they use fewer resources and can start up and shut down quickly.

Another reason why containers are essential is their role in the microservice architecture, which is a way of designing software applications. In the microservice architecture, an application is broken down into smaller, independent pieces, each performing a specific task. These small pieces, or *microservices*, can be developed, updated, and scaled independently, which makes the whole application more flexible and easier to manage. Containers provide the perfect environment for microservices because a container can be used to package and run each microservice independently, no matter where a microservice is deployed.

So, a container is like a little bubble that holds one or more software processes. These processes are kept separate from everything else on the system. Containers offer some of the same benefits as VMs, like security and isolation, but they need less hardware power and are quicker to start and stop. This makes them a great tool for modern software development, where speed and flexibility are key.

Here are some key benefits of containers:

![Images](square.jpg)   **Agility** Containers enable rapid application deployment and scaling. They can be created, replicated, or deleted in seconds.

![Images](square.jpg)   **Portability** Applications packed in containers can run consistently across various platforms and environments, reducing the “it works only on my machine” problem.

![Images](square.jpg)   **Efficiency** Containers share the host system kernel, making them much lighter than VMs. This enables more applications to be run on the same hardware, increasing efficiency.

![Images](square.jpg)   **Isolation** Each container operates independently from others, reducing the risk of system-wide failures.

![Images](square.jpg)   **Version control and component reuse** Containers support versioning, and you can share or reuse container images across different teams, which improves the overall development process.

![Images](square.jpg)   **Security** Each container is isolated from others and the host system, providing an additional layer of security.

As we delve deeper into the intricacies of containers in the following sections, these benefits will become increasingly evident.

#### Virtualization and Containers

Virtualization technology allows us to create services that act like their physical counterparts but aren’t actually tied to any specific physical device. Both virtual machines and containers are forms of virtualization, but they differ significantly in their structure and function.

Virtual machines offer a type of virtualization called *hardware virtualization*, as illustrated in [Figure 10-1](#ch10.xhtml_ch10fig1). This form of virtualization abstracts physical host resources, such as CPU, memory, and storage, creating a VM that acts like a real computer with its own operating system.

FIGURE 10-1 Virtual machines versus containers

![Images](F10-01.jpg)

This abstraction is managed by specialized software known as a *hypervisor* or *virtual machine monitor*. This software runs directly on the server’s hardware, and it’s tasked with managing the resources for each VM. Hypervisors come in two types, as introduced in [Chapter 1](#ch01.xhtml): type-1 hypervisors run directly on the system hardware (bare-metal), while type-2 hypervisors run on a host operating system.

Each VM operates with its own instance of an operating system, which could be Linux, Windows, or others. Within each VM, libraries and the application itself are installed and run as if they were on a standalone computer system.

In contrast, containers are a more lightweight form of virtualization. As also shown in [Figure 10-1](#ch10.xhtml_ch10fig1), containers don’t run their own operating system. Instead, they share the host’s operating system kernel. They’re essentially isolated processes running on the host, but they’re set up in such a way that they run as if they’re operating in their own separate environments.

This isolation is achieved through specific technologies in the Linux kernel, such as namespaces and cgroups (discussed in the next section), which give containers the illusion of running in separate environments similar to VMs, but without the overhead of a full operating system.

When comparing VMs and containers, there are pros and cons to both approaches. VMs are fully isolated and can run different operating systems, but they also have more overhead, requiring more resources and time to start. Containers, on the other hand, are lightweight, start quickly, and are highly portable, but they share the same kernel and are slightly less isolated than VMs.

In conclusion, the decision between using VMs and using containers depends on what you need. If you need to run many different operating systems or need full isolation, then VMs are your best bet. But, if you’re looking for something that’s fast, efficient, and easy to move around, then containers are the way to go. They’re lighter, start up quicker, and can be moved around easily while still giving you enough isolation for most use cases. This makes them a popular choice for running applications, especially in cloud computing and DevOps work. While VMs still have their uses, containers are becoming the go-to option for deploying applications quickly and efficiently.

#### Understanding Container Architecture

The architecture of containers is a fascinating blend of several key Linux features, specifically designed to provide process and resource isolation. These features—namespaces, control groups, and SELinux—work in harmony to create the container environment that many developers and organizations have come to rely on today.

*Namespaces*, at their core, are a Linux kernel feature that govern the visibility of various system resources. Imagine a process group that can only “see” certain aspects of the system, such as process IDs (PIDs), filesystems, and network interfaces. By segregating these resources between different sets of processes, namespaces create a unique “illusion” for each set, making them believe they are operating in their own isolated environment. This is a fundamental underpinning of how containers isolate processes and filesystems from each other.

While namespaces are focused on resource visibility, *control croups (cgroups)* come into play to control the actual usage of system resources. If namespaces are about “seeing,” cgroups are about “using.” They impose limits and manage the allocation of CPU, memory, network bandwidth, and disk I/O among various process groups. This is crucial in a container environment as it ensures that each container gets its fair share of resources, and a single greedy container cannot bring the entire system to a standstill.

SELinux adds another layer to this architecture, contributing a robust security mechanism. Known for its implementation of mandatory access controls (MAC), SELinux allows fine-grained permission control over every process and file in the system. In a container context, this is highly advantageous as it restricts what each container can do and helps limit the “blast radius” in case of a container breakout.

Moving away from the underlying Linux features, let’s look at what makes a container possible in practical terms: the *container image*. An image is like a blueprint for a container; it packages the software application, its dependencies, and some configuration details into a single object. When this image is executed on a container run time (like Podman or Docker), it “comes to life” as a running container. Having such an image is essential because it guarantees the same environment can be replicated anywhere, be it a developer’s laptop or a production server.

But how are these images standardized and made portable? This is where the Open Container Initiative (OCI) comes in. It’s an open-source project aimed at setting common standards for container platforms. OCI primarily focuses on defining specifications for container images and run times, promoting interoperability and preventing vendor lock-in, making it easier for developers to build and deploy containers across different environments.

Lastly, just like how codebases need repositories, container images need a storage place too, known as a *container registry*. A registry is an online repository where container images can be stored, retrieved, and shared, facilitating the distribution of applications packaged as containers. Examples include Docker Hub, Google Container Registry, and Quay.io.

In a nutshell, the container architecture is a combination of these robust Linux features, standardized container images, and the efficient use of container registries, all working together to deliver the power of containerized applications.

#### Docker and Podman

Docker is often credited for popularizing container technology, even though the idea of containers had been around in the Linux world for years before Docker’s inception. Docker, which was first released in 2013 by a company called dotCloud, was designed to simplify and accelerate the process of developing, shipping, and running applications. Docker uses containers to package and isolate applications with their entire run-time environment, making them portable across different systems. Docker’s ease of use and efficient workflow quickly gained it popularity and a thriving user community.

However, Docker’s architecture wasn’t without its flaws. A crucial design feature of Docker is its reliance on a central daemon. This daemon runs with root privileges, presenting a potential security risk. Additionally, the Docker daemon handles all interactions with the Docker API, creating a potential single point of failure and complexity in distributed systems.

In response to these challenges, Red Hat developed Podman. Introduced around 2018, Podman addresses some of Docker’s security and design issues by providing a daemonless, rootless container engine. In other words, Podman doesn’t require a constantly running, high-privileged background process to manage containers. Instead, Podman launches containers and containerized services as child processes, enhancing security and reducing the attack surface.

Moreover, Podman’s rootless feature allows nonprivileged users to manage containers, further reducing the security risks. Additionally, Podman offers better integration with system-level features, such as systemd for service management, cgroups for resource limiting, and SELinux for security, aligning more closely with traditional Unix philosophy.

Despite these differences, Podman was designed to be command-compatible with Docker, meaning most Docker commands work identically in Podman, which has made it easier for users to transition from Docker to Podman. With the industry’s growing focus on security and efficiency, Podman presents a viable and secure alternative to Docker, while maintaining Docker’s ease of use and flexibility.

### CERTIFICATION OBJECTIVE 10.02

### Getting Started with Containers

In this section, we’ll guide you through launching your first container using Podman, an open-source tool for developing, managing, and running containers on Red Hat Enterprise Linux. This initial section introduces several basic Podman commands, each of which will be explored more thoroughly in subsequent sections.

#### Installing Container Tools

Getting started with containers on RHEL 9 begins with installing the container-tools meta-package. A *meta-package* does not contain any tools itself but serves as a convenient method to install a group of related packages. Use the **dnf** command to install the container-tools meta-package:

`# dnf install container-tools`

One of the key packages included in container-tools is Podman, the daemonless container engine responsible for developing, managing, and running OCI containers and container images. If Podman is not already present on your system, installing the container-tools meta-package will ensure it’s added.

The container-tools meta-package also triggers the installation of a script named **docker**. This script acts as a wrapper around **podman**, allowing you to utilize the **docker** command just like you would with Docker, while it’s actually Podman that is managing your containers behind the scenes.

Another significant utility that accompanies the container-tools meta-package is Skopeo. Skopeo is a command-line utility designed for various operations on container images and repositories, with no requirement to pull the image or create a container. This includes inspecting images directly on Docker registries and copying, deleting, or signing images. Skopeo works harmoniously with both OCI images and the original Docker Image format.

The container-tools meta-package would not be complete without Buildah, a specialized command-line tool that can build OCI container images. Buildah offers a flexible approach to creating, building, updating, and managing container images without a need for a full container run time or daemon. Podman uses Buildah behind the scenes to build container images.

#### Running Your First Container

Now that all the prerequisite tools have been installed, it’s time to illustrate how to launch a container. In this demonstration, we’ll run a container that hosts the Apache 2.4 web server:

![Images](f0413-01.jpg)

After executing the command, you should see output similar to the output displayed in [Figure 10-2](#ch10.xhtml_ch10fig2). If all is working as expected, pointing your browser to [http://localhost:8080](http://localhost:8080) should display the web server’s test page, as shown in [Figure 10-3](#ch10.xhtml_ch10fig3).

FIGURE 10-2 Create and run a container

![Images](F10-02.jpg)

FIGURE 10-3 The Apache web server’s test page

![Images](F10-03.jpg)

The previously mentioned command carries out multiple tasks. Initially, it checks for the presence of the httpd-24 image in the local environment. If the image is unavailable locally, Podman retrieves that image from the Red Hat registry, an operation equivalent to the following command:

![Images](f0414-01.jpg)

Following the image retrieval, the **podman run** command initiates a new container from the httpd-24 image, with the name “webserver.” The **-d** flag specifies detached mode, ensuring the container runs in the background, thereby not occupying your current terminal or shell session.

When it comes to services within the container that need to be accessible over a certain port, you can utilize the **-p** argument to expose a specific port. By using **-p 8080:8080**, you are instructing Podman to open port 8080 on the host machine and to route all incoming traffic on this port to port 8080 inside the container.

![Images](job.jpg)

**Newer versions of Docker and Podman have introduced grouping specific commands based on their usage. For instance,** podman container **groups all commands related to container management, and** podman container run **would be equivalent to the simpler** podman run**. Nonetheless, Podman maintains backward compatibility; hence, newer versions of commands coexist with their traditional counterparts.**

After the httpd-24 image has been downloaded and made locally available, which you can confirm via the **podman images** command, the **podman ps** command lets you view all the containers in a running state, as shown in [Figure 10-4](#ch10.xhtml_ch10fig4).

FIGURE 10-4 View running containers

![Images](F10-04.jpg)

The output of the **podman run** command concludes with a unique ID generated by Podman for managing the container. You can, for example, halt the container using the following command:

`$ podman stop a8b`

where “a8b” are the first three characters of the unique ID. For convenience, Podman doesn’t require the entire ID, just the first few characters. Alternatively, you can reference the container by its given name, as shown next:

`$ podman stop webserver`

Keep in mind that, by default, the **podman ps** command lists only running containers. To display containers that are stopped as well, use the **-a** flag:

`$ podman ps -a`

Once you are done with the container, it’s good practice to clean up. You can remove the stopped container by using **podman rm webserver**, and you can delete its corresponding image with **podman rmi httpd-24**.

#### Rootless and Rootful Containers

So far, we’ve been operating containers as a nonprivileged user. In the language of container technology, this is often referred to as running “rootless” containers. Conversely, when containers are run by the root user, or a user with equivalent permissions, they are called “rootful” containers. Let’s dive deeper into these concepts.

Rootful containers, as the name suggests, are those run by the root user or an equivalently privileged user. This setup grants these containers broad capabilities, allowing them to fully exploit the resources and functionalities of the host system. However, this potent access also poses significant potential risks. A misstep in configurations or a container vulnerability can trigger severe security breaches. The unrestricted nature of rootful containers could potentially lay open the entire host system to exploitation.

In contrast, rootless containers are the safer counterpart, run by non-root users, without any exceptional privileges. They offer a more constrained and controlled environment, limiting the container’s ability to interact with the host system. This significantly curtails the potential risk of compromising the host, making it a preferred option for prioritizing security.

Running rootless containers is like playing in a sandbox. You can do whatever you want inside the sandbox without affecting the playground around it. That’s why, for most cases, rootless containers are the best choice. They give you what you need while keeping your system safe.

However, there are instances where rootful containers are necessary and advantageous. For example, when there’s a need to directly interact with specific system resources or when you need to listen to network ports below 1024, which are restricted for non-root users, a rootful container might be the most feasible option.

When deciding between rootless and rootful containers, it’s essential to consider the specific needs of your operations and balance them against potential security implications. By doing this, you can ensure the best possible outcome, whether your focus lies in exploiting capabilities, ensuring security, or finding a balance between the two.

### CERTIFICATION OBJECTIVE 10.03

### Building and Using Container Images

In this section, we delve into the world of container registries and the construction of container images. Container registries are integral to the container ecosystem, functioning as storage and distribution hubs for container images. Understanding how to interact with these registries, including how to push, pull, and locate images, is a fundamental skill for any container practitioner. Simultaneously, building your own container images can provide you with precise control over the container’s environment, thereby enabling the creation of customized solutions that perfectly fit your requirements.

#### Image Registries

An image registry is a vital component of container-based development and deployment. It serves as a storage and distribution system for container images, enabling developers to publish their creations, and others to pull and use these images as needed. The images can be scaled and versioned, facilitating effective management. Depending on the requirements, registries can be public (accessible to anyone), private (restricted to certain users or organizations), or a hybrid of both.

The **podman images** command displays all the images that have been downloaded and are currently stored on your local machine. However, these images must initially be retrieved from a registry. When you invoke the **podman info** command, it outputs various configuration details about Podman, including the registries that are currently configured, as shown in [Figure 10-5](#ch10.xhtml_ch10fig5). These can be customized by editing the file /etc/containers/registries.conf.

FIGURE 10-5 Partial display of the **podman info** command output

![Images](F10-05.jpg)

Two noteworthy registries in the list are [registry.access.redhat.com](http://registry.access.redhat.com) and [registry.redhat.io](http://registry.redhat.io). Both these registries primarily host identical container images, but there are some images that demand a subscription, which are available exclusively from [registry.redhat.io](http://registry.redhat.io).

Another commonly used public registry in the list is docker.io, colloquially known as Docker Hub. Docker Hub houses a vast library of prebuilt Docker images for a multitude of applications and services, shared by users worldwide.

The **podman search** command is a useful tool for locating images in the list of configured registries. For instance, executing **podman search python** will instruct Podman to search for images that contain the string “python” in their name or metadata in all configured registries. By default, Podman searches across all unqualified-search registries. A part of the output generated by the command is displayed in [Figure 10-6](#ch10.xhtml_ch10fig6).

FIGURE 10-6 Excerpt of the output of the **podman search python** command

![Images](F10-06.jpg)

For a deeper understanding of a specific image, the **skopeo inspect** command comes into play. For instance, the following command provides details about the httpd-24 image:

`skopeo inspect docker://registry.access.redhat.com/ubi9/httpd-24`

A snippet of the output from the **skopeo inspect** command is shown in [Figure 10-7](#ch10.xhtml_ch10fig7). This data can be vital for evaluating whether a specific image aligns with your requirements.

FIGURE 10-7 Partial output of the **skopeo inspect** command

![Images](F10-07.jpg)

#### Building Container Images: A Primer

In the containerized environment, flexibility and customization often necessitate the creation of custom container images. While you can manually modify an image of a running container for specific changes or testing, the utility of Containerfiles presents a more systematic and replicable approach.

INSIDE THE EXAM

Even though the RHCSA exam objectives do not require you to author a Containerfile, understanding its contents and the process of building an image from a Containerfile is imperative.

A typical Containerfile, as illustrated in [Figure 10-8](#ch10.xhtml_ch10fig8), always initiates with the **FROM** instruction. This specifies the base image upon which your container will be built.

FIGURE 10-8 A Containerfile

![Images](F10-08.jpg)

![Images](job.jpg)

**If you have prior experience with Docker, you’re likely familiar with Dockerfiles. Containerfiles and Dockerfiles are essentially the same. Whether you use a Dockerfile or a Containerfile, Podman can seamlessly build an image from it.**

The **LABEL** instruction is used to add custom metadata to the image in the form of key-value pairs. This can be helpful for documenting your image or adding custom information that can be used by run-time tools.

Next, the **COPY** instruction allows you to add files or directories from the host system to the container’s filesystem. This instruction is often used to include application code or configuration files.

The **RUN** instruction (not shown in [Figure 10-8](#ch10.xhtml_ch10fig8)) is used to execute commands inside the image during the build process. This instruction is typically used to install software packages, making it a vital element of the Containerfile.

The **EXPOSE** instruction indicates the ports that the container uses. While this instruction does not actually open any ports, it serves as a form of documentation that can be useful when running containers from the image.

Setting a working directory within the container is achieved with the **WORKDIR** instruction, which behaves analogously to the **cd** command in Linux.

The **CMD** instruction allows you to specify a default command and its arguments that will be executed when you initiate the container with **podman run**.

An optional **ENTRYPOINT** instruction can also be used to set a command that always executes upon the container’s startup and remains persistent even if a command is provided to **podman run**. **ENTRYPOINT** can also be overridden, but doing so requires the explicit **--entrypoint** flag.

To translate the instructions in a Containerfile into a functional container image, the **podman build** command is used. For example:

`podman build -t python-webserver.`

In the preceding command, the period denotes the path to the directory containing the Containerfile (the current directory, in this case). The **-t** option assigns a name (and optionally, a tag) to the newly created image, such as **python-webserver:1.0**. If a tag is omitted, Podman will automatically assign the **latest** tag to the image.

Exercise 10-1 further explicates the process of building a custom image and running a container from it. Then, Exercise 10-2 shows you how to upload the image to the Quay registry.

EXERCISE 10-1

**Building and Running a Container Image**

In this exercise, you’ll go through the process of creating a Containerfile, building an image from it, and subsequently running a container. This practice will solidify your understanding of managing containers using Podman.

1.   Create a Containerfile using the template provided in [Figure 10-8](#ch10.xhtml_ch10fig8). Ensure you understand the instructions within the Containerfile, as they dictate the structure and functionality of the container image.

2.   In the same directory as your Containerfile, generate a file named index.html. This file will serve as the content served by your web server. Add a simple message to it like “Welcome to our simple webserver!”

3.   With your Containerfile and index.html prepared, you can proceed to build the image. Run the following command to construct the image. The **-t** flag assigns the name python-webserver to your image, and the dot refers to the location of your Containerfile—the current directory:

`# podman build -t python-webserver .`

4.   Confirm that the image has been built and is available on your local system by running **podman images**. This lists all available images, and you should see python-webserver in this list.

5.   Run a container from the image you just built:

`# podman run -d --name simple-webserver -p 8000:8000 python-webserver`

This starts a container named simple-webserver in the background, mapping the container’s TCP port 8000 to the host’s port 8000, based on the python-webserver image.

6.   Confirm that the container is up and running with the **podman ps -a** command. You should see simple-webserver in the list of active containers.

7.   Your container runs a lightweight web server that listens on TCP port 8000\. To verify that it’s functioning correctly, connect to it using a web browser or run **curl http://localhost:8000** in your terminal. You should see the content you added to index.html—“Welcome to our simple webserver!”

8.   Once you’ve confirmed that everything is working as expected, it’s good practice to clean up. Stop the container:

`# podman stop simple-webserver`

9.   Don’t remove the container image yet. You will be using it for the following exercise.

EXERCISE 10-2

**Uploading an Image to Quay.io**

This exercise familiarizes you with Quay.io, an image repository sponsored by Red Hat that offers some advanced features. These features include server-side image building, detailed access control, and automated vulnerability scanning of images. Your goal in this exercise is to upload to Quay.io the python-webserver image you built earlier.

1.   Navigate to [https://quay.io](https://quay.io) and sign in using your Red Hat account credentials. If you don’t have a Red Hat account, you’ll need to create one.

2.   Once logged in, click the account settings located in the top-right corner of the web page.

3.   In the account settings, find and click Generate Encrypted Password. This will create an encrypted password for you to use with Podman. In the same window, navigate to the Podman Login tab. Here, you’ll find the exact Podman command you’ll need to log into Quay.io.

4.   Copy the Podman login command and paste it into your terminal. The command should resemble the following:

![Images](f0421-01.jpg)

5.   Before proceeding, ensure that the simple-webserver image is available locally on your system:

![Images](f0421-02.jpg)

6.   With the image available, you can now tag it for Quay.io using the following command:

![Images](f0421-03.jpg)

This command renames or “tags” your python-webserver image, prepending the Quay.io repository path to it.

7.   Now, you can push or upload the image to Quay.io. Execute the following command to push the image:

![Images](f0421-04.jpg)

8.   Finally, head back to the Quay.io web page and navigate to your repositories. Here, you should see the simple-webserver image listed, confirming that the image was uploaded successfully.

### CERTIFICATION OBJECTIVE 10.04

### Managing Containers

In this section, we dive deeper into the rich set of Podman commands, expanding your understanding of how to interact with and manage containers. We will take a closer look at a variety of commands, each with its own purpose, and how they help in making the most of container technology.

Toward the end of this section, we will shift our focus to examine how to run a container as a systemd service. This feature has immense utility in real-world applications as it offers the advantage of automatic startup during system boot, thus ensuring high availability of the containerized services. Finally, we will explore how to use persistent storage with containers.

#### Podman Commands

In this section, you’ll get to know more about Podman commands. You’ve already used some of these commands, and you’re going to learn some new ones as well. Podman commands are like tools in a toolbox, each doing a special job. They help us create and manage containers or images, and they let us look at details about containers or images.

To make the variety of Podman commands easier to understand, we can sort them into five main groups:

![Images](square.jpg)   **Container management commands** These commands are like the controllers. They help us to make, start, stop, and remove containers.

![Images](square.jpg)   **Container inspection commands** These commands are like detectives. They help us find out what’s happening with a container, what its setup is, and what it’s been doing.

![Images](square.jpg)   **Image management commands** These commands are the organizers for our image library. They help us make, get, name, and remove images.

![Images](square.jpg)   **Image inspection commands** These commands are also like detectives, but for images. They help us find out all the details about an image.

![Images](square.jpg)   **Miscellaneous commands** This group is for the commands that don’t fit into the other groups. They do all sorts of different jobs, like managing the whole system or setting up networks.

[Figure 10-9](#ch10.xhtml_ch10fig9) shows the commands in each category.

FIGURE 10-9 A classification of Podman commands

![Images](F10-09.jpg)

Next, we’ll go into each group of commands and learn about the specific jobs they do.

![Images](exam.jpg)

**Remember, this categorization is a guide to understand Podman commands. However, during the RHCSA exam, you have a convenient resource at hand—the Podman manual page. Simply type** man podman **for broad documentation or use a command such as** man podman-run **for specific command details. It’s an invaluable aid during your exam.**

##### Container Management Commands

The commands presented in [Table 10-1](#ch10.xhtml_ch10tab1) are pivotal for managing containers.

TABLE 10-1 Container Management Commands

![Images](f0424-01.jpg)

We have already introduced the **podman run** command, but let’s dive deeper. This command is essentially a combination of **podman create** and **podman start**. Depending on the flags you use, the behavior can differ. For instance, using **-d** (detached mode) allows the container to run in the background, whereas **-it** enables interactive mode with a terminal.

Let’s consider some examples. If you want to run a container in the background, you could use

`$ podman run -d registry.access.redhat.com/ubi9/httpd-24`

For interactive terminal sessions, you might use

`$ podman run -it registry.access.redhat.com/ubi9 /bin/bash`

The latter command would start a bash shell in the container, allowing you to interact with it directly. The **podman run** command offers several other commonly used options. For instance, you can use **--name** to designate a specific name for the container. If a name is not assigned to the container with **--name**, then Podman generates a random string name. You can also utilize **-p** to establish port mappings, as demonstrated in the section “Running Your First Container.” Moreover, at the end of this chapter, we will delve into a fresh option, **-v**, which enables the mounting of a volume into the container.

![Images](job.jpg)

**ubi9 is the Red Hat Universal Base Image (UBI), a base image provided by Red Hat. It serves as a foundation for building containerized applications and is designed to be lightweight, secure, and reliable. UBI is based on Red Hat Enterprise Linux.**

If we were to decompose **podman run**, we would first use **podman create** to create the container, and then **podman start** to run it. For example:

![Images](f0424-02.jpg)

When you issue the **podman stop** command, the container ceases to run but still exists in the system. You can easily start it up again using **podman start**. For instance:

![Images](f0424-03.jpg)

Finally, to permanently remove a container from the system, you would use **podman rm**. It’s important to note that this will delete all the data associated with the container. For example:

![Images](f0424-04.jpg)

##### Container Inspection Commands

[Table 10-2](#ch10.xhtml_ch10tab2) introduces a range of container inspection commands, which are indispensable for understanding the inner workings of our containers.

TABLE 10-2 Container Inspection Commands

![Images](f0425-01.jpg)

First up is **podman inspect**, a versatile command that provides detailed information about a container. This includes but is not limited to its ID, created time, path, args, state, and much more. This command will output a JSON representation of the container’s current state, giving you valuable insight into its configuration and status. You can see an excerpt of the output in [Figure 10-10](#ch10.xhtml_ch10fig10).

FIGURE 10-10 An excerpt of the output of the **podman inspect command**

![Images](F10-10.jpg)

Next, the **podman ps** command shows you all the running containers. You will see details like the container ID, image, command, when it was created, status, and names. But what if you want to see all containers, not just the running ones? That’s when the **-a** option comes into play. Running **podman ps -a** will list both running and stopped containers, providing a comprehensive overview of all your containers.

Finally, **podman logs** is a must-have tool in your container troubleshooting toolkit. It fetches the logs of a specified container, which can be crucial when diagnosing problems. For example, see [Figure 10-11](#ch10.xhtml_ch10fig11).

FIGURE 10-11 The output of the **podman logs** command

![Images](F10-11.jpg)

Together, these commands form the basis of container inspection and provide a valuable insight into the container’s operations. They can be instrumental when debugging issues or understanding the behavior of your containers.

##### Image Management Commands

[Table 10-3](#ch10.xhtml_ch10tab3) reviews a variety of image management commands. These commands are essential tools for creating, retrieving, renaming, and deleting container images.

TABLE 10-3 Image Management Commands

![Images](f0427-01.jpg)

First, let’s review the **podman build** command, previously introduced in the section “Building Container Images: A Primer.” This command is used to build a container image from a Containerfile (or a Dockerfile). For instance, if you have a Containerfile in your current directory, you can run the following command to create an image named my-image:

`$ podman build -t my-image.`

The **-t** option allows you to tag your image, while the period (.) denotes that the build context is the current directory.

The trio of commands **podman tag**, **podman push**, and **podman pull** are essential for managing images between local and remote registries. **podman tag** is used to assign a tag or another name to an existing image, providing a convenient way to reference images. For instance, the command shown next tags the image my-image with a version designation of v1.0:

`$ podman tag my-image:latest my-image:v1.0`

Next, the **podman push** command enables you to push an image from your local machine to a remote registry. If you’ve tagged your image my-image:v1.0, you can push it to a registry such as Quay.io by running

`$ podman push quay.io/username/my-image:v1.0`

and replacing “username” with your Quay.io username. Note that in a private registry that requires authentication, such as Quay.io, you need to log in first with the **podman login** command.

In contrast, the **podman pull** command is used to fetch an image from a remote registry to your local machine. For example, the following command would pull the latest nginx-122 image from the Red Hat registry:

`$ podman pull registry.access.redhat.com/ubi9/nginx-122`

Lastly, the **podman rmi** command is used for removing images from your local storage. If you’re finished with an image, or if you need to clean up storage, **podman rmi my-image:v1.0** would remove the specified image. It’s good practice to keep your image storage tidy, removing unneeded images to save space.

##### Image Inspection Commands

In the following discussion, outlined in [Table 10-4](#ch10.xhtml_ch10tab4), we’ll revisit some of the image inspection commands discussed earlier in the chapter. The objective of these commands is to provide you with extensive information about the container images that are present on a system.

TABLE 10-4 Image Inspection Commands

![Images](f0428-01.jpg)

One of the most basic but essential commands for working with Podman is **podman images**. It gives you an overview of all the container images that are stored locally on your system. The information it displays includes the repository name, the image tag, the image ID, when it was created, and the size of the image. For instance, if you run **podman images**, you’ll see a table with details of all the images you have downloaded or built on your machine, as shown in [Figure 10-12](#ch10.xhtml_ch10fig12).

FIGURE 10-12 A list of local container images shown by **podman images**

![Images](F10-12.jpg)

Next is the **podman inspect** command. While this command is versatile and can be applied to both containers and images, its usage with images provides a wealth of details about a specific image. If you run **podman inspect <image-name>**, where image-name is the name (or the ID) of your image, you’ll see JSON output with detailed information about the image, including its ID, configuration, and layers, among other things.

Here’s where it gets interesting: the **podman inspect** command varies from the **skopeo inspect** command previously introduced in the section “Image Registries.” The difference lies in the fact that **skopeo inspect** can fetch information directly from a remote registry, while **podman inspect** only inspects images already downloaded on your system. For example, the following command retrieves the metadata of the nginx image from the Red Hat registry, without downloading the image itself:

`$ skopeo inspect docker://registry.access.redhat.com/ubi9/nginx`

Lastly, the **podman search** command allows you to search for images on a container registry right from your terminal. The command **podman search <search-term>** will return a list of all images whose name matches the search term, along with a brief description and star ratings if available. It’s a handy tool when you’re looking for a particular image or exploring available options for a specific service. For example, **podman search ubi9** would return a list of available Red Hat Universal Base Image 9 from the default registries.

##### Miscellaneous Commands

Finally, we delve into a group of commands that, while not fitting neatly into our previous categories, offer unique and practical utilities in managing containers. These miscellaneous commands are outlined in [Table 10-5](#ch10.xhtml_ch10tab5).

TABLE 10-5 Miscellaneous Commands

![Images](f0430-01.jpg)

Let’s begin with the **podman attach** and **podman exec** commands. While both are used to interact with running containers, they have significant differences. The **podman attach** command connects to a running container’s main process, allowing you to interact with it as if you were directly logged in. For example, if you’ve started a container in detached mode using **podman run -d my-container**, you can attach to it with **podman attach my-container** (or using the container ID rather than the name).

On the other hand, **podman exec** executes a new process within an already running container. This is useful for running specific commands or scripts within a container without interrupting its main process. For instance, the following command would list the contents of the root (“/”) directory in your running container:

`$ podman exec my-container ls /`

Just like with all Podman commands, you have the flexibility to use either the name or the ID of a container (or image) interchangeably. This means you can refer to a specific container or image by its given name or unique identifier based on your preference or needs.

Moving on to **podman cp**, this command is akin to the familiar **cp** command on Linux, allowing you to copy files or directories between the host and a container. For instance, to copy a file from your host to a running container, you’d use the command shown next:

`$ podman cp /host/path/file.txt my-container:/container/path/`

To do the reverse, simply flip the source and destination.

The **podman generate** command, listed in [Table 10-5](#ch10.xhtml_ch10tab5), will be detailed in the next section.

Lastly, we have the **podman info** and **podman version** commands. **podman info** provides a comprehensive overview of your Podman installation, including configuration details and the status of storage, registries, and more. On the other hand, **podman version** simply returns the version of Podman you have installed, with the API version and other build details. These commands are especially useful when troubleshooting or verifying your setup.

#### Running a Container as a SystemD Service

Let’s delve into the process of running a container as a systemd service, which can be incredibly useful for containers that need to persist across reboots, such as a web server or a database container.

Back in [Chapter 5](#ch05.xhtml), you learned how to enable and manage services using the **systemctl** command. Podman extends this capability by allowing you to create systemd configuration files for your container services using the **podman generate systemd** command.

Let’s imagine that we have a web server container operating, brought to life with the following command, as described in the earlier section, “Running Your First Container”:

![Images](f0430-02.jpg)

Here, the **podman generate systemd** command can take this running container and use it as a blueprint to create a service configuration file. Here’s an example of this:

`$ podman generate systemd --name webserver --new`

This command will output the systemd configuration file necessary to run the container as a service, as shown in [Figure 10-13](#ch10.xhtml_ch10fig13). By employing the **--files** option, instead of outputting the configuration to your console, it will create the configuration file. If the container is running as a nonprivileged user, this file would then need to be relocated to the ~/.config/systemd/user directory. If it’s running as root, it should go into /etc/systemd/system.

FIGURE 10-13 A systemd unit configuration generated by **podman generate systemd**

![Images](F10-13.jpg)

INSIDE THE EXAM

If you’re feeling overwhelmed by the details in this section, the **man podman-generate-systemd** command will serve as a handy resource during the RHCSA exam.

Observe in [Figure 10-13](#ch10.xhtml_ch10fig13) that the systemd service has been named container-webserver
.service. By default, **podman generate systemd** prepends “container-” to the name of the container to form the systemd unit’s name, unless a different prefix is specified using the **--container-prefix** option.

Once your configuration file is in place, you can start the service and check its status using

![Images](f0431-02.jpg)

Let’s briefly unpack what the **--user** option does here. It specifies that we are managing services for the current user, rather than system-wide services.

To ensure the service starts automatically at boot, execute the following command:

![Images](f0432-01.jpg)

If you’re running a systemd service as a regular user, an additional step is needed. Without this, your container could stop shortly after you exit your SSH session. To prevent this and keep your user’s systemd services running, run the following command:

![Images](f0432-02.jpg)

This step isn’t necessary if the container is running as root.

To better understand and put into practice the concepts explained in this section, proceed to Exercise 10-3.

EXERCISE 10-3

**Running a Container as a Service**

In this exercise, you’ll walk through the practical steps to run a container as a systemd service, using the webserver container you previously set up in the section “Running Your First Container.”

1.   Log in as a regular user. To manage systemd user services, it’s important to directly log in without using the **su** or **sudo** commands to create a session.

2.   Start the Apache web server by executing the following command (previously discussed in the “Running Your First Container” section):

![Images](f0432-03.jpg)

If you’ve previously created this container and it’s currently stopped, you can get it up and running again using the **podman start** command.

3.   Check if the container is actively running:

`$ podman ps`

4.   Use the **podman generate systemd** command to take your running webserver container and create a systemd service configuration file:

`$ podman generate systemd --name webserver --new –files`

5.   Copy the configuration file to the ~/.config/systemd/user directory; if the directory doesn’t already exist, create it:

![Images](f0433-01.jpg)

6.   Stop and remove the active container:

![Images](f0433-02.jpg)

7.   Reload systemd so it recognizes the new unit file:

![Images](f0433-03.jpg)

8.   Start the container service and enable it to boot automatically at startup:

![Images](f0433-04.jpg)

Alternatively, the following command accomplishes both tasks at once:

![Images](f0433-05.jpg)

9.   To ensure systemd services for your user account start at system boot, run

![Images](f0433-06.jpg)

10.   Reboot your system:

![Images](f0433-07.jpg)

11.   Verify that your container is running and that the web server is accessible:

![Images](f0433-08.jpg)

12.   Finally, clean up:

![Images](f0433-09.jpg)

As an additional challenge, attempt this exercise as the root user. The differences here include not needing the **--user** option for **systemctl** commands and not having to run **loginctl enable-linger**. Moreover, the systemd configuration file should be relocated to /etc/systemd/system instead of the ~/.config/systemd/user directory.

#### Persistent Storage

Storage in containers is often described as “ephemeral,” meaning that it is temporary and its contents will not be retained once the container is removed. The fundamental nature of containerized applications is such that they operate on the assumption of always starting with a clean storage slate.

Let’s break down a few terms in the context of container images:

![Images](square.jpg)   *Ephemeral* means temporary. Any changes made to the container, such as adding files or modifying configurations, will be lost once the container is removed unless these changes are written to a persistent volume.

![Images](square.jpg)   *Immutable* means that a container based on that image will always start in the exact state of the image at the time of its creation.

![Images](square.jpg)   *Layered* means that each change to an image creates a new layer. These layers are stacked on top of each other, with each layer containing only the changes from the previous layer. This layered approach optimizes storage, simplifies updates and rollbacks, and speeds up container startup times.

While containers operate under the presumption of ephemeral and immutable storage, in some circumstances persistent storage is required. For instance, databases and other data-intensive applications require storage that persists beyond the lifespan of a single container instance. Persistent storage is also needed when multiple containers need to access the same data, or when data must be kept across updates and restarts.

Podman provides a solution for this by enabling the mounting of host directories inside a running container. The containerized application perceives these host directories as an integral part of the container storage, akin to how regular applications perceive a remote network volume as part of the host filesystem. Unlike the ephemeral storage in the container, the content of these host directories remains intact after the container is stopped, enabling them to be mounted to new containers as needed.

Let’s illustrate with an example. Assume you want to connect the contents of the directory ~/app on your host to a container named my-container under the directory /app. To achieve this, you would create the container with the following command:

![Images](f0434-01.jpg)

In this command, the **-v** option enables volume mounting, essentially linking a host directory (in this case, ~/app) to a directory inside the container (/app). The **Z** at the end instructs SELinux to apply the appropriate file context (container_file_t) to the directory.

One crucial point to note is that user IDs (UIDs) and group IDs (GIDs) inside a container differ from those of the user that initiated the container. This discrepancy occurs because containers have their own user namespaces, which can lead to permission issues when trying to access or modify files in the mounted directory. Hence, you must assign the correct permissions to the directory that you mount inside a container.

To put these concepts into practice, proceed to Exercise 10-4.

EXERCISE 10-4

**Attaching Persistent Storage to a Container**

This hands-on exercise walks you through a practical example of attaching persistent storage to a container, extending the webserver example from the section “Running Your First Container.”

1.   Log in as a regular user to your Linux system.

2.   Prepare the host directory that you want to mount onto your container. Create a directory called ~/html:

`$ mkdir ~/html`

3.   Navigate to the ~/html directory and create a file with some simple content. For instance, create an index.html file with the message “Welcome to our webserver!” by using the following **echo** command:

`$ echo "Welcome to our webserver" > ~/html/index.html`

4.   With your directory and file prepared, you are now ready to create and launch your container. Here, you will mount the ~/html directory from your local host to the /var/www/html directory within your container. Run the following command:

![Images](f0435-03.jpg)

5.   After creating and launching the container, ensure that it is actively running:

`$ podman ps`

6.   Next, verify that your web page is properly displayed. Use the **curl** command to fetch the content of the web page:

`$ curl http://localhost:8080`

You should see the message “Welcome to our webserver!”

7.   Experiment with changing the permissions of the ~/html directory on the host. Modify the permissions to make it accessible only by your user:

`$ chmod 700 ~/html`

8.   If you now try to access the web page, you will encounter a permission error. Verify this by running the following again:

`$ curl http://localhost:8080`

9.   To correct this, you need to adjust the permissions of the directory to make it accessible again. You can achieve this by setting the permissions back to 755:

`$ chmod 755 ~/html`

10.   Lastly, it’s time to clean up after the exercise:

![Images](f0436-02.jpg)

#### CERTIFICATION SUMMARY

This chapter delved into the transformative world of containers, an innovative technological development that has become a cornerstone in modern DevOps and cloud infrastructure ecosystems.

You can envision containers as secure, isolated boxes that encapsulate applications, functioning much like virtual machines. Yet, the comparison stops there. Containers are much more lightweight than virtual machines because they don’t need a separate operating system to function. They rely on and share the operating system of the host machine they’re running on. This unique characteristic allows containers to use fewer resources, and, as a result, they can initiate and terminate operations rapidly.

In RHEL 9, Podman is the tool of choice for managing containers. At the core of Podman operations is the **podman run** command, which creates a new container. This command can be customized with a plethora of subcommands and options to suit various scenarios.

The genesis of a container lies in an image, akin to a blueprint that specifies its structure and contents. These images act as templates from which containers are built. They are stored in dedicated storage locations known as registries, ready to be pulled and used whenever a container needs to be created.

In addition, images can also be tailor-made using a Containerfile, a text document that contains all the commands a user could call on the command line to assemble an image. Building images from a Containerfile opens up the possibility of creating personalized containers, fine-tuned to meet specific requirements.

Podman offers a comprehensive set of commands to manage and inspect containers and images, extending its usability far beyond mere creation. Some of the common commands include **podman create** for container creation, **podman start** for starting a container, **podman inspect** for inspecting container details, and **podman search** for searching images in a remote registry. However, this is just scratching the surface, and there are many more commands to explore.

One of the prominent features of Podman is the ability to run containers as systemd services that start automatically at boot. The **podman generate systemd** command can generate a systemd service configuration file based on a running container, enabling the seamless integration of containers into a systemd-driven system.

Despite their extensive capabilities, it’s important to remember that containers are ephemeral by nature. Their contents do not survive beyond their lifecycle. However, Podman provides a mechanism to persist data across container lifecycles. Host directories can be mounted inside a container using the **-v** option of the **podman run** command, enabling data to persist beyond the container’s lifespan and making it accessible to subsequent containers.

#### ![Images](right-a.jpg) TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in [Chapter 10](#ch10.xhtml).

##### Fundamentals of Container Technology

![Images](squ1.jpg)   DevOps practices have supported the use of containers, lightweight tools that ensure software consistency across different platforms.

![Images](squ1.jpg)   Containers are often favored over virtual machines due to their speed, efficiency, and portability.

![Images](squ1.jpg)   Container architecture utilizes key Linux features for process and resource isolation, such as namespaces, cgroups, and SELinux, along with standardized container images and container registries.

![Images](squ1.jpg)   Docker, responsible for popularizing container technology, now has major competition from Podman, a more secure and system-integrated alternative developed by Red Hat.

##### Getting Started with Containers

![Images](squ1.jpg)   The **container-tools** meta-package for RHEL 9 includes Podman, Skopeo, and Buildah.

![Images](squ1.jpg)   Containers can be created and started with the **podman run** command.

![Images](squ1.jpg)   Containers can be started in the background (detached) mode with the **-d** command option.

![Images](squ1.jpg)   Containers can be managed using their unique ID or their given name.

![Images](squ1.jpg)   After usage, containers can be cleaned up, with commands such as **podman rm** to remove containers and **podman rmi** to remove local images.

![Images](squ1.jpg)   Rootful containers, run by root users, have broad capabilities but also pose potential security risks, while rootless containers, run by non-root users, offer a more secure environment.

##### Building and Using Container Images

![Images](squ1.jpg)   Container images and registries provide a mechanism for storage, distribution, and versioning of container images.

![Images](squ1.jpg)   The **podman images** command allows you to view locally stored images.

![Images](squ1.jpg)   The **podman info** command provides configuration details about Podman, including currently configured registries.

![Images](squ1.jpg)   Notable registries include registry.access.redhat.com, registry.redhat.io, and docker.io (Docker Hub).

![Images](squ1.jpg)   The **podman search** command helps locate images across configured registries.

![Images](squ1.jpg)   For detailed information about specific images, the **skopeo inspect** command can be used.

![Images](squ1.jpg)   Building custom container images can be achieved through a Containerfile.

![Images](squ1.jpg)   The **podman build** command translates instructions from a Containerfile into a functional container image.

##### Managing Containers

![Images](squ1.jpg)   Running a container as a systemd service involves using the **podman generate systemd** command to create a systemd unit file from a running container.

![Images](squ1.jpg)   For nonprivileged users, systemd unit files are located in ~/.config/systemd/user, while for root they can be placed in /etc/systemd/system.

![Images](squ1.jpg)   In containers, storage is typically ephemeral and immutable. However, for certain applications like databases, persistent storage may be required.

![Images](squ1.jpg)   The **-v** option of the **podman run** command can mount a local directory into a mount point on a container.

#### Q SELF TEST

The following questions will help you measure your understanding of the material presented in this chapter. As there are no multiple-choice questions on the Red Hat exams, there are no multiple-choice questions in this book. These questions exclusively test your understanding of the chapter. Getting results, not memorizing trivia, is what counts on the Red Hat exams.

##### Fundamentals of Container Technology

**[1.](#ch10.xhtml_ch10ques1)**   What are the key differences between virtual machines and containers?

**[2.](#ch10.xhtml_ch10ques2)**   What are the key components of container architecture and how do they function?

**[3.](#ch10.xhtml_ch10ques3)**   How does Podman improve on Docker’s design?

##### Getting Started with Containers

**[4.](#ch10.xhtml_ch10ques4)**   What is the purpose of the **container-tools** meta-package in RHEL 9 and which key packages does it include?

**[5.](#ch10.xhtml_ch10ques5)**   Explain the process of running a container using the Podman tool, as well as the meaning of the **-d** and **-p** flags in the command.

**[6.](#ch10.xhtml_ch10ques6)**   Discuss the differences between rootless and rootful containers, their advantages, and when to use each.

##### Building and Using Container Images

**[7.](#ch10.xhtml_ch10ques7)**   What command do you run to build a container image and tag the image as dbserver if the Containerfile is in the current directory?

**[8.](#ch10.xhtml_ch10ques8)**   How do the **CMD** and **ENTRYPOINT** instructions differ in a Containerfile?

**[9.](#ch10.xhtml_ch10ques9)**   What is the function of the **skopeo inspect** command?

##### Managing Containers

**[10.](#ch10.xhtml_ch10ques10)**   How can you generate the configuration to run a container as a systemd service for a running container named ftpserver? Where should the unit configuration file be placed for a rootless container?

**[11.](#ch10.xhtml_ch10ques11)**   How do you ensure that a rootless container that is managed by a systemd unit named container-ftpserver.service is configured to automatically start at boot?

**[12.](#ch10.xhtml_ch10ques12)**   What is the meaning of the terms “ephemeral,” “immutable,” and “layered” in the context of container images?

#### LAB QUESTIONS

Red Hat presents its exams electronically. For that reason, the labs in this chapter are available from the companion website that accompanies the book. In case you haven’t yet set up RHEL 9 on a system, refer to [Chapter 1](#ch01.xhtml) for installation instructions. The answers for each lab follow the Self Test answers for the fill-in-the-blank questions

#### A SELF TEST ANSWERS

##### Fundamentals of Container Technology

**[1.](#ch10.xhtml_r_ch10ques1)**   Virtual machines and containers are both forms of virtualization, but they differ in their functionality and resource utilization. VMs are completely isolated and have their own operating system, making them more resource-intensive. In contrast, containers share the host’s operating system kernel, making them lighter and faster to start and stop. Containers, therefore, are highly portable and offer enough isolation for most use cases, making them popular for modern software development, particularly in DevOps and cloud computing.

**[2.](#ch10.xhtml_r_ch10ques2)**   Container architecture is composed of several Linux features designed to provide process and resource isolation, along with standardized container images and efficient use of container registries. The Linux features include namespaces that control the visibility of system resources, control groups (cgroups) that manage the allocation of system resources, and SELinux, which adds a robust security mechanism. Container images serve as blueprints for containers, packaging the software application, its dependencies, and some configuration details into a single object.

**[3.](#ch10.xhtml_r_ch10ques3)**   Podman, developed by Red Hat, addresses some of Docker’s security and design issues by offering a daemonless, rootless container engine. Unlike Docker, which requires a constantly running, high-privileged daemon to manage containers, Podman launches containers and containerized services as child processes, enhancing security and reducing the attack surface. Podman’s rootless feature also allows nonprivileged users to manage containers, further improving security.

##### Getting Started with Containers

**[4.](#ch10.xhtml_r_ch10ques4)**   The **container-tools** meta-package in RHEL 9 is used as a convenient method to install a group of related packages, and it doesn’t contain any tools itself. Key commands that come along with the meta-package include **podman** (a daemonless container engine), a script named **docker** (emulates Docker CLI executing Podman commands), Skopeo (a command-line utility for container images and repositories operations), and Buildah (a tool to build OCI container images).

**[5.](#ch10.xhtml_r_ch10ques5)**   Running a container using Podman involves using the **podman run** command. The **-d** flag specifies detached mode, which allows the container to run in the background and not occupy your current terminal or shell session. The **-p** flag exposes a specific port of the container, making it accessible. For example, **-p 80:8080** instructs Podman to open port 80 on the host machine and route all incoming traffic on this port to port 8080 inside the container.

**[6.](#ch10.xhtml_r_ch10ques6)**   A rootless container is run by a nonprivileged user, whereas a rootful container is run by a privileged user. Rootless containers, run by non-root users, offer a more constrained and controlled environment, thus posing less risk to the host system. They are generally preferred for their higher security. Conversely, rootful containers, run by the root user, have broad capabilities. For example, they can bind to network ports lower than 1024.

##### Building and Using Container Images

**[7.](#ch10.xhtml_r_ch10ques7)**   If the Containerfile is in the current directory, the command to build a container image and tag the image as dbserver is shown next:

`$ podman build -t dbserver .`

**[8.](#ch10.xhtml_r_ch10ques8)**   The **CMD** instruction specifies a default command, and its arguments that will be executed when you initiate the container with the **podman run** command. However, this can be overridden by providing a command to **podman run**. On the other hand, the **ENTRYPOINT** instruction sets a command that always executes upon the container’s startup and remains persistent even if a command is provided to **podman run**. **ENTRYPOINT** can also be overridden, but doing so requires the explicit **--entrypoint** flag.

**[9.](#ch10.xhtml_r_ch10ques9)**   The **skopeo inspect** command provides intricate details about a specific image. This can be vital for evaluating whether a specific image aligns with your requirements. For example, the following command provides detailed information about the httpd-24 image:

`$ skopeo inspect docker://registry.access.redhat.com/ubi9/httpd-24`

##### Managing Containers

**[10.](#ch10.xhtml_r_ch10ques10)**   You can generate the configuration to run a container named ftpserver as a systemd service by using the following command:

`$ podman generate systemd --name ftpserver --files --new`

The unit configuration file must be copied to the ~/.config/systemd/user directory.

**[11.](#ch10.xhtml_r_ch10ques11)**   To ensure that a rootless container that is managed by a systemd unit named container-ftpserver.service is configured to automatically start at boot, you must run the following commands:

![Images](f0441-04.jpg)

**[12.](#ch10.xhtml_r_ch10ques12)**   “Ephemeral” in the context of container images means temporary; any changes made to the container will be lost once it’s removed, unless these changes are written to a persistent volume. “Immutable” means that an image, once created, doesn’t change. Any container based on that image will always start in the exact state of the image at its creation. “Layered” means each change to an image creates a new layer, with each layer containing only the changes from the previous layer. This approach optimizes storage, simplifies updates and rollbacks, and speeds up container startup times.

#### LAB ANSWERS

##### Lab 1

BusyBox represents a valuable image for executing various tools or functioning as a foundation for additional containers.

**1.**   Search for the image through the following command:

`$ podman search busybox`

**2.**   Once you’ve located the image, pull it using the following command:

`$ podman pull docker.io/library/busybox`

**3.**   To verify the size of the image, which should be less than 5MB (demonstrating its lightweight nature), execute the following:

`$ podman images`

**4.**   Attempting to run a container using the busybox image in detached mode will result in the container’s immediate termination:

`$ podman run -d --name busybox busybox`

**5.**   You can verify this phenomenon using the **podman ps** command. The first command shown will not show the busybox container, as it’s not running, while the subsequent command, with the **-a** option, will show all containers, including the ones in a stopped state:

![Images](f0442-05.jpg)

**6.**   Proceed by deleting the current container and creating a fresh one that runs the /bin/sh shell:

![Images](f0442-06.jpg)

**7.**   Inside this shell, you can execute the **ls /bin** command to explore the commands available within the image. Remember, this command is executed within the container’s environment. You can quit this interactive shell by typing **exit**.

**8.**   Moving to the last task, initiate a container that runs a ping to [www.google.com](http://www.google.com):

`podman run busybox ping -c 5 www.google.com`

##### Lab 2

In this activity, you’re asked to build a Python image that runs a simple service that returns “pong” when pinged.

**1.**   Search for the Python 3.9 image with this command:

`$ podman search python-39`

This shows you the Red Hat UBI 9 Python 3.9 image to use.

**2.**   Make a Containerfile that tells Podman how to create your image. Here’s what you need to put in it:

![Images](f0443-02.jpg)

**3.**   You also need to create the pingpong.py file in the same directory. Make sure you copy the content provided in the lab exercise into this file.

**4.**   Build the image:

`$ podman build -t pingpong .`

**5.**   Create a container from the image you just made with this command:

`$ podman run -d --name pingpong -p 1234:8000 pingpong`

Pay attention to the -**p 1234:8000** command option. This tells Podman to connect TCP port 1234 on your computer to port 8000 on the container.

**6.**   Make sure the container is running with **podman ps**.

**7.**   Test the service with this command:

`$ curl http://localhost:1234/ping`

It should respond with “pong.”

**8.**   If something goes wrong, you can check the logs with **podman logs pingpong**.

**9.**   Do not stop or remove the container, as you’ll be using it for the next lab.

##### Lab 3

In this lab task, you’re building upon the steps you accomplished in Lab 2, but this time as a non-root user.

**1.**   Execute the following command to generate a systemd configuration file for your container service:

`$ podman generate systemd --name pingpong --new --files`

This command results in creating a container-pingpong.service file in your current directory.

**2.**   Move this file into the ~/.config/systemd/user directory. If this directory doesn’t already exist, you’ll have to create it:

![Images](f0444-02.jpg)

**3.**   Stop and remove the current pingpong container:

![Images](f0444-03.jpg)

**4.**   Refresh systemd and set up the service to automatically start when your system boots:

![Images](f0444-04.jpg)

**5.**   To verify that everything is set up correctly, reboot your system and check if the container is running:

![Images](f0444-05.jpg)

**6.**   Use the following commands to stop and remove the container and its image:

![Images](f0444-06.jpg)

To replicate this task and run the container as a root user, please be aware of a few subtleties. You should first move the existing container-pingpong.service file from the ~/.config/systemd/user directory to the /etc/systemd/system directory. It’s important to ensure that the rootless container has been halted and deleted beforehand. Furthermore, verify that the pingpong image has been built by the root user.

After ensuring this, proceed with the following commands to configure the service to initiate automatically at boot:

![Images](f0444-07.jpg)

Note that for a container running as root, the command **loginctl enable-linger** is not necessary.

##### Lab 4

This lab dives deep into the dynamics of ephemeral and persistent storage in containerized applications. Understanding the difference between these two storage types is crucial as it directly impacts the behavior and longevity of data within your containers. Ephemeral storage, as the name implies, is temporary and does not survive container re-creation, while persistent storage allows data to survive beyond the life of a single container.

**1.**   Set up and run a container that uses the Apache 2.4 web server (as covered earlier in the chapter). Before you begin, ensure that no other containers are currently using the same port; otherwise, the command to start the container will fail. Run the following command to start the container:

![Images](f0445-01.jpg)

**2.**   With the container running, open a shell inside it using the following command:

![Images](f0445-02.jpg)

**3.**   Within this shell, create the /var/www/html/index.html file and populate it with the text “Welcome to our webserver!”:

![Images](f0445-03.jpg)

**4.**   You can confirm that the newly created index.html page is being served by running the following command on your host:

![Images](f0445-04.jpg)

**5.**   Explore the ephemeral nature of container storage by stopping and removing the container and creating and running a new one with the same command:

![Images](f0445-05.jpg)

**6.**   If you check your web page now, you’ll see that the changes you made have been lost and the web page has reverted to its default state. This demonstrates the ephemeral nature of container storage:

![Images](f0445-06.jpg)

**7.**   Stop and remove the container again:

![Images](f0445-07.jpg)

**8.**   Explore the concept of persistent storage by creating a local ~/html directory on your host machine and adding the index.html file to it:

![Images](f0446-01.jpg)

**9.**   Re-create the container, but this time, mount the local ~/html directory to /var/www/html inside the container:

![Images](f0446-02.jpg)

**10.**   Confirm the visibility of the web page:

![Images](f0446-03.jpg)

Notice that even if you stop and delete the container and re-create it using the command provided in Step 9, the index.html file, which is now a part of persistent storage, is retained. This demonstrates the persistence of the storage—your changes are preserved across container lifetimes.

## Appendix A

## Prepare a System for the Sample Exams

Randy Russell, the Director of Certification at Red Hat, revealed in a blog post that Red Hat exams no longer mandate a “bare-metal installation.” Put simply, you will be provided with a pre-installed system when you sit for a Red Hat exam today. This appendix guides you through the setup of a pre-installed system suitable for the two sample exams accessible on McGraw Hill’s companion website. Details regarding each exam are provided on the first few pages of Appendixes B and C, respectively, followed by their solutions.

### Sample Exam System Requirements

As highlighted in [Chapter 1](#ch01.xhtml), a genuine RHEL 9 subscription is ideal for this purpose. Exercise 1-1 described how to enroll in the Red Hat Developer Program and obtain a Red Hat Developer Subscription for Individuals at no cost. Rebuild distributions, such as AlmaLinux, should function just as effectively since they are grounded on the openly available RHEL 9 source code. However, we strongly advise against using Fedora Linux for studying for Red Hat exams. Despite RHEL 9 being rooted in Fedora Linux, RHEL 9 presents a distinctive look and feel and, in certain instances, differs in functionality from the most similar Fedora release, Fedora 34.

Keeping these considerations in mind, we recommend using the server1.example.com and tester1.example.com virtual systems that you initially set up in [Chapter 1](#ch01.xhtml). However, you will need to reinstall RHEL 9 on both systems and configure them according to the following specifications before commencing the sample RHCSA exams:

![Images](square.jpg)   **Network settings** For server1.example.com, assign a random IPv4 address and netmask during installation to render the system network unreachable. On tester1.example.com, leave the IPv4 default settings to use DHCP and set the hostname to tester1.example.com. These settings can be found on the Networks and Hostname configuration screen, as shown in [Figures 1-6](#ch01.xhtml_ch1fig6) and [1-7](#ch01.xhtml_ch1fig7).

![Images](square.jpg)   **Root password** On server1.example.com, set a random password and forget about it (you will execute password recovery during the sample exams). On tester1.example.com, set the root password to changeme.

![Images](square.jpg)   **Disk space** On server1.example.com, select custom partitioning and manually configure the /boot and / partitions. Do not format the entire disk, and leave 1GB unallocated. On tester1.example.com, select automatic partitioning. For additional guidance on this topic, please consult the "Partition Creation Exercise" section in [Chapter 1](#ch01.xhtml).

![Images](square.jpg)   **Software selection** In the Software Selection screen, keep the default option Server with GUI selected, as shown in [Figure 1-13](#ch01.xhtml_ch1fig13).

![Images](square.jpg)   **System subscription** After the installation is completed, on tester1.example.com, set up the system to obtain packages from the Red Hat Network using the following commands:

![Images](f0448-01.jpg)

![Images](square.jpg)   **Web service** On tester1.example.com, install an Apache web server by executing the following command:

![Images](f0448-02.jpg)

In the /etc/httpd/conf/httpd.conf file, change the following line:

`DocumentRoot "/var/www/html"`

to the following:

`DocumentRoot "/html"`

Also change this line:

`Listen 80`

to the following:

`Listen 8234`

Then, add the following lines at the bottom of the file:

![Images](f0449-01.jpg)

Finally, run the following commands:

![Images](f0449-02.jpg)

INSIDE THE EXAM

While the setup of an Apache web server is not an RHCSA exam requirement, you should be able to “configure firewall settings using firewall-cmd/firewalld” and “manage SELinux port labels” and "file contexts” to make a service operational.

![Images](square.jpg)   **NFS service** On tester1.example.com, set up the NFS. First, add the following lines to /etc/exports:

![Images](f0449-03.jpg)

Then, run the following commands:

![Images](f0449-04.jpg)

INSIDE THE EXAM

Again, setting up an NFS server isn’t an RHCSA exam requirement, but you should be able to “mount and unmount network file systems using NFS.”

## Appendix B

## Solutions to RHCSA Sample Exam 1

The questions in the RHCSA Sample Exam 1 will help measure your understanding of the material covered in this book. As indicated in the introduction, you should be capable of completing the RHCSA exam in 3 hours. However, we have capped the time for this lab at 2.5 hours to accustom you to working under time constraints.

The RHCSA exam follows a “closed book” format. Nevertheless, you are permitted to refer to any documentation available on the Red Hat Enterprise Linux computer. Although test centers permit note-taking, these notes cannot be taken out of the examination room.

In the majority of cases, there isn’t a single solution or method to resolve a problem or install a service. With the plethora of options available in Linux, it is impossible to cover every potential scenario.

For the forthcoming exercises, avoid using a production computer. Even a minor error in any of these exercises could render Linux unbootable. If you cannot recover using the steps provided in these exercises, you might need to reinstall Red Hat Enterprise Linux. Consequently, you may not be able to recover any data saved on the local system.

Red Hat conducts its exams electronically, which is why the exams in this book can be accessed from the McGraw Hill companion website. This exam, named RHCSAsampleexam1, is available in Microsoft Word format. For instructions on setting up RHEL 9 as a suitable system for a practice exam, please refer to Appendix A.

### RHCSA Sample Exam 1 Discussion

In this discussion, we’ll describe briefly one way to meet the requirements listed for the RHCSA Sample Exam 1.

1.   To complete this task, review Exercise 5-2, “Recover the Root Password,” in [Chapter 5](#ch05.xhtml).

2.   Assuming that the network interface is named eth0, that the NAT subnet address of your VMware Workstation Player setup is 192.168.0.100, and that the IP of the default gateway/DNS is 192.168.0.2, execute the following commands:

![Images](f0453-01.jpg)

3.   To complete this task, review Exercise 4-2 in [Chapter 4](#ch04.xhtml).

4.   Create a file named /etc/yum.repos.d/epel.repo and add the following content:

![Images](f0453-02.jpg)

Then, run the following command to install the htop RPM:

![Images](f0453-03.jpg)

5.   Use the **parted** command to create a new partition. Assume that your hard drive is /dev/vda, the new partition is number 3, and there is some free space starting at about 19GB. Start the **parted** utility with **parted /dev/vda** and type

![Images](f0453-04.jpg)

Then, run the following commands:

![Images](f0453-05.jpg)

6.   Format the volume and create the mount point:

![Images](f0454-01.jpg)

To make sure that the volume is automatically mounted the next time the system is booted, configure it in /etc/fstab to the appropriate format, with the UUID associated with the volume, as provided by the **blkid** command:

![Images](f0454-02.jpg)

Then, add the following line to /etc/fstab:

![Images](f0454-03.jpg)

7.   Run the following command to complete this task:

![Images](f0454-04.jpg)

8.   To complete this task, run:

![Images](f0454-05.jpg)

9.   The /home/engineers directory should be owned by the group engineers. As long as users donna and mike are not part of that group, and other users don’t have permissions (or ACLs) on that directory, access should be limited to members of the engineers group. The directory should also have SGID permissions:

![Images](f0454-06.jpg)

10.   If you’ve modified user mike’s account to make his account expire in seven days, the right expiration date should appear in the output to the **chage -l mike** command. To complete the task, run

![Images](f0454-07.jpg)

11.   There are a number of ways to set up a cron job; it could be configured in the /etc/crontab file or as a cron job for the user root or mike with the **crontab -u <user> -e** command. To complete the exercise, you can add the following line to /etc/crontab:

![Images](f0455-01.jpg)

12.   One effective way to share a file between users is to create a group, add the relevant users to that group, and then change the file’s group ownership to that group. Create a new group, for example, “projectgroup”:

![Images](f0455-02.jpg)

Add users mike and donna to projectgroup:

![Images](f0455-03.jpg)

Next, as user mike, create the file, change its group ownership, and modify the file permissions to enable read access for the group:

![Images](f0455-04.jpg)

13.   Create a file /usr/local/bin/backup.sh with the following content and make it executable with **chmod +x /usr/local/bin/backup.sh**:

![Images](f0455-05.jpg)

Next, schedule the script to run automatically at 2:00 A.M. daily to create a backup of the /home directory in the /tmp filesystem. To do so, add the following line to /etc/crontab:

![Images](f0455-06.jpg)

14.   First, create the user sam:

![Images](f0456-01.jpg)

Then, configure NFS automounting. Install the autofs package:

![Images](f0456-02.jpg)

In the /etc/auto.master file, add the following line:

![Images](f0456-03.jpg)

Now, you need to create and configure the map file (/etc/auto.nethome) you just referenced in the auto.master file. This file will contain the following line (substitute for the IP address of tester1.example.com):

![Images](f0456-04.jpg)

After the configuration files are set up, start and enable the autofs service:

![Images](f0456-05.jpg)

Now, if you open a shell as user sam (**su – sam**), the NFS share from tester1.example.com:/sam will be automatically mounted as user sam’s home directory. The **-rw** option ensures that the NFS share is mounted in read-write mode.

15.   On tester1.example.com, run

![Images](f0456-06.jpg)

After running this command, Apache should be able to bind to port 8234\. You can verify this with the following command on tester1.example.com:

![Images](f0456-07.jpg)

16.   Run the following commands on tester1.example.com to allow other hosts to connect to the web server on port 8234:

![Images](f0456-08.jpg)

Change the SELinux context of the /html directory to the type httpd_sys_content_t. This type is used for static web content that should be accessible by **httpd**:

![Images](f0456-09.jpg)

The argument **"/html(/.*)?"** is a regular expression that matches the /html directory and all its subdirectories and files. The **-a** option is used to add a record. After that, use the **restorecon** command to apply this context mapping to the running filesystem:

![Images](f0456-10.jpg)

Then, the following command on server1.example.com should display the “Success!” test page (substitute for the IP address of tester1):

![Images](f0457-01.jpg)

17.   Run the following commands as user mike to start the container:

![Images](f0457-02.jpg)

Execute the following command to generate a systemd configuration file for the container service:

![Images](f0457-03.jpg)

This command results in creating a container-httpd.service. Next, copy this file into the /home/mike/.config/systemd/user directory. If this directory doesn’t already exist, you’ll have to create it:

![Images](f0457-04.jpg)

Afterwards, you’ll need to stop and remove the current httpd container:

![Images](f0457-05.jpg)

Now, it’s time to refresh systemd and set up the service to automatically start when your system boots:

![Images](f0457-06.jpg)

To verify that everything is set up correctly, reboot your system and check if the container is running:

![Images](f0457-07.jpg)

18.   Just like with all Red Hat exams, it’s essential for your modifications to endure a system reboot. Therefore, reboot the system and verify that your configurations remain fully functional.

## Appendix C

## Solutions to RHCSA Sample Exam 2

The questions in the RHCSA Sample Exam 2 will help measure your understanding of the material covered in this book. As indicated in the introduction, you should be capable of completing the RHCSA exam in 3 hours. However, we have capped the time for this lab at 2.5 hours to accustom you to working under time constraints.

The RHCSA exam follows a “closed book” format. Nevertheless, you are permitted to refer to any documentation available on the Red Hat Enterprise Linux computer. Although test centers permit note-taking, these notes cannot be taken out of the examination room.

In the majority of cases, there isn’t a single solution or method to resolve a problem or install a service. With the plethora of options available in Linux, it is impossible to cover every potential scenario.

For the forthcoming exercises, avoid using a production computer. Even a minor error in any of these exercises could render Linux unbootable. If you cannot recover using the steps provided in these exercises, you might need to reinstall Red Hat Enterprise Linux. Consequently, you may not be able to recover any data saved on the local system.

Red Hat conducts its exams electronically, which is why the exams in this book can be accessed from the McGraw Hill companion website. This exam, named RHCSAsampleexam2, is available in Microsoft Word format. For instructions on setting up RHEL 9 as a suitable system for a practice exam, please refer to Appendix A.

### RHCSA Sample Exam 2 Discussion

In this discussion, we’ll describe briefly one way to meet the requirements listed for the RHCSA Sample Exam 2.

1.   To complete this task, review Exercise 5-2, “Recover the Root Password,” in [Chapter 5](#ch05.xhtml).

2.   Assuming that the network interface is named eth0, execute the following commands:

![Images](f0461-01.jpg)

3.   To complete this task, review Exercise 4-2, “Subscribe a System to the Red Hat Subscription Management,” in [Chapter 4](#ch04.xhtml). Then, install the tmux RPM package with the following command:

![Images](f0461-02.jpg)

4.   Use the **parted** command to create a new partition. Assume that your hard drive is /dev/vda, the new partition is number 3, and there is some free space starting at about 19GB. Start the **parted** utility with **parted /dev/vda** and type

![Images](f0461-03.jpg)

5.   Run the following commands to format the filesystem and create the mount point:

![Images](f0461-04.jpg)

Add an entry to the /etc/fstab file. You will use the UUID (Universally Unique Identifier) of the partition for this, which you can obtain by running the **blkid** command as follows:

![Images](f0461-05.jpg)

Then, add the following line to /etc/fstab:

![Images](f0461-06.jpg)

And mount the filesystem:

![Images](f0461-07.jpg)

6.   Use the **parted** command to create a new partition. Assume that your hard drive is /dev/vda, and the new partition is number 4\. Start the **parted** utility and type

![Images](f0462-01.jpg)

7.   Format the new partition as swap:

![Images](f0462-02.jpg)

Find the UUID of the partition:

![Images](f0462-03.jpg)

Then, add the following line to /etc/fstab:

![Images](f0462-04.jpg)

And mount the filesystem:

![Images](f0462-05.jpg)

8.   The following command shows one method to complete this task:

![Images](f0462-06.jpg)

9.   New local users should be listed in /etc/passwd and /etc/shadow. To specifically deny regular users access to a directory, you can create a dedicated group for this purpose, for example “sysadmins”. You should be able to confirm that users bill and richard don’t have access to the /sysadmins directory by trying to list its contents or creating a file in it.

To complete the task, run the following commands:

![Images](f0462-07.jpg)

10.   Install the autofs and nfs-utils packages:

![Images](f0463-01.jpg)

Then, add the following line to /etc/auto.misc:

![Images](f0463-02.jpg)

To confirm your change, add an ISO file to the virtual drive on the virtual machine. Then, run the **ls /misc/dvd** command, and the automounter should mount the DVD and provide file information on that drive. This should be an easy configuration, based on a slight change to the default /etc/auto.misc file. Of course, you’ll need to make sure the autofs service runs after a reboot, which you can confirm with the **systemctl is-enabled autofs** command.

11.   To set the system to boot into the multi-user target by default, use the following command:

![Images](f0463-03.jpg)

You can verify that the default target has been set correctly with this command:

![Images](f0463-04.jpg)

12.   Open the file /etc/chrony.conf and locate any lines that start with server or pool. Comment those lines out by adding a # character at the beginning of each line. Then, add a new line to specify time.google.com as the server:

![Images](f0463-05.jpg)

Restart the **chronyd** daemon to apply the changes:

![Images](f0463-06.jpg)

To verify the current NTP sources, run

![Images](f0463-07.jpg)

13.   Open the /etc/selinux/config file. Locate the line that starts with **SELINUX=**. This line specifies the SELinux mode. Change it to **SELINUX=permissive**, save the file, and reboot the system. To verify that SELinux is set in permissive mode, run the **sestatus** command.

14.   Make sure the NFS client utilities are installed. You can do so with the following command:

![Images](f0463-08.jpg)

Create the directory where the NFS share will be mounted:

![Images](f0464-01.jpg)

Then, add the following line to /etc/fstab (substitute for the IP address of tester1.example.com):

![Images](f0464-02.jpg)

To mount the filesystem, run

![Images](f0464-03.jpg)

15.   As user mark on server1.example.com, generate an RSA SSH key pair with a key length of 4096 bits:

![Images](f0464-04.jpg)

Now, create user mike on tester1.example.com:

![Images](f0464-05.jpg)

Then, on server1.example.com, copy the public key to the destination server tester1.example.com. You can do this using the **ssh-copy-id** command (substitute for the IP address of tester1.example.com):

![Images](f0464-06.jpg)

You will be prompted to enter user mike’s password for tester1.example.com to allow the copy operation. Now, user mark from server1.example.com should be able to SSH into tester1.example.com as user mike using key-based authentication. When you initiate the SSH connection, you’ll be prompted to enter the passphrase for the key.

16.   First, make sure that the tuned RPM is installed and the service is running. If not, install the package, start the service, and enable it to start at boot:

![Images](f0464-07.jpg)

Now, to activate the virtual-guest profile, use the **tuned-adm** tool:

![Images](f0464-08.jpg)

To verify the active profile, you can use the following command:

![Images](f0464-09.jpg)

17.   As user bill, create a Containerfile with the following content:

![Images](f0465-01.jpg)

Use the following command to build the image:

![Images](f0465-02.jpg)

18.   Just like with all Red Hat exams, it’s essential for your modifications to endure a system reboot. Therefore, reboot the system and verify that your configurations remain fully functional.

## Appendix D

## About the Online Content

This book comes with online resources, including the labs for each chapter, a copy of Appendix A, “Prepare a System for the Sample Exams,” and files for the simulated sample RHCSA exams in a downloadable .zip file.

### Single User License Terms and Conditions

Online access to the digital content included with this book is governed by the McGraw Hill License Agreement outlined next. By using this digital content you agree to the terms of that license.

**Access**  To download your online content, simply follow these easy steps.

1.   Go to [https://www.mhprofessional.com/redhatlinux](https://www.mhprofessional.com/redhatlinux).

2.   You can also go to this URL: [https://www.mhprofessional.com](https://www.mhprofessional.com) and type the ISBN **9781260462074** into the Search By ISBN box.

3.   You will be taken to the book’s page. Click the Downloads & Resources tab, where you will find a link to download the online content for this book.

**Duration of License**  Access to your online content through the Web site will expire one year from the date the publisher declares the book out of print.

Your purchase of this McGraw Hill product through a retail store is subject to the refund policy of that store.

The Content is a copyrighted work of McGraw Hill, and McGraw Hill reserves all rights in and to the Content. The Work is © 2024 by McGraw Hill.

**Restrictions on Transfer**  The user is receiving only a limited right to use the Content for the user’s own internal and personal use, dependent on purchase and continued ownership of this book. The user may not reproduce, forward, modify, create derivative works based upon, transmit, distribute, disseminate, sell, publish, or sublicense the Content or in any way commingle the Content with other third-party content without McGraw Hill’s consent.

**Limited Warranty**  The McGraw Hill Content is provided on an “as is” basis. Neither McGraw Hill nor its licensors make any guarantees or warranties of any kind, either express or implied, including, but not limited to, implied warranties of merchantability or fitness for a particular purpose or use as to any McGraw Hill Content or the information therein or any warranties as to the accuracy, completeness, correctness, or results to be obtained from, accessing or using the McGraw Hill Content, or any material referenced in such Content or any information entered into licensee’s product by users or other persons and/or any material available on or that can be accessed through the licensee’s product (including via any hyperlink or otherwise) or as to non-infringement of third-party rights. Any warranties of any kind, whether express or implied, are disclaimed. Any material or data obtained through use of the McGraw Hill Content is at your own discretion and risk and user understands that it will be solely responsible for any resulting damage to its computer system or loss of data.

Neither McGraw Hill nor its licensors shall be liable to any subscriber or to any user or anyone else for any inaccuracy, delay, interruption in service, error or omission, regardless of cause, or for any damage resulting therefrom.

In no event will McGraw Hill or its licensors be liable for any indirect, special or consequential damages, including but not limited to, lost time, lost money, lost profits or good will, whether in contract, tort, strict liability or otherwise, and whether or not such damages are foreseen or unforeseen with respect to any use of the McGraw Hill Content.

### Downloadable Book Resources

The following sections detail the resources available with your book. You can access these items by selecting the Download & Resources tab toward the bottom of the page at the URL listed above and clicking on the Download link. All the resources are available in one convenient .zip file. Download the .zip file to proceed.

#### Lab Files

The lab files for each chapter are arranged in a directory within the .zip file with a folder for each chapter. The lab files are available in Microsoft Word format. The lab solutions can be found in the Self Test section of each chapter.

#### Appendix A: Prepare a System for the Sample Exams

Appendix A provides instructions on how to prepare your system to take the sample RHCSA exams. The PDF can be found in the Appendix A folder in the .zip file.

#### Sample Exams

Two sample exams are available, each simulating the RHCSA exam experience. Each sample exam is available in Microsoft Word format in the Sample Exam 1 and Sample Exam 2 folders.

### Technical Support

For questions regarding downloadable book content, visit [https://mhedu.force.com/CSOM/s/](https://mhedu.force.com/CSOM/s/).

## INDEX

~ (tilde), 52

**A**

Access Vector Cache messages, [340](#ch08.xhtml_page_340)

accounts

command-line tools for, [225](#ch06.xhtml_page_225)–228

managing, [216](#ch06.xhtml_page_216)

modifying, [230](#ch06.xhtml_page_230)–232

system, [217](#ch06.xhtml_page_217), [329](#ch08.xhtml_page_329)

Address Resolution Protocol (ARP), [99](#ch03.xhtml_page_99)

administrative control, [232](#ch06.xhtml_page_232)

administrative users, [3](#ch01.xhtml_page_3), [232](#ch06.xhtml_page_232)

default aliases, [58](#ch02.xhtml_page_58)

/etc/group file and, [220](#ch06.xhtml_page_220)–221

home directory, [52](#ch02.xhtml_page_52)

PATH, [54](#ch02.xhtml_page_54)

regular user differences from, [49](#ch02.xhtml_page_49)

special file attributes and, [62](#ch02.xhtml_page_62)–63

su command and, [233](#ch06.xhtml_page_233)–234

SUID bit and, [62](#ch02.xhtml_page_62)

system installation and, [35](#ch01.xhtml_page_35)

UID of, [68](#ch02.xhtml_page_68)

AIX, [2](#ch01.xhtml_page_2)

alias command, [57](#ch02.xhtml_page_57)–58, [217](#ch06.xhtml_page_217)

AlmaLinux, [2](#ch01.xhtml_page_2)–3, [9](#ch01.xhtml_page_9)

Anaconda, [23](#ch01.xhtml_page_23)

anacron command, [372](#ch09.xhtml_page_372)–373, [384](#ch09.xhtml_page_384)–385

Apache web server, [192](#ch05.xhtml_page_192)

log files, [389](#ch09.xhtml_page_389)

port labels and, [338](#ch08.xhtml_page_338)

application level virtualization, [8](#ch01.xhtml_page_8)

AppStream repository, [130](#ch04.xhtml_page_130), [163](#ch04.xhtml_page_163)

apropos command, [80](#ch02.xhtml_page_80)

archiving, [354](#ch09.xhtml_page_354), [367](#ch09.xhtml_page_367)–369

ARP. *See* Address Resolution Protocol

arp command, [95](#ch03.xhtml_page_95)–96

at.allow, [376](#ch09.xhtml_page_376)

at command, [354](#ch09.xhtml_page_354), [369](#ch09.xhtml_page_369)

running job with, [374](#ch09.xhtml_page_374)–375

securing, [375](#ch09.xhtml_page_375)–376

at.deny, [376](#ch09.xhtml_page_376)

atq command, [376](#ch09.xhtml_page_376)

atrm command, [376](#ch09.xhtml_page_376)

auditd service, [331](#ch08.xhtml_page_331)

audits

log files for, [391](#ch09.xhtml_page_391)

SELinux, [313](#ch08.xhtml_page_313), [339](#ch08.xhtml_page_339)–340

with top command, [356](#ch09.xhtml_page_356)

ausearch command, [340](#ch08.xhtml_page_340)

authorized_keys file, [325](#ch08.xhtml_page_325)

authpriv logging rules, [389](#ch09.xhtml_page_389)–390

autofs, [254](#ch07.xhtml_page_254), [296](#ch07.xhtml_page_296)–297, [299](#ch07.xhtml_page_299)

automated installations, [3](#ch01.xhtml_page_3)

automounter service, [254](#ch07.xhtml_page_254), [296](#ch07.xhtml_page_296)–300

Avahi daemon, [339](#ch08.xhtml_page_339)

awk command, [73](#ch02.xhtml_page_73)

**B**

bare-metal hypervisors, [8](#ch01.xhtml_page_8)

baseline packages, [35](#ch01.xhtml_page_35)

BaseOS repository, [130](#ch04.xhtml_page_130), [150](#ch04.xhtml_page_150), [163](#ch04.xhtml_page_163)

bash, [44](#ch02.xhtml_page_44), [46](#ch02.xhtml_page_46)

history, [51](#ch02.xhtml_page_51)

.bash_logout, [237](#ch06.xhtml_page_237)

.bash_profile, [237](#ch06.xhtml_page_237)

.bashrc, [237](#ch06.xhtml_page_237)

bash scripts, [355](#ch09.xhtml_page_355)

control structures, [381](#ch09.xhtml_page_381)–386

creating, [386](#ch09.xhtml_page_386)–388

environment variables and, [379](#ch09.xhtml_page_379)

for loop, [385](#ch09.xhtml_page_385)–386

parameter expansion, [380](#ch09.xhtml_page_380)–381

parameters, [380](#ch09.xhtml_page_380)

positional parameters, [380](#ch09.xhtml_page_380), [386](#ch09.xhtml_page_386)

running, [377](#ch09.xhtml_page_377)–378

scope of variables, [379](#ch09.xhtml_page_379)

special parameters, [380](#ch09.xhtml_page_380)

test operators and conditional constructs, [382](#ch09.xhtml_page_382)–383

variables, [378](#ch09.xhtml_page_378)

basic encrypted communication, [325](#ch08.xhtml_page_325)–327

Basic Input/Output System (BIOS), [7](#ch01.xhtml_page_7), [173](#ch05.xhtml_page_173), [175](#ch05.xhtml_page_175)

partitions, [257](#ch07.xhtml_page_257)

Bell-LaPadula model, [330](#ch08.xhtml_page_330)

BIOS. *See* Basic Input/Output System

blkid command, [290](#ch07.xhtml_page_290), [294](#ch07.xhtml_page_294), [298](#ch07.xhtml_page_298)

boolean settings

enforce, [331](#ch08.xhtml_page_331)

managing, [334](#ch08.xhtml_page_334)

SELinux, [313](#ch08.xhtml_page_313), [331](#ch08.xhtml_page_331), [334](#ch08.xhtml_page_334), [340](#ch08.xhtml_page_340), [342](#ch08.xhtml_page_342)–343

/boot directory

files in, [136](#ch04.xhtml_page_136)

filesystem volume, [28](#ch01.xhtml_page_28)–29

mount point, [31](#ch01.xhtml_page_31)

/boot/efi/EFI/redhat/grub.cfg, [182](#ch05.xhtml_page_182)–183

bootloaders, [176](#ch05.xhtml_page_176)–177

modifying, [182](#ch05.xhtml_page_182)–184

boot media, [22](#ch01.xhtml_page_22)–23

rescue mode, [188](#ch05.xhtml_page_188)

boot process, [174](#ch05.xhtml_page_174)

basic system configuration, [175](#ch05.xhtml_page_175)–176

booting to different target, [180](#ch05.xhtml_page_180)–181

bootloaders, [176](#ch05.xhtml_page_176)–177

first process, targets, units, [191](#ch05.xhtml_page_191)–193

kernels and initial RAM disk, [190](#ch05.xhtml_page_190)

rd.break option, [179](#ch05.xhtml_page_179)

startup menus, [176](#ch05.xhtml_page_176)

switching targets, [193](#ch05.xhtml_page_193)

bridged networks, [16](#ch01.xhtml_page_16)

Btrfs filesystem, [274](#ch07.xhtml_page_274), [276](#ch07.xhtml_page_276)

Buildah, [412](#ch10.xhtml_page_412)

bunzip2 command, [367](#ch09.xhtml_page_367)

Burrows-Wheeler block sorting algorithm, [367](#ch09.xhtml_page_367)

bzip2 command, [354](#ch09.xhtml_page_354), [367](#ch09.xhtml_page_367)–368

**C**

cat command, [49](#ch02.xhtml_page_49), [69](#ch02.xhtml_page_69)–70

cd command, [52](#ch02.xhtml_page_52), [54](#ch02.xhtml_page_54)

CD/DVD drives, [293](#ch07.xhtml_page_293)–294

CentOS Linux, [11](#ch01.xhtml_page_11)

CentOS Stream, [11](#ch01.xhtml_page_11)

cgroup2 filesystem, [293](#ch07.xhtml_page_293)

cgroups, [195](#ch05.xhtml_page_195)–196, [410](#ch10.xhtml_page_410)

chage command, [216](#ch06.xhtml_page_216), [231](#ch06.xhtml_page_231)–232

chattr command, [65](#ch02.xhtml_page_65)

chcon command, [335](#ch08.xhtml_page_335)

chgrp command, [63](#ch02.xhtml_page_63), [65](#ch02.xhtml_page_65)

chmod command, [63](#ch02.xhtml_page_63)–64, [241](#ch06.xhtml_page_241)

running scripts, [377](#ch09.xhtml_page_377)–378

chown command, [63](#ch02.xhtml_page_63), [65](#ch02.xhtml_page_65), [241](#ch06.xhtml_page_241)

chronyc sources command, [206](#ch05.xhtml_page_206)

chronyd, [205](#ch05.xhtml_page_205)–206

chroot command

rescue mode and, [189](#ch05.xhtml_page_189)

root password recovery, [182](#ch05.xhtml_page_182)

CIDR notation. *see* Classless Inter-Domain Routing notation

CIFS, [299](#ch07.xhtml_page_299)

Citrix Hypervisor, [8](#ch01.xhtml_page_8)

Classless Inter-Domain Routing notation (CIDR), [94](#ch03.xhtml_page_94)

Cockpit web console, [215](#ch06.xhtml_page_215), [228](#ch06.xhtml_page_228)

firewall configuration and, [314](#ch08.xhtml_page_314)

command line

adding or deleting groups at, [227](#ch06.xhtml_page_227)

adding users at, [226](#ch06.xhtml_page_226)

deleting users at, [228](#ch06.xhtml_page_228)

GRUB 2, [185](#ch05.xhtml_page_185)–187

options and arguments, [51](#ch02.xhtml_page_51)

SELinux configuration at, [331](#ch08.xhtml_page_331)

user privileges, [49](#ch02.xhtml_page_49)

command-line skills, [44](#ch02.xhtml_page_44)

command-line tools, [43](#ch02.xhtml_page_43)

file and directory concepts, [52](#ch02.xhtml_page_52)–54

file creation commands, [55](#ch02.xhtml_page_55)–58

file lists, [54](#ch02.xhtml_page_54)–55

file permissions, [60](#ch02.xhtml_page_60)–68

file searches, [59](#ch02.xhtml_page_59)–60

reading text streams, [68](#ch02.xhtml_page_68)–70

ssh and scp, [116](#ch03.xhtml_page_116)–117

standard, [51](#ch02.xhtml_page_51)–59

text file editing, [73](#ch02.xhtml_page_73)–78

text stream processing, [70](#ch02.xhtml_page_70)–73

user account management, [225](#ch06.xhtml_page_225)–228

wildcards, [58](#ch02.xhtml_page_58)–59

command options, [51](#ch02.xhtml_page_51)

cd command, [79](#ch02.xhtml_page_79)

chage command, [232](#ch06.xhtml_page_232)

df command, [256](#ch07.xhtml_page_256)

diff command, [72](#ch02.xhtml_page_72)

dnf command, [144](#ch04.xhtml_page_144), [155](#ch04.xhtml_page_155)–156, [158](#ch04.xhtml_page_158)–159, [164](#ch04.xhtml_page_164)

firewall-cmd command, [320](#ch08.xhtml_page_320)

grep command, [72](#ch02.xhtml_page_72)

groupadd command, [227](#ch06.xhtml_page_227)

ip command, [98](#ch03.xhtml_page_98)–99

journalctl command, [195](#ch05.xhtml_page_195), [393](#ch09.xhtml_page_393)–394

ls command, [54](#ch02.xhtml_page_54), [79](#ch02.xhtml_page_79)

mount command, [292](#ch07.xhtml_page_292)

parted command, [266](#ch07.xhtml_page_266)–267

permissions management, [63](#ch02.xhtml_page_63)

ps command, [356](#ch09.xhtml_page_356)–357

rm command, [217](#ch06.xhtml_page_217)

rpm command, [131](#ch04.xhtml_page_131)–132, [137](#ch04.xhtml_page_137), [140](#ch04.xhtml_page_140)

systemctl command, [431](#ch10.xhtml_page_431)–432

tar command, [368](#ch09.xhtml_page_368)

traceroute command, [97](#ch03.xhtml_page_97)

UNIX or POSIX and BSD styles, [357](#ch09.xhtml_page_357)

useradd command, [227](#ch06.xhtml_page_227)

usermod command, [231](#ch06.xhtml_page_231)

wc command, [72](#ch02.xhtml_page_72)

command redirection, [49](#ch02.xhtml_page_49)

compression, [354](#ch09.xhtml_page_354), [367](#ch09.xhtml_page_367)–369

conditional constructs, [382](#ch09.xhtml_page_382)–383

configuration files, [5](#ch01.xhtml_page_5). *See also* specific files

cron, [370](#ch09.xhtml_page_370)–371

hostname, [109](#ch03.xhtml_page_109)–111

systemd, [197](#ch05.xhtml_page_197)

Containerfiles, [418](#ch10.xhtml_page_418)–419, [426](#ch10.xhtml_page_426)

container images, [406](#ch10.xhtml_page_406)–407, [411](#ch10.xhtml_page_411)

building, [418](#ch10.xhtml_page_418)–420

context of, [434](#ch10.xhtml_page_434)

registries, [416](#ch10.xhtml_page_416)–418

uploading to Quay.io, [421](#ch10.xhtml_page_421)

container registry, [411](#ch10.xhtml_page_411)–412, [414](#ch10.xhtml_page_414), [416](#ch10.xhtml_page_416)–419, [427](#ch10.xhtml_page_427)

containers, [2](#ch01.xhtml_page_2), [9](#ch01.xhtml_page_9), [405](#ch10.xhtml_page_405)

architecture, [410](#ch10.xhtml_page_410)–411

benefits, [408](#ch10.xhtml_page_408)

fundamentals, [407](#ch10.xhtml_page_407)–412

managing, [407](#ch10.xhtml_page_407), [422](#ch10.xhtml_page_422)–434

persistent storage, [434](#ch10.xhtml_page_434)–436

rootless and rootful, [415](#ch10.xhtml_page_415)

running, [413](#ch10.xhtml_page_413)–415, [432](#ch10.xhtml_page_432)–433

tool installation for, [412](#ch10.xhtml_page_412)

tradeoffs of, [410](#ch10.xhtml_page_410)

virtualization and, [409](#ch10.xhtml_page_409)–410

VMs compared with, [406](#ch10.xhtml_page_406), [408](#ch10.xhtml_page_408)

contexts, [313](#ch08.xhtml_page_313), [329](#ch08.xhtml_page_329)

creating directories with, [337](#ch08.xhtml_page_337)–338

listing and identifying file, [334](#ch08.xhtml_page_334)–335

process, [338](#ch08.xhtml_page_338)–339

restoring file, [336](#ch08.xhtml_page_336)–337

control groups (cgroups), [195](#ch05.xhtml_page_195)–196, [410](#ch10.xhtml_page_410)

control structures

in bash, [381](#ch09.xhtml_page_381)–386

for loop, [385](#ch09.xhtml_page_385)–386

test operators and conditional constructs, [382](#ch09.xhtml_page_382)–385

cp command, [56](#ch02.xhtml_page_56)

CPUs, [6](#ch01.xhtml_page_6)

crashkernel option, [184](#ch05.xhtml_page_184)

createrepo command, [162](#ch04.xhtml_page_162)

cron.allow, [376](#ch09.xhtml_page_376)

cron command, [354](#ch09.xhtml_page_354), [369](#ch09.xhtml_page_369), [374](#ch09.xhtml_page_374), [377](#ch09.xhtml_page_377)

configuration files, [370](#ch09.xhtml_page_370)–371

hourly jobs, [372](#ch09.xhtml_page_372)

securing, [375](#ch09.xhtml_page_375)–376

setting up, [373](#ch09.xhtml_page_373)

crond, [192](#ch05.xhtml_page_192)

cron.deny, [376](#ch09.xhtml_page_376)

cron logging rules, [389](#ch09.xhtml_page_389)–390

crontab command, [77](#ch02.xhtml_page_77), [371](#ch09.xhtml_page_371), [373](#ch09.xhtml_page_373), [376](#ch09.xhtml_page_376)

crontab file, [369](#ch09.xhtml_page_369)–371

cupsd, [192](#ch05.xhtml_page_192)

CUPS service, [194](#ch05.xhtml_page_194)

**D**

DAC. *See* discretionary access control

data streams, [49](#ch02.xhtml_page_49)

date and time settings, [205](#ch05.xhtml_page_205)

date command, [384](#ch09.xhtml_page_384)

default gateway, [95](#ch03.xhtml_page_95)

default zone, [317](#ch08.xhtml_page_317), [319](#ch08.xhtml_page_319)–320

DEFLATE algorithm, [367](#ch09.xhtml_page_367)

dependencies, [131](#ch04.xhtml_page_131), [141](#ch04.xhtml_page_141)

systemd, [196](#ch05.xhtml_page_196)–197

dependency hell, [142](#ch04.xhtml_page_142)–144

/dev/null, [50](#ch02.xhtml_page_50)

DevOps, [406](#ch10.xhtml_page_406)–408

devpts filesystem, [293](#ch07.xhtml_page_293)

devtmpfs filesystem, [255](#ch07.xhtml_page_255)

df command, [255](#ch07.xhtml_page_255)–257, [266](#ch07.xhtml_page_266)

DHCP. *See* Dynamic Host Configuration Protocol

DHCP servers, [102](#ch03.xhtml_page_102)

diff command, [72](#ch02.xhtml_page_72), [104](#ch03.xhtml_page_104)

Digital Signature Algorithm (DSA), [324](#ch08.xhtml_page_324)–325, [327](#ch08.xhtml_page_327)

directories

separately mountable, [281](#ch07.xhtml_page_281)

shared, [241](#ch06.xhtml_page_241)–242

directory creation and deletion, [57](#ch02.xhtml_page_57)–58

directory paths, [53](#ch02.xhtml_page_53)

disabled mode, [329](#ch08.xhtml_page_329)

discretionary access control (DAC), [311](#ch08.xhtml_page_311)

disk drives

GPT size limits, [264](#ch07.xhtml_page_264)

MBR size limits, [264](#ch07.xhtml_page_264)

partition limits, [28](#ch01.xhtml_page_28)

usage, [255](#ch07.xhtml_page_255)–257

disk management, [253](#ch07.xhtml_page_253)

disk partitions. *See* partitions

Disk Utility, [271](#ch07.xhtml_page_271)–272

dmesg command, [50](#ch02.xhtml_page_50), [190](#ch05.xhtml_page_190)

dnf clean all command, [156](#ch04.xhtml_page_156)

dnf command, [128](#ch04.xhtml_page_128)–129, [141](#ch04.xhtml_page_141)–144

basic commands, [155](#ch04.xhtml_page_155)

basic configuration, [148](#ch04.xhtml_page_148)–152

downloading packages with, [131](#ch04.xhtml_page_131)

installation mode, [155](#ch04.xhtml_page_155)–156

logs, [391](#ch09.xhtml_page_391)

package groups, [157](#ch04.xhtml_page_157)–159

repository creation, [152](#ch04.xhtml_page_152)–153

security and, [157](#ch04.xhtml_page_157)

updates and security fixes, [157](#ch04.xhtml_page_157)

updating kernel, [135](#ch04.xhtml_page_135)

dnf.conf, [148](#ch04.xhtml_page_148)

dnf config-manager command, [151](#ch04.xhtml_page_151), [160](#ch04.xhtml_page_160)–161

dnf download command, [161](#ch04.xhtml_page_161)

dnf group info command, [158](#ch04.xhtml_page_158)–159

dnf group install command, [158](#ch04.xhtml_page_158)–159

dnf group list command, [35](#ch01.xhtml_page_35), [157](#ch04.xhtml_page_157)

dnf group remove command, [159](#ch04.xhtml_page_159)

dnf info command, [155](#ch04.xhtml_page_155)

dnf install command, [155](#ch04.xhtml_page_155), [157](#ch04.xhtml_page_157)

dnf list command, [155](#ch04.xhtml_page_155)

dnf module command, [163](#ch04.xhtml_page_163)

dnf module enable command, [164](#ch04.xhtml_page_164)

dnf module install command, [164](#ch04.xhtml_page_164)

dnf provides command, [156](#ch04.xhtml_page_156)

dnf repolist command, [155](#ch04.xhtml_page_155)

dnf update command, [156](#ch04.xhtml_page_156), [162](#ch04.xhtml_page_162)–163

DNS. *See* Domain Name System

Docker, [9](#ch01.xhtml_page_9), [411](#ch10.xhtml_page_411)–412, [414](#ch10.xhtml_page_414)

docker command, [412](#ch10.xhtml_page_412)

Docker Hub, [411](#ch10.xhtml_page_411), [417](#ch10.xhtml_page_417)

documentation, [45](#ch02.xhtml_page_45)

accessing, [78](#ch02.xhtml_page_78)–82

Domain Name System (DNS), [97](#ch03.xhtml_page_97)

done keyword, [382](#ch09.xhtml_page_382)

dotCloud, [411](#ch10.xhtml_page_411)

DSA. *See* Digital Signature Algorithm

dump command, [290](#ch07.xhtml_page_290)

dumpe2fs command, [290](#ch07.xhtml_page_290)–291

Dynamic Host Configuration Protocol (DHCP), [93](#ch03.xhtml_page_93)

dynamic IP addresses, [93](#ch03.xhtml_page_93)

**E**

ECDSA. *See* Elliptic Curve DSA

echo command, [238](#ch06.xhtml_page_238), [378](#ch09.xhtml_page_378)–379

echo $PATH command, [53](#ch02.xhtml_page_53)

EDITOR environment variable, [373](#ch09.xhtml_page_373)

edquota command, [77](#ch02.xhtml_page_77)

Elliptic Curve DSA (ECDSA), [324](#ch08.xhtml_page_324)–325, [327](#ch08.xhtml_page_327)

else operator, [383](#ch09.xhtml_page_383)

emergency shell, [178](#ch05.xhtml_page_178)–179

emergency target mode, [178](#ch05.xhtml_page_178)–179

encrypted communication, [117](#ch03.xhtml_page_117), [324](#ch08.xhtml_page_324)

basic, [325](#ch08.xhtml_page_325)–327

encryption keys, [325](#ch08.xhtml_page_325)

enforcing mode, [329](#ch08.xhtml_page_329)–330, [341](#ch08.xhtml_page_341), [344](#ch08.xhtml_page_344)

env command, [369](#ch09.xhtml_page_369)

environment, [236](#ch06.xhtml_page_236)

for practice labs, [12](#ch01.xhtml_page_12)–21

environment variables, [369](#ch09.xhtml_page_369)–370

bash scripts and, [379](#ch09.xhtml_page_379)

EDITOR, [373](#ch09.xhtml_page_373)

HOME, [369](#ch09.xhtml_page_369)

LANG, [370](#ch09.xhtml_page_370)

MAIL, [370](#ch09.xhtml_page_370)

PATH, [53](#ch02.xhtml_page_53)–54, [370](#ch09.xhtml_page_370)

SHELL, [369](#ch09.xhtml_page_369), [372](#ch09.xhtml_page_372)

EPEL repository, [154](#ch04.xhtml_page_154)

ephemeral storage, [434](#ch10.xhtml_page_434)

/etc/auto.master, [296](#ch07.xhtml_page_296)–297

/etc/auto.misc, [297](#ch07.xhtml_page_297)–298

/etc/auto.net, [298](#ch07.xhtml_page_298)

/etc/auto.smb, [299](#ch07.xhtml_page_299)

/etc/bashrc, [237](#ch06.xhtml_page_237)–238

/etc/containers/registries.conf, [416](#ch10.xhtml_page_416)

/etc/crontab, [369](#ch09.xhtml_page_369)–371

/etc/default/grub, [183](#ch05.xhtml_page_183)

/etc/dnf/plugins, [148](#ch04.xhtml_page_148)

/etc/fstab, [49](#ch02.xhtml_page_49), [288](#ch07.xhtml_page_288)–289

adding filesystems to, [293](#ch07.xhtml_page_293)

fields in, [290](#ch07.xhtml_page_290)

mount command and, [291](#ch07.xhtml_page_291)–292

mount options, [292](#ch07.xhtml_page_292)

network filesystems, [294](#ch07.xhtml_page_294)–295

removable media, [293](#ch07.xhtml_page_293)–294

UUIDs in, [290](#ch07.xhtml_page_290)–291

/etc/group, [218](#ch06.xhtml_page_218), [220](#ch06.xhtml_page_220), [234](#ch06.xhtml_page_234)

/etc/grub2.cfg, [182](#ch05.xhtml_page_182)–183

/etc/gshadow, [222](#ch06.xhtml_page_222)–223

/etc/hostname, [111](#ch03.xhtml_page_111)

/etc/hosts, [110](#ch03.xhtml_page_110)

/etc/login.defs, [223](#ch06.xhtml_page_223)–225

/etc/mtab, [289](#ch07.xhtml_page_289)

/etc/nfs.conf, [295](#ch07.xhtml_page_295)

/etc/nsswitch.conf, [109](#ch03.xhtml_page_109)–110

/etc/pam.d/password-auth, [233](#ch06.xhtml_page_233)

/etc/pam.d/system-auth, [233](#ch06.xhtml_page_233)

/etc/passwd, [67](#ch02.xhtml_page_67)–68, [218](#ch06.xhtml_page_218)–220, [230](#ch06.xhtml_page_230)

/etc/profile, [238](#ch06.xhtml_page_238)

/etc/profile.d, [238](#ch06.xhtml_page_238)

/etc/resolv.conf, [110](#ch03.xhtml_page_110)–111, [389](#ch09.xhtml_page_389)–390

/etc/rsyslog.conf, [389](#ch09.xhtml_page_389)

/etc/rsyslog.d, [389](#ch09.xhtml_page_389)

/etc/security/access.conf, [232](#ch06.xhtml_page_232)–233

/etc/selinux/config, [330](#ch08.xhtml_page_330)

/etc/shadow, [220](#ch06.xhtml_page_220)–222, [230](#ch06.xhtml_page_230)

/etc/skel, [236](#ch06.xhtml_page_236)–237, [239](#ch06.xhtml_page_239)

/etc/sudoers file, [216](#ch06.xhtml_page_216), [235](#ch06.xhtml_page_235)

/etc/systemd/journald.conf, [393](#ch09.xhtml_page_393)

/etc/yum.repos.d, [149](#ch04.xhtml_page_149), [151](#ch04.xhtml_page_151)

Ethernet interfaces, [96](#ch03.xhtml_page_96)

configuring, [102](#ch03.xhtml_page_102)–103

exercises

adding user with Cockpit web console, [228](#ch06.xhtml_page_228)–229

automounter configuration, [300](#ch07.xhtml_page_300)

booting to different target, [180](#ch05.xhtml_page_180)–181

building and running container images, [420](#ch10.xhtml_page_420)

configuring IPv4 settings, [105](#ch03.xhtml_page_105)–106

creating new user with vi, [75](#ch02.xhtml_page_75)–77

creating scripts, [386](#ch09.xhtml_page_386)–388

cron jobs, [374](#ch09.xhtml_page_374)

directories with SELinux contexts, [337](#ch08.xhtml_page_337)–338

dnf repository creation, [152](#ch04.xhtml_page_152)–153

environment for, [12](#ch01.xhtml_page_12)–21

EPEL repository access configurations, [154](#ch04.xhtml_page_154)

fdisk and parted, [272](#ch07.xhtml_page_272)–274

firewall configuration with Cockpit web console, [322](#ch08.xhtml_page_322)–324

firewall settings, [320](#ch08.xhtml_page_320)–321

formatting, checking, and mounting filesystems, [278](#ch07.xhtml_page_278)–279

getting RHEL 9, [12](#ch01.xhtml_page_12)

group ownership and SGID bit, [242](#ch06.xhtml_page_242)–243

GRUB 2 command line, [186](#ch05.xhtml_page_186)–187

log files, [392](#ch09.xhtml_page_392)

partitioning during installation, [32](#ch01.xhtml_page_32)–33

persistent storage and containers, [435](#ch10.xhtml_page_435)–436

real and fake shells, [230](#ch06.xhtml_page_230)

root password recovery, [181](#ch05.xhtml_page_181)–182

rpm commands, [140](#ch04.xhtml_page_140)–141

running containers as services, [432](#ch10.xhtml_page_432)–433

securing systems, [238](#ch06.xhtml_page_238)–239

subscribing to RHSM, [145](#ch04.xhtml_page_145)–147

uploading images to Quay.io, [421](#ch10.xhtml_page_421)

exit command, [233](#ch06.xhtml_page_233), [240](#ch06.xhtml_page_240), [378](#ch09.xhtml_page_378)

export command, [379](#ch09.xhtml_page_379)

ext2/ext3/ext4 filesystems, [274](#ch07.xhtml_page_274)–276

**F**

FAT filesystem, [275](#ch07.xhtml_page_275), [277](#ch07.xhtml_page_277)

fdisk command, [79](#ch02.xhtml_page_79), [254](#ch07.xhtml_page_254)–255, [272](#ch07.xhtml_page_272)–274, [282](#ch07.xhtml_page_282)

creating swap partitions, [263](#ch07.xhtml_page_263)–264

deleting partitions, [261](#ch07.xhtml_page_261)–263

exiting, [262](#ch07.xhtml_page_262)

partition creation, [260](#ch07.xhtml_page_260)

partition types, [261](#ch07.xhtml_page_261)–262

starting and help, [257](#ch07.xhtml_page_257)–259

using on new drive with no partitions, [259](#ch07.xhtml_page_259)

Fedora Linux, [3](#ch01.xhtml_page_3), [11](#ch01.xhtml_page_11)

FHS. *See* Filesystem Hierarchy Standards

fi keyword, [382](#ch09.xhtml_page_382)–383

file and directory management, [44](#ch02.xhtml_page_44)

concepts, [52](#ch02.xhtml_page_52)–54

permissions, [60](#ch02.xhtml_page_60)

file attributes, [65](#ch02.xhtml_page_65)–66

file contexts

listing and identifying, [334](#ch08.xhtml_page_334)–335

restoring, [336](#ch08.xhtml_page_336)–337

file-creation commands, [55](#ch02.xhtml_page_55)–58

file labeling

relabeling, [332](#ch08.xhtml_page_332), [335](#ch08.xhtml_page_335)

SELinux, [182](#ch05.xhtml_page_182), [342](#ch08.xhtml_page_342)–343

file lists, [54](#ch02.xhtml_page_54)–55

file permissions, [45](#ch02.xhtml_page_45), [60](#ch02.xhtml_page_60)–68

file searches, [59](#ch02.xhtml_page_59)–60

filesystem device nodes, [279](#ch07.xhtml_page_279)

Filesystem Hierarchy Standards (FHS), [279](#ch07.xhtml_page_279)

standard directories, [280](#ch07.xhtml_page_280)–281

filesystem management, [253](#ch07.xhtml_page_253)–254

filesystems

adding to /etc/fstab, [293](#ch07.xhtml_page_293)

check commands, [278](#ch07.xhtml_page_278)

format commands, [276](#ch07.xhtml_page_276)–277

formats, [274](#ch07.xhtml_page_274)

formatting, checking, and mounting, [278](#ch07.xhtml_page_278)–279

journaling, [276](#ch07.xhtml_page_276)

linux-swap, [269](#ch07.xhtml_page_269)

managing, [288](#ch07.xhtml_page_288)–295

mount options, [292](#ch07.xhtml_page_292)

mount points, [13](#ch01.xhtml_page_13)

network, [294](#ch07.xhtml_page_294)–295

read-only mode, [179](#ch05.xhtml_page_179)

standard, [275](#ch07.xhtml_page_275)–276

temporary, [189](#ch05.xhtml_page_189)

tmpfs, [29](#ch01.xhtml_page_29)

UUIDs for, [289](#ch07.xhtml_page_289)

virtual, [275](#ch07.xhtml_page_275)

filesystem volumes, [28](#ch01.xhtml_page_28)–29

file transfer

ports for, [315](#ch08.xhtml_page_315)

scp and sftp commands for, [117](#ch03.xhtml_page_117)

secure, [92](#ch03.xhtml_page_92), [115](#ch03.xhtml_page_115)

user deletion and, [228](#ch06.xhtml_page_228)

find command, [59](#ch02.xhtml_page_59)

findmnt command, [256](#ch07.xhtml_page_256)–257

firewall-cmd tool, [312](#ch08.xhtml_page_312), [314](#ch08.xhtml_page_314), [319](#ch08.xhtml_page_319)–320

SELinux administration, [344](#ch08.xhtml_page_344)

firewall-config utility, [312](#ch08.xhtml_page_312), [314](#ch08.xhtml_page_314), [316](#ch08.xhtml_page_316)–319

firewalld, [312](#ch08.xhtml_page_312), [314](#ch08.xhtml_page_314)–315

common ports, [318](#ch08.xhtml_page_318)

custom ports, [318](#ch08.xhtml_page_318)–319

services in, [317](#ch08.xhtml_page_317)–318, [320](#ch08.xhtml_page_320)

zones, [316](#ch08.xhtml_page_316)–320

firewalls

basic control of, [313](#ch08.xhtml_page_313)–320

configuration with Cockpit web console, [322](#ch08.xhtml_page_322)–324

console configuration, [319](#ch08.xhtml_page_319)–320

GUI configuration, [316](#ch08.xhtml_page_316)–319

settings, [320](#ch08.xhtml_page_320)–321

zone-based, [315](#ch08.xhtml_page_315)–316

firmware, [7](#ch01.xhtml_page_7)–8

for loops, [385](#ch09.xhtml_page_385)–386

for operator, [381](#ch09.xhtml_page_381), [384](#ch09.xhtml_page_384)–385

Fox, Brian, [377](#ch09.xhtml_page_377)

FQDNs. *See* fully qualified domain names

fsck command, [278](#ch07.xhtml_page_278), [290](#ch07.xhtml_page_290)

full virtualization, [8](#ch01.xhtml_page_8)

fully qualified domain names (FQDNs), [92](#ch03.xhtml_page_92)

**G**

gcc compiler, [142](#ch04.xhtml_page_142)

gdisk command, [254](#ch07.xhtml_page_254)–255, [257](#ch07.xhtml_page_257), [264](#ch07.xhtml_page_264)–265, [282](#ch07.xhtml_page_282)

GDM. *See* GNOME Display Manager

gedit editor, [78](#ch02.xhtml_page_78)

General Public License (GPL), [10](#ch01.xhtml_page_10)

getenforce command, [331](#ch08.xhtml_page_331)

getent passwd command, [385](#ch09.xhtml_page_385)

getsebool command, [334](#ch08.xhtml_page_334)

GID. *See* group ID

GMT. *See* Greenwich Mean Time

GNOME Desktop Environment, [14](#ch01.xhtml_page_14)

removable media mounting, [293](#ch07.xhtml_page_293)

gnome-disks, [271](#ch07.xhtml_page_271)–272

GNOME Display Manager (GDM), [47](#ch02.xhtml_page_47)–48

GNU Privacy Guard (GPG), [134](#ch04.xhtml_page_134), [325](#ch08.xhtml_page_325)

Google Container Registry, [411](#ch10.xhtml_page_411)

GParted, [271](#ch07.xhtml_page_271)

gpasswd command, [222](#ch06.xhtml_page_222)–223, [226](#ch06.xhtml_page_226)

GPG. *See* GNU Privacy Guard

gpgcheck directive, [148](#ch04.xhtml_page_148), [151](#ch04.xhtml_page_151)–152

gpgkey directive, [152](#ch04.xhtml_page_152)

GPL. *See* General Public License

GPT. *See* GUID Partition Table

graphical.target, [200](#ch05.xhtml_page_200)–201

Greenwich Mean Time (GMT), [205](#ch05.xhtml_page_205)

grep command, [45](#ch02.xhtml_page_45), [71](#ch02.xhtml_page_71)–72

ps results, [356](#ch09.xhtml_page_356)–357

SELinux boolean settings, [334](#ch08.xhtml_page_334)

groupadd command, [216](#ch06.xhtml_page_216), [224](#ch06.xhtml_page_224), [226](#ch06.xhtml_page_226)–227

groupdel command, [227](#ch06.xhtml_page_227)

group ID (GID), [224](#ch06.xhtml_page_224)–225, [240](#ch06.xhtml_page_240)

groupmod command, [216](#ch06.xhtml_page_216), [231](#ch06.xhtml_page_231)

groups

adding or deleting at command line, [227](#ch06.xhtml_page_227)

directly adding users, [225](#ch06.xhtml_page_225)–226

permissions and, [66](#ch02.xhtml_page_66)–68

primary, [218](#ch06.xhtml_page_218)

Red Hat, [241](#ch06.xhtml_page_241)

shadow password suite and, [218](#ch06.xhtml_page_218), [220](#ch06.xhtml_page_220)

shared directories, [241](#ch06.xhtml_page_241)–242

special, [240](#ch06.xhtml_page_240)

standard, [241](#ch06.xhtml_page_241)

supplementary, [218](#ch06.xhtml_page_218)

volume, [254](#ch07.xhtml_page_254)

GRUB 2, [176](#ch05.xhtml_page_176)–177

command line, [185](#ch05.xhtml_page_185)–187

emergency shell, [178](#ch05.xhtml_page_178)–179

rescue mode, [187](#ch05.xhtml_page_187)–189

updating, [184](#ch05.xhtml_page_184)

grub2-install command, [184](#ch05.xhtml_page_184)

grub2-mkconfig tool, [182](#ch05.xhtml_page_182)–184

grub2-set-default command, [184](#ch05.xhtml_page_184)

grub.cfg file, [182](#ch05.xhtml_page_182)–183, [185](#ch05.xhtml_page_185)–186

GRUB configuration file, [136](#ch04.xhtml_page_136)

GUI, [14](#ch01.xhtml_page_14)

SELinux administration, [341](#ch08.xhtml_page_341)–344

text file editing, [78](#ch02.xhtml_page_78)

GUID Partition Table (GPT), [8](#ch01.xhtml_page_8), [28](#ch01.xhtml_page_28), [173](#ch05.xhtml_page_173), [176](#ch05.xhtml_page_176)–177, [185](#ch05.xhtml_page_185), [254](#ch07.xhtml_page_254), [257](#ch07.xhtml_page_257)

disk size limits, [264](#ch07.xhtml_page_264)

GUI shell interfaces, [47](#ch02.xhtml_page_47)

gunzip command, [367](#ch09.xhtml_page_367)

gzip command, [354](#ch09.xhtml_page_354), [367](#ch09.xhtml_page_367)–368

**H**

hard links, [56](#ch02.xhtml_page_56)

hardware

architectures, [6](#ch01.xhtml_page_6)–7

compatibility, [6](#ch01.xhtml_page_6)

networking, [8](#ch01.xhtml_page_8)

RAM requirements, [7](#ch01.xhtml_page_7)

requirements, [5](#ch01.xhtml_page_5)–9

storage options, [7](#ch01.xhtml_page_7)–8

virtual machine options, [8](#ch01.xhtml_page_8)–9

hardware virtualization, [2](#ch01.xhtml_page_2), [7](#ch01.xhtml_page_7), [409](#ch10.xhtml_page_409)

head command, [70](#ch02.xhtml_page_70)

help

accessing from command line, [79](#ch02.xhtml_page_79)

displaying man pages, [80](#ch02.xhtml_page_80)–81

fdisk, [257](#ch07.xhtml_page_257)

gdisk, [264](#ch07.xhtml_page_264)–265

GRUB 2 command line, [185](#ch05.xhtml_page_185)

kill signals, [364](#ch09.xhtml_page_364)

LVM commands, [286](#ch07.xhtml_page_286)

mount options, [292](#ch07.xhtml_page_292)

parted, [266](#ch07.xhtml_page_266)

podman commands, [423](#ch10.xhtml_page_423)

test operators, [382](#ch09.xhtml_page_382)

home directory, [236](#ch06.xhtml_page_236)

HOME environment variable, [369](#ch09.xhtml_page_369)

hosted hypervisors, [8](#ch01.xhtml_page_8)

hostnames, [92](#ch03.xhtml_page_92)

configuration files, [109](#ch03.xhtml_page_109)–111

host-only networks, [16](#ch01.xhtml_page_16)

HP-UX, [2](#ch01.xhtml_page_2)

httpd, [192](#ch05.xhtml_page_192)

hypervisors, [8](#ch01.xhtml_page_8), [13](#ch01.xhtml_page_13), [409](#ch10.xhtml_page_409)

video card emulation by, [23](#ch01.xhtml_page_23)

virtual networks on, [16](#ch01.xhtml_page_16)–18

**I**

IANA. *See* Internet Assigned Number Authority

iburst configuration option, [206](#ch05.xhtml_page_206)

id command, [217](#ch06.xhtml_page_217)–218

id_dsa, [325](#ch08.xhtml_page_325)

id_dsa.pub, [325](#ch08.xhtml_page_325)

id_ecdsa, [325](#ch08.xhtml_page_325)

id_ecdsa.pub, [325](#ch08.xhtml_page_325)

id_rsa, [325](#ch08.xhtml_page_325)

id_rsa.pub, [324](#ch08.xhtml_page_324)–325

ifconfig command, [95](#ch03.xhtml_page_95)–96

if operator, [381](#ch09.xhtml_page_381), [383](#ch09.xhtml_page_383), [385](#ch09.xhtml_page_385)

image registries, [416](#ch10.xhtml_page_416)–418

info manuals, [81](#ch02.xhtml_page_81)–82

init daemon, [194](#ch05.xhtml_page_194)

initial RAM disk, [189](#ch05.xhtml_page_189)–190

installation, [3](#ch01.xhtml_page_3)

installing RHEL 9

baseline packages, [34](#ch01.xhtml_page_34)–35

basic steps, [24](#ch01.xhtml_page_24)–27

boot media, [22](#ch01.xhtml_page_22)–23

initial setup, [36](#ch01.xhtml_page_36)–37

Installation Destination screen, [27](#ch01.xhtml_page_27)

Installation Summary screen, [24](#ch01.xhtml_page_24)–25

Manual Partitioning screen, [30](#ch01.xhtml_page_30)–33

Network & Host Name configuration screen, [25](#ch01.xhtml_page_25)–26

package installation, [35](#ch01.xhtml_page_35)–36

partition creation during, [30](#ch01.xhtml_page_30)–34

partitions from perspective of, [27](#ch01.xhtml_page_27)–29

Software Selection screen, [34](#ch01.xhtml_page_34)–35

interface identifier, [112](#ch03.xhtml_page_112)

Internet Assigned Number Authority (IANA), [314](#ch08.xhtml_page_314)

Internet Engineering Task Force, [93](#ch03.xhtml_page_93)

iostat command, [356](#ch09.xhtml_page_356), [361](#ch09.xhtml_page_361)–362

IP address, [93](#ch03.xhtml_page_93), [95](#ch03.xhtml_page_95), [99](#ch03.xhtml_page_99)

IPv6, [111](#ch03.xhtml_page_111)–113

ping command, [97](#ch03.xhtml_page_97)

ip address show command, [98](#ch03.xhtml_page_98)

ip commands, [95](#ch03.xhtml_page_95), [115](#ch03.xhtml_page_115)

activating and deactivating network adapters, [99](#ch03.xhtml_page_99)

configuring network adapters, [98](#ch03.xhtml_page_98)

as diagnostic tool, [99](#ch03.xhtml_page_99)

options, [99](#ch03.xhtml_page_99)

reviewing network adapters, [98](#ch03.xhtml_page_98)

ip link show command, [98](#ch03.xhtml_page_98)

ip neigh command, [99](#ch03.xhtml_page_99)

ip route command, [95](#ch03.xhtml_page_95), [100](#ch03.xhtml_page_100)

iptables, [314](#ch08.xhtml_page_314)

IPv4, [92](#ch03.xhtml_page_92)

configuring settings, [105](#ch03.xhtml_page_105)–106

networks, [93](#ch03.xhtml_page_93)–94

IPv6, [92](#ch03.xhtml_page_92)

addressing, [111](#ch03.xhtml_page_111)–113

configuring addresses, [114](#ch03.xhtml_page_114)–115

troubleshooting tools, [113](#ch03.xhtml_page_113)

ISO 9660 filesystem, [275](#ch07.xhtml_page_275)

**J**

journalctl command, [190](#ch05.xhtml_page_190), [195](#ch05.xhtml_page_195), [392](#ch09.xhtml_page_392)–394

journaling filesystems, [276](#ch07.xhtml_page_276)

**K**

Katello, [145](#ch04.xhtml_page_145)

kdump, [184](#ch05.xhtml_page_184)

Kerberos

ports for, [315](#ch08.xhtml_page_315)

time drift and, [204](#ch05.xhtml_page_204)

kernel

initial RAM disk, [190](#ch05.xhtml_page_190)

passing parameters to, [178](#ch05.xhtml_page_178)

updating, [134](#ch04.xhtml_page_134)–136

key-based authentication, [312](#ch08.xhtml_page_312), [324](#ch08.xhtml_page_324)

client configuration files for, [325](#ch08.xhtml_page_325)

keys for, [326](#ch08.xhtml_page_326)–327

killall command, [356](#ch09.xhtml_page_356), [363](#ch09.xhtml_page_363)–364

kill command, [356](#ch09.xhtml_page_356)–357, [363](#ch09.xhtml_page_363)–364

Knoppix, [188](#ch05.xhtml_page_188)

known_hosts, [325](#ch08.xhtml_page_325)

ksh, [46](#ch02.xhtml_page_46)

Kubernetes, [9](#ch01.xhtml_page_9)

KVM, [9](#ch01.xhtml_page_9), [13](#ch01.xhtml_page_13)

**L**

lab environment, [2](#ch01.xhtml_page_2), [12](#ch01.xhtml_page_12)–21

LANG environment variable, [370](#ch09.xhtml_page_370)

lastlog command, [391](#ch09.xhtml_page_391)

LE. *See* logical extent

less command, [50](#ch02.xhtml_page_50), [69](#ch02.xhtml_page_69)–70

linux directive, [178](#ch05.xhtml_page_178)

linux-swap filesystem, [269](#ch07.xhtml_page_269)

Live DVDs, [188](#ch05.xhtml_page_188)

ln command, [56](#ch02.xhtml_page_56)–57

load balancing, [314](#ch08.xhtml_page_314)

locate command, [60](#ch02.xhtml_page_60), [62](#ch02.xhtml_page_62)

log files, [355](#ch09.xhtml_page_355), [388](#ch09.xhtml_page_388)–394

logging

file management, [390](#ch09.xhtml_page_390)

levels, [389](#ch09.xhtml_page_389)–390, [393](#ch09.xhtml_page_393)

service-specific logs, [392](#ch09.xhtml_page_392)

storage and, [393](#ch09.xhtml_page_393)

systemd, [195](#ch05.xhtml_page_195)

logical extent (LE), [282](#ch07.xhtml_page_282)

logical volume (LV), [282](#ch07.xhtml_page_282)

creating, [283](#ch07.xhtml_page_283)–284

removing, [287](#ch07.xhtml_page_287)

resizing, [287](#ch07.xhtml_page_287)–288

using, [284](#ch07.xhtml_page_284)

UUIDs for, [290](#ch07.xhtml_page_290)–291

Logical Volume Manager (LVM), [254](#ch07.xhtml_page_254)

definitions in, [282](#ch07.xhtml_page_282)–283

logical volume commands, [286](#ch07.xhtml_page_286)

physical volume commands, [284](#ch07.xhtml_page_284)

volume group commands, [285](#ch07.xhtml_page_285)

logical volumes, [29](#ch01.xhtml_page_29)

managing, [254](#ch07.xhtml_page_254)

login, [239](#ch06.xhtml_page_239)–240

login screens, [199](#ch05.xhtml_page_199)–200

login shell, [233](#ch06.xhtml_page_233)

LOGNAME environment variable, [369](#ch09.xhtml_page_369)

logout, [239](#ch06.xhtml_page_239)–240

logrotate command, [373](#ch09.xhtml_page_373), [390](#ch09.xhtml_page_390)

lsattr command, [65](#ch02.xhtml_page_65)–66

ls command, [50](#ch02.xhtml_page_50)–52, [54](#ch02.xhtml_page_54)–55

permissions and, [61](#ch02.xhtml_page_61)–62, [66](#ch02.xhtml_page_66)

ls -Z command, [329](#ch08.xhtml_page_329), [334](#ch08.xhtml_page_334)–335

LV. *See* logical volume

lvcreate command, [283](#ch07.xhtml_page_283)

lvextend command, [80](#ch02.xhtml_page_80), [283](#ch07.xhtml_page_283), [287](#ch07.xhtml_page_287)–288

LVM. *See* Logical Volume Manager

lvmconfig command, [287](#ch07.xhtml_page_287)

lvm partition type, [270](#ch07.xhtml_page_270)

lvremove command, [287](#ch07.xhtml_page_287)

**M**

MAC. *See* mandatory access control

MAC address, [99](#ch03.xhtml_page_99)

mailboxes, [224](#ch06.xhtml_page_224)

MAIL environment variable, [370](#ch09.xhtml_page_370)

mail logging rules, [389](#ch09.xhtml_page_389)–390

man command, [69](#ch02.xhtml_page_69), [80](#ch02.xhtml_page_80)–81

mandatory access control (MAC), [311](#ch08.xhtml_page_311), [410](#ch10.xhtml_page_410)

man mount command, [292](#ch07.xhtml_page_292)

mask command, [204](#ch05.xhtml_page_204)

Master Boot Record (MBR), [28](#ch01.xhtml_page_28), [173](#ch05.xhtml_page_173), [176](#ch05.xhtml_page_176)–177, [185](#ch05.xhtml_page_185)

disk size limits, [264](#ch07.xhtml_page_264)

partitions, [257](#ch07.xhtml_page_257), [259](#ch07.xhtml_page_259), [264](#ch07.xhtml_page_264)

mdkir command, [241](#ch06.xhtml_page_241)

microservices, [408](#ch10.xhtml_page_408)

Microsoft Active Directory, [224](#ch06.xhtml_page_224)

Microsoft Windows 11, [8](#ch01.xhtml_page_8)

mkdir command, [57](#ch02.xhtml_page_57)–58

mkfs command, [276](#ch07.xhtml_page_276)

mkfs.ext3 command, [276](#ch07.xhtml_page_276)–277

mkfs.ext4 command, [276](#ch07.xhtml_page_276)–277

mkfs.fat command, [277](#ch07.xhtml_page_277)

mkfs.xfs command, [269](#ch07.xhtml_page_269), [276](#ch07.xhtml_page_276)–277

mklabel command, [267](#ch07.xhtml_page_267)

mkpart command, [267](#ch07.xhtml_page_267)

mkswap command, [269](#ch07.xhtml_page_269), [277](#ch07.xhtml_page_277)

MLS. *See* Multi-Level Security

mls mode, [330](#ch08.xhtml_page_330)

module streams, [162](#ch04.xhtml_page_162)

getting information about, [163](#ch04.xhtml_page_163)–164

installing and removing, [164](#ch04.xhtml_page_164)–165

more command, [69](#ch02.xhtml_page_69)

mount command, [131](#ch04.xhtml_page_131), [255](#ch07.xhtml_page_255)–256, [288](#ch07.xhtml_page_288), [291](#ch07.xhtml_page_291)–292

network filesystems and, [294](#ch07.xhtml_page_294)–295

removable media and, [294](#ch07.xhtml_page_294)

mount points

adding, [30](#ch01.xhtml_page_30)–31

for virtual machines, [13](#ch01.xhtml_page_13)

Multi-Level Security (MLS), [330](#ch08.xhtml_page_330), [333](#ch08.xhtml_page_333)

mv command, [56](#ch02.xhtml_page_56)

**N**

name resolution, [92](#ch03.xhtml_page_92)

configuring, [109](#ch03.xhtml_page_109)

nameserver directive, [110](#ch03.xhtml_page_110)–111

namespaces, [410](#ch10.xhtml_page_410)

naming conventions

network interfaces, [96](#ch03.xhtml_page_96)

for partitions, [27](#ch01.xhtml_page_27)–28

nano editor, [77](#ch02.xhtml_page_77)–78

NAT. *See* network address translation

National Security Agency (NSA), [311](#ch08.xhtml_page_311)

NAutoVTs, [47](#ch02.xhtml_page_47)

Netfliter, [314](#ch08.xhtml_page_314)

netmask, [94](#ch03.xhtml_page_94)

netstat command, [95](#ch03.xhtml_page_95)–96, [100](#ch03.xhtml_page_100)

network adapters

activating and deactivating, [99](#ch03.xhtml_page_99)

configuring, [98](#ch03.xhtml_page_98)

reviewing, [98](#ch03.xhtml_page_98)

network address translation (NAT), [16](#ch01.xhtml_page_16)–18, [314](#ch08.xhtml_page_314)

network configuration, [92](#ch03.xhtml_page_92)

services, [101](#ch03.xhtml_page_101)–103

tools, [103](#ch03.xhtml_page_103)–109

network connections

diagnosing, [99](#ch03.xhtml_page_99)

displaying, [100](#ch03.xhtml_page_100)–101

hypervisors and, [16](#ch01.xhtml_page_16)

network filesystems, [294](#ch07.xhtml_page_294)–295

networking, [8](#ch01.xhtml_page_8), [93](#ch03.xhtml_page_93)

configuration and troubleshooting, [101](#ch03.xhtml_page_101)–111

configuration directives, [105](#ch03.xhtml_page_105)

configuration services, [101](#ch03.xhtml_page_101)–103

configuration tools, [103](#ch03.xhtml_page_103)–109

hostname configuration files, [109](#ch03.xhtml_page_109)–111

interface names, [96](#ch03.xhtml_page_96)

name resolution configuration, [109](#ch03.xhtml_page_109)

restarting, [102](#ch03.xhtml_page_102)

tools and commands, [95](#ch03.xhtml_page_95)–101

Network Manager, [101](#ch03.xhtml_page_101)–103, [114](#ch03.xhtml_page_114)

Network Manager Connection Editor, [107](#ch03.xhtml_page_107)–109

Network Time Protocol (NTP), [173](#ch05.xhtml_page_173)–174, [204](#ch05.xhtml_page_204), [206](#ch05.xhtml_page_206)

next operator, [50](#ch02.xhtml_page_50)

NFS servers, [294](#ch07.xhtml_page_294)–296, [298](#ch07.xhtml_page_298)

automounter and, [296](#ch07.xhtml_page_296)

Nftables, [314](#ch08.xhtml_page_314)

nice command, [355](#ch09.xhtml_page_355), [362](#ch09.xhtml_page_362)–363

nmcli command, [98](#ch03.xhtml_page_98), [101](#ch03.xhtml_page_101)–104, [114](#ch03.xhtml_page_114)

nm-connection-editor command, [103](#ch03.xhtml_page_103), [107](#ch03.xhtml_page_107)–109, [114](#ch03.xhtml_page_114)

nmtui command, [104](#ch03.xhtml_page_104)

Non-Volatile Memory Express (NVMe), [7](#ch01.xhtml_page_7), [258](#ch07.xhtml_page_258)

NSA. *See* National Security Agency

nslcd daemon, [394](#ch09.xhtml_page_394)

NTP. *See* Network Time Protocol

ntpd, [205](#ch05.xhtml_page_205)

NVMe. *See* Non-Volatile Memory Express

**O**

Open Container Initiative (OCI), [411](#ch10.xhtml_page_411)

OpenLDAP, [224](#ch06.xhtml_page_224)

OpenShift, [9](#ch01.xhtml_page_9)

Open Trusted Computing (OpenTC), [176](#ch05.xhtml_page_176)

ownership, [60](#ch02.xhtml_page_60)–62

commands to change, [63](#ch02.xhtml_page_63)–66

**P**

package groups, [157](#ch04.xhtml_page_157)–159

packages

baseline, [35](#ch01.xhtml_page_35)

conflict management, [130](#ch04.xhtml_page_130)

defining, [129](#ch04.xhtml_page_129)

dependencies, [131](#ch04.xhtml_page_131)

downgrading, [132](#ch04.xhtml_page_132)

file verification, [138](#ch04.xhtml_page_138)–140

installation in new system, [35](#ch01.xhtml_page_35)–36

installing, [131](#ch04.xhtml_page_131)–132

installing from remote systems, [133](#ch04.xhtml_page_133)

queries, [137](#ch04.xhtml_page_137)

repositories, [130](#ch04.xhtml_page_130)–131

signatures, [137](#ch04.xhtml_page_137)–138

uninstalling, [133](#ch04.xhtml_page_133)

packet classification, [314](#ch08.xhtml_page_314)

packet filtering, [314](#ch08.xhtml_page_314)

packets, [314](#ch08.xhtml_page_314)

paravirtualization, [8](#ch01.xhtml_page_8)

parted command, [254](#ch07.xhtml_page_254)–255, [257](#ch07.xhtml_page_257), [265](#ch07.xhtml_page_265), [272](#ch07.xhtml_page_272)–274, [282](#ch07.xhtml_page_282)

changing partition types, [269](#ch07.xhtml_page_269)–270

creating partitions, [267](#ch07.xhtml_page_267)–268

creating swap partitions, [269](#ch07.xhtml_page_269)

deleting partitions, [268](#ch07.xhtml_page_268)

graphical front ends for, [271](#ch07.xhtml_page_271)

on new disk with no partitions, [267](#ch07.xhtml_page_267)

starting, help, and quitting, [266](#ch07.xhtml_page_266)

using, [267](#ch07.xhtml_page_267)–270

partitions, [259](#ch07.xhtml_page_259)

changing type, [269](#ch07.xhtml_page_269)–270

configuring mount points, [30](#ch01.xhtml_page_30)–31

creating with fdisk, [260](#ch07.xhtml_page_260)

creating with parted, [267](#ch07.xhtml_page_267)–268

creation during installation, [30](#ch01.xhtml_page_30)–34

deleting with fdisk, [261](#ch07.xhtml_page_261)–263

deleting with parted, [268](#ch07.xhtml_page_268)

filesystem volumes, [28](#ch01.xhtml_page_28)–29

graphical front ends for managing, [271](#ch07.xhtml_page_271)–272

during install, [32](#ch01.xhtml_page_32)–33

installation perspective on, [27](#ch01.xhtml_page_27)–29

logical volumes from, [29](#ch01.xhtml_page_29)

managing, [254](#ch07.xhtml_page_254)

naming conventions for, [28](#ch01.xhtml_page_28)

swap space, [29](#ch01.xhtml_page_29), [263](#ch07.xhtml_page_263)–264, [269](#ch07.xhtml_page_269)

types, [261](#ch07.xhtml_page_261)–262

UUIDs for, [289](#ch07.xhtml_page_289)

partprobe command, [260](#ch07.xhtml_page_260)

passwd command, [62](#ch02.xhtml_page_62), [77](#ch02.xhtml_page_77), [226](#ch06.xhtml_page_226)

passwords

assigning, [226](#ch06.xhtml_page_226)

emergency shell and root, [179](#ch05.xhtml_page_179)

recovering root, [181](#ch05.xhtml_page_181)–182

shadow suite, [218](#ch06.xhtml_page_218)–225

PATH environment variable, [53](#ch02.xhtml_page_53)–54, [370](#ch09.xhtml_page_370)

pathmunge function, [238](#ch06.xhtml_page_238)

PE. *See* physical extent

permissions, [45](#ch02.xhtml_page_45)

commands to change, [63](#ch02.xhtml_page_63)–66

permissive mode, [313](#ch08.xhtml_page_313), [329](#ch08.xhtml_page_329), [331](#ch08.xhtml_page_331)

persistent storage

containers, [434](#ch10.xhtml_page_434)–436

log files, [393](#ch09.xhtml_page_393)

PGP. *See* Pretty Good Privacy

pgrep command, [356](#ch09.xhtml_page_356)

physical extent (PE), [282](#ch07.xhtml_page_282)

physical volume (PV), [282](#ch07.xhtml_page_282)

creating, [283](#ch07.xhtml_page_283)

pinfo command, [81](#ch02.xhtml_page_81)

ping6 command, [113](#ch03.xhtml_page_113)

ping command, [96](#ch03.xhtml_page_96)–97, [334](#ch08.xhtml_page_334)

pipelines, [44](#ch02.xhtml_page_44), [50](#ch02.xhtml_page_50)

Podman, [9](#ch01.xhtml_page_9), [406](#ch10.xhtml_page_406), [411](#ch10.xhtml_page_411)–412, [414](#ch10.xhtml_page_414)

commands, [422](#ch10.xhtml_page_422)–440

persistent storage and, [434](#ch10.xhtml_page_434)

podman attach command, [429](#ch10.xhtml_page_429)–430

podman build command, [419](#ch10.xhtml_page_419), [426](#ch10.xhtml_page_426)–427

podman command, [407](#ch10.xhtml_page_407), [412](#ch10.xhtml_page_412)–413

container inspection commands, [425](#ch10.xhtml_page_425)–426

container management commands, [423](#ch10.xhtml_page_423)–424

image inspection commands, [428](#ch10.xhtml_page_428)–429

image management commands, [426](#ch10.xhtml_page_426)–427

miscellaneous commands, [429](#ch10.xhtml_page_429)–430

podman cp command, [429](#ch10.xhtml_page_429)–430

podman create command, [423](#ch10.xhtml_page_423)–424

podman exec command, [429](#ch10.xhtml_page_429)–430

podman generate command, [430](#ch10.xhtml_page_430)–431

podman generate systemd command, [430](#ch10.xhtml_page_430)–431

podman images command, [414](#ch10.xhtml_page_414), [416](#ch10.xhtml_page_416), [428](#ch10.xhtml_page_428)

podman info command, [416](#ch10.xhtml_page_416), [429](#ch10.xhtml_page_429)–430

podman inspect command, [425](#ch10.xhtml_page_425), [428](#ch10.xhtml_page_428)

podman logs command, [425](#ch10.xhtml_page_425)–426

podman ps command, [414](#ch10.xhtml_page_414)–415, [425](#ch10.xhtml_page_425)

podman pull command, [427](#ch10.xhtml_page_427)

podman push command, [427](#ch10.xhtml_page_427)

podman rm command, [415](#ch10.xhtml_page_415), [424](#ch10.xhtml_page_424)

podman rmi command, [427](#ch10.xhtml_page_427)

podman run command, [414](#ch10.xhtml_page_414), [419](#ch10.xhtml_page_419), [423](#ch10.xhtml_page_423)–424, [429](#ch10.xhtml_page_429), [434](#ch10.xhtml_page_434)

podman search command, [417](#ch10.xhtml_page_417), [428](#ch10.xhtml_page_428)–429

podman start command, [423](#ch10.xhtml_page_423)–424

podman stop command, [424](#ch10.xhtml_page_424)

podman tag command, [427](#ch10.xhtml_page_427)

podman version command, [429](#ch10.xhtml_page_429)–430

policy violations, [313](#ch08.xhtml_page_313)

diagnosing and addressing, [339](#ch08.xhtml_page_339)–340

port labels, [313](#ch08.xhtml_page_313), [338](#ch08.xhtml_page_338)

ports

common, [318](#ch08.xhtml_page_318)

custom, [318](#ch08.xhtml_page_318)–319

firewalld services and, [317](#ch08.xhtml_page_317), [319](#ch08.xhtml_page_319)

SELinux administration, [344](#ch08.xhtml_page_344)

standard, [314](#ch08.xhtml_page_314)–315

positional parameters, [380](#ch09.xhtml_page_380), [386](#ch09.xhtml_page_386)

POSIX signals, [364](#ch09.xhtml_page_364)

POST. *See* Power On Self Test

Postfix, [203](#ch05.xhtml_page_203)–204

poweroff command, [117](#ch03.xhtml_page_117)

Power On Self Test (POST), [175](#ch05.xhtml_page_175)

PPID, [357](#ch09.xhtml_page_357)

practice labs, environment for, [12](#ch01.xhtml_page_12)–21

Pretty Good Privacy (PGP), [134](#ch04.xhtml_page_134)

primary group, [218](#ch06.xhtml_page_218)

private keys, [326](#ch08.xhtml_page_326)

private/public key pairs, [324](#ch08.xhtml_page_324)–325

setting up, [327](#ch08.xhtml_page_327)–328

process contexts, [338](#ch08.xhtml_page_338)–339

PROCESSES directives, [235](#ch06.xhtml_page_235)

process groups, [410](#ch10.xhtml_page_410)

process IDs (PIDs), [410](#ch10.xhtml_page_410)

process management

commands for, [355](#ch09.xhtml_page_355)

ps command, [356](#ch09.xhtml_page_356)–359

process priorities, [362](#ch09.xhtml_page_362)–363

proc filesystem, [293](#ch07.xhtml_page_293)

protocols. *See also* specific protocols

firewalld services and, [317](#ch08.xhtml_page_317)

ps aux command, [356](#ch09.xhtml_page_356)–358, [360](#ch09.xhtml_page_360)

ps axl command, [357](#ch09.xhtml_page_357)–358

ps command, [338](#ch08.xhtml_page_338), [355](#ch09.xhtml_page_355), [360](#ch09.xhtml_page_360)

process management with, [356](#ch09.xhtml_page_356)–359

usernames, [356](#ch09.xhtml_page_356)

ps -eZ command, [338](#ch08.xhtml_page_338)–339

pstree command, [357](#ch09.xhtml_page_357)

ps -Z command, [359](#ch09.xhtml_page_359)

public keys, [325](#ch08.xhtml_page_325)–327

PV. *See* physical volume

pvcreate command, [282](#ch07.xhtml_page_282)–283

pwd command, [52](#ch02.xhtml_page_52)

**Q**

QtParted, [271](#ch07.xhtml_page_271)

Quay.io, [411](#ch10.xhtml_page_411), [419](#ch10.xhtml_page_419), [421](#ch10.xhtml_page_421), [427](#ch10.xhtml_page_427)

quiet directive, [190](#ch05.xhtml_page_190)

**R**

raid partition type, [270](#ch07.xhtml_page_270)

RAM

allocating for VMs, [14](#ch01.xhtml_page_14)

RHEL 9 requirements, [7](#ch01.xhtml_page_7)

swap space assignment and, [29](#ch01.xhtml_page_29)

RANDOM_DELAY directive, [372](#ch09.xhtml_page_372)–373

rd.break boot option, [179](#ch05.xhtml_page_179)

rd.lvm.lv option, [184](#ch05.xhtml_page_184)

read-only mode, [179](#ch05.xhtml_page_179)

real-time processes, [362](#ch09.xhtml_page_362)

reboot, systemctl command for, [174](#ch05.xhtml_page_174), [178](#ch05.xhtml_page_178), [193](#ch05.xhtml_page_193)

Red Hat Certification Technician (RHCT), [4](#ch01.xhtml_page_4)

Red Hat Certified System Administrator (RHCSA) exam, [1](#ch01.xhtml_page_1)

basic hardware requirements, [5](#ch01.xhtml_page_5)–9

overview of, [4](#ch01.xhtml_page_4)–5

Red Hat Customer Portal, [9](#ch01.xhtml_page_9)–11, [22](#ch01.xhtml_page_22) repositories, [130](#ch04.xhtml_page_130)–131

Red Hat Enterprise Linux 9 (RHEL 9), [2](#ch01.xhtml_page_2)

architectures, [6](#ch01.xhtml_page_6)–7

bootloaders, [177](#ch05.xhtml_page_177), [182](#ch05.xhtml_page_182)–184

boot media for, [22](#ch01.xhtml_page_22)–23

control by target, [200](#ch05.xhtml_page_200)–204

default groups, [241](#ch06.xhtml_page_241)

filesystems, [274](#ch07.xhtml_page_274)–276

getting, [9](#ch01.xhtml_page_9)–12

GPT support in fdisk, [257](#ch07.xhtml_page_257)

graphical disk management tools, [271](#ch07.xhtml_page_271)–272

hardware compatibility, [6](#ch01.xhtml_page_6)

installation, [22](#ch01.xhtml_page_22)–37

KVM hypervisor, [9](#ch01.xhtml_page_9)

practice lab environment with, [13](#ch01.xhtml_page_13)

RAM requirements, [7](#ch01.xhtml_page_7)

root user default aliases, [58](#ch02.xhtml_page_58)

shells in, [46](#ch02.xhtml_page_46)

software packages on install DVD, [34](#ch01.xhtml_page_34)–35

standard log files, [391](#ch09.xhtml_page_391)

subscriptions, [10](#ch01.xhtml_page_10)

third-party rebuilds, [10](#ch01.xhtml_page_10)

UUIDs for partitions, [289](#ch07.xhtml_page_289)

virtual consoles and login screens, [199](#ch05.xhtml_page_199)–200

VM configuration for, [18](#ch01.xhtml_page_18)–21

Red Hat groups, [241](#ch06.xhtml_page_241)

redhat.repo configuration file, [149](#ch04.xhtml_page_149)–151

Red Hat Satellite Servers, [144](#ch04.xhtml_page_144)–145, [149](#ch04.xhtml_page_149), [162](#ch04.xhtml_page_162)

Red Hat Subscription Management (RHSM), [11](#ch01.xhtml_page_11), [128](#ch04.xhtml_page_128), [142](#ch04.xhtml_page_142), [144](#ch04.xhtml_page_144)–145

plugins, [149](#ch04.xhtml_page_149)

redirection, [44](#ch02.xhtml_page_44)

command, [49](#ch02.xhtml_page_49)

operators, [50](#ch02.xhtml_page_50)–51

standard streams and, [49](#ch02.xhtml_page_49)–50

regular expressions, [45](#ch02.xhtml_page_45)

special characters in, [71](#ch02.xhtml_page_71)

remote systems

accessing, [92](#ch03.xhtml_page_92)

package installation from, [133](#ch04.xhtml_page_133)

removable media

/etc/fstab, [293](#ch07.xhtml_page_293)–294

mount command and, [294](#ch07.xhtml_page_294)

renice command, [355](#ch09.xhtml_page_355), [362](#ch09.xhtml_page_362)–363

repositories, [130](#ch04.xhtml_page_130)–131

creating, [162](#ch04.xhtml_page_162)

dnf configuration, [149](#ch04.xhtml_page_149)–152

third-party, [154](#ch04.xhtml_page_154)

rescue mode

boot media, [188](#ch05.xhtml_page_188)

chroot command, [189](#ch05.xhtml_page_189)

GRUB 2, [187](#ch05.xhtml_page_187)–189

resource management, [354](#ch09.xhtml_page_354)

system commands for, [355](#ch09.xhtml_page_355)–364

restorecon command, [335](#ch08.xhtml_page_335)–337, [344](#ch08.xhtml_page_344), [368](#ch09.xhtml_page_368)

RFC 791, [93](#ch03.xhtml_page_93)

RFC 1517, [93](#ch03.xhtml_page_93)

RHCSA. *See* Red Hat Certified System Administrator exam

RHCT. *See* Red Hat Certification Technician

RHEL 9\. *See* Red Hat Enterprise Linux 9

rhgb quiet directive, [184](#ch05.xhtml_page_184)

RHSM. *See* Red Hat Subscription Management

Rivest, Shamir, Adelman (RSA), [324](#ch08.xhtml_page_324)–325, [327](#ch08.xhtml_page_327)

rm command, [57](#ch02.xhtml_page_57), [217](#ch06.xhtml_page_217)

rmdir command, [57](#ch02.xhtml_page_57)–58

rootful containers, [415](#ch10.xhtml_page_415)

rootless containers, [415](#ch10.xhtml_page_415)

root password

creating, [35](#ch01.xhtml_page_35)

emergency shell and, [179](#ch05.xhtml_page_179)

recovering, [181](#ch05.xhtml_page_181)–182

root user, [3](#ch01.xhtml_page_3)

default aliases, [58](#ch02.xhtml_page_58)

route command, [95](#ch03.xhtml_page_95), [100](#ch03.xhtml_page_100)

router, [95](#ch03.xhtml_page_95)

routing tables, [100](#ch03.xhtml_page_100)

rpm command, [128](#ch04.xhtml_page_128)–129, [142](#ch04.xhtml_page_142)–143

dependencies, [131](#ch04.xhtml_page_131)

file verification, [138](#ch04.xhtml_page_138)–140

installation security, [134](#ch04.xhtml_page_134)

installing from remote systems, [133](#ch04.xhtml_page_133)

installing packages, [131](#ch04.xhtml_page_131)–132

package queries, [137](#ch04.xhtml_page_137)

package signatures, [137](#ch04.xhtml_page_137)–138

updating kernel, [134](#ch04.xhtml_page_134)–136

RPM database, [130](#ch04.xhtml_page_130)

RPM Package Manager, [129](#ch04.xhtml_page_129)–136

conflict management, [130](#ch04.xhtml_page_130)

installing packages, [131](#ch04.xhtml_page_131)–132

RSA. *See* Rivest, Shamir, Adelman

rsyslog service, [196](#ch05.xhtml_page_196), [388](#ch09.xhtml_page_388)–389

runlevels, [192](#ch05.xhtml_page_192)

/run/log/journal, [388](#ch09.xhtml_page_388), [393](#ch09.xhtml_page_393)

run-parts command, [372](#ch09.xhtml_page_372)

**S**

sa1 command, [361](#ch09.xhtml_page_361)

sa2 command, [361](#ch09.xhtml_page_361)

Samba file server, [192](#ch05.xhtml_page_192), [294](#ch07.xhtml_page_294)–295, [299](#ch07.xhtml_page_299)

log files, [389](#ch09.xhtml_page_389)

SAN. *See* storage area network

sar command, [356](#ch09.xhtml_page_356), [360](#ch09.xhtml_page_360)–361

SAS. *See* Serial Attached SCSI

SATA. *See* Serial Advanced Technology Attachment

scalability, [2](#ch01.xhtml_page_2)

scheduling tasks, [354](#ch09.xhtml_page_354)

scp command, [115](#ch03.xhtml_page_115)–119, [324](#ch08.xhtml_page_324)

scripts

creating, [386](#ch09.xhtml_page_386)–388

running, [377](#ch09.xhtml_page_377)–378

SCTP. *See* Stream Control Transmission Protocol

SD cards. *See* Secure Digital cards

sealert command, [340](#ch08.xhtml_page_340), [344](#ch08.xhtml_page_344)

search directive, [110](#ch03.xhtml_page_110)

Secure Digital cards (SD cards), [296](#ch07.xhtml_page_296)

Secure Shell (SSH), [92](#ch03.xhtml_page_92), [312](#ch08.xhtml_page_312)

administration with, [115](#ch03.xhtml_page_115)–119

client configuration files, [325](#ch08.xhtml_page_325)

configuration commands, [324](#ch08.xhtml_page_324)

graphical access, [117](#ch03.xhtml_page_117)–118

key-based authentication, [324](#ch08.xhtml_page_324)–328

key pair generation, [327](#ch08.xhtml_page_327)–328

ports for, [315](#ch08.xhtml_page_315)

SELinux administration, [344](#ch08.xhtml_page_344)

security, [238](#ch06.xhtml_page_238)–239

dnf and, [157](#ch04.xhtml_page_157)

layers of, [330](#ch08.xhtml_page_330)

sed command, [73](#ch02.xhtml_page_73)

SELinux, [311](#ch08.xhtml_page_311)–313

alerts, [340](#ch08.xhtml_page_340)

audits, [339](#ch08.xhtml_page_339)–340

basic features, [329](#ch08.xhtml_page_329)

basic settings, [331](#ch08.xhtml_page_331)–332

boolean settings, [313](#ch08.xhtml_page_313), [331](#ch08.xhtml_page_331), [334](#ch08.xhtml_page_334), [340](#ch08.xhtml_page_340), [342](#ch08.xhtml_page_342)–343

command line configuration, [331](#ch08.xhtml_page_331)

containers, [410](#ch10.xhtml_page_410)

contexts, [313](#ch08.xhtml_page_313), [337](#ch08.xhtml_page_337)–338

disabled mode, [329](#ch08.xhtml_page_329)

enforcing mode, [329](#ch08.xhtml_page_329)–330, [341](#ch08.xhtml_page_341)

file labeling, [342](#ch08.xhtml_page_342)–343

GUI administration tool, [341](#ch08.xhtml_page_341)–344

identifying process contexts, [338](#ch08.xhtml_page_338)–339

installing configuration GUI, [131](#ch04.xhtml_page_131)

listing and identifying file contexts, [334](#ch08.xhtml_page_334)–335

log files, [389](#ch09.xhtml_page_389)

mls mode, [330](#ch08.xhtml_page_330)

network ports, [344](#ch08.xhtml_page_344)

permissive mode, [313](#ch08.xhtml_page_313), [329](#ch08.xhtml_page_329), [331](#ch08.xhtml_page_331)

policy violations, [313](#ch08.xhtml_page_313), [339](#ch08.xhtml_page_339)–340

port labels, [313](#ch08.xhtml_page_313), [338](#ch08.xhtml_page_338)

ps command switch, [359](#ch09.xhtml_page_359)

regular user configuration, [332](#ch08.xhtml_page_332)–333

restoring file contexts, [336](#ch08.xhtml_page_336)–337

standard directives, [330](#ch08.xhtml_page_330)

star command and, [368](#ch09.xhtml_page_368)–369

status, [329](#ch08.xhtml_page_329)–330

systemd journal messages, [190](#ch05.xhtml_page_190)

tar command and, [368](#ch09.xhtml_page_368)

targeted mode, [330](#ch08.xhtml_page_330)

user role options, [333](#ch08.xhtml_page_333)

selinuxuser_ping boolean setting, [334](#ch08.xhtml_page_334)

semanage boolean command, [334](#ch08.xhtml_page_334)

semanage command, port labels, [338](#ch08.xhtml_page_338)

semanage fcontext command, [335](#ch08.xhtml_page_335)–337

semanage login command, [332](#ch08.xhtml_page_332)–333

Serial Advanced Technology Attachment (SATA), [7](#ch01.xhtml_page_7)

Serial Attached SCSI (SAS), [7](#ch01.xhtml_page_7)

service configuration, [203](#ch05.xhtml_page_203)–204

service management, control by target for, [200](#ch05.xhtml_page_200)–204

services

in firewalld, [317](#ch08.xhtml_page_317)–318, [320](#ch08.xhtml_page_320)

system accounts, [217](#ch06.xhtml_page_217)

service-specific logs, [392](#ch09.xhtml_page_392)

service units, [191](#ch05.xhtml_page_191), [197](#ch05.xhtml_page_197)

session keys, [325](#ch08.xhtml_page_325)

sestatus command, [331](#ch08.xhtml_page_331), [341](#ch08.xhtml_page_341)

setenforce command, [344](#ch08.xhtml_page_344)

set group ID (SGID), [60](#ch02.xhtml_page_60)–62, [241](#ch06.xhtml_page_241)

setsebool command, [334](#ch08.xhtml_page_334), [344](#ch08.xhtml_page_344)

set-timezone command, [205](#ch05.xhtml_page_205)

set user ID (SUID), [60](#ch02.xhtml_page_60)–62

sftp command, [116](#ch03.xhtml_page_116)–117, [324](#ch08.xhtml_page_324)

sg command, [234](#ch06.xhtml_page_234)

SGID. *See* set group ID

SGID bit. *See* set group ID

sha256sum command, [11](#ch01.xhtml_page_11)

shadow password suite, [218](#ch06.xhtml_page_218)–225

shared directories, [241](#ch06.xhtml_page_241)–242

shebang, [377](#ch09.xhtml_page_377)

SHELL environment variable, [369](#ch09.xhtml_page_369), [372](#ch09.xhtml_page_372)

shells, [44](#ch02.xhtml_page_44), [46](#ch02.xhtml_page_46), [230](#ch06.xhtml_page_230)

configuration files in user home directories, [239](#ch06.xhtml_page_239)

GUI interfaces, [47](#ch02.xhtml_page_47)

wildcards, [58](#ch02.xhtml_page_58)–59

shell scripting, [377](#ch09.xhtml_page_377)–386

shut down, [193](#ch05.xhtml_page_193)

SIGKILL signal, [364](#ch09.xhtml_page_364)

SIGTERM signal, [363](#ch09.xhtml_page_363)–364

Skopeo, [412](#ch10.xhtml_page_412)

skopeo command, [407](#ch10.xhtml_page_407)

skopeo inspect command, [417](#ch10.xhtml_page_417)–418, [428](#ch10.xhtml_page_428)

smbd, [192](#ch05.xhtml_page_192)

smbpasswd command, [81](#ch02.xhtml_page_81)

soft links, [57](#ch02.xhtml_page_57)

Solaris, [2](#ch01.xhtml_page_2)

solid-state drives (SSDs), [258](#ch07.xhtml_page_258)

sort command, [71](#ch02.xhtml_page_71)

Spacewalk, [145](#ch04.xhtml_page_145), [149](#ch04.xhtml_page_149)

special groups, [240](#ch06.xhtml_page_240)

special parameters, [380](#ch09.xhtml_page_380)

ss command, [100](#ch03.xhtml_page_100)–101

SSDs. *See* solid-state drives

SSH. *See* Secure Shell

ssh-add, [324](#ch08.xhtml_page_324)

ssh-agent, [324](#ch08.xhtml_page_324)

ssh command, [115](#ch03.xhtml_page_115)–119, [324](#ch08.xhtml_page_324), [328](#ch08.xhtml_page_328)

ssh-copy-id, [324](#ch08.xhtml_page_324), [328](#ch08.xhtml_page_328)

SSH daemon, [173](#ch05.xhtml_page_173)

ssh-keygen, [324](#ch08.xhtml_page_324)

standard groups, [241](#ch06.xhtml_page_241)

standard input, [49](#ch02.xhtml_page_49)–50

standard output, [50](#ch02.xhtml_page_50)

standard ports, [314](#ch08.xhtml_page_314)–315

standard streams, [49](#ch02.xhtml_page_49)

star command, [354](#ch09.xhtml_page_354), [368](#ch09.xhtml_page_368)–369

startup menus, [176](#ch05.xhtml_page_176)

static IP addresses, [93](#ch03.xhtml_page_93)

stderr, [49](#ch02.xhtml_page_49)

stdin, [49](#ch02.xhtml_page_49)

stdout, [49](#ch02.xhtml_page_49)

sticky permission bits, [60](#ch02.xhtml_page_60)–62

storage, [7](#ch01.xhtml_page_7)–8

current system state, [255](#ch07.xhtml_page_255)–257

logs, [393](#ch09.xhtml_page_393)

units of measurement, [256](#ch07.xhtml_page_256)

storage area network (SAN), [8](#ch01.xhtml_page_8)

Stream Control Transmission Protocol (SCTP), [314](#ch08.xhtml_page_314)

subnet mask, [94](#ch03.xhtml_page_94)

subnets, [93](#ch03.xhtml_page_93)

su command, [216](#ch06.xhtml_page_216), [232](#ch06.xhtml_page_232)–233

limiting access to, [234](#ch06.xhtml_page_234)

SELinux and, [333](#ch08.xhtml_page_333)

sudo command, [232](#ch06.xhtml_page_232)–236

SELinux and, [333](#ch08.xhtml_page_333), [340](#ch08.xhtml_page_340)

SUID. *See* set user ID

su -l command, [233](#ch06.xhtml_page_233)

supplementary groups, [218](#ch06.xhtml_page_218)

swapon command, [269](#ch07.xhtml_page_269), [277](#ch07.xhtml_page_277)

swap partitions

creating with fdisk, [263](#ch07.xhtml_page_263)–264

creating with parted, [269](#ch07.xhtml_page_269)

swap space, [13](#ch01.xhtml_page_13)

partitions for, [29](#ch01.xhtml_page_29), [263](#ch07.xhtml_page_263)–264, [269](#ch07.xhtml_page_269)

swap volumes, [277](#ch07.xhtml_page_277)

sysctl command, [365](#ch09.xhtml_page_365)

sysfs filesystem, [256](#ch07.xhtml_page_256), [289](#ch07.xhtml_page_289), [293](#ch07.xhtml_page_293)

system accounts

SELinux and, [329](#ch08.xhtml_page_329)

services, [217](#ch06.xhtml_page_217)

system activity reports, [360](#ch09.xhtml_page_360)–361

system administration, [354](#ch09.xhtml_page_354)

system-config-selinux command, [341](#ch08.xhtml_page_341)

systemctl, [430](#ch10.xhtml_page_430)

service configuration, [203](#ch05.xhtml_page_203)–204

systemctl disable command, [203](#ch05.xhtml_page_203)–204

systemctl enable command, [204](#ch05.xhtml_page_204)

systemctl get-default command, [192](#ch05.xhtml_page_192)–193, [200](#ch05.xhtml_page_200)

systemctl isolate multi-user.target command, [201](#ch05.xhtml_page_201)

systemctl list-dependencies command, [192](#ch05.xhtml_page_192), [196](#ch05.xhtml_page_196)

systemctl list-unit-files command, [203](#ch05.xhtml_page_203)–204

systemctl list-units command, [197](#ch05.xhtml_page_197), [199](#ch05.xhtml_page_199)

systemctl poweroff command, [174](#ch05.xhtml_page_174), [193](#ch05.xhtml_page_193)

systemctl reboot command, [174](#ch05.xhtml_page_174), [178](#ch05.xhtml_page_178), [193](#ch05.xhtml_page_193)

systemctl set-default command, [193](#ch05.xhtml_page_193)

systemctl start command, [204](#ch05.xhtml_page_204)

systemctl status command, [202](#ch05.xhtml_page_202)

systemctl stop command, [204](#ch05.xhtml_page_204)

systemd, [173](#ch05.xhtml_page_173), [179](#ch05.xhtml_page_179), [190](#ch05.xhtml_page_190), [194](#ch05.xhtml_page_194)

configuration files, [197](#ch05.xhtml_page_197)

control groups, [195](#ch05.xhtml_page_195)–196

dependencies, [196](#ch05.xhtml_page_196)–197

logging, [195](#ch05.xhtml_page_195)

targets and units, [191](#ch05.xhtml_page_191)–193

units, [197](#ch05.xhtml_page_197)–199, [201](#ch05.xhtml_page_201)–203

viewing journal log entries, [392](#ch09.xhtml_page_392)–394

systemd-analyze blame command, [194](#ch05.xhtml_page_194)

systemd-analyze time command, [194](#ch05.xhtml_page_194)

systemd-cgls command, [196](#ch05.xhtml_page_196)

systemd-journald daemon, [388](#ch09.xhtml_page_388), [393](#ch09.xhtml_page_393)

system log configuration file, [389](#ch09.xhtml_page_389)–390

system roles, [14](#ch01.xhtml_page_14)

system tuning, [354](#ch09.xhtml_page_354)

profiles for, [365](#ch09.xhtml_page_365)–367

SysVinit, [194](#ch05.xhtml_page_194)–196

**T**

tail command, [70](#ch02.xhtml_page_70)

tarballs, [70](#ch02.xhtml_page_70)

tar command, [128](#ch04.xhtml_page_128), [354](#ch09.xhtml_page_354), [368](#ch09.xhtml_page_368)

targeted mode, [330](#ch08.xhtml_page_330)

targets, [191](#ch05.xhtml_page_191)–192, [197](#ch05.xhtml_page_197)

control by, [200](#ch05.xhtml_page_200)–204

functionality by, [200](#ch05.xhtml_page_200)–201

switching, [193](#ch05.xhtml_page_193)

TCP. *See* Transmission Control Protocol

TCP/IP, [93](#ch03.xhtml_page_93)

common ports, [318](#ch08.xhtml_page_318)

standard ports, [314](#ch08.xhtml_page_314)–315

tools for, [95](#ch03.xhtml_page_95)

tcsh, [46](#ch02.xhtml_page_46)

Telnet, [315](#ch08.xhtml_page_315), [324](#ch08.xhtml_page_324)

temporary filesystems, [189](#ch05.xhtml_page_189)

terminals, [47](#ch02.xhtml_page_47)–48

test operators, [381](#ch09.xhtml_page_381)–384

test systems, roles for, [14](#ch01.xhtml_page_14)

text completion, [51](#ch02.xhtml_page_51)

text editors, [45](#ch02.xhtml_page_45)

text files, managing, [68](#ch02.xhtml_page_68)–75

text output, analysis of, [45](#ch02.xhtml_page_45)

then operator, [383](#ch09.xhtml_page_383)

third-party rebuilds, [10](#ch01.xhtml_page_10)–11

timedatectl utility, [205](#ch05.xhtml_page_205)

time service, [174](#ch05.xhtml_page_174)

time synchronization, [204](#ch05.xhtml_page_204)–206

time zone configuration, [205](#ch05.xhtml_page_205)

tmpfs filesystem, [29](#ch01.xhtml_page_29), [255](#ch07.xhtml_page_255), [289](#ch07.xhtml_page_289), [293](#ch07.xhtml_page_293)

top command, [355](#ch09.xhtml_page_355)–356, [359](#ch09.xhtml_page_359)–360, [363](#ch09.xhtml_page_363)

touch command, [55](#ch02.xhtml_page_55)

TPM. *See* Trusted Platform Module

tracepath6 command, [113](#ch03.xhtml_page_113)

tracepath command, [96](#ch03.xhtml_page_96)

traceroute command, [96](#ch03.xhtml_page_96)–97, [334](#ch08.xhtml_page_334)

Transmission Control Protocol (TCP), standard ports, [314](#ch08.xhtml_page_314)–315

Trusted Platform Module (TPM), [176](#ch05.xhtml_page_176)

tuned, [365](#ch09.xhtml_page_365)–367

tuned-adm command, [365](#ch09.xhtml_page_365)–367

tuned-adm profile command, [365](#ch09.xhtml_page_365)

**U**

UBI. *See* Universal Base Image

ubi9 image, [424](#ch10.xhtml_page_424), [428](#ch10.xhtml_page_428)

Ubuntu, [2](#ch01.xhtml_page_2), [188](#ch05.xhtml_page_188)

UDP. *See* User Datagram Protocol

UEFI. *See* Unified Extensible Firmware Interface

ugo concept, [45](#ch02.xhtml_page_45)

UID. *See* user ID

umask command, [60](#ch02.xhtml_page_60), [67](#ch02.xhtml_page_67)–68

bashrc values, [237](#ch06.xhtml_page_237)

umount command, [291](#ch07.xhtml_page_291)

Unified Extensible Firmware Interface (UEFI), [7](#ch01.xhtml_page_7)–8, [173](#ch05.xhtml_page_173), [175](#ch05.xhtml_page_175)–176

partitions, [257](#ch07.xhtml_page_257)

units, [173](#ch05.xhtml_page_173), [179](#ch05.xhtml_page_179), [191](#ch05.xhtml_page_191)–192

controlling, [201](#ch05.xhtml_page_201)–203

systemd, [197](#ch05.xhtml_page_197)–199

Universal Base Image (UBI), [424](#ch10.xhtml_page_424)

universally unique ID (UUID), [254](#ch07.xhtml_page_254)

in /etc/fstab, [290](#ch07.xhtml_page_290)–291

for LVs, [290](#ch07.xhtml_page_290)–291

for non-LVM filesystems, [289](#ch07.xhtml_page_289)

Unix, [2](#ch01.xhtml_page_2)

up2date command, [144](#ch04.xhtml_page_144)

USB keys, mounting, [294](#ch07.xhtml_page_294)

user account management, [216](#ch06.xhtml_page_216)

command-line tools, [225](#ch06.xhtml_page_225)–228

modifying accounts, [230](#ch06.xhtml_page_230)–232

useradd command, [54](#ch02.xhtml_page_54), [216](#ch06.xhtml_page_216)–217, [224](#ch06.xhtml_page_224), [226](#ch06.xhtml_page_226)–227, [231](#ch06.xhtml_page_231)

home directory creation, [236](#ch06.xhtml_page_236)

user administration, [215](#ch06.xhtml_page_215)

User Datagram Protocol (UDP), standard ports, [314](#ch08.xhtml_page_314)–315

userdel command, [228](#ch06.xhtml_page_228)

user ID (UID), [68](#ch02.xhtml_page_68), [224](#ch06.xhtml_page_224)–225

usermod command, [216](#ch06.xhtml_page_216), [230](#ch06.xhtml_page_230)–231

su access control, [234](#ch06.xhtml_page_234)

user private group scheme, [225](#ch06.xhtml_page_225)

users

ability to log in, [232](#ch06.xhtml_page_232)–233

adding at command line, [226](#ch06.xhtml_page_226)

adding with Cockpit web console, [228](#ch06.xhtml_page_228)–229

administrative, [49](#ch02.xhtml_page_49)

assigning passwords, [226](#ch06.xhtml_page_226)

creating with vi, [75](#ch02.xhtml_page_75)–77

deleting, [228](#ch06.xhtml_page_228)

directly adding, [225](#ch06.xhtml_page_225)

kinds of, [217](#ch06.xhtml_page_217)–218

permissions and, [66](#ch02.xhtml_page_66)–68

regular, [49](#ch02.xhtml_page_49)

SELinux configuration for regular, [332](#ch08.xhtml_page_332)–333

user switching, [239](#ch06.xhtml_page_239)–240

/usr/share/doc, [81](#ch02.xhtml_page_81)–82

UTC time, [205](#ch05.xhtml_page_205)

utmpdump btmp command, [391](#ch09.xhtml_page_391)

utmpdump command, [391](#ch09.xhtml_page_391)

UUID. *See* universally unique ID

**V**

variables. *See also* environment variables

in bash, [378](#ch09.xhtml_page_378)–379

/var/log/journal, [393](#ch09.xhtml_page_393)

VG. *See* volume groups

vgcreate command, [283](#ch07.xhtml_page_283)–284

vgdisplay command, [284](#ch07.xhtml_page_284)

vgextend command, [283](#ch07.xhtml_page_283), [287](#ch07.xhtml_page_287)

vi editor, [5](#ch01.xhtml_page_5), [73](#ch02.xhtml_page_73)

alternatives to, [77](#ch02.xhtml_page_77)–78

basic text editing, [74](#ch02.xhtml_page_74)–75

command mode, [74](#ch02.xhtml_page_74)

commands, [75](#ch02.xhtml_page_75)

new user creation with, [75](#ch02.xhtml_page_75)–77

w! command, [63](#ch02.xhtml_page_63)

vigr command, [77](#ch02.xhtml_page_77), [226](#ch06.xhtml_page_226)

Vim editor, [73](#ch02.xhtml_page_73)

vimtutor command, [74](#ch02.xhtml_page_74)

vipw command, [75](#ch02.xhtml_page_75), [225](#ch06.xhtml_page_225)

VirtualBox, [8](#ch01.xhtml_page_8), [13](#ch01.xhtml_page_13)

virtual consoles, [47](#ch02.xhtml_page_47), [199](#ch05.xhtml_page_199)–200

virtual filesystems, [275](#ch07.xhtml_page_275), [289](#ch07.xhtml_page_289), [293](#ch07.xhtml_page_293)

virtualization, [3](#ch01.xhtml_page_3), [7](#ch01.xhtml_page_7), [13](#ch01.xhtml_page_13)

containers and, [409](#ch10.xhtml_page_409)–410

hardware, [409](#ch10.xhtml_page_409)

virtual machine monitors, [409](#ch10.xhtml_page_409)

virtual machines (VMs), [2](#ch01.xhtml_page_2)

configuring, [18](#ch01.xhtml_page_18)–21

containers compared with, [406](#ch10.xhtml_page_406), [408](#ch10.xhtml_page_408)

filesystem mount points, [13](#ch01.xhtml_page_13)

options for, [8](#ch01.xhtml_page_8)–9

RAM allocation for, [14](#ch01.xhtml_page_14)

tradeoffs of, [410](#ch10.xhtml_page_410)

virtual networks, on hypervisors, [16](#ch01.xhtml_page_16)–18

visudo command, [235](#ch06.xhtml_page_235)

VM-level virtualization, [8](#ch01.xhtml_page_8)

VMs. *See* virtual machines

VMware ESXi, [8](#ch01.xhtml_page_8)

VMware Player, [8](#ch01.xhtml_page_8)

VMware Workstation Player, [13](#ch01.xhtml_page_13)

getting, [14](#ch01.xhtml_page_14)–15

installation program modes and, [23](#ch01.xhtml_page_23)

virtual networks, [16](#ch01.xhtml_page_16)–18

VM configuration, [18](#ch01.xhtml_page_18)–21

volume groups (VG), [254](#ch07.xhtml_page_254), [282](#ch07.xhtml_page_282)

configuring, [286](#ch07.xhtml_page_286)

creating, [283](#ch07.xhtml_page_283)

volumes, [255](#ch07.xhtml_page_255)

filesystem formats, [274](#ch07.xhtml_page_274)–278

swap, [277](#ch07.xhtml_page_277)

vsftpd, [359](#ch09.xhtml_page_359)

**W**

WantedBy directive, [202](#ch05.xhtml_page_202)

wc command, [72](#ch02.xhtml_page_72)

w! command, [63](#ch02.xhtml_page_63)

whatis command, [80](#ch02.xhtml_page_80)–81

wheel group, [216](#ch06.xhtml_page_216), [234](#ch06.xhtml_page_234)

wildcards, [58](#ch02.xhtml_page_58)–59

Wine, [8](#ch01.xhtml_page_8)

write permissions, [60](#ch02.xhtml_page_60)–62

loophole in, [63](#ch02.xhtml_page_63)

**X**

Xen, [9](#ch01.xhtml_page_9)

xfs_admin command, [290](#ch07.xhtml_page_290)–291

XFS filesystem, [274](#ch07.xhtml_page_274)–277

check order, [290](#ch07.xhtml_page_290)

repairing, [278](#ch07.xhtml_page_278)

xfs_frowfs command, [288](#ch07.xhtml_page_288)

xfs_repair command, [278](#ch07.xhtml_page_278)

**Y**

yum command, [129](#ch04.xhtml_page_129), [142](#ch04.xhtml_page_142)–144, [161](#ch04.xhtml_page_161)

**Z**

zless, [69](#ch02.xhtml_page_69)

zone-based firewalls, [315](#ch08.xhtml_page_315)–316

zones

adding, [318](#ch08.xhtml_page_318)

default, [317](#ch08.xhtml_page_317), [319](#ch08.xhtml_page_319)–320

zsh, [46](#ch02.xhtml_page_46), [237](#ch06.xhtml_page_237)