# PERFORMING A NetWARE 6.5 INSTALLATION

The NetWare 6.5 OS comes on two CDs: Operating System CD 1 and Products CD 2. Operating System CD 1 is bootable and contains the files needed for the initial installation and pattern selection phases. Before starting the installation, you need to make sure your existing network and server are configured correctly. The following sections describe the steps for preparing your existing network and server and performing the actual NetWare 6.5 installation.

# Upgrade an Existing eDirectory Network

If you're planning to install NetWare 6.5 into an existing eDirectory tree, you need to use NetWare Deployment Manager (Nwdeploy.exe) to ensure that the existing eDirectory tree is updated to version 8.6. For example, Eric performed the following procedure to prepare the UAS eDirectory tree for NetWare 6.5:

+   1. First, Eric installed Novell Client on his Windows XP Professional computer, as described in Chapter 4.

+   2. Next, he inserted the NetWare 6.5 Operating System CD 1 into the CD-ROM drive to start NetWare Deployment Manager automatically. (You can also start this software by running Nwdeploy.exe from the root of the NetWare 6.5 Operating System CD 1.)

+   3. When NetWare Deployment Manager started, he viewed the tasks required for the upgrade process by double-clicking the Network Preparation folder and reading the Overview section.

+   4. He then backed up the existing NetWare server and eDirectory data by following the instructions in the Back Up Data section.

+   5. After the backup was finished, Eric updated eDirectory by selecting the View and Update eDirectory Version option.

+   6. To complete the upgrade, Eric extended the eDirectory tree structure by selecting the Prepare for eDirectory option. (You learn more about upgrading eDirectory in Chapter 4.)

After Eric completed the upgrade, the existing eDirectory tree was ready to receive the new NetWare 6.5 server installation, as described in the following sections.

# Prepare the Server

Preparing the server starts with verifying that the hard drive has no existing partitions. You can do this by booting the computer from a DOS disk and then running the Fdisk program to display any existing partitions. If your system contains existing partitions, use Fdisk to delete these partitions before starting the installation. You can also use a live or runtime version of Windows or Linux to initialize the hard drive.

After ensuring that your hard drive is empty, the next step is to determine the NetWare 6.5 installation startup method. If your computer will boot from the CD-ROM drive, you should use your CMOS Setup program to ensure that the system is set to boot from the CD-ROM drive first. If your system does not boot from the CD, you can create a DOS bootable disk that contains the CD drivers, and then start the NetWare 6.5 installation by using the DOS boot disk as described in the following steps:

+   1. Create a DOS bootable disk.

+   2. Install the DOS CD driver for your CD-ROM drive on the bootable disk.