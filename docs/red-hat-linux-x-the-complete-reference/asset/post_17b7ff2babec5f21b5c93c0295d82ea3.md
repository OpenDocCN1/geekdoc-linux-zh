
![](img/32a48d8db4c23e6e2eb70d1e5034c976_0_0.png)

## Red Hat: The Complete Reference
Enterprise Linux & Fedora Edition:
The Complete Reference

by Richard L. Petersen

ISBN:0-07-223075-4

McGraw-Hill © 2004 (797 pages)

Use this comprehensive guide to maximize the powerful capabilities of Red Hat Enterprise and Fedora Linux. Coverage includes Bluecurve, KDE, GNOME, deploying and managing servers and users, the 2.6 kernel, system and network security, and more.

## Back Cover

Maximize the powerful capabilities of Red Hat Enterprise and Fedora Linux using this comprehensive and up-to-date reference. You'll get full details on everything from installation and configuration to system administration and server management of Enterprise Linux-with specifics on the Linux Kernel 2.6. Thorough security coverage includes GPG, IPSec, SSH, Kerberos, and firewalls. Learn to deploy and manage Web proxy, mail, and print server, and administer users, software, and file systems.

- Install, manage, secure, and administer Enterprise Linux 3.0 and Fedora
- Master Bluecurve, KDE, GNOME, office and multimedia applications, the shell, file systems, and Internet clients
- Deploy and manage servers-vsftpd and ProFTP (FTP), Apache (Web), Sendmail and Postfix (mail), Squid (proxy), CUPS (print), and HTDig (search), SAMBA and NFS (file), NIS, and BIND (DNS), and DHCP
- Master the complete suite of Red Hat system and network administration tools
- Manage users, services, journaling file systems, RAID devices, LVM volumes, and printers
- Reconfigure the 2.6 kernel and its modules
- Ensure system and network security using packet filtering, authentication, digital signatures, VPNs, IPSEC, and encryption
- Deploy powerful desktop, office, database, graphic, editing, and Internet applications

## About the Author

Richard Petersen, MLIS, teaches UNIX and C/C++ courses at the University of California at Berkeley. He is the author of Linux: The Complete Reference (all four editions), Linux Programming: A Beginner's Guide, and many other titles.

## Red Hat - The Complete Reference Enterprise Linux & Fedora Edition

Richard Petersen

McGraw-Hill/Osborne
2100 Powell Street, 10th Floor
Emeryville, California 94608
U.S.A.

To arrange bulk purchase discounts for sales promotions, premiums, or fund-raisers, please contact McGraw-Hill/Osborne at the above address. For information on translations or book distributors outside the U.S.A., please see the International Contact Information page immediately following the index of this book.

Copyright © 2004 by The McGraw-Hill Companies. All rights reserved. Printed in the United States of America. Except as permitted under the Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of the publisher, with the exception that the program listings may be entered, stored, and executed in a computer system, but they may not be reproduced for publication.

1234567890 DOC DOC 019876543

Book p/n 0-07-223076-2 and DVD p/n 0-07-223077-0
parts of
ISBN 0-07-223075-4

**Publisher**
Brandon A. Nordin

**Vice President & Associate Publisher**
Scott Rogers

**Editorial Director**
Tracy Dunkelberger

**Project Editor**
Carolyn Welch

**Acquisitions Coordinator**
Jessica Wilson

**Technical Editor**
Dean Henrichsmeyer

**Technical Reviewer**
Ibrahim Haddad

**Copy Editor**
Bob Campbell

**Proofreaders**
Claire Splan, Mike McGee

**Indexer**
Claire Splan

**Composition**
George Toma Charbak, Jim Kussow, Kelly Stanton-Scott

## Illustrators

- Kathleen Fay Edwards,
- Melinda Moore Lytle

## Series Design

Peter F. Hancik, Lyssa Wald

This book was composed with Corel VENTURA™ Publisher.

Information has been obtained by McGraw-Hill/Osborne from sources believed to be reliable. However, because of the possibility of human or mechanical error by our sources, McGraw-Hill/Osborne does not guarantee the accuracy, adequacy, or completeness of any information and is not responsible for any errors or omissions or the results obtained from use of such information.

## To my sisters-in-law, Marylou and Valerie

## About the Author

Richard Petersen holds a M.L.I.S. in Library and Information Studies. He currently teaches Unix and C/C++ courses at the University of California, Berkeley.

## About the Technical Reviewer

Ibrahim Haddad is a Researcher at the Open System Lab (Ericsson Corporate Unit of Research), located in Montreal, Canada. He is involved with the system architecture of third-generation wireless IP networks and represents Ericsson on the Technical Board of the Open Source Development Labs, the Carrier Grade Linux Working Group. His other commitments include serving as Contributing Editor to the Linux Journal and LinuxWorld magazine as well as contributing articles to the O'Reilly Network and Linux User & Developer magazine. He has delivered a number of presentations and tutorials at local universities, IEEE and ACM conferences, Open Source forums, and international conferences. Ibrahim contributed to Richard Petersen's book Red Hat Linux Pocket Administrator, published by McGraw-Hill/Osborne. He received his bachelor and master degrees in Computer Science from the Lebanese American University. He is currently a Dr. Sc. Candidate at Concordia University in Montreal. Academic awards include the "J. W. McConnell Memorial Graduate Fellowship" and the "Concordia University 25th Anniversary Fellowship," both received in 2000.

