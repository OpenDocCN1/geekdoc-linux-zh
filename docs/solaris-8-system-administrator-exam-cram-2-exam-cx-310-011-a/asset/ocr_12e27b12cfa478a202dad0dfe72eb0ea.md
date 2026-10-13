| Table 13.3. The ping Command-line Arguments |  |
|---|---|
| **Argument** | **Description** |
| `-i interface` | Uses the specified interface address |
| `-I interval` | Specifies an interval between transmissions (default of 1 second) |
| `-n` | Displays addresses instead of hostnames |
| `-r` | Bypasses the routing tables (remote host is on the local network) |
| `-R` | Records the route in the IP header |
| `-s` | Sends ICMP packets until interrupted |
| `-t time` | Specifies a time to live (in seconds) for IP packets |
| `-v` | Displays detailed information (verbose mode) |

At a minimum, a hostname or an IP address must be specified. All command-line arguments are specified before the hostname or IP address. When you use the **ping** command without any command-line arguments (specifying only a hostname), you can specify a timeout after the hostname. The default timeout is 20 seconds, which is appropriate in most cases.

When you use **ping** with the **-s** command-line argument, you can specify a packet size and a count after the hostname. The following example uses the **ping** command to send five packets (each with 60 bytes of data) to the sparc20 host:

```
```sh
$ /usr/sbin/ping -s sparc20 60 5
PING sparc20 60 data bytes
68 bytes from sparc20 (192.168.99.208): icmp_seq=0. time=1. ms
68 bytes from sparc20 (192.168.99.208): icmp_seq=1. time=0. ms
68 bytes from sparc20 (192.168.99.208): icmp_seq=2. time=0. ms
68 bytes from sparc20 (192.168.99.208): icmp_seq=3. time=0. ms
68 bytes from sparc20 (192.168.99.208): icmp_seq=4. time=0. ms

---sparc20 PING Statistics---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip (ms)  min/avg/max = 0/0/1
$
```
```

# The Spray Command

The **/usr/sbin/spray** command sends a stream of User Datagram Protocol (UDP) packets to a host by using the Remote Procedure Call (RPC) mechanism. On the remote end, the spray daemon, **sprayd(1M)**, accepts these packets and acknowledges receiving them. The **spray** command, along with the **sprayd** program, verifies the connectivity between two hosts and the proper operation of the network interfaces and protocol stacks (of both hosts) up to the Application layer.