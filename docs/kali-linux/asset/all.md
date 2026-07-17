![](Images/cover00148.jpeg)

Kali Linux

Simple and Effective Approach to Learn Kali Linux

© Copyright 2019 by Ethan Thorpe - All rights reserved.

This document is geared towards providing exact and reliable information in regards to the topic and issue covered. The publication is sold with the idea that the publisher is not required to render accounting, officially permitted or otherwise qualified services. If advice is necessary, legal or professional, a practiced individual in the profession should be ordered.

- From a Declaration of Principles which was accepted and approved equally by a Committee of the American Bar Association and a Committee of Publishers and Associations.

In no way is it legal to reproduce, duplicate, or transmit any part of this document in either electronic means or in printed format. Recording of this publication is strictly prohibited, and any storage of this document is not allowed unless with written permission from the publisher. All rights reserved.

The information provided herein is stated to be truthful and consistent, in that any liability, in terms of inattention or otherwise, by any usage or abuse of any policies, processes, or directions contained within is the solitary and utter responsibility of the recipient reader. Under no circumstances will any legal responsibility or blame be held against the publisher for any reparation, damages, or monetary loss due to the information herein, either directly or indirectly.

Respective authors own all copyrights not held by the publisher.

The information herein is offered for informational purposes solely and is universal as so. The presentation of the information is without a contract or any type of guarantee assurance.

The trademarks that are used are without any consent, and the publication of the trademark is without permission or backing by the trademark owner. All trademarks and brands within this book are for clarifying purposes only and are owned by the owners themselves, not affiliated with this document.

Table of Contents

