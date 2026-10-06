# Chapter 25: Making Servers Public with DNS 971

In this office, other computers on the LAN are using the same Internet connection for outgoing communications, the firewall on the server does network address translation (NAT) to enable the client computers to use the firewall as a router to the Internet. Figure 25-1 shows the configuration of the example yourdomain.com.

Figure 25-1 illustrates a small office network sharing a single Internet connection. The DNS, Web, mail, and FTP servers all have public IP addresses. (These addresses are fictitious, so please don't try to use them.) Behind the DNS server (which is also operating as a firewall) are four client computers that have private IP addresses. (You can reuse these addresses and other private addresses I describe in Chapter 15.)

> DNS works, it doesn't deal with all the complexities you might find in setting up the computing infrastructure at your company. For example, you might well want a dedicated firewall protecting your Internet connection, with the DNS server being placed with the other servers behind which is referred to as a demilitarized zone that is separated from the company LAN.

![](bbox=[0.176, 0.375, 0.823, 0.658])

Figure 25-1: The sample yourdomain.com DNS server has a combination of public servers and private client computers.

The job of the DNS server, in this configuration, is to map the names of the public servers (www.yourdomain.com, mail.yourdomain.com, ftp.yourdomain.com, and ns1.yourdomain.com) into the static IP addresses that the ISP assigns (123.45.67.1, 123.45.67.2, 123.45.67.3, and 123.45.67.8, for our example). The DNS server also provides DNS service from the private addresses on the LAN, so each computer can reach the others on the LAN without needing to store all computer names in their own /etc/hosts file.