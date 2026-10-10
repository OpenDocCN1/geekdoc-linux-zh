
# PART I
## Installation and Configuration

- CHAPTER 1 Installing Fedora 9
- CHAPTER 2 Fedora Quick Start 41
- CHAPTER 3 Working with GNOME 53
- CHAPTER 4 Command-Line Quick Start 77

---

# CHAPTER 1
## Installing Fedora

This chapter shows you how to get a basic installation of Fedora up and running. You will learn how to start installation and how to specify certain configuration options during the install. Before you even insert the disc, you'll have a chance to consider choices that will affect how you install Fedora. It is impossible to take you through every single variation of the install, but you will get a step-by-step guide of a typical installation, including how to log in to your new system and shut down or reboot the system.

### Before You Begin the Installation

It can be a big step to wipe off whatever was on your hard drive and replace it with Fedora. Before you even go near the CD/DVD drive, prepare for the installation by researching some basic information about your hardware. In Appendix B, “Installation Resources,” you'll find a useful section on hardware specifications, with a list of hardware devices that you'll probably want. Fortunately, you can now take a test drive with Fedora without ever having to install it to your hard disk, as Fedora has created Live CD spins of the distribution.

### Live CDs

If you've not come across Live CDs, you might be a bit unsure as to what they are. Basically, a Live CD is a single CD that enables you to boot into a fully functional operating system, in this case Fedora. The Live CD stores all the system files on the CD in a compressed format, uncompressing parts of the operating system as needed. The upshot of this is that you can give Fedora a try without having to repartition or otherwise modify your hard drive.

More important, however, the Live CD enables you to test your hardware to make sure that it is compatible with Fedora. When you are happy, you can use the Live CD to give you a base Fedora installation. Just double-click the Install icon on the desktop and follow the installation instructions found later in this chapter. For now, download and burn the Live CD ISO file to a blank CD using your favorite CD-burning application—it will come in handy later!

### Planning Partition Strategies

If you are a diehard Windows user, partitioning is something that might never have entered your mind. But simply, it is the efficient layout of information on your hard drive, and it is certainly worth giving thought ahead of the installation as to how you want to partition your drive.

### What Is a Partition?

> It can be difficult to explain to new users about *partitions*. A useful analogy is of a kitchen, in which there are many different drawers and cupboards. Imagine the kitchen is your hard drive, and the drawers and cupboards are partitions. In one cupboard, you may keep cups, another might hold ingredients, yet another may hold pots and pans. They are all part of the kitchen but have specific roles within the kitchen.
>
> Taking this back to your hard drive, you may have a partition to hold your user information, another partition to hold the files you will use for serving web pages, and another for boot information.

Typically, Fedora creates three partitions on your drive: a `/boot` partition that stores information to help Fedora boot up, a `/` (or root partition) that stores the bulk of your information, and a swap partition that Fedora uses to temporarily store information when your RAM is full. For the majority of people this is fine, and many users go ahead and use the default partition options. However, there may be occasions when you want to store your `/home` directory (which contains your user settings and documents) on a separate partition. This might be the case if you plan on upgrading your distribution fairly often and don't want to lose settings unique to you. You should be mindful of not only the current business requirements, but also any anticipated requirements, especially if you are in a growing company. It can be very painful when you are running out of storage space because you underestimated storage or partitioning requirements.

Knowing how software is allocated on your hard drive for Linux involves knowing how Fedora organizes its *file system*—its layout of directories on storage media. This knowledge can help you make the most out of hard drive space; and in some instances, such as planning to have user directories mounted via NFS or other means, it can help head off data loss, increase security, and accommodate future needs. Create a great system, and you'll be the hero of information services.

To plan the best partitioning scheme, research and know the answers to these questions:

- How much disk space does your system require?
- Do you expect your disk space needs to grow significantly in the future?
- Will the system boot just Fedora, or do you need a dual-boot system?
- How much data will require backup, and what backup system will work best? (See Chapter 13, “Backing Up,” for more information on backing up your system.)

Most new users to Fedora will want to run a dual-boot system, meaning a system that will enable you to boot into Windows and Fedora. To do this, you need to make sure that you have allocated space on your hard drive for Fedora to use during installation. Unfortunately, Anaconda, the Fedora installation program, does not allow you to resize NTFS partitions, so you need to either use a program such as Partition Magic, or, if you don’t want to spend money on an application that you might use only once or twice, download a copy of the Fedora Live CD and use gParted.

gParted is a simple GUI program that allows you to resize your NTFS partition to make room for Fedora. You can find gParted under the Applications, System Tools menu on the Live CD. Its simple interface is shown in Figure 1.1.

![](img/34e72348d53ca54c2a1d9c871316691b_40_0.png)

**FIGURE 1.1** gParted enables you to work with the partitions on your hard drive to make room for Fedora.

To get started, right-click the main Windows partition shown and select Resize/Move to bring up the resizing options, as shown in Figure 1.2 and Figure 1.3.

![](img/34e72348d53ca54c2a1d9c871316691b_41_0.png)

**FIGURE 1.2** Select Resize/Move from the right-click menu to start the resizing process.

In Figure 1.3, you can see that you have the choice to resize the partition so that you have space free at either the beginning or end of the current partition. We strongly recommend that you add the free space following the existing partition, and in Figure 1.3 you can see that we have selected 8000MB as the free space after the existing partition. Alternatively, you can click and drag either side of the partition bar shown to resize the partition accordingly.

![](img/34e72348d53ca54c2a1d9c871316691b_41_1.png)

**FIGURE 1.3** Either enter a value in the Free Space Following field, or click and drag the arrows to either side of the partition bar.

As soon as you are happy, click the Move/Resize button and gParted returns to the main screen, with the pending operation listed in the lower half of the screen, as shown in Figure 1.4. As you are working with file systems, gParted does not make the changes immediately because you may want to carry out other operations on the file system before committing the changes. In this case, however, you just want to resize the disk, so to commit the changes go to Edit, Apply All Operations, or click the Apply button in the toolbar to start the process. gParted asks you whether you are sure, so click Apply only if you are really ready to commit your changes.

![](img/34e72348d53ca54c2a1d9c871316691b_42_0.png)

**FIGURE 1.4** This is the point of no return. After you have clicked Apply, gParted prompts you one last time before it starts to resize your partition.

After a few minutes, gParted completes the operation and returns you to the main screen, as shown in Figure 1.5.

### DVD Installation Jump-Start

To install Fedora from the DVD included with this book, you must have at least a Pentium-class CPU, 800MB hard drive, and 128MB RAM. You need at least 192MB to install with Fedora’s graphical installer. A 10GB hard drive can easily host the entire distribution, leaving about 3GB free for other data. Most modern systems have significantly larger drives, but it is still a good idea to invest in more storage from your local computer store.

To begin the installation, you need to get into your computer’s BIOS to set the boot sequence so that the CD/DVD drive is the first drive that is booted. Insert the DVD into the drive and let the system boot. When the boot: prompt appears, press the Enter key and follow through the various dialog boxes to install Fedora.

**IN THIS CHAPTER**

- Before You Begin the Installation
- Choosing How to Install Fedora
- Step-by-Step Installation
- Logging In and Shutting Down
- Reference
