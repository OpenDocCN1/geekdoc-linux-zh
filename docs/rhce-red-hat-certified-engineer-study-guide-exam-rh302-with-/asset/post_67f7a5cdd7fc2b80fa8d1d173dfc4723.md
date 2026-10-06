
5. Which of the following presents a secure environment for management of network information?

- A. LDAP with SSL
- B. NIS
- C. NIS+
- D. SSL

6. What is the name of the RPM package that should be installed to implement LDAP?

- A. 1ldap
- B. 1dapis
- C. 1dapssl
- D. openldap

# Answers to Review Questions

- 1. C. The files /etc/inetd.conf, /etc/hosts.allow, and /etc/hosts.den configure TCP wrappers.
- 2. C, D. UDP services should generally receive the wait option in addition to the udp protocol option.
- 3. C. The FTP service is known to inetd as in.ftpd. The LOCAL keyword specifies access to the local host.
- 4. A, B, C. The portmap service should not be specified with a host name that requires DNS resolution.
- 5. A, C. NIS is not a highly secure service. SSL does not provide management of network information, though it can be used with LDAP to do so.
- 6. D. The openldap package contains support for LDAP.

## Chapter 23

## Understanding Secondary Network Services

RHCE PREPARATION TOPICS COVERED IN THIS CHAPTER:

- Be familiar with secondary network services supported under Red Hat Linux, such as DHCP, IPX, lpd, Internet news, squid, and time synchronization.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_577_0.png)

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_578_0.png)

In addition to the primary network services covered in Chapter 21, Red Hat Linux supports many additional services. This chapter explains several of the most important and commonly used secondary network services. The Red Hat, Inc. study points for the Red Hat Certified Engineer exam require only conceptual familiarity with these secondary network services. This chapter, therefore, focuses on basic concepts related to secondary network services; however, it also includes practical hints to help you install, configure, and use the services.

## Dynamic Host Configuration Protocol (DHCP)

A Dynamic Host Configuration Protocol (DHCP) server can help manage your IP address space. The Red Hat Linux DHCP server is compatible with the BOOTP protocol still used in Unix shops. DHCP is particularly helpful if your network includes computers that are intermittently connected or that move from location to location, such as laptops.

When a host running a DHCP client boots, it contacts a DHCP server. The DHCP server can assign such host-related information as the following:

- IP address
- Host and domain names
- Network IP address
- Broadcast IP address
- Default gateway IP address
- DNS server IP address
- WINS server IP address

## Dynamic Host Configuration Protocol (DHCP) 567

A DHCP server can be configured to provide static or dynamic information, or both. A static configuration provides a client with a fixed IP address based on the Media Access Control (MAC) address assigned to the client's network interface and the subnet address of the client's point of network connection. Thus, the combination of host identity and location determine the assigned configuration.

A dynamic configuration arbitrarily assigns IP addresses from one or more ranges. This conserves IP addresses, because only hosts that are active have an associated IP address. However, the IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

## Installing DHCP

The DHCP server is contained in the dhcp package. To install DHCP, move to the directory containing the package and issue the command

```bash
rpm -Uvh dhcp-.rpm
```

DHCP requires the associated network interface to support and be configured for broadcast and multicast operation. To determine if a network interface is properly configured, issue the command

```bash
ifconfig -a
```

The output pertaining to a typical network interface should resemble the following:

```
eth1 Link encap:Ethernet HWaddr 00:AO:CC:25:8A:EC
inet addr:192.168.1.1 Bcast:192.168.1.255
Mask:255.255.255.0
UP BROADCAST RUNNING PROMIS MULTICAST MTU:1500
Metric:1
RX packets:4648466 errors:0 dropped:0 overflows:0
frame:0
TX packets:679303 errors:0 dropped:0 overflows:0
carrier:0
collisions:33062 txqueuelen:100
Interrupt:11 Base address:0x6000
```

Copyright©2000 SYBEX, Inc., Alameda, CA www.syex.com

## Chapter 23 • Understanding Secondary Network Services

Note the keywords BROADCAST and MULTICAST, which will appear in the third line of the output. If these keywords are not present, DHCP will not operate correctly. To resolve the problem, you may need to do any or all of the following:

- Reconfigure the interface by using the ifconfig command.
- Replace the network interface with a card that supports MULTICAST.

## Configuring DHCP

The DHCP configuration file is /etc/dhcpd. Here’s a typical configuration, which includes both dynamic and static information:

```bash
default-lease-time 64800;
max-lease-time 64800;

option subnet-mask 255.255.255.0;
option broadcast-address 192.168.1.255;
option routers 192.168.1.1;
option domain-name-servers 192.168.1.1;
option domain-name "azusapacific.com";
```

```bash
subnet 192.168.1.0 netmask 255.255.255.0 {

  server-identifier 192.168.1.1;

  host sara {
    hardware ethernet 00:50:04:d2:d3:15;
    fixed-address 192.168.1.33;
    default-lease-time 64800;
  }
}
```

The combination of host identity and location determine the assigned configuration.

Leases are assigned for a finite time, specified in /etc/dhcpd, which they must be renewed by the client. Before starting the DHCP server, you must create the /var/state/dhcp.leases file.

```bash
subnet 192.168.1.0 netmask 255.255.255.0 {

  server-identifier 192.168.1.1;

  host sara {
    hardware ethernet 00:50:04:d2:d3:15;
    fixed-address 192.168.1.33;
    default-lease-time 64800;
  }

  range 192.168.1.20 192.168.1.100;
}
```

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

To start the DHCP server, issue the command

```bash
/etc/rc.d/init.d/dhcp start
```

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

To stop the DHCP server, issue the command

```bash
/etc/rc.d/init.d/dhcp stop
```

To restart the DHCP server, issue the command

```bash
/etc/rc.d/init.d/dhcp restart
```

To check the status of the DHCP server, issue the command

```bash
/etc/rc.d/init.d/dhcp status
```

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.

The IP address associated with a host may be different each time the host boots. A DHCP configuration can be both dynamic and static, providing designated hosts with a static configuration and other hosts with a dynamic configuration.
