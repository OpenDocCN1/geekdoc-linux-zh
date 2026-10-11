In the previous chapter, you examined the configuration of a network interface and the usage of network utilities to interact with network services on the network. In this chapter, you examine the configuration of common network services, routing, and firewalls. Following this, you examine local and network security concepts, good security practices, and the utilities that you can use to secure your Linux computer and detect intruders.

# Network Services

Recall from Chapter 1, “Introduction to Linux,” that Linux provides a wide variety of services that are available to users across a network. Before you are able to organize the appropriate network services to meet your organization’s needs, you must first identify the types and features of network services. Following this, you can configure these network services as required, as well as configure additional network-related services, such as routing and firewalls.

# Identifying Network Services

Network services are processes that run on your computer and provide some type of valuable service for client computers on the network. They are often represented by a series of daemon processes that listen for certain requests on the network. Daemons identify to which packets they should respond by listening only for packets that have a certain number. This number is called a port and uniquely identifies a particular service. A port number is like an apartment number for the delivery of mail. The network ID of the IP address ensures that the packet is delivered to the correct street (network); the host ID ensures that the packet is delivered to the correct building (host); and the transport layer protocol and port number ensure that the packet is delivered to the proper apartment (service).

Ports and their associated protocol are defined in the /etc/services file. To see to which port the telnet daemon listens, you can use the following command:

```
```
[root@server1 root]# grep telnet /etc/services
    telnet          23/tcp
    telnet          23/udp
    rttelnet      107/tcp             # Remote Telnet
    rttelnet      107/udp
    telnets        992/tcp
    telnets        992/udp
[root@server1 root]# _
```
```

The preceding output indicates that the telnet daemon listens on port 23 using both TCP/IP and UDP/IP.