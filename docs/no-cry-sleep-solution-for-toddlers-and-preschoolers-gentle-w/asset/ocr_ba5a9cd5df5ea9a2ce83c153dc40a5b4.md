# Server Management

A single Linux system can provide several different services such as mail, Web, or FTP servers. Each service operates as a continually running daemon looking for requests for its particular services from remote users. You can turn services on or off by starting or shutting down their daemons. The process of starting up or shutting down a service is handled by service scripts, described in detail in this chapter.

# System Startup Files: /etc/rc.d and /etc/sysconfig

Each time you start your system, it reads a series of startup commands from system initialization files located in your /etc/rc.d directory. These initialization files are organized according to different tasks. Some are located in the /etc/rc.d directory itself, while others are located in a subdirectory called init.d. You should not have to change any of these files. The organization of system initialization files varies among Linux distributions. The Red Hat organization is described here. Some of the files you find in /etc/rc.d are listed in Table 20-1.

# /etc/rc.d/rc.sysinit

The /etc/rc.d/rc.sysinit file holds the commands for initializing your system, including the mounting and unmounting of your file systems. Kernel modules for specialized features or devices can be loaded in an rc.modules file. The /etc/rc.d/rc.local file is the last initialization file executed. You can place commands of your own here. When you shut down your system, the system calls the halt file, which contains shutdown commands. The files in init.d are then called to shut down daemons, and the file systems are unmounted. In the current distribution of Red Hat, halt is located in the init.d directory.

# /etc/rc.d/init.d

The /etc/rc.d/init.d directory is designed primarily to hold scripts that start up and shut down different specialized daemons, such as network and printer daemons and those for font and Web servers. These files perform double duty, starting a daemon when the system starts up and shutting down the daemon when the system shuts down.