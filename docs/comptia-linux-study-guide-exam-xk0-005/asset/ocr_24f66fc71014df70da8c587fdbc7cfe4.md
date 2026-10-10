In Table 6.1, you'll notice that systemd provides backward compatibility to the classic SysV init systems. The SysV runlevels will be covered later in this chapter.

> > **TIP**
> > The master systemd configuration file is the /etc/systemd/system.conf file. In this file you will find all the default configuration settings commented out via a hash mark (#). Viewing this file is a quick way to see the current systemd configuration. If you need to modify the configuration, just edit the file. However, it would be wise to peruse the file's man page first by typing man systemd-system.conf at the command line.

# ### Focusing on Service Unit Files

Service unit files contain information, such as which environment file to use, when a service must be started, what targets want this service started, and so on. These configuration files are located in different directories.

Keep in mind that a unit configuration file's directory location is critical, because if a file is found in two different directory locations, one will have precedence over the other. The following list shows the directory locations in ascending priority order:

+   1. /etc/systemd/system/
+   2. /run/systemd/system/
+   3. /usr/lib/systemd/system/

To see the various service unit files available, you can again employ the `systemctl` utility. However, a slightly different command is needed than when viewing units, as shown in Listing 6.6.

# **Listing 6.6** Looking at systemd unit files

```
```
$ systemctl list-unit-files
UNIT FILE                    STATE
[...]                        
dev-hugepages.mount        static
dev-mqueue.mount           static
proc-fs-nfsd.mount         static
[...]                        
nfs.service                  disabled
nfslock.service              static
ntpd.service                 disabled
ntpdate.service              disabled
[...]                        
ctrl-alt-del.target        static
default.target               static
emergency.target             static
[...]                        
```
```