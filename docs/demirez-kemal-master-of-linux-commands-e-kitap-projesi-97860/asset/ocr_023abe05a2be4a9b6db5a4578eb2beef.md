# DNS Configuration

The information and configuration file which has DNS settings information about our system called /etc/resolv.conf file. We can edit/regulate the DNS settings with modifying this file. For example, you can make an arrangement similar to the following.

```
root@kemal:-# echo "nameserver 4.2.2.2" > /etc/resolv.conf
root@kemal:-# echo "nameserver 8.8.8.8" >> /etc/resolv.conf
root@kemal:-# cat /etc/resolv.conf
nameserver 4.2.2.2
nameserver 8.8.8.8
root@kemal:-#
```

To make the adjustments permanent update-rc.d networking defaults can be used.

```
root@kemal:-# update-rc.d networking defaults
root@kemal:-#
```

# Hosts File

This file functions as local domain name server for the current system only. It is the first file to looked up when performing any domain name analysis. Local IP and domain name mappings can be arranged. File is located under /etc directory.

```
root@kemal:-# cat /etc/hosts
127.0.0.1       localhost
127.0.0.1       kemal
n# The following lines are desirable for IPv6 capable hosts
::1             localhost ipv6-localhost ipv6-loopback
ff02::1         ipv6-allnodes
ff02::2         ipv6-allrouters
root@kemal:-#
```