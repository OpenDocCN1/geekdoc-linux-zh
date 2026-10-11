
This command calls the `syslog` man page from section 8, which corresponds to system administration. Your `MANPATH` variable should look like this:

```
# echo $MANPATH
MANPATH=/usr/man:/usr/man/preformat:/usr/X11R6/man:/usr/local/man
```

The `man` command uses this path to search for man pages.

![](img/8ad518fddafc7f5e73715a2604b61d50_176_0.png)

> If you create your own man pages and put them in the /usr/man/preformat directory, you won't have to worry about using nroff (another UNIX text-formatting language) to format them.

If you want to look for a certain command in the man pages but you're not sure where it would show up, use the `man -k` form of the command, as in this example:

```
# man -k ssh
```

This command prints out all the man pages available for the string ssh (including the Secure Shell ssh and the Secure Shell daemon sshd).

Note, however, that this information is available from the `whatis` database. Two other commands allow you to search the `whatis` database: `apropos` (which allows you to search for strings) and `whatis` (which allows you to search for complete words).

If you want to build or rebuild the `whatis` database, use the `makewhatis` command as root. Just make sure you run it as a background process, and choose a time when the system load is not very intensive. Following command creates new man pages to be searched with `apropos`, `whatis`, and `man -k`.

```
# makewhatis &
```

### Investigating Additional Tools

Plenty of other administrator tools now exist that can help you. Some are GUI-based, others run well from the command line. Either way, the more tools you have, the easier your administration tasks -- because you enter any situation with multiple options at your disposal. If the tool you need isn't included on the Slackware CD-ROM, you can probably find it on the Web. A good place to start is the following site:

http://www.linuxhq.com

### Linuxconf

Linuxconf is a downloadable set of system-administration tools that not only provide you with an X interface, but can also control your system’s runtime levels and booting. This toolset is available for download at the following site:

http://www.solucorp.qc.ca/linuxconf

### Alien

Alien is a nice conversion tool that enables you to use other applications packaged with other Linux distribution packages, including Red Hat and Debian, on Slackware Linux. Many applications are now packaged specifically for Red Hat, but that need not prevent you from running them on Slackware – provided you have a good conversion tool. You can find Alien at the following site:

http://kitenet.net/programs/alien

### ProcMeter

ProcMeter is a tool for displaying diverse system information such as that found under the /proc directory. Find this tool on the Web at the following site:

http://www.gedanken.demon.co.uk/procmet er

![](img/8ad518fddafc7f5e73715a2604b61d50_177_0.png)

> For more Linux resources available on the Web, see Appendix A.

### Make Your Own

Okay, so you’ve searched through the Web sites and the mailing lists and still can’t find the tool you’re looking for. What do you do now? One answer: Make tools for a Linux system has the makings of a “religious war” – you may hear zealously different opinions from fellow Linux and UNIX users. In the end, however, it’s your system; it’s totally up to you. Your choices include some familiar names:

- Assembler
- COBOL
- Fortran
- Pascal
- C
- C++
- Smalltalk

Depending on your experience and the needs of your system, you may want to use an uncompiled language. The following programming languages are not compiled; instead, bytecode is fed through an interpreter that reads the actual code.

- Basic
- Java

In addition to compiled and uncompiled languages, you may want to consider interpreted languages such as the following:

- Perl
- Scheme
- Python
- Tk/Tcl
- awk
- LISP
- All the UNIX Shells

Whichever language you use, the UNIX shells can be an administrator's best friend; you can use them to create scripts to automate many of your tasks. For most system-administration needs, you can get away with Perl or shell scripting.

I’ve been using shell scripts for a long time, but I’m working on learning Perl because I find it has a little better functionality. Also, Perl is used for CGI programming–which is useful for Web development– but Perl is also easiest to hack from outside if your program is written by a novice. Sometimes (as in this case) cautious and seasoned programming expertise can be a vital resource.

### Summary

Slackware Linux includes many useful tools for the system administrator, mostly in `/usr/bin`, `/bin`, `/sbin`, `/usr/sbin`, and `/usr/local/bin`. These executables may be dynamically or statically linked to their library files; be careful when you partition your drives. Most of your tools need not be hard-coded at the command line; they are already included in your PATH.

If you are installing tools in a nonstandard executable directory, you may want to link them to `/usr/local/bin` to make upgrading easier and to avoid having to change every user's `PATH` to make them accessible.

Make sure you do not enable the `SUID` bit unnecessarily in files that don't need it, or you may create a security problem. Check the `SGID` bit for the same reason.

Many user commands can be used effectively for system administration, including `ls`, `tail`, `grep`, `find`, and other tools included with Slackware for archiving, compression, and packaging.

You can also use Linux commands to view and manipulate processes. The commands `ps`, `pstree`, and `fuser` can display information about processes (including open files and `PID` numbers) that administrators find indispensable.

If you want to make your output look pretty, you can use the `grep`, `sed`, `awk`, and `cut` tools to manipulate your text.

UNIX systems can also help an administrator to schedule jobs, whether for one-time running (with `at` or `batch`), or individual running on various schedules (with `cron`). As with all root processes, however, be sure to keep your `cron` jobs under control.

In addition to the command line tools, X has plenty to offer the system administrator. The graphical user interface is a great environment for multitasking. However, you do need to set up an `X` server to use it. Have all the information regarding your video card and monitor handy before you set them up.

You may want a hard copy of some files. To get printed output from a Linux system, you must (1) have a Linux-compatible printer set up properly and (2) make sure you understand how the Linux print queue works.

All UNIX operating systems use `man` pages as the basis for help files. You can tailor your system to the needs of users and system administrators, adding `man` pages locally and building a searchable database called the *whatis database*.

Finally, if you don't have all the tools you need or want, you can always download more from the Web or use the available script or programming languages to create your own tools.

# Chapter 6
# Kernel Tweaking and Hacking

## IN THIS CHAPTER

- Learning how your kernel works
- Rebuilding your kernel
- Troubleshooting your kernel
- Understanding patch management and upgrading
- Exploring kernel hacking

IN THIS CHAPTER, I touch on many neat things you can do with your kernel.

### Learning How the Kernel Works

In Linux, hardware and software don't communicate directly with each other. It's very much layered like an onion. You have the hardware, which consists of the keyboard, monitor, mouse, printer, and so on. As the user (including root), you interface with the hardware via a shell– a program that gives you consistent access to the hardware. Because you and I don't speak in binary and the computer does, we need interpreters to talk to the hardware. This interpreter would be the kernel.

The kernel interprets the electronic hardware signals and translates them into something usable for the shell. If you are running applications, they run on top of the shell. Figure 6–1 shows an illustration of how the layers listed are visualized.
