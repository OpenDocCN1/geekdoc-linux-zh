
turned into a security vulnerability. Hackers are now in a position to take over a Mac computer with the help of the Flash software. However, the Linux operating system is free of this vulnerability. Let us move on to the process of installing a Linux operating system on your computer.

The first step for the installation is to download the Ubuntu Linux server operating system. Go to www.ubuntu.com. On the home page of Ubuntu, you will find different versions of Ubuntu to do several things. You will find a desktop version of Ubuntu. You will also see a netbook version. There will be a cloud version as well, along with a version for tablets and cell phones. You have to locate the server version of Ubuntu and find its link for download.

If you are looking forward to installing Ubuntu on your computer system, you should make sure that the file boots off a DVD and not a hard disk drive. You can do this by pressing the DELETE or F1 key on the keyboard to enter the motherboard's BIOS settings. From there on, you may set up the point where you may want to boot the system from. Several motherboard manufacturers have different ways to enter the BIOS settings, so you should make sure that you consult the user’s manual of the motherboard on how you should do this.

Once you have downloaded the file and made it ready for booting from a CD or DVD, you may proceed to install it. You will be asked in which language you want to install Ubuntu Linux operating system. Choose the desired language and hit Enter. Linux will be installed on your computer system.

## Chapter Two

### Working with Linux Commands

When we talk about the Linux command line, we refer to the Linux shell. The Linux shell is a program that accepts keyboard commands and passes them on to your operating system for execution. All Linux distributions have a shell program, namely, bash. The bash is the short form of Bourne Again Shell. This is a reference to the fact that bash is the next level version of sh, which was the original UNIX shell program.

When you are using a graphical user interface, you need another program, namely a terminal emulator for interaction with the Linux shell. If you look through the desktop menus, you will be able to locate one.

### Let's Start

It is time to start working on the command line of your Linux operating system. The first step that you need to take is to kick off the terminal emulator. Once you have opened it, you should be able to see the following line.

```
linuxbox1:~$
```

This is known as the shell prompt. You will see that whenever the Linux shell is ready to take in the input. It may vary in appearance based on the distribution you are using. If you see a (#) instead of a dollar sign ($), the terminal session will offer you superuser privileges. Either you will be logged in as a root user, or you have selected a terminal emulator that offers superuser privileges. Let us type something on the shell and see what it does for you.

```
linuxbox1:~$ hkkhhhhk
/bin/sh: hkkhhhhk: not found
```

If you want to check on your command history, you may check it out by pressing the up-arrow key. Whether you have written and entered a hundred commands, you will see all of them on the screen. When you press the down-arrow, the command history will disappear. You might be thinking that the command line is all about the keyboard. However, that is not the case. You may use a mouse with the terminal emulator.

### The First Commands for Your Linux Operating System

It is time to enter your first commands on your Linux system to see how the terminal works. These are the simplest commands that you will be using to do some common tasks. The first command on the line is the calendar command by which you can display a full calendar of the current month.

```
linuxbox1:~$ cal
January 2021
Su Mo Tu We Th Fr Sa
               1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
31
```

You can experiment with the date and time command as well. By entering a simple command, you may display the current time and data on your screen. See the following command.

```
linuxbox1:~$ date
Sun Jan 24 10:35:23 UTC 2021
```

When you are using an operating system, you will need to know the exact space on your system to keep the functioning of the system smooth and easy.

```
linuxbox1:~$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
/dev/root        5120000    2417728   2702272  47% /
devtmpfs         125912          0    125912   0% /dev
tmpfs            126068          8    126060   0% /run
none             126068          0    126068   0% /dev/shm
```

If you want to see the amount of free memory, you will have to enter the free command.

```
linuxbox1:~$ free
             total       used       free     shared    buff/cache   available
Mem:       252140       5252     245980          8         908       243104
Swap:           0          0          0
```

When you have finished your work and you want to end your terminal session, you simply write exit on the command line and close the terminal session.

### Basic Commands

This section of the chapter will walk you through the Unix commands and utilities. The first on the line is the cat command that will display the contents of a file. I will use the system information file and then get back to the shell prompt. This is one of the easiest commands to understand. You can get the output of one or more than one file and read through them.

Note: I will use Fedora distribution to test commands from now onwards.

### File Navigation in Linux

Most of you might have been familiar with a graphical user interface. It is very easy to navigate in that system. You see a perfect file tree to see different files on your system. You can open them and navigate through them in seconds. However, that is not the case in Linux. There is no graphical display of files in a Linux operating system. It’s better to look at the Linux file system as a maze. The directory in which you are currently present is the current directory. The directory above you is the parent directory. You can display the current working directory with the pwd command.

```
[gha@localhost ~]$ pwd
/root
```

#### The ls command

The ls command will display the contents of one of the directories in your system. The default is the current directory. You can use ls -l command to display a lengthier version of the file. You can also use the ls -F command to display the information of the type of files.

```
[gha@localhost ~]$ ls
bench.py  hello.c
```

You can change the current working directory by using the cd command. Just type cd in the shell and the pathname of the directory you want to work in. A pathname is a general route that you take along the branches of a tree to reach the directory you want. You can specify it in two ways. The first way is the absolute pathnames. An absolute pathname starts with the root directory, and it follows the tree branch by branch until the path to file or desired directory stands completed. Take the example of a directory on your system in which most of the system's programs are installed.

```
[gha@localhost ~]$ cd /usr/downloads
[gha@localhost downloads]$ pwd
/usr/downloads
[gha@localhost downloads]$ ls
```

This command will list the files in that directory. The ls command is one of the widely used commands in a Linux operating system. With this command's help, you can see the contents of a directory and determine the number of files and directory attributes. As you have seen, you can enter the ls command to see the list of files and subdirectories that are contained inside a current working directory.

```
[gha@localhost ~]$ ls /usr
bin games include lib lib64 libexec local sbin share src tmp
```

You can list the home directory of the user and the /usr by using the following command.

```
[gha@localhost ~]$ ls ~ /usr
/root:
bench.py  hello.c

/usr:
bin games include lib lib64 libexec local sbin share src tmp
```

You can add -l to the ls command to change the format of the display and reveal more details. By adding -l to the same ls command, you can change the output to a longer format.

### Options and Arguments Commands

Most Linux commands are made up of one character preceded by a dash. However, some are longer, with two dashes followed by a word, such as those in the GNU support project. Some commands even allow two or more shorter options to be tagged to one another. In the example you see below, we will give the ls command two options – the first (l) will reduce the long output, while the second (t) sorts the results by modification time.

Let us see the result of the -l command.

```
[gha@localhost ~]$ ls -l
total 8
```
