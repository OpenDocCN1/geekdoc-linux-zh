
![](img/f34d37e3abe9f4517128e54f80ab2616_0_0.png)

# FreeBSD: The Complete Reference

## The Complete Reference

*   Install, configure, and run this open-source operating system like a pro
*   Configure network servers and workstation-productivity applications
*   Tap FreeBSD’s speed, security, load-handling, and administration benefits

Roderick W. Smith
Computer-book author and UNIX specialist

---

Digitized by the Internet Archive
in 2024

https://archive.org/details/freebsdcompleter0000smit

---

# About the Author

**Roderick W. Smith** is a professional computer book author and consultant based in Woonsocket, Rhode Island. He has been a user of UNIX systems since 1987, and has administered UNIX-like systems, including FreeBSD, since 1994. *FreeBSD: The Complete Reference* is his tenth book. His other titles include *Advanced Linux Networking* (Addison-Wesley, 2002) and *The Multi-Boot Configuration Handbook* (Que, 2000).

---

# FreeBSD: The Complete Reference

Roderick W. Smith

**McGraw-Hill/Osborne**

New York   Chicago   San Francisco   Lisbon   London   Madrid   Mexico City   Milan   New Delhi   San Juan   Seoul   Singapore   Sydney   Toronto

---

McGraw-Hill/Osborne
2600 Tenth Street
Berkeley, California 94710
U.S.A.

To arrange bulk purchase discounts for sales promotions, premiums, or fund-raisers, please contact **McGraw-Hill/Osborne** at the above address. For information on translations or book distributors outside the U.S.A., please see the *International Contact Information* page immediately following the index of this book.

**Copyright © 2003 by The McGraw-Hill Companies. All rights reserved. Printed in the United States of America. Except as permitted under the Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of publisher, with the exception that the program listings may be entered, stored, and executed in a computer system, but they may not be reproduced for publication.**

1234567890 DOC DOC 019876543

Book p/n 0-07-222674-9 and CD p/n 0-07-222675-7
parts of
ISBN 0-07-222674-9

| Role | Name |
| :--- | :--- |
| Copy Editor | Marti Paul |
| Proofreader | Emily Hsuan |
| Indexer | David Heiret |
| Computer Designers | Apollo Publishing Services, Michelle Galicia |
| Illustrators | Michael Mueller, Lyssa Wald |
| Series Design | Peter F. Hanclik |
| Publisher | Brandon A. Nordin |
| Vice President & Associate Publisher | Scott Rogers |
| Acquisitions Editor | Franny Kelly |
| Project Editor | Laura Stone |
| Acquisitions Coordinators | Emma Acker, Martin Przybyla |
| Technical Editor | Glenn Becker |

This book was composed with Corel VENTURA™ Publisher.

Information has been obtained by McGraw-Hill/Osborne from sources believed to be reliable. However, because of the possibility of human or mechanical error by our sources, McGraw-Hill/Osborne, or others, McGraw-Hill/Osborne does not guarantee the accuracy, adequacy, or completeness of any information and is not responsible for any errors or omissions or the results obtained from the use of such information.

---

# Contents at a Glance

This book is for Bethany and Tarl,
friends who moved too far away too soon after they’d moved to Boston.

---

# Part I FreeBSD Installation

1. FreeBSD Requirements . . . . . . . . . . . . . . . . . . . . . . . . . 3
2. System Installation . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 31
3. An Overview of the System . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 69
4. Coexistence with Other Operating Systems . . . . . . . . . . . . . . . . . . . . . 99

# Part II Basic System Administration

5. System Administration Tools . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 131
6. System Startup and Control Processes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 161
7. Managing Partitions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 183
8. Managing Files . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 205
9. Printer Configuration . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 237
10. Managing User Accounts . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 263
11. Installing Software . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 289
12. Kernel Configuration . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 313
13. The X Window System . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 327

# Part III Network Configuration

14. Basic Network Configuration 355
15. Dial-Up Networking 377
16. Principles of Network Clients and Servers 395
17. Setting Up a Firewall 411

# Part IV Servers

18. File Servers 435
19. Mail Servers 453
20. Web Servers 475
21. Login Servers 493
22. Miscellaneous Servers 521

# Part V Common User Programs

23. Desktop Environments 547
24. Networking Tools 569
25. Office Tools 599
26. Graphics Tools 623
27. Multimedia and Games 647

# Part VI System Maintenance

28. Automated and Nonautomated Routine Maintenance 673
29. System Security Considerations 699
30. Compiling Software 731
31. Writing Scripts 745
32. Troubleshooting 773
Glossary 797
Index 811

---

# Contents

*   Acknowledgments .............................. xxvii
*   Introduction .............................. xxix

## Part I
**FreeBSD Installation**

*   1. FreeBSD Requirements .............................. 3
    *   Why Run FreeBSD? .............................. 4
    *   FreeBSD as a Workstation OS .............................. 4
    *   FreeBSD as a Server OS .............................. 6
    *   FreeBSD vs. Non-UNIX OSs .............................. 7
    *   FreeBSD vs. Other UNIX-Like OSs .............................. 9
    *   The Software Environment .............................. 13
    *   The Development of FreeBSD .............................. 13
    *   Interactions with Other Computers on a Network .............................. 14
    *   Interactions with Other OSes on a Single Computer .............................. 16
    *   The Hardware Environment .............................. 18
        *   CPU Types and Speed .............................. 18
        *   RAM Requirements .............................. 19
        *   Hard Disks .............................. 20
        *   Video Hardware .............................. 23

*   Network Hardware ………… 25
*   Printers ………… 27
*   Miscellaneous Hardware ………… 28
*   Summary ………… 29

## 2 System Installation

*   Obtaining FreeBSD ………… 32
*   FreeBSD Licensing Issues ………… 32
*   Sources of FreeBSD ………… 34
*   Preparing Installation Media ………… 35
*   Preparing a Computer to Run FreeBSD ………… 36
*   Checking Hardware Compatibility ………… 37
*   Clearing Disk Space ………… 40
*   Beginning the Installation ………… 44
*   Booting an Installer ………… 44
*   Partitioning the System ………… 45
*   Selecting Software to Install ………… 50
*   Selecting an Installation Medium ………… 51
*   Installing FreeBSD ………… 52
*   Post-Installation Configuration ………… 52
*   Network Configuration ………… 53
*   System Console Settings ………… 55
*   Time Zone ………… 56
*   Linux Binary Compatibility ………… 57
*   Mouse Configuration ………… 57
*   XFree86 Configuration ………… 58
*   X Desktop Configuration ………… 61
*   FreeBSD Package Configuration ………… 63
*   User Configuration ………… 63
*   Finishing the Installation ………… 68
*   Summary ………… 68

## 3 An Overview of the System

*   Booting the Computer ………… 70
*   Selecting FreeBSD ………… 70
*   Interpreting Boot Messages ………… 71
*   Understanding Startup Scripts ………… 73
*   Logging into an Account ………… 74
*   Text-Mode and GUI Logins ………… 74
*   User vs. root Accounts ………… 76
*   A Summary of Text-Mode Commands ………… 77
*   Understanding Shells ………… 78
*   Running Text-Mode Programs ………… 80
*   File Manipulation Commands ………… 82
