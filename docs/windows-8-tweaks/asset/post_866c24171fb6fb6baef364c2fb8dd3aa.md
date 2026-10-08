
![](img/ea75090cfee8ac890f64c8c4f62f7285_42_0.png)

Figure 2-6: Check the Windows 8 Install regional settings.

![](img/ea75090cfee8ac890f64c8c4f62f7285_42_1.png)

Figure 2-7: Insert the product key.

5. Click I Accept The License Terms and then click Next.

6. On the next screen you can select either the Upgrade or Custom install. Don't even think about it; click Custom to perform a clean install as shown in Figure 2-8.

![](img/ea75090cfee8ac890f64c8c4f62f7285_43_0.png)

**Figure 2-8:** Choose Custom for a clean install.

7. The last manual step of the install is to select the drive to which you want to install. After I copy my data to a backup drive, I like to delete all the partitions on the drive on which I will be installing Windows 8. You can do this by selecting the partition and then clicking Drive Options. Then just click Delete. Repeat for the other partitions on the drive, select the Unallocated Space, and then click Next, as shown in Figure 2-9. This partitions and formats the drive automatically, and Windows begins to install.

Setup is now fully automated. Files are copied to the destination drive and the computer reboots a few times. When the install is finished the computer restarts, and after booting up asks you for your username, computer name, password, and other first-run information. Congratulations, Windows 8 is now installed and ready for tweaking.

![](img/ea75090cfee8ac890f64c8c4f62f7285_44_0.png)

**Figure 2-9:** Select where to install Windows 8.

## Dual-Booting Windows

With virtualization becoming more popular, the need to run multiple operating systems on a physical computer has significantly decreased. Application compatibility was the main reason in the past that users installed multiple operating systems. Your old Windows XP applications will not function in Windows 8? Just restart and boot into Windows XP. Virtual machine applications such as VMware Workstation, Sun VirtualBox, and Microsoft Hyper-V enable you to boot the second operating system on top of your main OS, eliminating the need and hassle of rebooting into another OS. This solves the compatibility problem for most apps, but a virtual machine is not always perfect.

Gaming is one area where problems may arise for virtual machines because 3-D support has gotten a lot better, but it’s not yet at bare metal performance. If you are a gamer or just want a cool way to try out Windows 8 with bare metal performance, I show you how you can dual-boot Windows 7 and Windows 8 on the same PC with a geeky twist.

You can achieve a dual-boot system with Windows 7 and Windows 8 in a number of ways, but the easiest and least destructive method is to have Windows 7 installed first. Then, using a little-known feature in Windows 7 called boot to VHD (virtual hard drive file), you can install Windows 8 in a VHD file, which is very safe because you don't need to alter your Windows 7 partition or install. When you are finished, the Windows 8 drive will be virtualized into a single file on your Windows 7 partition and will show up in the boot menu just as if it was installed on raw disk.

### Creating the VHD File on Windows 7

The first step to dual-booting Windows 8 and Windows 7 is to create the VHD file to hold the Windows 8 installation. Open up Disk Management on Windows 7 to create the file:

- 1. Click the Start button in Windows 7, type in **diskmgmt.msc**, and hit Enter. The Disk Management utility should load.
- 2. Click the **Action** menu and select **Create VHD**.
- 3. Enter a location, such as `C:\VHD\Win8.vhd`. Set the size—I suggest 40 GB—and select the Dynamically expanding format to save your disk space. Dynamic VHD files start out small and only grow with data written to the virtual disk. When your screen looks like Figure 2-10, click OK and the file is created.

![](img/ea75090cfee8ac890f64c8c4f62f7285_45_0.png)

### Installing Windows 8 to a VHD

Proceed to install Windows 8 using the clean install process covered earlier, but stop at the screen that asks “Where do you want to install Windows?” as shown in Figure 2-9. You need to attach the VHD file to the installer so that it recognizes it as a valid location to install Windows 8.

- 1. Hit Shift + F10 on your keyboard to bring up a Command Prompt window.
- 2. Type **diskpart** and hit Enter.
- 3. Now it is time to select the VHD file you created earlier. You need to know the full path to the VHD file. Keep in mind that a properly installed Windows 7 machine has two primary partitions: one hidden partition for the boot and recovery tools and a separate partition for the operating system. When Windows is running, it hides the hidden boot partition and gives the second OS partition the C drive letter. When the installer is running, the boot partition is not hidden, and therefore is given the C drive letter and the second OS partition is given the D drive letter. If the VHD file was created in `C:\VHD\Win8.vhd` while Windows 7 was running, you need to use `D:\VHD\Win8.vhd` as the full path to the VHD file while the installer is running. Run the following command with the adjusted path to the VHD file and then hit Enter:

```
select vdisk file=d:\vhd\win8.vhd
```

- 4. Type **attach vdisk** and hit Enter.
- 5. Close the Command Prompt window and click the Refresh button on the Where Do You Want To Install Window? screen.
- 6. Select the new 40 GB VHD drive now listed as Drive 1 and click Next as shown in Figure 2-11. Ignore any warnings saying Windows can’t be installed on that drive. They are incorrect, as the installer is not aware of this advanced method of installing Windows 8.
- 7. Now just continue to install Windows 8 as usual. The next time your PC reboots, you see a new boot menu that enables you to select between Windows 7 and Window 8, as shown in Figure 2-12.

![](img/ea75090cfee8ac890f64c8c4f62f7285_47_0.png)

Figure 2-11: You can install Windows 8 to a virtual hard drive.

![](img/ea75090cfee8ac890f64c8c4f62f7285_47_1.png)

Figure 2-12: Choose between Windows 7 and 8 in the Windows 8 boot menu.

## Using Windows To Go

New to Windows is a feature called the Windows To Go workspace, which is found only in the Enterprise edition of Windows 8. Instead of providing employees a desktop or laptop, let them use their own hardware and provide them with a bootable USB flash drive that contains their corporate desktop. They can take the Windows To Go workspace anywhere and can use it on just about any computer. Just plug it in and boot up the workspace.

As you can imagine, running Windows from a USB flash drive can be very slow if you don't have a fast device. In my testing, all USB 2.0 flash drives are completely useless, unless you don't mind a 20-minute boot time. In fact, Microsoft recommends using only USB 3.0 flash drives that are certified for Windows To Go. Microsoft specifically recommends three devices:

- Kingston DataTraveler Workspace
- Super Telen Express RC8
- Western Digital My Passport Enterprise

The Western Digital option is actually an external USB 3.0 hard drive, so in theory you can also use USB hard drives.

Beyond the performance of the device Microsoft also requires the ability to create multiple partitions on it. That requires a special controller that is rarely found on USB flash drives these days. Your best bet is to stick with USB 3.0 drives that are certified for Windows To Go.

## Why Enterprises Only?

I mentioned earlier that Windows To Go is found only in the Enterprise edition of Windows 8. The reason for that is all about product activation. By now you should know that every version of Windows made in the past decade requires Internet activation of some kind. The activation of Windows is based on the unique hardware makeup of your PC. If you rip out your hard drive and install it in another PC, Windows 8 boots up but you need to reactivate it.

The same thing happens to you if you're using Windows To Go. Every different machine you boot up on requires activation. Even if you go back to a machine you used in the past, it still requires reactivation. Because consumer product keys can be activated only a few times before they stop working, reactivating all the time is just not feasible.

Enterprise customers of Windows 8 typically use a different type of product activation. This activation uses what is called a *Key Management Service* (KMS) that is installed on a Windows server inside the corporate network. You can
