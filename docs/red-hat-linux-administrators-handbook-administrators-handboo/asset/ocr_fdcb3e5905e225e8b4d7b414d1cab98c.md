method. The available options are Local CD-ROM, NFS Image, hard drive, FTP, and SMB image. Because you are going to do a CD-ROM installation, press the Enter key to start the actual installation process.

# Deciding whether to do a new installation or an upgrade

The next screen asks you to choose between a new installation or an upgrade.

If you are installing Red Hat Linux for the first time, choose the Install option; conversely, if you plan to upgrade an existing Red Hat system, choose the Upgrade option. The difference is that the upgrade process will upgrade only your existing kernel and software packages and will not allow you to add new packages. This discussion assumes that you are installing for the first time; hence, choose the Install option to continue.

# Choosing an installation class

The installation program offers you three installation class options:

+   - **Workstation.** Choose this option if you plan to use the Red Hat Linux system as a personal workstation computer. This option allows the installation program to remove all of your existing Linux partitions and use the entire unpartitioned disk space to create a preconfigured system. The Workstation class system typically has a small swap partition (32MB) and a 16MB /boot partition for kernel and related files. The rest of the unpartitioned disk space is used to create a single / (root) partition. Typically, you should have at least 600MB of disk space for a Workstation class installation.
+   - **Server.** Choose this option to create a server system. It uses a 64MB swap partition, a 16MB /boot partition for kernel and related files, a 256MB / (root) partition, a 512MB (or more) /usr partition for storing commonly used applications and utilities, a 512MB (or more) /home partition for user home directories, and a 256MB /var partition for system logs and queues. You should have approximately 1.6GB of disk space for such a system.
+   - **Custom.** Allows you to choose whatever partitioning you want using partitioning tools and therefore is the most flexible.