[Introduction](#part0000.xhtml__Toc26861472)

[Chapter 1: Getting Started With Kali Linux](#part0000.xhtml__Toc26861473)

[What is Kali Linux?](#part0000.xhtml__Toc26861474)

[Installing and Preparing Kali Linux](#part0000.xhtml__Toc26861475)

[Installing Kali Linux Using USB-Method](#part0000.xhtml__Toc26861476)

[Dual Boot Kali Linux Installation](#part0000.xhtml__Toc26861477)

[Installing Kali Linux on Hyper-V](#part0000.xhtml__Toc26861478)

[Starting Installation Process](#part0000.xhtml__Toc26861479)

[ARM Installations](#part0000.xhtml__Toc26861480)

[Kali Linux Features](#part0000.xhtml__Toc26861481)

[Is Kali Linux For You?](#part0000.xhtml__Toc26861482)

[Chapter 2: Getting Started With Hacking](#part0000.xhtml__Toc26861484)

[What is Hacking?](#part0000.xhtml__Toc26861485)

[Learning About Types of Hackers](#part0000.xhtml__Toc26861486)

[Hacking Consequences](#part0000.xhtml__Toc26861487)

[Victims](#part0000.xhtml__Toc26861488)

[Chapter 3: The Hacking Process](#part0000.xhtml__Toc26861490)

[Information Gathering(Reconnaissance)](#part0000.xhtml__Toc26861491)

[Types of Reconnaissance](#part0000.xhtml__Toc26861492)

[Scanning](#part0000.xhtml__Toc26861493)

[Gaining Access](#part0000.xhtml__Toc26861494)

[Maintaining Access](#part0000.xhtml__Toc26861495)

[Clearing the Tracks](#part0000.xhtml__Toc26861496)

[Chapter 4: Learning About Cyber Security](#part0000.xhtml__Toc26861498)

[Why Cyber Security is Important](#part0000.xhtml__Toc26861499)

[Learning About the CIA Triad](#part0000.xhtml__Toc26861500)

[What Challenges Does the CIA Triad Bring?](#part0000.xhtml__Toc26861501)

[Different Types of Cyber Threats](#part0000.xhtml__Toc26861502)

[Why is Cyber Security Important?](#part0000.xhtml__Toc26861503)

[Chapter 5: Learning about Debian Connection](#part0000.xhtml__Toc26861505)

[How Packages Flow From Debian to Kali Linux](#part0000.xhtml__Toc26861506)

[How is The Debian Difference Managed?](#part0000.xhtml__Toc26861507)

[Chapter 6: Linux Fundamentals Refresh](#part0000.xhtml__Toc26861509)

[Understanding Linux](#part0000.xhtml__Toc26861510)

[Kernel Powering Hardware](#part0000.xhtml__Toc26861511)

[A Working File System](#part0000.xhtml__Toc26861512)

[Process Management](#part0000.xhtml__Toc26861513)

[Command Line: Interface To Talk To Your System](#part0000.xhtml__Toc26861514)

[Command Line Basics](#part0000.xhtml__Toc26861515)

[Filesystem Hierarchy Standard](#part0000.xhtml__Toc26861516)

[Home Directory](#part0000.xhtml__Toc26861517)

[Learning More Useful Commands](#part0000.xhtml__Toc26861518)

[Chapter 7: Kali Linux Configuration](#part0000.xhtml__Toc26861520)

[Network Configuration](#part0000.xhtml__Toc26861521)

[Configuring Network Using Command Line](#part0000.xhtml__Toc26861522)

[Using systemd-networkd](#part0000.xhtml__Toc26861523)

[Unix Groups and Users Management](#part0000.xhtml__Toc26861524)

[Getent Command](#part0000.xhtml__Toc26861525)

[Changing or Modifying an Account](#part0000.xhtml__Toc26861526)

[Account Disabling](#part0000.xhtml__Toc26861527)

[Use Groups Management](#part0000.xhtml__Toc26861528)

[Configuring Services](#part0000.xhtml__Toc26861529)

[PostgreSQL Database Configuration](#part0000.xhtml__Toc26861530)

[Apache Configuration](#part0000.xhtml__Toc26861531)

[Managing Services](#part0000.xhtml__Toc26861532)

[Chapter 8: Understanding Kali Linux Community and Documentation](#part0000.xhtml__Toc26861534)

[Documentation Sources](#part0000.xhtml__Toc26861535)

[Learning About Info Documentation](#part0000.xhtml__Toc26861536)

[Community-Driven Kali Linux](#part0000.xhtml__Toc26861537)

[Become Part of the Community: Do Bug Reports](#part0000.xhtml__Toc26861538)

[Chapter 9: Kali Linux Monitoring and Security](#part0000.xhtml__Toc26861540)

[Security Policy For The Rescue](#part0000.xhtml__Toc26861541)

[Data Confidentiality](#part0000.xhtml__Toc26861542)

[Extreme Cases](#part0000.xhtml__Toc26861543)

[Approach](#part0000.xhtml__Toc26861544)

[Security Measures](#part0000.xhtml__Toc26861545)

[How To Secure Network Services](#part0000.xhtml__Toc26861546)

[Getting Your Firewall To Work: Packet Filtering](#part0000.xhtml__Toc26861547)

[Logging and Monitoring](#part0000.xhtml__Toc26861548)

[How to Detect Changes](#part0000.xhtml__Toc26861549)

[Chapter 10: Debian Package Management](#part0000.xhtml__Toc26861551)

[APT Introduction](#part0000.xhtml__Toc26861552)

[Different Package Licenses](#part0000.xhtml__Toc26861553)

[Kali Repositories](#part0000.xhtml__Toc26861554)

[Basic Package Interaction](#part0000.xhtml__Toc26861555)

[Kali Linux Upgrade](#part0000.xhtml__Toc26861556)

[Purging and Removing Packages](#part0000.xhtml__Toc26861557)

[Learning About Package Contents](#part0000.xhtml__Toc26861558)

[Troubleshooting Packages](#part0000.xhtml__Toc26861559)

[Chapter 11: Kali Linux And Security Assessment](#part0000.xhtml__Toc26861561)

[Preparing Kali Linux for Security Assessment](#part0000.xhtml__Toc26861562)

[The Different Types of Security Assessments](#part0000.xhtml__Toc26861563)

[Vulnerability Assessment](#part0000.xhtml__Toc26861564)

[Compliance Penetration Test](#part0000.xhtml__Toc26861565)

[Traditional Penetration Test](#part0000.xhtml__Toc26861566)

[Application Assessment](#part0000.xhtml__Toc26861567)

[Chapter 12: Server And Network Scanning - How To Find And Secure Network Vulnerabilities](#part0000.xhtml__Toc26861569)

[Asking the Right Questions](#part0000.xhtml__Toc26861570)

[Thinking Like A Hacker](#part0000.xhtml__Toc26861571)

[Create A Map Of Publicly Available Information](#part0000.xhtml__Toc26861572)

[Reinforcing All The Weak Links and Vulnerabilities](#part0000.xhtml__Toc26861573)

[Chapter 13: Kali Linux Tools](#part0000.xhtml__Toc26861575)

[Nmap - The World’s Most Famous Network Mapper Tool](#part0000.xhtml__Toc26861576)

[Fierce - Network Mapping & Port Scanning Tool](#part0000.xhtml__Toc26861577)

[Unicornscan - Information Gathering & Data Correlation Tool](#part0000.xhtml__Toc26861578)

[Wireshark - Network Analyzer](#part0000.xhtml__Toc26861579)

[Aircrack-ng - Wireless Security Software Suite](#part0000.xhtml__Toc26861580)

[Kismet Wireless - Wireless LAN Analyzer, Sniffer, and IDS](#part0000.xhtml__Toc26861581)

[John The Ripper - Cryptography Testing Tool](#part0000.xhtml__Toc26861582)

[BeEF - Browser Exploitation Framework](#part0000.xhtml__Toc26861583)

[Yersinia - L2 Attacks](#part0000.xhtml__Toc26861584)

[DHCPig - DHCP Exhaustion Application](#part0000.xhtml__Toc26861585)

[THC Hydra - For Brute Force Crack Remote Authentication Services](#part0000.xhtml__Toc26861586)

[Metasploit Framework - Penetration Testing Suite](#part0000.xhtml__Toc26861587)

[FunkLoad - Web-Stress Tool](#part0000.xhtml__Toc26861588)

[SlowHTTPTest - Web-Stress Application For HTTP Servers](#part0000.xhtml__Toc26861589)

[Inundator - Multi-Thread IDS Evasion Security Tool](#part0000.xhtml__Toc26861590)

[Social Engineering Toolkit](#part0000.xhtml__Toc26861591)

[OpenVAS - Vulnerability Scanning Tool](#part0000.xhtml__Toc26861592)

[Nikto - Helps In Full Web Server Scans](#part0000.xhtml__Toc26861593)

[WPScan - Auditing Tool For WordPress Security](#part0000.xhtml__Toc26861594)

[CMSMap - A Centralized Security Solution For All Popular CMS](#part0000.xhtml__Toc26861595)

[Choose The Right Tool And Reinforce Your Network Security](#part0000.xhtml__Toc26861596)

[Conclusion](#part0000.xhtml__Toc26861598)

Introduction

Welcome to Kali Linux: Simple and Effective Approach To Learn Kali Linux. In this book, you will learn about Kali Linux and how to utilize it effectively. Both intermediate and beginner users can use the book by empowering them with the skills to use Kali Linux effectively.

In this book, we will learn about Kali Linux, its purpose, its effect on the hacking scene, the installation process, and other important concepts surrounding it.

Hacking has become a major point of interest for students or professionals who are fascinated by zeroes and ones.

BackTrack, Offensive Security writes Kali Linux. It contains tools and mechanisms that let you tinker with networks, computers, and security. Currently, Kali Linux offers 300+ tools that can be used for vulnerability assessment, password cracking, wireless hacking, and much more! Kali Linux is the house to the most popular tools, including Wireshark, Metasploit Framework, Nmap, Aircrack-ng, John the Ripper, and others!

To get started, we recommend you to have a basic working knowledge of Linux OS or operating system in general. If you are completely new to Linux OS or computers, then we recommend learning basic computer skills or Linux before proceeding with the book. However, if you are ambitious, you can read and implement the ideas shared in the book while learning Linux.

All the topics covered in the book are covered from the perspective of beginners. We start by looking at how to install Kali Linux properly. Our methods will include creating a dual boot or creating a virtual machine in Windows 10\. Both methods are covered to ensure a proper learning experience. In the later part of the book, our focus will shift to cyber security, hacking, or the tools that Kali Linux has to offer.

Also, our focus will be mainly on ethical hacking. But that doesn’t mean that we will not cover some of the black hat techniques.

At the end of the book, you will be equipped with the skills to make the most out of the Kali Linux, understand hacking, vulnerability, and be ready to protect your own installation.

# Chapter 1: Getting Started With Kali Linux

Kali Linux is one of the leading Linux distros out there. It is mainly used for hacking purposes. The hacking part can be both black hat and white hat(we will cover the different types of hackers in detail later on). As a learner myself, I have always wondered what makes Kali Linux so interesting. That encouraged me to write the book, and here we are!

## What is Kali Linux?

Kali Linux is a Linux operating system. It is based on Debian. The main purpose of Kali Linux is security. It is used for penetration testing and security auditing. This also makes it an ideal tool for hackers who have malicious intent.

The main thing that makes Kali Linux is the tools that it has to offer. It has tons of tools that are pre-installed. The tools can be used to perform various information security tasks. For instance, it lets you do reverse engineering, security research, computer forensics, and so on. Currently, it has more than 600 plus penetration testing programs. The number of tools will continue to grow as more research is done in the security domain.

Offensive Security manages the Kali Linux distribution. It is a leading information security training company. They now manage the funding that goes into making Kali Linux, the best Linux distribution for penetration testing and digital forensics. The two main persons behind the project include the Devos Kearns and Mati Aharoni of the Offensive Security. Another developer that made an impact is Raphael Hertzog, a Debian expert.

All of these make Kali Linux a perfect too to learn about hacking or pen-testing. You can choose how you want to use it.

The evolution of Kali Linux started with the demise of BackTrack Linux in 2013\. The project was re-booted into Kali Linux in March 2013 while maintaining the Debian development standards.

Kali Linux is also well known for supporting the Metasploit Project. The project is used for security exploit development and execution. 

## Installing and Preparing Kali Linux

Before we get started, we need to prepare Kali Linux. Installing Kali Linux is easy. Also, Kali Linux can be installed in two ways. You can install it on a separate hard disk using a USB drive or simply use a virtualization solution to virtualize the operating system.

*   USB Method
*   USB method dual boot installation
*   Virtualization method (VMware or Hyper-V)

If you are new to virtualization, let me explain it to you in simple words. Virtualization is a method through which an operating system or software is given its own separate virtual resources to run on an already existing operating system/device/solution. There are many virtualization solutions out there, including VMware. Many big companies rely heavily on virtualization techniques. Even cloud companies use virtualization to provide cloud computing to its subscribers. The hosting company also have virtualization ingrained into their services. By now, you should know that virtualization is a big thing, and it is!

If you are using Windows 10, the latest iteration of Windows, then you can use virtualization to install Kali Linux. Windows 10 has been slowly accepting Linux, and that’s why in 2016, they introduced their own Hyper-V solution for virtualization. If you are using the latest Windows 10 version or 1803 version or above, your Windows should come pre-equipped with Hyper-V software.

Let’s first learn how to install Kali Linux using the USB-drive method. But, before we do, check out the minimum requirements to install Kali Linux.

*   A USB-drive bootable media or DVD bootable media
*   20 GB minimum hard disk space
*   Kali Linux ISO.

You can download the Kali Linux ISO from the official Kali Linux website, [www.kali.org](http://www.kali.org). There you can find all the download options under the Kali Linux Downloads: [https://www.kali.org/downloads/](https://www.kali.org/downloads/). I also recommend you to use torrents to download it as you will get better speeds doing so.

From there, you should choose the Kali Linux 64-bit. For this book, we are going to use the 2019.3 version. I recommend you to download the same version as I did. This way, you can easily follow the tutorials and methods shared in the book. However, if you opt to download a slightly different version(especially the latest version), you will do just fine.

## Installing Kali Linux Using USB-Method

Installing Kali Linux to a bare-bone machine with no pre-installed operating system is easy. All you need is to make a bootable pen-drive or use a DVD installation drive. To make a bootable pen-drive, you need to follow the steps mentioned below.

*   Download the Kali Linux ISO
*   Now, download Rufus.
*   Once you downloaded Rufus, install it on your machine. In case you do not have a working machine, you should take help from a colleague or a friend who can do it for you.
*   Now, turn on Rufus, and it will look below.

![](Images/image00144.jpeg) 

*   Your Pendrive will showcase in the device section. In boot selection, you need to select the Kali Linux image. To do so, you need to click on SELECT and then choose the downloaded Kali Linux. In the partition scheme, you should leave it at MBR. The target system should be “BIOS or UEFI.”
*   When it comes to advance drive properties, you can leave the default settings as it shows.
*   Once every setting is set correctly, click on the Start button.
*   Now, wait for Rufus to complete the process.

With the USB drive ready, you now need to boot from it. All you now to do is follow the installation steps, as shown by the installation wizard.

## Dual Boot Kali Linux Installation

Dual-booting Kali Linux is very similar to the above process. Here, you need to make sure that you have enough room for installing the Kali Linux. A different partition(even on the same hard disk) will work. However, if you lack space, then you need to use a tool known as GParted. The tool gives you the ability to shrink the Windows installation and make space for the Kali Linux installation. To do a proper dual boot Kali Linux installation, you need to follow the steps mentioned below:

*   You first need to boot from your USB drive or the choice of your medium installation. Once you are in the Kali Linux boot screen, you now need to select “Live.” This will book the Kali Linux default desktop.
*   From there, you need to launch GParted program. The GParted program is useful in shrinking Windows partition. With this, you can successfully install Kali Linux in limited space.
*   Once GParted starts, you need to select the Windows partition and then right-click on it. Then click on “Resize/Move.” Make sure that you have 20 GB of installation size for Kali Linux.
*   After you select the changes, now click on “Apply All Operations.”
*   Once it is completed, now you need to boot the Kali Linux again and select the Guided -- use the largest continuous free space as the partition disk.
*   After the installation is done, the system will reboot, and you can finally boot into Kali Linux using a GRUB boot menu.

## Installing Kali Linux on Hyper-V

Now, we will learn how to install Kali Linux on Hyper-V. This is my recommendation when it comes to learning Kali Linux. Remember, this book focuses on learning Kali Linux, and it is best to virtualize.

### Enabling Hyper-V On Your Machine

Hyper-V offers virtualization in the Windows environment. To enable Hyper-V, you need to have the following requirements.

*   A SLAT(Second Level Address Translation) supported 64-bit CPU.
*   Virtualization support. Basically, it should be SVM mode for Ryzen chips and VT-c for Intel chips
*   4 GB minimum RAM.

Even though virtualization is supported on your machine, it needs to be enabled first before you use it. To enable it, you need to go to your BIOS and enable virtualization. I am using a decent mid-range rig with AB350 and Ryzen 1600\. For my machine, I have to go the CPU advanced feature, and then enable the SVM mode there. In cases where virtualization still doesn’t work on your system, you need to allow the enforced hardware Data Execution Prevention setting in your BIOS.

To check if your machine is now virtualization ready, especially for using Hyper-V solution, run the following command.

*   Run command prompt
*   Run systeminfo.exe command on the command prompt
*   Press Enter

You will see a positive reply from the command.

Enabling hardware-based virtualization is not enough. Windows, by default, doesn’t run the Hyper-V modules. To allow them to, you need to go to the Control Panel and search for the “Turn Windows Features on or off.”

There you will find the Hyper-V option, along with two options: Hyper-V Platform and Hyper-V Management Tools. Enable both the options and click OK to proceed.

Once done, you need to reboot and then move on to the actual installation process.

## Starting Installation Process

*   For this, we recommend going through the Quick Create option. Once you open Hyper-V, you will find the Quick Create option from the menu.
*   You will then be greeted with the Create Virtual Machine window. There you will find few options, including Ubuntu 18.04.3 LTS and Ubuntu 19.04.
*   Here you need to click on the “Local installation source” first and then move to “Change installation source.”
*   From there, select the Kali Linux ISO. Also, untick the “This virtual machine will run windows option.”
*   Once done, click on the “Create Virtual Machine” button.
*   It will then prompt you to Connect to your New Virtual Machine. Close the prompt and then right-click on the New Virtual Machine you just created and chose “Setting.”
*   Now, from there, go to the SCSI connector and then choose a hard drive.
*   From here, you need to click on “New” if you want to change the location of your virtual disk. This is important as, by default, the vhdx file is stored within the C: drive.
*   Click on “Connect.” Once done, you will now see the Kali Linux Live Boot Menu, as shown below.

![](Images/image00145.jpeg)

Here you can see the Live system option. The live system option is useful for using the Kali Linux without the need for installation. This is okay for testing out a feature, but it is not user-friendly as it doesn’t save the work environment settings or the work you have actually done. This makes working with installed Kali Linux a good idea.

To start the installation, you need to press Enter on start installer option. Once done, it will start the installation using the installation wizard.

A glimpse of what steps it will follow in the install process is as below.

![](Images/image00146.jpeg)

Let’s list the steps below to ensure proper installation.

*   Select the language of your choice for the installation process. It will also ask you the language choice for the installed system. We are going to choose English for both options.
*   Select your location, depending on where you stay.
*   It will then ask you to configure the keyword. Choose the keyboard layout that you like.
*   After that, it will load installer components from the source. In our case, it is an ISO. The wizard will also configure the network.
*   Once done, you need to choose a hostname for your system. It is a single word hostname. It will automatically pick Kali as the hostname, and we recommend you to use it as it will help you to follow the book contents easily. It will also ask you to choose a domain name. The hostname is optional.
*   Now, you need to choose a root password. Root passwords are a must, and you need to make sure that you choose one before you proceed. Now, choose a strong password that is hard to guess or crack. Also, make sure that you do not forget the password later on as it will make your Kali Linux installation inaccessible.
*   It will now ask you to set your time zone.
*   Now, it comes to configure your partition disks. Kali Linux or any Linux installation has a different file system, and hence, they might seem completely different from any other OS installation, especially Windows OS installation. To make sure that you do not have to do much, you can choose Guided - use entire disk option. As we are using virtualization, we do not have to worry about partitions as Hyper-V has already allocated a unique hardware location for our OS installation.
*   Once you select the guided partition, it will ask you to choose the partition scheme. It includes the following:

1.  All files in one partition(for new users)
2.  Separate /home partition
3.  Separate /home, /var, and /tmp partitions

As you are new to Kali Linux, we recommend using the first option.

Lastly, it will give you an overview of the partitions that are created. If everything looks fine to you, it is now time to click on choose “Finish partitioning and write changes to disk.”

*   Now choose Yes to proceed
*   Now you have to wait for the installation to complete.

## ARM Installations

In this section, we will discuss how to do ARM installations. ARM stands for Advanced RISC Machine. Some of the examples of the ARM-based devices include embedded computers, developer boards, laptops, and so on.

If you wish to install Kali Linux on ARM devices, then you cannot use the normal Kali Linux installation that we discussed just above. For the devices, you need to configure the kernel to make the boot loader work.

To get started, you need to use the Offensive Security scripts aimed at ARM devices. Check the link to download script: [https://gitlab.com/kalilinux/build-scripts/kali-arm](https://gitlab.com/kalilinux/build-scripts/kali-arm)

For ARM devices, you also need to use other installation images([https://www.offensive-security.com/kali-linux-arm-images/](https://www.offensive-security.com/kali-linux-arm-images/))

Once you have downloaded the image and the script, follow the steps to complete the Kali Linux installation on ARM-based devices.

*   Check if the checksum is matching with what you have downloaded. You can do it using the checksum tools available online.
*   Once you are sure you have downloaded the right image, then you need to acquire a storage device depending on what your ARM has to offer. You also need to make sure that the storage device has at least 8 GB of storage capacity.
*   Now copy the image to the storage device of your choice using the dd. You can also use Rufus to copy the image.
*   If you are using dd, you need to use the following command.
*   Next, you need to insert/plug the storage to your ARM device
*   Once done, log in using the credentials, user → root, and password → toor. Once connected, generate new SSH keys and root password.
*   Your ARM device is now ready to be used!

## Kali Linux Features

Until your installation is done, let’s quickly go through the features, which makes Kali Linux a great choice.

### Open source

Kali Linux is licensed under the Open Source model. It brings multiple benefits, including the ability to use it for free. The open-source community around Kali Linux is also strong, and we also see many developers contributing to it.

### Free to use

Kali Linux is free to use. This makes Kali Linux the number one choice for pen-testers. It comes with all the necessary things that you will need to work optimally. All of these without paying a single penny.

### Penetration testing tools

Another great feature of Kali Linux is its collection of penetration testing tools. It has more than six hundred penetration testing tools! That’s a huge number considering the scope of each tool's capabilities. Also, each tool included in the release is unique in its own ways. Tools that replicate or duplicate other tools functionalities are eliminated.

### FHS compliance

It follows the Filesystem Hierarchy Standard, which is also used by other Linux distros, including Ubuntu distro. As a user, you benefit from it as it allows you to carry your FHS knowledge from one distro to another. You do not have to re-think where you can find the libraries, binaries or other files.

### Custom kernel

Kali Linux kernel is custom made and includes the latest injection patches. It is frequency patched and also developed securely.

### Wireless device support

Not all Linux distros come with wireless support. However, Kali Linux comes with wireless device support. It is developed in such a way that it comes equipped with hundreds and thousands of devices compatibility.

### Language support

It supports many languages out of the box.

### GPG signed

All the packages used in Kali Linux are GPG signed, which means that the packages are secure and are made based on the standard protocols.

### Customizable

Kali Linux is highly customizable from the core. It is developed in such a way that it can meet every user requirement. The customization needs to be done on top of the kernel.

All these features make Kali Linux different from other Linux distros. First of all, it is a single user, i.e., root. This means that all the critical changes can only be made through root user. It also means that it is a single-user operating system. This is a good approach considering that most of the tools require high-level access. Apart from that, network services come disabled so that you can install applications without much difficulty. Lastly, it comes with minimal repositories which ensure better system integrity.

## Is Kali Linux For You?

Before we move into learning Kali Linux, we need to learn whether Kali Linux is the right choice for you. It is common for learners to choose an operating system only to find out that it is not for them. The book is for Kali Linux, but as a learner, you should make sure that you really need Kali Linux.

First of all, Kali Linux is not for normal users. It is an operating system that especially for penetration testing. This means if you want to become a security specialist or are already a one, you have made the right choice in learning or using Kali Linux. However, it is not a good choice for doing other development things or using it as a normal day-to-day activity.

Another thing that makes Kali Linux so amazing is its production value. Only a few veteran people are in a position to update the project. You can suggest new changes, but these veteran people decide if changes are made to it or not. Initially, the developer signs the repositories, which is followed by the entire team signature. As a user, this means you have restrictions when it comes to adding or customizing packages. So, if you wish to add a package, you need to do a lot of research and patience to accomplish it.

So, does it mean it is for you? To ensure that you are going the wrong path, ensure that you do not choose Kali Linux in the following case:

*   You have never used a Linux operating system before.
*   You do not understand basic administration knowledge or have no OS experience at all
*   If you think you are going to use Kali Linux as your daily driver when it comes to doing daily activities such as browsing the web, watching videos, or gaming.

Also, you should learn about the legal terms that come when it comes to doing unauthorized penetration testing on networks. If you make changes that damage a computer or network, you might get in trouble. Law enforcement against these kinds of activities is pretty strong, and you should know it beforehand then repent later.

However, if you are someone who wants to make computing safe for everyone, then Kali Linux is for you. You know your way when it comes to use penetration testing tools and have proper authorizing while doing your activities.

## Things We Learned in This Chapter

*   Kali Linux is used for penetration testing purposes.
*   It is managed by Offensive security
*   It offers a great collection of tools for penetration testing and hacking
*   Kali Linux development started form 2013 from BackTrack Linux project
*   It supports the Metasploit project
*   It offers a perfect playground to develop, execute, and test security exploits solutions.
*   Installing Kali Linux is easy. You can choose between the USB method(with or without dual boot) and the virtualization method.
*   Virtualization is best suited for learning as you do not have to go through the problems of dual booting. But, you can install standalone Kali Linux if you want.
*   Hyper-V lets you install Kali Linux directly into the Windows 10\. You need to have the Windows 10 1903 version or above to use it.
*   The installation process requires a careful setup that you need to follow
*   Kali Linux key features include custom kernel, FHS compliance, language support, free to use, open-source, customizable, GPG signed, and so on!

# Chapter 2: Getting Started With Hacking

As we already learned, Kali Linux is mainly used for hacking. And, that’s why we need to cover the topic in detail. We need to learn what is hacking, types of hackers, and the path you should take. We will also learn the role of Kali Linux in making you a security expert.

## What is Hacking?

Hacking is an activity that is done by hackers, which involves modification of a system, service, or solution. It can be done in a subversive manner, where the hacker can have authorized or unauthorized access.

However, in general space, hacking is always seen as a bad thing. It is all about doing criminal activity, including gathering information or data unauthorized, hacking security systems, or transferring a huge amount of money from a bank account. Even though they are an example of hacking, they do not confine what actually hacking is.

Currently, hacking can be related to multiple definitions. The best way we can define is hacking as “being creative.” Hacking is not only a computer-related activity. It is an activity that is carried out in our daily lives. If you modify or transform an object or process to the way you want -- that can be termed as hacking.

Hacking in computer terminology is exploring for vulnerability -- using it or fixing it. The world of cybersecurity runs on finding vulnerabilities and solving them so that anyone using that service or solution are safe. Computer hacking has now become one of the biggest skills to have. It is now performed by certified professionals who know what they are doing. This also gives rise to different types of hackers, including white hat, black hat, and gray hat hackers. The approach, motivation, and method of penetration determine their type.

You may find hackers and crackers confusing. Crackers are hackers but only do specific types of activity, including breaking passwords, bypassing software access, or going around computer security.

## Learning About Types of Hackers

There are three different types of hackers. These include the following.

*   Black Hat Hacker
*   White Hat Hacker
*   Gray Hat Hacker

### Black Hat Hacker

Black hat hackers are hackers who do hacking in an unethical way. Most of the time, the black hat hackers are new learners in the pen testing or cybersecurity field. Their eagerness to learn about hacking is what makes them use a more unethical approach. They are also not trained when it comes to hacking ethics. Also, lack of guidance and mentorship means there are more chances that they will pick up black hat hacking.

They do their activities without proper authorization and gain access to the system, either destroying them or gaining them to further their work. Black hat hackers are also known for blackmailing the owner for paying a ransom. This is a serious crime as it includes two offense - black hat hacking and blackmailing.

Most of the time, black hat hacking is all about feeling good about yourself. It can be defined as a selfish act where they are okay with harming others for their own achievements. Their approach is what defines them, and if they use unethical ways, they are simply harming others by their actions. This doesn’t end here as black hat hackers also continue to use the data they collect. They either sell the data in the black market(deep web) or use the data to further their black hat hacking.

Black hat hackers mostly work in groups. And, there are chances that many governments have their own set of black hat hackers to gain an advantage when it comes to ruling the world. But, in no circumstances, the action of black hat hackers can be justified as they always do unauthorized hacking.

### White Hat Hacker (Ethical Hackers)

White hat hackers work completely different from that of black hat hackers. White hat hackers are ethical in their approach and never do unauthorized access. They are more creative and know how to access networks or computers in different ways. They use their knowledge to look out for exploits or weaknesses and then fix them. If they do not know how to fix an exploit, they will simply inform the person who is the owner of the service, product, or solution.

White hat hackers are only different in their ethics. They use the same approach as that of black hat hackers. Their tools are the same, and there are chances for their skills to be the same.

It is not easy to become a white hat hacker as it requires tons of patience and training in both technical and ethical sense. Also, there is no single path to become a white hat hacker. There are many instances when a black hat hacker becomes a white hat hacker during his/her career. The opposite is also true where hackers change from white to black. Also, white hat hackers are commonly known as “Penetration Testers.” Their job is to find vulnerabilities in networks, machines, or solutions before they get exploited. Almost every tech company has its team of penetration testers as they want to make their products as secure as possible.

### Grey Hat Hacker

Grey hat hackers are hackers that lies between the white hat hacker and black hat hacker. They use both black hat and white hat techniques. Grey hat hackers are also inclined towards the good side but are not 100% committed in their approach.

The grey approach is mostly used by learners who want to improve themselves. They often do some unethical things, but also want to ensure that they inform the company about the vulnerability. Grey hat hackers thrive on problem-solving, and even companies are willing to pay them if they report the vulnerabilities. There are bounties that companies put if someone finds a vulnerability and report it to them. Grey hat hackers are also not inclined towards stealing data or making money.

Also, becoming a grey hacker is completely optional, and you can still create your own playground to test your skills and improve, rather than trying out your skills on other’s networks or computers.

## Hacking Consequences

Hacking can be a fascinating thing to do, especially for new learners, but it comes with its consequences. The consequence of unauthorized access can vary depending on the situation. In many cases, hackers, once caught, are prosecuted according to law. The laws are also not light when it comes to hacking. The criminal charges can be big, depending on the hacking done. For example, if you hacked a financial institute, you are bound to get a severe penalty, including serving in jail and paying a hefty amount. This is done to ensure to discourage hackers from doing unethical hacking.

But not all hacking is bad. White hat hackers or ethical hackers are at the core of good hackers. There are also cases where white hat hackers are caught doing unethical hacking. In those cases, their punishment depends on their actions and contributions they have made to the community.

## Victims

If you are going to do penetration testing with Kali Linux, you should also learn about the victims of your actions. If you are on the right path, then there is no need to worry, but what happens if you try to be unethical? Who will be your victims?

The victims can be anyone who is on the internet. There are hundreds of instances where hackers hack personal photos and post them on social media, embarrassing the said person. The hacker can also blackmail the person. In fact, the number one activity that hackers do is identity theft. They hack a person's account and copy all their photos and information. Once they are done, they create a similar profile and try to act as that said person. Another common activity is to do credit card theft and unauthorized payments.

## Things We Learned in This Chapter

*   Hacking is a process of getting access or stealing data to/from a system, process, or solution without authorized access.
*   Hacking can also be defined as a creative process of breaking things and gaining access to them.
*   There are three types of hackers including black hat hackers, white hat hackers, and grey hat hackers
*   Black hat hackers are hackers that choose an unethical path. Their main aim is to use exploits to steal data or gain access to a system.
*   White hat hackers(Ethical hackers) work to protect systems, solutions, and services from hackers. They follow an ethical route.
*   Grey hat hackers is a middle path between black and white hat hackers. Generally, they hack systems, only to inform the organization about the flaw so that it can be fixed.
*   There are hacking consequences if you take the unethical road. So, always beware of them.
*   Victims can be anyone who gets hampered because of the actions of hackers.

# Chapter 3: The Hacking Process

Kali Linux is a hacker tool. If you choose Kali Linux, I hope you know by now that you are going to use it for hacking or penetration testing. That’s why you need to learn about the hacking process. The hacking process can be applied to most of the hacking attempts and can be used as a framework. These steps will guide you to become better at hacking(both ethical and unethical).

The key five steps that are present within a hacking process include the following:

*   Information Gathering (Reconnaissance)
*   Scanning
*   Gaining Access
*   Maintaining Access
*   Covering Tracks

Let’s go through each of the steps in detail.

## Information Gathering(Reconnaissance)

The very first step that you are going to do is information gathering. It is the most important part of the hacking process. And, most of the time, it gets ignored. The information-gathering process is known as reconnaissance. In this step, your job is to gather as much information as you can — the more useful information you have, the better the chance of success of the hacking process. The information you gathered in your very first step will help you in all the next four steps, including scanning, gaining access, maintaining access, and covering tracks.

As a hacker or a learner, you may find the information gathering step a little boring -- as it has basically no need for the technical tools. Most of the time, you have to keep staring at the system and try to find information. You need to decide which information is useful to you. In terms of tools, you might need to use one. And, when it comes to techniques, there are quite a few of them out there that you need to learn.

## Types of Reconnaissance

Reconnaissance can be done in two types. To help you understand the concept, we will go through each of them one by one.

### Passive Reconnaissance

In passive reconnaissance, your work is to not interact with the system directly, but passively try to gather information. So, if you want to find loopholes in a system, you may want to go to the company’s website, learn about who they are hiring, understanding what technologies they are using, and so on. By doing so, you can learn about the company without trying to interact with the system you want to hack.

To get started, you can use Google to your advantage. There, you can find public records. To learn more about the company, you may want to do a WHOIS search. It will help you know about more data, the hosting they are using, and other important details.

Next, you can also try to research about the client to which the company works with. Also, try to find which employees are working on which project or at least try to find their most valuable employee. This information might seem insignificant but can be game-changing in the later phase of your hacking process.

Social Engineering is also a great technique that you can use. In social engineering, you simply stole the identity of a person and then used the identity to gain information from other people. This way, you might get access to a company’s account that the employee uses. Social engineering is a very powerful tool, but you should be very cautious before you start doing it. If you make a single mistake, your cover will be blown, and it will become harder for you to get into the system or gather more critical information.

The best way to approach social engineering is to make fake social media profiles and connect with people you think that you can get more information. Social engineering can also be done through calls. It might look a little intimidating initially, but with practice, you will become more successful in doing so.

Dumpster Diving is a technique where you look for information from the discarded place. You can gain information from the documentation that is dropped in the trash can. For example, you can gain access to an ATM slip, and from there, you can learn about the person’s transaction information. You can also gain access to phone numbers or even bank statements.

### Active Reconnaissance

Active reconnaissance is the complete opposite of passive reconnaissance. It requires active engagement with the system. The target needs to be clearly defined, and you should actively search for the system. But, active information gathering is more challenging than passive ones. One of the ways is to take help from an employee of the company. May be asking them to let you go through the normal process of using the solution/software. You may also want to go through their documentation(if they have any) and try to learn about their system as much as you can.

With active reconnaissance, you need to do the following:

*   Check if the system responds from external ping
*   If the system is not responding to ping, then you need to find other ways to interact with the system.
*   Work directly with the system by creating accounts, accessing their payment system, and more!
*   Try all the different ways to connect with the server. However, be very wary of how you do your interaction as it can activate the safety mechanisms of the system and flag your identity.

## Scanning

The next step in the hacking process is scanning. The scanning phase includes heavy use of tools. The scanning tools will help you further refine the information you gather from the reconnaissance phase. As a hacker, you need to use a variety of tools, including port scanners, ping tools, sweepers, vulnerability scanners, and network mappers. The network scanning is important as it will help you gain access to the system(the next step).

Learning about the list of open ports is also vital, as well. It will also inform you about more information, including the operating system being used. Also, the response type will be different depending on the operating system or the response ports that are open on the platform. So, if you are trying to access a Linux based operating system, you will get a different response.

Another technique you need to follow is "sniff" network packets. There are many tools out there that will let you do it. However, I recommend you use Wireshark, the number one tool used to analyze traffic. Once the phase is completed, you should be able to understand the whole network structure.

At the end of the scanning, you have the following things

*   More vital information, mostly technical
*   Proper network map
*   Open ports
*   Type of operating system used
*   Find any possible vulnerability

Also, you need to make sure that you have all the information in one single place. By doing all of this, you will be able to make sense of the data, and also remove or separate data that you think is less important.

## Gaining Access

With all our information gathering done, we are now ready to gain access to the target system. Until now, we have a good amount of information in our hands. This information will help us to gain access. Our information contains network mapping, logging information, and other vital information.

The goal is to take advantage of the vulnerabilities to gain access to the target system. If you were successful in finding a vulnerability and use it correctly, you should be able to get access to the system.

However, finding vulnerability is not easy, and you might need to do additional penetration testing to find a path. Also, it is the most important aspect of your hacking process. Without direct access to the target system, you simply cannot do anything. That makes finding vulnerability so important as it gains access to the target system.

So, what methods you can use to gain access? Actually, there are many ways you can do so. If you were successful in your social engineering technique, you might get a direct username and password to enter the system. That would be awesome! However, that’s extremely rare. In most cases, you need to find the vulnerability on the application hosted on the system. Otherwise, you need to find the vulnerabilities with the system version.

Few of the techniques that you can use are as follows:

*   Make Denial of Service attack
*   Use Session Hijacking

Denial of Service attack will not enable you to get access to the system but will allow you to expose the vulnerability of the system.

Once you find at least one vulnerability, you should be able to get into the system. However, the time to break in depends on how robust their security system in. Most companies invest heavily in their security aspects. They do have white hat hackers, and their job is to protect the system at any cost. If they find someone accessing the system unauthorized, then they will try to prevent it. It is better to be pre-equipped with this type of threat. As a hacker, it goes a long way to learn the working time for the white hat hackers and only try to get access to the system when you think that there are very minimal chances of you getting caught or defined the entry to the system.

If you are a grey hat hacker yourself, then you might want to report the vulnerability to the company. You can also continue with the process and may be reported later with more details about the vulnerability. The choice is yours.

Gaining access can also take some time to accomplish. Most of the hackers give up at this point. But, if you are determined, then you will eventually get into the system.

Another thing that you need to keep track of is human errors. They are pretty common, and you can find your way by capitalizing on the errors. Humans are prone to make mistakes. They lack 100% attention when doing tasks, which results in loopholes. These loopholes can be both technical and non-technical in nature.

## Maintaining Access

Once you get access to the system or the network, you now need to maintain access to it. This part is as challenging as getting access to the network. The networks/system have their own custom-made firewalls which continuously monitor the network for any anomalies. Some firewalls come equipped with advanced systems powered by the latest technologies. This makes maintaining access to one of the hardest steps in the hacking process.

The best approach is to ensure that you do not get identified as a rogue in the system. Also, to maintain access to the system, you need to include a backdoor or trojan into the system. A rootkit can also help you keep access to the system in the future.

Another approach is to infect other applications and machines within the network. The more infected machines there are, the better you have chances to maintain access now and in the future. However, do not go overboard with it. Always maintain a low-key and only infect machines in small numbers so that the host system does not get suspicious about your presence within the network.

Once you establish access, now you need to monitor emails, system login information, and other important things. You can also monitor the network traffic and modify them according to your requirements. The best approach to gather information from a particular terminal or machine is to equip it with a keylogger. This way, you can get further access to specific accounts, giving you more control over the network.

The goal is to keep yourself hidden within the system for as long as you can. You need to be slow and steady in your approach. Initially, you can simply observe the different workings of the system. Once you are confident about how the system/network work, then you can go and infect the environment.

## Clearing the Tracks

The last step of the hacking process is clearing your tracks. As a hacker, you do not want to get exposed, especially if you are doing black hat hacking. We already discussed how severe punishments could be, and if you are doing black hat hacking, you are exposing yourself to risks. To protect your presence in the long run, you need to hide your tracks or at least clear them so that no one knows that you ever accessed the system.

The main goal is to hide from the IT professionals that maintain the system. You should also think like a white-hat hacker and protect yourself against his techniques of finding you.

If the white hat team or the IT professional knows that someone is accessing the system unauthorized, then they would kick you out of the system, making you lose access to the system. This means no future access to the system, as well.

The best approach is to override the log mechanisms of the system. Logs offer different information about how the system works. This means you can remove your entries from the log. You can automate the system to do so. The logs are commonplace for white hat hackers who are looking for anomalies within the system.

By clearing your tracks, you are ensuring two things:

*   Keeping long access to the system
*   Ensuring you do not get caught and gets prosecuted

This leads us to the end of our hacking process steps. We went through it as it is important to learn Kali Linux. Kali Linux is a penetration testing operating system, and even if you are going to be a white-hat hacker, you need to know how the hackers work and think.

## Things We Learned in This Chapter

*   In this chapter, we learned solely about the hacking process.
*   The five critical steps of a hacking process include Information Gathering, Scanning, Gaining Access, Maintaining Access, and Covering Tracks.
*   In the information-gathering step, you need to gather as much information as possible using techniques.
*   There are two types of reconnaissance - passive and active.
*   In passive reconnaissance, you can use techniques like social engineering and dumpster diving.
*   In the active reconnaissance, you need to use techniques like scanning and tool as well.
*   To gain access, you need to find a vulnerability in the system and use it to your advantage. You can also use techniques including Denial of Service and Session Hijacking to reveal the issues with the system.
*   Once you gain access, you need to maintain Access to it. You can do it by staying low, deleting entries in the log files, or installing malware.
*   Lastly, you need to clear tracks so that you can have access to the system in the long run.

# Chapter 4: Learning About Cyber Security

Not everyone is on the dark side. Many people want to make the world a safer place. As a learner who is interested in Kali Linux, you also need to get yourself equipped with the cybersecurity terminology and knowledge.

We will keep this chapter short, and soon after this, we will move into the realms of Kali Linux. The fact that learning Kali Linux is not all about tools; you need to have the proper background knowledge to use them properly.

So, what is cybersecurity?

Cybersecurity is an ecosystem where you can find the practices, processes, and technologies used to protect a wide array of devices, programs, networks from malicious actors, and unauthorized access. It is also known as information technology security

## Why Cyber Security is Important

Cybersecurity is important to our society. With the introduction of computers and the internet, we slowly moved to the information technology era. Our lives are now deeply connected with information technology as we store, process, and retrieve data online.

Governments, medical organizations, military, and others heavily dependent on computers. Cybersecurity is used to keep all of them safe. Organizations have critical data stored in their server. This critical data is important for the organization as it gives them a competitive edge. If the data gets leaked, then they will lose the competitive edge and market share. Governments also have tons of sensitive information that needs protection. Cybersecurity is what protects them from leaking. Governments are also keen to invest heavily in intelligence, protect their sensitive information while looking for information to protect the countries interest.

## Learning About the CIA Triad

At the core of cybersecurity, we have the CIA triad. It is a fundamental concept that keeps the cybersecurity ecosystem working. Without any of the three elements in the CIA triad, there would never be a secure system.

The three elements are as below

*   Confidentiality
*   Integrity
*   Availability

If we want to explain the three elements in short, then you can confidentiality can be explained as a set of rules for information access; integrity is related to data accuracy and trustworthiness, whereas the availability makes sure that the data is available reliability for authorized people only.

Let’s go through them below.

### Confidentiality

The first element of the CIA triad is confidentiality. In other words, it is related to privacy. By maintaining confidentiality, a system ensures that the user’s privacy is maintained at any cost. It also ensures that the owner only accesses sensitive information, and malicious actors cannot access it.

Confidentiality rules can differ based on the data type and owner status. The categorization is done based on how intense the damage can be if the data falls in the wrong hands.

Confidentiality is hard to implement. To make it work, people need to be trained. This training ensures that the security risks associated with the data are reduced. One of the biggest security threats are humans itself. If they are not trained, they are more likely to leave loopholes open for hackers to exploit. They need to learn how to set strong passwords and how to keep the password secure. These best practices will also ensure identifying social engineering attempts. The social engineering method tries to pursue people to give up on their information, including passwords.

When it comes to the technical aspect, confidentiality is maintained with the use of cryptography. The hardened encryption ensures that the username and passwords are not leaked online by hackers. Companies need to store the data securely, and that’s what makes it more challenging — the other types of verification types, including security tokens, biometric verifications, soft tokens, and so on.

### Integrity

The second element in the CIA triad is integrity. It is all about the data trustworthiness, accuracy, and consistency through the data life cycle. This means that the data should not be modified or changed by unauthorized access or malicious actors. Most of the time, if the confidentiality breaks, the integrity of the data breaks too.

To maintain integrity, it is necessary to use access control to ensure that only authorized users can access the data. Also, the integrity needs to be checked and verified through methods, including cryptographic checksums or hash numbers, and so on.

Some of the algorithms used for checking data integrity include SHA1, SHA2, SHA3, SHA5, and MD5.

### Availability

The last trait is the availability trait. The data stored should be available at all times. The data that is not available is useless. To achieve 100% availability, the hardware manufacturers need to maintain their hardware and immediately repair them if any issues occur. They also need to focus on the software, or the operating system used so that the requested data can be served to the user in the best possible way.

Another big requirement is to provide enough bandwidth for optimal availability. Just having availability is not enough, and it is required to serve the data to the user in a well-defined time that is justifiable.

Other key aspects that need to be maintained include RAID, redundancy, failover, etc. A proper disaster recovery system ensures that none of the data is lost. It also makes sure that data delivery is not hampered in different scenarios.

Data availability also needs to be maintained during the denial-of-service(DoS) attacks. The best approach is to have proper firewalls and proxy servers to make the service work in the worst condition.

The two best ways to provide data availability is redundancy and backup.

## What Challenges Does the CIA Triad Bring?

Even though the CIA triad can seem a simple thing to achieve, in reality, it is just the opposite. It uses big data, and other technologies make the CIA paradigm a tough thing to maintain. Big data is all about collecting important data from a variety of data sources. This can add unwanted cost and makes it even harder to maintain the CIA triad.

Other technologies also pose their own issues. For example, IoT brings a new whole level of challenge. Connecting different devices together through a different medium, interface, and networks is in itself a challenge. Now, protecting data confidentiality, integrity, and availability is much bigger a challenge. IoT is not as secure as other technologies.

## Different Types of Cyber Threats

Cyber threats are at the core of cybersecurity. As a Kali Linux user, you also need to learn about the terminologies. The hackers are keen to use any form of cyber attack to get access to the system. To make sure that you know about the attacks, let’s list them below.

### Malware

One of the most common cyber attacks is the use of malware. It is a software that is used to gain system access. It can also be used to cause harm to the system without the owner’s prior knowledge.

### Social Engineering

Social engineering is a non-technical threat where a person tries to impersonate and gather information through social skills. It is all about psychologically manipulate people.

### Advanced Persistent Threats

Advanced persistent threats are used by unauthorized users to maintain access to networks or systems for a more extended period.

### Ransomware

Ransomware is a new type of malware. It is used mainly to ask for ransom from an affected computer. The extortion starts after the target machine is infected with malicious software. The software can lock important files in the system and then ask for money in exchange for unlocking them. Many ransomware would lock users completely out of their system. Even after the user agrees to pay the amount, the hacker might keep a backdoor to the system so that he can infect other computers in the network. He can also try to infect the system again after some time.

### Phishing

The last type of cyber attack that we want to discuss is phishing. It is a common attack that begins with fake emails. The emails are then used to gather key information, including credit card numbers or login information. The best way to protect against is to have proper filter mechanisms in the email service.

Other types of cyberattacks include the following:

*   Man-in-the-middle(MITM) attack
*   SQLi attack
*   Denial-of-service(DoS) attack
*   XSS Cross-Site Scripting attack
*   Distributed denial-of-service(DDoS) attack

There are other cyber attacks other than the above attacks. The type of attack depends on the devices and the network that the hacker is trying to hack.

Let’s try to explain these types of attack in simple terms below.

### Man-in-the-Middle (MITM) Attack

It is a popular attack that is often used in hacking devices. In this attack, a third-party malicious actor gains access to talk between two other parties. By doing so, it can steal information and use that information to harm the victims.

### SQLi Attack

In the SQLi attack, the hacker tries to execute malicious SQL statements on the database. If the hacker can execute them successfully, then he gains access to the database or the system. There are plenty of ways to protect the database against his common cyber-attack.

### Denial-of-Service(DoS) Attack

This is also one of the most common cyber-attacks out there. It takes place by jamming a network or service to provide the service. A large number of machines are used to carry out DoS attacks. DoS attack's main aim is to disrupt service and also reveal a weakness in the system. If multiple machines make the attack, then it is known as a distributed denial-of-service(DDoS) attack.

### XSS Cross-Site Scripting Attack

Cross scripting attack(XSS) is a web application vulnerability where the web pages are injected with client-side scripts.

## Why is Cyber Security Important?

Cyber security’s importance is paramount in our society. Every organization requires proper security to their systems. Without it, they will fall apart. Every institution also requires basic cybersecurity. In fact, individuals also need basic cybersecurity protection so that they do not become victims to hackers who may want to do Ransom or want to cause any harm to them.

Cybersecurity can be seen as an infrastructure -- a layer of protection that works on every single device and location. A unified system always works great in the world of different systems. The integrations, however, require work, and that can leave some loopholes.

Another thing is that anything can never be 100% secure. This means that the cybersecurity field is always a growing field. New technologies and evolutions take place almost every year, which makes it even harder for cybersecurity specialists to make the work safer.

## Things We  Learned in This Chapter

*   Cybersecurity deals with the protection of the organization, governments, medical organizations, and other institutions against cyber attacks and malicious actors.
*   There are CIA Triad that is at the core of cybersecurity. It includes confidentiality, integrity, and availability.
*   Confidentiality deals with the user’s privacy. It is all about maintaining the user’s privacy at any given cost. It protects sensitive information and is hard to implement in any system.
*   Integrity, the 2nd CIA triad, deals with data accuracy, consistency, and trustworthiness during the data life cycle.
*   Availability, the third CIA triad, is all about 100% system or data availability at any condition or scenario.
*   There are many challenges the CIA triad brings to the table.
*   There are many types of cyber threats, including malware, social engineering, advanced persistent threats, ransomware, phishing.
*   Other types of common cyber attacks include SQLi attack, Man-in-the-middle(MITM) attack, SQLi attack, XSS Cross-Site Scripting attack, Denial-of-service(DoS) attack.
*   Cybersecurity attack is important because it deals with the security of multiple organizations, system, and the overall ecosystem in which the internet thrives.

# Chapter 5: Learning about Debian Connection

Kali Linux is a genuine Debian derivative. The work on Kali Linux started in 2012\. Its connection to Debian is important to learn as it will make you understand its importance and also understand how it works.

More specifically, it is based on top of Debian Testing. This means that the packages that you see in Kali Linux are from Debian repository -- not all, but most. However, do not make the confusion that Kali Linux is dependent on Debian. Kali Linux has its own infrastructure when it comes to packaging selection and distribution. The user can choose whatever he wants and has the complete freedom to do so.

## How Packages Flow From Debian to Kali Linux

As we already mentioned that the packages flow from Debian distribution to Kali Linux. This is done properly.

The Debian gets updated by contributors daily. They update packages and also ensure that the packages get updated to the unstable Debian distribution. Once the packages are uploaded, it is then moved to the Debian Testing distribution. This is where all the bugs are removed, and the packages are then made available for release.

Debian testing is the best playground for Kali Linux as their goals are aligned.

The contributors of Kali Linux then take a two-step process to include the packages.

The first step is to force-inject the Kali packages to the Kali-dev repository. This can break the repository, but that’s the expected outcome. To make it work, the next step is to make sure that the new packages are recompiled along with the old ones to make it work.

Kali Linux also has a distribution named “Kali-rolling,” which can be used by the users to track all the changes that are made to the Kali-dev distribution. The end goal is to ensure that all dependencies are met before packages are migrated.

## How is The Debian Difference Managed?

The difference is mostly managed by reducing the number of forked package. This is done to ensure that Kali’s unique features are implemented correctly. The upstream packages are modified minimally. If you want to learn about the difference between Debian and Kali Linux packages, you can check out their Kali Package Tracker([https://pkg.kali.org/derivative/kali-dev/](https://pkg.kali.org/derivative/kali-dev/)).

## Things We  Learned in This Chapter

*   Kali Linux and Debian are closely related.
*   Packages flow from Debian to Kali Linux.
*   Kali Linux has a distribution known as “Kali-rolling” that deals with the changes made to the distribution packages.
*   If the packages are good, they are then moved to the main Kali distribution.

# Chapter 6: Linux Fundamentals Refresh

As a reader, you might not be completely informed about Linux. If you want to master Kali Linux, you first need to be comfortable with Linux. Learning Linux is not hard, and if you learn it, you will be able to understand most of the internet as servers, web, and other services use Linux servers to operate.

## Understanding Linux

We can define Linux as an operating system, but in reality, it is simply an operating system kernel. A kernel is a collection of files, libraries, and features that makes an OS work. It acts as a mediator between the software and the hardware and provides you the means of exploring your computer. A kernel is responsible for managing users, file system processes, hardware, and permission system. All the system related activities run in ring zero, which is also known as kernel space. On the contrary, Linux also has user space, which is defined as the space where everything other than kernel activities takes place.

## Kernel Powering Hardware

The number one task for kernel is to make sure that the hardware works as intended. It controls hardware components and configures them. So, if you plug in a USB drive, then it is the kernel who will identify the hardware and make it ready for use. One more thing that the kernel does is to make the hardware available to high-level software. In simple words, it acts as a bridge using a programming interface. The clear winner in this is applications as they get access to a virtual extension to utilize the resources.

The new hardware is detected with the help of /sys/ and /proc/ virtual file systems. The applications, on the other hand, need to access /dev/ as files are created there.

Everything in Linux is a file. This means that hardware is also represented as a file. For example, the disk drives are represented as /dev/sda. The partitions, on the other hand, are represented as /dev/sda1.

The device files, however, can be of two types, character and block. They are defined based on the method of how the information is stored or retrieved. A block is fixed in nature, and bytes can be accessed from any given block position. The character file, on the other hand, acts as a flow of characters.

A block file is represented by b in front of the permissions, whereas the character file is represented by c.

## A Working File System

The file system is also at the core of the Linux operating system. It is a feature that the kernel offers out of the box. The file system is inherited from the Unix kernel. Everything is located within a single directory, and it is known as the root. “/” character is used to represent the root directory. All the directories are contained within the root directory, where it creates a hierarchical tree.

An example of a subdirectory within the root directory is /home directory. The home directory contains user-specific files. It is also hierarchical and contains more sub-directories and files. So, if you create a file on your desktop, it will be stored within the desktop subdirectory present within the /home directory. The unified file system is used by major Linux distributions allowing easy data management. So, for instance, if you know about one Linux distribution, then you would be effectively able to use other distribution. It only uses one such hierarchy. It doesn’t matter how many disk drives or partitions you are using, it can list all the directories and subdirectories in a single hierarchy and under the /root.

If you are using multiple disks, then one disk is assigned as /root, whereas the other disks are named as ext2, ext3, and so on.

## Process Management

The kernel is also well-equipped with process management features. Any program in its running state is known as a process. The process makes sure that the program instance runs as intended. To do so, it uses memory. The kernel, in this case, makes sure that it creates and tracks the process. The memory management is also done by the kernel while ensuring that there is enough memory for the optimal work of the system. Once it allocates the memory, it then loads the executable file into the memory and starts running it. To make sure that it can track and manage the process, a process identifier(PID) is also allocated to the process.

Linux is a multitasking operating system. This means it is equipped with features to manage multiple applications running at the same time. It simply manages the memory and processor time allocation for each process, giving the illusion that it is multitasking. In general, it only runs one program at a time. Even though, in the background, it manages multiple processes in the dormant stage. Once a user changes to a background process, then it re-assigns resources to the said process.

## Command Line: Interface To Talk To Your System

Command-line is the way you can interact with the system. There are different types of terminals, but Kali Linux utilizes the GNOME terminal. To access the terminal, you need press CTRL + ALT + T. You can also access the terminal by typing “terminal” on the search bar in Kali Linux.

Once you start your terminal, you can now use commands on it. Let’s start with the ls command.

ls command lists all the files and directory at the location it is run.

As you can see, you need to provide input to the command line prompt. Once done, shell -- a command-line interpreter will then execute the input. In the case of Kali Linux, the default shell is Bash shell. Bash stands for Bourne Again Shell. If you see either $ or # at the beginning, it means the shell is waiting for your input.

## Command Line Basics

Let’s go through the commonly used Linux commands. These commands will let you optimally use the operating system.

pwd → Show you the current working directory

cd [directory_name] → use to change directory

cd . → go back one directory

cd .. → go back two directories

ls → list files and folders

mkdir [directory_name]→ create new directory

mv [directory_name] → move directory

rmdir [directory_name] → remove directory

I would also suggest you to read free online tutorials on the Linux command line. There are plenty of good tutorials out there that are worth your time. Always remember, that without proper working knowledge of Linux, it is next to impossible to learn Kali Linux, forget mastering it.

## Filesystem Hierarchy Standard

As we already discussed that the Kali Linux utilizes a unified file system known as the Filesystem Hierarchy Standard(FHS). To make sure that you work effectively with the Kali Linux OS or any distro, the knowledge of the FHS can help you engage with the OS. With this knowledge, you can easily get around Linux OS and know the purpose and use of each directory. Let’s list them below.

*   /boot/: contains files for the boot process
*   /dev/: contains device files
*   /bin/: contains basic programs
*   /etc/: configuration files
*   /opt/: third party applications
*   /root/: personal files for administrator
*   /home/: home user’s personal files
*   /media/: removal devices for mount points
*   /mnt/: temporary mount point
*   /lib/: basic libraries
*   /run/: contains runtime data, gets removed after reboot
*   /srv/: server hosted data on system
*   /sbin/: contains system programs
*   /tmp/: temporary files are stored here
*   /var/: variables used by daemons while running. It can include caches, queues, spools, and log files.
*   /sys/ and /proc/ used by Linux Kernel and is not part of FHS
*   /usr/: contains applications and architecture-independent data

## Home Directory

The home directory is also an important part of any Linux OS. However, it doesn’t contain any standardized elements, but it does contain some of the interesting stuff that you should know.

The home directory is mostly referred to as “~” tilde sign. This makes it easy for the user and as well as the command interpreters as they can change the tilde sign to the home directory.

To know the value of the home directory, you need to check the environmental HOME variable. In most cases, it is set to “/home/user.”

In the home directory, you can find the application configuration files. Also, the files contained within the home directory can be hidden by default. The files that are hidden start with . (dot), signifying that it is hidden. If you want to see all files including hidden files, then you need to use the ls command with the -a option as below.

ls -a

The configuration files used by programs and services can be multiple files. This can lead to issues as to where the configuration files are stored. To ensure that this doesn’t happen, XDG Base Directory Specification is followed. This ensures that the files have a clean structure attached to it -- the place they are stored. For instance, the cache files always need to be stored within ~/. cache, the configuration files in ~/. config, and so on.

## Learning More Useful Commands

This section will further list more useful commands that will help you do more things in the Linux operating system.

### Modifying and Displaying Files

To modify files or display them, you need to use the cat command. The command can be used to display file commands.

If you want to limit the content shown on the screen, then you need to use either less or more command with it. To run two commands together, you need to use pipe (|). It takes one command’s output and makes it an input to the other.

cat file1 | more

This will show the contents of file1, making sure you can view one page at a time. If you want to view more, you can use the enter key. To close the operation, you can press CTRL + Z and terminate it.

You can also use greater than (>) to store commands or string text to a file. Most of the time, a text editor is used when you want to modify a file. It can be either vi or nano. You can use the vi or nano command followed by the file name to open up the file in the respective text editor.

But, the simplest way to add content to a file is to use the > or  >> command. The > replaces the content of the file, whereas the >> appends it to the file’s content.

$ echo “We are learning Kali Linux” > Kali-Linux-Learning.txt
$ cat Kali-Linux-Learning.txt
$ We are Learning Kali Linux
$ echo “we learn every day” >> Kali-Linux-Learning.txt
$ cat Kali-Linux-Learning.txt
We are learning Kali Linux
We are learning every day

### Finding Files

You can search for files with the help of the find command. It takes the directory in which you are searching as input, followed by the text string.

### Process Management

Another important part of the Linux operating system is process management. You can do process management through the command line. Each process has its own PID. This means that it is easy to manage them.

To interrupt a process, you need to use the kill command.

kill [pid]

This will send a signal and stop or terminate the process. You can also make a command run in the background. To do so, you need to use the & after the command. This will make the command run in the background, and you will also instantly gain access to the shell itself. You can also use the jobs command to see the processes that are running on the system, and then do things accordingly.

If you want to move a process in the foreground, you need to use the fg command, which will bring the background process to the foreground. Also, once a process is moved to the background, it cannot be terminated. So, you need to bring it to the foreground to terminate it.

## Things We Learned in This Chapter

*   Here, we learn about Linux fundamentals.
*   At the core, kernel ensures the proper functioning of the system.
*   It also utilizes a proper file system for easy access to files and directories.
*   Kernel also does a proper process management.
*   Command-line is used to talk to the system
*   ls command is used to list all files and directories
*   Linux utilizes Filesystem Hierarchy Standard(FHS)

# Chapter 7: Kali Linux Configuration

You have reached a point where you are now ready to go into the Kali Linux operating system. In this chapter, we will learn how to configure Kali Linux. Configuring Kali Linux is important as it will make you use it to its full potential. This includes configuring the network, services, and Unix & user groups.

So, let’s get started.

## Network Configuration

Before you start to use your Kali Linux, you need to configure the network. Network configuration will help you connect with the internet. Let’s see how you can configure the network.

### NetworkManager

Gnome provides an interactive way to access different Kali Linux. It offers NetworkManager, an interactive way to configure your network. To get started, go to the top-right menu of your desktop view, and there you can see the drop-down arrow. Click on it, and then choose wired connection. From there, you need to choose “wired settings.”

Once you click on wired settings, you will see the following window open up.

![](Images/image00147.jpeg)

Here you can see that the connection is already setup. DHCP is used to configure the network, including IP address, gateway, and DNS server. If you want advanced settings, you need to click on the gear icon on the wired connection. From there, you can change settings, including IPv4, IPv6, security, and identity.

In fact, you can create multiple profiles by clicking on the plus symbol. This way, you can change between different settings. For a wired connection, you can change easily. If you are on the wireless network, then the SSID setting is used to connect to those networks. SSID stands for the public identifier.

NetworkManager utilizes PPPoE(point-to-point over ethernet) and WWAN(Wireless Wide Area Network).

You can also see that there is an option to set up a VPN. VPN works with the protocols used by the NetworkManager. You can connect with different VPN types through plugins, including OpenVPN, SSH, and so on.

Lastly, you can set the network proxy. By default, it is set as off. You can change it to manual or automatic.

## Configuring Network Using Command Line

You can also configure the network using the command line. There are instances where you might not have access to the graphical desktop.

Configuring the network through the command line includes the use of the ifupdown package. The package includes two tools, ifup, and ifdown tool. The tools are at the core of init script stored in the /etc/init.d/networking directory. The file is used to network configuration during system boot. The devices that are managed by ifupdown can be registered and deregistered using the ifdown tool.

So, how do you do it? Let’s take a look at the ifupdown configuration file. Inside the file, there are two main derivatives that you should know about:

auto network-device: This directive enables ifupdown to configure the network automatically. It only does it once the system finds a new network.

iface network-device: This directive is used actually to configure the interface.

The ifup is used to activate a network interface, whereas the ifdown is used to disable network interface. When you enable a network, it is now ready to receive and transmit data. On the other hand, disabling a network means that it can no further receive or transmit data.

## Using systemd-networkd

There can be instances where ifupdown tool might not work. This can be a reason behind it being too old. After all, it is a historical tool that is being used in Debian. You can use the new tool known as systemd-networkd. It comes integrated with the init systemd. This is a new tool and is not Debian based. It is also lightweight and is easy to integrate with multiple distros.

In the /etc/systemd/network/directory, you need to place the network files. This will enable you to configure the systemd-networkd. There you can find the [Match] section, which has information about network interfaces. There you can also find which configuration applies to which network interface. Moreover, you can also configure different aspects of the interface, including the MAC address.

Sometimes, the networkd might be disabled. That’s why you need to enable it to use it. Also, before you use it, you need to ensure that you have done the DNS resolution integration. It can be done by creating a symlink to the /run/systemd/resolve/resolv.conf replacing the /etc/resolv.conf file.

## Unix Groups and Users Management

User management is a very important part of any operating system. This is also true for Kali Linux. As a user, you need to make sure how to work with user permissions. There are some key files that you should know about. Let’s list them below:

List of users → /etc/passwd

User’s encrypted password → /etc/shadow

List of groups → /etc/group

Encrypted passwords of groups → /etc/gshadow

These file formats can be understood by learning the documentation of shadow, gshadow, passwd.

### User Account Creation

Kali Linux is a sophisticated operating system. It relies heavily on the root user to perform most of the tasks. However, there can be reasons to create users without root permission, especially if you use Kali Linux in your day-to-day activity.

To add a user, you need to use the adduser command.

Once you put it in, it will then ask you for the username. You can add the username and then press enter to complete the task.

However, as you can see from the above screenshot, it asks for a variety of information before finishing the process of creating a new user. It starts by creating the user, adding a new group, and adding a new user (1000) with a group. The group is created similar to that of the username. You can also mention the group name by adding it after the username. adduser command takes two inputs. The first input is the username, whereas the second input is groupname.

adduser [username] [groupname]

You can also gather more information on how the adduser function by typing the help command as below.

adduser --help

First, it asks for the password. You can set a password for the new user. The user can then change this password once he logs into his/her session.

Next, it will ask you to enter values asking for more information about the user. You can opt to skip it by simply pressing enter. The user itself can enter this information once he uses his user account.

The information asked by the adduser command includes the following.

Full Name

Room Number

Work Phone

Home Phone

Other

If you still want to know more, then you can check out the configuration file used by the adduser command. It is stored in /etc/adduser.conf. The configuration files include some nice stuff that you can learn about. For example, you will find that a user identity(UID) range is defined to ensure if something is shared with the group or not.

Also, you noticed how it created directories in the user home directory. The structure of the directories utilizes the /etc/skel/template. The adduser command uses the template and configuration files to ensure that a user is added by following set standards.

## Getent Command

There is one more useful command that you should know about. It is the getent command. It stands for get entries as it can query the system database. To do so, it first calls the needed library function, then followed by the calling the NSS(name service switch) module. This module is configured in the /etc/nsswitch.conf.

The syntax of the command is as below:

getent [database_name] [search_key]

So, if you want to search for a password for a particular user, you can run the following query.

getent passwd user1

## Changing or Modifying an Account

There can be many scenarios where you may need to modify an account. It can include changing passwords or other information about the account. The command to change the password for a Linux account is as below:

### passwd

The first command that we are going to discuss is passwd command. It is a straightforward command that lets you change password. Any root or normal user can use the command. No root privilege is required to run passwd.

It will ask you to type the password once you enter the command. It will once again ask to re-type it before changing the password.

Using the command modifies the /etc/shadow file.

### chfn

chfn lets you change the full name of the user. It is only reserved for the superuser, i.e., root user.

### chage

chage command is used to change the password expiration settings for a user. It can only be used by an administrator and is used to enforce good password habits. Passwords are sensitive in nature and hence needs to be modified from time to time. If you want a user to change the password immediately, then you need to use the -e argument. It will force the user to change the password the next time he logs in.

## Account Disabling

Some accounts need to be disabled due to many reasons, including not following rules or if an account gets hacked by someone else. To ensure that this does not hamper your Kali Linux installation, then you need to delete the account or at least lock the user out for an indefinite time while you run an investigation.

To disable an account, you need to use the passwd -l command.

passwd - l [username]

This will lock the account. This also means that the account files are not deleted and are only locked. They can be referenced later on once it is unlocked. As a Kali Linux administrator, you should only use account disabling to ensure that you can revert the account if needed. Also, some users may be sensitive information in their home directory. Data once deleted cannot be reverted, so be wary of the consequences before you delete a user account.

## Use Groups Management

Lastly, we are going to discuss how to manage groups. Groups are a critical part of any Linux operating system as they enable file and folder sharing for a group.

You can add groups by using the command, addgroup.

To delete a group, you can use the delgroup command.

If you want to modify a group command, then you need to use the groupmod command. It lets you modify the group using the GID or the identifier.

You can also set a group password using the gpasswdgroup. For removing the password, you need to use the following command.

gpasswd - r group

This leads us to the end of our Unix groups and user management. Now, let’s move to configure the services.

## Configuring Services

Service configuration is also an important part of Kali Linux. When we say services, we generally mean daemons. They are the programs that keep running in the background. The services are also responsible for making sure that the systems function as intended.

As there are tons of services running in the background, it is not possible to discuss each one of them. That’s why we are going to discuss a few of the important ones only. Let’s get started and see how important services can be configured.

### Specific Program Configuration

In this section, we will learn to configure a specific program. Before you get started, you first need to understand the program. To do so, you need to read the documentation properly. Generally, the README file is located in the following location. → /usr/share/doc/package/README. Debian

By going through the documentation, you will only save time. Generally, package configuration can be very specific, and the documentation does have the required information to do so. The documentation might also contain a link to other resources that you can find useful.

Next, it is a good idea to check the software’s official documentation.

If you feel lost, then you should check out the dpkg -L package command. This command will return a list of files. From there, you can easily find the documentation.

Another useful command is the dpkg -s package, which shows you the meta-data about the package. The meta-data can contain important information or simply can suggest other packages that can contain the required information.

Also, you can always try to run the configuration beforehand. By going through the configuration, you will know what to expect, and then find those things in the documentation.

The configuration steps can also be self-explanatory with proper comments. In some instances, some configuration files are disabled using comments. By uncommenting, you can make the configuration file to run and make the package execute.

### Remote Logins SSH

SSH stands for secure shell. It lets users connect to the machine remotely. After connecting, you can perform a different set of tasks, including executing commands or transferring files. SSH is a well-known tool among Linux users. In fact, it is used on an industrial level to connect to remote machines.

To use SSH, you first need to make sure that your machine comes pre-installed with the openssh-server. By default, it comes pre-installed. If it doesn’t, then you need to install it using sudo apt-get install command. Sometimes, SSH services can also be disabled. To make it work, you need to use the following command.

systemctl start ssh

You can also configure it to start it with the boot. To do so, you need to run the following command.

systemctl enable ssh

### Configuring SSH

By default, the SSH comes with good enough configuration. However, if you can configure it to make it more functional. To know what it has to offer, you can check its configuration file at /etc/ssh/sshd_config file. The documentation can be found in the sshd_config(5) file.

If you are using SSH for the first time, then you will notice that it doesn’t allow password-based logins. To connect, you need to use the SSH keys. The SSH keys is generated using the ssh-keygen.

If you want every user to use the SSH key-based login, then you need to set the PassswordAuthentication to “no” in the configuration file. This is always a better option compared to other password-based logins.

To ensure that the changes are applied, you need to use the following command.

systemctl reload ssh

### Generating new SSH Keys

SSH keys utilize their own cryptographic keys. They are stored as SSH host keys. Also, the keys are stored in /etc/shh/shh_host_*. The keys should be kept safe. This means that you should not share the keys to anyone and should be kept in a safe place.

One more thing that you need to make sure is to create new SSH keys. If you installed your OS using the debian-installer or simply copied the full disk image, then there can be some pre-installed SSH host keys. As a user, you do not want to use those keys. Moreover, you also need to reset the root password that comes along with them. This way, you will make sure that the keys are not being misused by someone else.

To generate new keys, you need to use the following commands:

# passwd

The above command will change the password.

Next, you need to generate new keys using the following set of commands.

# rm /etc/ssh/ssh_host_*

# dkpg-reconfigure openssh-server

# service ssh restart

## PostgreSQL Database Configuration

As an active user of Kali Linux, you need to use PostgreSQL - a database server. The service is very useful when it comes to other services or programs. As a user, you may not need to use it ever. To make sure that the services that rely on the PostgreSQL can run normally, you need to use database service. Mostly, it is used by services over the network.

To start the service, all you need to do is run the following command.

# systemctl start postgresql

### Configuring the PostgreSQL

By default, PostgreSQL keeps listening to the 5432 TCP port. You can change the PostgreSQL setting by editing the postgresql.conf file. It runs on the file-based socket known as the /var/run/postgreql/ .s.PGSQL.5432.

In the postgresql.conf file, you can change the port by editing the port directives. Other key directives include listen_address to change the address to which PostgreSQL will listen and the unix_socket_directories which deals with the file-based sockets that are created during the operation.

Whenever someone connects from the network, they can connect in two different ways. The two different ways are as below.

The first way is using a file-based socket. It is a popular way as it utilizes the Unix user account to log in as a PostgreSQL user. This means that once it connects, it requires no further authentication, making it the most obvious way of connecting.

Another way is to use a username and password over a TCP connection simply. The username and password, in this method, is not similar to your OS login username or password.

To change the behavior and configure how logins are done, you can check out the pg_hba.conf file, where you can define the socket for connection, and the method that needs to be used for authentication.

If you want full control over the database, then it is a good idea to use the 2nd method as the Postgres user has special privileges.

### Getting Started With User And Database Creation

Our next step is to create a new database and users now. To create a user, you need to use the createuser command. Removing a user is also easy. All you need to use is dropuser command. If you are confused about how these commands work or need more help, then you can always use the man command to read their manuals.

## Apache Configuration

Another important service that we need to configure is the Apache webserver. Kali Linux comes pre-installed with Apache. If it doesn’t, then you need to install the apache2 package.

To start the apache service, you need to use the following command.

systemctl start apache2

We need to learn a little bit of Apache as most of the applications are now distributed as web applications. By learning how to use Apache, you can teach yourself how to host your own applications on the network or use the other hosted network applications.

Apache has a modular design. This means that you can add features to Apache by adding new modules. Also, not all modules come pre-installed, and you need to install it to use it. Also, most of the libraries are external in nature.

As an Apache user, you will be able to find common modules that come installed. The default configuration makes sure of that.

To enable new modules, you need to run the a2enmod module to enable the module. You can also disable a module by using the a2dismod module.

The two of the above programs simply removes the symbolic links to disable and enable modules. The symbolic links are stored in /etc/apache2/mods-enabled. The actual files, on the other hand, is stored in the /etc/apache2/mods-available/.

### Enabling and Configuring Two Important Modules - PHP and SSL

As a Kali Linux user, you simply cannot focus on all the available modules. That’s why we will check out the two important ones, including SSL and PHP.

Web applications that utilize PHP use Apache webserver for execution. It utilizes the libapache-mod-php package. So, if you install Apache, it will automatically get enabled. The other package SSL, on the other hand, is required to make a proper HTTPS connection. It is included in Apache 2.4 and beyond.

To enable SSL, you need to use the a2enmod SSL. Once done, now, you need to add the directives, you also need to edit the configuration file.             

## Managing Services

Until now, we have learned how to manage some particular services on Kali Linux. Now, it is time to learn how to manage services. At the boot sequence, Kali Linux utilizes systemd for initializing the system.

The systemd init system is also a fully-featured service manager. It lets you manage services, including starting and monitoring them.

So, how do you manage the services? Let’s check it below.

systemctl is used for controlling and querying systemd.

To learn about the active services on the system, you need to use the following command.

systemctl list-units

You can also list the services in a hierarchical overview by running systemctl status command.

The status command, as you can see, gives a hierarchy output. You can also see that there are different kinds of units. The services, on the other hand, is part of those units.

A service unit represents each service. The service units are service file which is stored in /lib/systemd/system/. There are two other directories in which these service units are stored. These include the /etc/systemd/system/ and /run/systemd/system/. 

## Things We  Learned in This Chapter

*   Kali Linux is easy to configure
*   You can configure the network by using the NetworkManager or using the ifupdown command.
*   You can also utilize systemd-networkd also to manage the network.
*   Unix groups and user management is also a critical part of Kali Linux
*   You can add a user with the adduser command
*   getent command can be used to search for the username
*   passwd command is used to change password
*   chage command is used to set password expiration time
*   Remote logins can be done using SSH
*   You should always generate new SSH keys before you use it to log in.
*   Database management with PostgreSQL is also important for learning
*   You can manage services using systemctl list-units
*   systemctl status command is used to check the status of the processes

# Chapter 8: Understanding Kali Linux Community and Documentation

Kali Linux is a complex operating system. Even though you read the book completely, there would be something that will be left behind. Also, it doesn’t matter if you are working on it for years; there will be moments where you feel stuck. That’s where the Kali Linux community and documentation comes in. In short, you need to be as resourceful as possible. You need to be able to find solutions to your problems yourself. This will make you competent and a great problem solver.

This chapter aims to improve your Kali Linux community understanding. Clearly, there are plenty of ways you can get help, but it is better to understand your options before investing time in it.

We will also cover strategies on the best way to use the information available. Let’s get started.

## Documentation Sources

Kali Linux is well documented. That makes it easy for you to work with Kali Linux. Also, if you want to make sure what is going on, it is better to read documentation. A program can be a complex thing, and to be sure, read the documentation. This way, you can be sure of what is going around the program.

There is one more thing that you need to be wary about when going through forums or communities asking questions. If you are new to this, you may find others reply with the keyword, RTFM. This is a popular way of responding to queries that are covered in the manual. Its full form is “Read The Fine Manual.” It can also mean “Read The F**king Manual” as well on the internet. If you get these kinds of replies, that means that your answer is in the documentation itself. Also, do not get offended by the term. It simply means that you need to read the manual.

### Manual Pages

Your first place of hunting for information is manual pages. Manual pages take a different approach for organizing the information. The command to find the manual for a program or a command is ‘man.’

The syntax of the manual pages is as below.

man [command]

For instance, if you want to learn what ls command does and all its possible outcomes, then you need to use the following command.

man cp

The manual pages are also used to document other important aspects of the Kali Linux. For example, it also documents things like system calls, C library functions, configuration, and so on. This, however, can cause issues as the names can collide with each other. One classic example is the read command and the read system call. To ensure that the issue doesn’t interfere with your work, the manual pages are organized in a numbered way. Let’s take a look at the sections below.

*   Commands
*   System calls
*   Library functions
*   Devices
*   Configuration files
*   Games
*   Standards and macros sets
*   System administration command
*   Kernal routines

The above section number can help you to read the right manual for the command you are looking for. So, if you want to read the manual for a read system call, then you need to use the following command.

man 2 read

This will show you the manual page for the read system call. If you want to learn about the read command, then you need to use the following command.

man 1 read

You can also not include the number if you want to read the manual page of command as they are at the top of the section number. It takes the 1 by default or the number the command or program relates to. If you want to read the manual for the shadow and do not put any number, it will simply return the shadow(5), considering that the 1-4 sections do not have anything to return for the manual page.

However, there can be cases where you do not know what the name of the command is. This can lead to issues. But, you can still search for manual pages using a command.

The command to do the search is apropos command.

You can use the apropos command with any keyword you think that can relate to the command or program you are searching for. The keyword choice is important here as it will enable you to find the right command or program. The command will return you a list of choices. You can then select the one that you are looking for. It will also return a single sentence about the command so that you get a better idea.

If you are looking for more information about the command, then you can also lookout for a “See Also” section. If the documentation has the section, it will include links and more information about some external documentation.

There are other ways to find documentation. You can use yelp in Gnome and Konqueror in KDE.

## Learning About Info Documentation

Apart from the manual pages, you can also check out the info documentation. It is a GNU project that is aimed to write the documentation in the info format. You can also find many manual pages written in the info format. However, viewing the info pages can be a tough task as they are complex in nature. To ensure that you do not have to go through it, you can use pinfo. It lets you read the complex information in a much better way.

To install pinfo, you need to use the following command.

apt install pinfo

You may also want to run the following command so that all the dependencies are pre-installed without any issue.

So, how does the info document looks like? It is in a hierarchical structure.

### Package Specific Documentation

All packages come with their own documentation. You can easily find the README file within the package that contains the necessary information about how to install, operate, and troubleshoot the package.

The package-specific documentation is stored in the /usr/share/doc/package/directory. Simply change the package name to the package you are using, and you will be able to find the specific documentation. If you are not able to find it, then the documentation might have its own package. What we mean to say that sometimes the package files can be large. This makes it ideal for giving its own package. The documentation, in this case, is stored in package-doc. You can find the documentation package while installing it. It will recommend it to you so that you can install it. If you are still not able to find the documentation, then you need to search for the package website.

Debian is also proactive in providing documentation for some packages. These documentation files are contained within the default place of package documentation. It generally does it improve the documentation so that the user can benefit from it.

### Docs.Kali.Org: Kali Documentation

Kali Linux has its official documentation at docs.kali.org. The book we are working on includes a lot of stuff about Kali Linux, but it is always important to know about Kali Linux documentation. It contains some useful information include tutorials.

If you open the documentation, you will be able to find that there are a lot of things that are covered in the documentation including introduction, USB installation, Kali On ARM, Virtualization, Base Images, Containers, Cloud, Windows Subsystem for Linux, Tools, General Use, Kali NetHunter Documentation, Troubleshooting, Community, Kali Development and Policy.

All of these categories hold some valuable information.

## Community-Driven Kali Linux

Kali Linux is a community-driven project. You can find tons of communities on social media. In fact, there are also local communities that enjoy sharing knowledge and helping others when it comes to Kali. Communities are places where you can help others, share useful information, and interact with others with similar interests.

To help you, we are going to list two communities in which you can join and become part of it.

### IRC Channel on Freenode

Kali Linux has an IRC channel on Freenode. IRC stands for the real-time chat system. This is where you can interact directly with a group of people in real-time. These chat rooms are basically channels with a theme attached to them.

You can connect to the Kali Linux channel on Freenode by opening chat.freenode.net as IRC server, and then listening to the 6667 port. If it seems too technical, you can also use an IRC client, which lets you connect easily to the server.

We recommend using irssi if you are fond of console mode. Hexchat is also a good option as it offers a graphical interface. If you are not interested in downloading any client, then you can check out their web client at webchat.freenode.net.

### Understanding Rules

IRC channels are very strict when it comes to rules and regulations. Before you join or interact with other members, make sure that you read the rules. If you make mistakes, you can get silenced or removed from the server.

## Become Part of the Community: Do Bug Reports

To create a great community, you also need to be an active contributor. One of the best and easiest ways to do so is to submit bug reports. These bug reports can help developers to solve issues and make Kali Linux even better. As you might already know that not all software is free from issues. The same is true for Kali Linux.

By sharing the bug report, you are going to share valuable information with the developers, which can then be used by the developers to fix the issue. The more information you can provide, the better bug reports become. If it is well-thorough and explains the conditions at which you are able to generate it, the chances are that your bug report will be read and resolved in a few days.

## Things We Learned in This Chapter

*   Kali Linux has an amazing community and documentation
*   It has documentation sources. The packages have their own document manual.
*   You can read the manual pages with the man command
*   The format used to structure the documentation is info.
*   There is also package-specific documentation you should read if you feel stuck
*   You can find Kali Linux documentation at docs.kali.org
*   You can also connect to the IRC channel on Freenode
*   If you join, do not forget to read the rules before communicating.
*   You can also join the Kali Linux community by doing bug reports.

# Chapter 9: Kali Linux Monitoring and Security

Kali Linux is an operating system for penetration testers. By default, it is designed and created for professional workers. It may sound fun for newbies, but it requires careful planning to get the most out of it. In this chapter, we will learn how to define a policy, understanding the threats, and then finally discuss packet filtering and firewalls. In the end, you will be able to ensure that your system remains intact and secure. You will also be able to use the monitoring tool and actually design a strategy to secure your site.

## Security Policy For The Rescue

Security doesn’t happen by itself. If you are a security expert, you will know. Each organization requires a security strategy to become secure. You need to find out the right security policy for your organization. Just going through the currently available tools, procedures, or concepts will not help. The security aspects need to be configured depending on many conditions. If you try to rush the implementation, you are going to fail miserably and put your operating system at risk.

To ensure that you do not make hasty decisions, you need to find the goal. To do so, you need to ask questions and then find answers to them. Let’s go through the questions below together.

*   What aspects of your system do you need to protect?
*   What are the threats?
*   Who are the attackers?

Answering these three questions will give you critical information on how to define the security policy. Let’s try to understand each question below.

*   What aspects of your system need to be protected? In this question, you need to find out the type of system or data you want to protect. If you identify the system or the data, then you need to answer the question of what type of data or system you want to protect.
*   When it comes to 2nd question, you need to figure out the threats. The threats can be a malicious entity or simply the way the data or system is compromised. For example, you may want to protect against malicious actors that try to gain entry to the system. When it comes to method, you may want to protect confidential data leak, service disruption due to DDoS, and so on.
*   Lastly, you need to find figure out the threat types. For example, the threat can easily be the user or a third-party malicious entity. In both cases, you  have to make sure that your system is protected at any cost.

As a Kali Linux user, you also need to understand that security is not just one-time. It can be equated to an ongoing process where you need to work hard towards protecting the system constantly. With the system’s evolving every second day, it is common for bugs or exploits to go through. This is where hackers get a chance to do harm. This makes security one of the hardest things to do.

In reality, you need to make sure that you minimize the risk factor. There will always be a slight risk, but it should not be more than acceptable. Depending on the system evolution, risks change with time. By ensuring that you cover the constraints correctly, you can minimize the risk in a great way.

That’s why creating a risk model that evaluates all parameters can be of great help. Modeling around the risk model is what you need to do. Initially, you need to cover the basic minimal parameters. Once they are covered, then you need to find the extreme conditions at which the system can be compromised.

Another important factor is the cost of implementing the security and the risk associated with it. There can be instances where protecting risk is not worth the cost associated with it. You also need to evaluate the loss if the risk is exploited by someone else. If the loss is less than the cost of implementation, it is better to leave it as is.

## Data Confidentiality

Data confidentiality is very important. It is the number one priority for anyone who wants to protect their system. As a Kali Linux user or any system’s user, you need to make sure that your or system’s critical data. This should be your top priority, and you should consider this more important than any other security concerns. If you do not protect the data, it can land into a malicious entity that can harm you in one way or another. The hackers can also erase your data or destroy your hard disk or simply can use the information to gain an advantage over other computers. This makes data confidentiality a big topic in the security world.

## Extreme Cases

Any security policy should consider extreme cases while securing a system or data. Extreme cases are those that have low chances of happening and rely on hard exploits in any system. Zero-day vulnerability exploits can also be considered within the extreme cases as they are fresh and new in their own way. Almost every system out there suffers from zero-day vulnerability exploits. Also, not all extreme cases can be considered due to the hardness they carry to solve them or simply the cost associated with them to solve them. However, few extreme cases should be solved depending on the severity it carries.

## Approach

Systems can be complex in nature. That makes creating system policy a tricky thing. However, there is an approach that can simplify the process. As a user, you can create security policies for subsystems. This segmentation needs to be used to ensure that you can do slowly and steadily. It will also help you understand the constraints and requirements of each subsystem and then do a proper risk assessment depending on the broad security policy and needs.

Also, it is always easy to defend your system against small types of attacks. There are already established means of protecting your system against those. However, large attacks are where you should spend most of the time. In the end, you need to make sure that the data is protected at any cost.

One last thing that you also need to make sure is to define your firewall rules depending on the traffic you receive.

## Security Measures

So, what are the security measures you can do to secure Kali Linux? Let’s go through the options below.

### Laptop Security

If you are using a laptop as a penetration tester, then you have to protect yourself from risks associated with personal computers. As you are not on the public server, you at least do not have to worry about people who use scripts to hack into the system. As you are not connected to the network, you are almost safe from network-based attacks.

The real challenge is to protect your laptop from others who are around you. There can be a chance that authorities can seize your laptop, and you might not want them to read through the contents of your laptop. To make sure that they do not do it, you need to use full-disk encryption. If you are serious about data or other information within your laptop, then you can also go with the nuke option. If you have a nuke option, then it simply removes all the data from the laptop with a combination.

Apart from the data safety, you also need to make sure that you have proper firewall protection if you connect to the internet. This will provide you unwanted access by others. Configuring the firewall rules is important here. Just make sure that you only filter the traffic that you need.

### Server Setup Protection

Kali Linux on a public server is different from that of the laptop. Here, you need to have more security and ensure that you keep your login username and password secure. Also, you need to use the firewall every time you connect. One more thing to ensure is the generate a strong password for the users that you generate. Make sure that passwords are strong enough so that they do not get hacked from brute-force attacks.

## How To Secure Network Services

Kali Linux comes with a plethora of services. As a good rule of thumb, do not active the services that you do not need. Simply disable them. Even if you do not disable them, Kali Linux disables them for you.

Apart from it, you need to make sure that no firewall is running by default. If a firewall is running by default, then it means that it is listening to network interfaces that you do not want.

Also, some of the services running on the public server might not require any authentication to connect or discover. As a Kali Linux user, you need to make sure that the authentications are enabled and set a good password for them to discover you. The key here is to implement privacy in the best possible way. You may also want to disable services that require root access to run. If someone gets access to those services, they can simply gain access to your Kali Linux installation.

## Getting Your Firewall To Work: Packet Filtering

You can protect your Kali Linux setup with a firewall. Firewall can be of three types, hardware or software or both. Its work is to filter packets and ensure that they meet a certain condition. If you are a part of the network, you can also use a filtering network, which saves the whole network. Network firewalls have their own dedicated machines considering that they need to do a lot of work filtering packets.

However, as a Kali Linux user, your main job is to protect your local installation than that of a network. The good news is that Linux comes with its own firewall solution. It is the Netfilter firewall. But, there is one caveat that you need to take care of. You simply cannot just turn it on and leave it. You need to configure Netfilter according to your network requirement.

netfilter firewall can be configured using the ip6tables and iptables commands. The ip6tables command is used to configure an IPv6 network, whereas the IPv4 network can be configured by the iptables command.

You can also use the GUI-based fwbuilder tool that lets you graphically select the firewall rules. We will not go in-depth into these tools as you can easily find information on how to set up the firewall by yourself. If you are still confused, then you can check the documentation for each tool. They are simple and straightforward.

## Logging and Monitoring

Monitoring your machine is also very crucial to its security. In this chapter, we learned how to protect yourself from third-party malicious actors. We learned how important is data security. For this, we learned how to protect the device on which you were working and set up a firewall. Now, how do you know that things are working as intended? To do so, you need to use the monitoring and logging capabilities of the Kali Linux operating system.

Logging and monitoring enable you to detect anomalous behavior on your system. If you see that there is an issue with the system functionality or performance, then you need to check the log files to find out what’s wrong with the system. Sometimes, it can be packages that can clog the system resources or instances where there is actually a breach in your system. This is where you will learn how to successfully monitor and log your Kali Linux so that you know what is going on with the system.

### logcheck Monitoring Logs

The first tool that you can use is the logcheck program. It works by logging the system through log files generated by the system. Every one hour, it sends a report to the administrator through email. The administrator can then go through the log and see for any anomalies that are recorded in the system.

So, which files are monitored by logcheck? They include the directory /etc/logcheck/logcheck.logfiles.

logcheck is pretty comprehensive when it comes to gathering and reporting the issues to the administrator. It offers varied data levels gathering, including settings suited for a workstation, server, or paranoid.

Paranoid is the most verbose type of report generation. This means that it is not the best option out there. It is only useful for machines that host firewalls for the network. The default mode that logcheck uses is server mode. It is used for most users. The last mode is the workstation mode, which is meant for the workstation. The workstation mode is also very terse and is the only ideal for few scenarios where it is needed.

logcheck also offers different parameters which can then be used for customizing it. Some of these rules can help you detect cracking attempts and other security issues.

### Real-Time Monitoring

Real-time monitoring can also be done if you feel the need for it. The tool that you need to use for real-time monitoring includes the top interactive tool. It offers a currently running processes list.

The top tool offers a good amount of information, including the processor time, occupied memory, process identifier. It also lets you kill a process using the k key.

The top tool is excellent for monitoring the system. It also helps you to find out which process is slowing down your system by eating memory or processor.

## How to Detect Changes

With the knowledge of system monitoring, it is now time to learn how to detect changes. These ideas of detecting changes help you to figure out if your system files are changed or not. If there is a change after the basic installation, then it can mean that a malicious actor modifies the system files.

You can use dpkg --verify tool to verify if there is a change in the system files integrity. The command is as below

dkpg -- verify

dkpg -V

However, this is not always a sure shot answer to know if the system in question is really compromised or not. That’s why you might need to use more advanced tools. We are not going to discuss the tools as they are beyond the scope of the book.

## Things We  Learned in This Chapter

*   As a Kali Linux user, you should protect your Kali Linux.
*   The security policy should be used to ensure proper security
*   You should also make sure that the data confidentiality is maintained at any cost
*   Extreme cases should also be considered while working with the OS security
*   Kali Linux OS security also depends on where it is installed. If you are using a Laptop, then you need to have a different approach to security. Accessing the OS in a public server means a different approach.
*   You should use a package firewall to secure your OS
*   Logging is also important for accessing the system’s health
*   The log files are stored in the /etc/logcheck/logcheck.logfiles directory.
*   You can also do real-time monitoring using the top command
*   To detect changes in the core system’s package, you need to use the dkpg --verify command.

# Chapter 10: Debian Package Management

Kali Linux is a Debian-based Linux operating system, especially the Debian package management system. It simply borrows the package management system from Debian. We already discussed how new packages are created and added to Kali Linux.

At the core of Kali Linux, it is the package management system, and if we get to learn about it, we will be able to know a lot about the operating system. By studying it, we will learn how Kali Linux is structured and used. It will also help you to troubleshoot when needed.

In this chapter, our focus will be Debian package management system. We will also learn about APT suite tools and dpkg. By going through this, you will understand the main strength of the Kali Linux, i.e., its package management system. Kali Linux is also known for its package management system and how it has a seamless installation process.

The package management system also ensures that you do not have to work hard to make things work as the management system takes care of most of the things by itself. Let’s get started below.

## APT Introduction

APT stands for Advanced Package Tool(APT). It is more advanced than dpkg. But, what does dpkg do in the first place and how both of them compare? Let’s find out below.

### APT vs. dpkg

Any software application is stored in the Debian package. Also, if you want to get access to build a binary package(.deb), you need to have the source-pack, which includes the instructions and the files to install it. If you only take the binary package(.deb) into account, it only contains the directly usable files, including documentation or programs.

In short, a Debian package comes well equipped with all the information that is required to install the package. The metadata also includes the dependencies and have the proper information to know how to manage the package’s installation, upgrades, and removal.

To install the Debian package, you need to use the dpkg tool. The tool is very hand and is used most of the time to install the package. However, if there is a missing dependency, then it will not be able to install the package. An error will be thrown, telling you that the packages are missing.

The Advanced Package Tool(APT), on the other hand, is completely capable of installing the missing dependencies. It does it with the help of the apt and apt-get commands. APT is simply an upgraded version of the Debian packages.

Debian packages command is dpkg.

By using the command, you will be able to analyze the .deb packages and install them. However, dpkg is limited in nature. They simply do not know about any other packages. APT, on the other hand, has a better feature set compared to dpkg.

APT is a complete solution that enables you not only install and manage Debian applications or packages but also upgrade the system when needed. If you have used Linux before, you should know about the apt-get and apt-upgrade options. These options let you upgrade and update all the available packages(including their dependencies) correctly. We can consider APT as an umbrella tool. Also, you should not forget that the APT tool is useless without dpkg as dkpg handles all the core package management tasks, including installation, removal, and upgrade. APT’s advantage is the fact that it can connect online and then learn about the dependencies of a package during the installation process. This solves the dependency process and improves user experience.

APT and dkpg are a boon for the current Linux users. Earlier, a user need to compile programs by themselves by using the programs such as GCC, make and configure. They are compiling programs and can easily make the installation process complex. You might have to go through the different errors and mistakes before you can finally install the process. This required reading documentation and researching online -- which in turn takes a lot of time and effort.

With the advancement in user experience, we can say that Kali Linux(or Linux in general) has come a long way. APT and dkpg have solved the problems in a unique way, which makes Linux-based operating systems more user-friendly.

As we have already said, APT is connected online and is able to retrieve packages also. The source list from which APT gets its packages is listed in the /etc/apt/sources.list file.

### Going Through the sources.list File

At the core of APT, there is the source.list file. This file contains the configuration and the sources that APT use it make it work. If the file is not configured correctly, then there are chances that APT will fail to work as intended.

The source in the APT source.list file consists of three parts. Spaces separate these three parts. Let’s take a look at the example below.

deb [http://http.kali.org/kali](http://http.kali.org/kali) kali-rolling main non-free contrib

The first part of the command is the deb. In this case, it stands for binary packages. It is the source type. It can also be deb-src, which stands for the source packages.

The 2nd part is kind of clear by how it looks. It is the source URL. In this case, it can be the Debian mirror or other third-party URL. Yes, third-party can also maintain the sources to provide better services depending on the place you share. The source here is an HTTP:// which means that it is a web server where the source is stored. If you see FTP:// instead of HTTP://, this means that the sources are stored on an FTP server. Lastly, if the user is installing packages from a CD/DVD ROM, then they will see the cdrom: syntax used. However, that rarely helps as most of the work is now done online. Also, packages are frequently updated and it is not possible to update the device. This also means that CD/DVD ROM source can go outdated easily.

The third part is where things get interesting. Its structure depends on the repository that is being used.

## Different Package Licenses

Packages are provided licenses and are mainly chosen by the authors themselves. The packages than can be further differentiated based on three sections.

*   The packages that are contained in the MAIN are compliant with the Debian Free Software Guidelines.
*   Contrib is open-source software that requires non-free elements to work.

## Kali Repositories

Kali repositories are repositories where the packages are stored. The main Kali repository is as below.

deb [http://http.kali.org/kali](http://http.kali.org/kali) kali-rolling main contrib non-free

To get a better idea of the repositories, let’s take a look at the different types of repositories below.

### Kali-Rolling Repository

The Kali-Rolling repository is aimed at the end-user. This is where you can find recent packages that you can use in your Kali Linux operating system. A tool that merges the Kali-specific packages and Debian Testing is used so that the dependencies are maintained. This makes it ideal for end-users as all packages can be installed without much issue. The Kali-Rolling Repository is updated almost every day. This also means that the Debian Testing is also evolved.

### Kali-Dev Repository

The Kali-Dev Repository is maintained for developer’s use. It is not available to the public. The developers ensure that the dependency problems are solved here before the packages are moved to the main Kali-Rolling repository. The packages from the Debian Testing first land here, and then go through a proper testing method. If you are an advanced user, you can choose to work with the repository but beware you try it as it can lead to many hours of troubleshooting

### Kali-Bleeding-Edge Repository

The repository holds all the new packages that are built from the upstream Git. It is automatically built. This means that you can access to the bug fixes and latest features. These changes are so fresh that you can get it as soon as the changes are made available to it. If you think that your bug report is resolved, you can verify it by trying out the repository. Of Course, there is a downside to it as well. For instance, the changes are not thoroughly checked and hence can have issues in it. There can also be a dependency issue.

The Kali-Bleeding-Edge Repository can be accessed by adding the following line to the sources.list file.

deb [http://http.kali.org/kali](http://http.kali.org/kali) kali-bleeding-edge main contrib non-free

## Basic Package Interaction

Now that we have learned about the repositories, APT, and dkpg, it is now time to learn how we can do basic package interaction.

As we know, APT is a great tool. It single-handedly manages the installation, maintenance, and removal of packages. In fact, it also manages the dependencies if needed. It does it with the help of the apt-get command-line tool. It basically overcomes the drawbacks of the dkpg.

Before you start your journey with APT, make sure to run the apt update command. It will update the available package list and the sources from which the packages can be downloaded.

### Installing Packages

Let’s take a look at how packages can be installed using the tools. First, we will go through the dkpg and APT.

#### Using dkpg to Install Package

dkpg is the core tool that ensures that the package can be installed. dkpg tool only works with the .deb Debian packages. To install the package, you need to use the following command.

dkpg --unpack packagename.deb

Here you first need to unpack the package using the --unpack option for dkpg. It will unpack the package and process triggers, as well. Now, you need to configure the database for the package. To do so, you need to run the following command.

dkpg --configure packagename-db

Here you change the packagename to the name of the package that you are going to use.

Some of the steps are automatically executed once you run the dkpg command with the --unpack or --configure command. Also, if there is a dependency, then the command will throw an error showing that dependency packages are not present.

You can also forcefully install a package by simply enabling forcing the dpkg command to ignore the error. One such common error is the file collision error. To forcefully install a package, you need to run the following command.

dkpg -i --force-overwrite packagename.deb

#### Meet APT - an Overall Better Solution

APT is an advanced tool that handles a lot of stuff than dkpg. It makes interacting with packages simple and easy. That’s why, as a beginner, you should always use APT.

The command for apt is as below.

apt install package-name

You can also use alternative commands such as

*   apt-get install package-name
*   aptitude install package-name

Once run, it will first read the package list and then create a dependency tree. Once the tree is complete and it doesn’t find any missing dependency, it will move forward to install the package itself. But, if any dependency is missing, then it will update them and then install the package. Before it does that, it will ask you for confirmation. It will also show a message on how many packages need to be updated or installed before the operation can be done. If you press Y on your keyboard, it will automatically handle everything from there and complete the installation process.

## Kali Linux Upgrade

Kali Linux is an active operating system. It continually gets updated with new features, packages, and programs. In this section, we will learn how to keep your Kali Linux upgraded most of the time.

To do regular upgrades, you need to use the three basic upgrade commands.

*   apt upgrade
*   apt-get upgrade
*   aptitude safe-upgrade

All of the three commands lookout for the packages that can be upgraded. It also makes sure that the packages that need upgrades will not be removed. By running the command, you get access to the best possible Kali Linux experience.

The package selection is made by the apt tool. It chooses the recent stable version.

If you do not mind removing old packages that are obsolete, then you can choose to use the following command.

apt full-upgrade

The command will not hesitate to remove old packages if it requires new packages to be installed. We recommend using the command if you want to stick close to the Kali Rolling system.

As a Kali Linux user, you can also learn about the potential issues with the help of the apt-listchanges package. You simply need to install it and run it. Once done, it will showcase the problems before you run the upgrade. The information is stored in the /usr/share/doc/packages/NEWS.Debian file.

Also, one thing that you need to take care of is the frequency of updating your Kali Linux. The Kali Linux Rolling gets new updates every single day. As a user, you do not want to upgrade daily as it can mess up with your setup.

Only update if you know that a security update is out or there is a bug fix in the release. You should also make sure that you check the release notes before reporting a new bug. It might get fixed already.

So, which instances you need to avoid when it comes to not upgrading? Let’s list them below.

*   Do not do an upgrade if your Kali Linux operating system is running smoothly.
*   If you think that the new upgrade will cause more problems, then do not upgrade
*   And, finally, do not upgrade if you think that it removes some of the packages that you need. Simply review it using apt-listchanges packages before making the decision.

## Purging and Removing Packages

Until now, we discussed how to install packages or upgrade the system. Now, let’s take a look at how to get rid of the packages.

You can remove a package using the dpkg command along with the --remove or -r option. The syntax of the command is as below.

dkpg --remove [package-name]

Once you use the command, it will remove the package from your system. However, it is a soft removal, which means that associated files, including maintainer script, log files, configuration files, and associated files. This means that you should use the option only when you want to re-install the program later on. The leftover residue files can then be used once the package is installed back.

However, if you want to remove the packages, including the dependent packages completely, then you need to use the APT command. The command to completely purge the package from your system is as below.

apt remove package-name

The APT command also ensures that the user data and configuration files are not removed.

If you want to remove the user data, but no configuration file, then you need to use dpkg with the -p option. For apt, you need to use the apt purge command.

The purge command should be used cautiously as it can remove the user data, which cannot be retrieved in any condition.

## Learning About Package Contents

If you are curious about how to inspect packages that we got you covered. You can look into the contents of the packages by using apt, apt-cache, and dkpg packages.

To read the package files, you need to use the --listfiles or -L option with dpkg. The syntax of the command is as below.

dkpg --listfiles [package-name]

dkpg -L [package-name]

### Searching For a Particular File

If you are looking for a particular file within the package, then you can use the --search option. The syntax for it is as below.

dkpg --search [package-name]

dkpg -s [package-name]

### Status of The Package

To check the status of the package, you need to use the --status option. The syntax is as below.

dkpg --status [package-name]

dkpg -s [package-name]

### Listing the Known Number of Packages

To list all the packages in the system, you need to use the following command.

dpkg --list

dpkg -l

Both the commands work the same. You can also provide a wildcard as the third parameter to search for a particular package if you want. This will execute the search based on the wildcard or the string that you used for searching. The command for it is as below.

dpkg -l ‘file*.’

## Troubleshooting Packages

Running into problems is a part of working with Kali Linux. That’s why, in this section, we will go through troubleshooting.

### Problems After an Upgrade

Upgrading your Linux operating system can sometimes cause issues. It can lead to issues including incompatible packages, bugs, or even instability. In those cases, you can do the following.

#### Bug Reports

As a user, you may want to report the bug. You can also follow the Kali bug tracker to know if the bug is already reported or not. If it is not, then you should go forward and report it. You should also read the section where we discussed on bug reporting. Also, make sure that you do a proper bug report with as much information as possible.

#### Downgrading

You can also downgrade if needed. Sometimes, it is required to downgrade your Kali Linux or the package that you upgraded. You can downgrade if you know the old package version. This way, you can use the APT command to install that version. If you have the old .deb file, then also you can downgrade the package. Kali Linux or Debian, in general, have the .deb file stored in few places.

var/cache/apt/archives/

Kali mirror pool directory

You can also find the old package on [http://snapshot.debian.org](http://snapshot.debian.org)

## Things We  Learned in This Chapter

*   You can install packages using APT and dpkg tools
*   APT stands for Advanced Package Tool(APT).
*   dkpg is at the core of handling proper package management
*   APT is more advanced as it offers seamless package management
*   With APT, you do not have to worry about dependencies.
*   Multiple Kali Linux repositories hold the packages.
*   For normal users, Kali-Rolling Repository is best as it offers tested packages
*   Devs use Kali-Dev Repository.
*   You can get access to the latest package from Kali-Bleeding-Edge repository
*   To install a package, you can use dkpg or APT command
*   You can upgrade your packages using the apt upgrade command
*   You can remove a package using dkpg –remove

# Chapter 11: Kali Linux And Security Assessment

In this chapter, we will explore how Kali Linux can help us with the Security Assessment. First, let's familiarize ourselves with what security means in terms of an information system. We covered the CIA triad in earlier as well. For a refresh, let’s go through them again.

Mainly, you should concern yourself with three primary attributes:

*   Confidentiality - is your system information secure from authorized access?
*   Integrity - can your system information be changed or modified in a way that is not intended or desired?
*   Availability - and finally, is all the data and information on your system readily accessible as and when it is required?

These three factors form the triad of cybersecurity, also known as the CIA. These are the areas where you will focus your security concerns as a part of the deployment, maintenance, and assessment. With this in mind, let’s move on to discussing how to use Kali Linux in a Security Assessment.

## Preparing Kali Linux for Security Assessment

The first thing to make sure is always to use a clean Kali Linux installation. Many security professionals without much experience make the novice mistake of using the same installation in multiple security assessments. This can cause a lot of problems.

For starters, during the security assessments, you will need to reinstall, tweak, and change the system. All these changes will build on one another, increasing the overall complexity of future configurations. Furthermore, each assessment is unique in its own way, and using the same installation can cause cross-contamination of client data.

However, you can use a pre-customized version of Kali Linux primed for the network/system it is assessing. This can, in fact, help automate parts of the process, which will lead to more convenient and less time consumption.

Here are some points to keep in mind while creating your custom installation of Kali Linux:

*   Use an encrypted installation as it will protect your data on the physical machine. As an extra measure, create a decryption key, send it to the site where you will take the machine after completing the assessment and nuke the decryption that is with you. That way, even if the device gets stolen, all your data will be safe and encrypted.
*   Preplan all the tools and packages you will need during the assessment beforehand. During the assessment, it is highly likely that you won't have ready access to the internet. Therefore keep all these packages with you from the get-go.
*   Also, review your network settings before starting with the assessment. Review the services that are connected with your assigned IP address and recheck your DHCP settings.

Keeping these few things in mind will help you during and after the security assessment to ensure everything is handled smoothly.

## The Different Types of Security Assessments

With your Kali Linux ready to go, it is time you decide what type of security assessment you want to conduct on your network. The different types of security assessments can be broadly classified into four types: Vulnerability Assessment, Compliance Penetration Test, Traditional Penetration Test, and Application Assessment.

Here we will give you a brief run-down on all these different types of assessments. But first, you need to have a clear understanding regarding a vulnerability and an exploit.

### What Is A Vulnerability?

It is basically a flaw in the network that a bad actor can use to compromise the confidentiality, integrity, and availability of your system information.

### What Is An Exploit?

It is a software, which if and when used, can take advantage of a specific vulnerability in the system. In practice, an exploit requires changing a running process and forcing it to make unintended actions.

Now, with the definitions out of the way, here is a look at the different types of security assessments:

## Vulnerability Assessment

In a vulnerability assessment, you are required to create a simple inventory highlighting all the discovered vulnerabilities inside a target environment. You will most likely use an automated tool to identify listening services, server software, versioning, platform, and so on.

Once done, you will have to check each of them for any known signature of the potential threat of vulnerabilities. These signatures include a wide range of data point combinations which include but are not limited to:

### A Version of the Operating System

An outdated operating system that hasn’t received a security patch is more likely to have more vulnerability.

### Patch Level

Many times, even though a security patch is released, the admin hasn’t installed on their system, making it more vulnerable.

### Processor Architecture

Depending on what architecture the system is based on  - Intel x86, Intel x64, ARM, UltraSPARC, the network might be prone to different vulnerabilities.

### Software Version 

Certain software versions have security vulnerabilities that can be used by hackers to break into an otherwise secure system.

And much more.

Your job will be to use these data points to create a signature as a part of your vulnerability assessment. Now, as you can imagine, the more data points you have, the more accurate the signature you will be able to create.

## Compliance Penetration Test

Next, we have the Compliance Penetration Test. It is the most common type of penetration test as they are using government and industry mandated requirements and based on a compliance framework used by that particular organization.

Now, as you can imagine, there are tons of industry-specific compliance frameworks. A very popular example would be the PCI DSS - Payment Card Industry Data Security Standard, which is a compliance framework used by payment card companies that process retail transactions.

While conducting a compliance test, you might first have to start with a vulnerability assessment as it will satisfy many of base the requirements of most compliance frameworks.

## Traditional Penetration Test

Traditional Penetration Tests, in contrast to the previous assessment types, doesn’t start with a scope definition. It generally will focus on a goal - for example, you might be required to simulate a situation showcasing how much of the network gets compromised if an internal user is compromised.

As such, these types of tests aren’t focused on finding and documenting vulnerabilities inside a system. Instead, they focus on certain identified issues and stimulates the worst-case scenario that is possible if it were to happen.

Technically, it can get a bit more complicated. Not only will you have to find the vulnerabilities, you must follow up its impact by using an exploit, and then exploring the level of access the exploit provides to ultimately understanding if it can lead to further attacks against the target environment.

You will have to critically review your target environment and have to resort to manual searching, out of the box thinking, apart from using tools and vulnerability scanners. This generally needs to be done a couple of times to make sure that no stone is left unturned.

Generally, these sorts of assessments can be segmented into different phases where you will need to use different tools for information gathering, vulnerability discovery, exploitation, pivoting and exfiltration, reporting, and so on.

## Application Assessment

While the previous assessments involved testing the entire targeted environment, an application assessment requires you to focus all your resources on a single application. With more organizations putting extra focus on their mission-critical apps, this is slowly becoming an extremely popular and important security assessment.

Now, Application Assessments can be conducted in various ways. For example, you can use an application-specific automated tool to find potential vulnerabilities and security issues in the application. These types of tools use application-specific logic to identify unknown issues instead of relying on any known signatures. As such, the tools have a built-in understanding of how the application works and functions.

Also, depending on the application assessment, you might be required to conduct your tests inside a black box or white box manner:

### Black Box Application Assessment

Here, the tool will interact with the application without any special knowledge or deep access beyond what a standard user gets to experience. This can help you understand how a hacker can break into the application from the outside.

### White Box Application Assessment

This is completely opposite with the tool or assessor getting full access to the source code as well as administrative access to the platform running the application. This type of test helps create a comprehensive review of all the app functionality.

So which type of application assessment should you use? Well, it depends on the goal of the assessment! If you want to know the worst-case scenario when the app comes under a focused external attack, then running a black box assessment would make the most sense. On the flip side, if you are interested in identifying as many security issues as possible, then the white box approach would be the way to go.

There is also room for a hybrid assessment between white box and black box assessment, but as we said, it all depends on what goal you want to achieve.

## Things we  Learned in This Chapter

*   Preparing Kali Linux for a security assessment. Importance of using a clean installation, or a dedicated pre-configured installation of Kali Linux.
*   The difference between vulnerability and exploitation.
*   What is vulnerability assessment?
*   When to do compliance penetration testing and traditional penetration testing?
*   What is the Application Assessment?
*   Benefits of black box assessment and white box assessment.

# Chapter 12: Server And Network Scanning - How To Find And Secure Network Vulnerabilities

Scanning your network and server is very important. You might think that everyone, especially the professionals working on the network, has an idea about all the devices and ports connected to the system, but that isn’t always the case. Furthermore, routine scanning helps identify unauthorized users on the system, which helps in strengthening security.

So with that being said, let’s discuss on how you can scan your server and network on Kali Linux to make sure everything is working as it should be.

## Asking the Right Questions

All parts of your network aren’t equally vulnerable, which means you will need to prioritize and focus on areas which are most susceptible to hacking. This requires you to think like a hacker and search for areas in your network, which is most easy to break into.

Here we have put together a set of questions that you can use to give you a direction in terms of where to look for vulnerability and potential breaches.

*   Which part of your system is most vulnerable and likely to be the preferred entry point for hackers?
*   Which part of the system contains crucial information which would be really hard to retrieve if it ends up getting compromised?
*   Are there certain areas in the network you are not properly familiar with or rarely checked?

By focusing on these points, you will have a good sense of which areas to prioritize and how to organize your system scans. The next bit would be to follow a checklist to make sure you cover every point of entry the hackers/bad-actors can use to infiltrate your system. This will include:

*   Routers
*   Switches
*   Firewalls
*   Email servers, File servers, and Print servers.
*   PCs connected to the system - Laptops, Workstations, Tablets, etc.
*   All the OS connected to the system - both server and client.
*   The Applications and Databases linked to the system.

And so on.

These are the most common point of entry for hackers, and therefore you should multiple tests to make sure they are secure and fortified. However, with that being said, with more devices connected to your system, you have more vulnerabilities, which means you will need to spend more time and resources to check/scan them.

## Thinking Like A Hacker

One of the key aspects of reinforcing security on your system is to think like the hacker who is going to break into the system. Whether you are the owner of the system, or a security professional hired to protect it, getting admin access can blind you from focusing on the more practical vulnerabilities on your website.

Most hackers will do some manual research to collect information on your system or network before attempting to hack it. As such, if you can limit this sensitive information from easy public access, then that will play an extensive role in increasing your site’s security.

The first thing you will need to do is head on over to a search engine, and start collecting information about your business to see what can be accessed by the regular Joe.

You can start out by simple keyword-based searches on Google. However, hackers will perform advanced searches to find more sensitive information to help with their attacks. Therefore, you also need to be ready and well aware of all the information the hackers can use if you want to have the upper hand.

Here are somethings that you can search online to see what information is publically available:

*   Contact information of people connected to your business - Search Engines like USSearch, ZabaSearch, and Choicepoint, and help you find these information.
*   Press Releases that make public any major changes occurring within your company, including news of Technology adoption, Company Merger, and so on.
*   SEC documents that are available online.
*   Patents or Sensitive Documents available online.

The Hackers can search for this information and use it to break into your system. However, if you go ahead and search out this information beforehand, then you already know what information most of the hackers are likely to use to exploit your system. The knowledge on what info is being used to orchestrate a cyber-attack can be very helpful in mitigating it.

## Create A Map Of Publicly Available Information

Once you have identified the weak links on your network and the most likely information the hackers might use to exploit it, it's time to start protecting things and making it more secure. The first thing would be to create a map of the sensitive information available on your network.

A graphical representation of the network and related public information will help us better comprehend the network structure, which can help us easily find all weak links and potential issues that can happen if it gets exploited. Visual network representation is also a great way to find out the footprint the system or network is leaving for the users or hackers.

To begin the process, you will want to head on over to the Whois website from where you can figure out the domain registrar of the website as well as personal information about the website owner, including their names, email addresses, and the likes.

Whois can also provide information about the DNS server related to a particular domain along with information relating to their tech support. You might want to take a look at the DNSstuf where you should find a lot of information about your domain name including:

*   Information regarding how the host handles emails for the domain name.
*   The location of the hosting servers.
*   Generic information regarding the Domain Registrar that can be used by the hackers.
*   Whether or not there is a spam host with the domain name.
*   And so on.

Now, Whois is just one of the site which offers public access to all this information. Therefore, it is a good idea to go ahead and check information about yourself to understand what hackers are using to break into your system.

Apart from Whois, you can also snoop around Google Forums and Groups, where you are likely to find similarly useful information about your system and network. In fact, you might be amazed at the extensive collection of information on these pages, even though you haven’t submitted them yourself.

Someone(including your employees) might have posted a seemingly innocent message or post involving your company, but it might have clues and information which hackers can use to break into your system.

However, despite the security concerns it poses, finding and neutralizing this security is as easy as doing a quick search using your domain name or company name. If you find sensitive info, you can either request to remove it from the site or take appropriate actions on your end so it can’t be exploited.

## Reinforcing All The Weak Links and Vulnerabilities

Following all the above-mentioned steps, you should be able to find out a chunk of useful information which hackers might exploit to break into your system. Now it's time to close off all these vulnerabilities and secure your network.

### Step 1:

First, as mentioned earlier, you need to browse around the internet to find publicly available sensitive information about your hosting provider, IP addresses, and so on. However, there is no reason to think all this information is correct. You can do a scan yourself to verify the legitimacy of this information.

If they are wrong, then there is nothing to worry as the hackers will be led down a wild goose chase. But if they are correct, you can request the website to remove it. But do note that removing Whois information about your site can affect your business in terms of trustability and some SEO metrics.

### Step 2:

Now, it's time to scan your internal hosts and see what parts of your network is visible to your users. There is a high likelihood that the hacker might just come from within the network, either as a user of your services or via a compromised employee account.

Once you know all the network areas which are exposed to your users, you can exercise extra caution to make sure they are well protected. Also, make sure that your employees adhere to strict protocol and don’t lose their security credentials. Just as an extra measure of security, you can make it compulsory to change their passwords every two months or so.

### Step 3:

Next, you will want to check out the ping utility of the system. This can be easily handled by using a third-party tool like [SuperScan,](https://superscan.en.softonic.com/) which can even help you get more than one address to ping at a time.

### Step 4:

Finally, we would recommend doing an outside scan of your system, going over all the ports that are open and vulnerable to cyber threats. SuperScan can help you here, as well. Alternatively, you can also use a tool like Wireshark. It goes without saying that once you detect a vulnerable port, it's time to secure it to prevent any malicious attacks.

Now, following all these scans and basic precautionary steps, you will have the upper hand over the hackers trying to break into your network. You will know what information our IP address is sending out and therefore have an idea regarding what information hackers might seem if they try to intercept the signals.

As discussed earlier, the basic point of all these scans is to cultivate an understanding of what information the hackers are going to use to base their attacks. So the key takeaway of all these scans is to reinforce all these vulnerabilities or ready a plan of action which you will initiate as soon as there is a breach in your network using the weak links you discovered.

However, with that being said, it wouldn’t be wise just to perform a thorough scan of your network once and leave it be. In fact, you need to work out a regular routine where you keep track of your network and how it is changing.

With time, your network and system will change, and the security concerns will shift from one area to the other. Hackers are going to be always on the lookout for these vulnerabilities, so you need to be on your toes to make sure all angles are well protected and secured from malicious attacks.

## Things We  Learned in This Chapter

*   Pin-pointing areas in your network which are most vulnerable.
*   Getting into the hacker mindset and understanding how they are going to attack your network.
*   Working out a map of all publicly available information on your network, server, and host so you can provide extra security.
*   Using tools reinforce security on all system vulnerabilities and weak points.
*   Performing regular scans to maximize protection against cyber attacks.

# Chapter 13: Kali Linux Tools

In our previous chapter, we talked about the specific approach and mindset required to reinforce our network security. Now, here we are going to focus on a more practical topic - the different tools that can help us improve our network security.

We will cover a whole range of tools that can help us perform various security tests and scans on our system to detect vulnerabilities and fix them before they are exploited by hackers.

Now the best thing about Kali Linux that it includes tons of powerful security-hacking tools which can help you with information gathering, password cracking, hardware hacking, reverse engineering, wireless attacks, vulnerability analysis, exploitation testing, stress testing, sniffing & spoofing, and so on.

In fact, if you do a little searching online, you will find there are literally hundreds of Kali Linux tools advertised to help you with your network security. It can get really confusing when choosing which tools to use on your system to detect vulnerabilities and weak points.

This is why we have put together a list going over some of the best Kali Linux Tools in different categories to help you out. We have also made sure to include alternatives to a particular category of tools, so you are not completely stripped out of options.

## [Nmap - The World’s Most Famous Network Mapper Tool](https://nmap.org/)

The primary feature of Nmap is to help you find active hosts inside a network. Apart from this, it can also help you with port scanning and can even enumerate open ports on the local or remote host.

And that’s not all; the tool can also collect information regarding the hardware and OS used on all connected devices, detect the various applications used on the systems along with their version number. You can even extend its functionalities by using the Nmap Scripting Engine, a.k.a. NSE.

## [Fierce - Network Mapping & Port Scanning Tool](https://github.com/mschwager/fierce)

Fierce is a popular DNS reconnaissance tool that can help you find hostnames and non-contagious IP spaces against a specified domain. As such, you should not confuse Fierce as an IP scanner, or a DDoS tool. It can’t help you scan the whole internet or perform un-targeted attacks.

However, it can help you locate likely targets both inside and outside a specific network, which is one of the reasons why it is mostly used in corporate environments. At its core, it is essentially a PERL script that can quickly scan domains in a couple of minutes, using sophisticated algorithms and clever tactics.

## [Unicornscan - Information Gathering & Data Correlation Tool](https://sectools.org/tool/unicornscan/)

Unicornscan is one of the most popular Infosec tools that can help you with information gathering and data correlation. It comes with advanced asynchronized TCP and UDP scanning features backed by useful network discovery patterns to help you locate remote hosts.

The tool can also collect and showcase information about the software and applications running on each of these remote hosts. Other notable features include the option to use custom data sets along with support for SQL relational output.

## [Wireshark - Network Analyzer](https://www.wireshark.org/)

Wireshark is a cross-platform network analyzer tool that is widely used because of its ability to show detailed information about everything going on inside your network. It also tags along a very intuitive GUI, which makes it extremely beginner-friendly and easy to use.

Now coming to the feature side of things, the tool offers useful features like Packet Live Capture, Offline Analysis, Full Protocol Inspection, Gzip Compression and Decompression, VoIP analysis, and much more. You can also use the tool to help you decrypt WPA/WPA2, SSL/TLS, IPsec, and the likes.

## [Aircrack-ng - Wireless Security Software Suite](https://www.aircrack-ng.org/)

With Aircrack-ng, you will get access to a complete suite of tools to help you assess your network WIFi security. All the included tools are command-line based, which means you can do heavy scripting.             

Some of the notable tools available with Aircrack-ng can help you capture packets of data and export them to text files to get processed by third-party tools. Besides this, you also get access to attacking tools that can help you replay attacks, create fake access points, perform packet injects, and help with deauthentication.

## [Kismet Wireless - Wireless LAN Analyzer, Sniffer, and IDS](https://www.kismetwireless.net/)

Kismet is one of the first choice of security experts looking for Wireless LAN Analysis, Sniffers, Wardriving tools, and Wireless Intrusion Detection Frameworks. The tool is multi-platform compatible and works with almost any wireless card.

The tool can be used to work with WiFi interfaces, Bluetooth interfaces, software-defined radio hardware, and some other specialized capture hardware. In terms of functionality, it can help you identify wireless clients, detect wireless intrusions, and much more. You can even configure it to work in the background as you run your assessments using other tools.

## [John The Ripper - Cryptography Testing Tool](https://www.openwall.com/john/)

John The Ripper is one of the fastest password cracking cryptography tools in the market. Right from the start, the tool has been used to help users detect weak Unix passwords and has gained a lot of popularity thanks to its high speed and great performance.

The password decryption methods are set automatically based on the detected algorithms. The tool also comes with dedicated support for dictionary attacks along with the option to define your own dedicated custom dictionary attack lists. The brute force attacks can also be customized with your own set of rules.

## [BeEF - Browser Exploitation Framework](https://beefproject.com/)

Browser Exploitation Framework, also known as BeEF, is a powerful and popular penetration tester mostly used to scan out vulnerabilities and weak links in the browser and then exploit those flaws in the host. The tool is primarily focused on testing the security of both desktop and mobile browsers. As such, you will get access to specific modules that will help you audit the browser security in real-time.

Some of the main noteworthy features of the tool include a dedicated Web User Interface, a modular structure in terms of functionality, Metasploit Integration, powerful history and gathering intelligence, interprocess communication and exploitation, and much more. Also, being a browser exploitation framework, the tool can also help you detect any installed plugins on the browser.

## [Yersinia - L2 Attacks](https://github.com/tomac/yersinia)

Yersinia is a security framework dedicated for layer 2 Attacks on different networks. It can scan out flaws and vulnerabilities in the security protocols used by the networks to find points of attack. The tool works with a wide range of network protocols, including CDP, DHCP, DTP, ISL, HSRP, STP, and VTP.

You will get access to a sleek GTK Graphical User Interface from where you get to control all the features. Some of its notable functionalities include a dedicated ncurses mode, option to read custom configuration files, a debugging mode, support for log files to save all results & data, and much more.

## DHCPig - DHCP Exhaustion Application

DHCPig is a Dynamic Host Configuration Protocol (DHCP) exhaustion tool. It can help you create and launch advanced attacks on networks that can consume all IPs on a LAN, limit new users from obtaining IPs, and even release any IPs in use by the network. As the icing on the cake, the tool can even turn all windows hosts offline by using ARP.

Once you execute the script, it will first grab your Neighbours’ IPs and listen for DHCP requests from any connected clients. If it detects an offer, the tool will respond with a request for that offer. It can also loop and send DHCP requests from all different hosts and MAC addresses, detect neighbor MAC & IP address and release them from the DHCP server, and much more.

## [THC Hydra - For Brute Force Crack Remote Authentication Services](https://github.com/vanhauser-thc/thc-hydra)

Next up, we have THC Hydra - a free hacking tool that can help you launch brute force attacks to crack remote authentication services. The tool comes with support for more than 50 protocols, which makes it perfect for testing the password security levels of any type of server environment.

The tool is known for its super-fast password cracking speeds, the capability to run on multiple operating systems, option to launch multiple brute force attacks parallelly, and much more. Also, being a module-based application, it comes with the option to add custom modules to extend its functionality.

## Metasploit Framework - Penetration Testing Suite

The Metasploit Framework can help you create, test, and execute exploits against remote hosts. It gives you access to a whole suite of penetration testing tools paired with a powerful terminal-based console – msfconsole - to help you locate targets, start scans, exploit any vulnerabilities, and collect any and all available data.

It is, in fact, one of the most powerful security auditing tools in the market, and being available for free, it is something you should have up your belt. Notable features of the tool include support for network enumeration and discovery, ability to evade detection on remote hosts, development and execution of exploits, and much more.

## [FunkLoad - Web-Stress Tool](https://pypi.org/project/funkload/)

With FunkLoad, you get a powerful functional and load Web tester based on python. It can help you emulate a web browser complete with real browser functionalities like cookies, referrer support, and so on. It is perfect if you are looking to test a web project and analyze the performance of your web server.

In terms of functionality, the tool can help you will functional testing and regression testing of your web projects. It can also monitor your server performance after loading the application to help find any bottlenecks. Other notable features include load testing to help find bugs, stress testing to gauge application recoverability, and so on.

## [SlowHTTPTest - Web-Stress Application For HTTP Servers](https://github.com/shekyan/slowhttptest)

SlowHTTPTest is by far the most well-known application layer DoS attack simulator. It is highly configurable and can help you lengthen an HTTP connection to simulate the Application Layer Denial of Service attacks. It is ideal for testing your server or DoS vulnerability, or simply to test how many simultaneous connections it can handle at a time.

The tool also generates useful statistics on each test, so you get access to useful and actionable information. Once a test is completed, it will save all the stats and metrics in an HTML or CSV file, which you can use for representation or further analysis. Other notable features of the tool include an option to set various verbose levels, set a custom HTTP Connect Rate, and even support for Proxy redirects.

## [Inundator - Multi-Thread IDS Evasion Security Tool](http://inundator.sourceforge.net/)

Inundator is a multi-thread, queue-based intrusion detection false positive generator. Also, since it’s completely anonymous (thanks to TOR integration), it is perfect for testing intrusion detection or prevention systems. It can literally flood the security system by generating over a thousand false positives per second.

All the false positives generated using the tools used very poor pattern matching rules. As such, if the system detects little to no false positives, then it means it is based on a well-written set of rules. Whereas, if it becomes victim to the hundreds of false positives, then you should consider adopting heuristic-based detection or anomaly-based detection mechanisms on your networks.

## [Social Engineering Toolkit](https://github.com/trustedsec/social-engineer-toolkit)

Social Engineering Toolkit is another powerful penetration testing framework boasting tons of tools to help you create and execute a social engineering attack in a matter of clicks. It is perfect if you want to hack into social network accounts using powerful social engineering tips and tricks.

You will get access to tools that can help you with WiFi-based attacks that can redirect or intercept packets from users on the same WiFi network as yours. On top of that, you will get to create SMS, Email, and web-based spoofing and phishing attacks. The tool can even let you create malicious .exe files that will compromise users’ systems after they run it.

## [OpenVAS - Vulnerability Scanning Tool](http://www.openvas.org/)

OpenVAS is free software that can help you detect vulnerabilities in any local or remote networks. It can also help you write, create, and integrate your custom security plugin straight on the OpenVAS platform. On top of that, the platform will give you access to over fifty-thousand NVTs (Network Vulnerability Tests), which can scan almost any security vulnerability in your system.

Now, taking a look at some of the notable features of the software, you get the option to perform simultaneous host discovery, network mapping and port scanning, access to OpenVAS transfer protocol, full integration with SQL databases and SQLite, automatic scheduled scans, and much more.

## [Nikto - Helps In Full Web Server Scans](https://www.cirt.net/Nikto2)

Nikto is designed to work as a complementary software to some vulnerability scanning tools, including OpenVAS. It can help you perform a full scan on a web server to help locate vulnerabilities and flaws in the system/network. The scan results are extremely comprehensive and can gather information on insecure files, app patterns, server software that is out of date, file names (default), any software misconfiguration, and so on.

You can use it to scan several ports on the server at the same time. On top of that, it comes with IDS evasion techniques, the option to output results in various formats, username enumeration for both Apache and cgiwrap, and much more. The tool can even help you scan CGI directories, use configuration files customized to your requirements, debug output, and help identify software through headers, favicons, and files.

## [WPScan - Auditing Tool For WordPress Security](https://wpscan.org/)

WordPress, as you all know, is the most popular CMS platform powering over 30% of all websites on the world wide web. So it clearly makes sense to include a Kali Linux security tool that can help audit the WordPress security of a website. With WPScan, you get to scan and detect whether your web project is safe from certain types of attacks and how much sensitive information is being exposed from its core files, plugins, or themes.

The tool can also help you scan weak passwords used by all registered users, and stimulate brute force attacks to see if the passwords can be easily cracked or not. Other notable features include the option to perform non-intrusive security scans, WP username enumerations, and Scheduled WordPress Security Scans.

## [CMSMap - A Centralized Security Solution For All Popular CMS](https://github.com/Dionach/CMSmap)

Unlike WPScan, which is solely a security tool for WordPress websites, CMSMap is a centralized multi-platform security solution designed to work with not only WordPress, but also with Joomla, Drupal, and Moodle.

The tool can help you find security flaws on all the CMSs mentioned above by running brute force attacks, scanning for vulnerabilities, and launching exploits to break into any found vulnerabilities. The tool can also help you set custom user-agent and header, comes with support for SSL, a dedicated verbose mode for debugging purpose, and so on.

## Choose The Right Tool And Reinforce Your Network Security

So as you can see, Kali Linux is compatible with some of the best ethical hacking and penetration testing tools in the market. Not only that, but you also get access to a whole entourage of different security-centric tools that can help you in various other ways as well.

These tools can easily help you quickly scan out all security vulnerabilities in your network and fix them before any hacker has the time to exploit it.

## Things We  Learned in This Chapter

*   Kali Linux is known for its collection of tools.
*   It has more than 600+ pen-testing tools.
*   Nmap - used to scan a network
*   Fierce - It helps you to do network mapping and port scanning
*   Unicornscan - It is used for gathering information and also offers the ability to scan UDP and TCP.
*   Wireshark - Wireshark is a cross-platform network analyzer.
*   Aircrack-ng: It is wireless security software. It comes with tons of options and other small tools
*   Kismet Wireless - Another useful wireless tool used for sniffers, DIS and LAN analysis
*   John The Ripper - John the Ripper is a popular cryptography testing tool. It is used for cracking as well.
*   BeEF - It is a Browser Exploitation Framework. It is a penetration testing tool used to find exploit and vulnerability.
*   Yersinia - The tool is used for L2 attacks
*   DHCPig - The tool is useful for making advanced network attacks
*   THC Hydra - It is a brute force crack a remote authentication
*   Metasploit framework - A popular penetration testing suite
*   FunkLoad - It is a web stress tool for testing browsers
*   SlowHTTPtest - It is used for launching DOS attacks against HTTP servers
*   Inundator - It is a multi-thread IDS evasion security tool
*   Social Engineering Toolkit - Lets you make social engineering attacks with few clicks
*   OpenVas - It is a network vulnerability scanning tool
*   WPScan - It is a WordPress security auditing tool.
*   CMSMap - Centralized Security Solution for Popular CMS

# Conclusion

Kali Linux is the number one penetration testing tool. If you have an interest in security or hacking in general, then Kali Linux is something you should learn. I hope that you found the book useful. The book is also suitable for those who are into the Linux ecosystem and wants to learn about different distribution.

The book tried to teach you how to use Kali Linux to your advantage. We also covered other important topics such as cybersecurity, hacking process, and Debian package management. Our focus soon shifted more towards the intricacies of Kali Linux, where we learned about how to configure Kali Linux. We also learned Debian Package Management.

One interesting topic that we covered is how Kali Linux is closely connected with Debian. Without the evolution of Debian, Kali Linux would not be as successful as it is now. Kali Linux is also known for the tools that it offers. It has hundreds of useful tools that you can use to do penetration testing. As it is not possible to list every tool, we covered a few of them in this book. Each tool is powerful in its own way. However, the usage of the tools depends on the user itself. You need to be creative to make the most out of it.

You can also think of Kali Linux as a tool. Without the necessary problem-solving skills and aptitude, you will not be able to prosper the use of it. So, why I am stressing it? It is because, after you read the book, I want you to experiment with Kali Linux as much as possible. This will open up new possibilities and improve your understanding of a whole new level.

If you are interested more on Kali Linux, then I recommend reading more about the tools that we discussed on the Kali Linux Tools chapter. I also recommend contributing to the community to make the Kali Linux community more awesome! Kali Linux is mostly community-driven, and any contributions can make it more secure and useful.

I congratulate you on completing the book and wish you the best of luck in your future endeavors.