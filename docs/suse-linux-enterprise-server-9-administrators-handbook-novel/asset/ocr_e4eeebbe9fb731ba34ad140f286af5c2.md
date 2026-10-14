+   - Harden the Linux kernel using the grsecurity kernel patch (http://www.grsecurity.net) to prevent attacks that use buffer overflows and the like. A good starting reference is the “Linux Kernel Hardening” article from the SANS Institute (http://www.sans.org/rr/whitepapers/linux/1294.php).
+   - Specify logging and access control for all services, allowing only the minimum access necessary. Secure and review these logs regularly. (See “Using a Central syslog Server” later in this chapter for information on securing system logs.)
+   - Whenever possible, use chroot jail to run a service in a confined directory.
+   - If at all possible, create a special user to run server processes. For example, run named as user named. These accounts should not have shell access; for instance, they should be given /bin/false as the default shell.
+   - Restrict access to special system services like cron to system administrators.
+   - Restrict access to root. Administrative tasks should be performed using sudo whenever possible.
+   - Review and remove unnecessary SUID and SGID applications, such as CD burning programs.
+   - Review and ensure no weak file permissions are assigned to critical system files.
+   - Remove unnecessary filesystem permissions (such as world-write). Also check for missing sticky bits on world-writeable directories.

# TIP

You can use the following find command to get a list of all world-writeable directories whose sticky bit is not set:

```
find / -type d -perm +o+w not -perm +o+t -print
```

+   - Remove all compilers (such as gcc and g++) from the servers. After an intruder breaks into a system, he or she will often copy over the source code of a rootkit so a version specific to your server can be built and installed. If you need compilers, such as for software development work purposes, confine their installation to your workstation.
+   - Limit the number of daemons or processes using the instances directive in xinetd. Setting limits can help prevent some Denial of Service (DoS) attacks.