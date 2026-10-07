```
/sbin/setup.sh
fi
```

The rcS file sets up some environmental variables, including the PATH variable. It then runs a special configuration shell script if the system is running for the first time after installation. The rcS script then runs other scripts, which do things like enable virtual memory, mount filesystems, clean up certain log directories, initialize Plug-and-Play devices, load kernel modules, configure PCMCIA devices, set up serial ports, and run System V init scripts. The rcS script will call certain scripts in /etc/rc.d before it relinquishes control. These include:

+   * **rc.local** Similar to the Red Hat rc.local, it serves the same purpose.
* **rc.modules** Loads kernel modules: network card, PPP support, and other modules. If this script finds rc.netdevice, it will call that script as well.
* **rc.pcmcia** Probes for any PCMCIA devices that exist on the system and configures them. This is most useful for laptop users, who probably have a PCMCIA modem or network card.
* **rc.serial** Configures the serial ports by running the appropriate setserial commands.
* **rc.sysvinit** Looks for System V init scripts for the desired run level (symbolic links in /etc/rc.d/) and runs them. Similar to the Red Hat version, this rc.sysvinit script runs the scripts pointed to by the symbolic links in the appropriate subdirectory. In the case of run level 3, all links in /etc/rc3.d/ will be run.

Again, once this work is finished, the init program initiates a getty process and the XDM process, which displays a login prompt, and then waits for a login attempt or some other process that needs attention.

Now that we have the system initialized, let's look at what happens when a user logs in. You will need to know this process well so that you can troubleshoot user login problems.

# # User Initialization Files

A different type of initialization happens when a user logs in. This is not a system-wide initialization like the boot process. It is another sequence for user-specific initialization. But just as with the system initialization files, the system administrator is responsible for the user initialization files. The example that follows shows the sequence for the Bash shell, which is the Linux default shell. If you are using a different shell, the sequence will be similar.

When a user logs in, the system user configuration files are run first. These files are scripts and are sourced in instead of being executed. A file is sourced via the "dot" command. To source the .login file, for example, use the following command:

```
. /home/someuser/.login
```

> **Note** Sourcing a file executes each command as if it were typed in at the command prompt rather than as a separate program. The sourced file's environment becomes part of the shell in which it is run. A file does not have to be executable to be