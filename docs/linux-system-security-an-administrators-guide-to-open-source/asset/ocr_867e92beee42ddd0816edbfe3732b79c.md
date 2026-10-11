+   1. Allow root access only through `su` or `sudo` (`sudo` is discussed in Chapter 9).
+   2. Become root only when absolutely necessary.
+   3. Execute every command as root with caution.
+   4. Whenever you must remotely administer a system as root, use SSH (discussed in Chapter 11) and `sudo`.

Running as root all the time is not a good idea. Consider the root account to be a very special account (which it is!) for use under very special circumstances. Become root only to perform tasks that must be performed as root. In Chapter 9, we discuss the use of `sudo` to assist in restricting root access and generating a root audit trail. Restricting root access through `su` or `sudo` is discussed in the section, *Configuring `/etc/security`* on page 68.

When you do become root, be careful! For example, before you issue the `shutdown` command, verify that you are logged in to the system that you want to shut down by executing `uname -n` or `hostname` first. Before you execute `rm -r *`, make sure that you are in the right directory! Red Hat 5.2/6.0 helps out here by aliasing `rm` to `rm -i` (which causes `rm` to ask you if you want to delete each file before it actually deletes the file). In general, think twice before you perform some action as root.

Here are some tips for configuring the root account more restrictively.

+   1. Set up the **PATH** environment variable so that it contains a minimum number of entries.
+       \- Do not put user writable directories in root’s **PATH**. A more naive administrator may be coerced into executing a Trojan horse (see Chapter 1).
+       \- For the same reason do not put `"."` (hard link to the current directory) in root’s **PATH**.
+   2. Use absolute pathnames when invoking commands.
+   3. Do not specify `/` as root’s home directory (Red Hat 5.2/6.0 uses `/root`).

SSH (which we explore thoroughly in Chapter 11) is capable of performing authentication beyond simple Linux passwords. It also builds an encrypted tunnel between two systems, securing all aspects of the communication. Always use this utility (or something similar) when you must become root on a remote system.

# ## Multiple root Users

On major systems, it is not uncommon for administration needs to require more than one person to be root. Sometimes multiple root accounts are configured for this purpose. Suppose, for example, that Mary and Bill are responsible for maintaining a particular system. One way to track the root activities of Mary and Bill is to set up two accounts, say `rootm` for Mary and `rootb` for Bill.