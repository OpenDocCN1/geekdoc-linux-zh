# CAUTION

Even if you are running `ntpd` in chroot jail, the copy of `ntp.conf` to edit is still the copy in `/etc`, and not the copy in the jail’s `/etc` directory (which, by default, is `/var/lib/ntp/etc`). The copy is updated automatically by `ntpd`’s startup script.

When you use YaST to set up your NTP client configuration, it also updates `XNTPD_INITIAL_NTPDATE` variable (used by `ntpd` upon system startup to obtain the current date and time information) setting in `/etc/sysconfig/ntp`. However, if you manually edited `/etc/ntp.conf` outside YaST, the `XNTPD_INITIAL_NTPDATE` setting may contain obsolete host data until the next time YaST is used to update the NTP settings. The following example illustrates the telltale sign of this happening when you manually start or restart `ntpd` from a terminal session:

```
Athena:/home/admin # rcxntpd start
Try to get initial date and time via NTP from ticker failed
Starting network time protocol daemon (NTPD)        done
```

Ticker is a time source that has been removed from the network, and its server command entry was manually removed from `/etc/ntp.conf` without using YaST. As a result, `/etc/sysconfig/ntp` contains the outdated information (`XNTPD_INITIAL_NTPDATE = ticker`) leading to the failure message.

# Configuring an NTP Server

`ntpd` can function as an NTP client or as an NTP server or as both concurrently. This allows a single server in the network to run `ntpd` to obtain time from an authoritative time source (either an NTP server on the Internet or a locally attached reference clock); then it redistributes that information to other servers (running ntpd client-only mode) internally. This reduces traffic to the external time source and ensures all NTP clients use a common time source.

There are two ways in which an NTP client can locate an NTP server. The first method is simply to statically configure either the IP address or the DNS name of the NTP source in the client’s `/etc/ntp.conf` file. The other method is to set up the NTP time server to broadcast or multicast its time onto the network and configure the clients to listen for the broadcasted/multicasted time information.

To run `ntpd` with broadcasts or multicasts, add the `broadcast address` command to the configuration file. In broadcast mode, the address should be the broadcast address of one (or one) of the local network(s), such as 192.168.1.255. To enable multicast mode, the address should be 224.0.1.1 (for IPv4) or ff05::101 (site local, for IPv6)—the addresses assigned to NTP. Multiple