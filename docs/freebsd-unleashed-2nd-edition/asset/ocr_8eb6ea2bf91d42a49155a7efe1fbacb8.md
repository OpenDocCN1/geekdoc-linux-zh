You can solve this problem by placing the noauto option in /etc/fstab, as you saw in the earlier example. However, this means that you have to mount each NFS share manually after the system is fully booted. There's a better way to handle this—the -b option. Here's an example:

```
# Device            Mountpoint     Fstype Options   Dump Pass#
spots:/home         /home2         nfs     rw,-b     0    0
```

The -b option tells mount to make a quick attempt to contact the server, and if it can't, to fork off a child process to continue trying to connect while the boot process continues on. Similarly, if you mount a share from the command line using -b, the process forks into the background and returns you to the command prompt. The following is the output you would get when trying to mount the share specified in the preceding sample /etc/fstab line, after trying for 60 seconds:

```
# mount /home2

spots:/home: nfsd: RPCPROG_NFS: RPC: Port mapper failure - RPC: Timed out
nfs: Cannot immediately mount spots:/home, backgrounding
```

The background mount_nfs process will keep trying to mount the share until it's successful. This method is particularly useful in computing clusters or labs in which NFS-mounted resources are nice to have but not required for correct operation—for example, a cluster in which an NFS mount contains popular user programs or games, but all critical system functions are available on disks on the local system.

# ## Auto-Mount Daemon (amd)

The auto-mount daemon, amd, makes NFS mounts even more convenient. This daemon allows you to mount NFS shares (and other filesystem types, as a matter of fact) dynamically, simply by working in the directory in which the share would be mounted, without ever having to bother with mount commands.

FreeBSD provides a basic way to set up amd. Simply add the following line to /etc/rc.conf:

```
amd_enable="YES"
```

When the system is booted with this option, amd runs with the options specified in the amd_flags setting, which are such that anything in the /host or /net directories—both of which are created automatically by amd—will auto-mount by name. You can also start it in the same way as it would be at boot time by issuing the following command:

```
# amd -a /.amd_mnt -1 syslog /host /etc/amd.map /net /etc/amd.map
```