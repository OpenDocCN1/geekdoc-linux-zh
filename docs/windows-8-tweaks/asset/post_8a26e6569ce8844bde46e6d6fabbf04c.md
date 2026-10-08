
## Installing from USB

The Windows 8 retail versions include installation software on a DVD. That works fine for the majority of users, but it is a big problem for those who own laptops, tablets, or other computers without optical drives. If you don’t have an optical drive on your computer, you need to take some extra steps to install Windows 8.

A few solutions to this problem exist, such as PXE (Preboot Execution Environment) network booting to a Windows Deployment Server (a feature of Windows Server 2008 and newer). However, the most popular and easiest to configure is a bootable USB flash drive. This is my personal preference as well, because installing Windows 8 from a USB flash drive is actually much faster than installing from a DVD.

You need a 4 GB USB flash drive to have enough space to fit the entire Windows 8 installation code on the drive. I found that the 4 GB SanDisk Cruzer works well for booting the Windows 8 installation code and seems to be compatible with a wide range of computers. However, just about any 4 GB USB flash drive should work these days.

If you have physical media rather than a digital download ISO file, the instructions for creating boot media are slightly different. Follow the instructions relevant for your situation.

### Creating the USB Boot Media from a Physical DVD

This section is pertinent if you have access to a Windows PC, XP or newer, because you need DiskPart to be able to create the USB boot media.

Before you begin it is important to understand that any data on your USB flash drive used to create the boot media will be permanently deleted because the process reformats the drive. Save any important documents to another location before proceeding to the next section.

#### Preparing the USB Flash Drive

The partitioning and filesystem on the USB flash drive are important for booting. Only one partition can be on the device, it must be set to active, and the filesystem must be FAT32. Many computers with the new UEFI BIOS replacement have problems booting USB flash devices with any filesystem other than FAT32. Insert the drive into a Windows computer and follow these steps:

- 1. After the drive has been recognized and installed on the computer, click the Start button, type **DiskPart**, and hit Enter.
- 2. In the DiskPart window, type **list disk** and hit Enter as shown in Figure 2-1.
- 3. Locate the Disk # of your USB flash drive. You can easily find it by looking at the size column. Once you have the ID, type **select disk #** and hit Enter. (Replace # with the actual disk ID, such as 1.)
- 4. Type **clean** and hit Enter to destroy any partitions, file systems, and data that may currently be on the device.
- 5. Now it is time to create the partition. Type **create partition primary** and hit Enter.
- 6. For booting it is important to set the partition as active. Type **active** and hit Enter.
- 7. As I mentioned earlier, the filesystem must be FAT32. Type **format fs=fat32 label=win8boot quick** and hit Enter. This performs a quick format and labels the drive in one step.
- 8. Type **exit** to close DiskPart. Your USB flash drive is now prepared for the next phase.

![](img/ea75090cfee8ac890f64c8c4f62f7285_37_0.png)

### Copying the Installation Software

The final step, now that you have your USB flash drive prepared, is to copy the code. If you are a super geek you can use some fancy xcopy or robocopy commands for this step, but this simple copy-and-paste procedure works just fine.

Insert the DVD media into your PC and navigate to the drive on your computer that has the Windows 8 installation files. Select all the files, as shown in Figure 2-2, and then right-click and select Copy.

Navigate to the root of the USB flash drive, right-click and click Paste. The file copy can take a number of minutes, but after it is finished you can install Windows 8 quickly and on machines that don't have an optical drive.

![](img/ea75090cfee8ac890f64c8c4f62f7285_38_0.png)

**Figure 2-2:** Copying all Windows 8 installation source files

### Creating the USB Boot Media from a DVD Image

Different from a physical DVD, a DVD image or ISO file is what you get when you buy Windows 8 directly from Microsoft and digitally download your purchase. You can also get an ISO file for Windows 8 if you are an MSDN or TechNet subscriber or are a volume license enterprise customer.

You could follow an altered version of the instructions for a physical DVD, but there is a much better method using a free utility provided by the Microsoft Store. The utility is called the Windows 7 USB/DVD Download Tool, but it works fine with Windows 8 ISO images as well.

