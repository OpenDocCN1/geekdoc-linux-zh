# 4.3 Network problem determination

Having quickly covered the common networking options for Linux on System z, the network interface detection and configuration under Linux, in this section we discuss network problem determination. The previous two sections should act as a foundation for this section.

The network problems can be broadly classified into two categories:

+   - Problems related to network communication
+   - Problems related to network performance

Problems related to the network communication are discussed in detail in this chapter. Chapter 5, "Performance problem determination" on page 163, is dedicated to performance problem determination on Linux on System z and discusses network performance problems as well.

# 4.3.1 Problems related to network communication

Communication involves more than one party. Such is the case of computer systems. When computer systems exchange data or messages themselves, we say that they are communicating. When this exchange of messages breaks, we say that there is a communication problem. So, at a very high level, a network communication problem on a system can be a problem local to that system, or it can be outside of that system (that is, the local machine network is functioning correctly). In our discussion, we assume that the local system is a Linux system running on the System z server, and from that system we are trying to communicate to other systems.

# Problem determination on the local machine

When a system is not able to communicate with other systems, there are some logical questions that we need to ask. Are you able to communicate to any system on the network? Did we make any changes to the system prior to the problem occurrence? Are we able to communicate to some of the systems? Is there any information related to the problem in the error logs? We will look at each of these shortly.

# Network communication layer for Linux on System z

Figure 4-12 on page 124 shows the network communication layer for Linux on System z. Such a layer is very useful to narrow down the problem. The bottom-most layer is the hardware (HW) layer. The OSA device falls into this layer. The next layer is the virtual machine (VM) layer, and the virtualization done at the z/VM level (such as the VSWTICH) falls into this layer. The next layers, QDIO and QETH, represent the device driver. The MAC address is represented