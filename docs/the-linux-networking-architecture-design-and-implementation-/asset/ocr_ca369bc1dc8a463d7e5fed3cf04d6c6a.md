# 18.3 Traffic Control in the Outgoing Direction 367

![](bbox=[0.146, 0.076, 0.853, 0.477])

FIGURE 18-1
Traffic control in the Linux kernel.

# 18.2 BASIC STRUCTURE OF TRAFFIC CONTROL IN LINUX

18-1 shows where traffic control is arranged in the Linux kernel. Traffic control in the incoming direction is handled by the functions from the file net/sch/sch_ingress.c before incoming packets are passed to higher protocol layers or forwarded over other network cards within the kernel.

The largest part of traffic control in Linux occurs in outgoing direction. Here, we can use and interlink different elements for policing and traffic shaping.

# 18.3 TRAFFIC CONTROL IN THE OUTGOING DIRECTION

The traffic-control framework defines three basic elements:

Queuing discipline: Each network device is allocated to a queuing discipline. In general, packets to be sent are passed to a queuing discipline within this queue by specific rules. During a search for packets ready to be sent, these packets can be removed no earlier than the queuing discipline has marked them as ready for transmission. The algorithm used within a queuing discipline remains invisible to the outside. Examples for queuing disciplines include simple FIFO buffers