There are two start-up scripts that you should turn on for the NFS service to work properly. The NFS service exports file systems (from /etc/exports) and starts the nfsd daemon that listens for service requests. The NFSLOCK service starts the lockd daemon, which helps allow file locking to prevent multiple simultaneous use of critical files over the network.

> **NOTE**  If you see the message “Cannot register service: RPC: Unable to receive; errno=connection refused,” you probably need to start the portmap service on the client machine.

You can use the chkconfig command to turn on the NFS service by typing the following commands (as root user):

```
```
# chkconfig nfs on
```
```

The next time you start your computer, the NFS service will start automatically, and your exported directories will be available. If you want to start the service immediately, without waiting for a reboot, you can type the following:

```
```
# /etc/init.d/nfs start
```
```

The NFS service should now be running and ready to share directories with other computers on your network.

# Using NFS File Systems

After a server exports a directory over the network using NFS, a client computer connects that directory to its own file system using the mount command. The mount command is the same one used to mount file systems from local hard disks, CDs, and USB flash drives. Only the options to give to mount are slightly different.

The mount command can automatically mount NFS directories that are added to the /etc/fstab file, just as it does with local disks. NFS directories can also be added to the /etc/fstab file in such a way that they are not automatically mounted. With a noauto option, an NFS directory listed in /etc/fstab is inactive until the mount command is used, after the system is up and running, to mount the file system. The _netdev_ option will automatically mount the directory but will delay doing so until after the networking is up.

# Manually Mounting an NFS File System

If you know that the directory from a computer on your network has been exported (i.e., made available for mounting), you can mount that directory manually using the mount command. This is a good way to make sure that it is available and working before you set it up to mount permanently. Here’s an example of mounting the /home/timothy/files directory from a computer named flashg on your local computer:

```
```
# mkdir /media/flashg
# mount flashg:/home/timothy/files /media/flashg
```
```