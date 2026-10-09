Under the Security Level: drop-down list, the options are High, Medium, and No firewall:

+   □ The **High** setting configures the firewall to reject all incoming TCP connections (by blocking TCP packets that have the SYN flag set, and ACK cleared), and reject all incoming UDP packets, with the exception of replies to DNS queries on port 53 that come from the name servers we told Red Hat Linux about when we configured the network settings. (If the DNS replies were blocked, then we would be unable to resolve any host names that aren't defined in the local /etc/hosts file, which would make using the Internet very tedious.)

> Note that, since incoming connections are blocked, we can't run a Web server or any other kind of server behind such a firewall.

+   □ The **Medium** setting configures the firewall to reject all incoming TCP connections to ports in the range 0 to 1023, and also incoming UDP packets for these port numbers. NFS and X11 traffic are also blocked. The significance of the ports in the range 0 to 1023 is that these are "privileged" ports, and a program has to be running with root authority in order to open sockets on them. However, this does not mean that ports with numbers 1024 to 65536 can only have unprivileged programs opening sockets on them. It is quite possible to set up a Web server running with root authority listening on, say, port 8080.

+   □ If we select **No firewall** as the security level, then the firewall is disabled.

If we find that the default firewall rules do not meet our requirements, then we can select the **Customize** radio button. This enables the remaining options on the window:

![](bbox=[0.29, 0.56, 0.7, 0.9])