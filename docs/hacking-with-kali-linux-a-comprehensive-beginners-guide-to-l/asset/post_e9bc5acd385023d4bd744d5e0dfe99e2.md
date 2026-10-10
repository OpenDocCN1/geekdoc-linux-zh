
## CHAPTER 2
## HOW TO INSTALL THE KALI LINUX AND HOW TO MAKE A KALI BOOTABLE USB DRIVE

At times, we have sensitive data; we would prefer to encrypt using full disk encryption. With the Kali Installer, you can initiate an LVM encrypted install on either Hard Disk or USB drives. The installation procedure is very similar to a “normal Kali Linux Install,” except for choosing an Encrypted LVM partition during the installation process.

### Kali Linux Encrypted Installation Requirements

Installing Kali Linux on your computer is a natural process. First, you’ll need compatible computer hardware. The hardware requirements are minimal, as listed below, though the better device will naturally provide better performance. The i386 images have a default PAE kernel so that you can run them on systems with over 4GB of RAM. Download Kali Linux and either burn the ISO to DVD or prepare a USB stick with Kali Linux Live as the installation medium.

### Installation Prerequisites

- A minimum of 20 GB disk space for the Kali Linux install.
- RAM for i386 and amd64 architectures, minimum: 1GB, Recommended: 2GB or more.
- CD-DVD Drive / USB boot support

### Preparing for the Installation

- Download Kali Linux.
- Burn The Kali Linux ISO to DVD or Image Kali Linux Live to USB.
- Ensure that your computer is set to boot from CD / USB in your BIOS.

### Kali Linux Installation Procedure

To start your installation, boot with your chosen installation medium. It would be best if you were greeted with the Kali Linux boot menu. Choose a Graphical or a Text-Mode install. In this example, we decided on a GUI install.

Select your preferred language, and then your country location. You’ll also be prompted to configure your keyboard with the appropriate keymap.

The installer will copy the image to your hard disk, probe your network interfaces, and then prompt you to enter a hostname for your system. In the example below, we’ve entered "kali" as the hostname.

Enter a robust password for the root account.

Next, set your time zone.

The installer will now probe your disks and offer you four choices. For an Encrypted LVM install, choose the "Guided – use entire disk and set up encrypted LVM" option as shown below.

Choose the destination drive to install Kali. In this case, we chose a USB drive destination. We will use this USB drive to boot an encrypted instance of Kali.

Confirm your partitioning scheme and continue the installation.

Next, you will be asked for an encryption password. You will need to remember this password and use it each time to boot the encrypted instance of Kali Linux.

Configure network mirrors. Kali uses a central repository to distribute applications. You’ll need to enter any appropriate proxy information as required.

NOTE! If you select "NO" on this screen, you will NOT be able to install packages from the Kali repositories.

Next, install GRUB.

Finally, click Continue to reboot into your new Kali installation. If you used a USB device as a destination drive, make sure you enable booting from USB devices in your BIOS. You will be asked for the encryption password you set earlier on every boot.

## HOW TO MAKE A KALI BOOTABLE USB DRIVE

### Making a Kali Bootable USB Drive

Our fastest method and the most favorite method of getting up and running with Kali Linux is to run it “live” from a USB drive. This method has several advantages:

- It’s non-destructive — it makes no changes to the host system’s hard drive or installed OS, and to go back to normal operations, you remove the “Kali Live” USB drive and restart the system.
- It’s portable — you can carry Kali Linux in your pocket and have it running in minutes on an available system.
- It’s customizable — you can roll your custom Kali Linux ISO image and put it onto a USB drive using the same procedures.
- It’s potentially persistent — with a bit of extra effort, you can configure your Kali Linux “live” USB drive to have persistent storage, so the data you collect is saved across reboots.

To do this, we first need to create a bootable USB drive, which has been set up from an ISO image of Kali Linux.

### What You’ll Need

A verified copy of the appropriate ISO image of the latest Kali builds a model for the system you’ll be running it on: see the details on downloading official Kali Linux images.

If you’re running under Windows, you’ll also need to download the Win32 Disk Imager utility. On Linux and OS X, you can use the dd command, which is pre-installed on those platforms.

A USB thumb drive, 4GB or more substantial. (Systems with a direct SD card slot can use an SD card with a similar capacity. The procedure is identical.)

### Kali Linux Live USB Install Procedure

The specifics of this procedure will vary depending on whether you’re doing it on a Windows, Linux, or OS X system.

#### Creating a Bootable Kali USB Drive on Windows

Plug your USB drive into an available USB port on your Windows PC, note which drives designator (e.g., “F:\”) it uses once it mounts, and launch the Win32 Disk Imager software you downloaded.

Choose the Kali Linux ISO file to be imaged and verify that the USB drive to be overwritten is the correct one. Click the “Write” button.

Once the imaging is complete, safely eject the USB drive from the Windows machine. You can now use the USB device to boot into Kali Linux.

#### Creating a Bootable Kali USB Drive on Linux

Creating a bootable Kali Linux USB key in a Linux environment is comfortable. Once you’ve downloaded and verified your Kali ISO file, you can use the dd command to copy it over to your USB stick using the following procedure. Note that you’ll need to be running as root, or to execute the dd command with sudo. The following example assumes a Linux Mint 17.1 desktop — depending on the distro you’re using, a few specifics may vary slightly, but the general idea should be very similar.

WARNING: Although the process of imaging Kali Linux onto a USB drive is straightforward, you can just as easily overwrite a disk drive you didn’t intend to with dd if you do not understand what you are doing, or if you specify an incorrect output path. Double-check what you’re doing before you do it, it’ll be too late afterward.

Consider yourself warned.

First, you'll need to identify the device path to use to write the image to your USB drive. Without the USB drive inserted into a port, execute the command:

```
sudo fdisk -l
```

At a command prompt in a terminal window (if you don't use elevated privileges with fdisk, you won't get any output). You'll get output that will look something (not exactly) like this, showing a single drive — “/dev/sda” — containing three partitions (/dev/sda1, /dev/sda2, and /dev/sda5):

Now, plug your USB drive into an available USB port on your system, and run the same command, “sudo fdisk -l” a second time. Now, the output will look something (again, not exactly) like this, showing an additional device which wasn't there previously, in this example “/dev/sdb,” a 16GB USB drive:

Proceed to (carefully!) image the Kali ISO file on the USB device. The example command below assumes that the ISO image you're writing is named “Kali-Linux-2017.1-amd64.iso” and is in your current working directory. The blocksize parameter can be increased, and while it may speed up the operation of the dd command, it can occasionally produce unbootable USB drives, depending on your system and a lot of different factors. The recommended value, “bs=512k”, is conservative and reliable.

```
dd if=kali-Linux-2017.1-amd64.iso of=/dev/sdb bs=512k
```

Imaging the USB drive can take a good amount of time, over ten minutes or more is not unusual, as the sample output below shows. Be patient!

The dd command provides no feedback until it completed, but if your drive has an access indicator, you'll probably see it flickering from time to time. The time to dd the image across will depend on the speed of the system used, USB drive itself, and USB port it's inserted into, and once dd has finished imaging the drive, it will output something that looks like this:

```
5823+1 records in
5823+1 records out
```
