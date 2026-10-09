
![](img/243613168ac865b539f12460d966088e_107_0.png)

## Test the installation image file and test the installation medium

It is a good idea to test the installation (ISO) image file and the installation medium before you use it to install Linux. When you boot the system from the installation medium, Fedora/RHEL gives you the option of checking the image file for errors (see the tip on page 65). A bad file on an installation medium might not show up until you finish installing Fedora/RHEL and have it running. At that point, it might be difficult and time-consuming to figure out where the problem lies. Testing the file and installation medium takes a few minutes but can save you hours of trouble if something is not right. If you decide to perform one test only, test the installation medium.

It is critical to have certain pieces of information before you start. One thing Linux can never figure out is all the relevant names and IP addresses (unless you are using DHCP, in which case the addresses are set up for you).

Following is a list of items you might need information about. Gather as much information about each item as you can: manufacturer, model number, size (megabytes, gigabytes, and so forth), number of buttons, chipset (for cards), and so on. Some items, such as the network interface card and the sound card, might be built into the motherboard.

- Hard disks
- Memory; you do not need it for installation, but it is good to know
- SCSI interface card
- NIC (network interface card)
- Video interface card (including the amount of video RAM/memory)
- Sound card and compatibility with standards, such as SoundBlaster
- Mouse (PS/2, USB, AT, and number of buttons)
- Monitor (size and maximum resolution)
- IP addresses and names, unless you are using DHCP (page 491; most routers are set up as DHCP servers), in which case the IP addresses are automatically assigned to the system. Most of this information comes from the system administrator or ISP.
  - System hostname (anything you like)
  - System address
  - Network mask (netmask)
  - Gateway address (the connecting point to the network or Internet) or a phone number when you use a dial-up connection
  - Addresses for nameservers, also called DNS addresses
  - Domain name (not required)

## CHAPTER SUMMARY

A Live Image can run a live Fedora session without installing Fedora on the system. You can install Fedora from a live session. Running a live session is a good way to test hardware and fix a system that will not boot from the hard disk.

When you install Fedora/RHEL, you copy operating system files from an installation medium (e.g., DVD or USB flash drive) to hard disk(s) on a system and set up configuration files so that Linux runs properly on the hardware. Operating system files are stored on installation media as an installation (ISO) image file. You can use a Web browser, FTP, or BitTorrent to download an installation (ISO) image file. It is a good idea to test the image file when it is downloaded and the installation medium before you use it to install Fedora/RHEL.

When you install Fedora/RHEL, you can let the Anaconda installer decide how to partition the hard disk (default partitioning) or you can manually specify how you want to partition it.

The Fedora Project is sponsored by Red Hat and supported by the open-source community. Fedora is a Linux release that contains cutting-edge code; it is not recommended for production environments. RHEL is more stable than Fedora.

## EXERCISES

1. Briefly, what does the process of installing an operating system such as Linux involve?
2. What is an installer? What is the name of the Fedora/RHEL installer?
3. Would you set up a GUI on a server system? Why or why not?
4. A system boots from the hard disk. To install Linux, you need it to boot from a DVD. How can you make the system boot from a DVD?
5. What is free space on a hard disk? What is a filesystem?
6. What is an ISO image? How do you burn an ISO image to a DVD?

### Advanced Exercises

7. Give two reasons why RAID cannot replace backups.
8. What are RAM disks? How are they used during installation?
9. What is SHA2? How does it work to ensure that an ISO image file you download is correct?

*This page intentionally left blank*

# 3

# STEP-BY-STEP
# INSTALLATION

### In This Chapter

- Running a Fedora Live Session . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 56
- Installing from a Live Session . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 60
- Installing from an Install Image . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 60
- The Anaconda Installer . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 62
- Modifying Boot Parameters
  (Options) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 70
- Advanced Disk Configuration . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 72
- Manual/Custom Partitioning . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74
- Reclaiming Disk Space . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
- gnome-disks: The GNOME
  Disk Utility . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 78
- Editing a Kickstart Script . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 83
- Setting Up a Dual-Boot System . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84

### OBJECTIVES

After reading this chapter you should be able to:

- Run a live session and use **gnome-disks** to view and change disk partitioning
- Install Fedora from a live session
- Install Fedora/RHEL using an Install Image
- Modify system behavior using boot parameters
- Modify partitions during installation
- Select software during installation
- List the requirement and considerations for a dual-boot configuration

Chapter 2 covered planning the installation of Fedora/RHEL: determining the requirements; planning the layout of the hard disk; obtaining the files you need for the installation, including how to download and burn or write Install, Live, and Network Images to installation media; and collecting information about the system. This chapter focuses on installing Fedora/RHEL. Frequently the installation is quite simple, especially if you have done a good job of planning. Sometimes you might run into a problem or have a special circumstance; this chapter gives you tools to use in these cases. Read as much of this chapter as you need to; once you have installed Fedora/RHEL, continue with Chapter 4, which covers getting started using the Fedora/RHEL desktop and command line.

### THE NEW ANACONDA INSTALLER

The new Anaconda installer, introduced in Fedora 18, has been totally rewritten. The Anaconda user interface changed from a linear (wizard) model to a hub-and-spoke model. Using this model means Anaconda can perform background processing (e.g., you can still be entering information while Anaconda is installing packages) and you can skip screens that are not pertinent to your installation. See fedoraproject.org/wiki/Anaconda/NewInstaller for more information.

#### Chapter 17 explains how to set up a virtual system

> **tip**  To install Fedora/RHEL on a virtual system, you build the virtual system and then follow the instructions in this chapter for installing the operating system. See page 663 for instructions on setting up a QEMU/KVM virtual machine and page 671 for setting up a VMware virtual machine.

#### Upgrading a Fedora system

> **tip**  The new Anaconda installer will not upgrade a Fedora system from one release to the next. You must use FedUp (FEDORA UPgrader), which works on Fedora 17 and later. Visit the Fedora Web page at fedoraproject.org/wiki/FedUp for more information.

## RUNNING A FEDORA LIVE SESSION

As discussed in Chapter 2, a live session is a Linux session you run on a computer without installing Linux on the computer. When you reboot after a live session, the computer is untouched. If you are running Windows, after a live session Windows boots the way it did before the live session. If you choose, you can install Fedora from a live session. RHEL does not offer a live session.

A live session gives you a chance to preview Fedora without installing it. Boot from a Live Image to begin a live session and work with Fedora as explained in Chapter 4. When you are finished, remove the installation medium and reboot the system. The system will boot as it did before you ran the live session.
