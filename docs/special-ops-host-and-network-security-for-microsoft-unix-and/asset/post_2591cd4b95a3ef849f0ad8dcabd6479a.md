
DJBDNS is broken up into many daemons. This separation is the key to DJBDNS security. Every action is isolated and stripped down to its bare essentials, and then the code is hardened. DJBDNS consists of three major components:

- dnscache Resolver only
- tynydns Authoritative only
- axfrns Zone transfers only (zone transfers are recommended via rsync over encrypted tunnels. Due to this, we do not cover axfrns here.)

## dnscache Installation

Complete the steps to install the dnscache component of DJBDNS:

- 1. Create two users. For this example, dnscache and dnslog. They should look something like this:
```
dnscache:x:501:501:/home/dnscache:/bin/bash
dnslog:x:502:502:/home/dnslog:/bin/bash
```

- 2. Now edit /etc/passwd manually and change the login shell to something invalid. The step is very important.
```
dnscache:x:501:501:/home/dnscache:/sbin/nolog
dnslog:x:502:502:/home/dnslog:/sbin/nolog
```

- 3. Run the configuration manager dnscache-conf, and replace w.x.y.z with the interface you use DJBDNS to listen on.
```
dnscache-conf dnscache dnslog /etc/dnscache w.x.y.z
```

- 4. Add a symbolic link to the services directory. After this step, dnscache will start on its own. Verify that dnscache has started and is listening on the correct IP address.
```
ln -s /etc/dnscache /service

ps -aux |grep dns

dnscache 26096 0.0 0.5 2620 1312 ? S 07:40 0:00
/usr/local/bin/dnscache
dnslog 26097 0.0 0.1 1324 256 ? S 07:40 0:00
multilog
```

```
t ./main
netstat -lp
```
Active Internet connections (only servers) Foreign Address

| State Proto Recv-Q Send-Q Local Address PID/Program name Address |
|---|---|---|---|---|---|---|---|
| tcp 0 0 10.0.32.163:domain | *: | LISTEN | 26096/dnscache | | |
| udp 0 0 10.0.32.163:domain | *: | 26096/dnscache | | |

- 5. You have a local DNS resolver server running. To grant additional hosts resolver access, add their IPs. For example, to add 1.2.3/24, you would add a blank classfull descriptive file (1.2.3) in the approved ip resolver directory (restart of dnscache is unnecessary thanks to daemon-tools):
```
touch /etc/dnscache/root/ip/1.2.3
```

## TinyDNS Configuration

Configuration of TinyDNS can be done manually or through the configuration maker:

- 1. Run the configuration maker. Replace z.y.x.w with the appropriate IP address. Note that dnscache and TinyDNS cannot run on the same IP:
```
tinydns-conf tinydns dnslog /etc/tinydns 1.2.3.5
```
- 2. Just like dnscache, make a symbolic link to the service directory so daemontools can initiate TinyDNS:
```
ln -s /etc/tinydns /service
```
- 3. After starting TinyDNS, you need to add zone configurations:
```
vim /etc/tinydns/root/data
```
- 4. This file will include all zones. Insert the domains that will be hosted on this server. The syntax is very different from that of BIND or others. The dot (.) symbol is a nameserver record:
```
.example.com::ns1.example.com
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_467_0.png)

## Attacking and Defending DNS

The "at" (@) symbol is a mailserver record:
```
@example.com::smtp.example.com
```
The equal (=) symbol is an IP record:
```
=test.example.com:192.168.0.1
```
The (+) symbol is a forward record:
```
+www.example.com:192.168.0.1
```
After editing the data file, go to /etc/tinydns/root and make. This compiles the data cdb file that TinyDNS reads. According to Bernstein, after correctly installing dnscache, you will have a secure resolver and authoritative server and can add your configurations.

## Security Checklist

A preproduction checklist is a common requirement in many environments. Using a checklist to double-check details might shed light on missed configurations. The following is a general checklist for all daemons and operating systems. Customization for your environment is recommended.

NOTE: A real world example of preproduction checklist is RFC 2870: Name Server Operational Requirements which is the checklist that root servers must meet before going live.

## Hardware Capable of Stable Environment

- Ensure that the system has only one designated purpose.
- Verify that the system has sufficient processor/RAM.
- Debate the use of redundant storage.
- Allot a cold or standby system for emergencies.
- Schedule data backup and rotation.
- Ensure stable network connectivity if necessary.

## Harden the OS

- Verify that all current patches are installed.
- Remove or turn off unnecessary system services.
- Restrict system access to necessary persons only.
- Document users who have access to the machine.
- Increase log sizes to meet projected needs.
- Enable the use of Network Time Protocol (NTP) server.
- Implement an appropriate Layer 2–3 network security plan.
- Maintain system communication only through out of band (OOB) management ports.

## Securely Install Daemons

- Verify software MD5 checksums.
- Harden the environment; possibly implementing chroot.
- Verify that daemon accounts do not have login access.
- Make sure a failure notification procedure is in place.
- Verify that all current patches are good.
- Subscribe to newsgroup/mailing list to be notified of updates or risks.

## Configure DNS Daemons

- Check that all excess features are removed.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_469_0.png)

- Implement daemon ACLs.
- Restrict or turn off zone transfers.
- If zone transfers are needed, verify that they are running over encrypted protocols.
- Modify daemon version response.
- Verify valid-mail contacts are used in records.

## Logging

- Check that log sizes are manageable.
- Verify procedures regarding log errors.
- Monitor logs on a regular basis, and keep historical records of lookup failures.

## Monitor Data

- Maintain a baseline statistic.
- Identify and understand projected future requirements.
- Verify the allotted budget for growth.

## Summary

This chapter covered many DNS environments, some internal, others with services open to every attacker. As mentioned, very simple steps can decrease the chances of a security breach. DNS is the simplest application covered in this book—however, despite the fact that DNS exploitation is relatively low, if exploited, every system in your establishment would be at risk. With a heavy dependency on DNS, specific steps should always be taken to keep your systems protected. Constant log monitoring and limited exposure will reduce the system administration headache associated with day-to-day production. Keep up to date on current events via mailing lists and/or newsgroups. Using the correct application for each situation helps future expansion plans. Although many suggested security techniques rely on security through obscurity, they do aid in monitoring potential attackers who are profiling your systems. Emphasis on solitary purpose machines and redundancy to administer DNS is recommended, especially in a high-volume environment.

## Links to Sites

- microsoft.com Microsoft DNS updates and information
- http://www.to/djbdns.html Homepage of DJBDNS
- www.isc.org Internet Software Consortium; maintainer of BIND
- http://f.root-servers.org Root Server F Statistics Web site
- http://nanog.merit.net North American Network Operations Group; Core Internet Conference and mailing list.
- www.acmebw.com/askrdns DNS Resources Directory; Mr. DNS

## Mailing Lists

- ISP-Technical DNS mailing list (isp-lists.isp-planet.com/isp-dns) Moderate traffic list, unofficially the best place for DNS solutions.
- Common DNS Newsgroup (comp.protocols.dns.bind) Moderate traffic newsgroup; general help

![](img/729efc56f204a2ebffb8295c3a2dfdfb_471_0.png)
