
# NETWORKING

# The Complete Guide to
Linux System
Administration

THOMSON
COURSE TECHNOLOGY

Nicholas Wells

Includes Red Hat® Linux®
Fedora Core 2 Software

# The Complete Guide to Linux System Administration
maps to the following professional certifications:

- **Red Hat Certified Technician (RHCT)**. Objectives are listed and mapped to this book in Appendix A. See also www.redhat.com/training.
- **Linux Professional Institute (LPI) Level 1**. Objectives are listed and mapped to this book in Appendix B. See also www.lpi.org.
- **SAIR/GNU Linux Certified Administrator (LCA), Level 1**. Objectives are listed and mapped to this book in Appendix C. This text maps to the first two of four exams. See also www.linuxcertification.org.
- **CompTIA Linux+**. Objectives are listed and mapped to this book in Appendix D. See also www.comptia.org.

# The Complete Guide to
Linux System
Administration

Nicholas Wells

THOMSON
COURSE TECHNOLOGY

THOMSON
COURSE TECHNOLOGY

# The Complete Guide to Linux System Administration

is published by Course Technology.

Managing Editor
William Pitkin III

Production Editor
Brooke Booth

Technical Editor
Serge Palladino

Editorial Assistant
Jennifer Smith

Text Design
GEX Publishing Services

Product Manager
Amy M. Lyon

Senior Manufacturing Coordinator
Trevor Kallop

Quality Assurance Management
John Freitas

Cover Design
Abigail Scholz

Compositor
GEX Publishing Services

Developmental Editor
Deb Kaufmann

Senior Marketing Manager
Karen Seitz

Associate Product Manager
Sarah Santoro

COPYRIGHT © 2005 Course Technology, a division of Thomson Learning, Inc. Thomson Learning™ is a trademark used herein under license.

Printed in Canada
1 2 3 4 5 6 7 8 9 WC 09 08 07 06 05

For more information, contact Course Technology, 25 Thomson Place, Boston, Massachusetts, 02210.

Or find us on the World Wide Web at: www.course.com

ALL RIGHTS RESERVED. No part of this work covered by the copyright hereon may be reproduced or used in any form or by any means—graphic, electronic, or mechanical, including photocopying, recording, taping, Web distribution, or information storage and retrieval systems—without the written permission of the publisher.

For permission to use material from this text or product, submit a request online at www.thomsonrights.com

Any additional questions about permissions can be submitted by e-mail to thomsonrights@thomson.com

Disclaimer:
Course Technology reserves the right to revise this publication and make changes from time to time in its content without notice.

The Web addresses in this book are subject to change from time to time as necessary without notice.

Linux is a registered trademark of Linus Torvalds. Linux+ is a trademark of CompTIA.

ISBN 0-619-21616-6

BRIEF
Contents

INTRODUCTION xv

CHAPTER ONE
Introducing Linux 1

CHAPTER TWO
Exploring the Desktop 57

CHAPTER THREE
Using the Shell 109

CHAPTER FOUR
Understanding Users and File Systems 155

CHAPTER FIVE
Understanding Text Processing 197

CHAPTER SIX
Managing Processes 235

CHAPTER SEVEN
Using Network Clients 289

CHAPTER EIGHT
Installing Linux 327

CHAPTER NINE
Understanding System Initialization 401

CHAPTER TEN
Managing Software Packages and File Systems 433

CHAPTER ELEVEN
Managing Users 477

CHAPTER TWELVE
Configuring Networks 521

CHAPTER THIRTEEN
System and Kernel management 575

CHAPTER FOURTEEN
Writing Shell Scripts 635

CHAPTER FIFTEEN
Advanced Topics and Troubleshooting 677

APPENDIX A
Red Hat Certified Technician Objectives 757

APPENDIX B
Linux Professional Institute LPI Certification—Level 1 Objectives 771

APPENDIX C
SAIR/GNU Certified Linux Administrator (LCA) Level 1 Objectives 793

APPENDIX D
Linux+ Certification Objectives 815

GLOSSARY 821

INDEX 843

TABLE OF
Contents

INTRODUCTION xv

