# Networking and Internet Services
PART II

PING sylvia.subdomain.domain.cxm (192.168.42.40): 56 data bytes
64 bytes from 192.168.42.40: icmp_seq=0 ttl=255 time=0.398 ms
sylvia.subdomain.domain.cxm ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.235/0.316/0.398 ms

# brett.subdomain.domain.cxm
PING brett.subdomain.domain.cxm (192.168.42.41): 56 data bytes
64 bytes from 192.168.42.41: icmp_seq=0 ttl=255 time=0.479 ms
brett.subdomain.domain.cxm ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.242/0.360/0.479 ms

# rena.subdomain.domain.cxm
PING rena.subdomain.domain.cxm (192.168.42.42): 56 data bytes
64 bytes from 192.168.42.42: icmp_seq=0 ttl=255 time=0.482 ms
rena.subdomain.domain.cxm ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.244/0.363/0.482 ms

# valerie.subdomain.domain.cxm
PING valerie.subdomain.domain.cxm (192.168.42.43): 56 data bytes
64 bytes from 192.168.42.43: icmp_seq=0 ttl=255 time=0.471 ms
valerie.subdomain.domain.cxm ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.234/0.352/0.471 ms

Once the DNS server on sylvia can resolve its hostnames to IP addresses, it's time to delegate from numark.

# Delegate from numark to sylvia for the Subdomain

Add the following two lines to numark's /var/named/named.domain.cxm under all other NS statements (to prevent default names):

```
subdomain           IN      NS              sylvia.subdomain.domain.cxm.
sylvia.subdomain    IN      A               192.168.42.40
```

These lines say that sylvia.subdomain.domain.cxm is the nameserver for domain subdomain.domain.cxm.. (Remember that without a period it is the same as subdomain.domain.cxm..) Since sylvia.subdomain.domain.cxm. has been mentioned, it must be locally resolved to an IP address. Hence the second line.