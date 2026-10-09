If you get a permission denied message, check that

+   • You have not specified **rw** access in `/etc/exports` when the client has only read permission to the directory hierarchy.
+   • You have specified the directory hierarchy and client correctly in `/etc/exports`.
+   • You have not edited `/etc/exports` since you last ran `exportfs -r`.
+   • You are not trying to export a directory hierarchy and a subdirectory of that hierarchy. From the client you can mount a directory hierarchy and a sub-directory of that hierarchy separately, but you cannot export both from the server. Export the higher-level directory only.

Finally, try mounting directory hierarchies from remote systems and verify access.

# automount: Mounts Directory Hierarchies on Demand

In a distributed computing environment, when you log in on any system on the network, all your files—including startup scripts—are available. All systems are also commonly able to mount all directory hierarchies on all servers: Whichever system you log in on, your home directory is waiting for you.

As an example, assume `/home/zach` is a remote directory hierarchy that is mounted on demand. When Zach logs in or when you issue the command `ls /home/zach`, `autofs` goes to work: It looks in the `/etc/auto.misc` map, finds `/home/zach` is a key that says to mount `plum:/home/zach`, and mounts the remote directory hierarchy. Once the directory hierarchy is mounted, `ls` displays the list of files in that directory.

The `automount` maps can be stored on NFS and LDAP servers in addition to the local filesystem. Unless you change the `automount` entry in the `/etc/nsswitch.conf` file (page 495), the `automount` daemon will look for maps as files on the local system.

# PREREQUISITES

Install the following package:

+   • `autofs`

Run `systemctl` to cause the `autofs` service (**automount** daemon) to start each time the system enters multiuser mode and then start the `autofs` service. Use the `systemctl status` command to make sure the service is running.

```
# systemctl enable autofs.service
# systemctl start autofs.service
```

After modifying `autofs` configuration files, give the second command again, replacing **start** with **restart** to cause `autofs` to reread those files.