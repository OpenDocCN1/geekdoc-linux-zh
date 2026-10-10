
# Linux and Unix Security Portable Reference

A Must-Have Resource for Critical Security Information

- Learn how hackers break into Linux and Unix systems
- Secure your systems against the most sophisticated hackers
- Get concise coverage of Linux and Unix security tools and best practices
- Guard against advanced intrusion tactics such as buffer overflow attacks, port redirection, network sniffing, and more

**Nitesh Dhanjani**

# HackNotes

## Linux and Unix Security Portable Reference

> “A virtual arms cache at your fingertips. **HackNotes Linux and Unix Security Portable Reference** is a valuable reference for busy administrators and consultants who value the condensed and practical insight to understanding the threats they face and how to practically utilize tools to test the security of their environments.”
>
> —**Patrick Heim**, Vice President Enterprise Security, McKesson Corporation

**HackNotes Linux and Unix Security Portable Reference** is a valuable practical guide to protecting Linux and Unix systems from attack. Many books give general (and often vague) advice, whereas this book's style provides very precise descriptions of attacks and how to protect against them.

—**Mikhail J. Atallah**, Professor of Computer Science, Purdue University, CERIAS

> “A clear concise guide to security problems faced by sysadmins today. Every sysadmin should be familiar with the material covered in **HackNotes Linux and Unix Security Portable Reference**. For every vulnerability presented, the author provides common-sense guidelines for securing your network. Emphasis on real world examples reinforces just how serious today’s threat is.”
>
> —**Snax**, The Smhoo Group, Maintainer of AirSnort

# HackNotes™

## Linux and Unix Security Portable Reference

**NITESH DHANJANI**

McGraw-Hill/Osborne

New York Chicago San Francisco
Lisbon London Madrid Mexico City Milan
New Delhi San Juan Seoul Singapore Sydney Toronto

McGraw-Hill/Osborne
2100 Powell Street, 10th Floor
Emeryville, California 94608
U.S.A.

To arrange bulk purchase discounts for sales promotions, premiums, or fund-raisers, please contact McGraw-Hill/Osborne at the above address. For information on translations or book distributors outside the U.S.A., please see the International Contact Information page immediately following the index of this book.

# HackNotes™ Linux and Unix Security Portable Reference

Copyright © 2003 by The McGraw-Hill Companies. All rights reserved. Printed in the United States of America. Except as permitted under the Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of publisher, with the exception that the program listings may be entered, stored, and executed in a computer system, but they may not be reproduced for publication.

234567890 DOC DOC 019876543

ISBN 0-07-222786-9

**Publisher**
Brandon A. Nordin
*Vice President & Associate Publisher*
Scott Rogers
*Executive Editor*
Jane Brownlow
*Senior Project Editor*
Betsy Manini
*Executive Project Editor*
Mark Karimndy
*Acquisitions Coordinator*
Athana Honore
*Technical Editor*
Robert Clugston
*Series Editor*
Mike Horton
*Copy Editor*
Robert Campbell

**Proofreader**
Stefany Otis

**Indexer**
Valerie Perry

**Composition**
Carie Abrew
Lucie Erickson

**Illustrators**
Melinda Moore Lytle
Kathleen Fay Edwards
Lyssa Wald

**Cover Series Design**
Dodie Shoemaker

**Series Design**
Dick Schwartz
Peter F. Hanick

This book was published with Corel Ventura™ Publisher.

Information has been obtained by McGraw-Hill/Osborne and the author from sources believed to be reliable. However, because of the possibility of human or mechanical error by our sources, McGraw-Hill/Osborne, the author, or others, McGraw-Hill/Osborne and the author do not guarantee the accuracy, adequacy, or completeness of any information and is not responsible for any errors or omissions or the results obtained from use of such information.

![](img/77287f6ef97ef0bed6e23f6610950d06_4_0.png)

To my father.
To my mother.
And, to my grandmother.

## About the Author

### Nitesh Dhanjani

