
2. Create a new partition for the Linux file system. To do this, press the Add button on the Disk Druid screen. A dialog box appears as shown in figure 7, where you can mention /boot partition and enter the size in MB or accept the default option.

![](img/f3b9cff79e19317416c12eaf5ded7245_23_0.png)

▲ Figure 7

3. Create a new partition for the Linux file system. To do this, press the Add button on the Disk Druid screen. A dialog box appears as shown in figure 8, where you can fill in / as the mount point and enter the size in megabytes.

![](img/f3b9cff79e19317416c12eaf5ded7245_23_1.png)

▲ Figure 8

4. After making the changes, click the Next button in the Disk Druid screen to proceed to the next installation step. As shown in figure 9.

![](img/f3b9cff79e19317416c12eaf5ded7245_24_0.png)

## Configuring Linux Installation

After you prepare the disk partitions with Disk Druid and specify which partitions to format, perform the following steps to configure Linux installation:

- Install Boot Loader GRUB
- Configure the network
- Firewall configuration
- Set the time zone
- Set the root password and add user accounts
- Configure password authentication

The following sections guide you through each of these configuration steps.

### Installing the Boot Loader (GRUB)

The next part of the Boot Loader Configuration screen as shown in figure 10 gives you the option of installing the boot loader in one of the two locations, which are as follows:

- Master Boot Record (MBR), which is located in the first sector of your PC's hard disk.
- First sector of the partition where you loaded Linux.

![](img/f3b9cff79e19317416c12eaf5ded7245_25_0.png)

▲ Figure 10

### Configuring the Network

Perform the following steps to configure the network:

- □ As shown in figure 11, click the button labeled Configure using DHCP if your PC obtains its IP address and other network information from the Dynamic Host Configuration Protocol (DHCP) server.
- □ Fill in the necessary network related information manually.
- The Network Configuration screen asks for the following key parameters:
  - □ IP address of the Ethernet interface.
  - □ The host name for your Linux system. (For a private LAN, you can assign your own host name without worrying about that it could conflict with any other existing systems on the Internet).
  - □ IP address of the gateway (the system through which you might go to any outside network).
  - □ IP address of the primary name server.
  - □ IP address of a secondary name server.
  - □ IP address of a tertiary name server.

![](img/f3b9cff79e19317416c12eaf5ded7245_26_0.png)

▲ Figure 11

### Firewall Configuration

Here are your choices for configuring the firewall during the installation. If you enable firewall then you can click the appropriate check boxes and allow incoming requests for the following services as shown in figure 12.

![](img/f3b9cff79e19317416c12eaf5ded7245_26_1.png)

▲ Figure 12

### Setting the Time Zone

Select the time zone by either click a spot on the map or choose from the drop-down box as shown in figure 13.

![](img/f3b9cff79e19317416c12eaf5ded7245_27_0.png)

▲ Figure 13

### Setting the Root Password and add User Accounts

You must choose a password for your root user at this point. The root password provides the complete control of your Linux system. Enter the root password and then type it again in the confirm the box as shown in figure 14.

![](img/f3b9cff79e19317416c12eaf5ded7245_27_1.png)

▲ Figure 14

### Selecting the Package Groups to Install

For a new install, the installer automatically select default set of basic software packages to install. You can customized the list of the packages to be installed. As shown in figure 15 and figure 16.

![](img/f3b9cff79e19317416c12eaf5ded7245_28_0.png)

![](img/f3b9cff79e19317416c12eaf5ded7245_28_1.png)

### About to Install

A screen shown in figure 17 tells you that you are about to begin writing to the hard disk. You can still back out now, and your hard disk will not have changed. Click **Next** to proceed.

![](img/f3b9cff79e19317416c12eaf5ded7245_29_0.png)

▲ Figure 17

### Completing the Installation

When you see the congratulation screen as shown in figure 18, you are done. Eject the DVD or CD and click the robot.

![](img/f3b9cff79e19317416c12eaf5ded7245_29_1.png)

▲ Figure 18

### Firstboot: After Successful Installation

After installing Linux and rebooting, the welcome screen appears as shown in figure 19. The list on the left side of the screen shows the tasks and the setup will guide you through, click forward to continue.

