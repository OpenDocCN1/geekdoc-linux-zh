
## The Runlevels

In Linux, runlevels define the state of the system. Table 11-1 shows what runlevels are available.

| Command | Description |
|---|---|
| 0 | Halt |
| S | Used to boot into single-user mode (U.S. keyboard layout) |
| 1 | Single-user mode |
| 2 | Multiuser mode without network server services |
| 3 | Multiuser mode with network |
| 4 | Not used |
| 5 | Multiuser mode with network and display manager |
| 6 | Reboot |

Table 11-1

The runlevel command displays the runlevel you are currently in (second number) and the previous runlevel (first number), as in the following:

```
da10:~ # runlevel
3 5
da10:~ #
```

You can also use the who -r command, as shown in the following:

```
da10:~ # who -r
         run-level 5        Feb 14 08:43        last=3
da10:~ #
```

## init Configuration File (/etc/inittab)

To understand the contents of the /etc/inittab file, you need to know the following:

- inittab Syntax
- inittab Standard Entries

### inittab Syntax

Each line in the /etc/inittab file uses the following syntax:

```
id:rl:action:process
```

The parameters are explained here:

- **id**—A unique name for the entry in /etc/inittab. It can be up to four characters long.
- **rl**—Refers to one or more runlevels in which this entry should be evaluated.
- *action*—Describes what init is to do.
- *process*—Identifies the process connected to this entry.

- **inittab Standard Entries**

The first entry in the /etc/inittab file contains the following parameters:

```
id:5:initdefault:
```

The initdefault parameter signals to the init process which level it should bring the system to. The default runlevel is normally 3 or 5.
The next entry in /etc/inittab looks like this:

```
si::bootwait:/etc/init.d/boot
```

The bootwait parameter tells init to carry out this command while booting and wait until it has finished.
The next few entries describe the actions for runlevels 0 to 6:

```
l0:0:wait:/etc/init.d/rc 0
l1:1:wait:/etc/init.d/rc 1
l2:2:wait:/etc/init.d/rc 2
l3:3:wait:/etc/init.d/rc 3
#l4:4:wait:/etc/init.d/rc 4
l5:5:wait:/etc/init.d/rc 5
l6:6:wait:/etc/init.d/rc 6

lS:S:wait:/etc/init.d/rc S
~~:S:respawn:/sbin/sulogin
```

The wait parameter tells init to wait until the appropriate command has been carried out when the system changes to the indicated level. The parameter also means that further entries for the level are performed only after this process is completed.

The single-user mode S is a special case; it works even if the /etc/inittab file is missing. In such a case, enter S at the boot prompt when the computer starts. The sulogin command is started, which allows only the system administrator to log in. The respawn parameter tells init to wait for the end of the process and to then restart it.

/etc/inittab also defines the Ctrl+Alt+Del key combination for restarting:

```
ca::ctrlaltdel:/sbin/shutdown -r -t 4 now
```

