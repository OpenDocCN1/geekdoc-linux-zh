```
syslogd_flags="-ss"
```

If you need to send syslogd messages, use the -b flag to force syslogd to attach to only a single IP address.

```
syslogd_flags="-b 198.51.100.50"
```

Either solution lets your jails' administrators individually decide whether or not they’re going to log across the network. See Chapter 21 for a full discussion of syslogd.

# inetd

If you need inetd (see Chapter 20), you should almost certainly run it from within a jail rather than the host. If you can’t weasel out of running inetd on the host, though, use the -a flag to restrict it to a single IP address, as in the following rc.conf snippet.

```
inetd_flags="-a 198.51.100.50 -wW -C 60"
```

If I had only specified the -a flag and the IP address, it would’ve overwritten inetd’s default flags from /etc/defaults/rc.conf. Every release of FreeBSD from the last few decades has used the default flags of -wW -C 60; I added my -a and the IP address to those flags.

# sshd

The option ListenAddress in /etc/ssh/sshd_config tells sshd(8) which addresses to bind to. Restrict it to only your host IP.

```
ListenAddress 198.51.100.50
```

If the only service your jail host offers is sshd(8), you’ve done well.

# NFS

Network filesystem programs, such as rpcbind(8) and nfsd(8), bind to all IP addresses on a host, no matter what you do. Don’t run these programs inside a jail, and don’t run NFS from within a jail. If your