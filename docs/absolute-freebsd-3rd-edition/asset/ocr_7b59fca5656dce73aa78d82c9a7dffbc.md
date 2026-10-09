and mountd(8). If you must list hostnames, put them at the end of the line.

```
```text
/usr/home/mw Lucas www1 www2 www3
```
```

Assigning NFS on a per-host basis is more labor. Assign NFS permissions as broadly as possible without compromising security.

# **Combinations of Clients and Exports**

Each line in `/etc/exports` specifies exports from one partition to one network, address, or set of hosts. Different hosts require entirely different export statements. You can change the options for each if you wish.

```
```text
/usr/home/mw Lucas /usr/src /usr/obj /usr/ports/distfiles \
-maproot=5000 203.0.113.200
/usr -maproot=0 203.0.113.201
```
```

Here, I've exported several subdirectories of `/usr` to the NFS client at 203.0.113.200. The NFS client at 203.0.113.201 gets to mount the whole of `/usr` and may even do so as root.

# **NFS and Firewalls**

NFS is famous for not liking firewalls. The dynamic port assignment of services like mountd(8), rpc.lockd(8), and rpc.statd(8) makes packet filtering nearly impossible. You can use the -p flag to assign each of these services a specific TCP port. Here, I use `rc.conf` entries to nail mountd(8) to port 4046, rpc.lockd(8) to 4045, and rpc.statd(8) to 4047:

```
```text
mountd_flags="-r -p 4046"
rpc_lockd_flags="-p 4045"
rpc_statd_flags="-p 4047"
```
```

I can use these ports in my packet filter rules, providing some protection to my NFS server.

# **Managing NFS with zfs(8)**