The ctrlaltdel action is carried out by the init process only if these keys are pressed. If you do not want to allow this action, comment out (#) or remove the line.

The final large block of entries describes in which runlevels getty processes (login processes) are started:

```
1:2345:respawn:/sbin/mingetty --noclear tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

The getty processes provide the login prompt and in return expect a username as input. They are started in runlevels 2, 3, and 5.

![](img/9129877170834ca9d5fdac5319bf5f12_402_0.png)

Runlevel 4 in the previous example is ignored because the line that defines the actions for the runlevel is commented out earlier in the file (#14:4:wait:/etc/init.d/rc4).

If a session ends, the processes are started again by init. If a line is disabled here, no further login is possible at the corresponding virtual console.

![](img/9129877170834ca9d5fdac5319bf5f12_402_1.png)

You should take great care when making changes to the /etc/inittab file. If the file is corrupted, the system will no longer boot correctly. If an error does occur, first try entering S at the kernel command line in the GRUB boot menu. If this does not work, it is still possible to boot the system. Enter init=/bin/bash at the kernel command line in the GRUB boot menu.

In this way, the init process is replaced by a shell (so inittab is not read); you can then repair the system manually.

After changing /etc/inittab, use `init q` to have init reload its configuration.

## init Scripts and Runlevel Directories

/etc/inittab defines the runlevel the system uses after booting is complete. The services that need to be started in a certain runlevel are not defined in /etc/inittab itself. These are configured by symbolic links in /etc/init.d/rcx.d/ directories that point to scripts in /etc/init.d/. To be able to manage runlevels, you need to understand the following:

- init Scripts
- Runlevel Symbolic Links
- How init Determines Which Services to Start and Stop
- Activate and Deactivate Services for a Runlevel

### init Scripts

The `/etc/init.d/` directory contains shell scripts that are used to perform certain tasks at bootup and start and stop services in the running system. The following shows some of the files in `/etc/init.d/`.

```
dao:~ # ls -al /etc/init.d/
total 635
drwxr-xr-x 11 root root 3336 May 24 13:40 .
drwxr-xr-x 7 root root 6712 May 25 13:19 ..
-rwxr--r-- 1 root root 1393 May 24 13:40 .depend.boot
-rwxr--r-- 1 root root 3465 May 24 13:40 .depend.start
-rwxr--r-- 1 root root 3002 May 24 13:40 .depend.stop
-rw-r--r-- 1 root root 482 Aug 25 2004 Makefile
-rw-r--r-- 1 root root 7827 May 10 18:17 README
-rwxr-xr-x 1 root root 1257 May 8 20:09 SuSEfirewall2_init
-rwxr-xr-x 1 root root 1650 May 8 20:09 SuSEfirewall2_setup
-rwxr-xr-x 1 root root 2696 May 8 20:29 aeventd
-rwxr-xr-x 1 root root 5729 May 8 20:15 acpid
-rwxr-xr-x 1 root root 5265 May 8 21:01 alsasound
-rwxr-xr-x 1 root root 3689 May 9 14:49 atd
-rwxr-xr-x 1 root root 6691 May 9 15:03 auditd
-rwxr-xr-x 1 root root 9234 May 9 15:01 autofs
-rwxr-xr-x 1 root root 2967 Mar 14 13:40 autoyast
-rwxr-xr-x 1 root root 2792 May 8 20:29 boot.apparmor
-rwxr-xr-x 1 root root 7072 Apr 20 15:02 boot
```

The `.depend.{boot,start,stop}` files are created by insserv and contain dependencies that are used to determine which services can be started in parallel. See `/etc/init.d/README` for details on this functionality.

The shell scripts can be called up in the following ways:

- Directly by init when you boot the system, when the system is shut down, or when you stop the system with `Ctrl+Alt+Del`. Examples for these scripts are `/etc/init.d/boot` or `/etc/init.d/rc`.
- Indirectly by init when you change the runlevel. In this case, the `/etc/init.d/rc` script that calls the necessary scripts in the correct order and with the correct parameter during the runlevel change.
- Directly by `/etc/init.d/script parameter`.

You can also enter `rescript parameter` if corresponding links are set in `/sbin/` or `/usr/sbin/`.

The parameters shown in Table 11-2 can be used.

| Parameter | Description |
|---|---|
| start | Starts a service that is not running. |
| restart | Stops a running service and restarts it. |
| stop | Stops a running service. |
| reload | Rereads the configuration of the service without stopping and restarting the service itself. |
| force-reload | Reloads the configuration if the service supports this. Otherwise, it does the same thing as restart. |
| status | Displays the current status of the service. |

Table 11-2

When a script is called without parameters, a message informs you about the possible parameters.

Some of the more important scripts stored in /etc/init.d/ are described in the following list:

- **boot**—This script is started directly by init when the system starts. It is run once only. It evaluates the /etc/init.d/boot.d/ directory and starts all the scripts linked by filenames with an “S” at the beginning of their names (see “Runlevel Symbolic Links”). These scripts perform, for example, the following tasks:
  - Check the file systems
  - Set up LVM
  - Delete unnecessary files in /var/lock/
  - Set the system time
  - Configure Plug&Play hardware with the isapnp tools
- **boot.local**—This script includes additional commands to execute at boot before changing into a runlevel. You can add your own system extensions to this script.
- **halt**—This script is run if runlevel 0 or 6 is entered. It is called up either with the halt command (the system is completely shut down) or with the reboot command (the system is shut down and then rebooted).
- **rc**—This script is responsible for the correct change from one runlevel to another. It runs the stop scripts for the current runlevel, and then it runs the start scripts for the new one.
- **service**—Each service (such as cron, apache2, or cups) comes with a script allowing you to start and stop the service, to reload its configuration, or to view its status. To create your own scripts, you can use the /etc/init.d/skeleton file as a template.

## Runlevel Symbolic Links

To enter a certain runlevel, init calls the /etc/init.d/rc script with the runlevel as a parameter. This script examines the respective runlevel /etc/init.d/rcX.d/ directory, and starts and stops services depending on the links in this directory.
