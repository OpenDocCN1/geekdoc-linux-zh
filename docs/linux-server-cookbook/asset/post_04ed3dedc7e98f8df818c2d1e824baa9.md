
- **Ubuntu Pro:** This variant is optimized and certified for cloud providers such as Amazon AWS, Microsoft Azure, Google Cloud Platform, IBM Cloud, and Oracle.
- **Ubuntu Core:** This option is optimized for Internet of Things (IoT) and the Edge.
- **Ubuntu Server:** Supported as described previously for 10 years. Used to be installed in private or public data centers and supporting multiple architectures.

### Installation menu

The first screen appearing when the server is booting from the Ubuntu installer image starts the installation or tests the memory of the system. Ubuntu Server does not include a graphical user interface for the installation. The following figure shows the first screen of the installer:

![](img/863afa537de4eed7deb11978bfbfa90e_64_0.png)

*Figure 2.16: Ubuntu installation menu*

### Select installation language

After specifying the option to *Install Ubuntu Server*, the installer will move to the next step to specify the language for the installation.

### Keyboard configuration

The next step in the installation process is to specify the keyboard configuration: the layout and the variant.

## The base for the installation

After specifying the layout and the variant, the installer wizard shows the types of possible installation options for Ubuntu Server: default installation or minimized (used where users are not expected to log in to the system). The following screenshots show the options and the descriptions:

![](img/863afa537de4eed7deb11978bfbfa90e_65_0.png)

*Figure 2.17: Choose the type of install*

## Network connections

The following step is the network configuration. If DHCP is used, the IP assigned will be shown. In case of no DHCP, a manual configuration of the IP is required to access the repositories. In this step, it is possible to configure a bonding interface. The following figure shows an example of a network automatically configured with DHCP:

![](img/863afa537de4eed7deb11978bfbfa90e_65_1.png)

*Figure 2.18: Network connections*

After configuring the network interfaces, it is possible to configure the proxy to access the internet if it is needed.

## Configure the Ubuntu archive mirror

An archive mirror is a Web server containing the packages to be used for the installation and to install software after the system is installed. The installer will detect automatically, based on the system location, the closest archive mirror URL, allowing the user to specify an alternative one.

### Guided storage configuration

Ubuntu installer permits specifying how the storage would be configured if using a guided storage layout or creating a custom one. It is also possible to specify if the system uses Logical Volume Manager (LVM), what is selected by default, and if LVM would be encrypted with Linux Unified Key Setup (LUKS). The following figure shows an example of this step:

![](img/863afa537de4eed7deb11978bfbfa90e_66_0.png)

*Figure 2.19: Guided storage configuration*

After selecting the guided option and LVM, the next step will show the partition layout that will be applied to the disk. It is also possible to personalize the partitions to be created, the mount point, the sizes, and the names for logical volumes. The following figure shows a default partitioning:

![](img/863afa537de4eed7deb11978bfbfa90e_67_0.png)

*Figure 2.20: Storage configuration*

### Profile setup

After the disk layout is confirmed, the next step is related to the creation of a new user specifying the name, the username, and the password. The name of the server will also be specified in this step. The following figure shows the fields required to fill:

![](img/863afa537de4eed7deb11978bfbfa90e_67_1.png)

*Figure 2.21: Profile setup*

### SSH setup

The installer will ask if the OpenSSH server will be installed and enabled to be administered remotely. If the system is not a local system, it is recommended to enable this so that it can be administered remotely.

## Featured server snaps

Snap is a software packaging and deployment system developed by Canonical. The snaps are self-contained applications, including the needed libraries to run the service or application. Working with snaps, there are four important concepts: **snap** is the application package format and the command to execute the applications; **snapd** is the background service to manage and maintain; **snapcraft** is used to create customized applications and a marketplace for the snaps; and finally, **Snap Store** ([https://snapcraft.io/store](https://snapcraft.io/store)). The following figure shows some of the available snaps:

![](img/863afa537de4eed7deb11978bfbfa90e_68_0.png)

After selecting, if some of the Snaps are needed, the installation will start downloading and installing security updates. When the installation has finished it is possible to review the full log of the installation process or reboot the system to boot the Ubuntu server installed on the disk.

Ubuntu Server installation, as observed, does not set the root password; it creates a user and sets the permissions in the system for that user to use *sudo* for administrative tasks. After the system is rebooted, it is possible to login with the user created during the installation.

## Red Hat Enterprise Linux

Red Hat Enterprise Linux is the world's leading enterprise Linux platform, widely used in data center infrastructures, virtualization, and containers. As described previously, RHEL is a commercial open-source Linux distribution developed and supported by Red Hat for the commercial market.

RHEL uses **RPM Package Manager (RPM)** for package management, and this system is used in many distributions, such as CentOS, Fedora, Oracle Linux, AlmaLinux, or Rocky Linux.

Installation images for Red Hat Enterprise Linux are available on the website: [https://access.redhat.com/downloads/](https://access.redhat.com/downloads/). A subscription is required to access the repositories, with the option to request a no-cost Red Hat Developer subscription if the purpose is for development or a 60-day trial is available to try RHEL before buying the subscription.

RHEL offers three images for the installation:

- **Binary DVD:** It includes all required packages without the need for any additional repository. Useful when there is no internet access.
- **Boot ISO:** This image has the basic packages for the installation but requires an active network connection to access additional package repositories.
- **KVM Guest Image:** Used for KVM/QEMU hypervisor, such as Red Hat OpenStack (or community OpenStack) or Red Hat Virtualization (or oVirt project).

### Installation menu

The first screen that appears when the server is booting from the Red Hat Enterprise Linux installer image allows us to install and test the media or perform troubleshooting. The following figure shows the first screen of the installer:

![](img/863afa537de4eed7deb11978bfbfa90e_70_0.png)

*Figure 2.23: RHEL installation menu*

Selecting the Graphical install entry in the menu will move the installer to the next step as a continuation is shown.

### Select a language

The first step after specifying which installation user interface would be used is to specify the language to be used during the installation process. This language will be used as well as the default language once the system is installed.

### Installation summary

After choosing the language, the installer shows a dashboard with the configuration requirements before starting the installation. Some configurations are detected automatically (that is, the network configuration and the installation source), and another configuration is required to specify manually (registration, disk partition, and user passwords). An example of the dashboard is shown in the following figure:

![](img/863afa537de4eed7deb11978bfbfa90e_71_0.png)

*Figure 2.24: Installation dashboard*

The steps required in this step are as follows:

1. Connect to Red Hat with the username/password for the subscription required.
2. Confirm the disk to be used for the installation and the partitioning desired.
3. **Software selection:** specify which software will be installed in the system.
4. Set the password for the root user.
5. Create a regular user.

Other options possible to configure are as follows:

- Network configuration.
- Configure the Keyboard layout.
- Configure the time zone, time, and date.
- Other options such as kernel dump (kdump) and security profile.
