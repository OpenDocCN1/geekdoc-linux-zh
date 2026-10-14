The final large block of entries describes in which runlevels getty processes (login processes) are started:

```
```text
1:2345:respawn:/sbin/mingetty --noclear tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```
```

The getty processes provide the login prompt and in return expect a username as input. They are started in runlevels 2, 3, and 5.

![](bbox=[0.094, 0.303, 0.282, 0.378])

Runlevel 4 in the previous example is ignored because the line that defines the actions for the runlevel is commented out earlier in the file (#14:4:wait:/etc/init.d/rc4).

If a session ends, the processes are started again by init. If a line is disabled here, no further login is possible at the corresponding virtual console.

![](bbox=[0.094, 0.441, 0.282, 0.512])

You should take great care when making changes to the /etc/inittab file. If the file is corrupted, the system will no longer boot correctly. If an error does occur, first try entering S at the kernel command line in the GRUB boot menu. If this does not work, it is still possible to boot the system. Enter init=/bin/bash at the kernel command line in the GRUB boot menu.

In this way, the init process is replaced by a shell (so inittab is not read); you can then repair the system manually.

After changing /etc/inittab, use `init q` to have init reload its configuration.

# init Scripts and Runlevel Directories

/etc/inittab defines the runlevel the system uses after booting is complete. The services that need to be started in a certain runlevel are not defined in /etc/inittab itself. These are configured by symbolic links in /etc/init.d/rcx.d/ directories that point to scripts in /etc/init.d/. To be able to manage runlevels, you need to understand the following:

+   - init Scripts
+   - Runlevel Symbolic Links
+   - How init Determines Which Services to Start and Stop
+   - Activate and Deactivate Services for a Runlevel