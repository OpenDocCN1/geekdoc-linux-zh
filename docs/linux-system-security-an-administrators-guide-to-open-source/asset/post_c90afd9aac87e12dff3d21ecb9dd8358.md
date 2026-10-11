
# Linux System Security

An Administrator's Guide to Open Source Security Tools

Scott Mann and Ellen L. Mitchell

Prentice Hall PTR
Upper Saddle River, NJ 07458
www.phptr.com

Editorial/production supervision: BooksCraft, Inc., Indianapolis, IN
Acquisitions editor: Mary Franz
Editorial assistant: Noreen Regina
Marketing manager: Lisa Konzelmann
Manufacturing manager: Maura Goldstaub
Cover design director: Jerry Votta
Cover designer: Anthony Gemmellaro
Project coordinator: Anne Trowbridge

![](img/7933c44717ab0711177ea7153f959fc5_7_0.png)

© 2000 by Prentice Hall PTR
Prentice-Hall, Inc.
Upper Saddle River, NJ 07458

Prentice Hall books are widely used by corporations and government agencies for training, marketing, and resale.

The publisher offers discounts on this book when ordered in bulk quantities. For more information, contact:

Corporate Sales Department
Phone: 800-382-3419 Fax: 201-236-7141
E-mail: corpsales@prenhall.com

Or write:

Prentice Hall PTR
Corporate Sales Department
One Lake Street
Upper Saddle River, NJ 07458

All product names mentioned herein are the trademarks of their respective owners.

All rights reserved. No part of this book may be reproduced, in any form or by any means, without permission in writing from the publisher.

Printed in the United States of America

10 9 8 7 6 5 4 3 2 1

ISBN: 0-13-015807-0

Prentice-Hall International (UK) Limited, London
Prentice-Hall of Australia Pty. Limited, Sydney
Prentice-Hall Canada Inc., Toronto
Prentice-Hall Hispanoamericana, S.A., Mexico
Prentice-Hall of India Private Limited, New Delhi
Prentice-Hall of Japan, Inc., Tokyo
Pearson Education Asia Pte. Ltd., Singapore
Editora Prentice-Hall do Brasil, Ltda., Rio de Janeiro

To my wonderful wife, Connie,
and our three beautiful children,
Melissa, Joshua, and Christiana.
—Scott

To my parents, Fred and Beverly Mitchell,
and to my sister, Sara.
—Ellen

# Contents

Figures...xix
Examples...xxi
Tables...xxix
Preface...xxxiii

## Chapter 1

- Vulnerability Survey...1
- What Happened?...2
- Other Cracker Activities...3
- So, Are You Going to Show Us How to Break into Systems?...3
- A Survey of Vulnerabilities and Attacks...4
  - Technical...4
  - Social...6
  - Physical...6
- Summary...7
- For Further Reading...7
  - Books...7
  - Interesting Cracker Tales...8
  - Web Sites...8
  - Full-Disclosure Resources...9

## Chapter 2

- Security Policies...11
- What Is Computer and Network Security?...13
- Elements of a Computing Environment...13
- Risk Analysis...14
- The Security Policy...14
- Securing Computers and Networks...15
- User Privacy and Administrator Ethics...18
- Summary...18
- For Further Reading...18
  - Books...18
  - Web Resources...19
  - Other Resources...19

## Chapter 3

- Background Information 21
- BIOS Passwords 22
- Linux Installation and LILO 22
  - A Note about LILO 22
  - Recovering a Corrupt System 24
  - Installation and LILO Resources 24
- Start-Up Scripts 24
- Red Hat Package Manager 26
  - Verifying Packages with RPM 26
  - Checking PGP Signatures with RPM 27
  - RPM Resources 28
  - RPM Mailing List 28
- TCP/IP Networking Overview 30
  - The TCP/IP Model Layers 30
  - Remote Procedure Call Applications 36
  - Trusted Host Files and Related Commands 36
  - Some Major Applications 37
  - Network Monitoring 38
  - General TCP/IP Networking Resources 39
  - NFS, Samba, NIS, and DNS Resources 40
- Request for Comment 40
- Cryptography 41
  - The Purpose of Cryptography 41
  - Algorithm Types 42
  - Hash Functions and Digital Signatures 44
  - Passwords Aren’t Encrypted, They’re Hashed! 45
  - An Overview of PGP 45
  - Cryptography References 47
- Testing and Production Environments 47
  - Security Archives 47
  - Software Testing 48
  - Source Code Auditing 48
  - Pristine Backups 49
  - Security Resources 49
  - Licenses 50

## Chapter 4

- Users, Permissions, and Filesystems 57
- User Account Management 57
  - Good Passwords 58
  - All Accounts Must Have Passwords! Or Be Locked! 59
  - Passwords Aging and the Shadow File 61
  - Restricted Accounts 64
  - Shell History 66
- The Root Account . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 66
  - Using the Root Account . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 66
  - Multiple root Users . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 67
  - Minimizing the Impact of root Compromise . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 68
  - Configuring `/etc/security` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 68
- Group Account Management . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 69
- File and Directory Permissions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 70
  - User File and Directory Permissions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 71
  - System File and Directory Permissions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
  - SUID and SGID . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74
  - File Attributes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75
- Using `xlock` and `xsscreensaver` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
- Filesystem Restrictions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 78
- Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 79
- For Further Reading
  - System Administration . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 80
  - System Security . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 80

## Chapter 5

> Been Cracked?
> Just Put PAM On It!

- Pluggable Authentication Modules . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 81
  - PAM Overview . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 82
  - PAM Configuration . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 83
  - PAM Administration . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
  - PAM and Passwords . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
  - PAM and Passwords Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
  - PAM and login . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93
  - Time and Resource Limits . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
  - Access Control with `pam_listfile` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
  - PAM and `su` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 103
  - Using `pam_access` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 104
  - Using `pam_lastlog` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 105
  - Using `pam_rhosts_auth` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 106
  - One-Time Password Support . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 108
  - PAM and the `other` Configuration File . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 108
  - Additional PAM Options . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 109
- PAM Logs . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 109
- Available PAM Modules . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 109
- PAM-Aware Applications . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 112
- Important Notes about Configuring PAM . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 112
- The Future of PAM . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114
- Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114
- For Further Reading . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114
  - On-Line Documentation . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 115
