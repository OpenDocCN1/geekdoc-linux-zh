
**Availability:** Downloads of ISO images are available, and CDs can be purchased online from SUSE. Boxed editions also are available from third-party vendors.

**Cost:** Free to download images, $29–$89 for CDs.

## Xandros

Xandros started out as a commercial distribution but now has a limited, ad-supported version available for free download. This distro is a fairly new player (although the base development came from the old Corel Linux) and has gotten some popularity and press for its good usability.

**Install:** Installation is easy to zip through, with GUI screens and lots of choices suggested for you.

**Pros:** Like Linspire, Xandros works right out of the box. The distro shows the work that has gone into it with an array of tightly integrated utilities that are stable.

**Cons:** A limited number of applications are included. Some proprietary programs mean that you will have to wait for the company’s next release if you want those updated. Linux users are used to a little more flexibility than that. The only free version is ad supported. Support will have to come more from the company than from other users.

**Availability:** Download or buy from Xandros.

**Cost:** Free ad-supported download version, or $49–$99 for commercial versions.

## Yellow Dog

For years, Yellow Dog was the classic choice to run Linux on a Mac. The distro isn’t horribly innovative. Yellow Dog is essentially a direct port-over of the last Fedora version available, with certain conventions and tools of its own thrown in.

**Install:** Yellow Dog uses Fedora’s Anaconda installer, so the install is just as easy as Fedora. The installer also keeps its core concept of Apple users in mind, with a good selection of Apple hardware choices.

**Pros:** Yellow Dog is RPM based and also has Apt and Yum versions (update tools) available. Many of the utilities are ports from Fedora, so you will find that much of the online help from users applies to both distros. The company also maintains a good support mail list with archives.

**Cons:** Anytime you are using Linux on PPC, you will have more trouble finding compiled packages. Apt and Yum are available, but you are limited to only a few repositories. Some of the tools feel a little clunkier than they do on Fedora, but the tools are there and do work.

**Availability:** Yellow Dog has downloads of ISO images on mirror sites and CDs available for purchase. Boxed editions also are available from third-party vendors.

**Cost:** Free download of ISOs, $25–$85 for disks, depending on what version you want.

I concentrate on Fedora (Core 2) and Mandrake (10.0) throughout the rest of this book. I think that these two distros are the easiest for someone new to Linux to install, set up, and use. It also is very easy to find software packages already compiled for both. When you get used to a few of the conventions of the Linux world, that is the time for you to explore. In Mandrake and Fedora, you will find that the desktop environment and programs you use are mostly the same between distributions. The installation and system tools differ.

Deserving special mention is the next most popular choice among Linux users, SUSE (see Figure 1.2). SUSE is another distro that can be quite easy for new users, especially those switching from Windows. Utilities and system tools are intelligently arranged and easy to find in the menus. The distribution is RPM based, making installing new software uncomplicated for new users. If you opt to buy a boxed edition of Linux, SUSE has some of the best, most complete manuals included.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_34_0.png)

**Figure 1.2** The SUSE desktop after first login.

One of the most interesting newer choices on the distro front that also deserves special mention is Gentoo. Gentoo is a distribution for which the installation is longer than a bad TV miniseries, but the OS and the programs are compiled for your machine. Gentoo has an active community of users who are ferociously loyal to their distribution. Later, if you start to feel like you have run out of Linux challenges, Gentoo might be a fun toy to poke around with.

**BUY ME**

*HP has now released a native Linux notebook computer that runs SUSE. Laptops are infamously complex to set up Linux on because of the special little buttons and weird hardware on them. With a native Linux laptop, HP takes care of all that for you.*

## UNDER THE HOOD

There are many Linux distributions out now, and most of those distros offer a similar set of features. A patient new user could figure out even the most technical of distributions. The difference between Linux on the desktop now and Linux on the desktop two years ago is astounding. Each of the major distros contributes innovations that get worked into new versions of other distros. That's the character and power of Linux, the ability to share new ideas to benefit all and present choice for users.

Right now, you're the newbie. You've got to pick something. Fedora and Mandrake have simplified the installation, choices, tools, and utilities to be quite user friendly. You might even find some things easier in these distros than in your old OS. We will move forward with Fedora and Mandrake. In exploring these two distributions, you can learn most of the basic concepts of Linux that will make trying out new distributions painless.

## Burning Disk Images

You need to create installation disks if you have downloaded the disk image files from the Internet. If you buy a Linux distribution or try out Linux with a live CD version, you don't have to burn any disks.

When you download a Linux distribution, you need to know what to do with those giant files that you now have sitting on your computer. Those files that you downloaded are disk images, usually ISOs. An ISO contains all of the files needed for the CD that you will create. You might have three or four of those giant files. Most Linux distributions are multi-disk sets. Each disk image that you download is probably going to be larger than 600MB. Depending on your current operating system, the ISO files might look like archives to you. Don't unpack the archive and burn a disk as you normally would; burning a disk image is different than burning a data or music disk.

Fedora now also makes a DVD version of the distribution available for download. With the DVD disk image, you have fewer disks to burn. If you have a DVD burner available and you like playing with new toys, give it a try. The steps for burning DVD images might vary in Windows, depending on your software. The steps for burning a DVD disk image are the same in Mac OS X for anyone using Disk Utility.

### Burning Disk Images in Windows

Most common CD-burning programs in Windows have an option in the main window that says something like Burn Disk Image. If your program has that option, you are probably all set.

You can find a number of CD-burning software programs for Windows, and most have a help menu that will point you in the right direction.

### Burning Disk Images in Mac OS X

Whereas OS X makes burning music and data disks very easy, burning images is a little more complex. You can get a few third-party applications for burning disks on a Mac. Some of those programs make the job a little easier by putting all of the commands and utilities you need in one place. If you grab one of those programs, just follow the instructions that come with your software.

If you want to burn your disk images through OS X, you need to open Disk Utility. From a Finder window, simply drag each downloaded disk image file into the left column of Disk Utility. The Burn button on the toolbar should then be available. You can insert a blank CD or DVD and then choose *Burn*.

# Dual-Booting

## What Is Dual-Booting?

Dual-booting is the term commonly used when installing two separate operating systems on the same computer. You can partition a single drive with one operating system on each, use one hard drive for each operating system, or spread things out among a few drives. For example, you could dual-boot Linux and Windows or Linux and Mac OS.

Here is how dual-booting works. Your hard drive has on it what is called the Master Boot Record (MBR). The Master Boot Record is located in the first sector of your hard disk. The record contains your partition table as well as information to identify where and how your operating system will boot. Normally, with one operating system, the MBR just shoots right into the OS that you have on your hard disk. However, when you are dual-booting, the MBR first makes a stop at a program called a boot loader. The boot loader gives you a menu of choices so that you can choose which of the operating systems on your hard disk you want to boot into. If you make no choice, the default choice is chosen automatically after a set number of seconds. The labels for the operating systems, which one is the default, and how many seconds to wait are all configurable.

## Why Dual-Boot?

A good portion of the rest of the world is using other operating systems, mostly Windows and Mac OS. Those people will send you files, design Web sites,
