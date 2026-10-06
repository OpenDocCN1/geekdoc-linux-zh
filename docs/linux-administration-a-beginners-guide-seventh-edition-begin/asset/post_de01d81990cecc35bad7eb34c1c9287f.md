
# PART VI

# Appendixes

# A Creating a Linux Installer on Flash/USB Devices . . . 773

+   Creating a Linux Installer on . . . . . . . . . . 774
Flash/USB Devices (via Linux OS) . . . . . . . . . . 774
Creating a Linux Installer on Flash/ . . . . . . . 776
USB Devices (via Microsoft Windows) . . . . . . . 776
Fedora Installer Using Live USB Creator on Windows . . 777
Ubuntu Installer Using Unetbootin on Windows . . . . . . 779
OpenSUSE Installer Using Pendrivelinux.com's . . . 779
Universal USB Installer on Windows . . . . . . . 781

# B Demo Virtual Machine . . . . . . . . . . 785

+   Basic Host System Requirements . . . . . . . . . . 787
Installing the Virtualization Applications and Utilities 788
Download and Prep the Demo VM Image File . . . . . . 789
Import the Demo VM Image and . . . . . . . . . . . 791
Create a New VM Instance . . . . . . . . . . . . 791
Managing the Demo Virtual Machine . . . . . . . . . . 791
Connecting to the Demo VM . . . . . . . . . . . 794
Virtual Network Computing (VNC) . . . . . . . . . . 794
Connecting via SSH . . . . . . . . . . . . 796
Virtual Serial TTY Console . . . . . . . . . . . 797
Cockpit Application . . . . . . . . . . . . 798
Just Use It! . . . . . . . . . . . . . . . . . 801
Feedback . . . . . . . . . . . . . . . . . . 802

# Index . . . . . . . . . . . . 803

# Introduction

On October 5, 1991, Linus Torvalds posted this message to the news-group comp.os.minix:

Do you pine for the nice days of minix-1.1, when we were men and wrote their own device drivers? Are you without a project and just dying to cut your teeth on an OS can you try to modify for your needs? Are you finding everything works on minix? No more all-nighters to get a nifty program working? Then this post might be just for you :-)

Linux went on to introduce the first cut of Linux to the world. Unbeknown to him, he had unleashed what was to become one of the world's most popular and disruptive operating systems. More than 24 years later, an entire industry has grown up around Linux. And, chances, you've probably used it (or benefited from it) in one form or another!

# Who Should Read This Book

A part of this book reads "A Beginner's Linux Guide"; this is mostly apt. But what the title should say is "A Beginner to Linux Administration Guide," because we do a few assumptions about you, the reader. (and we jolly well couldn't use that title because it was such a mouthful and not sexy enough.) We assume that you are already familiar with Windows servers (or other operating systems, but we'll assume Windows for the sake of discussion) at a "power user" level or better. We assume that you are familiar with the terms (and some concepts) necessary to run a small- to medium-sized network of computers. Any experience with bigger networks or advanced Windows technologies, such as Active Directory, will allow you to get more from the book but is not required.

# XXVI Linux Administration: A Beginner's Guide

We make these assumptions because we did not want to write a guide for dummies. There are already enough books in the market that tell you what to do without telling why; this book is not meant to be among those ranks.

In addition to your Windows background, we assume that you are interested in having more information about the topics here than the material we have written online. After all, we've spent only 30 to 35 pages on topics that have entire books devoted to them! For this reason, we have scattered references to other resources throughout the chapters. We urge you to take advantage of these recommendations.

