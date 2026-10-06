# 7.3.2 Configuring Arkeia

Before you can configure Arkeia, check whether the Arkeia backup server is running. To do this, enter:

```
ps -ef | grep -v grep | grep nlservd
```

on the system which should be used as your backup server. If you see a line like

```
root 488 1 0 09:06 ? 00:00:00 /usr/knox/knox/bin/nlservd start
```

the backup server is running. To begin with the configuration of Arkeia, be sure, your X-Windows running. Then enter on the command line:

Arkeia

You will see a dialog like Figure 232:

![](bbox=[0.262, 0.319, 0.735, 0.568])

Figure 232. Arkeia initial window

The field for the server name is by default filled in with the name of the system you currently work with. You must change this field if you have installed the server component on another system.

The field for the login name is by default filled in with root. Change it if you have changed the name of the Arkeia administrator.