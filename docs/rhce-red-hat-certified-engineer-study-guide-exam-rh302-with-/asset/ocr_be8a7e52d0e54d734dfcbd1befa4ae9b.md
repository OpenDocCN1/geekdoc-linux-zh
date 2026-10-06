The Flags field can contain such values as:

+   - U, which indicates that the network link is up

+   - H, which indicates that the destination address refers to a host rather than a network

+   - G, which indicates that the routing rule specifies a gateway

The Metric, Ref, and Use fields are irrelevant except when using dynamic routing.

Now complete Exercise 29.1 to gain practical experience with network configuration.

# EXERCISE 29.1

# Network Configuration

If you have access to three hosts connected to a network, configure one as a router that joins the two remaining hosts. Then, experiment by using linuxconf and route to specify various routing rules until you feel comfortable manipulating the routing table.

Refer back to this chapter and other resources when completing this exercise. But, be prepared to perform similar operations without help taking the RHCE exam.

# Kernel Configuration

The Linux kernel provides a variety of network-related options. You can see most of these in Figure 29.6, which shows the top of the makeconfig page that includes the network-related options. Table 29.1 summarizes the most important options. Two especially important options Red Hat Linux for use as a router: IP: advanced router and IP: optimize as router host, which is not visible in Figure 29.6. If a Linux system is used primarily or exclusively—as a router, you should specify these options and recompile its kernel.