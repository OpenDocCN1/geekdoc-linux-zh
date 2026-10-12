
![](img/41feae212f5c6612ff709354891f7b39_70_0.png)

Figure 4-2: The Display Settings dialog box.

-   5. If you find it, select your monitor's manufacturer and model, click **OK**, and skip to Step 8.
-   6. If you don't find your monitor, your best bet is to rummage around in one of the two generic submenus. The Generic CRT Display submenu has generic settings for several resolutions for old-fashioned heavy, glass (monitor) monitors; CRT is short for *cathode ray tube*. The Generic LCD Display submenu provides settings for flat-panel displays using a *liquid crystal* display. If you don't know which type fits your monitor, take a guess and try one. Keep trying different generic monitors if your first choice doesn't work.
-   7. Select the generic setting that most closely matches your display, click **OK**, and return to the advanced settings window.
-   8. Click the **Configure** button next to the **Video Card** label. The Video Card window opens, as shown in Figure 4-3.
-   9. Select your video card from the long list of choices. If you cannot find your specific make and model of video card, select the **VESA driver (generic)** option.

> The lowest-resolution (8-bit) option allows only 256 colors on the window at one time. The 16-bit option allows 65,535 colors, and 24-bit allows more than 16 million colors (that's why it's also called *true color*).

-   10. Click **OK** to return to the Display Settings window.

![](img/41feae212f5c6612ff709354891f7b39_71_0.png)

![](img/41feae212f5c6612ff709354891f7b39_71_1.png)

-   11. Click **OK** and the Display Settings window closes. An Information window opens, informing you that you need to log out and then log back in to make the changes take effect.
-   12. Click **OK** to leave the Information window.
-   13. Log out and then log back in to make the changes take effect.

Alternatively, you can reboot your computer to enforce the changes.

You can also restart X unceremoniously, but quickly, by pressing Ctrl+Alt+Backspace. Your current X session is stopped and eventually restarted. You can then log back in.

## Delving deep into color depth

*Color depth*, the number of colors your system can have active on the window, is loosely a function of both the amount of video memory contained by your system and the window resolution.

If your system has a small amount of random access memory (RAM), your screen can have a resolution of 1024 x 768 pixels (dots) with 256 colors (8 bits) on the screen at one time. If your system has 2MB of memory, you can have 64 thousand colors (16 bits) on the screen at the same time at the same resolution. The more memory you have, the more colors you can display for any given resolution.

When you want to display an image and the color depth isn't correct, nothing drastic happens. The picture may look lackluster or not quite normal. That's because X has an interesting capability that allows the use of *virtual color maps*; the active window can utilize all the colors of the bits of color depth, even if other windows are using different colors.

![](img/41feae212f5c6612ff709354891f7b39_71_2.png)

## Introducing the Linux File System Tree

Linux, like Windows, uses files and directories to store and organize information and applications. This section introduces the Linux file system.

Linux sees all its parts, except its network, as files. No surprise that Linux accesses files, directories, and devices as *file addresses*. To figure out where everything is, Linux uses a system of letters and numbers to refer to drives and drive partitions — for example, */dev/hda* may be the name of the first IDE hard drive in the system, and */dev/sdb* may be the name of the second SCSI hard drive.

