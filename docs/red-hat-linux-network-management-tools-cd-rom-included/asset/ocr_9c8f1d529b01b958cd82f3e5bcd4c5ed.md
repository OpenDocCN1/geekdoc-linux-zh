port 1037, which is created when a user issues an ftp command or transfers a file. To stop the continuous display of output, use a ^c (control+c) sequence. As you can imagine, this is a very handy way to monitor network connectivity.

# Ping Tool

# General Description

The ping command provides two basic services. First, it can be used to determine whether a basic level of connectivity is available between one or more endpoints or systems. The ping tool can be used to determine if a remote device is reachable on a network from the local system and help debug connectivity problems among systems. Second, it can provide rudimentary network performance statistics, which can be used to diagnose traffic-related network problems. The term ping is derived from the phrase *packet internet groper*. The ping tool can be used in one of two ways: by specifying a valid hostname or IP address, or by using command-line options with a hostname or IP address. Using the first form, ping provides a handy way to determine that a remote device is available on the network.

Recall from Chapter 3, “TCP/IP Protocol Suite,” that ping uses the Internet Control Message Protocol (ICMP) to emit ICMP requests and waits for valid ICMP replies. Because ICMP is a required protocol within the TCP/IP family, ping can generally be used with every device that supports TCP/IP and is available on many operating systems and other networking devices. For instance, a Cisco router provides the capability to ping other devices on the network. The ping tool is a client-side application only; no additional software is needed nor required for it to function and interact directly with the remote system’s protocol layer to accomplish its task.

# Determine System Availability

The ping tool can be used to determine general availability of any TCP/IP device even if it doesn’t specifically have a general operating system. For example, to determine if the host *rembrandt* is reachable, issue the following *ping* command: