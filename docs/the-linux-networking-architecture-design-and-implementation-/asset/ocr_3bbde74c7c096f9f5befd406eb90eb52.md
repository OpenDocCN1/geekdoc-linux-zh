# 150 Chapter 8 The Point-to-Point Protocol (PPP)

The dial-on-demand mode means that a PPP connection is established automatically when needed (i.e., when IP packets are ready to output from the corresponding network device). The connection remains idle for a specific (configurable) period, when pppd tears it down automatically. This means that the expensive telephone line is used only upon demand, and the user does not have to dial. The only drawback of this mode is that it introduces a certain delay until the connection is up.

This functionality is implemented by the state PHASE DORMANT (See Section 8.4.2). pppd assumes this state before a peer dialed, if the option demand is stated in its configuration file. In this case, the generic PPP driver in the Linux kernel sends out IP packets for the respective PPP device directly to pppd; which dials to the provider, rather than to the asynchronous driver.

To better control the cost, the option active-filter can be used to specify a filter to decide which network traffic is important enough to establish a connection. Detailed information about this functionality is found in the management of pppd in the Options section.

# 8.2.4 Automatic Callback

The automatic callback function means that the client dials normally to a remote server. During the configuration phase, however, the client uses the PPP subprotocol CBCP (Call Back Configuration Protocol) to request a callback. Subsequently, the connection is torn down, and pppd terminates with return value 14. If the server is configured appropriately, it calls back the client, so that the client and the server, in effect, switch their roles. This functionality is suitable, for example, when a company wants to assume the cost for its teleworkers dialing into company computers.

# 8.3 PPP IMPLEMENTATION IN THE LINUX KERNEL

As mentioned before, the PPP implementation in Linux is divided into four different tasks: three kernel modules and the pppd user space daemon. During design of this vision, care was taken to move as little functionality as possible into the Linux kernel. For this reason, the kernel modules are rather simple, ppp includes 13,000 lines of code (2,100 lines in main.c), which means that it is four times the size of the three kernel modules (ppp generic.c, ppp syntty.c and ppp_async.c) together. In the following sections, we will first discuss the generic PPP driver and the driver for the asynchronous PPP TTY line discipline. The driver for the synchronous PPP line discipline is relatively simple, so we will not discuss it here.

# 8.3.1 Functions and Data Structures of the Generic PPP Driver

Figure 8-4 shows the most important data structures of the generic PPP driver. There is a separate PPP structure with general management information for each PPP device. Some important entries, particularly the transmit and receive queues, xq and rq, are a substructure of the type ppp_file. This substructure is also found in the channel structure, which is used to manage single channels in multilink PPP, which will not be discussed here, for the sake of simplicity.

There is a PPP device for each network device, the device structure which refers to the related PPP structure in the field priv. In addition, the PPP daemon can send