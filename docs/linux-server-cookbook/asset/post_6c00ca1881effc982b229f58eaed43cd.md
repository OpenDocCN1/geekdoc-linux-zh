
## Installation menu

The first screen appearing when the server is booting from the Debian installer image, indicates which installation type is desired. The following figure shows the first screen of the installer:

![](img/863afa537de4eed7deb11978bfbfa90e_51_0.png)

*Figure 2.4: Debian installer menu*

Selecting the Graphical install entry in the menu will move the installer to the next step as a continuation is shown.

### Select a language

The first step after specifying which installation user interface would be used is to specify the language to be used during the installation process. This language, as indicated, will be used as the default language once the system is installed.

### Select the location

After specifying the language to be used during the installation and to be used as default, the next step is to select the location to be used. This location will be used to set the time zone and the system locale. If the location wanted is not in the list shown, it is possible to select “other” and afterward specify the continent/region and then the country.

### Configure the keyboard

Once the correct location is indicated, the next configuration is the Keymap for the keyboard to be used. Pressing Continue in this step will start to load the modules for the different components of the system (storage, network, and other devices), and it will try to configure automatically the network using DHCP.

### Configure the network

This step includes two parts when DHCP is used: specify the hostname for the system and indicate the domain to be used. The following figures show the wizard steps to introduce the hostname and the domain:

Please enter the hostname for this system.

The hostname is a single word that identifies your system to the network. If you don't know what your hostname should be, consult your network administrator. If you are setting up your own home network, you can make something up here.

**Hostname:**

debian

![](img/863afa537de4eed7deb11978bfbfa90e_54_0.png)

*Figure 2.5/2.6: Configure the network*

If the network is not configured automatically with DHCP, manual static IP should be specified after the hostname and domain name are set. The following figure shows the step to configure a static IP:

![](img/863afa537de4eed7deb11978bfbfa90e_55_0.png)

Figure 2.7: Configure the network

### Set up users and passwords

After the network is configured, the following step is to set the password for the root user. The password has to be a secure one, or it will not be accepted. If the password in this step is not set, the root account will be disabled, and the regular user account to be created will have the possibility to run commands or switch to root using sudo (a command allowing delegating authority for administrative tasks).

After setting the password for the root user or keeping it empty to disable the user, the next step is to set the information for the new user to be created. The first dialog is to specify the full name of the new user. The second information required is the username for the new user. This username is going to be used to login into the system. And after deciding on the username for the account, the password would be specified.

### Configure the clock

The next step is configuring the clock for the system. Keeping the time synchronized with the correct time is really important for some systems and for the system administrators when they are troubleshooting.

### Partition disks

The installer allows to do manual partitioning disk or uses the guided option. Using the LVM is highly recommended to have dynamic partitions and more flexibility in managing disks and partitions. The following figure shows the partition disk step:

![](img/863afa537de4eed7deb11978bfbfa90e_56_0.png)

![](img/863afa537de4eed7deb11978bfbfa90e_56_1.png)

After indicating the partition method, a list of the disks available in the system is listed to specify in which disk the partitions will be created. Once the disk where the installation will be performed is selected, the installer gives some partition options (if the guided option was selected). The following figure shows the partitioning options:

![](img/863afa537de4eed7deb11978bfbfa90e_57_0.png)

Figure 2.9: Partition disks

The next step related to storage is to confirm the changes to be performed on the disk. It is important to ensure that the correct disk is selected before the next steps are taken. The following figure shows the confirmation steps:

Before the Logical Volume Manager can be configured, the disk partition tables of the following devices are changed: SCSI 2 (0,0,0) (sda). Write the changes to disks and configure LVM?

- [x] No
- [ ] Yes

![](img/863afa537de4eed7deb11978bfbfa90e_58_0.png)

![](img/863afa537de4eed7deb11978bfbfa90e_59_0.png)

*Figure 2.10/2.11: Partition disks*

### Install the base system and install software

After the partition process, the installer will install the base system in the disk, and partitions will be configured. In this step, the Linux kernel, the system tools, libraries, and services will be installed and configured. When the installation of the minimal required packages for the base system is completed, it is possible to scan extra installation media or skip that process. Then it is needed to configure the package manager specifying the mirror country for Debian archive files and the server to be used. The following figures show the steps to configure it:

![](img/863afa537de4eed7deb11978bfbfa90e_60_0.png)

![](img/863afa537de4eed7deb11978bfbfa90e_61_0.png)

If a proxy is needed to access the internet repository, the installer provides the option to specify an HTTP proxy and, if needed, the username and password to use it. The installer will retrieve the package list from the server repository, and it will continue with the installation of the base system. After the core of the system is selected, the installer gives the option to specify the software to be installed during the process, as is shown in the following figure:

![](img/863afa537de4eed7deb11978bfbfa90e_62_0.png)

Figure 2.14: Software selection

### Install the GRUB boot loader

After the base system and the software selected are installed, the last step of the installation is to install the boot loader on the disk. **Grand Unified Bootloader (GRUB)** is the boot loader predominant in Linux systems. The following figure shows the confirmation step:

![](img/863afa537de4eed7deb11978bfbfa90e_63_0.png)

Figure 2.15: Install the GRUB boot loader

After the acceptance of the installation of GRUB, a list of devices and partitions will be listed to confirm where the bootloader will be installed. The installation will be completed, and the system can be rebooted to the new system, ensuring the media installation is removed to boot from the local disk.

Booting the system will show the GRUB menu, where it is possible to boot to Debian, to different distributions (if they are installed in different partitions), or start Debian in a recovery mode or with different kernel versions (Advanced Options).

## Ubuntu server

Ubuntu is the most popular distribution for Desktop. It uses the same package manager (dpkg) as Debian. Ubuntu offers a faster release lifecycle compared with Debian, having the latest version of the software available. The canonical company, the publisher of Ubuntu, offers commercial support as described previously.

Ubuntu offers distribution variants through the official URL https://ubuntu.com/download/, including the following options:

- **Ubuntu Desktop**: This variant is the most popular for PCs and laptops, offering guaranteed support for five years with free security and maintenance updates.
