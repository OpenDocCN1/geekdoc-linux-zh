
# PART VI APPENDIXES 1137

## APPENDIX A: REGULAR EXPRESSIONS 1139
- Characters 1140
- Delimiters 1140
- Simple Strings 1140
- Special Characters 1140
- Periods 1141
- Brackets 1141
- Asterisks 1142
- Carets and Dollar Signs 1142
- Quoting Special Characters 1143
- Rules 1143
- Longest Match Possible 1143
- Empty Regular Expressions 1144
- Bracketing Expressions 1144
- The Replacement String 1144
- Ampersand 1145
- Quoted Digit 1145
- Extended Regular Expressions 1145
- Appendix Summary 1147

## APPENDIX B: HELP 1149
- Solving a Problem 1150
- Finding Linux-Related Information 1151
- Desktop Applications 1151
- Programming Languages 1152
- Linux Newsgroups 1152
- Mailing Lists 1153
- Specifying a Terminal 1153

## APPENDIX C: SECURITY INCLUDING GPG 1155
- Encryption 1156
- Public Key (Asymmetric) Encryption 1157
- Symmetric Key Encryption 1159
- Encryption Implementation 1160
- GnuPG/PGP 1160
- File Security 1161
- Email Security 1161
- MTAs (Mail Transfer Agents) 1161
- MUs (Mail User Agents) 1162
- Network Security 1162
- Network Security Solutions 1162
- Network Security Guidelines 1163
- Host Security 1165
- Login Security 1166
- Remote Access Security 1167
- Viruses and Worms 1168
- Physical Security 1168
- Tutorial: Using GPG to Secure a File 1169
- Creating a Key Pair 1170
- Exporting and Importing Public Keys 1172
- Signing and Verifying a File 1173
- Encrypting and Decrypting a File 1176
- Signing and Encrypting a File 1176
- Signing a Public Key 1177
- Using a Keyserver 1178
- Security Resources 1180
- Appendix Summary 1182

## APPENDIX D: Keeping the System Up-to-Date Using *apt-get* 1183
- Using *apt-get* to Install, Remove, and Update Packages 1184
- Using *apt-get* to Upgrade the System 1185
- Other *apt-get* Commands 1186
- Repositories 1186
- *sources.list*: Specifies Repositories for *apt-get* to Search 1187

## APPENDIX E: LPI AND CompTIA Certification 1189
- More Information 1190
- Linux Essentials 1190
- Topic 1: The Linux Community and a Career in Open Source 1190
- Topic 2: Finding Your Way on a Linux System 1193
- Topic 3: The Power of the Command Line 1196
- Topic 4: The Linux Operating System 1198
- Topic 5: Security and File Permissions 1201
- Certification Exam 1 Objectives: LX0-101 1204
    - 101 System Architecture 1204
    - 102 Linux Installation and Package Management 1206
    - 103 GNU and Unix Commands 1209
    - 104 Devices, Linux Filesystems, Filesystem Hierarchy Standard 1216
- Certification Exam 2 Objectives: LX0-102 1220
    - 105 Shells, Scripting and Data Management 1220
    - 106 User Interfaces and Desktops 1223
    - 107 Administrative Tasks 1224
    - 108 Essential System Services 1227
    - 109 Networking Fundamentals 1229
    - 110 Security 1232

# GLOSSARY 1235

# JUMPSTART INDEX 1283

# FILE TREE INDEX 1285

# UTILITY INDEX 1289

# MAIN INDEX 1295

# PREFACE

Whether you are an end user, a system administrator, or a little of both, this book explains with step-by-step examples how to get the most out of a Fedora or RHEL (Red Hat Enterprise Linux) system. In 29 chapters, this book takes you from installing a Fedora/RHEL system, through understanding its inner workings, to setting up secure servers that run on the system.

## The audience

This book is designed for a wide range of readers. It does not require you to have programming experience, although having some experience using a general-purpose computer, such as a Windows, Macintosh, UNIX, or another Linux system is certainly helpful. This book is appropriate for:

- Students who are taking a class in which they use Linux
- Home users who want to set up and/or run Linux
- Professionals who use Linux at work
- System administrators who need an understanding of Linux and the tools that are available to them, including the bash and Python scripting languages
- Computer science students who are studying the Linux operating system
- Technical executives who want to get a grounding in Linux

## Benefits

