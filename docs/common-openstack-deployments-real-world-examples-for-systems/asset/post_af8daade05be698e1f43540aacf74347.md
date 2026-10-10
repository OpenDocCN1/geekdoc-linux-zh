
available can help you further track down exactly what the service was doing before and after the problem started.

Moving beyond tracebacks and debug lines, you may also be able to use an error message you received from an OpenStack service to start the search through your logs. Services like Nova may run several daemons on a node. Using `grep -i "error message" /var/log/nova/*.log` may narrow down not only where in a log file to look, but **which** log you need to look at.

## Tip

Doing a lot of debugging? Logs can get very very big, which can make them difficult to search and work with. Use logrotate to rotate out logs that are older than what you're looking at, or manually make backups of older logs so you can focus on smaller log snippets and share them with your team.

Beyond this, I like to think of debugging OpenStack through log files as more of an art than a science. As you start exploring the log files, you will have to think about what behavior you're seeing and which service and server is responsible for it. Are you debugging a problem with launching a node? You may want to start on the compute node and look in /var/log/nova/nova-compute.log to see what the compute node itself is telling you. In most cases, the errors in this log will lead you to the real problem—perhaps it's with networking? You'll then need to determine whether it's a problem with the networking service (Neutron) server, which handles API requests and processes them on the control node, or with a specific agent or plug-in. Perhaps Open vSwitch is causing a problem, in which case you'll want to view the logs for the openvswitch-agent on the compute node. Perhaps your problem is actually with the dhcp-agent running on the controller node. There are logs for that, too.

Being able to identify behavior and pinpoint the exact source of your problem often takes experience. Certain behavior and types of error messages will, over time, assist with your troubleshooting technique, and you'll find yourself improving over time.

## Key Services

When you browse an OpenStack deployment environment, you may notice that there are three components that almost every other component relies on:

- Identity (Keystone)
- Queueing service (typically RabbitMQ)
- Networking (Neutron)

Misconfiguration or incorrect configuration assumptions in these services can cause problems for everything else. A service that can't reach the messaging queue will fail to be able to send along API requests. This is a very common problem and can be found in log files by searching for failures to connect to the AMQP server.

## Tip

RabbitMQ has a GUI that runs on port 15672. Access can be gathered from the credentials you set up in the Puppet Hiera configuration. If you find yourself struggling with the queuing service it’s worth looking into usage, but it’s beyond scope here.

An identity service that does not have an authentication account for a service will not be able to verify the service has the correct rights to perform certain actions. A misconfigured network can cause services not to be able to reach each other at all, which we’ll talk about in the “Networking” section.

It is incredibly common for a troubleshooting scenario to include several of these key services. Even though your problem may seem to be with compute, be sure to browse log files for these other services to make sure you’re not encountering a broader problem.

## Networking

Due to the complexity and importance, we made a decision to create an entire chapter devoted to networking early in the book. As explained in Chapter 3, “Networking,” the environment you have for OpenStack and your use case will heavily influence the decisions you make with regard to your networking configuration. A fundamental understanding of how OpenStack tackles networking, in addition to advice and guidance from your own network administration staff, is incredibly helpful for having a successful deployment.

With that in mind, our first word of advice is to refer back to that chapter and the series of diagrams provided in order to make sure you understand how everything should be configured. Once you understand that, you will be able to more intelligently debug.

Once you get to the step of debugging, there are a few tools that are particularly helpful, which we’ll give examples of here in order to get you started.

## Network Debugging Tools

Many of these tools we’ll cover will be familiar to Linux professionals and we won’t do a full tutorial of them, there are plenty of guides on-line and in print. Instead, we’ll focus on how they can be used with and are particularly valuable in an OpenStack environment.

### ip and Network Name Spaces

The ip command should be familiar to Linux professionals. It replaced a series of tools, including ifconfig, route and even some uses of netstat, for configuring, manipulating and viewing the networks on your system. At the simplest, you may run ip addr to see what addresses are directly assigned to your interfaces or ip -d link to see more specifics about the device configuration. The -d flag tells you roughly what kind of device each interface is, which can be very valuable when tracing your way through the network configuration.

Things get more complicated when you begin looking at tenant networking, which our deployments have. For the tenant network (our default is the 10.190.0.0/24 network), you will not see the IP addresses or devices by simply using the ip command on your controller node. Instead, these networks live in network name spaces that need to be accessed with the ip netns command. For example, in order to see the network where the DHCP server runs you’ll need to use:

```
$ sudo ip netns
grouter-1c1c7574-9116-438f-aa33-1eb9694f8f5a
gdhcp-961c7aa2-4c7b-452f-bc65-6b7cb2b9798a
```

The name space ID for the DHCP server begins with gdhcp-. In order to run commands in this name space to view details about and manipulate that network, you will use the exec command with the name space ID and the command you wish to run. The following runs ip addr on the qdhcp network name space:

```
$ sudo ip netns exec gdhcp-961c7aa2-4c7b-452f-bc65-6b7cb2b9798a ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
13: tap4c049b01-c0- <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1400 qdisc noqueue state UNKNOWN group default
link/ether fa:16:3e:83:01:c6 brd ff:ff:ff:ff:ff:ff
inet 10.190.0.5/24 brd 10.190.0.255 scope global tap4c049b01-c0
valid_lft forever preferred_lft forever
inet6 fe80::f816:3e83:1c6/64 scope link
valid_lft forever preferred_lft forever
```

As you learned in the networking chapter, the tap interface here is what has the address for your DHCP server. A test you can use to see if a new instance can effectively ping may be to ping this address from your instance, or to confirm you can ping the gateway for this network.

```
$ sudo ip netns exec gdhcp-961c7aa2-4c7b-452f-bc65-6b7cb2b9798a ping -c 2 10.190.0.1
PING 10.190.0.1 (10.190.0.1) 56(84) bytes of data.
64 bytes from 10.190.0.1: icmp_seq=1 ttl=64 time=0.322 ms
64 bytes from 10.190.0.1: icmp_seq=2 ttl=64 time=0.054 ms

--- 10.190.0.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 0.054/0.188/0.322/0.134 ms
```

As you can see, various commands can be run using this network, and so it’s very valuable for testing connectivity on these network name spaces that may seem invisible otherwise.

You may have noticed there is also a name space ID that begins with grouter-. This name space is used to provide routing at Network Address Translation (NAT) between the private instance tenant network and the external provider network. Go ahead and run similar exec commands on that interface and refer back to the networking chapter to learn more about what is happening.
