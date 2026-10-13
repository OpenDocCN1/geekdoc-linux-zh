+   - `rpc.ypasswdd`
+   - `rpc.ypxfrd`

> **Note**
> 
> `rpc.ypasswdd` is a program that runs only on the NIS master and allows users to change their NIS passwords. `rpc.ypxfrd` also only runs on the NIS master and speeds up map transfers to NIS slave servers.

To start ypserv and ypbind use the following commands:

```
# /etc/rc.d/init.d/ypserv start
# /etc/rc.d/init.d/ypbind start
```

To start rpc.ypasswdd, use this command:

```
# /etc/rc.d/init.d/ypasswdd start
```

To start rpc.ypxfrd, use this command:

```
# /usr/sbin/rpc.ypxfrd
```

When the system is rebooted, these programs will start automatically. On some Linux systems, rpc.ypxfrd will not be configured to start at boot time and you will need to edit the scripts in /etc/rc.d/init.d/ to make sure the program starts when the system boots. Consult Chapter 4, “Booting Up and Shutting Down Linux,” for details of the boot process and the scripts in /etc/rc.d/init.d/.

# SETTING UP AN NIS CLIENT

Once you have set up your NIS master server, you can configure your NIS clients to use the master server to handle NIS service requests. The following three steps are required to configure an NIS client:

+   1. Setting the NIS domain name in the `/etc/yp.conf` file
+   2. Running ypbind
+   3. Editing the `/etc/passwd` file

# SETTING THE NIS DOMAIN NAME IN THE /etc/yp.conf FILE

On the NIS client, you set the NIS domain name in the /etc/yp.conf file. This file is read by the ypbind daemon, which connects your NIS client to the appropriate NIS domain.