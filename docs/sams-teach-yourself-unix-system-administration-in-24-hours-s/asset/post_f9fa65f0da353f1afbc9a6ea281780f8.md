
## Solaris
## Red Hat Linux
## Mac OS X
## SAMS Teach Yourself
## Unix System Administration
## in 24 Hours
Dave Taylor

## SAMS
## Teach Yourself
## Unix System Administration
## in 24 Hours
Dave Taylor

## Sams Teach Yourself Unix System Administration in 24 Hours
## Copyright © 2003 by Sams Publishing
All rights reserved. No part of this book shall be reproduced, stored in a retrieval system, or transmitted by any means, electronic, mechanical, photocopying, recording, or otherwise, without written permission from the publisher. No patent liability is assumed with respect to the use of the information contained herein. Although every precaution has been taken in the preparation of this book, the publisher and author assume no responsibility for errors or omissions. Nor is any liability assumed for damages resulting from the use of the information contained herein.

International Standard Book Number: 0-672-32398-2

Library of Congress Catalog Card Number: 2001099557

Printed in the United States of America

First Printing: July 2002

05 04 03 02 4 3 2 1

## Trademarks
All terms mentioned in this book that are known to be trademarks or service marks have been appropriately capitalized. Sams Publishing cannot attest to the accuracy of this information. Use of a term in this book should not be regarded as affecting the validity of any trademark or service mark.

## Warning and Disclaimer
Every effort has been made to make this book as complete and as accurate as possible, but no warranty or fitness is implied. The information provided is on an “as is” basis. The author and the publisher shall have neither liability nor responsibility to any person or entity with respect to any loss or damages arising from the information contained in this book.

## ACQUISITIONS EDITOR
Kathryn Purdum

## DEVELOPMENT EDITOR
Heather Goodell

## MANAGING EDITOR
Charlotte Clapp

## PROJECT EDITOR
Elizabeth Finney

## PRODUCTION EDITOR
Seth Kerney

## INDEXER
Larry Sweazy

## PROOFREADER
Suzanne Thomas

## TECHNICAL EDITORS
Dee-Ann LeBlanc
David Ennis

## TEAM COORDINATOR
Amy Patton

## INTERIOR DESIGNER
Gary Adair

## COVER DESIGNER
Alan Clements

## PAGE LAYOUT
Stacey Richwine-DeRome

## Contents at a Glance
- Introduction 1
- 
- **PART I Installing Unix** 5
- Hour 1 Installing Unix 7
- 
- **PART II Introduction to the Filesystem** 21
- Hour 2 An Unsung Resource: Unix Documentation 23
- 3 Disk Usage 41
- 4 File Ownership 67
- 
- **PART III User & Package Management** 83
- Hour 5 Working with User Accounts 85
- 6 Account Management 107
- 7 Large File Management & Backups 133
- 8 Unix Package Management 161
- 
- **PART IV Advanced Filesystem Topics** 179
- Hour 9 Fixing Broken Disks 181
- 10 Adding Disks to Your System 197
- 11 Multiple Boot Configurations 217
- 12 Managing Disk Quotas 231
- 
- **PART V Process & System Controls** 245
- Hour 13 Changing System State 247
- 14 Exploring Processes 265
- 15 Running Jobs in the Future 285
- 16 Managing Your Log Files 301
- 
- **PART VI Network Topics** 325
- Hour 17 Basic Network Configuration 327
- 18 Running Your Own Name Server 353
- 19 Running Internet Services 373
- 20 Working with E-mail 391

## PART VII Web Server Management & Shell Programming 413
- Hour 21 Shell Scripting: The Administrator's Swiss Army Knife 415
- 22 Power Scripting with awk and Perl 443
- 23 Introduction to the Apache Web Server 457
- 24 Virtual Hosts with Apache 473
- Index 483

## Contents
- Introduction 1
- PART I Installing Unix 5
- HOUR 1 Installing Unix 7
- Unix Installation Options ....................8
- Basic Red Hat Linux Installation ....................10
- Installation Help Online ....................16
- Summary ....................17
- Q&A ....................17
- Workshop ....................18
- Quiz ....................18
- Answers ....................18
- PART II Introduction to the Filesystem 21
- HOUR 2 An Unsung Resource: Unix Documentation 23
- The Philosophy of Digging ....................23
- apropos: The Administrator's Secret Weapon ....................24
- Task 2.1: apropos and the Whatis Database ....................24
- Exploring the whatis Database ....................32
- Task 2.2: What's Inside the whatis Database ....................32
- Finding Commands ....................34
- Task 2.3: Which Command Are You Running? ....................34
- Digging Around in Executable Binaries ....................37
- Task 2.4: The strings Command ....................37
- Summary ....................39
- Q&A ....................39
- Workshop ....................39
- Quiz ....................39
- Answers ....................40
- HOUR 3 Disk Usage 41
- Physical Disks and Partitions ....................41
- Task 3.1: Exploring Partitions ....................42
- A Closer Look with du ....................47
- Task 3.2: Using du to Ascertain Directory Sizes ....................47
- Simplifying Analysis with sort ....................52
- Task 3.3: Piping Output to sort ....................53
- Identifying the Biggest Files ....................55
- Task 3.4: Finding Big Files ....................55

Keeping Track of Users: diskhogs ........................................59
Task 3.5: This Little Piggy Stayed Home? ................................59
Summary ...................................................64
Q&A .......................................................64
Workshop ...................................................64
Quiz .......................................................64
Answers ....................................................65
## HOUR 4 File Ownership 67
Starting at the Beginning: Permission Strings ...........................67
Task 4.1: The Basics of File Permissions ........................68
Ownership and /etc/passwd ..................................70
Task 4.2: Understanding /etc/passwd .........................70
Understanding Unix Groups and /etc/group ....................73
Task 4.3: Groups and the /etc/group file ....................74
Using Groups to Control Access .............................77
Task 4.4: Access Control with Groups .......................77
Summary ....................................................80
Q&A ........................................................80
Workshop ...................................................80
Q&A ..................................................80
Answers ....................................................81
## PART III User & Package Management 83
## HOUR 5 Working with User Accounts 85
Understanding the /etc/passwd File ..........................86
Task 5.1: Exploring /etc/passwd .............................86
Password Files in BSD/Mac OS X ..............................91
Task 5.2: Accounts and the Password File in Darwin ..........91
Adding Users and the adduser Script ........................94
Task 5.3: Adding Users in a Conventional Unix World .........95
Adding Users in a NetInfo World ............................100
Task 5.4: The Darwin Version of adduser .....................100
Summary ....................................................103
Q&A ........................................................103
Workshop ...................................................104
Quiz ........................................................104
Answers ....................................................104
## HOUR 6 Account Management 107
Ways to Suspend User Accounts ...............................108
Task 6.1: Suspending Users................................108
Deleting User Accounts ......................................112
Task 6.2: Deleting User Accounts.............................112
