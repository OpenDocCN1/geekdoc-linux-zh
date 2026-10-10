
![](img/e85417bb52fc523c6fc7b3b77b124ecb_0_0.png)

## Comprehensive Coverage of Linux Commands

Bryan Pfaffenberger

# Linux Command Instant Reference

The Perfect Companion for Any Linux Distribution

Quickly Find the Command You Need to Execute Specific Tasks

Covers the Essentials, Plus Powerful Utilities

## Get the Answers You Need Quickly with

**Linux Command Instant Reference**

### LEARN SHELL FUNDAMENTALS (SEE CHAPTER 3)

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Find out which processes are hogging the most memory or CPU time? | **ps**, **top** | `ps -el --sort --size` |
| Redirect command output to a file, as well as show it on-screen? | **tee** | `dir \| tee > listing.txt` |
| Export a variable that is needed by an application? | **export** | `export MYFILES=~/home/suzanne/essays` |
| Add a directory to the path without wiping out the existing path? | **export** | `export PATH=$PATH:~/home/suzanne/essays` |

### NAVIGATE THE FILESYSTEM AND FIND FILES (SEE CHAPTER 4)

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| List files sorted by the time of their last modification, showing the most recently modified files first? | **dir**, **ls** | `ls -cl` |
| Find all the files that have been changed in the last two hours? | **find** | `find /home/suzanne -ctime 2` |
| Find a file in the current directory that has been changed since you last made changes to another file? | **find** | `find /home/suzanne -newer 'essay1.doc'` |

### ARCHIVE, ENCODE, COMPRESS, AND ENCRYPT FILES (SEE CHAPTER 6)

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Extract from a backup archive only those files that meet a shell pattern that I specify? | **cpio** | `cpio -iv '*.doc' < archive.cpio` |
| Make a backup archive of all the files in the working directory? | **cpio** | `ls cpio -v > this-directory.cpio` |
| Encrypt a file so that no one can read it unless they know the passphrase, and compress it so that it takes up the least possible storage space? | **mcrypt** | `mcrypt -uZ mysecrets.txt` |

### WORK WITH TEXT FILES (SEE CHAPTER 8)

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Compare two sorted files and view the differences between them with surrounding context? | `diff` | `diff -c first-draft.txt second-draft.txt` |
| Number the lines in a text file? | `nl` | `nl magic.txt > magic-numbered.txt` |
| Convert a Portable Document Format (PDF) file to PostScript? | `pdf2ps` | `pdf2ps resume.pdf resume.ps` |
| Translate all the uppercase characters in a text file to lowercase? | `tr` | `cat uppercase.txt \| tr '[A-Z]' '[a-z]'` |

### WORK WITH SOUND AND GRAPHIC FILES (SEE CHAPTER 9)

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Create a thumbnail index of all the graphic files in the working directory? | `convert` | `convert 'vids:*.jpg' catalog.jpg` |
| Create a printed jewel case label for a CD-ROM that I've just burned? | `cdlabelgen` | `cdlabelgen -c 'My Favorites' -s '2000' -i 'BluesJazzRock& Alternative Rock\nTechno\nIndustrial' -e images/mp3.eps > cover.ps` |
| Create a composite image of two or more graphic files using special effects? | `combine` | `combine -compose bumpmap image1.jpg image2.jpg combined.jpg` |

### CONFIGURE AND USE NETWORKS AND THE INTERNET (SEE CHAPTER 13)

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Display information about all the TCP/IP sockets currently in operation? | `netstat` | `netstat -a` |
| Copy a file to a remote server for which I have appropriate permissions? | `rcp` | `rcp essay1.doc essay1.bak@lothlorien:/home/suzanne/Documents/Backup` |
| View available NFS shares? | `showmount` | `showmount -a` |
| Mount a Samba share on a remote system? | `smbmount` | `smbmount //lothlorien/suzanne /home/suzanne/lothlorien` |
| Connect to a remote Telnet service? | `telnet` | `telnet lothlorien.mynetwork.org` |

# Linux Command Instant Reference

## BPB PUBLICATIONS
B-14, CONNAUGHT PLACE, NEW DELHI-110001

## FIRST INDIA EDITION 2001

### Distributors:

**MICRO BOOK CENTRE**
2, City Centre, CG Road,
Near Swastic Char Rasta,
AHMEDABAD-380009 PHONE: 6421611

**COMPUTER BOOK CENTRE**
12, Shungar Shopping Centre, M.G. Road,
BANGALORE-560001 Phone: 5587923, 5584684

