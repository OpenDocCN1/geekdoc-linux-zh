# 320 Part III Choosing and Installing a Linux Distribution

The following --contents option lets you see the full contents of the package choose as if you were listing the contents with ls -l command. You can see the name and path to each file, its permission settings and file/group ownership:

```
$ dpkg --contents lsof-4.71-1_i386.deb
drwx-xr-x root/root 0 2004-04-03 07:34:41 ./
drwx-xr-x root/root 0 2004-04-03 07:34:36 /usr/
drwx-xr-x root/root 0 2004-04-03 07:34:39 /usr/bin/
```

# Installing Package Sets (Tasks) with Tasksel

Some package sets are too large to be managed practically through meta packages, so tasks have been created as an alternative. Tasks are installed and removed using the tasksel utility. When run without any arguments, tasksel presents a menu from which you can select tasks to install or remove.

> Caution Do not install any tasks if you plan to use this system in conjunction with server examples in Chapters 24 and 25.

Additional options are available from the command line:

+   * To see a list of known tasks, run tasksel --list
* To list the packages that are installed by a task, run tasksel --task-packages <task name>.

> Caution When a task is removed, all packages associated with that task, whether installed manually or as part of that task, are removed!

An example of a popular task to install is the desktop task. The desktop task installs three complete desktop environments on the X Window System: GNOME, KDE, and XFCE environments. Note that this task will take a long time to download and requires several gigabytes of disk space to complete. To start the desktop task, run the following:

```
$ tasksel install desktop
```

# Alternatives, Diversions, and Stat Overrides

In cases where there is more than one installed program that provides a specific function, package maintainers have the option of utilizing Debian's alternatives system. The alternatives manages which program is executed when you run a specific command. For instance, the ed, nano, and nvi packages provide a text editor. An alternative maintained in the system guarantees that a text editor is accessible through the generic editor command, regardless of which combination of these packages are installed.