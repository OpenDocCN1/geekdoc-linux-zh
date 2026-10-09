# TOPIC B

# Troubleshoot Hardware Issues

You rectified system-based issues in a Linux system. Hardware devices may get corrupted and may not work properly. In this topic, you will troubleshoot hardware issues.

Systems may be connected to external devices such as speakers or modems. Sometimes, these devices may not work properly. Finding the cause of the problem will help you solve hardware issues.

# Troubleshooting Tools

There are many troubleshooting tools that you can use, depending on the type of problem you are facing and the environment in which you are working. Some of these tools are described in the following table.

![](bbox=[0.76, 0.32, 0.9, 0.37])

| Tool | Description |
| :--- | :--- |
| dmesg | A system administration command that is used to examine and control the kernel initialization process. It is used to print messages about the status of various hardware devices on the system during kernel initialization. Status messages can also be accessed from the /var/log/dmesg file. |
| /dev | A file that is used to create a boot or recoverable disk. |
| GNU Parted | A program that allows you to create, destroy, resize, move, and copy hard disk partitions. |
| HardDrake | A service that provides hardware detection in a graphical interface. |
| KNOOPPIX | A bootable CD (or DVD) that contains GNU/Linux software, which includes automatic hardware detection and support. KNOOPPIX can be used as a rescue system. |
| ifconfig | A file that is used to view the IP address and subnet mask and verify that they are allocated. It can also be used to debug or tune a system. |
| /proc | The proc filesystem is a pseudo-filesystem that is used as an interface to the kernel data structures. Each process contains a subdirectory in the /proc directory. |

# LNX-BBC

LNX-BBC is a Linux distribution that is small enough to fit in a CD-ROM, which is the size and shape of a business card. LNX-BBCs can be used to rescue damaged machines or as a temporary Linux workstation. More information regarding LNX-BBC can be found at http://www.lnx-bbc.org.

# Starting and Stopping Processes to Locate and Correct Problems

As discussed earlier in the course, both services and processes can be stopped and restarted. This can sometimes be used to fix problems. You can use the ps command along with the grep command to locate processes that you need to check on. You can then kill the processes if necessary.