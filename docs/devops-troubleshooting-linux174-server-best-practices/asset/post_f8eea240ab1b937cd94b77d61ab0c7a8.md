
The following would be used on Red Hat-based systems:

```bash
$ sudo service network restart
```

On a side note, it’s amazing that these distributions have to differ even on something this fundamental.

Once you have identified the gateway, use the ping command to confirm that you can communicate with the gateway:

```bash
$ ping -c 5 10.1.1.1
PING 10.1.1.1 (10.1.1.1) 56(84) bytes of data.
64 bytes from 10.1.1.1: icmp_seq=1 ttl=64 time=3.13 ms
64 bytes from 10.1.1.1: icmp_seq=2 ttl=64 time=1.43 ms
64 bytes from 10.1.1.1: icmp_seq=3 ttl=64 time=1.79 ms
64 bytes from 10.1.1.1: icmp_seq=4 ttl=64 time=1.50 ms
64 bytes from 10.1.1.1: icmp_seq=5 ttl=64 time=1.50 ms
--- 10.1.1.1 ping statistics ---
5 packets transmitted, 4 received, 20% packet loss, time 4020ms
rtt min/avg/max/mdev = 1.436/1.966/3.132/0.686 ms
```

As you can see, we were able to successfully ping the gateway, which means that we can at least communicate with the 10.1.1.0 network. If you couldn’t ping the gateway, it could mean a few things. It could mean that your gateway is blocking ICMP packets. If so, tell your network administrator that blocking ICMP is an annoying practice with negligible security benefits and then try to ping another Linux host on the same subnet. If ICMP isn’t being blocked, then it’s possible that the switch port on your host is set to the wrong VLAN, so you will need to further inspect the switch to which it is connected.

## Is DNS Working?

Once you have confirmed that you can speak to the gateway, the next thing to test is whether DNS functions. Both the `nslookup` and `dig` tools can be used to troubleshoot DNS issues, but since you need to perform only basic testing at this point, just use `nslookup` to see if you can resolve web1 into an IP:

```bash
$ nslookup web1
Server:    10.1.1.3
Address:   10.1.1.33

Name: web1.example.net
Address: 10.1.2.5
```

In this example DNS is working. The web1 host expands into web1.example.net and resolves to the address 10.1.2.5. Of course, make sure that this IP matches the IP that web1 is supposed to have! In this case, DNS works, so we can move on to the next section; however, there are also a number of ways DNS could fail.

### No Name Server Configured or Inaccessible Name Server

If you see the following error, it could mean either that you have no name servers configured for your host or they are inaccessible:

```bash
$ nslookup web1
;; connection timed out; no servers could be reached
```

In either case you will need to inspect `/etc/resolv.conf` and see if any name servers are configured there. If you don't see any IP addresses configured there, you will need to add a name server to the file. Otherwise, if you see something like the following, you need to start troubleshooting your connection with your name server, starting off with ping:

```bash
search example.net
nameserver 10.1.1.3
```

If you can't ping the name server and its IP address is in the same subnet (in this case, 10.1.1.3 is within the subnet), the name server itself could be completely down. If you can't ping the name server and its IP address is in a different subnet, then skip ahead to the *Can I Route to the Remote Host?* section, but only apply those troubleshooting steps to the name server's IP. If you can ping the name server but it isn't responding, skip ahead to the *Is the Remote Port Open?* section.

### Missing Search Path or Name Server Problem

It is also possible that you will get the following error for your `nslookup` command:

```bash
$ nslookup web1
Server: 10.1.1.3
Address: 10.1.1.53
** server can't find web1: NXDOMAIN
```

Here you see that the server did respond, since it gave a response: *server can’t find web1*. This could mean two different things. One, it could mean that web1’s domain name is not in your DNS search path. This is set in `/etc/resolv.conf` in the line that begins with `search`. A good way to test this is to perform the same `nslookup` command, only use the fully qualified domain name (in this case, web1.example.net). If it does resolve, then either always use the fully qualified domain name, or if you want to be able to use just the hostname, add the domain name to the search path in `/etc/resolv.conf`.

