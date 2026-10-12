
# 322 Part VI: Appendices

If all you have is a SCSI hard drive, Drive 0 or Drive 1 is usually your drive C, and others follow in order.

If you have a mixture of IDE and SCSI controllers, your drive C could be on any of them. The sections “Discovering Your Windows 9x or Windows Me Hardware” and “Discovering your Windows NT, Windows 2000, or Windows XP Hardware,” later in this appendix, show you how to identify how many hard drives you have, which type(s) they are, and which controllers they’re attached to.

Considering putting Fedora Core on a separate hard drive, away from any Windows operating system, for a couple of reasons. First, you can now find 80GB hard drives for well under $100 (U.S.). Second, it’s a pretty daunting task (at worst, nearly impossible) to shrink MS-DOS and Windows till they’re small enough to allow Fedora Core to reside in its full glory on an existing hard drive. Also, although technically you can split the Fedora Core distribution and put it on several hard drives, doing so makes updating the distribution difficult later.

![Image](img/41feae212f5c6612ff709354891f7b39_339_0.png)

### A Bit About Memory Bytes

Memory is the most important factor in determining how fast your computer runs. Computers use Random-Access Memory (RAM) to store and access the operating system, programs, and data. The Intel processor usually has the following amounts of RAM (main memory):

- Linux can run on a surprisingly small amount of memory. With some work and no graphics, you can squeeze Linux onto an old PC with only 16MB of memory; 32MB makes life much easier and your computer significantly faster.
- Many people use suitable old PCs with small amounts of memory as simple network servers.

![Image](img/41feae212f5c6612ff709354891f7b39_339_1.png)

- If you want to run Linux with graphics, however, you need 64MB.
- With 128MB, Fedora Core runs multiple graphical programs (such as OpenOffice.org) with ease.
- You need 256MB or more (many PCs now come standard with 512MB) for hard-core computing. Using big applications, such as VMware, makes having enough memory essential.

VMware virtual computers need their own RAM to operate at a reasonable speed; for example, you should allocate a minimum of 128MB of memory to run a Windows 2000 virtual computer. Plan to use 512MB if you want to run multiple instances of VMware virtual computers.

![Image](img/41feae212f5c6612ff709354891f7b39_339_2.png)

You can install Fedora Core on most laptop computers by using the notebook's built-in CD-ROM drive, or a PCMCIA, USB, or proprietary CD-ROM drive. If you don't have any of these items, you can try to get a PCMCIA Ethernet controller and do a network installation, as long as another Linux system on the network has a CD-ROM drive installed. If that's the course you take, consult the Fedora Core installation documentation at www.redhat.com/support. You also need a video card that Fedora Core understands. Fedora Core supports most video cards, and usually the only problems result from bleeding-edge notebook computers that use the latest and greatest video hardware. You can use the generic VGA, XGA, or SVGA drivers that Fedora Core supplies if you cannot find the specific driver.

### Discovering Your Windows 9x or Windows Me Hardware

You don't have to go to Hollywood to be discovered — provided you're a piece of computer hardware. Windows provides the tools to discover your bits and pieces right at home. This section describes how to use Windows 9x or Windows Me (which Microsoft will still support for a while yet) for the discovery process.

If you have a Windows 9x or Windows Me computer, use this section to discover and display information about your computer. Use the ubiquitous Control Panel. Start your Windows computer and follow these instructions:

1. Click the **Start** button and choose **Settings: Control Panel**. Double-click the **System** icon and select the **Device Manager** tab.
2. At the top of the screen, select **View Devices by Connection**. This step shows you all components and how they relate to each other.
3. On the **Device Manager** tab (from the **Control Panel**) in the **System Properties** dialog box, select the **View Devices by Type** option.

On the list, notice how a plus (+) or minus (−) sign precedes some icons. A plus sign indicates that the entry is collapsed. A minus sign indicates that the entry is expanded to show all subtrees.

4. Click the **plus (+) sign** to expand the list.

Expanding the list shows each computer subsystem. Every device that makes up your computer is shown. Right-click a device and choose the **Properties** option to display information about a particular device.

You can use the Web to find out about your computer. Computer companies provide detailed information about their products on their Web sites. Go to the manufacturer's Web page and look up your computer's model number. When you get to your page, look for the **Specification** (or **Specs**) link.

### Discovering Your Windows NT, Windows 2000, or Windows XP Hardware

Discovering information about a system running Windows NT, Windows 2000, and Windows XP is similar to making the same discovery on a Windows 9x or Windows Me system. The process is the same, although getting there is a little different:

On Windows NT and Windows 2000 computers, follow these steps:

1. Click the **Start** button and choose **Settings Control Panel**. Then, double-click the **System** icon in the **Control Panel** window.
2. Click the **Hardware** tab when the **System Properties** window opens. Then, click the **Device Manager** button to open the **Device Manager** window.
3. Click the plus (+) sign of any hardware subsystem you want to examine. A submenu opens, showing you all the devices of a particular type.
4. **Right-click** any hardware subsystem and choose **Properties**. The **Properties** option shows you information about that particular device.

On Windows XP computers, follow these steps:

1. Click the **Start** button and choose the **My Computer** option.
2. **Double-click** the **Control Panel** icon.
3. **Double-click** the **System** icon, select the **Hardware** tab, and then double-click the **Device Manager** button. The **Device Manager** window opens.
4. Click the plus (+) sign to display the devices within a subsystem.
5. **Right-click** a device to open a menu from which you can choose the **Properties** option. The **Properties** window opens and shows information about the device.

# Appendix C
Filing Your Life Away

## In This Appendix

- Finding out all about Linux files and directories
- Navigating the Linux file system
- Creating, moving, copying, and destroying directories and files
- Changing file ownership and permissions

In this appendix, you step boldly through the Linux file and directory structure. Don't worry: Linux may live a structured life, but it's still flexible. With a little bit of introduction, you can quickly get the hang of the Linux way of life.

We also introduce you to file types, subdirectories, paths, and the root directory. You're also shown the way home — to your home directory. After you're oriented to the Linux files-and-directories structure, we show you how to make some changes, such as how to copy and move files and directories and how to — eek! — destroy them.

## Getting Linux File Facts Straight

Linux files are similar to Unix, DOS, Windows, and Macintosh files. All operating systems use files to store information. Files allow you to organize your stuff and separate your information. For example, the text that makes up this appendix is stored in a file — as is every other chapter, each in its own file. Follow the bouncing prompt as we make short work of long files.

## Storing files

We assume that you know that a file is a discrete collection of information identified by a filename — and that Linux can store multiple files in directories, as long as the files have different names. (Linux stores any files with the same name in different directories.)
