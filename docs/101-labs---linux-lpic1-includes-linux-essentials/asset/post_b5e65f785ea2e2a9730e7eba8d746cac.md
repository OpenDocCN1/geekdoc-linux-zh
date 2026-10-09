
## 101 LABS-LINUX LPIC-1: SYSTEM ADMINISTRATOR

- L PIC1 Linux Administrator-Exam 102
- Lab 64 Customize and Use the Shell Environment: User Profiles
- Lab 65 Customize and Use the Shell Environment: Aliases and Functions
- Lab 66 Customize or Write Simple Scripts: Standard Syntax
- Lab 67 Customize or Write Simple Scripts: Miscellaneous Tools
- Lab 68 Customize or Write Simple Scripts: Scripting Practice
- Lab 69 Install and Configure X11
- Lab 70 Graphical Desktops
- Lab 71 Accessibility
- Lab 72 Manage User and Group Accounts and Related System Files: Users
- Lab 73 Manage User and Group Accounts and Related System Files: Groups
- Lab 74 Manage User and Group Accounts and Related System Files: Special Purpose Accounts
- Lab 75 Automate System Administration Tasks by Scheduling Jobs: Cron
- Lab 76 Automate System Administration Tasks by Scheduling Jobs: At and Systemd
- Lab 77 Localization and Internationalization: Timezones
- Lab 78 Localisation and Internationalisation: Locales
- Lab 79 Maintain System Time: NTP
- Lab 80 Maintain System Time: Chrony
- Lab 81 System Logging: Rsyslog
- Lab 82 System Logging: Logrotate
- Lab 83 System Logging: Journald
- Lab 84 Mail Transfer Agent (MTA) Basics: Aliases and Forwarding
- Lab 85 Mail Transfer Agent (MTA) Basics: Other MTA's
- Lab 86 Manage Printers and Printing
- Lab 87 Fundamentals of Internet Protocols: Ports and Services
- Lab 88 Fundamentals of Internet Protocols: Subnetting
- Lab 89 Fundamentals of Internet Protocols: IPv4 and IPv6
- Lab 90 Persistent Network Configuration: Network Configuration
- Lab 91 Persistent Network Configuration: NetworkManager
- Lab 92 Basic Network Troubleshooting: Modern Tools
- Lab 93 Basic Network Troubleshooting: Legacy Tools
- Lab 94 Configure Client-Side DNS: dnutil
- Lab 95 Configure Client-Side DNS: systemd-resolved
- Lab 96 Perform Security Administration Tasks: User Auditing
- Lab 97 Perform Security Administration Tasks: System Auditing
- Lab 98 Setup Host Security: User Security. 241
- Lab 99 Setup Host Security: Network Services. 243
- Lab 100 Securing Data with Encryption: SSH. 245
- Lab 101 Securing Data with Encryption: GPG. 247

### # Introduction 101 Labs

Welcome to your 101 Labs book.

When I started teaching IT courses back in 2002, I was shocked to discover that most training manuals were almost exclusively dedicated to theoretical knowledge. Apart from a few examples of commands to use or configuration guidelines, you were left to plough through without ever knowing how to apply what you learned to live equipment or to the real world.

Fast forward 17 years and little has changed. I still wonder how, when around 50% of your exam marks are based on hands-on skills and knowledge, most books give little or no regard to equipping you with the skills you need to both pass the exam and then make money in your chosen career as a network, security, or cloud engineer (or whichever career path you choose).

101 Labs is NOT a theory book: it's here to transform what you have learned in your study guides into valuable skills you will be using from day one on your job as a network engineer. We don't teach DHCP, for example; instead, we show you how to configure a DHCP server, which addresses you shouldn't use, and which parameters you can allocate to hosts. If the protocol isn't working, we show you what the probable cause is. Sound useful? We certainly hope so.

We choose the most relevant parts of the exam syllabus and use free software or free trials (whenever possible) to walk you through configuration and troubleshooting commands step by step. As your confidence grows, we increase the difficulty level. If you want to be an exceptional network engineer, you can make your own labs up, add other technologies, try to break them, fix them, and do it all over again.

–Paul Browning

## 101 LABS–LINUX LPIC-1: SYSTEM ADMINISTRATOR

This book is designed to cement the theory you have read in your Linux LPIC-1 study guide or video training course. If you haven’t studied any theory yet, then please check out our website https://www.howtonetwork.com, which also features practice exams.

The goal of this book is to dramatically improve your hands-on skills and speed, enabling you to succeed in the practical portions of the Linux LPIC exams and also to transfer your skills to the real world as a Linux network engineer. We don’t have space here to cover theory at all, so please refer to your Linux LPIC study guide to get a good understanding of the learning points behind each lab. Every lab is designed to cover a particular theoretical issue, such as the configuration requirements of fdisk.

If you want to become Linux LPIC-1 certified, you must pass two exams:

- 101-500
- 102-500

The book actually starts with the Linux Essentials syllabus for labs 1 through 25. If you wish to take this certification you can book the exam:

- 010-160

Please visit the LPIC website for information about the exam topics and booking details:
https://www.lpic.org

We’ve done our best to hit every syllabus topic mentioned in the exam syllabus on the Linux Professional Institute website. Please do check the syllabus on their website which may change. Their website also gives more details on the weighting given each subject area.

It’s also worth noting that once we show you how to configure a certain service or protocol a few times, we stop walking you through the steps in subsequent labs—to save valuable space. Anyway, you can always flick back a few pages to see how it’s done.

We’ve done our best to keep the topology as simple as possible, for this reason, almost all labs have been configured on a Ubuntu installation running on a virtual machine (with internet access). Please do check out our resources page, which will cover any additional information you need: https://www.101labs.com/resources

## DOING THE LABS

Apart from a couple of research labs at the start, all of the labs are hands-on. They have been checked by several students as well as a senior Linux consultant so should be error-free. Bear in mind that each machine will differ so your output will differ from ours in many instances. If you use a distro other than Ubuntu 18.04 then your results will differ from ours significantly.

If you get stuck or things aren't working, we recommend you take a break and come back to the lab later with a clear mind. There are many Linux support forums out there where you can ask questions, and if you are a member of 101labs.net you can post on our forum, of course.

Best of luck with your studies.

–Paul Browning, CCNP, MCSE

## 101 LABS–LINUX LPIC1 VIDEO COURSE

Each 101 Labs book has an associated video training course. You can watch the instructor configure each lab and talk you through the entire process step by step as well as share helpful tips for the real world of IT. Each course also has 200 exam-style questions to prepare you for the real thing. It's certainly not necessary to take use this resource, but if you do, please use the coupon code ‘101lpic’ at the checkout page to get a big discount as a thank you for buying this book. https://www.101labs.net

## INSTRUCTIONS

- 1.  Please follow the labs from start to finish. If you get stuck, do the next lab and come back to the problem lab later. There is a good chance you will work out the solution as you gain confidence and experience in configuring the software and using the commands.
- 2.  You can take the labs in any order, but we've done our best to build up your skill level as you go along. For best results, do ALL the labs several times over before attempting the exam.
- 3.  There are resources at www.101labs.net/resources.
- 4.  Please DO NOT configure these labs on a live network or on equipment belonging to private companies or individuals.
