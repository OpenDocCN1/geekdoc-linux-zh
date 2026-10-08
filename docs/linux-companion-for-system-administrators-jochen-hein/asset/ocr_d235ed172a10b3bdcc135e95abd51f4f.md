# REMOTE PROCEDURE CALL 407

+   - The appropriate daemons and programs must be compiled and installed.

+   - The new daemons must either be called at system start-up (for example in the /etc/rc.local script) or entered in the file /etc/inetd.conf. Since this file has different formats on different computers, it can unfortunately not be distributed by means of the NIS (Network Information System). You could, however, employ a package such as GNU cfengine.

# 4.6 Remote Procedure Call

Remote Procedure Calls (RPC) are another widely used possibility of communication. This method was developed by Sun, among others; the specification was published in [rfc1057]. Services such as NFS (Network File System, Chapter 17, and NIS (Network Information System, Chapter 21) were developed on the basis of RPC.

Each version of an RPC protocol (for example mount, ybind) is associated with a version number. In case of incompatible changes to the protocol, the version number is increased. Each client specifies at the establishment of a connection which version of a protocol is to be used. Many servers support several versions and use the matching protocol. This makes it possible to install a new version first on the server and then on the clients in a network without disrupting the network operation.

Management of services is taken on, in analogy to inetd, by the port mapper. Under LINUX, the program is called rpc.portmap and can be found in the /usr/sbin directory. In /etc/rpc, the ports are assigned to individual applications. By means of the rpcinfo program you can find out which RPC services are provided by a computer (rpcinfo -p computer, see Listing 14.8). If this function is called without a computer name, information on your own computer is displayed.

With the option -u (for UDP) or -t (for TCP) you can explicitly determine whether a computer provides a specific service (with a special version) (see Listing 14.9). To ensure functionality, the call is made to procedure 0 of the corresponding server.