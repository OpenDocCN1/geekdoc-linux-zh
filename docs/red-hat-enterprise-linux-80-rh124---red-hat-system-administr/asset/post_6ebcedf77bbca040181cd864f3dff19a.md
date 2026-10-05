
new /var/log/auth-errors file. Use the authpriv facility and the alert priority in the configuration file.

- 4.1. Create the /etc/rsyslog.d/auth-errors.conf file to specify the new /var/log-auth-errors as the destination for messages related to authentication and security issues. You may use the sudo vim /etc/rsyslog.d/auth-errors.conf command to create the configuration file.

authpriv.alert /var/log/auth-errors

- 4.2. Restart the rsyslog service so that the changes in the configuration file take effect.

```
[student@server] $ sudo systemctl restart rsyslog
```

- 4.3. Use the logger command to write a new message to the /var/log/auth-errors file. Apply the -p authpriv.alert option with the logger command to generate a log message relevant to authentication and security issues.

```
[student@server] $ logger -p authpriv.alert "Logging test authpriv.alert"
```

- 4.4. Use the tail command to confirm that the /var/log/auth-errors file is populated with the log entry containing Logging test authpriv.alert message.

```
[student@server] $ sudo tail /var/log/auth-errors
Feb 19 11:56:07 server student [6038]: Logging test authpriv.alert
```

- 4.5. Log out of server.

```
[student@server] $ exit
logout
Connection to server closed.
[student@workstation~]$
```

# Evaluation

On workstation, run the lab log-review grade command to confirm success of this exercise.

```
[student@workstation~]$ lab log-review grade
```

# Finish

On workstation, run lab log-review finish to complete this lab. This script ensures the original time zone is restored along with all the original time settings on server.

```
[student@workstation~]$ lab log-review finish
```

This concludes the guided exercise.

# SUMMARY

In this chapter, you learned:

- The systemd-journald and rsyslog services capture and write log messages to the appropriate files.
- The /var/log directory contains log files.
- Periodic rotation of log files prevent them from filling up the file system space.
- The systemd journals are temporary and do not persist after reboot.
- The chronyd service helps to synchronize time settings with a time source.
- The time zone of the server can be updated based on its location.

# CHAPTER 12

# MANAGING NETWORKING

# GOAL

Configure network interfaces and settings on Red Hat Enterprise Linux servers.

# OBJECTIVES

- Describe fundamental concepts of network addressing and routing for a server.
- Test and inspect current network configuration with command-line utilities.
- Manage network settings and devices using nmcli.
- Modify network settings by editing configuration files.
- Configure a server's static host name and its name resolution, and test the results.

# SECTIONS

- Describing Networking Concepts (and Quiz)
- Validating Network Configuration (and Guided Exercise)
- Configuring Networking from the Command Line (and Guided Exercise)
- Editing Network Configuration Files (and Guided Exercise)
- Configuring Host Names and Name Resolution (and Guided Exercise)

# LAB

Managing Networking

![](img/59afb92e10b67a9cecc358a2c65e93b5_408_0.png)

# DESCRIBING NETWORKING CONCEPTS

# OBJECTIVES

After completing this section, you should be able to describe fundamental concepts of networking addressing and routing for a server.

# TCP/IP NETWORK MODEL

The TCP/IP network model is a simplified, four-layered set of abstractions that describes how different protocols interoperate in order for computers to send traffic from one machine to another over the Internet. It is specified by RFC 1122, Requirements for Internet Hosts -- Communication Layers. The layers are:

- Application

Each application has specifications for communication so that clients and servers may communicate across platforms. Common protocols include SSH (remote login), HTTPS (secure web), NFS or CIFS (file sharing), and SMTP (electronic mail delivery).

- Transport

Transport protocols are TCP and UDP. TCP is a reliable connection-oriented communication, while UDP is a connectionless datagram protocol. Application protocols use TCP or UDP ports. A list of well-known and registered ports can be found in the /etc/services file.

When a packet is sent on the network, the combination of the service port and IP addresses forms a socket. Each packet has a source socket and a destination socket. This information can be used when monitoring and filtering.

- Internet

The Internet, or network layer, carries data from the source host to the destination host. The IPv4 and IPv6 protocols are Internet layer protocols. Each host has an IP address and a prefix used to determine network addresses. Routers are used to connect networks.

- Link

The link, media access layer, provides the connection to physical media. The most common types of networks are wired Ethernet (802.3) and wireless WLAN (802.11). Each physical device has a hardware address (MAC) which is used to identify the destination of the packets on the network segment.

# DESCRIBING NETWORK INTERFACE NAMES

Each network port on a system has a name you use to configure and identify.

Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify. Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify. Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify. Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify.

# MANAGING NETWORK

Each network port on a system has a name you use to configure and identify.

 Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify. Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify. Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify. Older versions of Red Hat Enterprise used names like eth0. New versions of Red Hat Enterprise use names like ens3. Each network port on a system has a name you use to configure and identify.

# IPV4 NETWORKING

IPv4 is the primary network protocol used on the Internet. You should have at least a basic understanding of IPv4 networking in order to manage network communication for your servers.

# IPv4 Addresses

An IPv4 address is a 32-bit number, normally expressed in decimal as four 8-bit octets ranging in value from 0 to 255, the address is divided into two parts: the network part and the host part. All hosts on the same subnet can talk to each other directly without a router, have the same network part; the network part identifies the subnet. No hosts on the same subnet can have the same host part; the host part identifies a particular host on the subnet.

In modern networking, the size of an IPv4 address is variable. To know which of IPv4 address is the network part and which is the host, an administrator must know the netmask, which is assigned to the subnet. The netmask indicates how many bits of the IPv4 address are used. The more subnets available for the host, the more hosts are on the subnet.

The lowest possible address on a subnet (host part is all zeros in binary) is sometimes called the network address. The highest possible address on a subnet (host part is all ones in binary) is for broadcast messages in IPv4, and is called the hostcast address.

Network masks are expressed in two forms. The older syntax for a netmask uses 24 bits for the network part and reads 255.255.255.0. A newer syntax, CIDR notation, specifies a network prefix of /24. Both forms convey the same information; namely, how many leading bits in the IP address count to its network address.
