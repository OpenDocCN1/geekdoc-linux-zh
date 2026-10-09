
some of those books. Those topics have been dropped to make space for FreeBSD-specific material, like ZFS and jails.

Some of these new features are hugely complex. Complete coverage of ZFS would fill entire books—I know, because I've written those books, too. FreeBSD supports a whole bunch of special-purpose filesystems, each incredibly useful to the folks who need them and totally irrelevant to those who don't. Rather than write a monster tome that nobody would actually read, I've elected to cover the material that every FreeBSD sysadmin must know. If you're interested in deeper coverage of a particular topic, it's available.

Some subsystems are undergoing radical revision. I could wait to write this book until every FreeBSD subsystem has a stable interface, but then it would come out about ... never. As I write this, the bhyve developers are actively rototilling their entire configuration system. Given the choice between glossing over a topic and providing flat-out wrong material, I've chosen to skip detail on bhyve. I hope to be able to delete this paragraph before this book goes to press.

I've ruthlessly excised obsolete information from this edition. For example, modern disk drives don't generally have to worry about write caching. If you discover that a piece of advice you remember using doesn't appear in this book, please check FreeBSD's information resources to see whether that advice is still applicable.

## Contents of This Book

Absolute FreeBSD, 3rd Edition contains the following chapters.

### Chapter 1: Getting More Help

This chapter discusses the information resources the FreeBSD Project and its devotees provide for users. No one book can cover everything, but knowing how to use the many FreeBSD resources on the internet helps fill any gaps you find here.

### Chapter 2: Before You Install

Getting FreeBSD installed isn't that hard. Make poor choices during the install, though, and you'll have a system that isn't suited for your needs. The best way to avoid reinstalling is to think about your requirements and make all the decisions beforehand so that the actual install doesn't require any thought.

### Chapter 3: Installing

This chapter gives you an overview of installing FreeBSD using different partitioning schemes and filesystems.

### Chapter 4: Start Me Up! 'The Boot Process

This chapter teaches you about the FreeBSD boot process and how to make your system start, stop, and reboot in different configurations.

### Chapter 5: Read This Before You Break Something Else! (Backup and Recovery)

Here we discuss how to back up your data on both a system-wide and a file-by-file level, and how to make your changes so that they can be easily undone.

### Chapter 6: Kernel Games

This chapter describes configuring the FreeBSD kernel. Unlike some other operating systems, you're expected to tune FreeBSD's kernel to best suit your purposes. This gives you tremendous flexibility and lets you optimize your hardware's potential.

### Chapter 7: The Network

Here we discuss the TCP/IP protocol that underlies the modern internet, both version 4 and version 6.

### Chapter 8: Configuring the Network

FreeBSD doesn't only shuffle packets crazy fast, but it also supports virtual LANs, link aggregation, and more. We'll configure all of that here.

### Chapter 9: Securing Your System

This chapter teaches you how to make your computer resist attackers and intruders.

### Chapter 10: Disks, Partitioning, and GEOM

This chapter covers some of the details of working with hard drives in FreeBSD. Working with modern hardware means understanding multiple partitioning schemes, disk alignment, and FreeBSD’s disk management infrastructure.

### Chapter 11: The Unix File System

UFS has been FreeBSD’s standard filesystem for decades, and the concepts of UFS pervade the whole operating system. Whether you intend to use UFS or not, you must understand its essentials.

### Chapter 12: The Z File System

ZFS is a newer filesystem very popular on larger systems. If you’re managing large amounts of data, you’ll want ZFS.

### Chapter 13: Foreign Filesystems

Every sysadmin needs to mount disks over the network or use ISOs without burning them to CD. This chapter takes you through those duties, as well as introducing FreeBSD-specific filesystems like devfs.

### Chapter 14: Exploring /etc

This chapter describes the many configuration files in FreeBSD and how they operate.

### Chapter 15: Making Your System Useful

Here I describe the packages system that FreeBSD uses to manage add-on software.

### Chapter 16: Customizing Software with Ports

