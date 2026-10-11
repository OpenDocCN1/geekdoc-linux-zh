Like configuring a NIC, information about each PPP device in stored in files named ifcfg-InternetServiceProviderName underneath the /etc/sysconfig/network-scripts directory. For example, the information configured earlier for the xDSL connection is stored in the /etc/sysconfig/network-scripts/ifcfg-isp file, as shown in the following output:

```
```bash
[root@server1 root]# cat /etc/sysconfig/network-scripts/ifcfg-isp
# Please read /usr/share/doc/initscripts-*/sysconfig.txt
# for the documentation of these parameters.

IPV6INIT=no
ONBOOT=yes
USERCTL=yes
PEERDNS=yes
TYPE=xDSL
DEVICE=ppp0
BOOTPROTO=dialup
PIDFILE=/var/run/pppoe-ads1.pid
FIREWALL=NONE
PING=.
PPPOE_TIMEOUT=80
LCP_FAILURE=3
LCP_INTERVAL=20
CLAMPMS=1412
CONNECT_POLL=6
CONNECT_TIMEOUT=60
PERSIST=no
SYNCHRONOUS=no
DEFRROUTE=yes
USER=user1
ETH=eth0
PROVIDER=isp
DEMAND=no
[root@server1 root]# _
```
```

Other configurations are used by the PPP daemon is stored in the /etc/ppp and /etc/isdn directories. It is good form to double-check the passwords used to connect to the ISP because incorrect passwords represent the most common problem with PPP connections. These passwords are stored in two files: /etc/ppp/pap-secrets (Password Authentication Protocol secrets) and /etc/ppp/chap-secrets (Challenge Handshake Authentication Protocol secrets). If the ISP accepts passwords sent across the network in text form, the /etc/ppp/pap-secrets file is consulted for the correct password; however, if the ISP requires a more secure method for validating the identity of a user, the passwords in the /etc/ppp/chap-secrets file are used. When you configure a PPP connection, this information is automatically added to both files, as shown in the following output: