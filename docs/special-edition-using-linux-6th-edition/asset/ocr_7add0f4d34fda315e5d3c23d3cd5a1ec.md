UUCP is actually a protocol for copying files across modems rather than actually getting a prompt. It is very uncommon today.

+   - **POP** — You can set up POP-only users who cannot log in to your machine, but can receive and download mail.

# ## Email Aliases

Email aliases are “fake” users who can receive mail, but only forward it on to other users or programs. Email aliases are a good way to set up very simple mailing lists if you don’t want to use a full package like majordomo or listproc.

# ## Policies

If you are running a multiuser server, you will probably want some password and account policies. These include rules for password creation and aging, available shells, and the message of the day (a message that is shown to users when they log in).

# ## Miscellaneous Services

Miscellaneous services covers only a few topics. First, you can set the default *run level*. Your default run level determines what services are started at boot time. Generally this is either 3, which is normal multiuser without X, or 5, which is multiuser with X.

Miscellaneous services also includes defining your modem connection. On Intel-based machines, you can select from one of four COM ports (or `/dev/ttyS0` through `/dev/ttyS3`).

# ## Boot Mode

Linuxconf allows you to configure LILO, which is the most common Linux boot loader. GRUB is rapidly overtaking the venerable LILO, but Linuxconf does not yet support GRUB.

The Boot mode section allows you to configure the available kernels to boot with, and other basic LILO configuration. For more information on LILO, see Chapter 18, “Building a Custom Kernel.”

# ## Cluster Administration

This cluster isn’t like Beowulf or other load-sharing clustering solutions for Linux. In Linuxconf parlance, a cluster is a group of machines that share common configuration files. Using Linuxconf, you can automatically keep them synchronized. This makes managing a large number of workstations much easier.

To put machines into groups, you can select Admin groups definitions and create a new group. An admin group is a collection of machines that share *subsystems*. A subsystem is a collection of configuration options. A configuration option could be an entire configuration file, or it can only be part of one (for example, specific entries in `/etc/passwd`, or only the NFS entries in `/etc/fstab`). Breaking up configuration into subsystems is generally much clearer than focusing on the specific files that implement those subsystems.

After you have selected your subsystems, you will want to put your group into an *administration tree*. An administration tree is a collection of unique subsystems. For example, one