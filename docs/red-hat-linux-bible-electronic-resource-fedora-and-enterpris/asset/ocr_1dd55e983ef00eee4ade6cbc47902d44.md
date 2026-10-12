# Using NFS file systems

After a server exports a directory over the network using NFS, a client computer connects that directory to its own file system using the `mount` command. The mount command is the same one used to mount file systems from local hard disks, CDs, and floppies. Only the options to give to mount are slightly different.

Mount can automatically mount NFS directories that are added to the `/etc/fstab` file, just as it does with local disks. NFS directories can also be added to the `/etc/fstab` file in such a way that they are not automatically mounted. With a `noauto` option, an NFS directory listed in `/etc/fstab` is inactive until the `mount` command is used, after the system is up and running, to mount the file system.

# Manually mounting an NFS file system

If you know that the directory from a computer on your network has been exported (that is, made available for mounting), you can mount that directory manually using the `mount` command. This is a good way to make sure that it is available and working before you set it up to mount permanently. Here is an example of mounting the `/tmp` directory from a computer named maple on your local computer:

```
```shell
# mkdir /mnt/maple
# mount maple:/tmp /mnt/maple
```
```

The first command (`mkdir`) creates the mount point directory (`/mnt` is a common place to put temporarily mounted disks and NFS file systems). The `mount` command then identifies the remote computer and shared file system separated by a colon (`maple:/tmp`). Then, the local mount point directory follows (`/mnt/maple`).

> **NOTE:** If the mount failed, make sure the NFS service is running on the server and that the server's firewall rules don't deny access to the service. From the server, type `ps ax | nfsd`. You should see a list of `nfsd` server processes. If you don't, try to start your NFS daemons as described in the previous section. To view your firewall rules, type `ipchains -L` or `iptables -L` depending on which firewall service you are using (see Chapter 14 for a description of firewalls). By default, the `nfsd` daemon listens for NFS requests on port number 2049. Your firewall must accept `udp` requests on ports 2049 (nfs) and 111 (rpc).

To ensure that the mount occurred, type `mount`. This command lists all mounted disks and NFS file systems. Here is an example of the mount command and its output:

```
```shell
# mount
/dev/hda3 on / type ext3 (rw)
none on /proc type proc (rw)
none on /dev/pts type devpts (rw, gid=5, mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
maple:/tmp on /mnt/maple type nfs (rw, addr=10.0.0.11)
```
```