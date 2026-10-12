Figure 25-1 illustrates a small office network that's sharing a single Internet connection. The DNS, Web, Mail, and FTP servers all have public IP addresses. (These addresses are fictitious, so please don't try to use them.) Behind the DNS server (which is also operating as a firewall) are four client computers that have private IP addresses. (You can reuse these addresses and other private addresses that I describe in Chapter 15.)

The job of the DNS server, in this configuration, is to map the names of the public servers (www.yourdomain.com, mail.yourdomain.com, ftp.yourdomain.com, and ns1.yourdomain.com) into the static IP addresses that the ISP assigns (123.45.67.1 through 123.45.67.4). The DNS server is also providing DNS service from the private addresses on the LAN, so each computer can reach the others on the LAN without needing to store all computer names in their own /etc/hosts file.

The sections that follow describe how to set up a DNS server for the example in Figure 25-1.

# ## Quick-starting a DNS server

The DNS server software that comes with Red Hat Linux 7.3 is Berkeley Internet Name Daemon (BIND) version 9. To configure BIND 9, you work with the following components:

+   - **Configuration file** (/etc/named.conf) — The primary configuration file for the DNS server.
+   - **Zone directory** (/var/named) — The directory containing files that keep information about Internet root DNS servers (named.ca file) and information about the zones that you create for your DNS server.
+   - **Daemon process** (/usr/sbin/named) — The daemon process that listens for DNS requests and responds with information that the named.conf file presents.
+   - **Debugging tools** (named-checkconf, and named-checkzone) — What you use to determine whether you created your DNS configuration correctly.

BIND 9 also includes tools for creating DNSSEC secured zones. By using these tools, you can create and generate keys to provide authentication and secure address resolution. The example illustrated in these sections doesn't include DNSSEC configuration.

The basic steps in creating a DNS server for your example are as follows:

+   - Identifying your DNS servers
+   - Creating DNS Configuration files (/etc/named.conf and /var/named/*)
+   - Starting the named daemon
+   - Monitoring named activities

In the example configuration, you set up a primary master DNS server and a slave DNS server. The primary holds the authoritative records for the domain. The secondary is there to share requests for information about the domain and in case the primary goes down.