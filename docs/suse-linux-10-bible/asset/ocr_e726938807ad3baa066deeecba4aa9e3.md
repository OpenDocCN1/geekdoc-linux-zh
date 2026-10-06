day, so it cannot be used to find files that have been created or moved very recently unless you manually update the database.

To find a file using locate is as simple as this example:

```
usable:> traceroute
/usr/sbin/traceroute
/usr/sbin/traceroute6
/usr/share/man/man/traceroute.1.gz
/usr/share/man/man/traceroute.6.gz
```

> Note The utility is located in /usr/bin/locate, but is installed only if you've installed the Experienced User set of packages on your system using YaST software installation module.

Note that any file whose name contains the string given (in this case traceroute) will be found.

The updating of locate database is daily from the file /etc/cron.daily/updatedb, which reads parameters from /etc/sysconfig/locate. In /etc/sysconfig/locate you can set whether or not you want the automatic updating to take place at all and which paths you want to be excluded from the database (by default, temporary and spool files are excluded, as removable media).

If you want to update the database manually, run the command (as root) /etc/cron.daily/updatedb. This is the command that is normally run automatically each day. It runs across the whole system, and writes the results to the database file /var/lib/locate It takes account of the settings in /etc/sysconfig/locate and calls /usr/sbin/updateddb with the correct options. As this command searches the entire system, it is, not surprisingly, fairly intensive.

# Using Konqueror to Find Files

Konqueror has a menu option (Tools Find File) that searches for files under the directory displayed when it is running in manager mode (see Figure 13-1).

# Finding Files in GNOME

The find files functionality in GNOME is separated from the Nautilus file manager itself. There is a small application called gnome-search-tool that can be accessed through the Actions on the desktop (Actions Search for Files), as shown in Figure 13-2.