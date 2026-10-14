power from the system. This addition greatly improves the likelihood of recovery from a manual shutdown.

# UNIX BOOT AND SHUTDOWN POLICIES

In most circumstances, you should not allow general users to boot, reboot, or shut down systems. For one reason, users cannot run the reboot, init, or shutdown commands; only the super-user can execute them. In addition, in cases where security is important, a system in the process of rebooting can be vulnerable. If you ban rebooting from the user, you can consider a rebooted system with suspicion. Finally, and most importantly, it is unlikely that a user will be certain of the role an individual workstation may play within the overall network. The system they shut down may have the print servers for the accounting office’s printers, the boss’s filesystem, or it may have other users working remotely. Since in UNIX the network is the machine, you should use caution with the shutdown or reboot process.

Of course, the need for caution applies to the system administrator as well. A policy should exist to cover when, why, and who may bring down a system. The possession of root privileges does not confer omniscience. The following should be checked before a shutdown:

+   - What filesystems are being exported?
+   - Do those filesystems contain users?
+   - Do those filesystems contain shared programs?
+   - Are users logged on?
+   - Are processes running in the background?
+   - Is this system a printer or license server?
+   - Is this system a mail, database, or Web server?
+   - Is this an emergency, or can the shutdown/reboot be done later?

Once you have the answers to these questions, you must use good judgment. In some cases, consigning reboots and shutdowns to off-peak hours is the best approach. The use of shutdown instead of reboot, init, or halt to halt or reboot a system is also wise. The options in shutdown to provide users warning and time to logout is just good manners, and will be less of an impact on productivity.

Only a system administrator should physically turn off a system if a shutdown has not been performed. The “it was hung” argument should not be accepted. The console could be locked up, but the rest of the system might be functioning fine.