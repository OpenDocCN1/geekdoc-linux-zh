# ## PINGING

The quickest way to determine if a host is alive is to ping it. The `ping` command, used for this purpose, sends out an ICMP echo request, causing the target to respond with an ICMP reply packet. Note that a host can be configured not to respond to ICMP echo requests. Therefore, even though a host does not respond to echo requests, it may still be alive.

# ### Pinging Hosts Using the ping Utility

Using the `ping` command will find alive hosts that respond to ICMP echo requests with ICMP echo replies:

```
```bash
[admin]$ ping 192.168.1.1
PING 192.168.1.1 (192.168.1.1) from 192.168.1.1 : 56 (84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.093 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.078 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.076 ms
64 bytes from 192.168.1.1: icmp_seq=4 ttl=64 time=0.062 ms
^C
--- 192.168.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% loss, time 299ms
rtt min/avg/max/mdev = 0.062/0.077/0.093/0.012 ms
```
```

# ## PING SWEEPING

Ping sweeping is the process of pinging numerous hosts. In the case of a large set of target IP addresses, one must perform a ping sweep to determine alive hosts that respond to ICMP echo requests.

# ### Using nmap to Perform Ping Sweeps

Using the `-sP` option in nmap will perform a ping sweep:

```
```bash
[admin]$ nmap -sP 192.168.1.*

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Host (192.168.1.1) appears to be up.
Host (192.168.1.100) appears to be up.
Host (192.168.1.150) appears to be up.

Nmap run completed -- 256 IP addresses (3 hosts up) scanned in 33 seconds
```
```