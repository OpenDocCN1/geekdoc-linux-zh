# Port Forwarding

Port forwarding is an addition to IP Masquerading which allows some forwarding of packets from outside to inside a firewall on given ports. This could be useful if, for example, you want to run a Web server behind the firewall or masquerading host and that Web server should be accessible from the outside world. An external client sends a request to port 80 of the firewall. The firewall forwards this request to the Web server, the Web server handles the request and the results are sent through the firewall to the original client. The client thinks that the firewall machine itself is running the Web server. This can also be used for load balancing if you have a farm of identical Web servers behind the firewall. Information about this feature is available from http://www.mommouth.demon.co.uk/ipsubs/portforwarding.html. For general info, please see ftp://ftp.comsoc.net/users/steve/ipportfw/linux21.

# Socket Filtering (CONFIG_FILTER)

Using this option, userspace programs can attach a filter to any socket and thereby tell the kernel that it should allow or disallow certain types of data to get through the socket. Linux socket filtering works on all socket types except TCP for now. See the text file . / Linux / Documentation / networking / filter.txt for more information.

# IP: Masquerading

The 2.2 kernel masquerading has been improved. It provides additional support for masquerading special protocols, etc. Be sure to read the IP Chains HOWTO for more information.

# Kernel Devices

There are a few block and character devices available on Linux that will also help you with security.

The two devices `/dev/random` and `/dev/urandom` are provided by the kernel to provide random data at any time.

Both `/dev/random` and `/dev/urandom` should be secure enough to use in generating PGP keys, `ssh` challenges, and other applications where secure random numbers are requisite. Attackers should be unable to predict the next number given any initial sequence of numbers from