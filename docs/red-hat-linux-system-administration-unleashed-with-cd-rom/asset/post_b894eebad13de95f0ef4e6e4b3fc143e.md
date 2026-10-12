
Now that we have covered /proc, the next section will look at some simple ways to alter files in /proc.

## Using echo to Alter System Behavior

Previously we examined /proc and what it is, and introduced the concept of changing system values within /proc to alter how the system operates. What we have not done is examine exactly how this can be accomplished with relative ease. We will look at two examples of passing information to the system using terminal echoing.

> **Note**
> 
> All of the examples discussed may or may not work depending on the revision of the kernel. For example, some parameter locations may be different or they may not even exist.

> **Note**
> 
> These examples are taken directly from http://www.linux.com/tuneup/database.phtml?Kernel/ and http://www.nl.linux.org/linuxxperf/.

### Understanding the Anti-Ping Setting

The first example is the anti-ping setting. For the sake of an example, let's say that on your corporate intranet, someone keeps pinging the Linux server Larry to see if it is alive instead of just browsing to the Web server. Although you would like to tell the user how you appreciate his ingenuity, you would prefer he just browsed to Larry's server and you will let him know if there are any problems. Of course, he doesn't listen. As a matter of fact, he has taken to running ping for hours on end. As a temporary measure, you would like to shut off the inbound ping requests without altering any other protocols. There is a long way to do this, which we will not get into, but the easiest way is to simply try this:

```
$ echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```

This will cause the system to ignore all ping requests.

Not only can certain running conditions or values be altered, but some system limits can be changed as well. Here is an example that shows how to use echo to change the maximum file and maximum inode count:

```
$ echo NEWVALUE > /proc/sys/fs/file-max
$ echo NEWVALUE > /proc/sys/fs/inode-max
```

For example, changing the maximum inodes to 65536 (a very popular value for some reason) would look like:

```
$ echo 65536 > /proc/sys/fs/inode-max
```

Once again, you should see the possible dangers here. Although changes such as file-max and inode-max are not too dangerous, there are plenty of ways to get your system into hot water by fooling around in /proc.

## Summary

Performance monitoring and tuning is not a lightweight topic. This chapter provided a brief look at both actions on Linux systems; however, there is much more to it when you have multiple systems and ever-growing systems. This should be enough to get you started in monitoring and tuning a Linux system after a little practice with the utilities and methods we discussed.

## 35
CHAPTER

## Customizing the Linux Kernel

### In This Chapter

- Use the Source 1082
- Patching the Kernel Source 1091
- Kernel Loadable Modules 1094
- Kernel Building 1100

When speaking to people unfamiliar with Linux, one of the misconceptions often heard is that rebuilding the Linux kernel is difficult and that only expert users should attempt this operation. This chapter attempts to dispel this myth. It begins by looking at reasons why you might want to compile the kernel source code. It then covers where to obtain the kernel source code and official patches to update from one kernel version to the next. Next, this chapter covers the issue of patches to the kernel source and the use of unofficial patches in the default Red Hat kernel. It then takes a look at the layout of the kernel source tree, explaining what is found in each directory. Once the layout is described, the discussion moves to a description of how to patch the Linux kernel source. A short section is devoted to examining the modules system, and the final part of the chapter is devoted to explaining the configuration options available when compiling the kernel and how to actually build a kernel using make.

## Use the Source

One of the primary reasons for the explosive growth that Linux has seen is the availability of the source code for just about any part of the system, including the operating system kernel. This freedom allows people from all over the Internet to modify or extend the functionality of the system as their programming talent allows. This freedom has attracted the attention of some of the brightest minds on the Internet and they contribute to making Linux a flexible and stable operating system.

For the systems administrator, having the source code means that the Linux kernel can be streamlined to suit the machines on which it will run, eliminating unused functionality, adding processor specific optimizations, or adding new functionality.

This section covers why you would want to recompile the kernel source code, where to obtain it, and how the kernel distributed by Red Hat differs from the kernel source distributed by Linus.

## Why Recompile? Reasons for Recompiling

