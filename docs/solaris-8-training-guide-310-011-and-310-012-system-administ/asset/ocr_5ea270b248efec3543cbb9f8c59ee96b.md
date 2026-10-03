# APPLY YOUR KNOWLEDGE

# Exercises

The following exercises require a minimum of two networked Solaris systems. Determine in advance, which system will serve as the NFS server and which system will be the NFS client. The NFS server must have manual pages installed in the /usr/share/man directory.

# 17.1 NFS Server setup

In this exercise, you’ll set up an NFS server to share the contents of the /usr/share/man directory for read-only access.

Estimated Time: 30 minutes

+   1. Make the following entry in the /etc/dfs/dfstab file:
```
share -F nfs -o ro /usr/share/man
```
2. Restart the /etc/init.d/nfs.server script to start the nfsd and mountd daemons:
```
/etc/init.d/nfs.server start
```
3. Verify that the two daemons are running by typing:
```
ps -ef|grep nfs
```
4. Verify that the resource is shared by typing the following:
```
share
```
The system should display:
```
. /usr/share/man ro ""
```
5. On the NFS client, rename the /usr/share/man directory so that man pages are no longer accessible by typing:
```
cd /usr/share
mv man man.bkup
```
6. Verify that the manual pages are no longer accessible by typing the following:
```
man tar
```

+   7. Create a new man directory to be used as a mount point as follows:
```
mkdir man
```
8. Verify that you are able to see the shared resource on the NFS server by typing the following:
```
dfshares <nfs server name>
```
The system should display a message similar to the following:
```
RESOURCE SERVER ACCESS TRANSPORT
192.168.0.4:/usr/share/man 192.168.0.4 -
```
9. Mount the /usr/share/man directory located on the NFS server to the directory you created in the previous step as follows:
```
mount <nfs server name>:/usr/share/man \
/usr/share/man
```
10. Now see if the man pages are accessible by typing the following:
```
man tar
```
11. Verify the list of mounts that the server is providing by typing:
```
dfmounts <nfs server name>
```
The system displays something like this:
```
RESOURCE SERVER PATHNAME \
CLIENTS
- 192.168.0.4 /usr/share/man \
192.168.0.21
```
12. Unmount the directory on the NFS client as follows:
```
umountall -r
```
Note that the -r option specifies that only remote file system types are to be unmounted.