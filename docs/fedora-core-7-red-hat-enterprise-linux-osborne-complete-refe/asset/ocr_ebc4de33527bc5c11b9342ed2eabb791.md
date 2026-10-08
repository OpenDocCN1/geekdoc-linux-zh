command to shut down the system. Runlevel 6 is the reboot state—it shuts down the system and reboots. Runlevel 1 is the single-user state, which allows access only to the superuser and does not run any network services. This enables you, as the administrator, to perform administrative actions without interference from others.

Other runlevels reflect how you want the system to be used. Runlevel 2 is a partial multiuser state, allowing access by multiple users, but without network services like NFS or xinetd (eXtended InterNET services daemon). This level is useful for a system that is not part of a network. Both runlevel 3 and runlevel 5 run a fully operational Linux system, with multiuser support and remote file sharing access. They differ in terms of the interface they use. Runlevel 3 starts up your system with the command line interface (also known as the text mode interface). Runlevel 5 starts up your system with an X session, running the X Window System server and invoking a graphical login, using display managers, such as gdm or systemd. If you choose to use graphical logins during installation, runlevel 5 will be your default runlevel. Linux provides two keyboard sequences to let you switch between the two during a login session: CTRL-ALT-F1 changes from the graphical interface (runlevel 5) to the command line interface (runlevel 3), and CTRL-ALT-F7 changes from the command line interface to the graphical interface. The runlevels are listed in Table 27-3.

Changing runlevels can be helpful if you have problems at a particular runlevel. For example, if your video card is not installed properly, then any attempt to start up in runlevel 5 will likely fail, as this level immediately starts your graphical interface. Instead, you should use the command line interface, runlevel 3, to fix your video card installation.

> **TIP** You can use the single-user runlevel (1) as a recovery mode state, allowing you to start up your system without running startup scripts for services like DNS. This is helpful if your system hangs when you try to start such services. Networking is disabled, as well as any multiuser access. You can also use **linux -S** at the boot prompt to enter runlevel 1. If you want to enter the single-user state and also run the startup scripts, you can use the special **s** or **S** runlevel.

| State | Description |
| :---- | :---------- |
| 0 | Halt (do not set the default to this level); shuts down the system completely. |
| 1 | Administrative single-user mode; denies other users access to the system, but allows root access to the entire multiuser file system. Startup scripts are not run. (Use **s** or **S** to enter single-user mode with startup scripts run.) |
| 2 | Multiuser, without network services like NFS, **xinetd**, and NIS (the same as 3, but you do not have networking). |
| 3 | Full multiuser mode with login to command line interface; allows remote file sharing with other systems on your network. Also referred to as the *text mode* state. |
| 4 | Unused. |
| 5 | Full multiuser mode that starts up in an X session, initiating a graphical login; allows remote file sharing with other systems on your network (same as 3, but with graphical login). |
| 6 | Reboots; shuts down and restarts the system (do not set the default to this). |

**TABLE 27-3 System Runlevels (States)**