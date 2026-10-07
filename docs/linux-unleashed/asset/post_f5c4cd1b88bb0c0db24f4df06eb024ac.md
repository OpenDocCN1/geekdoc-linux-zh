
## World Wide Web

  Everyone is using the World Wide Web (WWW) and you can use it to obtain a copy of Linux from one of several different Web sites. The primary FTP site offers Web access through the URL:

`http://sunsite.unc.edu/mdw/linux.html`

You can use any Web client software, such as Mosaic or Netscape, to access the Web site and use the menu-driven system to download a copy of the Linux files. Most Linux Web sites also offer documentation files.

There are many different Linux support Web sites on the Internet now, too many to list. Use your favorite search engine (such as `yahoo.com` or `altavista.digital.com`) and use the keyword Linux. You'll get an overwhelming list of matches. You can usually narrow the search with keywords like “binaries” or a specific version (such as “Slackware”).

### Email

If you don't have access to a Linux distribution site through the Internet's FTP or Web services, you can still get the files transferred to you if you have email. This is an alternative for those using online systems which allow Internet mail but do not allow direct access to FTP sites and for some corporate systems that do not allow you to dial out directly to reach FTP sites but can transfer email. To get Linux by email from an FTP site, you can use the site's `ftpmail` utility.

All of the sites mentioned above in the Linux FTP site list support `ftpmail`. To get complete instructions on using `ftpmail`, all you need to do is send an email message to `ftpmail` login at one of the sites (for example, address your email to `ftpmail@sun-site.unc.edu`). The body of the email message should have only the word “help” in it. Any other comments may cause the `ftpmail` utility to incorrectly process your request. For this reason, you may want to suppress any signature files that are automatically appended to your email.

Upon receiving your request, `ftpmail` will send you instructions about how to use the service. In most cases you embed the FTP commands you want executed at the remote site as the body of your mail message. For example, to get a directory listing of the Linux directory, send a mail message with the body:

```
open sunsite.unc.edu
cd /pub/Linux
ls
quit
```

The ftpmail utility at the remote site processes the commands as if they were typed directly into FTP. To transfer a file to yourself through email, send the following mail message:

```
open sunsite.unc.edu
cd /pub/Linux
binary
get README
quit
```

This sends you the file README via email. The ftpmail system is slower than FTP since you must wait for the email to make its way to the target machine, be processed by the remote system's ftpmail utility, format a reply, then send the return message back to you. Still, ftpmail does provide a useful access method for those without FTP connections and an easy way to check the contents of the Linux directories on several machines without having to log in to them. This can be useful when you want to occasionally check for updates to the software.

One caution: The files you want to transfer may exceed your mail system's maximum file size limits. Some mail systems break the files into smaller chunks and allow you to reassemble them when you receive them, but some email systems impose a small size limit on email making it impractical to use ftpmail to get large files like the complete Linux software distribution.

### Bulletin Board Systems (BBSs)

There are hundreds of Bulletin Board Systems (BBSs) around the world that now provide access to the Linux distribution software and support Linux discussion groups. Some BBSs regularly download new Linux releases from the FTP home sites, while others rely on the BBSs' users to update the software.

Any list of BBSs with Linux software would be lengthy and out of date quickly, so the best method to obtain this information is to obtain a list of current BBS sites from Zane Healy, who maintains a complete list of BBSs offering Linux material. To obtain the BBS list, send email requesting the Linux list to `healyzh@holonet.net`. If you don't have access to email, try a few local bulletin board systems and post messages asking for local sites that offer Linux software or ask someone with Internet access to post email for you. Many BBSs will also have the list, although the accuracy of the list may vary.

## What's a Linux Release?

A Linux release has two meanings to most users. The first meaning has to do with the vendor or distributor that provides Linux. For example, both Slackware and Red Hat are Linux releases. As mentioned earlier in this chapter, the differences between some releases are subtle, but there are differences.

The second meaning of release has to do with the version of Linux you use. For example, Slackware 2.3 and Slackware 2.4 are both releases of Linux. More properly, these should be *versions* of the same release (Slackware), but the term release has been used for every new set of kernels and tools provided by Linux since the very early days. It's somewhat confusing when someone asks you which release of Linux you're using because you're not sure if they mean the vendor or version, so most people beat the problem by providing both (“I’m running Slackware 2.0.33,” for example).

Do you need to have the very latest version of a Linux release? Most likely not. The differences between most version increases are typically small, especially for incremental releases such as 2.3 to 2.4. Unless there is some feature or driver support that you really want with the latest version, it's seldom worth the bother of upgrading. There are much more important differences between major version upgrades, such as from the 1.X series to 2.X series kernels. Major kernel upgrades are almost always worth installing, although you may have to reinstall everything from scratch with major version updates.

![image](img/e8e6b47ac20475e23d48b4c476f5d891_72_0.png)

> **NOTE**
>
> Avoid the common trap of upgrading your system every time a new release of Linux is available. Some people have to be running the very latest version of each software package on their system, but the effects of moving from 2.0.33 to 2.0.34 are most likely undetectable on most systems. The real motivation for upgrading should be for better performance, drivers for hardware, or major version upgrades. If you do catch “versionitis,” you're going to spend more time upgrading each component of your system than working (or playing) with it. Often, you'll end up reloading your entire system as well.

## Linux Releases and Disk Sets

A release is a collection of Linux software sufficient to install and run the entire operating system. The release is made up of a number of collections of software, called disk sets (even though they may not come on disks). Most Linux systems have a number of disk sets included when you obtain the distribution software.

Although most of the CD-ROMs and FTP sites have the same software, a few label the disk sets differently. To illustrate the disk sets available with Linux, one of the more popular CD-ROM versions, Slackware, can be used as an example. The current set of disk sets available with the Slackware Linux distribution is:

- **Disk Set A** — the base system. This contains the kernel and a set of basic utilities including shell, editor, and user utilities. Disk Set A is the only disk set that fits on a single high-density floppy. This lets you install and run Linux even from a floppy disk!
- **Disk Set AP** — Linux applications, including many different editors, all the standard UNIX command utilities, man pages, and GNU add-ons like GhostScript.
- **Disk Set D** — program development. This disk set includes the GNU languages, development utilities, libraries, and compiler tools. There is also a lot of source code for libraries used to customize the Linux kernel.
- **Disk Set E** — GNU emacs editor.
- **Disk Set F** — FAQ (Frequently Asked Questions) files and other Linux help files.
- **Disk Set I** — documentation files for the GNU software.
- **Disk Set IV** — Interviews libraries, include files, and documentation. Interviews is a C++ GUI development package.
- **Disk Set N** — networking software. This disk set includes the TCP/IP protocol set, UUCP, mail utilities, news system, and several utilities.
- **Disk Set OI** — ParePlace Object Builder and Object Interface Library. These are commercial development packages made available to Linux developers by ParePlace.
- **Disk Set OO** — Object Oriented Programming (OOP) tools including the GNU Smalltalk compiler and the Smalltalk Interface to X (STX).
- **Disk Set Q** — source files for the Linux kernel and boot images.
- **Disk Set T** — the TeX and LaTeX2 test formatting systems. TeX is widely used for typesetting.
- **Disk Set TCL** — Tcl language set, including Tcl, Tk, TclX, and utilities.
- **Disk Set Y** — games collection.
- **Disk Set X** — XFree86 including the X system and several window managers.
- **Disk Set XAP** — applications for X, including file managers, GhostView, some libraries, games, and utilities.
- **Disk Set XD** — X development kit including X libraries, server link kit, and PEX support. This disk set is necessary if you are going to develop X-based applications.
