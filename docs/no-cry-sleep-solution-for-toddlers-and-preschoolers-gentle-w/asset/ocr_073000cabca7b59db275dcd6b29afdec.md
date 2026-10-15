hard disk space, you can elect to perform a minimum install, installing only the Linux kernel without most of the applications. You could later install the applications you want, one at a time, using the redhat-config-packages tool accessible on the System Settings window.

+   - Hard disk requirements depend on the kind of installation you want:
+     - Custom Installation (minimum): 520MB
+     - Server (minimum): 870MB
+     - Personal Desktop: 1.9GB
+     - Workstation: 2.4GB
+     - Custom Installation (everything): 5.3GB

# Hard Drive Configuration

These days, Linux is usually run on its own hard drive, though it can also be run in a different partition on a hard drive that also contains a separate partition for a different operating system such as Windows.

If you want to install Linux and Windows on the same hard drive, you can use a partition management software package, such as fdisk, fips, Parted, or Partition Magic, to set up your Windows and Linux partitions. If you have already installed Windows on your hard drive and configured it to take up the entire hard drive, you would resize its partition to free up unused space. The freed space could then be used for a Linux partition. See the Red Hat Linux x86 Installation Guide for more details.

# Information Requirements

Part of adapting a powerful operating system like Linux to the PC entails making the most efficient use of the computer hardware at hand. In almost all configurations, your Linux installation process will automatically detect and configure your hardware components. Sometimes, however, particularly with older or very recent hardware, your installer may not be able to correctly identify a component. If you have such components, such as a new model monitor or video card, you should first check their manuals and take note of certain configuration settings.

You will also need to determine how you want to use hardware resources, for example, how much of your hard disk you want to devote to Linux.

# CD-ROM, Hard Disk, and Mouse Information

For some older SCSI CD-ROM drives, you need the manufacturer’s name and model.

Decide how much of your hard drive (in megabytes) you want to dedicate to your Linux system. If you are sharing with Windows, decide how much you want for Windows and how much for Linux.

Decide how much space you want for your swap partition. Your swap partition should be about the same size as your RAM memory, but it can work with as little as 64MB. For system’s with smaller RAM configurations, the swap disk should be twice the size of the RAM. The size of the swap partition was expanded with the 2.4 kernel. Your swap partition is used by Linux as an extension of your computer’s RAM.