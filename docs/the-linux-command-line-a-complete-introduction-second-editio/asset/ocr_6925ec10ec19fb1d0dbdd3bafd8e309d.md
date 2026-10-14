host to the destination network. An asterisk in this field indicates that no gateway is needed.

The last line contains the destination default. This means any traffic destined for a network that is not otherwise listed in the table. In our example, we see that the gateway is defined as a router with the address of 192.168.1.1, which presumably knows what to do with the destination traffic.

Like ip, the netstat program has many options, and we have looked only at a couple. Check out the ip and netstat man pages for a complete list.

# Transporting Files over a Network

What good is a network unless we can move files across it? There are many programs that move data over networks. We will cover two of them now and several more in later sections.

# ftp

One of the true “classic” programs, ftp gets its name from the protocol it uses, the File Transfer Protocol. FTP was once the most widely used method of downloading files over the Internet. Most, if not all, web browsers support it, and you often see URIs starting with the protocol ftp://.

Before there were web browsers, there was the ftp program. ftp is used to communicate with FTP servers, machines that contain files that can be uploaded and downloaded over a network.

FTP (in its original form) is not secure because it sends account names and passwords in cleartext. This means they are not encrypted, and anyone sniffing the network can see them. Because of this, almost all FTP done over the Internet is done by anonymous FTP servers. An anonymous server allows anyone to log in using the login name “anonymous” and a meaningless password.