Sometimes the prebuilt packages won’t cover everything you need. You can leverage FreeBSD’s package-building system to create your own software packages, tuned to meet your exact needs.

### Chapter 17: Advanced Software Management

This chapter discusses some of the finer points of running software on FreeBSD systems.

### Chapter 18: Upgrading FreeBSD

This chapter teaches you how to use FreeBSD’s upgrade process. The upgrade system is among the most remarkable and smooth of any operating system.

### Chapter 19: Advanced Security Features

Here we discuss some of the more interesting security features found in FreeBSD.

### Chapter 20: Small System Services

Here we discuss some of the small programs you’ll need to manage in order to use FreeBSD properly.

### Chapter 21: System Performance and Monitoring

This chapter covers some of FreeBSD’s performance-testing and troubleshooting tools and shows you how to interpret the results. We also discuss logging and FreeBSD’s SNMP implementation.

### Chapter 22: Jails

FreeBSD has a process-isolation subsystem, much like Linux and Solaris containers, called *jails*. We’ll cover the jail system and how you can leverage it for system security.

### Chapter 23: The Fringe of FreeBSD

This chapter teaches you some of the more interesting tricks you can do with FreeBSD, such as running systems without disks and with tiny disks, as well as cloud-friendly features, like libxo.

### Chapter 24: Problem Reports and Panics

This chapter teaches you how to deal with those rare occasions when a FreeBSD system fails, how to debug problems, and how to create a useful problem report.

You'll also find an annotated bibliography, an afterword, and a really spiffy professionally prepared index.

Okay, enough introductory stuff. Onward!

## 1

## GETTING MORE HELP

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_69_0.png)

As thick as this book is, it still can’t possibly cover everything you must know about FreeBSD. After all, Unix has been kicking around for close to 50 years, BSD is pushing 40, and FreeBSD is old enough to have its doctorate. Even if you memorize this book, it won’t cover every situation you might encounter. The FreeBSD Project supports a huge variety of information resources, including numerous mailing lists and the FreeBSD website, not to mention the official manual and Handbook. Its users maintain even more documentation on even more sites. The flood of information can be overwhelming in itself, and it can make you want to just email the world and beg for help. But before you send a question to a mailing list or forum, confirm that the information you need isn’t already available.

### Why Not Beg for Help?

FreeBSD provides two popular resources for assistance: mailing lists and forums. Many participants on both are very knowledgeable and can answer questions very quickly. But when you send a question to these community support resources, you’re asking tens of thousands of people all over the world to take a moment to read your message. You’re also asking that one or more of them take the time to help you instead of watching a favorite movie, enjoying dinner with their families, or catching up on sleep. Problems arise when these experts answer the same question 10, 50, or even hundreds of times. They become grumpy. Some get downright tetchy.

What makes matters worse is that many of these same people have spent a great deal of time and effort making the answers to most of these questions available elsewhere. If you make it clear that you’ve already searched the resources and your answer really doesn’t appear therein, you’ll probably receive a polite, helpful answer. If you ask a question that’s already been asked several hundred times, however, the expert on that subject just might snap and go ballistic on you. Do your homework, and chances are you’ll get an answer more quickly than a fresh call for assistance could provide.

### The FreeBSD Attitude

“Homework? What do you mean? Am I back in school? What do you want, burnt offerings on bended knee?” Yes, you are in school. The information technology business is nothing but lifelong, self-guided learning. Get used to it or get out. Burnt offerings, on the other hand, are difficult to transmit via email and aren’t quite so useful today.

Most commercial software conceals its inner workings. The only access you have to them is through the options presented by the vendor. Even if you want to learn how something works, you probably can’t. When something breaks, you have no choice but to call the vendor and grovel for help. Worse, the people paid to help you frequently know little more than you do.

If you’ve never worked with open source software vendors, FreeBSD’s support mechanism might surprise you. There is no toll-free number to call and no vendor to escalate within. No, you may not speak to a manager and for a good reason: you are the manager. Congratulations on your promotion!

### Support Options
