
![](img/ea75090cfee8ac890f64c8c4f62f7285_68_0.png)

3. When the command prompt loads, run the following command to create a backup of your entire Windows 8 install:

`wbadmin start backup -allCritical -backupTarget:d:`

Replace d: with the drive letter where you want your backup to be stored. It can be the drive letter of any drive in your PC or connected via USB, but cannot be the drive that you are backing up.

You can also replace d: with a UNC network path. For example:
`wbadmin start backup -allCritical -backupTarget:\servername\sharename`.

4. If the command was entered properly, you receive a confirmation screen asking you if you want to start the backup operation, as shown in Figure 4-4. Type Y and your backup will begin.

When finished, store your backup data in a safe place.

![](img/ea75090cfee8ac890f64c8c4f62f7285_69_0.png)

**Figure 4-4:** Create a system image.

## Restoring a System Image

In the event you ever need to restore your backup system image, you need to boot up into the System Recovery Console I covered earlier in this chapter. You can do that by pressing the F8 key right after the POST and after you turn on your computer, and selecting Repair My Computer. Alternatively, you can use the custom-made System Recovery Console Boot CD/DVD/USB that I showed you how to make.

After you load the System Recovery Console, follow these steps:

- 1. Attach the external hard drive on which you stored the backup image.
- 2. Boot to the recovery media.
- 3. Select your keyboard layout if asked.
- 4. Click Troubleshoot.
- 5. Click Advanced Options.
- 6. Select System Image Recovery. The Re-image Your Computer utility loads and searches for your backup files.
- 7. Pick the Select A System Image option and click Next. All backup locations discovered display, so you can connect to a network location as well.
- 8. Select a backup location to restore from and click Next. Alternatively, if you want to restore from a backup on a network location, click Advanced and then Search For A System Image on the network. Connect to your network and enter the full UNC path to the backup files. Once your files are found, your backup location shows up on the list just like files on an attached hard drive.
- 9. Choose the specific system image from all available images on the backup target and click Next.
- 10. On the Restore Options screen do not check the box that says Format And Repartition Disks. I have not had any success restoring backups with that option set. Simply click Next to move to the next screen.
- 11. Click Finish and then Yes on the confirmation screen.

At this point the restore begins. It can take a few hours depending how big your backup data is. When it is finished, your PC reboots and is ready for use.

## Using One-Click Recovery

New to Windows 8 are two new recovery features that make it very easy for anyone, even those without computer knowledge, to start over with a clean slate and restore their computer to brand-new, clean install condition. These features are called Refresh Your PC and Reset Your PC. Both operate very similarly but have very different results.

Using Reset Your PC is similar to a clean install of Windows 8. All of your applications, settings, and files are removed and everything is changed back to the default settings. The difference is that with Reset Your PC, you can just click a few buttons and everything is fully automated.

Refresh Your PC is similar to Reset Your PC but it preserves your Windows Store apps from the Windows Store, settings, and personal files. However, traditional Windows desktop apps are removed.

## Using Refresh Your PC

Refresh Your PC is the less destructive of the two new recovery features because it refreshes your system files and trashes only your traditional desktop applications.

- 1. Open the Start screen, type **Refresh your PC**, and change the search filter to Settings.
- 2. Select the Refresh Your PC option.
- 3. Click Next on the Refresh Your PC screen, as shown in Figure 4-5.

![](img/ea75090cfee8ac890f64c8c4f62f7285_71_0.png)

**Figure 4-5:** Choose Refresh Your PC to refresh your system files.

- 4. You may be asked to provide the Windows install DVD or recovery media provided by your manufacturer. When you insert the media, it is automatically detected and moves you to the next step if it is the correct media.
- 5. Click **Refresh** on the confirmation screen, and the refresh begins.

Your computer restarts a few times and then displays your logon screen when the refresh is completed. After you log in, all of your Windows Store apps are reinstalled automatically. A file called **Removed Apps.html** is placed on your desktop, listing all of the traditional desktop apps that were removed.

## Using Reset Your PC

Reset Your PC is the more destructive of the two new recovery features because it blows away all of your personal files, apps, and settings. Using Reset Your PC is equivalent to a clean DVD install that restores everything on your PC to default factory condition.

- 1. Open the Start screen, type **Remove Everything**, and change the search filter to Settings.
- 2. Select the **Remove Everything And Reinstall Windows** option.
- 3. Click **Next** on the **Reset Your PC** screen, as shown in Figure 4-6.

![](img/ea75090cfee8ac890f64c8c4f62f7285_72_0.png)

**Figure 4-6:** Resetting your PC lets you start with a fresh install as though the PC just came from the factory.

- 4. You may be asked to provide the Windows install DVD or recovery media provided by your manufacturer. When you insert the media, it is automatically detected and moves you to the next step if it is the correct media.
- 5. On the **Do You Want To Fully Clean Your Drive** screen, select **Just Remove My Files**. The Fully Clean The Drive option is only for situations when you want to securely wipe your data off the PC. That is helpful if you want to sell your PC and ensure all your private data is removed securely. Securely erasing files is much more time-consuming than just replacing files, so the first option is sufficient for resolving issues.
- 6. Click **Reset** on the confirmation screen.

Your computer restarts a few times and then presents you with the Windows 8 license terms when the reset is completed. You need to set up your user accounts, settings, and apps again just like the first time you started using Windows 8.

## Summary

This chapter covered how to tweak your computer safely by protecting it with System Restore. It showed you how you can recover your computer with the System Recovery Console and explained all about creating and restoring a full system image. The chapter ended with a review of the new one-click refresh and reset settings that will easily restore your install to brand-new condition.

You are now ready to begin tweaking the interface, performance, and security of Windows 8.

# Customizing Windows 8

## In This Part

- Chapter **5**: Customizing the Startup
- Chapter **6**: Customizing User Navigation
- Chapter **7**: Personalizing the Desktop
- Chapter **8**: Customizing the Appearance of the Windows Interface
- Chapter **9**: Fine-Tuning File Explorer
- Chapter **10**: Personalizing Internet Explorer
- Chapter **11**: Customizing Windows Media

![](img/ea75090cfee8ac890f64c8c4f62f7285_74_0.png)

# CHAPTER 5

# Customizing the Startup

Windows 8 has a great new look, but after a while, the new look can get old. With the help of some cool tools and tricks, you can customize many components of Windows 8.

This chapter guides you through customizing the lock screen.

You can customize this screen in several ways. For example, you can change the user picture and various settings that enable you to increase your privacy and the behavior of the lock screen. I even show you how to change the default lock screen and tweak the color scheme.

## Customizing the Lock Screen

Windows 8 includes a very different logon screen, now called the lock screen per Microsoft terminology. The new lock screen replaces the previously revamped screen in Windows Vista and the classic NT-style logon screen that many domain users are familiar with (because it was included in the last several releases of Windows up to XP).

Windows 8 continues to use the secure logon system that first appeared in Windows Vista that requires all logon components to be digitally signed by Microsoft. If any of the logon files are modified, the digital signature is destroyed and you will no longer be able to log on. This prevents malicious software from hijacking the logon process, but it also makes it next to impossible for people
