![](Images/cover00237.jpeg)

Linux command line

An Introduction to Linux Command Line Environment, Learning to Use Shell Scripting and Commands

By Charles Mint

© Copyright 2019 - All rights reserved.

The content contained within this book may not be reproduced, duplicated or transmitted without direct written permission from the author or the publisher.

Under no circumstances will any blame or legal responsibility be held against the publisher, or author, for any damages, reparation, or monetary loss due to the information contained within this book. Either directly or indirectly.

Legal Notice:

This book is copyright protected. This book is only for personal use. You cannot amend, distribute, sell, use, quote or paraphrase any part, or the content within this book, without the consent of the author or publisher.

Disclaimer Notice:

Please note the information contained within this document is for educational and entertainment purposes only. All effort has been executed to present accurate, up to date, and reliable, complete information. No warranties of any kind are declared or implied. Readers acknowledge that the author is not engaging in the rendering of legal, financial, medical or professional advice. The content within this book has been derived from various sources. Please consult a licensed professional before attempting any techniques outlined in this book.

By reading this document, the reader agrees that under no circumstances is the author responsible for any losses, direct or indirect, which are incurred as a result of the use of information contained within this document, including, but not limited to, — errors, omissions, or inaccuracies.

Table of Contents

[Introduction](#part0000.xhtml__Toc21978112)

[Chapter 1\. Using the Linux](#part0000.xhtml__Toc21978113)

[Chapter 2\. Linux Environment Variables](#part0000.xhtml__Toc21978114)

[Chapter 3\. Using the Terminal And Virtual Consoles](#part0000.xhtml__Toc21978115)

[Chapter 4\. More to know about Files](#part0000.xhtml__Toc21978116)

[Case Sensitivity](#part0000.xhtml__Toc21978117)

[Hidden Files and Directories](#part0000.xhtml__Toc21978118)

[Chapter 5\. Networking commands](#part0000.xhtml__Toc21978119)

[Finding Your IP Address](#part0000.xhtml__Toc21978120)

[Finding Your Default Gateway](#part0000.xhtml__Toc21978121)

[Obtaining an IP Address](#part0000.xhtml__Toc21978122)

[Releasing an IP Address](#part0000.xhtml__Toc21978123)

[Testing Your DNS Server](#part0000.xhtml__Toc21978124)

[Testing Connectivity](#part0000.xhtml__Toc21978125)

[Tracing Paths](#part0000.xhtml__Toc21978126)

[Chapter 6\. Startup and Shutdown](#part0000.xhtml__Toc21978127)

[Overview](#part0000.xhtml__Toc21978128)

[Commands covered in this section:](#part0000.xhtml__Toc21978129)

[Glossary of terms used in this section:](#part0000.xhtml__Toc21978130)

[Chapter 7\. Linux shell programming](#part0000.xhtml__Toc21978131)

[Chapter 8\. Networking](#part0000.xhtml__Toc21978132)

[Chapter 9\. Bash One-liners](#part0000.xhtml__Toc21978133)

[Chapter 10\. Sharing files commands](#part0000.xhtml__Toc21978134)

[FTP Server install Ubuntu and Debian](#part0000.xhtml__Toc21978135)

[FTP Server install Fedora](#part0000.xhtml__Toc21978136)

[Firewalls](#part0000.xhtml__Toc21978137)

[FTP Client](#part0000.xhtml__Toc21978138)

[Ubuntu and Debian Server](#part0000.xhtml__Toc21978139)

[Fedora Server](#part0000.xhtml__Toc21978140)

[Firewalls](#part0000.xhtml__Toc21978141)

[/etc/exports](#part0000.xhtml__Toc21978142)

[NFS Client](#part0000.xhtml__Toc21978143)

[Ubuntu and Debian Server](#part0000.xhtml__Toc21978144)

[Fedora Server](#part0000.xhtml__Toc21978145)

[Firewalls](#part0000.xhtml__Toc21978146)

[Configure a Samba Password](#part0000.xhtml__Toc21978147)

[Connecting to a Samba Server](#part0000.xhtml__Toc21978148)

[Chapter 11\. I/O Direction](#part0000.xhtml__Toc21978149)

[Redirecting Streams](#part0000.xhtml__Toc21978150)

[Getting Your Input from a File](#part0000.xhtml__Toc21978151)

[Sending Your Command Output to Another File](#part0000.xhtml__Toc21978152)

[Saving Errors in Files](#part0000.xhtml__Toc21978153)

[Chapter 12\. Commands for compressing and decompressing files](#part0000.xhtml__Toc21978154)

[To create a compress file with the tar extension that has the name file.tar](#part0000.xhtml__Toc21978155)

[To unpack the file](#part0000.xhtml__Toc21978156)

[To create a compressed file by the Gzip program](#part0000.xhtml__Toc21978157)

[To decompress the file created by Gzip](#part0000.xhtml__Toc21978158)

[To create a file compressed by the Bzip2 program](#part0000.xhtml__Toc21978159)

[To decompress the file created by Gzip](#part0000.xhtml__Toc21978160)

[Chapter 13\. Wildcards in Linux](#part0000.xhtml__Toc21978161)

[Chapter 14\. Advanced Linux Navigation commands](#part0000.xhtml__Toc21978162)

[Changing Directories and Finding Files](#part0000.xhtml__Toc21978163)

[Listing/Displaying Files](#part0000.xhtml__Toc21978164)

[Making, Deleting, Moving, Copying, Renaming](#part0000.xhtml__Toc21978165)

[Mounting Drives](#part0000.xhtml__Toc21978166)

[Chapter 15\. The Processes](#part0000.xhtml__Toc21978167)

[Different Types of Processes](#part0000.xhtml__Toc21978168)

[The Different Features of GRUB](#part0000.xhtml__Toc21978169)

[How to Manage Processes](#part0000.xhtml__Toc21978170)

[Listing Processes and Displaying Information](#part0000.xhtml__Toc21978171)

[Running Processes in the Foreground and Background](#part0000.xhtml__Toc21978172)

[Killing Processes](#part0000.xhtml__Toc21978173)

[Chapter 16\. Making Linux More Secure](#part0000.xhtml__Toc21978174)

[Why Worry About Security](#part0000.xhtml__Toc21978175)

[Ensuring Password Security in Linux](#part0000.xhtml__Toc21978176)

[Shadow Passwords](#part0000.xhtml__Toc21978177)

[PAMs](#part0000.xhtml__Toc21978178)

[Configuring Default Permissions](#part0000.xhtml__Toc21978179)

[Looking Out for Permissions to Set User ID](#part0000.xhtml__Toc21978180)

[Conclusion](#part0000.xhtml__Toc21978181)

# Introduction

Linux is the name for the kernel of an operating system that is based on the UNIX principles. The name is derived from the first name of its Finnish inventor, Linus Torvalds, and follows the methodology used by other UNIX-based systems (the last letter is an x). Today, Linux is developed and maintained by thousands of people around the world.

The kernel of an operating system is its heart. It is required for communication between the hardware of your computer and you, the user. An operating system is a collection of different software components: a kernel, various tools and the accompanying libraries. It is a software that extends the basic operating system of your computer, known as the BIOS.

1.1 From UNIX to Linux

The history of Linux can be traced back to the 1990s. In order to understand the story behind Linux, we also have to look back briefly at the early days of computing after the 2nd World War.

At that time computing machines filled entire buildings and the transformation from mechanical to electronic components, like microprocessors and the usage of multi-layer circuits, was underway. Moreover, in the 1960s and 1970s hardware and software components were quite expensive and not standardized. Various vendor-specific platforms existed and each of them had their own interface, protocols to transfer and exchange data, as well as operating system. The communication between these single computing devices required specific knowledge and the understanding of its protocols. The development of UNIX was an aim to circumvent these obstacles and to simplify the usage of computing devices on a larger scale.

UNIX

UNIX Variants

The concept of UNIX became licensed to several companies that developed and maintained their own variant of UNIX. This included Solaris/SUN OS (SUN Microsystems, nowadays owned by Oracle), AIX (IBM), Scenix (Siemens), SCO UNIX, Xenix (Microsoft), as well as HP-UX (Hewlett-Packard), NeXTSTEP, Mac OS (Apple) and Android (Google).

Open-source implementations comprised of the Berkeley System Distribution (BSD) with its variants: NetBSD, OpenBSD, and FreeBSD. Today, Linux is the most popular free software among open source developers. There is also a strong commercial support for the systems mentioned above.

The UNIX Philosophy

UNIX is designed with a number of strict principles in mind. These principles cover portability, multi-tasking and multi-user orientation in combination with a time-sharing approach. Furthermore, it is based on network connectivity following the TCP/IP scheme.

The original development was done in the C programming language that resulted in independence from a hardware platform. Delivered with a selection of development tools and libraries, it allows you to easily extend it to your specific needs. It is simple, but has a powerful ability to automate tasks that supports complex but maintainable scripts.

Similar to a toolbox, UNIX consists of a variety of tools. Each of them having a specific purpose and being designed exactly for that task. The idea is to use one tool per task. In order to achieve more complex goals, you would combine several tools into a chain. The following example combines the two commands ‘ls’ and ‘wc’ by means of a pipe to be able to count the number of Python files in the current directory.

| $ ls *.py &#124; wc -l6$ |

We will explain these commands and their usage in more detail later on in the guide.

1.2 A Brief History of Linux

Similar to UNIX, the Linux operating system has different roots and is based on the work of quite a few masterminds. Among others, this includes Richard M. Stallman, Andrew S. Tanenbaum and Linus Torvalds.

Richard M. Stallman, a hacker and developer at MIT, is the first president of the Free Software Foundation (FSF), and the father of the GNU project. GNU abbreviates the slogan GNU is Not UNIX. The goal of the project was to develop a free UNIX operating system. Until the beginning of the 1990s a collection of tools was available, but the kernel was still missing. The entire software was published under the GNU Public License (GPL) around 1983\.

The next step for Linux came from Andrew S. Tanenbaum. At that time, he was a professor at the University of Amsterdam. For his students he developed Minix, an operating system for educational purposes to demonstrate and understand the UNIX principles. As he pointed out, Minix was not intended to be used in practice.

Linus Torvalds, a Finish student at the University of Helsinki, was a user of Minix and quite unhappy with its boundaries. In 1990 he began to develop a new operating system based on the ideas of Minix, the UNIX principles, and the POSIX standard. His motivation was to have his own system that was understandable, and maximized to the boundaries of the hardware. He also wanted to have fun, and had no commercial intent in mind. The entire story behind Linux is described in his autobiographical book titled Just for Fun. Today, Linus Torvalds oversees the development of the Linux kernel.

To make Linux attractive to the outside world it needed a nice logo. Based on a competition for mascots, a large number of proposals were handed in. Larry Ewing sent in his idea for a penguin as seen on the cover of this book, and his proposal won. Designed with a cheeky smile and a well-fed body this penguin, named Tux, represents the image of a happy and satisfied user.

1.3 Linux Range of Use

Originally designed for Intel-based systems, Linux runs on a variety of platforms today. Among others this includes the ARM architectures (named arm and arm64), Motorola/Freescale’s 68k architecture (m68k), Intel x86 (i386 and amd64), IBM s390 (s390), PowerPC (powerpc) and SPARC (sparc).

Right from the beginning Linux focused on server systems. It is in constant use as a web server, file server, mail and news server, internet gateway, wireless router and firewall. Used as a computing unit, it helped to render video sequences and entire films such as Titanic, Shrek and Toy Story. Furthermore, Linux is in use in automotive products, astronautics, military, logistics and the engineering environment. Since 2006, Linux servers run all the world’s stock exchanges. It also runs almost all internet search engines.

Over the last decade Linux also conquered the desktop. Due to its high flexibility and stability, it works as a reliable setup for text processing, graphic design, desktop publishing, calculations in spreadsheets, communication (email, chat, audio, and video) as well as user interfaces for your phone and television.

1.4 Linux Certifications

The widespread use of Linux has increased the demand for engineers and users who know exactly what they are doing. At this point a certification for Linux becomes advantageous. These certifications can be divided into programs that are general (not specific to a distribution) and focused (specific to a Linux distribution). The lists below give an overview of the primary certifications that currently exist.

# Chapter 1. Using the Linux

If you are reading this book, you either have Linux and need some help learning how to use it, or you are thinking about getting Linux. For those who are still “on the fence” about making the switch to this operating system, this section should help you decide.

One problem with technology fanatics is that they can be very biased — almost like sports fans. If you were to speak with someone who loves Linux, and has been using it for years, they might paint a very positive picture of it. In addition, they would probably tell you that the other operating systems are junk. However, someone who loves Mac OS or Windows might inform you that Linux is junk, and that you shouldn’t bother trying to use it.

Many people seem to believe that Linux is overly complicated, and that only truly dedicated tech-lovers could ever hope to figure out how to use it. That is very untrue, and if you are worried that Linux is hard to use, leave those thoughts behind. There are versions of Linux that many believe are more user-friendly than anything else available.

Now, with an open mind, take a look at some of the top reasons why you should choose to use Linux:

● It is free. This is probably one of the biggest reasons for many people to choose anything. Of course, your computer probably came with an operating system already, and that would make this a minor factor. Have you thought about updates in the future? It will cost money to upgrade to the latest operating systems, in most situations. On the other hand, Linux is free and it will almost certainly be free long into the future.

● Great with slow computers. Many people choose to install Linux on older, slower computers. If you are still using an old PC from 10 years ago, the chances are that it will not run a new operating system well. Many people are happy running the operating system that came with their old computer. However, in time, these stops being supported, making them very unsecure, and almost impossible to use in any productive way. There are some versions of Linux that are specifically designed to run on low-end hardware, so you can get more out of your old PC. But keep in mind that not all versions of Linux will run well on slower hardware.

● Greater security. If you have been online much in your life, you are probably painfully aware of computer viruses. Even if you do have an antivirus on other computers, there is still a chance that your system with be corrupted. Linux users do not have to worry about computer viruses. In fact, you will not even need to install an antivirus on a computer running Linux.

● Easy to use. Back in the early days of Linux, it certainly was a complicated system to use. However, that was quite some time ago, and things have greatly changed. Many people think that Linux is only for the truly “nerdy”, who know a lot about computers. That is far from the truth these days, and many versions of Linux are simple, with attractive interfaces, and lots of automation.

● No need to find drivers. When you use a new piece of hardware, you will generally need a driver. This is a piece of software that tells your computer how to use your new piece of hardware, like a new printer, for example. With Linux, practically everything is plug-and-play. Just make sure that your hardware is all supported, as mentioned earlier in this chapter.

● The software repository. Think of this like the Linux “app store”. You don’t need to look around online, or worry about installing things manually, because Linux has you covered. In addition, software that you find in the repository will be compatible with your version of Linux, safe to use, and always updated automatically.

● Updates are painless. Updates are often the bane of people’s computer using existence. If you have ever tried to use your computer, only to find that an automatic update has taken over — you will appreciate the ease of Linux updates. They are simply installed in the background, quickly and easily. You will not need to wait to shut down your computer either.

● Attractive GUI. The GUIs (Graphical User Interfaces) of some versions of Linux are just beautiful. These include Unity, Gnome, and KDE, to name just a few. In comparison, Windows — and even Mac OS — can often seem boring and even ugly. In addition to this, it’s possible to customize just how your interface looks, in many ways.

If you are happy with your current operating system, you might have no good reasons to change over. However, if there are things that regularly bother you, it might be time to take a closer look at swapping over to Linux.

# Chapter 2. Linux Environment Variables

When talking about the bash shell, it is relevant to know about its features like the environment variables. These variables come handy in storing information about a particular shell session as well as the environment in which you have been working. With the help of these variables, you can feed information in the memory which can be accessed through running a script or simply by running a program. 

Global Variables

This is simple to learn. These are the variables that can be accessed globally. In simple words, you can access them at any phase of the program. When you have declared a variable, it is fed into the memory of the system while you run the program. You can offer alterations in any function that may affect the entire program. Global variables are always displayed in capital letters.

[aka@localhost ~]$ printenv

You have had a full list of global environment variables. Most of them are set during the login process. If you want to track down values of individual variables, you can do that with the help of echo command. Just don’t forget to add the $ sign before the variable to get its value. Let’s look at the syntax.

[aka@localhost ~]$ echo $PWD

/root
[aka@localhost ~]$

Local Environment Variables

These can only be seen in the local process. Both global environment variables and local environment variables are equally valuable. It is difficult to get a list of the local environment variables because you can’t just run a single command for the purpose. The set command shows the environment variables set for a particular purpose. 

[aka@localhost ~]$ set

BASH=/bin/bash

BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extquote:force_f

ignore:histappend:hostcomplete:interactive_comments:progcomp:promptvars:sourcepa

th

BASHRCSOURCED=Y

BASH_ALIASES=()

BASH_ARGC=()

BASH_ARGV=()

BASH_CMDS=()

BASH_LINENO=()

BASH_SOURCE=()

BASH_VERSINFO=([0]="4" [1]="4" [2]="23" [3]="1" [4]="release" [5]="riscv64-koji-

linux-gnu")

BASH_VERSION='4.4.23(1)-release'

COLUMNS=80

CVS_RSH=ssh

DIRSTACK=()

EUID=0

GROUPS=()

HISTCONTROL=ignoredups

HISTFILE=/root/.bash_history

HISTFILESIZE=1000

HISTSIZE=1000

HOME=/root

HOSTNAME=localhost

HOSTTYPE=riscv64

IFS=$' \t\n'

LANG=en_US.UTF-8

LESSOPEN='||/usr/bin/lesspipe.sh %s'

LINES=30

Please take into account the fact that all the global variables also are included in the set command details.

You can set your own local environment variables

You can set your own variables in the bash shell. You can assign value to a variable by using the equal sign. 

[aka@localhost ~]$ test=world

[aka@localhost ~]$ echo $test

world
[aka@localhost ~]$

The above example is fit for assigning simple values. In order to assign a string value with spaces between words, you need to try something different. Please note that you have to use lower case letters in order to create a new variable. This is important because you can get confused by seeing the environment variables in the capital case. Let’s take a look at the following syntax:

[aka@localhost ~]$ test=theskyisazure

[aka@localhost ~]$ echo $test

theskyisazure

[aka@localhost ~]$ test=the sky is azure

bash: sky: command not found

[aka@localhost ~]$ test='the sky is azure'

[aka@localhost ~]$ echo $test

the sky is azure

You can see that the difference lies in the use of single quotation marks.  

How to remove environment variables

You can remove the variables with a simple step. Let’s see the syntax of the unset command. 

[aka@localhost ~]$ echo $test

theskyisazure
[aka@localhost ~]$ unset test

[aka@localhost ~]$ echo $ test

[aka@localhost ~]$

If you remove the environment variable from the child process, it still remains in the parent process. You have to remove it from the parent process separately. 

[aka@localhost ~]$ test=azure

[aka@localhost ~]$ export test

[aka@localhost ~]$ bash

[aka@localhost ~]$ echo $test

azure

[aka@localhost ~]$ unset test

[aka@localhost ~]$ echo $test

[aka@localhost ~]$ $exit

[aka@localhost ~]$ echo $test
azure
[aka@localhost ~]$

You can clearly see that the environment variable was first exported so that it may become a global variable. The unset command was applied while I was still in the child process. When I switched to the parent shell, the command was still valid. That’s why you need to delete it from the parent shell as well. 

Check out the default shell variables

The bash shell contains environment variables that originate from the shell itself. Let’s check out some of the variables. 

[aka@localhost ~]$ echo $PATH

/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin

You can see different directories in this command. The shell looks for commands in these directories. More directories can be added to the command just by inserting colon and then adding the directory. A default value is assigned to the variables. Let’s take a look at the following table.

PATHAs I have shown you by an example, it carries the list of the directories.
HOMEThis refers to the home directory of the user.
IFSThis brings out a list of characters
CDPATHYou will get a list of directories that are separated by a colon.

Importance of the PATH Variable

This is perhaps the most important variable in the Linux system because it guides the shell to locate the commands for execution right after you enter on the command line. In case it fails to locate it, an error message will be displayed which can look similar to the one given as under:

[aka@localhost ~]$ newfile

-bash : newfile: command not found
[aka@localhost ~]$

It is an environmental variable in the Linux operating system. It becomes active as you enter a command or a shell script. A shell script is just like a mini program that offers text-only user interface for the users of Unix-like systems. It can read commands and then execute them accordingly. It is important to consider here that PATH with all capitals must not be replaced with a path with all the lower-case letters. 

The path variable is a completely different thing as it is the address of a directory. Relative path alludes to the address in relation to the directory you are currently in. There also is an absolute path as already discussed, which is the address in relation to the root directory. 

On the other hand, the PATH will turn out a series of paths distinguished by colons and stored in the form of plain text files. For revision and explanation purposes let’s take a look at how it is executed.

[aka@localhost ~]$ echo $PATH

/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin

You can add new directories to this string. Let’s try it.

[aka@localhost ~]$ echo $PATH

/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin

[aka@localhost ~]$ PATH=$PATH:/home/rich/azuresky

[root@localhost ~]# echo $PATH

/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/home/rich/azuresky

[root@localhost ~]$

It is important to mention that each user in the Linux operating system has a different PATH variable than others. Upon installation of an operating system, a default variable for your PATH is set. After that, you can add more to it or completely change as it suits you.

Note: It is important to mention that the root user’s PATH variable has more directories than any other user. An interesting thing about the PATH variable is that either you can change it just for the current session or on a permanent basis. 

How to find Environment Variables of the Linux System

There are multiple variables that a system uses for identification purpose in the shell scripts. With the help of system variables, you can easily procure important information for the programs. There are different startup methods in the Linux system, and in each system, the bash shell executes the startup files in a different way.

The Login Shell

This locates four distinct startup files from where it could process its commands. The very first file that is executed is the /etc/profile. You can dub it as the default file for the bash shell. Each you time you log in, this command will be executed. 

[aka@localhost ~]# cat /etc/profile

# /etc/profile

I have run this command while logged in as a superuser. The result on your window can be slightly different. 

Just take a look at the export command stated as under:

export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL

You can clearly see that the export command ensures that the variables remain accessible to the child processes.

The $HOME

This one is a user-specific variable. Let’s run it to know what it has got. 

[aka@localhost ~]# cat .bash_profile

# .bash_profile

# Get the aliases and functions

if [ -f ~/.bashrc ]; then

        . ~/.bashrc

fi

# User specific environment and startup programs

PATH=$PATH:$HOME/bin

export PATH

Interactive Shell

If you happen to start the bash shell without first logging into the system, you kickstart the interactive shell. You have the command line to enter command here. With the start from an interactive shell, the system does not load the /etc/profile file. It locates another file called .bashrc in the home directory of the user. Let’s see how this startup file looks in the Linux operating system.

[aka@localhost ~]# cat .bashrc

It conducts a couple of key tasks; first is checking for the bashrc file in the /etc directory. The second one is to allow the user to enter aliases. 

[aka@localhost ~]$ cat /etc/bashrc

Variable Arrays

You can use variables as arrays. The fun thing with arrays is their capacity to hold multiple values which you can reference for a complete array. You can simply cram multiple values in a single variable by listing them with single spacing in parenthesis. Let’s try it.

[aka@localhost ~]$ myworld=(one two three four five)

[aka@localhost ~]$ echo $myworld

one

[aka@localhost ~]$ echo ${myworld[2]}

three

[aka@localhost ~]$ echo ${myworld[1]}

two

[aka@localhost ~]$ echo ${myworld[4]}

five

You can see how easy it is to build up a variable array. You can bring out each value in the array with a special command. Now try the following to bring out the entire array.

[aka@localhost ~]$ echo ${myworld[*]}

one two three four five

In addition to this you can also unset a specific value from the array.

[aka@localhost ~]$ unset myworld[3]

[aka@localhost ~]$ echo ${myworld[*]}

one two three five

If you want to get rid of the entire array, you can do that by unsetting it. 

[aka@localhost ~]$ unset myworld[*]

[aka@localhost ~]$ echo ${myworld[*]}

[aka@localhost ~]$

Variable arrays are not portable to other shell environments, that’s why they are not the foremost option to be used with Linux operating system users.

# Chapter 3. Using the Terminal And Virtual Consoles

Before you do anything from the command line, you have to first actually access the command line interface. When you boot up Ubuntu or Linux Mint or another Linux distribution with a graphical interface, you might wonder how to even get to the command line. In this chapter, we'll discuss how to reach the command-line interface both from a GUI-based Linux distribution and a CLI-based one. We'll also show you how to have multiple command-line windows open at once, whether in the GUI or in a pure CLI environment.

ACCESSING THE COMMAND LINE FROM A CLI-BASED DISTRIBUTION

Some Linux distributions, such as Ubuntu Server, do not include a GUI. For such distributions, getting to the command line isn't hard. You simply boot up the computer or server, and the system goes to the logon prompt. Enter your username and password, and you will log into the system and arrive at the command line prompt, also known as a terminal session. The term terminal dates back to the days when UNIX ran on large mainframes accessed via remote terminals.

Sometimes you might see a blank screen on a CLI Linux machine that's powered up. This is no cause for panic – to save power, the system is usually configured to power off the screen after a set interval of inactivity. Simply tap the space bar to awaken the display once more.

ACCESSING THE COMMAND LINE FROM A GUI-BASED DISTRIBUTION

Accessing the command line from a GUI-based Linux distribution is a little trickier. By default, a GUI-based distribution boots into the graphical interface. Even within the GUI, it’s simple to access a command prompt. There are two common ways of doing so.

The first and most common is an application called a terminal emulator. As the name implies, a terminal emulator recreates the command line environment, but within a window of your GUI. You can access the full range of Linux commands from the terminal emulator application, but you can still use the benefits of the GUI - the mouse, the menu bar, and copying & pasting. (Copy & paste is particularly useful, since you can copy and paste complex and lengthy commands into the terminal emulator without the hassle of typing them.)

Almost all desktop Linux distributions include a terminal emulator application. You can usually launch it by going to the Applications menu, then to the Accessories category, and finally by clicking on the Terminal icon. If your distribution comes with a quick-launch bar (like Ubuntu’s Unity Launcher), very often the icon for the terminal emulator is pinned to the launcher.

The second way to access the command line in a Linux GUI is through what’s called a virtual console. We’ll discuss virtual consoles in this chapter, but first we’ll describe how to open multiple terminal windows.

OPENING MULTIPLE TERMINAL WINDOWS IN THE GUI

One nice feature of working with the terminal emulator application in the GUI is the ability to open multiple terminal windows. There are several advantages to running multiple terminal windows – if you run a command that displays real-time output (like the top monitoring command), you can open a new window to execute additional commands. Or if you're running a command that take a long time to process, like copying several gigabytes of files, you can open a new window and run another command while the first one finishes working.

Most terminal emulator applications support opening a new terminal window. To do so, you usually go to the File menu and select either New Window or New Terminal. A new terminal

window will open up.

If you don't want to clutter up your desktop with a bunch of windows, most terminal applications now offer tabs, much as the Mozilla Firefox and Google Chrome web browsers allow you to open new tabs for different web pages. If you open new tabs in the terminal emulator, a row of tabs will appear below the menu bar, each containing a separate terminal session. Usually, you can open new tabs by going to the File menu and clicking on New Tab.

Obviously a graphical terminal application will not work in the command-line environment. It is nonetheless possible to run multiple terminal windows from the command line using virtual consoles, which we will discuss in the next session.

VIRTUAL CONSOLES

A virtual console is, essentially, a second connection to the same computer. Remember that Linux was based upon UNIX, and most early UNIX machines were massive mainframe computers. To connect to those mainframes, users employed remote consoles or dumb terminals. Because UNIX was a multi-user operating system, multiple users could log into the mainframe at the same time from different consoles.

Virtual consoles are a legacy of those mainframes. Most Linux versions support a maximum of seven virtual consoles, software consoles built into the operating system that mimic the function of those old dumb terminals. Basically, a user can log into the operating system using one of those virtual consoles, and then a second user could switch to a different virtual console and log in, leaving the first user's session unaffected (though they would, of course, have to share the keyboard and mouse).

As we mentioned, Linux supports seven virtual consoles. To switch between virtual consoles, press the CTRL-ALT-FUNCTION# keys simultaneously. So to switch to virtual console one, you would hit CTRL-ALT-F1, to switch to virtual console 2, CTRL-ALT-F2, and so forth. When you switch to a new virtual console, you'll see a standard prompt to log in. You (or another user) can then log into the virtual console without affecting your original session.

If you have a version of Linux running a GUI, you can also use virtual consoles. By default, the GUI runs in virtual console seven (CTRL-ALT-F7). You can switch to any of the other six virtual consoles. When you are finished, you can return to the GUI by hitting CTRL-ALT-F7.

# Chapter 4. More to know about Files

Am sure that you are eager and keen to get stuck into more commands and begin doing some actual playing around with the system. We need to cover some theories first before we get into that. When you begin to play around with the system you are able to understand why it is behaving in such a way and you can also be able to learn the commands further.

Everything is a file

The first thing that we need to know is that everything is a file. For example, a text file is a file, your keyboard is a file, a directory is a file and even a monitor is a file.

Linux is an Extensionless System

A file extension is usually a set of 2 – 4 characters subsequent to the end of a file, which determines the type of file it is.

Common extension includes:

File.exe – an executable program or file,

File.txt – a plain text file.

File [path]

## Case Sensitivity

Many people who are new to learning Linux struggle with one specific problem - while many other systems, such as Windows, don’t pay attention to the case of a character in file reference, Linux does. Thanks to this feature, it’s possible to have multiple files or directors than have the same name, but letters in different cases.

Is Docs

MYFILE1.txt Myfile1.txt myfile1.TXT

file Docs/myfile1.txt

Docs/myfile1.txt: ERROR: cannot open ‘fil1.txt’ (No such file or directory)

In Linux, all of these are interpreted as completely separate files.

It’s important to be aware of case sensitivity while working with command line options. For example, in the command line the two options ’s’ and ’S’ perform completely different actions - it’s common to read an option in upper case, enter it in lower case, and then wonder why your input doesn’t return the expected output.

Name Spaces

While it is possible to incorporate spaces in perfectly valid file and directory names, it’s important to be careful with them. Spaces in a command line signify separate items - that’s how we can know what a program name is and identify each argument in the command line. For example, if the goal were to move into a director called ‘My Photos,’ the following command would not work properly:

Is Docs

MYFILE1.txt Myfile1.txt myfile1.TXT My Photos

cd My Photos

bash: cd: Happyday: No such file or directory

In this example, ‘My Photos’ is interpreted as two separate arguments in the command line. The first argument specifies the directory into which cd moves. In order to make this work properly, you can use one of two valid options.

Quotation Marks

First, you can surround an entire item with quotation marks. Single or double quotation marks are both acceptable, though slightly different in ways that will be addressed later. Anything within a set of quotation marks will be interpreted as an individual item.

cd ‘My Photos’

pwd

/home/mike/Docs/My Photos

Escape Characters

You can also define an item with a space in it by using an escape character, also known as a backslash ( \ ). The backslash nullifies the meaning of the character directly following it.

cd Happyday\ Pictures

pwd

/home/mike/Docs/My Photos

You can see above that the space between ‘Happyday’ and ‘Pictures,’ which would normally have a special meaning (separating into unique command line arguments). Thanks to the backslash, the special meaning is ignored in the argument.

## Hidden Files and Directories

The mechanism to specify whether a file or directory is hidden is very elegant in Linux. By beginning a file or directory’s name with a ‘.’ (full stop), it will be interpreted as hidden - it doesn’t even require any sort of special command or action. There are several reasons for a file or directory to be hidden. For example, a user’s configuration files (stored in the home directory) are generally hidden in order to declutter the space for the user’s everyday tasks.

Is Docs

MYFILE1.txt Myfile1.txt myfile1.TXT

Is -a Docs

… MYFILE1.txt Myfile1.txt myfile1.TXT .hidden .file.txt

…

The tar command

The tar command is used very often because it is simple and efficient. It backs up files, including the file tree.

Backup 

| tar -cvf Filename.tar Files |

c: creation of archive

v: Verbose chat mode: displays what is done

f: indicates that the following parameter is the name of the archive

Example:

| tar -cvf /media/your_media/archive.tar /home/user01/Documents/ |

Backup with compression

| tar -cvzf archive.tar.gz Filers |

Example:

| tar -cvzf /media/your_media/archive.tar.gz /home/user01/Documents/ |

z: add Gzip compression.

Show the contents of the archive

| tar -tvf archive.tar |

t: show the contents of the archive

Restoration 

NB: Do not forget to place in the folder (/) by the command (cd /)

| tar -xvf archive.tar Fichiers |

x: extracting all the files from the archive.

| tar -xvf /media/your_media/archive.tar ortar -xvzf /media/your_media/archive.tar.gz |

# Chapter 5. Networking commands

This chapter will show you how to perform networking tasks from the command line. You'll learn how to find your computer's IP address and MAC address, how to test connectivity, and how to find if your computer's DNS server is functioning properly.

## Finding Your IP Address

It's actually a lot easier to find your IP address from the command line than from the GUI in most Linux distributions. Simply type this command at the prompt:

ifconfig

The ifconfig command will generate an output that looks something like this:

![](Images/image00188.jpeg)

There's quite a bit of information here, but most of it is useful. The eth0 refers to the first Ethernet connection on your system. The indet addr displays your system's IP address, while Mask shows the subnet mask. HWaddr shows your Ethernet adapter's MAC (Media Access Control) address, which is (theoretically) unique to each adapter. (Some wireless networks require you to supply your MAC address before allowing your system to connect.)

You can pipe the output from the ifconfig command to grep to quickly find the specific item you want. Let's say you just want to find the IP address:

ifconfig | grep inet

This time, the output will look like this, and you can quickly pick your IP address from the mix:

![](Images/image00188.jpeg)

Likewise, you can quickly find your computer's MAC address with ifconfig and grep. (A MAC address stands for Media Access Control, and is a hard-wired address that is theoretically unique to each network adapter.)

ifconfig | grep HWaddr

You can easily pick out your MAC address from the output:

![](Images/image00188.jpeg)

## Finding Your Default Gateway

The ifconfig command generates lots of useful output, but it does not include the address of your default gateway. To do so, you can use the ip command with the route option:

ip route

The command will generate an output that looks something like this:

![](Images/image00188.jpeg)

Look for the line that begins default via. Your system's default gateway will be the IP address after those two words. In this example screenshot, the default gateway would be 192.168.2.1.

## Obtaining an IP Address

Most of the time, your Linux system will receive an IP address from a DHCP server.

DHCP stands for Dynamic Host Configuration Protocol, and is a kind of server that assigns an IP address to a client computer when it connects to the DHCP server's network. Configuring each individual computer with an IP address by hand is time-consuming and error prone; if one or more computers receive the same IP address, they won't be able to connect due to the address conflict. DHCP takes the guesswork out of the process. When a computer plugs into an Ethernet network (or connects to a wireless network), it sends out a request for a DHCP server. If there's a DHCP server on the network, it supplies the computer with an IP address, and the DHCP server ensures that no two computers receive the same IP address.

Most of the time, when you plug into a new network, you'll receive a DHCP address automatically. If you don't, however, try this command:

dhclient

Note that you will need to run dhclient as root, whether logged in as root or borrowing root powers via sudo.

This will manually tell your system to search for a DHCP server and accept an address. If this command doesn't work, that means either the network you're using doesn't have a functioning DHCP server, or that something is blocking the DHCP server from communicating with your computer.

## Releasing an IP Address

DHCP addresses come with a lease, which means the amount of time your computer is allowed to keep the address. Usually, your computer will contact the DHCP server at the halfway point before the lease expires, and ask for permission to keep it, which the DHCP server almost always grants.

Sometimes you want to release a leased IP address early - like if your network's DHCP server changes, or if your computer refuses to release its IP address. You can do this with the dhclient command and the -r option:

dhclient -r

This releases your IP address, and you can then use dhclient to contact a DHCP server to receive a new one.

## Testing Your DNS Server

As we mentioned above, if your DNS server stops responding, you can have all sorts of network problems. When it's working right, you will forget that it's there. But it goes bad, everything grinds to a halt. Without it, you can't type addresses into the address bar of your web browser, or use any network resources that depend upon DNS.

To diagnose your DNS server, you can use a command called nslookup. The nslookup command provides the IP address of your current DNS server, and also runs a test lookup against the server to see if it is functioning. For example, if you wanted to determine if your DNS server was operational, you would do so with this command:

nslookup distrowatch.org

The output would look something like this:

![](Images/image00188.jpeg)

The first two lines list the DNS server your computer is using. In this case, we are using a DNS server with an IP address of 192.168.2.1\. The second group of lines shows the result of the lookup we preformed – the IP address of distrowatch.org. In this case, you can see that distrowatch.org has an IP address of 66.180.174.35\. Since nslookup successfully returned an IP address for distrowatch.org, you know that your DNS server is functioning correctly.

## Testing Connectivity

If you’ve ever had to repair a computer (or even used one, for that matter), you know that network and Internet connection problems are a depressingly common occurrence. Fortunately, the command line’s tools are useful for obtaining valuable information about any network problems.

The first and most commonly used network-diagnostic command is the ping command. The ping command stands for Packet Internet Groper, and it relies upon the ICMP protocol, the Internet Control Message Protocol. Basically, the PING command sends a packet to a network destination, such as a server or another PC, and if the destination is active, it sends back an acknowledgment packet. For instance, if you wanted to ping the PC at the IP address of 192.168.1.2, you would use this command:

ping 10.10.11.254

If 10.10.11.254 is up, the ping command will generate an output like this:

![](Images/image00188.jpeg)

The ping command will continue pinging the target until you hit CTRL-C to cancel the command.

The command also has a few command options you can use to alter its performance. The -c option tells ping to send a set number of packets and then stop. For example, if you only wanted to ping 192.168.1.2 six times, you would use this command:

ping -c 6 192.168.1.2

Note that the ping command will not always work, even if a remote destination has an active network connection. This is because some operating systems by default block ICMP traffic. However, enough devices do permit ICMP traffic to make PING a useful diagnostic tool.

## Tracing Paths

Sometimes your network connection is active, but you can’t access a particular destination. In this case, the traceroute command becomes useful. The traceroute command maps the network route from your computer to the destination, and sends every device in the path an ICMP packet. You can

then see which devices in the path are not responding, and then hopefully determine a solution. For instance, to trace the path to 10.10.11.254, you would use traceroute like this:

traceroute 10.10.11.254

The output will look something like this, with one line for each hop (another device in the chain) to the destination:

![](Images/image00188.jpeg)

The traceroute command by default runs up to thirty hops.

# Chapter 6. Startup and Shutdown

## Overview

This chapter covers commands used to startup and shutdown Unix, Linux, and BSD systems. It also provides an overview of platform specific service control commands for popular platforms.

## Commands covered in this section:

shutdown
Shut down the system.

poweroff
Power off the system.

reboot
Reboot the system.

halt
Halt the system.

telinit
Change the runlevel.

runlevel
Display the previous and current runlevel.

service
Manage services on a Linux system.

sysv-rc-conf
Display and edit Linux runlevel configuration.

chkconfig
Display and edit runlevel configuration on Red Hat Linux-based systems.

rc-update
Display and edit runlevel configuration on Gentoo Linux systems.

rc-status
Display the status of services on Gentoo Linux systems.

stopsrc/startsrc
Stop/start services on AIX systems.

lssrc
Display the status of services on AIX systems.

svcs
Display the status of services on Solaris systems.

svcadm
Start/stop services on Solaris systems.

## Glossary of terms used in this section:

Init (INITialization)
A program that controls the startup (AKA initialization) of Unix, Linux, and BSD systems.

Runlevel
A set of profiles used by the init program that defines the programs and services to load during system startup (or when called by the telinit command).

Service
A system program that provides a service as a web server, DNS server, email server, etc. Services are sometimes referred to as Daemons or Service Daemons.

shutdown

Purpose: Shut down the system.

Usage syntax: shutdown [OPTIONS] [TIME] [MESSAGE]

# shutdown now
BROADCAST MESSAGE FROM ROOT:
The system is going down for shutdown now!
* Stopping services [ OK ]
* Terminating processes [ OK ]
...
The system will now halt.

Example output from the shutdown command

The shutdown command is used to shutdown the local system. There are several different types of shutdowns that can be performed: halt, poweroff, and reboot.

Note: Usage of the shutdown command varies between the various Unix, Linux, and BSD platforms. Examples on this page are intended for Linux systems. For usage examples specific to your environment, type man shutdown on your local system.

When the shutdown command is executed, a warning is broadcast to all users logged in to the local system. An optional message can be specified following the time argument as shown in the next example.

# shutdown 2 Save your work and log off ASAP!
BROADCAST MESSAGE FROM ROOT:
The system is going down for shutdown in 2 minutes!
Save your work and log off ASAP!

Example output from the shutdown command's broadcast message

Common usage examples:

shutdown now
Shutdown the system immediately

shutdown [MIN]
Wait the specified number of minutes before shutting down

shutdown [HH:MM]
Shutdown at the specified time (24-hour format)

shutdown -r now
Restart the system

shutdown -H now
Halt the system

shutdown -P now
Power off the system

poweroff

Purpose: Power off the system.

Usage syntax: poweroff

# poweroff
BROADCAST MESSAGE FROM ROOT:
The system is going down for power off now!
* Stopping services [ OK ]
* Terminating processes [ OK ]
...
The system will now power off.

Example output of the poweroff command

The poweroff command will immediately shutdown and power off the system. It is essentially a shortcut for shutdown -P now. The poweroff command is found on all Linux distributions and some BSD and Unix systems.

Note: To see if the poweroff command is supported on your system, type whereis poweroff.

Warning: The poweroff command does not offer a grace period and will immediately bring down the system when executed.

Common usage examples:

poweroff
Shutdown and poweroff the system

reboot

Purpose: Reboot the system.

Usage syntax: reboot

# reboot
BROADCAST MESSAGE FROM ROOT:
The system is going down for reboot now!
* Stopping services [ OK ]
* Terminating processes [ OK ]
...
The system will now reboot.

Example output of the reboot command

The reboot command is used to gracefully reboot the system. It is essentially a shortcut for shutdown -r now. Executing reboot on the command line will immediately reboot the system as demonstrated in the above example.

Warning: The reboot command does not offer a grace period and will immediately reboot the system when executed.

Common usage examples:

reboot
Gracefully reboot the system

halt

Purpose: Halt the system.

Usage syntax: halt

# halt
BROADCAST MESSAGE FROM ROOT:
The system is going down for halt now!
* Stopping services [ OK ]
* Terminating processes [ OK ]
...
The system will now halt.

Example output of the halt command

The halt command will halt an online system. A halt is a special type of shutdown which gracefully shuts down the operating system without powering off the system.

Note: Some commercial Unix systems will enter maintenance mode when halted. This can be used to access a pre-boot configuration/diagnostic environment.

Common usage examples:

halt
Halt the system

telinit

Purpose: Change the runlevel.

Usage syntax: telinit [RUNLEVEL]

# telinit 1
*** Switching to run level 1 ***
# runlevel
3 1

Using telinit to change the system's runlevel

telinit tells the system's init process to stop and start the necessary services configured for the specified runlevel. In the above example the telinit command is used to change the system to runlevel 1\. The runlevel command (see Section 7) is then executed to display the current and previous runlevels.

Each system's runlevel configuration is specific to the distribution being used and can be customized to fit your needs. Most Unix, Linux, and BSD systems will have a runlevel configuration similar to the one described in the following table.

0
Shutdown or special administrative mode

1
Single user mode

2
Multiuser mode

3
Multiuser mode

4
Multiuser mode

5
Distribution specific

6
Reboot

Common usage examples:

telinit [RUNLEVEL]
Tell the init process to load the specified runlevel

runlevel

Purpose: Display the previous and current runlevel.

Usage syntax: runlevel

$ runlevel
3 1

Output of the runlevel command

The runlevel command displays the current and previous runlevel. The runlevel is an initialization sequence called by the init process and defines procedures for system startup and shutdown. In the above example, runlevel is used to display the current runlevel information. The first number displayed is the previous runlevel and the second number is the current runlevel.

Note: If there is no previous runlevel, the system will display N in the first field.

Common usage examples:

runlevel
Display the previous and current runlevel

service

Purpose: Manage services on a Linux system.

Usage syntax: service [OPTIONS] [SERVICE] [ACTION]

# service --status-all
 [ + ] acpid
 [ - ] anacron
 [ + ] apache2
 [ + ] atd
 [ + ] cups
 [ + ] dbus
 [ + ] gdm
 [ + ] hal
 [ + ] klogd
 [ + ] ssh
...

Displaying the status of services with the service command

The service command manages services on Linux systems. In the above example, the --status-all option displays the status of all services on the system. The + symbol indicates a running service and the - symbol indicates a stopped service.

The start, stop, restart, and status options can be used to control individual services as demonstrated in the next example.

# service ssh stop
 * Stopping OpenBSD Secure Shell server sshd [ OK ]
# service ssh start
 * Starting OpenBSD Secure Shell server sshd [ OK ]
# service ssh restart
 * Restarting OpenBSD Secure Shell server sshd [ OK ]
# service ssh status
 * sshd is running

Stopping, starting, restarting, and viewing the status of services

Common usage examples:

service [SERVICE] stop
Stop the specified service

service [SERVICE] start
Start the specified service

service [SERVICE] restart
Restart the specified service

service [SERVICE] status
Display the status of the specified service

service --status-all
Display the status of all services

sysv-rc-conf

Purpose: Display and edit Linux runlevel configuration.

Usage syntax: sysv-rc-conf [OPTIONS] [SERVICE] [ON|OFF]

![](Images/image00189.jpeg)

Example output of the sysv-rc-conf command

The sysv-rc-conf command manages service/runlevel configuration on Linux systems. In the above example, executing sysv-rc-conf starts a configuration utility which enables the user to select which services start on the various runlevels.

Services can also be displayed and modified via the command line using the--list and --level options as demonstrated in the next example.

# sysv-rc-conf --level 2345 apache off
# sysv-rc-conf --list apache2
apache2 2:off 3:off 4:off 5:off
# sysv-rc-conf --level 2345 apache2 on
# sysv-rc-conf --list apache2
apache2 2:on 3:on 4:on 5:on

Using the sysv-rc-conf command to manage services on the command line

Common usage examples:

sysv-rc-conf
Display the runlevel configuration utility

sysv-rc-conf --list
List runlevel configuration for all services

sysv-rc-conf --level [LEVEL] [SERVICE] on
Enable a service on the specified level(s)

sysv-rc-conf --level [LEVEL] [SERVICE] off
Disable a service on the specified level(s)

chkconfig

Purpose: Display and edit runlevel configuration on Red Hat Linux-based systems.

Usage syntax: chkconfig [OPTIONS] [SERVICE] [ON|OFF] [LEVEL]

# chkconfig -l
acpi-support 0:off 1:off 2:on 3:on 4:on 5:on 6:off
acpid 0:off 1:off 2:on 3:on 4:on 5:on 6:off
alsa-utils 0:off 1:off 2:off 3:off 4:off 5:off 6:off
anacron 0:off 1:off 2:on 3:on 4:on 5:on 6:off
apache2 0:off 1:off 2:off 3:off 4:off 5:off 6:off
apport 0:off 1:off 2:on 3:on 4:on 5:on 6:off
...

Listing service configuration with the chkconfig command

The chkconfig command manages services on Red Hat Linux systems. The -l parameter lists the current runlevel configuration, as shown in the above example. If no service is specified, all services will be displayed. Specifying a service name will display the runlevel configuration for the service, as shown in the next example.

# chkconfig -l apache2
apache2 0:off 1:off 2:on 3:on 4:on 5:on 6:off

Listing a specific service with the chkconfig command

The -s option is used to enable or disable services at the specified run levels as demonstrated in the next example.

# chkconfig -s apache2 off 2345
# chkconfig -l apache2
apache2 0:off 1:off 2: off 3: off 4: off 5:off 6:off
# chkconfig -s apache2 on 2345
# chkconfig -l apache2
apache2 0:off 1:off 2:on 3:on 4:on 5:on 6:off

Managing services with the chkconfig command

Common usage examples:

chkconfig -l
List runlevel configuration for all services

chkconfig -l [SERVICE]
List a service's current configuration

chkconfig -s [SERVICE] on [LEVEL]
Enable a service on the specified level(s)

chkconfig -s [SERVICE] off [LEVEL]
Disable a service on the specified level(s)

rc-status

Purpose: Display the status of services on Gentoo Linux systems.

Usage syntax: rc-status [OPTIONS]

# rc-status
Runlevel: default
 amavisd [ started ]
 apache2 [ started ]
 clamd [ started ]
 courier-authlib [ started ]
 courier-imapd [ started ]
 courier-imapd-ssl [ started ]
 courier-pop3d [ started ]
 hostname [ started ]
 keymaps [ started ]
...

Output of the rc-status command

The rc-status displays the status of services on Gentoo Linux systems. In the above example, all services for the current level are listed along with their current status.

Note: Gentoo Linux uses a nontraditional init structure that differs from most Linux systems. You can read more about Gentoo's init system online at www.gentoo.org/doc/en/handbook/.

Common usage examples:

rc-status
List services for the current runlevel

rc-status -a
List all services

rc-status -l
List all defined run levels

rc-update

Purpose: Display and edit runlevel configuration on Gentoo Linux systems.

Usage syntax: rc-update [OPTIONS] [SERVICE] [LEVEL]

# rc-update show
 amavisd | default
 apache2 | default
 bootmisc | boot
 checkfs | boot
 checkroot | boot
 clamd | default
 clock | boot
 consolefont | boot
 courier-authlib | default
 courier-imapd | default
 courier-imapd-ssl | default
 courier-pop3d | default
 courier-pop3d-ssl | default
...

Using the rc-update command to display runlevel configuration

The rc-update command manages services on Gentoo Linux-based systems. In the above example, the show option is used to display the current runlevel configuration.

The add and del options are used to add and delete services from the specified runlevel, as shown in the next example.

# rc-update add sshd default
 * sshd added to runlevel default
# rc-update del sshd default
* 'sshd' removed from the following runlevels: default

Adding and removing services to the default runlevel using rc-update

Common usage examples:

rc-update show
List runlevel configuration for all services

rc-update add [SERVICE] default
Add the specified service to the default runlevels

rc-update del [SERVICE] default
Remove the specified service from the default runlevels

lssrc

Purpose: Display the status of services on AIX systems.

Usage syntax: lssrc [OPTIONS] [SERVICE/GROUP]

# lssrc -a
Subsystem Group PID Status
 syslogd ras 147590 active
 sendmail mail 188508 active
 portmap portmap 126980 active
 snmpmibd tcpip 151728 active
 inetd tcpip 163958 active
 snmpd tcpip 180316 active
 biod nfs 196706 active
 rpc.statd nfs 209038 active
 rpc.lockd nfs 204984 active
 qdaemon spooler 217200 active
 writesrv spooler 233588 active
 pconsole pconsole 270470 active
 cimsys 229504 active
 lpd spooler inoperative
...

Listing the status of all services

The lssrc command displays the status of services on AIX systems. The above example demonstrates using the -a option to display the status of all services. The next example demonstrates using the -s option to list a specific service.

# lssrc -s nfsd
Subsystem Group PID Status
nfsd      nfs       inoperative

Listing a specific service

Common usage examples:

lssrc -a
Display the status of all services

lssrc -s [SERVICE]
Display the status of the specified services

lssrc -g [GROUP]
Display the status of the specified group of services

stopsrc / startsrc

Purpose: Start/stop services on AIX systems.

Usage syntax: startsrc [OPTIONS] [SERVICE/GROUP]

# startsrc -s nfsd
0513-059 The nfsd Subsystem has been started. Subsystem PID is 221400.

Starting a service on AIX with startsrc

The startsrc command starts services (known as SRCs or system resource controllers) on AIX systems. The above example demonstrates using the startsrc command to start the NFS service.

The stopsrc command stops services on AIX systems. The next example demonstrates using stopsrc to stop the NFS service.

Usage syntax: startsrc [OPTIONS] [SERVICE/GROUP]

# stopsrc -s nfsd
0513-044 The nfsd Subsystem was requested to stop.

Stopping a service on AIX with stopsrc

Common usage examples:

startsrc -s [SERVICE]
Start the specified service

stopsrc -s [SERVICE]
Stop the specified service

startsrc -g [GROUP]
Start the specified group of services

stopsrc -g [GROUP]
Stop the specified group of services

stopsrc -a
Stop all running services

svcs

Purpose: Display the status of services on Solaris systems.

Usage syntax: svcs [OPTIONS] [SERVICE]

# svcs
STATE STIME FMRI
legacy_run 19:41:19 lrc: /etc/rcS_d/S50sk98sol
legacy_run 19:42:11 lrc: /etc/rc2_d/S20sysetup
legacy_run 19:42:13 lrc: /etc/rc2_d/S47pppd
legacy_run 19:42:13 lrc: /etc/rc2_d/S70uucp
legacy_run 19:42:13 lrc: /etc/rc2_d/S72autoinstall
legacy_run 19:42:13 lrc: /etc/rc2_d/S73cachefs_daemon
legacy_run 19:42:14 lrc: /etc/rc2_d/S81dodatadm_udaplt
legacy_run 19:42:14 lrc: /etc/rc2_d/S89PRESERVE
legacy_run 19:42:14 lrc: /etc/rc2_d/S94ncalogd
legacy_run 19:42:15 lrc: /etc/rc2_d/S98deallocate
legacy_run 19:42:16 lrc: /etc/rc3_d/S16boot_server
legacy_run 19:42:17 lrc: /etc/rc3_d/S50apache
...

Listing services on a Solaris system with the svcs command

The svcs command displays the status of services on Solaris systems. Executing svcs with no options will list all active services, as shown in the example above.

To see the status of an individual service, a service name can be specified as demonstrated in the next example.

# svcs apache
STATE STIME FMRI
legacy_run 19:42:17 lrc:/etc/rc3_d/S50apache

Listing the status of an individual service using the svcs command

Common usage examples:

svcs
Display all active services

svcs -a
Display all services

svcs [SERVICE]
Display the specified service

svcs -d [SERVICE]
Display the specified service's dependencies

svcs -D [SERVICE]
Display services that depend on the specified service

svcs -l [SERVICE]
Display detailed information about the specified service

svcadm

Purpose: Start/stop services on Solaris systems.

Usage syntax: svcadm [OPTIONS] [SERVICE]

# svcadm enable sendmail
# svcs sendmail
STATE STIME FMRI
online 14:26:14 svc:/network/smtp:sendmail

Starting a service with the svcadm command

The svcadm command controls services on Solaris systems. It can be used to start, stop, and restart services. In the above example, the enable parameter is used to start the sendmail service. The next example demonstrates using the disable parameter to stop the sendmail service.

# svcadm disable sendmail
# svcs sendmail
STATE    STIME    FMRI
disabled 14:27:51 svc:/network/smtp:sendmail

Stopping a service with the svcadm command

To restart a service, use the restart parameter as demonstrated in the next example.

# svcadm restart sendmail
Restarting a service with the svcadm command

Common usage examples:

svcadm enable [SERVICE]
Start the specified service

svcadm disable [SERVICE]
Stop the specified service

svcadm restart [SERVICE]
Restart the specified service

# Chapter 7. Linux shell programming

In Linux, it is very easy to create shell scripts. With shell programming, we can group multiple commands in a chain and then execute them to obtain the desired output. Let’s begin by writing out first script. Open your editor of choice; I am using the vi editor. Add the following shell program to the file:

#!/bin/bash

Echo “Hello World”

The above is an example of a shell program. Save the file and give it the name hello.sh. Note that we have used the .sh extension to imply that it is a shell program. Now, the next step is to make the script executable. This can be achieved as follows:

Open the command prompt and type the following command:

chmod 744 hello.sh

After running the above command, an executable of the file hello.sh will be created; chmod stands for change mode.

744 refers to the permissions and we have used this to add an execute permission to the file. Since we have made the program executable, we now need to execute it.

This can be achieved by running the following command on the terminal:

./hello.sh

After running the above command, the following output will be observed on the standard output:

![](Images/image00190.jpeg)

The command outputs a text saying “Hello World”. Remember that this is the text that we command the echo command to output.

#!/bin/bash is called the shebang and is used to precede shell programs.

To add comments to your program, precede them with a pound sign (#). 

Consider the shell program shown below:

#! /bin/bash

echo "Hey $USER"

echo "Hello, i am" $USER "The following are the processes running currently"

echo "List of running processes:"

ps

You can write and run the program. The following output will be observed after running the program:

![](Images/image00191.jpeg) 

As shown in the above figure, the program outputs your name. It also shows the list of processes that are currently running on your system. 

Now, let’s write a more interactive program. Write the code shown below and run it:

#! /bin/bash

echo "Enter your name”

read name;

echo "welcome Mr. /Mrs. $name ";

echo "Thanks Mr./Mrs. $name. You have provided us with your names";

echo "-----------------------------------------------------------------"

echo "Mr. /Mrs. $name, good bye friend"

After running the above program, the following output will be observed:

![](Images/image00192.jpeg) 

As you can see, you are prompted to provide your name. This has been achieved by use of the read command, which prompts users to provide their input. This input has then been displayed alongside some other text. 

Variables in Shell

The two types of shell variables are:

1.  System variables- these are created and maintained by the OS. They are defined in upper case letters.

2.  User Defined Variables- the user creates and maintains these. They are defined in lower case letters.

The following are some of the system variables in shell:

BASH- the shell name.

HOME- our home directory

LOGNAME- our login name.

PATH- our setting for the path.

USERNAME- the currently logged in user.

COLUMNS- number of columns making up our screen. 

OSTYPE- the type of the OS we are running.

PWD- the current working directory. 

The above shows only a sample of the system variables. If you want to print any of the above variables, use the echo and the $ sign command as shown below:

echo $HOME

echo $PWD

The next section explains how to work with user defined variables. 

Use the following syntax to define a user defined variable:

variable name=value

The ‘name’ refers to the name to be used to refer to the variable. The value is what it is. This is usually a number or a string. Example:

num=10

name=Mary

Tips when naming variable

1.  There shouldn’t be any spaces on either side of the equal sign. Example:

num=12- this is right

num= 12- this is wrong

num =12- this is wrong

num = 12- this is wrong

2.  The name of the variable should begin with an underscore or any of the alphanumeric characters. This should then be followed by any of the alphanumeric characters. The following are examples of valid variables:

PWD

SYSTEM_VERSION

num

3.  The names of variables are case sensitive. Example:

Num=2

num=6

nUm=9

nuM=10

NUM=90

The above shows that the above variable names are not equal. To print any of the above, also make sure that you specify these correctly. For example, to print 10, use the following code:

 echo $nuM

4.  To define null variables, do the following:

num=

num=””

To print it, use the following code:

E=echo $num

However, note that nothing will be displayed since the variable is null. 

5.  Some characters should not be used to name variables. These include the asterisk (*) and the question mark (?). 

Loops in Shell

A loop represents a group of instructions executed repeatedly. 

for Loop

This loop follows the following syntax:

for { name of the variable} in {list }

            do

                     execute the items in the list one after another until finished.

            done

Consider the program shown below:

for j in 1 2 3 4 5

do

echo “Test for the for loop”

done

After running the above program, you will observe the following as the output:

![00069.jpeg](Images/image00193.jpeg)

The program begins by defining the variable j and sets its value from 1 to 5\. The line echo “Test for the for loop” of the program will then be executed 5 times since the value of j will increment up to a maximum of 5\. This explains the source of the output.

while Loop

The while loop in shell takes the following syntax:

 while [ condition]

                do

                 1st command

                 2nd command

                 3rd  command

                 ..

                 ....

                  done

As long as the condition that you have specified is true, the loop will execute. 

Case statement

This is also common in Linux. One can use it rather than the if-else statement.

It takes the following syntax:

case  $name_of_the_variable  in

                1st pattern)   command

                                ...

                                ..

                                command;;

                2nd pattern)   command

                                ...

                                ..

                                command;;

                nth pattern)   command

                                ...

                                ..

                                command;;

                *)             command

                                ...

                                ..

                                command;;

           esac

Note that we start with case but we end with an esac statement. Consider the example shown below:

if [ -y $1 ]
then
  r=”the vehicle is unknown”
elif [ -x $1 ]
then
  r=$1
fi

case $r in
   "lorry") echo "For $r 10 per k/m";;
   "merc") echo "For $r 80 per k/m";;
   "corolla") echo "For $r 15 per k/m";;
   "motorbyke") echo "For $r 5 per k/m";;
   *) echo "we can’t obtain a $r for you";;
esac

If-else-fi for decision making

The command if-else-fi can be used in shell programming for the purpose of decision making. The programmer specifies a condition and once met, a command is executed. If not met, the other command is executed. It takes the following syntax:

if condition

           then

                       the condition is zero

                       execute commands until you meet the else statement

           else

                       if the condition is false

       execute commands until you find the fi statement

           fi

Consider the example shown below:

#!/bin/bash
if [ $# -eq 0 ]
then
echo "$0 : an integer must be supplied"
exit 1
fi

if t $2 -gt 0
then
echo "$2 is a positive number"
else
echo "$2 is a negative number"
fi

If the command line is not given, then an error will be printed, that is, an integer must be supplied. The next part involves checking the number of arguments that have been passed. If we passed any argument, then the “if” will turn out to be false and true otherwise. The exit 1 statement will terminate the program after a successful execution.

# Chapter 8. Networking

The days of the stand-alone home computer are long gone. Modern servers and workstations are almost always connected to the Internet, or at least a local area network. To effectively use a Linux system from the command line, you'll need at least a basic knowledge of TCP/IP computer networking, along with the network commands available from the prompt. In this chapter, we'll give you a basic overview of networking.

WHAT IS AN IP ADDRESS?

First, however, we should discuss IP addresses. Before we explain the Linux command prompt's networking commands, it’s a good idea to have a firm grasp of the basics of IP addressing.

The letters IP stand for Internet Protocol, and the Internet Protocol is part of the TCP/IP (Transmission Control Protocol/Internet Protocol) suite, a group of related protocols that lay down the rules for how computers communicate over networks, both over LANs and the larger Internet. An IP address, therefore, is a (theoretically) unique address assigned to a computer. It's a bit like a street address - it lets other computers send traffic to and receive traffic from your system. An IP address consists of four groups of numbers separated by dots:

192.168.1.1

These numbers are actually the numerical form of a binary number. None of these numbers can be higher than 255\. (While watching a detective TV show, it’s occasionally hilarious to see the police track a criminal using a ludicrously implausible IP address, like 689.34.385.339.)

The dominant version of the IP protocol is Version 4, commonly referred to as IPv4\. Under IPv4, there are only 4.6 billion IP addresses available, and the available IP addresses ran out in late 2011\. (IPv6, which has many more available addresses, will eventually replace IPv4, but for now, IPv4 remains dominant.) There are obviously far more computers, phones, routers, switches, and other networked devices in the world than 4.6 billion, so how do all these devices receive IP addresses?

The answer is a private IP address. Certain blocks of IP addresses have been reserved for use in private networks. These blocks, using a technology called Network Address Translation (NAT), are then translated to public IP addresses. This has extended the lifetime of the available IPv4 address space for decades. The ranges of the reserved private addresses are:

10.0.0.0 - 10.255.255.255

172.16.0.0 - 172.31.255.255

192.168.0.0 - 192.168.255.255

Odds are, your computer has an IP address in one of those ranges as part of a private network (even if it's just a private network generated by your wireless router).

SUBNET MASKS

IP address also have a subnet mask. A subnet mask defines which parts of the IP address designate the network, and which part designates the individual computer. Let's say the IP address of 192.168.1.1 from above has a subnet mask like this:

255.255.255.0

That means the 192.168.1 part of the address indicates the network, while the final 1 indicates the computer.

IP addresses usually include a broadcast address. Any traffic sent to the broadcast address is directed to every single computer in the local network. A broadcast address has a 255 as its final number, so a computer with a 192.168.1.1 address will have a broadcast address of 192.168.1.255.

DEFAULT GATEWAY

Lastly, IP addresses usually (but not always) come with a default gateway. The default gateway is the address your computer sends traffic destined for anywhere outside the local network segment. Like, say you want to visit Google with your web browser. Your computer recognizes that Google isn't on the 192.168.1.* network, and so forwards the request to the default gateway, which then sends the traffic on to Google. (This is a simplification, but adequate for our purposes.)

DNS

The final important piece of basic networking is the Domain Name System, or DNS.

As we mentioned above, every website on the Internet has, in theory, its own unique web address. Remembering all of those IP addresses can prove impractical. A few people might have keen enough memories to remember that microsoft.com has an IP address of 206.46.232.182 (at least at the time of this writing), but most of us cannot.

DNS provides an easier way to find websites. DNS maps each address to a domain name. When you type in a web address, such as microsoft.com or distrowatch.org, your request goes to a DNS server. The DNS server checks its database of domain name mappings (called zone data) and responds with the IP address assigned to that domain name. Your computer is then able to contact the website and begin downloading data.

DNS is integral to the smooth functioning of most computer networks. If your computer is suffering connection problems, DNS is one of the first things to check (other than making sure the network cable is plugged in, of course).

# Chapter 9. Bash One-liners

Working with files

1.  To truncate the size of a file to 0 (emptying) - Use the redirection command in this case. If the file exists, then its size is truncated to zero whereas if it does not exist, it is created. Note the operator opens the file for writing.

$ > file

To create a file containing content of your choice or to replace the file’s contents, use the following command:

$ echo “string to replace” > file

The string that you specify in between the quotes will act as the replacement     string. 

2.  To add a string to your file - the on-liner uses the output redirection operator >> to append some content to your file. Example:

$ echo “content to be appended” >> file

If the operator fails to find the file, a new one is created.  After the string has been appended to the file, a new line will follow it. 

To avoid this, use the –n option as shown below:

$ echo -n “content to be appended” >> file

3.  To assign the first line of a file to a variable- in this case, you need to read the first line of the file and then assign this line to a variable. The input redirection operator < is used. 

Consider the line of code shown below:

$ read -r myline < file

myline is a variable. The command read will read only the first line of the file and place it in the variable myline. The –r option will ensure that this line is read raw.

4.  To read a file - a read command can be combined with the while loop to read a file line-by-line. This is illustrated below:

while read -r myline; do

    # perform something on the variable myline

done < file

A code of failure will be returned when the read command meets end-of-failure. The while loop will then halt.

Note that we have placed < file at the end. To avoid this, pipe the file’s content to a while loop as shown below:

cat file | while IFS= read -r myline; do

    # perform something on the variable myline

done

5.  To read any line of a file and assign it to a variable - external programs assist the bash to read the lines of a program. Consider the code shown below:

$ read -r rline < <(shuf file)

Shuf is available on modern Linux systems and helps with this. The above code will read a random line of a file and assign it to the variable rline. 

6.  To extract a tar archive, use the following command:

tar xvf b.tar 

7.  To find the number of lines common between two files:

sort doc1 doc2 | uniq –d

8.  To randomize the lines of a file:

shuf filename.txt

9.  To sum a particular column:

awk '{ sum+=$1} END {print sum}' document.txt

# Chapter 10. Sharing files commands

When working in a network environment it is important to be able to share files between users and systems.  Linux has multiple ways to share file between Linux, Windows, and Mac systems.

[FTP](#part0000.xhtml__wzdov2u0wm8)

[SFTP](#part0000.xhtml__e9821a49wqxy)

[HTTP/HTTPS](#part0000.xhtml__pa57plpui70u)

[NFS](#part0000.xhtml__7oy0d1nulda0)

Samba

FTP

The FTP protocol is a quick and easy way to share files on the Internet or a network but is also very insecure.  The FTP protocol passes the username and password in clear text which can captured by anyone able to capture traffic between the client and the FTP server.  Due to security concerns, you should only use FTP to share files that do not need to be secured.

On most Linux system you will need to install an FTP server if you want to makes files available via FTP.  If you have to use FTP, make sure that the server you install the FTP server software on does not perform any critical function on the network.  You should also not put an FTP server on your internal network that allows connections from outside the network or the Internet.  If you need to share files with the Internet, your FTP server should be in the Demilitarized Zone (DMZ) on the firewall.

### FTP Server install Ubuntu and Debian

To install an FTP server on Ubuntu and Debian you can use the apt-get install command.

sudo apt-get install vsftpd

Ubuntu and Debian configure and enable the vstfpd service and start the service automatically during the install process.

### FTP Server install Fedora

To install an FTP server on Fedora you can use the dnf install command.  The --best option tells Fedora to install the version of the software that best matches your system when there are multiple versions available.

sudo dnf install vsftpd --best

Fedora installs the vsftpd server but does not start the service automatically.  To start and enable the vsftpd server to start during boot use the systemctl command.

sudo systemctl start vsftpd

sudo systemctl enable vsftpd

### Firewalls   

If your Linux system has a host based firewall installed and running then you will have to open up the port for FTP, TCP port 21, inbound in order to allow incoming connections.  There are security risks with running an insecure protocol such as FTP on a Linux system so make sure that you have the system properly configured and placed in the network before opening up a port on the firewall.

The following subsections will be covered in this section:

[Ubuntu and Debian](#part0000.xhtml__k8i2ho83u4t4)

[Fedora](#part0000.xhtml__tl76v3lzju8h)

Ubuntu and Debian

Ubuntu and Debian use the Uncomplicated Firewall (UFW) to control basic firewall configurations, however the firewall is not configured by default.  To open TCP port 21 using the following command:

sudo ufw allow in ftp

Fedora 

Fedora uses firewalld to control basic firewall configurations and the firewall is configured by default.  To open TCP port 21 using the following commands:

firewall-cmd --permanent --add-port=21/tcp

firewall-cmd --reload

### FTP Client

In order to connect to an FTP server, you need to use an FTP client.  Ubuntu and Debian come with ftp already installed.  Fedora does not come with an FTP client so you must install it with the dnf install command.

sudo dnf install ftp --best

The following subsections will be covered in this section:

[Connecting to a server](#part0000.xhtml__45vty3tmlkuo)

[Passive Mode](#part0000.xhtml__z336tnxfs6w2)

[Help](#part0000.xhtml__3v9gzjz5ia5j)

[List Remote Files](#part0000.xhtml__ckg9vlpbhe56)

[List Local Files](#part0000.xhtml__otaf2b4q8oik)

[Current Remote Directory](#part0000.xhtml__i8ykpg1dpkhs)

[Current Local Directory](#part0000.xhtml__4971o42pgzrl)

[Change Remote Directory](#part0000.xhtml__yt3m6e1e0bz9)

[Change Local Directory](#part0000.xhtml__91748tianfn9)

[Get Files](#part0000.xhtml__314p1vurpzsg)

[Put Files](#part0000.xhtml__2shexqokcez0)

[Exit FTP](#part0000.xhtml__n2ec1gl7ykx5)

Connecting to a server

To connect to an FTP server from the CLI use the ftp command followed by either the IP address or hostname of the server.  In the example below ftp command is used to connect to the IP Address 192.168.10.10.

![](Images/image00194.jpeg) 

You will be asked for the username and password to access the server as in the example below.  By default, ftp will use the username of the current user unless you specify a specific user.

![](Images/image00195.jpeg) 

You can also open a connection to a server from inside the ftp program by using the open command with the IP address or hostname as in the example below.  If you leave an ftp connection open for too long you will get disconnected from the server and may need to reconnect.

![](Images/image00196.jpeg) 

Passive Mode

The FTP protocol can run in two modes, active or passive.  Active mode uses two TCP ports, 20 and 21, and passive mode uses just TCP port 21.   Most servers today run in passive mode but most FTP clients assume active mode by default.  To make sure you are using the proper mode you must set the FTP client to passive mode using the passive command as in the example below:

![](Images/image00197.jpeg) 

Help

The FTP client comes with a help menu that can be accessed by typing either ? or help to access the help menu.

![](Images/image00198.jpeg) 

You can get help on a specific command by using the help command followed by the name of the command as in the example below.

![](Images/image00199.jpeg)

List Remote Files

You can get a list of files and directories on the remote system by using either the dir or ls commands as in the example below.

![](Images/image00200.jpeg) 

List Local Files

You can get a list of files and directories on the local system by putting the ! character in front of the the dir or ls commands as in the example below.

![](Images/image00201.jpeg) 

Current Remote Directory

You can find out what the current remote directory is by using the pwd command as in the example below.

![](Images/image00202.jpeg) 

Current Local Directory

You can find out what the current local directory is by using the !pwd command as in the example below.

![](Images/image00203.jpeg) 

Change Remote Directory

You can change the remote directory by using the cd command.  In the example below, the pwd command is used to check the remote directory, the ls command is used to view the remote director, and the cd command is used to change to the Documents directory.

![](Images/image00204.jpeg)

Change Local Directory

You can change the local directory by using the lcd command.   In the example below, the !pwd command is used to check the remote directory and the lcd command is used to change to the Documents directory.

![](Images/image00205.jpeg) 

Get Files 

To get or download a file from an FTP server you can use the get command followed by the filename.  In the example below, the !ls command is used to view the local directory, the ls command is used to view the remote directory, the mget command is used to get the myfile4 file, and the !ls command is used to view the local directory and verify that the file download occurred. 

![](Images/image00206.jpeg) 

To get or download multiple files from an FTP server you can use the mget command followed by the filename as in the example below.

![](Images/image00207.jpeg)

Put Files

To put or upload a file to an FTP server you can use the put command followed the filename.  By default, vsftpd is configured not to allow writing to the FTP server as in the example below.

![](Images/image00208.jpeg) 

To enable writing to the FTP server you must edit the vsftpd.conf file and remove the # character in front of the write_enable=YES line and save the file.  Ubuntu and Debian put the vsftpd.conf file in the /etc/ directory and Fedora puts the file in the /etc/vsftpd directory.

![00133.jpeg](Images/image00209.jpeg)

You will need to restart the vsftpd server.

sudo systemctl restart vsftpd

Once the server has restarted you will be able to use the put command to upload the file as in the example below.

![00134.jpeg](Images/image00210.jpeg)

To upload multiple files to an FTP server you can use the mput command followed by the filename and a wildcard as in the example below.

![00135.jpeg](Images/image00211.jpeg)

Exit FTP

To exit the ftp program just use the exit command.

SFTP

Since FTP is an insecure it is not recommended for secure file transfers.  To securely transfer files, you can use the SFTP protocol which uses the SSH protocol on TCP port 22 to transfer files.

You can use the sftp command just like you would use the ftp command as in the example below.

![00136.jpeg](Images/image00212.jpeg)

HTTP/HTTPS

You can share files using the HTTP and HTTPS protocols.  Files placed on a web server for download can be downloaded from the CLI using the wget command followed by the URL as in the example below.

![00137.jpeg](Images/image00213.jpeg)

The wget command will append a . and a number to the end of the filename if a file with the same name already exists in the directory the file is being downloaded into.

NFS

The Network File System (NFS) allows files and directories to be shared across the network between Linux systems.  The NFS server hosts directories that can be mounted by the NFS client on a remote system.

[Ubuntu and Debian Server](#part0000.xhtml__p643lhdlwjst)

[Fedora Server](#part0000.xhtml__vahrzj5yk8zz)

[Firewalls](#part0000.xhtml__ym0r6ckb6ns3)

[/etc/exports](#part0000.xhtml__3o9eofvo7cgc)

[NFS Client](#part0000.xhtml__31m1k6qnf8ot)

### Ubuntu and Debian Server  

To install the NFS server on Ubuntu and Debian use the apt-get install command.

sudo apt-get install nfs-kernel-server

### Fedora Server   

To install the NFS server on Fedora use the dnf install command.

sudo dnf install nfs-utils --best

### Firewalls   

If your Linux system has a host based firewall installed and running then you will have to open up the port for NFS, TCP and UDP port 2049, inbound in order to allow incoming connections.  There are security risks with running any protocol such as NFS on a Linux system so make sure that you have the system properly configured and placed in the network before opening up a port on the firewall.

The following subsections will be covered in this section:

[Ubuntu and Debian](#part0000.xhtml__s9m6b592ukpv)

[Fedora](#part0000.xhtml__q3bwkk6te9q3)

Ubuntu and Debian

Ubuntu and Debian use the Uncomplicated Firewall (UFW) to control basic firewall configurations, however the firewall is not configured by default.  To open TCP and UDP port 2049 using the following command:

sudo ufw allow in nfs

Fedora 

Fedora uses firewalld to control basic firewall configurations and the firewall is configured by default.  To open TCP and UDP port 2049 using the following commands:

firewall-cmd --permanent --add-service=nfs

firewall-cmd --reload

### /etc/exports   

Following the installation of the server the /etc/exports file needs to be edited to add directories that you want to make available via NFS.

sudo vi /etc/exports

The syntax for entries in the exports file are as follows:

directoryhosts(options)

The directory is the local directory that you want to share.

The hosts are hosts that should be allowed to access the share.  You can use an IP address, network ID, hostname, or * which means all hosts.

The options control the permissions for the share.  The following are the common options:

ro - Read only access

rw - Read and write access

no_root_squash - Allows the root user from the client to have root permission on the server.

no_subtree_check - disables the verifications of directory subtrees if an entire volume is shared to speed up access time.

sync - Prevents data corruption

The following are examples of shares in the /etc/exports file:

Share the /home directory with any IP address and provide Read and Write permissions:

/home  *(rw)

Share the /home directory with IP address 192.168.1.3 and provide Read only permissions:

/home  192.168.1.3(ro)

Share the /home directory with IP address 19.168.1.3 (Read and Write) and 192.168.1.4 (Read Only) and allows root to have permissions:

/home  192.168.1.3(rw,no_root_squash) 192.168.1.4(ro,no_root_squash)

Once you edit the /etc/exports file you must restart the nfs service:

For Ubuntu and Debian:

sudo systemctl restart nfs-kernel-server.service

For Fedora:

sudo systemctl restart nfs-server.service

### NFS Client

In order to connect from a Linux system to an NFS server the system must have an NFS client and the user using the client must have a matching username and password on the server.

[Ubuntu and Debian](#part0000.xhtml__kcg5pil5a99u)

[Fedora](#part0000.xhtml__pyyi0nxizlk3)

[mount](#part0000.xhtml__aat8zd85o81r)

Ubuntu and Debian

To install the NFS client on Ubuntu and Debian use the apt-get install command.

sudo apt-get install nfs-common

Fedora

To install the NFS client on Fedora use dnf install command.

sudo dnf install nfs-utils --best

mount

In order to access NFS shares on an NFS server you must mount the share to a local directory that is empty.

To make an empty directory use the mkdir command:

mkdir ~/mydir

To mount the share in the empty directory, use the mount command .  The syntax is as follows:

sudo mount ip_address:share_name local_directory

In the example below the mount command is used to mount the /home folder on the NFS server with the IP address 192.168.56.163 and mount it in the local folder myfolder.

![00138.jpeg](Images/image00214.jpeg)

To mount the share automatically during boot add the share information to the /etc/fstab file:

192.168.56.163:/home ~/myfoldernfsrw00

Samba

The Samba service allows files and directories to be shared across the network between Linux, Unix, Mac, and Windows systems.  The Samba server hosts directories that can be accessed and mounted by a Samba client on a remote system. Samba uses the Server Message Block (SMB) Protocol.

[Ubuntu and Debian Server](#part0000.xhtml__r8x2nghh5jfw)

[Fedora Server](#part0000.xhtml__zdc0ss9snqy0)

[Firewalls](#part0000.xhtml__10vwfgr4y5nr)

[Configure a Samba Password](#part0000.xhtml__n6azq0rr9xdd)

[Edit /etc/samba/smb.conf](#part0000.xhtml__hc0zqt5dnnqo)

[Connecting to a Samba Server](#part0000.xhtml__cmnj1658sa9l)

[Linux](#part0000.xhtml__oawf115zyzwy)

[Windows](#part0000.xhtml__rfqm994di3qv)

### Ubuntu and Debian Server  

To install the Samba server on Ubuntu and Debian use the apt-get install command.

sudo apt-get install samba

![00139.jpeg](Images/image00215.jpeg)

### Fedora Server   

To install the Samba server on Fedora use the dnf install command.

sudo dnf install samba --best

Fedora does not automatically start the smb service so you will need to start the service using the systemctl command.

sudo systemctl start smb nmb

### Firewalls   

If your Linux system has a host-based firewall installed and running then you will have to open up the port for SMB, TCP port 445, inbound in order to allow incoming connections.  There are security risks with running any protocol such as SMB on a Linux system so make sure that you have the system properly configured and placed in the network before opening up a port on the firewall.

The following subsections will be covered in this section:

[Ubuntu and Debian](#part0000.xhtml__ohgk6qenk2xc)

[Fedora](#part0000.xhtml__px5dwl7kdk7)

Ubuntu and Debian

Ubuntu and Debian use the Uncomplicated Firewall (UFW) to control basic firewall configurations, however the firewall is not configured by default.  To open TCP port 445 using the following command:

sudo ufw allow in samba

Fedora 

Fedora uses firewalld to control basic firewall configurations and the firewall is configured by default.  To open TCP port 445 using the following command:

firewall-cmd --permanent --add-service=samba

firewall-cmd --reload

### Configure a Samba Password

Samba uses a separate password than the Linux login password for a user, however, you can make the passwords the same.  Before a user can access a Samba share a password must be set using the smbpasswd command with the -a option as in the example below.

![00140.jpeg](Images/image00216.jpeg)

Edit /etc/samba/smb.conf

Samba shares are defined in the /etc/samba/smb.conf file.

sudo vi /etc/samba/smb.conf

Go to the end of the file and add the following:

[share_name]

   comment = share_comment

   path = share_path

   valid users = samba_user

   read only = yes or no

   guest ok = yes or no

   browseable = yes or no

The example below shows the configuration for a share name myshare.

![00141.jpeg](Images/image00217.jpeg)

You will need to restart the smb service for the changes to take effect.

Ubuntu and Debian

sudo systemctl restart smbd

Fedora

sudo systemctl restart smb nbd

### Connecting to a Samba Server

In order to connect from a Linux system or Windows system to a Samba server the system must have an SMB client and the user using the client must have a username and password on the server.

[Linux](#part0000.xhtml__oawf115zyzwy)

[Fstab](#part0000.xhtml__hs0eiywngor2)

[Windows](#part0000.xhtml__rfqm994di3qv)

Linux

On Linux systems you have to install a Samba client is one is not already installed.

Ubuntu and Debian

sudo apt-get install smbclient

Fedora

sudo apt-get install samba --best

Once the Samba client is installed you can use the smbclient command with the -L option to query the Samba server for share information as in the examples below.  The first example is share information from an Ubuntu server and the second example is from a Fedora server.  In both examples you can see the share myshare.  You will have to provide the Samba password that was created previously.

![00142.jpeg](Images/image00218.jpeg)

![00143.jpeg](Images/image00219.jpeg)

You can also use the smbclient command to connect to the share.  In the example below there are four \ before the IP address and two after.  This is because when using the smbclient command you must escape the \ character to give it meaning so if you need two \ characters you have to escape each one which gives you four.  You will have to provide the Samba password that was created previously.  Once connected you will get the smb: \> prompt which means you are connected to the server.  In the example below the ? command is used to access the help menu.

![00144.jpeg](Images/image00220.jpeg)

When connected to the Samba server you can use commands to get and put files on the server just like you can with FTP and SFTP.

The example below shows what happens when not enough \ characters are used.

![00145.jpeg](Images/image00221.jpeg)

You can also mount Samba shares using the Common Internet File System (CIFS).  Most Linux system do not have CIFS installed by default so you will have to install the software.

Ubuntu and Debian

sudo apt-get install cifs-utils

Fedora

sudo dnf install cifs-utils --best

Once CIFS is installed you can use the mount command to mount the Samba share as in the example below.

![00146.jpeg](Images/image00222.jpeg)

You can also use the mount command to view information about the mounted share as in the example below.  You will want to use the grep command to isolate the specific share as there may be many shares on the server.

![00147.jpeg](Images/image00223.jpeg)

To unmount a Samba share use the umount command.

sudo umount ~/myfolder

Fstab

Using the /etc/fstab file you can configure Samba shares to be mounted to the filesystem during the boot process.  There are some security concerns with this configurations, however, as the Samba username and password are place into a configuration file.  

##### User File 

Since the Samba share controls access to the share based on a username and Samba password you have to make the username and password available to the boot process by storing them in a file.  

Create /etc/samba/user file.

Add the following lines replacing sabmba_username with the actual username and the samba_password with the actual password.

username=sabmba_username

password=samba_password

Edit /etc/fstab and add the following line.

//ip_address/sharename /local_mount_point cifs credentials=/etc/samba/user,noexec 0 0

The example below mounts the myshare share from 192.168.56.1 to /home/matt/myfolder and users the username and password from the /etc/samba/user file.

//192.168.56.1/myshare /home/matt/myfolder cifs credentials=/etc/samba/user,noexec 0 0

Reboot the system to mount the Samba share.

Windows

To access a Samba share from a Windows system, open a File Explorer window and type \\ followed by the IP address of the Linux server running Samba in the address bar..

\\IP_address\

You can also connect directly to the share by including the share name.

\\IP_address\share_name

You will be required to provide the Samba username and password.

# Chapter 11. I/O Direction

Almost all of the Linux commands that you will encounter have a common feature – they are all received from your system’s standard input (your keyboard, for example), and then written to the standard output (your computer monitor). The standard error device receives any error messages that you may get. In Linux, these devices are called the following:

*   stdin – standard input
*   stdout – standard output
*   stderror – standard error

These are also called streams, which define how inputs and outputs are distributed in a Linux environment.

Commands get the necessary input that they need from files, and in turn, they sent their outputs to another line. This entire process has a rather highfalutin name, called the I/O (input/output) redirection.

## Redirecting Streams

If you want Linux to redirect the commands for these streams, you will need to enter a command that will do so. What happens is that Linux will write the output to a particular file. If the indicated file does not exist, your operating system will create a file with the name that you included in your command.

Note: If you use a command with a single bracket, the command will overwrite the contents of the existing destination.

Here is a table of the most common I/O redirection commands:

Image source: Linux All-in-One for Dummies

When you interact with the Linux terminal, your computer recognizes your input devices, such as your mouse and keyboard, to be the ones that should be transmitting commands. The standard output and error, on the other hand, are displayed on your screen as a text displayed in a terminal. 

What do you get when you manage to change the input and the output directions of your commands? Being able to do so allows you to make more complex tasks in your operating system. For example, if you are trying to manage your files or when you use Linux for software development, being able to manipulate I/O streams will allow you to become more efficient. 

## Getting Your Input from a File

If you need a command to take instructions from a particular file, you can instruct Linux to make use of that particular file as the standard input instead of your keyboard. For example, key in the command:

Running this command will allow you to see a list of all the lines that the /etc/passwd file contains. Because you used the < sign, you have managed to redirect the standard input, making Linux think that the stdin is the /etc/passwd file instead of your keyboard.

## Sending Your Command Output to Another File

If you want to have a record of a command’s output and save it as a file, you need to change the stdout to a file. For example, type the following command after changing into your home directory:

Using this command will allow you to search all the files that contains the text typedef, and then saves the results in a file named typedef.out. The > sign redirects the standard output into the file that you indicated. Also take note that the above command showed another bash feature: when an asterist is used, you are essentially asking Linux to include all the the files in the indicated directory, which in this case, all the files that are in the directory /usr/include.

Tip: You can append or add an output to the end of an existing file rather than having to create another file to save your output, you can use the >> sign. Take note of this format:

You can also change the standard out to a file by using the cat command, which will prepare small text files. For example, if you want Linux to store all the things that you are writing and only stop when you type in ZZ and press enter, you can use this command:

This means that your computer will be recording all the things that you are typing in your keyboard and will only stop when you press ZZ and Enter. 

## Saving Errors in Files

There are situations wherein you enter a command and then Linux returns with several lines of error messages. These error messages may scroll too fast that you cannot figure out what really is going on. When this happens, you have the option of saving these error messages in a file in order to know what really happened in the command by changing the standard error to a file that you can find later.

Type in the following command in a terminal:

This will look through your entire computer system for files that are named COPYING and will then save all the error to a file named finderr. The command 2> allows you to redirect the standard error to a file. 

Pipes

Type this command in the terminal:

ls | less

This command will pipe the data coming from ls, and then send it to the less command. The ls command is supposed to display the contents of a directory across numerous rows. When you pipe it to the less command, the directory entries are instead placed on a different line.

Filters

Commands that change the output and the piped redirection are called filters. They are also standard commands on Linux that you can use without having to use pipes. Here are some of the filter commands that you can use on the terminal:

*   grep – gives results that matches a text that corresponds to a string pattern that is sent to grep command
*   tr – finds one string and then replaces it with another one
*   find – displays files that has names that match arguments that are sent to the find command
*   tee – redirects the standard input to one/multiple files and the standard output
*   wc – counts lines, characters, and words

# Chapter 12. Commands for compressing and decompressing files

## To create a compress file with the tar extension that has the name file.tar

| tar cf file.tar filestar cf file.tar  file1.c file2.cpp |

## To unpack the file

| tar xf file.tar |

## To create a compressed file by the Gzip program

| tar czf file.tar.gz filestar czf file.tar.gz  file1.c file2.cpp |

## To decompress the file created by Gzip

| tar xzf file.tar.gz |

## To create a file compressed by the Bzip2 program

| tar cjf file.tar.bz2 filestar cjf file.tar.bz2  file1.c file2.cpp |

## To decompress the file created by Gzip

| tar xjf file.tar.bz2 |

# Chapter 13. Wildcards in Linux

There are numerous wildcards in Linux. Let’s examine them.

The “*” wildcard

This is used to match one or more characters in a specified file. When you want to know the list of files in the current directory whose name start with the letter “f”, run the following command:

ls f*

The above command is demonstrated in the figure shown below:

From the figure shown, it is clear that I only have two files whose name start with the letter “f” in the above directory. You can also use the wildcard to find out the files whose names end with a certain pattern. For example:

To know all the files whose name end with …me, run the following command:

ls *me

On my computer, the above command gives the following output:

From the above figure it is very clear that only one file in the directory obeys the pattern specified. 

The “?” wildcard

In Linux the above wildcard is used to match exactly one character. Run the following command:

ls f?le

The above command gives the following output in my computer:

Getting Help

It is also possible to get help in Linux. If you want to know more about a certain command, you can consult the manual files. To find out more about the command “ls”, run the following command:

man ls

The above command will tell you more about the “ls” command and the options associated with it. If you want a short description of the command, run the following command:

whatis ls

With the above command, the options associated with the command “ls” will not be displayed, so use it only when you are not interested in the options.

If you are not sure how to write a certain command in Linux, use the command “apropos” to get help. For example:

To find out the exact name of the “copy” command, type the following:

apropos copy

# Chapter 14. Advanced Linux Navigation commands

## Changing Directories and Finding Files

So, to find any particular file that you want to edit, you must first learn how to get to the folder or directory where that particular file is located. Again, to change directories, all you need to do is make use of the cd command just like in Windows. The syntax to change directory is:

$ cd <name of folder>

Now, there is more to this command than meets the eye. Remember, Linux is exceptionally literal when it comes to the interpretation of commands syntaxes. Again, let us make use of the diagram below:

If for example you are in the var directory/folder and you want to go to the abc folder, all you need to do is type:

$ cd abc

Now, if for example you are in the var folder and you want to go to the etc folder, just typing in $ cd etc from within var will not work. Because then Linux will think that you want to go to the etc folder that is within the var folder, which does not exist.

What you must do is type the command below:

$ cd /etc

Take note of the forward slash before the name of the directory that you want to go to. This forward slash will tell Linux to first go to the root directory and then find the etc folder or directory. Now, Linux will now be able to successfully bring you to the etc folder since it is able to locate it in the root directory.

Now, consider the example diagram above. Let us say that you are in the root directory and you want to go to the www directory. If you type:

$ cd www

Linux will not be able to bring you to the www directory; it will say that the directory does not exist. Why? Because remember, you are in the root directory. As far as Linux is concerned, there are only two files within the root directory at this point: etc and var. To be able to go to the www directory from root, you must type:

$ cd /var/www

Now you might be asking, won't the second forward slash in the above command bring you back to root? No, it will not. Linux only interprets the first instance of the forward slash as the root directory. The second forward slash will be interpreted as an instruction to look for the directory that succeeds it, from the directory that precedes it.

Here is another example: Let us say you are in the www directory and you want to go to the etc directory. If you type in:

$ cd etc

This command will not work. Keep in mind that you are currently in the www directory. As far as Linux is concerned, there is no etc directory inside the www directory. To make this work, you have to type the command below:

$ cd /etc

So again, the first instance of the forward slash will be interpreted by Linux as an instruction to go to the root directory first. Once it is in the root directory, it will then find the etc directory. Of course, this command will successfully bring you inside the etc directory since it exists within the root folder.

## Listing/Displaying Files

Now, once you are in a directory, it is always important to find out what else is in that directory. To list files in Linux, you simply use the command ls.

$ ls

And then, depending on what you want to do, you can apply one of two arguments. If you do:

$ ls -l

What will happen is that all the files and folders will get listed. In addition to that, it will also show you the permissions for those files and folders, the date they were modified, the group ownership of the files and folders, and the individual owner.

A lot of times that can turn into a really big file. So, what you can also do is type:

$ ls -m

This time, instead of Linux giving you a really long list, it just types everything into a nice block so you can see every bit of information about the files and folders. That is all you need to do to list files and folders in Linux.

Now, let’s say you want to edit a critical configuration file, but you have absolutely no idea where that file is. Thankfully, Linux does have a search option. In order to search for files and folders, all you do is type:

$ sudo find -iname <file/folder name>

That is sudo, a space, followed by the word find, another space, the argument -iname, another space, and then finally the name of the file or folder that you are looking for. Now you might be askin, what does that ­-iname argument do? Well, what it does is it makes the search case insensitive.

If you are looking for a folder named home for example, and you use the search command with the ­-iname argument, it will come back with all the folder that has home as the folder name. Whether that folder is name as Home, homE, hOme, HOme, hoMe, or HOME, it will come up in the search result.

Whereas if you mess up the capitalization of the name of the file or folder that you are looking for, and you did not use the -iname argument, the search may come back with no results because no file or folder match the capitalization.

Also, do not forget about the sudo command when executing find commands in Linux. If you do not put in sudo at the beginning, the find command will fail in the most obnoxious way in that it will not tell you that it failed. It will simply not give you any results. So you will think that the file does not exist on the computer, when in actuality it does exist but you just did not use sudo.

If you put an asterisk before a file or folder name, that means that you are looking for "anything before"  that particular file or folder name. Let us say you are trying to locate a configuration file in Linux. In Linux, all configuration files have .conf suffix. If you are looking for a configuration file but you forgot what the exact name is, you may want to pull up all the files that have .conf as their suffix. In this case, what you do is type the command below:

$ sudo find -iname *.conf

What this command will do is look for a file or folder name that begins with anything and ends with .conf. Now, what if you know the filename of the file that you are looking for, but you do not know the suffix. In this case, you need to type the command below:

$ sudo find -iname php*

What this command will do is look for a file or folder name that begins with php and ends with  anything.

## Making, Deleting, Moving, Copying, Renaming

Now we need to talk about making, deleting, moving, copying, and renaming files and folders in Linux. The first thing that we are going to do is talk about creating a folder. It is pretty straightforward. All you do is type:

$ sudo mkdir <name of directory/folder>

That is sudo, followed by a space, and then the mkdir parameter, another space, and then the name of the folder or directory that you want to make. As you can probably already guess, mkdir stands for "make directory."

Keep in mind that if you do not put the full path of the directory, this command will simply create that directory or folder inside the directory that you are currently in.

For example, let us say you are in the var directory and you want to create a Notes folder inside the etc directory. If you type:

$ sudo mkdir Notes

This command will just create the Notes folder in the var directory. To create the Notes folder in the etc directory from within var, you must type in the full path just like the one below:

$ sudo mkdir /etc/Notes

This way, Linux will go to the root directory first, and then into the etc directory, and within the etc directory create a Notes folder. Typing in the full file path will ensure that no matter where you are in the file system, you would be able to create the folder in the right location. That is all you need to do to create a folder or directory in Linux.

Deleting files or folders is just as simple. What you do is type the command below:

$ sudo rm <file or folder name>

That is sudo, a space, followed by the letters rm, another space, and then finally the name of the file or folder that you want to delete. As you may have already guessed, rm stands for remove. Let us say for example you want to delete a file named Notes. All you need to do is type:

$ sudo rm Notes

Deleting folders is a little bit different, however. You actually still follow the same syntax as when you are deleting a file. The only difference is that you have to add the -R argument at the end of the command when deleting folders. The argument ­-R stands for recursive. By using the recursive argument, you are basically telling Linux to do the same task to the contents of the folder.

Let us say you want to delete the www folder that has three files in it. To do this, you just type:

$ sudo rm www -R

This command will not only delete the folder itself, but also the three files that are inside it. If you do not put a recursive argument at the end of a delete folder command, Linux will not be able to execute it successfully, since you cannot delete a folder without deleting the contents as well. The only time you would be able to delete a folder successfully without the recursive argument is when the folder is empty to begin with.

In Linux, there is no command to rename files and folders per se. Instead of rename, we have the move command in Linux. Let us say for example you have a file named file1, and you want to change the name to file2. To do that you have to type the command syntax below:

$ sudo mv <name of old file> <name of new file>

That is sudo, a space, followed by the letters mv, another space, the name of the original file, another space again, and then followed by the name of the new file. So again, going back to our example, if you want to change the name file1 to file2, you have to type:

$ sudo mv file1 file2

This command will change the name of file1 to file2. It is still technically renaming a file. But in Linux, we use the term move. Now, how about moving a file from folder to folder? Well, the same syntax still applies. However, instead of just typing in the name of the files and folders, you must indicate the full path.

Let’s say you want to move a file named file1 inside the var folder to the etc folder in the root directory. To do this, you must type the command below:

$ sudo mv /etc/var/file1 /etc/file1

That is sudo, a space, followed by the letters mv for move, another space, the exact file path of the source file, another space, and then lastly followed by the exact file path to the destination. It is as simple as that.

Copying is another important task in Linux. A lot of times, especially if you are dealing with a configuration file, it is essential that you make a backup file before you start messing around with the original file. Otherwise, if you mess up the original file, you may end up damaging the program that that file is associated with.

To copy files in Linux, all you have to do is type:

$ sudo cp <name of the file> <name of the copied file>

That is sudo, a space, followed by the letters cp for copy, another space, the name of the file you want to make a copy of, another space, and then finally the name of the duplicate file. So, let us say you want to make a copy of a file named file10. All you need to do is type:

$ sudo cp file10 file10.bak

Here, file10.bak is the name of the duplicate file of file10. As you can see, it is easy to make copies of files in Linux.

## Mounting Drives

The last big thing that you have to understand in order to navigate Linux is mounting drives. This is where you have an external hard drive, you plug it into the computer, and you need to mount the drive in order for you to browse its contents. That external hard drive could be a normal hard drive, a flash drive, or a CD-ROM drive. Flash drives and CD-ROM drives are considered as hard drives in Linux.

Basically, any drive that you will connect to the computer is a drive that would have to be mounted. The first thing that you have to understand is how the mounting process works in Linux. The mounting process is as follows:

Step 1 – Connect the hard drive.

Step 2 – Create a folder for your mount point.

Step 3 – Grab some specific information about the hard drive and then point the mount point folder to that hard drive.

That is essentially how you mount the drive. The mount point folder now gets tied to the hard drive. Since they are tied together, you can now browse the contents of the hard drive through the mount point folder.

So how do you actually make the mount point folder in the command prompt? Simple: just type the command below:

$ sudo mkdir /mnt/<name of mount point folder>

Take note of the /mnt directory that we are creating here. Know that /mnt is the standard mounting directory in Linux. This mounting directory is universal. You can use a different mounting directory if you want. However, using /mnt is considered as a best practice since most Linux administrators and programmers will use it by default. 

Now, let’s say you want to mount a connected hard drive to a mount point named drive1\. To do this, you just type:

$ sudo mkdir /mnt/drive1

By typing the command above, you are creating the folder that your hard drive will be mounted to. Once you do this, the next thing that you have to do is find out the information about the hard drive that you are trying to mount. To do this you just run the command below:

$ sudo fdisk -l

The above command will list all of the physical hard drives that are connected to your system. This list is going to show you the different hard drives that are connected to your system, how much space they have, etc. In there, you are looking for something that is going to look like /dev/sda1\. These are called disk names in Linux.

Linux disk names are always arranged in an alphabetical order. If you have two hard drives connected to your Linux system, for example, they will be named /dev/sda and /dev/sdb, respectively. The numbers that succeed the disk names refer to the partitions within that particular disk.

If you have two partitions in your first hard drive for example, they will show up as /dev/sda1 and /dev/sda2 respectively. If you have three partitions in your second hard drive, they will show up as /dev/sdb1, /dev/sdb2, and /dev/sdb3 respectively.

So, in order to mount the hard drive, all we are going to do once we find the disk name is type the following:

$ sudo mount <disk name> <mount point>

If we were to apply this command syntax to our example, the command should look like this:

$ sudo mount /dev/sda /mnt/drive1

This is all you to do mount your hard drive. Now, you can go and change directory to /mnt/drive1 by typing:

$ sudo cd /mnt/drive1

And once you are in your mount point directory, you can type:

$ ls -l

The above command will list all the contents of that hard drive. You can now apply all the Linux navigation commands that you have learned so far in your mounted drive. That is basically how you mount a hard drive in Linux.

Now, if you are done with that hard drive and you want to un-mount it, all you need to do is type:

$ sudo umount <disk name> <mount point>

As you may have already guessed, umount stands for un-mount. Once you have successfully un-mounted a hard drive, you can repeat the same process of mounting a drive if you want to use a new hard drive.

# Chapter 15. The Processes

You should also understand processes if you want to be a Linux user. In this chapter, you’ll learn about the different computer processes performed in Linux operating systems.

The Basics

Multi-users and Multi-tasking

Now that you know how to interact with the system, you may study computer processes in more detail. Some commands cannot be executed using a single process. There are commands (e.g. “mozilla”) that trigger a group or series of processes.

Additionally, Linux is based on the Unix system, where it is natural to have different users running different commands simultaneously. Obviously, you need to make sure that the computer’s processor can handle all the active processes. You should also provide a functionality that allows users to switch between different processes. In certain cases, you have to continue running a process even if the user who initiated it already logged out. You should also give users the capability to resume interrupted processes.

## Different Types of Processes

Interactive Processes

You have to use a terminal session to start and control interactive processes. That means you can only start an interactive process if you are already connected to the system. Basically, the system doesn’t start these processes automatically as part of its basic functions. An interactive process runs in the foreground, taking over the terminal that started it. When this happens, you can’t initiate other programs as long as that particular process is active. As an alternative, you may run them in the background, so that the terminal you used can receive other commands.

Linux shells provide a feature called “job control.” This feature allows you to handle various processes easily. Job control can switch processes between the background and the foreground. With this, you may quickly start processes in the background.

Important Note: You can only run processes in the background for programs that don’t require user inputs. In general, tasks are placed in the background if they take a long time to complete.

The following list shows the common control applications for Linux systems:

*   “bg” – This is used to reactivate an interrupted process in the background.
*   “fg” – This returns the process onto the foreground.
*   “jobs” – It shows the commands being run in the background.
*   “kill” – This ends a task.
*   “regular_command” – This runs the command in the system’s foreground.
*   “command &” – This runs the command in the system’s background. It releases the terminal: you can run other programs while the previous command is still active.
*   Ctrl + Z – This stop (suspend, but not terminate) a process that runs in the system’s foreground.
*   Ctrl + C – This interrupt (stops and terminates) a process that runs in the foreground.
*   “%n” – The system assigns a number to each process that runs in the background. Using the “%” symbol, you can refer to a process through its number (e.g. bg %2).

Automatic Processes

Automatic (also known as batch) processes are not linked to any terminal. Instead, these are jobs that can be lined up in the spooler area, where they will be performed on a first-in first-out basis. These processes can be executed using one of these methods:

*   At a specific time and date – You must use the “at” command to accomplish this.
*   At times when the overall system load is sufficiently low to receive additional tasks. You can do this through the “batch” command. In general, processes are lined up so they can be executed once the system load is below 0.8\. In huge systems, the administrator may utilize batch processing when huge amounts of data need to be processed or when tasks requiring many resources need to be performed on an already busy system. You can also use batch processing to optimize system performance.

Daemons

These are server processes that continuously run. Often, they are activated during startup and wait in the system’s background until their services are needed. A common example is “xinetd”, the networking process, which is triggered in each boot procedure. After the booting process, xinetd waits until a program (e.g. a POP3 client) needs to connect to the internet.

The Boot Process

One of the popular features of Linux is its method of initiating and suspending the OS, where it gets specific programs through their ideal settings, allows you to modify the settings and the boot procedure, and stops in an organized and graceful way.

Beyond manipulating the boot and shutdown processes, the “openness” of Linux systems helps you to determine the causes of problems related to shutting down or booting up your machine.

The Procedure

When a computer is started up, the CPU looks for the Basic Input/Output System (BIOS) and executes it. This program is coded into the computer’s permanent ROM (read-only memory) and is available for use anytime. The computer’s BIOS provides peripheral devices with a low-level interface and manipulates the first phase of the startup procedure.

The BIOS checks the entire system, searches for and tests peripheral devices, and searches for a drive that can be used to start the system. Often, BIOS checks the CD-ROM drive (for newer OS) or the floppy drive (for older ones) for usable media. The sequence of the drives utilized for the booting process is commonly managed by a certain BIOS configuration on the operating system. Once a Linux system is installed onto the computer’s hard drive, the BIOS searches for an MBR (i.e. master boot record) starting at the initial part of the first hard disk, puts the data into the memory, and gives control to it.

The Master Boot Record holds the steps on how to use the LILO or GRUB boot-loader, through a predetermined OS. Afterward, the MBR activates the boot-loader, which controls the rest of the process (that is, if a boot-loader is installed in the Master Boot Record). In the standard configuration of the Red Hat OS, grub utilizes the settings in the master boot record to show available boot choices. Once grub gets the right instructions for the OS to boot, either from the configuration file or its own command line, it acquires the required boot file and passes the control of the computer to the OS.

## The Different Features of GRUB

This method of booting up a computer is known as direct loading. This is because no transitional code exists between the boot-loader and the OS’s main files (e.g. the kernel). Thus, startup instructions are utilized to load the OS directly.

On the other hand, the boot procedure used by other systems may be different from the one given above. For instance, MS-DOS and Windows OS overwrite the MBR completely as soon as they are installed without using any part of the existing MBR’s settings. This deletes the data stored by other operating systems (e.g. Linux) inside the MBR. Microsoft’s operating systems, just like other commercial systems, are booted through a process called chain loading startup method. In this method, the MBR checks the initial segment of the partition that holds the OS, where it gets the files required to boot the operating system.

Grub can support both of these methods. That means you can use grub with almost all operating systems, common file structures, and hard disks that can be recognized by your BIOS.

GRUB has other useful features. Here are the most important ones:

*   Grub provides x86 computers with a command-based environment (even if no OS has been installed yet). This allows computers to achieve maximum versatility – they can easily load operating systems or collect data about those systems.
*   Grub is compatible with LBA (i.e. Logical Block Addressing) mode. This mode is required to access IDE and SCSI hard drives. Without LBA, hard disks may face a 1024-cylinder restriction, where the computer’s BIOS cannot get a file past that point.
*   Each time the system is started, grub’s configuration files are loaded from the hard disk. That means you can change boot options without overwriting the data in the MBR.

The INIT

Once loaded, the kernel finds INIT in the “sbin” directory and runs it.

The INIT is the parent/grandparent of all the tasks that run automatically on a Linux OS. First, INIT reads its own initialization file (this file is located in the “etc/inittab” directory). The initialization file tells INIT to load a configuration script for the system, which arranges the paths, begins swapping, scans the system files, etc. Simply put, this stage completes everything your machine needs during system startup (i.e. starting serial ports, setting the computer’s clock, etc.).

Afterward, INIT keeps on reading the initialization file, which defines how the OS should be run in every operating level. This file also assigns a run level for the system. Run levels are the configurations of computer processes. Once a run level is assigned for the system, INIT begins the background tasks required by the system. INIT does this by checking the correct “rc” directory for the assigned run level. Lastly, INIT runs all of the kill scripts using a stop parameter.

Shutdown

Linux was not designed to be turned off. If you really need to, however, you may run the “shutdown” command. Once the shutdown process is completed, you may use –h to suspend the system or –r to restart it.

The –r and –h options are now capable of invoking the shutdown command if used while the OS is using run levels 1 to 5\. This range of run levels ensure correct shutdown for the whole system. However, this is a bad habit to develop since not all Linux systems have this capability.

If the machine doesn’t turn itself off, you must not power off the machine until the screen shows a message indicating that the OS is suspended or completed shutting down. Waiting for this message gives your computer ample time to disconnect active partitions. Remember: impatience can result to data loss.

## How to Manage Processes

The Admin’s Tasks

Although it is the Admin’s job to manage the system’s processes, it may be useful for common users to know some things about it. This knowledge becomes important if the users’ own tasks and efficiency are concerned.

This section will explain system performance using theories. Here, you’ll learn about:

The problems encountered by common users

The methods common users can use to optimize available resources

How Much Time Does a Process Require?

Bash provides a pre-installed time command that shows the amount of time required to execute processes. This tool offers accuracy and versatility – you can use it to get precise data about any command. To help you understand the time command, a screenshot is given below:

In this example, the time command is used to calculate the amount of time needed to create a certain .pdf file. The result shows that the process requires 1 minute and 41 seconds.

The file directory /usr/bin contains a time command for GNU (this is different from the pre-installed BASH tool). This command shows more data that can be used in various ways. Additionally, it displays the command’s exit status and total elapsed time. When used with the GNU time command, the example given above provides these results:

You may check the system’s Info pages if you want to learn more about these time commands.

Performance

For common users, “excellent performance” refers to quick and correct execution of processes. For system managers, however, these words have more meaning: the admin needs to maximize the performance of the entire system, including daemons, programs, and users. In general, system performance may depend on numerable “insignificant” things that are not evaluated by the time command. Here are some examples of these “insignificant” things:

*   Access to drives, display, controllers, interfaces, etc.
*   The program being run was poorly designed or doesn’t utilize the computer’s resources efficiently.
*   The number of active users in the system.
*   The time of day.
*   The accessibility of remote networks.

Load

Basically, load relies on what is ordinary for your network. For instance, an old P133 that runs a firewall, file server, SSH server, route daemon, proxy server, sendmail server, and other devices can support up to 7 active users. In this kind of situation, the load is still zero. Some systems, particularly those that have several processors, can easily support up to 67 users.

There is just one way to identify your network’s load: check it on a regular basis. This way, you’ll know what’s ordinary for your network. If you won’t use this method, you can only gauge system load from the command line’s response time. The response time lacks accuracy – it cannot be reliable since various factors are affecting it.

Remember that different networks behave differently even if they have identical load averages. For instance, a network can render 3D images smoothly if it has a graphics card that supports hardware acceleration. A network that uses an old VGA card, however, will be as slow as a turtle when rendering images. An old system can be extremely slow when starting an X server, while modern ones won’t even “feel” the added load.

Priority

The importance (or priority) of a task is determined by its nice number. Tasks with a high nice number are “cooperative” (or nice) to other users, other tasks, and the network itself: they are low-priority tasks. Low nice numbers indicate that the tasks they belong to are important and will take more system resources.

You can make a task “nicer” by giving it a higher nice number. However, this technique is only effective for processes that require lots of CPU time (e.g. software compilers). Processes that utilize lots of I/O time consistently are provided with a low nice number (i.e. higher priority). For instance, keyboard inputs always receive the highest priority in a computer network.

You can set a program’s importance using the nice command.

Many systems offer a command called BSD renice. This command allows users to edit the “niceness” of an active program. You may check the manual of your OS to find out if this command is available.

CPU Resources

On each operating system, many processes need to use the computer’s CPU at the same time. This is true even if you’re the only active user. Each process requires a specific amount of CPU resource in order to run properly. Sometimes, computer programs don’t get sufficient resources since the CPU handles many requests. You need to know the available system resources if you want to optimize your computer. There are tools that you can use to obtain this data.

Uptime, one of the commands you can use in Linux, lacks accuracy (it can only show averages, you need to identify the normal number), but can be useful in some situations. Here are some of the things you can do to improve the efficiency of your CPU.

*   Stop your system from performing unnecessary tasks. Stop programs and daemons that you aren’t using. You may use the locate command for this.
*   Run resource-intensive processes when the system’s load is at a low level. Often, you should run “heavy” processes during nighttime.
*   Run low-priority tasks first.

If these methods don’t solve your problem, you may need to get a better CPU. For Linux systems, this is the system admin’s job.

Users

In Linux systems, computer users can be segregated into different types, depending on how they use system resources. Here are the three types of Linux users:

*   People who run lots of small processes. A good example for this would be inexperienced Linux users.
*   People who run several (but complex) processes. Examples for this type are people running emulators, calculations, and simulations.
*   People who run few processes that require lots of CPU time (e.g. game developers).

As you can see, system requirements differ for each type of user. Also, it is extremely difficult to meet the needs of all the users in a network. If you belong to a multiuser network, it is beneficial (and entertaining) to identify the habits of your fellow users. This technique will help you to maximize the available system resources.

Visual Tools

For graphical environments, you have a wide-range of options in terms of monitoring tools. Here’s a screenshot of a tool called Gnome System Monitor. This tool can find and show information about active tasks. Also, it can monitor system resources.

Most Linux systems have some useful icons (e.g. monitors for load, disk, memory, etc.) that you may install onto your taskbar.

## Listing Processes and Displaying Information

To display the currently running processes use the ps command. If no options are specified, ps displays the processes associated with your current session. To see every process including ones that are not owned by you, use ps -e. To see processes running by a specific user, use ps -u username.

ps - Display process status.

Common ps options:

-e - Everything, all processes.

-f - Full format listing.

-u username - Display processes running as username.

-p pid - Display process information for pid. A PID is a process ID.

Common ps commands:

ps -e - Display all processes.

ps -ef - Display all processes.

ps -eH - Display a process tree.

ps -e --forest - Display a process tree.

ps -u username - Display processes running as username.

$ ps
  PID TTY          TIME CMD
19511 pts/2    00:00:00 bash
19554 pts/2    00:00:00 ps
$ ps -p 19511
  PID TTY          TIME CMD
19511 pts/2    00:00:00 bash
$ ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
bob      19511 19509  0 16:50 pts/2    00:00:00 -bash
bob      19556 19511  0 16:50 pts/2    00:00:00 ps -f
$ ps -e | head
  PID TTY          TIME CMD
    1 ?        00:00:02 init
    2 ?        00:00:00 kthreadd
    3 ?        00:00:19 ksoftirqd/0
    5 ?        00:00:00 kworker/0:0H
    7 ?        00:00:00 migration/0
    8 ?        00:00:00 rcu_bh
    9 ?        00:00:17 rcu_sched
   10 ?        00:00:12 watchdog/0
   11 ?        00:00:00 khelper
$ ps -ef | head
UID        PID  PPID  C STIME TTY      TIME CMD
root         1     0  0 Dec27 ?    00:00:02 /sbin/init
root         2     0  0 Dec27 ?    00:00:00 [kthreadd]
root         3     2  0 Dec27 ?    00:00:19 [ksoftirqd/0]
root         5     2  0 Dec27 ?    00:00:00 [kworker/0:0H]
root         7     2  0 Dec27 ?    00:00:00 [migration/0]
root         8     2  0 Dec27 ?    00:00:00 [rcu_bh]
root         9     2  0 Dec27 ?    00:00:17 [rcu_sched]
root        10     2  0 Dec27 ?    00:00:12 [watchdog/0]
root        11     2  0 Dec27 ?    00:00:00 [khelper]
$ ps -fu www-data
UID        PID  PPID  C STIME TTY      TIME CMD
www-data   941   938  0 Dec27 ?    00:00:00 /usr/sbin/apache2 -k start
www-data   942   938  0 Dec27 ?    00:00:00 /usr/sbin/apache2 -k start
www-data   943   938  0 Dec27 ?    00:00:00 /usr/sbin/apache2 -k start

Here are other commands that allow you to view running processes.

pstree - Display running processes in a tree format.

htop - Interactive process viewer. This command is less common than top and may not be available on the system.

top - Interactive process viewer.

## Running Processes in the Foreground and Background

Up until this point all the commands you have been executing have been running in the foreground. When a command, process, or program is running in the foreground the shell prompt will not be displayed until that process exits. For long running programs it can be convenient to send them to the background. Processes that are backgrounded still execute and perform their task, however they do not block you from entering further commands at the shell prompt. To background a process, place an ampersand (&) at the end of the command.

command & - Start command in the background.

Ctrl-c - Kill the foreground process.

Ctrl-z - Suspend the foreground process.

bg [%num] - Background a suspended process.

fg [%num] - Foreground a background process.

kill [%num] - Kill a process by job number or PID.

jobs [%num] - List jobs.

$ ./long-running-program &
[1] 22686
$ ps -p 22686
  PID TTY          TIME CMD
22686 pts/1    00:00:00 long-running-pr
$ jobs
[1]+  Running  ./long-running-program &
$ fg
./long-running-program

When a command is backgrounded two numbers are displayed. The number in brackets is the job number and can be referred by preceding it with the percent sign. The second number is the PID. Here is what it looks like to start multiple processes in the background.

$ ./long-running-program &
[1] 22703
$ ./long-running-program &
[2] 22705
$ ./long-running-program &
[3] 22707
$ ./long-running-program &
[4] 22709
$ jobs
[1]   Done         ./long-running-program
[2]   Done         ./long-running-program
[3]-  Running      ./long-running-program &
[4]+  Running      ./long-running-program &

The plus sign (+) in the jobs output represents the current job while the minus sign (-) represents the previous job. The current job is considered to be the last job that was stopped while it was in the foreground or the last job started in the background. The current job can be referred to by %% or %+. If no job information is supplied to the fg or bg commands, the current job is operated upon. The previous job can be referred to by %-.

You will notice that jobs number 1 and 2 are reported as being done. The shell does not interrupt your current command line, but will report job statuses right before a new prompt is displayed. For example, if you start a program in the background a prompt is returned. The shell will not report the status of the job until a new prompt is displayed. You can request a new prompt be displayed by simply hitting Enter.

To bring a job back to the foreground, type the name of the job or use the fg command. To foreground the current job execute %%, %+, fg, fg %%, fg %+, or fg %num. To foreground job number 3, execute %3 or fg %3.

$ jobs
[3]-  Running      ./long-running-program &
[4]+  Running      ./long-running-program &
$ fg %3
./long-running-program
$

To pause or suspend a job that is running in the foreground, type Ctrl-z. Once a job is suspended it can be resumed in the foreground or background. To background a suspended job type the name of the job followed by an ampersand or use bg followed by the job name.

$ jobs
[1]   Running   ./long-running-program &
[2]-  Running   ./long-running-program &
[3]+  Running   ./another-program &
$ fg
./another-program
^Z
[3]+  Stopped   ./another-program
$ jobs
[1]   Running   ./long-running-program &
[2]-  Running   ./long-running-program &
[3]+  Stopped   ./another-program
$ bg %3
[3]+ ./another-program &
$ jobs
[1]   Running   ./long-running-program &
[2]-  Running   ./long-running-program &
[3]+  Running   ./another-program &
$

You can stop or kill a background job using the kill command. For example, to kill job number 1 execute kill %1. To kill a job that is running in the foreground, type Ctrl-c.

$ jobs
[1]   Running     ./long-running-program &
[2]-  Running     ./long-running-program &
[3]+  Running     ./another-program &
$ kill %1
[1]   Terminated  ./long-running-program
$ jobs
[2]-  Running     ./long-running-program &
[3]+  Running     ./another-program &
$ fg %2
./long-running-program
^C
$ jobs
[3]+  Running     ./another-program &
$

## Killing Processes

Ctrl-c - Kills the foreground process.

kill [signal] pid - Send a signal to a process.

kill -l - Display a list of signals.

The default signal used by kill is termination. You will see this signal referred to as SIGTERM or TERM for short. Signals have numbers that correspond to their names. The default TERM signal is number 15\. So running kill pid, kill -15 pid, and kill -TERM pid are all equivalent. If a process does not terminate when you send it the TERM signal, use the KILL signal which is number 9.

$ ps | grep hard-to-stop
27398 pts/1    00:00:00 hard-to-stop
$ kill 27398
$ ps | grep hard-to-stop
27398 pts/1    00:00:00 hard-to-stop
$ kill -9 27398
$ ps | grep hard-to-stop
$

# Chapter 16. Making Linux More Secure

There are a lot of reasons that you need to protect your computer from other users, but the bottom line is that you do not want any user to delete or modify your system files. If you are handling a network of computers, you also do not want any user to inadvertently or purposely change anything in their system that may cause the entire system to be compromised.

As there is also a good chance that you will be connecting your Linux computer to the internet, you will need to ensure that you are always able to establish a secure connection and that you have done all the steps to protect your computer from unwanted access. In this chapter, you will learn how to create layers of security in order to prevent other users from denying you access to your computer, stealing information, or destroying your data.

## Why Worry About Security

Your internet connection makes your computer an entry point for a lot of security issues, simply because you allow your system to be accessible to hundreds of millions of other computer users online. If you are an operator of an internet host that shares data to others, you definitely will want to use your computer’s Internet services, such as file transfer protocol (FTP). However, these servers always have a vulnerability that criminal hackers may possibly exploit. For this reason, you will want to take extra precaution in order to lessen the risk of being attacked. At the same time, you will also want to protect your network from users outside your network, especially as you communicate with other computers through the web.

## Ensuring Password Security in Linux

Unix passwords are historically stored in a file named /etc/passwd, which can be read by any user. For example, the file entry for /etc/passwd for a computer’s root user may ![00099.jpeg](Images/image00224.jpeg)appear like this:

You will notice that colons separate the fields in this file, with the second field displaying the user’s password in an encrypted form. For the system to verify whether an entered user password is valid, the program that uses the password encrypts the entry and then compares the result with the encrypted text that was stored in the /etc/passwd file. If the entries match, then the user can use the program.

However, any hacker can easily decrypt passwords using a dictionary attack – a type of decrypting method by trying out possible combinations in an encrypted password to find out what the plain text equivalent is. If you have access to the /etc/passwd file, then you are only a few steps away from being able to crack a password. If you are not an authorized user of the computer that you are trying to hack, then you can make use of possible vulnerabilities in the target’s web services, such as the FTP and mailing services, in order to infiltrate and get the file that you want.

It is a good thing that Linux has made several improvements when it comes to making the operating more secure, which include the following:

### Shadow Passwords

Leaving passwords in locations that are easily accessible is bad security, even though these passwords are encrypted. For this reason, Linux no longer makes it a practice to store passwords in /etc/passwd file, which everyone can access – passwords are now stored in a shadow password file, which is named /etc/shadow, that only the root user can access. 

![00100.jpeg](Images/image00225.jpeg)In Linux, the /etc/passwd file looks like this: 

Take note that the second field does not show an encrypted password; instead, it shows a single character x. The x in this field is your shadow password, and the true encrypted ![00101.jpeg](Images/image00226.jpeg)password is stored in the file /etc/shadow, which looks like this:

You will notice that the fields in the file are still separated by colons, wherein the first two fields represent the username and the encrypted password, respectively. The remaining fields, on the other hand, control the expiration of your password. This means that you do not need to change or even decrypt the password stored in this file. Instead, you can change the expiration date of the password using the change command.

You can see a user’s password expiration date as a root user by using the following ![00102.gif](Images/image00227.jpeg)command:

If you want to see to it that you will be forced to change your password at regular intervals, you can set the number of days that a password will remain valid by using the –M option. For example, if you want to force the user kdulaney to change his password every 90 ![00103.jpeg](Images/image00228.jpeg)days, use the following command (see to it that you are logged in as root):

### PAMs

Linux also uses another feature when it comes to improving password security by using an MD5 algorithm. What it does is that it reduces a message to a 128-bit digest, which is called fingerprint, of a document so that you will be able to attach a digital signature and encrypt it with a private key. While MD5 is known for making documents secure, the same concept works well for passwords.

Another advantage that MD5 has over traditional passwords is that you can use a longer password. As you already know, longer passwords are tougher to crack, even when the /etc/shadow file falls into the hands of a criminal hacker. You can see that the password ![00104.jpeg](Images/image00229.jpeg)field in this file employs an MD5 encryption:

Another module that called the PAM (pluggable authentication module) encrypts the passwords with MD5\. In Linux, you can set the PAMs in such a way that you can switch authentication while on the go, without having to change programs that are necessary in verifying identity, such as the username and the password.

The PAMs in Linux are used extensively and they are also used in different other modules in your system. All configuration files involving the PAMs are stored in the directory named ![00105.jpeg](Images/image00230.jpeg)etc/pam.d. To see the files in this directory, use the following command:

## Configuring Default Permissions

When you create a new file, who can use this file by default? You can determine the answer to this question by typing in the command umask, which will show you the user file-creation mask. When you enter this command, you will see the file-creation mask for the file that you are inquiring about. If you are a root user, the user mask is configured to 22, and for everyone else, 0002\. In the following exercise, you will see how the file-creation mask works:

1.  ![00106.gif](Images/image00231.jpeg)Log in as the root user and type:

This will create a file with the name junkfile that does not have any content.

2.  Enter ls -l command in order to view the permissions. You will see a line that ![00107.jpeg](Images/image00232.jpeg)looks like this:

Now, you can interpret the value of the permission setting by converting the permission letters that are shown in the first field. To do that, think that the first letter gets a value of 4, the second gets 2, and the third gets 1\. If you have the permission letters rw-, this translates to 4+2+0 (0 because the third letter is not available), which is equivalent to 6\. Moving on to the next 3 letters, which is r--, you get the equivalent of 4\. That means that the permission string of -rw-r--r—is equivalent to 644\.

3.  Deduct the permission setting that you got from 666 to determine the umask setting.

666-644 is 022, which means that the permission setting is set to root.

Now, if you want to set a different umask, simply key in the command umask and then type in the numerical value of the mask. This is how you can perform this task:

1.  Determine the permission settings for newly-made files.

If you want all new files to be read and edited by the owner only, you will need to write a permission setting that appears as re-------

2.  Convert the permission setting into its corresponding numerical value. You will need to assign 4 to the initial field, 2 to the next field, and 1 to the third. 

For this example, you will need to have a permission setting that is set to 600\.

3.  Deduct the target permission from 666 to get the value of the mask that you wish to assign.

To achieve the 600 permission setting, compute for the mask by getting the result of 666-600\. You get a value of 066\.

4.  Type in the umask command, followed by the value you determined.

![00108.gif](Images/image00233.jpeg)To get the permission setting that you want, enter this command:

Note: 022 is set as a default umask because it translates to read and write function is only allowed for the owner of the document, while read permission is given to everyone else. The reason for this is because Linux assumes that file owners do not want their files to be editable by everyone to prevent possible risks.

## Looking Out for Permissions to Set User ID   

There is a permission setting that can be seen as threatening to security, which is called setuid or suid (set user ID). This permission setting applies to files that you can run, or executable files. When the setuid/suid permission is allowed, a file is executed under the owner’s user ID. In short, if the suid permission is on and the file is owned by the root user, the targeted program will view the root user to be the one running the file and not check on who ran the program in reality. This also means that the permission for suid will allow the program to do more functions than what the owner intends all the other users to perform. It also helps to take note that if the said program that contains the suid permission has some security vulnerabilities, criminal hackers can create more havoc through these programs.

To find all enabled suid permissions, you can use the find command like this:

![00109.jpeg](Images/image00234.jpeg)

![00110.jpeg](Images/image00235.jpeg)After entering this command, you will see a list of files that appears like this example:

Take note that there are numerous programs that are set with a suid permission because they require it. However, you may want to check the entire list to make sure that there are no programs that have odd suid permissions. For example, you may not want to have suid programs located in your home directory.

![00111.jpeg](Images/image00236.jpeg)Here is an example: typing the ls –l /bin/su will give you the following result:

The character s in the permission setting alluded to the owner (appears as –rws) shows that the file /bin/su has suid permission. This means that the su command, which allows any user to have superuser privileges, can be used by anyone. 

# Conclusion

There are thousands of reasons why you should learn Linux in this age. Even if you are not yet ready to make the switch from your current operating system to Linux-based systems, learning how they operate is a useful skill. A recent survey found out that employers are more likely to hire someone conversant with Linux-based distributions since it shows that you are flexible and versatile. There are many instances where using a Linux-based system will be more appropriate.

The Linux community is also another thing which should attract you. There are many Linux users always eager to help you out. In most cases, any issue you encounter will most likely have been resolved in the forums. So, take your time, sign up in a forum and go through the conversations to learn more about what is happening in the Linux world. When you finally become an advanced user, give back to the community be helping others. This is what makes the Linux community great and such a big force.

We can list many reasons why you should be using Linux, but the most important is the fact that you have the freedom to experiment and try out new things. The command line gives you so much power to understand and control how your computer works, the free software repositories, the multiple desktop feature, the hardware support, using Linux on any computer, security, and interoperability with other systems. All these reasons and many more make it essential to learn and be conversant with Linux.

If you want a new system that’s different from windows, more secure, and in many cases better than windows, Linux is ultimately the way to go with all of this, since you can do so much with it, and there are many customizing options that you can try out, including changing some of the aspects of the system. It is not as held back as Windows is in that regard, and there is a reason why many people are switching over to Linux when compared to other systems.  The next step that you should take when it comes to Linux, is to try it out for yourself. You should take some time and try to ensure that you are working on this system, and you can from there, create a great database and environment for your system. It does take a bit of time to learn, and it can be scary, but once you start running your computer on Linux, you will understand why everyone is doing it these days. It is simpler, faster, and overall allows for more options for you to try out, and a lot that you can enjoy with this that it will allow you to try out. It does make a difference when you use this, and you will be happier with this as well.