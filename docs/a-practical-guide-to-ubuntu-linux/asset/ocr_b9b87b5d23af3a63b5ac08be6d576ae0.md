# TESTING THE SERVER SETUP

From the server, run the nfs-kernel-server init script with an argument of status. If all is well, the system displays the following:

```
$ service nfs-kernel-server status
nfs running
```

Also check that mountd is running:

```
$ ps -e | grep mountd
29609 7      00:00:00 rpc.mountd
```

Next, for the server, run rpcinfo to make sure nfs is registered with portmap:

```
$ rpcinfo -p localhost | grep nfs
100003 2 udp 2049 nfs
100003 3 udp 2049 nfs
100003 4 udp 2049 nfs
100003 2 tcp 2049 nfs
100003 3 tcp 2049 nfs
100003 4 tcp 2049 nfs
```

Repeat the preceding command from the client, replacing localhost with the name of the server. The results should be the same.

Finally, try mounting directory hierarchies from remote systems and verify access.

# automount: MOUNTS DIRECTORY HIERARCHIES ON DEMAND

In a distributed computing environment, when you log in on any system on the network, all your files—including startup scripts—are available. All systems are also commonly able to mount all directory hierarchies on all servers: Whenever you log in on, your home directory is waiting for you.

As an example, assume /home/zach is a remote directory hierarchy that is mounted on demand. When you issue the command ls /home/zach, autofofs goes to work: It looks in /etc/auto.home map, finds zach is a key that says to mount plum:/export/home/zach, and mounts the remote directory hierarchy. Once the directory hierarchy is mounted, ls displays the list of files in your directory. If you give the command ls /home after this mounting sequence, ls shows that zach is present within the /home directory. The df utility shows that zach is mounted

# PREREQUISITES

Install the following package:

+   - autofofs