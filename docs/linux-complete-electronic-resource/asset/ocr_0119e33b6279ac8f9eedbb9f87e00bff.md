+   Enable loadable module support  
+   CONFIG_MODULES
+   - allows you to load ipmasq modules such as ip_masq_ftp.o

+   Networking support  
+   CONFIG_NET

+   Network firewalls  
+   CONFIG_FIREWALL

+   TCP/IP networking  
+   CONFIG_INET

+   IP: forwarding/gatewaying  
+   CONFIG_IP_FORWARD

+   IP: firewalling  
+   CONFIG_IP_FIREWALL

+   IP: masquerading  
+   CONFIG_IP_MASQUERADE

+   IP: ipportfw masq support  
+   CONFIG_IP_MASQUERADE_IPPORTFW
+   - recommended

+   IP: ipautofw masquerade support  
+   CONFIG_IP_MASQUERADE_IPAUTOFW
+   - optional

+   IP: ICMP masquerading  
+   CONFIG_IP_MASQUERADE_ICMP
+   - support for masquerading ICMP packets, recommended.

+   IP: always defragment  
+   CONFIG_IP_ALWAYS_DEFRAG
+   - highly recommended

+   Dummy net driver support  
+   CONFIG_DUMMY
+   - recommended

+   IP: ip fwmark masq-forwarding support  
+   CONFIG_IP_MASQUERADE_MFW
+   - optional

![](bbox=[0.9, 0.5, 0.95, 0.7])