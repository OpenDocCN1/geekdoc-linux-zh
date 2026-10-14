
-n name Use name as the nbp name. The default is hostname: AFPServer, where hostname is the Linux host name. Chances are, though, if you want to do this, you should use the afpd.conf file.

-s sysvolfile Use sysvolfile as the AppleVolumes.system file.

## Quick Reference to Other afpd.conf Options

-address addr Set the network address of the TCP server.

-afskrb, -noafskrb Enable AFS Kerberos authentication (you'll know if you need it).

-authall, -noauthall Enable all authentication except randnum and rand2num.

-ddp, -nodd p Run a DDP server.

-cleartxt, -nocleartxt Enable clear-text passwords.

-defaultvol file Set the AppleVolumes.default to file.

-guest, -noguest Allow guest access.

-guestname user Set the guest user to user.

-krbiv, -nokrbiv Enable Kerberos IV authentication.

-loginmsg text Display text upon access to a volume.

-nlspath path Set Native Language Support path.

- transall, -notransall
Enable all transport mechanisms (at the moment there are two: TCP and DDP).
- passwd, -nopasswd
Enforce entering of passwords.
- uampath path
In the current implementation, this does nothing.
- uservolfirst, nouservolfirst
If you have a $HOME/.AppleVolumes file, present volumes listed there first.
- uservol, -nouservol
Enable use of a $HOME/.AppleVolumes file (see above).

## AppleVolumes Files

Moving on to the AppleVolumes files, let's give an example of an AppleVolumes.default file for the Public AppleTalk Server line in the afpd.conf file earlier in this chapter:

```
~
/stage/projects Projects access=@staff
```

The first line—the tilde (~)—enables users to log in. Upon login, their home directory appears as an available volume. Since we said -nouservol in the afpd.conf file, we aren't allowing an .AppleVolumes file in users' home directories. (You should use these options only for cosmetic purposes. If users want to look at a place other than their home directory, they can make a symbolic link—you can't really do much about it unless you want to hack Netatalk to act more like a Web server and examine symbolic links.)

The second line presents a specific directory (/stage/projects) as the volume Projects, allowing access only for members of the staff group.

Relevant man page: afpd (8)

## 4.4 Web Proxy Service

The disk cache in most Web browsers has a tendency to run against the grain of shared resources. It's stored in a user's home directory with the browser's own caching scheme. This presents a number of problems:

- There's no sharing of users' caches—if many users access the same page, each user must pull the information through the network.
- The network connection to the outside world suffers when all users try to use it at once.
- If you have a large number of users, you have to waste a great deal of disk space on cache directories.

The built-in caches to Web browsers are not particularly fast. In fact, they are very slow when the user's home directory is not on a local disk (for example, if you mount the cache directory with NFS).

One solution is to install a Web proxy server that maintains a large shared cache for all users on the network. The most popular free server is squid. It comes with most Linux distributions and has a home page at http://www.squid-cache.org/.

Once you install squid, you need to decide what to do about the configuration file, squid.conf. Because this file is enormous, you may have trouble finding the important parameters inside it.

When setting squid up, you need first of all to decide where on the disk to put the cache. The option for this in squid.conf is cache_dir:

```
cache_dir /var/spool/squid/cache 1000 16 256
```

The default is a directory called cache under the prefix where you installed squid. If you configured squid with the defaults, it attempts to use /usr/local/cache—not a good place from the perspective of clean software distribution.

The 1000 in the line above is the total number of megabytes to use for the cache (the default is 100); 16 and 256 specify the numbers of subdirectories for the cache database. This example uses 16 subdirectories in /var/spool/squid/cache, with 256 more subdirectories in each of those original directories. You need to create the base directory (/var/spool/squid/cache here) by hand. After that, run

```
# squid -z
```

to create the rest of the hierarchy. You can have as many cache_dir lines in the squid.conf file as you like; this allows you to use multiple disks for the cache (you won’t need to do this unless you’re running a very large proxy for hundreds of machines).

### PROBLEM 46

Symptom: squid dies with access errors when it’s trying to start.

Problem: You don’t have the cache directory set up.

Fix: The cache directory must be writable by the user that squid is running as. The squid.conf file defines this as cache_effective_user. Use chown to change the ownership of the cache directory (and don’t forget squid -z, above).
