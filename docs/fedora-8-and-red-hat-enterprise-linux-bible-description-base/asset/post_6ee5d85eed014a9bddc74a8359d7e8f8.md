
During a DOS attack, the foreign address is usually the same for each connection. In this case, it is a simple matter of typing the whois command, followed by the foreign IP address, to determine who owns the IP address of the machine causing the attack.

During a DDOS attack, the foreign address will likely be different for each connection. In this case, it is impossible to track down all of the offenders because there will likely be thousands of them. The best way to defend yourself is to contact your ISP and see if it can filter the traffic at its border routers.

## Protecting against intrusion attacks

Crackers have a wide variety of tools and techniques to assist them in breaking into your computer. Intrusion attacks focus on exploiting weaknesses in your security, so the crackers can take more control of your system (and potentially do more damage) than they could from the outside.

Fortunately, there are many tools and techniques for combating intrusion attacks. This section discusses the most common break-in methods and the tools available to protect your system. Although the examples shown are specific to Fedora and Red Hat Enterprise Linux systems, the tools and techniques are generally applicable to any other Linux or UNIX-like operating system.

> **CROSS-REFERENCE:** The tripwire package, which is included in the Fedora repository, is a good tool for detecting whether intrusion attacks have taken place. The description of tripwire is not in this edition. However, if you are interested in installing the package on your own, you can find the description of tripwire on the companion Web site of this book at www.wiley.com/go/fedora8bible.

### Evaluating access to network services

Fedora, Red Hat Enterprise Linux, and its UNIX kin provide many network services, and with them many avenues for cracker attacks. You should know these services and how to limit access to them. Refer to Appendix B for listings and short descriptions of available services.

What do I mean by a network service? Basically, I am referring to a resource or facility that a remote user can request of the server machine, such as a login, file sharing, instant messaging, or other service. Routing e-mail is a network service. So is serving Web pages. Your Linux box has the potential to provide thousands of services. Many of them are listed in the /etc/services file. Look at a snippet of that file:

```
# /etc/services:

# service-name port/protocol   [aliases ...]   [# comment]
chargen      19/tcp              ttys source
chargen      19/udp              ttys source
ftp-data     20/tcp
ftp-data     20/udp
# 21 is registered to ftp, but also used by ftp
ftp			21/tcp
ftp			21/udp	fsp fspd
ssh			22/tcp		# SSH Remote Login Protocol
ssh			22/udp		# SSH Remote Login Protocol
telnet		23/tcp
telnet		23/udp
# 24 - private mail system
smtp			25/tcp		mail
```

After comment lines, you will notice three columns of information. The left column contains the name of each service. The middle column defines the port number and protocol type used for that service. The rightmost field contains an optional alias or list of aliases for the service.

As an example, examine the last entry in the file snippet. It describes the SMTP (Simple Mail Transfer Protocol) service, which is the service used for delivering e-mail over the Internet. The middle column contains the text 25/tcp, which tells us that the SMTP protocol uses port 25 and uses the Transmission Control Protocol (TCP) as its protocol type.

What exactly is a *port number*? It is a unique number that has been set aside for a particular network service. It allows network connections to be properly routed to the software that handles that service. For example, when an e-mail message is delivered from some other computer to your Linux box, the remote system must first establish a network connection with your system. Your computer receives the connection request, examines it, sees it labeled for port 25, and thus knows that the connection should be handed to the program that handles e-mail (which happens to be sendmail).

I mentioned that SMTP uses the TCP protocol. Some services use UDP, the User Datagram Protocol. All you really need to know about TCP and UDP (for the purpose of this Internet discussion) is that they provide different ways of *packaging* the information sent over a network connection. A TCP connection provides error detection and retransmission of lost data. UDP doesn't check to ensure that the data arrived complete and intact; it is meant as a fast way to send non-critical information.

### Disabling network services

Although there are hundreds of services (listed in /etc/services) that potentially could be available and subject to attack on your Fedora or Red Hat Enterprise Linux system, in reality only a few dozen services are installed and only a handful of those are on by default. Most network services are started by either the xinetd process or by a start-up script in the /etc/init.d directory.

xinetd is a daemon that listens on a great number of network port numbers. When a connection is made to a particular port number, xinetd automatically starts the appropriate program for that service and hands the connection to it. The xinetd daemon improves on its predecessor, inetd, by offering features that include more flexible access control, more logging settings, and denial-of-service prevention.

The configuration file /etc/xinetd.conf is used to provide default settings for the xinetd server. The directory /etc/xinetd.d contains files telling xinetd what ports to listen on and what programs to start. Each file contains configuration information for a single service, and the file is usually named after the service it configures. For example, to enable the rsync service, edit the rsync file in the /etc/xinetd.d directory and look for a section similar to the following:

```
service rsync
{
	disable = yes
	socket_type		= stream
	wait		= no
	user		= root
	server		= /usr/bin/rsync
	server_args = --daemon
	log_on_failure	+= USERID
}
```

Note that the first line of this example identifies the service as rsync. This exactly matches the service name listed in the /etc/services file, causing the service to listen on port 873 for TCP and UDP protocols. You can see that the service is off by default (disable = yes). To enable the rsync services, change the line to read like this:

```
disable = no
```

> **TIP:** The rsync service is a nice one to turn on if your machine is an FTP server. It allows people to use an rsync client (which includes a checksum-search algorithm) to download files from your server. With that feature, users can restart a disrupted download without having to start from the beginning.

Because most services are disabled by default, your computer is only as insecure as you make it. You can double-check that insecure services, such as rlogin and rsh (which are included in the rsh-server package), are also disabled by making sure that disabled = yes is set in the /etc/xinetd.d/rlogin and rsh files.

> **TIP:** You can make the remote login service active but disable the use of the /etc/host.equiv and .rhosts files, requiring rlogin to always prompt for a password. Rather than disabling the service, locate the server line in the rsh file (server = /usr/sbin/in.rshd) and add a space followed by -L at the end. Of course, that doesn't change the fact that your password and data will still be sent unencrypted over the network.

You now need to send a signal to the xinetd process to tell it to reload its configuration file. The quickest way to do that is to reload the xinetd service. As the root user, type the following from a shell:

```
# service xinetd reload
Reloading configuration:			[ OK ]
```

That’s it — you have enabled the rsync service. Provided that you have properly configured your mail server (see Chapter 19), clients should now be able to download files from your computer via the rsync protocol.

### Securing servers with SELinux

Red Hat, Inc. did a clever thing when it took its first swipe at implementing SELinux in Red Hat systems. Instead of creating only policies to control every aspect of your Linux system, it created a “targeted” policy type that focused on securing those services that are most vulnerable to attacks. Red Hat then set about securing those services in such a way that, if they were compromised, a cracker couldn’t compromise the rest of the system as well.

After you have opened a port in your firewall so others can request a service, and then started that service to handle requests, SELinux can be used to set up walls around that service. As a result, its daemon process, configuration files, and data can’t access resources they are not specifically allowed to access. The rest of your computer, then, is safer.

As Red Hat continues to work out the kinks in SELinux, there has been a tendency for users to experience SELinux failures and just disable SELinux. If you have tried SELinux in the past and turned it off when you had a problem, consider that SELinux has improved quite a bit in recent versions and it might be time for you to try it again.

If you do encounter a failure related to SELinux, try to find out if SELinux should have caused the failure. In other words, maybe you were doing something that was unsafe and SELinux was right to fail. However, if the failure you encounter turns out to be a bug with SELinux, file a bug report to `http://bugzilla.redhat.com` and help make the service better.

See Chapter 10 for a more in-depth description of SELinux in Fedora and RHEL.

### Protecting Web servers with certificates and encryption

Previous sections told you how to lock the doors to your Fedora or RHEL system to deny access to crackers. The best dead bolt lock, however, is useless if you are mugged in your own driveway and have your keys stolen. Likewise, the best computer security can be for naught if you are sending passwords and other critical data unprotected across the Internet.

A savvy cracker can use a tool called a *protocol analyzer* or a *network sniffer* to peek at the data flowing across a network and pick out *passwords*, credit card data, and other juicy bits of information. The cracker does this by breaking into a poorly protected system on the same network and running software, or by gaining physical access to the same network and plugging in his or her own equipment.

You can combat this sort of theft by using encryption. The two main types of encryption in use today are symmetric cryptography and public-key cryptography.
