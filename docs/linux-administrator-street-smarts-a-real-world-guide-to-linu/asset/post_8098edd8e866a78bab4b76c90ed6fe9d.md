
4.3 Given security requirements, implement appropriate encryption configuration (for example: `blowfish` 3DES, MD5)

4.4 Detect symptoms that indicate a machine’s security has been compromised (for example: review logfiles for irregularities or intrusion attempts)

4.5 Use appropriate access level for login (for example: `root` level vs user level activities, `su`, `sudo`)

4.6 Set process and special permissions (for example: SUID, GUID)

4.7 Identify different Linux Intrusion Detection Systems (IDS) (for example: Snort, PortSentry)

4.8 Given security requirements, implement basic IP tables/chains (note: requires knowledge of common ports)

4.9 Implement security auditing for files and authentication

4.10 Identify whether a package or file has been corrupted / altered (for example: checksum, Tripwire)

4.11 Given a set of security requirements, set password policies to match (complexity / aging / shadowed passwords) (for example: identify systems not shadow passwords)

4.12 Identify security vulnerabilities within Linux services

4.13 Set up user-level security (i.e., limits on logins, memory usage and processes)

## Domain 5.0 Documentation

5.1 Establish and monitor system performance baseline (for example: `top`, `sar`, `vmstat`, `pstree`)

5.2 Create written procedures for installation, configuration, security and management

5.3 Document installed configuration (for example: installed packages, package options, TCP/IP assignment list, changes—configuration and maintenance)

5.4 Troubleshoot errors using systems logs (for example: `tail`, `head`, `grep`)

5.5 Troubleshoot application errors using application logs (for example: `tail`, `head`, `grep`)

5.6 Access system documentation and help files (for example: `man`, `info`, readme, Web)

## Domain 6.0 Hardware

6.1 Describe common hardware components and resources (for example: connectors, IRQs, DMA, SCSI, memory addresses)

6.2 Diagnose hardware issues using Linux tools (for example: `/proc`, disk utilities, `ifconfig`, `/dev`, live CD rescue disk, `dmesg`)

6.3 Identify and configure removable system hardware (for example: PCMCIA, USB, IEEE1394)

6.4 Configure advanced power management and Advanced Configuration and Power Interface (ACPI)

6.5 Identify and configure mass storage devices and RAID (for example: SCSI, ATA/IDE, tape, optical recordable)

# Phase 1

# Working on the Command Line

![](img/f430a19bdf014c43ad7c2d594afd5b21_28_0.png)

Linux's tools for running programs and manipulating files are simple, unglamorous, and powerful. Although you can use GUI tools to drag and drop files, real Linux street smarts requires you to be able to manage your files from the command line by using odd-sounding commands such as `ls`, `cp`, `ln`, and `mv`. In the first few tasks of this phase, you'll learn to use some of the most basic of these tools. Don't think that the basic nature of these commands is unimportant, though; like the foundation of a house, these commands support more dramatic parts of the structure. Specific tasks described in this phase include using basic command-line features; managing files, directories, and links; finding files; and editing files.

Later tasks in this phase go further, examining streams, pipes, redirection, the shell environment, and shell scripts. You'll also learn about managing accounts. Most of the tasks in this phase assume you have both a normal user account and **root** access, but you must also be able to create, delete, and otherwise manage normal user accounts for yourself or other users of a Linux system.

> NOTE: This phase maps to portions of the CompTIA Linux+ objectives 2 and 3 and to portions of the LPIC objectives 103, 104, 109, and 111.

## Task 1.1: Use Basic Command-Line Features

Before delving into the details of commands used to manage, find, and manipulate files, you must be able to use basic command-line features. Linux supports several *shells*, which are programs that accept typed commands and display their output. Some shell commands are built into the shell, but many others are actually external programs. Knowing how to use your shell's features will enable to you to be more productive at the Linux command line. The most common Linux shell is the Bourne Again Shell (*bash*), and it is the one described here. Other shells, such as *tcsh* and *zsh*, support similar features, although some details differ.

### Scenario

A user is experiencing problems with the *what is* program, a standard Linux script that the user frequently runs. As the administrator, you must check that this script exists and that it's not obviously corrupt. In the process, you'll use several important Linux command-line features.

> NOTE
>
> Actually correcting a problem such as the one described here is likely to require the use of Linux's package management tools. These are described in Phase 3, “Managing Software.”

### Scope of Task

This task is fairly straightforward. It requires little time and effort. You might want to continue experimenting with **bash** after you’ve completed this task, though.

### Duration

This task will take about half an hour to complete. Once you’re familiar with the commands, using each one takes just seconds.

### Setup

You must have access to a working Linux system. For the specific examples shown in this task, your system should be configured to give you a **bash** shell by default and the **what is** program must be installed. Both of these conditions are usually true. If your Linux computer is not currently turned on, do so now and wait for it to finish booting.

### Caveats

Most Linux systems configure **bash** as the default shell for all users. If your account is configured to use **tcsh** or some other shell, some of the commands and procedures described here won’t work. Even with **bash**, a few details differ from one account or computer to another. Most commonly, the form of the command prompt varies from one system to another and sometimes even from one account to another. For simplicity and brevity, this book denotes user shell commands with a leading dollar sign ($), which is often used as part of real **bash** prompts, as in:

```
$ ls
```

This line means to type **ls** at a user command prompt. Some systems use a prompt that ends in a greater-than sign (>) instead of a dollar sign.

Most Linux systems provide a different prompt (often terminating in a hash mark, #) for the superuser (**root**) account. When a command must be typed as **root**, this book shows command lines beginning with this symbol:

```
# ls
```

When short commands appear inside paragraph text, the prompt ($ or #) is omitted.

## Procedure

To complete this task, you must log into your account on the affected workstation and enter several Linux commands. In the process, you'll learn how to type and edit commands, how to use command completion, and how to use command history. You'll also learn a few of the more common Linux commands.

### Logging In

The first task is logging into the Linux system. From the console, there are two ways to log in: using a graphical user interface (GUI) login manager or using a text-mode console. In either case, you type your username and then your password, typically in response to a **login** or **username** prompt and a **password** prompt, respectively.

Upon a successful text-mode login, you'll be greeted by a Linux command prompt and you can begin issuing Linux commands. GUI logins, though, present you with a graphical desktop environment—probably the K Desktop Environment (KDE) or the GNU Network Object Model Environment (GNOME). Although GUI desktop environments are convenient for end users, they don't usually present you with a text shell by default. To access one, you must locate an appropriate option from the menuing system. Look for entries called Shell, Terminal, or **xterm**. If all else fails, look for an option to run a command by name and type **xterm** in the dialog box. This should launch an **xterm** window, as shown in Figure 1.1. Your default shell should be running in this window.

If your computer displays a GUI login prompt but you'd prefer to work in a purely text-mode session, press Ctrl+Alt+F1. This key sequence switches to the first virtual console, which normally holds a text-mode session. You can switch between several (usually six) text-mode consoles by pressing Alt+F1 through Alt+F6 for each of the first six virtual consoles. The X Window System, Linux's GUI environment, normally runs in virtual console 7, so pressing Alt+F7 from a text-mode session switches to X if it's running.

FIGURE 1.1 An xterm window enables you to type text-mode commands in a GUI session.

![](img/f430a19bdf014c43ad7c2d594afd5b21_30_0.png)
