
# Chapter 2 • Understanding Unix

## Figure 2.4 Ubuntu Boot Options Screen

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_24_0.png)

You'll take the default, and press Enter to start Ubuntu. Now, it's not very Linux-like to be staring at a pretty graphic splash screen at boot time, so Hit Alt-F1. You'll see console boot messages by telling that in delightful detail what's going on in the boot process. Here's a taste (see Figure 2.5).

## Figure 2.5 Hitting Alt-F1 During Boot Shows Console Messages

| Loading Kernel modules... | [ OK ] |
| Loading manual drivers... fsck 14.0.2 (12-Jul-2007) | [ OK ] |
| Mounting local filesystems... | [ OK ] |
| Activating enable swap... | [ OK ] |
| Checking file system on /tmp/ | [ OK ] |
| Configuring network interfaces... | [ OK ] |
| Setting up config font and keymap... | [ OK ] |
| ubuntu 2.6.22-generic #1 SMP Nov Oct 14 23:05:12 GMT 2007 i686 | [ OK ] |

The programs included with this Linux system are free software; the details for each program are described in the individual files in /usr/share/doc/~/copyright.
ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.
to run a command as administrator (user "root"), use "sudo <command>". See "man sudo_root" for details.

| Loading ACPI modules... | [ OK ] |
| ubuntuubuntu: $ Starting ACPI services... | [ OK ] |

Understanding Unix • Chapter 2

And when we're all done, Ubuntu dumps you without prodding for a password into the pretty Gnome Window Manager (see Figure 2.6).

## Figure 2.6 Ubuntu 7.10 Default Desktop

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_25_0.png)

At this point, feel free to poke around and try some of the preinstalled applications. Now, in all the messages flying by at the console prompt, you may have noticed Ubuntu doing all sorts of wonderful things detecting your hardware, starting the X11 server so we can jump from the text world of the command prompt into the Gnome window manager.

The concept of X11 and a window manager is also a departure from the Windows world. In Windows, the graphics subsystem is intimately tied to the operating system, and you cannot boot straight to the DOS prompt without a great deal of gyration. In *n, the heritage of booting to a green screen login prompt does a particularly good job of hiding 99 percent of the time. In *n, graphical displays and a windowed interface are bolt-ons to the operating system's core functionality. X11 provides the basis for doing bitmap graphics and providing an application programmer's interface (API) for creating windows and interacting with the mouse. A windows manager, on the other hand, runs on top of the X11 base, is the source of the look and feel of your desktop, menus for starting programs, what the window close icon and window borders look like, what the right mouse button does when clicked the workspace, and things of that nature.

Though it may seem alien to a Windows user, there are choices in Windows managers in *n. Imagine in Windows XP if you didn't ever want to see a Start button again, or you wanted a desktop that had multiple workspaces so you can keep all the windows associated with your mp3 media program in one desktop workspace while your work applications are in another. Or suppose you wanted to remap Alt-F4 to do something other than a window. With the choice of different managers in *n (or the config file for the one you have), those sorts of things are possible. Gnome is the default for Ubuntu, but if you want to see KDE in action, there's a Linux distribution named Kubuntu that sets it as the default. Fluxbox is a very lightweight window manager for running on older hardware without a lot of memory. CDE and its dtvm manager you find on older Solaris or HP-UX servers. They all have a slightly different look and feel.

If you have a wired Ethernet connection and a Dynamic Host Configuration Protocol (DHCP) server, Ubuntu will surely have grabbed an Internet Protocol (IP) address and you are sitting ready to hit the Internet if you fire up the Firefox Web browser, for instance. Hunt around, get comfy. After all, you're not going to break anything because you've booted into Linux using a read-only CD-ROM. Unless you go out of your way to double-click the Install icon and answer several prompts that warn you that you're about to reformat your hard disk, or you intentionally browse to the hard drive icon in the file explorer, Ubuntu isn't going to touch your hard disk, let alone change anything on.

# The Shell

Since our work in Linux isn't about pretty GUI's, let's waste time in getting a shell opened up, using the Terminal application. The Linux shell is like a more powerful version of the Windows “Command Prompt” (see Figures 2.7 and 2.8).

## 2.7 Finding the Terminal Program Under Applications > Accessories

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_27_0.png)

## Figure 2.8 The Linux Bash Shell in Terminal

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_27_1.png)

# Chapter 2 • Understanding Unix

## All Hail the Shell

Like the Windows command prompt (except bigger, better, and more powerful), here's where you get to reacquaint yourself with the keyboard by typing Unix commands.

Unlike Windows, there are actually options for your shell. There isn't just one shell in *nix. In Windows, you have cmd.exe and ... well, cmd.exe, unless you've gone out of your way to implement a replacement Windows shell (or have installed Cygwin). In the *nix world, there are many supported shells preinstalled: Bourne shell (sh), Korn shell (ksh), C Shell (csh), Tom's C Shell (tch), and Bourne Again Shell (bash). Bash is the usual default in Linux, but HP-UX machines are often configured to default to ksh. Depending on the whims of the system environment. If you ever want to know what shell you're in, it's just echo $SHELL

```
ubuntu@ubuntu~$ echo $SHELL
/bin/bash
ubuntu@ubuntu~$
```

# Essential Commands

Here is a list of commands you should get familiar with, and common options. Note that command options and syntax have a way of being different between the flavors of *nix operating systems, so when in doubt, consult the man pages.

| Linux Command | Closest Windows Equivalent (if any) | What it does |
|---|---|---|
| ls -l | dir /od | List files in current directory. Options give you a long listing with all files that begin with "." in reverse order with the newest file last. |
| pwd | cd [no arguments] | Prints name of your current directory. |

| Linux Command | Command Equivalent (if any) | What it does |
|---|---|---|
| touch filename | Creates an empty file if the file doesn't already exist. If it does exist, it updates access and modification timestamps on the file. |
| rm filename | del | Unlinks ("deletes") a file. Overwrites a file to hide its contents, and optionally deletes it. |
| cd dirname | cd | Changing directory. Note that in *unix, the directory names use forward slashes, not backslashes, e.g., /tmp. |
| hostname | net config workstation | Shows the hostname of the machine. |
| ifconfig -a | less ipconfig /all | Shows all network interfaces, and pipes the output to a handy program named less. |
| cat filename | type | Displays the contents of the file to the screen. |
| less filename | View text files with ability to scroll forward and backward through the output with spacebar and b keys. q to quit. |
| more filename | View text files one screen at a time, advancing with the space bar. Available on all *unix systems. |
| head filename tail -f logfilename | Head displays the first lines of a file. Tail -f to follow the end of a growing text file or a log. |
| history | Shows your previously executed commands. |
| dmesg | Those console messages you saw on startup are all here. Extremely useful for debugging and figuring out names of external hard drives detected by hotplug. |
