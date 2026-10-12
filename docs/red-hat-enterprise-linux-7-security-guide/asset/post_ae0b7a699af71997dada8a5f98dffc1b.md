
http://www.unbound.net/

This document contains general information about the unbound DNS service.

http://www.nlnetlabs.nl/projects/dnssec-trigger/

This document contains general information about dnssec-trigger.

## 4.6. SECURING VIRTUAL PRIVATE NETWORKS (VPNS) USING LIBRESWAN

In Red Hat Enterprise Linux 7, a Virtual Private Network (VPN) can be configured using the IPsec protocol which is supported by the Libreswan application. Libreswan is a continuation of the Openswan application and many examples from the Openswan documentation are interchangeable with Libreswan. The NetworkManager IPsec plug-in is called NetworkManager-libreswan. Users of GNOME Shell should install the NetworkManager-libreswan-gnome package, which has NetworkManager-libreswan as a dependency. Note that the NetworkManager-libreswan-gnome package is only available from the Optional channel. See Enabling Supplementary and Optional Repositories.

The IPsec protocol for VPN is itself configured using the Internet Key Exchange(IKE) protocol. The terms IPsec and IKE are used interchangeably. An IPsec VPN is also called an IKE VPN, IKEv2 VPN, XAUTH VPN, Cisco VPN or IKE/IPsec VPN. A variant of an IPsec VPN that also uses the Level 2 Tunneling Protocol (L2TP) is usually called an L2TP/IPsec VPN, which requires the Optional channel x12tpd application.

Libreswan is an open-source, user-space IKE implementation available in Red Hat Enterprise Linux 7. IKE version 1 and 2 are implemented as a user-level daemon. The IKE protocol itself is also encrypted. The IPsec protocol is implemented by the Linux kernel and Libreswan configures the kernel to add and remove VPN tunnel configurations.

The IKE protocol uses UDP port 500 and 4500. The IPsec protocol consists of two different protocols, Encapsulated Security Payload(ESP) which has protocol number 50, and Authenticated Header (AH) which as protocol number 51. The AH protocol is not recommended for use. Users of AH are recommended to migrate to ESP with null encryption.

The IPsec protocol has two different modes of operation, Tunnel Mode (the default) and Transport Mode. It is possible to configure the kernel with IPsec without IKE. This is called Manual Keying. It is possible to configure manual keying using the ip xfrm commands, however, this is strongly discouraged for security reasons. Libreswan interfaces with the Linux kernel using netlink. Packet encryption and decryption happen in the Linux kernel.

Libreswan uses the Network Security Services (NSS) cryptographic library. Both libreswan and NSS are certified for use with the Federal Information Processing Standard (FIPS) Publication 140-2.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_83_0.png)

IMPORTANT

IKE/IPsec VPNs, implemented by Libreswan and the Linux kernel, is the only VPN technology recommended for use in Red Hat Enterprise Linux 7. Do not use any other VPN technology without understanding the risks of doing so.

### 4.6.1. Installing Libreswan

To install Libreswan, enter the following command as root:

```
~/# yum install libreswan
```

**To check that Libreswan is installed:**

```
~/# yum info libreswan
```

After a new installation of **Libreswan**, the NSS database should be initialized as part of the installation process. Before you start a new database, remove the old database as follows:

```
~/# systemctl stop ipsec
~/# rm /etc/ipsec.d/*db
```

Then, to initialize a new NSS database, enter the following command as **root**:

```
~/# ipsec initnss
Initializing NSS database
```

Only when operating in FIPS mode, it is necessary to protect the NSS database with a password. To initialize the database for FIPS mode, instead of the previous command, use:

```
~/# certutil -N -d sql:/etc/ipsec.d
Enter a password which will be used to encrypt your keys.
The password should be at least 8 characters long,
and should contain at least one non-alphabetic character.

Enter new password:
Re-enter password:
```

To start the **ipsec** daemon provided by **Libreswan**, issue the following command as **root**:

```
~/# systemctl start ipsec
```

