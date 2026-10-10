+       * **Software Updater (pirut)** — Update software packages in the Fedora or RHEL distribution or third-party sources from online repositories.
+           * **Configuration Editor (gconf-editor)** — Change settings associated with your GNOME desktop system.
+           * **Disk Usage Analyzer (gnome-utils)** — Displays and analyzes data on the use of your computer's hard disks.
+           * **Kickstart (system-config-kickstart)** — Create a Kickstart configuration file that can be used to install multiple Fedora or RHEL systems without user intervention.
+           * **System Monitor (frysk-gnome)** — Shows information about running processes and resource usage.

One other important system administration application that has been moved from the System Tools menu directly to the Applications menu is the Add/Remove Software (pirut) application. Procedures for using the various system graphical administrative tools are discussed throughout the book.

# Administrative commands

Many commands are intended for root. When you log in as root, your `$PATH` variable is set to include some directories that contain commands for the root user. These include the following directories:

+       * `/sbin` — This contains commands for modifying your disk partitions (such as `fdisk`), changing boot procedures (`grub`), and changing system states (`init`).
+           * `/usr/sbin` — This contains commands for managing user accounts (such as `useradd`) and checking network traffic (`wireshark`). Commands that run as daemon processes are also contained in this directory. (Look for commands that end in “d” such as `sshd`, `pppd`, and `crond`.)

Some administrative commands are contained in regular user directories (such as `/bin` and `/usr/bin`). This is especially true of commands that have some options available to everyone. An example is the `/bin/mount` command, which anyone can use to list mounted file systems, but only root can use to mount file systems.

To find commands that are intended primarily for the system administrator, check out the section 8 manual pages (usually in `/usr/share/man/man8`). They contain descriptions and options for most Linux administrative commands. For example, to see the man page for the `fdisk` command (`/usr/share/man/man8/fdisk.8.gz`), type:

```
$ man fdisk
```

Some third-party applications will add administrative commands to directories that are not in your PATH. For example, an application may put commands in `/usr/local/bin` (this is the most common location), `/opt/bin`, or `/usr/local/sbin`. Although `/usr/local/bin`