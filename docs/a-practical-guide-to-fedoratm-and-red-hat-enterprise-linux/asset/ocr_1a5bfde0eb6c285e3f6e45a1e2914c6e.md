root filesystem
The filesystem that is available when the system is brought up in single-user mode. This filesystem is always represented by / . You cannot unmount or mount the root filesystem. You can remount root to change its mount options.

root login
Usually the username of *Superuser* (page 1276).

root (user)
Another name for *Superuser* (page 1276).

root window
Any place on the desktop not covered by a window, object, or panel.

rootkit
Software that provides a user with root privileges while hiding its presence.

rotate
When a file, such as a log file, gets indefinitely larger, you must keep it from taking up too much space on the disk. Because you might need to refer to the information in the log files in the near future, it is generally not a good idea to delete the contents of the file until it has aged. Instead you can periodically save the current log file under a new name and create a new, empty file as the current log file. You can keep a series of these files, renaming each as a new one is saved. You will then **rotate** the files. For example, you might remove **xyzlog.4**, **xyzlog.3**➔**xyzlog.4**, **xyzlog.2**➔**xyzlog.3**, **xyzlog.1**➔**xyzlog.2**, **xyzlog**➔**xyzlog.1**, and create a new **xyzlog** file. By the time you remove **xyzlog.4**, it will not contain any information more recent than you want to remove.

router
A device (often a computer) that is connected to more than one similar type of network to pass data between them. See *gateway* on page 1251.

RPC
Remote procedure call. A call to a *procedure* (page 1267) that acts transparently across a network. The procedure itself is responsible for accessing and using the network. The RPC libraries make sure that network access is transparent to the application. RPC runs on top of TCP/IP or UDP/IP.

RSA
A public key encryption (page 1157) technology that is based on the lack of an efficient way to factor very large numbers. Because of this lack, it takes an extraordinary amount of computer processing time and power to deduce an RSA key. The RSA algorithm is the de facto standard for data sent over the Internet.

run
To execute a program.

runlevel
Before the introduction of the systemd init daemon, runlevels specified the state of the system, including single-user and multiuser. See Table 10-1 on page 449.

Samba
A free suite of programs that implement the Server Message Block (SMB) protocol. See *SMB* (page 1273).

SAN
Storage Area Network. A high-speed subnetwork of shared storage devices wherein all storage devices are available to all servers on a LAN or WAN. This setup offloads disk I/O overhead from the servers, allowing them to give more resources to the applications they are running. It also allows disk space to be added without altering individual machines.

schema
Within a GUI, a pattern that helps you see and interpret the information that is presented in a window, making it easier to understand new information that is presented using the same schema.

scroll
To move lines on a terminal or window up and down or left and right.