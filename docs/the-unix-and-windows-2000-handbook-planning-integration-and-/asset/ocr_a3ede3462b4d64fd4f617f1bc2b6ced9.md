These scripts are simple Bourne shell scripts that execute a series of commands. The rc.boot script performs these basic functions:

+   - Set hostname.
+   - Enables IP networking.
+   - Mounts / and /usr filesystems in read-only mode.
+   - Checks filesystems.

If all filesystems are clean, rc.boot runs rc.single. The first thing rc.single does is remount / and /usr in read-write mode. The rc.single script cleans up the mount table, shared library cache, and other system files. It also sets the time based on your local time zone. The loadkeys command is used to set the system keyboard mapping to match your system. When rc.single exits, rc.boot returns a system prompt if you are entering single-user mode.

If the system is going into multi-user mode, /etc/rc is run immediately after /etc/rc.boot (remember, rc.boot executed rc.single). /etc/rc

# Figure 3.3
BSD boot sequence.

![](bbox=[0.28, 0.58, 0.82, 0.96])