
# 14 CHAPTER 1 WELCOME TO LINUX

![](img/45ff4cd21497435daa35084a84b95d07_64_0.png)

**Figure 1-2** The Linux filesystem structure

files by grouping related files in directories. Each user has one primary directory and as many subdirectories as required (Figure 1-2).

Standards With the idea of making life easier for system administrators and software developers, a group got together over the Internet and developed the Linux Filesystem Hierarchy Standard (FHS, FHS). Before this standard was adopted, key programs were located in different places in Linux distributions. Today you can sit down a Linux system and expect to find any given standard at a consistent location (page 213).

Links A link allows a given file to be accessed in the same directory as the original file or in another directory. Generic links can make the same file appear in several users' directories, enabling those users to share the file easily. Windows uses the term *shortcut* in place of *link* to describe this capability. Macintosh users will be more familiar with the term *alias*. Under Linux, an *alias* is different from a *link*; it is a command feature provided by Unix (page 346).

Security Like most multiser operating systems, Linux allows users to protect their data from access by other users. It also allows users to share selected data and programs with other users by means of a simple but effective protection scheme. This level of security is provided by file permissions, which limit the users who can read from, write to, or execute a file. More recently, Linux has implemented Access Control Lists (ACLs), which give users and administrators finer-grained control over file access permissions.

## THE SHELL: COMMAND INTERPRETER AND PROGRAMMING LANGUAGE

In a textual environment, the shell—the command interpreter—acts as an interface between you and the operating system. When you enter a command on the screen, the shell interprets the command and calls the program you want. A number of shells are available for Linux. The four most popular shells are

## OVERVIEW OF LINUX

- *The Bourne Again Shell (bash), an enhanced version of the original Bourne Shell (the original UNIX shell).
- *The Debian Almquist Shell (dash; page 292), a smaller version of bash, with fewer features. Most startup shell scripts dash in place of bash to speed the boot process.
- *The TC Shell (tsh), an enhanced version of the C Shell, developed as BSD UNIX.
- *The Z Shell (zsh), which incorporates features from a number of shells, including the Korn Shell.

Different users may prefer different shells, multiuser systems can have different shells in use at any given time. The choice of shells demonstrates one of the advantages of the Linux operating system: the ability to provide a customized interface for each user.

Shell scripts Besides performing its function of interpreting commands from a keyboard and sending commands to the operating system, the shell is a high-level programming language. Shell commands can be arranged in a file for later execution (Linux calls these files shell scripts; Windows calls them batch files). This flexibility allows users to perform complex operations with relative ease, often by issuing short commands, or to work with surprisingly little effort elaborate programs that perform highly complex operations.

## FILENAME GENERATION

Wildcards ambiguous file references When you run commands to be processed, you can construct patterns using characters that have special meanings to the shell. These characters are called wildcard characters. The patterns, which are called ambiguous file references, are a kind of shorthand: Rather than typing in complete filenames, you can type patterns; the shell expands these patterns into matching filenames. An ambiguous file reference can save you the effort of typing in a long filename or a group of similar filenames. For example, the shell might extend the pattern mak* to make-3.80.tar.gz. Patterns can also be useful when you know only part of a filename or cannot remember the exact spelling of a filename.

## COMPLETION

In conjunction with the Readline library, the shell performs completion, filename, pathname, and variable completion: You type a prefix and press ESC, and the shell lists the items that begin with that prefix or completes the item if the shell provides a unique item.

## DEVICE-INDEPENDENT INPUT AND OUTPUT

Redirection Devices (as a printer or a terminal) and disk files appear as files to programs. When you give a command to the Linux operating system, you can instruct it to send the output to any of several devices or files. This diversion is called output redirection.

In a similar manner, a program's input, which normally comes from a keyboard, can be redirected so that it comes from a disk file instead. Input and output can be device independent; that is, they can be redirected to or from any appropriate device.

As an example, the cat utility normally displays the contents of the file on the screen. When you run a cat command, you can easily redirect its output to go to a disk file instead of the screen.

## SHELL FUNCTIONS

One of the most important features of the shell is that users can use it as a programming language. Because the shell is an interpreter, it does not compile programs for it but rather interprets programs each time they are loaded from the disk. Loading and interpreting programs is time-consuming.

Many shells, including the Bourne Again Shell, use shell functions that the shell holds in memory so it does not have to read them from the disk each time you execute them. The shell also functions in an internal format so it does not have to spend as much time interpreting them.

## JOB CONTROL

job control is a shell feature that allows users to work on several jobs at once, switching back and forth between them as desired. When you start a job, it frequently runs in the foreground so it is connected to the terminal. Using job control, you can move the job to the background and continue working on others. If a background job needs your attention, you can move it to the foreground. (The concept of job control originated with BSD UNIX.)

## A LARGE COLLECTION OF USEFUL UTILITIES

Linux includes a family of several hundred programs, often referred to as utilities. Most tools found on UNIX exist for Linux, but in some cases these tools have been replaced by more modern counterparts. This section describes some of the popular tools and features available under Linux. The man (for manual) and info utilities provide online documentation for Linux.

## INTERPROCESS COMMUNICATION

Linux enables users to establish both pipes and filters on the command line. A pipe sends the output of one program to another. A filter is a special kind of pipe that processes input data to yield output data. Pipes and filters frequently join utilities to perform a specific task. For example, you use a pipe to send the output of head (a filter that lists the ten lines of its input) to a third utility, lpr, which sends the data to a printer.

## SYSTEM ADMINISTRATION

On a Linux system the system administrator is frequently the owner and only user of the system. This person has many responsibilities. The first responsibility may be set up the system, install the software, and possibly edit configuration files. Once the system is up and running, the system administrator is responsible for downloading and installing software (including upgrading the operating system), backing up and restoring files, and managing such system facilities as printers, terminals, servers, and a local network. The system administrator is also responsible for setting up accounts for new users on a multiuser system, monitoring the system and taking care of any problems that arise.

## ADDITIONAL FEATURES OF LINUX

The developers of Linux included features from BSD, System V, and Sun Microsystems' Solaris, as well as new features, in their operating system. This section describes some of the popular tools and features available under Linux.

## GUIS

The Window System (also called X or X11) was developed in part by researchers at MIT (Massachusetts Institute of Technology) and provides the foundation for the GUIs with Linux. Given a terminal or workstation screen that supports X, a user can interact with the computer through multiple windows on the screen, display graphical information, or use special-purpose applications to draw pictures, monitor processes, or preview formatted output.

A desktop manager is a picture-oriented interface that enables you to interact with system programs by manipulating icons instead of typing the corresponding commands to a shell.
