
If you want to uninstall UT2004, you can use the uninstall script in the `ut2004` directory. Type

```
$ sh uninstall.sh
```

After confirmation, Unreal tournament removes itself from your system.

# Installing Quake 4

Being based on the DOOM 3 engine, you could almost expect Quake 4 (see Figure 13.4) to ship with a good deal of support for Linux. To get started, you must have the Windows version of the software because you need several files as well as the CD key to be able to play the game. First things first, though. Head on over to http://zerowing.idsoftware.com/linux/quake4/ to download the required Linux installer (quake4-1.1inux-1.0*.run) by either direct FTP or the more bandwidth-friendly BitTorrent.

![](img/2045828cf45e5632bf056f9ca99d6755_355_0.png)

FIGURE 13.4 Based on the popular DOOM 3 engine, Quake 4 pits you against the evil Strogg. Get out there and frag 'em!

After you download the file, drop down to a command line and type in

```
# sh quake4-1inux-1.0*.run
```

and then press Enter. The installer starts up and asks you a couple questions. After you answer these, the installer creates the necessary files and folders. All you need to do is to copy several files from the /quake4/qbase directory on the DVD to /usr/local/bin/quake4/qbase. You can start the game by typing `quake4` at a command prompt.

# Installing Wolfenstein: Enemy Territory

Whereas the earlier Return to Castle Wolfenstein was both single- and multiplayer, the freely available Wolfenstein: Enemy Territory is multiplayer only (see Figure 13.5).

![](img/2045828cf45e5632bf056f9ca99d6755_356_0.png)

**FIGURE 13.5** Teamwork is the key to victory in this lush but hostile graphical environment.

Available in Win32 and Linux native versions, it can be downloaded through http://www.SplashDamage.com/. After you download the 260MB file named et-linux-2.55.x86.run, install the game by typing

```
# sh et-linux-2.55.x86.run
```

Then accept the defaults. A symlink exists in /usr/local/bin to the script that loads the game. When using the KDE desktop, we had difficulty with sound due to a conflict with the KDE sound daemon artsd. The fix was prepending a line to the et script that read killall artsd.

# Playing Windows Games with Cedega

