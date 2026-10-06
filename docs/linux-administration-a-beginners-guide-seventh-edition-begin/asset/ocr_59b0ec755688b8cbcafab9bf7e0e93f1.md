# Starting and Stopping Samba

Most distributions of Linux have scripts and programs that will start and stop Samba without needing to do anything special. They take care of start-up at boot time and stopping at shutdown. On our sample systemd-enabled system running Fedora with Samba installed via RPM, the systemctl utility can manage Samba's start-up and shutdown.

For example, to start the smbd daemon, you can execute this command:

```
[root@server ~]# systemctl start smbd.service
```

And to stop the service, this type:

```
[root@server ~]# systemctl stop smbd.service
```

After making any configuration changes to Samba, you can restart it with this command to make the changes into effect:

```
[root@server ~]# systemctl restart smbd.service
```

Out of the box, the service might not automatically start up with the next reboot. You can use the systemctl command on systemd-enabled Linux distros like Fedora to make sure the samba unit is enabled to automatically start when the system boots by typing

```
[root@fedora-server ~]# systemctl enable smbd.service
```

> Stopping Samba without the use of proper scripts is a little trickier. But in general, you may have to use the ps command to list all of the Samba processes. From this list, find the instance of samba that is owned by root and kill this process. This will also kill all of the other Samba connections.

+   You can start the Samba daemon that we installed from source earlier from the command line with this command:
# /usr/local/samba/sbin/smbd -D
The only command-line parameter used here (-D) tells smbd to run as a daemon.
nmbd can be started in the same manner with
# /usr/local/samba/sbin/nmbd -D

# Creating a Share

We will walk through the first process of creating a share under the /tmp directory to be shared on the Samba. We'll first create the directory to share and then edit Samba's configuration (etc/samba/smb.conf) to create an entry for the share.
If you have any of the mainstream graphical desktop environments installed and running, you can often use tools built into the environment to complete simple file-sharing tasks for Samba or use any of the available web-based utilities to manage