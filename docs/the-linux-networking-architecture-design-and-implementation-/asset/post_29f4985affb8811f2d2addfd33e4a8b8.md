
## 21.1 Introduction 413

![](img/5a25b942ec3329b8799f2b5f0de564f6_436_0.png)

(normally, when a session flow is established from the internal network towards the external network). In addition, you can translate either the source address (source NAT) or the destination address (destination NAT) of a session flow, but never both addresses at the same time.

- **Basic NAT**: This NAT variant is used to map internal IP address to one or external IP addresses. To understand it better, let's assume that there is a (dynamic) allocation between the end system A (internal address 192.168.1.1) and a global address from the address space reserved for NAT (e.g., 199.10.42.1) in the sample network of Figure 21–1). Let's further assume that a WWW browser establishes a TCP connection from its port 1200 to port 80 in the WWW server 100.1.1.1. The NAT router binds the internal address 192.168.1.1 to the global address 199.10.42.1 for this session flow. However, this binding is valid for this single session flow only, and a new binding (to the same address) has to be done for each additional, secondary session flow.
- **Network Address and Port Translation** (NAPT): This NAT variant represents an extension of Basic NAT, NAPT can translate IP addresses and additionally TCP or UDP ports. It is used to map various session flows from different internal end systems to one global IP address. If only one single global address is available, then this corresponds to the “masquerading” of Linux 2.2.) It means that, in our example, we could establish a TCP connection from port 1200 of end system B to the same port 80 of the same server by translating port number 1200 (e.g., 1201) in addition to the IP address. In this case, we would obtain the following bindings:

```
192.168.1.1:1200 → 199.10.42.1:1200
192.168.1.2:1200 → 199.10.42.1:1201
```

Notice that, for mapping of source port numbers, port numbers from the privileged range (ports 1-1023) are mapped to the privileged range. For transforming the destination address, the ports should not be changed at all.

FIGURE 21–1
Example of a network using NAT.

## 414 Chapter 21 Network Address Translation (NAT)

Bidirectional NAT and Twice NAT: These two NAT variants are listed here for the sake of completeness. In contrast to traditional NAT, bidirectional NAT lets you bind addresses during the establishment of session flows in both directions. NAT NAT removes the limitation of traditional NAT that we can either the destination address or only the source address, but never both.

### 21.1.7 Problems

One general problem in address translation is application-layer protocols, whereas applications exchange address information. One good example is the File Transfer Protocol (FTP—see [Stev94a]). If an FTP client accesses an FTP server, then TCP first establishes a control connection to exchange FTP commands, such as GET or PUT. Now, if it wants to obtain data from the server, the client uses the PORT command to send an IP address and a port number. The client opens this passively (see Chapter 27) and waits for the data connection, which is established by the server to the address it obtained earlier, to transmit payload.

The problems arising in the above case are similar to those known from packets (see Section 19.1.2). One major problem is, if there is a NAT router somewhere between the client and the server, this router maps the client's IP address translation to another address, whereas the client sends its internal address in the NAT command, and this is invalid from the server's view. To ensure that the PORT command can operate correctly, the NAT router must also translate the address transported in the PORT command; it must be able to intervene in the FTP protocol on the application layer.

Another major problem occurs in NAPT and relates to IP packet fragmentation. When packets are fragmented, only the first fragment contains the transport-protocol header with the port numbers of the source and the destination; but NAT relies on this the other fragments of the same packet cannot be handled properly. Consequently, we must ensure that fragmented packets are reassembled before an attempt is made to translate addresses.

## 21.2 CONFIGURING NAT IN LINUX

The iptable_nat module implements the unidirectional NAPT variant described in Section 21.1.6. Like the Twice NAT variant, it can change the source and destination addresses of a session flow simultaneously.

To intercept and process packets, NAT uses the infrastructure supplied by the netfilter architecture (see Section 19.3.1). Figure 21–2 shows that it hooks the netfilter hooks NF_IP_PRE_ROUTING, NF_IP_POST_ROUTING, and NF_IP_LOCAL_OUT for purpose. The NAT module is invoked as a packet traverses the appropriate hook, and a pointer to the sk_buff structure is passed. Together with the packet, the NF_IP_POST_ROUTING hook works while the destination address is being translated in one of the other hooks (see Figure 21–2).

The first preliminary versions of the new netfilter architecture allowed the

## 438
## 21.2 Configuring NAT 45

![](img/5a25b942ec3329b8799f2b5f0de564f6_438_0.png)
FIGURE 21–2
Netfilter hooks used by the NAT module.functionality was fully integrated in iptables. More recently, this

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

The first preliminary versions of the new netfilter architecture allowed the

## 439
## 21.3 IMPLEMENTING THE NAT MODULE

This section introduces important data structures to manage session flows, allocations, and Subsequently, it will explain the functions to establish and tear down address bindings, to actually translate addresses, and to handle ICMP errors.

### 21.3.1 Important Data Structures

All session flows are completely managed by connection-tracking module described in Chapter 20. A structure of the type ip_conrack is stored for each session flow. (See Section 20.2.) This structure includes two data structures of the type ip_conrack_hash, representing the forward and reverse directions. If a session flow is translated by the NAT module, then the ip_conrack_hash structure for the reverse direction is adapted so that reply packets can be allocated properly.

In the example described in Section 21.1, where the internal address 192.168.1.1 is translated into the global address 199.10.42.1, a connection from port 1200 to port 80 in the WWW server 100.1.1.1 would be represented by the following:

```
Forward: 192.168.1.1:1200 -> 100.1.1.1:80
Reverse: 100.1.1.1:80 -> 199.10.42.1:1200
```

The connection-tracking module stores a pointer to the relevant data structure of the type ip_conrack in the sk_buff of each packet. If the NAT module needs to allocate an IP packet to a session flow, it invokes its ip_conrack_get() function, which returns the matching ip_conrack structure.

```
struct ip_expect
{
	...
};
```

The NAT module has an ordered list, nat_expect_list, with data structures of the type ip_expect to enable protocol-specific NAT modules (e.g. for FTP—see Section 21.1.7) to decide when a new session flow was expected, so that it requires special handling. Each of these structures consists essentially of a pointer to a function that actually makes that decision:

```
struct ip_expect
{
	struct list_head head;
	/* Returns 1 (and sets verdict) if has setup NAT for this
	connection (*expect)(struct sk_buff **pskb,
		usigned int hookname,
		struct ip_conrack *ct,
		struct ip_nat_info *info,
		struct ip_conrack *master,
		struct ip_nat_info *masterinfo,
		usigned int *verdict);
};
```
