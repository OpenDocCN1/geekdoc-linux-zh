# Chapter 21: Network Configuration and Security

# FIGURE 21-15

Allowing inbound/outbound SSH connections through your firewall

![](bbox=[0.029, 0.166, 0.483, 0.287])

# FIGURE 21-16

Rules for allowing inbound SSH connections

![](bbox=[0.029, 0.394, 0.293, 0.646])

The rules shown at the bottom of the gufw rules dialog refer to the ports associated with various services, which is not very user-friendly. If you aren't sure about the service that a rule is associated with, you can use the grep command to look up the port that it uses in the file /etc/services. For example, the following output shows how to look for the services associated with port 22 in this file:

```
$ grep -w 22 /etc/services
ssh 22/tcp # SSH Remote Login Protocol
ssh 22/udp
```

The other tabs in gufw utility rule dialog make it easy to define other types of rules. The Preconfigured tab provides a drop-down menu with number of default rules that you can use to enable (or disable) external access to various programs and services. To create a rule