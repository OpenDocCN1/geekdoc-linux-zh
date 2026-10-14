+   -transall, -notransall
+   Enable all transport mechanisms (at the moment there are two: TCP and DDP).
+   -passwd, -nopasswd
+   Enforce entering of passwords.
+   -uampath path
+   In the current implementation, this does nothing.
+   -uservolfirst, nouservolfirst
+   If you have a $HOME/.AppleVolumes file, present volumes listed there first.
+   -uservol, -nouservol
+   Enable use of a $HOME/.AppleVolumes file (see above).

# AppleVolumes Files

Moving on to the AppleVolumes files, let's give an example of an AppleVolumes.default file for the Public AppleTalk Server line in the afpd.conf file earlier in this chapter:

```
~
/stage/projects Projects access=@staff
```

The first line—the tilde (~)—enables users to log in. Upon login, their home directory appears as an available volume. Since we said -nouservol in the afpd.conf file, we aren't allowing an .AppleVolumes file in users' home directories. (You should use these options only for cosmetic purposes. If users want to look at a place other than their home directory, they can make a symbolic link—you can't really do much about it unless you want to hack Netatalk to act more like a Web server and examine symbolic links.)

The second line presents a specific directory (/stage/projects) as the volume Projects, allowing access only for members of the staff group.

Relevant man page: afpd (8)

# 4.4 Web Proxy Service

The disk cache in most Web browsers has a tendency to run against the grain of shared resources. It's stored in a user's home directory with the browser's own caching scheme. This presents a number of problems:

+   There's no sharing of users' caches—if many users access the same page, each user must pull the information through the network.
+   The network connection to the outside world suffers when all users try to use it at once.
+   If you have a large number of users, you have to waste a great deal of disk space on cache directories.