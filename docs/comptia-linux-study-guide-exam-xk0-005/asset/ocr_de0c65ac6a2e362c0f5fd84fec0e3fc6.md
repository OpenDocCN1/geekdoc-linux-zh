# **Listing 6.2** Checking the `init` program for links

```
# readlink -f /sbin/init
/usr/lib/systemd/systemd
#
```

You can see in Listing 6.2 that this system is actually using systemd. You can verify this by taking a look at PID 1, as shown in Listing 6.3.

# **Listing 6.3** Checking PID 1

```
# ps -p 1
PID TTY          TIME CMD
  1 ?          00:00:06 systemd
#
```

In Listing 6.3, the `ps` utility is used. This utility allows you to view processes. A process is a running program. The `ps` command shows you what program is running for a particular process in the `CMD` column. In this case, the `systemd` program is running. Thus, this Linux system is using `systemd`.

Keep in mind that these discovery methods are not foolproof. Also, there are other system initialization methods, such as the now-defunct Upstart. The following brief list shows a few Linux distribution versions that used Upstart:

+   - Fedora v9\~v14
+   - openSUSE v11.3\~v12.2
+   - RHEL v6
+   - Ubuntu v6.10\~v15.04

If you are using the distribution versions recommended in Chapter 1, “Preparing Your Environment,” be aware that those distributions are all systemd systems.

# # Managing systemd Systems

The systemd approach introduced a major paradigm shift in how Linux systems manage services. Services can now be started when the system boots, when a particular hardware component is attached to the system, when certain other services are started, and so on. Some services can be started based on a timer.

In the following sections, we’ll focus on starting, stopping, and controlling systemd managed services. We’ll walk you through the systemd technique’s structures, commands, and configuration files.