**MICRO BOOKS**
Shanti Niketan Building, 8, Camac Street,
CALCUTTA-700017 Phone: 2626518, 2626519

**BUSINESS PROMOTION BUREAU**
8/1, Ritchie Street, Mount Road,
CHENNAI-600002 Phone: 834796, 8550491

**DECCAN AGENCIES**
4-3-329, Bank Street,
HYDERABAD-400001 Phone: 4756450, 4756997

**MICRO MEDIA**
Shop No. 5, Mahendra Chambers, 150 D.N. Road,
Next to Capitol Cinema V.T. (C.S.T.) Station,
MUMBAI-400001 Ph. 2076936, 2076737, 2002732

**BPF PUBLICATIONS**
B-14, Connaught Place, NEW DELHI-110001
Phone: 3325760, 3723933, 3737742

**INFO TECH**
G-2, Siddharth Building, 96 Nehru Place,
NEW DELHI-110019
Phone: 6438245, 6415092, 6234208

**INFO TECH**
Shop No. 2, F-38, South Extension Part-1
NEW DELHI-110049
Phone: 4691288, 4641941

**INFO TECH**
B-11, Vanthamman Plaza, Sector-16,
Electronics Nagar, NOIDA-201301
Phone: 914-512329, 515917, 515918

**BPF BOOK CENTRE**
376, Old Lajpat Rai Market,
DELHI-110006 PHONE: 2961747

Original ISBN 0-7821-2748-7

SYBEX and the SYBEX logo are registered trademarks of SYBEX Inc.
TRADEMARKS: SYBEX has attempted throughout this book to distinguish proprietary trademarks from descriptive terms by following the capitalization style used by the manufacturer. SYBEX is not affiliated with any manufacturer.

Every effort has been made to supply complete and accurate information. However, SYBEX assumes no responsibility for its use, nor for any infringement of the intellectual property rights of third parties which would result from such use.

Copyright © 2001 SYBEX Inc., USA. World Right Reserved. No part of this publication may be stored in a retrieval system, transmitted, or reproduced in any way, including but not limited to photocopy, photograph, magnetic or other record, without the prior agreement and written permission of the publisher.

This edition is Authorized for sale only in the following countries: INDIA, BANGLADESH, NEPAL, PAKISTAN, SRI LANKA AND MALDIVE.
*Printed in India by arrangement with SYBEX Inc., USA.*

ISBN 81-7656-319-6
Published by Manish Jain for BPF Publications, B-14, Connaught Place
New Delhi-110001 and Printed by him at Pressworks, Delhi.

## Contents at a Glance

- Introduction …… xxi
- CHAPTER 1 Logging In and Managing Sessions …… 1
- CHAPTER 2 Getting Help and Finding Your Bearings …… 27
- CHAPTER 3 Learning Shell Fundamentals …… 49
- CHAPTER 4 Navigating the Filesystem and Finding Files …… 105
- CHAPTER 5 Managing Files and Directories …… 137
- CHAPTER 6 Archiving, Encoding, Compressing, and Encrypting Files …… 189
- CHAPTER 7 Managing Disk and Tape Drives …… 239
- CHAPTER 8 Working with Text Files …… 279
- CHAPTER 9 Working with Sound and Graphic Files …… 367
- CHAPTER 10 Working with Fonts …… 427
- CHAPTER 11 Using Text Editors …… 455
- CHAPTER 12 Configuring and Managing Your System …… 507
- CHAPTER 13 Configuring and Using Networks and the Internet …… 575
- Index …… 629

## Contents

Introduction xxi

### CHAPTER 1

#### Logging In and Managing Sessions

- Linux Fundamentals 3
  - _Linux Distributions_ 3
  - _Users and the System Administrator_ 7
  - _Logging In_ 7
  - _What You’ll See After You Log In_ 8
  - _Essential Typing and Editing Skills_ 11
  - _Using Virtual Consoles_ 11
  - _The X Window System_ 12
- Alphabetical Command Reference 15
  - _chvt_ 15
  - _login_ 15
  - _logout_ 16
  - _login_ 16
  - _rxvt_ 16
  - _shutdown_ 18
  - _startx_ 19
  - _su_ 20
  - _tty_ 20
  - _Xconfigurator_ 21
  - _xdm_ 21
  - _XF86Setup_ 22
  - _xterm_ 23

### CHAPTER 2

#### Getting Help and Finding Your Bearings

- Getting Help with Linux 29
- Alphabetical Command Reference 32
  - _apropos_ 32
  - _cal_ 33
  - _chfn_ 34