Simply download and install the free utility from the Microsoft Store by visiting [http://tweaks.com/935795](http://tweaks.com/935795). Once installed, launch the utility from the Start menu:

- 1. Plug your USB flash drive into your computer.
- 2. Click Browse and select your Windows 8 ISO file. Then click Next as shown in Figure 2-3.
- 3. On the Choose Media Type screen, choose USB device.
- 4. Select your USB device from the list and click Begin Copying, as shown in Figure 2-4.

When this completes, you have a fully functional Windows 8 USB flash drive that you can use to install Windows on just about any device much more quickly than you can when using a DVD.

![](img/ea75090cfee8ac890f64c8c4f62f7285_39_0.png)

![](img/ea75090cfee8ac890f64c8c4f62f7285_39_1.png)

## Understanding the Install Process

You have two primary options for installing any edition of Windows 8 on a PC that already has a version of Windows installed:

- Upgrading your install
- Using a clean install

The upgrade install has come a long way since the XP days. These days it essentially performs a clean install, but then applies your configuration and personalized settings from the old operating system. Applications transfer over only if you upgrade from Windows 7. All earlier versions require you to reinstall your applications.

The clean install is the purest method of installing Windows 8. Users are advised to back up their important data to an external hard drive and then delete the contents of the operating system drive. This allows the installer to install Windows 8 without any legacy settings, applications, or files getting pulled along for the ride.

Each install method has many pros and cons, and I cover those in the next two sections.

## Using the Upgrade Install Process

Upgrade installs are easier to implement than clean installs are, but many negative aspects to them will haunt you in the long run. The process works as follows: You launch the installer on a machine that has a previous version of Windows installed. The installer lets you know which of your apps are compatible. You will then have the option to stop the upgrade and remain on your current version of Windows or continue the upgrade and a while later you have Windows 8 PC. Most of the same settings and applications that were on the previous version of Windows will have transferred over flawlessly.

That is how the process works in a perfect world. In reality, it rarely goes that well. I have seen a significant number of technical issues on Windows 8 attributed to users who upgraded from a previous version of Windows. What is most impressive is that most issues went away when users did a clean install.

Microsoft has some smart people working on the upgrade process, and they have been working on this for decades. But the process rarely works well because the idea is flawed. Why would you ever want to carry over all of your Windows settings, applications, and junk that has accumulated on your old PC to a brand new PC? This is like buying a new car and then bolting on parts from your old car.

The underlying system has changed. Take the time to reinstall your applications and settings after a clean install. You will be rewarded with a Windows 8 PC that runs at top speed and suffers from far fewer issues over time.

## Using the Clean Install Process

The best way to install Windows 8 is with a clean install. This wipes your computer of all installed applications and data, but is worth it in the long run. Additionally, many applications have been updated to work better on Windows 8 and take advantage of the new features, so it is best to update and install new versions, anyway.

To get started with the clean install process, follow these steps:

- 1. Insert the installation DVD or USB flash drive you created into your computer. Then reboot and select the boot menu key for your computer. On mine, I press F12 and then select the device I want to boot to, as shown in Figure 2-5. If you are using a DVD, make sure to hit any key after you see the message “Press any key to boot from CD or DVD” on your screen.

![](img/ea75090cfee8ac890f64c8c4f62f7285_41_0.png)

**Figure 2-5**: Select the device to boot to from the PC Boot menu.

- 2. A progress bar displays at the bottom of the screen followed by the Windows logo. On the next screen, make sure the language, time and currency format, and keyboard are set properly. Hit Next when ready, as shown in Figure 2-6.
- 3. On the next screen, click Install Now.
- 4. If you are using Windows 8 or Windows 8 Pro edition media, you must enter a product key as shown in Figure 2-7 and then click Next. The product key that you provide determines whether Windows 8 or Windows 8 Pro is installed. If you are using Windows 8 Enterprise edition media, you aren’t prompted for a product key and can skip this step.
