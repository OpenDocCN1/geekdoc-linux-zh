Fedora 15 replaced it with the systemd **init** daemon, which is described in this section. Several other replacements for SysVinit are also available. Ubuntu uses Upstart (upstart.ubuntu.com), Solaris uses SMF (Service Management Facility), and MacOS uses launchd.

The name *systemd* comprises *system*, which systemd manages, followed by *d*. Under UNIX/Linux, daemon names frequently end in *d*: systemd is the system daemon. At boot time, systemd renames itself *init*, so you will not see a process named *systemd*. However, *init* is simply a link to systemd:

```
```
$ ls -l /sbin/init
lrwxrwxwx. 1 root root 22 05-28 12:17 /sbin/init -> ../lib/systemd/systemd
```
```

The name is also a play on words with *System D*, a reference to the French débourillard (to untangle) or démerder. System D is a manner of responding to challenges that requires fast thinking, adapting, and improvising.

The systemd *init* daemon is a drop-in replacement for SysVinit; most of the administrative tools that worked with SysVinit and Upstart work with systemd. Although systemd is relatively new, most of the user interfaces pertinent to administrators will remain stable (www.freedesktop.org/wiki/Software/systemd/InterfaceStabilityPromise).

# MORE INFORMATION

**Local** Use *apropos* to list *man* pages that pertain to systemd (*apropos systemd*). Some of the most interesting of these are *systemd*, *systemctl*, *systemd.unit*, and *systemd.special*.

+   * **Web**
+     systemd home page: www.freedesktop.org/wiki/Software/systemd
+     Fedora systemd home page: fedoraproject.org/wiki/Systemd
+     SysVinit to systemd conversion notes:
+     fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet
+     Blog about systemd by its creator, Lennart Poettering:
+     0pointer.de/blog/projects/systemd.html
+     systemd compatibility with SysV:
+     www.freedesktop.org/wiki/Software/systemd/Incompatibilities
+     systemd stability promise:
+     www.freedesktop.org/wiki/Software/systemd/InterfaceStabilityPromise
+     cgroups (control groups): www.kernel.org/doc/Documentation/cgroups/cgroups.txt

# SERVICE UNITS AND TARGET UNITS

The systemd *init* daemon is based on the concept of units, each of which has a name and *type*. Typically information about a unit is stored in a file that has the same name as the unit (e.g., *dbus.service*). The types of units are *service*, *socket*, *device*, *mount*, *automount*, *target*, *snapshort*, *timer*, *swap*, and *path*. This section discusses *service* and *target* units, which are critical to controlling daemons and runlevel under systemd.