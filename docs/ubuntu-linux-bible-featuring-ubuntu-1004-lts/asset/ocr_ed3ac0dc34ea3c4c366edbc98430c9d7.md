# Part III: Ubuntu System Administrators

| 100003 | 2 | udp | 2049 | nfs |
| 100003 | 3 | udp | 2049 | nfs |
| 100003 | 4 | udp | 2049 | nfs |
| 100021 | 1 | udp | 56344 | nlockmgr |
| 100021 | 3 | udp | 56344 | nlockmgr |
| 100021 | 4 | udp | 56344 | nlockmgr |
| 100003 | 2 | tcp | 2049 | nfs |
| 100003 | 3 | tcp | 2049 | nfs |
| 100003 | 4 | tcp | 2049 | nfs |
| 100021 | 1 | tcp | 50947 | nlockmgr |
| 100021 | 3 | tcp | 50947 | nlockmgr |
| 100021 | 4 | tcp | 50947 | nlockmgr |
| 100005 | 1 | udp | 54674 | mountd |
| 100005 | 1 | tcp | 33465 | mountd |
| 100005 | 2 | udp | 54674 | mountd |
| 100005 | 2 | tcp | 33465 | mountd |
| 100005 | 3 | udp | 54674 | mountd |
| 100005 | 3 | tcp | 33465 | mountd |
| 100005 | 1 | tcp | 33465 | mountd |
| 100005 | 2 | udp | 54674 | mountd |
| 100005 | 2 | tcp | 33465 | mountd |
| 100005 | 3 | tcp | 33465 | mountd |

This shows that NFS versions 3 and 4 are both supported by the NFS server and the Lock Manager. In this case, the required services seem to be available on the server. You should also verify that the required services are running on the NFS server and the client system by using the ps command with your favorite options for listing system processes, as in the following example from NFS 4:

```
$ ps -ef | egrep '[rpc/nfs]'
root 16447 - 2 0 Jul 2 ? 00:00:00 [rpciod/0]
statd 17308 1 0 Jul 2 ? 00:00:00 /sbin/rpc.statd
root 17316 1 0 Jul 2 ? 00:00:00 /usr/sbin/rpc.rpcidmapd
root 17345 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17346 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17347 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17348 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17349 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17350 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17351 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17352 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17353 2 0 Jul 2 ? 00:00:00 [nfsd]
root 17357 1 0 Jul 2 ? 00:00:00 /usr/sbin/rpc.mountd
root 17415 2 0 Jul 2 ? 00:00:00 [nfs4-svc]
root 17828 945 0 05:44 tty 00:00:00 egrep [rpc/nfs]
```

An NFS 4 server should be running at least the rpc.rpcidmap, rpc.mountd, and nfs processes. An NFS 4 client should be running at least the rpc.rpcidmap.daemon.