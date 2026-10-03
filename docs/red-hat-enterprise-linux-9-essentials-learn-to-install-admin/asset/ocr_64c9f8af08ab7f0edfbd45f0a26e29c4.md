computers, masquerading allows all of the internal systems to use the IP address of that RHEL 9 system when communicating over the internet. This has the advantage of hiding the internal IP addresses of any systems from malicious external entities and also avoids the necessity to allocate a public IP address to every computer on the network.

Use the following command to check whether masquerading is already enabled on the firewall:

```
# firewall-cmd --zone=external --query-masquerade
```

Use the following command to enable masquerading (remembering to use the --permanent flag if the change is to be permanent):

```
# firewall-cmd --zone=external --add-masquerade
```

# 14.3.8 Adding ICMP Rules

The Internet Control Message Protocol (ICMP) is used by client systems on networks to send information, such as error messages, to each other. It is also the foundation of the ping command, which is used by network administrators and users alike to detect whether a particular client is alive on a network. The ICMP category allows for the blocking of specific ICMP message types. For example, an administrator might choose to block incoming ping (Echo Request) ICMP messages to prevent the possibility of a ping-based denial of service (DoS) attack (where a server is maliciously bombarded with so many ping messages that it becomes unable to respond to legitimate requests).

To view the ICMP types available for inclusion in firewalld rules, run the following command:

```
# firewall-cmd --get-icmptypes
```

```
address-unreachable bad-header beyond-scope communication-prohibited destination-unreachable echo-reply ...
```

The following command, for example, permanently adds a rule to block echo-reply (ping request) messages for the public zone:

```
# firewall-cmd --zone=public --permanent --add-icmp-block=echo-reply
```

# 14.3.9 Implementing Port Forwarding

Port forwarding is used in conjunction with masquerading when the RHEL 9 system is acting as a gateway to the internet for an internal network of computer systems. Port forwarding allows traffic arriving at the firewall via the internet on a specific port to be forwarded to a particular system on the internal network. This is perhaps best described by way of an example.

Suppose that a RHEL 9 system is acting as the firewall for an internal network of computers, and one of the systems on the network is configured as a web server. Let’s assume the web server system has an IP address of 192.168.2.20. The domain record for the website hosted on this system is configured with the public IP address behind which the RHEL 9 firewall system sits. When an HTTP web page request arrives on port 80 the RHEL 9 system acting as the firewall needs to know what to do with it. By configuring port forwarding, it is possible to direct all web traffic to the internal system hosting the web server (in this case, IP address 192.168.2.20), either continuing to use port 80, or diverting the traffic to a different port on the destination server. In fact, port