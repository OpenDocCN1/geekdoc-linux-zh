# # TROUBLESHOOTING

*I get a port not registered or server denied access error when I try to mount a remote share.*

This problem can be very frustrating for those new to NFS. It seems that almost all errors result in a **port not registered** error. You might also see a **server denied access** error. You need to take the following steps:

+   1. Run `rpcinfo -p hostname`, substituting the server and then client name for `hostname`. All registered ports show up. If any ports don’t show up (nfs or mountd), you need to restart those daemons so the portmapper knows which ports they have chosen.
+   2. Check to ensure that you have the necessary modules loaded on both the server and client. The server needs `nfsd` (if loaded with modprobe, `nfsd` should load `sunrpc` and `lockd` first—if not, you don’t have a `/lib/modules/2.4.x/modules.conf` file). The client needs `nfs`, which also loads `sunrpc` and `lockd` first.
+   3. Ensure that you are exporting the directory on the server that you want to mount on the client.
+   4. If you still can’t mount the NFS share, ensure that your `/etc/hosts.allow` and `/etc/hosts.deny` files on the server are permitting you to mount the shares. Also ensure that you haven’t inadvertently blocked yourself out with `netfilter`. Your logs should note any attempts to mount the filesystem.
+   5. Finally, make sure your program versions are the same. This should not be an issue if you’re using the same distribution and version, but it might be if one system is running Caldera OpenLinux 1.3 and the other Red Hat 6.2 or varying versions of Debian or Red Hat.

*When I use a client with shares mounted from the server, all my files have the correct ownership. When I use a different client, my files either have numbers or the wrong name.*

What has happened is that you have `/etc/passwd`, `/etc/shadow`, and `/etc/group` files that are dissimilar between systems. If your account name is dab on all three systems, two of them might have your UID as 1000, and the other as some other number (like 1000). What the operating systems and NFS use are UIDs, whereas you use a name. Always use one system as your administrative system, update those files, and have cron run `rsync` to update those files on the other systems. Until Linux has a workable NIS+ server and client, `rsync` is the most feasible method for keeping systems in sync. Alternatively, just copy or FTP these three files, but be careful with file permissions. The NIS implementation, while available, is notoriously unsecure and should be used only on a very secure network.

![](bbox=[0.932, 0.082, 0.999, 0.341])