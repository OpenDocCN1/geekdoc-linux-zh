```
id:3:initdefault:
```

Here the default run level is set to 3, meaning that init runs the scripts needed to put the system in multiuser mode.

If you take a second look at /etc/inittab, you will notice that the following line specifies which rc script needs to be run for run level 3.

```
13:3:wait:/etc/rc.d/rc 3
```

The rc script is run with an argument of 3. As mentioned before, this script runs all the scripts whose names start with “S” in the /etc/rc.d/rc3.d directory. It also supplies “start” as an argument to each of the “S”-prefixed scripts. When all the “S” scripts are run, the rc script finishes and the system becomes available in the default run level.

# Booting to single-user mode

Booting to single-user mode is usually necessary in case of emergencies, such as when you need to fix a corrupt disk or reset a forgotten root password. Whatever the reason, you have two ways to boot in single-user mode.

If you're already logged into the system and want to switch to single-user mode, you can run the following command:

```
init 1
```

This tells init to switch run level to 1, which is the single-user mode. However, if you plan on getting access to the system in single-user mode when it is actually booting up, then at the LILO prompt enter:

```
linux single
```

This boots Linux to single-user mode.

![](bbox=[0.08, 0.88, 0.18, 0.95])

> If you are using graphical LILO prompt, you can press Ctrl+X to summon the text LILO prompt from which you can enter the above command.

# Booting in rescue mode

If your Linux system does not boot for some reason and you wish to try and rescue the system, you can boot the system in rescue mode if you have the official Red Hat CD-ROM.