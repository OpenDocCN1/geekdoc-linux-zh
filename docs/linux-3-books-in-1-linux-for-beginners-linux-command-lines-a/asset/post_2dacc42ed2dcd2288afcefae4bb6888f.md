
## Uploading the SSH Key
## Securing SSH
## Creating a Firewall
## Removing Unused Network Services

## Chapter Five: Password Encryption Methods in Linux

- Pretty Good Privacy (PGP) and Public-Key Cryptography
- S/MIME, SSL and S-HTTP
- Linux IPSEC Implementation
- Secure Telnet (stelnet) and Secure Shell (ssh)
- Pluggable Authentication Modules or PAM
- CIPF or Cryptographic IP Encapsulation
- Using Shadow Passwords
- John the Ripper and Crack

## Chapter Six: Tools to Encrypt and Decrypt Password Protected Files

- GNU Privacy Guard or GnuPG
- Bcrypt
- Ccrypt
- 4-Zip
- Openssl
- 7-Zip
- Nautilus Encryption Utility

## Chapter Seven: Using Tools to Encrypt Files on Linux

- Tomb
- Cryptmount
- CryFS
- GnuPG
- VeraCrypt
- EncFS
- 7-zip
- Dm-crypt
- eCryptfs
- Cryptsetup

## Chapter Eight: Using Cryptsetup to Setup Encrypted Filesystems and Swap Space

- 1. Using a Drive, Loop Device, or Partition for Encryption
- 2. Installing cryptsetup
- 3. Adding Additional Layers of Security

## Chapter Nine: Using Access Control Lists in Linux

- 1. Introduction to Access Control Lists (ACL)
- 2. Uses of ACL
- 3. List of Commands to Set Up ACLs
- 4. Modifying the ACL
- 5. Viewing ACL
- 6. Removing ACL
- 7. Using Default ACLs

## Chapter Ten: Downloading and Installing Kali Linux

- 1. Downloading Kali Linux
- 2. Hard Disk Installation
- 3. USB Drive Installation

## Chapter Eleven: The Penetration Testing Life Cycle

- 1. The Five Stages of the Penetration Testing Life Cycle

## Chapter Twelve: Scanning

- 1. Network Traffic
- 2. Firewalls and Ports
- 3. PING

## Conclusion

## References

## LINUX

## LINUX FOR BEGINNERS

Andy Vickler

## Introduction

![](img/aae83b54a1b1783f3f5369bd9062b27c_13_0.png)

Linux is an operating system just like Windows, Mac OS, and iOS, but compared to Windows or iOS, Linux is very lightweight and very flexible. Today, Linux can be found everywhere, from smartphones to home appliances, cars to supercomputers, personal computers to enterprise servers. In this book, you will understand everything there is to learn about Linux and why it has become a preferred operating system for everyone, from students to enterprises and businesses.

Linux is the brainchild of Linus Torvalds, a computer science student who wanted to create an operating system that would be free, easy to use, and was capable of serving the needs of every individual in the world. Linux Torvalds was a user of the UNIX operating system and understood quickly that it could be improved to make life easier for everyone. He has proposed his changes to the developers of UNIX, who rejected it. That is when Torvalds decided to develop his own version of the UNIX operating system and call it Linux. He wanted to create an operating system that would take feedback from its users and implanted modifications to make life easy for every user. He collaborated with student programmers at MIT - Massachusetts Institute of Technology and, around 1991, launched a working version of the Linux operating system.

It has been a common misconception that Linux is a very technical operating system, and new users usually shy away from it. But the fact is that in recent years, Linux operating systems have become more user-friendly compared to their counterparts, such as Windows, MAC, etc. There are thousands of Linux distributions available today that can be customized as per a user's requirements and have even more software on them to make every task easy for a computer user.

This is what Linux is all about, an operating system that makes life easy for you. And this book will help you transition into the world of Linux comfortably; opening a new world of computing possibilities for you as you progress.