Nitesh Dhanjani is an information security consultant for Foundstone, Inc. While at Foundstone, Nites has been involved in many types of projects for various Fortune 500 firms, including network, application, host penetration, and security assessments, as well as security architecture design services. Nitesh is a contributing author to HackNotes: Network Security Portable Reference (McGraw-Hill/Osborne, 2003) and to the latest edition of the best-selling security book Hacking Exposed: Network Security Secrets and Solutions (McGraw-Hill/Osborne, 2003). He has also has published articles for numerous technical publications such as the Linux Journal. In addition to authoring, Nitesh has both contributed to and taught Foundstone’s “Ultimate Hacking: Expert” and “Ultimate Hacking” security courses.

Prior to joining Foundstone, Nitesh worked as a consultant with the information security services division of Ernst & Young LLP, where he performed attack and penetration reviews for many significant companies in the IT arena. He also developed proprietary network scanning tools for use within Ernst & Young LLP’s eSecurity Solutions department.

Nitesh graduated from Purdue University with both a bachelor’s and a master’s degree in Computer Science. At Purdue, he was involved in numerous research projects with the CERIAS team (Center for Education and Research Information Assurance and Security). He was also responsible for creating content for and teaching C and C++ programming courses to be delivered remotely as part of a project sponsored by IBM, AT&T, and Intel.

Nitesh continues to be actively involved in open source projects, systems programming, and Linux kernel development. He can be reached at books@dhanjani.com.

## About the Technical Reviewer

### Robert Clugston

Robert Clugston is an information technology security consultant for Foundstone. He has over six years of experience in systems administration, network security, and web production engineering. Robert initially joined Foundstone to design and secure Foundstone’s Web site and is now focused on delivering those services to Foundstone’s clients. Prior to joining Foundstone, Robert worked as a systems administrator for an Internet service provider. His responsibilities included deploying, maintaining, and securing business-critical systems to include web servers, routers, DNS servers, mail servers, and additional Internet delivery devices/systems. Prior to joining Foundstone, Robert also worked briefly as an independent contractor specializing in Perl/PHP web development. Robert holds an MSCE in Windows NT.

# CONTENTS

- Acknowledgments
- Introduction

# Reference Center

- Common Commands
- Common Ports
- IP Addressing
- Dotted Decimal Notation
- Classes
- Subnet Masks
- CIDR (Classless Inter-Domain Routing)
- Loopback
- Private Addresses
- Protocol Headers
- Online Resources
- Hacking Tools
- Web Resources
- Mailing Lists
- Conferences and Events
- Useful Netcat Commands
- ASCII Table
- HTTP Codes
- Important Files

# Part I

# Hacking Techniques and Defenses

- Fingerprinting
- Search Engines
- Domain Registrars
- Regional Internet Registries
- DNS Reverse-Lookups

- Mail Exchange
- Zone Transfers
- Traceroute
- Summary

# 2 Scanning and Identification

- Pinging
- Ping Sweeping
- TCP Pinging
- Port Scanning
- TCP Connect
- TCP SYN/Half-Open
- FIN
- Reverse Ident
- XMAS
- NULL
- RPC
- IP Protocol
- ACK
- Window
- UDP
- Fingerprinting
- Summary

# 3 Enumeration

- Enumerate Remote Services
- FTP (File Transfer Protocol): 21 (TCP)
- SSH (Secure Shell): 22 (TCP)
- Telnet: 23 (TCP)
- SMTP (Simple Mail Transfer Protocol): 25 (TCP)
- DNS (Domain Name System): 53 (TCP/UDP)
- Finger: 79 (TCP)
- HTTP (Hypertext Transfer Protocol): 80 (TCP)
- POP3 (Post Office Protocol 3): 110 (TCP)
- Portmapper: 111 (TCP)
- NNTP (Network News Transfer Protocol): 119 (TCP)
- Samba: 137 to 139 (TCP and UDP)
- IMAP2/IMAP4 (Internet Message Access Protocol 2/4): 143 (TCP)
- SNMP (Simple Network Management Protocol): 161, 162 (UDP)
