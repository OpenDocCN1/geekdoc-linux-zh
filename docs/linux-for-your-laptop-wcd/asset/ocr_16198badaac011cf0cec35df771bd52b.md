![](bbox=[0.19, 0.08, 0.75, 0.3])

*Figure 3.1 The ntvsys command may be used to control the startup and use of various server software.*

/etc/initab. Type `cksysv` on the command line of an X11 terminal window and press Enter. You'll see the dialog box shown in Figure 3.2.

You should not use this command capriciously! The order of various services can be critically important during startup or shutdown. For example, it would not be a good idea to have the NFS service shut down before remote filesystems are unmounted by the shutdown process. On the other hand, you might want to enable

![](bbox=[0.19, 0.57, 0.7, 0.9])

*Figure 3.2 The tksysv command is used to control what services are available during various system runlevels. It can be used to reorder when a server daemon is started or stopped.*