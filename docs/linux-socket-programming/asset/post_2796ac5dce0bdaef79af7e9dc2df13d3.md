
### Broadcasting Messages to a Domain

The first form of distribution messaging, broadcasting [RFC919, RFC922], uses the nature of subnets and network masks to determine the destination. A broadcast is a mandatory messaging distribution form; both the subnet and the hosts have to receive the message. (In reality, if a host has not enabled broadcasting, the hardware does not accept the message. Still, the message does occupy bandwidth, and every host can read it.)

### Revisiting IP Structure

The subnet is very important to sending and receiving broadcast messages. As described in *Chapter 2, “TCP/IP Network Language Fluency,”* when you define an interface with `ifconfig`, you also define a broadcast address and a netmask. The broadcast address is a special address to which the host listens to get messages.

The subnet is typically the same as the netmask and broadcast address. For example, if you have about 250 hosts in your `198.2.56.xxx` subnet, your netmask and broadcast would be `255.255.255.0` and `198.2.56.255`. So, if you want to send a message to everyone in your subnet, you would use the `198.2.56.255` address. (As noted in *Chapter 2*, you can get very creative with the netmasks—just remember that the last significant bit is the end of the mask.)

The subnet is really a wrapper of the hardware implementation. The real work takes place in the lower levels of the hardware and the kernel. To understand what is happening, you need to start with the physical connection.

Beyond the physical connection, sending a broadcast message is easier than receiving one. To send any message, you only need the IP address (as described in *Chapter 2*, the network actually converts that address to the destination’s Ethernet MAC address). To get a message, the interface card has to be listening for the matching MAC address. The problem is that broadcast messages cannot assume a different MAC address from that of the host. In fact, as noted in *Chapter 2*, no two hosts in the same subnet are likely to have similar MAC addresses. So broadcasting cannot depend on any specialized MAC to conduct broadcast messages.

Instead, when a program sends a broadcast message, the kernel automatically assigns a MAC address of all ones (`FF:FF:FF:FF:FF:FF`). This MAC is a flag to all NICs to pick it up—even if no program is listening for a broadcast message.

The NIC opens the gates and lets the message fill its internal buffers. When complete, it notifies the kernel with an interrupt. The kernel retrieves the packet and looks at the destination IP. If the address matches the broadcast address, it passes the packet up to the network subsystem’s queues.

The network subsystem (typically UDP) inspects the message and, if it finds a broadcast socket with a matching port number, it moves the packet into the socket’s I/O channel. If not, it drops the packet. You may want to specify a port number to tell the kernel to filter out unwanted messages for you. Otherwise, you can cause a storm of unwanted replies.

### Programming to Enable Broadcasting

You can enable broadcasting using the `SO_BROADCAST` socket option. The rest of the program looks like a normal datagram-messaging program.

```c
/*****
***** Create a broadcast datagram socket  *****
/*****
const int on=1;
sd = socket(PF_INET, SOCK_DGRAM, 0);
if ( setsockopt(sd, SOL_SOCKET, SO_BROADCAST, &on, sizeof(on)) != 0 )
      panic("set broadcast failed");
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(port);
addr.sin_addr.s_addr = INADDR_ANY;
if ( bind(sd, &addr, sizeof(addr)) != 0 )
      panic("bind failed");
addr.sin_port = htons(atoi(strings[2]));
if ( inet_aton(strings[1], &addr.sin_addr) == 0 )
      panic("inet_aton failed (%s)", strings[1]);
```

After enabling broadcast, you can send messages to the broadcast address. You may want to create a process or thread for the receiver and the sender. Unlike other transmissions where you can expect a single reply for a single transmission, broadcasting can yield many replies for each message sent. If you do this, be sure to turn off the incoming queue on one of the channels.

```c
/*****
***** Split the responsibilities into sender and listener *****
***** Close the sender's listening channel. ***
/*****
if ( fork() )
      Receiver(sd);
else
{
     shutdown(sd, SHUT_RD);     /* close the input channel */
     Sender(sd);
}
wait(0);
```

# Broadcasting Limitations

Broadcast messages have a few problems. While you may be able to reach many computers at once with a single message, you can only reach those within your subnet. Still, you can increase your range of influence by changing your broadcast address. Unfortunately, you cannot use broadcasting on the WAN because the address `255.255.255.255` is no longer legal on the Internet. (You may even find that most routers do not allow broadcast messages to pass through at all. So, even if you have the right broadcast address, say `198.2.255.255`, the router at `198.2.1.0` may ignore the packet.)

Additionally, everyone on the subnet hears your message. Because of the way the hardware implements broadcasting, all network cards pick up broadcast messages. This can place a lot of unnecessary burden on the hosts that don't want the message.

Another problem is the protocol. IPv4 only supports broadcasting on datagrams (TCP is excluded). If you want reliability and streaming, you must implement your own. Datagrams serve well in many circumstances and, with a little beefing up, you can provide a good interface to which clients can connect.

# Multicasting Messages to a Group

Multicasting [RFC1112] answers some of the problems with broadcasting. The primary idea of broadcasting is sending a message to everyone within an address range. Multicasting uses agreed-upon addresses that hosts can join to listen for messages.

Multicasting uses a single IP address to send messages to several recipients. It has the following advantages over broadcasting:

- **All Protocols**—It supports datagram and streaming protocols (UDP and TCP). Datagrams support multicasting right now, but streams have no immediate implementations. You can find free (not Open Source) implementations of reliably delivered multcasts.
- **WAN Accessible**—You can join global multicasting groups. However, at the time of this writing, there are sections of the WAN that do not support or pass multicast messages.
- **Limited Listeners**—A multicast message does not *necessarily* force all NICs to pick it up (see the "How the Network Provides Multicasting" section later in this chapter).
- **IPv6 Support**—IPv6 dropped support for broadcasting, but it has adopted and extended multicasting.

> NOTE

# Turning On Multicasting Support

Most distributions include kernels that have multicasting turned on. (You can look in `/proc/net/dev_mcast` to check your currently running kernel.) However, multicast routing may not be enabled, or if you are using a downloaded kernel, you might not have the option set. If you want to use multicasting or you manage a router for others who want to use multicasting, you may need to reconfigure and recompile the kernel. The configurations are in the Networking part of the configuration.

# Joining Multicast Groups

Using multicasting is as simple as joining a list service. Like a list service, you get as many messages as others send, so it’s easy to overrun a constricted network connection. If you join a group, be careful that you have the bandwidth to support the data flow. Most likely, you may drop packets and make the connection less than useful.

Broadcast addresses follow a specific pattern so that the routers can recognize them. These addresses come directly from the IP allocation (first introduced in Chapter 2). The range is 224.0.0.0–239.255.255.255. These addresses are reserved for broadcasting. This range of addresses is subdivided into smaller ranges to indicate the *address scope* or how far the message can go before a router blocks it. Table 17.1 shows these divisions.

Table 17.1 Multicasting Address Allocation and Scope

| Scope | Typical TTL | Address Range |
| :--- | :--- | :--- |
| Cluster | 0 | 224.0.0.0–224.0.0.255 |
| Site | < 32 | 239.255.0.0–239.255.255.255 |
| Organization | < 128 | 239.192.0.0–239.195.255.255 |
| Global | <= 255 | 224.0.1.0–238.255.255.255 |
