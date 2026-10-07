| | |
| --- | --- |
| /proc/net | Network information |
| /proc/sys | Kernel configuration parameters |

# Shutdown

Red Hat uses the BSD-style shutdown command. This command's syntax is:

```
shutdown [options] time [message]
```

When the system has been signaled to shut down, all logged-in users are notified that the system is going down using either the standard message or the one specified as a parameter to the shutdown command. All processes are then sent a SIGTERM signal to tell them that the computer is going down. This gives these processes time to shut down cleanly. The shutdown command then signals the init process to change the run level to 0 (halt) if the option -h was provided or 6 (reboot) if the -r option was used instead.

The /etc/rc.d/rc script is run with an argument of 0 or 6 as appropriate. This changes the run level and runs the scripts pointed to by the symbolic links in /etc/rc.d/rc0.d or /etc/rc.d/rc6.d as determined by the argument passed to the /etc/rc.d/rc script.

If a user hits Ctrl+Alt+Del to initiate a shutdown, the shutdown command will check for an /etc/shutdown.allow file. If this file exists, it is read in and used to determine whether the user who initiated the shutdown has permission to shut down the system. The /etc/shutdown.allow file contains pairs of hostnames and usernames. If the hostname of the system attempting to shutdown is listed, and the username next to it is a user who is currently logged on, the shutdown will proceed.

Most modern Linux distributions also provide a shutdown option on the XDM login screen. This allows inexperienced users to shut down after logging out, in a manner reminiscent of Windows NT or 2000.

# Warning Users

The shutdown command sends the users on the system a message telling them that the system is being shut down, whether it is a reboot or a halt, and when the shutdown will occur. You may add a message of your own to tell why, when the system will be brought back up, or any other information which you'd like your users to know. As the shutdown time approaches, the message will be repeated. The frequency of the message increases as the shutdown time gets nearer.

It is best not to make the shutdown period so short that users cannot finish with their applications and exit the system. Of course, there will be times when the shutdown must occur right away; this can't be helped, but adding a message telling the users when they can expect access to the system again may help soften the blow.

# Shutdown Log Files

Some of the same log files used with the startup process are also used for logging shutdown. Any problems with the kernel that occur during shutdown will be annotated in /var/log/messages. The /var/log/boot.log will report any problems relating to the processes run by the init program from /etc/rc.d/init.d. The distinction between these files is not clear-cut, however, and messages about the same problem tend to show up in both. If, for instance, the eth0 device wasn't detected, you'd see something like the following in /var/log/boot.log: