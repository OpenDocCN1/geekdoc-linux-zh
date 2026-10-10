```
465 /lib/systemd/systemd-resolved not confined
747 /usr/sbin/avahi-daemon not confined
748 /usr/sbin/cupsd confined by ‘/usr/sbin/cupsd (enforce)’
804 /usr/sbin/cups-browsed confined by ‘/usr/sbin/cups-browsed (enforce)’
885 /usr/sbin/xrdp-sesman not confined
912 /sbin/dhclient confined by ‘/sbin/dhclient (enforce)’
935 /usr/sbin/xrdp not confined
982 /sbin/dhclient confined by ‘/sbin/dhclient (enforce)’
992 /usr/sbin/apache2 not confined
993 /usr/sbin/apache2 not confined
994 /usr/sbin/apache2 not confined
1094 /usr/sbin/mysqld confined by ‘/usr/sbin/mysqld (enforce)’
```

```
$
To turn off a specific profile, use the aa-complain command, which places the profile in
complain mode:
$ sudo aa-complain /usr/sbin/tcpdump
Setting /usr/sbin/tcpdump to complain mode.
```

```
$
In complain mode, any violations of the profile will be logged but not blocked. If you
want to completely disable an individual profile, use the aa-disable command:
$ sudo aa-disable /usr/sbin/tcpdump
Disabling /usr/sbin/tcpdump.
```

```
$
To turn a profile back on, use the aa-enforce command:
$ sudo aa-enforce /usr/sbin/tcpdump
Setting /usr/sbin/tcpdump to enforce mode.
```

Though not quite as versatile as SELinux, the AppArmor system provides a basic level of security protection against compromised applications on your Linux system.

# # Understanding Linux User Types

One of the more confusing topics in Linux is the issue of user types. In Linux, not all users are created equal, with some user accounts having different purposes, and therefore different permissions, than others. The following sections discuss the different types of Linux user accounts and how to change between them.