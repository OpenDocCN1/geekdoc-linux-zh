# Chapter 7 Networking

| Table 7.6 Most of the options available in /etc/dhcpd.conf (continued). | |
| Option | Purpose | Value |
| subnet-mask | The client’s subnet mask. | IP address. |
| tcp-keepalive-interval | How often to send messages that keep a TCP connection alive. | Number of seconds to wait before sending. 0 means not to do this by default. |
| time-servers | The time servers this client has access to. | A comma-separated list of IP addresses. |
| www-server | The Web servers this client has access to. | A comma-separated list of IP addresses. |

When it comes to declarations, these look a little odd when given in a general format:

```
```
declaration {
   parameter1
   parameter2
   ...
   parametern
   declaration1
   declaration2
   ...
   declarationn
}
```
```

As you can see, often you end up with declarations inside other declarations when building your dhcpd.conf file. The declarations available are listed in Table 7.7.

| Table 7.7 Declarations available in /etc/dhcpd.conf. | |
| Declaration | Purpose | Subdeclaration Issues |
| group | Used to apply identical parameters to a series of declarations. | Cannot include range. |
| host | Used to apply parameters to a specific host, denoted by its MAC. | None. |
| range | Defines the range of addresses in the subnet in question. | No subdeclarations allowed. |
| shared-network | Specifies which subnets share the same networking cables. | Must declare subnets inside this statement. |
| subnet | Identification information and settings for a particular subnet. | None. |