
# Kali Linux Revealed
## Mastering the Penetration Testing Distribution

Raphaël Hertzog, Jim O'Gorman, Mati Aharoni
Introduction by Johnny Long

![](img/46e3313ea1bb2892f314630a4f0677b8_0_0.png)

# Kali Linux Revealed
## Mastering the Penetration Testing Distribution
by Raphaël Hertzog, Jim O’Gorman, and Mati Aharoni

![](img/46e3313ea1bb2892f314630a4f0677b8_3_0.png)

# Kali Linux Revealed

Copyright © 2017 Raphaël Hertzog, Jim O'Gorman, and Mati Aharoni

This book is licensed under a Creative Commons Attribution-ShareAlike 3.0 Unported License.

- http://creativecommons.org/licenses/by-sa/3.0/

Some sections of this book borrow content from the “Debian Administrator's Handbook, Debian Jessie from Discovery to Mastery” written by Raphaël Hertzog and Roland Mas, which is available here:

- https://debian-handbook.info/browse/stable/

For the purpose of the CC-BY-SA license, Kali Linux Revealed is an Adaptation of the Debian Administrator’s Handbook.

“Kali Linux” is a trademark of Offensive Security. Any use or distribution of this book, modified or not, must comply with the trademark policy defined here:

- https://www.kali.org/trademark-policy/

All Rights Not Explicitly Granted Above Are Reserved.

ISBN: 978-0-9976156-0-9 (paperback)

Offsec Press
19701 Bethel Church Road, #103-253
Cornelius NC 28031
USA
www.offensive-security.com

Library of Congress Control Number: 2017905895

The information in this book is distributed on an “As Is” basis, without warranty. While every precaution has been taken in the preparation of this work, neither the authors nor Offsec Press shall have any liability to any person or entity with respect to any loss or damage caused or alleged to be caused directly or indirectly by the information contained in it.

Because of the dynamic nature of the Internet, any Web addresses or links contained in this book may have changed since publication and may no longer be valid.

Printed in the United States of America.

# Table of Contents

## 1. About Kali Linux
1.1 A Bit of History
1.2 Relationship with Debian
   1.2.1 The Flow of Packages
   1.2.2 Managing the Difference with Debian
1.3 Purpose and Use Cases
1.4 Main Kali Linux Features
   1.4.1 A Live System
   1.4.2 Forensics Mode
   1.4.3 A Custom Linux Kernel
   1.4.4 Completely Customizable
   1.4.5 A Trustable Operating System
   1.4.6 Usable on a Wide Range of ARM Devices
1.5 Kali Linux Policies
   1.5.1 Single Root User by Default
   1.5.2 Network Services Disabled by Default
   1.5.3 A Curated Collection of Applications
1.6 Summary

## 2. Getting Started with Kali Linux
2.1 Downloading a Kali ISO Image
   2.1.1 Where to Download
   2.1.2 What to Download
   2.1.3 Verifying Integrity and Authenticity
      _Relying on the TLS-Protected Website_
      _Relying on PGP's Web of Trust_
   2.1.4 Copying the Image on a DVD-ROM or USB Key
      _Creating a Bootable Kali USB Drive on Windows_
      _Creating a Bootable Kali USB Drive on Linux_
      _Creating a Bootable Kali USB Drive on OS X/macOS_
2.2 Booting a Kali ISO Image in Live Mode
   2.2.1 On a Real Computer
   2.2.2 In a Virtual Machine

_Preliminary Remarks_
_VirtualBox_
_VMware_

2.3 Summary

## 3. Linux Fundamentals
3.1 What Is Linux and What Is It Doing?
   3.1.1 Driving Hardware
   3.1.2 Unifying File Systems
   3.1.3 Managing Processes
   3.1.4 Rights Management
3.2 The Command Line
   3.2.1 How To Get a Command Line
   3.2.2 Command Line Basics: Browsing the Directory Tree and Managing Files
3.3 The File System
   3.3.1 The Filesystem Hierarchy Standard
   3.3.2 The User’s Home Directory
3.4 Useful Commands
   3.4.1 Displaying and Modifying Text Files
   3.4.2 Searching for Files and within Files
   3.4.3 Managing Processes
   3.4.4 Managing Rights
   3.4.5 Getting System Information and Logs
   3.4.6 Discovering the Hardware
3.5 Summary

## 4. Installing Kali Linux
4.1 Minimal Installation Requirements
4.2 Step by Step Installation on a Hard Drive
   4.2.1 Plain Installation
      _Booting and Starting the Installer_
      _Selecting the Language_
      _Selecting the Country_
      _Selecting the Keyboard Layout_
      _Detecting Hardware_
      _Loading Components_
      _Detecting Network Hardware_
      _Configuring the Network_
      _Root Password_
      _Configuring the Clock_
      _Detecting Disks and Other Devices_
      _Partitioning_
