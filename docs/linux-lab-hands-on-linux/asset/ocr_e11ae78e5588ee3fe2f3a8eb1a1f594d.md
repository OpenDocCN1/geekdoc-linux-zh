Server Side:

| Config Path | Description |
| :--- | :--- |
| /var/named/chroot/etc/named.conf | Main DNS configuration file that list location and name of the zone files to be used for your desired website domains. |
| /var/named/chroot/var/named/... (name of the forward zone file) | maps domain name to ip addresses |
| /var/named/chroot/var/named/... (name of the reverse zone file ) | ipaddresses to domain name. |
| /var/named/chroot/var/named/named.ca | List of 13 root authoritative servers. |
| /var/named/chroot/etc/rndc.key | File used in named authentication |


+   - Client side program: nslookup.dig and host
+   - Server Side program: named, named-checkzone-----

# ■ Steps to Install and configure DNS Server/Client

# ♦ Client Side

+   1. Edit /etc/resolv.conf
+   nameserver {ip address of DNS server}

For example, nameserver 172.16.20.1

Table 1 is displaying keywords of /etc/resolv.conf

| Keywords in /etc/resolv.conf | Value |
| :--- | :--- |
| nameserver | IP address of your DNS name server. There should be only one entry per nameserver keyword. If there is more than one name server, use multiple nameserver lines |
| Domain | The local domain name to be used by default. If the server is netmon.split.ac.in, then the entry would just be split.ac.in. |
| Search | If you refer to another server just by its name without the domain added on, DNS on your client appends the server name to each domain in this list and does a DNS lookup on each to get the remote server's IP address. This is a time-saving feature, enabling you to refer to servers in the same domain by only their server name without having to specify the domain. The domains in this list must be separated by spaces. |


![](bbox=[0.21, 0.74, 0.85, 0.76])

# ♦ Server Side

+   1. Configuring resolv.conf
+   You will have to make your DNS server refers to itself for all DNS queries by configuring the /etc/resolv.conf file to reference localhost only