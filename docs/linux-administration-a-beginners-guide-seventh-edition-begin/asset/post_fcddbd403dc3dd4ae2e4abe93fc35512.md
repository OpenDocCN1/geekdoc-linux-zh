
# 44 Linux Administration: A Beginner's Guide

## Set Up the Disk Partition

Use the ARROW keys on your keyboard to select the Guided – Use Entire Disk And Set Up LVM option, as shown here, and then press ENTER.

![](img/9f6657924397c33f088db5321b751a83_70_0.png)

Another screen will appear, prompting you to select the disk to partition. Accept the default and press ENTER.
If prompted to write the changes to disk and configure LVM, select Yes and press ENTER. You might get a different prompt if you are installing the operating system on a disk with existing partitions or volumes. In that case, you will need to confirm that you want to remove any partitions or volumes in order to continue.

This section of the installer allows you to customize the actual partition structure of the system. It allows you to select up different file systems for different uses (such as /var, /home, and so on). The same concept used in creating the different partitions during the Fedora installation earlier transfers over to Ubuntu. For the sake of brevity, we will not show this on our sample system here. We will instead accept the default partition and LVM layout recommended by the installer. As a result, we will end up with only three file systems: /boot, (/root), and swap.

The Ubuntu server installer will prompt you to specify the amount of volume group to use for the guided partitioning. Accept the default value. Select Continue and press ENTER.

# CHAPTER 2 Installing Linux in a Server Configuration

A summary of the disk partitions and LVM layout will be displayed in the next screen. You will be prompted to write the changes to disk. Select Yes and press ENTER. The base software installation begins.

> NOTE You might be prompted for proxy server information at some point during this stage of the installation. You can safely ignore the prompt, select Continue, and press ENTER.

## Other Miscellaneous Tasks

You'll see a Configuring Tasks asking you to select how to manage upgrades on the system. Select the No Automatic Updates option and press ENTER.

The next screen will inform you that your system has only the core system software installed. Since we are not ready to do any software customization at this time, ignore this section and press ENTER to continue.

When you are presented with a screen asking to install the GRUB boot loader to the master boot record, select Yes, and press ENTER.

You will be presented with the Installation Complete screen and a prompt to remove the installation media. Press ENTER to continue. The installer will complete the installation process and then reboot the system.

Once the system reboots, you will be presented with a simple login prompt (see Figure 2-5). You can log in as the user that was previously created during the installation. The username is master and the password is 72erty7!

![](img/9f6657924397c33f088db5321b751a83_71_0.png)

Figure 2-5 Classic Ubuntu Linux login prompt

# Summary

You have successfully completed the installation process. If you are having problems with the installation, be sure to visit Fedora's web site at https://getfedora.org and the Ubuntu web site at www.ubuntu.com and take a look at the various manuals and tips available.

The version release notes are also a good resource for specific installation issues. Even though the install process discussed in this chapter used Fedora as the operating system of choice (with a quick overview of the Ubuntu Server install process), you can rest assured that the installation concepts for other Linux distributions are virtually identical. The install steps also introduced you to some Linux/UNIX-specific concepts that will be covered in more detail in later chapters (for example, hard disk naming conventions, partitioning, volume management, network configuration, software management, and so on).

# CHAPTER 3 | The Command Line

# Linux Administration: A Beginner's Guide

the level of power, control, and flexibility that the command line offers Linux/UNIX users have one of its most enduring qualities. There is also a flip side to this, however: for the uninitiated, the command line can also produce extremes of emotions, including awe, frustration, and annoyance. Casual observers of Linux/UNIX gurus are often astonished at the results of a few crafted and executed commands. Unfortunately, this power comes at a cost—it can make Linux/UNIX appear less intuitive to the average user. For this reason, graphical user interface (GUI) front-ends for various Linux/Linux tools, functions, and utilities have been written.

More experienced users, however, may find it difficult for a GUI to present all of the available options. Typically, doing so would make the interface as complicated as the command-line equivalent, and experienced users ultimately return to the comprehensive capabilities of the command line. After all is said and done, the fact remains that it looks plain cool to do things at the command line.

Before we begin our study of the command-line interface under Linux, understand that this chapter is far from an exhaustive resource. Rather than trying to cover all the tools without any depth, this chapter describes a handful of tools that are most critical for the day-to-day work of a system administrator.

> NOTE This chapter assumes that you are logged into the system as a regular/privileged user. You can find the examples whether you are logged into the system or via a GUI desktop environment. If you are using the GNOME desktop environment, for example, you can start a virtual machine in which to launch. To launch a virtual application, simultaneously press the ALT+F2 key combination on your keyboard to bring up the Run dialog box. Type the name of a terminal.

## An Introduction to Bash

In this section, we examine some of Bash's built-in commands. A complete reference on Bash could easily fill a book, so we'll stick with the commands that a system administrator (or regular user) might use frequently. However, it is highly recommended that you study Bash's other functions and operations. As you get accustomed to Bash, you will find it easy to pick up and adapt to the subtle nuances of other shells—well, in other words, the differences between them are subtle. If you are managing a large site with lots of users, it will be advantageous for you to be familiar with many shells as possible.

The formal definition of a shell is "a language interpreter that executes commands." A less formal definition might be "a program that provides an interface to the system." The Bourne Again Shell (Bash), in particular, is a command-line interpreter that is used when a user logs into the system.

# CHAPTER 3 The Command Line 49

## Job Control

When working in the Bash environment, you can start multiple programs from the same prompt. Each program is considered a job. Whenever a job is started, it takes over the terminal. On today, either the straight text interface you see boot your machine or the window created by the X Window System on which Bash runs (The terminal interfaces in X Window System are called terminals, or for short.) If a job has control of the terminal, it can issue control codes so that text-only interfaces (the mail reader, for instance) can be made more attractive. Once the program is done, it gives full control back to Bash, and a prompt is rediscovered for the user.

Not all programs require this kind of terminal control, however. Some, programs that interface with the user through the X Window System, can be instructed to give up terminal control and allow Bash to bring back (re-present) the user prompt, even though the invoked program is still running.

In the following example, with the user master logged into the system via a graphical desktop environment, the user launches the Firefox web browser from the command line, with the additional condition that the program (Firefox) gives up control of the terminal (this condition is specified by appending the ampersand symbol to the program name):

```
[master@server ~]$ firefox &
```

Immediately after you press ENTER, Bash will present its prompt again. This is called backgrounding the task.

If a program is already running and has control of the terminal, you can make the program give up control by pressing CTRL-Z in the terminal window. This will stop the running job (or program) and return control to Bash so that you can enter new commands.
