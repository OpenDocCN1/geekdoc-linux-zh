
# Part III: Administering Fedora and RHEL

| Run Level | What Happens in This Run Level |
|---|---|
| a, b, c, A, B, C | Used in conjunction with the demand action. They don't specify a run level but can launch a program or daemon "on demand" if instructed. |

> NOTE: If there is no default specified in the inittab file, the boot sequence will be interrupted and you will be prompted to specify a default run level into which the machine will boot.

The next line in the inittab file instructs to execute the /etc/rc.d/sysinit script before entering the default run level. This script performs many initialization routines as choosing a keymap file, checking and monitoring root and proc files, setting the clock and hostname, configuring swap space, cleaning up tmp files, and loading modules.

The following lines control the commands executed within each run level. In fact, each script is called, using the desired run level as an argument. In turn, it descends into the appropriate directory tree (for example, the /etc/rc3/ directory is entered for run level 3).

The ctrlalt command in the inittab file tells to perform exactly what PC users would expect if the Ctrl, Alt, and Delete keys were pressed simultaneously. The system restarts itself in an ordinary fashion (a switch to run level 0) after a three-second delay.

The next two lines (with their comments) deal with graceful shutdowns if you have an uninterruptible power supply (UPS) and software installed. The first line initiates a halt (a switch to run level 0) minutes after receiving a signal from the UPS indicating a power failure. The second line cancels the shutdown in the event that power is restored.

The six lines start up virtual consoles to all logins. These processes are always running in any of the multiuser run levels. When someone connected to a virtual console logs in, that process dies, and respawn action tells it to start a new process. You can switch between virtual consoles by pressing Ctrl+Alt+F1, Ctrl+Alt+F2, and so on.

The last line indicates that as long as the system is in run level 5, the "preferred display manager" (xdwm, gnome, KDE, and so) will be running. This presents a graphical login prompt rather than the usual text-based login, and eliminates the need to run startx to start the GUI.

# System Startup and Shutdown

During system startup, a series of scripts are run to start the services that you need. These include scripts to start network interfaces, mount directories, and monitor your system. The program that starts most of these services up when you boot and stops them when you shut down is the /etc/rc.d/rc.d script. The following sections describe run-level scripts and what you can do with them.

# Chapter 12: Automating System Tasks

## Starting run-level scripts

As previously mentioned, the /etc/rc.d script is integral to the concept of run levels. Any change of run level causes the script to be executed, with the new run level as an argument. Here is a quick run-down of what the /etc/rc.d script does:

- Checks run-level scripts are correct — The rc script checks to find run-level script that excludes those that represent backup scripts by rpm updates.
- Determines current and previous run levels — Determines the current and previous run levels to know which run-level scripts (previous level) and start (current level).
- Decides whether to enter interactive startup — If the confirm option is passed to the boot loader at time, server processes must be confirmed by the system console before starting.
- Kills and starts run-level scripts — Stops run-level scripts from the previous level, then starts run-level scripts from the current level.

In Fedora and RHEL, most of the services that are provided to users and computers on the network are started by run-level scripts.

## Understanding run-level scripts

A package that has a service to start at boot time (or when the system changes run levels) can add a script to the /etc/init.d directory. That script can then be linked to an appropriate run-level directory and run with either the start or stop option (to start or stop the service).

Table 12-5 lists many of the typical run-level scripts that are found in /etc/init.d and explain their function. Depending on the Fedora or RHEL packages installed on your system, you may have more run-level scripts than you see here. (Later, I describe how these files are linked into particular run-level directories).

Each script representing a service that you want to start or stop is linked to a file in the run-level directories. For each run-level script, a script beginning with K stops the service, whereas a script beginning with S starts the service.

The two digits following the K or S in the filename provide a mechanism to set the priority in which the programs are run. For example, S12syslog is run before S90cron. However, the file S10my_daemon is run before S85gpm, even though you can see that 85 is less than 110. This is because the ASCII collation sequence orders the files, which simply means that one positional character is compared to another. Therefore, a script beginning with the characters S110 is executed between S10network and S15nets in run level 3.

All of the programs within the /etc/rcX.d directories (where X is replaced by a run-level number) are symbolic links, usually to a file in /etc/init.d. The /etc/rcX.d directories include the following:

- /etc/rc0.d: Run level 0 directory
- /etc/rc1.d: Run level 1 directory
- /etc/rc2.d: Run level 2 directory
- /etc/rc3.d: Run level 3 directory
- /etc/rc4.d: Run level 4 directory
- /etc/rc5.d: Run level 5 directory
- /etc/rc6.d: Run level 6 directory

In this manner, /etc/rc0.d/K05atd, /etc/rc1.d/K05atd, /etc/rc2.d/K05atd, /etc/rc3.d/S95atd, /etc/rc4.d/S95atd, /etc/rc5.d/S95atd, and /etc/rc6.d/K05atd are all symbolic links to /etc/init.d using simple, consistent mechanism, you can customize which programs are started.

## Table 12-5: Run-Level Scripts Contained in /etc/init.d

| Run-Level Scripts | What Does Do? |
|---|---|
| dhcpd | Starts or stops the dhcp daemon, which assigns IP addresses to computers. |
| dovecot | Starts the dovecot IMAP server, which allows e-mail clients to request and view their mail. |
| firstboot | Checks if reboot needs to be run and if so, runs it. This is typically done after Fedora or RHEL is first installed. |
| gpm | Controls the gpm daemon, which allows the mouse to interact with console. |
| haldaemon | Starts halt daemon to discover and set up hardware. |
| halt | Terminates all processes, writes accounting records, removes swap space, units all file systems, and shuts down or restarts the machine (depending on how the command was called). |
| hplip | Starts the HP Linux Imaging and Printing (HPLIP) service for running HP multi-function. |
| httpd | Starts the httpd daemon, which allows your computer to act as an HTTP server (that is, to serve Web pages). |
| iptables | Starts the iptables firewall daemon, which manages any iptables-style firewall rules set up for your computer. |
| keytable | Loads the predefined keyboard map. |
| killall | Shuts down any subsystems that may still be running prior to a shutdown or reboot. |
| ldap | Starts the Lightweight Directory Access Protocol daemon (ldap), which listens for LDAP requests from the network. |
| mysql | Runs the MySQL database daemon (mysqld) to listen for MySQL databases. |
| named | Starts and stops the BIND server daemon (named) to listen for and resolve domain name requests. |
| netfs | Mounts or unmounts network files (NFS, SMB, NCP) file systems. |
| network | Starts or stops all configured network interfaces and initializes the TCP/IP and IPX protocols. |
| NetworkManager | Switches automatically to the best available network connections. |
| nfs | Starts or stops the NFS-related daemons (rpc.nfsd, rpc.mountd, rpc.statd, and rpc.quotad) and exports shared file systems. |
| ntpd | Runs the Network Time Protocol daemon (ntpd), which synchronizes system time with Internet standard time servers. |
| acpid | Controls the Advanced Power Interface daemon, manages events. |
| anacron | Runs cron jobs that were not run. |
| apmd | Starts the Advanced Power Management daemon, manages battery status, and auto-play multimedia. |
| autofs | Starts the automount daemon, for automatically mounting systems. |
| bluetooth | Starts services such as authentication, discovery, and hardware devices. |
| ConsoleKit | Maintains a list of user sessions. |
| crond | Starts and stops the cron daemon to periodically run routine. |
| cups | Controls the printer daemon (cups), which handles spooling printing requests. |
