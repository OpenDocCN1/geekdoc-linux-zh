
## /etc/hosts

The `hosts` file allows us to set up aliases for local and remote hosts. This is a very powerful feature that can simplify host name lookups. For example, if you wanted to force all of your users to go to `www.google.com` when they enter `google`, simply add this record to the `hosts` file:

```
216.239.57.101 google
```

The IP address `216.239.57.101` is one of many IP addresses assigned to `www.google.com`. We can use the `ping` command to verify that the alias has taken effect:

```
$ ping google
PING www.google.com (216.239.57.101) from 192.168.254.2: 56(84) bytes of data.
64 bytes from www.google.com (216.239.57.101): icmp_seq=1 ttl=45 time=72.5 ms
...
```

> *Note that this will not work properly with network applications that perform their own DNS lookups, such as the Lynx text browser.*

## /etc/hosts.allow and /etc/hosts.deny

The `hosts.allow` file specifies (by name or IP address) the hosts that are allowed access to local TCP/IP services. By default, all other hosts are denied access. Or, we can specifically list the hosts for which we want to deny access in the `hosts.deny` file.

Suppose you want to control access to your server through the telnet protocol. Specifically, suppose you wanted to allow access only to remote users from the host `www.wrox.com` and to local users. To achieve this, you would specify this line in `hosts.allow`:

```
telnetd: LOCAL, 192.168.1., www.wrox.com
```

and this line in `hosts.deny`:

```
telnetd: ALL
```

All entries listed in `hosts.allow` take precedence over any entries in `hosts.deny`.

> *Note that you can use this access control mechanism only if `tcp_wrappers` (the `/usr/sbin/tcpd` server) is enabled for that specific service. See the `xinetd.d` entry, later in this section, for more information.*

## /etc/init.d

This is a symbolic link to a directory that contains a number of **startup scripts**. The startup scripts perform a number of functions, including initialization of network connections and startup of server daemon processes. For example, the file `/etc/init.d/crond` implements functionality to start, stop, restart, and reload (the configuration information) the `cron` daemon.

Not all of the scripts in this directory are executed when you start the system. Rather, execution is governed by the system's **run level**. We discussed run levels back in Chapter 2 – as you'll recall, the runlevels (0–6) are represented by the directories /etc/rc.d/rcX.d. Each of these directories contains symbolic links to the chosen scripts in the init.d directory. If you want a particular application or process to run within a particular run level, you can simply add a symbolic link to that application to the corresponding run level directory.

## /etc/inittab

The inittab configuration file is probably the single most important file in the system – it controls the initialization process that occurs when you start the system. It is responsible for starting the init process; it contains a line to set the default run level to be used:

```
id:3:initdefault:
```

This line will set the run level to 3; see Chapter 2 for more information on the different runlevels. If you want to start your system with an X Window System interface, you can simply change this to run level 5:

```
id:5:initdefault:
```

## /etc/issue and /etc/issue.net

The issue and issue.net configuration files contain the text that is displayed when you start a terminal session. Typically, this message contains the Red Hat version number and the kernel identification. The only difference between these two files is that issue.net is displayed only to remote users who log in to the system, while the contents of issue are displayed to local users only.

## /etc/ld.so.conf

This file contains a list of directories in which shared libraries (*.so) can be found. The information in this file is used by the ldconfig application to create the necessary links and cache to these libraries, so that development tools (such as the dynamic linker) can find them. You need to run ldconfig whenever you add, remove, or change the entries in this file.

## /etc/logrotate.conf

This file contains information that controls the rotation of log files and is used in conjunction with the logrotate application.

The main reasons for rotating log files are to keep them organized and to limit their size. If you don't control the size of your log files, then your backups take longer – and you also run the risk of your disk space filling up unexpectedly.

Moreover, when something goes wrong with the system, examination of the log files often helps us to trace the cause of the problem. But if the log files get too large, then this examination process becomes more difficult – and finding the problem is like searching for a needle in a haystack.

So the idea is that we rotate our log files periodically, or when a log file reaches a specified size. The `logrotate` application (located in `/usr/sbin`) does the work, and to do so it uses the rotation time interval or file-size limits specified in `logrotate.conf`.

In fact, the `/etc/cron.daily` directory contains a simple script called `logrotate`, which invokes the following command to rotate the logs:

```
/usr/sbin/logrotate /etc/logrotate.conf
```

If you look at the `crontab` file, you will see that all the scripts in `cron.daily` are configured to run at 4:02 am every day:

```
02 4 * * * root run-parts /etc/cron.daily
```

## /etc/modules.conf

The `modules.conf` configuration file tells the kernel (or more specifically, the `modprobe` and `depmod` applications) which modules to load on demand.

For example, if you want to use the `tulip` driver to handle your Ethernet/network card, you would add the following line to the `modules.conf` file:

```
eth0 tulip
```

Of course, this assumes that the `tulip` driver (`tulip.o`) exists in the `/lib/modules/2.4.20-2.48` directory; this directory contains the modules for the Linux kernel 2.4.18-4. You can use the following command to check that the driver exists:

```
# find /lib/modules/ -name tulip.o
```

> *We will discuss the modular nature of the Linux kernel, and the Linux Loadable Kernel Modules (LKM), later in the chapter.*

## /etc/passwd

The `passwd` configuration file stores the account information (including the user name, full name, and path to the home directory and default shell) for every user on the system. You can use the `redhat-config-users` application (Applications | System Settings | Users and Groups) if you do not feel comfortable modifying the contents of this file. See Chapter 8 for more information on adding users and groups.

## /etc/rc

The `rc` file and the files in the `rc.d` directory control what applications and services run at specific run levels. The `rc.d` directory contains a number of subdirectories – each subdirectory represents a run level from 0–6. These subdirectories, in turn, contain symbolic links to startup scripts in the `init.d` directory (see the entry for `init.d` above).

The rc file itself is responsible for starting and stopping services when a run level changes.

## /etc/resolv.conf

We discussed the `resolv.conf` file at the beginning of this chapter.

## /etc/security

The security directory contains a list of configuration files that impose restrictions on various resources. This includes information about who can log in and from which location(s) they can log in, and the privileges that console users are given and resource limits for all users.

For example, if you want to increase the hard limit for resources allocation (that is, the number of file descriptors) to all users from 1024 to 8192, you could add the following lines to `limits.conf`:

| Domain | Type | Item | Value |
| :--- | :--- | :--- | :--- |
| * | soft | nofile | 1024 |
| * | hard | nofile | 8192 |

This change, along with the following change to `/etc/pam.d/login`, will allow users to increase their file descriptor limits:

```
session required /lib/security/pam_limits.so
```

up until their hard limit by using the following command:

```
$ ulimit -n unlimited
```

Typically, you would increase resource limits for users and processes that are under a heavy and constant load, such as the Web server process.

## /etc/shadow

If shadow passwords are enabled, the `shadow` configuration file contains encrypted passwords for all users listed in the `passwd` file. This is a more secure approach, since the `shadow` file is readable only by root. See Chapter 8 for more information on users and passwords.

## /etc/shells

This file can be used to list all the valid shells on the system. The `chsh` command, which allows users to change their default shell, makes use of this list. Historically it has been used to restrict access: network services like FTP daemons have required users logging in to have a valid shell — with no valid shell, access is denied.

## /etc/skel

The `skel` directory contains a list of files, which will be copied to a user's directory when the user is first created. This allows us to provide each user with a set of default resources, such as scripts, configuration, and data files.
