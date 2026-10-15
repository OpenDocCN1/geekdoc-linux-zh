![](bbox=[0.06, 0.12, 0.66, 0.48])

Figure 10.28 The host (in the top Terminal window) is logged in to the virtual machine, and the virtual machine is logged in to the host!

To share files over FTP, simply open a session from the virtual machine to the host. If you are using bridged networking, connect to the IP address of the host's eth0 Ethernet device (192.168.20.2, in my example). If you are using host-only networking, connect to the IP address of the host's vmnet1 device (192.168.71.1, in my example).

Log in with a username and password that are valid on the host machine, and begin swapping files. Note that some FTP servers by default will not let you log in as root, to protect the system from possible grave tampering. You can consult an advanced text on FTP servers if you need to change features such as this.

> Actually, the example at the start of this section is pure proof-of-concept overkill. Because you can upload as well as download files (put as well as get, in FTP lingo), it's unnecessary to run FTP clients on both sides. But it's nice knowing it can be done!

If you have NFS available on your computer, you can also share drives that way. See Appendix B for details. Also some very clever FTP clients can help make accessing the networked drives virtually transparent.

If you connect over bridged networking, the domain name servers that your computers communicate with might cache the network name of your host PC, allowing you to drop the cumbersome IP address.