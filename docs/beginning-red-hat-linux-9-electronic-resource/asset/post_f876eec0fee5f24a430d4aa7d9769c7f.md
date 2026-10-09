
## Introduction

![Introduction Image](img/b852150740856958b10aff9e8c9d2adc_20_0.png)

## Installing Red Hat Linux 9

Installing an operating system is often a long, drawn-out process that requires a lot of upfront planning. Installation of traditional Unix-based operating systems seems to have been particularly painful in the past, requiring even experienced administrators to fret about partitions and drivers. Early versions of Linux were no different in this respect. The first version of Linux, back in 1993, could be booted up only using Minix (another Unix-like operating system). That version of Linux could support only the Finnish keyboard because the author of Linux didn't have access to a US keyboard!

However, since then Linux has grown by leaps and bounds. Each of the major distributions has put a lot of thought and effort into the Linux installation process, and today installing Linux for desktop use is, in common talk, a no-brainer.

Red Hat, in particular, has caught the attention of the public, breaking away from the standard tradition of distributing disk images and pioneering the concept of distributing software in the form of packages. (Right now, the Red Hat Package Manager – RPM – is a standard in distribution of pre-compiled software packages in the Linux world, and we'll learn more about the RPM in Chapter 4.)

Red Hat has also been improving Linux usability and features in that most daunting area of any operating system – installation. The latest version of Red Hat Linux, version 9, is truly the most user-friendly ever, with extensive inputs from professional usability experts and a ravishing new look to attract even the most hardened of technophobes.

The Red Hat Linux distribution offers four different configurations, and your choice will depend on how you plan to use the operating system:

- **Personal desktop**: This configuration is targeted at users who are new to Linux, or those who like to use Linux for day-to-day applications like office productivity tools and Internet browsing. This is the option we'll install in this chapter.
- **Workstation**: This configuration is targeted at developers or system administrators. It provides various tools for software development and system management.
- **Server**: This configuration is mainly intended for systems that will not be used directly, but are primarily for offering network-based services like e-mail, file sharing, network connectivity, and web resources.
- **Custom**: This configuration is for experienced users who want more control over exactly what is installed onto their systems. The user can select which packages are to be installed and how the hard disks are to be used, and has control over various other configuration options that are pre-selected in the other three configurations.

In this chapter, we are going to take a look at getting a Personal Desktop installation in place on a new computer. We are going to look at each step of the installation and the decisions that you would have to take at various stages of the installation to get a working Red Hat desktop in place. By the end of the chapter, you will have a desktop up and running that you will be able to use right away for your daily needs like Internet browsing, e-mail, and office productivity tools.

## Preparing for the Installation

While the installation process is quite straightforward, it is important that you do a little bit of preparation to ensure that the installation process goes as intended. Of course, you'll need the necessary installation disks to install the system; but it’s also worth looking over your hardware too. In this section, we'll examine both software and hardware aspects of preparation.

### The Software

Of course, to begin you need to have the necessary **software** for the job. The Red Hat Linux 9 distribution can be obtained from a number of sources. Here are a couple of options:

- **The Publisher’s Edition CD set included with this book**. This includes all the CDs that you need for the installation process itself. In this chapter, we’ll look at installation using the CDs that are included in this pack.
- **The official retail box set.** This includes all the CDs that you need for the installation process itself. It also includes other CDs that contain the source code for all the packaged software, and a CD that contains Red Hat-supplied documentation. Much of the software on these disks can be freely copied and distributed, but only the customer who bought the CD is entitled to official technical support from Red Hat. The box set also includes an array of bonus software packaged by Red Hat, as well as some proprietary software that may not be freely distributed.
- **The downloadable CD images**. In the true spirit of Open Source (http://www.opensource.org), Red Hat also makes all the installation CDs downloadable for free public use. While the contents of the downloadable CD images are identical to those in the official box set, users of these CD images are not entitled to official technical support from Red Hat.

These CD images can be obtained from any of Red Hat's various mirror web sites. You can find a list of mirror FTP and HTTP sites at http://www.redhat.com/download/mirror.html. Alternatively, you can obtain the CD images from VA Linux's extensive Sourceforge download mirror servers, at http://download.sourceforge.net/pub/mirrors/redhat.

When you have the CD images, you can write them onto CD recordable disks (be sure to tell your CD-burning software that you're burning CD images), and then you can use the CDs for installation.

The Personal Desktop configuration of Red Hat Linux that is downloaded or in the boxed set requires all three binary installation CD disks during the installation. Moreover, as you begin to explore some of the many applications supplied with the Red Hat Linux 9 distribution, you'll need these disks for installing the applications themselves. Therefore, it's worth keeping all the three binary CD disks in your possession.

### The Hardware

Before you start the installation, it's a good idea to make a note of the hardware details of the machine you plan to use for your Linux installation. These details can help you to get the most out of the installation process, and even in detecting problems in the hardware configuration itself – problems that can prevent Red Hat Linux from installing correctly.

### Determining Your Hardware

During the process of installation, Red Hat Linux may need some extra help to determine the exact hardware composition of your computer. To help it out, it is a good idea to make a note of the details on the following checklist, before you begin the installation:

- **Keyboard type**: The Red Hat Linux installation defaults to a standard US English 105-key keyboard. Unless you are using a language-specific keyboard like those used in many European and East Asian countries, you don't have to worry about this detail.
- **Mouse type**: Red Hat Linux supports two-button and three-button mice, as well as wheel-mice and the cordless variety. It's worth noting the exact make and nature of your mouse. Red Hat Linux also supports tablets; to verify that your make of tablet is compatible with Red Hat Linux, check the Hardware Compatibility List.
- **Hard disk size**: Make a note of the size of the hard disk that you'll be installing Red Hat Linux onto. If the installation process fails to detect the hard disk size correctly, it might point to an underlying hardware problem. Also note that a Personal Desktop installation will require around 1.8GB of hard disk space to cater for the programs loaded during installation. If you plan to install other applications, then you will need more.
- **Video (graphics) card**: Note the chipset of the video card and the amount of RAM. While the Red Hat X-server configuration program can usually probe and detect the video card, it sometimes fails. If it does fail, you'll need to tell Red Hat Linux the name of your video card chipset. Note that the video RAM is sometimes also displayed on the computer screen during boot up of the machine.

> If you can't find the name of your video card chipset in the Hardware Compatibility List (see below), don't worry. Note that this means only that the GUI of Red Hat Linux is affected. Generally, if you intend to use the computer only as a server system, you're recommended not to install any GUI — this is for reasons of resource load and security. If you do want a GUI, you'll still be able to configure your machine to use the VESA interface for running the X-server. The VESA interface standard is supported by most of the commonly available video cards.

- **Monitor**: If you have an unusual monitor model, then the configuration of the GUI X Server software (during the installation process) might not detect it. Therefore, it's worth noting information regarding your monitor. You'll need the horizontal and vertical sync rates, which can generally be found either in the monitor manual or at the monitor manufacturer's web site.
- **Sound card**: While the installation tries to detect the sound card, it sometimes doesn't succeed. Therefore, it's good to note the name of the sound card chipset in advance.
- **Network card**: During installation, Red Hat Linux tries to detect the network interface card (NIC) and load the appropriate software driver automatically. You should note the name of the chipset of the NIC in advance of installation, just in case the installation process fails to determine it.

How do you get hold of this information? Well, if you have the technical specification documents that were supplied with your computer, then you'll find the information in there. If not, then the machine's existing operating system will probably offer some way of browsing the hardware being used. For example:

- In Windows 2000, you can find out about existing hardware via Start | Settings | Control Panel | System (select the Hardware tab, and click the Device Manager button).
- In other Linux systems, you can find out about existing hardware through via various menu options of the GUI. For example, try the options in Programs | Settings or Main Menu | System Tools, depending on which version of Linux you're using.

### The Hardware Compatibility List

Red Hat maintains a list of officially supported hardware, called the Hardware Compatibility List (HCL). The HCL lists all the hardware components against which the operating system has been checked extensively for proper functioning. The list is available at [http://hardware.redhat.com/hcl/](http://hardware.redhat.com/hcl/).
