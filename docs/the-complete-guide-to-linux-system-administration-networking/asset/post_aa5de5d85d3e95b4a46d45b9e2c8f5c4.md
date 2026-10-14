
10. Use wget to download part of the Free Software Foundation Web site to your local system. Depending on the speed of your network connection, you may want to reduce the recursion level option (-l) from 3 to 2.

```
wget -p -k -r -l 3 http://www.gnu.org/ -o gnu_log &
```

11. Use a graphical Web browser to access the Web pages you have downloaded using wget.

12. Close all windows and log out.

## CASE PROJECTS

![](img/43f64015de86d989e30eff5bb284fb96_352_0.png)

## Working with Network Clients and Connections

You are researching a project to provide space science information for schools in your area. Someone has suggested that you copy the NASA Web site to one of the school district's local servers. Students often access the NASA site, but it is very busy and sometimes slow.

+   1. Briefly explore the site www.nasa.gov. What concerns would you have about mirroring that site? How might you overcome some of those concerns given the goals stated for mirroring the site?

+   2. One of the largest FTP sites is ftp.ibiblio.org. The school would also like to mirror this site for the convenience of users. How do your concerns about doing this compare to your concerns in Question 1?

+   3. Would you use rsync, wget, or another tool to mirror part of the ibiblio.org FTP site? Look on sites such as freshmeat.net and sourceforge.net to locate other possible tools to help you maintain a large FTP site mirror.

+   4. As you work with FTP in your organization, you are concerned that all the information transmitted using FTP is unprotected—someone with basic networking knowledge can see all the data as it traverses the network. You decide to use ssh to encrypt this FTP data. Review the man page of ssh and sshd, as well as documentation provided on www.openssh.org, to see how you can use ssh to create a secure communications channel for the ncftp program.

## CHAPTER 8

## Installing Linux

After reading this chapter and completing the exercises, you will be able to:

+   - Learn about the hardware components of your computer system
+   - Configure hard disk space to hold a new Linux installation
+   - Install Linux
+   - Automate installation of multiple systems

In the previous chapter you learned about basic network clients that you can use as a system administrator to access a system across a network connection. Several methods were presented, including Telnet, r-utilities, and the Secure Shell (SSH). You also learned about command-line and graphical utilities for accessing network data services such as FTP and the Web; these tools permit automated downloading of Web information as well as downloading numerous Web or FTP sites simultaneously. To help you effectively access remote connections and utilize network data services, you also learned basic information about networking and saw the ping and traceroute network diagnostic utilities.

In this chapter you learn how to prepare for and then install a new Linux operating system. To this point, you have been working on a system that another person installed. You now have enough background to understand the issues surrounding a new Linux installation. This chapter discusses those issues—including hardware compatibility, preparing your hard disk, and creating dual-boot systems—then it walks you through an actual installation of Red Hat Software’s Fedora Linux (the product included with this book). After you install the new system, you learn about postinstallation configuration issues. Finally, you will learn about utilities that let you perform similar installations on multiple systems, or perform installations without needing to enter any information during the installation.

## Reviewing Your Computer's Hardware

Most of the computer systems that you have used or purchased yourself probably had an operating system already installed. You didn't have to think about how the operating system ended up on the computer's hard disk or how it was configured to use components such as the mouse, the video display capabilities, and the keyboard.

Although you can purchase computers with Linux preinstalled, you can learn a great deal about your computer system and about how Linux operates by installing the operating system yourself.

Before you install Linux, you must plan your installation to make effective use of your hardware and prevent problems from occurring in the midst of the installation. To plan your installation, you must gather information about your computer hardware so that you can answer questions that arise during the installation process. You also must determine the best way to organize Linux on your computer—you will learn later in this chapter about completing both of these tasks.

Although the information in this chapter is useful for installing Linux on a single computer, it is even more important to understand installation planning issues when you install Linux on multiple computers, or on a large server with multiple hard disks and advanced hardware components.

You will soon discover that Linux is quite easy to install, especially on newer computers, about which Linux can automatically determine much of the needed information about your system. But the more you know about how the installation process functions, the better you can deal with problems that arise, and the more flexibility you will have when complex installation scenarios present themselves.

## Understanding Computer Hardware

As you have already seen with regard to hard disks, Linux treats your computer hardware as a collection of devices. Information is stored on a hard disk device, output is written to a video card device, input is read from a keyboard device, and so forth. Linux must be configured to use all of the devices on your computer system to function correctly. Sometimes the task of configuring your hardware is a challenge, although normally you don't need to do much at all.

![](img/43f64015de86d989e30eff5bb284fb96_355_0.png)

> Linux can be used on many types of computers, including those that use different types of microprocessors (CPUs), such as Alpha, SPARC, PowerPC, and Xeon. The discussion in this chapter is devoted solely to computers using Pentium-level Intel and Intel-compatible microprocessors—in other words, standard PCs.

Different types of hardware devices communicate with the operating system in different ways. This means that you may need to gather an array of information about your computer system before you can install Linux. The section "Creating a System Inventory," later in this chapter, explains how to locate the information you need. Because Linux installation programs have become so automated, gathering hardware information for your computer may be more an exercise than a necessity, but the background material provided in this section will help you in many situations where hardware questions arise.

You should begin by learning a few common terms that describe your computer hardware. Space or capacity on a computer system is measured in bytes. A byte is enough space to store one character. Each byte is typically composed of eight bits. A bit stands for binary digit; it can hold a value of either one or zero. Eight bits together—a byte—represent a numeric code that corresponds to a character.

Because computers store many characters, space is commonly measured in megabytes, abbreviated as MB. One megabyte is 1,048,576 bytes, or enough space to store roughly 1 million characters. Another common term is gigabyte, abbreviated as GB. One gigabyte is 1024 MB, or roughly enough space to store 1 billion characters. For comparison, this chapter has about 120,000 characters in it. A 400-page novel can contain about 600,000 characters, or less than 1 MB.

## Storing Information

The electronic memory of a computer is called random access memory, or RAM. Information in RAM is only available when the computer is turned on. When you turn the computer off, everything stored in RAM is lost. RAM is normally measured in MB, with most newer computers having from 128 MB to 512 MB of RAM. Computers used as servers may have 1–4 GB of RAM.

Another electronic component in a computer is called read-only memory, or ROM. ROM stores instructions controlling how the computer starts up and how the computer's devices are configured. Like RAM, ROM is stored on a computer chip, but information in ROM is not lost when the computer is turned off; it is permanent, or nonvolatile. One of the key things stored in ROM is the Basic Input/Output System, or BIOS, which provides instructions to the operating system for using the devices on the computer. The BIOS itself cannot be changed—it is permanent. But the computer also contains a special type of RAM that stores parameters to control parts of the computer configuration. You may hear this special storage referred to by its technical name, CMOS RAM. CMOS RAM depends on a tiny battery to maintain configuration data when the computer is turned off. You can change settings in the CMOS RAM using a utility that is part of the BIOS. Information stored in CMOS RAM by the BIOS utility might include the setting for the computer's clock, information about the structure of each disk drive, a start-up password, and many other details.
