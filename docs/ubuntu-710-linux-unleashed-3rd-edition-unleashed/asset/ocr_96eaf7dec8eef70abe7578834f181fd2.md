knowledge will help you make the most out of hard drive space; and in some instances, such as planning to have user directories mounted via NFS or other means, can help head off data loss, increase security, and accommodate future needs. Create a great system, and you'll be the hero of information services.

To plan the best partitioning scheme, research and know the answers to these questions:

+   - How much disk space does your system require?
+   - Do you expect your disk space needs to grow significantly in the future?
+   - Will the system boot just Ubuntu, or do you need a dual-boot system?
+   - How much data will require backup, and what backup system will work best? (See Chapter 13, “Backing Up” for more information on backing up your system.)

# CD-ROM Installation Jump-Start

To install Ubuntu from the disc included with this book, you must have at least a Pentium-class CPU, 3GB of hard drive space, and 256MB RAM. Most modern systems have significantly larger drives, and it is an idea to invest in more storage from your local computer store.

To begin the installation, you need to get into your computer’s BIOS to set the boot sequence so that the CD/DVD drive is the first drive that is booted. Insert the DVD into the drive and let the system boot. When the menu appears, press the Enter key to boot into Ubuntu Live.

Double-click the Install icon on the desktop and follow the instructions. When the installer finishes, choose to restart the system immediately; eventually, the disc ejects, and Ubuntu starts to boot. After a few seconds, the login window appears. Enter the username and password specified during the installation. Welcome to Ubuntu!

# The Boot Loader

During installation, Ubuntu automatically installs GRUB (Grand Unified Boot Loader) to the Master Boot Record (MBR) of your hard drive. Handily enough, it also detects any other operating systems such as Windows and adds entries in GRUB as appropriate. If you have a specific requirement not to install GRUB to the MBR, you need to install using the Alternate disc, which will allow you to specify the install location for GRUB.

# Installing from CD or DVD

Most PCs’ BIOS support booting directly from a CD or DVD drive, and enable you to set a specific order of devices (such as floppy, hard drive, CD-ROM, or USB) to search for bootable software. Turn on your PC and set its BIOS if required (usually accessed by pressing a Function or Del key after powering on); then insert your Ubuntu disc and boot to install Ubuntu.