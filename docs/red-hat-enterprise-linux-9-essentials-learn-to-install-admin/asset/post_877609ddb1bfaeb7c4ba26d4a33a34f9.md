
## RHEL 9 Firewall Configuration with firewalld

```
success
```

To verify that a service has been added permanently, be sure to include the --permanent flag when requesting the service list:

```
# firewall-cmd --zone=public --permanent --list-services
```

```
cockpit dhcpv6-client http https ssh
```

Note that as a permanent change, this new rule will not take effect until the system restarts or firewalld reloads:

```
# firewall-cmd --reload
```

Remove a service from a zone using the --remove-service option. Since this is a runtime change, the rule will be re-instated the next time the system restarts:

```
# firewall-cmd --zone=public --remove-service=https
```

To remove a service permanently, use the --permanent flag, remembering to reload firewalld if the change is required to take immediate effect:

```
# firewall-cmd --zone=public --permanent --remove-service=https
```

### 14.3.4 Working with Port-based Rules

To enable a specific port, use the --add-port option. Note that when manually defining the port, both the port number and protocol (TCP or UDP) will need to be provided:

```
# firewall-cmd --zone=public --permanent --add-port=5000/tcp
```

It is also possible to specify a range of ports when adding a rule to a zone:

```
# firewall-cmd --zone=public --permanent --add-port=5900-5999/udp
```

### 14.3.5 Creating a New Zone

An entirely new zone may be created by running the following command. Once created, the zone may be managed in the same way as any of the pre-defined zones:

```
# firewall-cmd --permanent --new-zone=myoffice
```

```
success
```

After adding a new zone, firewalld will need to be restarted before the zone becomes available:

```
# firewall-cmd --reload
```

```
success
```

### 14.3.6 Changing Zone/Interface Assignments

As previously discussed, each interface on the system must be assigned to a zone. The zone to which an interface is assigned can also be changed using the firewall-cmd tool. In the following example, the eth0 interface is assigned to the public zone:

```
# firewall-cmd --zone=public --change-interface=eth0
```

```
success
```

### 14.3.7 Masquerading

Masquerading is better known in networking administration circles as Network Address Translation (NAT). When using a RHEL 9 system as a gateway to the internet for a network of computers, masquerading allows all of the internal systems to use the IP address of that RHEL 9 system when communicating over the internet. This has the advantage of hiding the internal IP addresses of any systems from malicious external entities and also avoids the necessity to allocate a public IP address to every computer on the network.

Use the following command to check whether masquerading is already enabled on the firewall:

```
# firewall-cmd --zone=external --query-masquerade
```

Use the following command to enable masquerading (remembering to use the --permanent flag if the change is to be permanent):

```
# firewall-cmd --zone=external --add-masquerade
```

### 14.3.8 Adding ICMP Rules

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

### 14.3.9 Implementing Port Forwarding

Port forwarding is used in conjunction with masquerading when the RHEL 9 system is acting as a gateway to the internet for an internal network of computer systems. Port forwarding allows traffic arriving at the firewall via the internet on a specific port to be forwarded to a particular system on the internal network. This is perhaps best described by way of an example.

Suppose that a RHEL 9 system is acting as the firewall for an internal network of computers, and one of the systems on the network is configured as a web server. Let’s assume the web server system has an IP address of 192.168.2.20. The domain record for the website hosted on this system is configured with the public IP address behind which the RHEL 9 firewall system sits. When an HTTP web page request arrives on port 80 the RHEL 9 system acting as the firewall needs to know what to do with it. By configuring port forwarding, it is possible to direct all web traffic to the internal system hosting the web server (in this case, IP address 192.168.2.20), either continuing to use port 80, or diverting the traffic to a different port on the destination server. In fact, port forwarding can even be configured to forward the traffic to a different port on the same system as the firewall (a concept known as local forwarding).

To use port forwarding, begin by enabling masquerading as follows (in this case, the assumption is made that the interface connected to the internet has been assigned to the external zone):

```
# firewall-cmd --zone=external --add-masquerade
```

To forward from a port to a different local port, a command similar to the following would be used:

```
# firewall-cmd --zone=external --add-forward-port=port=22:proto=tcp:toport=2750
```

In the above example, any TCP traffic on port 22 will be forwarded to port 2750 on the local system. The following command, on the other hand, forwards port 20 on the local system to port 22 on the system with the IP address 192.168.0.19:

```
# firewall-cmd --zone=external \
    --add-forward-port=port=20:proto=tcp:toport=22:toaddr=192.168.0.19
```

Similarly, the following command forwards local port 20 to port 2750 on the system with IP address 192.168.0.18:

```
# firewall-cmd --zone=external --add-forward-port=port=20:proto=tcp:toport=2750:toaddr=192.168.0.18
```

### 14.4 Managing firewalld from the Cockpit Interface

So far, this chapter has provided an overview of firewalld and explored using the firewall-cmd command-line tool to manage firewall zones and interfaces. While firewall-cmd provides the most flexible way to manage the firewalld configuration, it is also possible to view and manage the services for the default zone within the Cockpit web console.

To access the firewalld settings, sign into the Cockpit interface and select Networking from the navigation panel. On the networking page, locate the Firewall section as shown in Figure 14-1 below and click on the Edit rules and zones button:

![](img/be1f159c3cc937d7b264dc5b134856dc_126_0.png)

Figure 14-1

The Firewall page displays the current service rules configured for the default zone (and allows services to be removed), new services to be added to the zone, and for the firewall to be turned on and off:

Networking > Firewall

### Firewall

Incoming requests are blocked by default. Outgoing requests are not blocked.

![](img/be1f159c3cc937d7b264dc5b134856dc_127_0.png)

Figure 14-2

### 14.5 Managing firewalld using firewall-config

If you have access to the graphical desktop environment, the firewall may also be configured using the firewall-config tool. Though not installed by default, firewall-config may be installed as follows:

```
# dnf install firewall-config
```

When launched, the main firewall-config screen appears as illustrated in Figure 14-3:

![](img/be1f159c3cc937d7b264dc5b134856dc_127_1.png)

Figure 14-3