![](img/f3b9cff79e19317416c12eaf5ded7245_30_0.png)

- **License Agreement**

You must agreed to the license before continuing to use Linux as shown in figure 20

![](img/f3b9cff79e19317416c12eaf5ded7245_30_1.png)

### Date and Time Setup

Date and Time screen in figure 21 can be used to set the correct date and time.

![](img/f3b9cff79e19317416c12eaf5ded7245_31_0.png)

### Display Setting

![](img/f3b9cff79e19317416c12eaf5ded7245_31_1.png)

### Sound Configuration

![](img/f3b9cff79e19317416c12eaf5ded7245_32_0.png)

▲ Figure 23

### Adding System Users

For the daily use of Linux, you should have your own user account. You should log in with this user name, and work with Root user account for administrative tasks. You can create user as shown in figure 24.

![](img/f3b9cff79e19317416c12eaf5ded7245_32_1.png)

▲ Figure 24

### Additional Software Packages

![](img/f3b9cff79e19317416c12eaf5ded7245_33_0.png)

▲ Figure 25

> Installation steps for different Linux versions (RedHat 7.1–9.0, Fedora Core 1–10 and RHEL1–5) are more or less same.

## Monitoring Linux Installation

### Using Virtual Console during Installation

Red Hat Linux installation goes beyond a simple sequence of dialog boxes. In fact, you can look at different diagnostic messages during the installation process. You can switch among five virtual consoles, which can be helpful if you encounter problems during installation. The table 2 below shows the consoles, the key to switch to each console, and the purpose of that particular console.

| Console # | Keystroke | Output |
| :--- | :--- | :--- |
| 1 | Ctrl+Alt+F1 | Installation Dialog box |
| 2 | Ctrl+Alt+F2 | Shell Prompt |
| 3 | Ctrl+Alt+F3 | Install Log (message from the install program) |
| 4 | Ctrl+Alt+F4 | System Log (message from OS kernel) |
| 5 | Ctrl+Alt+F5 | Other Messages |
| 7 | Ctrl+Alt+F7 | X Graphical Display |

![](img/f3b9cff79e19317416c12eaf5ded7245_34_0.png)

> Install output is written to five of the virtual consoles. Note these key bindings are for the installation only.

Let’s summarize the main points of the Lab1 .

### Summary

We learned the installation of Linux using CD-ROM source, partitioning of a hard disk, configuration of GRUB boot loader, network, firewall, and selection of software packages.

## NOTES

## 02 LAB: Advanced Linux Installation (Network and Dual-Boot)

### OBJECTIVES

- 1. Learn to set a Linux installed server.
- 2. Learn to install Linux over the network from image Server.
- 3. Learn to install network on your Linux operating system.
- 4. Learn about Dual-Booting Linux.

### REQUIREMENTS

- 1. Two Standard PCs with Intel or compatible Configuration
- 2. Linux Distributions (Fedora Core/RHEL) CDs or a DVD OR
- 3. CD- ISO images (typically 4 to 5) or single DVD- ISO image of Linux Distribution

### CONCEPT

During the network based installation of a Linux operating system we need to understand the TCP/IP configuration of our system as we can be asked for IP and network addresses. You can input the IP address and netmask of device either manually or through a Dynamic Host Configuration Protocol (DHCP). You can also add the address of Default gateway and primary name server. Basic process outline in this lab are as follows.

- 1. Our the network installation is a client Server Architectcre.
- 2. We are creating the server where we store Linux distribution Directories (For HTTP and FTP) and Linux ISO images (for NFS)
- 3. Then we configure client by providing topological correct IP address so that it can access installation images on server and then install Linux on its own machine.

### Setting up an Installation Image Server

If you have a LAN connection from your computer to a computer which has a CD/DVD-ROM drive and about 4 GB of disk space and it offers NFS, FTP, or Web services (http), you can install Linux from that server.

For setting up a Linux Installation Image server, you need to create an Installation directory (Distribution) where installation images are stored and need to configure different server services so that it allows to share installation images. Our machine act as a client, it will connect to the installation Image server and access that share to install Linux in its own machine..
