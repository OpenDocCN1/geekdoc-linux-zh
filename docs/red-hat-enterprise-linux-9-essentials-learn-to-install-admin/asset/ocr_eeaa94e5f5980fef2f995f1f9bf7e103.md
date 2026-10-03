# Configuring a RHEL 9 Postfix Email Server

you are feeling adventurous and want to configure a more sophisticated email system.

The format of myhostname is host.domain.extension. If, for example, your Linux system is named MyLinuxHost and your internet domain is MyDomain.com you would set the myhostname option as follows:

```
myhostname = mylinuxhost.mydomain.com
```

The mydomain setting is just the domain part of the above setting. For example:

```
mydomain = mydomain.com
```

The myorigin setting defines the name of the domain from which the output email appears to come from when it arrives in the recipient’s inbox and should be set to your domain name:

```
myorigin = $mydomain
```

One of the most crucial parameters, mydestination relates to incoming messages and declares the domains for which this server is the final delivery destination. Any incoming email messages addressed to a domain name, not on this list will be considered a relay request which, subject to the mynetworks setting (outlined below), will typically result in a delivery failure.

The inet_interfaces setting defines the network interfaces on the system via which postfix is permitted to receive email and is generally set to all:

```
inet_interfaces = all
```

The mynetworks setting defines which external systems are trusted to use the server as an SMTP relay. Possible values for this setting are as follows:

+   - **host** - Only the local system is trusted. Attempts by all external clients to use the server as a relay will be rejected.
- **subnet** - Only systems on the same network subnet can use the server as a relay. If, for example, the server has an IP address of 192.168.1.29, a client system with an IP address of 192.168.1.30 could use the server as a relay.
- **class** - Any systems within the same IP address class (A, B, and C) may use the server as a relay.

Trusted IP addresses may be defined manually by specifying subnets, address ranges, or referencing pattern files. The following example declares the local host and the subnet 192.168.0.0 as trusted IP addresses:

```
mynetworks = 192.168.0.0/24, 127.0.0.0/8
```

For this example, set the property to subnet so that any other systems on the same local network as the server can send email via SMTP relay. In contrast, external systems are prevented from doing so:

```
mynetworks = subnet
```