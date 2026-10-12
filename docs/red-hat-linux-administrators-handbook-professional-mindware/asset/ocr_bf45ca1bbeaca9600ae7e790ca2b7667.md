# Chapter 7

# Network Administration

# Classifying IP Networks

IP numbers are used to identify network interfaces on host computers. These numbers are not randomly assigned. Each IP number carries two types of information in it. You can think of an IP address as follows:

```
IP = {Network Address} + {Interface address of the host computer}
```

For example, 192.168.2.10 is an IP address in the 192.168.2.0 network, and the interface address, which is often called the host address, is .10. In other words, this IP address points to the network interface .10 in the 192.168.2.0 network. Which part of the IP address is used to identify the network depends on the class of the network. Notice that when you are writing a network address, the interface identifier bytes are written as zeros. The 32-bit IP address covers a range from 0.0.0.0 to 255.255.255.255 (2^32) addresses. They are classified (with exceptions) as follows.

# Class A networks

Any IP address that ranges from 0.0.0.0 to 127.255.255.255 is a class A IP network. Figure 7-1 shows the possible range of IP addresses in this class.