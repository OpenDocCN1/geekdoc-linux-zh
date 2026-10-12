
![](img/a7eec43a54473e95dc5ea333fecf1bd7_119_0.png)

Figure 4-21:
Selecting and previewing a theme in the KDE Control Center.

To try a theme, click Apply. If you don't like it, click Reset to revert back to the current look and feel.

## Logging out of KDE

When you're done exploring KDE, log out. To log out of KDE, choose K→Logout. You can also right-click empty areas of the desktop and choose Logout from the pop-up menu that appears.

## Playing with the Shell

Red Hat Linux is basically UNIX, and UNIX just doesn't feel like UNIX unless you can type cryptic commands in a text terminal. Although GNOME and KDE have done a lot to bring us into the world of windows, icons, mouse, and pointer (affectionately known as WIMP :-), sometimes you're stuck with nothing but a plain text screen with a prompt that looks like this (when you log in as root):

```
[root@dhcppc4 etc]#
```

This is most often the case when something is wrong with the X Window System, which is essentially the machinery that runs the windows and menus you normally see. In those cases, you have to work with the shell and learn some of the cryptic Linux commands.

You can prepare for unexpected encounters with the shell by trying out some Linux commands in a terminal window while you're in the GNOME or KDE GUI. After you get the hang of it, you might even keep a terminal window open, just so you can use one of those cryptic commands simply because it's faster than trying to point and click (those two-letter commands do pack some punch!).

## Starting the Bash shell

Simply put, the shell is the Linux command interpreter — a program that reads what you type, interprets that text as a command, and does what the command is supposed to do.

Before you start playing with the shell, open a terminal window. In either GNOME or KDE, choose Main Menu→System Tools→Terminal. What appears is a window with a prompt, like the one shown in Figure 4-22. That's a terminal window, and it works just like an old-fashioned terminal. A shell program is running and ready to accept any text that you type. You type text, press Enter, and something happens (depending on what you typed).

![](img/a7eec43a54473e95dc5ea333fecf1bd7_120_0.png)

Figure 4-22: You can type Linux commands at the shell prompt in a terminal window.

The prompt that you see depends on the shell that runs in that terminal window. The default Linux shell is called Bash.

Bash understands a whole host of standard Linux commands with which you can look at files, go from one directory to another, see what programs are running (and who else is logged in), and a whole lot more.

In addition to the Linux commands, Bash can run any program stored in an executable file. Bash can also execute shell scripts, text files that contain Linux commands.

## Understanding shell commands

Because a shell interprets what you type, it's important to know how the shell figures out the text that you enter. All shell commands have this general format:

```
command option1 option2 ... optionN
```

Such a single line of commands is commonly called a command line. On a command line, you enter a command followed by one or more optional parameters (or arguments). Such command-line options (or command-line arguments) help you specify what you want the command to do.

One basic rule is that you have to use a space or a tab to separate the command from the options. You also must separate options with a space or a tab. If you want to use an option that contains embedded spaces, you have to put that option inside quotation marks. For example, to search for two words of text in the password file, I enter the following grep command (grep is one of those cryptic commands used to search for text in files):

```
grep "Font Server" /etc/passwd
```

When grep prints the line with those words, it looks like this:

```
xfs:x:43:43:X Font Server:/etc/X11/fs:/sbin/nologin
```

If you created a user account in your name, go ahead and type the grep command with your name as an argument, but remember to enclose the name in quotes.

## Trying a few Linux commands

While you have the terminal window open, try a few Linux commands just for fun. I guide you through some random examples to give you a feel for what you can do at the shell prompt.

To see how long the Red Hat Linux PC has been up since you last powered it up, type the following. (Note: I show the typed command in bold, followed by the output from that command.)

```
uptime
```

```
7:13pm up 29 days, 55 min, 3 users, load average: 1.00, 1.00, 1.00
```

The part up 29 days, 55 min tells you that this particular PC has been up for nearly a month. Hmmm... can Windows do that?

To see what version of Linux kernel your system is running, use the uname command like this:

```
uname -srv
```

```
Linux 2.4.21-20.1.2024.2.1.nptl #1 Fri Jul 11 06:04:52 EDT 2003
```

In this case, the system is running Linux kernel version 2.4.21.

To read a file, use the more command. Here's an example:

```
more /etc/passwd
```

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
... lines deleted ...
```

To see a list of all the programs that are currently running on the system, use the ps command, like this:

```
ps ax
```

```
PID TTY   STAT   TIME COMMAND
1 ?       S      0:04 init
2 ?       SW     0:00 [keventd]
3 ?       SW     0:00 [kapmd]
4 ?       SWN    0:00 [ksoftirqd_CPU0]
5 ?       SW     0:44 [kswapd]
6 ?       SW     0:00 [bdflush]
7 ?       SW     0:00 [kupdated]
8 ?       SW     0:00 [mdrecoveryd]
12 ?      SW     0:17 [kjournald]
91 ?      SW     0:00 [khubd]
194 ?     SW     0:00 [kjournald]
604 ?     S      0:04 syslogd -m 0
609 ?     S      0:00 klogd -x
629 ?     S      0:00 portmap
657 ?     S      0:00 rpc.statd
... lines deleted ...
```

Amazing how many programs can run on a system even when there's only you logged in as a user, isn't it?

As you can guess, you can do everything from a shell prompt, but it does take some getting used to.

## Shutting Down

When you're ready to shut down Red Hat Linux, you must do so in an orderly manner. Even if you're the sole user of a Red Hat Linux PC, several other programs are usually running in the background. Also, operating systems such as Linux try to optimize the way that they write data to the disk. Because disk access is relatively slow (compared with the time needed to access memory locations), data generally is held in memory and written to the disk in large chunks. Therefore, if you simply turn off the power, you run the risk that some files won't be updated properly.

Any user (you don't even have to be logged in) can shut down the system from the desktop or from the graphical login screen. Choose Main Menu. A Logout dialog box appears that provides the options for rebooting or halting the system or simply logging out. To shut down the system, simply select Shutdown, and click OK. The system then shuts down in an orderly manner.

If you're at the graphical login screen, click the Shutdown label in the bottom part of the screen. Then another dialog box asks you to confirm that you really want to halt the system. Click the Yes button. The system then shuts down in an orderly manner.

As the system shuts down, you see messages about processes being shut down. You may be surprised at how many processes there are, even when no one is explicitly running any programs on the system. If your system does not automatically power off on shutdown, you can manually turn off the power.

Note that it does not require root access to shut down or reboot the system in this manner. Make sure that physical access to the console is protected adequately.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_123_0.png)

## Book II

## Workstations and Applications

## The 5th Wave

By Rich Tennant

© RICH TENNANT

![](img/a7eec43a54473e95dc5ea333fecf1bd7_124_0.png)

> "IT'S REALLY QUITE AN ENTERTAINING PIECE OF SOFTWARE. THERE'S ROLLER COASTER ACTION, SUSPENSE AND DRAMA, WHERE SKILL AND STRATEGY ARE MATCHED AGAINST WINNING AND LOSING. AND I THOUGHT MANAGING OUR BUDGET WOULD BE DULL."