We believe that seasoned Linux system administrators can also benefit from this book because it can serve as a quick-cookbook on various topics that might not be the seasoned's strong points. We understand that system administrators have aspects of system administration that they like or love a lot. For example, making backups is not one of our favorite aspects of system administration, and this is reflected in the half page we've dedicated to backups. (Just kidding, there's an entire chapter on the topic.)

## What’s in This Book?

Linux Administration: A Beginner's Guide, Seventh Edition comprises six parts.

## Part I: Introduction, Installation, and Software Management

Part I includes four chapters (Chapter 1, “Technical Summary of Linux Distributions”; Chapter 2, “Installing Linux in a Server Configuration”; Chapter 3, “The Command Line”; and Chapter 4, “Managing Software”). The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

# XXVI Linux Administration: A Beginner's Guide

We make these assumptions because we did not want to write a guide for dummies. There are already enough books in the market that tell you what to do without telling why; this book is not meant to be among those ranks.

In addition to your Windows background, we assume that you are interested in having more information about the topics here than the material we have written online. After all, we've spent only 30 to 35 pages on topics that have entire books devoted to them! For this reason, we have scattered references to other resources throughout the chapters. We urge you to take advantage of these recommendations.

We believe that seasoned Linux system administrators can also benefit from this book because it can serve as a quick-cookbook on various topics that might not be the seasoned's strong points. We understand that system administrators have aspects of system administration that they like or love a lot. For example, making backups is not one of our favorite aspects of system administration, and this is reflected in the half page we've dedicated to backups. (Just kidding, there's an entire chapter on the topic.)

## What’s in This Book?

Linux Administration: A Beginner's Guide, Seventh Edition comprises six parts.

## Part I: Introduction, Installation, and Software Management

Part I includes four chapters (Chapter 1, “Technical Summary of Linux Distributions”; Chapter 2, “Installing Linux in a Server Configuration”; Chapter 3, “The Command Line”; and Chapter 4, “Managing Software”). The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

Chapter 3, “The Command Line,” begins covering the basics of working with the Linux command-line interface (CLI) so that you can become comfortable working without a GUI. The first two chapters provide you with a nice overview of what Linux is, how it compares to Windows in several key areas, and how to install server-grade Fedora and Ubuntu distributions.

# Introduction

# Part II
Part II covers the material necessary to manage what we call “stand-alone” system, a system that does not require any services to other systems. Although the notion of a server seem counterintuitive, it is the foundation on which many concepts are built, and it will come in hand on the network.

Part II comprises six chapters. Chapter 5, “Managing Users and Groups,” covers the basics of user and group concepts on Linux, as well as day-to-day management of adding and removing users. The chapter also introduces the basics of multiuser operation and the Linux permissions. (Wait, I missed a line: The chapter also introduces the basics of multiuser operation and the Linux permissions.)

Chapter 6, “Booting and Shutting Down,” covers the entire booting and shutting processes. This chapter includes details on how to start services manually, which will also come in hand on the book.

The basics of operation continue in Chapter 7, “File Systems,” continues with the basics of file systems—their organization, creation, and most importantly, their management.

The basics of operation continue in Chapter 8, “Core Systems,” with coverage of basic tools such as xinet, upstart, rslog, cron, systemd, journal, and so. systemd is the Linux equivalent of svhost, and rslog manages logging for all applications in a unique framework.

Chapter 9, “The Linux Kernel,” documents the process of configuring, compiling, and installing your custom kernel in Linux. This capability is one of the points that gives Linux administrators an extraordinary amount of fine-grained control over their operating systems.

Chapter 10, “Knocks and Dials: Virtual File Systems,” covers some kernel-level tweaking through /proc and /sys. The ability to view and modify certain kernel-level configuration and runtime variables through /proc and /sys, as shown in this chapter, gives administrators almost infinite kernel-tuning possibilities. When applied properly, this ability amounts to an arguably better and easier way to tweak the kernel than afforded by Windows.

# Part III: Networking and Security

Part III begins our journey into the world of networking and security. We are not quite sure why we combined these two things under the same part, but if forced to justify this, we would say that “the network is the root of most evils and therefore it needs to be secured.” Moving right along; with the ongoing importance of security on the Internet, as well as compliance issues with Sarbanes-Oxley (SOX) and the Health Insurance Portability and Accountability Act (HIPAA), the use of Linux in scenarios that require high security is unprecedented.

![](img/9f6657924397c33f088db5321b751a83_22_0.png)
