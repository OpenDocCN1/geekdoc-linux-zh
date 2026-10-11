The configuration files shown here were copied from a fully working system. All dynamically registered entries have been removed. In addition to these files, BIND version 9 will create for each of the dynamic registration files a file that has a `.jnl` extension. Do not edit or tamper with the configuration files or with the `.jnl` files that are created.

# 46.2.2 DHCP Server

The following file is used with the ISC DHCP Server version 3. The file is located in `/etc/dhcpd.conf`:

```
ddns-updates on;  
ddns-domainname "quenya.org";  
option ntp-servers 192.168.1.2;  
ddns-update-style ad-hoc;  
allow unknown-clients;  
default-lease-time 86400;  
max-lease-time 172800;  

option domain-name "quenya.org";  
option domain-name-servers 192.168.1.2;  
option netbios-name-servers 192.168.1.2;  
option netbios-dd-server 192.168.1.2;  
option netbios-node-type 8;  

subnet 192.168.1.0 netmask 255.255.255.0 {  
  range dynamic-bootp 192.168.1.60 192.168.1.254;  
  option subnet-mask 255.255.255.0;  
  option routers 192.168.1.2;  
  allow unknown-clients;  
}
```

In this example, IP addresses between 192.168.1.1 and 192.168.1.59 are reserved for fixed-address (commonly called **hard-wired**) IP addresses. The addresses between 192.168.1.60 and 192.168.1.254 are allocated for dynamic use.