To confirm that the daemon is now running:

```
~/# systemctl status ipsec
* ipsec.service - Internet Key Exchange (IKE) Protocol Daemon for IPsec
  Loaded: loaded (/usr/lib/systemd/system/ipsec.service; disabled; vendor preset: disabled)
  Active: active (running) since Sun 2018-03-18 18:44:43 EDT; 3s ago
    Docs: man:ipsec(8)
          man:pluto(8)
          man:ipsec.conf(5)
  Process: 20358 ExecStopPost=/usr/sbin/ipsec --stopnlog (code=exited, status=0/SUCCESS)
  Process: 20355 ExecStopPost=/sbin/ip xfrm state flush (code=exited, status=0/SUCCESS)
  Process: 20352 ExecStopPost=/sbin/ip xfrm policy flush (code=exited, status=0/SUCCESS)
  Process: 20347 ExecStop=/usr/libexec/ipsec/whack --shutdown (code=exited, status=0/SUCCESS)
  Process: 20634 ExecStartPre=/usr/sbin/ipsec --checkknflog (code=exited, status=0/SUCCESS)
  Process: 20631 ExecStartPre=/usr/sbin/ipsec --checknss (code=exited, status=0/SUCCESS)
  Process: 20369 ExecStartPre=/usr/libexec/ipsec/_stackmanager start (code=exited, status=0/SUCCESS)
  Process: 20366 ExecStartPre=/usr/libexec/ipsec/addconn --config
/etc/ipsec.conf --checkconfig (code=exited, status=0/SUCCESS)
Main PID: 20646 (pluto)
Status: "Startup completed."
CGroup: /system.slice/ipsec.service
└20646 /usr/libexec/ipsec/pluto --leak-detective --config
/etc/ipsec.conf --nofork
```

To ensure that **Libreswan** will start when the system starts, issue the following command as `root`:

```
~]# systemctl enable ipsec
```

Configure any intermediate as well as host-based firewalls to permit the **ipsec** service. See **Chapter 5, Using Firewalls** for information on firewalls and allowing specific services to pass through. **Libreswan** requires the firewall to allow the following packets:

- **UDP** port 500 and 4500 for the **Internet Key Exchange** (IKE) protocol
- **Protocol 50** for **Encapsulated Security Payload** (ESP) **IPsec** packets
- **Protocol 51** for **Authenticated Header** (AH) **IPsec** packets (uncommon)

We present three examples of using **Libreswan** to set up an **IPsec** VPN. The first example is for connecting two hosts together so that they may communicate securely. The second example is connecting two sites together to form one network. The third example is supporting remote users, known as *road warriors* in this context.

### 4.6.2. Creating VPN Configurations Using Libreswan

**Libreswan** does not use the terms “source” and “destination” or “server” and “client” since **IKE/IPsec** are peer to peer protocols. Instead, it uses the terms “left” and “right” to refer to end points (the hosts). This also allows the same configuration to be used on both end points in most cases, although a lot of administrators choose to always use “left” for the local host and “right” for the remote host.

There are four commonly used methods for authentication of endpoints:

- **Pre-Shared Keys** (PSK) is the simplest authentication method. PSKs should consist of random characters and have a length of at least 20 characters. In **FIPS** mode, PSKs need to comply to a minimum strength requirement depending on the integrity algorithm used. It is recommended not to use PSKs shorter than 64 random characters.
- **Raw RSA** keys are commonly used for static host-to-host or subnet-to-subnet **IPsec** configurations. The hosts are manually configured with each other's public RSA key. This method does not scale well when dozens or more hosts all need to setup **IPsec** tunnels to each other.
- **X.509** certificates are commonly used for large-scale deployments where there are many hosts that need to connect to a common **IPsec** gateway. A central *certificate authority* (CA) is used to sign RSA certificates for hosts or users. This central CA is responsible for relaying trust, including the revocations of individual hosts or users.
- **NULL** Authentication is used to gain mesh encryption without authentication. It protects
