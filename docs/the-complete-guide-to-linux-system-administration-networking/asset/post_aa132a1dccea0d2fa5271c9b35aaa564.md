
Chapter Summary 731
Command Summary 733
Key Terms 736
Review Questions 740
Hands-On Projects 744
Case Projects 754

## APPENDIX A

### Red Hat Certified Technician Objectives

757

- Objectives Based on Course RH 033—Red Hat Linux Essentials 758
- Unit 1: Overview 758
- Unit 2: Command-line File System Browsing 758
- Unit 3: GNOME and KDE Desktops 759
- Unit 4: The Bash Shell 759
- Unit 5: Users, Groups, and Permissions 759
- Unit 6: vi and vim Editor Basics and Printing 759
- Unit 7: The Linux File System 760
- Unit 8: Configuring GNOME, KDE, and X-based Tools 760
- Unit 9: The Bash Shell and Configuration 761
- Unit 10: Advanced Topics in Users, Groups, and Permissions 761
- Unit 11: Advanced Uses of the vi and vim Editors 762
- Unit 12: Standard I/O and Pipes 762
- Unit 13: Introduction to String Processing 762
- Unit 14: String Processing with Regular Expressions 762
- Unit 15: Introduction to Processes 763
- Unit 16: Bash Shell Scripting 763
- Unit 17: Basic Networking Clients 763
- Unit 18: Programming and Administration 764
- Objectives Based on Course RH 133—Red Hat Linux System Administration 764
- Unit 1: Hardware, Device Configuration, and Installation 764
- Unit 2: Linux File System Management 765
- Unit 3: System Initialization and Services 766
- Unit 4: User Administration 766
- Unit 5: Network Configuration 767
- Unit 6: System Administration Tools 767
- Unit 7: RPM, Boot Loaders, and Kickstart 768
- Unit 8: Kernel Services and Configuration 769
- Unit 9: The X Window System 769
- Unit 10: Troubleshooting 769

## APPENDIX B

### Linux Professional Institute LPI Certification—Level 1 Objectives

771

- Objectives for Exam 101 772
- Topic 101 Hardware and Architecture 772
- Topic 102 Linux Installation and Package Management 774
- Topic 103 GNU and UNIX Commands 776
- Topic 104 Devices, Linux File Systems, and File System Hierarchy Standard 779
- Topic 110 The X Window System 781
- Objectives for Exam 102 782
- Topic 105 Kernel 782
- Topic 106 Boot, Initialization, Shutdown, and Run Levels 783
- Topic 107 Printing 784
- Topic 108 Documentation 785
- Topic 109 Shells, Scripting, Programming, and Compiling 786
- Topic 111 Administrative Tasks 786
- Topic 112 Networking Fundamentals 788
- Topic 113 Networking Services 790
- Topic 114 Security 792

## APPENDIX C

### SAIR/GNU Certified Linux Administrator (LCA) Level 1 Objectives 793

- Course 3X0-101—Linux Installation and Configuration 794
- 1.1 Theory of Operation 794
- 1.2 Base System 796
- 1.3 Shells and Commands 797
- 1.4 System Services 798
- 1.5 Applications 799
- 1.6 Troubleshooting 800
- Course 3X0-102: Linux System Administration 800
- 2.1 Theory of Operation 800
- 2.2 Base System 801
- 2.3 Shells and Commands 802
- 2.4 System Services 803
- 2.5 Applications 803
- 2.6 Troubleshooting 804
- Course 3X0-103 Linux Networking 804
- 3.1 Theory of Operation 805
- 3.2 Base System 806
- 3.3 Shells and Commands 807
- 3.4 System Services 808
- 3.5 Applications 809
- 3.6 Troubleshooting 809
- Course 3X0-104 Linux Security, Ethics, and Privacy 810
- 4.1 Theory of Operation 810
- 4.2 Base System 811
- 4.3 Shells and Commands 811
- 4.4 System Services 812
- 4.5 Applications 812
- 4.6 Troubleshooting 813

## APPENDIX D

### Linux+ Certification Objectives 815

- Domain 1.0 Installation 816
- Domain 2.0 Management 816
- Domain 3.0 Configuration 818
- Domain 4.0 Security 819
- Domain 5.0 Documentation 819
- Domain 6.0 Hardware 820

## GLOSSARY 821

## INDEX 843

## Introduction

