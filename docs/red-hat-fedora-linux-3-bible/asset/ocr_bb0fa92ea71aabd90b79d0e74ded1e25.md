# Part III: Administering Fedora

![](bbox=[0.25, 0.08, 0.75, 0.4])

Procedures for using the various system graphical administrative tools are discussed throughout the book.

# Administrative commands

Many commands are intended only for root. When you log in as root, your `$PATH` variable is set to include some directories that contain commands for the root user. These include the following directories:

+   - **/sbin** — This contains commands for modifying your disk partitions (such as fdisk), changing boot procedures (grub), and changing system states (init).

+   - **/usr/sbin** — This contains commands for managing user accounts (such as useradd) and configuring your mouse (mouseconfig). Commands that run as daemon processes are also contained in this directory. (Look for commands that end in "d" such as sshd, pppd, and crond.)

Some administrative commands are contained in regular user directories (such as /bin and /usr/bin). This is especially true of commands that have some options available to everyone. An example is the /bin/ mount command, which anyone can use to list mounted file systems, but only root can use to mount file systems.

To find commands that are intended primarily for the system administrator, check out the section 8 manual pages (usually in /usr/share/man/man8). They contain descriptions and options for most Linux administrative commands.

Some third-party applications will add administrative commands to directories that are not in your PATH. For example, an application may put commands in /usr/local/bin.