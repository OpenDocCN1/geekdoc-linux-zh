![](graphics/9780137866946.jpg)

![cover-image](graphics/9780137866946.jpg)

# CompTIA Linux+ XK0-005 Cert Guide

Ross Brunson

Pearson

## Contents

1.  [I System Management (Obj. 1.1 - 1.7)](#part01.xhtml_part01)

    1.  [1 Understanding Linux Fundamentals](#ch01.xhtml_ch01)

    2.  [2 Managing Files and Directories](#ch02.xhtml_ch02)

    3.  [3 Configuring and Managing Storage](#ch03.xhtml_ch03)

    4.  [4 Managing Process and Services](#ch04.xhtml_ch04)

    5.  [5 Using Network Tools and Configuration Files](#ch05.xhtml_ch05)

    6.  [6 Building and Installing Software](#ch06.xhtml_ch06)

    7.  [7 Managing Software Configurations](#ch07.xhtml_ch07)

2.  [II Security (Obj. 2.1 - 2.5)](#part02.xhtml_part02)

    1.  [8 Understanding Linux Security Best Practices](#ch08.xhtml_ch08)

    2.  [9 Implementing Identity Management](#ch09.xhtml_ch09)

    3.  [10 Implementing and Configuring Firewalls](#ch10.xhtml_ch10)

    4.  [11 Use Remote Connectivity for System Management](#ch11.xhtml_ch11)

    5.  [12 Understand and Apply Access Controls](#ch12.xhtml_ch12)

3.  [III Scripting, Containers and Automation (Obj. 3.1 - 3.5)](#part03.xhtml_part03)

    1.  [13 Automating Tasks via Shell Scripting](#ch13.xhtml_ch13)

    2.  [14 Perform Basic Container Operations](#ch14.xhtml_ch14)

    3.  [15 Perform Basic Version Control with Git](#ch15.xhtml_ch15)

    4.  [16 Understand Infrastructure as Code](#ch16.xhtml_ch16)

    5.  [17 Understand Containers, Cloud, and Orchestration](#ch17.xhtml_ch17)

4.  [IV Troubleshooting (Obj. 4.1 - 4.5)](#part04.xhtml_part04)

    1.  [18 Analyzing and Troubleshooting Storage](#ch18.xhtml_ch18)

    2.  [19 Analyzing and Troubleshooting Networks](#ch19.xhtml_ch19)

    3.  [20 Analyzing and Troubleshooting CPU & Memory](#ch20.xhtml_ch20)

    4.  [21 Analyzing and Troubleshooting User and File Permissions](#ch21.xhtml_ch21)

    5.  [22 Resolving Linux systemd Common Problems](#ch22.xhtml_ch22)

    6.  [23 Final Preparation](#ch23.xhtml_ch23)

    7.  [A Answers to the “Do I Know This Already?” Quizzes and Review Questions](#appa.xhtml_appa)

    8.  [B Study Planner](#appb.xhtml_appb)

    9.  [Glossary](#gloss.xhtml_gloss)

## Table of Contents

1.  [I System Management (Obj. 1.1 - 1.7)](#part01.xhtml_part01)

    1.  [1 Understanding Linux Fundamentals](#ch01.xhtml_ch01)

        1.  [“Do I Know This Already?” Quiz](#ch01.xhtml_ch01lev1sec01)

        2.  [Foundation Topics](#ch01.xhtml_ch01lev1sec02)

        3.  [Filesystem Hierarchy Standard](#ch01.xhtml_ch01lev1sec03)

        4.  [Basic Boot Process](#ch01.xhtml_ch01lev1sec04)

        5.  [Boot Loaders and Files](#ch01.xhtml_ch01lev1sec05)

        6.  [When Kernels Panic](#ch01.xhtml_ch01lev1sec06)

        7.  [Device Types in /dev](#ch01.xhtml_ch01lev1sec07)

        8.  [Installing Software from Source](#ch01.xhtml_ch01lev1sec08)

        9.  [Storage Concepts](#ch01.xhtml_ch01lev1sec09)

        10.  [Listing Your Hardware Info](#ch01.xhtml_ch01lev1sec10)

        11.  [Summary](#ch01.xhtml_ch01lev1sec11)

        12.  [Exam Preparation Tasks](#ch01.xhtml_ch01lev1sec12)

        13.  [Review All Key Topics](#ch01.xhtml_ch01lev1sec13)

        14.  [Define Key Terms](#ch01.xhtml_ch01lev1sec14)

        15.  [Review Questions](#ch01.xhtml_ch01lev1sec15)

    2.  [2 Managing Files and Directories](#ch02.xhtml_ch02)

        1.  [“Do I Know This Already?” Quiz](#ch02.xhtml_ch02lev1sec01)

        2.  [Foundation Topics](#ch02.xhtml_ch02lev1sec02)

        3.  [File and Directory Operations](#ch02.xhtml_ch02lev1sec03)

        4.  [File Metadata and File Types](#ch02.xhtml_ch02lev1sec04)

        5.  [Soft and Hard Links](#ch02.xhtml_ch02lev1sec05)

        6.  [File Compression, Archiving, and Backup](#ch02.xhtml_ch02lev1sec06)

        7.  [Copying Objects Between Systems](#ch02.xhtml_ch02lev1sec07)

        8.  [File Editing](#ch02.xhtml_ch02lev1sec08)

        9.  [nano, nano](#ch02.xhtml_ch02lev1sec09)

        10.  [Summary](#ch02.xhtml_ch02lev1sec10)

        11.  [Exam Preparation Tasks](#ch02.xhtml_ch02lev1sec11)

        12.  [Review All Key Topics](#ch02.xhtml_ch02lev1sec12)

        13.  [Define Key Terms](#ch02.xhtml_ch02lev1sec13)

        14.  [Review Questions](#ch02.xhtml_ch02lev1sec14)

    3.  [3 Configuring and Managing Storage](#ch03.xhtml_ch03)

    4.  [4 Managing Process and Services](#ch04.xhtml_ch04)

    5.  [5 Using Network Tools and Configuration Files](#ch05.xhtml_ch05)

    6.  [6 Building and Installing Software](#ch06.xhtml_ch06)

        1.  [“Do I Know This Already?” Quiz](#ch06.xhtml_ch06lev1sec01)

        2.  [Foundation Topics](#ch06.xhtml_ch06lev1sec02)

        3.  [Package Management](#ch06.xhtml_ch06lev1sec03)

        4.  [RPM and YUM Package Management](#ch06.xhtml_ch06lev1sec04)

        5.  [Sandboxed Applications](#ch06.xhtml_ch06lev1sec05)

        6.  [System Updates](#ch06.xhtml_ch06lev1sec06)

        7.  [Summary](#ch06.xhtml_ch06lev1sec07)

        8.  [Exam Preparation Tasks](#ch06.xhtml_ch06lev1sec08)

        9.  [Review All Key Topics](#ch06.xhtml_ch06lev1sec09)

        10.  [Define Key Terms](#ch06.xhtml_ch06lev1sec10)

        11.  [Review Questions](#ch06.xhtml_ch06lev1sec11)

    7.  [7 Managing Software Configurations](#ch07.xhtml_ch07)

2.  [II Security (Obj. 2.1 - 2.5)](#part02.xhtml_part02)

    1.  [8 Understanding Linux Security Best Practices](#ch08.xhtml_ch08)

        1.  [“Do I Know This Already?” Quiz](#ch08.xhtml_ch08lev1sec01)

        2.  [Foundation Topics](#ch08.xhtml_ch08lev1sec02)

        3.  [Public Key Infrastructure](#ch08.xhtml_ch08lev1sec03)

        4.  [Certificate Use Cases](#ch08.xhtml_ch08lev1sec04)

        5.  [Authentication](#ch08.xhtml_ch08lev1sec05)

        6.  [Linux Hardening](#ch08.xhtml_ch08lev1sec06)

        7.  [Summary](#ch08.xhtml_ch08lev1sec07)

        8.  [Exam Preparation Tasks](#ch08.xhtml_ch08lev1sec08)

        9.  [Review All Key Topics](#ch08.xhtml_ch08lev1sec09)

        10.  [Define Key Terms](#ch08.xhtml_ch08lev1sec10)

        11.  [Review Questions](#ch08.xhtml_ch08lev1sec11)

    2.  [9 Implementing Identity Management](#ch09.xhtml_ch09)

        1.  [“Do I Know This Already?” Quiz](#ch09.xhtml_ch09lev1sec01)

        2.  [Foundation Topics](#ch09.xhtml_ch09lev1sec02)

        3.  [Account Creation and Deletion](#ch09.xhtml_ch09lev1sec03)

        4.  [Group Accounts](#ch09.xhtml_ch09lev1sec04)

        5.  [Adding Users and Groups](#ch09.xhtml_ch09lev1sec05)

        6.  [Modifying Users and Groups](#ch09.xhtml_ch09lev1sec06)

        7.  [Removing Users and Groups](#ch09.xhtml_ch09lev1sec07)

        8.  [The Shadow Suite](#ch09.xhtml_ch09lev1sec08)

        9.  [Changing Passwords](#ch09.xhtml_ch09lev1sec09)

        10.  [Summary](#ch09.xhtml_ch09lev1sec10)

        11.  [Exam Preparation Tasks](#ch09.xhtml_ch09lev1sec11)

        12.  [Review All Key Topics](#ch09.xhtml_ch09lev1sec12)

        13.  [Define Key Terms](#ch09.xhtml_ch09lev1sec13)

        14.  [Review Questions](#ch09.xhtml_ch09lev1sec14)

    3.  [10 Implementing and Configuring Firewalls](#ch10.xhtml_ch10)

    4.  [11 Use Remote Connectivity for System Management](#ch11.xhtml_ch11)

        1.  [“Do I Know This Already?” Quiz](#ch11.xhtml_ch11lev1sec01)

        2.  [Foundation Topics](#ch11.xhtml_ch11lev1sec02)

        3.  [SSH (Secure Shell)](#ch11.xhtml_ch11lev1sec03)

        4.  [Executing Commands as Another User](#ch11.xhtml_ch11lev1sec04)

        5.  [Summary](#ch11.xhtml_ch11lev1sec05)

        6.  [Exam Preparation Tasks](#ch11.xhtml_ch11lev1sec06)

        7.  [Review All Key Topics](#ch11.xhtml_ch11lev1sec07)

        8.  [Define Key Terms](#ch11.xhtml_ch11lev1sec08)

        9.  [Review Questions](#ch11.xhtml_ch11lev1sec09)

    5.  [12 Understand and Apply Access Controls](#ch12.xhtml_ch12)

        1.  [“Do I Know This Already?” Quiz](#ch12.xhtml_ch12lev1sec01)

        2.  [Foundation Topics](#ch12.xhtml_ch12lev1sec02)

        3.  [File Permissions](#ch12.xhtml_ch12lev1sec03)

        4.  [File and Directory Ownership](#ch12.xhtml_ch12lev1sec04)

        5.  [Understanding and Using umask](#ch12.xhtml_ch12lev1sec05)

        6.  [Permission Granularity Issues](#ch12.xhtml_ch12lev1sec06)

        7.  [Finding Files by Permission](#ch12.xhtml_ch12lev1sec07)

        8.  [Access Control Lists](#ch12.xhtml_ch12lev1sec08)

        9.  [Context-Based Access](#ch12.xhtml_ch12lev1sec09)

        10.  [Command-line Utilities](#ch12.xhtml_ch12lev1sec10)

        11.  [Summary](#ch12.xhtml_ch12lev1sec11)

        12.  [Exam Preparation Tasks](#ch12.xhtml_ch12lev1sec12)

        13.  [Review All Key Topics](#ch12.xhtml_ch12lev1sec13)

        14.  [Define Key Terms](#ch12.xhtml_ch12lev1sec14)

        15.  [Review Questions](#ch12.xhtml_ch12lev1sec15)

3.  [III Scripting, Containers and Automation (Obj. 3.1 - 3.5)](#part03.xhtml_part03)

    1.  [13 Automating Tasks via Shell Scripting](#ch13.xhtml_ch13)

    2.  [14 Perform Basic Container Operations](#ch14.xhtml_ch14)

        1.  [“Do I Know This Already?” Quiz](#ch14.xhtml_ch14lev1sec01)

        2.  [Foundation Topics](#ch14.xhtml_ch14lev1sec02)

        3.  [Container Management](#ch14.xhtml_ch14lev1sec03)

        4.  [Container Image Operations](#ch14.xhtml_ch14lev1sec04)

        5.  [Summary](#ch14.xhtml_ch14lev1sec05)

        6.  [Exam Preparation Tasks](#ch14.xhtml_ch14lev1sec06)

        7.  [Review All Key Topics](#ch14.xhtml_ch14lev1sec07)

        8.  [Define Key Terms](#ch14.xhtml_ch14lev1sec08)

        9.  [Review Questions](#ch14.xhtml_ch14lev1sec09)

    3.  [15 Perform Basic Version Control with Git](#ch15.xhtml_ch15)

    4.  [16 Understand Infrastructure as Code](#ch16.xhtml_ch16)

        1.  [“Do I Know This Already?” Quiz](#ch16.xhtml_ch16lev1sec01)

        2.  [Foundation Topics](#ch16.xhtml_ch16lev1sec02)

        3.  [File Formats](#ch16.xhtml_ch16lev1sec03)

        4.  [Infrastructure as Code Concepts](#ch16.xhtml_ch16lev1sec04)

        5.  [Continuous Integration/Continuous Depolyment](#ch16.xhtml_ch16lev1sec05)

        6.  [Advanced Git Topics](#ch16.xhtml_ch16lev1sec06)

        7.  [Summary](#ch16.xhtml_ch16lev1sec07)

        8.  [Exam Preparation Tasks](#ch16.xhtml_ch16lev1sec08)

        9.  [Review All Key Topics](#ch16.xhtml_ch16lev1sec09)

        10.  [Define Key Terms](#ch16.xhtml_ch16lev1sec10)

        11.  [Review Questions](#ch16.xhtml_ch16lev1sec11)

    5.  [17 Understand Containers, Cloud, and Orchestration](#ch17.xhtml_ch17)

        1.  [“Do I Know This Already?” Quiz](#ch17.xhtml_ch17lev1sec01)

        2.  [Foundation Topics](#ch17.xhtml_ch17lev1sec02)

        3.  [Kubernetes Benefits and Application Use Cases](#ch17.xhtml_ch17lev1sec03)

        4.  [Single-node Multicontainer Use Cases](#ch17.xhtml_ch17lev1sec04)

        5.  [Container Persistent Storage](#ch17.xhtml_ch17lev1sec05)

        6.  [Container Networks](#ch17.xhtml_ch17lev1sec06)

        7.  [Service Mesh](#ch17.xhtml_ch17lev1sec07)

        8.  [Bootstrapping](#ch17.xhtml_ch17lev1sec08)

        9.  [Container Registries](#ch17.xhtml_ch17lev1sec09)

        10.  [Summary](#ch17.xhtml_ch17lev1sec10)

        11.  [Exam Preparation Tasks](#ch17.xhtml_ch17lev1sec11)

        12.  [Review All Key Topics](#ch17.xhtml_ch17lev1sec12)

        13.  [Define Key Terms](#ch17.xhtml_ch17lev1sec13)

        14.  [Review Questions](#ch17.xhtml_ch17lev1sec14)

4.  [IV Troubleshooting (Obj. 4.1 - 4.5)](#part04.xhtml_part04)

    1.  [18 Analyzing and Troubleshooting Storage](#ch18.xhtml_ch18)

    2.  [19 Analyzing and Troubleshooting Networks](#ch19.xhtml_ch19)

        1.  [“Do I Know This Already?” Quiz](#ch19.xhtml_ch19lev1sec01)

        2.  [Foundation Topics](#ch19.xhtml_ch19lev1sec02)

        3.  [Network Configuration Issues](#ch19.xhtml_ch19lev1sec03)

        4.  [Firewall Issues](#ch19.xhtml_ch19lev1sec04)

        5.  [Interface Errors](#ch19.xhtml_ch19lev1sec05)

        6.  [Bandwidth Limitations](#ch19.xhtml_ch19lev1sec06)

        7.  [Name Resolution Issues](#ch19.xhtml_ch19lev1sec07)

        8.  [Testing Remote Systems](#ch19.xhtml_ch19lev1sec08)

        9.  [Summary](#ch19.xhtml_ch19lev1sec09)

        10.  [Exam Preparation Tasks](#ch19.xhtml_ch19lev1sec10)

        11.  [Review All Key Topics](#ch19.xhtml_ch19lev1sec11)

        12.  [Define Key Terms](#ch19.xhtml_ch19lev1sec12)

        13.  [Review Questions](#ch19.xhtml_ch19lev1sec13)

    3.  [20 Analyzing and Troubleshooting CPU & Memory](#ch20.xhtml_ch20)

        1.  [“Do I Know This Already?” Quiz](#ch20.xhtml_ch20lev1sec01)

        2.  [Foundation Topics](#ch20.xhtml_ch20lev1sec02)

        3.  [Runaway and Zombie Processes](#ch20.xhtml_ch20lev1sec03)

        4.  [High CPU Utilization/Load Average/Run Queues](#ch20.xhtml_ch20lev1sec04)

        5.  [CPU Times and CPU Process Priorities](#ch20.xhtml_ch20lev1sec05)

        6.  [Memory Exhaustion and Out of Memory](#ch20.xhtml_ch20lev1sec06)

        7.  [What is Out Of Memory (OOM)?](#ch20.xhtml_ch20lev1sec07)

        8.  [Swapping](#ch20.xhtml_ch20lev1sec08)

        9.  [Hardware](#ch20.xhtml_ch20lev1sec09)

        10.  [Summary](#ch20.xhtml_ch20lev1sec10)

        11.  [Exam Preparation Tasks](#ch20.xhtml_ch20lev1sec11)

        12.  [Review All Key Topics](#ch20.xhtml_ch20lev1sec12)

        13.  [Define Key Terms](#ch20.xhtml_ch20lev1sec13)

        14.  [Review Questions](#ch20.xhtml_ch20lev1sec14)

    4.  [21 Analyzing and Troubleshooting User and File Permissions](#ch21.xhtml_ch21)

        1.  [“Do I Know This Already?” Quiz](#ch21.xhtml_ch21lev1sec01)

        2.  [Foundation Topics](#ch21.xhtml_ch21lev1sec02)

        3.  [User Login Issues](#ch21.xhtml_ch21lev1sec03)

        4.  [User File Access Issues](#ch21.xhtml_ch21lev1sec04)

        5.  [Password Issues](#ch21.xhtml_ch21lev1sec05)

        6.  [Privilege Elevation Issues](#ch21.xhtml_ch21lev1sec06)

        7.  [Quota Issues](#ch21.xhtml_ch21lev1sec07)

        8.  [Summary](#ch21.xhtml_ch21lev1sec08)

        9.  [Exam Preparation Tasks](#ch21.xhtml_ch21lev1sec09)

        10.  [Review All Key Topics](#ch21.xhtml_ch21lev1sec10)

        11.  [Define Key Terms](#ch21.xhtml_ch21lev1sec11)

        12.  [Review Questions](#ch21.xhtml_ch21lev1sec12)

    5.  [22 Resolving Linux systemd Common Problems](#ch22.xhtml_ch22)

        1.  [“Do I Know This Already?” Quiz](#ch22.xhtml_ch22lev1sec01)

        2.  [Foundation Topics](#ch22.xhtml_ch22lev1sec02)

        3.  [Unit Files](#ch22.xhtml_ch22lev1sec03)

        4.  [Common Problems](#ch22.xhtml_ch22lev1sec04)

        5.  [Summary](#ch22.xhtml_ch22lev1sec05)

        6.  [Exam Preparation Tasks](#ch22.xhtml_ch22lev1sec06)

        7.  [Review All Key Topics](#ch22.xhtml_ch22lev1sec07)

        8.  [Define Key Terms](#ch22.xhtml_ch22lev1sec08)

        9.  [Review Questions](#ch22.xhtml_ch22lev1sec09)

    6.  [23 Final Preparation](#ch23.xhtml_ch23)

        1.  [Exam Information](#ch23.xhtml_ch23lev1sec01)

        2.  [Getting Ready](#ch23.xhtml_ch23lev1sec02)

        3.  [Tools for Final Preparation](#ch23.xhtml_ch23lev1sec03)

        4.  [Suggested Plan for Final Review/Study](#ch23.xhtml_ch23lev1sec04)

        5.  [Summary](#ch23.xhtml_ch23lev1sec05)

    7.  [A Answers to the “Do I Know This Already?” Quizzes and Review Questions](#appa.xhtml_appa)

    8.  [B Study Planner](#appb.xhtml_appb)

    9.  [Glossary](#gloss.xhtml_gloss)

## I: System Management (Obj. 1.1 - 1.7)

## Chapter 1\. Understanding Linux Fundamentals

This chapter covers the following topics:

• [Filesystem Hierarchy Standard](#ch01.xhtml_ch01lev1sec03)

• [Basic Boot Process](#ch01.xhtml_ch01lev1sec04)

• [Boot Loaders and Files](#ch01.xhtml_ch01lev1sec05)

• [When Kernels Panic](#ch01.xhtml_ch01lev1sec06)

• [Device Types in /dev](#ch01.xhtml_ch01lev1sec07)

• [Install Software from Source](#ch01.xhtml_ch01lev1sec08)

• [Storage Concepts](#ch01.xhtml_ch01lev1sec09)

• [Listing Hardware Information](#ch01.xhtml_ch01lev1sec10)

The exam objectives covered in this chapter are as follows:

**Objective 1.1:** System Managment

Linux is a great operating system, useful for a large variety of tasks, but also with a lot of tweakable and configurable options, some of which are not that well documented, or easy to understand.

It's like buying a car off the car dealer's lot, if you just start it up and drive it, it's pretty simple, just avoid crashing and keep the fluids full and you'll be ok for a while.

The REAL fun begins when something doesn't work right, you have to pop the hood (or bonnet for our European friends) and start figuring out what went awry or what needs changed. Linux can be very easy to use, but also allows you to dive s deep under the hood into the inner workings as you could possibly want to.

This chapter is all about the essentials of Linux System Management, including information about what the Filesystem Hierarchy Standard is, what files and directories go where and contain what, particulars about the /dev directory and it's contents, the basics of storage management including types of storage, partition types, RAID and FUSE, the boot process of a Linux system and constructing software packages from source.

We'll also look at what happens when the Linux kernel panics or crashes occur and how to investigate what hardware your system contains.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 1-1](#ch01.xhtml_ch01tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 1-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/01tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** The set of firm suggestions that most distribution vendors follow about what files and directories are where and what they contain is?

**a.** Data Positioning Standard

**b.** File and Directory Protocol

**c.** Filesystem Heirarchy Standard

**d.** None of these answers

**2.** In order to format a filesystem on a newly-installed disk device on a Linux system, what must be done?

**a.** Mount the device

**b.** fsck the device

**c.** Defrag the device

**d.** Partition the device

**3.** If your system has encountered an internal error and is unable to continue processing, which of the following has occurred?

**a.** Stop error

**b.** Green screen of death

**c.** Kernel panic

**d.** Init zero

**4.** Which of the following is NOT a valid device type that you would typically find in the /dev directory on a Linux system?

**a. tty**

**b. zero**

**c. urandom**

**d. tmp**

**5.** You wish to compile a software package on your system. Which of the following must be run first in order to customize the makefile for your system?

**a. make conf**

**b. setup**

**c. conf makefile.c**

**d. configure**

**6.** Which directory is the beginning of the virtual filesystem?

**a. /**

**b. /vert**

**c. /sys**

**d.** None of these answers are correct.

**7.** Which command gives an overview of all the hardware and drivers in the system, including the ports used to talk to the CPU?

**a. lspci**

**b. lsdev**

**c. lsusb**

**d. sysinfo**

### Foundation Topics

### Filesystem Hierarchy Standard

The filesystem’s structure starts with the root of the filesystem, which is denoted by the forward slash character (/). Every item on the filesystem is accessible by a single unique path off the root of the system, such as /usr/local/bin/foobar, no matter which device that file is stored on.

Unix evolved its own set of traditions as to where certain files would go. The fragmentation of the commercial and academic Unixes led to differences in conventions depending on which flavor of Unix you were using.

Linux borrows practices from many different Unixes and has fragmentation of its own in the form of different distributions. The community started working on a standard for filesystem layout called the File System Hierarchy Standard (FHS) to make it easier for both people and software to know where files can be found.

The latest FHS is available from the Linux Foundation, and is at version 3.0 at the time of this writing.

The FHS isn’t exactly a standard but a firm set of suggestions that most, but not all, distribution vendors follow. There will be questions on the exam about the FHS. The FHS describes where particular types of files are to be placed, which helps maintain consistency across different distributions.

#### What Goes Where

The exams make somewhat of a big deal about what the proper directories and locations are for Linux files, but few things are more vexing than to be asked what should positively be in the root ( / ) directory, or what can be stored elsewhere. This means you'll probably have to at least do a cursory read-through of the FHS, it's good information and will help you understand Linux systems even better, so go ahead and do it!

![Images](graphics/key_topic_icon.jpg)

##### The Root of the Filesystem

The existence of a filesystem, and indeed, the actual system being a functional Linux computer begins with the / or root directory, and the sub-directories that are contained there, which also can contain files and [*subdirectories*](#ch01.xhtml_key01-a) all the way down to the lowest level files on the system.

Starting off with the / or root directory, [Table 1-2](#ch01.xhtml_ch01tab2) lists out the more common top-level subdirectories off the / (root) along with a short explanation.

![Images](graphics/key_topic_icon.jpg)

**Table 1-2**–Common Subdirectories off of the root (/) directory and what they are typicaly for.

![Images](graphics/01tab02.jpg)

The exam will contain questions designed to determine if you know what the most common directories are for on your Linux system. You may see a question about choosing what directories are listed as optional, so again, I encourage you to peruse the table of contents of the FHS and be sure you are aware of those.

##### Where to Put Programs

The FHS does not allow programs to create their individual named directories in the /usr section. This tree is where programs or binaries are normally kep that are not core applications for the running of a Linxu system, those go in /bin and /sbin, typically.

The subdirectories allowed to exist directly under the /usr directory are:

• **bin:** Contains most user commands.

• **lib:** Contains libraries.

• **local:** Contains local/sharable programs, may be empty.

• **sbin:** Contains nonvital system binaries.

• **share:** Contains architecture-independent data.

The FHS discourages having individual application directories in the /usr tree root, but instead wants them stored in a subdirectory off of /usr, or one of it's allowed subdirectories.

### Basic Boot Process

Booting a Linux system isn’t just a matter of turning on the system and having it eventually present you with a login prompt. Rather, it’s a set of events that results, if all goes well, in your being presented with that login prompt.

In this next set of sections we will look at the boot process as a set of tasks performed to get a system to the point where it can enter the default runlevel, where things can become complex due to the various methods of configuring, starting, and managing system services or processes.

We'll be covering:

• **BIOS**:**** Basic Input/Output System

• **UEFI**:**** Unified Extensible Firmware Interface

• **Boot Commands**:**** Such as mkinitrd, grub2* and dracut

• **GRUB2**:**** The Grand Unified Boot Loader 2

• **Boot Sources**:**** PXE, USB and ISO booting

#### What Is the Boot Process?

The boot process for Linux is the process by which a system progresses from the power-on of the hardware (or virtual hardware) until the chosen operating system is at the desired state of functionality. Thanks to the popularity of systemd, Upstart, and other initialization methods, there are a number of pathways to achieving a running system.

The Linux boot process can be broken up into four distinct stages:

**1.** Boot loader phase

**2.** Kernel phase

**3.** Early user space

**4.** Init process

#### System Boot Options

There are a number of ways to boot a system. Some require installation of software and configuration on the local disk, some allow for using a boot or installation server, and some allow you to boot from remote filesystems across the network.

![Images](graphics/key_topic_icon.jpg)

##### initrd and initramfs

Linux runs on an extremely wide range of hardware, and many of the distributions use a fairly standard Linux kernel image for compatibility and depend on the detection of each system’s individual hardware and the loading of needed kernel modules to properly accommodate that hardware during the installation and subsequent system initializations.

Because of the incredible range of possible boot methods, styles, and types of hardware involved, there is a bit of a “chicken-or-egg” problem: The system must boot off hardware with a generic Linux kernel image, but where is the root filesystem, and how can you let the generic image know its location?

Rather than take the inelegant option of compiling into the kernel the modules that are required for a given hardware configuration, an early user space temporary filesystem is used. The temporary filesystem is located on disk, and the location is known to the firmware or boot loader. The temporary filesystem is accessed and mounted, and an array of possible modules are made available for use during the booting process. The kernel and the early user space filesystem’s image are loaded into RAM, and the kernel is informed of the location in memory of the image so that it can detect its format–either initrd or initramfs.

The [*initrd*](#ch01.xhtml_key02-a) method, which is quite old, is effectively an image of a filesystem that is represented as the **/dev/ram** device and gets mounted as the temporary root filesystem for the kernel to use. The disadvantage of this method is that the kernel must have a compiled-in or hardcoded reference to the driver for this filesystem. This is possibly problematic if the disk is changed, such as through swapping out a disk, changing the size or geometry of the disk, or modifying the partition containing the file.

The command traditionally used to create an initial RAM disk is the **mkinitrd** command, followed by the initrd image to be created and the kernel it is being created for, as in this example:

```
n# sudo mkinitrd -preload=/boot/initrd.img-5.11.0-37-generic 5.11.0-37-generic
```

If there is a particular module that should be loaded so that the kernel can find and access the disk with the initrd on it, you can specify it by using the **--preload** option followed by the module name, as shown here:

```
# sudo mkinitrd -preload=/boot/initrd.img-5.11.0-37-generic 5.11.0-37-generic
```

The more commonly used option for providing an early user space filesystem is the [*initramfs*](#ch01.xhtml_key03-a) method. This method uses an initial root filesystem that is unpacked from a particular type of archive file (cpio) and gets mounted in RAM as the temporary root filesystem. A distinct upside of this method is that there is no need to have special modules precompiled or included in the kernel, so it is generic and compatible with many system configurations.

Constructing an initramfs image initially involves using the **mkinitrd** command, which is also used in the initrd method. However, the **dracut** command is almost immediately involved in the construction of the initramfs image, which it attempts to create with the least possible dependency on hard-coded scripts. The **dracut** framework relies on udev (the device manager in the kernel) to tell it what devices are detected and mounted and when the proper device is mounted, the system switches the root filesystem over to that device.

A main advantage of **dracut** is its wide support of boot devices, including devices that use RAID and LVM and more esoteric device types, such as remote devices via iSCSI and NFS.

Creating an initramfs image with **dracut** is fairly simple. If you run the command alone, the system attempts to create a functional initramfs image for the currently running kernel. This causes an error message, as this is an attempt to overwrite the current initramfs image.

To create an initramfs image without overwriting the current image, simply specify another image name, and then you can inspect the format of the resulting initramfs image:

```
# dracut some-image-file-name.img
```

##### Booting with UEFI

The problem child for most Linux installations these days is the United Extensible Firmware Interface (UEFI). The portion of the UEFI that makes installation so much more difficult for Linux distributions is called Secure Boot. Secure Boot is ostensibly designed to make it as hard as possible for bad folks to corrupt, change out, or alter your boot manager image and thereby gain inappropriate access to your computer.

In reality, because initially all UEFI Secure Boot images had to be signed by an official signing authority, and the only authority was Microsoft, installing Linux was made much more difficult, requiring distribution maintainers to either go to Microsoft to get a boot image signed off on or create their own completely alternative signing authority and get that approved through the UEFI process.

The best solution, and one that still currently works, is to simply turn off UEFI Secure Boot in the preboot system configuration and avoid the whole issue from the beginning. To be very clear, you only need to disable the Secure Boot portion of the UEFI process, and there are great reasons to continue to use UEFI. On the whole, it’s a definite improvement over the master boot record (MBR) method.

The **/boot/efi** directory is not always present in every distribution, but if it’s there, typically it’s used when you must dual-boot a system, as the UEFI system wants a UEFI partition to be available.

Note

On the system examples in this chapter, the Ubuntu machine has no **/boot/efi** directory, and the CentOS machine has a **/boot/efi/EFI** directory that contains only an empty directory named centos.

If a system were configured to use EFI for booting, there would be a FAT32 partition (an EFI system partition) mounted on **/boot/efi** that would contain the boot files for the various operating system boot options on the system, with the extension .efi, as in the following file, which is an EFI boot image:

```
/boot/efi/EFI/arch/vmlinuz-linux.efi
```

The file may also be named simply **linux.efi.**

##### Booting via PXE

The Preboot Execution Environment (PXE) requires a client to have a PXE-capable network interface card (NIC) and, on the server side, a DHCP server that supports PXE booting.

The PXE server side is more complex than the client side, requiring several protocols to be supported in the right combination, including having a valid network boot program (NBP) available to be transferred to the client after it has its networking configured via DHCP.

The process of booting up a PXE-capable client computing device goes something like this:

**Step 1.** The client device is powered on, and the PXE boot option is chosen from the BIOS/Startup interface.

**Step 2.** The client sends out a DHCPDISCOVER broadcast that has built-in PXE options that let the DHCP server know what type of a request it is.

**Step 3.** The PXE-capable DHCP server returns a DHCPOFFER broadcast that contains all the networking information needed for the PXE client to set up its networking stack and contact the DHCP server’s Trivial FTP (TFTP) service.

**Step 4.** The PXE client finishes its network setup and initiates a TFP transfer of the NBP image and stores it in the client’s RAM.

**Step 5.** Finally, the client boots with the NBP and, depending on the operating system, requests additional boot files from the TFTP server or from other network resources, such as a Network File System (NFS) server.

##### Booting via NFS

We have already looked at using TFTP and DHCP servers to distribute networking configuration and network boot programs. It’s now reasonable to consider booting systems from files contained on an NFS share on the network.

Booting a running system from NFS is a little different from PXE booting a system, which is normally used for installation (though not restricted to that function).

For an example of booting from NFS, we’ll use the scenario of a diskless workstation, where the entire operating system is downloaded and mounted to the PXE-capable system from an NFS server.

Here is an overview of what needs to happen to enable a diskless workstation to boot and mount its root filesystem over NFS:

**Step 1.** Select a server and install/enable DHCP and TFTP services.

**Step 2.** Configure TFTP to support PXE booting.

**Step 3.** Copy the appropriate pxelinux image to the TFTP boot directory.

**Step 4.** Ensure that the DHCP/TFTP server’s firewall allows the traffic.

**Step 5.** Configure the DHCP server to support PXE booting.

**Step 6.** Create a root directory that contains a full Linux system for sharing across NFS. Various distributions recommend using rsync or using the YUM option **--installroot**.

**Step 7.** Configure the appropriate kernel that the diskless workstation will be booting from.

**Step 8.** Create and set the permissions on the initrd method and copy it into the TFTP boot directory.

**Step 9.** Share out the diskless root directory by adding it to the **/etc/exports** file and either restart the NFS daemon or use the **exportfs** command.

**Step 10.** Boot the diskless workstation and choose the **PXE Boot** option, and when the system presents a menu of boot options, choose the one that was just configured. The system mounts the remote root filesystem as its own **/** filesystem, and the system is now a functioning system.

##### Booting via ISO

Booting from an ISO file (a disk image of a Linux distribution installation CD/DVD) is relatively simple to set up. The main reason for doing so is to have an on-disk rescue environment in case the distribution installed to disk has a problem or password recovery is needed.

The only things really needed are an ISO of a Linux distribution CD/DVD, a free partition big enough to hold the CD’s/DVD’s contents, and the ability to edit the grub.cfg file to point one of the menu entries to the ISO file on the partition you copied the ISO file to.

There are multiple ways to boot a rescue system from ISO, and this is a relatively simple method for doing so:

**Step 1.** Choose a Linux distribution and download an installation CD/DVD.

**Step 2.** If you are installing Linux to the system for the first time, create the rescue partition during the install, making sure to label it something obvious like RESCUE, and create an MS-DOS filesystem on the partition.

**Step 3.** If you are modifying an existing and running Linux system, you can use parted or gparted to resize the current partitions and free up room for a rescue partition. (This is far beyond the scope of the Linux+ exam.)

**Step 4.** Copy the ISO file to the disk and note the name of the file.

**Step 5.** Update the grub.cfg file to include a boot stanza that uses the MS-DOS partition as the root partition and then mounts as a loopback device the ISO file of the Linux distribution.

**Step 6.** Boot the system and test the configuration.

There are dozens of tutorials online that can walk you through all the various aspects of this process, which differs on the various distributions. The main concept here is that you can boot from an ISO file that’s contained on a disk device.

### Boot Loaders and Files

When a computer boots up, it doesn’t know how to talk to all its peripherals or even how to load applications. But each computer has a [*Basic Input Output System (BIOS)*](#ch01.xhtml_key17-a) that gives it just enough intelligence to read and write to local disks and write some text to the screen.

After a computer boots up, it transfers control to the BIOS, which initializes the hardware and reads the first block–512 bytes–from the boot disk. This block contains the first part of the boot loader that loads the boot manager from disk and runs it. This special sector on the disk is called the [*master boot record (MBR)*](#ch01.xhtml_key18-a).

The Linux boot block can be placed in the first block of the Linux partition if an existing operating system already occupies the MBR. In this case, the first boot manager needs to be told to pass control over to the Linux boot manager. It’s complicated, but this multi-booting allows two different operating systems to coexist on the same computer.

The boot manager displays a menu offering different operating system choices. Usually a default is chosen if no input is received within a short period of time, which allows a computer to boot unattended. Boot managers can also pass parameters to the kernel, such as to initialize hardware differently, disable problematic features, or alter the boot sequence.

Several boot managers are available, but most distributions have standardized on the [*Grand Unified Boot Loader (GRUB)*](#ch01.xhtml_key19-a), which is currently in version 2, aka GRUB2.

Note

The exam will focus on GRUB2, but it's important to know where GRUB came from, and what the differences are between original GRUB and the newer GRUB2.

#### GRUB Legacy

In the early days of Linux, the boot manager was simple: You would boot a kernel either from an existing Microsoft DOS system through **LOADLIN.EXE** or directly with the Linux Loader (LILO). The latter was fairly inflexible. While you had a basic menu system, any changes needed to be made by rewriting the boot manager to disk. Even the location of the kernel blocks on disk needed to be known beforehand. LILO would have to generate a list of blocks containing a kernel and write them to a known place so that it could piece the kernel back together on boot.

Eventually the GNU Foundation started work on GRUB. This boot manager is more flexible than others because it offers an interactive menu that can be easily changed and adapted to boot many operating systems. GRUB understands different filesystems, and it can read the kernel from disk as if it were a file instead of needing to know where the individual blocks are.

GRUB uses a temporary boot volume, **/boot** by default, to store kernels and the GRUB configuration. A BIOS might not be able to see the whole disk, so putting the boot manager in a safe area means that it can boot a kernel that has the functionality to read the entire disk.

#### GRUB2

GRUB2 is the version of GRUB currently in use, and it has been the default for most distributions since about 2010\. GRUB2 started out as a core rewrite for stability and features and quickly became what is now known as GRUB2\. Those who are familiar with GRUB will quickly understand GRUB2’s syntax, commands, and structure; they are fairly similar, aside from a few filename and location changes and a number of important and handy features.

##### Changes Made for GRUB2

One of the core changes in GRUB2 is the name of the configuration file, which has changed from **menu.lst** or **grub.conf** in GRUB to **grub.cfg** in GRUB2\. In addition, in GRUB2 the main configuration file (**/boot/grub2/grub.cfg**) is generated by the **grub-mkconfig** command or the installation routine. Because of how system updates are currently done, your **/boot/grub2/grub.cfg** file may be regenerated by a kernel or another system update, so to be safe, there are two locations where customizations can safely be stored so they are available after any automated changes to the **/boot/grub2/grub.cfg** file. Those two locations for any customizations (entries or parameters) are the **/etc/grub.d/40_custom** file and the **/boot/grub/custom.cfg** file. These files are read by the **grub-mkconfig** command and used when generating the **/boot/grub2/grub.cfg** file.

Another change from GRUB to GRUB2 is a change in how partitions are numbered. GRUB used fd/hd to denote disks, and the first hd on a device was labeled hd0; the first partition on that device would be referred to as hd0,0\. This has changed in GRUB2 so that partitions start with the numeral 1, while devices still start with 0.

In addition, the filename **/etc/grub2.cfg** is a symbolic link to the grub.cfg file for compatibility purposes.

![Images](graphics/key_topic_icon.jpg)

##### GRUB2 Command Names

A quick mention of the command names for GRUB2 is in order. While the documentation may leave the **2** designation off the commands (for example, **grub-install** vs. **grub2-install**), some distributions use the version number in the command names, and others don’t. For example, Ubuntu doesn’t use the **2** in the command names, but Fedora and CentOS do. The easiest way to find out what a distro uses is to type the **grub** portion of the command and press the **Tab** key twice to get output like that shown in [Example 1-1](#ch01.xhtml_exe1_1).

**Example 1-1**–Example of the **grub**-Related Commands on a System

```
root@tuxix:/boot# grub
grub                    grub-mklayout
grub-bios-setup       grub-mknetdir
grub-editenv          grub-mkpasswd-pbkdf2
grub-file              grub-mkrelpath
grub-fstest           grub-mkrescue
grub-glue-efi         grub-mkstandalone
grub-install          grub-mount
grub-kbdcomp          grub-ntldr-img
grub-macbless         grub-probe
grub-menulst2cfg      grub-reboot
grub-mkconfig         grub-render-label
grub-mkdevicemap      grub-script-check
grub-mkfont           grub-set-default
grub-mkimage          grub-syslinux2cfg
```

As you can see, this distribution doesn’t use the **2** version designation behind the **grub** portion of the command.

##### Installing GRUB2

The first step in getting GRUB2 installed is to have the tool write itself to the master boot record as follows:

```
[root@localhost ~]# grub2-install /dev/sda
Installing for i386-pc platform.
Installation finished. No error reported.
```

This copies the boot sector image to disk and the remaining files to **/boot**. If your bootable partition is not **/boot**, you can override this default setting, such as **/mnt/tmpboot** in [Example 1-2](#ch01.xhtml_exe1_2).

**Example 1-2**–Installing GRUB2 to an Alternate Location

```
[root@localhost ~]# grub2-install
--boot-directory=/mnt/tmpboot/dev/sda
Installing for i386-pc platform.
Installation finished. No error reported.
[root@localhost ~]# tree -d /mnt/tmpboot/
/mnt/tmpboot/
|−-- grub2
 | - - fonts
 | - - i386-pc
 |−-- locale
 4 directories
```

In [Example 1-2](#ch01.xhtml_exe1_2) the GRUB2 files are installed to **/mnt/tmpboot**, and the **tree** command shows the directories created for the boot manager. The GRUB2 image and related modules are inside the **i386-pc** directory.

This alternate boot disk option is most often used for making boot disks on an existing system, where you will have an image of the disk temporarily mounted.

##### Using the GRUB2 Command Line

Your first interaction with the GRUB2 command line is during the boot process. When you boot a computer, you see the **GRUB2** menu offering a list of kernels to boot and an option to enter the **c** character to get to the command line. Pressing this gets you to a simple command prompt:

```
grub>
```

If you can’t boot normally, you can use the GRUB2 command line to inspect your running system and get a kernel booted. You can look at the list of devices with the **ls** command:

```
grub> ls
(proc) (hd0) (hd0,gpt2) (hd0,gpt1) (hd1) (cd0)
```

The syntax of the partitions is similar to the Linux partition naming syntax. It’s important to remember that disks are counted from 0, but partitions are counted from 1\. So the first partition on the first disk is hd0,msdos1, which corresponds to sda1 in Linux. It is often difficult to know which partition contains the files you want, so you can inspect each. The shell does not provide wildcards, though you can press the **Tab** key as a substitute:

```
grub> ls (hd0,msdos1)/vml<TAB>
```

Possible files are

```
vmlinuz-0-rescue-1bc6a0e5dd394f63b228657b634ba252
vmlinuz-3.10.0-862.14.4.el7.x86_64
```

Note

If you are new to Linux, you might find these naming inconsistencies confusing. Linux tools are developed by different people with different ways of doing things. Devices in the Linux kernel are fairly consistently named, but GRUB is developed by a completely different set of people with a different set of goals. GRUB was designed to boot different operating systems, so some concepts don’t line up directly with the way things are done in Linux.

The **Tab** key looks on the device for any files beginning with **vml**, which are kernel files. Two are shown here. If you know, based on the name, that the second one is the kernel to boot, you can give GRUB enough information to boot it by supplying the name of the kernel and the name of the corresponding initial RAM disk. The initial RAM disk, abbreviated initrd, contains the extra drivers necessary to boot the kernel on the specific hardware the kernel is running on.

By using the **Tab** completion, you can discover your way to the proper kernel and initramfs to use, and then when those are set, you can type **boot**, and it should boot properly. Here is an example:

```
grub> linux (hd0,gpt2)/ vmlinuz-5.4.0-91-generic
  genericroot=/dev/mapper/fedora-root ro
grub> initrd (hd0,gpt2)/ initrd.img-5.4.0-91-generic
grub> boot
<boot process output truncated>
```

While several parameters are involved in booting the kernel, they are already in the **grub.cfg** file, which you can view by using the **cat** command or searching on the Internet. The kernel can take many parameters, but it is important to pass the path to the root filesystem (**root=**), and that filesystem should initially be booted read-only (**ro**).

In the early days of Linux, a problem with a boot manager meant that you needed to find a CD or floppy disk containing Linux so that you could boot and begin recovery. GRUB2’s command line means that you can still get into your system and fix it up more quickly.

##### Demystifying Kernel Images

You can’t spend much time in the kernel booting configuration world without encountering two apparently random versions of the kernel: vmlinuz and vmlinux.

In short, the vmlinux file is an uncompressed and statically linked kernel image file. This file was used primarily in earlier kernel days. The file is fairly small and can be loaded into the free space in lower RAM. Having to load into lower RAM limits the size of the image to 512KB, as it has to fit in the lower 640KB of RAM.

The vmlinuz and vmlinux files are created by compiling the kernel using the zImage option, which produces a kernel that is designed to be uncompressed into that lower 640KB of RAM.

As the kernel grew in its capabilities and features, the kernel images also grew in size, and they quickly could not fit into the space available in lower RAM; thus, the vmlinuz method was adopted. The kernel is compiled with the bzImage option, which sounds like it’s related to bzip2 but isn’t. This produces a compressed kernel image, which is uncompressed shortly before it’s booted. This also means that the image will not fit into the lower RAM, so it must be loaded into higher memory (that is, above 1MB).

##### Configuring GRUB2

GRUB2’s configuration file is called **grub.cfg** (or **grub2.cfg** on some distributions). In this file, you find the configuration that sets up the menus you see when the system boots.

Note

GRUB uses menu.lst and grub.conf for configuration. The syntax changed between GRUB and GRUB2, and your distribution’s default may look more like code than a configuration file.

Configuring GRUB2 is more complicated than configuring GRUB. Whereas with GRUB you edit **grub.conf** and are done, with GRUB2, **grub.cfg** is generated with a script, and you must look to the scripts to see how to make your changes. The **grub-mkconfig** command generates the configuration file for you, optionally receiving a path to the output file. If you don’t specify a file, the output goes to your screen, as demonstrated in [Example 1-3](#ch01.xhtml_exe1_3).

**Example 1-3**–**grub-mkconfig** Command Output

```
# grub2-mkconfig -o /boot/grub/grub.cfg
Sourcing file `/etc/default/grub'
Sourcing file `/etc/default/grub.d/init-select.cfg'
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-5.4.0-91-generic
Found initrd image: /boot/initrd.img-5.4.0-91-generic
Found linux image: /boot/vmlinuz-5.4.0-80-generic
Found initrd image: /boot/initrd.img-5.4.0-80-generic
Adding boot menu entry for UEFI Firmware Settings
done

```

The inputs to **grub-mkconfig** are **/etc/default/grub** and the files in **/etc/grub.d/**. The former sets various defaults; the latter is a series of shell scripts:

```
# ls /etc/grub.d/
00_header    05_debian_theme  10_linux  10_linux_zfs  20_linux_xen
30_uefi-firmware  30_os-prober  41_custom  40_custom  README
```

Each one is run in order, and all their outputs are concatenated into the master output. If you want to add a custom section to your boot manager menu, look at the file named 40_custom for example, and either extend what you find there or add your own.

#### Common Commands at Boot Time

When booting Linux, you often want to change an option at the beginning of the process, such as changing the default *runlevel* or *target*, disabling or enabling specific hardware capabilities, or setting a particular mode for hardware that allows Linux to load properly.

Note

The parameters typed at the command prompt or boot options prompt are passed directly to the kernel upon initialization. These prompts are typically at the beginning of the boot process and give you the first opportunity to enter any parameters. Some distributions are configured to show a splash screen or logo, and you have to find out what keystroke allows for the entry of boot parameters.

The following are some common Linux boot options:

• **vga:** Enables you to set the framebuffer’s resolution to a given mode, such as **vga=2**, which was historically used for difficult laptop LCDs

• **apm:** APM (Automated Power Management) is on by default. Declaring **apm=off** or **noapm** at the beginning of the boot process enhances the system’s compatibility. This should be done only when indicated by a vendor or FAQ from a distribution provider.

• **init:** Specifying **init** at the start causes the **/sbin/init** process to be the first process to run on the system. This may not work properly on initialization schemes where **init** is not present.

• **panic=#seconds:** The kernel does not reboot by default after a panic error occurs, which can cause a system to sit disabled until a technician can reach it physically. If a panic occurs, the kernel waits the specified number of seconds and then reboots and attempts to load normally.

• **single or 1:** These options cause the system to skip a full initialization to a default runlevel, and instead the system goes into a troubleshooting or simple root-level state, where you are the root user and have minimal processes running.

• **2, 3, 4, or 5:** These options can be entered at the GRUB prompt to cause the system to initialize and then move to the specified runlevel or, in the case of systemd, move to the specified target that matches the runlevel number indicated.

• **ro or rw:** The **ro** option causes the root filesystem to be mounted in read-only mode so that **fsck** can be run on the root filesystem if errors occur. The **rw** parameter ensures that the root filesystem is mounted read/write, which is the default state.

• **mem=xxxxM:** This old system boot parameter simply sets the amount of memory that can be accessed by the about-to-be-booted system. You can use it when you suspect that a memory bank is bad or to test a system with a specific amount of memory, such as when testing a set-top box configuration or other limited-hardware device.

Note

You have to look at the boot parameter documentation for your given distribution and boot manager to find out exactly which options are appropriate.

### When Kernels Panic

The Linux kernel is a complex set of software and services. Things don’t always go smoothly. For example, something related to hardware, a driver, or a software package might misbehave, or memory addresses might be overwritten inappropriately.

Much as an ejection seat can get you safely out of a malfunctioning jet fighter, the kernel is designed to panic, or stop its operations when a condition or conditions have occurred that make continuing normal processing impossible.

#### Identifying a Kernel Panic

You can usually tell a [*kernel panic*](#ch01.xhtml_key04-a) has occurred based on several symptoms. The most common symptom is that the system shows a kernel panic message that typically consists of trace information about what was running at the time of the panic. Another common indication is mysterious reboots, often obscured to the sysadmin unless the log files contain helpful information about the issue.

Because of the severity of the issue that causes a kernel panic, it’s normally not possible for the system to continue functioning normally, so either the system has the panic and displays the tracing information to the console and stops otherwise functioning, or it reboots itself. Either way, one of the last things a system does in a panic situation is to attempt to write to the logs that a panic has occurred.

#### Getting More Information

If you are experiencing multiple kernel panics, one step you can take to try to get more information is to look in your system logging configuration and try removing the leading **-** from any of the targets (log files) so that logging disk writes are not cached or stored up to let other more important disk writes finish first.

![Images](graphics/key_topic_icon.jpg)

#### Kernel Panic Causes

What causes a kernel panic? There are unfortunately many possibilities, including the following:

• Corrupted hard disk sectors

• Incomplete or corrupted or truncated kernel modules

• File or directory permissions problems

• References to invalid or nonexistent memory addressed

• References to memory addresses that contain key codes

• Hardware failures, especially defective or failing RAM

• CPU failure or unhandled bugs

• Insertion or removal of hardware that causes conflicts, attempts to load defective, or incomplete modules

A cause that is often missed but occurs often enough to deserve special mention is system overheating; with either the hardware with a host OS on it or the underlying hardware for a virtualization or containerized system, physical overheating or cooling can cause the system to panic or halt to avoid further damage.

### Device Types in /dev

Devices live in the /dev directory, though what’s in there is really files that behave as device access points. When the system is booted, the kernel and it’s sub-processes will look through the BIOS and find the attached physical devices and then match those real devices to the appropriate special files in the /dev directory. Special files refers to the fact that these are NOT simple files or directories, they have a special meaning in that they are a connection point to real or pseudo devices on the system.

Device directory files are broken up into 4 main types, **block**, **character links** and **directories**. The main difference between block and character special files are how they send and receive data from what is attached to them.

A **block device** is communicated with by a driver and when doing so sends or receives an entire block of data at a time, a typical example being a disk, CD or DVD or other storage device, or something that has a filesystem on it, as those are made up of data blocks.

A **character device** sends and receives a single character at a time, and is characterized (see what I did there!?) by such devices as a scanner or a keyboard, things that communicate in non-block modes.

(sub)**Directory** files in the /dev directory usually lead to groups of special files that all are of a given type, an example being the /dev/input directory that will contain special files that pertain to devices that generate events, such as mouse pointers with their x-y coordinate events.

Link files in the /dev directory are fairly self-explanatory, they are files that are symbolic links or pointers to other files elsewhere on the system, such as the /dev/cdrom file which on our test system points to /dev/sr0 or the first SCSI-type CDROM detected on the system.

There are several pertinent (and testable!) individual files that exist in the /dev directory, including:

• **/dev/null:** The /dev/null special file is known as the “bit bucket” or the “black hole” of the system, it literally is a way to throw away output such as unwanted errors generated (in great quantities) by the find command etc. This is used only to discard either standard output or standard error.

• **/dev/zero:** The /dev/zero special file exists to provide an endless series of null characters or white space noise for the purposes of sending non-content data to a source for testing purposes, or for initializing a device with character data that doesn’t have any content. The /dev/zero special file is different than the /dev/null special file in that you can conduct read AND write operations with /dev/zero, while /dev/null can ONLY accept write operations, it cannot be read from.

• **/dev/urandom:** The /dev/urandom special file is there to produce cryptographic-level random number data for use when randomization of data is needed. The more noise gathered from various hardware sources, (fan noise variances, mouse movements, thermal noise, or anything that can be used to feed randomness to the generator. The numbers generated by /dev/urandom can be used to feed randomness into cryptographic key generation or anything that needs a steady supply of random characters.

In summary, there are a number of files in the /dev directory, tha main types of which are character and block special files, and some of the more important or key special files are the /dev/null, /dev/zero and /dev/urandom files describe previously.

### Installing Software from Source

[*Source code*](#ch01.xhtml_key06-a) is the heart of all computing, and access to that source is the linchpin of Linux and open source software. Without access to the source, you can’t inspect the code for bugs, security issues, or other flaws.

When programmers produce source code, they typically tar it up, or create a compressed archive called a tarball. [*Tarballs*](#ch01.xhtml_key07-a) are typically created with the **tar** command and some switches; then the software is made available on the Internet so others can try it and report bugs.

The following are advantages of installing programs via source code:

• It allows inspection of code for flaws, bugs, and security issues.

• It’s available earlier than binary packages.

• Compiling optimizes the resulting program for the current system.

• It feeds that cutting-edge need. (Beta testing can be fun!)

Typically, you don’t see a program that’s under heavy development in any format other than a source tarball. It’s time-consuming and unwieldy to make a package out of the source code until it’s at least of release or late beta stability.

After you’ve installed a program from source, you’ll be more comfortable with the process, so start with small programs and work your way up. For example, you might download and install rdesktop ([http://www.rdesktop.org](http://www.rdesktop.org)) and see the whole process in a couple minutes, including compile time.

The other end of the scale would be installing Apache or Samba from source, which is a much longer and more complex process.

The following are disadvantages of installing programs via source code:

• It requires a more complex installation.

• The necessary dependencies might not exist or might be very difficult to resolve.

• It’s often poorly documented, sometimes with only a readme or an install file available.

• Uninstalling source packages can be difficult, particularly if the package’s makefile doesn’t have an uninstall routine, which means you need to manually discover and remove the package files.

When installing from source, a number of conflicts and dependency problems can occur. Until a package is released by the various distribution vendors as a part of their products, it’s typically not for the faint of heart. If your goal is stability, wait for the eventual release; otherwise, you might spend hours searching for missing libraries and other needed files.

You should use source code installs when needed for performance and security.

![Images](graphics/key_topic_icon.jpg)

#### Components of a Source Code Install

Source code tarballs typically include the following:

• **Configure script:** This checks out the system and configures the makefile.

• [*Makefile*](#ch01.xhtml_key05-a)**:** This file governs the installation location, parameters, and other variables.

• **Source files:** These are the actual directories of the source files.

• **Readme:** The readme file contains important information about the installation process.

• **Install:** Typically, this contains the actual installation instructions; it’s not present in all source installs.

• **Install script:** This is often a single script that can be run to perform the installation.

#### The Makefile

A makefile is a set of instructions and compiling parameters that makes the installation possible. After it’s updated by the configure script, typically the **make** command and then the **make install** command are run to compile and install the software.

To quote the man page for **make**:

The purpose of the make utility is to determine automatically which pieces of a large program need to be recompiled, and issue the commands to recompile them.

![Images](graphics/key_topic_icon.jpg)

A makefile typically contains the following sections:

• **Platform:** The platform of the system

• **Debug:** How to handle errors

• **Optimize:** Items that are customized by **.configure**

• **Source:** Where the source files are found

• **Targets:** All, install, clean, dist, and so on

Targets of the makefile deserve a little attention because some confusion exists about what they consist of. The **make** command by itself usually compiles the source code but does not do anything else. Running the **make** command with the clean target usually removes any temporary files from a previous attempt to compile the code. If you run the **make** command with the install target, it puts the compiled code into the right directories in the path, continuing until the proper software has been installed.

A typical makefile has the following paths and variables (though this can vary from program to program):

```
install-prefix = .
bin_dir = $(install-prefix)/bin
uparm_dir = $(install-prefix)/lib/uparm
include_dir = $(install-prefix)/include
```

These instructions tell the installation and other targets where to put the various pieces of the program. **$(install-prefix)** indicates that, when it is compiled, the software is stored in the subdirectories of the current directory–for instance, **./bin**, **./lib/parm**, and **./include**.

#### Example of a Compilation of Source Code

In this example, a simple program is compiled and installed on a default Linux system. (You must have the gcc compiler and related development tools and libraries installed to compile source code.) Here’s how you do it:

**Step 1.** Open a browser and go to [http://www.rdesktop.org](http://www.rdesktop.org).

**Step 2.** Click the **Download** link.

**Step 3.** Click the latest stable version.

**Step 4.** Choose the location that’s closest to you from the list of download links, and then click the small page icon under the **Download** column at the right of the page.

**Step 5.** When prompted, put the source code in your user’s home directory. Usually all you have to do is click the **Save** button in the browser you’re using.

**Step 6.** Open a shell session or an xterm client.

**Step 7.** Navigate to the directory that contains the compressed file.

**Step 8.** Unpack the archive file.

**Step 9.** After the scrolling stops, change to the source directory:

```
cd sourcedir
```

**Step 10.** Run an **ls** command and notice what files are present.

**Step 11.** Run the configure script with the following command:

```
./configure
```

**Step 12.** Run the **make** command to compile the software.

**Step 13.** When the software is finished compiling, install the program with the **make install** command.

These are the basic steps needed to install an app or a command from source code. To prepare for the Linux+ exam, you don’t necessarily need to do an installation from source; just ensure that you are aware of the steps in a typical source installation, as shown here.

### Storage Concepts

![Images](graphics/key_topic_icon.jpg)

Before users can use a disk to store their information, a systems administrator must perform a few typical tasks:

**Step 1.** Install the device.

**Step 2.** Partition the device.

**Step 3.** Make a filesystem on the partition(s).

**Step 4.** Make or choose a mount point (directory).

**Step 5.** Mount the filesystem.

**Step 6.** Configure the filesystem to be mounted on boot.

**Step 7.** Set the permissions.

Linux devices are associated with a device file in the **/dev** directory. There are many preexisting files in this directory. As you saw earlier in this chapter, a hard drive has a corresponding device file similar to **/dev/sda**. This hard disk is referred to as a “raw device.” The device is partitioned into one or more partitions, such as **/dev/sda1**. A filesystem is applied to the partition, and then the device is grafted onto the rest of the filesystem to make the storage usable. Finally, the permissions are configured to allow the necessary people to access it.

#### Partitions

On most modern systems, there are two partition schemes you will use: the master boot record (MBR) and the GUID partition table (GPT). There are several differences between these two technologies, but the most important one is generally considered to be the partition structure itself.

Note

On the exam you can expect to be put into a scenario where you must identify the type of partition scheme being detailed and choose that answer from a list, or conversely, be told you're using a particular type and have to identify it's characteristics from a set of available answers.

##### MBR

Disks on systems that use MBR (master boot record) can have up to four primary partitions per disk, and in cases when you need more than four, one of the primary partition slots can be exchanged for an extended partition. The extended partition can then be divided further into more partitions, called [*logical partitions*](#ch01.xhtml_key20-a).

Only one extended partition can be used per disk. The extended partition can hold an unlimited number of logical partitions, although warnings abound to hold the number down to 12 or so.

The logical partitions inside an extended partition are virtually identical to a primary partition; they just happen to live only inside an extended partition. No perceivable difference exists between a primary partition and a logical partition except in the numbering, the position on disk, and the fact that the boot files for a Linux machine should exist on a primary partition.

Logical partitions exist to get around the four-partition MBR limitation.

##### GPT

The MBR partitioning scheme has been around for a very long time and provides a workaround to the x86 architecture limitation of four primary partitions. Modern systems support a newer partitioning scheme called GPT. Unlike with MBR, with GPT there is no limitation of four primary partitions. As a result, there is no need for extended or logical partitions.

With GPT there is only a limitation of 128 partitions. Note that some older partitioning tools, such as the **fdisk** utility, do not support GPT.

#### Data Storage Methods

Most computer systems have the same general method of storing data on storage devices, they may call it something different, but the underlying concepts and a lot of the practices are the same.

To summarize these methods, they are:

• Block Storage

• File Storage

• Object Storage

![Images](graphics/key_topic_icon.jpg)

##### Block Storage

File systems have traditionally used blocks, or block storage, to store data on disks or storage media. Blocks are treated individually, assigned an identifier that uniquely addresses that block and makes it easier to distribute or store data either in contiguous, non-contiguous or even cross-platform or cross-media.

Blocks make it so that the data is stored wherever it is, and the storage subsystem on the computing device is the one that tracks, accesses the blocks in the right order and from the proper location and makes the data on those blocks available for the higher-level storage mechanisms on the device.

Block storage, because of it's efficiency and reliability, is often associated with SAN (Storage Area Network) devices and is almost always either accessed via an access point by a client, or most often, used by attaching or "fronting" it with a server system that users will attach to, mount shared filesystems from and use for their remote network storage.

Block storage is read and written as a block, doesn't handle metadata except at a very basic level and is great for large chunks of data access, such as very large media files and databases. Block storage can be quite expensive, as well.

![Images](graphics/key_topic_icon.jpg)

##### File Storage

File Storage is a higher layer of storing data than Block Storage, in that a disk may be made up of blocks, evenly sized units of storage, and a filesystem will exist on top of a portion or all of that block storage, and contain what we are used to seeing as files, directories and hierarchical structures of these.

Files and Directories are very familiar to us, like a piece of paper would represent a file, and a directory would be a folder, or a drawer in a storage cabinet.

File Storage, or a filesystem full of files and directories will appear to be a single structure that we can navigate, access data from and make changes to, but that structure may actually consist of multiple file systems that are built on top of multiple different block devices, and may not be even remotely physically near each other, or the system they make up the heirarchical structure of.

File storage allows for files to be changed, updated, and modified at a very detailed level, such as updating a single word or many pages in a file, whereas a block would have to be changed as a block. File storage is good for reasonable sized data sets, but for very large data sets, block storage is better and faster.

![Images](graphics/key_topic_icon.jpg)

##### Object Storage

[*Object storage*](#ch01.xhtml_key08-a) is a much more complex and featureful method of storing data, in that it contains the most metadata or specific and actionable information about what it's storing. The example of a media file that has a number of different access levels for how people access it, but also may contain metadata about where that media file was produced, the software used, the author and much more.

Objects in this type of storage are almost completely self-contained, so where they are physically is much less important than how they inter-relate or fit together with other objects.

Object storage is typically accessed on an as-needed basis, making it cost-effective, and it's a favorite of the off-premise cloud providers. It's flat-heirarchy, suitability for non-dynamic data and ability to scale to tremendous data sets and the ability to use search criteria for finding the objects instead of large indexes to be read and parsed makes it very quick to find the objects that are desired.

Objects are only modifiable by writing or overwriting the entire object and they don't really play very well in mixed database environments as they are accessed and written to in very different manners.

#### FUSE (Filesystem in Userspace)

Traditionally, (which is a way of saying "some time ago!") filesystems had to be dealt with mostly or only in the kernel area of the operating system, which made it very difficult for a user to create their own filesystem. If the goal was absolute control over what happened on, say, a server system, then this scheme was likely to be a way to achieve a safer system, and therefore one that would be less likely (in theory) to crash because of some rash or ill-advised action of a mere user.

##### Why Use a FUSE?

[*FUSE*](#ch01.xhtml_key09-a), or Filesystem in Userspace is a way to allow filesystems to be created, as the name suggests, in the Userspace, or under the control of a mere standard user. Whereas a server system should be as predictable as possible for teh sake of making sure it's up and available as much as possible, many Linux systems are in the hands of end users, developers and many other types of users and having filesystems able to be created and managed solely by the user is very handy and powerful for many scenarios.

##### Handling FUSE User Requests

FUSE filesystems are governed by a program (a handler, or intermediary) that is the go-between for all actions that occur with the filesystem being created, managed or read and written upon. The handler program must be known to and interact with the kernel and when the filesystem is interacted with, the user request to the filesystem is sent from the kernel to the handler program, which to the handler program, which then interacts with the handled filesystem, and when it sends responses back to the user, those go back through the kernel and then are given to the user or process that was making the request.

![Images](graphics/key_topic_icon.jpg)

##### Possible FUSE Applications/Uses

The list of possible applications or uses where a FUSE is is desirable includes but is not limited to:

• NTFS (Windows Filesystem)

• LTFS (Linear Tape File System)

• Layered Filesystems (Overlay of a FUSE on a given filesystem)

• Virtual compressed Filesystems

• Backup and Archival Filesystems

• Remote Filesystems (JuiceFS, MooseFS, SSHFS among many)

• Distributed Filesystems (Lustre Clustering, GlusterFS, ObjectiveFS)

• Many other Filesystems with widely varied uses

Note

FUSE is also available for several uses on Windows systems, but that will not be a topic for the Linux+ exam!

#### RAID

[RAID](#ch01.xhtml_key10-a) or Redundant Array of Individual Disks is an important feature for server operators who need disk and storage to be as consistently available as possible for use on their systems. When a hard disk fails, typically all of the data on the disk is lost. Certain professionals might be able to recover some of the data, but that can be time-consuming and expensive, and ultimately the professionals might not be able to recover the data that you really need.

Redundant array of inexpensive disks (RAID) is a technology that was originally designed to provide a solution to the problem of hard disk failure. The original RAID (now called RAID 1) mirrored data between two hard disks. As a result, if one hard disk failed, the data still was available on the second hard disk.

![Images](graphics/key_topic_icon.jpg)

##### RAID Levels

Since the original RAID was created, several other RAID levels have been created, we are only including those in common practice:

• **RAID 0:** This level provides no redundancy but rather increases available storage by merging multiple hard disks (or partitions) into a single device. For example, three hard disks of 30GB each can produce a RAID 0 device with 90GB of storage space. Data is written to each physical device (hard disk/partition) in stripes, which results in the requirement of each physical device needing to be the same size to avoid wasting storage space. RAID 0 can improve the performance of reading data from the devices.

• **RAID 1:** This level is where two drives are mirrored and identical data is written to both devices, requiring two writes, but when data needs to be read from the RAID, then on spinning-disk storage the disk that has a read-write head closest to the data location is used, which can noticeably speed up data reads. The data volume is limited to the size of the least disk, and will not use additional space on mismatched disks.

• **RAID 3:** This level stripes data across several disks with a dedicated disk for that provides parity or data that can be used to keep the volume operational if a disk fails. This type of RAID has some significant drawbacks, as it requires disks to be in synchronicity and store data in the same locations on each disk. It's great for large contiguous uncompressed sets of data, but less than ideal for smaller read and write operations of a more random nature.

• **RAID 5:** This level provides more efficient use of the physical storage devices. Unlike RAID 1, which completely mirrors all data to all physical storage devices, RAID 5 writes different data to each physical storage device with the exception of one device, which is used to store parity data. In the event that a physical storage device is lost or damaged, the data on that device can be restored by using the parity data and the real data on the other storage devices. RAID 5 requires at least three storage devices and can have a negative impact on system performance, so software RAID (RAID performed by the kernel) is not commonly used. However, hardware RAID (RAID performed by a separate processing chip) is fairly common on high-end servers.

RAID devices are created by using the **mdadm** command, which is covered elsewhere. In terms of the current topic (device mapper and device file location), you should be aware that specific device names are associated with RAID devices. These device names begin with **/dev/md** and have a numeric value between 0 and 31\. When you used the **mdadm** command, you assigned your RAID to an “MD device,” such as **/dev/md0** or **/dev/md1**. (Note that *md* in this case stands for the phrase [*metadata*](#ch01.xhtml_key21-a).)

![Images](graphics/key_topic_icon.jpg)

##### Mirroring

In the world of RAID, [*Mirroring*](#ch01.xhtml_key11-a) (or RAID 1) is where you have two disks that are configured to appear as if they are a single disk, or a volume, often via software but also via hardware. As an example, two disks could be configured to appar as a volume would be partitioned, then have filesystems written on, and each disk in the volume would contain exactly the same filesystem and data, or what is called a Mirror.

Mirroring is very safe, since an entire disk can fail and there is an exact duplicate that can be used with little or no reconfiguration. Mirroring disks has the effect of slowing down writes, as there must be two write functions, one per disk, for each write to the volume or where the data is stored. Mirroring has the opposite effect on reads from the disks, as the system will read from whichever disk is going to produce the fastest access to the data desired.

Note

Mirroring works slightly differently on SSD (Solid State Device) disk storage, but the concept of Mirroring is effectively the same on either type of device used.

![Images](graphics/key_topic_icon.jpg)

##### Striping

The concept of [Striping](#ch01.xhtml_key12-a) is where you store segments or stripes of data across multiple devices, so that any given stripe of data blocks can be read more efficiently by issuing multiple reads or writes through the disk controller to the devices that are storing the stripes of data.

Like Mirroring, Striping was invented and implemented primarily on spinning platter disk storage devices, it's less noticeable or effective on Solid State Drives, since they do not have spinning platters or read-write heads that can be in any position. Reading and writing data from SSD's is a matter of issuing the read or write request for the location the data exists or will exist.

Another use for Striping is to take two disks and combine their aggregate storage space into a single volume or make them appear to be a single disk that is the addition of their individual sizes minus the usual space dedicated to format structure.

Striping (or RAID 0) can result in a larger virtual or apparent disk (N+N) and can also result in faster access times because of the multiple possible reads or writes occurring simultaneously or closely in parallel. The main danger of Striping across multipl disks to build a larger volume is that the loss of any of those devices will result in the loss of access to the entire volume. Imagine a bridge with 3 main supports across a river and one of those main supports is removed, it makes no difference if the other two remain, the integrity or ability to use the volume or bridge is lost.

![Images](graphics/key_topic_icon.jpg)

##### Parity

Now that we have both Mirroring and Striping defined and (hopefully) demystified somewhat, let's put them together with the concept of [*Parity*](#ch01.xhtml_key13-a), where at least one disk is used to provide fault tolerance for a RAID volume.or the use of at least a third disk or device to contain enough of each of the first two to maintain access to the volume that contains the filesystem and data.

An very simple example of this would be having 3 disks in a system, and using all three in a RAID 3 arrangement. Disk 1 and Disk 2 would be the disks where the volume and data is stored and Disk 3 is calculated to hold enough of BOTH of Disk 1 and Disk 2 data to maintain access to and the integrity of the data volume if one of them were to fail.

Putting all of this together, a RAID 5 disk arrangement would include BOTH Striping of data across the involved disks, as well as storing Parity data so that any of the 3 disks could fail and the data volume would still exist and be usable.

Note

RAID can go from simple to very complex is a short order, so keep in mind the various levels as you are preparing for the exam, you'll likely see questions that refer to the levels we mention, RAID 2, 4, and 10 in particular are very specialized and not common usages.

### Listing Your Hardware Info

Your running Linux system contains a treasure trove of important information, and you can easily query that information using a set of commands mostly known as the "ls*" commands.

The primary source for the information about a running Linux system is from the **/proc** directory, but it's a very large heirarchical tree of files, directories and cryptic numbers, so the **ls*** commands are a great way to mine that set of information.

##### The Proc Filesystem

Unix has a philosophy that “everything is a file,” and this means, in part, that hardware information and state information for both the system and processes are exposed on the filesystem. In Linux this started off as **[procfs](#ch01.xhtml_key14-a)**, which is usually mounted on **/proc**. In this directory, you find that each process on the system has a directory containing information about itself. Features that must keep state to work, such as a firewall that tracks network connections being handled by the system, also expose their information through **/proc**.

In addition, **procfs** contains details about the hardware in the system. Files such as **/proc/ioports**, **/proc/dma**, and **/proc/interrupts** can show an investigating user or a sysadmin a lot of pertinent information about the system’s configuration.

Incidentally, **procfs** is called a pseudo-filesystem. It looks like a device but doesn’t exist on any real hardware. It’s simply a way of exposing kernel information to the user in a well-defined format.

When errors or conflicts occur, a number of commands are essential to resolving the conflicts shown in the output. Viewing information straight from the **/proc** directory is accomplished with the following commands:

```
cat /proc/interrupts
cat /proc/ioports
cat /proc/dma
cat /proc/usb
cat /proc/pci
```

In addition, a series of commands beginning with **ls*** gather the same information and present it in a more human-readable format.

Note

On the Linux+ exam there are 3 main utilities, **`lsusb`**, **`lspci`** and **`dmidecode`**, but it's very important to know ALL the commands that are able to show you information about your system, so you'll see the rest of the notable ones as well.

![Images](graphics/key_topic_icon.jpg)

##### Notable **ls*** Commands

The pertinent commands are as follows:

• **lscpu:** Provides details about the CPU, such as the number and speed of each socket and core.

• **lspci:** Shows a lot of information about the PCI bus and devices. It can identify devices on the bus that the kernel doesn’t know about and provides addressing information for configuring them.

• **lsscsi:** Shows information about the SCSI devices on the system, if the system supports SCSI. This tells you whether the system can see the disk.

• **lsdev:** Shows the devices recognized by the system.

• **lsraid:** Displays the RAID devices on the system.

• **lsusb:** Displays the USB information and devices for the system.

• **lsblk:** Displays the block devices (disks) attached to the system.

• **dmesg:** Displays the “kernel ring buffer,” which is a collection of messages that were created during the boot process. This is a great tool for determining what devices were recognized by the system during booting.

![Images](graphics/key_topic_icon.jpg)

##### Friends of procfs

Mining the **`/proc`** directory and it's contents, (mounted via the procfs filesystem), is the most popular way to expose kernel information to users, but there are more options. The files under **`/proc`** are unstructured and contain information about both processes and devices. The goal of **[sysfs](#ch01.xhtml_key15-a)** is to solve some of these shortcomings by migrating device data to **`/sys`**. Data still can exist on both, and the device tools such as **`lspci`** still use **/`proc`**.

##### The **dmidecode** Command

The **dmidecode** command works primarily with the **/`sys`** directory and it's contents, and is one of the items you are likely to see on the Linux+ exam, so let's look at what it is, where it's going to get it's information and what you can do to better display all of this amazingly detailed and voluminous system information!

![Images](graphics/key_topic_icon.jpg)

##### Displaying DMI Table Information

The **dmidecode** command is designed to query the [*DMI*](#ch01.xhtml_key16-a) (Desktop Management Interface) Table, which contains information gathered from the System BIOS and represented in an in-memory table or set of tables that allow processes and commands to access that information without having to resort to a direct hardware query.

To better understand what's being queried and displayed by the **dmidecode** command, think of most of the information being returned as following this format:

```
Handle, Type, Size
Decoded Value
```

An example of an entry the **dmidecode** command would return is:

```
Handle 0x0005, DMI type 16, 23 bytes
Physical Memory Array
       Location: System Board Or Motherboard
       Use: System Memory
       Error Correction Type: None
       Maximum Capacity: 4 GB
       Error Information Handle: Not Provided
       Number Of Devices: 1
```

As you can see, the first three items are on the first line, with the Handle being a unique identifier in the table, the type showing where the information came from and the size being how much information is in that entry in the table.

A great way to familiarize yourself with what is displayed by the **dmidecode** command, (and what's in your system's DMI Table!) is to funnel the 100+ lines of output dmidecode typically returns through a pager like the **less** command, such as running this command:

```
$ sudo dmidecode | less
```

This will display the information gathered from the DMI Table in the context of the less pager, where you can scroll up and down, use PGUP and PGDN, Home and End and do some searching if that suits your needs!

Note

It is very important to remember when a command can be run as a standard user and when it must be run as either the root user or via a privilege elevation mechanism such as the **sudo** command. The Linux+ exam writers are aware of the difference between running a root-level command as a standard user and as a root-level user, so watch closely for that distinction on the exam!

### Summary

On the Linux+ exam you may be asked to read a scenario, and then from the scenario determine the most effective, or fastest, or most secure storage method from a list of options. You should know these methods well enough to be able to identify them from a description of their use, as well.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 1-3](#ch01.xhtml_ch01tab3) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 1-3**–Key Topics for [Chapter 1](#ch01.xhtml_ch01)

![Images](graphics/01tab03.jpg)![Images](graphics/01tab03a.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[subdirectories](#ch01.xhtml_key01)

[initrd](#ch01.xhtml_key02)

[initramfs](#ch01.xhtml_key03)

[kernel panic](#ch01.xhtml_key04)

[makefile](#ch01.xhtml_key05)

[source code](#ch01.xhtml_key06)

[tarball](#ch01.xhtml_key07)

[object storage](#ch01.xhtml_key08)

[FUSE](#ch01.xhtml_key09)

[RAID](#ch01.xhtml_key10)

[Mirroring](#ch01.xhtml_key11)

[Striping](#ch01.xhtml_key12)

[Parity](#ch01.xhtml_key13)

[procfs](#ch01.xhtml_key14)

[sysfs](#ch01.xhtml_key15)

[DMI](#ch01.xhtml_key16)

[Basic Input Output System (BIOS)](#ch01.xhtml_key17)

[master boot record (MBR)](#ch01.xhtml_key18)

[Grand Unified Boot Loader (GRUB)](#ch01.xhtml_key19)

[logical partitions](#ch01.xhtml_key20)

[metadata](#ch01.xhtml_key21)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** To change the configuration of the GRUB boot loader, which of the following files would you edit?

**a. /grub/grub2.config**

**b. /etc/boot/grub**

**c. /etc/sysconfig/grub/boot**

**d. /boot/grub2/grub2.cfg**

**2.** Your Linux server installs correctly, but when you try to boot it, you cannot see the specialized disk subsystem that it installed to. Which of the following commands will be helpful in fixing this situation? (Choose two.)

**a. zImage**

**b. dracut**

**c. mkinitrd**

**d. initramfs**

**3.** You are looking for the numbered set of directories that represent your system's running processes, which of the following directories would most likely contain them?

**a. /sys**

**b. /proc**

**c. /run**

**d. /tmp**

**4.** Your server system seems fine, it’s backed up often, and its power is provided via UPS (uninterruptible power supply), but upon inspecting your logs and system uptime, you determine that it’s rebooting at least once a day. Which of the following best describes what is happening?

**a.** Scheduled updates

**b.** Compromised security

**c.** Kernel panic

**d.** System of a Down

**5.** Which of the following IS an advantage of using source code to install your system software instead of packaged software?

**a. Ease of updating software**

**b. Software version control**

**c. More compatible**

**d. Specific configuration control**

**6.** There is a set of in-memory tables which contain information gathered from the System BIOS and allows processes and commands to access that information without having to resort to a direct hardware query. Select the most likely command you can use to display these tables?

**a. dmidecode**

**b. lspci**

**c. lsusb**

**d. lsdev**

**7.** What kind of data storage allows for files to be changed, updated, and modified at a very detailed level, such as updating a single word or many pages in a file?

**a. Block storage**

**b. Object storage**

**c. Line storage**

**d. File storage**

## Chapter 2\. Managing Files and Directories

This chapter covers the following topics:

• [File and Directory Operations](#ch02.xhtml_ch02lev1sec03)

• [File Metadata and File Types](#ch02.xhtml_ch02lev1sec04)

• [Soft and Hard Links](#ch02.xhtml_ch02lev1sec05)

• [File Compression, Archiving, and Backup](#ch02.xhtml_ch02lev1sec06)

• [Copying Objects Between Systems](#ch02.xhtml_ch02lev1sec07)

• [File Editing](#ch02.xhtml_ch02lev1sec08)

The exam objectives covered in this chapter are as follows:

**Objective 1.2:** Given a scenario, manage files and directories

Management of files and directories is very important on a Linux system, as literally every single thing on a Linux system is a file of some kind, and directories are files of the type directory.

Properly managing these objects includes many things, such as knowing more about what you are managing by displaying information about the files, their contents, creating, altering the details editing the contents of them, determining file types and gaining insight by displaying deeper information that normally shown.

The concept of editing files being part of managing them is not as odd as it might seem, you definitely have to manage files when you are doing a lot of editing, and many times you must be aware of file creation, deletion, transforming them, and displaying them differently than they currently exist.

Managing files also includes the important step of copying or moving them from system to system, typically without losing their important attributes such as permissions, ownership and other critical details.

Managing by knowing how to comppress, uncompress, and backup your files is a skill that can make your day, or break your career, depending on what the situation is. Data in files can be mundane, have little or no value, or be the expression for intellectual property or national secrets that have immense importance, all located in a lowly text or formatted file. Losing important data can be at the very least inconvenient, and at the very worst cause loss of revenue, business opportunities and even result in life-changing circumstances.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 2-1](#ch02.xhtml_ch02tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 2-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/02tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** You are currently in the directory **/home/user1/subdir1** and need to navigate to the directory **/home/user3**. Which of the following commands will accomplish this? (Choose two.)

**a. cd home/user3**

**b. cd ~/user3**

**c. cd ../../home/user3**

**d. cd ../../../home/user3**

**2.** Which command will show you the three file dates and times kept in metadata when used on a file or directory?

**a. file**

**b. ls -li**

**c. stat**

**d. info**

**3.** Which of the following situations would prevent you from creating a hard link?

**a.** The link spans filesystems.

**b.** The source of the link is a hidden file.

**c.** The source of the link is a device file.

**d.** The source of the link is a directory.

**e.** The destination contains special characters.

**4.** You want to display the contents of a .tar.gz compressed file. Which of the following commands would show you the contents, along with the file particulars as if you had display them with the ls command?

**a. tar -czvf file1.tar.gz**

**b. tar - xzvf file1.tar.gz**

**c. tar -tzvf file1.tar.gz**

**d. tar -lzvf file1.tar.gz**

**5.** You want to copy a file in your local directory to the home directory of the mortimer user on a remote system. Which of the following commands would result in this action?

**a. scp ~file1 @192.168.10.10:mortimer**

**b. scp ./file1 mortimer@192.168.10.10/home/mortimer:**

**c. scp file1 mortimer@192.168.10.10:~**

**d. scp mortimer:file1 < scp @192.168.10.10**

**6.** In the VIM editor, instead of using the up and down arrow keys, you can use what keys?

**a. k** for up and **j** for down

**b. j** for up and **k** for down

**c. Ctrl+D** for down and **Ctrl+U** for up

**d. j** for up and **h** for down

### Foundation Topics

Linux (and it's antedecent UNIX) systems are almost exclusively constructed of files, be they regular files such as text, graphics, databases, device files such as block or character types, binary program or executable script files, and let's not forget a very important type of file, that of directory files.

System operators who will be dealing with files and systems made up of files for most of their work life must know how to properly do a large number of file and directory-related tasks, including creating, modifying, deleting, listing, displaying the contents of, viewing, changing and setting permissions on, archiving, unarchiving, compressing, and transforming files.

Additionally, system operators need to be able to create empty files, edit many different types of files to change their contents and also be able to navigate all around their systems using the tools available, such as the **cd** command, the directory indicates (. and ..) and how to view their file and directory structures in helpful and efficient ways using such utilities as the **tree** command and mc, (Midnight Commander.)

### File and Directory Operations

Note

The Linux+ objectives have the topics listed in an order that is simply not the best flow for what we have to do here, so I have thoughtfully rearranged the topics to flow naturally and make the most sense, just like I would with any set of objectives.

Being able to properly work with files and directories on a Linux system is as important as any other task, as a major amount of any time spent with a Linux system is spent working at the command line. As a good sysadmin, you are expected to know how to create, delete, edit, set permissions, display, move, copy, link and unlink, find and locate, determine the type of files and programs, and even determine the differences between two sets of files and directories.

![Images](graphics/key_topic_icon.jpg)

#### Tips for Working with Linux Files

Because most users and sysadmins come from a Windows or other OS background, a quick set of recommendations for less-experienced Linux sysadmins can be of help here:

• **Hidden files aren’t really hidden:** They just begin with a **.**, such as the **.bashrc** and **.bash_profile** files. They are normally not visible unless you explicitly ask for them to be displayed, and they aren’t deleted by commands such as **rm -f *.***.

• **Filenames can contain multiple periods or no period characters:** The filenames **this.is.a.long.file** and **thisisalongfile** are perfectly reasonable and possible.

• **Spaces in filenames look nice but are a pain to type:** Use an **_** or a **-** instead of spaces because it’s neater and easier than prefixing all spaces with a **\**. (To display a space in a filename, the system shows a space prefixed with a backslash.)

• **File extensions aren’t mandatory:** However, they are useful for sorting, selection, and **copy/move/delete** commands, as well as for quickly identifying a file’s type.

#### Basic Navigation

The command to change the current working directory, **cd**, is used frequently, and knowing how to move around the filesystem is a main focus of the Linux+ exam.

The following command simply moves you from wherever you are to the **/etc** directory. This type of move uses [*absolute pathnames*](#ch02.xhtml_key01-a) and can be used from within any directory:

```
# cd /etc
```

The path is called absolute because it defines a path starting at the root of the filesystem. You can quickly see that a path is absolute if it starts with a slash (/).

Moving from the current directory to a subdirectory is quick and easy. For example, here is how you can change into the **/etc/samba** directory from your current position in the **/etc/** directory:

```
# cd samba
```

This is referred to as a [*relative path*](#ch02.xhtml_key02-a) because the option you pass to the **cd** command is relative to the current directory. You are in **/etc**, and moving to **samba** gets you in **/etc/samba**. If you were in **/home** and ran **cd samba**, it would not work unless **/home/samba** also existed.

If you get confused about where you currently are, use the **pwd** command to print the working (current) directory:

```
# pwd
/etc/samba
```

By itself, the **cd** command takes you back to your home directory, wherever you happen to be. The tilde (~) also means “home directory,” so **cd ~** takes you to your home directory, and **cd ~sean** takes you to Sean’s home directory.

#### Advanced Navigation

It’s good to get experience with some complex relative path situations. For example, say that you are in the directory **/home1/user1** and want to move into the directory **/home2/user2**:

```
# tree /
/
|-- home1
| `-- user1
`-- home2
 `-- user2
```

#### Which Command Would You Use?

Remember that you aren’t using absolute pathnames, just relative pathnames. The answer is

```
# cd ../../home2/user2
```

Each of the **..** pairs takes you up one level: The first takes you to **/home1**, and the second puts you at the root. From there, it’s relative pathnames. Practice this method and remember that going up one level in this exercise only gets you to the **/home1** directory. This is a relative path because the path does not start with a /. The directory where you end up depends on where you started.

Although this example of relative and absolute pathnames was used to look at changing directories, it applies to any situation where you’re prompted for a filename.

Additionally, you can use the single dot character to denote the current directory, such as if you are trying to run a **find** command that uses the current directory as the path portion of the **find** command's arguments, like the following:

```
# find ./ -iname "*.txt"
```

This command will start searching in the current directory, wherever that is, and extend it's search below. The . character is also extremely helpful when copying or moving something to the current directory, such as the following command that would copy the /etc/hosts file to the current directory:

```
# cp /etc/hosts .
```

As you can probably imagine, there are any number of command situations where being able to refer to the current directory is very helpful, so remember not only .. for the upper level directory, but . for the current directory!

#### Listing Files and Directories

The **ls** command is used for listing directories or files or both.

If you use the **ls** command to see multicolumn output of the current directory, only the file or directory names are shown, not other details about the file:

```
# ls
file1 file2 file3 file4
```

Use the **-l** (long) listing option to see all the details of a particular file or directory or set of files or directories in a single column, like so:

```
# ls -l
total 0
-rw-r--r-- 1 root root 0 Jan 24 18:55 file1
-rw-r--r-- 1 root root 0 Jan 24 18:55 file2
-rw-r--r-- 1 root root 0 Jan 24 18:55 file3
-rw-r--r-- 1 root root 0 Jan 24 18:55 file4
```

Using the **-l** option is the only way to use the **ls** command and see the permissions, ownership, and link counts for objects. The only other command that can give such information is the **stat** command, which shows a single filesystem object at a time.

Other examples of using the **ls** command include

• **ls /home/user:** Shows a plain listing of the specified directory.

• **ls -a:** Lists all files, including hidden **.** files.

• **ls -d foo:** Lists just the directory called **foo** and not the contents.

• **ls -i:** Lists the inode number for the target file or directory. Linux uses inodes to represent files on disk; inodes are discussed later in this chapter, in the section *Copying Files and Directories*.

• **ls -l:** Shows permissions; links; and date, group, and owner information. [*Permissions*](#ch02.xhtml_key03-a) dictate who can access the file and are discussed in detail in [Chapter 12](#ch12.xhtml_ch12), Understand and Apply Access Controls.

• **ls -lh:** Shows human-readable output of file sizes, in kilobytes, megabytes, and gigabytes, along with file details.

Chaining together the options produces useful results. For example, if you needed to see all the files (including hidden ones) in the current directory, their permissions, and their inode numbers, you would use the following command:

```
# ls -lai
290305 drwxr-x--- 13 root root 4096 Jan 24 18:55 .
 2 drwxr-xr-x 20 root root 4096 Jan 24 17:56 ..
292606 -rw-r--r-- 1 root root 1354 Jan 21 00:23 anaconda-ks.cfg
292748 -rw------- 1 root root 3470 Jan 24 18:16 .bash_history
290485 -rw-r--r-- 1 root root 24 Jun 10 2000 .bash_logout
290486 -rw-r--r-- 1 root root 234 Jul 5 2001 .bash_profile
290487 -rw-r--r-- 1 root root 176 Aug 23 1995 .bashrc
290488 -rw-r--r-- 1 root root 210 Jun 10 2000 .cshrc
```

![Images](graphics/key_topic_icon.jpg)

#### Globbing Files

The asterisk (*) symbols you see being used by many commands including the **ls** command is known as a [*glob*](#ch02.xhtml_key05-a). A glob is a wildcard operator that matches some number of files based on a pattern. **/etc/*** matches all files in the **/etc** directory, such as **/etc/foo** and **/etc/bar** but not **/etc/foo/bar**, because this really means a file named **bar** in a subdirectory named **foo**.

One thing that’s distinct about Linux (and all Unixes) is that the shell is responsible for expanding the glob to the list of files it matches. If you type **ls /tmp/thing*** and there are two files that start with **thing**, such as **thing1** and **thing2**, it’s the same as if you typed **ls /tmp/thing1 /tmp/thing2**:

```
$ ls thing*
thing1 thing2
```

This [*globbing*](#ch02.xhtml_key06-a) feature makes renaming a group of files more difficult. In Windows you could type **ren *.foo *.bar**, and any file with the extension **foo** would then have the extension **bar**. In Linux, typing **mv *.foo *.bar** would expand the globs to the list of files matched: ***.foo** would match the files you want to rename, and ***.bar** would match nothing. This is different from what you might expect! The following output shows this problem:

```
$ ls *.foo *.bar
ls: *.bar: No such file or directory
file1.foo file2.foo
$ echo mv *.foo *.bar
mv file1.foo file2.foo *.bar
$ mv *.foo *.bar
mv: target `*.bar’ is not a directory
```

In the output, the first command shows that there are three files with the extension **foo** but none with the extension **bar**. The **echo** command displays the output that follows it, such that it shows what would be executed if you ran the **mv** command by itself. The ***.bar** glob shows up because there are no files that match it. The error happens because there is not a directory called ***.bar**.

There are other glob operators. [Example 2-1](#ch02.xhtml_exe2_1) shows some uses of file globs.

**Example 2-1**–Examples of Using Globs

```
$ ls
file file1 file10 file11 file2
$ ls file*
file file1 file10 file11 file2
$ ls file?
file1 file2
$ ls *1
file1 file11
$ ls file[123]
file1 file2
```

[Example 2-1](#ch02.xhtml_exe2_1) starts by listing all the files in the directory. The same list of files is also available with **file***, which matches the word **file** followed by anything or nothing at all. Note that it includes the bare name **file**. Next, the **file?** glob matches anything starting with the word **file** and followed by one character. Both **file** and the files with two-digit numbers in their names are excluded.

Note

A glob doesn’t have to appear at the end of a filename. For example, ***1** matches anything ending in the number 1.

Finally, **file[123]** uses the square bracket operator that means “any one character from the set.” It matches **file1** and **file2**.

#### Touching Files

The **touch** command seems odd at first, but it comes in handy often. You give it the name of one or more files, and it creates the files if they don’t exist or updates their timestamps if they do.

There are various reasons to use the **touch** command, such as to create a new blank log file or update a file’s modification time to use as a reference, such as to know the last time a job was run.

To create a new file, you can use the relative pathname for creating one in the current directory:

```
# touch filename
```

Or you can use the absolute pathname to create the file, such as shown here:

```
# touch /home/ross/filename
```

As you prepare for the Linux+ exam, expect to see **touch** for log file creation, along with the use of a reference file to mark the last backup. In other words, if a log file is created from a successful backup, that file can be used as a date and time reference file because it occurred at a desirable time.

When you use **touch** on an existing file, the default action is to update all three of the file’s times:

• **access:** The last time a file was written to/read from

• **change:** The last time the contents of the file were changed or that the file’s [*metadata*](#ch02.xhtml_key08-a) (owner, permission, inode number) was changed

• **modify:** The last time the file’s contents were changed

A programmer preparing a new release of a software package would use the **touch** command to ensure that all files have exactly the same date and times. Therefore, the release could be referred to by the file date, given multiple revisions.

Setting a file’s date is relatively easy; the following command sets **file1**’s date to a particular date and time:

```
# touch -t 202201010830 file1
```

The time format used here is ***yyyymmddhhmm***, or a four-digit year, two-digit month, two-digit day, two-digit hour, and two-digit minute.

Reference files are useful, particularly when you just want to have a file or set of files updated to a particular date/time rather than to the current date/time. You could use the following:

```
# touch -r reffile file2update
```

The date/time of **reffile** is applied to the **file2update** file date/time.

#### Copying Files and Directories

One aspect of copying an object is that the act creates a new file with a separate inode, which is literally a number assigned by the filesystem from a table and effectively is the system’s method of referring to the file; the friendly filename is really for the understanding of humans.

Note

An inode is a pointer to a file on a disk. An inode is created along with all the other files as a part of the filesystem and, depending on the filesystem, it can be either finite in number or auto-generated as needed. An inode essentially equates to the presence of a file on the system, for a file cannot exist without its own inode or a reference to one.

All of this means that the operating system sees the new file as being separate from the old one. Contrast this to a move operation, where it’s the same file (that is, the same inode, as long as it’s on the same filesystem) with a new name.

When you create an object in a filesystem, it gets its own permissions. **cp** doesn’t always copy the permissions over to the new file. This can be done, but it requires the use of the **-p** option to preserve the permissions and ownership. The root user is the only user that can change the [*ownership*](#ch02.xhtml_key04-a) of a file; therefore, regular users using this option always own the copied files, no matter who the original owner was.

A normal copy is simple to perform and essentially causes the file to be replicated to the new location:

```
# cp file1 /dir1/file2
```

A few options that make life easier for copying files include

• **-d:** Doesn’t follow symbolic links; copies a link instead. A link points one file to another (see the section *Linking Files*, later in this chapter).

• **-f:** Forces overwriting existing files.

• **-i:** Interactively asks before overwriting.

• **-l:** Creates a hard link to the source file.

• **-r or -R:** Recursively traverses directories (copying everything).

• **-s:** Creates a symlink to the source file.

• **-u:** Updates the copy only when the source is newer than the target or the target doesn’t exist.

• **-x:** Doesn’t traverse to filesystems mounted from other devices.

Copying an existing directory to a new one is simple:

```
# cp -r dir1 dir2
```

The **-r** option is necessary because the **cp** command doesn’t process directories by default. As long as the target directory does not exist, the previous command makes an identical copy of the source and all subordinate files and directories in the target directory.

Copying a source directory to an existing target directory doesn’t involve an overwrite; it involves making the source directory into a new subdirectory of the target. For example, if you are in the **/test** directory and have the following structure, you might assume that issuing **cp -r dir1 dir2** would overwrite **dir2**–or at least prompt you to do so:

```
# tree .
|-- dir1
| |-- file1
| `-- subdir1
`-- dir2
```

When you issue the **cp -r dir1 dir2** command, the filesystem (along with the **cp** command) notices the existing **dir2** entry and automatically drops the source directory into **dir2** as a subdirectory, like this:

```
|-- dir1

file1
| `-- subdir1
`-- dir2
 `-- dir1
 |-- file1
 `-- subdir1
```

The correct way to copy the contents of **dir1** into **dir2** and mirror **dir1** exactly is to focus on the word *contents*. By suffixing the source (**dir1**) with a forward slash and an asterisk (that is, **dir1/***), you tell the **cp** command to ignore the directory entry and focus on the filenames inside the directory.

With the same initial setup, if you issue the command **cp -r dir1/* dir2**, you get the correct results:

```
# tree .
|-- dir1
| |-- file1
| `-- subdir1
`-- dir2
 |-- file1
 `-- subdir1
```

The Linux+ exam will test your ability to properly copy a directory and its contents. In addition, if you see a source directory with only a trailing forward slash but no asterisk, such as **dir1/**, this is identical to using **dir1**. In other words, to copy just the contents of a directory, you have to address them specifically with the forward slash and asterisk (**dir1/***).

Two special characters used in relative directory naming are often used when copying files. The current directory is represented by a single period (.) and the parent directory by two periods (..). For example, if you are currently in the **/home/rossb** directory and want to copy a set of files from the **/home/lukec** directory, you can avoid typing the full path of the current directory by using the (.) character. Both of these commands perform the same action:

```
# cp /home/lukec/*.mp3 .
cp /home/lukec/*.mp3 /home/rossb
```

#### Moving Objects

Whereas the **cp** command copies a file by creating a new file, inode, and data, the **mv** command simply changes which directory file contains the file or directory entry or alters the entry in the file if it stays in the same directory. When you change just the metadata that points to the file, you can quickly move a file on the same device. If the file move happens across two devices, the file is copied to the new device and deleted from the old one.

Create a file named **file1** and then run the **stat** command on it to check the details, as shown in [Example 2-2](#ch02.xhtml_exe2_2).

**Example 2-2**–Running the **stat** Command on **file1**

!

```
# touch file1
# stat file1
 File: ‘file1’
 Size: 0 Blocks: 0 IO Block: 4096 regular empty file
Device: fd00h/64768d Inode: 2261179 Links: 1
Access: (0664/-rw-rw-r--) Uid: (500/sean) Gid: (500/sean)
Access: 2015-02-03 21:47:46.000000000 -0600
Modify: 2015-02-03 21:47:46.000000000 -0600
Change: 2015-02-03 21:47:46.000000000 -0600
 Birth: -
```

Now move the file to a new name with the **mv** command, as shown in [Example 2-3](#ch02.xhtml_exe2_3).

**Example 2-3**–Moving a File to a New Name

```
# mv file1 file2
# stat file2
 File: ‘file2’
 Size: 0 Blocks: 0 IO Block: 4096 regular empty file
Device: fd00h/64768d Inode: 2261179 Links: 1
Access: (0664/-rw-rw-r--) Uid: (500/sean) Gid: (500/sean)
Access: 2015-02-03 21:47:46.000000000 -0600
Modify: 2015-02-03 21:47:46.000000000 -0600
Change: 2015-02-03 21:48:41.000000000 -0600
 Birth: -
```

Because the device and inode stayed the same in [Example 2-3](#ch02.xhtml_exe2_3), you know this is the same file as before. The change time is modified to reflect the fact that the file was renamed.

When you move a file, the **mv** command overwrites the destination if it exists. This command supports an option, **-i**, that first checks the target to see whether it exists. If it does, **mv** asks whether you want to overwrite the target. Some distributions make **-i** a default option with a shell alias.

Another quirk of the command is the lack of an **-r**, or [*recursive*](#ch02.xhtml_key07-a), option. This is because when you move a directory or a file, you’re just changing the directory entry for the file. The directory continues to point to the same files, so there is no need to move the files themselves.

You can avoid the overwriting of newer target files or directories by using the **-u** option, which preserves the latest copy of an object.

Examples of moving files and directories include moving a single directory to another directory name, as shown here:

```
# mv -f dir1 dir2
```

This merely changes the directory entry **dir1** to the new name **dir2**. The **-f** option also omits the “are you sure?” prompt.

Just as with the **cp** command, moving directory contents requires a correctly formed command; otherwise, you’ll move a directory not to the new name but to a subdirectory of the existing directory. For example, consider the **/test** directory again, which has a structure similar to the following:

```
# tree .
|-- dir1
| |-- file1
| `-- subdir1
`-- dir2
```

If you were a Windows administrator, it would make sense to run the following command to move **dir1** to **dir2**:

```
# mv dir1 dir2
```

If you do this on a Linux system and then run the **tree** command, you see the following output:

```
# tree .
`-- dir2
 `-- dir1
 |-- file1
 `-- subdir1
```

This moves **dir1** under **dir2** because **dir2** already existed. To properly move the contents of the source **dir1** to the target **dir2**, you don’t need to use the nonexistent **-r** option. (Remember this for the Linux+ exam.) You can just use a forward slash and an asterisk to refer to the files underneath **dir1**, like this:

```
# mv dir1/* dir2
```

Note

The * wildcard operator doesn’t match hidden files because they begin with a period. Handling this case is actually quite complicated and beyond the scope of the Linux+ exam.

![Images](graphics/key_topic_icon.jpg)

If you run the **tree** command, you see the following output:

```
# tree .
|-- dir1
`-- dir2
 |-- file1
 `-- subdir1
```

Finally, the directories you pass to the **mv** command don’t always have to be underneath your current directory. You can use absolute pathnames, such as **mv /dir1 .** to move **dir1**, which is off the root directory, into the current directory. You can also run **mv /dir1 /tmp** from anywhere in the system to move that same directory into the temporary directory.

#### Creating and Removing Directories

A basic task in file management is to be able to create and remove directories, which sometimes means creating or removing whole trees at once. To create a directory named **dir1**, you use **mkdir dir1**. To create a directory named **subdir1** in the **dir1** directory, you use **mkdir dir1/subdir1**.

Always think of the last segment of any directory path as the object being created or removed and think of the rest of the items in a path as supporting or parent objects. The **mkdir** and **rmdir** commands are similar in features and options, including the capability of **mkdir** to create a deep subdirectory tree from scratch in a single command (using the **-p** or **parent** option to create any subdirectories needed to create that last subdirectory):

```
# mkdir -p /home/user1/dir1/dir2/dir3/dir4
```

One of the quirks about the **rmdir** command is that it can remove only empty directories. For example, the last directory of the chain **/dir1/dir2/dir3/dir4** is the real target for this command, and only if that directory is empty (containing no regular or directory files) can it be removed:

```
# rmdir -p /home/user1/dir1/dir2/dir3/dir4
```

By using the **-p** or **parent** option with **rmdir**, you can remove the tree starting with the last subdirectory all the way back to the top one–but only if the sole entry in any directory was the one just removed. One option to the **rmdir** command does allow it to remove directories that have files and so on in them. It’s called **--ignore-fail-on-non-empty** and is the longest option I know of in Linux. I’d rather type **rm -rf targetdir** 20 times than use this beast.

#### Removing Objects

You typically want to remove objects after creating or copying them, which is done with the **rm** command for most objects. **rmdir** can also be used.

Deleting files with the **rm** command is a matter of choosing the target to be removed and the options that work best.

If you want to remove a particular file and never be prompted by confirmation messages, the command is **rm -f target**.

To remove a directory and all its contents, without getting a confirmation message, the command is **rm -rf /full/path/to/target**.

### File Metadata and File Types

Since everything on a Linux system is really a file, (of one type or the other) it’s very important to know that files come in different types, what those are and how to identify what you are looking at, which we will do in this section.

![Images](graphics/key_topic_icon.jpg)

#### Determining File Types

With no absolute requirement for extensions on Linux files, a tool for easily determining file types is essential. The **file** command can be used to read a file’s headers and match that data against a known set of types.

#### The **file** Command

The **file** command uses several possible sources, including the **stat** system call, the magic number file (**/usr/share/magic**), and a table of character sets, including ASCII and EBCDIC. Finally, if the file is text and contains recognizable strings from a given programming or other language, it is used to identify the file.

The output can be used, manipulated, and filtered to show useful things. For example, simply using the **file** command on a given file shows the type:

```
$ file file1
file1: ASCII text
```

Running the **file** command against a known binary shows various elements about the architecture and layout of the file, as shown here:

```
$ file /bin/ls
/bin/ls: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically
linked (uses shared libs), for GNU/Linux 2.6.32, stripped
```

Running the **file** command against a directory full of files is useful for viewing the possible types, but the real gold lies in filtering the output using the pipe operator (|) and the **grep** command to see only the results that contain a particular word, such as **empty**:

```
$ file /etc/* | grep empty
/etc/dumpdates: empty
/etc/exports: empty
/etc/fstab.REVOKE: empty
/etc/motd: empty
/etc/printconf.local: empty
```

This is one way of finding empty files that are littering your system. They are probably required in the **/etc** directory but only clutter temporary directories such as **/tmp**.

#### Displaying File Metadata

If all you know how to do is use the **ls** command and it's various options, you are missing out on many important and significant pieces of information that will prove useful to you. Along with the **file** command, which uses the stat system call but not much else it provides, you can do wonders with the actual **stat** command.

![Images](graphics/key_topic_icon.jpg)

#### The **stat** Command

The **stat** command is most useful even by itself, it shows a multitude of different file information items, and as mentioned before it can work in conjunction with other commands to unveil even more.

stat is fairly simple to use, just invoke it with a file or file system object as it's argument and you'll see what it has to offer:

```
$ stat file1
  File: file1
  Size:0    Blocks:0   IO Block:4096   regular empty file
Device: 801h/2049d   Inode: 259418      Links: 1
Access: (0664/-rw-rw-r--) Uid:(1000/ ubuntu)Gid:(1000/  ubuntu)
Access: 2022-01-14 19:32:09.307094382 -0700
Modify: 2022-01-14 19:32:09.307094382 -0700
Change: 2022-01-14 19:32:09.307094382 -0700
 Birth: -
```

As you can see, you get so much more than a simple ls -l output, even the file type as if you had used the **file** command.

Information the **stat** command shows:

• **File:** This shows the file name as it exists on the filesystem

• **Size:** The file is an empty file, or one that has zero bytes of data in it

• **Blocks:** The file also takes up 0 blocks of space

• **IO Block:** The file does occupy or is associated with a 4096 byte block

• **File Type:** There is no label for this information, the file is a regular empty file, similar information as shown by the **file** command

• **Device:** This is the device it's block is located on

• **Inode:** The inode # associated with the file

• **Links:** This is a regular file, no hard links exist to the same inode

• **Access:** This is the permissions and user/group ownership for the file

• **Access:** This is the date/time of last file contents read

• **Modify:** This is the last date/time the file metadata (name, size, permissions was changed

• **Change:** This is the last date/time the actual file contents were changed

• **Birth:** This field is only used by certain filesystems such as Ext4, and is there to be a separate and static initial birth date/time for the file.

The **stat** command can also be used to display any number or order of the supported [*format sequences*](#ch02.xhtml_key09-a), such as %i, %A, and so on, which can be found in the man page for the **stat** command. These are shortcodes for what individual piece of stat output you want to display, and putting them into a particular order can be very helpful, or allow you to send that output to other commands for further processing!

As an example, you could issue the following command:

```
$ stat -c %i file1
  259461
```

The use of the -c followed by the %i will restrict stat output to just the Inode Number of the file. To output several format sequences all together, surround them with 'single quotes' like this:

```
$ stat -c '"%n",%i,"%F",%h' file1
"file1",259461,"regular file",1
```

The use of double quotes to surround possible filenames or descriptions that have spaces or commas in them, and separating the output with commas will make it very easy to generate something truly useful like a filesystem contents report that contains the fields you want to report on in the right order to use them in a spreadsheet etc.

Note

You should also be aware of the -printf format sequence option, which would allow you greater control by interpreting backslash escapes, such as trailing newlines with \n and more..

Hopefully having this knowledge about the multiple uses of the **stat** command will both be useful in your daily work as well as help you answer any questions about File Metadata you will find on the Linux+ exam!

### Soft and Hard Links

Links are very useful for several purposes, the main one is so that users don’t have to navigate all over the system just to access a file or run a command.

#### Linking Files

Links come in two varieties: symbolic (or soft) and hard links. Each has its own set of advantages and disadvantages. Sysadmins use links for a multitude of purposes; chief among them is the need to make shortcuts on a system for users to access data without having to navigate multiple directory levels.

If you have users on your Linux systems, you need to have a single mount point that is accessible to multiple users. The options include having users navigate to the **/mnt/somemount** directory to save data and putting a link to that mount point in each user’s home directory. You’re much better off using a link for this task.

##### Symbolic Links

A symbolic link is primarily used to make a shortcut from one object to another. A [*symbolic link*](#ch02.xhtml_key10-a) creates a tiny file with its own inode and a path to the linked file. Symlinks can span filesystems and drives, primarily because a symlink has its own inode. [Figure 2-1](#ch02.xhtml_ch02fig01) shows the relationship between a symlink and a target file.

![Images](graphics/key_topic_icon.jpg)![Images](graphics/02fig01.jpg)

**Figure 2-1**–Symbolic link detail

For example, you might mount an external disk on the **/mnt/projdata** mount point and want each user to be able to access that remote share from her own home directory. You simply have to issue the following command in each user’s home directory to accomplish this:

```
# ln -s /mnt/projdata projdata
# ls -l projdata
lrwxrwxrwx 1 root root 13 Jan 26 12:09 projdata -> /mnt/projdata
```

Notice that the listing for the new symlink shows exactly where the link points, and the permissions are set to the maximum to avoid interfering with the permissions on the target object.

Symbolic links always look like they have the same permissions, but they don’t try to change them. Changing permissions on a symlink changes the permissions on the target permissions instead.

To unlink a symbolic link, you simply delete the file that is the symbolic link, which removes the reference to the original file. As scary as it may appear to be removing that symbolic link file, by default doing so does not remove the target linked file.

##### Hard Links

A [*hard link*](#ch02.xhtml_key11-a) is normally used to make a file appear in another place. A hard link is simply an additional name in a directory that points to exactly the same inode and shares every aspect of the original file except the actual name (although the filename could be identical if it were in a different directory). [Figure 2-2](#ch02.xhtml_ch02fig02) shows the relationship between a hard link and the target file.

![Images](graphics/key_topic_icon.jpg)![Images](graphics/02fig02.jpg)

**Figure 2-2**–Hard link detail

For an example of using a hard link, consider the need to ensure that a frequently deleted file is easily restorable for a given user. The user, Jaime, travels a lot, but when he’s in the office, he seems to delete things a lot or claims that the system has eaten his files. When Jaime is flying, you don’t have any issues, so the problem must be the user’s actions.

To anchor or back up an important file, such as the company contact list, in Jaime’s home directory, you first must create a backup directory, such as **/backup**. Then you create a hard link from Jaime’s **ccontactlist.txt** file to a file in the **/backup** directory, like so:

```
# cd ~jaime
ln ccontactlist.txt /backup/home_jaime_ccontactlist.txt
ls -l ccontactlist.txt
-rw-r--r-- 2 jaime users 0 Jan 26 13:08 ccontactlist.txt
```

Notice that the file appears normal, but the number **2** for the link count lets you know that another name entry for this file exists somewhere.

Also notice that the listing for the new hard link doesn’t show the target file and doesn’t seem to refer to it in any way. Running the **stat** command on this file won’t show you the other filename or seem to be aware of it except for the higher link count.

The name and location of a file are the only things about the file that are not stored in the inode. You will see questions about this on the Linux+ exam.

Hard links can’t be created if the target is on another filesystem, disk, or remote object. The need to associate multiple names to the same inode makes such remote creation impossible.

Be careful when changing the permissions and ownership on hard-linked files because all name entries point to exactly the same inode. Thus, any changes are instantly made to what would appear to be multiple files but what, in reality, are only filenames.

Deleting a file that has multiple hard links requires the removal of every hard link or the multiple names. While it would appear that you are unlinking the files, since they are all exactly the same inode and data with different names in the filesystem directory files, you have to remove all the files that point to the original file to successfully perform an “unlink” from the original file.

In addition, to find all the links for a file, run the following command:

```
# ls -i ccontactlist.txt
17392 ccontactlist.txt
find / -inum 17392
/home/jaime/ccontactlist.txt
/backup/home_jaime_ccontactlist.txt
```

When you have found all the links to the file by querying the common inode number, you can delete all the undesired links to the original file, but you need to take great care not to remove *all* the links to the file; that is, do not delete the file entirely!

Note

For the Linux+ exam, remember that a symlink is another actual file with its own inode. A large number of symlinks can therefore cause a problem for a filesystem, such as one that contains users’ home directories. Using too many inodes can restrict you from using the storage space available. Run the **df -i** command to see what the statistics are.

### File Compression, Archiving, and Backup

[*Archiving*](#ch02.xhtml_key12-a) and restoring files have come a very long way since the days of Mountain tape drives and putting disk packs from mainframes into a case to be taken off-site by a delivery driver.

System operators who will be dealing with files and systems made up of files for most of their work life must know how to properly archive, list, unarchive, compress, and transform files.

Being able to competently design and implement a system backup and recovery scenario is one of the most critical tasks besides making sure the servers are serving files and providing services. Without a good backup and recovery scheme, a business that suffers a crippling systems crash may risk going out of business. I often say that most small businesses are one hard drive crash and a missed pay cycle from extinction.

It is important to take your organization or personal data security, safety, and integrity very seriously by backing it up, using proper storage, and making certain what you have backed up can be restored properly.

#### Using tar

The **tar** command is the workhorse of the archival world. The name, which comes from the term **t**ape **ar**chive, goes back to the time when most backup was done to a local tape drive. You can think of **tar** as a pipeline that takes in a series of files and outputs a single file that is meant to be streamed to tape, but this output could be sent to a file on disk as well.

As the data goes through the pipeline, you can do some transformations on the files, such as chop up the output into something that fits across multiple tapes, exclude files that weren’t recently changed, or rewrite the directory names stored in the archive.

**tar** also provides extraction options. You can run a **.tar** file, also called a [*tarball*](#ch02.xhtml_key20-a), through **tar** to get back a copy of the original files. It is possible to extract only certain files and manipulate the filenames.

The **tar** command can also be used with special option characters to make use of various [*compression*](#ch02.xhtml_key13-a) commands, particularly the **gzip**/**gunzip**, **bzip2**/**bunzip2**, and **xz/unxz** commands. This has the effect of creating a compressed archive file, typically named **.tar.gz** for **gzip**-compressed files, **.tar.bz2** for **bzip2**-compressed files, and **.tar.xz** for **xz**-compressed files.

**tar** commands have a slightly unusual syntax. The command is **tar**, followed by a dash (-), and then all the options concatenated together, such as **xvjf**. After this is a list of zero or more filenames; the meanings depend on the options you choose.

The **tar** command can act on files or **tar** archives in three main ways; each has a corresponding letter that must be the first letter in the list of options:

• **c:** Creates an archive.

• **t:** Tells you the contents of an archive.

• **x:** Extracts files from an archive.

• A number of other optional options are available, including the following:

• **v:** Be verbose by giving a list of files as they are processed.

• **j or z:** Compress or decompress with **bzip2** or **gzip**, respectively.

• **f:** The next word is the name of the file to operate on.

[Figure 2-3](#ch02.xhtml_ch02fig03) shows the choices graphically. Next, we’ll look at examples of these options.

![Images](graphics/key_topic_icon.jpg)![Images](graphics/02fig03.jpg)

**Figure 2-3**–Picturing the **tar** options

When you’re creating an archive with **tar**, you should think about what you want to archive, where you want the resulting archive to be created, and what compression, if any, you want to use.

To create a simple **tar** archive, the options you need are as follows:

```
tar -cf archive.tar /foo
```

In this example, the **-c** option signals **tar** to create the file specified after the **-f** option and specifies the directory you are archiving, which is the **/foo** directory. Note that you have to add the **.tar** suffix. By default, the operation is recursive, so if you specify a directory as the target, it archives that directory and all its subdirectories and files in that tree.

To create a **tar** archive and see the filenames as they are processed, use the **-v** option:

```
tar -cvf archive.tar /foo
```

This produces the following output:

```
tar: Removing leading ‘/’ from member names
foo/
foo/install.log
foo/install.log.syslog
foo/.bash_logout
```

If given an absolute directory name to archive, **tar** strips the leading **/** from the full path of the objects in the archive. It would not be good if you could overwrite files in your **/usr** directory by extracting a file in an unrelated directory!

You can pass more than one directory or file to **tar**. For example, **tar -cf foo.tar bin var** creates an archive called **foo.tar** that contains both the **bin** and the **var** directories.

Note

The **tar** command does not compress the files it places into an archive file. Even though the entirety of the files on disk and the file size might be slightly different, there’s no real compression happening.

#### Using Compression Utilities

Due to the toolset mentality of Linux and Unix commands, where everything does one thing really well and works well with other commands, you can use compression utilities with the **tar** command to get much smaller archive file sizes.

The Linux+ exam objectives mention three compression commands: **gzip**, **bzip2**, and **xz**. These three commands are accompanied by corresponding decompression utilities: **gunzip**, **bunzip2**, and **unxz**.

All three of these utility pairs share a similar command line syntax, and they are perfect companions to the **tar** command, which doesn’t really compress files and directories, but it puts them into an archive file and leaves the compression up to the commands we are discussing now.

By default, the **gzip/gunzip**, **bzip2/bunzip2**, and **xz/unxz** commands act on individual files, which is almost exactly the opposite of the **tar** command’s behavior.

For example, if you have three files, **file1**, **file2**, and **file3**, in the current directory, you could use the **tar** command on them to produce a **tar** archive file that contains all three of these files. Conversely, using any of the three compression utilities against these files will result in each of the individual files being compressed and *replaced* by a file that has the same name but ends now in either **.gz**, **.bz2**, or **.xz**.

To create the same archive with **gzip** compression, you simply insert a **-z** option and use the letters **.gz** as the filename suffix:

```
# tar -czf archive.tar.gz /foo
```

The result will be a **gzip**-compressed file named **archive.tar.gz** in the current directory.

To create the same archive with **bzip2** compression, you simply insert a **-j** option and use the letters **.bz2** as the filename suffix:

```
# tar -cjf archive.tar.bz2 /foo
```

The result will be a **bzip2-compressed** file named **archive.tar.bz2** in the current directory.

![Images](graphics/key_topic_icon.jpg)

To create the same archive with **xz** compression, you simply insert a **-J** option and use the letters **.gz** as the filename suffix:

```
# tar -cJf archive.tar.xz /foo
```

The result will be a **gzip**-compressed file named **archive.tar.xz** in the current directory.

The following is an example of listing all three of these archive files:

```
tar -tzf archive.tar.gz
tar -tjf archive.tar.bz2
tar -tJf archive.tar.xz
```

Keep in mind that the appropriate archive option character *must* be paired up with the corresponding compressed archive file, or it will fail.

The output of the listing is affected by the use of the **v** option:

```
-rw-r--r--rossb/rossb 34 2019-03-22 08:34 compressfiles/ld.so.conf
-rw-r--r--rossb/rossb 552 2019-03-22 08:34 compressfiles/pam.conf
-rw-r--r-- rossb/rossb 14867 2019-03-22 08:34 compressfiles/ltrace.conf
```

Without the **v** option, you would simply see a listing of the filenames, not the longer listing just shown:

```
compressfiles/ldso.conf
compressfiles/pam.conf
compressfiles/ltrace.conf
```

##### Using tar with Compression Utilities

You will likely see questions on the Linux+ exam that test your knowledge of which compression command has the highest compression. In our testing, the order of highest compression to lowest compression effectiveness is:

• Highest = **xz**

• Medium = **bzip2**

• Lowest = **gzip**

Another command, **zip**, is an interesting utility, in that it was developed on Unix but was most used on the PC platform. The **zip** command is accompanied by the **unzip** command, similar to the other compression command pairings. While this is a fine utility set, it’s not as commonly used as the three sets previously mentioned.

You are most likely to use **zip** and **unzip** on Linux when you are sent an archive file from someone that is in that format, and you need to unarchive the file’s contents.

**zip** and **unzip** work slightly differently than the other three commands mentioned previously, in that **zip** doesn’t automatically replace a file with a compressed version of itself, like the other three do; it works more like a combination of **tar** and a compression utility.

Note

If you grew up using **pkzip** and **pkunzip** or **winzip**, you’ll immediately recognize how **zip** and **unzip** work. For you, the **tar** and **gzip**/**bzip2**/**xz** utilities may seem strange.

Let’s look at how to create a compressed archive with **zip**. To zip up a set of files in a directory, such as the current one, you use this command:

```
# zip somefile.zip file1 file2 file3
```

Or you could zip up all the files in the directory with this command:

```
# zip somefile.zip *
```

This command zips up everything in the current directory, including subdirectories, but very importantly, it does not include the files in those subdirectories unless you specify the **-r** (recursive) option.

Say that you have the following directory and file tree:

```
 file1
 file2
 subdir1
  file3
  file4
1 directory, 4 files
```

Running **zip** does not, as you might think it would, get the contents of the **subdir1** directory. Instead, it produces a zip file that has **file1**, **file2**, and **subdir1** in it:

```
# zip somefilenor.zip *
 adding: file1 (stored 0%)
 adding: file2 (stored 0%)
 adding: subdir1/ (stored 0%)
```

To properly zip up the current directory and all its subdirectories and their files, you would run

```
$ zip -r somefilewithr.zip *
 adding: file1 (stored 0%)
 adding: file2 (stored 0%)
 adding: somefilenor.zip (stored 0%)
 adding: subdir1/ (stored 0%)
 adding: subdir1/file3 (stored 0%)
 adding: subdir1/file4 (stored 0%)
```

Before you unzip a zip archive, it’s considered elegant and reasonable to list the archive contents, since you probably don’t want 3,000 loose files in the current directory. Listing the contents of a zip archive is easy:

```
# unzip -l somefile.zip
Archive:  somefilewithr.zip
Length    Date         Time     Name
---------     ----------      -----       ----
 20       2019-07-11   12:16     file1
 26       2019-07-11   12:18     file2
488       2019-07-18   11:41     somefilen.zip
  0       2019-07-18   11:37     subdir1/
 20       2019-07-18   11:34     subdir1/file3
 26       2019-07-18   11:34     subdir1/file4
---------                           -------
580                              6 files
```

Notice that the files are listed according to whether they are at the root of the archive file or in a subdirectory, which is the case with **file3** and **file4**. The **-l** option does not unarchive the zip file; it simply iterates through the contents of the file.

Performing an unzip on a zipped file is pretty simple:

```
# unzip somefile.zip
Archive: somefilewithr.zip
replace file1? [y]es, [n]o, [A]ll, [N]one, [r]ename:
```

This message is asking if you want to overwrite an existing set of files that match some or all of the contents of the zip archive. If you were to answer with the A character for “overwrite all,” this would be the result:

```
 extracting: file1
 extracting: file2
 extracting: somefilenor.zip
 extracting: subdir1/file3
 extracting: subdir1/file4
```

There are a number of other options available for the **zip**/**unzip** command pair, but you already know all you need to know for the Linux+ exam.

##### Taking Pity on the Unarchiver

It’s considered proper and elegant to create **tar** archives by specifying a directory that contains the files to be archived, not just a bunch of files that are in the current directory. This means that when the files are untarred, they show up in a single directory instead of in the current directory.

For example, create an archive of the **/etc** directory contents with the following command:

```
# tar -cf etc.tar /etc
```

When you unarchive the **tar** file, by default it creates an **etc** directory in the current directory, which contains the entirety of the **/etc** directory you archived.

Contrast this with the nightmare that happens when you navigate to the **/etc** directory and create the archive from there with this command:

```
# tar -cf /root/badetc.tar *
```

This archive file contains the same files as the previous one, but they aren’t contained in a top-level **etc** directory; rather, everything is in the top level of the archive. Imagine what will happen to your system when you unarchive this file in the root user’s home directory. You will spew approximately 2,400 files directly into the root user’s home directory!

It really does matter where you are in the filesystem and which path options you use when you create or expand an archive file. It’s best practice to use absolute pathnames.

To solve the problem of 2,400 files polluting your root user’s home directory, use the following command, where **badetc.tar** is the offending archive file:

```
# tar -tf badetc.tar | xargs rm -rf
```

This command produces a list of the paths and filenames of files in the archive and uses the **xargs** command to feed each line of output as a filename specification to the **rm -rf** command, removing all the files and directories expanded from the **badetc.tar** file.

##### Useful Creation Options

A number of options can be used for creating **tar** archives. Here is a list of the ones that are most useful and most likely to appear on the Linux+ exam:

• **-b:** Sets the block size to fit the media to which you are archiving. This is necessary for some tape devices.

• **-M:** Specifies multiple archive targets or spreads a large archive across multiple tapes or media.

• **-g:** Creates a new format incremental backup (only files that have changed since the last full or incremental backup).

• **-l:** Stays on the local filesystem; it’s used to prevent backing up the entire NFS network by accident.

• **-L:** Sets the tape length so multiple tapes can be used for an archive. It is followed by a number that indicates the number of kilobytes, so, for example, **-L 500** equals 500KB.

• **--remove-files:** Removes the specified files from the filesystem after they have been added to the archive. This option is dangerous!

#### Listing Archive Files

Listing is underrated. It’s something you’re likely to do after you don’t get the results you want or realize what you’ve just done and want to confirm how hard it is going to be to clean up.

You can learn the contents of a **tar** archive by using the following command:

```
# tar -tf archive.tar
```

This produces the following output:

```
etc/
etc/sysconfig/
etc/sysconfig/network-scripts/
etc/sysconfig/network-scripts/ifup-aliases
etc/sysconfig/network-scripts/ifcfg-lo
```

To list an archive that uses compression, simply insert the necessary letter between the **-t** and the **-f** options, such as the **bzip2** -**j** option shown here:

```
# tar -tjf archive.tar.bz2
```

This produces the following output:

```
etc/
etc/sysconfig/
etc/sysconfig/network-scripts/
etc/sysconfig/network-scripts/ifup-aliases
etc/sysconfig/network-scripts/ifcfg-lo
```

To list an archive and see the file details for its contents, you add the **-v** option to the existing command to see output listing the details:

```
# tar -tvjf archive.tar.bz2
```

This returns output similar to the following:

```
drwxr-xr-x root/root 0 2015-02-10 03:46 etc/
drwxr-xr-x root/root 0 2015-01-31 10:09 etc/sysconfig/
drwxr-xr-x root/root 0 2014-11-10 22:13 etc/sysconfig/network-scripts/
```

When you create an archive with the **-v** option, a list of the files being archived is shown onscreen. When you unarchive an archive with the **-v** option, you see a similar list of the files being unarchived. It’s only when you list an archive with the **-v** option that you get the type of output that approximates an **ls -l** command being run on the archive contents. This is a Linux+ exam topic, so be ready for it.

![Images](graphics/key_topic_icon.jpg)

#### Using cpio

The **cpio** command doesn’t appear much in the Linux+ exam objectives. The exam might ask you about the **cpio** command at only the simplest levels. For example, you need to know that the command exists, how it works in general terms, and whether it can be used to back up a Linux system.

All the **cpio** command actions treat the filesystem as the home base. If you are copying out, it’s from the filesystem out to another file. The same is true with copying in: You copy in from a file into the filesystem.

The **cpio** command has three options for acting on files and filesystems:

• **-o or --create:** This copies files to an archive, using a list of files typically created by the **find** command.

• **-i or --extract:** This copies files into the filesystem from an archive or a list of the archive contents.

• **-p or --pass-through:** This copies files from one directory tree to another without the use of an archive, essentially performing the same function as the **cp -r** command.

The **cpio** command accepts a list of files in a one-file-per-line format and uses this list to send the archived files to either the standard output or an archive file you specify.

**cpio** supports a variety of archive formats, including binary, ASCII, crc, and **tar**.

The following example creates a **cpio** archive from the files in the current directory:

```
# find . “*” | cpio -o > archive.cpio
```

This command outputs the list of files found by this particular **find** command, and the **cpio** command sends all the files to the **archive.cpio** file by redirecting standard output to the file.

The **cpio** command doesn’t accept a list of files to archive on the command line, as do the other utilities you’ve seen so far. Instead, it reads the names of the files from the standard input or console. So be aware that you need to use either the **find** command or the **ls** command to feed **cpio** a list of filenames.

For example, if you needed to archive all the files that have the extension **.txt** in the current directory to a **cpio** archive named **txt.cpio**, you use the following command:

```
# ls *.txt | cpio -o > txt.cpio
```

Notice that this command redirects the output of **cpio** to a file rather than letting it write the file itself. Therefore, the filename is up to you, and if you want a **.cpio** file extension, you need to add it yourself.

#### Using the dd Command

The **dd** command is useful for a variety of tasks, not the least of which is creating backup images, called ISO files, of CD or DVDs. The two main formats **dd** interacts with are the raw device file and the full path of a file or an object on the system.

For example, when creating a new boot disk, the **.img** binary file is read block by block from the CD-ROM (as a file) and written to a USB disk raw device as a set of blocks:

```
# dd if=/mnt/cdrom/images/boot.img of=/dev/sdb
```

Creating an image of a CD-ROM involves reading the raw USB device block by block and creating a file on the filesystem that contains all those blocks:

```
# dd if=/dev/sdb of=/root/usb.img
```

To duplicate a USB device named sdb to another USB device named sdc, the command is

```
# dd if=/dev/sdc of=/dev/sdc
```

The **if** keyword means to input file, and the **of** keyword means to output file. The exact order is unimportant, but as you can imagine, mixing up the in and out files can cause terrible problems such as overwriting parts of your hard drive!

**dd**, unlike most other Unix utilities, does not use dashes for its options. Options are specified in the format *option*=*value*.

The **dd** command is also often used to duplicate a drive or a partition of a drive to another object.

For example, to copy the first partition from the **/dev/sda** disk to the same location on the second hard drive on the system, you use the following command:

```
# dd if=/dev/sda1 of=/dev/sdb1
```

You can also copy an entire disk device to another device on the system by leaving off the partition numbers:

```
# dd if=/dev/sda of=/dev/sdb
```

This works only if the second device is as large as or larger than the first; otherwise, you get truncated and worthless partitions on the second one.

Backing up the MBR is another trick that **dd** does well. Remember that the master boot record contains the indexes of all the partitions on that drive, and thus it is very important. To create a disk file that contains only the first 512 bytes of the first hard drive in the system, use this command:

```
# dd if=/dev/sda of=/root/MBR.img count=1 bs=512
```

The **count** keyword sets the number of reads from the input file you want to retrieve, and the **bs** keyword sets the block size.

If you don’t set the count and block size on this command to back up the MBR, you’ll be copying the entire device’s blocks to the filesystem–a snake-eating-its-own-tail operation that is guaranteed to fill up the partition quickly and crash the system.

The restoration procedure is just the opposite:

```
# dd if=/root/MBR.img of=/dev/sda count=1 bs=512
```

#### Compression Tools

Whereas the **tar** command is used to gather files and put them in a container, the **gzip**, **bzip2**, and **xz** commands are used to compress that container. Used by themselves, they act on each file they find and replace that file with a compressed version that has an extension indicating that the file is compressed.

The **gzip** and **bzip2** compression utilities compress files and are similar in their functions and operations. The main difference is that **bzip2** offers slightly better compression than **gzip**, but **gzip** is much more widely used. The **xz** utility offers better compression than either of the other two and is enjoying a growing user base.

These commands replace the original file with a new file that has an additional extension, so don’t delete the **.gz** or **.bz2** files that you create. They are the original files in a compressed wrapper!

To compress all the files in the current directory with **gzip**, use this command:

```
# gzip *
```

This replaces all the regular files (not the directories or their contents) in the current directory with the original filenames plus a **.gz** extension. So, if you had two files named file1 and file2 in the directory, they would be replaced with

```
file1.gz
file2.gz
```

To uncompress these files, just do the opposite of the compression:

```
# gunzip *
```

This restores the original files.

Using **bzip2** produces the same sort of results. You can issue the following command in the same directory:

```
# bzip2 *
```

You would then have the following two files:

```
file1.bz2
file2.bz2
```

To uncompress these files, issue this command:

```
# bunzip2 *
```

This restores the files to their original states.

**xz** is a newer option for compressing files than **bzip2** and **gzip**. In some cases it has better performance than **bzip2**, but at a cost of more memory. Files are compressed with **xz**, **xz -z**, or **xz --compress** and decompressed with **unxz**, **xz -d**, **xz --uncompress**, or **xz --decompress**.

The **.xz** file extension indicates that a file was compressed with **xz**. To uncompress **foo.xz**, for example, you would run **xz -d foo.xz** and would be left with an uncompressed file called **foo**.

Watch for Linux+ exam questions that ask about why you would use either **gzip**, **bzip2**, or **xz** for a particular compression task.

#### Backing Up Is Hard to Do

If there’s anything that is more important than a good backup, it’s a successful restore! Backups are useless without the ability to restore the data properly and in a timely manner.

Note

For the sake of simplicity, this section discusses backups in a manner that is detached from the actual media (disk, tape, DVDs, and so on).

There are many considerations for backup scenarios. The following sections lay out the different methods and discuss why you would use them–either singularly or with each other.

![Images](graphics/key_topic_icon.jpg)

#### Backup Types

There are three basic types of backups:

• **Full backup:** This is the most basic method of backup, in which the operator initiates a full copy of the dataset to a backup location. An advantage is that a single-step restore is possible because all the data is there. Disadvantages are long backup times and an ever-growing amount of storage needed for the backups.

• [*Incremental*](#ch02.xhtml_key14-a) **backup:** This type of backup is a real time-saver, as it backs up *only* new data since the last backup operation, whatever type it was. Advantages are a quick backup time, compared to a full backup, and the most efficient use of space, since it only includes data since the last operation. Disadvantages include an increasing number of valid backups to do a successful restore, and if one fails, you lose all that data from the restore.

• [*Differential*](#ch02.xhtml_key15-a) **backup:** This method strikes a balance between a full backup and an incremental backup in that it includes all data from the last full backup. The advantage is that you need only two backups to do a restore at any point: the last full backup and the last differential backup (which includes all data changed since the last full backup). The disadvantage is that the backups take an increasing amount of space because the time between the current date and the last full backup increases.

#### Other Backup Types

There are a couple other types of backups to mention: snapshot clones and images.

The Linux+ exam objectives actually say “snapshot clones,” but VMware and other vendors use the terms *snapshots* and *clones* separately.

A snapshot is used primarily with a virtual machine (VM), where the initial state of the VM is the baseline. A snapshot is essentially an incremental backup of what’s changed with the VM since the last snapshot.

For example, if you have a VM that you set up for software testing or experimentation and you don’t want to go through the whole setup routine again, you can snapshot it, or create a backup of the current state of the VM, and then you will be able to restore to that point at any time in the future.

Another great use of a snapshot, or series of snapshots, is when you are testing lab steps and want to be able to quickly take the machine back to or up to any level of changes.

A clone, on the other hand, is essentially a full backup of a VM. It can be used to test new software, OS updates, and so on–on what is effectively the production VM.

A clone is heavy because it is really another VM like the original, except for the name, IP address, and other identifying information.

Benefits of snapshots are that you can start off with a clean setup, do a snapshot, do almost anything to the VM, revert back to the clean setup with a couple of mouse clicks or commands, and start the process again.

An image is effectively a clone that occupies a single file, and the software that manages the image backup can do a number of things with it, including restore to dissimilar hardware, pull individual files and sets of files out of the image and restore to another device, and a lot more.

Another use of image backups is to build a VM, with all the software and services it needs to immediately perform a given service or function and then deploy it across a network, in virtualization environments such as Docker, Kubernetes, and so on.

### Copying Objects Between Systems

While you use the **cp** command when copying files to different locations on the same filesystem or between filesystems on the same machine, copying files between computers is accomplished with the **scp** command.

#### Using the scp Command

The **scp** command, which is part of the SSH suite of protocols and utilities, authenticates between the source and target systems in the same way as **ssh**, using the public/private key mechanisms.

Copying a file from **systema** to **systemb** using **scp** has a couple more components to the command line than a standard **cp** command from one directory to another on the same machine. To copy the file **foobar.txt** from **systema** to **systemb**, for example, you need to specify what user you want to be on the remote system; otherwise, it will use the default username on the source system.

For example, in the following command, say that you are root on **systema** but want to copy **foobar.txt** to the **ross** home directory on **systemb**:

```
# scp foobar.txt ross@systemb:~
ross@systema’s password:
foobar.txt 100% |**********************| 1379 00:00
```

Following password entry and any other prompts, the file is copied to the remote system and placed in the **/home/ross** directory.

Another fun feature of the **scp** command is the ability to copy from another system to yours, just by reversing the order of the command. For example, this is how you copy the file **tarfoo.txt** to the **ross** home directory on **systema** from **systemb**’s root user home directory:

```
# scp root@systemb:~/tarfoo.txt ross@systema:~
root@systema’s password:
tarfoot.txt 100% |**********************| 1379 00:00
```

The **scp** command also has a useful ability to copy from **systemb** to **systemc** from the user’s vantage point on **systema**. Linux simply uses the tunneling aspect of the SSH protocol and creates a tunnel for the command to work from **systemb** to **systemc**; it’s just as if you were on **systemb** copying the file to **systemc**, only you are really on **systema**:

```
# scp root@systemb:~/blahwoof.txt ross@systemc:~
root@systemc’s password:
blahwoof.txt 100% |**********************| 1379 00:00
```

Note

The **scp** command is very versatile, and while we have introduced you to its main tricks and capabilities in this section, there is much more to explore and learn by reading the man pages for **scp** and **ssh**.

![Images](graphics/key_topic_icon.jpg)

#### Everything and the Kitchen rsync

While we are on the topic of copying objects around systems and even between systems, it’s important to include a discussion of the **rsync** command.

The **rsync** command is an extremely powerful command that we can’t begin to cover fully, but let’s look at it and see what it’s most known for and probably most used for.

**rsync** is similar to the **copy** command in that you can use **rsync** to copy a file from one place to another, one file to another, and even one directory tree to another–all functions that the **copy** command can do.

So what exactly are the real reasons to use the **rsync** command? It is useful for its speed of operation, efficiency in just copying what’s changed, and its ability to be used inside SSH for better security.

A main aspect of the **rsync** command that makes it so useful is that **rsync** can make a copy of a set of files and directories, and it can also be used to copy just the changes between files, directories, and trees of files and directories. This makes it much faster and more efficient than a traditional **copy** command, as it can just copy over and update the changes to files and directories.

To make a mirror of a directory and all its descendants, use the following command:

```
# rsync -ar ./somedir /data/someotherdir
datafile1
datafile2
datafile3
<output truncated>
```

This makes an exact mirror copy of every file and directory from the source (**somedir**) to the target (**/data/someotherdir**), including all contents, ownership, file permissions, and timestamps for the files, as mentioned.

A major feature of **rsync** is its capability to perform copying and mirroring functions across systems. It can be used in a similar fashion to the **scp** command:

```
# rsync -avzh /home/ross/datafiles ross@192.168.10.20:~
datafile1
datafile2
datafile3
<output truncated>
```

This command opens a connection to the remote system and transfers the directory **/home/ross/datafiles** to the remote machine and makes or updates the **/home/ross/datafiles** directory on that system.

Another key feature of **rsync** is the capability to conduct all of its otherwise normal operations over the SSH protocol, such as this copy of a directory tree from the local system to a remote system:

```
# rsync -avzh datafiles -e ‘ssh -p 22’ ross@192.168.10.20:~
datafile1
datafile2
datafile3
<output truncated>
```

Not all your operations with **rsync** will be quick. Some will likely contain many megabytes or, more likely, multiple gigabytes of data. A very useful option for determining the operation’s progress is the **--progress** option, and you can add the **--delete** option as well so that you can be certain that the target directory will be a mirror of the source:

```
# rsync -avzh test --progress --delete ross@10.0.0.41:~
Password:
deleting test/etc2/xrdb/Xaw.ad
deleting test/etc2/xrdb/Tk.ad
deleting test/etc2/xrdb/Motif.ad
deleting test/etc2/xrdb/General.ad
deleting test/etc2/xrdb/Emacs.ad
deleting test/etc2/xrdb/Editres.ad
deleting test/etc2/xrdb/
deleting test/etc/mailcap.order
deleting test/etc/magic.mime

sent 97.42K bytes  received 124.60K bytes  63.43K bytes/sec
total size is 6.57M  speedup is 29.60
```

As you can see, this command has done what you wanted: removed various files and directories that don’t exist on the source and given some statistics about the transfer to the remote system, including the amount of data sent and received in the transfer and the total data size transferred.

In short, **rsync** is a very useful command and a key part of any awesome sysadmin’s kit of tools. It’s a lot like a merging of the **copy** command and **scp**, with a few other great options.

### File Editing

Lets begin with the most common editor, Vim.

One of the most confusing things about **vim** is the presence of modes, or states, in the editor. It has three modes:

• Command

• Insert

• LastLine, also called “ex” mode

Each of these modes is used for different purposes. The [*Command mode*](#ch02.xhtml_key16-a) is used for moving the cursor around and doing operations on text. [*Insert mode*](#ch02.xhtml_key17-a) is for adding text to your document. [*LastLine mode*](#ch02.xhtml_key18-a) is used to invoke more complicated modes, such as search and replace, or to manipulate split window panes.

#### The Message Line

The bottom of the **vim** screen contains a number of pieces of information that can help you, varying to suit the situation and actions just completed. This section details some of the messages that can appear.

If you’ve just entered **vim file1**, when the editor opens the file, the message line should contain something similar to the following:

```
“/home/rbrunson/file1” 57L, 1756C 18,1 Top
```

The numbers 18,1 on the right side of the message line are the current line and column numbers, and the Top text is the current position of the cursor. This changes to Bot if you entered the last half of the file. The other value possible is All, which simply means that all the contents of the file are currently on the screen.

A new file (one invoked with **vim file1**) would show the line

```
“file1” [New File] 0,0 All
```

If you are in Insert mode, the message line shows

```
-- INSERT -
```

#### Editing in Vim

**vim** always starts in Command mode, unless you specify differently. True editing (where you type a character, and that character appears on the screen) takes place in Insert mode.

![Images](graphics/key_topic_icon.jpg)

The keys you commonly use to invoke Insert mode from Command mode are:

• **i:** The most common method of moving into Insert mode is to press the **i** key, which leaves the cursor at the current position. All typing from that point pushes existing text to the right. Think of this as “insert here.”

• **I:** The uppercase **I** key moves to the beginning of the current line and from there acts like the **i** key. Think of this as “Insert at the beginning of the line.”

• **a:** The second-most-common method is to press the **a** key, which moves the cursor one character to the right and essentially behaves like an **i** key after that. Think of this as “append after current position.”

• **A:** The uppercase **A** moves to the end of the current line and from there acts like an **a** key. Think of this as “Append to the end of the line.”

• **o:** Use this key to open a new line under the present line. For example, if you’re on line 3 in Command mode, pressing **o** drops line 4 down to become 5 and opens a new line 4 that’s empty. Think of it as “Open a new line below.”

• **O:** The uppercase **O** opens a new line at the current line. For example, if you’re on line 3, pressing **O** drops line 3 down to become line 4 and opens a new empty line 3 for editing. Think of it as “Open a new line above.”

Getting back to Command mode is easy: Press the **Esc** key at least once; many people double-press it just to make sure they’re really there. At any time, you can return to Command mode from Insert mode by pressing the **Esc** key.

##### Opening a File for Editing

To create a new file in the current subdirectory, you type **vi *filename***.

To create a new file in a particular directory, use the full path: **vi */full/path/to/file***.

Sometimes you will want **vim** to open a file with a search string and put the cursor on the first found instance of that string. To accomplish this, enter **vi +/string filename**.

Other times, you’ll want to edit a file and have the cursor jump to a particular line when the file is opened, such as the **initdefault** line in **/etc/inittab**. In this case, you would enter **vi +18 /etc/inittab**.

Note

Expect Linux+ exam questions about opening files with particular options, searching a file upon opening it, and starting the **vim** editor in other ways. The **+** command line option tells **vim** to run that particular command once the file is open.

##### Navigating Within a File

The **vim** editor allows you to use the following keystrokes to move left, right, up, and down, but if you have cursor keys, you can use them, too:

• **h:** This functions as the **Left Arrow** key; it’s easy to remember because it’s the leftmost key in the four-key set.

• **j:** Use this for the **Down Arrow** key.

• **k:** Use this for the **Up Arrow** key.

• **l:** Use this for the **Right Arrow** key.

[Figure 2-4](#ch02.xhtml_ch02fig04) illustrates how these keys work.

![Images](graphics/key_topic_icon.jpg)![Images](graphics/02fig04.jpg)

**Figure 2-4**–Cursor key directions

As you can see in [Figure 2-4](#ch02.xhtml_ch02fig04), one of the ways to remember the keyboard cursor keys is to just look down at the home row and remember that **h** is the leftmost, **j** goes jown (down), **k** goes kup (up), and **l** is on the right. Makes perfect sense, right?

**Tip**

You’ll see questions on the Linux+ exam about the movement keys. The arrow keys are a favorite topic, whereas the **Ctrl** keys don’t get much love. Know those arrow (**h, j, k, l**) movement keys!

You can also move around in **vim** by using **Ctrl** key combinations:

• **Ctrl+F:** Moves forward a page.

• **Ctrl+B:** Moves backward a page.

• **Ctrl+D:** Moves forward a half-page.

• **Ctrl+U:** Moves backward a half-page.

• **G:** Moves to a particular line, such as 12G to go to line 12\. Without a number, G takes you to the end of the file.

##### Force Multipliers

You can have just about any keystroke or action repeat a given number of times by prefixing it with a number. For example, from Command mode, to move down 5 lines, you would type 5j. Moving 12 words to the right is accomplished with 12W.

A lot of editing, inserting, and escaping back can sometimes leave the message line without some pertinent information showing, such as the name of the file being edited. When you get confused about where you are or under which filename you saved a particular iteration of a file, you can press **Ctrl+G** while in Command mode to see the filename, total number of lines, and current position expressed as a percentage of the total lines in the file.

##### Undo Operations

The undo operations are a useful and largely unknown set of options. You press **u** in Command mode to undo a single operation or the latest in a series of changes. If you opened a file, made 30 changes, and then pressed the **u** key 30 times, you would end up with exactly the same file you originally opened.

Don’t bother trying to use **U** to undo all changes; that’s not what it’s for. U undoes all the changes on a single line. Instead, use the **:e!** keystroke combination to undo all changes since the last disk write to the file. The **:** takes you to LastLine mode, and the **e!** command reloads the current file, discarding all unsaved changes.

##### Saving Files

The most straightforward way to save a file in **vim** is to enter **:w** in Command mode. This saves the file and allows you to continue to edit it. To remember the **w**, think of “write.”

![Images](graphics/key_topic_icon.jpg)

##### Quitting vim

When you’ve made changes to a document, **vim** doesn’t let you quit normally, such as with **:q**. One of the most frustrating situations every **vim** user faces is the dreaded “E37: no write since last change (add ! to override)” message. This error can be fixed only by using the correct additional **!** character. To exit a file that is read-only or that you don’t want to save the changes to, you must use the keystrokes **:q!**. This is known as *qbang*, or “quit dammit.”

Note

If I had a dollar for each time a student got stuck in **vim** and had to use the **:q!** option to get out of the session, I would be very rich.

Saving and quitting a given file is simple, too. In Command mode you enter **:wq**. Think of “write, quit” to remember this command. If you are editing a file, such as a configuration file, as the root user, this file might lack the write permission, which means the **:wq** command would fail. Entering **:wq!** forces the file to be written, as long as the only barrier is a missing write permission.

Two additional methods of saving and quitting a file are available. The first is to enter **:x** to save and exit. The second is to press **ZZ** (hold down the **Shift** key and press the **Z** key twice); this is my personal favorite and is easy to remember. Because **:x** starts with a colon, the **x** is a LastLine command (as is **wq**). ZZ is a Command mode command. The **x** LastLine command has the added benefit of not saving a file that’s already been saved, which makes exiting much faster on large files.

**Tip**

Read Linux+ exam questions carefully, especially when they ask about saving and/or exiting the **vim** editor. Many test takers have mentioned that the question’s syntax is critical to getting it right. For example, the question “Which of the following saves and exits a file in **vi**?” is very different from the question “Which of the following can be used to save or exit a file in **vi**?”

##### Changing or Replacing Text

A number of options are incredibly useful when you’re altering an existing file and need to change a character, a line, a sentence, or just a word. For example, the **c** command changes text, and you can add additional modifiers after the command to indicate to vim how much text to change. Use the following options to change or replace text:

• **cw:** Changes a single word from the current cursor position. To change a whole word, you put the cursor on the first character of the word.

• **c$:** Changes from the current cursor position to the end of the line, even if that line is wrapped to appear as another line on the screen.

• **r:** Replaces the character under the cursor.

• **R:** Replaces text on the same line as you type until Esc is pressed, but it doesn’t change text on the next line.

Note

Remember to use the [force multipliers](#ch02.xhtml_key19-a) in the appropriate places. You can easily change multiple words by using **5cw**, or you can replace 10 characters with **10r**. Some commands don’t accept the force multipliers, such as **R**, and some behave differently than you might expect. For example, **10O** accepts text and then repeats it 9 more times.

##### Deleting Text and Lines

You can use **vim** to remove or delete characters, words, or even lines. Be careful to check your deletions and changes. Also keep in mind that you can press the **u** key to get things back to normal and try it again. These options are available for deleting text and lines in **vim**:

• **x:** Deletes a single character under the cursor.

• **X:** Deletes a single character before the cursor.

• **dw:** Deletes a single word that’s currently under the cursor, from the cursor position onward.

• **dd:** Deletes the current line entirely, regardless of the cursor position in the line.

• **D:** Deletes all text from the current cursor position to the end of the line.

• **dL:** Deletes all text from the cursor to the end of the screen.

• **dG:** Deletes all text from the cursor to the end of the file.

• **d^:** Deletes all text from the beginning of the line to the cursor.

Note

When you delete in **vim**, **vim** stores the cut or deleted string of text in the unnamed buffer for future use. This buffer’s contents will be overwritten by any further cuts or deletions.

**Tip**

For the Linux+ exam, it is important to know how to delete. If asked to delete from the current position to the end of the line, don’t pick or type the keys that delete the whole line; there are no partial credits on the exam!

#### Searching in vim

To search for text in Linux utilities, you typically need to follow a common convention. With the **less**, **more**, and **vim** commands, a forward slash followed by a search term searches forward in the file from the current cursor position or the top of the file, highlighting found strings. Initiating a backward search from the cursor position is done with a question mark followed by the string to search for, such as **?*sometext***.

Note

Searches are performed only in Command mode, so remember to press the **Esc** key to get back there before searching.

Finding the next occurrence (whether a forward or backward search) is usually accomplished by pressing the unshifted **n** key to search in the same direction as the original search. You press **Shift+N** for a search in the opposite direction of the original search.

![Images](graphics/key_topic_icon.jpg)

#### Searching and Replacing

When you want to search a document for a given string or character to replace it, you commonly use either **vim** while editing a given file or the **sed** command on a large set of data. **vim** and the **sed** command share a common search-and-replace syntax, with small differences that won’t confuse you if you use both. Indeed, learning to search and replace in one will equip you how to use it in the other.

The search-and-replace syntax is as follows:

```
action/tofind/replacewith/modifier
```

For example, the following string in **vim** replaces just the first instance of the string **bob** in the current line with the string **BOB**:

```
:s/bob/BOB/
```

To replace all instances of the string **bob** with **BOB** in the current line, you would use this line:

```
:s/bob/BOB/g
```

The **g** stands for *global*, or doing the action on every found instance of the string.

To replace all instances of **bob** with **BOB** in the entire file, no matter how many exist or how many changes are made to each line, you would use this:

```
:%s/bob/BOB/g
```

**Tip**

It’s critical that you read a multiple-choice Linux+ exam question and all its answers to see exactly what is being asked for. A percent symbol (%) in front of the search-and-replace string causes **vim** to search the entire file rather than just the current line.

### nano, nano

In the past 20 or so years, we have seen a sea change from the use of more powerful editors like **vim** and **EMACS** to ones like nano. nano is quick and easy to use, gives you onscreen clues about what keystrokes are available, and edits files quite nicely.

As a bit of historical perspective, computers used to have very limited RAM and disk space, so it was essential not to load them up with extra packages when very usable packages already existed on the system by default.

Many times I have rolled up to someone else’s computer–whether a desktop, a server, or remotely–and edited a file in **vi** or **vim**, without a thought about any other editors. The only places I haven’t been able to use **vi**/**vim** were on a couple of network edge systems that were embedded OS versions. This shows you how consistently **vi**/**vim** is deployed and available.

![Images](graphics/key_topic_icon.jpg)

#### Why nano and not Pico?

nano is almost an exact clone of the Pico editor, which has existed for a long time. Pico, a non-free software-licensed program that has existed for many years on Unix and Linux, was originally a part of the Pine email program. (It was the editing part, which makes sense.)

For many reasons, Linux distribution maintainers did not want to include the Pico editor with all the other programs in a Linux distribution. Mixing free licensed software and non-free licensed software is problematic and inelegant and will generally get you frowned upon in the world of Linux and open source.

Chris Allegretta created nano in an attempt to make a virtual clone of Pico that was easily distributable under appropriate free software licensing. However, it has grown to include a number of features that have taken it far beyond Pico’s capabilities, earning it respect in its own right.

#### nano’s Interface

Unlike **vi**/**vim**, which has a very sparse interface, nano gives you some onscreen clues about useful keystrokes. Instead of requiring you to use action keys and LastLine commands such as **:wq**, nano allows you to use the **Ctrl** key with another key. [Figure 2-5](#ch02.xhtml_ch02fig05) illustrates the user interface with the **nano** command invoked.

![Images](graphics/key_topic_icon.jpg)![Images](graphics/02fig05.jpg)

**Figure 2-5**–The **nano** command interface, showing the **Ctrl**-key editing and formatting options onscreen

As you can see in this figure, the last two lines of the **nano** interface are devoted to 14 useful commands and provide hints about what to press. The ^ character denotes the **Ctrl** key, and it is followed by the character you would then press while holding down the **Ctrl** key, such as **Ctrl+X** to exit the file or buffer if there is no file you are editing (at which point you are prompted to save or discard anything done in your nano session).

The interface is a little misleading in that the characters that follow the ^ character in the interface are uppercase letters. However, you do not have to use **Ctrl-Shift-X** to exit the editor. This was apparently done for readability and is notable because the rest of Linux and command line interactions are very specific about uppercase/lowercase distinctions.

In addition to the **Ctrl** key combinations, you can use the Meta key, which is mapped variously but is universally accessible by pressing the **Esc** key plus the keystroke character indicated. For example, after entering some text, you could tap the **Esc** key and then press the **U** key to invoke the Undo function, and then tap **Esc** again and press the **E** key to restore what you just undid.

**Tip**

**nano** allows for the use of Esc as the Meta (M) key, but it also might–depending on your computer’s OS, how it’s configured by the user, and other factors–allow you to use the Windows key on the keyboard of a PC or the Cmd or Apple key on a Mac system.

You can also use the mouse to select, cut, copy, and paste text inside **nano**, even on a non-GUI session, if the mouse is recognized by the text terminal you are operating in.

#### That’s a Wrap

**nano** is a little more self-explanatory than **vi**/**vim** is, but if you want to know more, see the help documentation, accessible by pressing **Ctrl+G** and using the navigation keys to find out all about **nano**’s features and key combinations.

### Summary

In this chapter you learned about a large amount of file and directory related tasks that affect the daily operations of a system. You learned about files and directories, how to manage them, how to get more information about your system's files and how to use commands like file and stat to get much more info of a useful nature and format it. You also learned about links, both hard and soft or symbolic, all about how file compression, using the **tar** command and how to backup data happens.

Additionally, you realized and learned that data needs to be sent between systems using the **scp** command and it's options, and finally learned a comprehensive though not too lengthy amount about editing text on Linux systems with nano and my personal favorite editor, VIM.

### Exam Preparation Tasks

As mentioned in the section “*Goals and Methods”* in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 2-2](#ch02.xhtml_ch02tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 2-2**–Key Topics for [Chapter 2](#ch02.xhtml_ch02)

![Images](graphics/02tab02.jpg)![Images](graphics/02tab02a.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[absolute pathname](#ch02.xhtml_key01)

[relative path](#ch02.xhtml_key02)

[permissions](#ch02.xhtml_key03)

[ownership](#ch02.xhtml_key04)

[glob](#ch02.xhtml_key05)

[globbing](#ch02.xhtml_key06)

[recursive](#ch02.xhtml_key07)

[metadata](#ch02.xhtml_key08)

[format sequence](#ch02.xhtml_key09)

[symbolic link](#ch02.xhtml_key10)

[hard link](#ch02.xhtml_key11)

[archiving](#ch02.xhtml_key12)

[compression](#ch02.xhtml_key13)

[incremental](#ch02.xhtml_key14)

[differential](#ch02.xhtml_key15)

[command mode](#ch02.xhtml_key16)

[insert mode](#ch02.xhtml_key17)

[lastline mode](#ch02.xhtml_key18)

[force multiplier](#ch02.xhtml_key19)

[tarball](#ch02.xhtml_key20)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** You are currently located in the directory /etc/nginx/conf.d and want to return to the home directory for your user in the shortest number of typed characters. Which of the following will accomplish this?

**a.** cd .

**b.** cd ~

**c.** cd

**d.** cd $$

**2.** Which of the following commands will consult a reference set of data types and report back information on each file it is used on?

**a. stat**

**b. ls -lT**

**c. file**

**d. info**

**3.** Which of the following is a characteristic that distinguishes a symbolic link from any other type?

**a.** It has a different inode number

**b.** You can change it's permissions easily

**c.** The linked file shares the same name

**d.** It cannot span across filesystems

**e.** Deleting one link has no effect on the other

**4.** You find a backup file that has an extension of .bz2\. Which of the following commands was this file likely created with?

**a. tar -czvf**

**b. tar -cyvf**

**c. tar -cjvf**

**d. tar -cbvf**

**5.** You are trying to copy a local directory and all of it's contents to a remote system, and are getting an error, what is the most likey option to include to the **scp** command to get the result you want?

**a. -x**

**b. -r**

**c. -z**

**d. -f**

**6.** You are using **vi** or the VIM text editor to write a technical article for your organization’s website, and after typing a couple of lines of content, you want to save and exit the file. Which of the following keystrokes will accomplish saving and exiting the file? (Choose two.)

**a. ESC**

**b. :wq**

**c. :F1**

**d. :save**

**e. ZZ**

## Chapter 3\. Configuring and Managing Storage [This content is currently in development.]

**This content is currently in development.**

## Chapter 4\. Managing Process and Services [This content is currently in development.]

**This content is currently in development.**

## Chapter 5\. Using Network Tools and Configuration Files [This content is currently in development.]

**This content is currently in development.**

## Chapter 6\. Building and Installing Software

This chapter covers the following topics:

• [Package Management](#ch06.xhtml_ch06lev1sec03)

• [Sandboxed Applications](#ch06.xhtml_ch06lev1sec05)

• [System Updates](#ch06.xhtml_ch06lev1sec06)

The exam objectives covered in this chapter are as follows:

• **Objective 1.6:** Given a scenario, build and install software.

Linux systems are made up of a lot of software, all organized in packages, or collections of software code, directories, files, supporting files and often as not, pre-compiled binaries of those applications.

Packages are the top-level manifestation of the software world, they are constructed to make distribution, installation, removal, updating and other administrative tasks easier and less prone to errors and conflicts.

A Linux system is meant to be useful, such as serving as some kind of application server or allowing a user to read email or browse the Web. The Linux kernel is great, but by itself it doesn’t do much; to make a Linux system useful, you need software.

A lot of software is available for Linux; you just need to install it. You can install software in a few ways, depending on your distribution and how the software was packaged.

At one point software was distributed in *source format*, which needed to be compiled into something that could run on a computer. Source format is still around, but as a community, we’ve moved on to distributing *binary packages* that are much easier to install. Binary packages avoid the compilation step (by being already compiled); in addition, dependencies, libraries, configuration, and documentation are automatically managed. There are a few different formats of these packages, but two are most prevalent: Debian style and Red Hat style. You are expected to know both of these main styles for the Linux+ exam because many computing environments have both types of systems, and the package style used depends on the project and the services being provided by the systems.

Additionally, we'll look into the newer area of application sandboxing, or what is also called app containerization, via Snap, FlatPak and AppImage.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 6-1](#ch06.xhtml_ch06tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 6-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/06tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** Which of the following is most likely a Debian/Ubuntu package file?

**a.** packagename.tgz

**b.** packagename.rpm

**c.** packagename.deb

**d.** packagename.sh

**2.** A type of package is described as being a derivative of a cpio archive with some added meta information. Which package type best describes this sort of package?

**a.** RPM

**b.** Slackware

**c.** Debian

**d.** Gentoo

**3.** Which of the following is NOT a desired feature of using sandboxed applications?

**a.** Built for any and every distribution

**b.** Full control over dependencies

**c.** Requires permission to access host resources

**d.** Application updates via the host distribution

**4.** Which of the following are common features among the 3 application sandboxing methods popular in Linux software? (AppImage, Flatpak and Snap) Choose all that apply.

**a.** Run without root access

**b.** Must run from an uncompressed source

**c.** Multiple running versions possible

**d.** Can be updated independently from distro

**e.** Has access to system-level resources

**f.** Vendor independent repositories

**5.** What types of updates are best suited for use as Live Kernel Patching updates?

**a.** Binary

**b.** Security

**c.** Feature

**d.** Module

**6.** This application sandboxing method has as a feature a "one file per app" specification. Which of the following does this best describe?

**a.** Snapd

**b.** Flatpak

**c.** AppImage

**d.** AppArmor

### Foundation Topics

### Package Management

A package is a compressed archive file that contains all the necessary files that make up a given command, application, or set of applications. Packages come in several different formats, such as RPM, DEB, and a few others, but they are all similar in their function, if slightly different in format.

#### The Most Common Package Types

![Images](graphics/key_topic_icon.jpg)

The most common package types are **rpm** (Red Hat Package Manager) and **deb** (Debian Package Format) files. Packages can come in several other formats, chief among them compressed files such as **.tar** (tar archive), **.tgz** (tar archives compressed with the **gzip** command), and **.gz** (a package that has been compressed with the **gzip** command).

A compressed (**.tar**/**.tgz**/**.gz**) file is not a package that can be installed by a package manager such as RPM or Apt. Instead, it must be unarchived so the contained file or files can be either compiled from source or, if a binary, copied to the proper location for execution.

[RPM](#ch06.xhtml_key05-a) package files are typically in the cpio archive format, with an **.rpm** extension (for example, **application.rpm**), and consist of the following:

• **Header:** The header is a separate structure that defines the file’s format and tagged data that contains the package info, copyright and versions, build host, and a package integrity signature.

• **Archive:** An archive holds package files, including scripts to be run during installation, files to be copied, and links to be made.

Debian packages are usually in the ar archive format, have a **.deb** extension (for example, **application.deb**), and consist of the following:

• **data.tar.gz:** A hierarchically related set of files, man pages, links, and so on to be copied to the system during the install.

• **control.tar.gz:** All package information, including copyright, description, and so on. Also contains any scripts that should be run in the process of installation or removal of the package.

#### Package Managers

Package managers were invented to solve the problem of software version proliferation and the cruft of extra or abandoned files that result from many upgrades or installations.

A package manager keeps track of which files belong to which package, which packages depend on which other packages, and where the different types of files are stored. All modern distributions of Linux use package managers in some fashion.

#### Debian Package Management

Debian and Debian-derived systems such as Ubuntu have a powerful package management system that provides a way for administrators to find, install, query, and remove packages. The package tracks the parts of an application and helps you figure out which other packages (dependencies) are needed to install a given package and whether any packages rely on other packages.

The basic unit of Debian package management is a file with a **.deb** extension (for example, **application.deb**), as explained earlier.

You can install, remove, and query packages with the [dpkg](#ch06.xhtml_key06-a) tool, typically in a single-package mode. Installing multiple packages is possible but can quickly become cumbersome due to interlocking dependencies.

To install a package and all its dependencies and even get new packages from an online and updated source, you need to employ a package management tool such as the [APT](#ch06.xhtml_key04-a) (Advanced Package Tool) suite.

Commonly known collectively as apt-get, the APT suite can make even many-part package installs, updates, and even entire system upgrades as simple as a couple of easily remembered commands and options.

Graphical and text-based interfaces such as **aptitude** and **synaptic** are layered on top of the APT tools. They give you an interface that’s easier to use than having to remember commands.

So, to recap: Local packages are **.deb** files and are installed with **dpkg**. APT handles searching remote package repositories and downloading packages. Aptitude and the like provide a graphical interface to APT. The graphical and APT tools use the **dpkg** command as their underlying package interaction tool, supplying it with the needed commands and options and arguments to effectively automate the process of installation, removal, and updating/upgrading large numbers of packages easily.

##### Managing Local Debian Packages

![Images](graphics/key_topic_icon.jpg)

The **dpkg** tool manipulates packages on a system and can process the **.deb** packages you might download. If you have a package on a system, you can find out what’s inside it by using the **--info** option, as shown in [Example 6-1](#ch06.xhtml_exe6_1).

**Example 6-1**–Finding Out What’s Inside a .deb File

```
# dpkg --info acct_6.5.5-1_amd64.deb
 new debian package, version 2.0.
 size 120424 bytes: control archive=1899 bytes.
 79 bytes, 4 lines conffiles
 746 bytes, 18 lines control
 1766 bytes, 27 lines md5sums
 507 bytes, 30 lines * postinst #!/bin/sh
 370 bytes, 26 lines * postrm #!/bin/sh
 163 bytes, 7 lines * prerm #!/bin/sh
 Package: acct
 Version: 6.5.5-1
 Architecture: amd64
 Maintainer: Mathieu Trudel-Lapierre <mathieu.tl@gmail.com>
 Installed-Size: 380
 Depends: dpkg (>= 1.15.4) | install-info, libc6 (>= 2.3)
 Section: admin
 Priority: optional
 Homepage: http://www.gnu.org/software/acct/
 Description: The GNU Accounting utilities for process and login accounting
 ...
```

![Images](graphics/key_topic_icon.jpg)

The information about the package is contained inside the **.deb** file; the **dpkg** command displays it nicely for you. The top section describes the control files that provide the metadata for **dpkg** to use. The file itself is 120,424 bytes, and inside it is an archive of control files totaling 1899 bytes. Inside that archive are

• **conffiles:** A list of files used to configure the package after it’s installed. These files are treated differently than other files in the package; for example, they are not removed when the package is removed.

• **control:** The file containing all the metadata about the packages, such as dependencies.

• **md5sums:** A list of files and a checksum so that you can verify that the file hasn’t changed at any point.

• **postinst:** A shell script that is run after the installation.

• **postrm:** A shell script that is run after the removal of the package.

• **prerm:** A shell script that is run just before the package is removed.

After the control information you see various pieces of information about the package, such as the name, version, which hardware it is meant to go on, and the dependencies.

##### Installing Packages with dpkg

The most common way to install packages is by using one of the following commands at the command line from the current directory:

```
# dpkg --install gcc-4.7-base_4.7.2-5_amd64.deb
# dpkg -i gcc-4.7-base_4.7.2-5_amd64.deb
```

This returns output similar to the following:

```
Selecting previously unselected package gcc-4.7-base:amd64.
(Reading database ... 142987 files and directories currently
installed.)
Unpacking gcc-4.7-base:amd64 (from gcc-4.7-base_4.7.2-5_amd64.deb) ...
Setting up gcc-4.7-base:amd64 (4.7.2-5) ...
```

Sometimes you need to install dependencies for a package. You can either install the dependency first or specify all the necessary packages on the same command line. The command for the latter option looks like this:

```
# dpkg -i gcc-4.7-base_4.7.2-5_amd64.deb
libgcc1_1%3a4.7.2-5_amd64.deb
```

##### Removing Packages

When you need to remove a package with the **dpkg** command, you can use one of two methods: **remove** or **purge**. The **-r** or **--remove** option removes the package’s files but leaves any configuration files intact on the disk. The other option for getting rid of packages is the **-P** or **--purge** option, which removes all the package’s files, including any configuration files.

To remove a package but leave its configuration files in place, use one of the following:

```
# dpkg --remove package_name
# dpkg -r package_name
```

To purge a package, including its configuration files, use one of the following:

```
# dpkg --purge package_name
# dpkg -P package_name
```

When a package is installed, any configuration files are noted in the **conffiles** file. You can use this file to determine which files are left in place during a remove action and which files should also be purged in a purge action.

##### Dependency Issues

When you are working with packages, a desired package installation often finds entries in the package database that conflict with the files it is attempting to install. Also, sometimes during a removal, a package has a file it wants to remove that other packages depend on.

In keeping with the sturdy and less-than-verbose nature of Debian, using the package tools **--force** option can lead to some truly unpleasant circumstances for a machine. Take great care when removing packages that have dependencies, and read in detail the man page for **dpkg**’s **force** section. For the Linux+ exam, you need to know how to force an action, but you don’t need to know all 20 or so forcing options.

To force the removal of a broken package marked in the database as requiring reinstallation, use the following:

```
# dpkg --force-reinstreq package_name
```

Use **--force-reinstreq** on packages marked as requiring reinstallation; it allows **dpkg** to remove those packages.

In addition, you can use the **--force-depends** option after **--install** to turn all those nasty error messages into dire warnings, but the tool then allows you to do whatever inadvisable action you’re about to perform.

![Images](graphics/key_topic_icon.jpg)

Here’s an example:

```
# dpkg --install --force-depends package_name
```

Finally, you can use the **--force-remove-essential** option. Be warned, however, that overriding the dependency recommendations might leave your system in a broken state.

If you positively must (usually on direction from the vendor or a nearby Debian guru), you can force the installation of a package, regardless of the conflicts generated with the command and options, like so:

```
# dpkg --install new_pkg.deb --force-conflicts
```

If you have problems with the package or other packages after forcing past any conflicts, remember that you were warned.

##### Querying Packages

Keep in mind that when you are querying packages and not referring to a **.deb** file on the local disk or mounted filesystems, you are actually querying the package database–that is, the complete list of all the packages and their file locations that are currently installed to the system through **dpkg** or another package management tool.

Packages currently installed can be queried for a plethora of information. In particular, you can list the existence, version, name, and a description of a package by using the **-l** or **--list** option:

```
# dpkg --list krb*
# dpkg -l krb*
```

You can use either a singular package name, such as **krb5-user** for a Kerberos-related package, or the previous filename to see the listing shown in the following output:

```
# dpkg --list krb*
Desired=Unknown/Install/Remove/Purge/Hold
|
Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Architecture Description
+++-=================-===============-===============-
==============================
un krb5-doc <none> (no description available)
ii krb5-locales 1.10.1+dfsg-5+d all Internationalization
support for MIT Kerberos
un krb5-user <none> (no description available)
```

After some headers, the output shows that there are three packages starting with **krb5**. Two of them, with lines beginning with the string **un**, are uninstalled, while **krb5-locales** is installed as version 1.10.1\. The Debian package system shows you packages previously installed on your system, which is different from other systems.

![Images](graphics/key_topic_icon.jpg)

You can check the status of a particular package or packages by using the **-s** or **--status** option:

```
# dpkg --status krdc
```

The output returned is an abbreviated version of what you get with the **--info** option.

You can see the files that were installed by a package by using the **-L** or **--listfiles** option:

```
# dpkg --listfiles coreutils
```

This results in output similar to the following (which has been truncated to fit):

```
/.
/bin
/bin/cat
/bin/chgrp
/bin/chmod
/bin/chown
```

The use of either the **-S** or the **--search** option lets you search the installed files on disk via the package database, such as

```
# dpkg -S apt.conf
```

The following output contains the various places an **apt.conf** file was found from the database entries:

```
apt: /etc/apt/apt.conf.d/01autoremove
unattended-upgrades:
/etc/apt/apt.conf.d/50unattended-upgrades
apt: /usr/share/man/ja/man5/apt.conf.5.gz
apt: /usr/share/man/pt/man5/apt.conf.5.gz
apt: /usr/share/doc/apt/examples/apt.conf
apt-listchanges: /etc/apt/apt.conf.d/20listchanges
aptdaemon: /etc/apt/apt.conf.d/20dbus
aptdaemon: /etc/dbus-1/system.d/org.debian.apt.conf
```

The output lists all the packages that contain a file with **apt.conf** in the name. The package name is on the left, and the filename is on the right. Note that the search string can happen anywhere within the filename, even if it’s a directory name.

##### Reconfiguring Packages

Some packages include a configuration tool that is executed when you install the package. This tool makes it easy to manage the initial setup of the software you are installing. If a package includes such a configuration tool, you can run that utility again with the **dpkg-reconfigure** command followed by the name of the package.

[Figure 6-1](#ch06.xhtml_ch06fig01) shows the output of running the Postfix mail server configuration with this command:

```
# dpkg-reconfigure postfix
```

![Images](graphics/06fig01.jpg)

**Figure 6-1**–Reconfiguring Postfix with **dpkg-reconfigure**

#### Using Repositories

It is possible for a CD/DVD or an ISO image of a CD/DVD to hold only a limited amount of software (or packages). An ever-expanding amount of the available software for any distribution can be found online, either as a single source code set, as prebuilt packages for download, or in a combination of official, semi-official, and very unofficial locations collectively called *repositories*.

Repositories in Debian/Ubuntu can be confusing, as Ubuntu and Canonical have a close relationship, so when discussing repositories, it’s impossible to avoid or not show the Main or official Canonical supported repository. To keep things easier, we’ll discuss repositories from the standpoint of the Ubuntu distribution, and you can look up anything you might need to learn for standard Debian.

The APT tools work by maintaining a local cache of what packages are available on remote servers, including the dependencies. This means you can search your local cache much more quickly than if you had to query remote servers.

![Images](graphics/key_topic_icon.jpg)

The list of remote package repositories is stored in **/etc/apt/sources.list** and in individual files under **/etc/apt/sources.list.d**. Each line represents one repository.

A **sources.list** file may look like [Example 6-2](#ch06.xhtml_exe6_2).

**Example 6-2**–A Default Sources List File

```
deb http://cdn.debian.net/debian/ wheezy main
deb-src http://cdn.debian.net/debian/ wheezy main

deb http://security.debian.org/ wheezy/updates main
deb-src http://security.debian.org/ wheezy/updates main

# wheezy-updates, previously known as ‘volatile’
deb http://cdn.debian.net/debian/ wheezy-updates main
deb-src http://cdn.debian.net/debian/ wheezy-updates main
```

##### What Is a Repository?

![Images](graphics/key_topic_icon.jpg)

At its simplest, a repository is a collection or an archive of software that can be addressed by the system. Repositories can exist on local disk, on attached or mounted disk, or even across a local or wide area network on a server via a sharing protocol such as HTTP or FTP.

Ubuntu repositories come in various types, including

• **Main:** Canonical-supported free and open source packages

• **Universe:** Community-maintained free and open source packages

• **Restricted:** Proprietary driver packages for devices

• **Multiverse:** Software that has copyright or legal issues

Typically, the Ubuntu installation media contains packages that are drawn from the most recent version of the Main and Restricted repositories so that you can actually complete a proper install. In modern Linux, installation is just the start; in order to get updates and additional software, it’s necessary to have the correct repositories configured.

##### Viewing Configured Repositories

During installation, the system configures a number of default repositories by placing the appropriate entries in the **/etc/apt/sources.list** file or, if you prefer, by having files that end with the **.list** extension in the **/etc/apt/sources.list.d** directory.

An example of a populated **sources.list** file is shown in [Example 6-3](#ch06.xhtml_exe6_3).

**Example 6-3** Contents of a sources.list file

```
# deb cdrom:[Ubuntu 18.04.1 LTS _Bionic Beaver_ - Release amd64 (20180725)]/
bionic main restricted
# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb http://us.archive.ubuntu.com/ubuntu/ bionic main restricted
# deb-src http://us.archive.ubuntu.com/ubuntu/ bionic main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://us.archive.ubuntu.com/ubuntu/ bionic-updates main restricted
# deb-src http://us.archive.ubuntu.com/ubuntu/ bionic-updates main restricted
## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb http://us.archive.ubuntu.com/ubuntu/ bionic universe
# deb-src http://us.archive.ubuntu.com/ubuntu/ bionic universe
deb http://us.archive.ubuntu.com/ubuntu/ bionic-updates universe
# deb-src http://us.archive.ubuntu.com/ubuntu/ bionic-updates universe
## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team, and may not be under a free licence. Please satisfy yourself as to
## your rights to use the software. Also, please note that software in
## multiverse WILL NOT receive any review or updates from the Ubuntu
## security team.
deb http://us.archive.ubuntu.com/ubuntu/ bionic multiverse
# deb-src http://us.archive.ubuntu.com/ubuntu/ bionic multiverse
deb http://us.archive.ubuntu.com/ubuntu/ bionic-updates multiverse
# deb-src http://us.archive.ubuntu.com/ubuntu/ bionic-updates multiverse
```

In this example, several lines contain comments that are preceded with the **#** (hash or comment) character. Uncommented lines are actual repository configurations.

The repository lines break down as follows:

• **deb:** This denotes that the repository contains precompiled or binary packages; it is the most common repository type.

• **deb-src:** This means that the repository contains packages of source code that are put together for easy transport and “installation,” or copying to the user’s system.

• **URL:** In most cases (that is, the four main repository channels) the URL is [http://us.archive.ubuntu.com/ubuntu/](http://us.archive.ubuntu.com/ubuntu/). Consult the official mirrors list on [www.ubuntu.com](http://www.ubuntu.com) for more options.

• **Trusty:** This is the release name or the version of the Ubuntu distribution and affects what software is being pulled from the repository.

• **Main:** This is the name of the component or section, in lowercase and separated by spaces. There can be several components or sections.

##### Adding Repositories

To manually add a repository from the command line, you can either edit the **/etc/apt/sources.list** file, add a file containing the appropriate line(s) to the **/etc/apt/sources.list.d** directory, or use the **add-apt-repository** command, as in the [Example 6-4](#ch06.xhtml_exe6_4):

**Example 6-4** Adding a repository via the add-apt-repository command

```
# sudo add-apt-repository “deb
http://us.archive.ubuntu.com/ubuntu/ bionic universe”
Hit:1 http://us.archive.ubuntu.com/ubuntu bionic InRelease
Get:2 http://us.archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]
Get:3 http://security.ubuntu.com/ubuntu bionic-security InRelease [83.2 kB]
Get:4 http://us.archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6
kB]
Get:5 http://us.archive.ubuntu.com/ubuntu bionic-updates/ main i386 Packages
[389 kB]
Get:6 http://us.archive.ubuntu.com/ubuntu bionic-updates/ main amd64 Packages
[437 kB]
Get:7 http://us.archive.ubuntu.com/ubuntu bionic-updates/ main
Translation-en [164 kB]
Get:8 http://security.ubuntu.com/ubuntu bionic-security/ main i386 Packages
[164 kB]
Get:9 http://security.ubuntu.com/ubuntu bionic-security/ main amd64 Packages
[206 kB]
Get:10 http://security.ubuntu.com/ubuntu bionic-security/ main Translation-en [81.0 kB]
Fetched 1,687 kB in 1s (1,376 kB/s)
Reading package lists... Done
```

This process adds an appropriate repository line to the **/etc/apt/sources.list** file, making that software available to be queried, installed, and used.

While you can use the **apt-add-repository** command to do a lot of things, including add, remove, and auto-update on add, it’s more traditional to use your favorite text editor and make the changes directly to the **/etc/apt/sources** tree of files and directories or even to use the graphical software tools, which are beyond the scope of this discussion.

#### Installing Remote Packages

Now that you know what repositories are and how to add them to your systems, you can use the **apt-get** utility for most remote software installation operations. Every **apt-get** invocation is followed by a command that indicates what to do. Use the **install** command to install a package, as shown in [Example 6-5](#ch06.xhtml_exe6_5).

**Example 6-5**–Installing a Remote Package

```
# sudo apt-get install nginx-light
[sudo] password for tux:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libnginx-mod-http-echo nginx-common
Suggested packages:
  fcgiwrap nginx-doc
The following NEW packages will be installed:
  libnginx-mod-http-echo nginx-common nginx-light
0 upgraded, 3 newly installed, 0 to remove and 8 not upgraded.
Need to get 449 kB of archives.
After this operation, 1,503 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://us.archive.ubuntu.com/ubuntu bionic-updates/ main
amd64 nginx-common all 1.14.0-0ubuntu1.2 [37.4 kB]
Get:2 http://security.ubuntu.com/ubuntu bionic-security/universe
amd64 libnginx-mod-http-echo amd64 1.14.0-0ubuntu1.2 [21.3 kB]
Get:3 http://security.ubuntu.com/ubuntu bionic-security/universe
amd64 nginx-light amd64 1.14.0-0ubuntu1.2 [390 kB]
Fetched 449 kB in 1s (448 kB/s)
Preconfiguring packages ...
Selecting previously unselected package nginx-common.
(Reading database ... 163823 files and directories currently installed.)
Preparing to unpack .../nginx-common_1.14.0-0ubuntu1.2_all.deb ...
Unpacking nginx-common (1.14.0-0ubuntu1.2) ...
Selecting previously unselected package libnginx-mod-http-echo.
Preparing to unpack .../libnginx-mod-http-echo_1.14.0-0ubuntu1\. 2_amd64.deb
...
Unpacking libnginx-mod-http-echo (1.14.0-0ubuntu1.2) ...
Selecting previously unselected package nginx-light.
Preparing to unpack .../nginx-light_1.14.0-0ubuntu1.2_amd64.deb ...
Unpacking nginx-light (1.14.0-0ubuntu1.2) ...
Processing triggers for ufw (0.35-5) ...
Processing triggers for ureadahead (0.100.0-20) ...
Setting up nginx-common (1.14.0-0ubuntu1.2) ...
Created symlink /etc/systemd/system/multi-user.target.wants/nginx. service
 /lib/systemd/system/nginx.service.
Processing triggers for systemd (237-3ubuntu10.6) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Setting up libnginx-mod-http-echo (1.14.0-0ubuntu1.2) ...
Setting up nginx-light (1.14.0-0ubuntu1.2) ...
Processing triggers for ureadahead (0.100.0-20) ...
Processing triggers for ufw (0.35-5) ...
```

[Example 6-5](#ch06.xhtml_exe6_5) installs the **nginx-light** package through **apt-get install nginx-light**. The program determines that the **nginx-common** package is also required, so both packages are downloaded and installed. Any setup scripts, including **dpkg-reconfigure**, are run at this time as well.

![Images](graphics/key_topic_icon.jpg)

Finally, pay attention to the differences between the **apt-get** and **dpkg** commands, especially with regard to the first option. **apt-get** commands do not have a leading dash or dashes, while **dpkg** commands do. For example, **dpkg -i** installs a local package, but **apt-get install** installs a remote package. Don’t get tripped up on any questions that try to conflate the two, such as with **apt-get --install pkgname**.

##### Working with the Cache

The APT tools work by maintaining a local cache of the packages available on remote servers, including the dependencies. You can search your local cache much more quickly than if you had to query remote servers.

You must update the package cache after modifying **sources.list** or to fetch any upstream changes. You do this by running **apt-get update**.

When the APT cache is up to date, you can investigate packages by using the **apt-cache** command:

**apt-cache search *term*:** Searches for packages matching the term

**apt-cache show *package_name*:** Shows information about a given package name, including a description and dependencies

**apt-cache showpkg *package_name*:** Shows more technical details about a package, such as what depends on it, what it depends on, and what services it provides

#### Upgrading the System

A system has many packages installed–hundreds or even thousands of them. Each one of these packages might need updates at some point in time. Updates take the form of:

Security updates that fix problems in a package that could lead to bad guys doing bad things on the machine

Bug fixes to correct problems in software that cause it to perform incorrectly, crash, or even lose data

Feature improvements that update to the latest version of some software

To update a specific package, you reinstall that package as shown here:

```
# apt-get install cpio
Reading package lists... Done
Building dependency tree
Reading state information... Done
Suggested packages:
 libarchive1
The following packages will be upgraded:
 cpio
```

The last two lines of the output show that **apt-get** upgrades the package rather than installing it fresh. If **cpio** weren’t installed, it would be installed. If it’s important that the package not be installed if it is missing, add the **--only-upgrade** long option.

Updating package by package is tedious. You can run **apt-get dist-upgrade** to upgrade all the packages on a system at once. If you are running a more conservative system, using **apt-get upgrade** is a safer choice. The difference between the two upgrade options is that **dist-upgrade** may remove some minor packages to handle dependency problems, while **upgrade** would rather fail than remove a package.

#### Removing Packages

A time will come when you want to get rid of a package entirely. The **apt-get** command has two options: **remove** and **purge**. The difference is that **remove** leaves behind configuration files, while **purge** gets rid of them entirely.

#### Graphical Managers

At times it’s useful to view package management in an interface where you can look at packages graphically instead of working on a command line. Debian offers two graphical package managers: aptitude and synaptic. They are both front ends to the APT tools. Aptitude has a text mode interface, while Synaptic is fully graphical. [Figure 6-2](#ch06.xhtml_ch06fig02) shows the two next to each other, with Synaptic running on the left and Aptitude running inside a terminal window on the right.

![Description: A screenshot of a computer Description automatically generated](graphics/06fig02.jpg)

**Figure 6-2**–A look at graphical package managers

### RPM and YUM Package Management

![Images](graphics/key_topic_icon.jpg)

RPM refers not only to the package format but the **rpm** command and the RPM database. The components of the RPM package management style are as follows:

**The RPM database:** A collection of files that manage the RPMs on a system

**Package files:** The packages in RPM format that are distributed with the **.rpm** extension

**The rpm command:** Used for all package installation, removal, and query tasks

Graphical package management tools such as gnorpm or the RPM-handling routines built in to various file managers (such as Nautilus and Konqueror) are typically just a front end to the text-mode **rpm** command and provide a friendly interface for installing packages.

Note

Incidentally, RPM originally stood for Red Hat Package Manager before it became more widely used in other distributions. Referring to the system as RPM Package Manager will draw the ire of the graybeards in your office, almost as if you called an automated teller machine at your bank an “ATM machine.”

#### The RPM Database

The RPM database is a collection of Berkeley database files that together make up the database of packages and files installed by those packages on a system.

![Images](graphics/key_topic_icon.jpg)

The RPM database is located in the **/var/lib/rpm** directory. That directory contains many files in a binary format that are used by the **rpm** command. Thankfully, you don’t need to know all the files in the directory and their purposes, just that they are there and exist in an uncorrupted state.

Modifications to the RPM database are restricted to the root user. Unprivileged users can query and verify installed packages against this database.

The RPM database can become outdated or corrupted with heavy usage, and it might need to be rebuilt. To rebuild the database from the installed package’s headers, you use the following command as the root user:

```
# rpm --rebuilddb
```

This command does not produce output unless errors are found, and even then the errors are purely informational and not of much use for fixing the problem.

Only one user can use the database at a time. This prevents corruption of the data and prevents two people from installing software on top of each other. If you accidentally try to run two **rpm** commands while one has the database locked, you see the following:

```
warning: waiting for transaction lock on
/var/lib/rpm/.rpm.lock
```

This message simply indicates that the database is in use and cannot be locked for additional tasks at this time. This keeps multiple sysadmins from causing corruption by performing incompatible tasks simultaneously.

#### RPM Package Files

![Images](graphics/key_topic_icon.jpg)

RPM packages come in two types: source and binary. A binary RPM file is a discrete package that, when installed, copies to specified locations the compiled binary files, other associated files such as documentation and configuration, and any other files needed to run that package.

A source RPM file is a collection of the source files needed for installing a package, plus some instructions for building the binary RPM from the source.

There is an important distinction between installed packages and uninstalled package files. Information about an installed package comes from the RPM database, whereas information about an uninstalled package comes from the RPM file itself. After an RPM file has been installed, the original RPM is no longer required.

An RPM package contains a set of files and configuration scripts that comprise a software program or application in most instances. Notable exceptions are packages strictly for placing text configuration files, such as files in the **/etc** directory.

![Images](graphics/key_topic_icon.jpg)

An RPM package should contain at least the following:

• Compressed binary application files

• The name and version of the package’s software

• The build date and host on which it was built

• A description of the package and its purpose

• The checksums and dependencies required

##### Package Name Conventions

An installed package is known by a short name, although some operations require that long names be used. Typically, long package names are needed for deletions when multiple packages whose short names match exist.

Here’s an example of a short package name:

```
wireshark
```

Here’s an example of a long package name:

```
wireshark-2.6.4-1.fc30
```

To find two packages installed with different versions of the same software, use the following:

```
# rpm -q kernel
5.19.0-39-generic.fcXX.x86_64
4.31.0-13-generic.fcXX.x86_64
```

Viewing a particular package’s information can be difficult if you use the **-l** and **-i** options for file listings and info pages. Most of the time, you want to see information about only one of the packages, so to see just that package’s details you must use the long name (**5.19.0-39-generic.fcXX**) in the query, which isolates that individual package for the query.

#### The rpm Command

![Images](graphics/key_topic_icon.jpg)

The text-mode **rpm** package tool is used to perform all operations on packages on the system, either installed and in the RPM database or uninstalled and on disk.

Common operations that use the **rpm** command include:

• Installing packages

• Upgrading packages

• Removing and uninstalling packages

• Querying the RPM database for information

• Verifying the package file

• Checking installed files

The **rpm** command keywords and options come in several formats. The common options are single letters (for example, **-i** for installation). There are almost always long options that match, and some options occur only in the long format.

Note

On the Linux+ exam, you might see long options in several locations, either right after a short option or on the end of the entire command. The important thing is to have tried the long options and to know that you can tack them on the end, as long as something else doesn’t depend on that option’s placement.

##### Validation of Packages

For purposes of security, it’s important that you validate or check the signatures of packages that are downloaded from any source other than the distribution vendor’s site; otherwise, you could end up installing malware. RPM uses two checks to ensure the integrity of a package: MD5 and PGP (or its open source variant, GPG).

MD5 acts as a checksum to make sure that the package contents have not changed since the package was created. The PGP or GPG signature is tied to a particular person or organization and indicates that the person or organization created the package.

Validating a package typically takes place when the package is accessed or installed, although it can be triggered explicitly. To check the MD5 checksum and GPG signatures for the **R** statistics environment, you use the following command:

```
# rpm -K R-3.5.1-1.fcXX.x86_64.rpm
```

This returns the following output:

```
R-3.5.1-1.fcXX.x86_64.rpm: RSA sha1 ((MD5) PGP) md5 NOT OK (MISSING KEYS: (MD5) PGP#8e1431d5)
```

The presence of **NOT OK** shows that the signatures could not be verified. Importing the key from the distribution site fixes the problem. For example, if you are working on a Fedora system, you can execute the following:

```
# rpm --import https://getfedora.org/static/8E1431D5.txt
# rpm -K R-3.5.1-1.fcXX.x86_64.rpm
R-3.1.2-1.fcXX.x86_64.rpm: rsa sha1 (md5) pgp md5 OK
```

For the Linux+ exam, you just need to know that signatures come in MD5 and GPG varieties, plus the **--checksig** and -**K** options. The key is to be sure that the package you have is the original from the maintainer, not a package full of Trojan horses and rootkits.

##### Installation of Packages

![Images](graphics/key_topic_icon.jpg)

Installing software via packages requires root access, the **rpm** command, and a package or packages. Prior to installation, the **rpm** command checks to ensure the following:

• Enough free disk space exists for the package.

• Existing files will not be overwritten.

• All dependencies listed in the package are met.

You install packages with at least the **-i** option (or **--install**), and you can often include other options that improve the experience. To install the **R** package and get a progress bar (consisting of hash marks printed onscreen) and verbose messages on the installation, use the following command:

```
# rpm -ivh R-3.5.1-1.fcXX.x86_64.rpm
Preparing... ################################# [100%]
Updating / installing...
 1: R-3.5.1-1.fcXX ################################# [100%]
```

These options work well for installing groups of packages, too. Instead of specifying a single package, as shown previously, specify a file glob instead:

```
# rpm -ivh *.rpm
```

Wildcards can be used for installing and upgrading but not removing packages because the glob operator, *****, expands to match files in the current directory, not packages in the RPM database. For now, you just need to understand that ***.rpm** means “any file that ends in **.rpm**.”

##### Additional Installation Options

Whenever you install RPM packages, keep in mind that there will be extenuating circumstances such as files that exist on the system that RPM doesn’t know about but that will be overwritten by a package’s contents. Sometimes this happens when someone installs software manually or if a previous package operation fails.

Such situations can be handled with the **--replacefiles** or **--force** options. (The **force** option overrides a variety of these safeguards, including **replacefiles**, which just overrides the duplicate file safeguard.) For example, if you try to install a package named **tarfoo-1.2-3.i386.rpm**, and it finds a file on the system that will be overwritten by a file in the package, you get an error message stating so, and the installation fails:

```
# rpm -ivh tarfoo-1.2-3.i386.rpm
tarfoo /etc/tarfoo.conf conflicts with file from foobar-1.1
```

The solution is to check the offending file and either remove it if it’s unnecessary or use this command to force it:

```
# rpm -ivh --force tarfoo-1.2-3.i386.rpm
```

If the package won’t install due to unresolved dependencies, you can (somewhat foolishly!) use the **--nodeps** option to have the **rpm** command ignore dependencies. Using **--nodeps** without a clear fix in mind or an understanding of where the dependencies will come from will almost certainly cause problems when you try to use the software that the package provides.

For example, if you try to install the **pebkac** package, and it has dependency issues, it might look like this:

```
# rpm -ivh pebkac.1-1.fcXX.x86_64.rpm
```

This returns output such as

```
error: Failed dependencies:
 id10t = 3.5.1-1.fcXX is needed by pebkac.5.1-1.fcXX.x86_64
 loosenut = 3.5.1-1.fcXX is needed by pebkac.5.1-1.fcXX.x86_64
 hubproblem = 3.5.1-1.fcXX is needed by pebkac.5.1-1.fcXX.
x86_64
```

You face the possibility of seriously munging (messing up) your system if you use the **--nodeps** option outside a recommendation from the distribution vendor or a support professional. You might so severely damage the software that a full reinstall is the only option.

##### Verifying a Package’s Integrity

There might be situations in which you need to verify that a package is working properly. For example, if users are complaining about problems with running the software that came with a package, or if you suspect that someone has been tampering with your computer, you might want to verify the package.

![Images](graphics/key_topic_icon.jpg)

Verify an installed RPM with the **-V** option (or **--verify**) like so:

```
# rpm -V logrotate
S.5....T. c /etc/logrotate.conf
```

The status of the package is returned as a series of nine characters indicating the results of nine different tests:

• **S:** The file size differs.

• **M:** The mode differs (permissions or type of file).

• **5:** The MD5 sum differs; this is also seen with **--checksig**.

• **D:** The device’s major/minor number doesn’t match.

• **L:** A readLink(2) path problem exists.

• **U:** The user ownership was altered.

• **G:** The group ownership was altered.

• **T:** The modification time is different from the original.

• **P:** The capabilities set on the file differ.

Following the nine tests is an attribute marker that helps you understand whether the file should change as part of normal operations. The most common option is a configuration file, indicated by the letter **c**.

The output shown indicates that **/etc/logrotate.conf** is a configuration file that has changed in size, content, and modification time since the RPM was installed.

Change is not always a bad thing. Configuration files change often because the defaults provided by the distribution may not line up with current needs. Email configurations, log cleanup policies, and web server configurations are all things that get customized frequently and therefore show up as changes. If you expect them to change, you can ignore the output, which is why configuration files have the separate attribute marker. If you see a change to binaries, such as **/bin/ls**, you should be suspicious.

![Images](graphics/key_topic_icon.jpg)

To verify the state of all the packages on the system, you add an -**a** instead of specifying a package name, as shown here:

```
# rpm -Va
```

Note

If you choose to run the **rpm -Va** command, it will attempt to verify the nine points of status of EVERY file installed by EVERY package on your system, and this may/will take a long time and use a lot of CPU.

If you want to log the state of your configuration files for comparison against a future date, you can check the condition of every configuration file on the system and write it to a file with this command:

```
# rpm -Vac > /root/somelog.txt
```

##### Freshening vs. Upgrading

The daily maintenance of a newly installed system is likely to involve updates and fixes downloaded as package updates. Properly applying these updates and fixes to the system takes some finesse, particularly with a system that must stay as stable as possible or not have new software added to it without strict testing.

The -**U** and **--upgrade** options are designed to install or upgrade versions of packages to the latest version. An interesting side effect of these options is the removal of all other versions of the targeted package, leaving just the latest version installed.

As an example, the following command upgrades the system to the latest version of the RPMs in a particular directory of patches and fixes downloaded from the distribution vendor:

```
# rpm -U *.rpm
```

The **-U** and **--upgrade** options upgrade packages that are already installed and install packages that aren’t.

Freshening your system with the **-F** and **--Freshen** options is different in one important aspect: If a package isn’t installed and you try to freshen it with a new RPM, the installation is skipped. If the package is installed already, freshening behaves the same as upgrading.

As an example, you use the following to apply a directory full of RPM files that contains security patches and fixes to a firewall or another security server:

```
# rpm -Fvh *.rpm
```

This feature is useful for local package cache updates, where you’ve downloaded the latest patches and fixes to a local network resource and want to run scripts on your machines to update them to the latest security releases.

One of the more fun analogies I have come up with for explaining this process is what happens when you finish a cocktail or drink in a pub: **-U** can get a completely different one or the same, as the glass is empty, whereas if you are half done with a drink and are asked if you want more, you’d of course simply **--Freshen** it with the same ingredients.

##### Removing Packages

Removing a package or set of packages consists of using the **-e** or **--erase** option and requires root access. Removal of packages can be even more fraught with dependency problems than installation because a package can be deeply buried in a tree of dependencies over time.

![Images](graphics/key_topic_icon.jpg)

Removing a package without dependencies is easy. To remove the **tarfoo** package, you use the following command:

```
# rpm -e tarfoo
```

There’s usually no output, the package is removed, and the system returns to the prompt.

The trouble begins when you have multiple packages that all have the same short name, such as a kernel. With two versions of the kernel package on a system, querying the database for the package as shown here returns both packages’ long-format names:

```
# rpm -q kernel
5.19.0-39-generic.fcXX.x86_64
4.31.0-13-generic.fcXX.x86_64
```

If you attempt to remove the package by its short name, you get this error:

```
# rpm -e kernel
error: “kernel” specifies multiple packages:
 5.19.0-39-generic.fcXX.x86_64
 4.31.0-13-generic.fcXX.x86_64
```

Instead, use the long name of the package:

```
# rpm -e 5.19.0-39-generic.fcXX
```

You can remove both packages with one command, as shown here:

```
# rpm -e kernel --allmatches
```

No output is returned if all is successful; you just get returned to the prompt. If you don’t want to remove both of the packages, the only choice is to specify the long package name of the package you want to remove.

##### Other Removal Options

At times you need to force the removal of a package or remove one regardless of the broken dependencies that will result. For example, you might fix a broken package by forcibly removing it and reinstalling it to refresh the files and links that were broken. (You should do this on the recommendation of support professionals, not some thread you found on a six-year-old forum!)

![Images](graphics/key_topic_icon.jpg)

To remove a package that has other packages depending on it, use the following command:

```
# rpm -e foobar --nodeps
```

Be careful about removing packages you can’t replace or when you don’t have the original package file to reinstall from. You need to find the original package or rebuild it from source. If you remove a package that other packages depend on, those packages will not be able to run.

The process of removing packages can also leave behind altered or customized configuration files. For example, if you alter a package’s main configuration file and then remove the package, the configuration file is saved with its original name suffixed with **.rpmsave**. This configuration file can be archived for future use or, if the package is to be upgraded with the **-U** option, a complex set of algorithms is used to ensure that the configuration is properly applied.

##### Querying Packages

Querying for package data is only one of the steps that take place when you manage packages, although it has arguably the most options of all the tasks RPM performs.

It’s important that you understand the difference between packages installed on a system (that appear in the RPM database) and packages that exist simply as files on a disk or other resource. The chief difference in the **rpm** command’s usage is the addition of the **-p** option to specify that the package being acted on is a file on disk.

![Images](graphics/key_topic_icon.jpg)

The most basic of all queries is to check to see whether a particular package is installed:

```
# rpm -q cogl
cogl-1.18.2-9.fc21.x86_64
```

Simply by adding a few modifier characters to this query, you can gather a lot of information about any package. For example, [Example 6-6](#ch06.xhtml_exe6_6) shows how to get information on the package.

**Example 6-6**–Querying a Package for Information

```
# rpm -qi tree
Name          : tree
Version      :1.7.0
Release      :15.fcXX
Architecture: x86_64
Install Date: Wed 24 Oct 2018 08:01:29 PM EDT
Group        : Unspecified
Size         :114531
License      : GPLv2+
Signature    : RSA/SHA256, Sun 15 Jul 2018 07:08:52 PM EDT, Key ID
a20aa56b429476b4
Source RPM   : tree-1.7.0-15.fcXX.src.rpm
Build Date   : Sun 15 Jul 2018 10:27:43 AM EDT
Build Host   : buildvm-11.phx2.fedoraproject.org
Relocations :(not relocatable)
Packager     : Fedora Project
Vendor        : Fedora Project
URL           : http://mama.indstate.edu/users/ice/tree/
Bug URL      : https://bugz.fedoraproject.org/tree
Summary      : File system tree viewer
Description :
The tree utility recursively displays the contents of directories in a tree-like
format.  Tree is basically a UNIX port of the DOS tree   utility.
```

To get information about a package’s files, use both the **-q** (query) option and the **-l** (file listing) option, as shown in the following output:

```
# rpm -ql tree
/usr/bin/tree
/usr/lib/.build-id
/usr/lib/.build-id/78
/usr/lib/.build-id/78/0d8723b45ad93065b6912439e4d2355d3c8e3e
/usr/share/doc/tree
/usr/share/doc/tree/LICENSE
/usr/share/doc/tree/README
/usr/share/man/man1/tree.1.gz
```

When you get Linux+ exam questions about listing package files or information, remember the difference between listing the contents of a package in the database and listing the contents of a package on disk:

**rpm -qil *package_name*:** Used for installed packages, with a short or long name specified

**rpm -qilp *package_name*.rpm:** Used for uninstalled packages, with a file specified

In addition, remember that you can specify these options in any order, as long as they are all there. In effect, **rpm -qipl**, **rpm -qlip**, and **rpm -pliq** all work.

To see a revision history or changelog for the package, use the following command:

```
# rpm -q --changelog tree
* Sat Jul 14 2018 Fedora Release Engineering
  <releng@fedoraproject.org> - 1.7.0-15
- Rebuilt for https://fedoraproject.org/wiki/Fedora_29_Mass_
Rebuild

* Fri Feb 23 2018 Florian Weimer <fweimer@redhat.com> - 1.7.0-14
- Use LDFLAGS from redhat-rpm-config
```

This output is similar to the release notes found in most software package source code repositories describing the history of package changes. Mixing the long and short options for the **rpm** command is a method exam writers love to use on the Linux+ exam. If you’ve never used RPM to this level, the questions will get the best of you. Don’t forget that you must use the **-q** and **--changelog** options together; otherwise, you get a syntax error.

Note

Our usual example, the **tree** command, doesn’t have config files, so we’ll use something that does, such as the postfix suite.

![Images](graphics/key_topic_icon.jpg)

To find all the configuration files for a package, you use the query and config options as shown in [Example 6-7](#ch06.xhtml_exe6_7). This output shows only the files marked by the package as configuration files. If you want the whole list of files inside the package, you need to use **rpm -ql**.

**Example 6-7**–Finding a Package’s Configuration Files

```
# rpm -qc postfix
/etc/pam.d/smtp.postfix
/etc/postfix/access
/etc/postfix/canonical
/etc/postfix/generic
/etc/postfix/header_checks
/etc/postfix/main.cf
/etc/postfix/master.cf
/etc/postfix/relocated
/etc/postfix/transport
/etc/postfix/virtual
/etc/sasl2/smtpd.conf
```

To see other capabilities or package dependencies, use the **--requires** or **-R** option (and remember that it’s a package on disk, so use **-p**), as shown in [Example 6-8](#ch06.xhtml_exe6_8).

**Example 6-8**–Querying the Dependencies of a Package File

```
# rpm -qRp tree-1.7.0-16.fcXX.x86_64.rpm
libc.so.6()(64bit)
libc.so.6(GLIBC_2.2.5)(64bit)
libc.so.6(GLIBC_2.3)(64bit)
libc.so.6(GLIBC_2.3.4)(64bit)
libc.so.6(GLIBC_2.4)(64bit)
rpmlib(CompressedFileNames) <= 3.0.4-1
rpmlib(FileDigests) <= 4.6.0-1
rpmlib(PayloadFilesHavePrefix) <= 4.0-1
rpmlib(PayloadIsXz) <= 5.2-1
rtld(GNU_HASH)
```

This method of finding the dependencies tells you which files or packages are needed without requiring you to install the package. You can track the dependencies back to a package, such as to find out which package provides the **libc.so.6** file required by **tree**, as shown here:

```
# rpm -qf /usr/lib64/libc.so.6
glibc-2.28-9.fcXX.x86_64
```

What about the problem of finding the package from which a particular file was installed? For example, if the **/etc/krb.conf** file were somehow damaged, you could find the package it came from with this command:

```
# rpm -qf /etc/krb5.conf
krb5-libs-1.16.1-21.fcXX.x86_64
```

#### Package Management with YUM

![Images](graphics/key_topic_icon.jpg)

[YUM](#ch06.xhtml_key03-a), the Yellowdog Updater, Modified, is a front end to RPM. Just as the **apt-*** series of tools makes working with **dpkg** and remote repositories easier, YUM brings **rpm** and remote repositories together for you and packages them in an interface with far fewer options to remember.

##### Installing Packages

Install a package, such as the R statistical language, with **yum install**, as shown in [Example 6-9](#ch06.xhtml_exe6_9).

**Example 6-9**–Installing a Package from a Remote Repository

```
# yum install R
Last metadata expiration check: 0:16:58 ago on Sun 25 Nov 2018 01:08:46 PM EST.
Dependencies resolved.
=======================================================================
 Package              Arch    Version
Repository
Size
=======================================================================
Installing:
 R                    x86_64 3.5.1-1.fcXX                            fedora
11 k
Installing dependencies:
 java-1.8.0-openjdk          x86_64 1:1.8.0.191.b12-8.fcXX     updates 237 k
 java-1.8.0-openjdk-devel   x86_64 1:1.8.0.191.b12-8.fcXX      updates 9.8 M
 java-1.8.0-openjdk-headless
                                x86_64 1:1.8.0.191.b12-8.fcXX      updates
32 M
 perl-XML-XPath               noarch 1.43-1.fcXX                   updates
83 k
 perl-open                     noarch 1.11-424.fcXX                 updates
26 k
 R-core                        x86_64 3.5.1-1.fcXX                  fedora
55 M
 R-core-devel                 x86_64 3.5.1-1.fcXX                  fedora
89 k
 R-devel                       x86_64 3.5.1-1.fcXX                  fedora
10 k
 R-java                        x86_64 3.5.1-1.fcXX                  fedora
11 k
 R-java-devel                 x86_64 3.5.1-1.fcXX                  fedora
11 k
 annobin                       x86_64 8.23-1.fcXX                    fedora
122 k
 bzip2-devel                 x86_64 1.0.6-28.fcXX                  fedora
215 k
 dwz                           x86_64 0.12-9.fcXX                    fedora
105k
 efi-srpm-macros            noarch 3-3.fcXX                        fedora
21 k
 expat-devel                 x86_64 2.2.6-1.fcXX                    fedora
49 k
 fontconfig-devel          x86_64 2.13.1-1.fcXX                   fedora
127k
 fpc-srpm-macros           noarch 1.1-5.fcXX                       fedora
7.5 k
 freetype-devel            x86_64 2.9.1-2.fcXX                     fedora
441k
 gcc-c++                     x86_64 8.2.1-2.fcXX                    fedora
12 M
Transaction Summary
=======================================================================
Install  312 Packages

Total download size: 312 M
Installed size: 706 M
Is this ok [y/N]: Downloading Packages:
Installed:
  R-3.5.1-1.fcXX.x86_64
  perl-File-ShareDir-1.116-3.fcXX.noarch
  perl-List-MoreUtils-0.428-4.fcXX.noarch
  perl-Params-Util-1.07-25.fcXX.x86_64
  java-1.8.0-openjdk-1:1.8.0.191.b12-8.fcXX.x86_64
  java-1.8.0-openjdk-devel-1:1.8.0.191.b12-8.fcXX.x86_64
  java-1.8.0-openjdk-headless-1:1.8.0.191.b12-8.fcXX.x86_64
  perl-XML-XPath-1.43-1.fcXX.noarch
  perl-open-1.11-424.fcXX.noarch
Complete!
... output omitted ...
```

The output in [Example 6-9](#ch06.xhtml_exe6_9) shows that **yum** calculates the dependencies, downloads all needed packages, and installs them.

Note

The output of the **yum** transactions in Example 2-7 was greatly condensed from its original almost 2,000 lines of returned text. If you are logging these upgrades/updates, keep in mind that the log files can become very large!

Note

**yum** commands typically do not use dashes or double dashes, whereas **rpm** commands do. However, next we introduce some notable exceptions, such as the **-y** option, which effectively supplies the needed answer to an installation question so that automation can occur.

If you want to skip the step where you confirm the installation, simply add **-y**, as in this example:

```
# yum -y install foo
```

It is possible to just download the packages instead of installing them. There are several ways to accomplish this:

• At the **y/d/N** prompt, answer **d** (download) instead of **y** (yes).

• Use **yum install --downloadonly** instead of the plain **yum install**.

• Use **yumdownloader** instead of **yum**.

The **yumdownloader** command behaves similarly to **yum install** except that you have a few more options available to you:

• **source:** Downloads the source RPM instead of binary RPMs

• **urls:** Displays the URLs of the files instead of downloading them

• **resolve:** Modifies the command to also include any missing dependencies

• **destdir:** Specifies the location where the files will be stored

##### Fetching Updates

YUM knows where to get new packages and what’s currently on a system, so it can also calculate which packages are out of date. Upgrading a package requires just **yum update *package_name***, so **yum update tcpdump** updates the **tcpdump** package along with any dependencies.

You can check for any out-of-date packages with **yum check-update** and upgrade the whole system with **yum update** all by itself.

##### Finding Packages to Install

You can search remote repositories in different ways. If you know the name of the package, you can use **yum list**:

```
# yum list tomcat
Last metadata expiration check: 0:08:45 ago on Mon 26 Nov 2018
11:31:19 AM EST.
Available Packages
tomcat.noarch      1:9.0.10-1.fcXX
fedora
```

Packages that can be split into separate components are usually distributed as separate packages sharing a common prefix. Suppose you want to see what components you could add to Tomcat. You could use a wildcard operator with the **yum list** command, as shown in [Example 6-10](#ch06.xhtml_exe6_10).

**Example 6-10**–Listing Packages That Match a Wildcard

```
# yum list tomcat*
Last metadata expiration check: 0:09:01 ago on Mon 26 Nov 2018 11:31:19 AM EST.
Available Packages
tomcat.noarch                          1:9.0.10-1.fcXX           fedora
tomcat-admin-webapps.noarch         1:9.0.10-1.fcXX           fedora
tomcat-docs-webapp.noarch           1:9.0.10-1.fcXX           fedora
tomcat-el-3.0-api.noarch            1:9.0.10-1.fcXX           fedora
tomcat-javadoc.noarch                1:9.0.10-1.fcXX           fedora
tomcat-jsp-2.3-api.noarch           1:9.0.10-1.fcXX           fedora
tomcat-jsvc.noarch                    1:9.0.10-1.fcXX           fedora
tomcat-lib.noarch                     1:9.0.10-1.fcXX           fedora
tomcat-native.x86_64                  1.2.17-2.fcXX             fedora
tomcat-servlet-4.0-api.noarch       1:9.0.10-1.fcXX           fedora
tomcat-taglibs-parent.noarch        3-8.fcXX                   fedora
tomcat-taglibs-standard.noarch      1.2.5-6.fcXX              fedora
tomcat-webapps.noarch                 1:9.0.10-1.fcXX          fedora
tomcatjss.noarch                       7.3.5-1.fcXX             fedora
```

Finally, if you know you need a web server but aren’t sure what to pick, you can use a general search, as shown in [Example 6-11](#ch06.xhtml_exe6_11).

**Example 6-11**–Searching YUM Repositories for Packages That Match a Concept

```
# yum search “web server”
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: repo.miserver.it.umich.edu
 * extras: repo.miserver.it.umich.edu
 * updates: repo.miserver.it.umich.edu
=========================== N/S matched: web server
============================
libcurl.i686 : A library for getting files from web servers
libcurl.x86_64 : A library for getting files from web servers
pcp-pmda-weblog.x86_64 : Performance Co-Pilot (PCP) metrics from web server
logs
python-paste.noarch : Tools for using a Web Server Gateway Interface stack
python-tornado.x86_64 : Scalable, non-blocking web server and tools
xbean.noarch : Java plugin based web server

  Name and summary matches only, use “search all” for everything.
```

#### Configuring YUM

The main configuration file for **yum** is **/etc/yum.conf**. In it are the global options for **yum** and some defaults for all the repositories. You will rarely have to edit this file, but it does contain helpful information if you’re trying to figure out where files are kept. [Example 6-12](#ch06.xhtml_exe6_12) shows a default Fedora configuration.

**Example 6-12**–A Default **yum.conf** Configuration for CentOS

```
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1
gpgcheck=1
plugins=1
installonly_limit=5
bugtracker_url=http://bugs.centos.org/set_project.php?project_id=23&
ref=http://bugs.centos.org/bug_report_page.php?category=yum
distroverpkg=centos-release

#  This is the default, if you make this bigger yum won’t see if the metadata
# is newer on the remote and so you’ll “gain” the bandwidth of not having to
# download the new metadata and “pay” for it by yum not having correct
# information.
#  It is esp. important, to have correct metadata, for distributions like
# Fedora which don’t keep old packages around. If you don’t like this checking
# interupting your command line usage, it’s much better to have something
# manually check the metadata once an hour (yum-updatesd will do this).
# metadata_expire=90m

# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
```

In [Example 6-12](#ch06.xhtml_exe6_12) you can see that all the cached files are stored under **/var/cache/yum**, and the log file is **/var/log/yum.log**. A full list of the options is in the man page for **yum.conf**.

The repository configuration files are stored in **/etc/yum.repos.d**. Each file may contain multiple repositories, but you will find that the repositories are grouped according to function. For example, the main distribution repository is in one file, along with the repository for the source packages and a repository for the debugging symbols. Another file contains the repositories for the updates, the source for the updates, and the debugging symbols for the updates.

A single repository configuration looks like [Example 6-13](#ch06.xhtml_exe6_13).

**Example 6-13**–An Individual Repository’s Configuration from CentOS

```
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client. You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.
#
#

[base]
name=CentOS-$releasever - Base
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$base
arch&repo=os&infra=$infra
#baseurl=http://mirror.centos.org/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
name=CentOS-$releasever - Updates
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$base
arch&repo=updates&infra=$infra
#baseurl=http://mirror.centos.org/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$base
arch&repo=extras&infra=$infra
#baseurl=http://mirror.centos.org/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```

In [Example 6-13](#ch06.xhtml_exe6_13), note that several options start with a dollar sign ($). These are placeholders that are expanded when **yum** is invoked. **$releasever** becomes the distribution version, and **$basearch** becomes the hardware architecture, such as x86_64.

A repository either has a **baseurl**, which is a link to the repository, or a **metalink**, which returns a list of mirrors for the repository. (A mirror spreads the load across many different servers, hosted by different companies.)

An important directive in the configuration is **enabled**. When you run a **yum** command, only the enabled repositories are searched. You can enable a repository in a **yum** command by adding **--enablerepo reponame**.

Hiding repositories is helpful because it gives you access to a wider variety of packages without requiring you to configure the repository. You might, for example, hide the debugging symbol repository unless you actually need debugging symbols, such as when trying to track down crashes. You can also have access to bleeding-edge software when you need it but install more trusted software by default.

#### Dandified YUM

![Images](graphics/key_topic_icon.jpg)

One of the recent additions to the package manager world is the [DNF](#ch06.xhtml_key01-a) ([Dandified YUM](#ch06.xhtml_key02-a)) tool, which debuted with Fedora 18 and is meant to be the next generation of the YUM package manager.

DNF is (mostly) compatible with YUM on the command line and options front, is considered to be a little easier to configure than traditional YUM, and uses fewer system resources in its operation, which can be very important with large updates or package management operations.

Overall, DNF is considered more reliable and consistent than YUM, is based on a later version of Python, and uses a more efficient algorithm than YUM. These reasons, along with concerns about documentation of the YUM API, have made DNF the choice for the future.

#### zypper

The name **zypper** is often used to refer to the [ZYpp](#ch06.xhtml_key07-a) or libzypp package management engine, but **[zypper](#ch06.xhtml_key08-a)** is the command line interface to the engine, not the actual package manager. For the sake of clarity, when we talk about the ZYpp/libzypp package manager overall, we use ZYpp, and when referencing commands and the actual command line tool, we use **zypper**.

ZYpp is used primarily on the openSUSE and SUSE Linux Enterprise product lines; several other distributions, such as Ark and Tizen, also make use of the ZYpp/libzypp package manager scheme.

The vast majority of a user’s interactions with the ZYpp/libzypp scheme are through the **zypper** command, so let’s go over a few very common commands with appropriate options for those.

![Images](graphics/key_topic_icon.jpg)

The **zypper** command is functionally more capable than the **rpm** command, and it functions in many ways similarly to the Debian APT suite of package management tools. It can help you search for packages either in the package database or in repositories (as discussed later in this chapter), perform updates to existing software, and handle many other functions. It’s a companion to graphical utilities such as the YaST software module on the SUSE system.

##### Installing Software Packages with zypper

To list the possible sources of software to install, use the **zypper** list repositories (**zypper lr**) command to produce output similar to that shown in [Figure 6-3](#ch06.xhtml_ch06fig03). This output shows the configured repositories from which you can install software.

![Description: A screen shot of a computer Description automatically generated](graphics/06fig03.jpg)

**Figure 6-3**–**zypper lr** command output

To refresh the metadata from your configured repositories (which is necessary to have the most updated repository information), use the **zypper ref** command. This command returns a list of metadata changes that will then be resident on your system to facilitate interactions with the repository and any installations or updates you choose to perform, as demonstrated in [Figure 6-4](#ch06.xhtml_ch06fig04).

![Images](graphics/06fig04.jpg)

**Figure 6-4**–**zypper ref** command output

To initiate a search for a particular package in your repositories, use the **zypper se vim** command. The returned output will contain any matches on the character string **vim**, which will invariably include the gvim package, which you can see in the list in [Figure 6-5](#ch06.xhtml_ch06fig05).

![Description: A screenshot of a computer Description automatically generated](graphics/06fig05.jpg)

**Figure 6-5**–**zypper se vim** command output

Note

The **zypper** search output shows whether a package that is returned is installed or not; the lowercase **i** in the first column of the output indicates installed.

To install the gvim package on a system, use the **zypper in gvim** command, as demonstrated in [Figure 6-6](#ch06.xhtml_ch06fig06).

![Description: A screenshot of a computer Description automatically generated](graphics/06fig06.jpg)

**Figure 6-6**–Installing the gvim package

The **zypper** command gets the desired package from the repository and lets the user know what will be happening. It usually requires the user to type **y** to agree to both download and install the package and any of its dependencies that **zypper** has identified. Once the user has answered this prompt, the package is downloaded and installed, and the console indicates that this has happened, as demonstrated in [Figure 6-7](#ch06.xhtml_ch06fig07).

![Description: A screenshot of a computer Description automatically generated](graphics/06fig07.jpg)

**Figure 6-7**–Confirming package download and installation

##### Removing a Package with zypper

Once a package is installed, it can easily be removed with the **zypper rm gvim** command.

Once again, a prompt requires a **y** answer to ensure that the package is really supposed to be removed or uninstalled from the system.

##### Managing Repositories

A software repository can take several forms, the most common of which is a network-reachable collection of software (typically RPM package files and accompanying metadata) that is configured as a repository on the machine(s) that wants to have access to its contents.

Repositories can be official and supported, such as the ones that are offered with a subscription of SUSE Linux Enterprise (SLES), official and unsupported, such as the ones that are configured and maintained as a part of the openSUSE project, and third party, such as the very fun and useful Packman repository. Packman is the largest and most diverse collection of additional software available for the openSUSE and SLES distributions; it features multimedia applications, third-party drivers, and much more.

###### Listing the Repositories on a System

Listing the configured repositories on a system is very easy: Use the **zypper lr** command:

```
# zypper lr
```

###### Adding a Repository

To add a repository, you need to first list the repositories and then determine from a web search or another method the repository you want to add. To illustrate, this section shows how to add a non-oss repository to our test system; non-oss means the repository has packages that are not strictly open source software, such as the browser Opera.

To add a repository to the configured set of repositories for a system, the command follows this format:

```
# zypper ar <uri> <alias>
```

The **zypper** command uses the **ar** directive to add a repository, and the network-reachable ***<uri>*** is basically a URL that the system uses for querying and downloading packages and metadata. This is followed by ***<alias>***, which is a friendly name for referring to this repository.

To add the non-oss repository for Leap 15.0 to the system, use this command:

```
# zypper ar
http://download.opensuse.org/distribution/leap/15.0/
repo/non-oss/ Non-OSS
```

The repository is added to the system, and some useful information is shown about the repository, as demonstrated in [Figure 6-8](#ch06.xhtml_ch06fig08).

![Description: A screenshot of a computer Description automatically generated](graphics/06fig08.jpg)

**Figure 6-8**–Adding a repository

###### Refreshing the Repository

To get the latest information about a repository (which you should do for all repositories before querying or installing from them), use the **zypper ref** command, as demonstrated in [Figure 6-9](#ch06.xhtml_ch06fig09).

![Description: A computer screen with a message Description automatically generated](graphics/06fig09.jpg)

**Figure 6-9**–Refreshing the repository

New repositories must be accepted, and the package-signing key must be stored locally; **zypper** takes care of this when you answer **y** for “yes this once” or **a** for “always trust this repository.” It is a good idea to choose **a**, as demonstrated in [Figure 6-10](#ch06.xhtml_ch06fig10).

![Description: A screenshot of a computer Description automatically generated](graphics/06fig10.jpg)

**Figure 6-10**–Accepting new repositories and storing the package signing key locally

As shown in the output in [Figure 6-10](#ch06.xhtml_ch06fig10), the repository has been queried, its information has been downloaded, and it is ready to be used as an installation and update source.

### Sandboxed Applications

To understand this section, you must first be familiar with sandboxing as a concept. To sandbox a piece of software is to make it so that it is executed in a restricted space that is configurable by a developer or administrator, all while minimizing any damage to the host operating system.

![Images](graphics/key_topic_icon.jpg)

#### What is a Sandboxed App?

A further step on this path is application sandboxing, where an application is packaged up so that it can be distributed for a user to run without needing backend system access, operating under very strict controls over what it can read from or has access to on the host operating system.

[Sandboxed](#ch06.xhtml_key09-a) applications typically do not require root access to download and run, have tuneable access to the hosting operating system and typically include any dependencies for their operation.

There are a number of competing implementations of sandboxing, but they all share a similar set of characteristics or goals:

• To be distribution-neutral

• Easy to package up applications

• Ability to include dependencies

• Few or no modifications to the operating system

• No installation needed

• Regular User Permissions

• Simple to run and use

• Portable between distributions

• Ability to restrict access to resources

Depending on which of the application sandboxing schemes you choose, you will get more or less of the above characteristics.

#### App Sandbox Methods

![Images](graphics/key_topic_icon.jpg)

When we talk about sandboxing methods, there are several, but the Linux+ exam focuses on three in specific:

• Flatpak

• AppImage

• Snapd

Let's discuss these in order, so you know what they do, what components are involved and can identify them by characteristics or usage modality, on the exam.

##### Flatpak

Uniquely, [Flatpak](#ch06.xhtml_key11-a) comes from the X Desktop Group (XDG) and so is inspired by different beginnings than the other two, but similar goals, that of having applications that can be packaged up, distributed and run with minimal fuss and permission or access issues, by regular users.

Flatpak uses a repository called Flathub, which lives at [flathub.org](http://flathub.org) and is the most likely place for a user to go to get an application, and so it is also the destination for Flatpak developers to get their applications to be available for those users.

Those using Flatpak applications will need to grant certain permissions so those applications can use the network and audio resources. Flatpak applications can even be updated independently of the distribution they are installed on.

##### AppImage

Initially named klik (as in mouse click?) [AppImage](#ch06.xhtml_key12-a) came to prominence after it was renamed in 2013, and it aspires to being binarily compatible, independent of any one distribution and leaving the underlying host alone, and just being able to be run and used.

AppImage-packed applications are not installed per se, but they are an image that is mounted using the FUSE, (or Filesystem in Userspace) software interface to make it available to be run.

AppImage applications are self-contained, including the libraries needed to have the application run, and running those applications is simple, doesn't change the localhost and shutting them down removes them from the Process Table and unmounts the ISO of the AppImage application.

##### Snapd

Unlike the other two candidates or methods, [Snapd](#ch06.xhtml_key10-a) or Snap (as it's commonly called) is from Canonical, the company closely associated with Ubuntu. Of all of the methods of sandboxing applications we discuss, it's more of an entire ecosystem, having a vendor backing it, and is intended to be a one-stop-shop for applications both for the regular user and for system purposes, though to a lesser degree.

Snap refers to the overall scheme, with snaps being what package applications are called, with snapd being the utility that works to acquire them, run them and perform some management of them.

Also of note is the Snap Store, where Canonical manages the snaps or applications that are submitted and does things like check them for malware and viruses.

Snaps are also somewhat unique in that they can access resources from other snaps, as well as using a concept called "Portals" that allow snaps to have access to configured sets of host-based system resources.

### System Updates

The concepts of updating or upgrading packages has been covered earlier in this chapter, and so we'll concentrate briefly on the more specific concept and practice of updating the Linux Kernel.

#### Updating the Kernel

Why would you want to update your version of the kernel? There are a variety of reasons, some of which are:

• Improvements to Stability

• Security Issues

• Advances in Hardware Drivers

• Efficiency

• New Features

Regardless of the reason to update your kernel, there are a couple of ways it can happen, it all depends on how critical the system is. If the system is a desktop, or a test system, or not a production system, updating it is a good bit simpler, you're not interrupting a bunch of users, or dropping your organization's downtime, you're just rebooting a system after a package upgrade.

But, what if your system is a production server? What if rebooting this server after an update or upgrade will cause a lot of disruption?

These are important questions, and thankfully there is an answer, read on for a discussion of both methods, and why you'd choose one over the t'other matey.

#### Choosing an Update Method

There are a couple of main ways to update the kernel:

• Replacing the kernel entirely (reboot mandatory)

• By patching a running kernel (no reboot involved)

We'll cover both methods, starting with the various ways to update with a reboot involved. We'll then cover the live patch option, also known as a hot patch, either way the kernel is left running and portions of it are replaced, all without dropping the kernel or rebooting.

While the second method helps retain user connections and preserves system uptime, there are situations when a live or hot patch will NOT work, and you are looking at a reboot anyway. The most likely reason to use a live or hot patch is a security update that fixes a zero day exploit or must be applied immediately to fix a known vulnerability.

#### With Reboot Methods

There are a couple of main ways to update the kernel that will require a reboot, starting with a simple package update.

##### Manual Update

At it's most simple, this would be you performing the following steps:

1\. Go to [kernel.org](http://kernel.org) and find the latest version of the stable kernel

2\. Download this package file to your system

3\. Unpack it, and depending on your packaging tool, simply run the install routine for the package

4\. Once the installation is done

5\. Reboot the system and look for any errors

Obviously, this is not the most highly-recommended option, but it's doable, it can result in an updated kernel for your system.

What are the likelihood that a kernel update will require additional packages to be downloaded and installed? Nearly a guarantee, and this method does not make for a fun or efficient experience. Not recommended, and if done, only for those who desperately need more troubleshooting experience, because you are going to get a lot this way.

##### Update with Package Manager

The more likely and much less, well, "adventurous" route is to update your kernel using the package manager on your system, which will have several good factors recommending it, the first is that you'll be following a path that is provided for by the maintainer of your distribution, and that you'll be using a kernel that was packaged and may have customizations to it that will help it fit in with the rest of your distribution.

This is actually a reasonable way to update your kernel, but people often accidentally update the WHOLE DISTRIBUTION by using too generic or wide of a command, as shown in the following.

To get the latest package information from your configured repositories, on a Ubuntu system, use the command:

```
# sudo apt-get update
```

This will refresh all your configured repositories with the latest information. Then you can upgrade your ENTIRE distribution, including the kernel, with the command:

```
# sudo apt-get ugrade
```

However, if all you want to do is update your kernel, you can usually use just the command:

```
# sudo apt-get upgrade linux-image-generic
```

##### Linux Kernel Utilities

The final way I would like you to consider is the Linux Kernel Utilities, a set of 3 scripts that you can use to update your kernel, compile it the way you want it and also to remove old kernels as needed.

The three scripts are:

• compile_linux_kernel.sh

• update_ubuntu_kernel.sh

• remove_old_kernels.sh

Obviously this is to be used on our Ubuntu system. There are multiple methods for many other distributions, in order to anchor the concept, we'll focus on Ubuntu for this purpose.

You can retreive a copy of the linux kernel utilities from Mark Tompkins Github page:

**Step 1.** Open a shell prompt

**Step 2.** Make a test diretory with "mkdir ~/test"

**Step 3.** Pull down the linux kernel utilities with the command:

```
# git clone
https://github.com/mtompkins/linux-kernel-utilities.git
```

**Step 4.** Change into the ~/test/linux-kernel-utilities directory and change the permissions with:

```
# chmod 750 *.sh
```

**Step 5.** Then do a git pull

**Step 6.** Then run the compile script to list out the available kernels

**Step 7.** Install the latest kernel with the command:

```
# ./compile_linux_kernel.sh --latest
```

**Step 8.** Install the updated kernel with the command:

```
# ./update_ubuntu_kernel.sh
```

**Step 9.** Reboot the system

Alternatively, you can use the update script with the --latest option to get a pre-compiled version of the kernel from the Ubuntu kernel repository:

```
# ./update_ubuntu_kernel.sh --latest
```

**Step 10.** Finally, you can remove old versions of the kernel with the remove script:

```
# ./remove_old_kernels.sh
```

This concludes the methods that you should be aware of that require a reboot, of course there are those that are out there that can be used, but it's probably a good idea to stick with whatever your distribution vendor or maintainer recommends, and some of them have some pretty nice utilities, such as UKUU and UKtools, but those are not somethign you'll see on the LInux+ exam.

#### No Reboot Methods

Of course you will want to understand when it's best to just do a full update and reboot, and when it's best to patch that exploit NOW and keep the system rolling along, providing services.

###### Live Kernel Patching Overview

There are live patching scenarios for most major distributions, and each one has it's own take on what the process is and what tools work best, but let's understand what is being done here, before we get into the details.

When you patch a live or running kernel, it's almost always going to be to apply a security fix or update. System downtime can be costly, due to lack of availability, can cause your organization compliance problems, you may have agreements with your customers or be required to maintain a certain mix of uptime and service updates that makes long reboot cycles and service downtime windows unattractive or even costly.

###### Issues with Live Patching

As long as the fixes or updates are relatively minor, live patching makes very good sense. When a kernel's structure, the structure of data or the way processing handled can cause live patching to be anything from a non-optimal choice, to outright impossible.

In other words, if the changes that need to be made to secure or protect the system are widespread or comprehensive, live patching may simply not be possible and you are back to an update and a reboot.

###### The Live Patch Process

Let's concentrate on Ubuntu or Canonical's methodology just to have a process we can follow.

Canonical offers a Livepatch Service which automatically updates the kernel of a system wtih any patches or fixes and doesn't reboot the system.

One of the caveats for this option is that you will need to schedule or remember to keep the system package information updated regularly with the command:

```
# sudo apt-get update
```

You will have to notice when the kernel updates are available and initiate the patching with the command:

```
# sudo apt-get upgrade
```

SUSE has a service called KLP or Kernel Live Patching, which is similar in function to the Canonical offering, but is a bit more integrated. Both require connecting the correct update repositories, and the SUSE version will require you to register the system with the SUSE Customer Center, or you can also use the SUSE Manager system management product to be the intermediary.

To check and see if a live-patch has been installed, use the command:

```
# zypper se --details kernel-livepatch-*
```

The system will show you any installed livepatch packages, and you can make your patching decision from there.

You also can determine patching status or installed patches with the command:

```
# klp -v patches
```

As you can see, there are good reasons to consider livepatching your kernel, but it's not for every situation. Livepatching is like flying a glider, sooner or later you'll have to reach the ground and start over, just like sooner or later your system will need an update that will force a reboot.

### Summary

In this chapter you learned a lot about software packages, package management, using sandboxed applications and how to update your packages and your kernel.

These are great skills to have, you'll need to do some solid studying of the options and additional command features, and most especially in this area, do your lab work! This will be very helpful in the real world, and of course on the exam.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 6-2](#ch06.xhtml_ch06tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 6-2**–Key Topics for [Chapter 6](#ch06.xhtml_ch06)

![Images](graphics/06tab02.jpg)![Images](graphics/06tab02a.jpg)![Images](graphics/06tab02b.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[DNF](#ch06.xhtml_key01)

[Dandified YUM](#ch06.xhtml_key02)

[YUM](#ch06.xhtml_key03)

[APT](#ch06.xhtml_key04)

[RPM](#ch06.xhtml_key05)

[dpkg](#ch06.xhtml_key06)

[rpm ZYpp](#ch06.xhtml_key07)

[zypper](#ch06.xhtml_key08)

[sandboxed](#ch06.xhtml_key09)

[snapd](#ch06.xhtml_key10)

[flatpak](#ch06.xhtml_key11)

[AppImage](#ch06.xhtml_key12)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** You have downloaded what you thought were RPM binary packages but when you install them, you don't get a binary. What have you likely mis-downloaded?

**a.** Source RPMs

**b.** Repositories

**c.** Dependencies

**d.** Libraries

**2.** You wish to install new software via packages, and when you issue the install command, a lengthy pre-install process has to be completed. What best describes that process?

**a.** Binary Integrity Checks

**b.** Application Dependency Listings

**c.** Software Library Amalgamation

**d.** Downloading Repository Updates

**3.** When performing a verification of a package's integrity, how many fields are shown for each checked package?

**a.** 5

**b.** 7

**c.** 9

**d.** 11

**4.** When removing a package, you get an error because there are multiple versions of the same package and you want to remove all of them at once. Which option will do this?

**a.** --allfiles

**b.** --allmatches

**c.** --allsets

**d.** --allpackages

**5.** When running a sandboxed application, which of the following are you most likely to need permissions to access?

**a.** Memory

**b.** Network

**c.** Display

**d.** Keyboard

**6.** You need to be able to attach, via a shell session, to other hosts over a secure and encrypted connection and to log on to the remote system without entering a password every time. Which of the following is a program or utility that directly makes this possible?

**a. ssh-add**

**b. ssh-keygen**

**c. ssh-agent**

**d. .ssh/authorized_keys**

## Chapter 7\. Managing Software Configurations [This content is currently in development.]

**This content is currently in development.**

## II: Security (Obj. 2.1 - 2.5)

## Chapter 8\. Understanding Linux Security Best Practices

This chapter covers the following topics:

• [Managing Public Key Infrastructure Certificates](#ch08.xhtml_ch08lev1sec03)

• [Certificate Use Cases](#ch08.xhtml_ch08lev1sec04)

• [Authentication](#ch08.xhtml_ch08lev1sec05)

• [Linux Hardening](#ch08.xhtml_ch08lev1sec06)

The exam objectives covered in this chapter are as follows:

• **Objective 2.1:** Summarize the purpose and use of security best practices in a Linux environment

Breaking into the realm of security can be daunting for the newcomer, and Linux security is no easy topic to grasp quickly, unless you have a security background and are just picking up Linux skills. This is a very important set of topics for those who are charged with protecting everything from a single Linux web server or file server all the way to huge infrastructures serving millions of customers!

There is a lot to cover in this chapter, starting wtih the concepts involved in Public Key Infrastructure or PKI, moving on into how Certificates will be used.

There's also the whole topic of Authentication, from Tokens all the way through Pluggable Authentication Modules and SSSD, ending up with LDAP and SSO or Single Sign On.

Finally, we'll hit the fascinating subject of Hardening a Linux system, which I sum up for my classes with my own version of that quote from Coco Chanel, "Before you leave the house, look in the mirror and take one thing off.”

As I like to advise students, "Before you leave the server secured, turn off any service you cannot live without."

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 8-1](#ch08.xhtml_ch08tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 8-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/08tab01.jpg)

**Caution**

The goal of -sign-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** You run a whistleblower’s website for those reporting fraud and abuse in a particular industry and are unable to get a central authority to issue you a certificate. Which of the following best describes your certificate authority status?

**a.** Rogue

**b.** Self-signed

**c.** Protected

**d.** Resigned

**2.** Your intern comes to you and asks you what is the difference between SSL and TLS, which of the following is true?

**a.** SSL is part of TLS

**b.** SSL was obsoleted by TLS

**c.** SSL and TLS are competing standards

**d.** TLS is much older than SSL

**3.** You have enabled a service definition rule as a file in the PAM configuration directory and suddenly notice that other authentication service rules are not working or are clearly missing. What is the issue?

**a.** You need to restart the PAM daemon.

**b.** You have obviated the **/etc/pam.conf** file.

**c.** You need to rename the service file so that it ends in **.conf**.

**d.** None of these answers are correct.

**4.** You are ordered to disallow access to the Telnet service on your server for the host snuffypc and to use the TCP wrappers files and utilities to accomplish this. What file would this entry go in to accomplish this task?

**a.** /etc/hosts.deny

**b.** /etc/hosts.block

**c.** /etc/hosts.disallow

**d.** /etc/hosts.stop

### Foundation Topics

### Public Key Infrastructure

Public key infrastructure (PKI) is a complex range of roles, procedures, and methods to provide public key encryption/decryption services, ranging from an email sent between two parties to bank-to-bank transactions to the entirety of all e-commerce activity on the Web.

#### Purpose of Certificates

The main purpose of a PKI setup is to ensure that a given certificate (used to sign and identify an entity) belongs to and identifies who it says it does.

#### Certificate Authentication

![Images](graphics/key_topic_icon.jpg)

To understand PKI, let’s use the open web as an example. If you are going to be doing commerce, accepting payments and handling people’s personal and (hopefully) private information, you can try to convince everyone how trustworthy you are purely through marketing, or you can take the time and trouble necessary to get a certificate from a managing authority and then use that to identify your services as being properly managed and secured. A central certificate management scheme requires you to interact with and trust the centralized authority–something that not every organization will do.

#### Self-Signed Certificates

![Images](graphics/key_topic_icon.jpg)

One of the other methods of using PKI is to be self-signing and develop a web of trust among and with other self-signers and to slowly build a reputation for being trustworthy. This is effectively the PKI version of word-of-mouth marketing or compliance. There are advantages to both scenarios–and downsides as well.

#### Certificate Authorities

A distinct upside to a central [certificate authority](#ch08.xhtml_key06-a) is that once it is verified as trustworthy by a certificate authority, a site or service or company can very quickly be verified by even individual users as being trustable. This would be where you would see the actuality of [self-signed certificates](#ch08.xhtml_key03-a), as your certificate authority is the authority for these!

A distinct downside of a central authority is that if you provide a good or service or have customers that the central authority does not approve of, it might be impossible to secure a certificate and participate in being approved as trustworthy. Then the entity will have to go unsigned or work to create a circle of trust with other like entities.

#### Private Keys

[Private keys](#ch08.xhtml_key02-a) are always paired with public keys in the PKI process. Everyone has a pair of public and private keys, generated by their favorite tool, and while everyone can and should make their public key accessible to all they wish to communicate with, a private key should remain utterly inaccessible to anyone but the owner.

#### Public Keys

The role of [public keys](#ch08.xhtml_key01-a) in this whole experience is that when someone wants to send you a message that is verifiably from her only, she will use your public key and her private key to sign or encrypt that message; then she will deliver it to you.

You can then use the other user’s public key and your private key to decrypt the message, and if you have verified that the other user’s public key is truly her (such as by looking at a certificate authority or finding it publicly posted on her website), then you can be certain the message is from her and not from a third party.

It kind of goes like this:

Say that Rebecca has her public and private keys and wants to encrypt a file to send to Robert. She uses her private key and Robert’s public key to encrypt the file and then sends it to Robert.

Robert either has verified Rebecca’s public key or does so and then uses his private key and her public key to decrypt the message.

It’s the combination of the encrypter’s private and the decrypter’s public key that creates the encrypted file, and only the decrypter’s private key can decrypt the file that was encrypted with the public key.

This is somewhat simplistic, but it is more than is needed for the scope of this book and the Linux+ exam.

#### Encryption and Hashing

![Images](graphics/key_topic_icon.jpg)

The concept and practice of [encryption](#ch08.xhtml_key10-a) just described is a two-way process. There is another method of encrypting something, involving [*hashing*](#ch08.xhtml_key05-a) or using *message digests*, which enables you to effectively run math functions on an object to derive a hash sum. Then, anyone else who runs that same math or hash calculation on the object gets the same number.

Vendors use this method in practice when they post publicly available RPM and DPKG package files that they want users to download and use to patch their systems. If there were no method of verifying that these packages are authentic and have not been altered, applying them would be unwise. The vendor hash sums the packages and posts the sums, and when the user downloads the package, he runs the same hash calculation, and if he gets the same sum as the vendor, he knows the file is unaltered. If he gets a different sum, he should not trust the package and should report the issue to the vendor and re-obtain the package file from the vendor’s source and do the calculation again.

#### Digital Signatures

Another example of the PKI concept is for [digital signatures](#ch08.xhtml_key04-a). PKI can be used to authoritatively sign a document, such as an employment contract or contract for services, while never having the document exist as paper or be physically signed.

A prime example of a digital signatures service is DocuSign, which allows you to upload a document and then invite someone to review and sign that document, entirely electronically, and have complete trust that the signed document will stand up in a court of law as the equivalent of a physically signed document.

### Certificate Use Cases

This section is shorter than it might be, as some of the use cases are covered in the previous topic, such as [Certificate Authentication](#ch08.xhtml_key09-a) and Encryption. We need to cover the differences between SSL and TLS, and why the change-over is important to the security of the public and private Internet.

![Images](graphics/key_topic_icon.jpg)

[Secure Sockets Layer (SSL)](#ch08.xhtml_key07-a) and [Transport Layer Security (TLS)](#ch08.xhtml_key08-a) are the technologies behind Hypertext Transfer Protocol Secure (HTTPS). HTTPS allows web clients and servers to connect in a secure manner. On a web server in which sensitive data is accessed, such as a banking site or an online shopping site, enabling these technologies is critical. Information-only websites to which users may log in also should have these technologies enabled to secure user account data. These technologies are also used to ensure that the web client is accessing the correct web server rather than some rogue web server masquerading as the real website.

Secure Sockets Layer (SSL) used to be alone in the field of securing web transactions, but Transport Layer Security (TLS) now encompasses SSL. Originally developed as a security protocol to allow browsers and servers to securely pass information to and from each other, this security layer is now considered essential for proper network citizens on the public Internet. One of the hallmarks of SSL encryption in a browser session is the telltale padlock icon to the left of the URL in the address, which appears when a session is properly established.

### Authentication

Linux has come far from the days of just using the local **/etc/passwd** or user database file, and a key reason for this is the concept of pluggable or swappable authentication choices, many of which we will cover here, particularly those on the Linux+ Exam.

#### Multifactor Authentication

![Images](graphics/key_topic_icon.jpg)

With [multifactor authentication (MFA),](#ch08.xhtml_key12-a) a user must provide multiple bits of evidence to prove her identity. One common multifactor authentication method is called two-factor authentication, or 2FA. For this method, the user is required to provide two forms of identification, which could include the following:

• Something the user knows

• Something the user has

• Something that the user is

Another common multifactor method is two-step authentication. This requires the user to perform a primary authentication, such as providing a username and password, and then provide additional information from another source, such as an authentication token.

This section covers various topics related to multifactor authentication.

##### Tokens

A [*token*](#ch08.xhtml_key11-a) is a unique value (typically either a number or an alphanumeric value) that is generated by either a hardware device or a software program. Tokens are typically automatically generated on an ongoing basis and normally are valid for only short periods of time, such as 30 seconds.

###### Hardware Tokens

A hardware token is a token that is generated by a hardware device. Typically it is a very small device, such as a key fob. A hardware token may have additional authentication methods, such as a fingerprint scanner, but this tends to be somewhat rare.

###### Software Tokens

A software token is a token that is generated by a program. A common example is an app on a mobile device.

##### OTP

One-time password (OTP) is an authentication technique that is often incorporated in two-factor authentication. It is also a technique that can be used in the event that a user has lost or forgotten his password.

##### Biometrics

Biometrics takes advantage of the “something that the person is” component of multifactor authentication. Fingerprint scanning, iris scanning, and identification based on other biological data can be used to verify a user’s identity.

##### RADIUS

Remote Authentication Dial-In Service (RADIUS) is a protocol that allows a client system to make use of a server to authenticate users. This service provides AAA (authentication, authorization, and accounting) management in a centralized location.

RADIUS is often compared to TACACS+, but knowing the differences between these protocols is beyond the scope of the Linux+ exam. It is most important that you realize that RADIUS can provide very powerful functions in a security policy because it centralizes the AAA management. Also, you should realize that RADIUS is more vendor agnostic than TACACS+.

##### TACACS+

Terminal Access Controller Access-Control System Plus (TACACS+) is a protocol that allows a client system to make use of a server to authenticate users. This service provides AAA (authentication, authorization, and accounting) management in a centralized location.

TACACS+ is often compared to RADIUS, but, as mentioned in the preceding section, knowing the differences between these protocols is beyond the scope of the Linux+ exam. It is most important that you realize that TACACS+ can provide very powerful functions in a security policy because it centralizes the AAA management. Also, you should realize that TACACS+ was developed by Cisco and is not as vendor agnostic as RADIUS.

#### LDAP

![Images](graphics/key_topic_icon.jpg)

[Lightweight Directory Access Protocol (LDAP)](#ch08.xhtml_key15-a) is a protocol that provides directory services information. LDAP can be used to provide user account information, but it does not provide the full AAA functionality that RADIUS and TACACS+ provide. LDAP is also often used to store other information not directly related to user accounts, such as hostnames.

LDAP can be used to authenticate users, but when considering a security policy, you should realize that RADIUS and TACACS+ provide more robust solutions. For example, LDAP does not provide the accounting part of AAA that protocols like RADIUS and TACACS+ provide.

#### Pluggable Authentication Modules (PAMs)

Linux has come far from the days of just using the local **/etc/passwd** or user database file, and a key reason for this is the concept of [pluggable authentication modules](#ch08.xhtml_key13-a), otherwise known as PAMs.

PAMs, which are used by a large superset of Unix/Linux systems for authentication, ensure that an overall common scheme or method is used by any number of applications, services, and so on. The alternative would be for every application or service to have its own method of authenticating.

PAMs are pluggable, meaning that the sysadmin or even the developer of a distribution can decide which methods are used and when, and that person can add mechanisms without necessarily replacing all authentication backend services for existing services and applications.

PAM doesn’t work alone; it takes PAM-aware applications and services to work properly, and thanks to the very well-designed and implemented application programming interface (API), application programmers can insert minimal code into their applications to take advantage of the services of PAMs on a system.

##### Password Policies

By default, Linux requires a minimum password length of six characters, which is laughably simple in today’s world of high computing power and compute clusters. It could take many years to brute force crack a six-character password manually, but with a reasonable bot group or a supercomputer, it would take about four or five hours.

The password and other authentication-specific files that affect (and, well, effect!) authentication policy are the **/etc/pam.conf** file and the **/etc/pam.d** directory. This section focuses on DPKG/Debian system examples, which can be easily translated to RPM systems with a quick Google search.

![Images](graphics/key_topic_icon.jpg)

PAM uses the **/etc/pam.conf** configuration file by default, and the configuration of services is being laid out in lines or rules that follow this format:

```
service  type  control  module-path  module-arguments
```

The PAM configuration rules fields are as follows:

• ***service*:** The name of the application or service being affected, such as **su** or **login**.

• ***type*:** Made up of **account**, **auth**, **password**, and **session** options, the types separate and control the different types of requirements for the user to access a service. For example, the **auth** type establishes that the user is who she appears to be with a password prompt and handles group and other privileges being granted.

• ***control*:** This item governs what happens if a module can’t successfully establish authentication. Configuration happens in **key:value** sets in brackets. Options include **required**, which denies access if authentication fails; **requisite**, which defers access back to the overall application; **sufficient**, which can fail while allowing authentication to still occur; and **optional**, which doesn’t negatively affect authentication if it fails.

PAMs can additionally use service configuration files located in the **/etc/pam.d** directory, with each file being the configuration for a given service. In this case, the service name is the (all-lowercase) name of the file.

##### Password Length

An example of a PAM rule would be a rule that governs password length. Setting a 10-character password length requirement on a Linux system is as easy as editing the **/etc/pam.d/common-password** file and editing the following line:

```
password [success=2 default=ignore] pam_unix.so obscure sha512
```

so that it reads:

```
password [success=2 default=ignore] pam_unix.so obscure sha512
minlen=10
```

Pay special attention to the spacing and make sure to duplicate this line exactly, or it may error out.

#### LDAP Integration

In order to set up LDAP integration with PAM, there must be an LDAP server configured and available, and the **pam_user_map** module must be installed and available in the authentication server’s PAM configuration.

The upshot of the integration is that you will be configuring LDAP authentication and then making a choice of whether to allow authentication for users on this system to occur solely via LDAP sources or to allow *either* local or LDAP authentication.

This is a complex subject, and while it’s a worthwhile field of endeavor to pursue, it is beyond the scope of this book and the Linux+ exam.

#### User Lockouts

Another important feature of PAM is the ability to configure user or password lockout policy, essentially being able to stop brute-force password guessing by making the system stop allowing subsequent password tries until a timeout period has been met.

An example of setting a 10-minute timeout would entail editing the **/etc/pam.d/system-auth** file by adding the following text to the **auth** line:

```
auth required pam_tally2.so deny=3 unlock_time=600
```

This requires a 10-minute timeout to occur after three unsuccessful password attempts by the same user. Such a measure will significantly slow down any brute force system cracking attempts.

#### The **/etc/pam.d** Directory

For simpler systems, the **/etc/pam.conf** file should be sufficient for the configuration of PAM, but on more complex systems with many different services and more complex configurations, the **/etc/pam.d** directory is another choice.

![Images](graphics/key_topic_icon.jpg)

Use of the **/etc/pam.d** directory or the presence of service files in that directory will cause a PAM to skip the use of the **/etc/pam.conf** file, so be very aware that even a *single* service file in **/etc/pam.d** will obviate any configuration in the **pam.conf** file.

The **/etc/pam.d** directory contains files that follow the general format of the lines in the **/etc/pam.conf** file, also called *rules*. The main difference is that whereas the **/etc/pam.conf** file has a line that begins with **service**, in the **/etc/pam.d** directory the name of the service rule file is the name of the service, and each of the files configures just that service.

Another great feature of a PAM is that it allows for the stacking or layering of configuration rules, and the failure of any of the stacked rules causes the authentication to fail, which safeguards the system.

#### pam_tally2 and faillock

One of the workhorses of a PAM system is the **pam_tally2** module, which comes as a separate module or a shared object (**.so**) and is designed to ensure that brute force attacks fail so the system remains secure. This module is designed to count the number of attempts to gain access, refer to any timeouts configured, ensure that those timeouts are followed, and upon successful access, reset any failed attempt counters.

An important note about lockouts is that the root user is typically not configured to access the system through remote means, such as SSH, so in the default lockout configuration, the root user is *not* affected, as this would mean a root user who fumbles the login too many times would effectively be locked out of the system from the console–not a good thing!

The companion utility to this process is the **faillock** command, which allows the system operator to query, display, and make needed changes to the failed attempts that the **pam_faillock.so** module keeps in per-user listings in the tally directory structure.

For example, you might query a user named snuffyg’s record of failed logging attempts with this command:

```
$ faillock -user snuffyg
```

If the user has too many failed login attempts and is currently in timeout, you can reset the user’s failed login attempts back to zero and give the user a new start with the followin

#### SSSD

[SSSD or the System Security Services Daemon](#ch08.xhtml_key14-a) is an extension to the PAM or Pluggable Authentication Modules that allows and provides access to multiple possible authentication sources in a concentrated and purposeful manner.

SSSD is often used to allow for users to access one resource via a given authentication method, and another via a configured up disparate authentication method.

An example of this might be the local usage of authentication for a user of the system, while using a configured Active Directory remote authentication source for those systems or resources that require that authentication source.

SSSD is effectively a broker or one-stop shop that when configured for multiple sources, will allow for relatively seamless authentication and access to the various resource.

Attributes that SSSD is well-known for, (and you might have to identify on the exam!) include:

Single source for Authentication Stores: SSSD helps decrease performance issues from multiple authentication sources while increasing the possible available sources through a common framework.

Online and Offline Authentication Options: The option to locally cache an authentication token or proof while offline, and then use that token or information to negotiate and updated token is a seriously helpful option for those with a lot of remote users.

Smoother Kerberos and SSO: Those using Kerberos for Single Sign On will have an easier time through the use of the Offline caching configuration option.

[Figure 8-1](#ch08.xhtml_ch08fig01) shows the author's concept of how SSSD works, which we'll explain briefly as well.

![Images](graphics/key_topic_icon.jpg)![Images](graphics/08fig01.jpg)

**Figure 8-1**–SSSD Overview

In [Figure 8-1](#ch08.xhtml_ch08fig01), you'll see that the requesters or client processes such as ssh and passwd will be configured to make their respective requests to a Responder, one for each method. Those Responders will interact with the SSSD Monitor, configured by the /etc/sssd/sssd.conf and it's associated include directory and backed up by the SSSD Cache, which will help with authentication via Kerberos and Single Sign On when the system is offline from the backend authentication providers. Those backend authentication providers are serviced in turn by the appropriate plugin via the sssd_be or Backend Provider, which in turn takes the authentication request and matches it up with the appropriate source and brokers the request and response.

In short, the client process makes it's usual request, and the SSSD process and it's helpers make it happen, online or offline, in most cases.

#### Single Sign-On (SSO)

![Images](graphics/key_topic_icon.jpg)

[SSO or Single Sign-On](#ch08.xhtml_key16-a) is how you permit a user to sign-in or authenticate into not just a single system, or service, but an environment of multiple connected and possibly synchronized data services.

At it's simplest, SSO works by having an agent in an application that will request and store the user's authentication details, and act on that user's behalf as they work their way to various configured services in the environment.

There are multiple possible SSO providers, with more coming on the market all the time.

Some of those providers are:

• Microsoft

• OAuth

• OpenID

• MiniOrange

• Auth0

• Okta

• Ping

Single Sign-On is essential for today's Saas (Software as a Service) environments where not just one service is provided, but services are a combination or amalgamation of several to many services that are combined to give an integrated and comprehensive overall service to the users.

### Linux Hardening

Hardening a Linux system is a multi-layered scenario, there is no one single thing that you can do to completely secure a Linux system from attack other than unplug it or remove the battery and make it impossible to power on...

One of the activities you can undertake is to scan your systems for vulnerabilities, using tools such as the **nmap** command nc or netcat. There are others, many in fact, but the concepts are the most important item we can convey to you, so lets talk about how to probe and get information on your systems.

#### The **nmap** Command

The **nmap** command is used to probe a remote system to determine which network ports are reachable from the local system. This is useful for many reasons, including

• Determining what services are available on the remote system

• Testing security features on the remote system, such as TCP wrappers

• If the **nmap** command is executed from a remote network, verifying the effectiveness of the network’s firewall

Note

The **nmap** command is considered a port scanning tool. Scanning ports on systems that you don’t have written authorization to scan can land you in trouble as port scanning can be considered a hacking technique.

To use the **nmap** command, provide either the IP address or hostname of the system that you want to scan. For example, [Example 8-1](#ch08.xhtml_exe8_1) shows the output of a scan performed on a router.

**Example 8-1**–The **nmap** Command

```
# nmap 192.168.1.1
Starting Nmap 7.8 ( http://nmap.org ) at 2022-1-31 23:22 PDT
Nmap scan report for 192.168.1.1
Host is up (2.9s latency).
Not shown: 987 closed ports
PORT     STATE SERVICE
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
110/tcp  open  pop3
119/tcp  open  nntp
143/tcp  open  imap
465/tcp  open  smtps
563/tcp  open  snews
587/tcp  open  submission
993/tcp  open  imaps
995/tcp  open  pop3s
5000/tcp open  upnp
Nmap done: 1 IP address (1 host up) scanned in 4.89 seconds
```

The lines that describe the open ports start with the port number/protocol (for example, 23/tcp) and end with the corresponding service (for example, telnet).

By default, only Transmission Control Protocol (TCP) ports are scanned. To scan User Datagram Protocol (UDP) ports, use the **-sU** option combination, as demonstrated in [Example 8-2](#ch08.xhtml_exe8_2).

**Example 8-2**–Scanning UDP Ports

```
# nmap -sU 192.168.1.1
Starting Nmap 5.51 ( http://nmap.org ) at 2022-1-31 23:36 PDT
Nmap scan report for 192.168.1.1
Host is up (0.0011s latency).
Not shown: 999 open|filtered ports
PORT   STATE SERVICE
53/udp open  domain
Nmap done: 1 IP address (1 host up) scanned in 4.09 seconds
```

By default, only certain common ports (about 2,000 of them) are scanned. To scan all ports, use the command shown in [Example 8-3](#ch08.xhtml_exe8_3) (and then take a coffee break because it could take a while to run).

**Example 8-3**–Scanning All Ports

```
# nmap -p 1-65535 192.168.1.1
Starting Nmap 5.51 ( http://nmap.org ) at 2022-1-01 00:26 PDT
Nmap scan report for 192.168.1.1
Host is up (1.0s latency).
Not shown: 65521 closed ports
PORT     STATE SERVICE
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
110/tcp  open  pop3
119/tcp  open  nntp
143/tcp  open  imap
465/tcp  open  smtps
563/tcp  open  snews
587/tcp  open  submission
993/tcp  open  imaps
995/tcp  open  pop3s
1780/tcp open  unknown
5000/tcp open  upnp
Nmap done: 1 IP address (1 host up) scanned in 5731.44 seconds
```

Typically a port has an associated local service. The **nmap** command can also probe these services to determine what version of the service is available. This feature isn’t available for all services, but for those that it is available for, it can provide useful information. Use the **-sV** option combination to see service version information, as shown in [Example 8-4](#ch08.xhtml_exe8_4).

**Example 8-4**–Scanning Service Version Information

```
# nmap -sV 192.168.1.1
Starting Nmap 7.8( http://nmap.org ) at 2022-1-01 09:41 PST
Nmap scan report for 192.168.1.1
Host is up (1.0s latency).
Not shown: 987 closed ports
PORT     STATE SERVICE     VERSION
23/tcp   open  telnet?
25/tcp   open  smtp?
53/tcp   open  domain      dnsmasq 2.15-OpenDNS-1
###Remaining output omitted
```

Say that you discover a machine with IP address 192.168.1.11 on your network, but you don’t even know what sort of system it is. One of the benefits of the **nmap** command is that it might provide a clue as to what sort of system this is by probing it. For example, executing the **nmap** command on that IP address can provide you with an idea of what sort of system a machine is, as demonstrated in [Example 8-5](#ch08.xhtml_exe8_5).

**Example 8-5**–Probing a Machine

```
# nmap -sU 192.168.1.11
Starting Nmap 7.8 ( http://nmap.org ) at 2022-1-31 23:38 PDT
Nmap scan report for 192.168.1.11
Host is up (0.00045s latency).
Not shown: 992 filtered ports
PORT     STATE          SERVICE
67/udp   open|filtered dhcps
137/udp  open           netbios-ns
138/udp  open|filtered netbios-dgm
443/udp  open|filtered https
1900/udp open|filtered upnp
4500/udp open|filtered nat-t-ike
5353/udp open|filtered zeroconf
5355/udp open|filtered llmnr
Nmap done: 1 IP address (1 host up) scanned in 52.23 seconds
```

Given that **netbios-ns** and some of the other services listed in this output are Microsoft Windows–based services, it is likely that Windows is the operating system of this unknown system.

In some cases, you might be able to use the **-O** option to determine the operating system type, but it isn’t always successful, as demonstrated in [Example 8-6](#ch08.xhtml_exe8_6).

**Example 8-6**–Attempting to Determine the Operating System Type

```
# nmap -O 192.168.1.11
###Output omitted
Aggressive OS guesses: QEMU user mode network gateway (91%),
  Bay Networks BayStack 450 switch (software version 3.1.0.22) (85%),
  Bay Networks BayStack 450 switch (software version 4.2.0.16) (85%),
  Cabletron ELS100-24TXM Switch or Icom IC-7800 radio transceiver (85%),
  Cisco Catalyst 1900 switch or RAD IPMUX-1 TDM-over-IP
  multiplexer (85%), Sanyo PLC-XU88 digital video projector (85%),
  3Com SuperStack 3 Switch 4300, Dell PowerEdge 2650 remote access
  controller, Samsung ML-2571N or 6555N printer, or Xerox Phaser 3125N
  printer (85%), Dell 1815dn printer (85%)
No exact OS matches for host (test conditions non-ideal).
OS detection performed. Please report any incorrect results at
http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.37 seconds
```

So, how did you discover that 192.168.1.11 machine in the first place? Another useful feature of the **nmap** command is its capability to scan an entire network to determine which IP addresses are in use. To perform this operation, use the **-sP** option combination, as demonstrated in [Example 8-7](#ch08.xhtml_exe8_7).

**Example 8-7**–Probing a Network

```
# nmap -sP 192.168.1.0/24
Starting Nmap 7.8 ( http://nmap.org ) at 2022-1-31 23:51 PDT
Nmap scan report for 192.168.1.0
Host is up (0.00043s latency).
Nmap scan report for 192.168.1.1
Host is up (0.0026s latency).
Nmap scan report for 192.168.1.2
Host is up (0.70s latency).
Nmap scan report for 192.168.1.3
Host is up (0.045s latency).
Nmap scan report for 192.168.1.4
Host is up (0.043s latency).
Nmap scan report for 192.168.1.7
Host is up (0.00011s latency).
Nmap scan report for 192.168.1.11
Host is up (0.0020s latency).
Nmap scan report for 192.168.1.12
Host is up (0.00013s latency).
Nmap scan report for 192.168.1.14
Host is up (3.7s latency).
Nmap scan report for 192.168.1.16
Host is up (0.00088s latency).
```

You can even see information about your own system, including a list of network interfaces and the routing table, by using the **--iflist** option, as shown in [Example 8-8](#ch08.xhtml_exe8_8).

**Example 8-8**–Listing Network Interfaces

```
# nmap --iflist

Starting Nmap 7.8 ( http://nmap.org ) at 2022-1-01 09:39 PST
************************INTERFACES************************
DEV  (SHORT) IP/MASK      TYPE     UP MTU   MAC
lo   (lo)    127.0.0.1/8  loopback up 65536
eth0 (eth0)  10.0.2.15/24 ethernet up 1500  08:00:27:E0:E2:DE

**************************ROUTES**************************
DST/MASK    DEV  GATEWAY
10.0.2.0/24 eth0
0.0.0.0/0   eth0 10.0.2.2
```

#### The nc Command

The man page of the **nc** command (also referred to as the **netcat** command) provides an excellent summary of the **nc** command:

The nc (or netcat) utility is used for just about anything under the sun involving TCP or UDP. It can open TCP connections, send UDP packets, listen on arbitrary TCP and UDP ports, do port scanning, and deal with both IPv4 and IPv6\. Unlike telnet(1), nc scripts nicely and separates error messages onto standard error instead of sending them to standard output, as telnet(1) does with some.

There are quite a few uses for the **nc** command. For example, suppose you want to know whether a specific port is being blocked by your company firewall before you bring online a service that makes use of this port. On the internal server, you can have the **nc** command listen for connections on that port:

```
# nc -l 3333
```

You should end up with a blank line below the **nc** command. Next, on a remote system outside your network, you could run the following **nc** command to connect (replacing *server* with the resolvable hostname or IP address of the local system):

```
# nc server 3333
```

If the connection is established, you see a blank line under the **nc** command line. If you type something on this blank line and press the **Enter** key, then what you typed appears below the **nc** command on the server. Actually, the communications works both ways: What you type on the server below the **nc** command appears on the client as well.

The following are some useful options to the **nc** command:

• **-w:** This option is used on the client side to close a connection automatically after a timeout value is reached. For example, **nc -w 30 server 333** closes the connection 30 seconds after it is established.

• **-6:** Use this option to enable IPv6 connections.

• **-k:** Use this option to keep the server process active, even after the client disconnects. The default behavior is to stop the server process when the client disconnects.

• **-u:** Use this option to use UDP connections rather than TCP connections (the default). This is important for correctly testing firewall configurations as a TCP port might be blocked, while the UDP port might not be blocked.

You can also use the **nc** command to display open ports, similar to the way you use the **netstat** command:

```
# nc -z localhost 1000-4000
Connection to localhost 3260 port [tcp/iscsi-target]
succeeded!
Connection to localhost 3333 port [tcp/dec-notes] succeeded!
```

The **-z** option can also be used for port scanning on a remote host.

Note

There is one feature of the **nc** command that I don’t expect you will see on the exam; however, it is a useful technique for transferring all sorts of data. Assuming that the transfer is from the client to the server, on the server, you use the following format:

```
nc -l 3333 | cmd
```

And on the client, you use this format:

```
cmd | nc server 3333
```

For example, you can transfer an entire **/home** directory structure from the client to the server by using the **tar** command by first executing the following on the server:

```
nc -l 333 | tar xvf -
```

Then on the client, you execute the following command:

```
tar cvf - /home | nc server 333
```

The client merges the contents of the **/home** directory structure into a tar ball. The **-** tells the **tar** command to send this output to standard output. The data is sent to the server via the client’s **nc** command, and then the server’s **nc** command sends this data to the **tar** command. As a result, the **/home** directory from the client is copied into the current directory of the server.

This is just one technique of many for using this powerful feature of the **nc** command.

#### Secure Boot and UEFI

The problem child for most Linux installations these days is the United Extensible Firmware Interface (UEFI). The portion of the UEFI that makes installation so much more difficult for Linux distributions is called Secure Boot. Secure Boot is ostensibly designed to make it as hard as possible for bad folks to corrupt, change out, or alter your boot manager image and thereby gain inappropriate access to your computer.

In reality, because initially all UEFI Secure Boot images had to be signed by an official signing authority, and the only authority was Microsoft, installing Linux was made much more difficult, requiring distribution maintainers to either go to Microsoft to get a boot image signed off on or create their own completely alternative signing authority and get that approved through the UEFI process.

The best solution, and one that still currently works, is to simply turn off UEFI Secure Boot in the preboot system configuration and avoid the whole issue from the beginning. To be very clear, you only need to disable the Secure Boot portion of the UEFI process, and there are great reasons to continue to use UEFI. On the whole, it’s a definite improvement over the master boot record (MBR) method.

![Images](graphics/key_topic_icon.jpg)

The **/boot/efi** directory is not always present in every distribution, but if it’s there, typically it’s used when you must dual-boot a system, as the UEFI system wants a UEFI partition to be available.

#### System Logging Configurations

We have already covered in some detail the system logging scenario, it's in [Chapter 7](#ch07.xhtml_ch07), “[Managing Software Configurations.](#ch07.xhtml_ch07)”

#### Using umask

If your system is a typical Linux system, a value is set in either the **/etc/bashrc** file or the **~/.bashrc** file that governs the default permissions of any created object. This value is known as the *umask*, and this single value is used to determine default permissions for both directories and files. The umask applies only when you create a new file or directory.

The maximum default permissions for directories and files are different, which means the *umask* value results in different default permissions for files than it does for directories. The default permissions with no umask value set are:

• **For files:** rw-rw-rw- (or 666)

• **For directories:** rwxrwxrwx (or 777)

![Images](graphics/key_topic_icon.jpg)

View the umask for your current shell by executing the following command:

```
# umask
0022
```

This just means that of the four possible positions to mask out (special permissions, user owner permissions, group owner permissions, and other permissions), the last two have the write permission masked out or not used. Note that the first position never has any effect because the special permissions are never set by default. As a result, the umask value of 0022 is really the same as 022.

If you create a file when the umask is set to 022, the file’s permissions are as follows:

```
-rw-r--r-- 1 root root 881 Feb 17 09:11 file1
```

If you create a directory with the same umask set, the directory’s permissions are as follows:

```
drwxr-xr-x 2 root root 4096 Feb 17 14:47 dir1
```

To understand why these permission sets are different, think about the process of how the umask is applied. To begin with, recall the default permissions:

![Images](graphics/untab08-01.jpg)

Now, consider a umask value of 022\. This means you are “masking out,” or removing, the write permissions for the group owner and others (represented by the M values here):

![Images](graphics/untab08-02.jpg)

When those permissions are masked out, you end up getting the following permissions on new files and directories:

![Images](graphics/untab08-03.jpg)

As you can see, the umask value changes the default permissions of a created object based on the following formula:

```
Maximum default value - umask value = create value
```

You can change the umask value to a more restrictive one with the **umask 027** command.

Now, you can create another file, and the permissions should be

```
-rw-r----- 1 root root 881 Feb 17 09:22 file2
```

Create another directory with the umask value 027, and the permissions should be

```
drwxr-x--- 2 root root 4096 Feb 17 14:48 dir2
```

Notice in the previous example that the umask has a value greater than the default value of the file being created. The umask values go from 000 to 777 because a directory object has a maximum default value of 777; however, a file has a maximum default value of 666\. The umask value must encompass both sets of possible values, so if you have a 7 in a umask value, it affects the file default permission as if it were a 6. In other words, in this case 6 – 7 = 0.

Expect to see the umask value on the Linux+ exam. For example, you might see a question that provides a file permission listing and asks you to provide the umask value that resulted in those permissions. To become familiar with how umask values work, try different scenarios to determine what the result would be. Use the following chart and plug in different values for your umask value for practice:

![Images](graphics/untab08-04.jpg)

Finally, it is important to note that while all of your shells initially have the same umask value, you can change this value in one shell without affecting the umask values in other shells. Recall that this value is initially set via an initialization file (typically either **/etc/bashrc** or **~/.bashrc**).

#### Disabling/Removing Insecure Services

We have covered how to disable and or mask, as well as remove services in [Chapter 4](#ch04.xhtml_ch04), “[Managing Processes and Services.](#ch04.xhtml_ch04)”

A quick note about insecure or unsecure services, there are some obvious one, such as Telnet, or FTP, which are NOT secure, and have been replaced by the SSH suite of commands.

You'll have to do your own research in your test or production environment as to what services you will determine are unsecure, and use the knowledge gained here to manage them.

#### Enforcing Password Strength

Password strength is another of those simple phrases that has some complexity underlying it. Passwords are how we keep control of who has access to what on the system, and there are ways that we can make sure they are not only strong, but also a moving target for those who might want to try to brute-force attack a system by guessing passwords.

There are 3 main things I recommend to system managers to ensure their passwords are strong and solid:

• Set initial password options

• Routinely age passwords

• Never use group passwords

##### Setting Password Parameters

![Images](graphics/key_topic_icon.jpg)

Probably the most important file for establishing and maintaining password strength is the **/etc/login.defs** file. It's the configuration file for the Shadow Suite, which is the piece of a Linux system that manages the actual password or **/etc/shadow** file, and contains the settings or rules that anything that works with passwords must follow.

This file has a lot of very important parameters, and it's where you set the ground rules for the type, length, encryption and many other parameters for your system's passwords.

This is a text file, easily read and parsed, and editable with the proper account and permissions.

Important settings include:

• **ENCRYPT_METHOD:** This sets the encryption algorithm for the group passwords, values can be DES, MD5, SHA256 and SHA512\. The PAM or Pluggable Authentication Modules govern user account passwords.

• **FAIL_DELAY:** Very important, this is how long you have to wait before you can attempt another login after a password fails.

• **LOG_OK_LOGINS:** Normally only failed logins are recorded, this setting allows for logging ALL logins, successes and failures.

• **LOGIN_RETRIES:** This sets the maximum number of retries if a bad password is detected, usually 3, but this is also normally governed by PAM.

##### Aging Your Passwords

Users’ passwords need to be changed frequently enough so that attackers don’t have enough time to guess them. Most users want to come to work, get paid, and go home; system security is of much lower importance to them than convenience.

![Images](graphics/key_topic_icon.jpg)

To age passwords properly, use the **chage** command. The syntax for the **chage** command is

```
chage -option value username
```

This command acts on fields in the **/etc/shadow** file and has the following options:

• **-m:** Changes the minimum value, or how long after a password is changed that the user must wait until it can be changed again.

• **-M:** Changes the maximum value, which is the maximum number of days that can go by before the user must change the password.

• **-d:** Changes the last change value, which is the number of days since January 1, 1970, that the password was last changed. This is rarely modified directly; when a password is changed with the **passwd** command, this value is automatically updated.

• **-E:** Changes the expiration value, which is the number of days since January 1, 1970, that represents the day the user’s account will be disabled. The format used is *YYYY-MM-DD*.

• **-I:** Changes the inactive value, or the number of days of inactivity (no logins) after the account has reached the maximum limit before the user account is locked, at which point root attention will be required to reenable the account. Setting this to 0 disables the feature.

• **-W:** Changes the warning value, or the number of days before the user must change her password. This warning is provided only when the user logs in to the system.

Thankfully, you don’t have to memorize these values except to know them for potential Linux+ exam questions. Just execute the **chage username** command as the root user, and the system prompts you interactively for each value that can be configured for the specified user.

Users can use the **-l** option to view their own information, or the root user can view another user’s information with this option:

```
# chage -l snuffy
```

This produces the following output:

```
Minimum: 0
Maximum: 99999
Warning: 7
Inactive: -1
Last Change: Mar 19, 2022
Password Expires: Never
Password Inactive: Never
Account Expires: Never
```

The **passwd** utility includes some of the previous options, such as these:

• **-d:** Disables a user account by removing its password.

• **-n:** Sets the minimum password lifetime, in days.

• **-x:** Sets the maximum password lifetime, in days.

• **-w:** Sets the warning number of days before the password expires.

• **-i:** Sets the number of days an account with an expired password can be inactive before it’s locked.

• **-S:** Shows the user password information, such as what encryption is used and whether a password is set.

##### No Wire Hangers (Group Passwords)

Passwords are usually the domain of individual accounts, but in some cases you might want to have a group password, to allow users to change groups and possibly give themselves access they should not have.

Group passwords are a big security risk, and while in certain non-typical instances may be useful, they will often cause security audits to flag their presence and should normally be avoided.

#### Removing Unused Packages

This is a simple issue, that of not having packages installed that are not necessary to the functioning of your system during it's normal operations.

You may not know if you need a package, and there are ways to find out when a package was last installed or updated, but those are like mining for a needle in a haystack.

It's best to run a listing of all your installed packages and if you don't know what something is, run a package info command on it, those depend on the distribution, but on a RPM system, you might use the command and options shown in [Example 8-9](#ch08.xhtml_exe8_9).

**Example 8-9**–Listing Network Interfaces

```
# rpm -qi vim-enhanced

Name        : vim-enhanced
Epoch       : 2
Version     : 8.2.4485
Release     : 1.fc34
Architecture: x86_64
Install Date: Thu 07 Apr 2022 10:19:16 PM MDT
Group       : Unspecified
Size        : 4438331
License     : Vim and MIT
Signature   : RSA/SHA256, Tue 01 Mar 2022 05:13:56 AM MST, Key ID
1161ae6945719a39
Source RPM  : vim-8.2.4485-1.fc34.src.rpm
Build Date  : Tue 01 Mar 2022 05:00:15 AM MST
Build Host  : buildhw-x86-07.iad2.fedoraproject.org
Packager    : Fedora Project
Vendor      : Fedora Project
URL         : http://www.vim.org/
Bug URL     : https://bugz.fedoraproject.org/vim
Summary     : A version of the VIM editor which includes recent enhancements
Description :
VIM (VIsual editor iMproved) is an updated and improved version of the
vi editor. Vi was the first real screen-based editor for UNIX, and is
still very popular.  VIM improves on vi by adding new features:
multiple windows, multi-level undo, block highlighting and more.  The
vim-enhanced package contains a version of VIM with extra, recently
introduced features like Python and Perl interpreters.
```

As you can see, there is a great deal of information shown about the package, when it was built, installed, etc.

You can also look at the various logs that YUM, Zypper, RPM, APT, etc. use to store the information about what is installed. Those vary by package manager, so look at the man pages for the particular command and search for the keywords such as "installed" etc.

#### Tuning Kernel Parameters

We have covered how to set and tune the kernel's parameters in [Chapter 7](#ch07.xhtml_ch07), “[Managing Software Configurations.](#ch07.xhtml_ch07)”

#### Securing Service Accounts

Remember that a service account is similar to a user account, except that it will not be configured to have someone login as that account, it's used solely for a service to have an account owner for security, and it should never show up as having been logged in as.

![Images](graphics/key_topic_icon.jpg)

I like to show people how to use the **lastlog** command, by default it shows information formatted with the following headers:

```
Username    Port    From    Latest
```

The command shows you an entry for every user or service account that exists in the **/etc/passwd** file, most of which will have not logged in or should never log in, as they are service accounts for managing and owning processes, not user accounts. This is problematic in that you have to sort through a lot of output where the last field, **Latest,** shows the text **“Never logged in”**, and only down at the bottom do you see actual users’ data.

Probably my favorite way to use **grep** (other than to search for swear words in the kernel source code, that is) is to use the **-v** (inverse) option, which shows you everything that does *not* match what you just searched for.

For example, you can use **-v** on the **lastlog** command output to mask out any line of output that contains the string **“Never logged in”**, thereby showing only the users that have logged in:

```
# lastlog | grep -v “Never logged in”
Username    Port    From             Latest
ross          pts/1   192.168.33.144   Wed, Feb 22, 08:20
-0700 2022
ulogin        pts/2   192.168.33.88     Wed, Feb 22, 07:10
-0700 2022
shaggy       pts/3   192.168.33.76     Wed, Feb 22, 05:50
-0700 2022
```

Note that if you run this command and see that a service account, such as **ntp**, **systemd-network**, or **kernoops**, has logged in, you should immediately start investigating why. Service-related accounts are not supposed to be used to log in, so such a login indicates some sort of system hack.

#### Configuring the Host Firewall

You can see the entire set of information about configuring firewalls in [Chapter 10](#ch10.xhtml_ch10), “[Implementing and Configuring Firewalls.](#ch10.xhtml_ch10)”

### Summary

In this chapter you learned about how to apply Linux security best practices to your systems to protect your communications and data, through such technologies as PKI, Certificates, SSL/TLS, Authentication options such as Tokens, PAM, SSSD and SSO.

You also learned how to harden or more tightly secure a Linux system by applying best practices that remove vulnerabilities, unused packages, tighten up password policies and ensure you can find issues that need to be fixed.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 8-2](#ch08.xhtml_ch08tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 8-2**–Key Topics for [Chapter 8](#ch08.xhtml_ch08)

![Images](graphics/08tab02.jpg)![Images](graphics/08tab02a.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[Public Key](#ch08.xhtml_key01)

[Private Key](#ch08.xhtml_key02)

[Self-signed Certificate](#ch08.xhtml_key03)

[Digital Signature](#ch08.xhtml_key04)

[Hashing](#ch08.xhtml_key05)

[Certificate Authorities](#ch08.xhtml_key06)

[Secure Sockets Layer (SSL)](#ch08.xhtml_key07)

[Transport Layer Security (TLS)](#ch08.xhtml_key08)

[Certificate Authentication](#ch08.xhtml_key09)

[Encryption](#ch08.xhtml_key10)

[Tokens](#ch08.xhtml_key11)

[MFA (Multifactor Authentication)](#ch08.xhtml_key12)

[PAM (Pluggable Authentication Modules)](#ch08.xhtml_key13)

[SSSD (System Security Services Daemon)](#ch08.xhtml_key14)

[LDAP (Lightweight Directory Access Protocol)](#ch08.xhtml_key15)

[SSO (Single Sign-on)](#ch08.xhtml_key16)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** Secure Sockets Layer is now encompassed within what suite of Security Protocols?

**a.** Polynomial Security Services

**b.** Security Services Protocols

**c.** Multifactor Token Authentication

**d. Transport Layer Security**

**2.** In Public Key Infrastructure, what does a client or host need from the other system in order to properly encrypt or decrypt data?

**a.** Hashed Key

**b.** Public Key

**c.** Secure Key

**d.** Private Key

**3.** Which command is used to set the effective permissions mask for files and folders on a Linux system?

**a. fmask**

**b. chgmask**

**c. setmask**

**d. umask**

**4.** Besides being controlled by local authorities, what advantage does Self-signed Certificates offer your organization?

**a.** Ease of configuration

**b.** Support Options

**c.** Standards Compliance

**d.** Lesser Costs

**5.** To enforce the use of SSL/TLS on a web server means, which of the following protocols should be used?

**a.** SSH

**b.** SSH

**c.** HTTPS

**d.** gopher

**6.** Which of the following are valid control values for use in the PAM or Pluggable Authentication Modules configuration files? Choose all that apply.

**a.** requisite

**b.** supposed

**c.** efficient

**d.** optional

## Chapter 9\. Implementing Identity Management

This chapter covers the following topics:

• [Account Creation and Deletion](#ch09.xhtml_ch09lev1sec03)

• [Account Management](#ch09.xhtml_ch09lev1sec04)

The exam objectives covered in this chapter are as follows:

**Objective 2.2:** Given a scenario, implement identity management

Accounts and identity are at the heart of a Linux system. No processes can be executed outside of the kernel without being associated or "owned" by an account, be it a service account or user account.

Along with accounts come groups, passwords, all the associated [configuration files](#ch09.xhtml_key11-a) that define accounts and groups, templates for user home directories, user and group management commands and commands that affect the overall environment.

Many of the commands are designed to be use by a root user, but some are also dual-use, where different sets of privileges are available depending on the user running the command.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 9-1](#ch09.xhtml_ch09tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 9-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/09tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** Which **useradd** option can you use to specify the user’s login shell?

**a. -m**

**b. -d**

**c. -k**

**d. -s**

**2.** Which command enables you to change password aging for a user account?

**a. usermod**

**b. chage**

**c. passwd**

**d. gpass**

**3.** You are about to add dozens of users to a given test system and want them all to have a particular set of files in their home directory upon login. Where would you stage these so they were included in a new user’s home directory when the user is created?

**a. /home/newusers**

**b. /etc/default/useradd**

**c. /etc/skel**

**d. /usr/baredir**

**4.** On modern Linux systems, which file stores the user account passwords?

**a. /etc/passwd**

**b. /etc/security**

**c. /etc/shausers**

**d. /etc/shadow**

### Foundation Topics

### Account Creation and Deletion

Note

The author has been working on describing and demonstrating this set of information for about 30 years now, and regardless of what the order of the items are in the Linux+ Objectives, I will be doing this in my own flow and order, which I have found works very well and is very understandable that way. I hope you enjoy my way of doing the topics.

#### User Account Fundamentals

User and group accounts are not known to the kernel by the names humans use and see but by the *user ID* (*UID*) and *group ID* (*GID*) associated with the name. Early versions of the kernel supported two tables of static numbers representing up to 65,536 users and 65,536 groups. Then, the 2.6 kernel made available 4,294,967,296 possible users and groups.

The only associations between the username and the UID are entries in the **[/etc/passwd](#ch09.xhtml_key12-a)** file that defines users. The only associations between the group name and the GID are entries in the **[/etc/group](#ch09.xhtml_key14-a)** file that defines groups.

A user must have a username entry in the **/etc/passwd** file to log in to the system. Users cannot log in using their UID; only the username is accepted.

#### What Accounts Are What?

The **/etc/passwd** file contains a number of system accounts, all of which are assigned UIDs that range from 0 to 499\. Some of the most interesting accounts (which are also most likely to be on the Linux+ exam) are shown here:

![Images](graphics/key_topic_icon.jpg)

• **0:** The root user on the system.

• **1:** The bin user, which is responsible for some system binaries and nonlogin accounts.

• **48:** The apache user; the HTTPD daemon runs as apache.

• **99:** The nobody account, which is used for many things. It is mainly used for anonymous access on FTP and HTTP servers, but it also maps to root accounts that attempt NFS access to shares that have been configured to deny access to the root user.

Note

I normally assign my junior sysadmin and server operator accounts UIDs in the 500–1000 range, just to differentiate them from the other users and to make keeping track of them easier. Users with UIDs in the 500–1000 range don’t automatically gain special privileges. However, these are the accounts that I set up to have extra access by using the **sudo** command.

##### Regular User Accounts

We never say "normal" users, the joke being no user is normal! With that in mind, typical users are assigned UIDs ranging from 500 to 65,000\. This is fine for a single system, but it can cause problems in larger environments.

If you have the need to allow for both local user accounts and network accounts (for using NFS and NIS), it is a good idea to assign network accounts UIDs that start at the five-digit UID mark–in other words, with UIDs from 10,000 to 65,000–and assign local user accounts UIDs from 500 to 9,999\. Such a scheme provides more structure in your UID numbering system.

Note

If you can, force the use of a standardized UID and GID structure across all your enterprise systems. If you have more than 100 users, consider using LDAP for managing how users log on to their systems. The now deprecated NIS and the newer LDAP methods are beyond the scope of this discussion and not on the Linux+ exam objectives, but they provide great ways to centralize account and password management across all machines in an environment.

If you are working on a system that has both network and local accounts, displaying user account information can be tricky. Local user account data is stored in local files, such as the **/etc/passwd** and **[/etc/shadow](#ch09.xhtml_key13-a)** files. Network account information is stored in databases located on a server. One command, **getent**, can be used as follows to search both local and network sources for account information:

```
# getent passwd ross
```

This command searches both local and network sources in an order determined by the **/etc/nsswitch.conf** file:

```
passwd: files nis
shadow: files nis
```

**files nis** means “search local files first and then search the database for the specified value.”

##### User Entries in /etc/passwd

![Images](graphics/key_topic_icon.jpg)

A user’s entry in the **/etc/passwd** file consists of the following:

```
ross:x:500:100:Ross Brunson:/home/ross:/bin/bash
```

The entries in the **/etc/passwd** file are as follows:

• **ross:** The username; this must be eight or fewer characters and should be lowercase.

• **x:** Passwords used to be stored in this file. The **x** value tells the system that the password for this account is now stored in the **/etc/shadow** file. For security reasons, the password should never be in the **/etc/passwd** file on modern Linux systems.

• **500:** The user’s UID.

• **100:** The user’s *primary group*. This group is used as the group owner of all the file objects created by this user account, except in situations where ownership inheritance has been set.

• **Ross Brunson:** This field is a description field (also known as the *GE Common Operating System*, or *GECOS*, for historical purposes). It can be blank or can have a comment or a full name in it.

• **/home/ross:** The home directory field is used to define the complete path to the user’s home directory.

• **/bin/bash:** This field defines the login shell for the user.

Note

The GECOS field is normally just used for simple comments. However, historically it was used to specify more complex data, including useful information like the user’s name, office location, and phone number. This information (and other user information) could be displayed with the **finger** command.

##### Special Login Files

Several files affect the user’s login experience and define when a user can log in and from where. These files are as follows:

• **/bin/false:** If the user’s shell is set to **/bin/false**, the user cannot log in. This is best used for system accounts that should never be logged in to.

• **/sbin/nologin:** When used as a login shell for a user’s account, this program displays a message that the account is unavailable and exits with a nonzero exit code. If the **/etc/nologin.txt** file exists, the contents of that file are shown instead of the standard message.

• **/etc/motd:** After a successful login, the **/etc/motd** file contents are displayed, right before the user’s shell is executed. This is a great place for warning and legal messages to be displayed.

• **.hushlogin:** This file, if created in the user’s home directory, changes the login process so it does not perform a mail check and does not display the last login information or the message of the day to the user.

• **/etc/login.defs:** This file defines the defaults for when users are created using the **useradd** command. These defaults include entries for mail, password complexity and limitations, UID and GID minimum and maximum values, and whether the user’s home directory is created by default.

• **/etc/securetty:** This file specifies from where the root user is allowed to log in. If it does not exist, root can log in from any location.

• **/etc/usertty:** This file is used to set the parameters for login locations, days, times, and systems the user can connect from. The **/etc/usertty** file is used only on systems that don’t have *PAMs* (*pluggable authentication modules*).

Watch for Linux+ exam questions about the files listed here. Questions tend to focus on what happens when a file exists, whether it’s assigned as a login shell, and what shows on a user’s screen when she logs in to the system.

Note

Modern Linux systems utilize a feature called PAMs (pluggable authentication modules). PAMs are a rich collection of modules that give an administrator a great deal of flexibility regarding the manner in which users are granted access to the system. While PAMs are not included in the Linux+ exam objectives, you should consider exploring this useful feature. Start learning about PAMs by executing the command **man pam**.

#### pam_tally2 and faillock

The subject of PAM or Pluggable Authentication Modules is covered in detail in [Chapter 8](#ch08.xhtml_ch08), Understanding Linux Security Best Practices. The pam_tally2 and faillock subject is part of the PAM discussion.

### Group Accounts

![Images](graphics/key_topic_icon.jpg)

A group is a grouping of users. No nesting of groups is possible in Linux or Unix. Users are associated with groups using two methods:

• **Primary:** A GID appears in the **/etc/passwd** file entry in the fourth field; this group is made the group owner of all created objects (files, directories, and so on) for this user. The primary group for a user is special; if a user is assigned a primary group in the **/etc/passwd** file, she does not have to be listed as a member in the **/etc/group** file because the GID in the **/etc/passwd** entry complements the secondary group membership defined in the **/etc/group** file.

• **Secondary:** If a user’s name appears in the **/etc/group** entry for a group, the user is a member of that group, and she gets access to the objects of which that group is the group owner. The last field of each entry of the **/etc/group** file stores the secondary member list.

Groups are assigned numbers, just as user accounts are. The group numbers are called GIDs (group IDs). A few important GIDs:

• **0:** The root group. Anyone who is a member of this group has access to resources restricted to the root account.

• **1:** The bin group, which is similar to the bin user account.

• **100:** The users group, where you can place regular users and then give them access to resources by assigning that group ownership of things that all users should have access to.

Note

On BSD-related systems (recall that BSD is a Unix flavor), a user cannot use the **su** command unless her account is a member of the wheel group, even if she knows the root password. This wheel group feature is not implemented by default on Linux systems, but the group is there for compatibility. Many administrators use the wheel group on Linux to create a sort of “administrator group” and provide special access to commands via the **sudo** command.

A special situation exists primarily on Red Hat–based systems when a user account is created without a specific primary group assigned. In this case, the system creates and assigns a group whose GID should match the number of the user’s UID (although if that GID is not available, the next incremented number available would be used) and whose group name should be the same as the user account name. This type of group is called a *user private group* (*UPG*).

A UPG is a security feature. If you have created a user and haven’t assigned her to a primary group, the system might assign her to the users group as a primary group. This is a security risk because this user might be a contractor or an auditor who should not, by default, have access to the users group’s resources.

However, a UPG can also cause security issues. If a user is the only member of this private group, it is difficult for the user to share file objects with others. Users are forced to share their files with everyone (the others permission set) to be able to share files with one other person.

Debian-based systems don’t use UPGs but rather assign new accounts to the users (100) group by default.

In reality, both of these systems pose security issues. The best solution is to create groups for people who need to share files and place the appropriate users in the correct groups. This approach requires more work for the administrator but leads to better security.

#### Group Entries in /etc/group

The entries in the **/etc/group** file are much simpler and shorter than the ones in the **/etc/passwd** file. A group file consists of the following fields:

```
users:x:100:ross,snuffy
```

The entries in a group file are

• **users:** The name of the group, which should be eight or fewer characters and lowercase.

• **x:** Like user passwords, group passwords are kept in a separate file. The group passwords are in **/etc/gshadow**. (Note that while understanding this file can be useful, it is not a Linux+ exam objective and is not covered further in this book.)

• **GID:** This is the system’s number for this group and is resolved (translated) to the group name for user viewing convenience.

• **ross,snuffy:** Users in the group are listed one after the other, separated with commas (,); no spaces should occur. This list defines secondary group membership.

#### Group Passwords

A user can have only a single primary group; a user who needs to create an object that has to be assigned to another group can use the **chgrp** command. For a single file, this is easy, but if the user wants to create a bunch of files owned by a different group, this technique can be tedious.

Another option is for a user to temporarily change his or her primary group with the **newgrp** command. For example:

```
# newgrp users
```

The **newgrp** command doesn’t alter the **/etc/passwd** file or the **/etc/group** file; it opens a new shell with a different primary group. By default, a user can use the **newgrp** command to temporarily change her primary group to any group she is a member of. After creating the necessary files, the user can return to the shell that has the default primary group by executing the **exit** command. Keep in mind that users can change only to groups of which they are secondary members.

A password can be assigned to a group with the **gpasswd** command, but there is only one password, and you have to give it to every user who needs to use this functionality. Once a group is assigned a password, users need to use the password to execute the **newgrp** command, even if the user is a member of that group.

### Adding Users and Groups

Although you can edit the **/etc/passwd** and **/etc/group** files directly, doing so can lead to serious problems if you make errors in these files. It is much safer to use the commands described in the following sections.

#### Adding Users with useradd

The **[useradd](#ch09.xhtml_key01-a)** command is used to create new user accounts. To add a user with the default values (default primary GID, default home directory, and so on), execute the following command:

```
# useradd snuffy
```

Currently, on a Red Hat machine, this command performs several operations, including the following:

• It creates the user snuffy with the next available UID (typically the next available UID above 500).

• It creates a group with the same group name and GID as the username and UID.

• It sets the user’s primary GID to the newly created group.

• It creates a home directory for the user under the **/home** directory and with the same name as the username (**/home/snuffy** in this case).

• It copies the contents of the **[/etc/skel](#ch09.xhtml_key16-a)** directory into the new user’s home directory and gives the new user ownership of the copied files and directories.

Currently, on a Debian machine, the command **useradd snuffy** creates the user snuffy with the next available UID and the GID set to the users group (100); no home directory is created.

To set up the user on a Debian system with a specified home directory, you have to specify the **-m** and **-d** options. To copy the contents of the **/etc/skel** directory into the user’s home directory, use the **-k** option. To specify the primary group, use the **-g** option. The **-u** option can be used to specify the UID for the new user. Note that all these options can also be used on a Red Hat system, but often they are omitted in favor of default values. For example:

```
# useradd -m -d /home/snuffy -k /etc/skel -g 100 -u 1025 snuffy
```

This creates the user with all the specified information. On a Red Hat machine, the **/bin/bash** shell is auto-supplied, whereas on a Debian machine, the shell is blank by default, causing the system to assume the **/bin/sh** shell (which is a symbolic link to **/bin/bash**). On both systems, this value can be defined with the **-s** option.

Other important **useradd** options are as follows:

• **-D:** Executing the **useradd** command with this option displays the defaults defined in the **/etc/default/useradd** file. This option can also be used to modify the defaults.

• **-e:** This option sets an expiration date on the account; after that date, the account is disabled.

• **-G:** This option sets secondary group membership at account creation, which is often done after creating the account by using the **usermod** command.

• **-f:** This is the number of days after the password has reached its maximum life that the user can still log in (if the user changes his password during the login process). Setting the maximum and minimum password values is discussed later in this chapter.

• **-o:** This allows the creation of a user with a nonunique UID. This option is very dangerous and not recommended.

• **-s:** The full path and filename of the user’s login shell must follow the **-s** option.

#### useradd Defaults

On Red Hat–based systems, the **useradd** defaults are defined in the **/etc/default/useradd** file and can be altered with the use of the **-D** option for the **useradd** command.

##### The Default Shell

For example, to change the [default shell](#ch09.xhtml_key10-a) from **/bin/bash** to **/bin/tcsh**, execute the following command:

```
# useradd -D -s /bin/tcsh
```

Debian-based systems also use this file. For example, executing the **useradd -D -g 10** command sets the default group to be the wheel group (with GID 10) when you add a user on Debian.

#### skel Templates

When you use the **useradd** command and the **-m** and **-d** options, a home directory is created for the user. By default, the new home directory is a copy of the **/etc/skel** directory and its contents.

For example, **useradd -m -d /home/snuffy snuffy** creates the home directory **/home/snuffy**. This home directory is copied by default from the **/etc/skel** directory, and the ownership is changed to match the new user (as demonstrated in [Example 9-1](#ch09.xhtml_exe9_1)).

**Example 9-1**–Using **/etc/skel**

```
[root@server1 ~]# ls -la /etc/skel
total 24
drwxr-xr-x. 3 root root 74 May 9 18:15 .
drwxr-xr-x. 154 root root 8192 May 28 20:18 ..
-rw-r--r--. 1 root root 18 Mar 5 14:06 .bash_logout
-rw-r--r--. 1 root root 193 Mar 5 14:06 .bash_profile
-rw-r--r--. 1 root root 231 Mar 5 14:06 .bashrc
drwxr-xr-x. 4 root root 37 May 9 18:15 .mozilla
[root@server1 ~]# useradd snuffy
[root@server1 ~]# ls -la /home/snuffy
total 12
drwx------. 3 snuffy snuffy 74 May 28 21:25 .
drwxr-xr-x. 4 root root 30 May 28 21:25 ..
-rw-r--r--. 1 snuffy snuffy 18 Mar 5 14:06 .bash_logout
-rw-r--r--. 1 snuffy snuffy 193 Mar 5 14:06 .bash_profile
-rw-r--r--. 1 snuffy snuffy 231 Mar 5 14:06 .bashrc
drwxr-xr-x. 4 snuffy snuffy 37 May 9 18:15 .mozilla
```

You can put just about anything in a new user’s home directory by placing files or directories in the **/etc/skel** directory. It’s even more elegant to create a set of **/etc/skel_*XXX*** directories to make creating certain groups of users easier. For example, to have a special home directory structure for users in the payroll department, you might use the following steps:

Step 1\. Copy the **/etc/skel** directory to a new directory named **/etc/skel_payroll_staff**.

Step 2\. Populate **/etc/skel_payroll_staff** with the files and directories that you want users who are in the payroll department to have.

Step 3\. The next time you create a user from the payroll department, use the following syntax to specify the correct **skel** *template* directory:

```
# useradd -k /etc/skel_payroll_staff bob
```

#### Adding Groups with groupadd

The **[groupadd](#ch09.xhtml_key03-a)** command is much simpler than the **useradd** command, with fewer options and shorter command lines. To add a group named somegroup with the defaults for new groups, type the following:

```
# groupadd somegroup
```

This command creates a group with a GID determined by using the “next available” number above 500\. The result should be an entry like the following in the **/etc/group** file:

```
somegroup:x:516:
```

Note that no users are added to the group; the last field is empty. The **usermod** command, discussed in the next section, is used to add users to existing groups.

To add a group with a particular GID, execute a command like the following:

```
# groupadd -g 1492 somegroup
```

### Modifying Users and Groups

Creating users and groups is one thing, but being able to make them fit a changing system environment is another. Typically, you add and remove users from secondary groups, locking and unlocking accounts, and even changing a password expiration now and then.

#### Modifying User Accounts with usermod

To modify a user account with the **[usermod](#ch09.xhtml_key05-a)** command, you need to decide which of the following options is needed:

• **-c:** Describes the user; this modifies the GECOS field in the **/etc/passwd** file.

• **-d:** Changes the user’s new home directory. If there are files in this new home directory, you need to also change the user ownership of these files.

• **-e:** Changes the date the user account expires and is disabled.

• **-f:** Changes the number of inactive days. When a user account is locked out because the maximum password time frame has been exceeded, the user can have a grace period in which she can still log in as long as she changes her password during the login process. (This is discussed further later in this chapter, in the section “Aging Passwords.”)

• **-g:** Changes the primary group for the user; either GID or group name can be specified. Warning: This changes which file objects the user has access to.

• **-G:** Changes the user’s secondary groups. This is a single value or a list of comma-separated values of groups of which the user is to be a secondary member. Important note: Be sure to include all groups, including groups to which the user already belongs as a secondary member. This command replaces all secondary group memberships with the argument provided to the -**G** option.

• **-s:** Changes the path to the user’s login shell.

• **-u:** Changes the user’s UID. Warning: While this changes the UID ownership of files in the user’s home directory to match the new UID, other files on the system will not automatically be changed!

• **-L:** This locks a user’s account by altering the **/etc/shadow** file and prefixing the current encrypted password with an exclamation point (!).

• **-U:** This removes the lock on the user’s account by removing the exclamation point (!) from the front of the encrypted password in the **/etc/shadow** file.

Note

Another way to lock and unlock a user’s account is to use the **passwd** command and its **-l** and **-u** options to accomplish the locking and unlocking.

#### Modifying Groups with groupmod

The **[groupmod](#ch09.xhtml_key06-a)** command has fewer options than the **usermod** command, and there are only a few reasons to use this command. It’s primarily for altering a group’s name and GID. To modify a group’s GID, execute the following command:

```
# groupmod -g 101 users
```

Think twice before altering the GID of a group because you could orphan a lot of important files if you do. Remember: Files and directories are not owned by usernames and group names but rather by UIDs and GIDs. If you modify a group’s GID, a file previously owned by that GID now no longer has a group name associated with the file, as demonstrated in [Example 9-2](#ch09.xhtml_exe9_2).

**Example 9-2**–Changing GID

```
[root@server1 tmp]# ls -l sample
-rw-r--r--. 1 root test 0 May 28 20:17 sample
[root@server1 tmp]# grep test /etc/group
test:x:1001:
[root@server1 tmp]# groupmod -g 2000 test
[root@server1 tmp]# grep test /etc/group
test:x:2000:
[root@server1 tmp]# ls -l sample
-rw-r--r--. 1 root 1001 0 May 28 20:17 sample
```

You should also look in the **/etc/passwd** file to see which users’ primary groups will be affected when you change a group. Do not attempt to change the GID of a group that has a user member currently logged in. Finally, be aware that on some systems, if you remove or orphan the primary group of a user, the user defaults to being a member of the staff (50) group.

### Removing Users and Groups

Removing users and groups isn’t difficult, but several options need attention. Removing accounts from the system isn’t like on a Windows machine, which uses SIDs (security IDs) that are numerically unique and cannot be re-created easily. Linux accounts can be re-created easily (unless you delete the user’s home directory, which could only be recovered from a backup). Remember that Linux uses tables of static UIDs and GIDs, not SIDs.

#### Removing Users

If a user leaves the company, you are faced with either deleting the user account and leaving the user’s home directory on the system (perhaps for his replacement) or purging the system of the user by removing his account and home directory in one step.

Removing a user without affecting his home directory is accomplished by executing the following command:

```
# userdel snuffy
```

![Images](graphics/key_topic_icon.jpg)

To remove the user along with his home directory (the one configured in the **/etc/passwd** entry), you execute the following command:

```
# userdel -r snuffy
```

Note

Keep in mind that the **userdel -r** command also deletes the user’s mail file. However, other files on the system owned by this user will not be deleted. Those files will be owned by just the UID, not the name, of this user. In addition, if you create a new user with the same UID as the old user, the new user would be the owner of these files.

You cannot delete a currently logged-in user, so you must find out why he is still logged on. On some Linux systems, if the user is logged in and you attempt to delete that account, you receive an error message like the following:

```
# userdel: user snuffy is currently used by process 17098
```

If you don’t receive this sort of message, you can execute the **ps** command to determine the login shell’s PID. Before you kill this user’s login shell, use the **usermod -L** command to lock the account; then use **kill -9 PID** to log the user off the system. For example, to log off the tim user and delete the account, execute the following commands:

```
# usermod -L snuffy
# kill -9 17098
# userdel -r
```

One reason you shouldn’t just remove a user’s home directory is that usually either important files or important evidence (perhaps of wrongdoing on the user’s part) exists in that directory. If you are planning to replace the user, consider keeping the directory and just deleting the user account. This leaves the home directory and its contents with only a UID where the username was:

```
drwxr-sr-x 2 1002 staff 4096 Mar 18 07:17 snuffy
```

This is actually not a bad thing to see because it is a visual clue to you that the user who owned this home directory was deleted. However, because the home directory still belongs to the UID 1002 and the old user’s login name was set as the directory name, you have everything you need to re-create the user or set up a new user. For example, the following uses snuffy’s old home directory for the new sarah account:

```
# mv /home/snuffy /home/snuffy
# useradd -u 1002 -d /home/snuffy snuffy
```

#### Removing Groups

Before you delete a group, consider checking the following:

• Confirm that the group has no secondary members.

• Confirm that the group isn’t a primary group for a user account.

• Use the **find** command to find all files owned by the group. After you find them all, change the group ownership of all these files to another group.

To delete a group, type the following:

```
# groupdel grpname
```

Note

The majority of the questions on the Linux+ exam focus on the **useradd**, **usermod**, and **[userdel](#ch09.xhtml_key02-a)** commands. There isn’t much to ask about the group commands, but there might be a couple of questions about them in the fill-in-the-blank questions just to see whether you’re paying attention.

### The Shadow Suite

An important piece of a Linux machine with regard to security is the *Shadow Suite*. The Shadow Suite is a set of authentication tools and utilities that insinuates itself into the mix of the **/etc/passwd** file and user accounts. Without the use of the shadow tools, your encrypted passwords would be exposed to anyone who wants to see them because they would be in the world-readable **/etc/passwd** file in field 2\. The Shadow Suite also provides password aging properties that don’t exist without this suite. All this is accomplished by storing this data in another file: the **/etc/shadow** file.

#### Encrypted Passwords and Shadow Fields

The following is an example of an entry from the **/etc/passwd** file on a system that doesn’t use the Shadow Suite:

```
snuffy:$1$vEEOvj1b$GlzLuD9F..DjlQr/WXcJv1:501:10::/home/snu
ffy:/bin/sh
```

As you can see, an encrypted string appears in the second field. Unfortunately, all users can view this file, making this a potential security risk. In the next example, the **/etc/passwd** entry is shown on a system with the Shadow Suite enabled; note that the encrypted string is replaced with an x:

```
snuffy:x:501:10::/home/snuffy:/bin/sh
```

When the Shadow Suite is installed, the system stores encrypted passwords in the **/etc/shadow** file for user accounts and in the **/etc/gshadow** file for group accounts. The fields in the **/etc/shadow** file contain the user’s account password and password aging information. The following is an example of a shadow file entry:

```
snuffy:$1$vEEOvj1b$GlzLuD9F..DjlQr/WXcJv1:16263:0:99999:7:3
0:17000:
```

![Images](graphics/key_topic_icon.jpg)

The fields in the **/etc/shadow** file are

• **snuffy:** Login name: The user’s login name.

• **$1$vEEOvj1b$GlzLuD9F..DjlQr/WXcJv1:** Password: The user’s encrypted password.

• **16263:** Last change: The days since January 1, 1970, that have elapsed since the password was last changed.

• **0:** Minimum: The days that must elapse before the password can be changed. (0 effectively always allows immediate changes.)

• **99999:** Maximum: The days before the password must be changed. (99999 effectively disables the need to change the password because this is over 273 years.)

• **7:** Warning: The number of days before the password expires due to the Maximum field when the user will be warned.

• **30:** Inactive: The number of days after the account expires due to the Maximum field in which the user could still log in if the password is changed during login.

• **17000:** Expiration date: The number of days from January 1, 1970, and the day the account will expire.

Note

The last field in the file is reserved for future use and is not tested or much talked about.

Some of the fields of the **/etc/shadow** file are tricky. Consider the following:

```
julia:$1$vEEOvj1b$GlzLuD9F..DjlQr/WXcJv1:16263:5:90:7:30::
```

The julia account does not have an expiration date (the Expiration field is empty); however, this user is required to change her password every 90 days (the Maximum field is 90). Seven days before the 90-day time frame is up, the user will receive a warning when she logs in (the Warning field is 7). If she does not heed this warning, her account will be locked out on day 91\. She can still log in for up to 30 days after her account is locked (the Inactive field is 30), provided that she creates a new password during the login process. Finally, after changing her password, she cannot change her password again for at least 5 days (the Minimum field is 5); this is meant to prevent her from just switching back to her original password.

Note

The password aging provided by the Shadow Suite is far from perfect. Pluggable authentication modules (PAMs) provide much richer and more powerful password aging features.

#### shadow File Permissions

The permissions on the **/etc/shadow** file are important and may appear on the Linux+ exam. Because the **/etc/shadow** file isn’t world readable and only the system updates it, your passwords are much safer than without **shadow** installed.

The **/etc/shadow** file permissions are prominently featured on the Linux+ exam, as are the permissions for the **/etc/passwd** file. Here is a listing of the files and permissions on both Red Hat and Debian:

```
/etc/passwd”
Red Hat = -rw-r--r-- (644)
Debian = -rw-r--r-- (644)
/etc/shadow”
Red Hat = -r-------- (400)
Debian = rw-r----- (640)
```

As mentioned previously, these files and their permissions appear on the Linux+ exam. It’s important that you remember that Red Hat has a stricter permissions setup than Debian.

Note

Take note of the security permissions on the shadow files of your various test systems. You’ll find small but important variations. Some systems use **-------** and some use **r------**; make sure to note what each system uses. The **/etc/passwd** file is essentially open and readable by anyone, even those not on the system. The important and private encrypted passwords are in the **/etc/shadow** file. The **/etc/gshadow** file mentioned previously is also part of the Shadow Suite. However, this file is not listed in the Linux+ exam objectives.

### Changing Passwords

Users’ passwords are typically initially set to some value that is easily remembered by the root user when the account is created, and then the user is told to change her password immediately.

To change the root password, execute the following command when you are logged in as the root user:

```
# passwd
```

You are prompted to enter a password twice for verification. If you are executing this command as a normal user, the user’s current password is required before the new password will be accepted. This measure is meant to prevent a situation where you walk away from the system and someone quickly tries to change the password.

If you’re changing another user’s password, like the password of the snuffy user, you execute the following when you are logged in as the root user:

```
# passwd snuffy
```

Note

It’s important to remember who you are logged in as and what you type on the command line when changing a password. I’ve seen many a sysadmin change her own password instead of a user’s because she was in a big hurry!

#### Aging Passwords

Users’ passwords need to be changed frequently enough so that attackers don’t have enough time to guess them. Most users want to come to work, get paid, and go home; system security is of much lower importance to them than convenience.

To age passwords properly, use the **chage** command. The syntax for the **chage** command is

```
chage -option value username
```

This command acts on fields in the **/etc/shadow** file and has the following options:

• **-m:** Changes the minimum value, or how long after a password is changed that the user must wait until it can be changed again.

• **-M:** Changes the maximum value, which is the maximum number of days that can go by before the user must change the password.

• **-d:** Changes the last change value, which is the number of days since January 1, 1970, that the password was last changed. This is rarely modified directly; when a password is changed with the **passwd** command, this value is automatically updated.

• **-E:** Changes the expiration value, which is the number of days since January 1, 1970, that represents the day the user’s account will be disabled. The format used is *YYYY-MM-DD*.

• **-I:** Changes the inactive value, or the number of days of inactivity (no logins) after the account has reached the maximum limit before the user account is locked, at which point root attention will be required to reenable the account. Setting this to 0 disables the feature.

• **-W:** Changes the warning value, or the number of days before the user must change her password. This warning is provided only when the user logs in to the system.

Thankfully, you don’t have to memorize these values except to know them for potential Linux+ exam questions. Just execute the **chage username** command as the root user, and the system prompts you interactively for each value that can be configured for the specified user.

Users can use the **-l** option to view their own information, or the root user can view another user’s information with this option:

```
# chage -l snuffy
```

This produces the following output:

```
Minimum: 0
Maximum: 99999
Warning: 7
Inactive: -1
Last Change: Mar 19, 2023
Password Expires: Never
Password Inactive: Never
Account Expires: Never
```

The **passwd** utility includes some of the previous options, such as these:

• **-d:** Disables a user account by removing its password.

• **-n:** Sets the minimum password lifetime, in days.

• **-x:** Sets the maximum password lifetime, in days.

• **-w:** Sets the warning number of days before the password expires.

• **-i:** Sets the number of days an account with an expired password can be inactive before it’s locked.

• **-S:** Shows the user password information, such as what encryption is used and whether a password is set.

#### User Variables

It is possible to place certain limitations on a user’s account. If you want a user to be unable to create objects over a certain size or use too many system resources, you can configure the *ulimit* settings for that user. The **ulimit** command accepts many options, including the following:

• **-c:** Limits the size of core (crash dump) files.

• **-d:** Limits the size of the user’s process data.

• **-f:** Limits the maximum size of files created in the shell.

• **-n:** Limits the number of open file descriptors or open files allowed.

• **-t:** Limits the amount of CPU time allowed to the user (expressed in seconds).

• **-u:** Limits the number of processes that a given user can run.

• **-v:** Limits the maximum amount of virtual memory available to the shell.

To check a user’s **ulimit** settings, use this command:

```
# ulimit -a
```

Note

Remember that making these limits more permanent requires editing one of the user’s configuration files (**[.bashrc](#ch09.xhtml_key17-a)** or **.profile**) or the systemwide configuration files (**/etc/bashrc** or **/etc/profile**).

#### A Login Shell Session

![Images](graphics/key_topic_icon.jpg)

A login shell is a shell that is executed when logging in to the system. In other words, a login shell is one where the user either approaches the physical system and logs in normally as a user or logs in across the network and gets the full benefit of the contents of the files that make up the user’s environment.

The **[/etc/profile](#ch09.xhtml_key15-a)** script is the global configuration file that affects all users’ environments if they use the BASH shell. It’s sourced (read) every time a user performs a login shell. This file is a script and is executed right before the user’s profile script. After this, any files inside **/etc/profile.d** are sourced.

The user’s **~/.bash_profile** script, if it exists, is the next script sourced. This file contains variables, code, and settings that directly affect that user’s–and only that user’s–environment. If **.bash_profile** doesn’t exist, the shell looks for **.bash_login** or **.profile** and stops when it has found a match.

The **.bash_profile** script–or an alternative script if found–sources **.bashrc**. Note that this isn’t behavior in the shell; it’s a convention that makes everything easier later.

When the user logs out, the shell sources the **.bash_logout** file. This file is used to issue the **clear** command, so text from any previous command is not left on the user’s screen after the user logs out. It can also clean up anything that may have been launched as part of the session.

Be careful with questions on the Linux+ exam about login shell sessions. A lot of test takers do not pick the **.bash_logout** file as part of the user’s login session. It’s definitely one of the more commonly missed elements in the shell section of the exam.

The following is an example of a user’s login session:

Step 1\. The user logs in with a username and password.

Step 2\. The **/etc/profile** is sourced.

Step 3\. Files under **/etc/profile.d** are sourced.

Step 4\. The user’s **~/.bash_profile** is sourced.

Step 5\. The user’s **~/.bashrc** is sourced from within **~/.bash_profile**.

Step 6\. The user conducts her business.

Step 7\. The user initiates a logout with the **logout** or **exit** command or by pressing **Ctrl+D**.

The user’s **.bash_logout** script is sourced.

#### A Non-Login Shell Session

![Images](graphics/key_topic_icon.jpg)

*Non-login shell* sessions are typically the root user using the **su** command to temporarily become another user or a sysadmin using **su** to become the root user without loading the entire environment of the root or other user. Non-login shells are also started by opening new terminals from within a graphical session.

Note

The **su** command creates a non-login shell. If you need a login shell, place a dash after the **su** command (for example, **su - sean**).

When a user executes a non-login session, the only file sourced is the target account’s **~/.bashrc** file. (On Red Hat machines, the first action in the **~/.bashrc** file is to source the **/etc/bashrc** file if it exists. Other distributions run different files.)

Upon exiting that shell, no logout files or scripts are sourced; in addition, the source account’s scripts are not run again.

#### User Identity Query Options

An interesting problem that occurs often on a Linux system is knowing what user account you might be logged in as, or what effective rights and privileges you currently have, since you can easily transition over into the root user or other users with the **su** command and effectively act as a semi-root user with the **sudo** command’s help.

##### IDing Who You Are

The **[id](#ch09.xhtml_key07-a)** command is a very useful tool in determining who you are and what your current UID and GID are. It can also be used in scripts to ensure that the user is in the right security context.

Running the **id** command produces the following output:

```
# id
uid=1000(rossb) gid=1000(rossb) groups=1000(rossb),4(adm),
24(cdrom),27(sudo),30(dip),46(plugdev),115(lpadmin),
128(sambashare)
```

As you can see, the UID, primary GID, and other groups this user belongs to are shown.

##### Who Am I?

Two commands begin with the characters [*who*](#ch09.xhtml_key08-a), and they have different reasons for existing.

The **who** command tells you more than just who you are; as shown in the following example, it tells you who else is on the system, either locally on a console or on a pseudo terminal (aka ssh’ed in from elsewhere), and it includes not only the user’s name but the port the user is signed in on/from as well as when he signed in:

```
# who
rossb    tty7         2022-03-17 06:02 (:0)
rossb    pts/4        2022-03-30 07:33 (127.0.0.1)
```

In this output, you can see that the user ross is signed in locally on tty7, which indicates either a shell session from the console after pressing **Ctrl+F7** and signing in or, much more likely, a terminal application within the Linux Desktop GUI (which is the case here).

The second line of output is the same user ssh’ed in from another system, as indicated by the **pts/*X*** pseudo terminal connection type. Another indication of where the user is coming from is the in parentheses notation, where the first line of output shows :0, or the graphical display 0, and the 127.0.0.1 in the second line of output shows that the user is connected in from the localhost.

##### Who Am I, Really?

The **whoami** command must have been created by a frustrated system operator for those legions of users who simply cannot remember who they are and where they are.

Typing **whoami** yields the simplest output possible: the user’s current username. There is no possibility of getting fancy or cute with this command; its only possible options are to print out the version of the command or a very simple help page.

##### W, No, Not the Hotel

![Images](graphics/key_topic_icon.jpg)

Contrast the very simple and clean **whoami** command with the more complex **[w](#ch09.xhtml_key09-a)** command, whose output shows several useful bits of information:

```
$ w
09:33:07 up 1 day, 18:10, 2 users,     load average:  0.00, 0.00, 0.00
USER    TTY    FROM            LOGIN@   IDLE   JCPU  PCPU WHAT
rossb   tty7    :0             17Mar19 15days  1:16  0.59s mate-session
rossb   pts/5  127.0.0.1       09:32   19.00s  0.03s  0.03s -bash
```

The **w** command shows you the current time, the uptime in days and hours, the number of logged-in users, and the system loads for the last 1, 5, and 15 minutes.

Most importantly, the **w** command also shows you the command or applications that various users are running. While this isn’t very helpful if users are using an X terminal or a graphical application, you can see exactly what they are running on the command line. For example, the user in the following example is clearly looking for all spreadsheet files on the entire system–something that is at the very least slightly questionable and at worst an attempt to find pricing or salary information:

```
# watch -n 15 w
Every 15.0s: w          brunsonix: Mon Apr  1 09:42:20 2022

 09:42:20 up 1 day,18:19,2 users,  load average: 0.06, 0.06, 0.02
USER    TTY    FROM      LOGIN@   IDLE   JCPU   PCPU WHAT
rossb   tty7   :0        17Mar19 15days  1:21    0.59s mate-session
rossb   pts/5  127.0.0.1 09:32   20.00s  0.03s  0.03s find / -iname
“*.xls”
```

Therefore, if you want to keep an eye on who is logged in to your system with console access and monitor what they are running, execute the **watch** command with a reasonable time period, such as 30 seconds, and have it run the **w** command in a console that you can easily refer to.

##### Last but Not Least, just Last

![Images](graphics/key_topic_icon.jpg)

The **last** command reads the **/var/run/wtmp** file and shows who is logged on to the system, from where, and for how long. The **last** command shows similar information to the other query command choices; it doesn’t show anything particularly new, just a different look at some of the same information.

### Summary

In this chapter you learned about accounts, both user and group accounts as well as the concept of that a service account is and does. You also know now how to add, delete, modify users and group accounts, as well as how to tell what user is logged in, and other details about the user.

You additionally learned how to monitor your system using tols that report the logged in and connected users, how to configure the user's environment for the best effect and how to station files and directories you want in all new user account home directories.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 9-2](#ch09.xhtml_ch09tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 9-2**–Key Topics for [Chapter 9](#ch09.xhtml_ch09)

![Images](graphics/09tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[useradd](#ch09.xhtml_key01)

[userdel](#ch09.xhtml_key02)

[groupadd](#ch09.xhtml_key03)

groupdel

[usermod](#ch09.xhtml_key05)

[groupmod](#ch09.xhtml_key06)

[id](#ch09.xhtml_key07)

[who](#ch09.xhtml_key08)

[w](#ch09.xhtml_key09)

[default shell](#ch09.xhtml_key10)

[configuration files](#ch09.xhtml_key11)

[/etc/passwd](#ch09.xhtml_key12)

[/etc/shadow](#ch09.xhtml_key13)

[/etc/group](#ch09.xhtml_key14)

[/etc/profile](#ch09.xhtml_key15)

[/etc/skel](#ch09.xhtml_key16)

[.bashrc](#ch09.xhtml_key17)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

1\. Which field in the **/etc/shadow** file sets the number of warning days before the user’s password expires? Fill in just the numeral of this field in the followingblank:

__________________________________________________________

2\. If you saw the following output of the **ls -l** command, what would it indicate?

drwxr-sr-x 2 1002 staff 4096 Mar 18 07:17 snuffy

a. The account was deleted, but the user’s home directory was not.

b. The file is not owned by any account.

c. The **/etc/passwd** file is corrupt.

d. The user’s group is incorrect.

3\. If you created 10 accounts beginning with UID 501 and then deleted 501 and 504, what would be the UID of the next user you create, by default? Write your answer in the following blank:

__________________________________________________________

4\. By default, which directory is copied to a newly created user’s home directory when the **-m** and -**d** options are used with the **useradd** command? Fill in the full path and name of the directory in the following blank:

__________________________________________________________

5\. Which command is used to set the password expiration, warning, and other **/etc/shadow** file field information interactively?

a. **passwd**

b. **chpass**

c. **vipw**

d. **chage**

6\. Which command allows a user to open a shell with a different primary group? Fill in the blank below with just the command:

__________________________________________________________

## Chapter 10\. Implementing and Configuring Firewalls [This content is currently in development.]

**This content is currently in development.**

## Chapter 11\. Use Remote Connectivity for System Managment

This chapter covers the following topics:

[SSH (Secure Shell)](#ch11.xhtml_ch11lev1sec03)

[Executing commands as another user](#ch11.xhtml_ch11lev1sec04)

The exam objectives covered in this chapter are as follows:

**Objective 2.4:** Given a scenario, configure and execute remote connectivity for system management

Use to be that you could just move your chair and work on a server system, way back in the day, but so very quickly that changed to having all the servers in the server room somehwere else, and not wanting to walk there, or even being in the location or even city or country as the servers!

Having grown up in computing when Telnet (an unsecure remote connectivity option the preceded SSH) and clear-text FTP was commonplace, the world was a much kinder and more gentle place, hacking being not very common and people nodding hello in the hallway.

Sadly, but predictably, the situation quickly got to where we really needed secure terminal access and being able to safely and reliably connect to remote systems to do your work, mainly administering them, was an absolute requirement.

Today, you must have SSH installed, configured to be the most secure you can make it and even know how to use passphrase authentication and not just type in your password every time you connect to a server, or a couple of dozen servers all in a row or all at once!

Also of great importance in this chapter is the concept of [privilege elevation](#ch11.xhtml_key12-a), or as the objectives state "executing commands as another user", which requires a number of different tools, all critical for the budding and responsible system administrator to have knowledge (and practice!) of.

The elevation of privilege is even more appropriate in conjunction with SSH as you would typically never allow the root user to sign in over SSH, so gaining access to root-restricted resources means you need to elevate yourself to having root access or equivalent when you get TO the other system!

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 11-1](#ch11.xhtml_ch11tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 11-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/11tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** A user who normally works in a corporate office goes on a road trip, and in order to protect their machine from intrusions and attacks, chooses to run what technology to best protect their system?

**a.** Virtual Private Network

**b.** Web Application Firewall

**c.** TOR Client

**d.** Firewall

**2.** You have a small business office and have experienced what appears to be hacking attempts on your computers through your Internet router. You grab a handy Linux server and use what package to provide protection by running it and having that server be in between the outside router and your local network?

**a. checkpoint**

**b. firewalld**

**c. iptables**

**d. apparmord**

**3.** The process of receiving incoming packets, doing a stateful inspection of them and only forwarding certain ones that meet a particular criteria, this is commonly known as packet ________? Choose the best answer.

**a. inspecting**

**b. monitoring**

**c. filtering**

**d. transitioning**

**4.** Your firewall finds that a certain packet or set of packets do not meet the requirements to be forwarded to the destination host, acts in a way that will inform the sender of the situation. What would best describe this activity?

**a. flogging**

**b. dropping**

**c. responding**

**d. rejecting**

**5.** Your security administrator regularly uses a command to scan the log files of your systems in order to find hosts that are repeat offenders in attempts to act inappropriately over the network. What is the name of this command?

**a. scan2drop**

**b. monitor2reject**

**c. fail2ban**

**d. scan2act**

**6.** On your Red Hat/Fedora system you are using a command to configure your iptables rules via the firewalld technology. What is the name of that command?

**a. ufw**

**b. rhiptables**

**c. apparmorctl**

**d. firewall-cmd**

### Foundation Topics

As mentioned in the very top of this chapter, remote connectivity in general, and gaining access to a remote shell so you can do everything you need to on the command line on that remote system, is a vital and necessary skill for any systems operator to have.

### SSH (Secure Shell)

By this time, you are probably aware that the Telnet protocol sends passwords and data in clear text and shouldn’t be trusted for important sessions and tasks. The *Secure Shell* (*[SSH](#ch11.xhtml_key01-a)*) suite includes a protocol, a daemon, and client utilities that make your host-to-host shell sessions much more secure–about as secure as being at the physical console.

One of the features that makes SSH desirable as a remote protocol is its end-to-end encryption, which encrypts not only the username and password but also all communications.

The SSH suite replaces **telnet**, as well as **rsh**, **rexec**, **rcp**, and other unsecure utilities. You can use SSH to connect for a shell session, or you can use the **scp** command to remotely transfer files through the secure pipe that SSH builds between the hosts.

#### SSH Components

![Images](graphics/key_topic_icon.jpg)

SSH includes a number of programs and files:

• **ssh:** Used for remote shell sessions on another host, it replaces the **telnet**, **rsh**, and **rexec** commands.

• **scp:** Used for remote copying operations, it replaces the **rcp** command.

• **sshd:** The SSH daemon.

• **ssh-agent:** Runs as a wrapper to the user’s session and provides authentication when requested.

• **ssh-add:** Loads the user’s key(s) into the agent.

The SSH package configuration files are somewhat scattered. SSH daemon and global configuration files are kept in the **/etc/ssh** directory, and local or user-specific configuration files are kept in the **~/.ssh** directory for each user.

![Images](graphics/key_topic_icon.jpg)

The global configuration files include

• **/etc/ssh/[sshd_config](#ch11.xhtml_key02-a):** This is the main configuration for the **sshd** daemon.

• **/etc/ssh/ssh_host_[dr]sa_key:** These files, the **ssh_host_dsa_key** file and the **ssh_host_rsa_key** file, are in the same directory and are the private parts of the host’s key structure and should be protected from public view. The permissions for these files are 600 or rw for the root user and no permissions for anyone else.

• **/etc/ssh/ssh_host_[dr]sa_key.pub:** These files, the **ssh_host_dsa_key.pub file** and the **ssh_host_rsa_key.pub file**, are in the same directory and are the public parts of the host’s key structure. These must be world-readable and write-only by the root user or set to 644.

• **/etc/nologin:** This isn’t a part of SSH. However, if it’s present, no one can log in via SSH except the root user. Non-root users see the contents of the **/etc/nologin** file and then are denied access to the system.

A couple of special file pairs affect how SSH works, particularly the **/etc/ssh/ssh_[known_hosts](#ch11.xhtml_key04-a)** and **~/.ssh/known_hosts** files. The global file (**/etc/ssh /ssh_known_hosts**) is used to check the public key of a host attempting to attach via SSH. The local file (**~/.ssh/known_hosts**) is the file from which the client gets the public key of the remote server. If a new connection is begun to a previously unknown host, the user sees a message saying that the host is unknown and asking whether the user wants to store the host’s key in his known hosts file. If the user answers in the affirmative, the host’s public key is added to the **~/.ssh /known_hosts** file.

The **/etc/ssh/ssh_known_hosts** file should be world-readable and root-writable. The **~/.ssh/known_hosts** file must be owned by and writable for the user.

![Images](graphics/key_topic_icon.jpg)

A file of interest, the **~/.ssh /authorized_keys** file, affects only a particular user’s environment. This file is used to store the public keys that can be used for logging in as this user. These keys are matched with the keys presented by an **ssh** or **scp** client upon login request.

The SSH client utilities are versatile, with a number of options available to customize the experience. You just need to know the basics for the Linux+ exam, but this section includes a few fun options.

The SSH client command is used to replace the RSH and Telnet programs specifically. Its syntax is as follows:

![Images](graphics/key_topic_icon.jpg)

```
# ssh -l username remotehost
```

If you don’t specify a username with the **-l** option, the **ssh** command assumes that you want to use the name of the account with which you are locally logged in. For example, if you are logged in as the user ross and you execute the **ssh** command without the **-l** option, the command attempts to log you in as ross on the remote system.

For example, I could attach to the host mp3server as the user snuffy with this command:

```
# ssh -l snuffy mp3server
```

If I have not connected to this server before, I get a message similar to what’s shown here:

```
The authenticity of host ‘mp3server (192.168.33.44)’ can’t be
established.
RSA key fingerprint is
73:4f:fa:b0:42:a4:3a:a8:64:2c:ad:26:1d:b1: 21:e0.
Are you sure you want to continue connecting (yes/no)?
```

If I answer yes, the host’s public key is added to my **~/.ssh/known_hosts** file and looks something like this:

```
192.168.3.44 ssh-rsa
AAAAB3NzaC1yc2EAAAABIwAAAIEA1gFIB9VQpFKWAZUzNM+ac/U81Tk9R8O
CFfUkegVJXwj6nqCISPyV2iJwaukcVVaVAQ+JR3EhvOvh4PhoSg4yzBSUkJ
8aUBYoRSGj7PCD+vyWyi1922HGxWbWooMBAO/Was8I7N0zQ6jxDO9qNOHcr
IFeU7qbOCrKjQDM08HQjk0=
```

Rather than work with RCP or FTP for file transfer work, I tend to use SCP. The **scp** command uses the SSH protocol and encrypts the files sent from one host to another host. For example, if I wanted to transfer file1 from my root user’s home directory on my machine to the same location on a host named remotehost, I could use the following command:

```
# scp /root/file1 root@remotehost:/root/file1
```

The system would prompt me with the RSA key question (as shown in the previous **ssh** example) if I have not connected to this system previously from this account. I would be prompted for the password, and then the system would transfer the files. The output from a file transfer looks like this:

```
# root@192.168.1.73’s password:
mypubkey.txt 100% |**********************| 1379 00:00
```

You can copy files from your host to another host, as shown previously, or copy files from a remote host to your system by reversing the source and target specifications.

You can even copy files from one remote system to another remote system. For example, the following command recursively copies the **/data** directory and all its contents from the remote1 host to the remote2 host after prompting you for the password for both hosts:

```
# scp -r root@remote1:/data root@remote2:/data
```

Another use of the SSH protocol is to log in to a host and use SSH to forward the output from an X client back to your display. This feature, which can be specifically invoked with the **-x** option, is referred to as an *X11 tunnel*.

SSH allows for skipping the password prompt when signing on between computers, which can be convenient if you use the **ssh** or **scp** command frequently and don’t mind the possibility that someone could sit down at your accidentally unlocked station and have her way with your network!

Note

There has been a lot of talk about why it’s important to delete **.rhosts** files from user directories. Basically, if you have a user who has a hostname in her **.rhosts** file and that host also has the user’s hostname in its **/etc/hosts_equiv** file, that user can log in without a password by using the **rlogin** command. This would be a security risk, so my advice is to delete these files with the following command:

![Images](graphics/key_topic_icon.jpg)

```
# find /home -iname .rhost -exec rm -f {} \;
```

Note

This deletes all **.rhosts** files it finds in users’ home directories and does not prompt you for each deletion.

Note

The system-wide configuration for the SSH client is kept in the **/etc/ssh/[ssh_config](#ch11.xhtml_key03-a)** file, while each user’s individual configuration file for the SSH client is kept in the user’s **~/.ssh/config** file.

The following example shows the steps required to enable SSH use without a password. In this example I have two machines, fattyre and murphy, both of which are Linux workstations with the necessary SSH software loaded, as per the defaults. This demonstration assumes that fattyre and murphy are both in each other’s **/etc/hosts** files or resolvable via DNS.

![Images](graphics/key_topic_icon.jpg)

Here’s how you can enable SSH use without passwords:

**Step 1.** Log in to fattyre as the root user.

**Step 2.** For this example, create a new user named user1:

```
useradd -m user1
```

**Step 3.** Set user1’s password with the **passwd** command to whatever you want:

```
passwd user1
```

**Step 4.** Switch to the user1 user account:

```
su - user1
```

**Step 5.** Create and set the permissions for the **.ssh** directory:

```
mkdir .ssh ; chmod 700 .ssh
```

**Step 6.** Generate an RSA key:

```
ssh-keygen -b 1024 -t rsa
```

**Step 7.** When prompted for the location for the file, press **Enter** to accept the default.

**Step 8.** When prompted for a passphrase, enter

```
seatec astronomy
```

**Step 9.** Reenter the passphrase when prompted.

**Step 10.** Change to the **.ssh** directory and set the permissions on the **id_rsa.pub** file:

```
cd .ssh ; chmod 644 id_rsa.pub
```

**Step 11.** Copy the **id_rsa.pub** file to a new file called **authorized_keys**:

```
cp id_rsa.pub authorized_keys
```

Note

The next steps take place on the host murphy.

**Step 12.** From the host murphy, ensure that you can contact the host fattyre with a ping:

```
ping fattyre
```

**Step 13.** Sign on to the host murphy as the root user.

**Step 14.** Add a user named user2:

```
useradd -m user2
```

**Step 15.** Set the password for user2:

```
passwd user2
```

**Step 16.** Enter the password twice to confirm it.

**Step 17.** Switch to the user2 account:

```
su - user2
```

**Step 18.** Make a directory and set its permissions with the following command:

```
mkdir .ssh ; chmod 700 .ssh
```

Note

The next steps take place on the host fattyre.

**Step 19.** From the host **fattyre**, connect to the murphy host as user2:

```
ssh -l user2 murphy
```

**Step 20.** When prompted about the RSA key, answer yes and then enter user2’s password.

**Step 21.** While logged in as user2 on the host murphy via SSH, copy the **authorized_keys** file from the fattyre host with the following command:

```
scp user1@fattyre:~/.ssh/authorized_keys ~/.ssh
```

The output of the **scp** program should look similar to this:

```
authorized_keys 100% |************************| 236 00:00
```

**Step 22.** Exit user2 on the host murphy and return to being user1 on fattyre.

**Step 23.** On fattyre as user1, invoke the **ssh-agent** as a wrapper to your shell:

```
ssh-agent $SHELL
```

**Step 24.** Add your key to the agent:

```
ssh-add
```

**Step 25.** When prompted for the passphrase, enter the following:

```
no more tears
```

You then see output similar to this:

```
Identity added: /home/ssha/.ssh/id_rsa (/home/ssha/.ssh/id_rsa)
```

**Step 26.** Try to log in as user2 on murphy and watch what happens:

```
ssh -l user Murphy
```

You shouldn’t see any password prompt; you should see only the confirmation of where you last logged in from:

```
Last login: Wed May 26 13:46:55 from fattyre
```

**Step 27.** If you do see a prompt for the passphrase, enter **no more tears** as you did before.

This is all it takes to get two accounts and machines set up to use SSH utilities without having to enter anything but the **ssh-agent** command along with the passphrase. Remember that **ssh-agent** resides in memory and wraps a security blanket around your shell session, answering any SSH-related security requests for you. The **[ssh-add](#ch11.xhtml_key07-a)** utility is for adding key information into the agent and doesn’t have to be run again as long as your key information remains the same.

Note

The **[ssh-copy-id](#ch11.xhtml_key06-a)** command is also a possible choice for sending a user’s authorized key to another server. For example, to have the user ZakkW’s authorized key exist on the Eternal server, you could use the command

```
# ssh-copy -id -i ~/zakkw/.ssh/keyfile zakkw@eternal
```

This will copy the user zakkw’s file to the remote server and install it into the **authorized_keys** file, prompting for a password to authenticate the process.

Ideally, this would be performed by the root user for both systems and assumes that you are on a remote system from the Eternal server.

#### Tunneling

![Images](graphics/key_topic_icon.jpg)

One of the greatest features of SSH is that it can "tunnel" or provide a conduit from inside one network and even behind a firewall, and through to another network. In many cases using [tunneling](#ch11.xhtml_key08-a) can make it so that you can do things that either your network administrator doesn't want you to do, or you need to do because of an overly-restrictive policy, such as at a coffee shop or internet cafe somewhere.

Let's talk about some of the various scenarios where tunneling can come in handy.

##### X11 Forwarding

X is complex and hard to setup some times, and it might seem that tunneling X from another machine to show on yours will be hard too, but it's fairly straightforward due to the magical properties of ssh tunneling!

Let’s say you have a Linux system named cygnusx1 that you want to run an application in the GUI environment on, but you want that application that runs on the remote host to display on YOUR local system?

Here's a possible set of steps you might take.

**Step 1.** On a Mac, you might use xQuartz, (found at xquartz.org), which you download and install

**Step 2.** Then you would run the command **ssh -X ursulak@cygnusx1**

**Step 3.** This will open a shell in the terminal on the remote host (cygnusx1) where you can then run the app

**Step 4.** In a second or two, the remote application, running as a process on the remote host, will display on YOUR system as if it were being run locally.

This is just an example of how [forwarding X11](#ch11.xhtml_key09-a) applications from the host they are running on to your local system would work. There's all sorts of things that could go wrong, but all that is out of the scope of the Linux+ exam, the main thing is the concept, which we have more than adequately covered.

##### Port Forwarding

Most of the times when someone talks about port forwarding, it's because there is a need to get around some overly-strict or controlling network or firewall situation. Keep in mind that there are also often VERY good reasons for those restrictions and rules, so be responsible and don't willingly cause issues using port forwarding.

Using SSH to forward ports takes several paths, but the main concept is the same, you are using the ssh client on one system to tunnel out to the ssh server on another system and cause services that are represented by a port on one system to be mapped or to appear to be connected to the other system.

In general, port forwarding occurs in three main ways:

• **Local [Port Forwarding](#ch11.xhtml_key10-a)**: In this, you'll cause a remote port to be mapped to and to appear as if were on your local system. Kind of like mounting an NFS share locally, mapping a port from a remote system to yours locally will effectively appear as if your local system is providing that service.

• **Remote Port Forwarding:** Flip the scenario around and allow your local system resources to be used by a remote machine. For example, I might map a remote system's port 8080 to my local 5500 port, and anyone connecting to that remote server on the 8080 port will get transported to my local port and service.

• **[Dynamic Port Forwarding](#ch11.xhtml_key11-a):** Sometimes you don't want to explicitly assign ports and just want the SOCKS proxy on your system to use dynamically assigned local ports and handle all the details. Think of a situation where you need to access ports and protocols that are not allowed through a convention center network setup, you can use what is effectively a VPN/Proxy to drill through the local restrictive network stack and let you connnect and communicate freely with your desired target hosts, services and ports.

Note

The beauty of using SSH tunneling for these purposes, is that you don't have to worry that by doing so you are exposing the local network or system unnecessarily, you're using the very secure SSH protocols and stack to do all of this!

### Executing Commands as Another User

By this time, you are probably aware that the Telnet protocol sends passwords and data in clear text and shouldn’t be trusted for important sessions and tasks. The *Secure Shell* (*SSH*) suite includes a protocol, a daemon, and client utilities that make your host-to-host shell sessions much more secure–about as secure as being at the physical console.

#### The sudo Command

The problem with the **[su](#ch11.xhtml_key14-a)** command is that to provide a user with elevated privileges, you need to provide the user with the root password, and then that user would have full administrative access to the system.

Often you want to allow a regular user to execute some commands, but not all commands, as the root user. For example, if a network error occurs on a user’s workstation, you might want that user to be allowed to restart the networking service. On some systems, this can be accomplished by executing the following command:

```
# /etc/rc.d/init.d/network restart
```

To execute this command successfully, the user needs to have root privileges.

This is where you either give them the root password, (don't do it!) or you do it the correct and reasonable way, via the **[sudo](#ch11.xhtml_key13-a)** command and it's partner tools.

Instead of providing the user with the root password, you can set up the **sudo** command to allow the user to run just the necessary command. To do this, you need to log in as the root user and then execute the following command:

```
# visudo
```

This command allows you to edit the **[/etc/sudoers](#ch11.xhtml_key15-a)** file, the file that allows you to provide root access for specific commands to specific users. The **[visudo](#ch11.xhtml_key17-a)** command automatically assumes that you want to use the **vi** editor to edit this file. To use a different editor, such as the **nano** editor, execute a command like the following:

```
# export EDITOR=nano
```

Note

![Images](graphics/key_topic_icon.jpg)

Why use the **visudo** command instead of editing the **/etc/sudoers** file directly? The **visudo** command performs some error checking when you exit the editor to make sure you didn’t make formatting mistakes.

#### The sudoedit Command

One of the conundrums of granting a user access to edit a configuration file is that if you are using **vi**/**vim**, you are essentially giving the user the ability to run *any* command as root.

To prevent a user from gaining shell access with a simple set of keystrokes from **vi**/**vim** while running it as root, there exists the **[sudoedit](#ch11.xhtml_key16-a)** command, which is really just a symbolic link to a function contained in the **sudo** command.

![Images](graphics/key_topic_icon.jpg)

The **sudoedit** command lets you allow a user to use any editor, not just **vi**/**vim**. It also enables the user to edit the files specified as himself or herself, rather than as the root user.

When a user edits a file by using the **sudoedit** functionality, a temporary copy of the file(s) is made, and it is owned by the user in question. Since the user is now the owner of the temporary file(s), he can successfully edit the file without having root access. Upon saving the file(s), the temporary copy owned by the user is copied back to the original file location, and the original ownership is restored; the now unnecessary temporary copy is discarded.

To configure **sudoedit**, add the following line to the **/etc/sudoers** file:

```
%newsudo ALL = sudoedit /some/path/to/a/file
```

Configure the newsudo group in **/etc/sudoers** to have the users you want to use **sudoedit**, and then all they need to do is run the command:

```
sudoedit /path/to/that/file
```

The **/etc/sudoers** file has many options. For the Linux+ certification exam, you just need to know how to provide a user with the ability to execute commands as the root user. For example, if you want a user account with the name ross to be able to run all commands as the root user, add the following line:

```
ross ALL=(ALL) ALL
```

To limit a user to a specific command, such as the **/etc/rc.d/init.d/network** command, add the following line:

```
ross ALL=(ALL) /etc/rc.d/init.d/network
```

For a user to execute a command as root, she needs to use the **sudo** command. The syntax is as follows:

```
# sudo /etc/rc.d/init.d/network restart
```

The user is then prompted for her own password (not the root password). If the correct password is given and the access is permitted based on an entry in the **/etc/sudoers** file, the command is executed as the root user. If the user attempts to execute a command that she is not authorized to execute, an error message appears on the screen, and the attempt is logged.

#### User Privilege Escalation

Users on a Linux system come in a number of types, and knowing the types as which you are logged in and how to escalate or deescalate at will is important. The following user types are available:

• **Root:** This is the root user, who is the super user and the most privileged user on the system. There should be only one of them, characterized by the name root and the UID (user ID) 0.

• **Standard:** Otherwise known as “regular” or “normal” users, these are the rank-and-file users on the system; they have no special privileges and typically have UIDs that range from 1000 and higher.

• **Service:** These are the accounts that have to exist to ensure that every service or daemon on the system is running as a user, since every process must have a user attached. These accounts are never signed into; they exist in the **/etc/passwd** file and may even have **/bin/nologin** as the specified shell.

The best security practice is to avoid logging in as the root user unless you need to perform specific administration commands. In most cases, you should not log in as the root user directly but rather should gain root access by executing either the **su** command or the **sudo** command.

Note

The wheel group is an odd thing on the Linux system these days. Traditionally used on Unix systems to allow users to gain root access, the wheel group is often now tied directly to having **sudo** access.

If the wheel group is configured to have privileged access via **sudo** and the **/etc/sudoers** file, then adding a user to the wheel group gives the user those privileges. For example, in our openSUSE system, the wheel group is set up to be able to allow members of that group to execute any command, just as the root would be able to:

```
%wheel  ALL=(ALL) ALL
```

This entry is normally commented out, but it would be very easy to remove the single # comment in front of it in the default file to enable the wheel group (and its members) to have full administrative access to the system.

#### The su Command

To gain access to another user account with the **su** command, use the following syntax:

```
su account_name
```

![Images](graphics/key_topic_icon.jpg)

For example, to switch to the root account, execute the following command:

```
# su root
```

This provides you with a non-login shell for the root user. Typically you want a login shell because it provides you with the full user environment (environment variables, shell customizations, and so on). This can be accomplished by using the **-l** option or just a **-** option:

```
# su - root
# su -l root
```

To gain access to a regular user account, you must provide the account name. However, if you don’t provide an account name, the **su** command assumes that you want to switch to the root account. As a result, the following commands are all the same:

• **su - root**

• **su -l root**

• **su -**

• **su -l**

When switching from the root account to a regular user account, no password is required. This means the root user can switch to a regular user account to test that account’s features (or troubleshoot problems for the user) without having to change that user’s password.

To switch from a regular user account to any other account, you must know the password of the account you are switching to.

Note

Some distributions’ versions of the **su** command allow for the use of X and remote X; simply use the **sux** command instead of the **su** command. This is most notably present on the openSUSE and SUSE Linux Enterprise distributions.

#### PolicyKit

[PolicyKit](#ch11.xhtml_key18-a) exists to provide application-level definition and handling of unprivileged access to privileged processes. For example, you might use PolicyKit to allow a user the ability (and the rights) to perform a task by executing a command with elevated privileges. If that sounds eerily like the **sudo** command, it's understandable, they both have fairly similar goals.

One difference is that PolicyKit is a little easier, and certainly less tedious than prefacing almost everything you do with the **sudo** command!

Note

As can happen with the Linux+ objectives, they reference here a package (PolicyKit) that has been superseded by the polkit package. However, since the objectives specify PolicyKit, we have to talk about it, and mostly leave polkit alone.

One of the main positives of PolicyKit is that it's a central place for defining and accessing policies that allow unprivileged users to perform what would normally be privileged actions.

The PolicyKit local configuration is kept in /etc/polkit-1/localauthority and uses the common method of include files that contain PolicyKit configuration and end in .conf, or the more specialized .pkla files.

Examples of those types of actions PolicyKit can be configured for include:

• Allow the user to configure Wireless connections

• Make it possible to mount and unmount USB and other detached media devices

• Let the user manage shutdown, reboot and hibernate events

• Make devices accessible that are traditionally difficult to access, such as system audio

#### The pkexec Command

With the previous discussion of the PolicyKit package, **[pkexec](#ch11.xhtml_key19-a)** makes a lot more sense, as it's the most common way to utilize the PolicyKit policies.

The **pkexec** command, when used to run another command, will execute that command as the targeted user. The user can be specified or if not, **pkexec** will attempt to execute the target command as the root user.

For example, to execute the lemmy.sh script as the root user you would type:

![Images](graphics/key_topic_icon.jpg)

```
# pkexec lemmy.sh
```

Since we did not specify a user, the default for pkexec is to attempt to run the subsequent command, script or executable as the root user.

Note

Don't forget that PolicyKit is on it's way out, and though polkit has mostly replaced it, the concepts will be similar enough that when it's time to do this in a production environment, you'll recognize how things work!

### Summary

The focus of this chapter is how to remotely and securely connect with systems for the purposes of administering them, using the SSH suite of technologies and all those ssh-prefaced commands we learned about in this chapter.

You also learned about the methods for privilege elevation, or running commands or acting as another user such as su, sudo and pkexec.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 11-2](#ch11.xhtml_ch11tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 11-2**–Key Topics for [Chapter 11](#ch11.xhtml_ch11)

![Images](graphics/11tab02.jpg)![Images](graphics/11tab02a.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[ssh](#ch11.xhtml_key01)

[sshd_config](#ch11.xhtml_key02)

[ssh_config](#ch11.xhtml_key03)

[known_hosts](#ch11.xhtml_key04)

ssh-keygen

[ssh-copy-id](#ch11.xhtml_key06)

[ssh-add](#ch11.xhtml_key07)

[tunneling](#ch11.xhtml_key08)

[X11 Forwarding](#ch11.xhtml_key09)

[Port Forwarding](#ch11.xhtml_key10)

[Dynamic Forwarding](#ch11.xhtml_key11)

[privilege elevation](#ch11.xhtml_key12)

[sudo](#ch11.xhtml_key13)

[su](#ch11.xhtml_key14)

[/etc/sudoers](#ch11.xhtml_key15)

[sudoedit](#ch11.xhtml_key16)

[visudo](#ch11.xhtml_key17)

[PolicyKit](#ch11.xhtml_key18)

[pkexec](#ch11.xhtml_key19)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** After configuring the PolicyKit settings for your system, what command would you use to use those rules when executing a target command that your current user doesn't have rights to execute by itself?

**a.** sudo

**b.** pkexec

**c.** suexec

**d.** execit

**2.** When configuring the sudo command, what is the full path and filename of it's primary configuration file?

__________________________________________________________

**3.** You are able to access a remote system using just a passphrase for authentication, what must have you copied from your system to the remote system in order for this to happen?

**a.** Your personal public key

**b.** The system's public key

**c.** The wheel group's public key

**d.** The remote user's private key

**4.** When configuring your system to allow or deny certain groups or users to sign in via SSH, what is the full path and filename of the configuration file where these settings are kept?:

_________________________________________________

**5.** If you invoke the ssh command with the -X option, what are you likely to be doing after you sign on the remote system?

**a.** Nothing, just standard commands

**b.** Running Xeyes locally and displaying remotely

**c.** Running X11 on the remote and displaying locally

**d.** Running remote X apps that display locally

**6.** Which of the following editors are specifically designed to make it more secure to edit files when using sudo to elevate your privileges?

**a.** sudovim

**b.** visudo

**c.** sudoedit

**d.** nanobot

## Chapter 12\. Understand and Apply Access Controls

This chapter covers the following topics:

• [File permissions](#ch12.xhtml_ch12lev1sec03)

• [Security-Enhanced linux (SELinux)](#ch12.xhtml_ch12lev2sec18)

• [Context-Based Access](#ch12.xhtml_ch12lev1sec09)

• [Command Line Utilities](#ch12.xhtml_ch12lev1sec10)

The exam objectives covered in this chapter are as follows:

• **Objective 2.4:** Given a scenario, apply the appropriate access controls

Setting, maintaining and verifying access to system resources is a key part of being a valid systems administrator.

In this chapter, we'll be looking at the world of straightforward access controls, and then taking the complexity and intensity of the tools up a level with those two competitors, SELinux and AppArmor.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 12-1](#ch12.xhtml_ch12tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 12-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/12tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** As a sysadmin, you need to set up a shared directory with multiple users. What special permission can be set to cause the inheritance of group ownership?

**a. 0**

**b. 1**

**c. 2**

**d. 4**

**2.** You want to change the group owner of a file or directory. Which of the following can accomplish this? (Choose two.)

**a. chuser**

**b. chgrp**

**c. chown**

**d. chmod**

**3.** Which of the following is considered a MAC security system?

**a.** SecureMAC

**b.** AppArmor

**c.** Lockdown

**d.** AppSecure

**4.** Which of the following is a valid SELinux mode? (Choose all that apply.)

**a.** Disabled

**b.** Enforcing

**c.** Defensive

**d.** Permissive

**e.** Progressive

**5.** Which command is used to display security context on processes?

**a. show**

**b. list**

**c. ps**

**d. ls**

**6.** Which command is used to display security context on files?

**a. show**

**b. list**

**c. ps**

**d. ls**

### Foundation Topics

Access to system resources is very important to have proper control over. Linux traditionally, up to a certain point of the addition of [ACL's or Access Control Lists](#ch12.xhtml_key03-a), did not support multiple user owners, group owners and additional users and groups that have access.

Additionally, the use securing of your systems via the use of SELinux and AppArmor is another way to secure those systems and maintain control over the systems resources.

Note

As frequently happens, the topics from the Linux Objectives don't line up like we would prefer, so we'll move things around so that they flow well throughout the chapter.

In particular, where the Linux+ Objectives have a large lump of commands at the end of the section, we will encounter them all through the normal discussions of the various topics as we go along.

If there are any that remain, they'll be covered in the "Command-line utilities" section.

### File Permissions

[Permissions](#ch12.xhtml_key01-a) determine how users can access resources on a system. System security is configured by the user’s UID (user ID), GIDs (group IDs–both primary and secondary), and the permissions on the object she is attempting to access.

Every object on a system must belong to at least a user owner and group owner. This is a security feature, and it helps establish who has rights to do what to objects on the filesystem, as discussed in the following sections.

#### Permission Trio Bits

![Images](graphics/key_topic_icon.jpg)

[Figure 12-1](#ch12.xhtml_ch12fig01) shows the 10 positions (1 type bit and 3 trios of permission bits) that make up the permissions section of a file.

![Description: Table Description automatically generated](graphics/12fig01.jpg)

**Figure 12-1**–Permission trios

The first of the 10 bits is the type of the object:

• **.:** Indicates that this is a normal file.

• **l:** Indicates that this is a symlink (symbolic link), which is a file that points to another object.

• **b:** Indicates that this is a block device file.

• **c:** Indicates that this is a character device file.

• **d:** Indicates that this is a directory.

The next 9 bits are the *permission trios*. Each of the trios affects a certain set of users (user owner, group owner, or other). To determine which permissions a user has to a given object, begin from the left, and as soon as a match is made, that trio alone is the permissions in effect for that user and object. Here are the three trios:

• **[User owner](#ch12.xhtml_key04-a):** If the user is the user owner, this permission trio is in effect.

• **[Group owner](#ch12.xhtml_key05-a):** If the user’s primary or secondary groups are this group, but only if that user is not the user owner, this permission trio is in effect.

• **Other:** If the user is neither the user owner nor a member of the group owner, this permission trio is in effect.

Note

On some modern Linux systems, you see another character right after the permission set. This could either be a . character, which is related to SELinux, or a + character, which is related to access control lists (ACLs). Do not mix up the Windows environment and Linux in your mind. Linux filesystem permissions (non-ACL permissions) do not have “effective permissions”; you must use an ACL to have more than a single user owner or more than a single group owner.

Each of the trios is made up of 3 bits (which can have the values 4, 2, 1). The bits work like light switches: If a bit is on, then the value counts; if it is off, the value doesn’t count. That value is used with the **chmod** command as well as with other commands.

![Images](graphics/key_topic_icon.jpg)

The bit values equate to the following permissions for files:

• **4:** Read, which is the ability to view the file’s contents

• **2:** Write, which is the ability to change the file’s contents

• **1:** Execute, which means the file can be executed (The read permission is also needed for a script, but a binary can execute with only the execute permission.)

These permissions have similar, but slightly different, meanings for directories:

• **4:** Read, which is the ability to view the directory’s contents (using the **ls** command). However, to see file attributes (such as with the **-l** option to the **ls** command), execute permission on the directory is also required.

• **2:** Write, which is the ability to add and delete files in the directory. This is a powerful permission for directories because a user can delete every file in a directory, even files that he doesn’t own, if he has the write permission on the directory. Caveat: For write permission to be valid, the user also must have execute permission.

• **1:** Execute; the user can use the **cd** command to get into the directory or use the directory in a pathname. For example, if the user attempts to execute **cd /home/bob**, she needs execute permission on the **/** directory, the **home** directory, and the **bob** directory.

To better understand directory permissions, think of a directory as a room. If you want to see what is in the room, you need a window. Think of the read permission as the window. If this permission is set, you can see into the directory (room). If you want to get into the room, you need a door. Think of the execute permission as the door. This concept helps the caveat for the write permission make more sense: To remove something from a room, you first need to be able to get into the room!

If you execute the **ls -l** command on an object, and its permission trios are 666 (or rw-rw-rw-), the only way that number could be arrived at with the possible bit values is for the 4 and 2 bits to be on–or rw- (read and write, but not execute). If you see a file that is set to 666, that equates to all three trios having the same permissions–read and write but not execute.

Note

Watch for Linux+ exam questions that try to trick you with a user who is both the user owner and a member of the group owner, but the correct permissions for executing or changing the file aren’t in a single trio. You can’t mix the trios, even if your user account encompasses several of the trios.

For example, say that a user named fred is the user owner of the file object **/home/fred/22AcaciaAvenue.mp3** and is a member of the group owner of that object. The file’s listing has the following permissions set:

```
-rw-r-xr-x 2 fred users 0 Jan 26 13:08 22 AcaciaAvenue.mp3
```

The fred user’s permissions might seem to span the various trios, but because fred is the user owner, he matches the first trio and stops there. In other words, the user fred has read and write permission, but not execute, even though fred is a member of the users group, and members of that group do have execute permission on this file.

#### Manipulating Permissions

The **[chmod](#ch12.xhtml_key06-a)** command is used when modifying or altering an object’s permission trio bits. Only the root and object’s owner can alter permissions.

The two modes of manipulating the permissions for an object are octal and symbolic. Both modes have their place, but it’s hard to say which is used more to set permissions these days.

The general rule is that if you are wanting to set permissions (that is, wipe out the current permissions and set them to a given permission), you use the octal method, which looks like this: (644, 777 and so on). If you want to alter permissions, you use the symbolic or letters method: (g+rx, o=a). Many times I have needed to clean up after someone who has accidentally set an entire directory structure’s permissions and caused havoc. You should be familiar with and skilled at both methods, but remember that the symbolic method is more exacting and precise.

![Images](graphics/key_topic_icon.jpg)

#### Octal Mode

The [octal](#ch12.xhtml_key10-a) notation method uses the same bits to describe what you want your permissions to be (4 = read, 2 = write, 1 = execute). For example, if you are told that the current permissions for an object are 644 and you are asked to ensure that all users have read and write access to that object, execute the following command:

```
chmod 666 file1
```

The **chmod** command works great on groups of files, too:

```
# chmod 644 /home/lukec/*.txt
```

It even works on directories and their contents. For example, say that the user bertrandr has a directory on which he wants to set all the files to the permission 640 to make the files more secure. He could use the following command:

```
# chmod -R 640 /home/bertrandr/data/*
```

Take a moment to understand why this command works the way it does. The **chmod** command has an **-R** option that affects the object named and all its child objects. The user bertrandr doesn’t want to change the permission of the data directory itself; he just wants to change the permission on the contents, which is why the slash and asterisk characters are on the end of the target. This command acts on the entire contents of the **/home/bertandr/data** directory but doesn’t modify the directory’s permissions. However, if there were any directories within the **/home/bertandr/data** directory, all those directories would have the permissions changed (along with all files and directories beneath them)!

The **chmod** command has a few useful options:

• **-c:** Reports only which files were changed.

• **-v:** Reports all files.

• **-h:** Changes symbolic links, not the original file.

• **-f:** Suppresses error messages.

• **-R:** Operates recursively through directories.

The **chmod** command’s recursive option is an uppercase R, not a lowercase r, as with some other commands. If you are familiar with the cases of the various command options, you will be fine on the Linux+ exam.

Note

When using the octal notation method, you should always specify three values: owner, group, and others. If you specify only one value, the system uses that value for the others permission set and assumes a value of 0 for the owner and group permissions. This is never a good idea!

![Images](graphics/key_topic_icon.jpg)

#### Symbolic Mode

When using the **chmod** command with symbolic values, keep in mind that you can change all the permissions, as in the numeric mode, but you need to use a much longer command. The primary reason to use [symbolic mode](#ch12.xhtml_key11-a) is to affect, or alter, smaller sets of permissions rather than to overwrite them all.

With symbolic mode, you use a letter to identify each trio:

• User owner = u, group owner = g, other = o, and all = a

• A qualifier: + to add, - to remove, or = to assign

• The permissions being set: r = read, w = write, and x = execute

To use the symbolic values to set permissions, you can change them all at once, as the following command demonstrates:

```
# chmod a=rwx file
```

This produces permission trios that are set to -rwxrwxrwx.

Or you can use each one of the identifiers, with its qualifier and permissions separated by commas:

```
# chmod u=rw,g=rx,a= file
```

This produces a file that has its permissions set to -rw-r-x---.

Note

This method of using the symbolic mode is unwieldy and somewhat inelegant for constant use. Use symbolic mode when you want to fine-tune permissions, not when you want to set all the permissions.

To change just the user owner’s permissions to rwx, use the following command:

```
# chmod u=rwx mystuff
```

To change the group owner’s permissions to r-x, use the following command:

```
# chmod g=rx mystuff
```

To change the other or everyone else’s permissions to r, use this command:

```
# chmod o=r mystuff
```

Keep in mind when using symbolic mode that the permissions you are not specifying stay as they were before you executed the **chmod** command.

You can use several methods to set a file to be executable without knowing its other permissions. For example, if you know a file exists but don’t know the permissions and you are told to make sure it’s executable by all permission trios, use the following command:

```
# chmod a+x file1
```

Alternatively, you can leave off the *a* and get all the trios by default:

```
# chmod +x file1
```

Remember: When changing permissions, you can always use either the numeric method or the symbolic method. The numeric method is normally easier when changing all the permissions, while the symbolic method is normally easier when changing one or just a few permissions.

### File and Directory Ownership

Ownership is critical to any Linux/UNIX system, everything must be owned by at least a user owner and a group owner, not to be confused with additional groups.

You can use the ls command to view the ownership of any object that you have access to, but be sure to use the -l option, so the permissions and ownership show up properly.

#### Changing File Ownership

The **[chown](#ch12.xhtml_key07-a)** command is used to set the user owner, group owner, or a combination of the two with one command. The format for the **chown** command is

```
# chown -options user:group object
```

The **chown** command accepts both of the following commands as valid (where the owner/group separator can be either a : or a . character):

```
# chown snuffy:users file1
# chown snuffy.users file1
```

In addition, you can use the following syntax with **chown**:

![Images](graphics/square.jpg) **owner:** Changes only the user owner.

![Images](graphics/square.jpg) **owner:group:** Changes both the user owner and the group owner.

![Images](graphics/square.jpg) **owner::** Changes the user owner and sets the group owner to the primary group of the current user.

![Images](graphics/square.jpg) **:group:** Changes only the group owner and leaves the user owner unaffected.

Let’s say that the user snuffy’s primary group is called users, and the account is a secondary group member of the accounting group. By default, every object snuffy creates on the system has snuffy as the user owner and users as the group owner. This can cause problems in shared directories. For example, if snuffy visits a shared directory whose group ownership is set to the accounting group and creates a file named **snuffysexpenses.txt**, that file is inaccessible to any of the other users who share that directory unless they are also members of the group users.

Say the user martha does expenses and needs to have ownership of the file and you, as the administrator, want to change the group ownership of this file to the accounting group. To accomplish this task, use this command:

```
# chown martha:accounting snuffysexpenses.txt
```

Let’s say that now the file needs to be owned by another user who cuts the checks, fluchre; you can change just the user owner without having to bother with the group owner:

```
# chown fluchre snuffysexpenses.txt
```

If for some reason you decide that an entire directory tree of files needs to have ownership changed, you can change them all with the following command:

```
# chown -R root:accounting /accounting
```

Note

The only user on the system who can change the user ownership of an object is the root user. Even the owner of a file can’t “give ownership” to another user. However, a regular user can change the group ownership of an object as long as the user is a member of the group whose ownership she is changing.

#### Changing Group Ownership

When just the group owner needs to be changed, the simplest method is to use the **[chgrp](#ch12.xhtml_key08-a)** command. The syntax of the command is straightforward:

```
# chgrp staff file1
```

Changing a large set of files to another group owner requires the use of the **-R** (recursive) option:

```
# chgrp -R staff /data/*
```

This command changes the contents of the **/data** directory (and all its subdirectories) to the group owner staff but leaves the user owner alone.

Options for the **chgrp** command include the following:

![Images](graphics/square.jpg) **-c:** Shows a line of output only for changed objects.

![Images](graphics/square.jpg) **-h:** Changes symbolic links, not the original file.

![Images](graphics/square.jpg) **-R:** Recursively affects the target and all children.

![Images](graphics/square.jpg) **-v:** Shows a line of output for every object, regardless of the actions performed on the object.

Note

Although it is not a Linux+ exam objective, the **newgrp** command can be handy when it comes to group ownership. A regular user can execute the command **newgrp *groupname*** if he is a member of *groupname*. This opens a new shell in which the primary group is *groupname*, which is useful when creating a bunch of files that need to be group owned by a secondary group. To close this new shell, simply execute the **exit** command.

### Understanding and Using umask

[Umask](#ch12.xhtml_key09-a) was covered in detail in [Chapter 8](#ch08.xhtml_ch08), “[Understanding Linux Security Best Practices.](#ch08.xhtml_ch08)”

### Permission Granularity Issues

Several aspects of how the Linux and Unix filesystems are constructed can cause problems for administrators. For example, if you are not using ACLs, only a single group can be the group owner for a given object. Whoever wants access to that object needs to be a member of the group that owns the file (unless you, as the owner of the file, want to give permission to all others). For example, consider the following **ls -l** output:

```
-rw-r----- 1 bob staff 0 Jan 26 13:08 22 data.txt
```

To be able to see the contents of this file, you need to be either the bob user or a member of the staff group.

Configuring many groups and users to have access to the right files can be difficult. Every user has a primary group and could be a member of additional groups (secondary groups). This poses problems when sharing files between members who are in shared secondary groups. For example, say that the bob user (primary group staff, secondary group project), the sue user (primary group payroll, secondary group project), and the steve user (primary group acct, secondary group project) are working on a joint project and sharing files in the **/home/project** directory. The bob user creates a file that ends up looking like the following when listed with the **ls -l** command:

```
-rw-r----- 1 bob staff 0 Jan 26 13:08 22
data_for_sue_and_steve.txt
```

Unfortunately, even though all users are in the same group (the project group), the sue and steve users can’t view the contents of this file. They are not members of the staff group, so their permission set is others for this file.

As described later, the bob user can change the group ownership of the file to the project group, but then users must perform this action every time they create a file. It is unreasonable to assume that all users will remember to do this all of the time (and, as an administrator, you don’t want to have to teach all the users to perform this action on their files).

There’s a way out of this situation: You can set an additional or special bit on the shared directory, which causes all users who have access to inherit the group owner of the directory on all objects they create in that directory. This permission set, called *SGID*, is covered in detail in this chapter.

Note

It used to be that only a few Linux distributions featured ACL's or Access Control Lists, and you were relegated to using the Special Bit Permissions to try to allow multiple sets of users access to resources. Now many distributions feature ACL's and Special Bits are used less for those reasons.

#### Special Bit Permissions

![Images](graphics/key_topic_icon.jpg)

The following special bits are available for Linux filesystem use:

• **SUID:** The *set user ID* (*SUID*) permission allows a user to run a program as if he or she were the user owner of the program; in most cases, the user owner is the root user. The numeric value of this permission set is 4*XXX* (where *XXX* is replaced by the numeric values for the trio sets mentioned previously).

• **SGID:** When set on a directory, the set group ID (SGID) permission automatically gives group ownership of all new files created in the directory to the group owner of the directory (numeric = 2*XXX*). When set on a file, the SGID allows a user to run a program as if he or she were the group owner of the file.

• **Sticky bit:** This permission set is used to keep “nonowners” from deleting files in a common directory (numeric = 1*XXX*). In a *sticky bit* directory, only the owner of the file or the owner of the directory can delete the file. (Root can always delete files as well.)

Note

The Linux+ exam objectives make mention of the GUID in the permissions section, but GUID (globally unique identifier) usually refers to a more robust form of the UUID (universally unique identifier) and so seems out of place here in a chapter on permissions. Traditionally, though, some Unix documentation referred to the SGID bit as the GUID.

Remember that these special permissions are used only when necessary, which isn’t often; the SUID and SGID permission sets on an executable file pose a security risk, even when properly used. Avoid providing write permission to SUID and SGID executables. This permission gives a regular user the ability to replace the code within the file and opens a security hole on the system.

[Special permissions](#ch12.xhtml_key12-a) can be set using either the numeric or the symbolic method, just as other permissions can be set using both methods with the **chmod** command.

Note

The use of the characters *XXX* in the following examples indicates that permissions exist and need to be included but removes the focus from the permissions. In other words, these are the regular permissions discussed previously, and we have substituted the *XXX* characters in these examples to focus on the special bits instead.

The first way to set these special permissions is to use the numeric mode when executing the **chmod** command. All permissions must be overwritten when using numeric mode; the following sets the SUID permission on the file:

```
chmod 4XXX /some/program
```

Several bits can be changed or set simultaneously. The following command, for example, sets both the SUID and SGID bits for the program (which is somewhat rare but permitted):

```
chmod 6XXX /some/program
```

The second way to set special permissions is to use the symbolic mode. For example, to add SUID on a file:

```
chmod u+s /some/program
```

Again, you can set several special bits at once even with the symbolic mode, although the syntax is a bit more complex:

![Images](graphics/key_topic_icon.jpg)

```
chmod u+s,g+s /some/program
```

#### Setting the SUID Bit on Files

A command related to the SUID bit is **chsh**. The **chsh** command allows a regular user to change her login shell. Note the current permissions for this command:

```
-rws--x-- 1 root root 15432 Apr 29 2013 /usr/bin/chsh
```

The **s** in place of the user owner’s execute permission indicates that this is an SUID command. When this command executes, it modifies the contents of the **/etc/passwd** file. The **/etc/passwd** file is not normally something that can be modified by non-root users; as you can see, normally only the root user has this ability:

```
-rw-r--r-- 1 root root 2036 Mar 8 18:39 /etc/passwd
```

However, with the SUID permission set, the **chsh** program is able to access files as either the person who runs the command or as the owner of the **chsh** program (which, in this case, is root).

What if you, as the administrator, do not want users to change their login shells? Just execute the following command as root:

```
# chmod u-s /usr/bin/chsh
```

[Example 12-1](#ch12.xhtml_exe12_1) shows a live example.

**Example 12-1**–Demonstration of SUID

```
[root@localhost ~]# ls -l /usr/bin/chsh
-rws--x--x. 1 root root 15432 Apr 29 2013 /usr/bin/chsh
[root@localhost ~]# su - student
[student@localhost ~]$ chsh
Changing shell for student.
Password:
New shell [/bin/bash]: /bin/csh
Shell changed.
[student@localhost ~]$ exit
logout
[root@localhost ~]# chmod u-s /usr/bin/chsh
[root@localhost ~]# su - student
[student@localhost ~]$ chsh
Changing shell for student.
Password:
New shell [/bin/csh]: /bin/bash
setpwnam: Permission denied
Shell *NOT* changed. Try again later.
```

Note

While the user can “try again later,” as the last line of output in [Example 12-1](#ch12.xhtml_exe12_1) suggests, until the root user resets the SUID permission set, no regular user will be able to change his login shell.

#### Setting the SGID Bit on Files

The SGID permission is rarely set on files. Consider the following program with the SGID bit set:

```
-r-xr-sr-x 1 root tty 10996 Jul 19 2011 /usr/bin/wall
```

The **s** in place of the group owner’s execute permission indicates that this is an SGID command. The **wall** command allows users to send messages to the terminal windows of all users who are logged in. Normally this would be a security issue; you don’t want a user to interfere with another user’s terminal window. Having a message pop up in a terminal where a user is working can be distracting.

Users can use the **wall** command in this way because it is an SGID program. When this program executes, it accesses files as if the person executing the command were a member of the tty group. This, in turn, allows the **wall** program to have write access to the terminal device files group owned by the tty group:

```
# ls -l /dev/tty1
crw--w---- 1 root tty 4, 1 Jun 2 17:13 /dev/tty1
```

If you are having problems with users abusing the **wall** command, simply take away the SGID access:

```
# chmod 0555 /usr/bin/wall
```

Note

The **wall** program can be used to communicate with other users, but because maturity levels vary among humans and definitely among computer users, you may have users harassing others or inappropriately sending broadcast messages. By restricting a user’s access to this command, you improve all the productivity of all system users.

#### Setting the SGID Bit on Directories

Consider the earlier scenario in which the bob user (primary group staff, secondary group project), the sue user (primary group payroll, secondary group project), and the steve user (primary group acct, secondary group project) are working on a joint project and sharing files in the /**home/project** directory. The bob user creates a file that ends up looking like the following when listed with the **ls -l** command:

```
-rw-r----- 1 bob staff 0 Jan 26 13:08 22
data_for_sue_and_steve.txt
```

Recall that this results in a problem: Even though bob, sue, and steve all have a common group, sue and steve can’t access this file. If bob were to change the group ownership to the project group, then sue and steve would be able to view the contents of this file. However, expecting users to do this every time they create a file isn’t reasonable.

The solution is to add SGID permission to the **/home/project** directory:

![Images](graphics/key_topic_icon.jpg)

```
# chmod g+s /home/project
```

This command changes the group ownership to be the projects group, which means all new files created in the **/home/project** directory are automatically group owned by the group owner of the directory (which would have to be set to the project group, of course). Note that this doesn’t solve the problem of the existing file; it affects only new files.

#### Setting the Sticky Bit

The sticky bit is used mostly for ensuring that users in a shared directory can’t delete anyone else’s files. A good example of this is the **/tmp** directory:

```
drwxrwxrwt 29 root 4096 Jun 2 17:27 /tmp
```

The t in place of the others execute permission indicates that this is a sticky bit directory. The **/tmp** directory is a location where all users must be able to create files. Unfortunately, the permission that allows users to create files also allows them to delete files–all files–in that directory.

When you add the sticky bit permission, the meaning of the write permission for directories changes. Instead of meaning “add and delete all files in the directory,” it means the only users who can now delete files in this directory are as follows:

• The owner of the file

*or*

• The owner of the directory (which is normally the root user)

*or*

• The root user

Anyone can still add a file to this directory, as long as it doesn’t result in overwriting another user’s file.

#### Viewing and Changing File Attributes

In addition to permissions, there are filesystem [attributes](#ch12.xhtml_key02-a), or another way to think of them is they are "advanced settings" for each file or directory on the filesystem. Notice we use filesystem as the container, not disks, there are attributes that are only valid for a particular filesystem type, which you can check out in the appropriate man page.

Handling file attributes from the command line is accomplished by the dynamic duo of commands:

• **[lsattr](#ch12.xhtml_key19-a):** This command displays the attribute set for a given set of files and/or directories.

• **[chattr](#ch12.xhtml_key20-a):** This command is used to set a file or directories attributes, with some notable exceptions, which are out of scope for this exam.

##### Displaying File Attributes

The primary way you'll view a file's attributes is using the **lsattr** command, which displays a line of attribute notations, typically a bunch of minus symbols punctuated by an letter, such as:

```
#  lsattr file1
--------------e----- file1
```

The command displays that only the **e** or extent format attribute is set, which in this case means that the file is using something called extents to map blocks on the disk. This happens to be one of the very few attributes that isn't easily changed by the **chattr** command.

##### Key File Attributes

Far from being just an oddity, there are some very important attributes that affect files on a filesystem, some of those more notable attributes are:

• **a**–The a attribute being set means the file can only be appended to, not overwritten.

• **A**–The A attribute is one used very often for read-only data sets that are accessed frequently, such as busy static portions of a web site, it means the atime record is not updated.

• **C**–The C attribute is used to change the file's copy-on-write attribute and how it's handled on filesystems that support C-O-W.

• **i**–The i attribute is a very powerful one, it causes the file to be unmodifiable, not deletable, no renaming and many other restrictions.

There are a number of other attributes, which you can and absolutely SHOULD look up in the man page for the **chattr** command, it's good information, but we have covered the most likely ones in our list previously.

##### Setting File Attributes

To set an attribute on a file, it couldn't be simpler:

```
#  chattr +A file1
```

Now if you were to display the file's attributes again, you'd see:

```
#  lsattr file1
--------A-----e----- file1
```

If you were to display the file contents, or read the file with a program, the file's atime or access timestamp record would not be updated.

##### Removing File Attributes

To remove an attribute on a file, it is about as easy as setting the attribute:

```
#  chattr -A file1
```

Now if you were to display the file's attributes again, you'd see:

```
#  lsattr file1
--------------e----- file1
```

This removes or unsets the A attribute, which means that the atime record will be updated as usual when this file is accessed.

Note

Please note that there are a LOT of options that have restrictions or don't work on a particular filesystem, or even don't work on ANY but a couple filesystems. Hit the chattr and lsattr man pages, there's a lot of good information there. Additionally, use test files and directories to gain skills with chattr and lsattr, not important password or system files, or you'll end up having to troubleshoot and maybe fix some issues.

### Finding Files by Permission

Note

If you are looking in the Linux+ objectives for finding files by permission, you won't find it, but I have always gone beyond the objectives to make sure you have the information you'll need when you get into the production environment, so enjoy this little bonus section!

Attackers who breach a system often attempt to set certain files to have the SUID or SGID bit set in order to allow their otherwise normal accounts to perform all sorts of unauthorized tasks.

The **find** command has an operator that makes it easy to find vulnerable files. The **-perm** operator is usually followed by a three- or four-digit set of permissions, as shown in this example:

```
# find /usr/bin -perm 777
```

This example searches for any object in the **/usr/bin** directory and all subdirectories that has the exact permissions rwxrwxrwx. This is fine, but it doesn’t help you find security risks caused by the SUID and SGID bits. This next command does, however:

```
# find / -perm -4000
```

At first glance, this might look as if it’s a search for all files that have the SUID bits and then blank permissions from that point on. In fact, it searches the entire system for all files that have the SUID bit set, regardless of the other permissions.

You should install the system and then run a **find** command that reports any file that has an SUID bit set, like so:

```
# find / -perm -4000 -ls
```

Redirect this output to a file and keep that file on a disk or in some safe place off the system (such as on a USB drive). Every so often (especially after installing new software or when you think your system has been exploited), you should run the same **find** command and then compare the results to the original with the **diff** command, like this:

```
# diff /root/latestfindperm /mnt/usb/findperm.orig
```

Investigate any differences!

### Access Control Lists

Anyone who spends any amount of time using Unix/Linux standard permissions will either cultivate a habit of swearing bitterly at their restrictions or choose to learn more about ACLs.

#### Not Enough Granularity

Why would you need more than the regular Unix/Linux permissions? In a number of instances, the limitations of having only one user owner or only one group owner are debilitating or overly restrictive. Yes, it’s true that you can add people to the group that owns an object, but you can only have one group that is the owner, with a single set of permissions, and there will be times when you need another group of people to have fewer or more permissions[md]and then what do you do? For example, you might have a set of pricing spreadsheets that are maintained by the purchasing department, which must have read and write access to the contents of the pricing subdirectory. Also, you might have a group of sales associates who depend on being able to have read access to those spreadsheets so they can refer to them when giving pricing quotes to customers.

In the standard Unix/Linux permissions scheme, there can be only one group owner, and if you put both the sales associates and the purchasing people into a single group, one of these groups will not have adequate or appropriate access to the shared files.

#### ACLs to the Rescue

An ACL enables you to attach multiple user owners, multiple group owners, and even multiple other owners to a filesystem object or group of objects. In the pricing spreadsheets example, you can assign a secondary set of group ownership with different permissions to the pricing spreadsheets, using a command that sets the ACL to allow that group to have different capabilities on the directory and, by default, its contents.

#### Viewing ACLs

Before you assign any alternative or additive permissions to a directory or file, you should view its permissions by using the **getfacl** command. This keeps you from accidentally setting conflicting or overriding permissions if someone else has already set an ACL on the object.

To view the full permissions of a file:

```
$ getfacl test
# file: test
# owner: ross
# group: users
user::rwx
group::rwx
other::rwx
```

The first line of the output confirms that you are viewing the file **test** and its access control list settings, which at this time are blank, though they can be set. The next two lines confirm who the user owner and the primary group owner are. The next three lines after that are the blank permissions that you can now set.

#### Setting an ACL

Using the **setfacl** command is fairly easy, though things can get complex if you are trying to set multiple groups to access an object with different permissions.

When setting the permissions on an object, you use three sections for those permissions. The following example sets user permissions (u) for the user snuffy and adds the permissions to read and write but not execute for this object. The **-m** option enables you to modify the permissions:

```
# setfacl -m u:snuffy:rw test
```

This results in the user snuffy being given rw access as a user owner, not disturbing or displacing the original (and current owner) ross. You can confirm this by using the **getfacl** command:

```
$ getfacl test
# file: test
# owner: ross
# group: users
user::rwx
user:snuffy:rw-
group::rwx
mask::rwx
other::rwx
```

Notice in the output of the **getfacl** command that under the default permission set, which is the original user owner’s permissions, there is now a line that details what permissions the user snuffy has on this file.

Setting an ACL for a group owner is just about as easy: You simply change the **u** in the command to **g** and replace the user snuffy with the proper group and alter the permissions to reflect the permissions you want this now secondary group owner to have on the object:

```
# setfacl -m g:itcrowd:r-x
```

Now retrieve the permissions again with

```
$ getfacl test
# file: test
# owner: ross
# group: users
user::rwx
user:snuffy:rw-
group::rwx
group:itcrowd:r--
mask::rwx
other::rwx
```

As you can see, the group itcrowd has now been added to the ACL for the file test. Effectively, this means that users who are not the owner of the file who belong to the users group will have full rwx access to this file, but users who are not the user owner and are a member of the itcrowd group will have only r access to the file.

#### We All Wear Masks

The final facet of ACLs that we need to cover is the concept of masks. Masking for an ACL involves restricting permissions for all configured users and groups in the ACL. It’s an easy way to make sure that people can read scripts in a directory but not execute them or to ensure that users and groups can view files but not change them.

To set a mask that restricts all ACL users and groups from reading an object, enter the following:

```
# setfacl -m m::rx test
```

You can run the **getfacl** command on the file to see that the mask has been altered from its default full permissions to be restrictive to r and x:

```
$ getfacl test
# file: test
# owner: ross
# group: users
user::rwx
user:snuffy:rw-                  #effective: r--
group::rwx                      #effective:r-x
group:itcrowd:r--
mask::rwx
other::rwx
```

You can see additional text next to any additional user owners and group owners that tells you what their effective rights are now. If the displayed rights are not acceptable, then don’t use the mask but instead restrict the permissions by the groups and users.

### Context-Based Access

Files and directories may be compromised by users who either do not understand permissions or who are accidently provided with more access than intended. There’s an old system administration saying: “If we didn’t have users, nothing would break, and the system would be more secure.” Of course, the response to this saying is, “Without users, we wouldn’t have a job!” Users’ mistakes often do provide unintended access to the data that is stored in files.

Context-based access can be configured to deal with compromised permissions by providing an additional level of security when processes are used to access files. The control of file and directory access is not in the hands of the user but rather is handled by the administer.

It isn’t just user files and directories that are a concern. Imagine a situation in which a remote hacker is able to utilize an exploit to gain control of your web server process (the **httpd** process). Without context-based controls, this hacker could direct the **httpd** process to read critical system files (such as the **/etc/passwd** file) and get information that could lead to further intrusions on the system or the network.

Traditional Linux permissions (read, write, and execute on files and directories) make use of discretionary access control (DAC), while context-based permissions utilize mandatory access control (MAC). However, when a context-based solution is enabled, DAC still applies (both MAC and DAC are enforced). Typically, the MAC controls are first evaluated and, if the access is granted, then the file’s permissions are checked.

This chapter covers two commonly used context-based methods: SELinux and AppArmor.

#### Security-Enhanced Linux (SELinux)

An [SELinux](#ch12.xhtml_key13-a) security policy can require processes to be a part of an SELinux security context (think “security group”) in order to be able to access files and directories. Regular permissions are still used to further define access, but for accessing the file/directory, this SELinux policy would be applied first.

A bigger concern, and one that most SELinux policies are designed to address, is how daemon (or system) processes present a security risk. Consider a situation in which you have many active processes that provide a variety of services. For example, one of these processes might be a web server, as shown in the following example:

```
# ps -fe | grep httpd
root       1109     1  0  2022 ?        00:51:56
/usr/sbin/httpd
apache    1412  1109  0 Dec24 ?        00:00:09
/usr/sbin/httpd
apache    4085  1109  0 05:40 ?         00:00:12
/usr/sbin/httpd
apache    8868  1109  0 08:41 ?         00:00:06
/usr/sbin/httpd
apache    9263  1109  0 08:57 ?         00:00:04
/usr/sbin/httpd
apache   12388  1109  0 Dec26 ?        00:00:47
/usr/sbin/httpd
apache   18707  1109  0 14:41 ?         00:00:00
/usr/sbin/httpd
apache   18708  1109  0 14:41 ?         00:00:00
/usr/sbin/httpd
apache   19769  1109  0 Dec27 ?        00:00:15
/usr/sbin/httpd
apache   29802  1109  0 01:43 ?         00:00:17
/usr/sbin/httpd
apache   29811  1109  0 01:43 ?         00:00:11
/usr/sbin/httpd
apache   29898  1109  0 01:44 ?         00:00:10
/usr/sbin/httpd
```

In this output, each line describes one Apache web server process (**/usr/sbin/httpd**) that is running on the system. The first part of the line is the user who initiated the process. The process that runs as root is used only to spawn additional **/usr/sbin/httpd** processes. The others, however, respond to incoming web page requests from client utilities (web browsers).

Imagine for a moment that a security flaw is discovered in the software for the Apache web server; this flaw allows a client utility to gain control of one of the **/usr/sbin/httpd** processes and issue custom commands or operations to that process. One of those operations could be to view the content of the **/etc/passwd** file, which would be successful because of the permissions placed on this file:

```
# ls -l /etc/passwd
-rw-r--r-- 1 root root 2690 Dec 11  2022 /etc/passwd
```

As you can see from the output of this command, all users have the ability to view the contents of the **/etc/passwd** file, based on the fact that all users have read permission. Do you want some random hacker to have the ability to view the contents of the file that stores user account data?

With an SELinux policy, the **/usr/sbin/httpd** processes can be “locked down” so that each one can access only a certain set of files. This is what most administrators use SELinux for: to secure processes that may be compromised by hackers making use of known (or, perhaps, unknown) exploits.

#### SELinux Mode

![Images](graphics/key_topic_icon.jpg)

There are three [SELinux modes](#ch12.xhtml_key15-a):

• **Disabled:** When in disabled mode, SELinux is not functional at all. No checks are performed when users attempt to access files or directories.

• **Enforcing:** When in enforcing mode, SELinux performs checks and blocks access to files or directories, if necessary.

• **Permissive:** When in permissive mode, SELinux performs checks but never blocks access to a file or directory. This mode is designed for troubleshooting problems as log messages are created when in this mode.

Use the **getenforce** command to determine the current SELinux mode:

```
# getenforce
Enforcing
```

The result Enforcing means SELinux is installed, and the security policy is currently active.

You can change the mode (which is useful when testing a new policy or trouble-shooting SELinux problems) by issuing the **setenforce** command:

```
# setenforce 0
# getenforce
Permissive
```

While in permissive mode, SELinux does not block access to files and directories, but warnings are issued and viewable in the system log files.

You can switch between enforcing and permissive modes, but disabling SELinux requires changing a configuration file and then rebooting the system. For example, on a RHEL (Red Hat Enterprise Linux) system, you would change the SELINUX setting in the **/etc/selinux/config** file as follows:

```
# cat /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#       enforcing - SELinux security policy is enforced.
#       permissive - SELinux prints warnings instead of enforcing.
#       disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of these two values:
#       targeted - Targeted processes are protected,
#       mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

Conversely, if the current SELinux mode is *disabled*, you can change the SELINUX setting to either *enforcing* or *permissive* in the **/etc/selinux/config** file and reboot the system. It is always a good policy to verify that a change has taken place by running the **getenforce** command after the reboot is complete.

#### SELinux Policy

An [SELinux policy](#ch12.xhtml_key16-a) is a collection of rules that determine what restrictions are imposed by the policy. The policy itself is often very complex, and details are beyond the scope of the Linux+ exam. It is, however, important to know that the policy sets the restrictions based on rules.

You should also know that one of the most commonly used policies is the targeted policy. This policy normally exists by default on systems that have SELinux installed, and it is typically the default policy that is enabled when SELinux is first enabled.

A targeted policy contains rules that are designed to protect the system from services rather than regular users. Each service is assigned one or more security contexts, Boolean values, and additional rules that limit the service’s ability to access files and directories.

![Images](graphics/key_topic_icon.jpg)

The **sestatus** command provides overall status information about SELinux, including the current policy:

```
# sestatus
SELinux status:                  enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:             /etc/selinux
Loaded policy name:              targeted
Current mode:                   enforcing
Mode from config file:              enforcing
Policy MLS status:                enabled
Policy deny_unknown status:      allowed
Max kernel policy version:         28
```

#### SELinux Booleans

What exactly a policy consists of and how to create a policy are beyond the scope of the Linux+ exam and, as a result, this book. However, you can modify the behavior of a policy by using Booleans. A Boolean is a true/false value that changes how SELinux performed MAC.

An SELinux policy typically has dozens of different Booleans. To determine what a Boolean is used for, use the **semanage** command:

```
# semanage boolean -l | head
SELinux boolean            State  Default Description

privoxy_connect_any       (on   ,  on)   Allow privoxy to
connect any
smartmon_3ware          (off  ,   off)   Allow smartmon to
3ware
mpd_enable_homedirs     (off  ,   off)   Allow mpd to enable
homedirs
xdm_sysadm_login        (off  ,   off)   Allow xdm to sysadm
login
xen_use_nfs              (off  ,   off)   Allow xen to use
nfs
mozilla_read_content      (off  ,   off)   Allow mozilla to
read content
ssh_chroot_rw_homedirs   (off  ,   off)   Allow ssh to chroot
rw homedirs
mount_anyfile             (on   ,  on)   Allow mount to
anyfile
```

For example, in this output, there is a Boolean named xdm_sysadm_login. XDM is a display manager, which means it is a tool that enables a user to log in to the system by using a GUI interface. This Boolean is used to determine whether the XDM software will allow the root user to log in. (off, off) is used to display the default value and the current value for this Boolean. In this case, off means the root user is not able to log in using the GUI interface because the description for this Boolean is “Allow xdm to sysadm login.”

You can also use the **getsebool** command to display just the current value of a Boolean:

```
# getsebool -a | head
xdm_sysadm_login --> off
abrt_handle_event --> off
abrt_upload_watch_anon_write --> on
antivirus_can_scan_system --> off
antivirus_use_jit --> off
auditadm_exec_content --> on
authlogin_nsswitch_use_ldap --> off
authlogin_radius --> off
authlogin_yubikey --> off
awstats_purge_apache_log_files --> off
```

When a Boolean is provided as an argument, the **getsebool** command gives only that Boolean’s current value:

```
# getsebool xdm_sysadm_login
xdm_sysadm_login --> off
```

To set an SELinux Boolean as either on or off, use the **setsebool** command:

```
# getsebool xdm_sysadm_login
xdm_sysadm_login --> off
# setsebool xdm_sysadm_login 1
# getsebool xdm_sysadm_login
xdm_sysadm_login --> on
```

Provide the argument **0** to turn off a Boolean and **1** to turn on a Boolean.

Note that, by default, the **setsebool** command modifies only the current state of a Boolean. A reboot causes all Booleans to return to their previous status unless the **-P** (for *persistent*) option is used with the **setsebool** command:

```
# setsebool -P xdm_sysadm_login 1
```

The Boolean values are typically a bit lengthy and a pain to type. Commands like **setsebool** and **getsebool** provide a unique tab completion feature. For example, note the behavior of the following when the **Tab** character is pressed:

```
# setsebool samba_<tab>
samba_create_home_dirs           samba_portmapper
samba_domain_controller           samba_run_unconfined
samba_enable_home_dirs           samba_share_fusefs
samba_export_all_ro                samba_share_nfs
samba_export_all_rw
```

#### SELinux Contexts

Just how does SELinux protect files (and directories) from unauthorized use? The answer is by using [SELinux contexts](#ch12.xhtml_key14-a).

Each file can have a context applied that will affect the ability of a process to access the file. Processes themselves have an SELinux context applied, and this context essentially places the processes in a security group.

Each process runs with a security context. To see this, use the **-Z** option to the **ps** command as shown here (where the **head** command is used simply to limit the output of the command):

```
# ps -eZ | grep httpd | head -2
system_u:system_r:httpd_t:s0 root      1109     1  0  2022 ?
  00:51:56 /usr/sbin/httpd
system_u:system_r:httpd_t:s0 apache    1412  1109  0 Dec24 ?

  00:00:09 /usr/sbin/httpd
```

The security context (**system_u:system_r:httpd_t:s0**) is complicated, but for understanding the basics of SELinux, the important part is **httpd_t**, which is like a security group or domain. As part of this security domain, the **/usr/sbin/httpd** process can only access files that are allowed by the security policy for **httpd_t**. This policy is typically written by someone who is an SELinux expert, and that expert should have proven experience regarding which processes should be able to access specific files and directories on the system.

Files and directories also have an SELinux security context that is defined by the policy. To see a security context for a specific file, use the **-Z** option to the **ls** command:

```
# ls -Z /var/www/html/index.xhtml
unconfined_u:object_r:httpd_sys_content_t:s0
/var/www/html/index.xhtml
```

Note here that the SELinux context contains so much data that the filename cannot fit on the same line. As you might be able to conclude, a process running with the security context **system_u:system_r:httpd_t:s0** is able to access files that have been labeled with the **u:object_r:httpd_sys_content_t:s0** context. It isn’t always so simple as SELinux Booleans can have a major impact on how contexts are applied, but this is essentially the idea. Remember that you don’t need to be an SELinux expert for the Linux+ exam (which is a good thing because it is a very large topic).

How did the context of **u:object_r:httpd_sys_content_t:s0** get applied to the **/var/www/html/index.xhtml** file? Typically, SELinux security contexts are applied automatically, depending on where the file is placed. So, a new file placed in the **/var/www/html** directory would also be labeled with the context **u:object_r:httpd_sys_content_t:s0**.

In some cases, you might need to apply this context manually. For example, if you were to move a file from another location, it might retain its original security context. In such cases, use the **chcon** command to change the context of a file or directory:

```
# chcon -t user_home_t /var/www/html/index.xhtml
```

You can also take advantage of the SELinux rules that define the default security contexts for a majority of the system files. The **restorecon** command is used to reset the default security context on a file or directory based on its current location and these SELinux rules. Here is an example:

```
# restorecon /var/www/html/index.xhtml
```

A commonly used option to the **restorecon** command is the **-R** option, which performs the changes recursively on a directory structure.

#### The audit2allow Command

The **audit2allow** command exists to parse the log files for events where the system has disallowed an access or permission for some action, and very handily to then create a little snippet of policy rule that specifically allows that particular action or access.

You still have to load the snippet into the current policy and ensure it's active, but this is a HUGE timesaver for SELinux administrators who are facing some tiny but important access issue.

Note

As noted in the documentation, you should be very careful when you use the snippets audit2allow produces, they are not to be implemented lightly, make sure you are not accidentally enabling some sort of security risk with these possible additions to the policy.

#### AppArmor

[AppArmor](#ch12.xhtml_key17-a) is a MAC system that plays a role similar to SELinux in that it provides a context-based permission model. This section describes the key components of AppArmor that might be tested on the Linux+ exam.

Note

This chapter provides less information on AppArmor than on SELinux. There are a few reasons for this:

![Images](graphics/square.jpg) As a MAC, AppArmor’s concepts are similar to those of SELinux.

![Images](graphics/square.jpg) SELinux tends to be used much more often than AppArmor. While there are a few Linux distributions that use AppArmor as the default MAC, it is primarily SUSE that uses AppArmor.

![Images](graphics/square.jpg) SELinux is emphasized more strongly in the Linux+ exam objectives than AppArmor.

##### aa-disable

An [AppArmor profile](#ch12.xhtml_key18-a) is a rule set that describes how AppArmor should restrict a process. It is possible to disable a profile for a specific profile by using the **aa-disable** command. Another technique that is commonly used is showed in the following example:

```
# ln -s /etc/apparmor.d/usr.sbin.mysqld /etc/ apparmor.d/disable
#  apparmor_parser -R /etc/apparmor.d/usr.sbin.mysqld
```

Note

To view the status of a profile, use the **aa-status** command. To enable a profile again, use the following commands:

```
# rm /etc/apparmor.d/disable/usr.sbin.mysqld
#  apparmor_parser -r /etc/apparmor.d/usr.sbin.mysqld
```

##### aa-complain

If you need to troubleshoot an AppArmor profile, it is best to put it into complain mode. In this mode, no restrictions are enforced, but any problems will be reported.

Use the **aa-complain** command to put a profile into complain mode:

```
#  aa-complain /usr/sbin/mysqld
Setting /usr/sbin/mysqld to complain mode.
```

To put the profile back into enforcing mode, use the following command:

```
#  sudo aa-enforce /usr/sbin/mysqld
Setting /usr/sbin/mysqld to enforce mode
```

##### aa-unconfined

Use the **aa-unconfined** command to list processes that are not restricted by the AppArmor profiles.

![Images](graphics/key_topic_icon.jpg)

##### /etc/apparmor.d/

The **/etc/apparmor.d** directory is the location of the definitions of the AppArmor profiles. Knowing how to create or read these files is beyond the scope of the Linux+ exam, but it is important to know the locations of these profiles in order to determine which profiles are available and to use the AppArmor commands, such as the **aa-disable** command.

##### /etc/apparmor.d/tunables

The **/etc/apparmor.d/tunables** directory holds files that can be used to fine-tune the behavior of AppArmor. Knowing how to create or read these files is beyond the scope of the Linux+ exam.

### Command-line Utilities

The Linux+ Objectives make a big deal out of this section, like you could ever extract just the command-line utilities and list them out, and have it be useful?

As we warned you at the beginning of this chapter, we have put all our commands into the normal flow of the discussion of the topics, so we will just note that here and move on.

### Summary

The focus of this chapter was how to further secure your system resources using special permissions, context-based access controls like SELinux and AppArmor and all the different utilities that support these actions.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 12-2](#ch12.xhtml_ch12tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 12-2**–Key Topics for [Chapter 12](#ch12.xhtml_ch12)

![Images](graphics/12tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[Permissions](#ch12.xhtml_key01)

[Attributes](#ch12.xhtml_key02)

[Access Control Lists](#ch12.xhtml_key03)

[User Owner](#ch12.xhtml_key04)

[Group Owner](#ch12.xhtml_key05)

[chmod](#ch12.xhtml_key06)

[chown](#ch12.xhtml_key07)

[chgrp](#ch12.xhtml_key08)

[umask](#ch12.xhtml_key09)

[Octal Mode](#ch12.xhtml_key10)

[Symbolic Mode](#ch12.xhtml_key11)

[Special Permissions](#ch12.xhtml_key12)

[SELinux](#ch12.xhtml_key13)

[SELinux Contexts](#ch12.xhtml_key14)

[SELinux Modes](#ch12.xhtml_key15)

[SELinux Policy](#ch12.xhtml_key16)

[AppArmor](#ch12.xhtml_key17)

[AppArmor Profile](#ch12.xhtml_key18)

[lsattr](#ch12.xhtml_key19)

[chattr](#ch12.xhtml_key20)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** What type of access does the execute permission for directories provide?

**a.** The ability to list filenames in a directory

**b.** The ability to add files to a directory

**c.** The ability to remove files from a directory

**d.** The ability to change into a directory

**2.** Consider the following output of the **ls -l** command:

-rw-rwxr-x 2 ross users 0 Jan 26 13:08 22 test.mp3

Which of the following statements is true?

**a.** The user ross has only read permission on **test.mp3**.

**b.** The user ross has only read and write permission on **test.mp3**.

**c.** The user ross has read, write, and execute permission on **test.mp3**.

**d.** The user ross has no permission on **test.mp3**.

**3.** Which of the following are SELinux contexts applied to? (Choose all that apply.)

**a.** Files

**b.** Users

**c.** Processes

**d.** All of these answers are correct.

**4.** In which mode is SELinux not functional at all?

**a.** Permissive

**b.** Disabled

**c.** Inactive

**d.** Null

**5.** Which of the following commands can be used to set or alter the filesystem attributes that are attached to a file or directory?

**a.** auditdisplay

**b.** SEperms

**c.** cfgobject

**d.** chattr

**6.** As a systems administrator, you have discovered a file on disk that won't allow you to delete it, change it's permissions, read it's contents or just about anything else you try. Which of the following commands will allow you to view the special settings for this file?

**a.** displayattr

**b.** vimattr

**c.** lsattr

**d.** cfgattr

## III: Scripting, Containers and Automation (Obj. 3.1 - 3.5)

## Chapter 13\. Automating Tasks via Shell Scripting [This content is currently in development.]

**This content is currently in development.**

## Chapter 14\. Performing Basic Container Operations

This chapter covers the following topics:

• [Container Management](#ch14.xhtml_ch14lev1sec03)

• [Container Image Operations](#ch14.xhtml_ch14lev1sec04)

The exam objectives covered in this chapter are as follows:

• **Objective 3.2:** Given a scenario, perform basic container operations.

In this chapter we'll look not just at what the Objectives demand we do, but we'll work our way through a typical testing environment setup, pulling and running images, configuring them and querying for more information on those images and running instances.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 14-1](#ch14.xhtml_ch14tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 14-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/14tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** A Container is based on a __________? Choose the best answer.

**a.** Repository

**b.** Pod

**c.** Image

**d.** Scope

**2.** What must you do with a container image before you can list it?

**a.** Inspect it

**b.** Scope it

**c.** Download it

**d.** Build it

**3.** What keystrokes are used together to disconnect from a running container? Choose all that apply.

**a. Ctrl-q**

**b. Ctrl-c**

**c. Ctrl-z**

**d. Ctrl-s**

**e. Ctrl-p**

**4.** You need to see the latest log entries from the most recently executed container, which command would you use?

**a.** podman logs -T

**b.** podman logs

**c.** podman logs -a

**d.** podman logs -l

**5.** Which of the following can you push a container image to? Choose all that apply.

**a.** Public Repository

**b.** Private Repository

**c.** Portal Repository

**d.** Primary Repository

**6.** You have multiple identically-named images in your local storage, which option to the podman **rmi** command would allow you to remove those identically-named images?

**a. -f**

**b.** -x

**c.** -z

**d.** None of the answers are correct.

### Foundation Topics

Working and managing containers can be a complex topic, so rather than try to have you visualize what all this may mean, we'll work from the beginning of one of my favorite demos all the way to the end, and cover all the topics while we go along. It'll be more instructive that way, and flows better. At the time of this writing, if you use the commands and images I have here, it should all work well for you!

Note

As we have done in so many chapters, we will use our own order and highlight the most important items in our own preferred way, never mind the order or grouping that the Linux+ Objectives put them in.

### Container Management

Managing [containers](#ch14.xhtml_key02-a) is more important now that we can run local root-less container scenarios, making it much easier for developers and system engineers to test changes without having to port everything off to a cloud instance somewhere.

#### Install and Verify the Container Tools

The first thing you need to know is how to install the container tools that will be needed.

##### Install the Container-tools Package and Dependencies

You can start with a simple clean install, say of Red Hat Enterprise Linux, and to install the container tools, you'd use:

```
# sudo yum module install container-tools
```

The install process will ask you if you'd like to install the container tools and a fair amount of dependencies, so answer "**y**" for yes and allow the install to finish.

[Figure 14-1](#ch14.xhtml_ch14fig01) shows the ending of this process and the query to which you'd answer yes to.

![Description: A picture containing graphical user interface Description automatically generated](graphics/14fig01.jpg)

**Figure 14-1**–Installing the container tools packages

##### Verify the Podman and Skopeo Tool Installation

You can verify that the [podman](#ch14.xhtml_key04-a) and skopeo tools are installed by inspecting the output, which should be similar to what you see in [Figure 14-2](#ch14.xhtml_ch14fig02).

![Images](graphics/14fig02.jpg)

**Figure 14-2**–Verifying the installation of the container-tools packages

However, a far easier method of doing this than reading through all that output is to see if they are found in the path with the command:

```
# which podman skopeo
/usr/bin/podman
/usr/bin/skopeo
```

#### Finding and Pulling a Container Image

Everything in containers comes from images, so we'll have to find some to work with first.

##### Find a Suitable Image

Next we'll look for an image that will work for our purposes, which can be a little difficult, given the amount of possible images in the repository.

Search for the UBI or Universal Basic Images for RHEL 8 with the command:

```
# podman search registry.access.redhat.com/ubi8 | wc -l
26
```

Instead of boring you with a listing of all 26 of the images, we just had them counted by the **wc** command. Since 26 is still a LOT of images to select from, so let's make it easier and further focus our output with the command:

```
# podman search registry.access.redhat.com | grep -i latest

```

This will display the listing of available "latest release" images, which may also include previous and later versions such as RHEL 7 and RHEL 9, similar to what is shown in [Figure 14-3](#ch14.xhtml_ch14fig03):

![Images](graphics/14fig03.jpg)

**Figure 14-3**–Finding the latest UBI image

You can see that the latest generic image is simply notated as **/ubi**, and we'll use that one in our demonstration.

To see more information about the **/ubi** image, you should be using the **skopeo** command. There is a LOT of information contained in a, well, [container image](#ch14.xhtml_key03-a), so we'll pipe the output from **skopeo** to the **grep** command, using the context parameter (-A 1) to just show the description line, which you'll see the results of in [Figure 14-4](#ch14.xhtml_ch14fig04):

```
# skopeo inspect docker://registry.access.redhat.com/ubi8/ubi
| grep -i -A 1 \"description\"
```

![Images](graphics/14fig04.jpg)

**Figure 14-4**–Displaying the container image description

##### Pulling an Image

![Images](graphics/key_topic_icon.jpg)

Next we'll pull the image from the repository using the **podman pull** command:

```
# podman pull registry.access.redhat.com/ubi8/ubi:latest
Trying to pull egistry.access.redhat.com/ubi8/ubi:latest...
Getting image source signatures
Checking if image destination supports signatures
Copying blob 0c673eb68f88 done
Copying blob 028bdc977650 done
Copying config 2fd9e14788 done
Writing manifest to image destination
Storing signatures
2fd9e1478809c0c53820517b998e1b2a044207515e5d61eccb6295276bb
baffc
```

As you can see, the image was pulled from the repository, and the extremely long signature of the image is now stored locally.

Note

The **IMAGE ID** column shows the Image's ID, which is something we'll use to control the image as we start it or otherwise interact with it as an image. You'll see the similar length Container ID numbers shortly, those are how we control and manage running containers. You'll want to keep these two firmly in mind when answering Image and Container-related questions on the exam.

#### View and Inspect Images

It's not enough to just pull an image, it must be inspected to ensure it's the correct code.

##### Viewing Local Images

![Images](graphics/key_topic_icon.jpg)

Once an image has been pulled, you can inspect it several ways, the first being to see if it's listed on your host by running:

```
# podman images
REPOSITORY                          TAG    IMAGE ID  CREATED
SIZE
registry.access.redhat.com/ubi8/ubi latest 2fd9e1478809 3 week
225MB
```

You may notice that the Image ID is much shorter in this listing, that is because it's being truncated, showing now as the first 12 characters of the much longer ID.

Note

You'll want to take notice that the Container Image ID will stay the same over time as you work with it, it's the one that identifies this image overall, and shouldn't change unless the registered image on the repository changes. However, the running Container ID should be different each time you run it, and definitely different between running Container instances. Watch for this difference on the exam.

##### Inspecting a Local Image

You can find out much more about the image now by using the **podman inspect** command with the short IMAGE ID as a parameter:

```
# podman inspect 2fd9e1478809
```

There's no need to show the output of this command, it's essentially the same as what you saw displayed with the **skopeo** command output we fed to the **grep** command above. This proves it's the same image we queried previously, while it was still in the repository.

#### Running and Attaching/Detaching to Containers

In this section we show you how to properly connect and detach from containers, leaving them running and functional.

##### Running an Image as a Container

Now for the part you've been expecting, we'll run the image by specifying the **-i** (interactive) and **-t** (attach pty to the terminal) parameters, which allows us to immediately access and use the command line inside the now-running container.

![Images](graphics/key_topic_icon.jpg)

Let's start the instance with the command:

```
# podman run -i -t 2fd9e1478809
```

The only visual indication that something is different is the prompt will change to something that indicates the host you are now at the shell prompt on, such as:

```
[root@ 35c54f588bbc /]#
```

You can verify that you are on a different host either by running an **ls** command and looking at the files in the home directory, or perhaps checking the host release information with the command:

```
[root@ 35c54f588bbc /]# cat /etc/redhat-release
Red Hat Enterprise Linux release 8.6 (Ootpa)
```

##### Assigning a Container Friendly Name

A name can be associated with a Container ID by specifying the friendly name you want at the time of instance creation:

```
# podman run -it --name OpenContainer 2fd9e1478809
[root@ 35c54f588bbc /]#
```

You can also rename a container very easily, just use the rename instead of name commands:

```
# podman run rename OpenContainer ClosedContainer
```

##### Detaching and Attaching to Containers

If you have run a container with the **-it** options to give you immediate access on the shell prompt to it, it might be a surprise when you type the **exit** command to get out of the container and it also QUITS the container!

![Images](graphics/key_topic_icon.jpg)

In order to detach from a running container that you are attached to, the keystrokes are, in close succession:

```
Ctrl-p Ctrl-q
```

This will detach you from the container, and leave it running. You can verify it's still running with the **podman images** command:

```
# podman images
CONTAINER ID  IMAGE                          COMMAND
CREATED             STATUS                    PORTS
NAMES
35c54f588bbc  registry.access.redhat.com/ubi8/ubi:latest
/bin/bash   About 5 minutes ago  Up 5 minutes ago
compassionate_chatelet
```

Note

I'm truly sorry for the horrible formatting that we are forced to use in showing the very long images and **ps -a** command output, there's literally no way to show it all on one line unless it's about 4 pts in size, and then you can't read it. This will make much more sense when you type the commands and follow along with this chapter and demonstration on your own virtual machine.

The only visual indication that something is different is the prompt will change to something that indicates the host you are now at the shell prompt on the container, so pay close attention!

##### Exiting and Ending Execution of a Container

To exit from an interactive session and also terminate the execution of the container, at the command prompt, type:

```
# exit
```

You can then make sure the container has exited by inspecting the status of the container processes with:

```
# podman ps -a
CONTAINER ID  IMAGE               COMMAND     CREATED
STATUS                    PORTS       NAMES
35c54f588bbc  redhat.com/ubi8/ubi:latest  /bin/bash   About
a minute ago  Exited (0) 6 seconds ago    infallible_khayyam
```

Note

Remember that we will see a Container ID in the **CONTAINER ID** column, and that's how we interact with a running or exited container, not using the Image ID.

##### Removing a Container

Remembering that a container image becomes a Container when it's run or executed, we'll use that Container's ID to remove it from the host's table of existing Containers with:.

```
# podman rm 35c54f588bbc
35c54f588bbcb8acddbda95dfe91f02c553f211421fd7149a01729e0639
c6379
```

The display of the full Container ID confirms the removal of the Container from the host's list.

Verify the Container was removed with the command:

```
# podman ps -a 
CONTAINER ID  IMAGE  COMMAND  CREATED  STATUS  PORTS  NAMES
```

Now that the Container has been removed, you can either use the Container Image to start another running Container, or remove that Container Image from your system with the podman command and it's subcommand **rmi**:

```
# podman rmi 2fd9e1478809
Untagged:registry.access.redhat.com/ubi8/ubi:latest
Deleted:2fd9e1478809c0c53820517b998e1b2a044207515e5d61eccb6
295276bbbaffc
```

Your host should now not show that Container Image if you use the podman **images** command again:

```
# podman rmi 2fd9e1478809
REPOSITORY  TAG         IMAGE ID    CREATED     SIZE
```

##### Viewing Container Logs

![Images](graphics/key_topic_icon.jpg)

Working with container logs is done by using the podman command logs, followed by the container ID:

```
# podman logs 35c54f588bbc
This was a logger test entry
```

The command accepts the Container ID of the Container you want to query the main log entries for, or if you are just looking to see what the latest log entries are for your most recently-started container, (-1 or lower-case L), use the command:

```
# podman logs -l
This was a logger test entry
```

Note

You may also wish to investigate the podman **events** command, and compare and contrast it with the podman **logs** command.

##### Exposing and Mapping Ports

Ports are not automatically available to the host from a container, you have to expose them, typically at the inception of the container, which makes them available for contacting, such as the NGINX container shown in the following that we have exposed port 80 on, with the command:

```
# podman run --expose=80 --publish-all
registry.access.redhat.com/rhscl/nginx-16-rhel7 &
```

This will run the image mentioned (an NGINX 1.7 image) as a container, and expose port 80, then publish all of it's exposed ports to the host. The **&** suffix is to set the process to execute in the background.

OR, we can also map a container port, such as the 8080 port on this NGINX container, to a specific port on the host using the command:

```
# podman run -d -p 8080:80
registry.access.redhat.com/rhscl/nginx-16-rhel7
```

You can then view the exposed ports using two methods, the first running just a **podman** subcommand named **port**, as in:

```
# podman port -a
52ee615ae4b7     80/tcp -> 0.0.0.0:8080
ae054514e8f6     80/tcp -> 0.0.0.0:36319
ae054514e8f6     443/tcp -> 0.0.0.0:44783
```

Notice that the Container starting with "ae" has an entry per port, showing the numbers and where they mapped to on the host.

The other and slightly longer or more explicit set of information can be gotten by using the command:

```
# podman ps -a
CONTAINER ID  IMAGE
COMMAND               CREATED         STATUS
PORTS                                          NAMES
ae054514e8f6
registry.access.redhat.com/rhscl/nginx-16-rhel7:latest
nginx -g daemon o...  32 seconds ago  Up 31 seconds ago
0.0.0.0:36319->80/tcp, 0.0.0.0:44783->443/tcp
optimistic_archimedes
52ee615ae4b7
registry.access.redhat.com/rhscl/nginx-16-rhel7:latest
nginx -g daemon o...  6 seconds ago   Up 6 seconds ago
0.0.0.0:8080->80/tcp
infallible_easley
```

Either way you can see that the ports are exposed in the case of the `ae054514e8f6` container, and mapped in the case of the `52ee615ae4b7` container.

##### Summary

This ends the demonstration or labs-centric portion of this chapter, next will be the Container Image Operations references and explanations.

### Container Image Operations

There are some other commands and concepts that are listed on the objectives, but are more related to the maintenance of your images, which we'll cover in more than sufficient detail here.

#### build

Building a container with Docker typically required root-level access, but now Podman and [Buildah](#ch14.xhtml_key05-a) (a tool Podman uses) allow even regular users to build an image without additional access.

There's a lot of complex information that we won't go into, you need to know the concept of what happens when you want to build a container image, not all the gory details. I do highly recommend the excellent Red Hat documentation: "Building, Running and Managing Containers" available on their documentation resource sites.

Whether you're using Docker and building from a Dockerfile, or using Buildah and either a ContainerFile or an image you want to use as a base for your new image, it's roughly the same concepts.

We won't focus on the limitations, its not necessary to the task of explaining what is going on with building a container image.

When you issue the **podman build** command, the tool that is being used under the covers is named **buildah**.

Here's how it works:

1\. Create a Containerfile

2\. Create a script to run as a test

3\. Set the permissions of the script

4\. Build the image with the **buildah** command

5\. Verify the image with the **buildah images** command

6\. Run the image with the **podman run** command

#### push

Pushing an image is the process of sending it from your local storage to either a public repository, or even, a private repository you maintain or use.

Pushing to a private registry is not hard, you can create one on your system using the podman command with it's registry subcommand and some parameters.

Once the repository is created, you can use the **buildah push** command to send the image to the registry, including the source signatures and manifest that causes it to be listed as part of the repository.

You can then verify the registry properly contains the image with the **curl** command, it will display the listing showing the image exists.

#### pull

![Images](graphics/key_topic_icon.jpg)

Pulling an image is the process of retrieving an image from a public or private respository, very easy if the repository is open, and only slightly less easy if you have the proper authentication for the repository. Pulling images was covered in the demonstration in the earlier part of this chapter.

#### list

Listing an image or images requires you to have pulled or otherwise have local storage for the images. Use the **podman images** command to list local images your system knows about.

#### rmi

![Images](graphics/key_topic_icon.jpg)

The podman **rmi** command is how you remove an image or images from your system's knowledge, but it requires those images to be stopped, so issue the podman **stop** command to stop the running container and allow the image that underlies it to be removed.

Additionally, you'll find that you can remove all the images from your local storage using the podman **rmi -a** command.

If you have multiple images with the same name, or wish to use what amounts to a "force" option, you can use the podman **rmi -a -f** command.

### Summary

In this chapter we worked you through one of my most favorite demonstrations I do, and taught you all about Containers and Container operations at the same time!

You know now how to install the container-tools package, pull images, list them, start and stop them, connect and disconnect to them, how they do logging and how ports are exposed and also mapped.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 14-2](#ch14.xhtml_ch14tab2) lists these key topics and the page number on which each is found.

**Table 14-2**–Key Topics for [Chapter 14](#ch14.xhtml_ch14)

![Images](graphics/14tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

Pod

[Container](#ch14.xhtml_key02)

[Container Image](#ch14.xhtml_key03)

[Podman](#ch14.xhtml_key04)

[buildah](#ch14.xhtml_key05)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** While executing or starting a container from an image, you want to immediately execute commands from the shell prompt as if you had ssh'ed to the container, which option/options should you specify at the start of the container to allow this??

**a.** -in

**b.** -it

**c.** -if

**d.** -ssh

**2.** You have started a container and not used the interactive or tty options, how may you connect to that container? Choose the podman subcommand that will accomplish this.

**a.** connect

**b.** ssh

**c.** attach

**d.** pipe

**3.** When listing images, containers and processes, you have noticed that one of them stays consistent throughout all operations, while the others seems to change each time. Which one of the ID's stays consistent?

**a.** Container ID

**b.** Process ID

**c.** Image ID

**d.** None of the above

**4.** To inspect the logs for a given container, which podman subcommand would you use?

**a.** event

**b.** logs

**c.** logger

**d.** syslog

**5.** When building a container, what two components are the most likely to be used to create that new container? Choose Two.

**a.** buildah

**b.** skopeo

**c.** Containerfile

**d.** Histsize

**e.** Manifest

**6.** Your organization has ceased it's use of Docker, and instituted another set of tools to manage root-less containers for it's developer staff. Which of the following is the most likely tool for this task?

**a. Walkabout**

**b. Podman**

**c. ContainerCrew**

**d. Virtualtool**

## Chapter 15\. Perform Basic Version Control with Git [This content is currently in development.]

**This content is currently in development.**

## Chapter 16\. Understanding Infrastructure as Code

This chapter covers the following topics:

• [File Formats](#ch16.xhtml_ch16lev1sec03)

• Utilities

• [Continuous Integration/Continuous Deployment](#ch16.xhtml_ch16lev1sec05)

• [Advanced Git Topics](#ch16.xhtml_ch16lev1sec06)

The exam objectives covered in this chapter are as follows:

• **Objective 3.4:** Summarize common infrastructure as code technologies.

This chapter is all about how today's infrastructure is mostly expressed and configured in code, be it YAML or JSON, how you can use the available Infrastructure Automation options to build, test and deploy your applications and projects, how Continuous Integration and Continuous Integration and their components help you do that without undue manual efforts and how to understand a couple of more advanced Git options such as merge, rebase and Pull Requests.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 16-1](#ch16.xhtml_ch16tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 16-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/16tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** Which of the following is NOT a characteristic of the JSON data definition?

**a.** Hyphens

**b.** Spaces

**c.** Comments

**d.** Periods

**2.** Which of the following is NOT a characteristic of the YAML data definition?

**a.** Tabs

**b.** Spaces

**c.** Hyphens

**d.** Periods

**3.** When working with Ansible, you create lists of tasks that will be executed on a set of hosts. What are these lists commonly and typically called in the Ansible world?

**a.** Recipes

**b.** Taskers

**c.** Formats

**d.** Playbooks

**4.** When using an Infrastructure as Code tool, you notice that it causes you to work in three main stages: 1) Code, 2) Plan, and 3) Apply. Which IaC tool are you almost certainly using?

**a.** Terraform

**b.** Puppet

**c.** Chef

**d.** Ansible

**5.** Which of the following are reasonable use cases for a Continuous Integration/Continuous Deployment scenario? Choose all that apply.

**a.** Gaming Application

**b.** Financial Services

**c.** Asynchronous Transfer Mode

**d.** Social Media Site

**6.** What does the CD portion of the CI/CD Acronym stand for? Choose two.

**a.** Continuous Development

**b.** Continuous Deployment

**c.** Continuous Defense

**d.** Continuous Delivery

**7.** What is the main difference between a git merge and a git rebase?

**a.** The status of all future changes

**b.** The status of all previous pull requests

**c.** The status of all current branches

**d.** The status of all previous commits

### Foundation Topics

### File Formats

Infrastructure as Code can be defined as the process of visualizing, designing, testing, revising, implementing, running, troubleshooting, and managing your project or companies infrastructure through the medium of code.

#### YAML Ain’t Markup Language

YAML is a data serialization language that is sued to store a text-based representation of objects, or object state. YAML is mainly used for configuration files with a stanza-based format of hierarchical items and is imminently human friendly and readable.

YAML also allows for a larger feature set, as well as the ability to include comments for documentation and clarity. A set of information in YAML is known as a "stream," and there can be multiple streams in a given YAML file.

##### Key Characteristics of YAML

![Images](graphics/key_topic_icon.jpg)

YAML has a certain set of identifying characteristics that distinguish it from other data-serialization languages or scenarios, those include:

• Typically begin with the use of 3 hyphens such as ---.

• T Typically end, or show end of stream with 3 periods such as ...

• T Uses whitespace indentation for structure, spaces only, NO tabs.

• T Comments are started by a # character, continue to EOL, except inside of a string, where they are a literal.

• T Lists (regular) are denoted by preceeding with a - character and are 1 entry per line. An list can also be shown inline as [item1,item2,item3].

##### YAML Stream Examples

You can display items in a list in YAML in a couple of ways, first the normal or regular method which is more obviously a list, but takes a LOT of vertical space to render:

**---** *# Favorite Bands*

- The Psychedelic Furs

- Accept

- Dokken

- Marty Friedman

- Motorhead

This list can also be represented in the inline fashion like:

**---** # *Favorite Bands*

[The Psychedelic Furs, Accept, Dokken, Marty Friedman, Motorhead]

Note

A good friend and fellow instructional designer likes to wear his t-shirt at the office that proclaims:

```
 Yaml:
      - Y: Yelling
        - A: At
        - M: My
        - L: Laptop
```

Just a little humor, but also a good visual aid if you are slightly lost and someone wanders into your office wearing it.

#### JSON Bourne

JSON is used as a way to serialize data. JSON stands for JavaScript Object Notation. It’s simpler in format than YAML and can be used to conduct data exchange and transfer between APIs and their requesting applications or services.

JSON is a subset of YAML, and it can be parsed with a YAML interpreter or parser, so you can use YAML and JSON together for your templating needs.

JSON is also primarily recognizable by the fact that all the keys and values in JSON are enclosed in "double quotes."

Your author spent a couple of years working with AWS Cloud Formation templates that were mostly expressed in JSON, and I don't miss it much, all those damned quotes all over the data and just let you get one un-matched double quote and NOTHING WORKS!

##### Key Characteristics of JSON

![Images](graphics/key_topic_icon.jpg)

JSON has a certain set of identifying characteristics that distinguish it from other data-serialization languages or scenarios, those include:

• T Stanzas begin with the left curly bracket {and end with the right curly bracket }.

• T Typically the JSON statement begins with the top and left-most { and ends with the bottom and left-most } character.

• T Allows the use of tabs and spaces, carriage returns and linefeeds as structural tools.

• T There are NO comments allowed.

• T Lists are defined by a string in double quotes followed directly by a colon character, then a space left square bracket, the data on a new line indented and ending with semi-colons, and finally finished off with a right square bracket on a new line.

##### JSON Examples

JSON often gets used to define different types of objects, such as the following object used to describe a particular band, as we have in [Example 16-1](#ch16.xhtml_exe16_1):

**Example 16-1 –**Example of JSON formatted data

```
{
  "Favorite Band": {
    "name": "The Psychedelic Furs",
    "Begun": 1977,
    "First Album": "The Psychedelic Furs",
    "Soundtrack Credits": "Pretty in Pink, 1986",
    "photo": " https://en.wikipedia.org/wiki/File:Psychedelic_Furs.jpg",
        "Albums": [
               "The Psychedelic Furs",
               "Talk Talk Talk",
               "Forever Now",
               "Mirror Moves",
               "Midnight to Midnight",
               "Book of Days",
               "World Outside",
               "Made of Rain"
        }
}
```

We also created an array in [Example 16-1](#ch16.xhtml_exe16_1), the array name is "Albums" and the items in the array are the album names.

I am certain that with the above explanations, definitions and examples of YAML and JSON, you'll be just fine on the exam, you just need to know a reasonable amount about these file formats or rather, data definitions to fulfill the objectives.

The real reason you need to know about them is that you'll encounter them infinitely in the Infrastructure as Code world, for all kinds of configuration and data storage uses.

### Infrastructure as Code Concepts

[Infrastructure as Code (IaC)](#ch16.xhtml_key04-a) can be defined as the process of visualizing, designing, testing, revising, implementing, running, troubleshooting, and managing your project or companies infrastructure through the medium of code.

Note

The phrase "code" in the Infrastructure as Code refers not to C, C++, C#, Assembly or Java etc. coding languages, but the use of text files that contain the instructions and settings that make a default service perform as you want it to.

Of course, not all the infrastructure is just code, it's the code (actually text in a particular format) that feeds the software configuration, settings and modifications from the default behaviors.

#### Just Making a Config Change

As an example, you can run the NGINX web server with it's default configuration, and make changes via editing the configuration files and restarting the service, but that's not IaC in practice, it's just making a configuration change.

Even the simplest configuration change, given enough scale (or systems to make the change to) will cause you to move to a more manageable method, which IaC is perfect for.

#### Using Source Control

To really be using the IaC concepts, you'd have your configuration files for NGINX as a part of a Git repository, (or other source control) so that you can spool up your service or application, note how it works, make any changes to the IaC files and then redeploy it again, this time with the changes implemented.

If you haven't read [Chapter 15](#ch15.xhtml_ch15), with it's discussion of all things Git, please do, it'll make the more advanced topics for Git at the end of this chapter make a lot more sense.

#### Living the IaC Lifestyle

Living out the IaC dream is not terribly complex, but there are steps that you should consider taking, all of them, that will make your approach more predictable, give you better results and save you time overall.

#### Getting Started with IaC

Do an inventory of everything you want to run with IaC, be it your current (and future desired) applications, back-end services, all the configuration needed for each of those items and every single applications settings, configuration and any of the other files that might make it not work well across multiple systems.

THEN, when the above is done, you'll want to consider the following steps:

1\. Always try to use version control for everything, it makes fixing mistakes as simple as a couple of quick commands and a restart

2\. Automate absolutely everything. Don't do anything manually except make everything automated.

3\. Verify absolute consistency in implementing your IaC. Run it 50 times, should get an identical result, every single time.

4\. Try to make your IaC as modular as possible, so that a change to one section doesn't affect many others just because it's not modular.

5\. Dont' get ridiculous with the modularization, some things belong together.

6\. Do a hundred dry runs, heck, do a thousand, it should all be automated!

7\. Develop a quick but thorough manner with which to test funcationality. Use the **curl** command to get a result back from a service, that's a primary way, maybe not even show the output, but just output a "success" if it works!

Next up we'll talk about the tools that you can use to make this more automated and actually cause a given state to be not only created, but maintained in some instances.

#### Infrastructure as Code Utility Philosophy

IaC utilities are not quite a dime-a-dozen these days, but there are an increasing number of them out there, which is both a good and bad thing. It's a good thing because you can shop around and find the tool that suits your and your organization's needs, but maybe the number of tools and philosophies that go along with them can be confusing.

The most important concept about IaC tools is; are the tools functional or procedural.

• **Functional:** Also known as the Declarative Approach, Functional focuses on what the actual configuration of the targeted unit should be. This is not a complete list of exactly how to get there, but more of a declaration of intent or the finished state.

• **Procedural:** Also know as the Imperative Approach, Procedural is the aforementioned set of steps and commands that need to be run or executed so that you get to the results you are looking for.

#### IaC Utility Choices

Let's cover these in order, they're all great, but each has it's own characteristics that make it unique, which we'll note.

Note

The Linux+ objectives don't mention all of the choices, but we will focus on those they do mention and will be on the exam.

#### Ansible

Red Hat is the developer of Ansible and it was created in order to make things easier for the things they needed to do, and Red Hat is a good place to come up with something innovative, it's a great place to make something have a good reach for the rest of the community.

[Ansible](#ch16.xhtml_key06-a) is a suite of IaS open source tools that deal with automation of provisioning, deployment, and config management.

![Images](graphics/key_topic_icon.jpg)

Ansible is arguably simple to use, (maybe the simplest of the options) and flexible enough to do most if not all of what you'd want to do with your systems and application environment. Ansible uses [playbooks](#ch16.xhtml_key12-a), which are how you define (in code!) what you want to happen as far as creating the infrastructure you want, or enabling the final state that you desire.

The Ansible documentation is excellent, and in the following, I've included an example of an Ansible Playbook in [Example 16-2](#ch16.xhtml_exe16_2):

**Example 16-2**–Example Ansible Playbook

```
---
- name: Update web servers
  hosts: webservers
  remote_user: root

  tasks:
  - name: Ensure apache is at the latest version
    ansible.builtin.yum:
      name: httpd
      state: latest
  - name: Write the apache config file
    ansible.builtin.template:
      src: /srv/httpd.j2
      dest: /etc/httpd.conf

- name: Update db servers
  hosts: databases
  remote_user: root

  tasks:
  - name: Ensure postgresql is at the latest version
    ansible.builtin.yum:
      name: postgresql
      state: latest
  - name: Ensure that postgresql is started
    ansible.builtin.service:
      name: postgresql
      state: started

```

In [Example 16-2](#ch16.xhtml_exe16_2), you see the simplicity of an Ansible playbook, where each line is about as obvious as it can be as to what it does.

For example, the - name defines a section, such as "Update web servers," defines the "hosts: webservers" and the user this should be done as with "remote_user: root".

Once the hosts and user have been defined, the "tasks:" section contains a couple of sets of instructions, one making sure that Apache (httpd) is updated to the latest version and then the next set of instructions uses Ansible's ability to complete file actions by copying the source file from /srv/httpd.j2 to the desired destination of /etc/httpd.conf.

The rest of the playbook follows the same simplistic and very readable format that is so characteristic of Ansible.

#### Puppet and Chef

It's not really possible to talk about Puppet with out talking about Chef as well. They are possibly the oldest of the utilities, or configuration managers, as they were called before we came up with all the fancy buzzwords such as Infrastructure as Code.

##### Puppet

![Images](graphics/key_topic_icon.jpg)

[Puppet](#ch16.xhtml_key08-a) is a declarative utility, as mentioned earlier in this chapter, a declarative tool basically describes the state you want something to be in, but leave the actual steps to other tools. Puppet's configuration is constructed in JSON or YAML, contained in simple text files.

Puppet users should be comfortable with JSON and YAML and editing configuration files, but it's not really programming, nor do you need that skill to be competent and work with Puppet.

##### Chef

![Images](graphics/key_topic_icon.jpg)

[Chef](#ch16.xhtml_key07-a) on the other hand, is a great example of an imperative utility, where you can feel free to specify exactly how things will be happening, and what you want the eventual state to be. Chef uses the Ruby Domain Specific Language, or DSL and you have everything available to you that the Ruby language can do.

Chef aggressively uses culinary terms, with [recipes](#ch16.xhtml_key11-a) and cookbooks and the concept of a staging area referred to as a Test Kitchen.

Chef users should be comfortable with Ruby, and programming skills are a big plus, and developers seem to be more comfortable with Chef than anyone else.

##### Why Use One or the Other?

Why do people use one or the other? Sometimes it's tradition, having selected one and mostly sticking with it either because it works so well and is suited to your needs, or sometimes because it's easier to use it than change everything.

#### SaltStack

[Saltstack](#ch16.xhtml_key09-a) is a very interesting utility, it's very featureful and capable, and has been used as the basis for other products such as versions of the SUSE Manager configuration manager and most recently the VMWare vRealize Automation Suite.

Note

SaltStack as a company has been bought by VMWare, and the SaltStack team is now part of the SaltStack team inside VMWare. The Salt Open offering (the SaltStack Open Source project is now called Salt Project, but there are no real differences, it's the same Salt Open or Salt Project you know and love.

##### Salt Architecture

SaltStack in any version is made up of a Master/Minion pairing. The Salt Master (their phrase, not mine) is the server that is the one that manages the Minion systems, essentially the clients.

![Images](graphics/key_topic_icon.jpg)

Salt Masters communicate with the Salt Minions via ports 4505/4506 and it's the ZeroMQ messaging library that manages all of this for Salt.

##### Salt Master Options

SaltStack can run in several manners, depending on your needs:

• **Single Salt Master:** One Salt Master, no backups or failovers, communicating with it's configured Salt Minions.

• **Salt Master Failover:** Two Salt Master Servers, one configured as the live or hot Salt Master, the other as a failover in case the live one fails.

• **Salt Master of Masters:** For those who have more enterprise-friendly or scalable set of Salt Master, you can have a Master of Masters, which has subordinate Salt Masters, each of which governs a set of Minions. (This might be for business divisions, or roles within an organization.)

Additionally, you can use SaltStack in a Masterless manner, where you just load up the Salt Minion on a system, and then use that for development and testing of your Salt States and routines, this should not be normally used for production systems.

Salt Masters are fed by what is known as Salt States, which are text files that end in the .sls extension, and which contain the configuration that is used by Salt to push the Salt State instructions to the Salt Minions where the Salt Modules will perform the needed functions.

##### Salt Configuration Locations

Salt configuration files are typically in the /etc/salt/ directory, initially in the /etc/salt/master and /etc/salt/minion locations. Additionally, the usual .d include directory feature (such as /etc/salt/conf.d) is there, so any additional configuration put there will be read in after the main configuration is parsed.

##### Salt State Files

The Salt File Root is normally located at /srv/salt, and that is where you will put .sls State files.

A [State file](#ch16.xhtml_key10-a) is effectively a set of instructions that is designed to produce a particular "state" to be achieved on the Minion when the Minion gets the state instructions from the Master and runs it through the Remote Execution Modules.

Remote Execution Modules, of which there are MANY, are usually small instruction execution programs that do things like add users to the system, install requested packages, copy files from the Salt Master to the Salt Minion and many many other functions.

An example of how to install and keep NGINX (the best web server!) running is shown in the example state file nginx_inst.xls in [Example 16-3](#ch16.xhtml_exe16_3).

**Example 16-3**–Example of an NGINX state file

```
nginx:
  pkg:
    - installed
  service:
    - running
    - watch:
      - pkg: nginx
      - file: /etc/nginx/nginx.conf
```

What's happening in this state file is relatively simple, let's take it line by line.

• nginx: This is the name of the package or service you want to affect

• pkg: This indicates to the Salt system this is a package, not just a file

• - installed This says to Salt that this package should be installed

• service: Indicates to Salt that this is a system service

• - running This will cause Salt to keep the service running

• watch: This notifies salt to watch or monitor what follows

• - pkg: If the NGINX package is updated, to a restart of the service

• - file: If the nginx.conf file is changed, then initiate a restart

This is more than enough to get you either interested in SaltStack or to be able to easily answer any questions you'll find on the exam.

I recommend going and looking up the SaltStack documentation, or go look at the excellent SaltStack courses that A Cloud Guru (Linux Academy) has on their site, the main SaltStack DevOps instructor there is an excellent teacher, she really breaks things down for you.

#### Terraform

[Terraform](#ch16.xhtml_key05-a) is arguably the newer and more difficult of the many options covered in the Linux+ objectives. There are many people who will tell you how to DO Terraform, but very few who can tell you WHY to choose Terraform over the other more "mentally accessible" IaC options. Let's see if we can get there.

Terraform is the epitome of the Declaritive manner of using IaC, in that you just tell it what you want the result to be, and let the tool take care of how it gets done.

This allows you to focus on architecting your infrastructure, while not getting down in the weeds with every single steps or command that needs to be run to accomplish it.

#### It's as simple as...

![Images](graphics/key_topic_icon.jpg)

There are three main phases of using Terraform, they are:

1\. Code(ing)

2\. Plan(ning)

3\. Apply(ing)

##### Coding

When you are in the Coding phase, you are creating the actual .tf file that contains what you want to have happen. [Figure 16-1](#ch16.xhtml_ch16fig01) shows a desired environment of three elements, a couple of Virtual Machines, each containing an NGINX server and a Kubernetes cluster, networked together.

![Description: Graphical user interface, text, application, chat or text message Description automatically generated](graphics/16fig01.jpg)

**Figure 16-1** Three Element Environment for use in the Coding Phase.

In [Figure 16-1](#ch16.xhtml_ch16fig01), you see the state we are declaring we want to have exist.

The **myenvironment.tf** file would contain the relatively simple instructions that will cause this desired environment Plan to be created by Terraform, telling you what will happen when the last phase happens, that of Applying the instructions and actually generating and creating the environment.

Note

The environment file to create what we have as the outcome is too long to reasonably list here, and goes way beyond the scope of what the Linux+ objectives need us to cover. There are MANY examples of valid and useful Terraform .tf files out there, including from Terraform itself.

##### Planning

When you enter the Plan phase of Terraform, the tool will take your Code or **myenvironment.tf** file and run through and let you know what will happen when it's applied.

This is a very good thing, there's nothing like thinking you've got a good environment setup only to find out that something has gone horribly awry and you're creating 1024 VM's by accident.

To do this, you'll run the **terraform** command with the sub-command plan, which will do the run-through and generate an actual plan file as well as let you know with the output that mirrors what the Plan contains.

##### Applying

The process of applying is to instruct Terraform to take the Plan you have had it generate, and then to Apply the Plan in your infrastructure.

There is a whole lot more to Terraform, all of which is outside of the scope of what we have done here, and the Linux+ Objectives, but at least you now know what it is, and how it works overall.

### Continuous Integration/Continuous Depolyment

Continuous Integration/Continuous Deployment or CI/CD as it is almost always shortened to, (just say that 30 times in an hour class!) is the process of having a continuous dev, fix, test, release process that keeps your code updated and the latest fixed and tested code into production.

#### What's The Problem?

Software and environments have gotten so multi-valued and multi-layered, with dozens to hundreds of different resources in some cases, so not only should you try to automate some of this, you should probably try to automate as much of it as possible, and review it often.

Doing the amount of work in coding doesn't change a lot, but the amount of iterations and their frequency of happening for testing and deployment quickly becomes impossible without a large amount of automation.

#### How Can it be Solved?

Instead of running around doing manual development, building, testing and deployment of all the different applications (think of these as published services such as a web application that uses multiple resources to provide that service as an "application service".)

![Images](graphics/key_topic_icon.jpg)

CI/CD often gets visualized as a 3 step process, shown in [Figure 16-2](#ch16.xhtml_ch16fig02).

![Description: A picture containing timeline Description automatically generated](graphics/16fig02.jpg)

**Figure 16-2:** Continuous Integration Process

##### Continuous Integration (CI)

When you are properly using [Continuous Integration (CI),](#ch16.xhtml_key01-a) you have reached a state where multiple developers are working at the same time on different portions or aspects or modules of your infrastructure or app, and it's all getting integrated on a consistent basis into the main branch or set of code.

At this same time, there will be automated (hopefully!) testing and building procedures that check to see that what's been checked in, or submitted works with the sometimes many other portions that make up what will be the next update of the application.

##### Continuous Delivery (CD)

There are literally two slightly different processes that match the phrase CD:

• **[Continuous Delivery](#ch16.xhtml_key02-a)**, which means that after the developers check in their code, it's tested and merged into the main app code, then it's delivered automatically to a repository (grouping of code or packages, typically). If all has gone well in the Continuous Integration area, then Continuous Delivery just makes sure that code is available for use in the next step of making your application as up to date as possible in an automated way.

• **[Continuous Deployment](#ch16.xhtml_key03-a)**, which mean that after the code is delivered to the repository, it's then included as part of an update or release of the application to go into production. This could mean there is mere minutes between a check-in of code, it's automated testing and building and it being deployed on the production systems. While both exhilarating and horrifying, it's a great way to get almost instantaneous feedback on the true state of your application's most reent release.

As you can see from [Figure 16-2](#ch16.xhtml_ch16fig02), it all integrates well into a delivery and deployment methodology that has increased the ability of teams and organizations to get their software fixed, built, tested and in the use of users and customers much faster and more reliably often than the manual method allowed them to even dream of.

#### CI/CD Use Cases

It's a bit disingenuous to try to list many of the thousands of possible use cases for Continuous Integration as a methodology of handling your application environment and how you work with it as a team.

At this point, most any shop or project that is starting a new project should consider using Continuous Integration, but many current and even legacy projects are using a form of CI/CD these days.

You might get asked about some of the typical use cases for CI/CD, which might include:

• Web Applications

• Financial Services

• Shopping Sites

• Gaming Applications

• Social Media Applications

Any project that has a developer, test and production, can benefit from the use of the CI/CD methodology, and so the use cases listing could literally be majority of the projects hosted on Github, for example!

### Advanced Git Topics

This small section is here to explain a couple of objective-driven commands that are part of the git world, merge, rebase, and pull requests.

#### merge

![Images](graphics/key_topic_icon.jpg)

Git uses the **[merge](#ch16.xhtml_key13-a)** command as a way to reunite forked history. When you've created independent lines of developing, also known as branchs, you can then re-unite those branchs back together, creating a single united branch. The **merge** command allows you to combine branches in a forward manner.

#### rebase

![Images](graphics/key_topic_icon.jpg)

Git uses the **[rebase](#ch16.xhtml_key14-a)** command slightly differently than the **merge** command, which moves things forward, where rebase can allow you to create a new base commit.

Effectively, a rebase allows you to change the base of a branch so that it seems as if the new branch is from a completely different commit.

As another way to visualize this, consider a word document that has been developed by several authors, and has hundreds of embedded track change entries. You might want to take that base document, save it as a new version and strip all those track change entries out and start with a clean base document.

This is very similar to what rebase does, it allows you to declare a branch as "this is where I want to start with this new branch" and it's effectively a brand new branch from there, not encumbered with possibly hundreds of commit history items.

#### pull requests

![Images](graphics/key_topic_icon.jpg)

A [Pull Request (PR)](#ch16.xhtml_key15-a) is the mechanism whereby a contributor notifies the maintainer of a Git repo that they would like to submit some code/changes etc. for review.

Issuing a Pull Request from a contributor standpoint tells the server that there are some local un-reviewed commits that you are presenting for the maintainer to review and possibly integrate into this repository.

A Pull Request is a great way for someone who is interested in the contents of a repository to get commits made, without having to be the maintainer, or have authorization via an SSH key to the repository.

### Summary

In this chapter we worked hard to help you understand the concepts and some of the higher-level functions of the Continuous Integration/Continuous Delivery the final step, Continuous Deployment.

You also know about the very important data definition languages or formats, YAML and JSON. You are now even more aware of Git's higher end features such as merge, rebase and the ever-popular Pull Requests.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 16-2](#ch16.xhtml_ch16tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 16-2**–Key Topics for [Chapter 16](#ch16.xhtml_ch16)

![Images](graphics/16tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[Continuous Integration](#ch16.xhtml_key01)

[Continuous Delivery](#ch16.xhtml_key02)

[Continuous Deployment](#ch16.xhtml_key03)

[Infrastructure as Code](#ch16.xhtml_key04)

[terraform](#ch16.xhtml_key05)

[ansible](#ch16.xhtml_key06)

[chef](#ch16.xhtml_key07)

[puppet](#ch16.xhtml_key08)

[saltstack](#ch16.xhtml_key09)

[state files](#ch16.xhtml_key10)

[recipes](#ch16.xhtml_key11)

[playbooks](#ch16.xhtml_key12)

[merge](#ch16.xhtml_key13)

[rebase](#ch16.xhtml_key14)

[pull requests](#ch16.xhtml_key15)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** You have created a text file that contains instructions about creating and deploying Infrastructure as code, and that file ends with the .tf extension. That file is used with the terraform command to generate the _______ file. Choose the best word to fill in the blank.

**a.** code

**b.** test

**c.** plan

**d.** analyze

**2.** You have been researching methods of deploying and managing your infrastructure through the medium of text or code. Which main data definition formats have you found? Choose all that apply.

**a.** EBCDIC

**b.** YAML

**c.** ASCII

**d.** JSON

**d.** XML

**3.** You're a Red Hat Enterprise Linux user and want to choose the most direct and closely associated Infrastructure as Code option to create, deploy and manage your infrastructure. Which of the available methods is most close associate with Red Hat?

**a.** Puppet

**b.** Chef

**c.** Ansible

**d.** RPM

**4.** You are putting instructions into a file that will cause a particular set of actions to happen in the Saltstack IaC utility. What is the generic name of such a file?

**a.** state file

**b.** salt file

**c.** salt book

**d.** minion file

**5.** Which of the git commands will allow you to take a branch with previous commits and effectively allow it to become a new branch with no previous commit history? Choose the best git command.

**a.** git **emerge**

**b.** git **asnew**

**c.** git **nocommit**

**d.** git **rebase**

**6.** You are used to working with one of the main data definition formats and accidentally include a comment as you would normally do in your preferred format, but it causes an error. Which of the data definition formats does NOT allow the use of comments?

**a.** EBCDIC

**b.** YAML

**c.** ASCII

**d.** JSON

**e.** XML

## Chapter 17\. Understand Containers, Cloud, and Orchestration

This chapter covers the following topics:

• [Kubernetes Benefits and Application Use Cases](#ch17.xhtml_ch17lev1sec03)

• [Single-node, Multi-container Use Cases](#ch17.xhtml_ch17lev1sec04)

• [Container Persistent Storage](#ch17.xhtml_ch17lev1sec05)

• [Container Networks](#ch17.xhtml_ch17lev1sec06)

• [Service Mesh](#ch17.xhtml_ch17lev1sec07)

• [Bootstrapping](#ch17.xhtml_ch17lev1sec08)

• [Container Registries](#ch17.xhtml_ch17lev1sec09)

The exam objectives covered in this chapter are as follows:

**Objective 3.5:** Summarize container, cloud, and orchestration concepts.

From the number of included sub-topics, you'd think this objective and chapter was the size of the whole book! When the objective was being created, it was designed to be a catch-all for container and mesh concepts.

Remember, you don't need to have every detail of these concepts, they are just that, conceptual, overviews, you have to demonstrate some familiarity with the technology and how it works overall.

You are meant to study these concepts, understand when they are meant to be used, or are to your advantage to study further and consider implementing, and there are some great technologies and options here!

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 17-1](#ch17.xhtml_ch17tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 17-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/17tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** Which organization is the originator of the Kubernetes technology?

**a.** Kube Foundation

**b.** Linux Professional Institute

**c.** Google

**d.** F5

**2.** Why would you use a multi-container node or pod in Kubernetes?

**a.** Network isolation for all containers

**b.** CPU Isolation for all containers

**c.** Process Isolation for all containers

**d.** Ingress isolation for all containers

**3.** When using stateful applications in containers, what type of storage resources are most appropriate?

**a.** Resistant

**b.** Consistent

**c.** Insistent

**d.** Persistent

**4.** What is a main advantage of implementing Container Networking over traditional Pod Networking?

**a.** IP per Container

**b.** Security at the Container Level

**c.** Process Isolation at the Pod Level

**d.** The ability to bridge Containers

**5.** What technology takes the logic that controls service-to-service communication and implements it as a layer of infrastructure?

**a.** API Gateway

**b.** Reverse Proxy

**c.** Control Plane

**d.** Service Mesh

**6.** When [bootstrapping](#ch17.xhtml_key15-a) a container instance in AWS, which of the following are types of passable data you can use to execute configuration on the instance? Choose two.

**a.** .ec2 files

**b.** cloud boothooks

**c.** bootstrap container scripts

**d.** cloud-init directives

**7.** What is a primary purpose for having a container registry?

**a.** make package management easier

**b.** monitor the services installed on your system

**c.** scale workloads more easily

**d.** to store and access container images

### Foundation Topics

### Kubernetes Benefits and Application Use Cases

Not long ago the question "What is Kubernetes and what can you use it for?" would have been rather hard to answer, it's been a long road since it's announcement in 2014 by Google to today where it's a very large part of the cloud computing landscape and still growing it's market share.

[Kubernetes](#ch17.xhtml_key01-a), or K8s as it's often referred to as, was the first seed project for the Cloud Native Computing Foundation, the creation of Google and the Linux Foundation.

Within the space of 3 or so years, Kubernetes had won over most of the large cloud providers, including the Big 3, Google's GCS or Cloud Services, Microsoft's Azure and Amazon's AWS, all offering support for Kubernetes

Since there is no other mention of Kubernetes in this version of the Linux+ Objectives, and it's become such a large part of our computing environment, it's important to ensure you understand what Kubernetes is and at least the broad strokes of how it functions.

#### What is Kubernetes, Really?

Kubernetes is a set of technologies that all fit well and together as a greater construct make it possible to create, deploy, maintain and most critically, scale your applications based on a number of criteria. Those criteria include the amount of CPU needed for a task, the amount of Memory required to support the computing and a host of other additional criteria that you can specify and configure to suit your application needs.

In other terms, Kubernetes is a orchestration manager for containers and the applications that run in or on them. Orchestration is a term that means using software to automate actions that would otherwise have to be done manually, such as configuring, coordinating, managing and monitoring large-scale applications that run on your computing architecture.

Note

Following up on the modes we learned about in [Chapter 16](#ch16.xhtml_ch16), “[Understand Infrastructure as Code](#ch16.xhtml_ch16),” where a tool is considered to be Functional/Declarative or Procedural/Imperative, Kubernetes is definitely on the Declarative side of things.

For example, you do not tell Kubernetes HOW to do something, you tell it that you WANT it to happen, or you set a parameter such as CPU utilization that will then cause Kubernetes to increase or decrease resources.

#### The High-Level Structure of Kubernetes

![Images](graphics/key_topic_icon.jpg)

Kubernetes is made up of a lot of different items, control planes, nodes, services runnning that you mostly don't see, so let's demystify it a bit.

• **Kubernetes Control Plane** – Multiple components that have the duty to manage the whole cluster. These are sometimes called Kubernetes Masters or Controllers.

• **Kubernetes Nodes** – A Kubernets Node is a machine where the containers that make up a Kubernetes cluster are running on. While a Kubernetes Cluster can have any number of Nodes, you can run a Kubernetes Cluster on a single machine easily.

• **Kubernetes Pods** – A [Pod](#ch17.xhtml_key02-a) is the smallest item in the Kubernetes world, and when deployed, consist of a single or more containers. Containers in a Pod are linked together, and have the same lifecycle, as well as other characteristics of note.

The previous list is just a very high-level overview of Kubernetes Clusters, let's get into what components are located where next.

#### Kubernetes Control Plane Structure

![Images](graphics/key_topic_icon.jpg)

The Kubernetes Control Plane contains the functions that manage the Kubernetes Nodes, those items include:

• **kube-controller-manager** – is the process/component that manages all the control loop for Kubernetes.

• **kube-scheduler** – is the component that takes Pods that have no containers yet and assigns the containers to the pods based on the requirements that are the default or configured for the Kubernetes environment.

• **cloud-controller-manager** – is the component that workings with cloud providers via their API interfaces to handle specific tasks like name resolution and how to scale up and down across hardware resources.

• **kube-api-server** – is the component that performs the front-end operations for the Kubernetes API process.

• **etcd** – is a key-value store that performs in a highly-available manner to store all the database information for Kubernetes, keeping great log records of all that occurs and making sure that's available across it's nodes and other components.

Note

Kubernetes deployments can be at a regular level, where the components are not in a highly-available (multiple replicas of a component) state, and in a highly-available state where certain components are replicated for redundancy and an order of leader election is established. This is far beyond the scope of the Linux+ objectives, but good for you to know.

#### Kubernetes Node Structure

![Images](graphics/key_topic_icon.jpg)

Kubernetes Nodes are the systems/servers that run the applications that make up your Kubernetes environment. Nodes can contain various processes, but they at least contain:

• **kubelet** – is the process that gets the orders for what a given Pod's desired or target state is and then makes sure that Pod gets deployed properly and is healthy.

• **kube-proxy** – is the process that, not surprisingly from the name, handles all the UDP, TCP and SCTP proxy tasks of all the Nodes and helps provide the load-balanced services.

• **Pods** – these are the smallest level of Kubernetes function on a Node, they contain at least one Container, and if there are multiple containers, they are closely linked together, as a lot of functionality is kept at the Pod level, such as most networking, the lifetime of the Containers are linked to the Pod etc.

• **Containers** – The ONLY piece of Kubernetes that is really not a part of or native to Kubernetes! Kubernetes supports multiple container standards, but it doesn't have its very own container scheme.

#### Container Runtime Interface

Kubernetes and Docker both run containers, but Docker can access the Containerd runtime directly, whereas Kubernetes uses an access API called CRI or Container Runtime Interface.

From there either CRI-O or Containerd are used, which both use the Open Container Initiative's OCI specification to cause runC to create and run the actual containerized processes.

#### Specialized Container Types

Along with regular application containers, where an application is packaged up with all the dependencies it will need and stored as an image and then that image is executed and becomes a container, there are a couple of specialized container types you need to know about:

![Images](graphics/key_topic_icon.jpg)

• **Sidecar** – A [sidecar](#ch17.xhtml_key03-a) container is one that rides along with the main application container, or containers, and shares the same storage and network resources as the other containers. A sidecar can be thought of as an executive assistant, where functions that are required of all the various application containers in a Pod can use a sidecar for traffic routing, high availability needs, aggregated logging and certificate distribution to name a few functions.

• **Ambassador** – An [ambassador container](#ch17.xhtml_key04-a) typically sits between a web server and it's backend microservice so that in the event a microservice has to be moved, there are no changes that need to be made to the website, it communicates exactly as it has with the ambassador container, which routes the traffic to the new location or new backend microservice. NGINX users will recognize this as a form of Reverse Proxy, where the client doesn't know or care who or where the backend resource is, that's up the the Reverse Proxy configuration.

#### Benefits of Using Kubenetes

Many organizations can and do use Kubernetes, but some of the largest organizations are it's biggest fans. Some of the benefits of running Kubernetes include:

• Improved Resource Utilization

• Shorter software development timelines

• Easing of application upgrades and associated maintenance

• Ability to containerize older and monolithic applications

• Reduction in the use of Public Cloud and associated costs

• Flexibility of operations

• Developer efficiency gains

• Operator efficiency

As you can see, Kubernetes is somewhat complex, but it's very much taken over the majority of the computing landscape, and certainly it's a huge part of the public and increasingly, the private cloud.

The previous section should have given you a good overview of Kubernetes and it's main components, as well as how they interact together. As a further avenue of understanding Kubernetes, as the Linux+ is NOT where you'll get the fullest level of understanding of it, I recommend the fine set of resources on the Kubernetes site hosted by the CNCF or Cloud Native Computing Foundation, [https://kubernetes.io/](http://kubernetes.io/).

### Single-node Multicontainer Use Cases

Once again, the Linux+ objectives cryptically specify that we should know about a topic and then don't really tell us what aspect or even what about that topic we really need to know.

The fact that they gave us a very very tiny clue with the single word "Compose" for this topic does lead us down a set of related use cases for creating development environments that roughly mimics a production environment.

From that single word, we can assume that they are referring to using Docker [Compose](#ch17.xhtml_key06-a). Docker is one of the ways that you can create and deploy containers in your cluster.

#### Multicontainer Development Environment

There are a few ways you could roll with this scenario, the most simple of which would be to setup a couple of containers on the same Node, in the same Pod, and have them work together to make a larger set of capabilities.

##### 2 Container Node Example A

One example of multiple containers being configured on a single node would be to setup a relatively simple development environment where your Node has an NGINX Reverse Proxy container that protects a backend Elasticsearch container.

By putting the NGINX Reverse Proxy and the Elasticsearch containers in the same Pod, you get the ability to address both containers with the same IP Address, just on different ports.

You can use Elasticsearch for a number of things, none of which actually matter to our example, but it excels at enabling application, website, and enterprise-wide searching of data, analytics and monitoring and a lot more.

##### 2 Container Node Example B

Another example of multiple containers being configured on a single node would be to have a Node where an NGINX web server and a backend database such as Mariadb were configured with the database container being accessed solely by the web server container. The web server container would be configured to be publicly accessible through the Pod's networking configuration and the database container would work solely behind the scenes with the web server to provide content.

##### 3 Container Node Example

A more complex scenario regarding [single-node multicontainer uses](#ch17.xhtml_key05-a) may be where you're using a traditional pairing such as in Example B, but you then incorporate a Service Mesh into your environment.

This would add a sidecar proxy which helps protect and enhance the capabilities of the main container, which might be doing something very specific, such as providing web services via NGINX!

Let's take note that the standard Kubernetes cluster explanations and intention typically say there should be one service per container, and that's true, but also it's good to keep your Pods as uncomplex as possible, as all the containers in that Pod are effectively tied together, networking, restart cycles and more.

### Container Persistent Storage

[Persistent container storage](#ch17.xhtml_key07-a) is not as complex as it might seem, as containers themselves have nothing persistent, they have to depend on other tools to keep and store anything that is needed across container instances.

#### Docker Volumes

Since the objective doesn't specifically talk about Kubernetes, we can start more simply and discuss Docker Volumes, or where you have used the **docker volume create <dockervol>** command to create a volume on the local system that runs Docker, such as the following command:

$ docker volume create mydatavol

From there, you can mount the volume to a new container using the command:

$ docker -d -p 5000:5000 -v mydatavol:/mydatavol mydatavol

Now you can open a bash shell in the container and see the /mydatavol storage location is present.

##### Advantages of Using Docker Volumes

A Docker volume can be created, attached and interacted with from the container or containers that have it attached, and when those containers are stopped and go away, the data volume remains, and can be used again and again.

Obviously this allows you to store configuration and other data on that locally-resident volume and have containers access it either in read-write or read-only modes, depending on what the container needs and what you want to have happen.

In short, the main advantages of using Docker Volumes are it's faster, not tied to the containers lifecycle and designed for multiple container usage.

##### Disadvantages of Using Docker Volumes

Frankly, there are not many significant challenges to using Docker Volumes, except of course, if you are NOT using Docker... It's good to remember that Docker Volumes are destroyed when the last container using that volume is stopped or killed.

There are some indications that the best way to keep your data, even across the removal of the last OTHER container is to have a container that is dedicated to collecting and storing that data from more transient containers and then commit that data to either the image you are using for standing up containers, or more permanent file system storage.

#### Bind Mounts

In contrast to Docker Volumes, there has existed almost since the very beginning of Docker, the bind mount.

![Images](graphics/key_topic_icon.jpg)

A bind mount is where you have a file or directory on the host systems storage, and then you bind or mount that to the container's filesystem. Bind mounts are always referred to in an absolute path/file way.

If you are familiar with the concept of using a file on disk to add additional swap space to a Linux system, then using a bind mount will make sense.

##### Advantages of Using Bind Mounts

A Bind Mount also allows you to have persistent storage for containers, and can be high-performing, depending of course, on the state and busyness of the file system that is being mounted.

Bind Mounts have been around a long time, they're very easy to use, and a lot of code has been built around creating, managing and removing them.

##### Disadvantages of Using Bind Mounts

A Bind Mount may be easy, but like a lot of things that are easy, there are significant issues that using Bind Mounts can introduce to your environment.

Most significantly, a Bind Mount is actually accessing directly a file on the host's filesystem, which is a security risk, to say the least.

It would be a very simple hack to create a very large file or set of files through a Bind Mount of a directory that would fill up the host filesystem or even to access other files, processes etc. on the host, particularly if you had Bind Mounts in the /tmp or /var/run locations.

#### Kubernetes Persistent Volumes

No discussion on data persistence for containers is complete without discussing how Kubernetes handles persistent storage for containers.

Kubernetes has a very large amount of volume types, everything from AWS-specific to vSphere, but that functionality is far beyond what we need for the Linux+ exam.

##### The Kubernetes PersistentVolume Subsystem

![Images](graphics/key_topic_icon.jpg)

Kubernetes has a subsystem that handles how storage is consumed. There are two API resources or calls that govern this:

• **PersistentVolume** – Otherwise known as a PV, this is a resource in the cluster that has been either manually or automatically provisioned for use. A PV is at the same level as a Node in the cluster, and unlike a Volume, where the lifecycle is tied to a container, a PV has it's own persistence and lifecycle, and is independent of any Pod (or one of it's containers) that requests storage from it.

• **PersistentVolumeClaim** – Otherwise known as a PVC, this is a request from a user or process for storage resources. These occur at the Pod level and can take many forms, depending on what the requesting user/process needs the storage for.

##### The PV and PVC Lifecycles

Remember that a PV exists independently in the Kubernetes cluster, and has it's own lifecycle, and that PVC's are very ephemeral and are created and destroyed, or reclaimed, depending on whether the user/process is done with the Claim, and the PV receives instructions to reclaim, retain or delete that resource.

Note

The Linux+ objectives will test you on your overall knowledge of volumes, persistence of storage and how Docker and Kubernetes deal with storage persistence. We've gone beyond that, but it's important to give you a full context so you're not just hearing phrases, you understand how this all fits together.

### Container Networks

[Container networking](#ch17.xhtml_key08-a) can be a complex topic, so it's best to start with defining what an Overlay Network is, and why they exist.

##### What's an Overlay Network?

![Images](graphics/key_topic_icon.jpg)

An [Overlay Network](#ch17.xhtml_key09-a) is a network construct or schema that is put on TOP of an existing network infrastructure. In some cases, the concept of having Subnets is an overlay over the actual physical hardware that provides the networking infrastructure.

In containers, and Overlay Network is how you can have a distributed network that allows multiple containers (through their Pods) to access each other via a network scheme.

Overlay Networks are different than inter-Pod communications where the containers within a Kubernetes Pod can communicate safely between each other without using any outer resources.

Note

Overlay networks are also useful and necessary when you have several host systems that have resident containers who need not just to communicate between containers on the same host, but between containers located on separate hosts.

##### Docker Swarm

Docker has a concept that is called a Swarm where encrypted communication is allowed between containers, and the Swarm is an Overlay on top of the networking configuration of the actual Docker hosts.

There are a couple of networks that get create when you create an Overlay Network with Docker:

• **ingress** – This network handles the swarm-related data and traffic, and swarm services automatically connect to this network unless directed to connect to user-created overlays.

• **docker_gwbridge** – This network interconnects the Docker daemons to each other, those that are joined to the swarm.

##### Kubernetes Overlay Networks

Not surprisingly, while Docker's overlays and swarms are relatively easy to understand and implement, Kubernetes goes the full distance and has many choices for overlaying network structures, including but not limited to:

• **Flannel** – The Flannel agent (flanneld) resides on each host and once the IP and subnet information is assigned, uses the Kubernetes API to store the hosts networking configuration information.

• **Calico** – Continuing the fabric (get it?) theme, Calico is more complex and full-featured and provides a robust networking stack that includes the presence of a virtual router that uses BGP (Boundary Gateway Protocol) to advertise the presence of services to the rest of the environment.

• **Cillium** – At the top end, the Cillium solution is the most full-featured and complete network solution for Kubernetes at present. It can do everything from assignment, to filtering and policy enforcement to even replacing the actual kube-proxy agents with it's own!

Note

Once again, the Linux+ objectives will test you on your overall knowledge of overlay networks, and we've made sure to go beyond what we know is needed, because you really do need to know how overlays are used, both in Docker and for Kubernetes.

##### Bridging Networks

In this example, we'll use Docker and how it uses a bridge to connect resources. A bridge is the default network setup for allowing containers to communicate with each other in the Docker world. Any container connected to the same bridge network can contact and communicate with the others on the same bridge.

![Images](graphics/key_topic_icon.jpg)

However, a bridge network is only for communications between containers on the same host, so an overlay network would be necessary to have inter-host communications or to have containers on separate hosts communicate with each other. (See the recent NOTE about overlay networks and inter-host communications.)

By default, on startup, Docker creates a bridge network named, rather unimaginatively: bridge, and any containers started after it's creation are automatically connected to the same default bridge network.

If the default bridge network is not to your satisfaction, it's easy to create user-defined bridges with custom settings.

##### Swotting a NAT

The concept of a [NAT](#ch17.xhtml_key12-a) or [Network Address Translation](#ch17.xhtml_key11-a) setup is something that most people use every single day on their work or home router. NAT is where you have a public address on the outside of the router that is capable of communication in every sense with the outside networks, or Internet. Inside the NAT, a private IP Address scheme is used, (either 10.0.0.0, 172.16.0.0 or 192.168.0.0) and all hosts inside the NAT can communicate with each other on the same subnet scheme, or with the host or router, but they are NOT publicly addressable through the router.

When a host system has a NAT setup running, that external interface is the egress or jump-off point for all NAT-generated traffic from the virtual machines or containers that are on the private address schemes behind the NAT.

This has a big advantage for use in containers, there is no need for any external address, other than the one assigned to the host system, and all traffic that is sent outside of that host to the public networks or Internet is from the external address, with no outer indication it's from a NAT source.

However, the NAT knows that traffic was sent from internal sources, and upon receiving a response to any sent request, routes that response back to the source internal virtual machine or container, all without exposing the virtual machine or container to the dangerous outside networks or Internet.

![Images](graphics/key_topic_icon.jpg)

NAT is especially useful for when external IP Addresses are expensive or difficult to obtain, it helps an organization spend less on IP management and more on getting the actual work done.

##### Host Networking

The [host networking](#ch17.xhtml_key13-a) mode is where a container can share or piggyback on the host system's networking stack. In this case, the container does not have it's own IP Address, but instead shares the host IP Address, and traffic is separated by the network driver to get to the host destination or to the container destination.

Think of host networking as a "Party Line", such as back when a telephone line was shared by several rural households or locations, all of whom had equal access to the line.

### Service Mesh

A [service mesh](#ch17.xhtml_key14-a) is a complex and many-layered topic, almost always involving Kubernetes or another clustering setup, a need for security and observability and some patience, as service meshes are sometimes difficult to install, operate and get the right value from.

Also, the need for a service mesh often exists up at the very highest levels of those organizations that are using containers, Kubernetes the CI/CD pipeline and IaC areas of provision of services to customers.

##### What IS a Service Mesh?

The world of using modern applications to provide services to clients is mostly constructed of micro-services, collected into groups of services that provide a particular function. The knitting together of a modern application, such as an Amazon or Alibaba shopping site can involve dozens to hundreds of separate but critical micro-services, all of which need to be managed, secured, observed for faults, monitored for performance etc.

This need for an overlay of management and security, the need for the component services to not only communicate with the cluster or application, but each OTHER, poses an unique challenge, that of how to manage all of this without so burdening the application/micro-services with that management that it affects performance?

##### Example Service Mesh

![Images](graphics/key_topic_icon.jpg)

The most recognizable service mesh provider is Istio. The Istio product is open source, it overlays and injects itself into your Kubernetes (for example) cluster and inserts it's components into sidecars in each Pod, effectively becoming a sidecar proxy, but with much more functionality that just a simple proxy.

Istio says it very well on their site, the project brings the following advantages to the table when deployed and used:

• Secure service-to-service communication in a cluster with TLS encryption, strong identity-based authentication and authorization

• Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic

• Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection

• A pluggable policy layer and configuration API supporting access controls, rate limits and quotas

• Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress

##### Istio Components

Istio is made up of the same general style of components as Kubernetes, a control plane and a data plane, but it's designed to fit over and into Kubernetes like snapping on an exo-skeleton to a soldier, to make them stronger, have more control and to add extra capabilities.

##### Commercial Istio Distributions

There may be others, but the prime example of using an Istio distribution as the basis of a commercially-viable product is the Aspen Service Mesh, recently acquired by F5 Inc.

Aspen Service Mesh is based on the Istio open source project code, and adds some key features, support and training and all the usual enhancements that come with a commercially-available distribution of and open source project.

##### Non-Istio Service Meshes

The NGINX Service Mesh product is a very interesting adjunct to the Istio Service Mesh, in that it's meant to do very much the same sort of task as Istio, but it's based on the NGINX Plus, the NGINX Ingress Controller and NGINX-specific sidecar proxies that are inserted in between service containers and the rest of the cluster, very similar in concept to the Istio model.

### Bootstrapping

Just about every way you can manage your infrastructure requires you to first install a tool, and with several instances, that's manageable, but what about if you need to bring up and configure dozens, or hundreds, or even thousands of instances of multiple configurations?

Introducing a handy little tool named cloud-init, which is included on a large subset of current Linux images, ready to take your orders and make your cloud images usable upon bootup or shortly after.

You can think of [cloud-init](#ch17.xhtml_key16-a) as a script interpreter, which effectively it is, and the cloud-init scripts are usually delivered from what is commonly called "userdata" to the cloud-init script itself, which sets about obeying the actions and configuration contained in that set of instructions.

![Images](graphics/key_topic_icon.jpg)

You write your cloud-init configurations up in YAML, so it's very easy to read and troubleshoot.

It's impressive the number of things that a cloud-init script can do, such as:

• Pass user data on to the system

• Setup users and groups

• Set the locale and timezone information

• Install, update, remove packages and more

• Adding, changing or update repositories

• Configure Encryption such as SSH and CA Certificates

• Configure any client OS setting you can type a command for

• Boot, reboot, shutdown systems

• Install management frameworks

### Container Registries

As a last topic in this chapter, it's good for us to talk about [Container Registries](#ch17.xhtml_key17-a), because they are not very well understood unless you work with containers a lot.

##### What is a Container Registry?

There are two main types of container registries, public and private.

![Images](graphics/key_topic_icon.jpg)

Public registries are typically for a community of users, such as the Docker container registry, but those can be a bit of a free-for-all, and smaller and private teams that want to generate, curate and store their container images will likely consider a private container registry option.

##### Why Use a Container Registry?

Simply put, for the ability to have a single source of truth, as it were, for your container images. Imagine a dozen developers all with their own local folder(s) full of experimental, in-development and production container images, and after you stop shuddering at the thought, imagine a central repository that you post your images to, that maintains them like a source code version control system would, and that you can always find a particular image when you want it, and all it's versions and revisions.

Additionally, having a repository helps you with container image security issues, fix issues that occur and post the updated version, and all without multiple spreadsheets, post-it notes on monitors and crippling confusion.

##### What about Bigger Teams?

Container registries can scale along with your needs, replicating a single central registry to backup your registry is one application, but having a local and synchronized container registry copy in each of your global regions can be a huge time and bandwidth saver as well.

##### What are My Container Registry Options?

You know now why you'd choose to have a private registry, but what are the options that are out there for free or for pay to help you with this?

The top-rated container registries are:

• Amazon ECR – [https://aws.amazon.com/ecr/](http://aws.amazon.com/ecr/)

• Microsoft Azure Container Registry – [https://azure.microsoft.com/en-us/services/container-registry](http://azure.microsoft.com/en-us/services/container-registry)

• Docker Hub Container Registry – [https://hub.docker.com/](http://hub.docker.com/)

• Github Package Registry supports containers now – [https://github.blog/2020-09-01-introducing-github-container-registry/](http://github.blog/2020-09-01-introducing-github-container-registry/)

• Google Artifact Registry – [https://cloud.google.com/artifact-registry/](http://cloud.google.com/artifact-registry/)

• Red Hat Quay Registry – [https://quay.io/](http://quay.io/)

##### That's a Wrap

All of the above will give you a great idea of what your container registry options are, and where to get all the information you need to make a solid choice that will serve your needs, large or small, public or private!

### Summary

In this chapter we worked hard to help you understand the concepts and some of the higher-level functions of Containers, Cloud and Orchestration.

Given the previous chapter (16) where we discussed Iac (Infrastructure as Code) and this chapter where we delved deeper into the Cloud and it's components, you should now have a clearer and exam-friendly view of the current state of Cloud Computing and it's components as they pertain to you and your organization's needs.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 17-2](#ch17.xhtml_ch17tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 17-2**–Key Topics for [Chapter 17](#ch17.xhtml_ch17)

![Images](graphics/17tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[Kubernetes](#ch17.xhtml_key01)

[Pods](#ch17.xhtml_key02)

[Sidecards](#ch17.xhtml_key03)

[Ambassador Containers](#ch17.xhtml_key04)

[Single-node multicontainer use cases](#ch17.xhtml_key05)

[Compose](#ch17.xhtml_key06)

[Container Persistent Storage](#ch17.xhtml_key07)

[Container Networks](#ch17.xhtml_key08)

[Overlay Networks](#ch17.xhtml_key09)

Bridging

[Network Address Translation](#ch17.xhtml_key11)

[NAT](#ch17.xhtml_key12)

[Host networking](#ch17.xhtml_key13)

[Service Mesh](#ch17.xhtml_key14)

[Bootstrapping](#ch17.xhtml_key15)

[Cloud-init](#ch17.xhtml_key16)

[Container Registries](#ch17.xhtml_key17)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** What deployed component of Kubernetes is made up of at least 1 container? Choose the best answer.

**a.** Node

**b.** Sidecar

**c.** Pod

**d.** Cluster

**2.** Which of the following types of networks are in typical use when virtual machines or containers are resident and running on a host system? Choose all that apply.

**a.** Overlier

**b.** Host

**c.** Switch

**d.** Bridge

**e.** Token

**3.** You have an application container inside a Pod on a Node, and decide to place another container in that Pod to serve as a proxy to the outside. What is the proper word or phrase to describe this proxy container?

**a.** Helper

**b.** Utility

**c.** Sidecar

**d.** Ingress

**4.** You have a need for storing data that does not go away when a container is removed, so you create and use a _______? What is the name of this type of storage in Docker or Kubernetes?

**a.** Persistent Volume

**b.** Solid State

**c.** Consistent Storage

**d.** Mount Point

**5.** You have a fairly large Kubernetes cluster providing several micro-services and need to have between-application encrytion, better visibility of application states and stats and the hope of someday being regulatory compliant. What is the likely tool or system that you will now add to your cluster?

**a.** Sidecar Proxy

**b.** Helm

**c.** Cloud Registry

**d.** Service Mesh

**6.** Your cloud development team is going crazy trying to find, retain and catalog all your development, testing, pre-production and production container images. What might you consider using to bring some sanity to all this madness?

**a.** Scotch and Advil

**b.** Service Mesh

**c.** Cloud Broker

**d.** Container Registry

## IV: Troubleshooting (Obj. 4.1 - 4.5)

## Chapter 18\. Analyzing and Troubleshooting Storage [This content is currently in development.]

**This content is currently in development.**

## Chapter 19\. Analyzing and Troubleshooting Network Resource Issues

This chapter covers the following topics:

• [Network Configuration Issues](#ch19.xhtml_ch19lev1sec03)

• [Firewall Issues](#ch19.xhtml_ch19lev1sec04)

• [Interface Errors](#ch19.xhtml_ch19lev1sec05)

• [Bandwidth Limitations](#ch19.xhtml_ch19lev1sec06)

• [Name Resolution Issues](#ch19.xhtml_ch19lev1sec07)

• [Testing Remote Systems](#ch19.xhtml_ch19lev1sec08)

The exam objectives covered in this chapter are as follows:

• **Objective 4.2:** Given a scenario, analyze and troubleshoot network resource issues

Network troubleshooting is a key part of any systems professional's life, if you can't get to the network, or something is wrong preventing your system from resolving names properly, your ability to function is severely limited.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 19-1](#ch19.xhtml_ch19tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 19-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/19tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** You are trying to reach a remote host that has recently been contactable, but are getting errors or very long wait times. What is the easiest troubleshooting method to pursue first?

**a.** Go find your DNS Administrator

**b.** Dig into the networking configuration files

**c.** Check your networking cable is connected

**d.** Sacrifice a goat to Imhotep

**2.** You are trying to ssh to a remote host not long after a security audit, and are not able to get a login prompt from the host. What may have been adjusted to disallow SSH access?

**a.** The host firewall rules

**b.** The organizational securit policy

**c.** Classless Inter-domain Routing configuration

**d.** Your host's VLAN location

**3.** Your office location has moved, and when you boot your Linux Desktop, you are unable to connect to the network, even though you have done the simple step of looking to see if your Ethernet cable is properly plugged in. What command with options is recommended to display your systems IP Address information?

**a. ifconfig -a**

**b. netplan show**

**c. sysconfig -v**

**d. ip a s**

**4.** Your work partner has been testing a server's bandwidth usage and when you use it for your throughput testing, things seem very slow. Which of the following commands might they have used to control the system's bandwidth? Choose all that apply.

**a. tc**

**b. ncat**

**c. wondershaper**

**d. ipfw**

**e. trickle**

**5.** After spending a lot of time locally developing a website and then deploying it, you find that none of your updates are showing on what you assume to be the public site. What file should you check to ensure you are seeing the production site, and not a local site?

**a.** /etc/sysconfig/network

**b.** /etc/resolv.conf

**c.** /etc/nsswitch.conf

**d.** /etc/hosts

**6.** Which of the following commands could you use to show you if a remote system is available and the possible network path your traffic took to get to it? Choose Two.

**a. ifconfig**

**b. ip**

**c. netplan**

**d. traceroute**

**e. dig**

### Foundation Topics

### Network Configuration Issues

In this day and age, there are a lot of auto-configuration tools and most Linux distributions will walk you through a simple set of steps to get your network device connected either to wired Ethernet or WiFi.

Lets start simple with what are the main causes of network configuration problems. We'll limit ourselves to the ones detailed in the Linux+ Objectives, Subnet sand Routing, but we won't be able to not mention the Default Gateway, which the author feels is missing from this Objective entirely.

#### Causes and Symptoms

![Images](graphics/key_topic_icon.jpg)

There most likely possible causes of network configuration issues are:

• Subnet issues

• Routing issues

Symptoms of [high latency](#ch19.xhtml_key05-a) might include:

• Having a configured IP Address, but unable to see any other hosts on the network, even if they can see each other

• Being able to see hosts on the local network, but NOT contact hosts outside of your local network

#### Diagnosing and Fixing the Problem

You can use several utilities to see different aspects of your network configuration, but the main one is **ip**.

The **ip** command is a very versatile and complete command, featuring a number of sub-functions, but showing your overall network configuration is probably it's most used function.

##### Diagnosing Subnets with the **ip** Command

The **ip** command by itself is about all you'll need to see the majority of details about your IP Addresses, Subnets and Gateway information.

For example, the **ip** command can also display network configuration data, just like the **ifconfig** command. If you execute the **ip addr show** command, the output looks like that shown in [Example 19-1](#ch19.xhtml_exe19_1).

**Example 19-1**–An Example of **ip addr show** Command Output

```
$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN
 link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
 inet 127.0.0.1/8 scope host lo
 inet6 ::1/128 scope host
 valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state
UP qlen 1000
 link/ether 08:00:27:08:ea:ff brd ff:ff:ff:ff:ff:ff
 inet 192.168.1.22/24 brd 192.168.1.255 scope global eth0
 inet6 fe80::a00:27ff:fe08:eaff/64 scope link
 valid_lft forever preferred_lft forever
```

When the **ip** command displays it's information, you kind of have to parse the output to see what you need, so I recommend using the **grep** command to filter the output to get just what you want, where **grep** is being used to filter for the word inet, which then displays the output in [Example 19-2](#ch19.xhtml_exe19_2).

**Example 19-2**–An Example of **ip addr show | grep "inet"** output

```
$ ip addr show | grep "inet"
inet 192.168.1.22/24 brd 192.168.1.255 scope global eth0
inet6 fe80::a00:27ff:fe08:eaff/64 scope link
```

What you are looking for in this situation is that your subnet mask (in this case a /24, or 24 bits long, aka 255.255.255.0) means you are on a standard Class C network in which the last octet (8 bits)is where the hosts are located.

On a Class C with a standard Subnet Mask you have 254 possible addressable hosts. Since the Subnet Mask is a /24, and the network being addressed as 192.168.1.0, the last address in the 255 available for hosts (.255) is also reserved for the use of broadcasting to all hosts on the subnet.

You can see in the output that the "brd" is followed by the previously-mentioned broadcast address of 192.168.1.255 and finally the last bit of info we can get on that line is the actual interface, which here is the eth0 or first Ethernet interface.

Note

The real issue with Subnet Masks is if there is a mismatch between the actual Subnet you're on and the configuration your system has. If your system has recently been moved, or perhaps it has a manually-assigned IP Address and other network configuration, those should be checked.

##### Diagnosing Routes Using the **ping** Command

Next up is the route that your traffic will take, and that means not just on your local subnet, where your system can broadcast out and find another host and then communicate.

Note

It should be noted (see what I did there?) that if your Subnet Mask is improperly configured, you'll be trying to communicate on the wrong network, and that can cause your system to not know how to get out of the current network and cause routing issues.

The route your traffic will take is most important when it's ANOTHER subnet, be it the very next one off your local router, or all the way across the Internet.

One of the first tools you should use when you aren't sure if your system has a proper route is to see if you can reach a remote host you are pretty sure exists and will respond with the **ping** command.

We covered the **ping** command in [Chapter 5](#ch05.xhtml_ch05) - Using Network Tools and Configuration Files, and it's so simple to use that most every troubleshooting session that is about networking should start with a simple **ping otherhost** command, just make sure that your networking EXISTS.

You can also use the **ping** command to see if what you THINK is the default gateway out of your network is reachable, if not, there's probably a gateway problem.

##### Diagnosing Routes Using the **ip route** Command

Another tool and another part of the **ip** command is the route object, or sub-command of the **ip** command. (Just think of it as the OBJECT that the **ip** command is acting upon.) When you use this object, it focuses on the route portion of your **ip** command and shows you the information that can be pulled from the /proc and probably /sys trees about the routing for your interface(s).

For instance, in [Example 19-2](#ch19.xhtml_exe19_2a) , you see the output of the **ip route** command on a typical system with a local and eth0 interfaces.

**Example 19-2**–An Example of **ip route show** output

```
$ ip route show
default via 192.168.64.1 dev enp0s2 proto dhcp src 192.168.64.2 metric 100
192.168.64.0/24 dev enp0s2 proto kernel scope link src 192.168.64.2
192.168.64.1 dev enp0s2 proto dhcp scope link src 192.168.64.2 metric 100
```

What we are looking in this output is the combination of items that will make for a properly configured route out of our network, starting with the first line that shows the default gateway, denoted by the "default via 192.168.64.1". This line also shows the device, the protocol, where the traffic comes from and a metric.

You could say that the **ip route show** command's output is more complete than the **ip address show** command, in that it focuses on the route and gateway address, it even shows the local hosts IP Address, the 192.168.64.2 address!

##### Diagnosing Routes Using the **traceroute** Command

The final tool is **traceroute**, an venerable and trusty tool that has sadly become less helpful across the wide area network or Internet due to the blocking of one of it's main protocols, that of ICMP or Internet Control Message Protocol.

![Images](graphics/key_topic_icon.jpg)

The **traceroute** command effectively sends out a series of packets to the first and then subsequent routers it finds along the route to the remote host, each time reporting back that router and building a set of routes that you can use to, well, trace where your packets have to travel, the number and timings for each section of that route.

Partly because **traceroute** is SO helpful in seeing what's happening and giving you statistics about the routers and timings, ICMP has been disabled on many public and even a lot of private networks, since it can be used to gain a little too much information at times.

As an example, if we did a **traceroute** from our local computer to the [rossbrunson.com](http://rossbrunson.com) host, you'd see something similar to the output in [Example 19-3](#ch19.xhtml_exe19_3).

**Example 19-3**–An Example of **traceroute [rossbrunson.com](http://rossbrunson.com)** output

```
$ traceroute rossbrunson.com
traceroute to rossbrunson.com (192.0.78.24), 30 hops max, 60 byte packets
 1  _gateway (192.168.64.1)  0.161 ms  0.101 ms  0.092 ms
 2  www.webgui.nokiawifi.com (192.168.12.1)  2.544 ms  2.483 ms  2.422 ms
 3  192.0.0.1 (192.0.0.1)  4.332 ms  4.248 ms  4.206 ms
 4  * 192.0.0.1 (192.0.0.1)  62.602 ms *
 5  192.0.0.1 (192.0.0.1)  84.482 ms  84.430 ms  84.381 ms
 6  * * *
 7  * * *
 8  192.0.0.1 (192.0.0.1)  73.586 ms  80.029 ms  79.968 ms
 9  10.170.233.133 (10.170.233.133)  71.639 ms  71.975 ms  73.179 ms
10  10.164.176.237 (10.164.176.237)  68.158 ms  68.107 ms  79.140 ms
11  six.automattic.net (206.81.81.70)  77.953 ms  69.818 ms  69.747 ms
12  * * *
```

In [Example 19-3](#ch19.xhtml_exe19_3), anywhere you see a set of 3 consecutive * characters, that is a router that has ICMP turned off, didn't respond in a timely manner or is otherwise restricted, and so you'll just get those asterisks instead of useful information.

Take note of the lines where you DO get good information, the 3 packets that are sent out report back the trip time for that packet and therein lies a good amount of information, sometimes you'll see a router or two that are having issues or long trip times, a sure sign of heavy traffic or being overloaded.

Note

You should also try the **traceroute** command with the **-T** or "use TCP SYN for probes" option, it often will show a shorter and more complete output by avoiding the use of the much-restricted ICMP.

### Firewall Issues

Even though we already covered Firewalls in [Chapter 10](#ch10.xhtml_ch10) "Implementing and Configuring Firewalls," we need to cover the concept of what can go wrong with a firewall, mostly in how a misconfigured firewall can affect appropriate or allowed traffic to a host.

#### Firewall Refresher

![Images](graphics/key_topic_icon.jpg)

Keep in mind that a firewall exists so that a host can be protected from unwanted or harmful traffic. The real problem exists in blocking the unwanted traffic but allowing what is sometime exceedingly similar wanted traffic!

Let's say we have a simple scenario where a user's client computer wants to access a simple NGINX web server, and there is a firewall in between them, as shown in our diagram in [Figure 19-1](#ch19.xhtml_ch19fig01).

![Description: A diagram of a firewall Description automatically generated](graphics/19fig01.jpg)

**Figure 19-1**–Diagram of simple firewall scenario.

The user's computer needs to access the web server, and there is a firewall in the way, which be default will not send the user's request traffic to the web server.

If we want the user, (or any host for that matter) to access the web server or have it receive and respond to a request, there must be at least an exception added to the firewall rules that allows traffic on port 80 (for HTTP) and port 443 (for HTTPS), so the firewall knows it's ok to forward requests on those ports to the web server.

Once those exceptions are made, and the rules are in effect, the user's computer will be able to make a request to the web server and get a response.

#### What Could Possibly Go Wrong?

That's a whole book in and of itself, but there are a couple of main things that can go wrong in even such a simple scenario as this.

We'll stick to our general format for the troubleshooting chapters and detail those in the next section, before we get into how to fix them or avoid them.

#### Causes and Symptoms

![Images](graphics/key_topic_icon.jpg)

There are several possible causes of firewall issues, including:

• Service not running

• Incorrect ports being listened on

• Incorrect ports for the traffic being allowed or denied

• Non-standard ports are being used

Symptoms of low throughput might include:

• Can reach the firewall, but not the destination server

• Can reach the gateway of the device's network, but not the device

• The connection happens, but the result is not what is expected

#### Diagnosing and Fixing the Problem

There are several utilities that will give you a good view as to what may be the problem with your firewall, they include:

• **ping** – Described ad nauseum previously as a tool, you'll be using a simple ping to see if you can reach the remote target host, another host on that network, the firewall, the gateway on that network, your own gateway etc.

• **telnet** – The **telnet** command is mostly deprecated, and your installation of Linux may not even have it available. It's a useful tool, something akin to using a stick to check if a turtle is sleeping, any response will be informative.

• **[nmap](#ch19.xhtml_key09-a)** – The **nmap** command is a new tool so far for us, we'll cover nmap in more detail in the "Testing Remote Systems" section of this chapter.

Note

A lot of networking utilities are already covered in [Chapter 05](#ch05.xhtml_ch05) - Using Network Tools and Configuration Files, so we'll concentrate on making sure you know services are running properly and how to see if they are running remotely.

##### Diagnosing with the **ping** Command

You've seen the **ping** command before, it's important to know how to use it, no matter what your job is around Linux and Open Source.

The most basic thing to establish if a host is accepting connections, or is alive at all, is to ping the device, such as:

```
$ ping remotehost
```

Also consider that [DNS (Domain Name Services)](#ch19.xhtml_key08-a) may be busy or malfunctioning and use the remote host's IP Address if you know it.

Once the host responds, then you can try higher level connection requests. If the host doesn't respond, try another host on that same network, if you know of one.

##### Diagnosing with the **telnet** Command

Never use **telnet** for actual remote command line sessions anymore, it's stupendously unsecure, you really should only use as a quick and dirty way to display the response you get to a query on a remote port.

For any connection that will contain any data of any import at all, always use the Secure Shell or SSH suite of utilities rather than the Telnet and R-suite of utilities.

As a veteran of the Operating System Wars, I tend to use the **telnet** command first to poke a system on a particular port to see what responds, if anything. For example, I might want to see if a remote host has a web server configured on Port 80, and I could just use the **curl** command to do that, but I might also want to just see if the port is responding at all, and with what.

Note

As a further point about the (possibly) puzzling use of a decades-out-of-date tool like telnet here, we do it because the telnet command when used this way is like sticking a straw into the target service:port and then looking at what leaks onto the screen as the output. It's very informative, and mostly BECAUSE the telnet command is SO leaky and open.

Let's poke a remote system with the **telnet** command, [Figure 19-2](#ch19.xhtml_ch19fig02) shows the output of the our **telnet** to the remotehost system and it's response.

![Description: A computer screen shot of a computer program Description automatically generated](graphics/19fig02.jpg)

**Figure 19-2**–The output of a **telnet** to a remote system

The **telnet** command was executed, the response is the first block ending in the "Escape character is..." and after hitting enter or any character and then Enter, the NGINX service reponded to the invalid or bad request with a 400 return message.

Now I know that there is an Open Source version of NGINX over there on that host, listening on Port 80, I might try Port 443 next.

##### Making Sure Services are Running

What does this have to do with firewalls? I have seen some really embarassing moments when someone reports a firewall issue and it's a "that system is NOT running THAT service" issue.

Covered elsewhere, the **systemctl** command is the best way to ensure that a service is running, what it's general configuration is and some key log file entries that have happened.

[Figure 19-3](#ch19.xhtml_ch19fig03) shows the output of the **systemctl status nginx** command.

![Description: A screen shot of a computer Description automatically generated](graphics/19fig03.jpg)

**Figure 19-3**–The output of the **systemctl status nginx** command

As you can see, the service is running, accepting connections and everything seems to be ok, but at least look at the log files to ensure things are being read and reported properly, like the previous **telnet** command and it's 400 error should be shown, and are in [Figure 19-4](#ch19.xhtml_ch19fig04).

![Description: A black background with white text Description automatically generated](graphics/19fig04.jpg)

**Figure 19-4**–The output of cat on the /var/log/nginx/access.log file

Oddly enough, you won't see the 400 error message in the actual error.log file for NGINX, it's going to show in the access.log file output.

So, as you can see, the service is running, accepting and rejecting connections and throwing errors properly.

### Interface Errors

Since your network interface(s) are the way you contact, communicate with and in general experience any other computer or resource, it's critical to understand what can go wrong with those interfaces and what you may be able to do about it.

#### Dropped Packets and Collisions

When the objectives mention dropping packets, they're not talking cigarettes, they're referring to when a network interface is discarding or losing data packets, very often an indication of a damaged network cable somewhere, a firewall that is configured to not forward those packets or even disfunctional network card memory.

[Collisions](#ch19.xhtml_key03-a) happen all the time on Ethernet, it's a fact of life. If you've ever had to move quickly down a long hallway filled with other people, you'll know how an Ethernet packet feels on it's way down the wire.

#### Diagnosing and Fixing the Problem

![Images](graphics/key_topic_icon.jpg)

There are several utilities that will give you a good view as to what may be the problem causing you to drop packets and experience collisions, they include:

• **ethtool** – The **ethtool** command is versatile, it reports all kinds of good information for the network interfaces, physical and virtual. It also can be used to set many parameters and control the interfaces, which is out of our scope.

• **netstat** – The **netstat** command can be used to show many things, including the Kernel Interface Table, which will show details regarding the local network interfaces on the system.

• **/sys/class/net/<device>/statistics** – The raw statistics that are in /sys are the same general ones shown in the **ethtool** command output, with some minor differences, and there are MORE statistics in this directory set than are shown in the ethtool -S statistics.

Note

There is a LOT that goes into understanding [dropped packets](#ch19.xhtml_key02-a), like a knowledge of how Ethernet works overall, what packets are and how they collide, are filtered etc. The Linux+ Objectives LOVE to ask you about sub-items and leave the authors of this kind of work to fill in the hard stuff. Sigh.

##### Diagnosing with the **ethtool** Command

While you CAN view the raw statistics from the /sys/class/net/device/statistics directory and it's files/contents, the **ethtool** command has a very useful statistics option that is very easy to use, as shown in [Figure 19-5](#ch19.xhtml_ch19fig05), where we show the output of the **ethtool -S** command.

![Description: A screenshot of a computer Description automatically generated](graphics/19fig05.jpg)

**Figure 19-5**–The output of the **ethtool -S <interfacename>** command

The **ethtool** command can be used to view the NIC (Network Interface Card) statistics like is shown in [Figure 19-5](#ch19.xhtml_ch19fig05), or you can filter those using the **grep** command similarly to what is shown in [Example 19-6](#ch19.xhtml_exe19_6).

**Example 19-6**–An Example of **ethtool -S statistics <device>** output

```
$ ethtool -S enp0s2 | grep -i 'drop'
rx_queue_0_drops: 0
rx_queue_0_xdp_drops: 0
tx_queue_0_xdp_tx_drops: 0
```

In [Example 19-6](#ch19.xhtml_exe19_6) you see we are looking for any instances of lines that contain the text "drop" and we get 3 lines that show there are no packets being dropped currently.

##### Diagnosing with the **netstat** Command

You can also run the **netstat** command to find out your drops and collisions, such as in [Example 19-7](#ch19.xhtml_exe19_7).

**Example 19-7**–Viewing the Kernel Interface Table using **netstat -i**

```
$ netstat -i
Kernel Interface table
Iface   MTU    RX-OK   RX-ERR RX-DRP RX-OVR  TX-OK  TX-ERR TX-DRP TX-OVR
Flg
enp0s2  1500   233716      0      0    0     80587    0      0      0
BMRU
lo      65536    5234      0      0    0      5234    0      0      0
LRU0
```

The Kernel Interface Table shows you a lot of good information by interface, with the lo interface being the localhost, and in Example 19-5 the enp0s2 is the eth0 equivalent on an Ubuntu virtual machine.

##### Diagnosing with the /sys/net/class/<device>/statistics Information

There is a more granular and less easy-to-read set of information you can consult for dropped packets and collisions, it lives in the /sys tree structure, deep down into the /sys/net/class/<device>/statistics directory and it's basically a set of files named revealingly, so you can basically look at the filename and know what statistic you are viewing data for.

A great way to understand the structure of this directory is to run the **tree** command against it, such as we're showing in [Figure 19-6](#ch19.xhtml_ch19fig06).

![Description: A screenshot of a computer program Description automatically generated](graphics/19fig06.jpg)

**Figure 19-6**–The output of the **tree** command on the /sys/net/class/enp0s2 directory.

It's incredibly difficult to find documentation for these values, you'd think that being as important as they are, there'd be a ready source that joyfully explains all you'd want to know about each one. Forgive the author for being cynical in a historically-informed manner, but this is why the author has been bugging the heck out of software engineers all his career. Documentation and explanation, while present in the software developer/software engineer community, is not as prevelant (or even nearly as complete) as you'd wish.

To get the most documentation that exists on these counters, visit the [kernel.org](http://kernel.org) documentation page for struct_rtnl_link_stats64, ([https://docs.kernel.org/networking/statistics.xhtml?highlight=tx_dropped#c.rtnl_link_stats64](http://docs.kernel.org/networking/statistics.xhtml?highlight=tx_dropped#c.rtnl_link_stats64)) and follow the links to the **sysfs-class-net-statistics** page ([https://www.kernel.org/doc/Documentation/ABI/testing/sysfs-class-net](http://www.kernel.org/doc/Documentation/ABI/testing/sysfs-class-net)) for even more slightly cryptic information regarding these counters.

##### Wrapping up Dropping Packets

Detecting dropped packets and collisions are similar to panning for gold, most of the time you'll find a few little items here and there, but when you are least expecting it, errors will crop up and be pretty obvious they are happening.

I recommend that outside of replacing malfunctioning hardware and gathering information, you try not to mess around with your networking, particularly using the **ethtool** command, it's possible to bollux up your interfaces and how they function to the point of having to reinstall drivers, if you're lucky.

#### Link Status

Networking happens on several layers, so you'll want to know how to check the status of a link on those various layers, it can be very helpful in determining where the issue is if a network device or link isn't showing up properly or is not apparently working.

#### Diagnosing and Fixing the Problem

Let's do this one by layer, starting with the lowest and going up, specifying the tools as we go.

Note

No longer is it as likely that you'll be able to find a blinking or steady green light on a NIC (Network Interface Card) to let you know all is well in networking, so much is either not local or is completely virtual, so instead of going old school first, we'll go all high-tech and stay there.

##### Layer 1 - Physical

At this layer, you're basically looking for if the cables or wires are actually present and conveying the signals they are supposed to be.

![Images](graphics/key_topic_icon.jpg)

The prime way to find out of things are working here is to use the **ip** command and it's link subcommand and options.

In [Example 19-7](#ch19.xhtml_exe19_7a) we show the output from the **ip link** command.

**Example 19-7**–Output from the **ip link show** command

```
$ ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode
DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state
UP mode DEFAULT group default qlen 1000
    link/ether ca:3b:cc:0e:10:69 brd ff:ff:ff:ff:ff:ff
```

The key part here is to look at the non-lo interface, in this case the enp0s2 (eth0 equivalent) and see if the "mode" has an "UP" preceeding it, which this interface does. This means the interface is up and connected.

Another method for this is to use the **ethtool** command to determine if the link is up, shown in [Example 19-8](#ch19.xhtml_exe19_8).

**Example 19-8**–Output from the **ethtool** command

```
$ ethtool enp0s2 | grep Link
Cannot get wake-on-lan settings: Operation not permitted
      Link detected: yes:ff
```

There are other settings that can be seen in the ethtool output for a given interface, but we're looking for the Link information and so have used grep to show just that. You can safely ignore the wake-on-lan message.

##### Layer 2 - Data Link

At this layer, we're not looking for if the link is up, we're looking around to see if this device can see other devices on the network, if it can't, there might be a VLAN (Virtual LAN) issue or it could be literally on it's own network.

Regardless, if we can see if it can find it's neighbors using the ARP (Address Resolution Protocol), basically shouting "HELLO? ANYONE THERE?" on the local network, then it'll help us understand what else might be wrong.

The important thing is to query the ARP table, which you can do with the plain **arp** command, or using the **ip neighbor show** command, as shown in [Example 19-9](#ch19.xhtml_exe19_9).

**Example 19-9**–Output from the **ip neighbor show** command

```
$ ip neighbor show
192.168.64.1 dev enp0s2 lladdr 3e:22:fb:91:6a:64 REACHABLE
```

In this output you'll see that there is a host that is reachable by the example host, and given the IP Address, it's probably a gateway, and in this case it is.

In [Example 19-10](#ch19.xhtml_exe19_10) you see the **arp** command showing similar information.

**Example 19-10**–Output from the **arp** command

```
$ arp -a
_gateway (192.168.64.1) at 3e:22:fb:91:6a:64 [ether] on enp0s2
```

As we suspected, this is a gateway we are seeing, and it's known that way to the arp table and command. You can have it display the IP Address instead of _gateway in the **Address** column.

Note

Keep in mind that the link status world has changed, there used to be a lot of use of the **ifstatus** command, but **ip link show** has mostly taken over from that command, it's not even installed by default on many distributions.

### Bandwidth Limitations

The rest of your computing environment can be a a very fast pace, but if your bandwidth or access to the rest of the world of computing is slow or has latency, it'll seem as if your computer is slow.

#### Bandwidth and Latency

![Images](graphics/key_topic_icon.jpg)

Bandwidth is the speed of the pipe or how much speed you can get from your router, WiFi or however you get your connection.

Latency CAN be part of that speed, obviously if you have a very slow connection from your location to your upstream provider, that will slow everything down.

The main issue with Bandwidth and Latency is that the latter can be affected or produced by MANY things out of your control.

#### Diagnosing and Fixing the Problem

Latency is usually determined by "feel" or the response you are getting is not meeting your expectations of how quickly or responsive your session should be, or has been and is not now. Ask hard-core gamers if their version of latency, aka "lag" is a factor and you'll get a resounding "YES!"

There are several utilities that will give you a good view into the situation of latency issues on your system, they are:

• **ping** – Described previously, use the **ping** command to see a very simple set of response times, anything in the high 2 digit (80-99 ms) is pretty long and anything above that indicates a fair amount of delay. The remoteness of the host can be a factor in this measurement.

• **traceroute** – Also described previously, use the **traceroute** command output to show you where delays are happening.

• **bandwidth analyzers** –There are several of these, the simplest is [www.fast.com](http://www.fast.com), run by Netflix, which will give you a quick speed indication, but not much else. This is somewhat akin to looking at the speedometer on your vehicle and assuming that since it SHOWS 190 MPH, that you can GO that fast. Another more informative one is [www.speedtest.net](http://www.speedtest.net) which gives you more metrics including upload and download speeds and you can typically choose a remote server to test against.

• **hping3** – Created by Antirez, the hping3 utility can be used to get more information than it possible with the **ping** command, and also some other interesting capabilities that include IP Address spoofing and sending randomize traffic as a way to test a host.

Note

Determining Latency and it's relationship with Bandwidth is mostly using the tools listed to find out where the slowdown or throttle-point is, and seeing if you can relieve it. Often people will complain they have latency, all while being in a location like a coffee-shop where the people around them are doing all kinds of video and downloading of ISO and movie files etc. Have to know what is going on around you as well, in order to make good determinations as to what the problem is.

### Name Resolution Issues

The resolution of host and domain names is so important that the Internet as we know it wouldn't really be possible without it. The centralization or the heirarchical organization of world-wide [name resolution](#ch19.xhtml_key06-a) is a very good way to have all these names be handled, not without a lot of work, but with much less work than constantly trying to manually update all the names attached to hosts you need to reach.

#### The Trifecta of DNS

One of my favorite sets of files is the ones that affect [DNS (Domain Name Services)](#ch19.xhtml_key07-a) or how names are resolved on your system.

![Images](graphics/key_topic_icon.jpg)

We covered those files, **/etc/hosts**, **/etc/resolv.conf** and the **/etc/nsswitch.conf** file in [Chapter 05](#ch05.xhtml_ch05) - Using Network Tools and Configuration Files, so please review them there.

Effectively, if you are troubleshooting your name resolution it's because you are not able to use host or domain names to get where you are going.

#### Diagnosing and Fixing the Problem

The process of troubleshooting what the issue is may be as simple as the following steps:

**Step 1.** Ping the remote system by name, aka [www.example.com](http://www.example.com)

**Step 2.** If you don't get a valid response, try pinging it by the IP Address, which you may not have, but MAY show up in the failed name ping

**Step 3.** If that doesn't work, view your /etc/hosts file and look for an entry there that would inaccurately try to resolve the remote host's name

**Step 4.** If nothing there, show the contents of the /etc/resolv.conf file and ensure those DNS servers are valid, can be contacted via ping and will respond to a **dig** command

**Step 5.** If the host is responding, try looking to see if there is an A record that corresponds to that host's name, such as the www host at [example.com](http://example.com).

This can be done like the **dig** command in [Example 19-11](#ch19.xhtml_exe19_11).

**Example 19-11**–Output from the **dig** command

```
$ dig www example.com
; <<>> DiG 9.16.1-Ubuntu <<>> www example.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 53331
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.                           IN      A

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Thu Dec 29 17:33:31 MST 2022
;; MSG SIZE  rcvd: 32

;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 30864
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;example.com.                   IN      A

;; ANSWER SECTION:
example.com.            3075    IN      A       93.184.216.34

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Thu Dec 29 17:33:31 MST 2022
;; MSG SIZE  rcvd: 56
```

In the output in [Example 19-11](#ch19.xhtml_exe19_11), we have requested the A or Address record type for the www host at the example.com domain or site. **dig** has gotten us a lot more than we truly need, but the bolded sections in the output contain our answer to the query, which is; is there a host named www at the example.com domain and what is it's IP Address, mostly so we can ping that directly.

Note

If you can't ping by name a host on your local network, but can a remote host, then it's a local network or DNS server issue, likely, but check the /etc/hosts. If you can ping a lot of other hosts, local and remote, but not a particular one, it's that system or it's name resolution that is the issue.

### Testing Remote Systems

Testing aka "probing" remote systems is a great way to get into a LOT of trouble, as certain activities are considered at the VERY least inappropriate and at worst can constitute an attempt to hack or penetrate a remote system.

#### How (not) to Break the Law

Checking your local laws before using nmap in particular is highly recommended and there are a LOT of resources on the web that will caution you about how you should NOT use nmap and other tools to test remote systems.

![Images](graphics/key_topic_icon.jpg)

The key is simply this: Secure WRITTEN authorization before testing a system that you do not personally own. Period.

You can get a copy of the Open Source Security Testing Methodology Manual at the ISECOM site, it contains a very clear methodology that you can follow to make sure you are not breaking laws and causing yourself or others harm using probing tools like NMAP.

OSSTMM Site: [https://www.isecom.org/research.xhtml#content5-a0](http://www.isecom.org/research.xhtml#content5-a0)

#### Testing a Remote System (for what?)

Why would you want to test a remote system? For security purposes, absolutely. But what else might you want to know about a system that is remote, aka other than the one you're using to test?

![Images](graphics/key_topic_icon.jpg)

Reasons to query or test remote systems:

• Network Mapping

• Port State Discovery

• Ghost or Shadow Device Detection

• Operating System Inventory

• Service Discovery

• Vulnerability Inventory

#### Testing Remote Systems with NMAP

On your own corporate network, using NMAP for the previously listed tasks is quite reasonable, there are many examples of each of these that are discussed and demo'ed in the NMAP official book, the online version of which is available at the NMAP.org site: [https://nmap.org/book/toc.xhtml](http://nmap.org/book/toc.xhtml).

Getting NMAP on your system is usually really easy, it's available in the package repositories for most of the major and many of the minor distributions.

Running NMAP is fairly easy, at least on the lower end of functionality, it can get EXTREMELY complex on the command line as you expand what you're asking NMAP to accomplish.

##### Running a Simple System Scan

I own my own network and have access to a lot more for work, but I am incredibly aware of how quickly I could get into trouble areas with my organization and even the ISP I use to get my data to my work networks, if I start port-scanning without their knowledge.

Let's run a simple scan on a local target host and see what NMAP can tell us about that host, you may be surprised at how much we get from a supposedly-secure Linux system! The results of our scan of the target host are shown in [Example 19-12](#ch19.xhtml_exe19_12).

**Example 19-12**–Output from a simple nmap scan of the target host

```
$ nmap -v 192.168.64.2
Starting Nmap 7.80 ( https://nmap.org ) at 2022-12-31 19:04 MST
Initiating Ping Scan at 19:04
Scanning localhost (127.0.0.1) [2 ports]
Completed Ping Scan at 19:04, 0.02s elapsed (1 total hosts)
Initiating Connect Scan at 19:04
Scanning localhost (127.0.0.1) [1000 ports]
Discovered open port 80/tcp on 127.0.0.1
Discovered open port 22/tcp on 127.0.0.1
Completed Connect Scan at 19:04, 0.15s elapsed (1000 total ports)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00073s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.24 seconds
```

In [Example 19-12](#ch19.xhtml_exe19_12), you can see that we have scanned the target host and found immediately that two ports are open out of the 1,000 scanned in a very short time.

We found that Ports 22 and 80 are open, so SSH and HTTP are allowing incoming traffic on this host and that's more than we could have gotten with a simple ping.

##### Running a Service Discovery Scan

Now that we have a couple of ports that show as open, we can get more information on those services using nmap and it's slightly more advanced scanning features.

The results of our scan of the target host are shown in [Example 19-13](#ch19.xhtml_exe19_13).

**Example 19-13**–Output from a simple nmap scan of the localhost

```
$ nmap -sV -p 22,80 192.168.64.2
Starting Nmap 7.80 ( https://nmap.org ) at 2022-12-31 19:18 MST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0022s latency).
Other addresses for localhost (not scanned): ::1

PORT   STATE SERVICE VERSION
22/tcp open  ssh  OpenSSH 8.2p1 Ubuntu 4ubuntu0.4(Ubuntu Linux; protocol
2.0)
80/tcp open  http nginx 1.18.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at
https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.99 seconds
```

In the output shown in [Example 19-13](#ch19.xhtml_exe19_13), you can now see that we have some information about the service that's running on each port, along with the version, and this is valuable information, as an attacker would want to know what version of OpenSSH or NGINX you are running, in case there are vulnerabilities that can be exploited in that particular version.

##### Running a Vulnerability Scan

Oh now the fun begins, since we know the target host has a couple of ports open and we have identified teh services running, let's do our final task in this section about NMAP, scanning and reporting back on vulnerabilities to those services.

The results of our vulnerability scan of the target host are shown in [Example 19-14](#ch19.xhtml_exe19_14).

**Example 19-14**–Output from a vulnerability scan of the target host

```
$ nmap -P 80 -sV --script=vulners 192.168.64.2
Starting Nmap 7.80 ( https://nmap.org ) at 2022-12-31 19:53 MST
Nmap scan report for primary (192.168.64.2)
Host is up (0.0090s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux;
protocol 2.0)
| vulners:
|   cpe:/a:openbsd:openssh:8.2p1:
|       CVE-2020-15778    6.8   https://vulners.com/cve/CVE-2020-15778
|       C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3      6.8
        https://vulners.com/githubexploit/C94132FD-1FA5-5342-B6EE-
0DAF45EEFFE3  *EXPLOIT*
|       10213DBE-F683-58BB-B6D3-353173626207      6.8
        https://vulners.com/githubexploit/10213DBE-F683-58BB-B6D3-
353173626207  *EXPLOIT*
|       CVE-2020-12062    5.0   https://vulners.com/cve/CVE-2020-12062
|       CVE-2021-28041    4.6   https://vulners.com/cve/CVE-2021-28041
|       CVE-2021-41617    4.4   https://vulners.com/cve/CVE-2021-41617
|       CVE-2020-14145    4.3   https://vulners.com/cve/CVE-2020-14145
|       CVE-2016-20012    4.3   https://vulners.com/cve/CVE-2016-20012
|_      CVE-2021-36368    2.6   https://vulners.com/cve/CVE-2021-36368
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
| vulners:
|   cpe:/a:igor_sysoev:nginx:1.18.0:
|       OSV:CVE-2022-41742      0.0   https://vulners.com/osv/OSV:CVE-
2022-41742
|       OSV:CVE-2022-41741      0.0   https://vulners.com/osv/OSV:CVE-
2022-41741
|_      OSV:CVE-2021-3618 0.0   https://vulners.com/osv/OSV:CVE-
2021-3618
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at
https://nmap.org/submit/ .
Nmap done: 2 IP addresses (1 host up) scanned in 10.54 seconds
```

The great thing about a vulnerability scan is that it will not only show they exist, but give you the link to go see what it is that needs to be fixed!

Hopefully you can see what a great tool NMAP is, even if only scanning a single target host for standard ports, associated services and of course, anything that could be used for an attack on those ports and services.

#### Testing Remote Systems with s_client

Running, maintaining and accessing [OpenSSL](#ch19.xhtml_key10-a) servers can be a lot to handle, there's a fair amount of things to go wrong, so having a great tool like the s_client module to the **openssl** command can be very helpful in troubleshooting your OpenSSL servers and clients and their sometimes stormy relationships!

#### Verifying SSL Connection to a Remote System

The [s_client](#ch19.xhtml_key11-a) module will perform a large number of test and connection functions, probably the first of which would be to confirm that the remote system HAS an SSL certificate, and then view the contents of that certificate.

Running a simple verify query against a remote system is shown in [Example 19-13](#ch19.xhtml_exe19_13a).

**Example 19-13**–Output from a s_client verify of [example.com](http://example.com)

```
$ openssl s_client -verify_return_error -connect example.com:443
CONNECTED(00000003)
depth=2 C = US, O = DigiCert Inc, OU = www.digicert.com, CN = DigiCert
Global Root CA
verify return:1
depth=1 C = US, O = DigiCert Inc, CN = DigiCert TLS RSA SHA256 2020 CA1
verify return:1
depth=0 C = US, ST = California, L = Los Angeles, O =
Internet\C2\A0Corporation\C2\A0for\C2\A0Assigned\C2\A0Names\C2\A0and\C2\A0
Numbers, CN = www.example.org
verify return:1
---
Certificate chain
 0 s:C = US, ST = California, L = Los Angeles, O =
Internet\C2\A0Corporation\C2\A0for\C2\A0Assigned\C2\A0Names\C2\A0and\C2\A0
Numbers, CN = www.example.org
   i:C = US, O = DigiCert Inc, CN = DigiCert TLS RSA SHA256 2020 CA1
 1 s:C = US, O = DigiCert Inc, CN = DigiCert TLS RSA SHA256 2020 CA1
   i:C = US, O = DigiCert Inc, OU = www.digicert.com, CN = DigiCert Global Root CA
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIHRzCCBi+gAwIBAgIQD6pjEJMHvD1BSJJkDM1NmjANBgkqhkiG9w0BAQsFADBP
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMSkwJwYDVQQDEyBE
aWdpQ2VydCBUTFMgUlNBIFNIQTI1NiAyMDIwIENBMTAeFw0yMjAzMTQwMDAwMDBa
Fw0yMzAzMTQyMzU5NTlaMIGWMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZv
cm5pYTEUMBIGA1UEBxMLTG9zIEFuZ2VsZXMxQjBABgNVBAoMOUludGVybmV0wqBD
<output truncated, it's extremely long>
```

We've connected to the example.com server and requested to see their Certificate chain, which you can see in the output is locatd in Los Angeles, California and is managed by the ICANN organization.

#### Other Useful s_client Commands

Because of the extreme length of the s_client module's query responses from any valid OpenSSL host, we'll just detail a couple of key commands and their explanations instead of spend many pages on the output you'll shortly see if you try these commands out.

##### Commands to Use when Connected to a Host

![Images](graphics/key_topic_icon.jpg)

There are some commands you can use to perform various actions when connected via the s_client module to another host, they are:

• **Q** – End the SSL connection and exit the command

• **R** – Renegotiate the SSL connection session, certain protocols only

• **B** – Send a heartbeat message to the system

• **k** – Send a Key Update message to the system

• **K** – Send a Key Update message to the system, and request a Key Update back from the system

Note

There are MANY other things you can do with the s_client module, some simple and a lot of them fairly complex. Read the s_client man page for more than you probably want and certainly much more than you need for the Linux+ exam.

```
$ man s_client
```

##### Opening an SSL Connection to a Host

To open up an SSL connection to a host, and to get a LOT of useful information back, use the command:

```
$ openssl s_client -connect example.com:443
```

You'll have a lot of output, parse through it and notice how the query has been responded to, you can either use the commands or just quit the session.

##### Showing SSL Certificates on a Host

To show the entire certificate chain for a given host, use the command:

```
$ openssl s_client -connect example.com:443 -showcerts
```

You'll see the certificate information listed, just parse through it to find out more about the host and it's certifcate(s).

##### Testing a Particular TLS Version on a Host

There are times when you'll want to make sure that a given TLS version is available on hosts, to query just that, use the command:

```
$ openssl s_client -connect example.com:443 -tls1_3
```

I know we said no more outputs, but you'll want to verify from the previous query that the proper TLS information is shown in the SSL-Session: block, as shown in [Example 19-14](#ch19.xhtml_exe19_14a).

**Example 19-14**–Output from the openssl s_client TLS Version query

```
$ openssl s_client -connect example.com:443 -tls1_3
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID:
84BF20BB5699F250177C680D4A074B9DB7E8976099C1C6C5D6AF67A996D64
    Session-ID-ctx:
    Resumption PSK:
13005B8986AB6F6B74E89CE87B9497FBA20241110AA3F67D4A58E9D83
```

Notice the version of TLS we were querying for is present in the Protocol: portion of the query response.

### Summary

In this chapter you learned all about troubleshooting networks, from subnets and routing, to firewalls issues, to [interface errors](#ch19.xhtml_key01-a) like dropped packets and collisions. You learned how to understand the relationship between bandwidth and latency issues, how the Name Resolution system can have issues and how to understand where they can occur.

Additionally, you learned about testing remote systems with nmap, the scourge of the networks and tester of system and people's legal knowledge, as well as how to connect to remote SSL systems, query them for information, protocol support, show their certificates and much more.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 19-2](#ch19.xhtml_ch19tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 19-2**–Key Topics for [Chapter 19](#ch19.xhtml_ch19)

![Images](graphics/19tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[interface errors](#ch19.xhtml_key01)

[dropped packets](#ch19.xhtml_key02)

[collisions](#ch19.xhtml_key03)

bandwidth limitations

[high latency](#ch19.xhtml_key05)

[name resolution](#ch19.xhtml_key06)

[DNS](#ch19.xhtml_key07)

[Domain Name System](#ch19.xhtml_key08)

[nmap](#ch19.xhtml_key09)

[openssl](#ch19.xhtml_key10)

[s_client](#ch19.xhtml_key11)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** Which of the following is an example of a standard Class C subnet? Choose the best answer.

**a.** 255.0.0.0

**b.** 255.255.0.0

**c.** 255.255.255.0

**d.** 255.255.255.255

**2.** When testing a remote system, which of the following tools can you use to test if any services are responding on particular ports?? Choose all that apply.

**a.** ssh-connect

**b.** nmap

**c.** portscan

**d.** telnet

**e.** netbus

**3.** Which of the following is a primary cause of dropped packets?

**a.** RJ-11 error

**b.** E-Sim error

**c.** NIC error

**d.** Port Error

**4.** When you suspect a latency issue, you run a simple website tool that will show your connection's current bandwidth capabilities, what website does this?

**a.** [fast.com](http://fast.com)

**b.** [lagging.com](http://lagging.com)

**c.** [speed.com](http://speed.com)

**d.** [example.com](http://example.com)

**5.** You've been developing a website locally and have pushed the code to production, yet when you push more changes, you don't see the results. Which file may contain a hint as to why this is happening?

**a.** /etc/resolv.conf

**b.** /etc/services

**c.** /etc/nsswitch.conf

**d.** /etc/hosts

**6.** What command to the **openssl s_client** command will send a Key Update to the remote system and request it to send a Key Update back?

**a. B**

**b. Q**

**c. R**

**d. K**

## Chapter 20\. Analyzing and Troubleshooting CPU and Memory Issues

This chapter covers the following topics:

• [Runaway and Zombie Processes](#ch20.xhtml_ch20lev1sec03)

• [High CPU Utilization/Load Average/Run Queues](#ch20.xhtml_ch20lev1sec04)

• [CPU Times and CPU Process Priorities](#ch20.xhtml_ch20lev1sec05)

• [Memory Exhaustion and Out of Memory](#ch20.xhtml_ch20lev1sec06)

• [Swapping](#ch20.xhtml_ch20lev1sec08)

• [Hardware](#ch20.xhtml_ch20lev1sec09)

The exam objectives covered in this chapter are as follows:

• **Objective 4.3:** Given a scenario, analyze and troubleshoot central processing unit (CPU) and memory issues.

CPU and Memory are closely linked, one feeds the other and anytime you're experiencing Memory issues, such as [swapping](#ch20.xhtml_key08-a) or out of memory issues, that's going to affect the CPU.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 20-1](#ch20.xhtml_ch20tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 20-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/20tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** You see a process that is marked with a Z in the **STAT** column and realize it's a Zombie process. What phrase describes what has not happened at the Parent Process level for this process?

**a.** pausing

**b.** terminating

**c.** reaping

**d.** polling

**2.** You suspect your system has overly high CPU utilization as normal tasks are taking longer than usual and the system seems sluggish. Which tools will give you a quick overview of the system's CPU, Memory and other details on a refreshing display?

**a.** top

**b.** tail

**c.** stat

**d.** uptime

**3.** Which of the following commands displays the amount of time a process is taking up on the CPU?

**a. cpuinfo**

**b. syscpu**

**c. procps**

**d. iostat**

**4.** There is an quirkily-named process in the Linux kernel that is invoked to free up memory when there is a danger of the system becoming bogged down or not allow new processes to be created. What is the name of this process/component?

**a.** Texas Chainsaw

**b.** Chuckie

**c.** The Thing

**d.** OOM Killer

**5.** Swap for Memory can be configured via what two methods?

**a.** block

**b.** disk

**c.** register

**d.** file

**e.** xrecord

**6.** On a system that allows access to replaceable RAM SIMMS, what is the simplest way to troubleshoot a supposed Memory error?

**a.** Perform a 3" drop on the chassis

**b.** Press and hold the **Power** button

**c.** Reboot and hold down the **Shift** key

**d.** Shutdown and reseat the SIMMS

### Foundation Topics

### Runaway and Zombie Processes

Since we covered Processes and how to deal with them quite thoroughly in [Chapter 4](#ch04.xhtml_ch04),“Managing Processes and Services”, we'll just recap what they are and how to understand the difference between a normally-working process and a runaway or zombie, two very different extremes of process behavior.

#### Runaway Processes

![Images](graphics/key_topic_icon.jpg)

A [*runaway process*](#ch20.xhtml_key01-a) is a process that has either malfunctioned or is accidentally or maliciously creating copies of itself until the system becomes unresponsive or unusable due to the CPU load being taken over.

##### What Causes Runaway Processes?

Typically a program will be loaded, a process or processes will be created and when the main program exits, the child processes of that main process will be ended by the parent or main process.

There are multiple schedulers in Linux and an issue can occur with realtime or deadline processes where they can completely fence off or make useless any other process on the system by being a runaway.

Since about Kernel 2.6 or so, we have been able to set a couple of safety hatches for being able to kill off a runaway process that is using up all the CPU time and won't allow for a **kill** command from any process, aka the shell, that is running at a HIGHER priority than the runaway process!

Yes, it is entirely possible to have a runaway process or processes hang the system so badly that you cannot correct the situation, because you can't start or use a shell that can issue the kill or other process-ending commands.

##### Reserving Some CPU for Non-Realtime Processes

There are two files that exist in /proc that allow you to reserve an amount of CPU time for non-realtime or non-deadline processes, which are:

• /proc/sys/kernel/sched_rt_period_us

• /proc/sys/kernel/sched_rt_runtime_us

These two files contain integer values that are measured from -1 which means reserve no time, to whatever value you wish to set, all measured in microseconds.

This is very important, because unless you can reserve even a second or so, you won't be able to fit in a process that can kill a runaway process. No reserved time, no chance to run a non-realtime process such as a root shell to kill the runaway process!

For example, the default value for the /proc/sys/kernel/sched_rt_period_us file is 100,000 or a second, which will allow you to try to squeeze in a command from the shell.

##### Identifying a Runaway Process

One of the ways to identify a runaway process is when the system is racing or unresponsive and you can't hardly get a keystroke in.

Not all runaways take up the entire system, so if you have access to the command line, try using the **top** command and seeing what floats to the top of the chart of processes and kill it.

It's also possible to find these processes using the **ps** command, but nowhere as clear as with the **top** command. You can also use the very useful **htop** command, which gives you options that other tools don't and it's visually easy to understand and use.

##### Ending a Runaway Process

To end a runaway process, you could use the built-in "kill" options that the **top** or **htop** commands offer. You would first highlight the offending process, then press the **F9** key and the program will send a SIGTERM or -15 signal to attempt to kill that process, all within those programs.

To have the most control over the kill of a process, use the **kill** command and specify the -9 or SIGKILL signal.

#### Zombie Processes

Processes have a Parent Process, and often Child Processes. Even the kernel or the init process will have an entry for it's PPID or Parent Process ID, which will point to it's own process.

There are times when you'll see a process marked in **top**, **htop**, the **ps** command output etc. with a "Z" which denotes it's a Zombie Process.

![Images](graphics/key_topic_icon.jpg)

A [*Zombie Process*](#ch20.xhtml_key02-a) is one that has exited, died, or been terminated, but the Process Descriptor in the Process Table (a location in RAM holding the information about processes) has not been updated.

##### What Causes Zombie Processes?

A Zombie is not responsible for doing anything about it's being killed, ended or quit, other than sending to it's Parent Process that it's been terminated, stopped by a signal or resumed by a signal. The Parent Process is the one that is responsible to remove the Child Processes information from the Process Table, and if the Parent Process never uses the wait() syscall to retrieve the Child Process termination information, the Process Table is not updated, and a Zombie exists.

When a Child Process is marked as a Zombie, it hangs around "eating brains" or taking up a little bit of space in memory until it's cleaned up by the Parent Process.

There are also times when a Parent Process ends suddenly, and orphans all the Child Processes, which are then marked as Zombies.

##### Are Zombie Processes Bad?

No, they just exist, they're not bad or harmful, not unless there are a lot of them. A Zombie Process takes whatever memory it was using, and having them now and then is fairly normal and to be expected.

However, if you are consistently getting them or are seeing a number of them consistently, it can be a sign of a malfunctioning program or corrupted code.

##### Removing Zombie Processes

A Zombie Process can be removed by sending a particular signal to the Parent Process, such as in [Example 20-1](#ch20.xhtml_exe20_1).

**Example 20-1**–An Example of the **kill** command

```
$ kill -s SIGCHLD 12345

```

There may or may not be output from the command, but the signal SIGCHLD has been sent to the Parent Process which will cause it to go and reap the Zombies among it's Child Processes.

### High CPU Utilization/Load Average/Run Queues

Since the CPU, Memory, Caching and Disk are all so inter-related, or one feeds the other which feeds the next, a [*high CPU utilization*](#ch20.xhtml_key03-a) situation can be any or all of several things:

• Resource-intensive processes

• Poorly-written programs

• Memory leaks in programs

• Failing or over-burdened disk

The fix for high CPU utilization is to find what process(es) are the problem, and end them as described elsewhere, such as using the **kill** command.

#### High Load Average

The Load Average starts with understanding that the load of a Linux system is defined as what is currently the amount of CPU utilization or what's running at that given moment in time.

You can think of a load as a numeric measurement of the number of processes being executed, or even waiting for execution. You'll see that a smooth and consistent set of loads over time is preferable to highly variable or spiky loads due to heavy system demands and then nothing for a while, then another heavy demand etc.

Because the number that indicates the current load changes from almost instant to instant, the really significant number we can view is the Load Average, or the averaged number of processes being executed or in waiting over a period of time.

##### Viewing System Load Details with the **uptime** Command

One of the easiest ways to get the load numbers is to run the **uptime** command, which will bring back a series of numbers and other information such as [Example 20-2](#ch20.xhtml_exe20_2).

**Example 20-2**–Output from the **uptime** command

```
$ uptime
16:28:23 up 13 min,  1 user,  load average: 0.47, 0.15, 0.08
```

First you see the actual time the system has been or up, followed by the number of users and the 3 separate load averages which breaks down into:

**0.47** - This number is the load average for the last 1 minute

**0.15** - This number is the load average for the last 5 minutes

**0.08** - This number is the load average for the last 15 minutes

But the **uptime** command is sort of boring, it's just some text and it only runs once and you'd have to use the **watch** command to make it run more often. Make sure you try **uptime** with the **-s** or **--since** option, where you can view the starting or specified time the system has been running since.

##### Viewing System Load Details with the **tload** Command

Now let's go to the **tload** command, my favorite it's much more interesting and you can make it show some very useful information graphically, in a text method.

However, **tload** is initially just as uninspiring as the **uptime** command, running just the command itself yields even less information the uptime output, the main difference being that there is no user or up since information, though it does refresh itself until you use **Ctrl-c** to cancel it's operation.

To really get some good stuff out of **tload**, you should invoke it with the **-s** option and let it get rolling with displaying load via a side-scrolling graph made up of asterisks that represents the load on an ongoing basis.

To show the graphical chart, invoke tload as shown in [Example 20-3](#ch20.xhtml_exe20_3).

**Example 20-3**–Invoking the **tload** command with options

```
$ tload -s 100
0.04, 0.03, 0.03
```

You'll quickly see a set of asterisks begin to appear at the bottom left of the display, and slowly march across the screen from left to right. You can open up applications and move windows around if you are on a graphical system, just to see the results in the graph, similar to my system shown in [Figure 20-1](#ch20.xhtml_ch20fig01).

![Images](graphics/20fig01.jpg)

**Figure 20-1**–The output of tload with the -s 100 option

The user's computer needs to access the web server, and there is a firewall in the way, which be default will not send the user's request traffic to the web server.

As you can see, the load is being shown at intervals (which you can specify using the -d <value> option) on the screen.

It's good to experiment with the options for tload to get exactly what you want.

Notice the version of TLS we were querying for is present in the Protocol: portion of the query response.

Note

Let's not forget that our old friend the **top** command also shows the same kind of information as uptime does, just look in the top few lines for that information

### CPU Times and CPU Process Priorities

The concept of [*CPU Time*](#ch20.xhtml_key05-a) requires us to realize that the real measurement of time is what time has elapsed since the start of a task to the present or the end of the task, or Elapsed Time.

![Images](graphics/key_topic_icon.jpg)

Think of the difference between CPU Time and Elapsed time as Elapsed Time would be how long since you bought a vehicle, and CPU Time might represent the amount of time you actually DRIVE the vehicle.

Additionally, Elapsed Time is real time, slivers of seconds to minutes to hours to days, etc. Most computers have bursts of activity where the CPU Time represents being under load, or executing code, but that time is a relatively small or smaller fraction of the Elapsed Time.

The fix for high CPU utilization is to find what process(es) are the problem, and end them as described elsewhere, such as using the **kill** command.

#### Measuring CPU Time

To determine how much of the CPU Time is currently being used, or in effect, how much of the CPU is being utilized, you can use a couple of commands, one of which we have covered in detail elsewhere, the **top** command.

Another very important and useful utility is the **time** command, which measures the amount of time a command takes, and parses out what time was spent in what context or user or kernel space. [Example 20-4](#ch20.xhtml_exe20_4) shows the **find** command being run and the time statistics beind displayed.

**Example 20-4**–Output from the **time** command

```
$ time find / -iname *.doc 2> /dev/null
/snap/gnome-3-34-1804/77/usr/lib/python2.7/pdb.doc
/snap/gnome-3-34-1804/72/usr/lib/python2.7/pdb.doc
real 0m6.997s
user 0m0.676s
sys  0m1.800s
```

What we are doing is timing a command to see how long it takes in real time, but also how much of that time is spent accessing, updating, or displaying in user or system space for that CPU Time.

There are a HUGE number of output possibilities, all of which you can see in the man page for the **time** command.

The main thing you need to know about it is what it's measuring, and what the output shows you regarding the passage of real time (like the clock on the wall) and how much of that is taken up by the userspace and the system space for that command.

Note

Don't try to match the times up as a sum, but do read the man page for the **time** command, it'll teach you a lot about the system time and CPU utilization and how to report back on the characteristics you find most important.

Also keep in mind that running the exact same command multiple times may display shorter (in some cases, dramatically so) times after the first command is run. The system is caching from a disk block and filesystem perspective, and this will likely be the reason for the difference.

#### Important CPU Time Terms

There are some items that you will be tested on (potentially) that we should define, so that you know what is being asked about.

• **steal** - steal time refers to the amount of time that a virtualized OS wanted to execute something, but could not, as that time amount was being given to or used by another guest of the hypervisor.

• **user** - user time is the amount of time that is spent executing something that is located in the userspace or user-specific portion of the running Operating System.

• **system** - System time is amount of time that is spent executing something in the kernel portion of the system.

• **idle** - idle time refers to the amount of time that the system spent not being busy, or running the System Idle Process. Effectively, this means that the CPU was not being used in any meaningful capacity.

• **iowait** - iowait refers to the amount of time that the system was otherwise idle, but there was an unfulfilled or in-process disk I/O request.

#### CPU Process Priorities

We have covered Process Priority and how to manage those priorities for both starting a command (via the **nice** command), and remediating or altering a running commands priority, (via the **renice** command), in [Chapter 4](#ch04.xhtml_ch04), Section “*Managing Process Priorities”*.

Since that is already covered, we won't restate or rehash it here.

### Memory Exhaustion and Out of Memory

![Images](graphics/key_topic_icon.jpg)

The concept of [*Memory Exhaustion*](#ch20.xhtml_key06-a) typically means that the system has run out of both PHYSICAL RAM and Swap Space, which is how you fake out the programs that make them think the system has more RAM than it actually does.

Memory Exhaustion doesn't happen in a vacuum, if you have very little memory and constantly load that available memory up with running programs, eventually you'll reach a state where even a massive amount of Swap won't help you and everything grinds to a halt, usually accompanied with many error messages, one of which is shown in [Example 20-5](#ch20.xhtml_exe20_5).

**Example 20-5**–Logfile entries showing memory exhaustion

```
Allowed memory size of xxxxxxxx bytes exhausted (tried to allocate 62
bytes)
Allowed memory size of xxxxxxxx bytes exhausted (tried to allocate 39
bytes)
Allowed memory size of xxxxxxxx bytes exhausted (tried to allocate 62
bytes)
Allowed memory size of xxxxxxxx bytes exhausted (tried to allocate 39
bytes)
```

This isn't usually the first sign that something is going wrong, the system will likely seem very sluggish and unresponsive, there may be interface issues and service-response issues.

Memory Exhaustion works hand in glove with the next section, “What is [Out Of Memory(OOM)](#ch20.xhtml_key07-a)?”

Because a Linux system uses a multi-part system for what it calls memory, Swap (on disk or on the filesystem)and Physical RAM, it can get a little confusing at times.

We'll get into all of this in the next section, where we talk about Swap, caches and buffers and Virtual Memory.

### What is Out Of Memory (OOM)?

The OOM Manager (named out_of_memory(), rather obviously) is a process that runs and has a very focused set of tasks to perform. It is not invoked except in certain cases of working with memory requests, (expanding heap and certain remap functions), so it's a bit of a niche player, but important, and of course, it's in the Linux+ Objectives!

Note

The system attempts to not have to invoke the OOM Manager by harvesting old memory page frames, which may or may not be enough to handle the memory requests being made.

The first thing that happens is that the system will attempt to check if there is enough memory to fulfill a request for memory pages, and if the harvesting of old page frames isn't successful, the OOM Manager is kicked in and performs:

• Determine if there is enough available memory for a request

• If not enough, verify the system is really out of memory

• Select a process according to a number of determinants to kill to release memory page frames

Note

There exists a possibility that the system is NOT out of memory, but has gotten ahead of the ability to process Swap calls. The system goes through an extensive checklist once when it's called and before the process selects something to kill, it will go verify the steps again.

##### Memory Leaks

As discussed earlier in this chapter pertaining to High CPU Utilization, a memory leak can be from a malfunctioning program, just bad code or something malicious. Regardless, you'll find the system memory slowly being used up, then Swap (Virtual Memory) being used up and then the OOM process kicks in and eventually failure may happen.

##### The Process Killer

The process for killing a process to start freeing up memory pages is shown in the diagram in [Figure 20-2](#ch20.xhtml_ch20fig02).

![Images](graphics/20fig02.jpg)

**Figure 20-2**–OOM Killer Process Diagram

The scenario for the out_of_memory kill process is fairly complex and completely out of the scope of this discussion. The Linux kernel documentation site has a great deal of useful information about how this works, including a diagram from which [Figure 20-2](#ch20.xhtml_ch20fig02) was pulled.

Note

There exists a possibility that the system is NOT out of memory, but has gotten ahead of the ability to process Swap calls. The system goes through an extensive checklist once when it's called and before the process selects something to kill, it will go verify the steps again.

### Swapping

The concept of Swap is a relatively simple one that hides a wealth of details and complexity from the user, and in some cases the system administrator.

![Images](graphics/key_topic_icon.jpg)

Swap is where you declare a portion of the filesystem (a swap file) or a dedicated partition (swap partition) that becomes the overflow area for the actual system RAM.

**Physical system RAM + configure Swap = Virtual Memory**

As you see stated previously, the size of the actual physical RAM the machine holds is not the entirety of the memory that can be used for programs. However, you cannot actually have a running or executing program in swap, it's for storing things that are not needed by what is currently executing via the CPU.

You can run the **free** command and see what's going on with your system's RAM and Virtual Memory, and the combination of the two, which the system uses like a flexible pool for holding data for the processes and threads that are being executed currently (RAM) and those that have just gotten some time slices or are about to have a time slice of the CPU.

#### Swap, Caching and Buffers

The **free** command is used to determine the amount of free memory on a system, not just by displaying the amount of unused system RAM but also by giving you more detailed information about how much free and in-use physical memory you have, how much swap space or disk-based fake memory is in use, and how much of the used system RAM is being taken up by buffers and caches. It's these buffers and caches that can produce a lot of confusion at times.

You can see what the **free** command shows in [Example 20-6](#ch20.xhtml_exe20_6).

**Example 20-6**–Output from the **free** command with the -h option

```
$ ~ $: free -h
          total        used        free      shared  buff/cache
available
Mem:      3.8Gi       1.0Gi       1.2Gi       158Mi       1.6Gi
2.4Gi
Swap:     2.0Gi          0B       2.0Gi
```

There has always been a moment of realization that takes place for any Linux system user who looks at the output of a command like free right after starting the lab system and wonders "WHAT IS EATING UP ALL MY SYSTEM RAM???"

This was always one of my favorite moments in class, and I have always taken the time to explain that system RAM on a lightly utilized system is like a bus that is only half full of passengers: Every passenger has room in the seat next to him or her for magazines, snacks, and drinks and ample room to stretch out a bit. I then make the correlation between the passenger and a running process.

We point out that the room the passenger has allocated to her is similar to the working set (everything needed to run) for a process. The key here is that when lightly loaded, a system can allocate otherwise unused system RAM to handy and useful items such as cache and buffers, and the processes can stretch out a bit and have fully loaded working sets for efficient running of the processes.

#### Blocks and Buffers

![Images](graphics/key_topic_icon.jpg)

Key to the running of processes and the speed of processing on a system are blocks and buffers. Block devices such as disks have an addressable unit called a *block*. This is typically (though not always) 512 bytes in size. System software also uses a construct called a block, but it’s typically much larger than the physical size of a block on a hard disk or another block device.

When a disk block is read into system memory, it’s stored in a *buffer*. A buffer is associated with one and only one block, and that buffer is used to address the data contained in that block while in memory.

#### Pages, Slabs, and Caches

The kernel uses *pages* to manage memory on a system. The processor can address very small units of memory (such as a “word” or “byte”), but the memory management unit uses pages and only addresses memory in page-sized chunks. The kernel addresses every single page of the memory in the struct_page table and includes in the table information that is critical to managing that page in each page’s entry.

Pages are frequently populated with the same data, read from buffers and written back to *caches* for later reading. The system manages its own structure and marks pages as being used or free; the system can also use a number of other flags or parameters, but they are not important in this conversation.

Caches are made up of *slabs*; a slab is typically one page, though it can be multiple contiguous pages. To illustrate the relationship between a cache and a slab, we can say that a cache is like a city, a slab is like a neighborhood, and a page is like a block in that neighborhood.

To sum this all up, blocks are data locations on disk, blocks are read into buffers when a file or set of files is requested from disk, and then when those buffers are read into a page in memory, that page is a part of a slab or set of slabs that make up a cache.

To continue the bus and passenger analogy from earlier, remember that a lightly loaded system shows a large utilization of RAM but also a correspondingly hefty use of cache and buffers, while a heavily loaded system, with many processes running, shows a lot of RAM in use but relatively low cache and buffers. Effectively, as you load up the system with more processes, all the passengers/processes have to tighten up their working sets; put their magazines, snacks, extra luggage, and drinks in the overhead rack or under the seat; and be respectful of their fellow passengers/processes.

#### How Much Swap Is Enough?

In some ways this is like asking which car is better than another? I have been around Linux since it's beginnings and have seen this change more times than a Youtube Influencer changes outfits for a video shoot!

[Table 20-2](#ch20.xhtml_ch20tab2) contains a simple guide, taken from a Opensource.com survey that was run with a high number of respondents, so there is safety and data in numbers, hmm?

**Table 20-2**–How much swap is recommended

![Images](graphics/20tab02.jpg)

As you can see, even with a handy guide such as [Table 20-2](#ch20.xhtml_ch20tab2), it can be slightly unclear in some situations. The **Hibernation** column is primarly for those system which will be using the Hibernation option, which shouldn't be Servers and high-end Workstations.

### Hardware

There are a couple of utilities that can be used to gain more information about your [*hardware*](#ch20.xhtml_key09-a), especially the CPU and Memory/RAM.

#### Viewing CPU Info

The **lscpu** command read the CPU information from the /sys and /proc/cpuinfo locations and formats it for a human to read. The default is a lot of output, and so might be better to run by piping it to the **less** command as shown in this command line:

```
$ lscpu | less
```

Another extremely useful option that I use a lot is the Caching display option, or -C, which shows information for the various levels of caches, shown in [Example 20-7](#ch20.xhtml_exe20_7).

**Example 20-7**–Output from the **lscpu -C** command

```
$ lscpu -C
NAME ONE-SIZE ALL-SIZE WAYS TYPE        LEVEL  SETS PHY-LINE COHERENCY-
SIZE
L1d       32K      64K    8 Data            1    64        1
64
L1i       32K      64K    8 Instruction     1    64        1
64
L2       256K     512K    4 Unified         2  1024        1
64
L3        16M      16M   16 Unified         3 16384        1
64
```

#### Viewing Memory Info

The **lsmem** command read the system memory information from the /sys and /proc/meminfo locations and formats it as well as it can, but it's pretty technical in nature. There isn't that much output, but at least it's cryptic, as you can see in [Example 20-8](#ch20.xhtml_exe20_8).

**Example 20-8**–Output from the **lsmem** command

```
$ lsmem
RANGE                                  SIZE  STATE REMOVABLE BLOCK
0x0000000000000000-0x00000000afffffff  2.8G online       yes  0-21
0x0000000100000000-0x000000014fffffff  1.3G online       yes 32-41

Memory block size:       128M
Total online memory:       4G
Total offline memory:      0B
```

### Summary

In this chapter you learned all about Troubleshooing the CPU and Memory on a Linux system. We covered a lot of topics including Runaway and Zombie Processes, High CPU Utilization and the associated [High Load Averages](#ch20.xhtml_key04-a) and High or Long Run Queues. We looked at CPU Times and CPU Process Priorities and Memory Exhaustion and Out of Memory states.

Additionally, you learned about Swap, it's associated caches, blocks, buffers and how all this affects and is affected by the physical system RAM.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 20-3](#ch20.xhtml_ch20tab3) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 20-3**–Key Topics for [Chapter 20](#ch20.xhtml_ch20)

![Images](graphics/20tab03.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[Runaway Processes](#ch20.xhtml_key01)

[Zombie Processes](#ch20.xhtml_key02)

[High CPU Utilization](#ch20.xhtml_key03)

[High Load Average](#ch20.xhtml_key04)

[CPU Times](#ch20.xhtml_key05)

CPU Process Priorities

[Memory Exhaustion](#ch20.xhtml_key06)

[Out Of Memory (OOM)](#ch20.xhtml_key07)

[Swapping](#ch20.xhtml_key08)

[Hardware](#ch20.xhtml_key09)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** Which of the following commands will show you a table of available and used system RAM, swap, buffers and caching information?

**a. meminfo**

**b. bufflist**

**c. free**

**d. lsmem**

**2.** When a child process has exited but it's entry in the process table has not been cleared by it's parent process, that process is called a _______?

**a.** Abandoned

**b.** Orphan

**c.** Zombie

**d.** Loose

**3.** You've started a process and through investigation, you find that it's consuming more an the usual amount of system resources. It's important and timely, so you don't want to just kill it and start over. Which of the following commands will allow you to affect the priority of this process as it's running?

**a. renice**

**b. procadj**

**c. sig**

**d. ps**

**4.** When your system needs to attempt to clear enough memory page frames to fulfill a request for memory usage and cannot, what overall process is called and used to attempt to fix this situation?

a. select_bad_process

b. badness

c. force_sig

d. out_of_memory

**5.** You're convinced that your system doesn't have enough swap space configured and you want to add some without interrupting the workloads that are in process. Your system has a single internal disk that is fully-allocated but has free space on it. What method of swap can you safely add?

**a.** hardware-based

**b.** software-based

**c.** partition-based

**d.** filesystem-based

**6.** The **lscpu** command reads data from what /proc-based file?

**a.** cpustats

**b.** cpudetails

**c.** cpugrep

**d.** cpuinfo

## Chapter 21\. Analyzing and Troubleshooting User and File Permissions

This chapter covers the following topics:

• [User Login Issues](#ch21.xhtml_ch21lev1sec03)

• [User File Access Issues](#ch21.xhtml_ch21lev1sec04)

• [Password Issues](#ch21.xhtml_ch21lev1sec05)

• [Privilege Elevation Issues](#ch21.xhtml_ch21lev1sec06)

• [Quota Issues](#ch21.xhtml_ch21lev1sec07)

The exam objectives covered in this chapter are as follows:

• **Objective 4.4:** Given a scenario, analyze and troubleshoot user access and file permissions..

Since everything on a Linux system is a file, right down to the filesystem objects, making sure your users have proper access to those files, and blocking improper access, is key.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 21-1](#ch21.xhtml_ch21tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 21-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/21tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** A new web designer who isn't familiar with how Linux works tries to sign on as the user nginx, and sends you a request to reset the password. You explain to the user that no one is allowed to login as a _______ account. Choose the missing word or phrase.

**a.** user

**b.** login

**c.** service

**d.** access

**2.** A user has signed in with their usual account ID but needs to temporarily change over to a different ID. Which command would keep them from having to logout and then back in again as that secondary account?

**a. su**

**b. id**

**c. ip**

**d. df**

**3.** A user has been migrated from another system and is having an issue with their password. Upon displaying the /etc/passwd entry for that user, you find the expected x in the 2nd column, but in the /etc/shadow, you will likely find a ___ character, showing the user has not set a password yet. Choose the character that denotes this.

**a.** #

**b.** @

**c.** %

**d.** !

**4.** Since you'd rather be boiled alive than give one of your regular users the root password, what utility will allow you configure their ability to run various programs as if they were the root user, but not have any knowledge of the actual password?

**a.** rootme

**b.** newuser

**c.** su -i

**d.** sudo

**5.** A user mentions they had expected to be restricted from using over a certain amount of disk space, but were able to save and store more than that, and wants to know why? What feature or option of Quota management is responsible for this apparent lack of restriction?

**a.** weak save

**b.** soft limit

**c.** grace period

**d.** block restriction

### Foundation Topics

### User Login Issues

Nothing is as irritating to a user than not being able to login, and of course they'll spread that irritation to the IT people, it's all part of being a user!

#### User Login Process

The [*user login*](#ch21.xhtml_key01-a) process and much more about users, groups and their management can be found in [Chapter 9](#ch09.xhtml_ch09), “[Implementing Identity Management.](#ch09.xhtml_ch09)” With a familiarity from reading that chapter and viewing all the examples, we can move straight into the most common login issues that users will experience and how to not have them happen, or fix them when the do.

#### Inspecting Account Details

Before you go running off in several directions about users not being able to login, it is important to be able to look at a user's account particulars and see if all is right, or is there a problem.

To truly understand what's going on with a user and their signon issues, you need to run at LEAST the following 3 commands to get enough information to make an informed and accurate picture of that user's world looks like.

##### ID Please

The **id** command is very useful since it will display a wealth of information for any user, as you can see in [Example 21-1](#ch21.xhtml_exe21_1).

![Images](graphics/key_topic_icon.jpg)

**Example 21-1**–An Example of **id** Command Output

```
$ id
uid=1000(rossb) gid=1000(rossb) groups=1000(rossb),4(adm),20(dialout),
24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),117(
netdev),118(lxd)

```

The first key value is the uid, which stands for User ID, and that is shown matched up with the username, as configured in the /etc/passwd or other name services database.

The second value is the gid, which stands for the Primary Group ID, in other words, the group ID that would be used as the Group Owner if this account created the typical file or directory.

The third value is the groups, which stands for the Secondary Groups this user is a member of, but are NOT the Primary Group.

What you're looking for here is anything out of the ordinary, and especially if you

##### Get Entity

The **getent** command is additionaly quite useful since it will query a database such as the /etc/passwd or /etc/shadow file and return information like you see in [Example 21-2](#ch21.xhtml_exe21_2).

![Images](graphics/key_topic_icon.jpg)

**Example 21-2**–An Example of **getent** Command Output

```
$ getent passwd rossb
rossb:x:1000:1000:RossB:/home/rossb:/bin/bash
$ sudo getent shadow rossb
rossb:!:19051:0:99999:7:::
```

The query to the passwd file shows data for the rossb account, which you will likely inspect and say to yourself "But Ross, this is exactly what I would have gotten if I had run the **grep** command against the /etc/passwd file and searched for the user rossb. And you'd be right.

Note

Also VERY important is that there be a valid shell as the last field in the entry in the passwd file. If there is not, they can't login. Take a look at the /bin/false and /sbin/nologin information in [Chapter 9](#ch09.xhtml_ch09), those re designed to change the user's ability to login dramatically.

The second query, that to the shadow file is necessary to run as root, since that file is NOT publicly-accessible, if you ran it without the **sudo** command all you'd get is a blank return, no error.

In the shadow file you see what may indeed be a problem for this user trying to login, there is an x in the **password** column in the /etc/passwd file, as there should be, but there is the all-important ! in the **password** column in the /etc/shadow file, which means this user has NOT had a password set!

Note

Rather amusingly, I have had a student ask me why in a case like this, doesn't the system just prompt the user to set a password when they try to login? As I gazed at them, contemplating how to answer, they suddenly nodded and said "Oh, yeah, right, then anyone could set a password for that user...." Bingo, they won the prize!

#### Case-Sensitivity

Let's face it, if you know about case-sensitivity in Linux, you know. If you don't, you will soon become very aware of how important even a single upper/lower case character can be.

If you're logging in to a remote system that is Linux-based, and your main system is running Windows, at least you've got a step in the right direction! In all seriousness, many users will have the same username or login on both Windows and Linux systems, but Windows is not case-sensitive except in very certain spots, and login is not one of them.

If your home system is used to supplying automatically your login name at any prompt, it may do so when you attempt to remotely login in or use a webform to access a Linux system, which will fail due to the initial capitalized letter of your Windows login.

#### How Can I Fix This?

You usually can't. The lack of upper/lower sensitivity is so endemic or "baked-in" to Windows that you may not be able to find where to cause this to be different.

The key thing is to realize that if you are logging in or presenting credentials, BOTH the username and password are exquisitely and exactly case-sensitive.

#### Has the User Ever Logged In?

Sometimes you just know the user has never logged in, such as when they are new, but there are times when you know the user logs in regularly and you'll need to know that information

##### The **last** Command

![Images](graphics/key_topic_icon.jpg)

The **last** command is used to show you a listing of output that lets you see what has happened last on the system, such as who has signed in, from what port, what they might have been running etc.

It's very helpful to see a reverse-chronological order of things that could be important, in particular when the system was last booted, and who's still signed in, as you can see in [Example 21-3](#ch21.xhtml_exe21_3).

**Example 21-3**–An Example of **last** Command Output

```
$ last | head
ubuntu   pts/0        192.168.64.1     Sun Feb 12 20:31   still logged in
ubuntu   pts/0        192.168.64.1     Sun Feb 12 20:29 - 20:31  (00:01)
ubuntu   pts/0        192.168.64.1     Fri Feb 10 15:28 - 17:00  (01:31)
reboot   system boot  5.4.0-99-generic Fri Feb 10 15:20   still running
ubuntu   pts/0        192.168.64.1     Sun Jan 15 22:21 - 22:17  (23:55)
reboot   system boot  5.4.0-99-generic Sun Jan 15 22:09   still running
```

##### The **lastlog** Command

Also quite useful but with some different information is the **lastlog** command, useful for a listing of users and their login status, date and time, port from and IP Address if discernable.

[Example 21-4](#ch21.xhtml_exe21_4) shows the lastlog default output.

**Example 21-4**–An Example of **lastlog** Command Output

```
$ lastlog | tail
tss                                        **Never logged in**
uuidd                                      **Never logged in**
tcpdump                                    **Never logged in**
sshd                                       **Never logged in**
landscape                                  **Never logged in**
pollinate                                  **Never logged in**
systemd-coredump                           **Never logged in**
ubuntu           pts/0    192.168.64.1     Sun Feb 12 20:31:34 -0700 2023
lxd                                        **Never logged in**
dnsmasq                                    **Never logged in**
```

This is very useful, but there is a trick you can pull using the **grep** command that will allow you to determine only who HAS logged in, screening out all those service accounts with the "Never logged in" message.

[Example 21-5](#ch21.xhtml_exe21_5) shows the lastlog output filtered with the **grep** command to show only the accounts that have successfully logged in.

**Example 21-5**–An Example of **lastlog | grep -v** Command Output

```
$ lastlog | grep -v "Never logged in"
ubuntu           pts/0    192.168.64.1     Sun Feb 12 20:31:34 -0700 2023
```

Now THAT is some seriously useful information to get. You don't have to sort through a couple of dozen service accounts just to see what user accounts have successfully logged in, AND you can look for service accounts that show up as HAVING logged in, a sure sign of an error or a hack/crack on the system.

### User File Access Issues

Group issues can be even more hard to track down and troubleshoot than user login issues, since login is a 1 or 0, but group issues can feel like they're happening periodically.

#### Group Issues

One of the issues that can evade casual inspection is if the user is in the proper [*group*](#ch21.xhtml_key03-a) that has been assigned to have access to a resource.

The simplest way to find out what groups a user is a member of is to issue the **groups** or **id** command with that username as an argument, such as in [Example 21-6](#ch21.xhtml_exe21_6).

![Images](graphics/key_topic_icon.jpg)

**Example 21-6**–An Example of **groups** Command Output

```
$ groups rossb
rossb : rossb adm dialout cdrom floppy sudo audio dip video plugdev netdev
```

You should then inspect the **ls -l** output of the resource (or use ls -ld for a directory) and see if that group is listed in the middle 3 rwx positions as having at least r or read permissions. You can read more about the other tools you may need to use in [Chapter 2](#ch02.xhtml_ch02), “[Managing Files and Directories](#ch02.xhtml_ch02),” such as the **chmod** command, which you'd use to make any needed adjustments to the permissions for the group on the resource.

#### Context Issues

[*Context*](#ch21.xhtml_key04-a) issues occur within the realm of AppArmor or SELinux, and can be complex to troubleshoot. It's recommended that you consult [Chapter 12](#ch12.xhtml_ch12), “[Understand and Apply Access Controls](#ch12.xhtml_ch12),” for more information about how these two security context methods are applied and how you can troubleshoot them.

#### Permission Issues

[*Permissions*](#ch21.xhtml_key05-a) are much simpler in Linux than they are in Windows, which is where a lot of confusion comes from. Not Windows, but the difference between how Windows applies and manages permissions on files and directories and how Linux does.

In [Chapter 2](#ch02.xhtml_ch02), you'll find a very full-featured discussion of permissions and how to view them, change them and confirm them, all of which are the most likely actions you'd take to remediate a permissions issue.

#### ACL (Access Control List) Issues

Once again, when it comes to [*Access Control List or ACL*](#ch21.xhtml_key06-a) issues, [Chapter 12](#ch12.xhtml_ch12) is where you'll find the best discussion of how ACL's work, how they are used and how to read and troubleshoot them.

#### Attribute Issues

File [*attributes*](#ch21.xhtml_key07-a) are a kind of hazy situation where a special attribute has been set on a filesystem object, such as a file that has been set as being "append only" where it cannot be overwritten, only added to. Another very common attribute that is set, especially on filesystems that undergo a very high set of read traffic, such as a web server, is the noatime attribute, where the reading of a file does NOT update the atime file information, which you can see along with the other two times, mtime and ctime, using the command shown in [Example 21-7](#ch21.xhtml_exe21_7).

**Example 21-7**–An Example of the **stat** Command Output

```
$ stat file1
  File: file1
  Size: 0            Blocks: 0          IO Block: 4096   regular empty file
Device: fc01h/64513d Inode: 258226      Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/  ubuntu)   Gid: ( 1000/  ubuntu)
Access: 2022-06-01 23:15:35.864502122 -0600
Modify: 2022-06-01 23:15:35.864502122 -0600
Change: 2022-06-01 23:29:41.424625649 -0600
 Birth: -
```

As you can see, the three times are towards the bottom of the output, and are labeled Access (atime), Modify (mtime) and Change or (ctime.)

![Images](graphics/key_topic_icon.jpg)

To see the special attributes on a filesytem object, use the **lsattr** command against that object like you see in [Example 21-8](#ch21.xhtml_exe21_8).

**Example 21-8**–An Example of the **lsattr** Command Output

```
$ laattr file1
------dA------e----- file1
```

As you can see, the "do not dump", "no atime updates" and "extent format" attributes are set on the humble file1.

Other attributes of note:

• s or Secure Updates is a secure wipe, where when that file is deleted, the filesystem mechanism overwrites it's disk resources with zeros and writes those back to disk.

• d or No Dump means don't backup this file if the **dump backup** command is used.

• i or Immutable, as in the file is set to be unchangeable, and must be set to be mutable to make any changes.

• e or Extents are being used for mapping the blocks on disk for this file.

Special attributes may not be obvious, and usually only show up on Ext filesystems, other filesystems may not allow the setting of any or all of these special attributes.

Best place to get more attribute information is the chattr (1) and lsattr (1) man pages.

#### Policy/Non-Policy Issues

Once again, the Linux+ Objectives are not very specific, or even helpful in determining what [*Policy*](#ch21.xhtml_key08-a) or [*Non-Policy*](#ch21.xhtml_key09-a) issues are being asked about.

What does occur to this author, and something I have seen before is what I will term "Silent Access Issues" which are usually related to having SELinux turned on and not getting anything from the logs about access being denied to a resource.

SELinux attempts to reduce the number of false positives that occur when a service over-queries it's access, and as such uses a thing called "dontaudit" rules, which results in a service being denied access but it being mis-reported or most importantly, not reported at ALL!

If you find yourself in such a situation, you can disable your "dontaudit" rule and cause such access attempts to be logged with the command:

```
$ semodule -DB
```

This will disable the "dontaudit" policy rule with the -D option, and also rebuild the policy via the -B option.

Now you can run the program, service or command and watch the SELinux logs for more useful troubleshooting messages.

To re-enable the "dontaudit" policy, simply rebuild the policy overall with the command:

```
$ semodule -B
```

### Password Issues

Outside of the main issue which is that users cannot seem to remember their [*passwords*](#ch21.xhtml_key10-a) from day-to-day, and that's no joke, there are a couple of issues that occur that can be relatively easy to fix.

When a user's password ages out, there are several opportunities to change it, or to fail to change it and I have rarely had a user admit they have put the change off until it's either too late, or just bobble the password change enough times that the system won't let them in.

#### The **faillog** Command

A utility that I highly recommend running every day, even to having it mail you the output, is the **faillog** command.

The **faillog** command can be run by itself , or specify a user such as:

```
$ sudo faillog -u rossb
```

![Images](graphics/key_topic_icon.jpg)

The **faillog** command can be very helpful, even allowing you to reset a user's failure counters after you get the problem fixed, with the **-r** or **--reset** option:

```
$ sudo faillog -u rossb --reset
```

Note

The **faillog** command may or may not need you to create the /var/log/faillog file, and if it does, just use the **touch** command as the root user:

```
$ sudo touch /var/log/faillog
```

This will create the file that faillog uses and allow it to commit any entries that occur to that logfiote

#### /etc/security.access.conf

Another possible location that you might want to check is the PAM-related /etc/security/access.conf file, which is usually not in play, but contains a lot of very nice examples that seem to pick on the user john.

Ensure that your user in question is not configured to be limited in any of these circumstances, and if they are, comment them out or remove that entry and have the user attempt to login again.

The /etc/security/access.conf file is not well-known and if misconfigured or mangled or corrupted can cause a world of pain and hassle for users.

It's highly recommend that you look at the man page for the access.conf file, it's very helpful in understanding what access.conf does, and that it affects all users who login to the system. Just use the command:

```
$ man access.conf
```

Highly recommended that you look also at the pam_access file man page, just use the command:

```
$ man pam_access
```

### Privilege Elevation Issues

The typical issue that someone experiences when attempting [*privilege elevation*](#ch21.xhtml_key11-a) is that they don't know the difference between the **su** command and using the **su** command with the - option, so that the login process is fully experienced, not just stepping in as the root user, but becoming the root user.

Another very likely issue is that the user is trying to use the **sudo** command, and they are not configured properly, or with enough privileges in the /etc/sudoers file.

You can refresh yourself about sudo and the /etc/sudoers files by referring back to [Chapter 11](#ch11.xhtml_ch11), “[Use Remote Connectivity for System Managment.](#ch11.xhtml_ch11)”

### Quota Issues

Quotas are outdated, for the most part. [*Quotas*](#ch21.xhtml_key12-a) for disk usage meant a lot when disks were smaller, extremely expensive and shared among massive numbers of users, such as we used to see at colleges and universities.

In my decades of experience, I have found quotas hard to enforce, difficult to maintain and almost always misunderstood by sysadmins and users alike.

I know quotas are in use still, but as a busy sysadmin, instructor and courseware developer, and author, I haven't seen a case of quotas in use in the wild (industry) for a decade or more.

Nevertheless, there is a big problem with quotas that is not related at all to how the quota system works, it's really the understanding that users have of how it works.

#### The Main Problem

Hard and Soft Limits are what causes the biggest problem for users, in that they are not very well defined from the outset, and when you get messages about having exceeded one, or grace periods, it never seems to make sense.

In [Example 21-9](#ch21.xhtml_exe21_9), you see the output of a the **edquota ross** command, which we'll use to try to make more sense of what is going on.

**Example 21-9**–The edquota editor window for the rossb user

```
$ sudo edquota rossb
Disk quotas for user rossb (uid 505):
   Filesystem                blocks   soft   hard  inodes soft hard
   /dev/VGroup01/MainVol01   106833      0      0   15120    0    0
```

In our first column, you see the filesystem that has the quotaon parameter enabling quotas set for.

In the 2nd column, you see the number of disk blocks the user is currently using. In the 3rd and 4th columns, you see the soft and hard limits for DISK BLOCKS for the user on this filesystem.

The 5th column is number of inodes that are in use for the files that the user is responsible for, and the last two columns are the hard and soft limits for the INODES the user is allowed on this system.

##### Possible Files or Entirety of Blocks?

The problem is that a lot of users, and even sysadmins or system managers forget that there is an indirect linkage between the number of disk blocks in use by a user and the number of inodes. If you think of inodes as being the potential number of individual files, then that's however many files you want to let that user create, own and maintain. It is NOT the entirety of the size of those files, that's the blocks quota soft and hard limits.

##### Converting to Usable Numbers

This was always the part of quotas that I hated the most. You need to know several things, in particular the size of the blocks on the disk in question, how many of those make up a usable number like a Gigabyte, and then how many of THOSE do you want the user to have for their quota?

I'm not about to do all that math here, you can figure out the block size of your disk in question using the **stat** command and it's -f option, like you see in [Example 21-10](#ch21.xhtml_exe21_10).

**Example 21-10**–Finding out a filesytem block size using stat -f

```
$ stat -f /dev/sda1
  File: "/dev/sda1"
    ID: 0        Namelen: 255     Type: tmpfs
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 120761     Free: 120761     Available: 120761
Inodes: Total: 120761     Free: 120360
```

With a block size of 4096, and each file taking up at LEAST 1ea 4K block, you can do the rest of the math and determine how many blocks you want this user, and each user to have for their soft and hard limits.

### Summary

In this chapter you learned all about Troubleshooting user login issues, [user file access](#ch21.xhtml_key02-a) issues, password issues, privilege elevation issues and quota issues.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 21-2](#ch21.xhtml_ch21tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 21-2**–Key Topics for [Chapter 21](#ch21.xhtml_ch21)

![Images](graphics/21tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[User login](#ch21.xhtml_key01)

[user file access](#ch21.xhtml_key02)

[group](#ch21.xhtml_key03)

[context](#ch21.xhtml_key04)

[permission](#ch21.xhtml_key05)

[Access Control List (ACL)](#ch21.xhtml_key06)

[Attribute](#ch21.xhtml_key07)

[Policy](#ch21.xhtml_key08)

[Non-Policy](#ch21.xhtml_key09)

[Passwords](#ch21.xhtml_key10)

[Privilege Elevation](#ch21.xhtml_key11)

[Quota](#ch21.xhtml_key12)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** If a user cannot login after their account has been created, what file would you check to see if the user had a password that had been generated and set?

**a.** passwd

**b.** security

**c.** shadow

**d.** nologin

**2.** You are bewildered at the inability to make a change to a file in your user's home directory, and suspect the sysadmin has somehow marked it as being not just read-only, but not writable. Which of the following commands would you use to see special settings for this or any other file?

**a. blattr**

**b. chattr**

**c. lsattr**

**d. mattr**

**3.** One of your new Linux users is an experienced Windows user, but seems to have a lot of problems getting logged in consistently. What is the most common issue for transitioning Windows users in getting used to Linux system logins and files overall?

**a.** case-sensitivity

**b.** share permissions

**c.** extended attributes

**d. Ctrl-Alt-Del**

**4.** A user who you have allowed (foolishly, let's admit) to use privilege elevation keeps getting "command not found" messages when issuing standard root-level commands and ones they do use don't seem to work properly. What command and/or options should they have used to directly become the root user?

**a. suda**

**b. su -x**

**c. su**

**d. su -**

**5.** You've trained your users to check on their quota statistics often in order to not have problems happen with their space usage without any warnings. A user reports they cannot create new files, but they can add contents to existing files. Which of the following needs to be adjusted for them?

**a.** repquota limit

**b.** grace limit

**c.** block soft limit

**d.** inode hard limit

## Chapter 22\. Analyzing and Troubleshooting systemd Common Problems

This chapter covers the following topics:

• [Unit Files](#ch22.xhtml_ch22lev1sec03)

• [Common Problems](#ch22.xhtml_ch22lev1sec04)

The exam objectives covered in this chapter are as follows:

• **Objective 4.5:** Given a scenario, use systemd to diagnose and resolve common problems with a Linux system.

The systemd method is somewhat complex, especially to newcomers, so having some good troubleshooting tips will help ease your transition to systemd, which is how the majority of Linux distributions handle their services these days.

### “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz enables you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. [Table 22-1](#ch22.xhtml_ch22tab1) outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in [Appendix A](#appa.xhtml_appa), “[Answers to the ‘Do I Know This Already?’ Quizzes and Review Questions](#appa.xhtml_appa).”

**Table 22-1**–“Do I Know This Already?” Foundation Topics Section-to-Question Mapping

![Images](graphics/22tab01.jpg)

**Caution**

The goal of self-assessment is to gauge your mastery of the topics in this chapter. If you do not know the answer to a question or are only partially sure of the answer, you should mark that question as wrong for purposes of the self-assessment. Giving yourself credit for an answer you correctly guess skews your self-assessment results and might provide you with a false sense of security.

**1.** What is a primary characteristic of a systemd Service Unit file?

**a.** Starts with service_

**b.** Contains _service_ in the name

**c.** Ends with the extension .service

**d.** Has no extension whatsoever

**2.** In the transition of the majority of distributions to using systemd, what has replaced the concept of SysV Runlevels?

**a.** Targets

**b.** Service-Level

**c.** ExecStarts

**d.** Focuses

**3.** What systemd feature/function is designed to supplement and possibly supplant the use of Cron and Cron Jobs?

**a.** Ticks

**b.** Tasks

**c.** Todos

**d.** Timers

**4.** What directive when used in a service unit will cause that service to not start until another service has started and is available?

**a.** Notyet=

**b.** Requires=

**c.** Until=

**d.** After=

### Foundation Topics

### Unit Files

Since systemd is relatively new, at least compared to SysV or the Init scheme, there is a lot to be confused by and to go wrong, as systemd can be accurately described as both "progress" and "somewhat complex."

#### systemd Troubleshooting

This chapter will focus on the all-important Unit files and issues regarding the keywords or directives found therein, as well as a few common problems that can affect systemd functioning.

![Images](graphics/key_topic_icon.jpg)

#### Unit Files

[Unit files](#ch22.xhtml_key01-a) are text files, but they are formatted in a certain way, with Sections, such as [Unit], [Service] and many others. The man pages discuss Unit files as being "ini-like" which means they are similar to .ini files, or are made up of directives with values separated by an "=" sign, such as you see in [Example 22-1](#ch22.xhtml_exe22_1).

**Example 22-1**–An example of a simple Unit file

```
[Section Name]
Directive=avalue
Directive=othervalue

[Other Section Name]
Directive=somevalue
```

You can find out much more about Unit files and their contents in [Chapter 4](#ch04.xhtml_ch04), “[Managing Processes and Services.](#ch04.xhtml_ch04)”

Note

The goal of this chapter is to point out some of the possible issues or misconfigurations that will cause you to have to troubleshoot the issue. As the vast majority of Unit files and even systemd are made up of editable text files, there is a LOT that can go wrong and human error and editing mistakes are at the top of the heap of trouble you can get into.

#### How This Will Work

We'll address the most common or likely issue for each section of the Linux+ Objectives for this chapter, and move on to the next, there are quite a few item to cover.

#### Service Unit File Issues

Keep in mind that a [Service](#ch22.xhtml_key02-a) Unit file, such as blahwoof.service is yet another text file that is broken up by [Sections] containing Directive=value configuration.

##### Networking Services

One of the main issues with systemd is that seemingly all the services start at once, which is not usually true, but it sure seems like everything is up and roaring and available, but sometimes not networking.

Usually the issue will be that you want a firewall to start BEFORE networking configures your interfaces, but it could be any service that requires or needs the network to be functioning that can cause the issue.

![Images](graphics/key_topic_icon.jpg)

Of the three network-related target units, only the [network-online](#ch22.xhtml_key13-a).target is an active unit, or one that will very specifically cause any other service to wait until the network is up before they start. The network-online.target target makes a convenient inclusion to any service unit file, you just specify that any unit that is dependent on the network be started After the network-online.target verifies there is a configured IP address and stack.

You can see in [Example 22-2](#ch22.xhtml_exe22_2) the two configuration lines that should be included in any service unit file that truly depends on the network to be up and functioning before it runs.

**Example 22-2**–After and Wants Directive Usage

```
[Unit]
Otherdirectives=values
After=network-online.target
Wants=network-online.target
```

Note

Keep in mind that there are a couple of wait services that systemd can operate with, including the NetworkManager-wait-online.service if you are using NetworkManager and the other is systemd-networkd-wait-online.service. Which one you use will cause you to further specify that service in the network-online.target file. Much more about this can be found in the systemd documentation, or run the **man** command and specify systemd-networkd-wait-online.service.

The other, and more passive, unit that can be used to order services that will rely on the network is the network-pre.target.

The main method for using this target is to set an After=network-pre.target and Wants=network-pre.target directives in the service unit file that will be wanting or depending on the network to be present to function properly.

##### ExecStart/ExecStop

These two have a LOT of additional parameters, and getting something even slightly wrong will cause a lot of troubleshooting for you.

When [ExecStart](#ch22.xhtml_key05-a) is used, the command(s) that follow the = symbol are executed at the time the containing unit service is started.

![Images](graphics/key_topic_icon.jpg)

HOWEVER, you can get into trouble right away by the type of service, because unless the service Type=oneshot, you cannot have multiple commands or multiple ExecStart lines!

If the service Type=forking or any of the others, you can have PRECISELY one command on the ExecStart=command line, not multiple commands, and no multiple ExecStart lines!

The [ExecStop](#ch22.xhtml_key06-a) directive is tightly paired with the ExecStart directive, it's used to specify how that command or commands are to be ended when the containing service is ended.

HOWEVER, you cannot depend on just a kind SIGTERM signal to end those processes, they may ignore it. You should consult the systemd.kill man page for the KillMode= and KillSignal= parameters, and experiment with the various signals to ensure that the commands or processes that were ExecStart'ed are ExecStop'ped, as it were!

##### Before and After

These are relatively simple ordering directives, where you might have a service that has to be started [before](#ch22.xhtml_key03-a) a dependent service, or [after](#ch22.xhtml_key04-a) a service that it itself depends on.

![Images](graphics/key_topic_icon.jpg)

Note

There are two methods of dependencies in systemd: ordering and requirements. The Before/After directives are of the ordering dependency method. When starting a service, all of the dependencies are read and a matrix constructed and then the right services are started in that particular order.

When you are starting two or more services, there is no inherent order, but you can impose one by specifying Before=name.service and After=name.service!

One of the main characteristics of systemd is that when the system starts services, it will attempt to start as many of them in parallel as possible, and this can cause some confusion among services that depend on each other, or when a number of services depend on a particular service to be there for them to start properly and function.

The main thing here is that you can OVER-configure Before and After, you don't need to to configure both, you just need to decide which service should contain a Before and the names of the other services, or configure the After in those services to point to the service they depend on. This can take a whiteboard and a few puzzling moments, so take your time and do it right!

If I were configuring serviceA to start Before serviceB, I have two possibilities:

1\. I can put a Before=serviceB directive line in the serviceA unit file, which will automatically put an After=serviceA entry into the dependency matrix for serviceB.

2\. I can put an After=serviceA directive line in the serviceB unit file, which will cause the same order, but will put a Before=serviceB entry into the dependency matrix.

Either way, the order will be the same. If we used three services, serviceA, serviceB, and serviceC, and we wanted both serviceB and serviceC to be started After serviceA, we could do the same thing as shown, but just put the two service names in the After= or Before= line.

The real issue here is do you want to order these services, or do you want to have a requirement on them being available/unavailable in order to have another service(s) started or ended? That will be covered in the “Requires and Wants” section later in this chapter.

##### Type

![Images](graphics/key_topic_icon.jpg)

The [type](#ch22.xhtml_key07-a) of a unit is one thing, but since they are all just text files, and the unit type is usually indicated by the .service or .socket suffix, that’s not the issue we need to discuss, it’s the Type= directive and the options we saw in a previous chapter, such as:

• simple

• forking

• oneshot

The main issue I have seen over and over is the mis-application of the Type=oneshot configuration, leading to extended waits and other issues.

A simple or forking Type setup will cause the unit to be processed and the service or executable to be started, and in the forking type case, it will immediately start a child process but the system is EXPECTING this and will keep track of what’s going on.

The simple type will use something else like a similarly-named .socket unit if the service communicates via a socket. Either way, it’s a much simpler and straightforward scenario if simple or forking are used.

The toughest issue is when the Type=oneshot is used, and that is mainly because a oneshot will be very short-lived, but the system (systemd) is supposed to WAIT for the process to exit before it continues processing other units.

It’s imperative to make sure that the proper Type= statement is used, or systemd may hang or wait an inordinately long time for a service to exit when it’s supposed to keep running.

##### User

A systemd service can be configured to run as a given user, you just need to specify something like what we see in [Example 22-3](#ch22.xhtml_exe22_3).

**Example 22-3**–Setting a systemd service to run as a given user

```
[Service]
Type=simple
User=rossb
Group=staff
```

Specifying a user is usually done because there is a configuration wrinkle or reason to run that service as that particular user. This can affect most any service, but important and well-written services usually have their own given configuration that specifies the user they should be running as.

For example, NGINX has the user it should run as specified in the /etc/nginx/nginx.conf file, even though it typically runs as a systemd service on most distributions.

##### Requires and Wants

![Images](graphics/key_topic_icon.jpg)

The main difference between the Requires= and Wants= directives is that if serviceA Requires serviceB, then it cannot run without serviceB, so serviceB MUST be running to allow serviceA to even start.

The concept of the Wants= directive is that thought serviceA does not HAVE to have serviceB running to start, it’s a very good idea, therefore it Wants to have serviceB there. This is really important to know the difference, because many a service WILL start without Name Services available, but they may not function properly without it.

#### Timer Unit File Issues

[Timer](#ch22.xhtml_key08-a) Unit files are the systemd way of trying to replace CRON jobs, with some limited success.

##### OnCalendar

The [OnCalendar](#ch22.xhtml_key09-a) setting defines a specific date and time for a timer event, which can cause some confusion if a timer doesn’t occur on the specified moment. The clock needs to be accurate, so look at the AccuracySec setting for more information on ensuring the clock is accurate.

##### OnBootSec

Be certain that timers that have the [OnBootSec](#ch22.xhtml_key10-a) setting are not in conflict with user settings, you can view any user-specific settings using systemctl -user.

##### Unit

This setting indicates the Unit that should be activated or turned on when the timer is reached, and having a configuration error or specifying a non-existant unit are a couple of the most common problems.

If you accidentally set the unit to be another timer, it will not execute or activate that .timer unit, but default over to that same name.service, which can be very confusing, or alarming, in this case....

##### Time Expressions

The system method of [time expressions](#ch22.xhtml_key11-a) is rather complex and can be quite confusing to the newcomer. In addition, for those used to using @time notations in CRON, you’ll need to pay very close attention to what these mean in system time expressions.

#### Mount Unit File Issues

Mount units are designed to control and supervise systemd mounted devices and filesystems, including what can and cannot be mounted. Mount units are text files like the other units, and as such are subject to errors and typos that can complicate an already complex scenario.

##### Naming Conventions

The most sensitive and misconfigured part of Mount units is the naming. The name of a Mount unit MUST match the name of the filesystem it controls, with one simple but important distinction: The mount point to be represented is matched up in the name not with /mount/point/filesystem, but with mount-point-filesystem. You just replace the / characters with – characters, since a / is a protected system character that only occurs between two file objects, typically a directory and another directory or file inside of it.

##### What

When reading a Mount unit, systemd does NOT use the User= and Group= directives or settings, it uses instead What= to show what is the source of the mount, ie: what is the device being mounted.

This is subject to typos, you should check this setting very carefully in Mount units that are manually created. The ones systemd will auto-generate are less susceptible to (human) error.

##### Where

Working hand-in-hand with the What= setting, is the Where= setting, which paradoxically for systemd is about as clear as you can get, it specifies Where systemd is to mount What you have specified in the Mount unit.

There are situations that can cause issues, such as having an existing mount point that is actually used for something else, mounting a filesystem over an existing directory as a mount point will obscure or make unavailable anything that was in that mount point and below until the new mount is unmounted.

##### Type

Usually systemd will detect the type of a filesystem when it’s being mounted, but in some cases you may have to manually configure the type of the filesystem being mounted.

Keep in mind that root permissions are normally required to mount a filesystem, but systemd has provisions for non-root users to perform mounts, but that’s out of the scope of the Linux+ Objectives.

##### Options

There are times when you realize that Mr. Lennart and the development team working so hard at making systemd an industry standard have thought about something pretty hard, and this is true of the Options= line in the Mount unit files.

This is effectively to mimic the **Options** column in the /etc/fstab, or to supplant it, depending on your point of view.

Of particular note is the fact that not all options are supported, and some experimentation will be necessary to see which of your desired options will work

#### Target Unit File Issues

Target Units are most similar to the Sys V Runlevels, and issues with Targets will affect large amounts of other Units being loaded, or in the case of errors, not loaded.

##### Default

The default.target isn’t really a target, remember, it’s a link to the target unit that was designated to be the default.

In order to check that the default target is the one you thought it was, or it ought to be, remember to use the systemctl get default command, like you see in [Example 22-4](#ch22.xhtml_exe22_4).

![Images](graphics/key_topic_icon.jpg)

**Example 22-4**–Determining the default target

```
$ systemctl get-default
graphical.target
```

The default is shown as it’s known to the system. However, if you get a different result, f you remember from a previous chapter, we can see what the actual linked target is with the command shown in [Example 22-5](#ch22.xhtml_exe22_5).

**Example 22-5**–Determining the default target via the **find** command

```
$ find /usr -iname default.target -exec ls -l {} \;
lrwxrwxrwx 1 root root 16 Jun 27  2022
/usr/lib/systemd/system/default.target -> graphical.target
```

As you can see, the default.target is really a symlink to the graphical.target. If you are getting strange Target errors, check this first, then make sure the target is not MASKED, or cannot be run by systemd.

There are times when you will see a target has been masked, and cannot be run, such as the graphical.target in our previous examples. You can see if this is the case by listing the loaded target units, such as in [Example 22-6](#ch22.xhtml_exe22_6).

![Images](graphics/key_topic_icon.jpg)

**Example 22-6**–Viewing the loaded targets for troubleshooting purposes

```
$ systemctl list-units --type=target
  UNIT                   LOAD   ACTIVE SUB    DESCRIPTION
  basic.target           loaded active active Basic System
  cryptsetup.target      loaded active active Local Encrypted Volumes
  getty.target           loaded active active Login Prompts
  graphical.target       masked active active graphical.target
  local-fs-pre.target    loaded active active Preparation for Local File
Syst
  local-fs.target        loaded active active Local File Systems
● multi-user.target      loaded active active Multi-User System
  network-online.target  loaded active active Network is Online
  network-pre.target     loaded active active Preparation for Network
  network.target         loaded active active Network
  nss-lookup.target      loaded active active Host and Network Name
Lookups
  nss-user-lookup.target loaded active active User and Group Name Lookups
  paths.target           loaded active active Path Units
  printer.target         loaded active active Printer Support
  remote-fs.target       loaded active active Remote File Systems
  slices.target          loaded active active Slice Units
  sockets.target         loaded active active Socket Units
  sound.target           loaded active active Sound Card
  swap.target            loaded active active Swaps
  sysinit.target         loaded active active System Initialization
  time-set.target        loaded active active System Time Set
  timers.target          loaded active active Timer Units
  veritysetup.target     loaded active active Local Verity Protected
Volumes

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.
23 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
```

If you inspect the line for the graphical.target, you’ll see it’s masked, and the way to unmask it is with the **unmask** sub-command:

```
$ sudo systemctl unmask graphical.target
```

Then you can inspect it with the command in [Example 22-6](#ch22.xhtml_exe22_6), and see that it’s unmasked and available. Probably best to reboot if possible in order to make sure things are loaded like you want them to from this point.

##### Multiuser

My most favorite issue of all is someone saying that their system doesn’t load the graphical subsystem when booting up, only to find that the default target is the multi-user.target. This means that the system was not SUPPOSED to load the graphical subsystem, but the text-only interface. This is easily fixed by making the graphical.target the default target using:

```
$ sudo systemctl set-default graphical.target
```

This will make it so that the system will attempt (if not actually) to start and end up with the graphical subsystem as the interface default.

##### Network-online

One of the main issues with systemd is that seemingly all the services start at once, which is not usually true, but it sure seems like everything is up and roaring and available, but all of this takes time, and services that are all started at once will obviously load at different timings, due to their size or complexity.

One of the main things you can do to ensure that network services are online when needed is to configure either a Wants= or a Requires= directive that points to the appropriate network service management scheme for your system.

The “Network Services” section near the beginning of this chapter will have more information on how to determine what network management scheme you are using.

##### Graphical

Because the graphical.target is just that, a target, there can be a lot of things that will keep it from loading how you expect.

In particular, if your system will boot up, and you get the text login prompt but then if the runlevel or target level is 5 or graphical, you have a dependency issue or problem loading some needed service or other target and need to inspect your log files and systemd configuration.

First thing to do is look at the After= line in the /usr/lib/systemd/system/graphical.target file, which may look like this:

```
After=multi-user.target rescue.service rescue.target display-
manager.service
```

This indicates what should be there for the graphical target to be loaded, so make sure that those services and targets are running using the command:

```
systemctl list-units --type=target
```

Also look to see if there are any errors about gdm, the GNOME Display manager, by running:

```
systemctl status gdm
```

This will show a display that will indicate if the gdm.service is running and a few log entries indicating it’s status.

If you need more information on this or any other service, use the journaling logs to get that with the command:

```
$ journalctl -b
```

This will show the system journal entries from the latest system boot to the present, earlier versions are available by referencing them in a backwards chronological way, such as:

![Images](graphics/key_topic_icon.jpg)

```
$ journalctl --list-boots
```

This will show a listing of the previous boots, with the current boot scenario referenced as 0, such as shown in [Example 22-7](#ch22.xhtml_exe22_7).

**Example 22-7**–An Example of **journalctl –list-boots output**

```
$ journalctl --list-boots
-4 7702c4eb2f7d40f193b489b144c7b41e Thu 2022-07-07 12:41:15 MDT–Thu 2022-
07-07 13:16:04 MDT
-3 8a9177df73c94980a4e30104d81e75c2 Mon 2022-07-18 07:42:28 MDT–Mon 2022-
07-18 07:47:31 MDT
-2 05235a33547349c1a36facfefdf7a232 Mon 2022-07-18 07:47:37 MDT–Mon 2022-
07-18 07:51:41 MDT
-1 89437fce32c24b95ba16aa8f5b3e7a84 Sat 2023-03-18 12:14:13 MDT–Sat 2023-
03-18 12:16:33 MDT
 0 c9c983a4e4f7460a8fb5bd9d28824855 Sat 2023-03-18 12:16:39 MDT–Mon 2023-
03-20 20:29:04 MDTnetdev
```

To see a previous boot log scenario, just specify that instance, in this case from -1 to -4, with the command:

```
$ journalctl -b -2
```

You also might try focusing on a single service at a time, such as looking at gdm.service (the GNOME Display Manager, a common culprit in this type of scenario) with the command:

```
$ journalctl -f -u gdm.service
```

This will display only lines that have to do with the gdm.service unit and it’s operations.

In summary, you will find out something or multiple bits of info that will help inform your further troubleshooting using these steps!

### Common Problems

This last section of the last chapter, (whew!) is a bit of a catch-all for troubleshooting, hitting the hightlights for some of the more common problems that can affect your Linux systems and cause you issues.

#### Name Resolution Failure

So much of our current systems and services depend on the resolution of friendly names to IP Addresses that even a short outage of Name Services can wreak a lot of havoc.

Since this topic has appeared in [Chapter 5](#ch05.xhtml_ch05), “[Using Network Tools and Configuration Files](#ch05.xhtml_ch05),” where we discussed the various [Name Resolution](#ch22.xhtml_key14-a) components, and also in [Chapter 19](#ch19.xhtml_ch19), “[Analyzing and Troubleshooting Networks](#ch19.xhtml_ch19),” where we discussed troubleshooting Name Resolution issues, we will count that topic as properly and fully covered and move on to the next common problem.

#### Application Crash

Just like a crime scene, an [application crash](#ch22.xhtml_key15-a) can be difficult to investigate, there are often not a lot of clues except a suddenly-crashed application and if you’re lucky, an on-screen message that may or may not be helpful.

The first and probably easiest thing you can do is look in the system log files for any indication that something has happened, it’s very likely that some sort of an error message(s) was committed to the logs or the journal in systemd-based systems.

You’ve seen multiple examples of how to view log and journal entries in this and other chapters of this book, so just be sure that you go look at those sources as soon as you can, and be judicious about your search terms when you do, some applications will not even do much more than scream “Ooh, HELP!” in there own language, and you’ll likely need to parse a number of error entries in your search for the truth.

![Images](graphics/key_topic_icon.jpg)

Another great way to see where any entries have been placed on a syslog-based system is to use the **journalctl** command to view a timeframe of a few minutes past log entries, such as we do in [Figure 22-1](#ch22.xhtml_ch22fig01).

![Description: A screenshot of a computer screen Description automatically generated](graphics/22fig01.jpg)

**Figure 22-1**–Output of the **journalctl --since “5 minutes”** command

This command can be modified to just about any time period, such as “1 hour ago” and “2 days ago”, to name just a few possibilities.

When an application crashes, you can configure the system to take a snapshot of the memory that system was using and commit to disk, which is called a “core dump” or a “crash dump”, depending on your background.

To enable core dumps on a systemd-based system:

**Step 1.** As the root user, set the ulimit for crash files to unlimited:

```
# ulimit -c unlimited
```

**Step 2.** Run the **sleep** command and crash it with:

```
sleep 50 & ; killall -SIGSEGV sleep
```

**Step 3.** This will either show a text mode message about sleep suffering a segmentation fault, or kick off a graphical application (Apport) that will walk you through saving and possibly sending off a crash report.

Note

To reset the core size limitation, just use the same command you did to set it to “unlimited”, as shown previously but instead of “unlimited” use “0” or the character zero.

**Step 4.** Depending on what distribution you are using, you may want to check if the core dump is in /var/crash, which if it is, a simple **ls** command will show it’s presence and size.

**Step 5.** Your system may put the crash dump in your application’s working directory, which you can confirm by looking at the /etc/sysctl.conf for the line that contains kernel.core_pattern.

**Step 6.** You can also view the kernel.core_pattern info with the **sysctl** command:

```
$ sysctl kernel.core_pattern
```

Ubuntu has an automated routine that catches a crash that happens and pops up the aforementioned Apport program, which will walk you through inspecting the details of a crash.

Note

You can also use the apport-cli program, which will require a little reading and experimentation, but can be very helpful on non-graphical systems while investigation a crash!

#### Time-zone Configuration

One of the less-understood but very important configuration items is the Time Zone, which even if a server is getting it’s time set from a valid Time Server, the Time zone offset can make it an hour or many more off of the correct time!

This is a critical issue when you have systems that are indexed on the exactly correct time, in particular database servers and anything else that requires exquisitely accurate timestamps.

A very quick way to see what your timezone is set to is to run the **date** command like in [Example 22-8](#ch22.xhtml_exe22_8).

![Images](graphics/key_topic_icon.jpg)

**Example 22-8**–An Example of **date** command output

```
$ date
Mon Mar 20 22:53:09 MDT 2023
```

The MDT characters right before the 4-digit year shows what your current $TZ variable value is, as set in your time configuration file /etc/timezone.

You can temporarily set this to anything you want, such as Pacific Daylight time by exporting a different value to the $TZ variable as shown in [Example 22-9](#ch22.xhtml_exe22_9).

**Example 22-9**–An Example of temporarily changing the time zone

```
$ export TZ=”America/Los_Angeles” ; date
Mon Mar 20 22:55:34 PDT 2023
```

You can of course permanently change your time zone info by using the /etc/localtime symlink, which you can view the results of in [Example 22-10](#ch22.xhtml_exe22_10).

**Example 22-10**–An Example of **the /etc/localtime symlink target**

```
$ ls -l /etc/localtime
lrwxrwxrwx 1 root root 34 Mar 18 11:16 /etc/localtime ->
/usr/share/zoneinfo/America/Denver
```

You can investigate the /etc/share/zoneinfo directory contents and decide which of the other timezone files you might want to change this symlink to point to, such as the America/Los_Angeles one we used earlier.

#### Boot Issues

The boot process and some resulting issues and troubleshooting steps have been covered in [Chapter 1](#ch01.xhtml_ch01), “[Understanding Linux Fundamentals.](#ch01.xhtml_ch01)”

#### Journal Issues

Journaling used to mean a transaction log on EXT filesystems, but since the introduction of systemd, journaling means logging in systemd.

A lot of the issues that people have with journald is that it’s not syslog! There are several main differences that make life difficult for those new to journaling, including the possibility that your journals are not persistent in some cases!

#### Services Not Starting on Time

The issue of services not starting on time has been covered earlier in troubleshooting, and relates mostly to making sure that services that everything depends on, in particular name services and the network are in the Wants= or Requires= directives for those services.

More about this can be found in the Networking Services troubleshooting discussion at the early part of this chapter.

### Summary

In this chapter you learned all about Troubleshooting common problems including Unit file issues such as Services, Timers, Mounts and Target unit file issues.

You also learned about Common Problems, though most of those were covered in detail elsewhere in previous chapters or earlier in this chapter.

### Exam Preparation Tasks

As mentioned in the section “Goals and Methods” in the Introduction, you have a couple of choices for exam preparation: the exercises here, [Chapter 23](#ch23.xhtml_ch23), “[Final Preparation](#ch23.xhtml_ch23),” and the exam simulation questions in the Pearson Test Prep Software Online.

### Review All Key Topics

Review the most important topics in this chapter, noted with the Key Topic icon in the outer margin of the page. [Table 22-2](#ch22.xhtml_ch22tab2) lists these key topics and the page number on which each is found.

![Images](graphics/key_topic_icon.jpg)

**Table 22-2**–Key Topics for [Chapter 22](#ch22.xhtml_ch22)

![Images](graphics/22tab02.jpg)

### Define Key Terms

Define the following key terms from this chapter and check your answers in the glossary:

[Unit File](#ch22.xhtml_key01)

[Service](#ch22.xhtml_key02)

[Before](#ch22.xhtml_key03)

[After](#ch22.xhtml_key04)

[ExecStart](#ch22.xhtml_key05)

[ExecStop](#ch22.xhtml_key06)

[Type](#ch22.xhtml_key07)

[Timer](#ch22.xhtml_key08)

[OnCalendar](#ch22.xhtml_key09)

[OnBootSec](#ch22.xhtml_key10)

[Time expressions](#ch22.xhtml_key11)

Naming Conventions

[Network-online](#ch22.xhtml_key13)

[Name Resolution](#ch22.xhtml_key14)

[Application Crash](#ch22.xhtml_key15)

### Review Questions

The answers to these review questions are in [Appendix A](#appa.xhtml_appa).

**1.** What is a primary characteristic of a systemd Service Unit file?

**a.** Starts with service_

**b.** Contains _service_ in the name

**c.** Ends with the extension .service

**d.** Has no extension whatsoever

**2.** In the transition of the majority of distributions to using systemd, what has replaced the concept of SysV Runlevels?

**a.** Targets

**b.** Service-Level

**c.** ExecStarts

**d.** Focuses

**3.** What systemd feature/function is designed to supplement and possibly supplant the use of Cron and Cron Jobs?

**a.** Ticks

**b.** Tasks

**c.** Todos

**d.** Timers

**4.** What directive when used in a service unit will cause that service to not start until another service has started and is available?

**a.** Notyet=

**b.** Requires=

**c.** Until=

**d.** After=

## Chapter 23\. Final Preparation

Are you excited for your exam after reading this book? I sure hope so. You should be. In this chapter we will put certification prep all together for you and take a more detailed look at the actual certification exam itself.

This chapter shares some great ideas for ensuring that you ace that exam. If you read this book to master Linux and you were not really considering certification, then maybe this chapter might even convince you to give it a try!

The first 29 chapters of this book cover the technologies, protocols, programming concepts, and considerations required to be prepared to pass the CompTIA Linux+ (XK0-005) exam. While these chapters supply the detailed information, most people need more preparation than just reading the first 29 chapters of this book. This chapter details a set of tools and a study plan to help you complete your preparation for the exam.

This short chapter has four main sections. The first section lists the CompTIA Linux+ (XK0-005) exam information and breakdown. The second section shares some important tips to keep in mind to ensure that you are ready for this exam. The third section discusses exam preparation tools that may be useful at this point in the study process. The final section of this chapter lists a suggested study plan for you to follow now that you have completed all the earlier chapters in this book.

### Exam Information

Here are details you should be aware of regarding the Linux+ exam:

![Images](graphics/square.jpg) **Question types:** Multiple choice and performance based

![Images](graphics/square.jpg) **Number of questions:** Maximum of 90

![Images](graphics/square.jpg) **Time limit:** 90 minutes

![Images](graphics/square.jpg) **Required passing score:** 720 (on a scale of 100 to 900)

![Images](graphics/square.jpg) **Languages:** English (at launch). Japanese, Portuguese, and Spanish (coming soon)

![Images](graphics/square.jpg) **Exam fee:** US $358

![Images](graphics/square.jpg) **Exam ID code:** XK0-005

CompTIA Linux+ certification validates the skills of IT professionals with hands-on experience configuring, monitoring, and supporting servers running the Linux operating system. The new Linux+ exam has an increased focus on the following topics: security, kernel modules, storage and visualization, device management at an enterprise level, Git and automation, networking and firewalls, the server side and the command line, server (vs. client-based) coverage, troubleshooting, and SELinux.

The exam is broken up into five different domains. The following pages list those domains, the objectives in each domain, and the percentage of the exam devoted to each of the domains:

**1.0 Hardware and System Configuration (21% of the exam)**

1.1 Explain Linux boot process concepts.

1.2 Given a scenario, install, configure, and monitor kernel modules.

1.3 Given a scenario, configure and verify network connection parameters.

1.4 Given a scenario, manage storage in a Linux environment.

1.5 Compare and contrast cloud and virtualization concepts and technologies.

1.6 Given a scenario, configure localization options.

**2.0 Systems Operation and Maintenance (26% of the exam)**

2.1 Given a scenario, conduct software installations, configuration, updates and removals.

2.2 Given a scenario, manage users and groups.

2.3 Given a scenario, create, modify, and redirect files.

2.4 Given a scenario, manage services.

2.5 Summarize and explain server roles.

2.6 Given a scenario, automate and schedule jobs.

2.7 Explain the use and operation of Linux devices.

2.8 Compare and contrast Linux graphical user interfaces.

**3.0 Security (19% of the exam)**

3.1 Given a scenario, apply or acquire the appropriate user and/or group permissions and ownership.

3.2 Given a scenario, configure and implement appropriate access and authentication methods.

3.3 Summarize security best practices in a Linux environment.

3.4 Given a scenario, implement logging services.

3.5 Given a scenario, implement and configure Linux firewalls.

3.6 Given a scenario, backup, restore, and compress files.

**4.0 Linux Troubleshooting and Diagnostics (20% of the exam)**

4.1 Given a scenario, analyze system properties and remediate accordingly.

4.2 Given a scenario, analyze system processes in order to optimize performance.

4.3 Given a scenario, analyze and troubleshoot user issues.

4.4 Given a scenario, analyze and troubleshoot application and hardware issues.

**5.0 Automation and Scripting (14% of the exam)**

5.1 Given a scenario, deploy and execute basic BASH scripts.

5.2 Given a scenario, carry out version control using Git.

5.3 Summarize orchestration processes and concepts.

Be sure to visit CompTIA’s web page at [https://certification.comptia.org/certifications/linux](http://certification.comptia.org/certifications/linux) to ensure that you have the latest information for the CompTIA Linux+ exam.

### Getting Ready

Here are some important tips to keep in mind to ensure that you are ready for this rewarding exam:

![Images](graphics/square.jpg) **Build and use a study tracker:** Consider using the exam objectives shown in this chapter to build a study tracker for yourself. Such a tracker can help ensure that you have not missed anything and that you are confident for your exam. As a matter of fact, this book offers a sample Study Planner as a website supplement.

![Images](graphics/square.jpg) **Think about your time budget for questions on the exam:** When you do the math, you will see that, on average, you have one minute per question. While this does not sound like a lot of time, keep in mind that many of the questions will be very straightforward, and you will take 15 to 30 seconds on those. This leaves you extra time for other questions on the exam.

![Images](graphics/square.jpg) **Watch the clock:** Check in on the time remaining periodically as you are taking the exam. You might even find that you can slow down pretty dramatically if you have built up a nice block of extra time.

![Images](graphics/square.jpg) **Get some earplugs:** The testing center might provide earplugs, but get some just in case and bring them along. There might be other test takers in the center with you, and you do not want to be distracted by their screams. I personally have no issue blocking out the sounds around me, so I never worry about this, but I know it is an issue for some.

![Images](graphics/square.jpg) **Plan your travel time:** Give yourself extra time to find the center and get checked in. Be sure to arrive early. As you test more at a particular center, you can certainly start cutting it closer time-wise.

![Images](graphics/square.jpg) **Get rest:** Most students report that getting plenty of rest the night before the exam boosts their success. All-night cram sessions are not typically successful. Don’t forget to eat a banana (for the Niacin) and drink a good amount of water (hydrated brains take exams better!) before you go to the exam room.

![Images](graphics/square.jpg) **Bring in valuables but get ready to lock them up:** The testing center will take your phone, your smartwatch, your wallet, and other such items and will provide a secure place for them.

![Images](graphics/square.jpg) **Take notes:** You will be given note-taking implements and should not be afraid to use them. I always jot down any questions I struggle with on the exam. I then memorize them at the end of the test by reading my notes over and over again. I always make sure I have a pen and paper in the car, and I write down the issues in my car just after the exam. When I get home—with a pass or fail–I research those items.

![Images](graphics/square.jpg) **Practice exam questions are great – so use them:** This text provides many practice exam questions. Be sure to go through them thoroughly. Remember that you shouldn’t blindly memorize answers; rather, use the practice questions to really see where you are weak in your knowledge and then study up on those areas.

### Tools for Final Preparation

This section lists some information about the available tools and how to access them.

#### Pearson Test Prep Practice Test Software and Questions on the Website

Register this book to get access to the Pearson IT Certification test engine (software that displays and grades a set of exam-realistic multiple-choice questions). Using the Pearson Test Prep practice test software, you can either study by going through the questions in Study Mode or take a simulated (timed) CompTIA Linux+ exam.

The Pearson Test Prep practice test software comes with two full practice exams. These practice tests are available to you either online or as an offline Windows application. To access the practice exams that were developed with this book, please see the instructions in the card inserted in the sleeve in the back of the book. This card includes a unique access code that enables you to activate your exams in the Pearson Test Prep software.

##### Accessing the Pearson Test Prep Practice Test Software Online

The online version of this software can be used on any device with a browser and connectivity to the Internet, including desktop machines, tablets, and smartphones. To start using your practice exams online, simply follow these steps:

Step 1\. Go to [http://www.PearsonTestPrep.com](http://www.PearsonTestPrep.com).

Step 2\. Select Pearson IT Certification as your product group.

Step 3\. Enter your email and password for your account. If you don’t have an account on PearsonITCertification.com or CiscoPress.com, you need to establish one by going to PearsonITCertification.com/join.

Step 4\. In the My Products tab, click the Activate New Product button.

Step 5\. Enter the access code printed on the insert card in the back of your book to activate your product. The product will now be listed in your My Products page.

Step 6\. Click the Exams button to launch the exam settings screen and start your exam.

##### Accessing the Pearson Test Prep Practice Test Software Offline

If you wish to study offline, you can download and install the Windows version of the Pearson Test Prep software. You can find a download link for this software on the book’s companion website, or you can just enter this link in your browser:

[http://www.pearsonitcertification.com/content/downloads/pcpt/engine.zip](http://www.pearsonitcertification.com/content/downloads/pcpt/engine.zip)

To access the book’s companion website and the software, simply follow these steps:

Step 1\. Register your book by going to PearsonITCertification.com/register and entering the ISBN 9780789760586.

Step 2\. Respond to the challenge questions.

Step 3\. Go to your account page and select the Registered Products tab.

Step 4\. Click on the Access Bonus Content link under the product listing.

Step 5\. Click the Install Pearson Test Prep Desktop Version link in the Practice Exams section of the page to download the software.

Step 6\. When the software finishes downloading, unzip all the files on your computer.

Step 7\. Double-click the application file to start the installation, and follow the onscreen instructions to complete the registration.

Step 8\. When the installation is complete, launch the application and click the Activate Exam button on the My Products tab.

Step 9\. Click the Activate a Product button in the Activate Product Wizard.

Step 10\. Enter the unique access code found on the card in the sleeve in the back of your book and click the Activate button.

Step 11\. Click Next, and then click the Finish button to download the exam data to your application.

Step 12\. You can now start using the practice exams by selecting the product and clicking the Open Exam button to open the exam settings screen.

Note that the offline and online versions sync together, so saved exams and grade results recorded on one version will be available to you on the other as well.

#### Customizing Your Exams

When you are in the exam settings screen, you can choose to take exams in one of three modes:

![Images](graphics/square.jpg) Study Mode

![Images](graphics/square.jpg) Practice Exam Mode

![Images](graphics/square.jpg) Flash Card Mode

Study Mode enables you to fully customize your exams and review answers as you are taking the exam. This is typically the mode you use first to assess your knowledge and identify information gaps. Practice Exam Mode locks certain customization options in order to present a realistic exam experience. Use this mode when you are preparing to test your exam readiness. Flash Card Mode strips out the answers and presents you with only the question stem. This mode is great for late-stage preparation, when you really want to challenge yourself to provide answers without the benefit of seeing multiple-choice options. This mode does not provide the detailed score reports that the other two modes provide, so it is not the best mode for helping you identify knowledge gaps.

In addition to these three modes, you will be able to select the source of your questions. You can choose to take exams that cover all of the chapters, or you can narrow your selection to just a single chapter or the chapters that make up specific parts in the book. All chapters are selected by default. If you want to narrow your focus to individual chapters, simply deselect all the chapters and then select only those on which you wish to focus in the Objectives area.

You can also select the exam banks on which to focus. Each exam bank comes complete with a full exam of questions that cover topics in every chapter. You can have the test engine serve up exams from both banks or just from one individual bank by selecting the desired banks in the exam bank area.

There are several other customizations you can make to your exam from the exam settings screen, such as the time allowed to take the exam, the number of questions served up, whether to randomize questions and answers, whether to show the number of correct answers for multiple-answer questions, and whether to serve up only specific types of questions. You can also create custom test banks by selecting only questions that you have marked or questions on which you have added notes.

#### Updating Your Exams

If you are using the online version of the Pearson Test Prep software, you should always have access to the latest version of the software as well as the exam data. If you are using the Windows desktop version, every time you launch the software, it will check to see whether there are any updates to your exam data and automatically download any changes made since the last time you used the software. This requires you to be connected to the Internet at the time you launch the software.

Sometimes, due to a number of factors, the exam data might not fully download when you activate your exam. If you find that figures or exhibits are missing, you might need to manually update your exams.

To update a particular exam you have already activated and downloaded, simply select the Tools tab and click the Update Products button. Again, this is only an issue with the desktop Windows application.

If you wish to check for updates to the Windows desktop version of the Pearson Test Prep exam engine software, simply select the Tools tab and click the Update Application button. Doing so allows you to ensure that you are running the latest version of the software engine.

##### Premium Edition

In addition to the free practice exams provided on the website, you can purchase additional exams with expanded functionality directly from Pearson IT Certification. The Premium Edition of this title contains an additional two full practice exams and an eBook (in both PDF and ePub format). In addition, the Premium Edition title has remediation for each question to the specific part of the eBook that relates to that question.

Because you have purchased the print version of this title, you can purchase the Premium Edition at a deep discount. There is a coupon code in the book sleeve that contains a one-time-use code and instructions for where you can purchase the Premium Edition.

To view the Premium Edition product page, go to [www.informit.com/title/9780135301371](http://www.informit.com/title/9780135301371).

#### Chapter-Ending Review Tools

[Chapters 2](#ch02.xhtml_ch02) through [22](#ch22.xhtml_ch22) each have several features in the “Exam Preparation Tasks” section at the end of the chapters. You might have already worked through these in each chapter. It can also be useful to use these tools again as you make your final preparations for the exam.

### Suggested Plan for Final Review/Study

This section lists a suggested study plan from the point at which you finish reading through [Chapter 22](#ch22.xhtml_ch22) until you take the CompTIA Linux+ exam. You can ignore this plan, use it as is, or just take suggestions from it.

The plan involves three steps:

Step 1\. **Review key topics and “Do I Know This Already?” (DIKTA?) questions:** You can use the table that lists the key topics in each chapter or just flip the pages, looking for key topics. Also, reviewing the DIKTA? questions from the beginning of the chapter can be helpful for review.

Step 2\. **Review “Review Questions” sections:** Go through the “Review Questions” section at the end of each chapter to identify areas where you need more study.

Step 4\. **Use the Pearson Test Prep Practice Test software to practice:** The Pearson Test Prep practice test software enables you to study using a bank of unique exam-realistic questions available only with this book.

### Summary

The tools and suggestions listed in this chapter have been designed with one goal in mind: to help you develop the skills required to pass the CompTIA Linux+ exam. This book has been developed from the beginning to not just tell you the facts but help you learn how to apply the facts. No matter what your experience level leading up to when you take the exams, it is our hope that the broad range of preparation tools, and even the structure of the book, will help you pass the exam with ease. We hope you do well on the exam.

## Appendix A. Answers to the “Do I Know This Already?” Quizzes and Review Questions [This content is currently in development.]

**This content is currently in development.**

## Appendix B. Study Planner

![Images](graphics/appbtab01.jpg)![Images](graphics/appbtab02.jpg)![Images](graphics/appbtab03.jpg)![Images](graphics/appbtab04.jpg)![Images](graphics/appbtab05.jpg)![Images](graphics/appbtab06.jpg)![Images](graphics/appbtab07.jpg)![Images](graphics/appbtab08.jpg)![Images](graphics/appbtab09.jpg)![Images](graphics/appbtab10.jpg)![Images](graphics/appbtab11.jpg)![Images](graphics/appbtab12.jpg)![Images](graphics/appbtab13.jpg)![Images](graphics/appbtab14.jpg)

## Glossary [This content is currently in development.]

**This content is currently in development.**