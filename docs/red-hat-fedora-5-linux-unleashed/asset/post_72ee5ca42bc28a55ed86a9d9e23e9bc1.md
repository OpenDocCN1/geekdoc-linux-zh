
*) echo "Invalid parameter";
esac
}
DisplayMonth 8
```

The preceding program displays the following output:

Month 1 is August

## RELATED FEDORA AND LINUX COMMANDS

You can use these commands and tools when using the shell or writing shell scripts:

- `chsh` — Command used to change one's login shell
- `ksis2` — Allows two-person interaction with a single shell
- `mc` — A visual shell named the GNU Midnight Commander
- `nano` — An easy-to-use text editor for the console
- `system-config-users` — A graphical user-management utility that can be used to change one or more user login shells
- `shar` — Command used to create shell archives
- `vi` — The vi (actually vim) text editor

## Reference

- http://www.linuxgazette.com/issue70/ghosh.html — A Linux Gazette article on “Bootstrapping Linux,” which includes much detail on the BIOS and MBR aspects of the boot process.
- http://www.lostcircuits.com/advice/bios2/1.shtml — The LostCircuits BIOS guide; much detail on the meaning of all those BIOS settings.
- http://www.r0kspot.com/default.aspx?location=l — The BIOS Optimization Guide; details on tweaking those BIOS settings to your heart's content.
- http://www-106.ibm.com/developeros/java/linux/library/l-slack.html — A link through IBM's website to an article on booting Slackware Linux, along with a sidebar about the history of System V versus BSD init scripts.
- */usr/src/linux/init/main.c* — The best place to learn about how Linux boots. Fascinating reading, really. Get it from the source!
- http://sunsite.dk/linux-newbie/ — Home page for the Linux Newbie Administrator Guide— A gentle introduction to Linux System Administration.
- The GRUB Manual— The still yet-to-be-completed manual can be found at http://www.gnu.org/software/grub/manual/. On your Fedora system, *info grub* provides a plethora of information and a sample grub.conf file (/boot/grub/menu.lst is a symbolic link to /boot/grub/grub.conf; use either name) can be found in /usr/doc/grub.
- “LILO User's Guide”—Werner Almesberger's definitive technical tome on the Linux Loader, or LILO, and how it works on Intel-based PCs. Look under the /usr/share/doc/lilo/doc directory for the file user_guide.ps, which can be viewed using the gv client. LILO has been dropped from Fedora; GRUB is now the default boot loader supported in the distribution.
- “Managing Initscripts with Red Hat's chkconfig”—by Jimmy Ball, Linux Journal, April 2001; pp. 128–132.
- “Grub, Glorious Grub”—Hoyt Duff, Linux Format, August 2001; pp. 58–61. A tutorial on the GRUB boot loader.
- http://www.redhat.com/docs/manuals/linux/RH_9-Manual/custom-guide/s1-services-serviceconf.html—Red Hat’s guide to use the system-config-service client (then called redhat-config-service).
- http://www.linuxbase.org/spec/refspecs/LSB_1.0_0/g/LSB/sysinit.html—The Linux Standard Base description of system initialization; this is the standard.
- http://www.gnu.org/software/bash/bash.html—The bash home page at the GNU Software Project.
- http://www.tldp.org/LDP/abs/html/—Mendel Cooper’s “Advanced Bash-Scripting Guide.”
- http://www.linuxnewbie.org/nht/intel/shells/basic.html—Learn basic shell commands at this site.
- http://www.cs.princeton.edu/~llk/l1/—“The New Korn Shell—ksh93,” an article by David G. Korn, Charles J. Northrup, and Jeffery Korn regarding the korn shell.
- http://web.cs.mun.ca/~michael/pdksh/—The pdksh home page.
- http://lug.umbc.edu/~mabzugi/bash-httpd.html—The Bash-httpd FAQ, with links to the latest version of the bash web server, bash-httpd-0.02.
- http://www.tsch.org/—Find out more about tsch here.
- http://www.zsh.org/—Examine zsh in more detail here.

# CHAPTER 16
## System Resources

**IN THIS CHAPTER**

- System-Monitoring Tools
- Reference

## System-Monitoring Tools

To keep your system in optimum shape, you need to be able to monitor it closely. Such monitoring is imperative in a corporate environment where uptime is vital and any system failures can cost real money. Whether it is checking processes for any errant daemons, or keeping a close eye on CPU and memory usage, Fedora provides a wealth of utilities designed to give you as little or as much feedback as you want. In this chapter we look at some of the basic monitoring tools, along with some tactics designed to keep your system up longer. Some of the monitoring tools cover network connectivity, memory, and hard drive usage, but all should find a place in your sysadmin toolkit. Finally, you will learn how to manipulate active system processes using a mixture of graphical and command-line tools.

### Console-Based Monitoring

Those familiar with UNIX system administration already know about the ps or process display command commonly found on most flavors of UNIX. Because Linux is closely related to UNIX, it also benefits from this command and allows you to quickly see the current running processes on the system as well as who owns them and how resource-hungry they are.

Although the Linux kernel has its own distinct architecture and memory management, it also benefits from enhanced use of the proc file system, the virtual file system found on many UNIX flavors. Through the proc file system you can directly communicate with the kernel to get a deep view of what is currently happening. Developers tend to use the proc file system as a way of getting information out from the kernel) and for their programs to manipulate it into more human readable formats. The `/proc` file system is beyond the scope of this book, but if you want to get a better idea of what it contains you should head on over to http://en.tldp.org/LDP/Linux/Filesystem-Hierarchy/html/proc.html for an excellent and very in-depth guide.

Processes can also be controlled at the command line, which is important because you might sometimes have only a command-line interface. Whenever an application or command is launched, either from the command line or by clicking on an icon, the process that comes from the kernel is assigned an identification number called a *process ID* or PID for short. This number is shown in the shell if the program is launched via the command line.

```
$ xosview &
[1] 11670
```

In this example, the xosview client has been launched in the background, and the (bash) shell reported a shell job number ([1] in this case). A job number or job control is a shell-specific feature that allows a different form of process control, such as sending or suspending programs to the background and retrieving background jobs to the foreground (see your shell's man pages for more information if you are not using bash).

The second number displayed (11670 in this example) represents the process ID. You can get a quick list of your processes by using the `ps` command like this:

```
$ ps
  PID TTY          TIME CMD
  736 tty1    00:00:00 bash
  743 tty1    00:00:00 startx
  744 tty1    00:00:00 tee
  752 tty1    00:00:00 xinit
  756 tty1    00:00:00 kwm
11670 pts/4   00:00:00 xosview
11671 pts/4   00:00:00 ps
```

Note that not all output from the display is shown here. But as you can see, the output includes the process ID, abbreviated as PID, along with other information, such as the name of the running program. As with any UNIX command, many options are available; the `ps` man page has a full list. A most useful option is `aux`, which provides a friendly list of all the processes. You should also know that `ps` works not by polling memory, but through the interrogation of the Linux `/proc` or process filesystem. (`ps` is one of the interfaces mentioned at the beginning of this section.)

The `/proc` directory contains quite a few files--some of which include constantly updated hardware information (such as battery power levels, and so on). Linux administrators often pipe the output of `ps` through a member of the grep family of commands to display information about a specific program, perhaps like this:
