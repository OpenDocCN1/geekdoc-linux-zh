# Listing 12-7
Simple NFS exports File

```
$ cat /etc/exports
# /etc/exports
/home/chris/sandbox/coyote-target *(rw,sync,no_root_squash)
/home/chris/sandbox/pdha-target *(rw,sync,no_root_squash)
/home/chris/workspace *(rw,sync,no_root_squash)
```

These entries on my workstation allow a client to remotely mount any of the three directories shown. The attributes following the directory specification instruct the NFS server to allow connections from any IP address (*) and to mount the respective directories with the given attributes (read/write with no_root_squash). The latter attribute enables a client with root privileges to exercise those privileges on the given directory. It is usually required when working with embedded systems because they often have only root accounts.

You can test your NFS configuration right from your workstation. Assuming that you have NFS services enabled (requires both NFS server and client components enabled), you can mount a local NFS export as you would mount any other file system:

```
# mount -t nfs localhost:/home/chris/workspace /mnt/remote
```

If this command succeeds and the files in .../workspace are available on /mnt/remote, your NFS server and configuration is working.

# 12.3.4 Target NFS Root Mount

Mounting your target via NFS root mount is not difficult, and, as mentioned elsewhere, it is a very useful development configuration. However, a set of details must be correct before it will work. The steps required are as follows:

+   1. Configure your NFS server and export a proper target file system for your architecture.
+   2. Configure your target kernel with NFS client services and root file system on NFS.
+   3. Enable kernel-level autoconfiguration of your target’s Ethernet interface.