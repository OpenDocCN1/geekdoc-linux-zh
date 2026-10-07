don't want to be able to log in remotely as root. That is a major security hazard. The more secure way is to log in as another user and, once logged in, use the su command to assume superuser privileges. If you're still convinced that you want to log in as root, you can enable your system to allow this. The /etc/security lists the virtual consoles and tys from which root is permitted to log in. Since logging remotely brings you in on a pseudoterminal, you need to add pts/n lines to the /etc/security file. How many pseudoterminals need to add depends on the number of remote connections. It's important to remember that doing this is a bad idea. Don't do this unless you absolutely have to. If you have to do this to test something, add the pts lines, the test, and remove the pts lines immediately.

# Troubleshooting Problems

An apparent network problem should be done in stages. Find out whether a local machine can ping the remote host and whether the remote machine can ping back. If the local ping is successful but the remote machine's ping fails, look for problems in the configuration of the remote machine. If you can't find the source of the problem, look for a remote machine that can ping the local machine and compare the configuration of both machines. Most Ethernet cards have link lights that indicate whether the card is able to send data packets. The best way to troubleshoot a network is to do it.

Following are a few networking problems related to Linux or software configuration. We cannot address the much wider problem space presented by networking hardware, simply because there are too many possible combinations and configurations to cover.

# Unknown Host Message

If you get this error when trying to Telnet or use various other networking tools, the hostname cannot be resolved into an IP address. This could be because a name server problem, a network problem, or a typing error. Try to ping the IP address instead of the hostname. If you can ping the host by numeric IP, the problem is with the name setup. Otherwise, verify that the name you typed in is the correct one. If it is, try to ping another machine on the same network as the one causing you problems. If you can, the problem is almost definitively with the setup of the problematic host or the cable that runs to it from the network.

Another possibility, especially on local networks that do not use DNS internal, is a problem with the /etc/hosts file. This file can be used as a substitute for DNS on local networks; it contains the mapping of hostnames to IP addresses. An example resembles the following.

![](bbox=[0.965, 0.215, 0.995, 0.735])