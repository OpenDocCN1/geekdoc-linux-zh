
## Part V Programming Linux

- 29 Using Perl....775
- 30 Working with Python....801
- 31 Writing PHP Scripts....821
- 32 C/C++ Programming Tools for Fedora....865

## Part VI Fedora Housekeeping

- 33 Securing Your Machines....889
- 34 Performance Tuning....901
- 35 Command-line Masterclass....915
- 36 Advanced Yum....941
- 37 Managing the File System....951
- 38 Kernel and Module Management....993

## Appendix

- A Fedora and Linux Internet Resources....1019
- Index....1031

## Table of Contents

### Introduction

- What Is Linux? 2
  - What Is Fedora Core? 2
  - Roots of Red Hat and Fedora 3
  - Licensing 4
- Why Use Linux? 5
- Who This Book Is For 6
- What This Book Contains 7
- Conventions Used in This Book 9

## Part I Installation and Configuration

### 1 Introducing Fedora

- What Is Fedora Core? 15
  - Inside Fedora Core 15
  - Features of the Fedora Install 18
  - Fedora File System Features 19
- Fedora for Business 20
- Fedora in Your Home 21
- 64-bit Fedora 22
- Getting the Most from Fedora and Linux Documentation 23
- Fedora Developers and Documentation 24
- Reference 25

### 2 Preparing to Install Fedora

- Planning Your Fedora Deployment 28
  - Business Considerations 28
  - System Considerations 29
  - User Considerations 30
  - A Predeployment Planning Checklist 30
  - Planning the Installation 31
- Hardware Requirements 32
  - Meeting the Minimum Fedora Core Hardware Requirements 32
  - Using Legacy Hardware 33
  - Planning for Hard Drive Storage for Your Fedora 34
  - Installation Class 34
  - Checking Hardware Compatibility 35
- Preparing for Potential Hardware Problems 36
- Preparing and Using a Hardware Inventory 39
- Preparing for the Install Process 42
- Preparing to Install from a CD-ROM 44
- Partitioning Before and During Installation 44
  - Choosing a Partitioning Scheme 46
  - Hosting Parts of the Linux File System on Separate Partitions 46
- Using Fedora’s Kickstart Installation Method 47
- Reference 50

### 3 Installing Fedora

- Before You Begin the Installation 53
  - Research Your Hardware Specifications 53
  - Choose an Installation Type 54
  - Choose Software Installation Options 54
  - Planning Partition Strategies 54
  - The Boot Loader 56
- Choosing How to Install Fedora 57
  - Installing from CD or DVD 57
  - Installing Using a Network 58
- Step-by-Step Installation 59
  - Starting the Install 60
  - Partitioning Your Drive 65
  - Choosing, Configuring, and Installing the Boot Loader 69
  - Network Configuration 70
  - Firewall and Security Configuration 71
  - Setting the Time Zone 72
  - Creating a Root Password and User Accounts 73
  - Software Selection and Installation 74
  - Creating a Boot Disk 75
  - Finishing the Install 77
  - Logging In and Shutting Down 77
- Reference 78

### 4 Post-Installation Configuration

- Troubleshooting Post-Installation Configuration Problems 81
- Your Hardware and Kudu 82
- Pointer and Keyboard Configuration 84
  - Configuring Keyboards with Linux 84
  - Configuring Pointing Devices in Fedora 88
- Configuring Display Graphics 93
- Configuring Sound Devices 95
- Detecting and Configuring a Modem 96
  - Configuring a Serial-Port Modem 96
  - Configuring a Fax Modem 99
  - Configuring minicom for Modem Use 99
  - Configuring WinModems for Laptops 100
- Configuring Power-Management in Fedora 101
- Resetting the Date and Time 103
  - Using the date Command 104
  - Using the nwclock Command 104
  - Using the system-config-date Client 104
- Managing PCMCIA 106
  - Using PCMCIA 106
  - Controlling PCMCIA Service 107
- Configuring and Using CD, DVD, and CD-RW Drives 108
  - Checking Drive Assignment 108
  - Initializing FireWire CD Drives 110
- Reference 114

### 5 First Steps with Fedora

- Working with the Linux File System 118
  - Viewing the Linux File System 119
  - Use Essential Commands from the /bin and /sbin Directories 121
  - Store the Booted Kernel and View Stored Devices in the /boot and /dev Directories 122
  - Use and Edit Files in the /etc Directory 122
  - Protect the Contents of User Directories—/home 125
  - Use the Contents of the /proc Directory to Interact with the Kernel 125
  - Work with Shared Data in the /usr Directory 127
  - Temporary File Storage in the /tmp Directory 127
  - Access Variable Data Files in the /var Directory 128
- Logging In to and Working with Linux 128
  - Text-based Console Login 128
  - Working with Virtual Consoles 129
  - Using Simple Keyboard and Mouse Techniques in a Linux Console Session 129
  - Logging Out 131
  - Logging In and Out from a Remote Computer 131
- Changing Your User Information 133
- Reading Documentation 135
  - Using man Pages 135
  - Finding and Reading Software Packages Documentation 136
- Using the Shell
  - Using Environment Variables
  - Navigating and Searching with the Shell
  - Managing Files with the Shell
  - Compressing and Decompressing Files Through the Shell
- Using the Text Editors
  - Working with vi
  - Working with emacs
- Working with Permissions
  - Assigning Permissions
  - Directory Permissions
  - Understanding Set User ID and Set Group ID Permissions
- Working As root
- Creating Users
- Deleting Users
- Shutting Down the System
- Rebooting the System
- Reference

## Part II Fedora Desktop

### 6 The X Window System

- Basic X Concepts
- Using X11R6
- Elements of the xorg.conf File
- Configuring X
- Starting X
  - Using a Display Manager
  - Starting X from the Console by Using startx
- Selecting and Using Window Managers
  - Using Fedora's switchdesk
  - The Tab Window Manager (*twm*)
  - The Motif Window Manager (*mwm*)
- The GNOME and KDE Desktop Environments
  - GNOME: The GNU Network Object Model Environment
  - KDE: The K Desktop Environment
- Reference

### 7 Managing Software and System Resources

- Using RPM for Software Management
- Command-Line and Graphical RPM Clients
- Using rpm on the Command Line
