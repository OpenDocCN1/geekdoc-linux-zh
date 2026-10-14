
# Table 13-4: Cursor Movement Escape Sequences

| Escape Code | Action |
|---|---|
| `\033[1;ch` | Move the cursor to line 1 and column c. |
| `\033[nA` | Move the cursor up n lines. |
| `\033[nB` | Move the cursor down n lines. |
| `\033[nC` | Move the cursor forward n characters. |
| `\033[nD` | Move the cursor backward n characters. |
| `\033[2J` | Clear the screen and move the cursor to the upper-left corner (line 0, column 0). |
| `\033[K` | Clear from the cursor position to the end of the current line. |
| `\033[s` | Store the current cursor position. |
| `\033[u` | Recall the stored cursor position. |

Using these codes, we’ll construct a prompt that draws a red bar at the top of the screen containing a clock (rendered in yellow text) each time the prompt is displayed. The code for the prompt is this formidable looking string:

```
PS1="\[\033[s\033[0;41m\033[K\033[1;33m\t\033[0m\033[u\]\u@\h \W\$ "
```

# Table 13-5: Breakdown of Complex Prompt String

| Sequence | Action |
|---|---|
| `\[` | Begins a non-printing character sequence. The real purpose of this is to allow bash to correctly calculate the size of the visible prompt. Without this, command line editing features will improperly position the cursor. |
| `\033[s` | Store the cursor position. This is needed to return to the prompt location after the bar and clock have been drawn at the top of the screen. *Be aware that some terminal emulators do not honor this code.* |
| `\033[0;0H` | Move the cursor to the upper-left corner, which is line 0, column 0. |
| `\033[0;41m` | Set the background color to red. |

# PART 3

# COMMON TASKS AND
ESSENTIAL TOOLS

# 14

# PACKAGE MANAGEMENT

If we spend any time in the Linux community, we hear many opinions as to which of the many Linux distributions is “best.” Often, these discussions get really silly, focusing on such things as the prettiness of the desktop background (some people won’t use Ubuntu because of its default color scheme!) and other trivial matters.

The most important determinant of distribution quality is the *packaging system* and the vitality of the distribution’s support community. As we spend more time with Linux, we see that its software landscape is extremely dynamic. Things are constantly changing. Most of the top-tier Linux distributions release new versions every six months and many individual program updates every day. To keep up with this blizzard of software, we need good tools for package management.

*Package management* is a method of installing and maintaining software on the system. Today, most people can satisfy all of their software needs by installing *packages* from their Linux distributor. This contrasts with the early days of Linux, when one had to download and compile *source code* in order to install software. Not that there is anything wrong with compiling source code; in fact, having access to source code is the great wonder of Linux. It gives us (and everybody else) the ability to examine and improve the system. It’s just that working with a precompiled package is faster and easier.

In this chapter, we will look at some of the command-line tools used for package management. While all of the major distributions provide powerful and sophisticated graphical programs for maintaining the system, it is important to learn about the command-line programs, too. They can perform many tasks that are difficult (or impossible) to do using their graphical counterparts.

# Packaging Systems

Different distributions use different packaging systems, and as a general rule a package intended for one distribution is not compatible with another distribution. Most distributions fall into one of two camps of packaging technologies: the Debian .deb camp and the Red Hat .rpm camp. There are some important exceptions, such as Gentoo, Slackware, and Foresight, but most others use one of the two basic systems shown in Table 14-1.

# Table 14-1: Major Packaging System Families

| Packaging System | Distributions (partial listing) |
|---|---|
| Debian style (.deb) | Debian, Ubuntu, Xandros, Linspire |
| Red Hat style (.rpm) | Fedora, CentOS, Red Hat Enterprise Linux, openSUSE, Mandriva, PCLinuxOS |

# How a Package System Works

The method of software distribution found in the proprietary software industry usually entails buying a piece of installation media such as an "install disk" and then running an "installation wizard" to install a new application on the system.

Linux doesn’t work that way. Virtually all software for a Linux system is found on the Internet. Most of it is provided by the distribution vendor in the form of package files, and the rest is available in source code form, which can be installed manually. We’ll talk a little about how to install software by compiling source code in Chapter 23.

# Package Files

The basic unit of software in a packaging system is the package file. A package file is a compressed collection of files that comprise the software package. A package may consist of numerous programs and data files that support the programs. In addition to the files to be installed, the package file also includes metadata about the package, such as a text description of the
