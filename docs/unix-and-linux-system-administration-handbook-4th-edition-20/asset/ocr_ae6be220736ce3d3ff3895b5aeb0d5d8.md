# Red Hat startup scripts

start at run level 3 in Red Hat, the network script is sequence number 10 and the sshd script has sequence number 55, so network is certain to run first. Be sure to consider this type of dependency when you add a new service.

To tell the system when to start a daemon, you must place symbolic links into the appropriate directory. For example, start cupsd (the printing daemon) at run level 2 and to stop nicely before shutting down, the following pair of links would suffice:

```
# In -s /etc/init.d/cups /etc/rc2d/S80cups
# In -s /etc/init.d/cups /etc/rc0d/K80cups
```

The first line tells the system to run the /etc/init.d/cups startup script as one of the last things to do when entering level 2 and to run it with the start argument. The second line tells the system to run /etc/init.d/cups relatively soon when shutting down the system and to run it with the stop argument. Some systems treat shutdown and reboot differently, so we should probably put a symbolic link in the /etc/rc6.d directory as well to make sure the daemon shuts properly when the system is rebooted.

# Red Hat startup scripts

Startup scripts are one of the areas in which Linux distributions are most distinguished from each other. Red Hat uses a primary init-script-based approach, with a few twists just to make life difficult for everyone.

At each run level, init invokes the /etc/rc.d/rc with the new run level as an argument. /etc/rc.d/rc usually runs in 'normal' mode, in which it runs scripts, but it can also run in 'confirmation' mode, where it prompts you for confirmation before running each individual startup script.

Startup scripts store lock files in the /var/lock/subsys directory. The presence of a lock file with the same name as a startup script indicates that service should already be running. Startup scripts create lock files when you give a start command and remove them when performing a stop.

Red Hat has a chconfig command to help you manage services. This adds or removes startup scripts from the system, manages the run levels at which they operate, and lists the run levels for which a script is configured. See the man page for usage information for this simple and handy tool.

Red Hat also has an /etc/rc.d/rc.local script (not directory) that runs at boot. The last run script as part of the startup process and is a good place to add specific tweaks and post-boot tasks.

Once you see the “Welcome to Red Hat Enterprise Linux” message during the boot process, you can press the 'i' key to enter confirmation mode. Unfortunately, Red Hat gives you no confirmation that you have pressed the right key. It continues to mount filesystems, activate partitions, load keymaps, and locate