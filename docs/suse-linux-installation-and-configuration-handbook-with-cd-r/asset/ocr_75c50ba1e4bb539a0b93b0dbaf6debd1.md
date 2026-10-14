# Preparing Yourself

In this section, you will learn some conventions you might encounter during the installation process. Bear in mind that YaST2 gives you the option of Automatic Installation in which you won't have to suffer the pain of navigating new territory. However, if you install SuSE Linux through the Guided Installation option when installing using YaST2 or if you are planning to use YaST, you will have to learn some of the conventions in this section.

# Multiuser Environment

SuSE Linux is a multiuser environment. In a multiuser environment, the system can be used and shared by many users while retaining the settings each user has configured for herself. If the machine on which SuSE Linux will be installed is on a network, users can connect to the SuSE Linux box through many networking facilities provided by SuSE Linux. The space provided to each SuSE Linux user is located in the /home/username directory. No normal user can control system settings or alter system configurations unless allowed to by the system's top-level user, called root. The root user is the default user for the system and can control and set up the system. Because you will be installing SuSE Linux, you will be root during the installation process. You should not use the system as root after you have installed it. You should log in as the root user only when you are modifying the system settings.

Each user on the SuSE Linux system has a username and password. During the installation process, you will be asked to enter the root password. You should enter a password that is not easy to guess and that you will not forget. You also will be prompted to create a new user for the system. You should create this user so you can log in to your system as a normal user, not as root.

# Disk Partitions in SuSE Linux

Disk partition naming in SuSE Linux has a completely different convention from that of MS-DOS or MS Windows. There is nothing called C: or D: for disks. Rather, there are mount points and a filesystem. The filesystem is made up of the physical devices, such as hard disk partitions, floppy disks, CDs, zip drive disks, and so forth. Alternatively, a mount point is a directory in which you mount those filesystems. A mount point makes the connection between you and the physical device.

In addition, you still can arrange your files in directories. Note that your only restriction is that all your directories will reside in /home/<username>. No other user on the system will be able to see your files unless you allow him to.

During the installation, you will be asked where to install SuSE Linux. Table 2.1 details the mapping you can use to understand the filesystems about which YaST or YaST2 will ask you.