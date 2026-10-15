
# Configure DHCP Pools and Failover

On the secondary server, the corresponding messages look like:

```
Jul 4 12:00:20 da12 dhcpcd: DHCPREQUEST for 149.44.85.16 from 00:04:ac:d6:58:96 via eth1: ignored (not authoritative).
Jul 4 12:00:25 da12 dhcpcd: DHCPREQUEST for 149.44.85.16 from 00:04:ac:d6:58:96 via eth1: ignored (not authoritative).
Jul 4 12:00:30 da12 dhcpcd: pool 800e40f8 10.0.0.111 total 20 free 10 backup 10 its 0
Jul 4 12:00:30 da12 dhcpcd: DHCPDISCOVER from 00:04:ac:d6:58:96 via eth1
Jul 4 12:00:31 da12 dhcpcd: DHCPOFFER on 10.0.0.111 to 00:04:ac:d6:58:96 (linux-5ncs) via eth1
Jul 4 12:00:31 da12 dhcpcd: DHCPREQUEST for 10.0.0.111 (10.0.0.111) from 00:04:ac:d6:58:96 (linux-5ncs) via eth1
Jul 4 12:00:31 da12 dhcpcd: DHCPACK on 10.0.0.111 to 00:04:ac:d6:58:96 (linux-5ncs) via eth1
```

On this server, the DHCPOFFER message is printed as this server offers the IP address. The final message is DHCPACK from the client.

The DHCP log file /var/lib/dhcp/db/dhcpd.leases contains information like this:

```
failover peer "digitalairlines" state {
  my state recover at 2 2006/07/04 09:57:39;
  partner state unknown-state at 2 2006/07/04 09:57:39;
}

failover peer "digitalairlines" state {
  my state recover at 2 2006/07/04 09:57:39;
  partner state recover at 2 2006/07/04 09:57:39;
}

failover peer "digitalairlines" state {
  my state recover-done at 2 2006/07/04 09:57:56;
  partner state recover at 2 2006/07/04 09:57:39;
}

failover peer "digitalairlines" state {
  my state recover-done at 2 2006/07/04 09:57:56;
  partner state recover-done at 2 2006/07/04 09:57:39;
}

failover peer "digitalairlines" state {
  my state normal at 2 2006/07/04 09:57:56;
  partner state recover-done at 2 2006/07/04 09:57:39;
}

failover peer "digitalairlines" state {
  my state normal at 2 2006/07/04 09:57:56;
  partner state normal at 2 2006/07/04 09:57:39;
}
lease 10.0.0.120 {
  starts 2 2006/07/04 09:57:56;
  tstp 2 2006/07/04 09:57:56;
  binding state backup;
}
lease 10.0.0.119 {
  starts 2 2006/07/04 09:57:56;
  tstp 2 2006/07/04 09:57:56;
  binding state backup;
}
...
```

```
...
lease 10.0.0.120 {
  starts 2 2006/07/04 09:57:56;
  tstp 2 2006/07/04 09:57:56;
  tsfp 2 2006/07/04 09:57:56;
  binding state backup;
}
lease 10.0.0.119 {
  starts 2 2006/07/04 09:57:56;
  tstp 2 2006/07/04 09:57:56;
  tsfp 2 2006/07/04 09:57:56;
  binding state backup;
}
...
lease 10.0.0.111 {
  starts 2 2006/07/04 10:00:31;
  ends 2 2006/07/04 10:30:31;
  tstp 2 2006/07/04 09:57:56;
  tsfp 2 2006/07/04 10:45:31;
  cltt 2 2006/07/04 10:00:31;
  binding state active;
  next binding state expired;
  hardware ethernet 00:04:ac:d6:58:96;
  uid "\001\000\004\254\326X\226";
}
```

The file /var/lib/dhcp/db/dhcpd.leases on the secondary contains information like the following:

```
failover peer "digitalairlines" state {
  my state recover at 2 2006/07/04 09:58:50;
  partner state unknown-state at 2 2006/07/04 09:58:50;
  mclt 0;
}

failover peer "digitalairlines" state {
  my state recover at 2 2006/07/04 09:58:50;
  partner state recover at 2 2006/07/04 09:58:50;
  mclt 1800;
}

failover peer "digitalairlines" state {
  my state recover-done at 2 2006/07/04 09:58:51;
  partner state recover at 2 2006/07/04 09:58:50;
  mclt 1800;
}

failover peer "digitalairlines" state {
  my state recover-done at 2 2006/07/04 09:58:51;
  partner state recover-done at 2 2006/07/04 09:58:50;
  mclt 1800;
}

failover peer "digitalairlines" state {
  my state normal at 2 2006/07/04 09:58:51;
  partner state recover-done at 2 2006/07/04 09:58:50;
  mclt 1800;
}

failover peer "digitalairlines" state {
  my state normal at 2 2006/07/04 09:58:51;
  partner state normal at 2 2006/07/04 09:58:50;
  mclt 1800;
}
lease 10.0.0.120 {
  starts 2 2006/07/04 09:57:56;
  tsfp 2 2006/07/04 09:57:56;
  binding state backup;
}
```

When the secondary server fails (e.g. the server is shut down) and recovers later again, messages like the following will appear in /var/log/messages on the primary:

```
Jul 4 12:16:25 dal0 dhcpd: peer digitalairlines:
disconnected
Jul 4 12:16:25 dal0 dhcpd: failover peer digitalairlines:
I move from normal to communications-interrupted
Jul 4 12:20:06 dal0 dhcpd: failover peer digitalairlines:
peer moves from normal to normal
Jul 4 12:20:06 dal0 dhcpd: failover peer digitalairlines:
I move from communications-interrupted to normal
Jul 4 12:20:06 dal0 dhcpd: pool 800e4138 10.0.0/24 total 20 free 10 backup 9 lts 0
```

On the secondary, the startup messages look like this:

```
Jul 4 12:21:01 dal2 dhcpd: failover peer digitalairlines:
I move from normal to startup
Jul 4 12:21:01 dal2 dhcpd: failover peer digitalairlines:
peer moves from normal to communications-interrupted
Jul 4 12:21:01 dal2 dhcpd: failover peer digitalairlines:
I move from startup to normal
Jul 4 12:21:01 dal2 dhcpd: failover peer digitalairlines:
peer moves from communications-interrupted to normal
Jul 4 12:21:01 dal2 dhcpd: pool 800e40f8 10.0.0/24 total 20 free 10 backup 9 lts 0
```

In order to not get confused about the time stamps, make sure that you synchronize the time stamps of all your servers using the network time protocol (ntp).
