![](bbox=[0.24, 0.08, 0.78, 0.38])

**Figure 10-3:** Show log files of activities from system boot, FTP, mail, news, and other services.

Procedures for using the various Red Hat graphical administrative tools are distributed throughout the book.

# # Administrative commands

Many commands are intended only for root. When you log in as root, your `$PATH` variable is set to include some directories that contain commands for the root user. These include the following directories:

+   - `/sbin` — This contains commands for modifying your disk partitions (such as `fdisk`), changing boot procedures (`grub`), and changing system states (`init`).

+   - `/usr/sbin` — This contains commands for managing user accounts (such as `useradd`) and configuring your mouse (`mouseconfig`) or system services (`chkconfig`). Commands that run as daemon processes are also contained in this directory. (Look for commands that end in “d” such as `sshd`, `pppd`, and `crond`.)

Some administrative commands are contained in regular user directories (such as `/bin` and `/usr/bin`). This is especially true of commands that have some options available to everyone. An example is the `/bin/mount` command, which anyone can use to list mounted file systems, but only root can use to mount file systems.

To find commands that are intended primarily for the system administrator, check out the section 8 manual pages (usually in `/usr/share/man/man8`). They contain descriptions and options for most Red Hat Linux administrative commands.

Some third-party applications will add administrative commands to directories that are not in your `PATH`. For example, an application may put commands in `/usr/local/bin`.