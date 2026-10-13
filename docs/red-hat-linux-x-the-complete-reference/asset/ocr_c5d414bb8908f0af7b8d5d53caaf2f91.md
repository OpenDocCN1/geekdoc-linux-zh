# System Startup Files: /etc/rc.d and /etc/sysconfig

Each time you start your system, it reads a series of startup commands from system initialization files located in your /etc/rc.d directory. These initialization files are organized according to different tasks. Some are located in the /etc/rc.d directory itself, while others are located in a subdirectory called init.d. You should not have to change any of these files. The organization of system initialization files varies among Linux distributions. The Red Hat organization is described here. Some of the files you find in /etc/rc.d are listed in Table 20-1.

# /etc/rc.d/rc.sysinit

The /etc/rc.d/rc.sysinit file holds the commands for initializing your system, including the mounting and unmounting of your file systems. Kernel modules for specialized features or devices can be loaded in an rc.modules file. The /etc/rc.d/rc.local file is the last initialization file executed. You can place commands of your own here. When you shut down your system, the system calls the halt file, which contains shutdown commands. The files in init.d are then called to shut down daemons, and the file systems are unmounted. In the current distribution of Red Hat, halt is located in the init.d directory.

# /etc/rc.d/init.d

The /etc/rc.d/init.d directory is designed primarily to hold scripts that start up and shut down different specialized daemons, such as network and printer daemons and those for font and Web servers. These files perform double duty, starting a daemon when the system starts up and shutting down the daemon when the system shuts down. The files in init.d are designed in a way to make it easy to write scripts for starting up and shutting down specialized applications. They use functions defined in the functions file. Many of these files are set up for you automatically. You shouldn't need to change them. If you do change them, be sure you know how these files work first.

Table 20-1: System Startup Files

| File | Description |
|---|---|
| `/etc/sysconfig` | Directory that holds system configuration files and directories. |
| `/etc/rc.d` | Directory that holds system startup and shutdown files. |
| `/etc/rc.d/rc.sysinit` | Initialization file for your system. |
| `/etc/rc.d/rc.local` | Initialization file for your own commands; you can freely edit this file to add your own startup commands; this is the last startup file executed. |
| `/etc/rc.d/rc.modules` | Loads kernel modules (not implemented by default on Red Hat Linux). |
| `/etc/rc.d/init.d` | Directory that holds network scripts to start up network connections. |
| `/etc/rc.d/rcnum.d` | Directories for different runlevels, where num is the runlevel. The directories hold links to scripts in the /etc/rc.d/init.d directory. |
| `/etc/rc.d/init.d/halt` | Operations performed each time you shut down the system, such as unmounting file systems; called rc.halt in other distributions. |
| `/etc/rc.d/init.d/cups` | Start up and shut down the cups printer daemon. |