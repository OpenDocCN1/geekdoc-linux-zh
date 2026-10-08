# TCP/IP basics

# 14

Chapter 13 has shown how to configure a LINUX computer for participation in a TCP/IP-based network. This chapter will introduce the individual protocols and their use within within the network. This should enable you to understand the functioning of a TCP/IP network. As already shown in Figure 13.2, the hardware connections form the basis for a series of protocol layers, whose interaction will now be explained in more detail.

# 14.1 Protocols

The Internet is based on a series of protocols which guarantee orderly data exchange between computers. The numbers of these protocols are defined in the file /etc/protocols (Listing 14.1). It is extremely improbable that you will ever be called on to modify this file.

Essentially, four protocols are used whose existence in the kernel is also signalled by LINUX during booting: