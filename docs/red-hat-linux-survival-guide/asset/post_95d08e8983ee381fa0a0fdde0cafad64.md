
## Tell Us What You Think of This Book

If you are interested in communicating with me directly, send e-mail messages to kabir@evoknow.com. I will do my best to respond promptly.

## Acknowledgments

I want to thank both Red Hat Press and Hungry Minds teams, who together helped make this book a reality. It is impossible to list everyone involved, but I must mention the following kind individuals:

James Russell, the project development editor, who kept this project going. I don’t know how I could have done this book without his generous help and suggestions every step of the way. Thanks James.

Debra Williams-Cauley, the acquisitions editor, who provided me with this book opportunity and made sure I saw it through to the end. Thanks, Debra.

Gregory W. Stephens and Nancy Elizabeth Ellison, the technical reviewers, who provided numerous technical suggestions, tips, and tricks — many of which have been incorporated in the book. Thanks, guys.

Razib Quraishi, a friend and co-worker, who helped me with various aspects of writing this book. Thanks, Raz.

Sheila Kabir, my wife, who had to put up with many long work hours during the few months it took me to write this book. Thank you, sweetheart.

## Contents at a Glance

Preface .................................................... ix

Acknowledgments ............................................ xiii

## Part I: Installation and Basic Configuration ................. 1

- Chapter 1: Installing a Fresh Linux System .................... 3
- Chapter 2: Upgrading Red Hat Linux ........................... 35
- Chapter 3: Dual-Booting Red Hat Linux with Windows ........... 55
- Chapter 4: Booting and Shutting Down .......................... 67
- Chapter 5: Configuring the X Window System .................... 89
- Chapter 6: Setting Up Networking .............................. 117

## Part II: Getting Started ................................... 141

- Chapter 7: Managing Users ................................... 143
- Chapter 8: Working with Files and Directories ................. 167
- Chapter 9: Running Programs .................................. 195
- Chapter 10: Using the GNOME Desktop ........................... 223
- Chapter 11: Configuring the Kernel ............................ 237

## Part III: Configuring Services .............................. 279

- Chapter 12: The Apache Web Server .......................... 281
- Chapter 13: Configuring E-mail Services ....................... 357
- Chapter 14: Configuring FTP Services .......................... 395
- Chapter 15: Configuring DNS .................................. 435
- Chapter 16: Sharing Files and Printers with Windows ........... 493

## Part IV: Appendixes ........................................ 523

- Appendix A: Common Linux Commands ........................ 525
- Appendix B: IP Networking Basics ............................. 585
- Appendix C: Internet Resources for Linux ...................... 589
- Appendix D: Recovering from a System Crash .................... 597

## Index ...................................................... 601

## Contents

- Preface ............................................ ix
- Acknowledgments ........................................ xiii
- Part I: Installation and Basic Configuration ................ 1
- Chapter 1: Installing a Fresh Linux System ................ 3
  - Choosing an Appropriate Installation Source ................ 4
  - Meeting the System Requirements ................ 4
    - Workstation hardware prerequisites ................ 5
    - Server hardware prerequisites ................ 7
    - Laptop requirements ................ 8
  - Installing from Red Hat CD-ROM ................ 9
    - Choosing an installation interface ................ 9
    - Choosing the installation language ................ 10
    - Choosing your keyboard ................ 11
    - Choosing an installation type ................ 12
    - Partitioning hard disks ................ 13
    - Assigning mount points to partitions ................ 18
    - Choosing which disk partitions to format ................ 20
    - Passing extra information to kernel during boot ................ 20
    - Configuring LILO ................ 21
    - Configuring your network ................ 22
    - Configuring firewall ................ 24
    - Configuring mouse ................ 26
    - Configuring language of the operating system ................ 27
    - Configuring time zone ................ 27
    - Setting the root password and creating an ordinary user ................ 27
    - Configuring authentication options ................ 30
    - Selecting package groups to install ................ 30
    - Getting started with your coffee break ................ 31
- Chapter 2: Upgrading Red Hat Linux ................ 35
  - Upgrading Individual Software Package ................ 35
  - Upgrading using command-line RPM tool ................ 36
  - Upgrading using Gnome RPM tool ...................................39
  - Using Red Hat Network Update Agent ................................41
  - Upgrading the Linux Kernel .......................................51
    - Making a boot floppy ............................................51
    - Compiling a new upgrade kernel ..................................52
    - Configuring LILO to boot the new and the old kernels ............52
    - Rebooting the system ............................................53
    - Verifying the running kernel's version ...........................53

## Chapter 3: Dual-Booting Red Hat Linux with Windows ......55

- Dual-Booting with Windows NT/2000 ...............................55
- Prerequisites for dual-booting Linux and Windows NT/2000 .....56
- Dual-booting using LILO .......................................57
- Dual-booting by using NTLoader ................................60
- Dual-booting Linux with Windows 98 .............................63
- Booting Windows within Linux by Using VMware ...................64

## Chapter 4: Booting and Shutting Down .......................67

- Understanding the Boot Process ...............................67
- Understanding Run Levels ......................................69
- Booting Up Your System .......................................69
  - Booting to single-user mode ................................70
  - Booting in rescue mode .....................................70
- Shutting Down Your System ....................................72
  - Shutting down by using the shutdown command ...............72
  - Shutting down your system with init .......................73
  - Canceling a shutdown ......................................73
  - Automatic shutdown on power failure .......................73
- Rebooting Your System .......................................74
  - Rebooting with Ctrl+Alt+Delete ............................75
- Configuring init ............................................75
  - /etc/inittab: The init configuration file ................76
  - /etc/rc.d/rc.sysinit ......................................80
  - /etc/rc.d/init.d ..........................................80
  - /etc/rc.d/rc ..............................................81
  - /etc/rc.d/rc[0-6].d .......................................82
  - /etc/rc.d/rc.local ........................................82
  - /etc/rc.d/rc.serial .......................................83
- Managing init Files ...........................83
- Managing run levels with chkconfig ...................83
- Managing run levels with ntsysv ...................84
- Managing run levels with Linuxconf ...................85
- Creating a new service for a run level ...................85

## Chapter 5: Configuring the X Window System ............89

- What Is XFree86? ...........................90
- Preparing Your System for X ...........................90
- RAM requirements ...........................90
- Video card requirements ...........................90
- Monitor requirements ...........................91
- Disk space requirements ...........................91
- Installing X ...........................91
- Configuring X ...........................92
- Creating an XF86Config file using Xconfigurator ...........93
- Understanding the XF86Config file ...................99
- Starting X ...........................110
- Configuring .xinitrc ...........................111
- Customizing the look and feel of client applications ...........113
- Using xdm, the X Display Manager ...................113

## Chapter 6: Setting Up Networking ...................117

- Configuring a Network Interface ...................117
- Configuring a network interface card manually ...........118
- Configuring a network interface card using netcfg ...........125
- Why Use a Default Gateway? ...................130
- Dividing a Network into Subnetworks ...................132
- Gateway computer configuration ...................137
- Host computer configuration ...................138

## Part II: Getting Started ............141

## Chapter 7: Managing Users ...................143

- Becoming Root ...................143
- Using su to become root ...................144
- Creating multiple superusers ...................144
- Getting hacked by false superusers ...................145
- Using sudo to perform root tasks by ordinary users ...........147
- Managing Ordinary Users and Groups ...................150
