
cal white paper on vPars. and managed the Early Access Program for HP customers on vPars. Through his interactions with customers and HP technologists he is helping to shape the future of partitioning technologies within Hewlett-Packard.

# Conventions Used in the Book

I don't use a lot of complex notations in the book. Here are a few simple conventions I've used to make the examples clear and the text easy to follow:

- **$ and #**
  The **HP-UX** command prompt. Every command issued in the book is preceded by a command prompt. Either one of these two will be used or a system name are usually used as prompts.
- ***italics***
  *Italics* are used for variable values and when referring to functional areas and menu picks in the System Administration Manager (SAM).
- **bold and " "**
  **Bold** text is the information you would type, such as the command you issue after a prompt or the information you type when running a script. Sometimes information you would type is also referred to in the text explaining it, and the typed information may appear in quotes.
- **<---**
  When selections have to be made, this convention indicates the one chosen for the purposes of the example.
- **[ ]**
  Brackets indicate optional items and command descriptions.
- **{ }**
  Curly braces indicate a list from which you must choose.
- **|**
  A vertical bar separates items in a list of choices.
- **<Enter>**
  Indicates that the "Enter" key has been pressed on the keyboard. Sometimes **<Return>** is used to indicate that the return key has been pressed.

One additional convention is that used for command formats. I don't use command formats more than I have to because I could never do as thorough a job describing commands as the HP-UX manual pages. The manual pages go into detail on all HP-UX commands. Here is the format I use when I cover commands:

```
form 1    command [option(s)] [arg(s)]
form 2    command [option(s)] [arg(s)]
form n    command [option(s)] [arg(s)]
```

I try not to get carried away with detail when covering a command, but there are sometimes many components that must be covered in order to understand a command. Here is a brief description of the components listed above:

- **form #** - There are sometimes many forms of a command. If there is more than one form of a command that requires explanation, then I will show more than one form.
- **command** - The name of the executable.
- **option(s)** - Several options may appear across a command line.
- **cmd_arg(s)** - Command arguments such as path name.

## CHAPTER 1
### Installing HP-UX 11i and Virtual Partitions Software

#### Introduction to Virtual Partitions

I want to cover only loading software in this chapter but I can’t do it. Even though loading software is the first step to creating Virtual Partitions (vPars) we’ll have to go over some background in order to understand the concept of vPars and select the devices off which our vPars will boot.

HP-UX Virtual Partitions allow you to run multiple instances of HP-UX on the same HP 9000 server. From a hardware perspective a vPar consists of CPU, memory, and I/O that is a subset of the overall hardware on the computer. From a software perspective a vPar consists of the HP-UX 11i Operating Environment and all application-related software to successfully run your workload. Figure 1-1, which appears in other places throughout this book, shows a conceptual diagram of the way in which HP 9000 computer system resources can be allocated to support multiple vPars.

![](img/eff8b9287a5f38c5adf538f24aacf29e_35_0.png)

The components of which your HP 9000 is comprised can be allocated in a variety of ways. You can see that the eight-way system shown has a different number of processors, different amount of memory, and different number of I/O cards allocated to each vPar. The unused components can be added to any of the vPars or be the basis for yet another vPar. In addition, components can be moved from one vPar to another with some restrictions described later in the book.

In this chapter we’re most concerned about the software included in each vPar. We want to end up with both HP-UX 11i and the Virtual Partitions software on every disk that will host a Virtual Partition. This means that if you have a system on which you want to run two vPars, you’ll have to load all of the software necessary to support completely independent instances of HP-UX 11i. We’ll end up with a system that looks like that shown in Figure 1-2.

![](img/eff8b9287a5f38c5adf538f24aacf29e_36_0.png)

Figure 1-2 Virtual Partitions Software Stack

There are many components in Figure 1-2. Starting from the bottom we have the hardware, firmware, and Virtual Partition Monitor (covered as part of the boot process in Chapter 3.) Next, we move up to the software components, which include HP-UX 11i installed on two different disks. There are two HP-UX 11i instances shown in the leftmost two stacks of Figure 1-2. These operating systems will have to be loaded on every disk that will act as the boot disk of a Virtual Partition.

