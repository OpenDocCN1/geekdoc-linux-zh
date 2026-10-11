A tool with similar functionality is **chkconfig**. It can be used to disable or enable services and also to list which services are enabled in which runlevel. The following gives a brief overview on how to use chkconfig:

```
dal0:~ # chkconfig cron
cron on
dal0:~ # chkconfig cron -l
cron          0:off 1:off 2:on 3:on 4:off 5:on 6:off
dal0:~ # chkconfig cron off
dal0:~ # chkconfig cron -l
cron          0:off 1:off 2:off 3:off 4:off 5:off 6:off
dal0:~ # chkconfig cron on
dal0:~ # chkconfig -l
Makefile      0:off 1:off 2:off 3:off 4:off 5:off 6:off
SUSEfirewall2_init  0:off 1:off 2:off 3:off 4:off 5:off 6:off
SUSEfirewall2_setup 0:off 1:off 2:off 3:off 4:off 5:off 6:off
aeeventd    0:off 1:off 2:off 3:off 4:off 5:off 6:off
acpid       0:off 1:off 2:on 3:on 4:off 5:on 6:off
alsasound   0:off 1:off 2:on 3:on 4:off 5:on 6:off
atd         0:off 1:off 2:off 3:off 4:off 5:off 6:off
auditd      0:off 1:off 2:on 3:on 4:off 5:on 6:off
...
```

You can also use the YaST runlevel editor to set these links. We recommend that you either use inserv/chkconfig or YaST. Switching between methods can lead to errors.

# **Activate and Deactivate Services for a Runlevel with YaST**

To configure runlevels with YaST, start the YaST Runlevel Editor module by starting YaST and then selecting System > System Services (Runlevel), or open a terminal window and as root enter **yast2 runlevel**.