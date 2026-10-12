
Network connectivity, including sharing folders and securing the network
Internet connectivity via dial-up and broadband connections

Part IV, “Fedora As a Server,” looks at the opportunities provided by every Fedora system by covering

- Building and deploying web servers
- Database creation, management, and manipulation
- File and print servers
- Using FTP for serving files across the Internet and local networks
- Building and deploying email servers using Postfix as well as managing mailing lists
- Creating remote access gateways and services
- Configuring DNS for your network
- Using LDAP for storing information on users and security
- Configuring a local news server

Part V, “Programming Linux,” provides a great introduction into ways in which you can extend Fedora’s capabilities even further using the development tools supplied with it. This part covers

- Programming in Perl, using variables and scripting
- An introduction to the Python language
- Writing PHP scripts and linking them to databases
- C and C++ programming tools available with Fedora, and how to use the GNU C Compiler (gcc)

Part VI, “Fedora Housekeeping,” looks at some of the more advanced skills you need to keep your system running in perfect condition, including

- Securing your machine against attack from outsiders and viruses
- Performance tuning
- Command-line masterclass
- Advanced yum
- Kernel and module management and compilation
- Managing the file system

There is also an extensive reference in Part VII, “Appendix,” which gives you scope to explore in even more depth some of the topics covered in this book.

## Conventions Used in This Book

A lot of documentation is included with every Linux distribution, and Fedora Core is certainly no exception. Although the intent of Red Hat Fedora 4 Unleashed is to be as complete as possible, it is impossible to cover every option of every command included in the distribution. However, this book offers numerous tables of various options, commands, or keystrokes to help condense, organize, and present information about a variety of subjects.

This edition is also packed full of screenshots to illustrate nearly all Fedora-specific graphical utilities—especially those related to system administration or the configuration and administration of various system and network services.

To help you better understand code listing examples and sample command lines, several formatting techniques are used to show input and ownership. For example, if the command or code listing example shows typed input, the input is formatted in boldface like this:

```
$ ls
```

If typed input is required, as in response to a prompt, the example typed input also is in boldface, like so:

```
Delete files? [Y/n] y
```

All statements, variables, and text that should appear on your display use the same boldface formatting. Additionally, command lines that require root or superuser access are prefaced with a pound sign like this:

```
# printool &
```

Command-line examples that can be run by any user are prefaced with a dollar sign ($), like so:

```
$ ls
```

The following elements provide you with useful tidbits of information that relate to the discussion of the text:

> **NOTE**
> Notes provide additional information you might want to make note of as you are working; augment a discussion with ancillary details; or point you to an article, a whitepaper, or another online reference for more information about a specific topic.

> **TIP**
> A tip can contain special insight or a timesaving technique, as well as information about items of particular interest to you that you might not find elsewhere.

> **CAUTION**
> A caution warns you about pitfalls or problems before you run a command, edit a configuration file, or choose a setting when administering your system.

### Sidebars Can Be Goldmines

Just because it is in a sidebar doesn't mean that you won't find something new here. Be sure to watch for these elements that bring in outside content that is an aside to the discussion in the text. You will read about other technologies, Linux-based hardware, or special procedures to make your system more robust and efficient.

Other formatting techniques used to increase readability include the use of *italics* for placeholders in computer command syntax. Computer terms or concepts also are *italicized* upon first introduction in text.

Finally, you should know that all text, sample code, and screenshots in *Red Hat Fedora 4 Unleashed* were developed using Fedora and open-source tools.

Read on to start learning about and using the latest version of Fedora Core. Experienced users will want to consider the new information presented in this edition when planning or considering upgrades. New users, or users new to Fedora, will benefit from the details presented in this book.

## PART I
## Installation and Configuration

### IN THIS PART

- CHAPTER 1 Introducing Fedora 13
- CHAPTER 2 Preparing to Install Fedora 27
- CHAPTER 3 Installing Fedora 53
- CHAPTER 4 Post-Installation Configuration 81
- CHAPTER 5 First Steps with Fedora 117