## CHAPTER ONE
Introducing Linux

- A Brief History 2
  - Understanding Operating Systems 2
  - Operating System Functions 3
  - The UNIX Operating System 4
  - The Free Software Foundation and the GNU Project 5
  - Linux Arrives 6
  - Motivating Free Software Developers 9
  - The Strengths of Linux 10
- Linux in the Market 10
  - Linux Distributions 11
  - Red Hat Software 11
  - Hardware Requirements 13
  - Version Numbering 14
  - Linux Certification 16
- The Work of a System Administrator 17
  - Careers in Linux 17
  - The Duties of a System Administrator 18
  - Ethics, Privacy, and the Law 21
- Starting to Use Linux 23
  - Logging In 23
  - Graphical Environments 24
  - Opening a Terminal Window 25
- Exploring the File System 25
  - File System Concepts 26
  - Managing Files with Graphical Utilities 28
  - Working at a Command Line 32
- Finding Command Help 38
  - Reading Linux Documentation 38
  - Linux Command Information 40
- Chapter Summary 41
- Command Summary 43
- Key Terms 43
- Review Questions 47
- Hands-On Projects 51
- Case Projects 55

## CHAPTER TWO
Exploring the Desktop

- Linux Graphical Desktops 58
- Understanding the X Window System 58
- How the X Window System Functions 59
- Components of the X Window System 59
- Starting X 62
- Desktop Interfaces 63
- The Graphical Login Screen 65
- Working with Graphical Windows 66
- Configuring GNOME and KDE 69
- Switching Between Desktop Interfaces 70
- Saving Your Configuration Between Logins 70
- Configuring the Graphical Login Screen 72
- The Panel 76
- Configuring Other GNOME Features 81
- Core Graphical Utilities 81
- Configuring the Nautilus File Manager 81
- Configuring the Use of Other Utilities 84
- Popular Graphical Programs 85
- OpenOffice.org 85
- Using E-mail Clients 90
- Chapter Summary 96
- Command Summary 98
- Key Terms 98
- Review Questions 98
- Hands-on Projects 102
- Case Projects 106

## CHAPTER THREE
Using the Shell

- Exploring the Bash Shell 110
- The Shell Prompt 110
- The Functions of a Shell 111
- Different Types of Shells 112
- Entering Commands 114
- The Shell Start-up Process 118
- Using Aliases 119
- Command-line Expansion 121
- Shell Variables 124
- Data Redirection 128
- Editing Text with vi 131
- Printing from the Command Line 136
- Setting up a Printer 136
- Printing from a Command Line 139
- Chapter Summary 141
- Command Summary 142
- Key Terms 142
- Review Questions 144
- Hands-On Projects 148
- Case Projects 153

## CHAPTER FOUR
Understanding Users and File Systems 155

- Linux Users and Groups 156
- Types of User Accounts 156
- Linux Groups 158
- User and Group Files 159
- Shadow Passwords 162
- Changing User Passwords 163
- User Information Commands 165
- File Permissions 166
- Changing Ownership 167
- Changing File Permissions 169
- Default File Permissions 170
- Introducing the File System 171
- Partitions and File Systems 171
- Inodes and Links 172
- File Types 175
- Accessing Removable Media 176
- Using find 178
- Managing File Archives 179
- Compressing Files 179
- Using tar and cpio for Archiving Files 180
- Chapter Summary 182
- Command Summary 184
- Key Terms 185
- Review Questions 187
- Hands-On Projects 190
- Case Projects 195

## CHAPTER FIVE
Understanding Text Processing 197

- Regular Expressions 198
- Manipulating Files 201
- Searching for Patterns with grep 201
- Examining File Contents 203
- Manipulating Text Files 205
- Using sed and awk 209
- Filtering and Editing Text with sed 209
- Formatting with awk 211
- More Advanced Text Editing 214
- File Operations in vi 214
- Screen Repositioning 215
- More Line-editing Commands 216
- Setting vi Options 218
- Summary of vi Commands 219
- Chapter Summary 221
- Command Summary 222
- Key Terms 223
- Review Questions 223
- Hands-On Projects 227
- Case Projects 233
