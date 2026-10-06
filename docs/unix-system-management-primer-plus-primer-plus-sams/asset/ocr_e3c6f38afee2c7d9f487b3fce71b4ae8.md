# Chapter 14 • INTERNAL COMMUNICATION 42

The quintessential revision control tool on Unix is RCS (Revision Control System). RCS is the oldest and most popular revision control tool on Unix. RCS consists of a suite of commands that perform the revision control functions for you. Because RCS is so widely used by Unix system administrators, the following sections use that tool in their description of revision control techniques.

![](bbox=[0.375, 0.188, 0.623, 0.223])

# Other Revision Control Tools

Two other popular Unix revision control tools are CVS (Concurrent Versions System), and SCCS (Source Control System). These tools are typically used for maintaining large source code repositories, while RCS excels at maintaining individual files. For this reason, RCS is preferred by most system administrators for revision control on their configuration files.

# Checking In Files

Checking a file into RCS commits your changes to the RCS repository and creates a new version of the file. Checking in a file is also the first action you must perform to create an RCS repository. A repository can be a single file under RCS control, or it can be a directory of different files. RCS keeps master copies of each file in the repository, including all versioning information, with a suffix of .v. These files should never be edited directly. For example, checking in the file resolv.conf would result in the file resolv.conf, which would contain all versioning information for resolv.conf.

# Create an RCS Directory for Version Masters

To keep the .v files separate from working files, create a directory called RCS in your current directory. RCS will store the .v files for your working directory in the RCS directory. With the versioning files stored in a separate directory, you're unlikely to accidentally edit or remove them.

![](bbox=[0.098, 0.648, 0.163, 0.693])

# Never Edit ,v Files!

Never edit a file ending in .v. You could permanently corrupt the versioning information in the checked-in file.

Checking a file in RCS using the -u flag unlocks the file in the repository after checking it in, so that others can check out the file for editing. When you check in a file for the first time, ci asks for a description of the file, as follows:

```
bash$ ls -l
total 40
drwx-xr-x 2 jeff jeff 4096 Apr 6 12:41 RCS
-rw-r--r-- 1 jeff jeff 33988 Apr 6 12:39 httpd.conf
bash$ ci -u httpd.conf
RCS/httpd.conf,v <-- httpd.conf
enter description, terminated with single '.' or end file:
```

![](bbox=[0.098, 0.908, 0.163, 0.953])