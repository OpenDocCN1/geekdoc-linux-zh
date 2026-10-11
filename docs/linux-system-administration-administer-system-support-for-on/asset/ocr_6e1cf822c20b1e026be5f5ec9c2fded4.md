If you are installing tools in a nonstandard executable directory, you may want to link them to `/usr/local/bin` to make upgrading easier and to avoid having to change every user's `PATH` to make them accessible.

Make sure you enable the `SUID` bit unnecessarily in files that don't need it, or you may create a security problem. Check the `SGID` bit for the same reason.

Many user commands can be used effectively for system administration, including `ls`, `tail`, `grep`, `find`, and other tools included with Slackware for archiving, compression, and packaging.

You can also use Linux commands to view and manipulate processes. The commands `ps`, `pstree`, and `fuser` can display information about processes (including open files and `PID` numbers) that administrators find indispensable.

If you want to make your output look pretty, you can use the `grep`, `sed`, `awk`, and `cut` tools to manipulate your text.

UNIX systems can also help an administrator to schedule jobs, whether for one-time running (with `at` or `batch`), or individual running on various schedules (with `cron`). As with all root processes, however, be sure to keep your `cron` jobs under control.

In addition to the command line tools, X has plenty to offer the system administrator. The graphical user interface is a great environment for multitasking. However, you do need to set up an `X` server to use it. Have all the information regarding your video card and monitor handy before you set them up.

You may want a hard copy of some files. To get printed output from a Linux system, you must (1) have a Linux-compatible printer set up properly and (2) make sure you understand how the Linux print queue works.

All UNIX operating systems use `man` pages as the basis for help files. You can tailor your system to the needs of users and system administrators, adding `man` pages locally and building a searchable database called the *whatis database*.

Finally, if you don't have all the tools you need or want, you can always download more from the Web or use the available script or programming languages to create your own tools.