If you examine the configuration of the kernel that comes with your Red Hat Linux system, you will see that it is as generic as possible and that support for as much hardware as possible is included through modules. By generic, I mean that it contains support for most common hardware and is not specifically tuned for the machine on which it will be running. Because it is likely that this kernel will run on any machine you install it on, you may ask why you should recompile the kernel. There are several reasons. Here are a few of them:

- Removing unused or unwanted drivers and modules.
- Adding missing functionality.
- Upgrading to a later kernel release.

A common reason for recompiling your kernel is to remove unused or unwanted drivers from the kernel. This allows your kernel to use up less space on the hard drive, and possibly to load faster, because checks for hardware that you do not have are eliminated. Considering the fact that large capacity hard drives are now standard on most systems and are relatively inexpensive, the space issue may seem inconsequential, but if you are building boot floppies, every byte used can make a difference.

Adding missing functionality is another reason why you might want to recompile your Linux kernel. There are numerous options available for the Linux kernel and not all of them are included with the default kernel installed by Red Hat. In addition, patches are available independent of the kernel source that add functionality. For example, there is a driver available for SCSI changer devices such as those used in tape libraries or CD changers. The driver for this functionality is distributed as a kernel patch that you can add to your kernel. Another example of this is the PCMCIA drivers, which come with your Red Hat install media that add support for PCMCIA cards used in most laptop computers.

Probably the most common reason for recompiling your kernel source is to upgrade to a new kernel version. The open source development model ensures that kernel development proceeds at a fairly rapid pace. Between the time that the Red Hat install media was created and the time that you are reading this book, there may have been dozens of upgrades to the kernel source and these upgrades may include new functionality or important security fixes.

You may be wondering how often you should upgrade to a new kernel version. The answer is highly dependent on the purpose of the system in question. If the system is a corporate Web server that needs to be up and running twenty-four hours a day, you will probably only want to upgrade to add a significant new feature or to eliminate a specific defect. Another reason for upgrading is to plug a security hole. In general, you should only upgrade to achieve some tangible benefit. As the old adage goes, "If it ain't broke, don't fix it."

## Obtaining the Source

Since the beginning, the release of the Linux kernel source code has been controlled by Linus Torvalds. Linus serves as the chief architect of the Linux kernel, and the kernel released by him is considered the official kernel. The primary FTP site for the kernel source code is ftp.kernel.org and its mirror sites. The official mirror sites use a standard naming convention of ftp.XX.kernel.org, where XX is the two digit country code for the country in which the mirror is located. For example, the United States mirror site is ftp.us.kernel.org, the United Kingdom mirror site is ftp.uk.kernel.org, and so on. A complete list of mirror sites can be found at the kernel.org Web site at http://www.kernel.org.

The directory layout for these mirrors differs slightly from site to site, but once you reach the kernel directory the layout is well defined. For each kernel version, where kernel version is defined by a major and a minor release number, there is a directory whose name is vM.N; M being the major release number and N being the minor release number. For example, for the current stable release at the time that this book was written, this directory would be v2.2. All of the various kernel releases and patches for this release are in this directory.

> **Note**
> Beginning with the release of the 1.0 Linux kernel, a kernel numbering scheme was devised to differentiate between stable kernel tracks and development tracks. This numbering scheme states that kernels with an even minor number are considered to be on the stable track and that patches to this kernel should only be made to correct deficiencies. On the other hand, the development track kernels are given an odd minor number, may include new features, and allow for the evolution of the kernel from one stable release to the next.

The most recent release is indicated by a file in that directory named LATEST-IS-M.N.P, where M is the major release number, N is the minor release number, and P is the patch level. For example, when the 2.2.5 version of the kernel was released, this file was updated and was named LATEST-IS-2.2.5. Listing 35.1 is an example of an FTP session showing this directory structure.

### LISTING 35.1 FTP Session Transcript to ftp.us.kernel.org

```
[tschenk@quicksilver tschenk]$ ftp ftp.us.kernel.org
Connected to ftp.us.kernel.org.
```