## About the Technical Editor

Dean Henrichsmeyer has been using Linux since 1995. He has a B.S. in Computer Science and has been an active member of the Linux community, presenting at Linux focused tradeshows such as LinuxWorld Conference and Expo. He's worked for VA Research (now known as VA Software) since 1999. He currently is working for OSDN, the Open Source Development Network, where, among other things, he is the site director for Linux.com.

## Acknowledgments

I would like to thank all those at McGraw-Hill/Osborne, who made this book a reality: Tracy Dunkelberger, Editorial Director, for her continued encouragement and analysis as well as management of such a complex project; Dean Henrichsmeyer and Ibrahim Haddad, technical editor and technical reviewer, whose analysis and suggestions proved very insightful and helpful; Jessica Wilson, acquisitions coordinator, who provided needed resources and helpful advice; Bob Campbell, copy editor, for excellent editing as well as his insightful comments; and project editor Carolyn Welch, who incorporated the many features found in this book and coordinated the intricate task of generating the final version. Thanks also to Scott Rogers who initiated the project.

Special thanks to Linus Torvalds, the creator of Linux, and to those who continue to develop Linux as an open, professional, and effective operating system accessible to anyone. Thanks also to the academic community, without whose special dedication Unix would not be the flexible and versatile operating system it is today. I would also like to thank professors and students at the University of California, Berkeley, for their experience and support in developing new and different ways of understanding operating system technologies.

I would also like to thank my parents, George and Cecelia, and my brothers George, Robert, and Mark for their support and encouragement with such a difficult project. Also Valerie and Marylou and my nieces and nephews Aleina, Larisa, Justin, Christopher, and Dylan, for their support and deadline reminders.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_5_0.png)

## Introduction

The Red Hat Linux distribution has become one of the major Linux distributions, bringing to the PC all the power and flexibility of a Unix workstation as well as a complete set of Internet applications and a fully functional desktop interface. This book is designed not only to be a complete reference on Linux, but also provides clear and detailed explanations of Linux features. No prior knowledge of Unix is assumed; Linux is an operating system anyone can use.

Red Hat has split its Linux development into two lines: Red Hat® Enterprise Linux® and the Fedora™ Project. Red Hat Enterprise Linux features commercial enterprise products for servers and workstations, with controlled releases issued every two years or so. The Fedora Project is an Open Source initiative whose Fedora Core release will be issued every six months on average, incorporating the most recent developments in Linux operating system features as well as supported applications. The Fedora release consists entirely of Open Source software. Development is carried out, using contributions from Linux developers, allowing them to promote enhancements, new features, and cutting-edge applications. The project operates like other open source projects, with releases keeping pace with the course of rapid online development. Unlike Red Hat Enterprise Linux, the Fedora Core version of Linux is entirely free, though not supported by Red Hat, Inc. You can download the most current version, including test betas, from fedora.redhat.com. The Fedora Project release will replace the original entry-level Red Hat Linux distribution. The Fedora Project will also provide Fedora extras, software that enhances the core collection, and Fedora alternatives, popular alternatives to core software applications.

The Red Hat Enterprise line of products is designed for corporate, research, and business applications. These products focus on reliability, stability, and performance. They are released on a much more controlled schedule than the Fedora Project versions. What was once the low-cost consumer version of Red Hat Linux will be replaced by a scaled-down commercial Enterprise version for consumers and small businesses. Red Hat offers three Enterprise versions: one for the workstation and two for servers. Red Hat Enterprise AS provides the highest level of support from intense mission critical requirements for all aspects of network support, including servers, databases, and security. Red Hat Enterprise ES provides a similar package but one geared to mid-level business requirements. The Red Hat Enterprise WS implements a workstation with a wide range of clients that can be used for either Red Hat Enterprise ES or AS networks.

This book covers the current Fedora Core release, while maintaining compatibility with Red Hat Enterprise Linux. The complete Fedora Core release is provided on the DVD-ROM included with this book. This book identifies seven major Linux topics: Basic setup, environments, applications, security, servers, system administration, and network administration. Whereas the book details the latest Red Hat tools, desktops, and kernel featured in the Fedora Project, it also covers in depth the network servers, administrative tasks, and applications featured in Red Hat Enterprise Linux. The book can be used as a comprehensive reference for both Red Hat Enterprise Linux and the Fedora Project.

The first two sections of the book are designed to cover tasks you would need to perform to get your system up and running. After an introduction to the working environment, including both GNOME and KDE desktops, you learn how to quickly update your system, manage users and groups, and set up your printer using the Red Hat administrative tools. The software management is nearly automatic, letting you install software on your system, including applications, with just a couple of mouse clicks. Internet access can be set up for modems, DSL, wireless, and Ethernet networks with easy-to-use administrative tools that guide you every step of the way. Many people now use Linux to set up a home or local business network. The steps involved to implement a basic network can now be carried out using simple software tools. You can even install Bluetooth devices. All these topics are covered in greater detail later in the book.

GNOME and the K Desktop Environment (KDE) have become standard desktop Graphical User Interfaces (GUI) for Linux and are noted for their power, flexibility, and ease-of-use. These are complete desktop environments that are more flexible than either Windows or the Mac/OS. You can install both, run applications from on the other, and easily switch from one to the other. Both have become integrated components of Linux, with applications and tools for every kind of task and operation. Instead of treating GNOME and KDE as separate entities, GNOME and KDE tools and applications are presented throughout the book.
