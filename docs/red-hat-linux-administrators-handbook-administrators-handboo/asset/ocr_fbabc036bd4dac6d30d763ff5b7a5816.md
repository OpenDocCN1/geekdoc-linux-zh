# Booting Up Your System

During the bootup process, init first runs the rc.sysinit script and then runs the script for the default run level. The default run level is set in /etc/inittab, using a line such as the following:

```
id:3:initdefault:
```

Here, the default run level is set to 3. This means that init will run the script needed to put the system in multiuser mode.

Looking back at Listing 2-1, the following line specifies what needs to be run for run level 3:

```
l3:3:wait:/etc/rc.d/rc 3.
```

The rc script is run with an argument of 3. As previously mentioned, this script runs all the scripts whose names start with S in the /etc/rc.d/rc3.d directory. It also supplies start as an argument to each of the S-prefixed scripts. After all the S scripts are run, the rc script finishes and the system becomes available in the default run level.

![](bbox=[0.08, 0.75, 0.18, 0.82])

**Tip**
It is possible to override the default run level at the LILO prompt. For example, if you want to boot the system in single-user mode, you can specify linux single to boot in single-user mode. If you use a label other than "linux" to boot Linux, you have to specify yourlabel single, instead, where yourlabel is the name of the appropriate label.

# Shutting Down Your System

You can run init manually and tell it to change the system run level, by providing the desired run level in the command line. For example,

```
init 1
```

tells init to change the current run level to 1. In other words, this halts the system. If you are running in multiuser mode (run level 3), the preceding command is less than ideal, because it does not inform the users on the system that the system is going to halt.