As mentioned earlier, the key to mass-market appeal of an operating system is in the applications available for it. A group of developers saw that the vast majority of the computing world was using Windows-based productivity and gaming software and decided to develop a way to run this software on Linux, thereby giving Linux users access to this large application base. The developers came up with a program called Wine, which has been updated regularly and forms the basis of the gaming variant called CedeGa. This is a commercial product available from developers TransGaming Technologies (http://www.transgaming.com/), so you cannot retrieve it using yum.

However, CedeGa is a very popular and up-to-date product with support for recent releases such as Half-Life 2, Sid Meier's Pirates, and World of Warcraft. Because the state of CedeGa is constantly changing, TransGaming Technologies has a subscription service, which means that you get updates for the code when they are released—ensuring that you are able to enjoy not only the games of today, but also those of tomorrow.

So, if you can't wait for Linux to become more popular with game developers, use CedeGa as a stop-gap until they can be persuaded to support Linux directly.

> **TIP**
> The keys to successful gaming in Linux are to always read the documentation thoroughly, always investigate the Internet resources thoroughly, and always understand your system. Installing games is a great way to learn about your system because the reward of success is so much fun.

# Reference

- http://www.transgaming.com/—The official TransGaming Technologies website provides details of games that are directly supported under CedeGa.
- http://www.linuxgames.com/—A good source of up-to-date information about the state of Linux gaming.
- http://zerowing.idsoftware.com/linux/doom/—Includes a complete how-to and troubleshooting guide for running DOOM 3 under Linux.
- http://www.unrealtournament.com/—The official site of Unreal Tournament.
- http://www.nvnews.net/nbbulletin/forumdisplay.php?f=14—The Official NVIDIA Linux driver support forum.
- http://www.nvidia.com/object/linux.html—Home page for the NVIDIA Linux drivers.
- http://tinyurl.com/3pm2y—Home page for the ATI Linux drivers (courtesy of tinyurl.com).

# PART III

# System Administration

## IN THIS PART

- CHAPTER 14 Managing Users 325
- CHAPTER 15 Automating Tasks 351
- CHAPTER 16 System Resources 413
- CHAPTER 17 Backing Up, Restoring, and Recovery 423
- CHAPTER 18 Network Connectivity 455
- CHAPTER 19 Remote Access with SSH and Telnet 507
- CHAPTER 20 Xen 515

# CHAPTER 14

# Managing Users

One of the most important things you need to learn while using Fedora is effective user administration. Whether you are setting up a box for use just by yourself, sharing it among a family of five, or even working with a machine that has to handle several thousand different users, it is important that you understand how to effectively assign user permissions and lock down the areas you want to protect. Equally important is the ability to fine-tune user access rights, to enable people to do what they need to do, and not necessarily what they want to!

Managing users includes managing home directories and settings that are unique to each user. You also have to examine how much of the overall system you want to give the users access to, as well as establish good password practice. We will cover all these tasks among others, which will teach you how to effectively manage the users of your system. We will also take a look at the super-user account so that you can understand why it is so important and also how to let others access some, if not all, of the super-user's power.

## User Accounts

Every Fedora installation typically contains three types of accounts: the super-user, the day-to-day user, and the system user. Each type is important in its own right and you must know what each is responsible for. Without working together, Fedora would have a hard time doing anything!

All users must have accounts on the system. Fedora uses the /etc/passwd file to hold information on user accounts. Each user, regardless of type, will have a one-line entry of account information stored in the /etc/passwd text file.

## IN THIS CHAPTER

- User Accounts
- Managing Groups
- Managing Users
- Managing Passwords
- Granting System Administrator Privileges to Regular Users
- The User Login Process
- Disk Quotas
- Reference

Each account entry contains a username (used for logging in), a password field containing an $\star$ as passwords are actually contained in /etc/shadow, a user ID (UID), and a group ID (GID). The fifth field contains optional human ID information, such as real name, office location, phone number, and so on. The last two fields are the location of the user's home directory and the user's default login shell. See the "The Password File" section later in this chapter for more information.

Like other Linux distributions, Fedora makes use of the established UNIX file ownership and permission system. Each file (which can include directories and even devices) can be assigned one or more of read, write, and/or execute permissions. These can be assigned further to the owner, a member of a group, or anyone on the system. File security is drawn from combining ownership and permissions. The system administrator (most commonly referred to as the *super-user*) has total responsibility to make sure that users have proper UIDs and GIDs, as well as ensuring that sensitive files (which can include important system files) are locked down using file permissions.

Regardless of how many system administrators are present on the system, there can only be one *root* user. This is the user who has access to everything, and can grant or take away any privileges on the system. The root user has a user ID of $0$ and a group ID of $0$, making it unique among all other users on the system. The root user can use any program, manipulate any file, go anywhere in the file system, and do anything within the Fedora system. For reasons of security, that kind of raw power should only be given to a single trusted individual.

It is often practical for that power to be delegated by the root user to other users. This delegation is referred to as an *elevation of privileges*, and these individuals are known as *super-users* because they enjoy the same powers that root enjoys. This approach is normally used only on large systems in which one person cannot effectively act as the system administrator.

> **NOTE**
>
> On your Fedora system, when you log in as root, you are root or the super-user. In this chapter, the terms *root*, *super-user*, *system administrator*, and *sysadmin* are used interchangeably, although they need not all refer to a single person.

A regular user is someone who logs onto the system to make use of it for nonadministrative tasks such as word processing or email. These users do not need to make systemwide changes, nor do they have to manage any other users. However, they might want to be able to change settings that are specific to them (for instance, a desktop background). Of course, depending on how draconian the root user is, regular users might not even be able to do that!

The super-user grants privileges to regular users by means of file and directory permissions. (Those are covered in Chapter 5, "First Steps with Fedora.") For example, if the super-user does not want you to change your settings in $-/.profile$ (the $-$ is a shell shortcut representing your home directory; see Chapter 15, "Automating Tasks"), root can alter the permissions so that you may read from, but not write to, that file.