The Virtual Partition Monitor is a component of the Virtual Partition application. Without this application the two HP-UX 11i instances can't run simultaneously on this system. We cover loading the Virtual Partitions application in this chapter.

Without Virtual Partitions created we can boot HP-UX off one *or* the other of these disks, but we can't run both. Creating our Virtual Partitions is covered in Chapter 2. Once this is done, we can indeed have two instances of HP-UX 11i running simultaneously. After Virtual Partitions have been created, you can proceed to load the middleware and applications shown on top of HP-UX 11i in Figure 1-2.

Although we're covering running multiple instances of HP-UX 11i in the Virtual Partitions we create, we won't be restricted to only HP-UX 11i in the future. On systems based on the Itanium Processor Family (IPF) CPUs we'll be able to run additional operating systems. The rightmost Virtual Partition on Figure 1-2 depicts this future capability. This capability does not exist at the time of this writing, so it is not covered. Look for an updated revision of this book in the future to cover this capability once it exists, and keep an eye on *www.hp.com* for both IPF and Virtual Partition enhancements.

We need to select the devices on which we'll install software before beginning our software load. The next section covers this topic.

#### Selecting the Disks on Which to Load Software

There are some restrictions related to the devices on which we can load the operating system and other software used by Virtual Partitions. You'll want to read two upcoming chapters that cover hardware in detail when you get to the point of creating and working with vPars: Chapter 2 covers working with vPars and Chapter 5 covers vPars and devices. In this section, however, we do need to cover the basics of selecting disks on which to load software so that you meet the restrictions at the time of this writing and load the software on disks that meet the requirements of vPars.

Let's take a look at an **ioscan** output that shows the disks on a system (**ioscan** and issues related to hardware and vPars in general are covered in detail in Chapters 2 and 5 as mentioned earlier.)

At the time of this writing, components that are at or below the Local Bus Adapter (LBA) level are devoted to a partition. This means that the disks on which you load the software for two different vPars must be on two different LBAs. Let’s take a brief look at the LBAs and disks on a system in order to select the disks on which we’ll load software. If you need more detail than is covered here, please refer to the chapters that cover this topic in more detail. Also please keep in mind that the layout of systems varies depending on the model and that you need to become familiar with the layout of your system to the extent that you can determine the location of components in your system relative to the LBA level.

Let’s take a look at an L-Class system to view the System Bus Adapter (SBA) and multiple LBAs.

```bash
cvhdcon3:/ # ioscan -f | grep ba

# L-Class
ica   0  0       sba
ba    0  0/0     l4k     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (783)
ba    1  0/1     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    2  0/2     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    3  0/3     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    4  0/4     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    5  0/5     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    6  0/6     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    7  0/9     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    8  0/10    lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    9  0/12    lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
cvhdcon3:/ #
```

This L-Class has only one SBA, as indicated by the leading 0 on all of the buses in the previous listing, and it has two SCSI buses on LBA 0.0. The internal disks are normally mirrored across these two different SCSI buses. There are then many additional LBAs. Let’s now see which disks are connected to this system and determine with what LBA they are associated.

```bash
cvhdcon3:/ # ioscan -f | grep disk
disk  0  0.0/1.0.1.0.0      mdisk CLAIMED DEVICE HP DVD-ROM 304
mdisk 1  0.0/1.1.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
mdisk 2  0.0/1.2.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
mdisk 3  0.0/2.0.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
mdisk 4  0.0/2.0.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
disk  7  0.0/0.0.8.0.5.0.0 sdisk CLAIMED DEVICE HP AS277A
disk 10 0.0/0.0.8.0.5.0.0.1 sdisk CLAIMED DEVICE HP AS277A
disk 11 0.0/0.0.8.0.5.0.0.2 sdisk CLAIMED DEVICE HP AS277A
disk 12 0.0/0.0.8.0.5.0.0.3 sdisk CLAIMED DEVICE HP AS277A
disk 15 0.0/0.0.8.0.5.0.0.3 sdisk CLAIMED DEVICE HP AS277A
disk 17 0.0/0.0.8.0.5.0.2.0 sdisk CLAIMED DEVICE HP AS277A
```
