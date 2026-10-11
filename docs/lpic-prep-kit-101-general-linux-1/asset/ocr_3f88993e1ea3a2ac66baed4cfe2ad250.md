run multiple applications at the same time. This is the only time that init does not read the /etc/inittab file. Rather, the default action is to run the /bin/su command and you are logged in as the superuser or root.

When starting at a runlevel higher than the single-user mode, the system starts up in multiuser mode. In this mode, init executes those lines with an action of sysinit, boot, or bootwait. Frequently, these lines mount the filesystems.

Next, the init daemon will execute all the other lines that are listed with the present run-level in the runlevel field.

Your initial runlevel is defined by the line

```
id:3:initdefault:
```

Notice that this line does not define any processes to start, but rather defines the runlevel with which to start. You can change the runlevel by using the command init. Its syntax is

```
init [runlevel]
```

The init command takes a runlevel as an argument. You can specify how long to wait before changing the runlevel by using the telinit command with the -t seconds option. The default delay is 5 seconds. The telinit command is a link to the init command. Be sure that you notify any logged on users before changing the runlevel.

For example, the command

```
init 5
```

will change the runlevel to level five. init first sends a signal to stop any processes running that are not defined for the new runlevel. After the specified delay, telinit then sends a kill signal to these processes. It then starts any processes defined for the new run-level that are not already running.

You also can change to single-user mode by passing either s or S to the init or telinit commands.

The next section in the /etc/inittab file defines the startup scripts to run, as in

```
si::sysinit:/etc/rc.d/rc.sysinit
```

The ID si at the beginning of the line is used internally by the init daemon. This line starts the script rc.sysinit, which handles tasks such as activating the swap partition, running fsck, and mounting your filesystems. The fsck command checks the filesystem for corrupt entries and is discussed in more detail in Chapter 6, “Maintaining the Filesystem.” This script can vary depending on your distribution. Read the one located on your system to get the details of what it accomplishes.