## CHAPTER 1
## Introducing Fedora

Welcome to Red Hat Fedora 4 Unleashed! Fedora Core is a unique Linux distribution and is the first and primary product of The Fedora Project, an open-source, community-driven project sponsored by Red Hat. Fedora Core, or more simply, Fedora, is a base Linux distribution available free over the Internet at http://fedora.redhat.com. Alternatively, places like linuxcentral.com or even your local Linux user group can supply you with a copy if you don't have a good Internet connection.

Fedora represents an evolution in the business direction of its sponsor, Red Hat. For nearly 10 years, Red Hat provided copies of its commercial Linux distribution, Red Hat Linux, free over the Internet. All that changed in October 2003, when Red Hat discontinued the sale and free distribution of its consumer-oriented Red Hat Linux.

As the company has since its inception, Red Hat then released all its work on the freely licensed software in the former consumer distribution. The work, which was to be a new version of Red Hat Linux, was then merged with an existing Fedora Linux project and was reborn as Fedora Core. Red Hat now focuses its efforts on enterprise and corporate Linux-based products and services, but again, continues to make source code available for all its products that are under an open-source license.

Red Hat's Enterprise Linux is a series of software products aimed for corporate and enterprise migration, deployment, and use. Although all Linux distributions could be considered the same underneath because all use the Linux kernel, Red Hat takes special pains to create, test, sell, and support commercial Linux distributions optimized for deployment on multiple hardware and CPU architectures. These high-performance enhancements include hardware-tweaked Linux kernels, fail-over and load-balancing clustering, and integrated Java support—essential for mission-critical applications and production environments.

### IN THIS CHAPTER

- What Is Fedora Core?
- Fedora for Business
- Fedora in Your Home
- 64-bit Fedora
- Getting the Most from Fedora and Linux Documentation
- Fedora Developers and Documentation
- Reference

## About Red Hat

Red Hat is one of the world's foremost open-source development houses and retransforms nearly all its development efforts back to the Linux development community.

The company has been involved in many open-source and GNU GPL projects, such as the Apache web server, the glibc software libraries, the GNU Network Object Model Environment (GNOME), various GNU software tools and packages, the Linux kernel and device drivers, the PostgreSQL database system, and the Red Hat Package Manager (RPM).

Red Hat also supports many other projects by providing FTP service and web hosting and is one of the few companies actively promoting and using the open source business development model. This means that, although many of its products are free, revenue streams are derived from spin-off and related technologies and services. These pursuits include embedded development (the open-source eCOS operating system); training and certification programs such as the Red Hat Certified Engineer (RHCE) track; commercial software development; fee- and subscription-based support; consulting; and advanced software products, such as an advanced e-commerce platform, a secure web server, a credit card verification system (CCVS), and the Red Hat Database.

One possible reason for the success of Linux could be "Best hack wins." In other words, software that works well, fills a critical need, is readily available in source form, and is distributed under a free software license (such as the GNU GPL) will quickly spread and see extensive use. The growth in popularity and widespread adoption of Linux around the world is a testament to quality, licensing, and need for Linux.

Unix enjoyed a similar rapid-fire adoption after it was distributed in the early 1970s and fulfilled user needs on a number of fronts. However, its licensing was restrictive, caused much grief in some open-source communities (such as education), and continues to spawn problems to this day.

Here is the bottom line: You are holding nearly $1 billion worth of software in your hands. That is one estimate of what it would cost to develop as complete an operating system, graphical interface, and related software to equal the operating system included with this book.

It was not long ago that any new major project involving use of Linux by big business, government (on any level), or academia would have been big news. Today, Linux is increasingly used by IS/IT strategists for computing solutions. Linux and related open-source software rule the Internet. It is the host platform of choice for traditional server operations. Linux is poised to take over the desktop, occupying the number two spot behind a monolithic software entity.

> **NOTE**
> The list of Linux projects, efforts, and partnerships reads like a Who's Who of the software industry: Amazon, Ameritrade, Borland, Computer Associates, Dell, Hewlett-Packard/Compaq,
