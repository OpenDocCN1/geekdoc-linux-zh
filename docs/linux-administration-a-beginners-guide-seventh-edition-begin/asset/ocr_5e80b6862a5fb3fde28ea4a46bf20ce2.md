# CHAPTER 6 Booting and Shunting Down 169

starting with K, a parameter of stop is passed. Likewise, for scripts starting with S, the parameter start is passed.

Let's peer into the /etc/rc.d/rc3.d directory of our sample Fedora server and see

```
[root@fedora-server ~]# ls -l /etc/rc.d/rc3.d/
lrwxrwx-x.1 root root 20 Nov 4 21:32 K50netconsole -> ../init.d/netconsole
lrwxrwx-x.1 root root 17 Nov 4 21:32 K90network -> ../init.d/network
```

From the sample output, you will see that K50netconsole is one of the files in the
etc/rc.d/rc3.d directory (the first line in the output). Thus, when the file K50netconsole is executed or invoked, this command is being executed instead:

```
# /etc/init.d/netconsole stop
```

By the same name, if a file named - S99carpald is invoked, the following
command is what really gets:

```
# /etc/init.d/carpald
```

# Writing Your Own rc Script

In the course of administering a Linux script and keeping it running, at some point you will need to modify the startup or shutdown script. You can do this using various approaches.

If you change to take effect at boot time and the change is small, you may simply edit the /etc/rc.d/rc.local or /etc/rc.local script. This script is run at the tail end of the boot process—after all the other startup scripts.

On the other hand, if your addition is more elaborate and/or requires that the shutdown process explicitly stop, you should add a script to /etc/rc.d/ or /etc/rc* directory. This script should take the parameters start and stop, and should act accordingly.

Of course, the first option, the rc.local script, is the easier of the two. To make additions to this script, simply open it in your editor of append the commands you want to run for one- or two-line changes.

As mentioned, if your situation needs a more elaborate or elegant solution, you will need to create a separate script and use the second option. The process of writing an rc script is not as difficult as you think. Let's step through the process using an example to see how it works. You can use this as a skeleton script, by the way, changing it to anything you need.

Let's assume you are running a server that supports SysV-style startup scripts and you want to start a special program that pops up a message every hour and reminds that you need to take a break from the keyboard (a good idea if you don't