Linux is now the fastest growing server operating system in the world, according to analysts such as IDG and Gartner Group, with a market share that has outpaced Macintosh. Millions of Internet sites and internal servers are run on Linux, and billions of dollars are generated in Linux-related revenue for companies like IBM, Hewlett-Packard, Dell, Red Hat Software, and others. Linux also continues to expand its technical prowess by adding high-end features and spreading globally into new market niches. Many world governments now mandate that Linux and other open source software be considered before money is spent on commercial alternatives. Because most networks include multiple operating systems, any system administrator planning for a long term career is well-advised to include Linux as a core competency to offer to potential employers, many of whom have already installed Linux and are looking for staff to maintain it.

This book guides you through the basics of Linux technology and trains you as a system administrator to maintain a Linux server that other users rely on for e-mail, Web, database, networking, or other system services. The book begins by introducing basic Linux concepts that may be unfamiliar to you, and then explains the installation and use of a Linux-based computer from the viewpoint of a system administrator.

This book cannot cover everything there is to know about Linux. Instead, it presents the basics of many areas, with enough theory and practice that, after reading it and completing the exercises and review questions included in each chapter, you should feel comfortable working on a Linux system and be able to locate additional utilities, and additional documentation about utilities, to enable you to progress in your knowledge of Linux (and in your career) with a solid foundation. Although this book was designed with a classroom setting in mind, nothing in it requires that setting, and many Linux users (the author included) were self-trained, without the guidance that a good instructor can provide. This book is based on a two-volume set: Guide to Linux Installation and Administration, Second Edition and Guide to Linux Networking and Security. It replaces the first volume and includes most of the core concepts and utilities of the second volume (it's also larger than either one alone); if you need more detailed information about networking and security, you should consult the second volume or another specialized text. This volume assumes you have never seen a Linux system, but that you are familiar with basic computer operation, such as entering commands, using a mouse to selecting graphical items on screen, and working with removable discs and CD-ROMs.

One aim of the material presented here is to prepare you to pass a Linux certification exam, which will demonstrate to potential employers that you have mastered important

theoretical and practical knowledge about Linux-based computers. Several certification programs for Linux are currently available. The material in this book maps to three of the most popular Linux certification programs: Red Hat Certified Technician (RHCT), Linux Professional Institute (LPI) Level 1, and Linux+ from CompTIA. It also maps to the first two (of four) exams of the SAIR/GNU Linux Certified Administrator Level 1 certification. The objectives for each certification program, Web site references where you can obtain official information, and cross-references to relevant chapters and sections in this book, are provided in the appendices to this book. These certification exams are generally multiple choice tests that you can take at a testing facility near your home or school after paying a fee. More advanced certification programs are available from Red Hat Software, LPI, and SAIR/GNU, but having any one of these certifications makes a very strong statement to potential employers about your knowledge of Linux.

The Red Hat certifications, which are generally considered the most challenging, are also more expensive and less widely available—they require that you perform hands-on system administration tasks in a lab setting. Because of this, and the market-leading position of Red Hat Software, the focus in this book has been on Red Hat’s products, specifically the Fedora version of Linux. Users will find that nearly all of the knowledge obtained in this book is easily transferred (usually with no modification) to other versions of Linux. The exceptions are Red Hat specific graphical utilities, which the reader may encounter in any event in a future job setting.

The inclusion of Fedora Linux in this book is a compromise of sorts. A more realistic training environment would suggest using Red Hat Enterprise Linux, which is the basis for the Red Hat Software certification exams and which is widely used in large organizations. Though the cost of Red Hat Enterprise Linux doesn’t permit its inclusion here, Fedora is the technology core from which Red Hat Enterprise Linux is taken. Fedora is a completely free operating system that can be downloaded from the Internet (see fedora.redhat.com). Except for technical support options and a few high-end management features (and the color of the installation screens), Fedora is similar enough to Red Hat Enterprise Linux to be considered a clone for training purposes.

This book uses an "onion skin" or layered approach to learning about Linux. Instead of beginning with a subject, such as user accounts, and disgorging all there is to know about them, leaving the reader with no context of when that information is useful (and perhaps little memory of it), this layered approach introduces a number of concepts on a superficial level, so that they fit together in a useful fashion. Other concepts are added, and the text then returns with more depth to explore important concepts that were introduced initially. Thus, for example, user accounts are mentioned in Chapter 1, explored more fully in Chapter 4, and are the subject of a "full" discussion in Chapter 11, once the context for the utilities and policies have been fully set out.
