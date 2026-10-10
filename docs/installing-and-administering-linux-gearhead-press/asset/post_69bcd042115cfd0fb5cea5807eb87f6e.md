
### 2. When invoking shell scripts, which permissions among the following must be given to the script file?
- drwsxrxwx
- r but not necessarily w or x
- x and r
- 755
- -rw-r-xr-x
- r but not necessarily w or x and -rw-r-xr-x
- r but not necessarily w or x; x and r
- -rw-r-xr-x

### 3. How would you handle making variables available to subshells?
- Define the variable inside the script.
- Recreate the variable in the new shell.
- Export the variable.
- Place all new variables required in a file.

### 4. How could you guarantee that whoever ran your script would run it in a bash environment?

### 5. Will the following script print true or false?

```
#!/bin/bash
T1="foo"
T2="bar"
if [ "$T1" = "$T2" ] ; then
    echo This script evaluates as true
else
    echo This script evaluates as false
fi
```

### 6. Using the same script, if we were to export T2="foo", would it change how the script evaluates?

See Appendix C for answers.

# CHAPTER 14
# The Linux X Window System

Thus far, we have concentrated on Linux at the command line. Depending on your information source, that is also called

- At the character cell prompt
- At the console
- In the ASCII character environment

Although it seems to be an outmoded way of doing things—especially when there are so many GUIs available for a price or for free—for effective Linux usage and especially administration, we often rely on our ability to use and understand command-line concepts, commands, and utilities.

Linux also has powerful and flexible GUI capabilities, however. This chapter provides an introduction to the GUI foundation, called the X Window System. We wholeheartedly recommend installing the X Window System when you first install Linux on your system (our preference) or later after Linux has been installed. After you properly install and configure X, it will facilitate your productivity and enjoyment and will enable you to use many more Linux/UNIX programs.

> **WARNING** For those who are planning to install X Window System, we echo the advice of all X installers: Pay special attention to your system’s video card and monitor specifications. Failure to do so could result in system or monitor damage.

Meanwhile, some of the concepts in this chapter (and the way we explain them) will seem to be very basic—even trivial to some (dare we say, “most?”). If so, we apologize. But it is still very important to form a proper knowledge foundation. Also, you never know when you might find a “pearl” among these oysters. Hey, some people like oysters. I know I do.

## A Brief History

The first X Window System was developed in 1984 by the *Massachusetts Institute of Technology* (MIT). The X Window System, which is often referred to as X or X11, provides a powerful network-based foundation for a Linux/UNIX GUI environment. X is a collection of programs, including servers, documentation, fonts, programming libraries, and utilities, but its foundation programs are as follows:

- A basic windowing program that provides windowing services
- The X Network Protocol, a protocol for network communication
- A low-level interface called Xlib, which sits between the higher-level programs (on top) and the network or base system (on the bottom)
- A “window manager”—an X application to control the type and appearances of the windows

The X Window System enhances UNIX in the same way that the “other GUI operating system” enhances (or enhanced at one time) DOS, only more reliably. What do we mean by *enhance?* Some advantages and features of GUIs are listed next:

- An attractive and intuitive (that is, easy-to-use) human-to-machine interface
- Potentially easier ways of identifying, entering, and modifying data
- Several control devices that require no knowledge of programming or other commands (for example, buttons, icons, menus, and scrollbars)
- Consistency of look and utility, which leads to reduced training requirements for new applications
- Greater ease in managing multiple and simultaneous processes and applications

Now, all is not perfect in the world of GUIs. GUI programs by nature are generally large and rather inefficient because they tend to use a lot of resources. They have to write or call upon many controlling functions for window manipulation, graphics output, and data input from a keyboard and a mouse. In short, GUIs require more resources than the command line but can also make complex programs easier to use.

Since the birth of X in 1984, commercial vendors---particularly the vendor- and researcher-based organization called the X Consortium, whose membership includes IBM, Digital Equipment, and MIT---have effectively made X the UNIX industry standard. X is installed on most UNIX systems around the world.

A free software conversion (in other words, a free “port”) of X for Linux and other UNIX variants, called XFree86, was developed by the XFree86 Project Inc. (now a member of the X Consortium). XFree86 is a version of MIT’s X Window System v. 11, rel. 6 (that is, X11R6).

If XFree86 is installed on this, you will see several X11R6 references as part of directory or filenames. The original X version 11 was released in 1987, release 6 came out in 1994, and the latest version is X11R6.4. As of this writing, the latest release of XFree86 is 4.1.0. Your version of XFree86 probably has all the binary files, support files, libraries, and tools that you will need. If not, check the XFree86 Project Internet site at www.XFree86.org. You can also check that Web site for the latest version of XFree86.

## X Window Networking

In Figure 14.1, we illustrate a simplified X Window System network consisting of various types of machines. In an environment like this one, an X application could run on any processor or even on one type of processor. A user or administrator could sit at any other system on the network and run an X Window application. Thus, we can claim that X is platform independent. X enables a display and keyboard attached to one system to use programs (that is, clients) running on a completely different system---even a completely different type of system.

![](img/cae5c706c216875d12d4b7d28144cc71_441_0.png)

X Window System functions are split into terminal and application support. Typically, the application support runs on a Linux/UNIX system. The terminal support can run on the same Linux/UNIX system, on a remote Linux/UNIX system, or even on a non-Linux/UNIX system. An example of the last two systems is one that might have a slow CPU of its own or might have no hard disk drive. The client applications would run on a remote, fast central server while only the terminal-supporting X Window server would run on the underpowered terminal. For this reason, we refer to the X Window System as a networking window system. Any connections between the client and the server are TCP/IP protocol-based connections.

## Different Client/Server Environment Concepts

For those who do not customarily operate in UNIX X environments, the concepts of client and server are generally understood to be the following:

- A server is a system that provides resources such as applications, hard drive storage, modems, printers, and so on to other systems across one or more networks.
- A client is a system that uses those resources, accessing them across one or more networks. In the Linux/UNIX environment, however, the client and server concepts are different.

In the world of the Linux/UNIX X Window system, however, a client is defined as a device-independent program that runs on your local machine or on a remote machine and requires input from the user and the capability to display or otherwise provide output to the user. In other words, the client is the system or machine providing the application support.

Common applications, such as xcalc and xclock as well as the more complicated database or simulation applications, are clients to a Linux/UNIX X system.

On the other hand, a server is a device-dependent program that runs on your local machine and controls the input devices (for example, keyboard and mouse) as well as the terminal display and other output devices. We say that the server is the system or machine providing the terminal support. In many cases—especially in a small network or home environment—the client and the server run on the same system. Even so, they still communicate with each other by using the TCP/IP protocol.

## X Client Features

A user interacts with X clients when he or she interacts with applications (such as xclock, xcalc, and xterm) that might be running on either a local machine or on a remote machine. The applications themselves are the X clients that are invoked and run by the users in an X window system.

X clients can be started from the command line by special startup files or from other X clients. For example, you can start window managers manually or invoke them automatically when your machine boots up. To access remote machines, you might need special applications invoked on a local machine (for example, WRQ Inc.'s product, ReflectionX/E, enables Windows machines to access UNIX machines. Their Web site, if you are interested, is www.wrq.com.

Most X clients share the same or similar options, such as foreground color, background color, display name, fonts, and window geometry. For example, invoke xterm ? on the command line. Examine the specifications and options. Then, invoke xclock ? and compare those specifications.
