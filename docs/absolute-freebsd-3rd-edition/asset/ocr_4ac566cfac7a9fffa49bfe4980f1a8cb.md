```
`^C
--- 203.0.113.1 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max/stddev = 1.436/1.569/1.701/0.133 ms`
```

For IPv6, use ping6(8) instead of ping(8). If you use router discovery, the default route will almost always be a link-local address.

```
`# ping6 2001:db8::1
PING6(56=40+8+8 bytes) 2001:db8::bad:c0de:cafe --> 2001:db8::1
16 bytes from 2001:db8::1, icmp_seq=0 hlim=64 time=0.191 ms
16 bytes from 2001:db8::1, icmp_seq=1 hlim=64 time=0.186 ms
16 bytes from 2001:db8::1, icmp_seq=2 hlim=64 time=0.197 ms
--snip--`
```

If you don’t get any answers, your network connection isn’t working. Either you have a bad connection (check your cables and link lights) or you have misconfigured your card.

# ## Set Default Route

The default route is the address where your system sends all traffic that’s not on the local network. If you can ping the default route’s IPv4 address, set it via route(8).

```
`# route add default 203.0.113.1`
```

That’s it! You should now be able to ping any public IPv4 address on the internet.

Adding the default IPv6 route is much the same, but you need to add the -6 command line flag to change the IPv6 routing table.

```
`# route -6 add default 2001:db8::1`
```

If you didn’t choose nameservers during the system install, you’ll have to use the IP address rather than the hostname.

Once you have a working default router, make it persist across reboots by adding the proper *defaultrouter* and *ipv6_defaultrouter* entries in *etc/rc.conf*: