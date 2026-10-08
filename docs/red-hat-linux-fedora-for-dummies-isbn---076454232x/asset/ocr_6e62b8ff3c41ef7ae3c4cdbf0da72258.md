+   The Advanced Power Management Daemon (APMD): APMD is useful if you — like most people — regularly power-off your personal workstation or laptop. However, APMD is generally unnecessary on servers that run continuously. You want to keep APMD in the former case (workstation or laptop) and remove it in the latter (server).
GPM: This service allows you to use a mouse when running in nongraphical mode. You're running in graphical mode, so turn it off.
The job queue daemon: The atd daemon is used to schedule one-time cron-like jobs. If you need atd, you know it. Otherwise, turn it off.
Network File Sharing (NFS): You need only services such as nfs, nfslock, portmap, and autofs when you're running an NFS server or client. The last thing you want to do is share files to the Internet, for example.
Print services: Many people don't run the printer daemon on servers. Turn off cups or lpd whenever you don't need to print.
Samba: Just like with NFS, you should turn off Samba if you don't need it.

The rest is up to you. Terminate services with a vengeance.

You can't modify a service when it isn't running. You can toggle off the check mark on a nonrunning service, but it doesn't have any effect if it's not running.

You can use the CLI-based chkconfig utility. Open a GNOME Terminal session and log in as root (**su -**):

+   List the services by running the chkconfig --list command.
List an individual service by specifying the service after the --list option: chkconfig -- list apmd.
Stop a service with the --add option: chkconfig -- add apmd.
Delete a service with the --del option: chkconfig -- del apmd.

# Using a Secure Shell client

You may be most familiar with graphical network communication applications, like the Mozilla web browser and Evolution e-mail clients. However, a world of text-based tools is available, such as Secure Shell, Telnet, and FTP. Those applications provide an interactive method for connecting to other computers across networks and the Internet using a command-line interface (CLI); refer to Chapter 4 for more information about CLIs.