> **NOTE**
> 
> Not all Linux distributions use the same runlevel configurations or runlevel definitions! For example, although Fedora uses runlevel 3 for a full, console-based multiuser mode, pre-7.1 versions of SUSE Linux defined this system state as runlevel 2. Red Hat, Fedora, and SUSE now use the same runlevels to conform to the Linux Standards Base, or LSB. As a system administrator, you should be aware of this issue, especially if you have devised any administrative scripts or tools that deal with system states.

Each runlevel tells the **init** command what services to start or stop. Although runlevels might all have custom definitions, Fedora has adopted some standards for runlevels:

+   - **Runlevel 0** —Known as "halt," this runlevel is used to shut down the system.
+   - **Runlevel 1** —This is a special runlevel, defined as "single," which boots Fedora to a root access shell prompt where only the root user may log in. Networking, X, and multiuser access are turned off. This is the maintenance or rescue mode. It allows the system administrator to perform work on the system, make backups, or repair configuration or other files.
+   - **Runlevel 2** —This runlevel dictates that Fedora be booted to a console, or text-based mode, with multiuser access.
+   - **Runlevel 3** —This runlevel is identical to runlevel 2, except that it also starts any networking services.
+   - **Runlevel 4** —This runlevel is undefined, and it can readily be configured to boot Fedora to a custom system state.
+   - **Runlevel 5** —This runlevel boots Fedora to a networking, multiuser state with an active X session. This is the most common runlevel for home users who want a graphical interface.
+   - **Runlevel 6** —This runlevel is used to reboot the system.

Runlevel 1 (also known as *single-user mode* or *maintenance mode*) is most commonly used to repair file systems and change the root password on a system when the password has been forgotten. Trespassers with physical access to the machine can also use runlevel 1 to access your system.

> **CAUTION**
> 
> Never forget that uncontrolled physical access is virtually a guarantee of access to your data by an intruder.

# Booting into the Default Runlevel

Entries in /etc/inittab use a field-based notation that determines the runlevel—when to execute the process, whether or not the process is executed when booting, whether or not

![](bbox=[0.93, 0.11, 0.96, 0.18])