If even the fully qualified domain name doesn’t resolve, then the problem is on the name server. The complete method for troubleshooting all DNS issues is covered in Chapter 6, but here are some basic pointers. If the name server is supposed to have that record, then that zone’s configuration needs to be examined. If it is a recursive name server, then you will have to test whether or not recursion is working on the name server by looking up some other domain. If you can look up other domains, then you must check if the problem is on the remote name server that does contain the zones.

## Can I Route to the Remote Host?

After you have ruled out DNS issues and see that web1 is resolved into its IP 10.1.2.5, you must test whether you can route to the remote host. Assuming ICMP is enabled on your network, one quick test might be to ping web1. If you can ping the host, you know your packets are being routed there and you can move to the next section, *Is the Remote Port Open?*. If you can’t ping web1, try to identify another host on that network and see if you can ping it. If you can, then it’s possible web1 is down or blocking your requests, so move to the next section. If you can’t ping any hosts on the remote network, packets aren’t being routed correctly. One of the best tools to test routing issues is `traceroute`. Once you provide `traceroute` with a host, it will test each hop between you and the host. For example, a successful `traceroute` between dev1 and web1 would look like this:

```bash
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  web1 (10.1.2.5)  8.039 ms  8.348 ms  8.643 ms
```

Here you can see that packets go from dev1 to its gateway (10.1.1.1), and then the next hop is web1. This means it’s likely that 10.1.1.1 is the gateway for both subnets. On your network you might see a slightly different output if there are more routers between you and your host. If you can’t ping web1, your output would look more like the following:

```bash
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  * * *
 3  * * *
```

Once you start seeing asterisks in your output, you know that the problem is on your gateway. You will need to go to that router and investigate why it can’t route packets between the two networks. Instead you might see something more like

```bash
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 1  10.1.1.1 (10.1.1.1) 3006.477 ms !H 3006.779 ms !H 3007.072 ms
```

In this case, you know that the ping timed out at the gateway, so the host is likely down or inaccessible even from the same subnet. At this point, if you haven’t tried to access web1 from a machine on the same subnet as web1, try pings and other tests now.

> If you have one of those annoying networks that block ICMP, don’t worry. you can still troubleshoot routing issues. You just need to install the `tcptraceroute` package (`sudo apt-get install tcptraceroute`), then run the same commands as for `traceroute`, only substitute `tcptraceroute` for `traceroute`.

## Is the Remote Port Open?

So you can route to the machine but you still can’t access the web server on port 80. The next test is to see whether the port is even open. There are a number of different ways to do this. For one, you could try `telnet`:

```bash
$ telnet 10.1.2.5 80
Trying 10.1.2.5 ...
telnet: Unable to connect to remote host: Connection refused
```

If you see `Connection refused`, then either the port is down (likely Apache isn’t running on the remote host or isn’t listening on that port) or the firewall is blocking your access. If `telnet` can connect, then, well, you don’t have a networking problem at all. If the web service isn’t working the way you suspected, you need to investigate your Apache configuration on web1. Troubleshooting web server issues is covered in Chapter 8.

Instead of `telnet`, I prefer to use `nmap` to test ports because it can often detect firewalls. If `nmap` isn’t installed, use your package manager to install the `nmap` package. To test web1, type the following:

```bash
$ nmap -p 80 10.1.2.5
Starting Nmap 4.62 ( http://nmap.org ) at 2009-02-05 18:49 PST
Interesting ports on web1 (10.1.2.5):
PORT STATE SERVICE
80/tcp filtered http
```

Aha! `nmap` is smart enough that it can often tell the difference between a closed port that is truly closed and a closed port behind a firewall. Normally when a port is actually down, `nmap` will report it as closed. Here it reported it as filtered. What this tells us is that some firewall is in the way and is dropping the packets to the floor. This means you need to investigate any firewall rules on the gateway (10.1.1.1) and on web1 itself to see if port 80 is being blocked.

## Test the Remote Host Locally

At this point, we have either been able to narrow the problem down to a network issue or we believe the problem is on the host itself. If we think