## Chapter One

## Introduction to Linux

## History of Linux

In the beginning, a computer would be as big as a car or a house. Naturally, it was a very complicated task to operate a computer. Every computer would have its unique operating system, which made it even more difficult to operate on them. Every operating system would have a specific purpose that would work on a particular computer and could not be used on another computer.

In 1969, a group of developers from Bell Labs decided to develop a common operating system that would work on every computer. They name this operating system ‘Unix.’ It has a recyclable code known popularly as a ‘kernel’ today that could be used with any computer. This code was also open-source in nature.

As the years passed, companies like IBM and HP started developing their versions of Unix in the 1980s. The multiple variants of Unix did not gain much popularity, though.

In 1991, a student named Linus Torvalds from the University of Helsinki in Finland envisioned an academic version of Unix and started writing his code. Linux developed a variant of the Unix operating system that is today known as the Linux kernel. This was the project that he started for fun, but little did he know that he was giving the world one of the most powerful tools that would be used forever.

## What is Linux?

Linux is a powerful operating system, just like Windows, Mac OS, and iOS. You would be surprised to know that the most popular mobile operating system, Android, is also powered by Linux. An operating system manages the hardware for any computing device such as a laptop, desktop, smartphone, tablet, etc. In simple words, an operating system handles all the communication between other software and the hardware of a system. Any software would cease to function in the absence of an operating system.

Numerous pieces make up the Linux operating system. Let us go through them one by one.

### Bootloader

The bootloader is a module that manages the boot process for a computer. You may have already encountered this without knowing much about it. It's usually the screen that pops up for a few seconds and then goes away when you switch on your computer.

### Kernel

The kernel is the fundamental unit of an operating system that controls your computer's Central Processing Unit (CPU), memory, and other devices.

### Init System

This is a section of the Linux operating system that controls the daemons. The most popular init system today is *systemd*. The systemd daemon manages the boot process after the bootloader passes the control over to it.

### Daemons

Some background services are initiated during the boot process in Linux. These are called daemons and comprise services such as sound, printing, scheduling, etc.

### Graphical Server

The Linux subsystem responsible for displaying the user interface on the monitor is known as the graphical server. It is also known as the X server or simply X.

### Desktop Environment

The section of the Linux operating system that users interact with is known as the desktop environment. Linux offers a variety of desktop environments, and every environment comes with a set of applications that a user would commonly need to get started with the operating system, such as configuration tools, file managers, games, web browsers, and more.

## Applications

A user will not find all the applications they need in the desktop environment by default. Linux has a huge list of applications that can be installed manually. Modern versions of Linux also have something like an app store where you can easily download and install an application.

## Why Should You Use Linux?

Almost every new user would have this question in their mind. Why should you use Linux when there are other operating systems like Windows and Mac OS already available? What is the need to learn about a completely new operating system architecture when the default operating system that comes with your laptop or desktop does the job?

We would like to answer this question by putting forward another question to you. Does the default operating system that comes with your computer work fine, or do you face challenges such as viruses, malware, slow speed, eventually? Also, do you get the default operating system for free, or do you have to pay for its licensing? If you struggle with these challenges, Linux is the perfect solution for you. It is a zero-cost operating system for any computer and is very reliable. Yes, it is completely free. You can install Linux on any number of computers without having to shell out a single buck.

If a free operating system is not enough to win you over, how about an operating system that works without any issues forever? For over a decade, I have used Linux for both personal use and as a server system without a single issue of malware, ransomware, or viruses. Linux is not very vulnerable to these attacks. Servers using Linux operating systems need a boot only when the software is updated, and they can go without a reboot for years without causing any performance issues.

## Open-Source

We mentioned the word *open-source* earlier. What exactly does open-source mean? Open-source refers to the following aspects.

- You can use the software for anything
- You can study the software and have the liberty to make changes
