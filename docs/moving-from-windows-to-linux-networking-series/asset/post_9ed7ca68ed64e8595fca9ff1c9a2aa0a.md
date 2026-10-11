
## Run Levels and init

This chapter is about Linux administration from the shell, and the most fundamental administrative task would be to shut down or reboot the machine. As even a casual Windows user, you realize that turning the power off repeatedly is not very good for your system. With Windows XP you would go to the Start menu and choose Turn Off the Computer, and you would be presented with a screen like what you see in Figure 19.1.

![](img/12d790664598bbf390261087fbe55bbc_384_0.png)

Before the advent of Windows 95, Windows 3.1 was a desktop environment separate from the underlying operating system, DOS, and you could invoke Windows from DOS by typing in `win`. With a shell in Linux, you will still need a way to shut down the machine, reboot the machine, or invoke the desktop environment. In the shell you accomplish all of this with run levels.

### Run Levels

A run level is the level at which your system is currently running or operating. You can change the run level any time you like from the shell by typing in `init` followed by the number designating the run level you want to use. There are six run levels in all. Each designates that progressively more of the system is functioning. Run level 0 designates that the system is shut down. Run level 1 indicates the system is running in shell mode only, no graphical interface and no network support. This moves progressively to run level 5, which means that full network support and a graphical desktop environment such as KDE or GNOME is running. The last run level is 6, which designates a reboot. All of the run levels are summarized in Table 19.1.

Table 19.1: Run Levels

| Run Level | Purpose |
| :--- | :--- |
| 0 | This is a complete system shutdown. You invoke this run level by typing `init 0` at the shell. In Windows you can accomplish the same thing by clicking on the Start button and then clicking on Shut Down. |
| 1 | This is single-user mode. There is no support for any network or Internet connection and no support for any graphical desktop environment. This is similar to the Safe Mode in Windows. You invoke this run level by typing `init 1` at the shell. |
| 2 | This is multiuser mode without any graphical interface and without network support. You invoke this run level by typing `init 2` at the shell. |
| 3 | This is full multiuser mode with all functionality except a graphical desktop. This run level is often used for servers that do not require a graphical interface. You invoke this run level by typing `init 3` at the shell. |
| 4 | This run level is unused at this time. |
| 5 | This run level is a complete system with multiuser capability, full network support, and a graphical desktop environment. This is most often used for personal workstations. You invoke this run level by typing `init 5` at the shell. |
| 6 | This is a system reboot. You invoke this run level by typing `init 6` at the shell. |

What all of this means is that if you type `init 0` from the shell, the machine will commence its shutdown process. However, if you type `init 6`, the machine will reboot. This may lead you to ask, what is this `init`? The `init` command, like all shell commands, is a program built into Linux shells. The `init` program is very important. In fact, it is absolutely essential to the operation of a Linux system. The `init` program literally initializes your system. When used as a shell command, it initializes your system to the specified run level. This is why it is also used to invoke certain specified run levels. When you type in `init 6`, you are saying to initialize the machine to run level 6. You can see this in Figure 19.2.

![](img/12d790664598bbf390261087fbe55bbc_385_0.png)

### init

It is important that you recall that all shell commands are actually programs. As was previously mentioned, the `init` program just happens to be a very important one. What is it that `init` does that is so important and how does it work? Some readers may not want this level of detail about `init` and should feel free to skip the following paragraphs. However, for the curious reader who wants to understand what is happening in the background, the following few paragraphs will explain quite a bit. The `init` program works to initialize the machine. It takes over the boot process as soon as the Linux kernel is done loading into memory. The Linux kernel finishes its part of the boot process by starting the `init` program. This means that `init` is always the first process on your machine, and that is why its process number is always 1. `init`, like all commands is really a program, and can be found in the directory `/sbin/init`. If the kernel can't find `init`, it tries to run `/bin/sh`, and if that also fails, the startup of the system fails.

When `init` starts, it completes the boot process by performing a number of administrative tasks. The `init` program will start by checking filesystems, starting various services, and starting the `getty` process. The `getty` process handles input from the keyboard. You might not have thought about it before, but there must be a process on your machine to handle everything your computer needs to do. With operating systems such as Windows, all of that is transparent to you. You cannot access background system processes, and even system administrators are often unaware of their existence. However, Linux and all Unix-like systems allow you to access many fundamental system processes.

**Note** Most university computer science programs include coursework on Unix or Linux. It often is either required or highly recommended. The reason for this emphasis on Unix-like systems is the aforementioned access to the underlying processes. For a computer science student, even one who may never professionally work with Linux or Unix, the ability to look into the fundamental mechanisms of the operating system is crucial to his learning process.

## The Filesystem

Every operating system must organize the files on the computer in some fashion. You may recall that early on in this book we discussed file systems. Every operating system has certain directories that are of paramount importance. In Windows, the actual operating system is stored in the `windows` directory on your root drive, usually your `C` drive. In most cases, you will find Windows in `c:\windows`. Beneath the `windows` directory you will see a number of subdirectories, such as `system` and `system32`. The entire `windows` directory, with its subdirectories, contains files that are critical to your computer functioning. Unless you have some advanced knowledge of the Windows operating system, you should not tamper with anything in these directories.

Other important directories include `Program Files` shown in Figure 19.3. This is where most programs will be installed by default. This is also generally on the root drive. You also have probably noticed a default `document` directory on Windows machines. This is a directory that the operating system creates for you. It is meant to contain items that are considered crucial or fundamental to the system’s normal operation.

![](img/12d790664598bbf390261087fbe55bbc_386_0.png)

**Note** It was mentioned briefly earlier in this book but must be emphasized again that Windows refers to a directory as a folder. They are the same things. In this book we will use the terms interchangeably.

Since we are using the phrase *root drive*, it might be prudent to define that term. Do not confuse the root drive of any operating system with the root user. The root user, in Unix and Unix-like systems, is the system administrator. In Windows the root user is referred to as the administrator. The root drive or directory, for any operating system, is the main directory. For example, if you have three hard drives in your system, or one hard drive divided into three partitions, the one that contains the operating system is the root drive.

As was mentioned previously, in any operating system there are certain key directories. These directories hold certain types of files. This is true in Linux as well as Windows. Let’s examine some of those directories and what they contain. There are several directories in Linux, each with its own particular purpose. The File Manager, shown in Figure 19.4, is showing all the top-level directories. We will examine several of these in the following pages.
