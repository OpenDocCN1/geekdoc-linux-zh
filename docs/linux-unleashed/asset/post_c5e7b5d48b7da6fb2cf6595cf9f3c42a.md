
# Getting to Know Linux

## In This Part

- Getting Started
- Basic Linux Commands
- Using the File System
- File and Directory Permissions
- GNU Project Utilities
- bash
- pdksh
- tcsh
- Shell Programming
- FTP and Telnet

# Chapter 6: Getting Started

**by Ed Tiejels and Tim Parker**

## In This Chapter

- Starting and stopping your Linux system
- What's this about "logging in"?
- Passwords
- Creating a new login
- Logging out
- Trying out your new login
- The who command
- Virtual terminals
- Command and programs

## Starting and Stopping Your Linux System

The startup phase of Linux depends on the configuration of LILO that you chose during your Linux installation. In the simplest case, Linux starts automatically from your hard drive or from a boot floppy disk. If your system has multiple versions of Linux or other operating systems installed, you will have to enter a boot string to start Linux.

When your Linux system starts up, you see quite a few Linux initialization messages scroll across the screen. These are system messages that indicate the hardware that Linux recognizes and configures, as well as all the software drivers it loads when starting up. When Linux completes its startup sequence, you should see a prompt similar to this one:

```
darkstar login:
```

You will probably see another name before the login prompt, which in most versions of Linux is set when you install the software. Some Linux systems also show the current version number of the software when the login prompt is displayed, like this:

```
Welcome to Linux 1.2.13
darkstar login:
```

Don't worry if your prompt doesn't look exactly like this because each version of Linux does it a bit differently. You will get some sort of a prompt—such as a dollar sign—with every version, though.

> **WARNING**
>
> A Linux system must always be shut down properly. Improper shutdown, usually caused by simply turning off your system at the power switch, can cause serious damage to your Linux filesystem! When you are finished using your Linux system, you must shut it down properly as described in the next section. If you start to boot up Linux and then change your mind, you should let the system start up fully and then follow the shutdown procedure. You risk losing files or your entire system if you fail to follow this advice!

You already know how to start Linux, but it is even more important to know how to shut down the system properly. Like many multiuser systems such as UNIX and Windows NT, if Linux is not powered down properly, damage to individual files or the entire filesystem can result. This is caused by Linux keeping more current versions of the disk's table of contents (known as the I-node table) in memory in order to speed disk access. When you shut down the system properly, the memory version of the I-node table is written to disk prior to the system halting. If you power down without writing the memory version of the I-node table to disk, the disk’s contents may not be correct and files may be lost. Also, since Linux is continually using the disk drives even when you are not using the system, it’s possible that a disk write-protect could get interrupted when you power off manually. Shutting down the system properly causes all disk writes to cease.

The easiest way to ensure a proper shutdown is to press the Ctrl+Alt+Delete keys simultaneously. (This is the famous Ctrl+Alt+Delete “three-finger salute” used in DOS and Windows.) Pressing Ctrl+Alt+Delete causes a number of advisory messages and Linux shutdown messages to be displayed. When the Linux shutdown procedure has finished, your monitor shows either the initial “power-on” screen or a shutdown message before turning your computer off. Since the shutdown process takes Linux only a few seconds, this is not time-consuming. It’s fast and easy, and maintains your system’s integrity.

One quick warning: If any users are logged in to your Linux system when you do the Ctrl+Alt+Delete sequence, they will be logged off rather forcefully and possibly lose whatever they were working on. Use the Ctrl+Alt+Delete sequence with care, and try to tell everyone to log off if they are using the system. You can use the who command to find out who is logged in (see “The who Command” section found later in this chapter).

### Linux Shutdown Commands

There are several other ways to shut down the system, but the Ctrl+Alt+Delete sequence is probably the easiest. A number of other commands can activate the shutdown process, but they vary, depending on the version of Linux you are using. Commonly used commands are `shutdown`, `haltsys`, and `fasthalt`. Experiment with your particular Linux version to find out which commands are supported.

The second most commonly used method of shutting down Linux (aside from Ctrl+Alt+Delete) is none other than the `shutdown` command. The syntax usually allows you to specify several parameters, such as the amount of time before Linux shuts down and whether to reboot immediately. Practically every Linux version of `shutdown` requires an argument that indicates the number of seconds to wait before starting the shutdown procedure. For example, the command:

```
shutdown -t 45
```

tells Linux to wait 45 seconds before starting the shutdown process. The time argument often requires the `-t` option ahead of it, but some versions assume any number is the number of seconds. If you want to start the shutdown process immediately, you can set the number of seconds to zero or on some systems type the word **now**: `shutdown now`.

An `-r` option tells Linux to reboot after shutting down. This can be handy when you want to load new configuration information such as device drivers. There are several other options supported by `shutdown`. Usually, you can find them by simply typing **shutdown** with no arguments and checking the error message that appears. Alternatively, the man page will have a list of supported options, too.

The `fasthalt` and `haltsys` commands are left over from other versions of UNIX but have been implemented in some Linux releases. Both commands do as their names imply and quickly shut the system down.

## What's This About "Logging In"?

After you boot the system, Linux waits for a login. A login is simply the name that you supply to Linux to identify yourself to the operating system. Linux keeps track of which names are permitted to log in to the system and allows only valid users to have access. All others are refused access.

Every login name on the system is unique and typically, a password is assigned to each one. This secret password is like the identification number you use with your bank card to prove that you are who you say you are. Also, the things you can do with your login—the login's privileges—are controlled by Linux; different logins have different levels of privileges. Some logins can do anything they want to the system, while others may not be able to do very much. The system administrator (or whoever creates the login) assigns these privileges.

> **WARNING**
>
> Usually, login names reflect a person's real name. On larger systems, login names are usually composed of the first and last names, such as `tparker` or `rmaclean`. Smaller systems tend to be less formal, so you may simply have first names or first name and an initial, such as `tim`, `tmp`, or `tjp`. Some administrators base login names on something else entirely, such as `wizard` or `goblin`, but these tend to have very little meaning to others outside the single machine.

Although you can't have two identically named logins on your system, you can easily create logins for users with the same (real) name by changing one or two characters. So the login names `suej` and `suek`, for example, are treated by Linux as completely separate logins.

Conversely, there is no reason that one person (for instance, you) can't have two, three, or a dozen login names. In fact, because you will be the system administrator of your Linux system, you will have one or more administrative logins and one or more regular user logins.

At the login prompt, type your name, your dog's name, or any other random name that occurs to you. None of these are valid logins (at least not yet). The system asks you for a password; it doesn't matter what you type, so simply press Enter or type a random string of characters. Because the logins are not valid on the system, Linux won't let you in. It displays the message **Login incorrect** to tell you that either the name or the password you entered is not valid.

Most likely, the only valid login on your Linux system after installation is the most powerful and dangerous login Linux offers: `root`. In the section "Creating a New Login" that appears later in this chapter, we will create a safe login for you to use. This safe login can have your name, your dog's name, or whatever you choose. Some versions of Linux prompt you to create a user login during the installation procedure, so you have two logins (root and a username) that you can use.

> **WARNING**
>
> Why does Linux bother asking for a password even when the login name is not valid? It's because Linux uses a program called `login` that's instructed to get your login and password first, then check the list of valid users. The login program then displays a message that shows if you are denied access or it lets you through to the next program that starts your user session.

### Why You Should Not Use the root Login

You will have to use the root login from time to time. Some things simply cannot be done on the Linux system without logging in as root. You should not, however, use the root login as your regular user login. This is especially true if you are exploring the