A Practical Guide to Fedora™ and Red Hat® Enterprise Linux®, Seventh Edition, gives you a broad understanding of many facets of Linux, from installing Fedora/RHEL through using and customizing it. No matter what your background, this book provides the knowledge you need to get on with your work. You will come away from this book understanding how to use Linux, and this book will remain a valuable reference for years to come.

## Features in this edition

This edition covers many topics to help you get your work done using Fedora/RHEL.

- Full coverage of LPI’s Linux Essentials certification learning goals and extensive coverage of CompTIA’s Linux+ exam objectives (Appendix E; page 1189)
- Updated chapters reflecting new features in Fedora 19 and RHEL 7 (beta)
- A new chapter that covers setting up VMs (virtual machines) and working in the cloud (Chapter 17; page 659)
- A new chapter on the Python programming language (Chapter 28; page 1081)
- A new chapter covering 32 Linux utilities (Chapter 7; page 215)
- A new chapter on the MariaDB/MySQL relational database (Chapter 29; page 1113)
- New coverage of the *firewall* service (Chapter 25; page 898)
- Tutorials on the *vim* and *nano* editors (Chapter 7; pages 262 and 270)
- Nine chapters on system administration (Part III; page 325)
- A chapter on writing programs using *bash* (Chapter 27; page 981)
- Coverage of the XFS filesystem (Chapter 11; page 527)
- Coverage of LDAP (Chapter 21; page 786)
- A section on the Cacti network monitoring tool (Chapter 16; page 645)
- Coverage of IPv6 (Chapter 8; page 293)
- Four indexes, making it easier to quickly find what you are looking for. These indexes locate tables (page numbers followed by the letter t), provide definitions (italic page numbers), and differentiate between light and comprehensive coverage (light and standard fonts).
- The JumpStart index (page 1283) lists all JumpStart sections in this book. These sections help you set up servers and clients as quickly as possible.
- The File Tree index (page 1285) lists, in hierarchical fashion, most files mentioned in this book. These files are also listed in the Main index.
- The Utility index (page 1289) supplies the location of all utilities mentioned in this book. A page number in a *light font* indicates a brief mention of the utility, whereas the regular font indicates more substantial coverage. The Utility index also appears on the inside of the front and back covers of the print book.
- The revised Main index (page 1295) is designed for ease of use.

## Overlap

If you have read *A Practical Guide to Linux® Commands, Editors, and Shell Programming, Third Edition*, you will notice some overlap between that book and the one you are reading now. The first chapter, the chapters on the utilities and the filesystem, the appendix on regular expressions, and the Glossary are very similar in the two books, as are the three chapters on the Bourne Again Shell (*bash*) and the chapters on Python and MariaDB. Chapters that appear in this book but do not appear in *A Practical Guide to Linux® Commands, Editors, and Shell Programming, Third Edition*, include Chapters 2 and 3 (installation), Chapter 4 (Fedora/RHEL) and the GUI, Chapter 8 (networking), all of the chapters in Part III (system administration) and Part IV (servers), and Appendix C (security).

## Differences

While this book explains how to use Linux from a graphical interface and from the command line (a textual interface), *A Practical Guide to Linux® Commands, Editors, and Shell Programming, Third Edition*, works exclusively with the command line and covers Mac OS X in addition to Linux. It includes full chapters on the vim and emacs editors, as well as chapters on the gawk pattern processing language, the sed stream editor, and the rsync secure copy utility. In addition, it has a command reference section that provides extensive examples of the use of 98 of the most important Linux and Mac OS X utilities. You can use these utilities to solve problems without resorting to programming in C.

# THIS BOOK INCLUDES A FEDORA 19 (SCHRÖDINGER'S CAT) DVD

The print book includes a DVD that holds an Install Image of Fedora 19 (Schrödinger’s Cat). You can use this DVD to install Fedora 19. Chapter 2 helps you get ready to install Fedora/RHEL. Chapter 3 provides step-by-step instructions for installing Fedora from this DVD as well as installing RHEL. This book guides you through learning about, using, and administrating a Fedora/RHEL system.

## DVD features

The DVD includes many of the software packages supported by Fedora. You can use it to perform a graphical or textual (command-line) installation of either a graphical or a textual Fedora system. If you do not have an Internet connection, you can use the DVD as a software repository: After you have installed Fedora, you can install supported software packages from the DVD.

# FOR READERS OF DIGITAL EDITIONS

If you are reading a digital edition of this book, see “Downloading an Installation Image File and Writing to/Burning the Installation Medium” on page 46 for instructions on how to download an Install Image and create a DVD or USB flash drive that holds that image.
