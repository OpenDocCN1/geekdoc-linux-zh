
You can compare the Linux file system to a tree, as shown in Figure 4-1, which shows three subdirectories of root (more than a dozen subdirectories are in the root directory); a subdirectory is a directory within a directory. The top of the upside-down tree, represented by a / (slash), is the root directory. A series of limbs, branches, and leaves extends below the root: Limbs are mount points, the branches that extend from the limbs are directories, and the leaves on those branches are your files.

![](img/8c094d1b36276212c03d10d898508a6e_71_0.png)

![](img/8c094d1b36276212c03d10d898508a6e_71_1.png)

> Each mount point is a drive partition or remote file system (such as your DVD or CD-ROM drive) that is mounted, or made visible to, a directory of the limb above it. Whenever a disk partition or remote file system is mounted on the directory branch, it turns that branch into another limb, allowing even more branches to be positioned and attached below the mount point.

Red Hat Linux needs at least a root partition in your directory structure and a swap space partition. The root partition is used to store all your personal and system files and directories; Linux uses swap space, the Hamburger Helper of the computer world, to extend your memory beyond the limit of your random access memory (RAM). If you have 512MB of RAM and 512MB of swap space, for example, you can run programs that use 1GB of memory.

This configuration isn't much different from the Windows and MS-DOS file systems. Windows uses the concept of a hierarchical directory tree. However, the syntax is somewhat different. The top-level directory in Red Hat Linux, root, is designated with a forward slash (/). Every subsequent subdirectory name follows that initial slash. For example, the home directory is a subdirectory of root and is shown as /home. In the Windows world, the root directory is designated with an initial backslash (\). The famous C : is synonymous with C :\. The theme for both operating systems is carried forward when dividing subdirectories: Linux uses forward slashes, and Windows uses backslashes. Your home directory is then shown as /home/me in Linux and as \user_directories\me in Windows.

![](img/8c094d1b36276212c03d10d898508a6e_72_0.png)

Another primary difference between Linux and Windows file systems is that Linux requires you to explicitly mount file systems. Windows does so automatically. Explicitly mounting the file system isn’t as onerous as it sounds. Red Hat Linux installs utilities that automatically sense and mount file systems when necessary. For example, the default Red Hat Linux configuration mounts a DVD or CD-ROM automatically whenever you insert it in the drive.

The Workstation installation type we describe in Chapter 3 automatically sets up your root and swap partitions in addition to an additional boot partition used for storing the Red Hat Linux kernel and other files used for booting your computer. (The Personal Desktop installation type uses the same partitioning scheme as the Workstation installation type.)

The next section describes how to start and stop Linux.

## Giving Red Hat Linux the Boot

To boot a computer means simply to start it (and to *reboot* means to restart it). Follow these steps to boot your Red Hat Linux system for the first time:

- 1. Make sure that your computer is turned off.
- 2. Turn on the power to the monitor and then turn on the computer’s main power switch.

After a short time, the Red Hat boot menu appears on your screen. If you have only Red Hat Linux installed on your computer, you are given only one choice of operating systems to boot: Linux.

![](img/8c094d1b36276212c03d10d898508a6e_72_1.png)

The default operating system is the one at the top of the list. If you have installed Red Hat Linux along with another operating system, you can change the one that boots by default.

![](img/8c094d1b36276212c03d10d898508a6e_72_2.png)

Linux runs in three different states: 1, 3, and 5 (referred to as *run levels*). Each run level is used to perform different functions. At Level 1 (also called *single-user mode*), Linux operates with a minimum of processes so that you can make configuration changes and debug problems. Level 3 is essentially the same as Level 5 except that Level 3 doesn’t run the X server — it’s non graphical. You typically run servers that don’t need to run graphical applications, such as word processors, at Level 3. Level 5 is the default for personal workstations. You can use GRUB (Grand Unified Bootloader) to select a different Linux run level. When GRUB appears, press e for edit. Three lines appear. Press the down-arrow key to select the line that begins with *Kernel*. Press the e key again, append a space, and then press either **1, 3,** or **5**. Press the Enter key and then press the b key. Your computer boots into either single-user mode (1), nongraphical mode (3), or graphical mode (5).

- 3. Press the up- and down-arrow keys to highlight the word Linux (if it's not highlighted already) and press Enter.

If you don't press anything, the default operating system (Linux sets itself as the default when you install it) starts automatically after a five-second delay.

If you're running more than one operating system (for example, Red Hat Linux and Windows), you can select any of the listed operating systems to boot; we assume here that you choose Linux.

After you press Enter, Red Hat Linux boots. During this process, lots of information is displayed on your screen. Red Hat Linux gleans this information as it probes your computer in order to determine what hardware (disk drives and printers, for example) is present.

Because Red Hat Linux is a multiuser system, one or more users can use it at the same time; for example, you can be logged in at the computer console (the attached keyboard and monitor) while someone else is logged in via a network connection. Therefore, you and every other user need a user account in order to use the computer. Each account requires an individual account name and password to protect your information and keep your tasks separate from other people's tasks.

## Logging In

When you use Red Hat Linux, you must log in as a particular user with a distinct login name. Why? Because Red Hat Linux is a multiuser system and therefore uses different accounts to keep people from looking at other people's secret files, erasing necessary files from the system, and otherwise (intentionally or unintentionally) doing bad things.

The use of unique identities helps to keep the actions of one person from affecting the actions of another because many people may be using the same computer system at the same time (for example, over a network). A benefit of this strategy is that Red Hat Linux systems are essentially invulnerable to viruses simply because each user's files and directories can't be used to corrupt the system as a whole. (Not that we're keeping score or anything, but viruses can destroy or just make life miserable for Windows 9x systems because they don't have this capability.)

As Red Hat Linux boots, you see all sorts of messages scrolling by on the screen. After the scrolling stops, the login screen appears.

If you chose (during installation) not to have X start automatically whenever you boot your system, you see the `login:` prompt.

If you make a mistake while typing the password or your login, the system asks you to retype it.

We strongly recommend that you do most of your experimentation with Red Hat Linux as a nonprivileged user and log in as the root user only when necessary. By operating as root, you run the risk of corrupting your system, having to reinstall again, or losing data because you can delete or change anything and everything. When you are logged in as a regular user, you can accidentally erase your own files and data, but you can’t erase someone else’s files or system files.

Fortunately, Red Hat Linux provides many graphical administration utilities you can start as a nonprivileged user. Each Red Hat administrative utility prompts you to enter the root password as it starts and then performs its specific function, but only that function, with root privileges. You’re prevented, therefore, from doing unintended damage to other systems. (See Appendix C for information about how file permissions work and how you can modify them.)

## The Command-Line Interface (CLI) versus the Graphical User Interface (GUI)

Red Hat Linux installs the X Window System by default. You can perform most administrative tasks with the GUI-based tools (GUI stands for graphical user interface) that Red Hat provides. Most of the how-to instructions in this book use the X-based applications and utilities. We do that because they’re generally easier to use and because this book wasn’t written for systems administrators.

Occasionally, a utility or program doesn’t run graphically; at other times, using nongraphical methods and systems is just more interesting or convenient. Believe it or not, some geekier Linux users *prefer* to use a text-based, command-line interface (CLI). If you’re not familiar with doing some basic administrative tasks with a CLI, we don’t recommend using one just to prove that you can. Being less of a geek is okay. We still like and respect you. On the other hand, it makes good sense to know some basics, just in case a need arises for you to have to wing it with the text-based interface.
