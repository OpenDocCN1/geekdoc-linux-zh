
http://www.gnu.org/software/bash/bash.html—The bash home page at the GNU Software Project.

http://www.tldp.org/LDP/abs/html/—Mendel Cooper’s “Advanced Bash-Scripting Guide.”

http://www.linuxinnewbie.org/nhf/intel/shells/basic.html—Learn basic shell commands at this site.

http://www.cs.princeton.edu/~jlk/jl/—”The New Korn Shell—ksh93,” an article by David G. Korn, Charles J. Northrup, and Jeffery Korn regarding the korn shell.

http://web.cs.mun.ca/~michael/pdksh/—The pdksh home page.

http://lug.umbc.edu/~mabzug1/bash-httpd.html—The Bash-httpd FAQ, with links to the latest version of the bash web server, bash-httpd-0.02.

http://www.tcsh.org/—Find out more about tcsh here.

http://www.zsh.org/—Examine zsh in more detail here.

## CHAPTER 16

## System Resources

## System-Monitoring Tools

To keep your system in optimum shape, you need to be able to monitor it closely. Such monitoring is imperative in a corporate environment where uptime is vital and any system failures can cost real money. Whether it is checking processes for any errant daemons, or keeping a close eye on CPU and memory usage, Ubuntu provides a wealth of utilities designed to give you as little or as much feedback as you want. In this chapter, we look at some of the basic monitoring tools, along with some tactics designed to keep your system up longer. Some of the monitoring tools cover network connectivity, memory, and hard drive usage, but all should find a place in your sysadmin toolkit. Finally you will learn how to manipulate active system processes using a mixture of graphical and command-line tools.

### Console-Based Monitoring

Those familiar with UNIX system administration already know about the ps or process display command commonly found on most flavors of UNIX. Because Linux is closely related to UNIX, it also benefits from this command and enables you to quickly see the current running processes on the system as well as who owns them and how resource-hungry they are.

Although the Linux kernel has its own distinct architecture and memory management, it also benefits from enhanced use of the /proc file system, the virtual file system found on many UNIX flavors. Through the /proc file system, you can directly communicate with the kernel to get a deep view of what is currently happening. Developers tend to use the /proc file system as a way of getting information out from the kernel and for their programs to manipulate it into more human-readable formats. The /proc file system is beyond the scope of this book; but if you want to get a better idea of what it contains, head on over to http://en.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/proc.html for an excellent and in-depth guide.

### IN THIS CHAPTER

- System-Monitoring Tools
- Reference

Processes can also be controlled at the command line, which is important because you might sometimes have only a command-line interface. Whenever an application or command is launched, either from the command line or by clicking on an icon, the process that comes from the kernel is assigned an identification number called a process ID, or PID for short. This number is shown in the shell if the program is launched via the command line:

```
$ xosview &
[1] 5918
```

In this example, the xosview client has been launched in the background, and the (bash) shell reported a shell job number ([1] in this case). A job number or job control is a shell-specific feature that allows a different form of process control, such as sending or suspending programs to the background and retrieving background jobs to the foreground. (See your shell's man pages for more information if you are not using bash.)

The second number displayed (5918 in this example) represents the process ID. You can get a quick list of your processes by using the ps command like this:

```
$ ps
  PID TTY      TIME     CMD
 5510 pts/0    00:00:00 bash
 5918 pts/0    00:00:00 xosview
 5932 pts/0    00:00:00 ps
```

Note that not all output from the display is shown here. As you can see, however, the output includes the process ID, abbreviated as PID, along with other information, such as the name of the running program. As with any UNIX command, many options are available; the proc man page has a full list. A most useful option is aux, which provides a friendly list of all the processes. You should also know that ps works not by polling memory, but through the interrogation of the Linux /proc or process file system. (ps is one of the interfaces mentioned at the beginning of this section.)

The /proc directory contains quite a few files—some of which include constantly updated hardware information (such as battery power levels and so on). Linux administrators often pipe the output of ps through a member of the grep family of commands to display information about a specific program, perhaps like this:

```
$ ps aux | grep xosview
USER     PID %CPU %MEM   VSZ   RSS TTY      STAT START   TIME COMMAND
andrew  5918  0.3  1.1  2940  1412 pts/0    S   14:04   0:00 xosview
```
