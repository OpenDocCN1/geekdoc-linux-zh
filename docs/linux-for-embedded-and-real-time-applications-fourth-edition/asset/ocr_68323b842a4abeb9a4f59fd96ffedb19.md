![](bbox=[0.18, 0.08, 0.83, 0.27])

![](bbox=[0.18, 0.44, 0.83, 0.48])

# Figure 4.3
Systemctl command.

systemctl is the user interface to the systemd system and service manager. The arguments to systemctl are a command and the name of a service, which is represented by a script file in /usr/lib/systemd/system. If the NFS server is not running, you start it with this command:

```
systemctl start nfs-server
```

To stop it you would execute:

```
systemctl stop nfs-server
```

If, for example, you were to make changes to /etc/exports, you would want to restart NFS for the changes to take effect:

```
systemctl restart nfs-server
```

Look in /usr/lib/systemd/system to see that there is a script file named nfs-server.service. Have a look at the file to see how it works.

# Trivial File Transfer Protocol

The last item of business for this chapter is installing (if necessary) and enabling TFTP, the Trivial File Transfer Protocol. We will use that later when building a new Linux kernel.