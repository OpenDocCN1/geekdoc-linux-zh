
# 48 · CHAPTER 4

```
# Run gettys in standard runlevels
1:2345:respawn:/sbin/getetty tty1
2:2345:respawn:/sbin/getetty tty2
3:2345:respawn:/sbin/getetty tty3
4:2345:respawn:/sbin/getetty tty4
5:2345:respawn:/sbin/getetty tty5
6:2345:respawn:/sbin/getetty tty6

# Run xdm in runlevel 5
# xdm is now a separate service
x5:2345:respawn:/etc/x11/getdm -F
pppt:2345:respawn:/usr/sbin/ppptd
```

Figure 4.2: The initab file controls the initialization sequence of Red Linux (part of 2).

The initab file follows a format that is initially very difficult to understand. Each line conforms to the following:

```
code:runlevel:action:command
```

The code is a unique one- or two-character sequence that identifies the specific entry in the initab file. The runlevel indicates that runlevel 0 executes the processes required to do a hard halt, runlevel 3 executes processes required to enable a Linux multiuser mode, and runlevel 6 qualifies reboot processes to run. The initab file has one line that identifies the default runlevel. In Figure 4.2, runlevel 3 is to be used unless otherwise qualified with the execution of the init program, as during the boot process.

You can manually run the init program by invoking it with the runlevel as a parameter. For instance, to shut down your system, you could use the following command as the root user:

```
init 6
```

The si:sysinit/etc/rc.sysinit entry that follows the default runlevel enters a script called rc.sysinit to execute. This script does such checking and monitoring file systems, enabling memory for disk swapping, and synchronizing the Linux system clock with the platform's hardware clock. Following the execution of the rc.sysinit script, a script called rc is executed with a parameter that qualifies the runlevel.

On Red Hat, the rc executes scripts that exist in directories qualified, by the runlevel. When the init program runs with runlevel 3, the initab file calls the rc script to turn around and runs the scripts located in a directory called /etc/rc.d/rc3.d. Red Hat's rc.3 script executes all scripts that are prefixed with a K before it executes the ones that are prefixed with an S. The K scripts kill, stop down, processes that might already be executing, and the S scripts start processes. The two digits following the K or S control the execution order of scripts.

On Red Hat, the various runlevels start or stop the same processes, the common scripts are in a directory called /etc/rc.d/init.d, while symbolic links to those scripts are in the various rc.X directories. To give you an example of how this works, consider a Red Hat 7.1 system where PostgreSQL should start when the system boots. While the rc3.d directory contains a link to the /etc/rc.d/init.d/postgresql script called K12postgresql, it does not contain a link to /etc/rc.d/init.d/postgresql preceded by an S. When Red Hat was installed, it placed the link in rc.3 that would shut down PostgreSQL, in case the user wanted to start PostgreSQL manually and forgot about it on Linux shutdown.

To have rc.3 automatically start PostgreSQL, you would simply have to create a link to /etc/rc.d/init.d/postgresql called S12postgresql (where the 12 could be any two-digit number), with the following command:

```
ln /etc/rc.d/init.d/postgresql S12postgresql
```

Even though the rc scripts run as a separate process, the init program waits until finish executing the rc entries in the initab file explicitly to say. After the rc scripts complete, the init program executes the rest of the entries in the initab file. We will skip most of them, as they are self-explanatory. However, take a look at the /etc/getty scripts. These script start up six virtual consoles, which means you can sign on six different times as six different people on the single system console. To toggle between virtual consoles, press Ctrl-Alt followed by the number of the console you wish to see.

The only other initab entry mentioning this is:

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

This entry causes Linux to be able to capture the Ctrl-Alt-Delete keystroke combination and gently shut down the system.

# Customizing Startup

A better way of configuring PostgreSQL to start up, rather than adding the link in the rc.3 directory, is to modify the script called /etc/rc.d.local. Each of the rc.N directories contains a link called S99local that points to a file called /etc/rc.d.local. Because 99 is the largest possible number, a script called rc.local will always be executed last. So, instead of creating the link called S12postgresql, you could place the entry in the rc.local script:

```
/etc/rc.d/init.d/postgresql start
```

There are two advantages to this approach:

- It places all your startup modifications in one script file.
- You can ensure that your custom processes are started after all the default processes are initialized.

# Signing On

The root user is the omnipotent profile of Linux, also known as the super user. When Linux is installed, you are prompted for the password for the root user. Part of the Linux install is to create a less powerful user. As discussed in chapter 3, Linux security is set up that all the files on the system have three levels of authorization: user (or owner), user group, and users who are neither the owner nor part of the authorized user group. The root user, being all-powerful, has access to all files. For security purposes, you should use the sign-on only when it is necessary.

To make it easier to use the root sign-on, Linux provides the su command (for "super user"). If you are logged in as a user other than root, but need root privileges, the su command, which prompts for the root user's password. You can then execute commands that require root privileges. Be sure, however, to use the exit command to return to your alter-ego of a normal user with super (and potentially dangerous) powers. You can also use the su command while you're logged in root to temporarily assume the role of a normal user. In that case, the command requires the user name. For instance, to temporarily run as user bill while logged in root, you'll use this:

```
su bill
```

# Running Linux Commands

The Linux login screen program is known as the bash shell. Once you've logged into Linux, you can invoke thousands of commands from bash. Chapter 12 covers bash in detail, while this section bootstraps, to boost your knowledge of bash and Linux commands in general. The bash prompt defaults to your user name, the host name of your system, the current directory, and a dollar sign ($) if you are logged in as a normal user, or a pound sign (#) if you are logged in root.

From the bash prompt, you are ready to begin mastery of Linux. Linux commands follow a common structure:

```
command option(s) argument(s)
```

Many commands, however, execute without requiring options or arguments. A starter set of Linux commands is shown in Table 4.1. The cd command can be used to move around the various directories of your file system. When you use cd, you can use relative or absolute addressing. Absolute addressing means specifying the full directory with a slash (/). For instance, to change the directory to /usr/local you'd use the following command:

```
cd /usr/local
```

Relative addressing is used when you change the directory relative to your current directory. For instance, if you're in /usr/local you wanted to go up one directory you'd use:

```
cd ..
```

A single dot indicates the current directory.

# Linux Configuration and Startup

Table 4.1: A Starter Set of Linux Commands
| Command | Description |
|---|---|
| cd | Change the directory. |
| pwd | Print the working directory. |
| ls | List all the files, directories, and links in the current directory. |
| cp | Copy a file. |
| mv | Move or rename a file. |
| less | Display the contents of a file one screen at time. |
| man | Display documentation about a command. |
| apropos | List all commands that have the string argument in your manpage for the command. |