You can compare the Linux file system to an upside down tree. The trunk of the tree is the root directory — represented by a */* (slash). A series of limbs, branches, and leaves extends below the root: Limbs are mount points, the branches that extend from the limbs are directories, and the leaves on those branches are your files. Figure 4-4 shows the root, several directories, including etc, and a couple of files in etc.

![](img/41feae212f5c6612ff709354891f7b39_72_0.png)

Each mount point is a drive partition or a remote file system (such as your DVD or CD-ROM drive) that is mounted to— identified and made visible as a directory of the limb “above” it on the imaginary tree. Whenever a disk partition or remote file system is mounted on the directory branch, it turns that branch into another limb — allowing even more branches to be positioned and attached below the mount point.

Fedora Core needs at least a root partition in your directory structure and a swap space partition. The root partition stores all personal and system files and directories; Linux uses swap space to extend memory capabilities temporarily beyond the limit of your random-access memory (RAM). If you have 512MB of RAM and 512MB of swap space, for example, you can run a program that uses almost 1GB of memory. Part of it is stored in memory and the rest sits in swap space.

This configuration isn’t much different from the Windows and MS-DOS file systems — Windows, after all, uses the concept of a hierarchical directory tree — but the syntax is somewhat different. The top-level directory in Fedora Core, *root*, is designated with a forward slash (/). Every subsequent subdirectory name follows that initial slash. For example, the home directory is a subdirectory of root and is shown as /home. In the Windows world, the equivalent of the root directory is designated with an initial backslash (\). The famous C: prompt is synonymous with C:\. The theme for both operating systems is carried forward when dividing subdirectories: Linux uses forward slashes and Windows uses backslashes. For instance, a directory can be shown as /x/y/z in Linux and as C:\x\y\z in Windows. Both operating system can have subdirectories, such as /x/y/z/abc in Linux or C:\x\y\z\abc in Windows.

The location of a file or directory is given as a path. For instance, /x/y/z/abc describes the path to the subdirectory abc; if the file i23 lives in subdirectory abc, then its path is /x/y/z/abc/i23. Paths can be absolute or relative. Absolute paths always refer to the root directory (as in the examples just given). Relative paths refer to wherever you happen to be in the system; they’re relative to your current location.

![](img/41feae212f5c6612ff709354891f7b39_73_0.png)

Another fundamental difference between Linux and Windows file systems is that Linux requires you to explicitly mount file systems. Windows does so automatically. Explicitly mounting the file system isn’t as onerous as it sounds. Fedora Core installs utilities that automatically sense and mount file systems when necessary. For example, the default Fedora Core configuration mounts a DVD or CD-ROM automatically whenever you insert it in the drive.

The Workstation installation type we describe in Chapter 3 automatically sets up your root and swap partitions in addition to an extra root partition used for storing the Fedora Core kernel and other files used for booting your computer. (The Personal Desktop installation type uses the same partitioning scheme as the Workstation installation type.)

## Creating User Accounts

Because Fedora Core is a multiuser system, more than one person at a time can use it. For example, you can be logged in at the computer console (the attached keyboard and monitor) while someone else is logged in via a network connection. Therefore you — and every other user — must have an individual user account in order to use the computer. Each account requires an individual account name and password to protect your information and keep your tasks separate from other people’s tasks.

If you have cause to add new users (if you have a home network, for example) or you forgot to create a *nonroot* user account during installation, this section shows you how. Fedora Core offers both graphical and text-based user account creation and modification tools for your convenience. The following two sections describe how to use both types of utilities.

![](img/41feae212f5c6612ff709354891f7b39_74_0.png)

You can use the Fedora Core User Manager to modify an existing user account. Click the user name and then the Properties button, and a window similar to the Create New User window opens. You can then modify any aspect of the account.

### Using the Graphical User Manager

The Fedora Core User Manager is an excellent administration tool that can make your life easier. It provides an easy-to-use interface that simplifies your system administration job. Use the User Manager to create a new account by following these steps:

![](img/41feae212f5c6612ff709354891f7b39_74_1.png)

-   1. **Open the User Manager by clicking the GNOME Menu button and then choosing System Settings→ Users and Groups.**
    This is a job for *superuser*. If you’re not logged in as the *root* user, you’re prompted to enter the *root* password. The Fedora Core User Manager window appears.
-   2. **Click the Add User button in the upper-left corner of the screen.**
    The Create New User window appears, as shown in Figure 4-5.
-   3. **Enter your user name, real-life name (full name), and password twice (to confirm that it’s correct); accept the Login Shell default of /bin/bash.**
    The Fedora Core User Manager also creates a home directory by default.

Most of these items are self-explanatory, but here’s some additional information:

-   Your user name (also known as a *login name*) is the name you use to log in to your computer. Make your user name easy to remember and use all lowercase letters. Cute names may not seem appropriate later. Avoid choosing a name that is too long because you may have to type it several times a day. You may also end up using your user name as your e-mail address and have to give it up over the telephone, so a login name such as *phool* results in missent messages, leaving you feeling phoolish.
