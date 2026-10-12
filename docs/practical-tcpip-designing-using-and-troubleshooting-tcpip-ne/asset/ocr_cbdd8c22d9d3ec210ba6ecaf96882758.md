# 23.8 Implementation (1)

**A. Draw a sketch-map of your planned network**

Draw your network as you expect to implement it and add the IP numbers you expect to allocate. (See Appendix 9 for an example.)

**B. Allocate your IP addresses for testing**

By now you know the range of IP addresses (“LAN-IP-range”), and the netmask (“LAN-netmask”) you’ll be using on your LAN – either the static range your ISP allocated, or the NAT range you will configure on your router for in step C below.

| | |
|---|---|
| **LAN-IP-range** | . . . . |
| **LAN-netmask** | . . . . |
| **LAN-default gateway = IP address of router’s internal interface** | . . . . |

**C. Configure your router’s NAT settings if it’s performing NAT**

(This applies only if you have what we called connection type 2 in the previous module – no static IP addresses at all. If you will be using NAT but have static IP addresses, skip this step, because you use non-NATed addresses for the first phase of testing.)

You want to tell your router the range of IP numbers that you’ll be using on your private (internal) network. These are specified by the LAN-IP-range and LAN-netmask in step B above.

Most routers nowadays have a Web interface, and we’ve found that configuring NAT isn’t a big deal. With a modern device with a good user interface, it might take you less than half an hour, including finding and reading the relevant documentation. (With a bad user interface and bad documentation it could take you days.)