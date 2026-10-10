However, for systems that use traditional UNIX SysV system initialization, you must create or modify the symbolic links within the /etc/rc[runlevel]d directories. To make this process easier, there are commands that you can use to do this for you. The **chkconfig** command is available on many Linux systems, and can be used to both list and modify the runlevels that a daemon is started in. For example, the following command indicates that the postfix daemon is not started in any runlevel:

```
```
[root@server1 ~]# chkconfig --list postfix
postfix  0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@server1 ~]#
```
```

To configure the postfix daemon to start in runlevels 3 and 5 and to verify the results, you could run the following commands:

```
```
[root@server1 ~]# chkconfig --level 35 postfix on
[root@server1 ~]# chkconfig --list postfix
postfix  0:off 1:off 2:off 3:on 4:off 5:on 6:off
[root@server1 ~]#
```
```

Unfortunately, the chkconfig command is not available in Ubuntu Server 14.04 by default. Instead, you can use the **update-rc.d** command on Ubuntu Server 14.04 to configure the files within the /etc/rc[runlevel]d directories. First, you should remove any existing symbolic links within the /etc/rc[runlevel]d directories for the postfix daemon using the following command:

```
```
[root@server1 ~]# update-rc.d -f postfix remove
Removing any system startup links for /etc/init.d/postfix ...
/etc/rc0.d/K20postfix
/etc/rc1.d/K20postfix
/etc/rc2.d/S20postfix
/etc/rc3.d/S20postfix
/etc/rc4.d/S20postfix
/etc/rc5.d/S20postfix
/etc/rc6.d/K20postfix
[root@server1 ~]#
```
```

Next, you can use the update-rc.d command to configure the appropriate symbolic links within the /etc/rc[runlevel]d directories for the postfix daemon. Since most daemons are started in runlevels 2 through 5, you can specify the **defaults** keyword to create symbolic links that start the postfix daemon in runlevels 2 through 5, as shown in the following output:

```
```
[root@server1 ~]# update-rc.d postfix defaults
Adding system startup for /etc/init.d/postfix ...
/etc/rc0.d/K20postfix -> ../init.d/postfix
/etc/rc1.d/K20postfix -> ../init.d/postfix
/etc/rc6.d/K20postfix -> ../init.d/postfix
/etc/rc2.d/S20postfix -> ../init.d/postfix
/etc/rc3.d/S20postfix -> ../init.d/postfix
/etc/rc4.d/S20postfix -> ../init.d/postfix
/etc/rc5.d/S20postfix -> ../init.d/postfix
[root@server1 ~]#
```
```