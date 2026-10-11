![](bbox=[0.13, 0.04, 0.28, 0.09])

> *Nmap is limited as it falls back to crafting packets by using the standard Berkeley socket API.* 198

Let's explore some port scanning examples to get a better feel for Nmap and its options.

# 7.2.2.1 Accountability for Our Traffic

A default Nmap TCP scan will scan the 1000 most popular ports on a given machine. Before we start running scans blindly, let’s examine the amount of traffic sent by this type of scan. We'll scan one of the lab machines while monitoring the amount of traffic sent to the target host using **iptables**.199

We will use several **iptables** options. First, we will use the `-I` option to insert a new rule into a given chain, which in this case includes both the **INPUT** (Inbound) and **OUTPUT** (Outbound) chains followed by the rule number. We will use `-s` to specify a source IP address, `-d` to specify a destination IP address, and `-j` to **ACCEPT** the traffic. Lastly, we will use the `-Z` option to zero the packet and byte counters in all chains.

Let's run those commands now:

```
kali@kali:~$ sudo iptables -I INPUT 1 -s 10.11.1.220 -j ACCEPT
kali@kali:~$ sudo iptables -I OUTPUT 1 -d 10.11.1.220 -j ACCEPT
kali@kali:~$ sudo iptables -Z
Listing 229 - Configuring our iptables rules for the scan
```

Now let's generate some traffic using **nmap**.

```
kali@kali:~$ nmap 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:20 EST
Nmap scan report for 10.11.1.220
Host is up (0.29s latency).
Not shown: 989 closed ports
PORT STATE SERVICE
21/tcp open ftp
53/tcp open domain
88/tcp open kerberos-sec
135/tcp open msrpc
139/tcp open netbios-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open kpasswd5
593/tcp open http-rpc-epmap
636/tcp open ldapssl
3268/tcp open globalcatLDAP
3269/tcp open globalcatLDAPSsl
3389/tcp open ms-wbt-server
```