programs on a Linux system. Restrictions for each application are stored within text files named for the program under the /etc/apparmor.d directory; each text file is called an **AppArmor profile**. For example, the AppArmor profile for the CUPS daemon (/usr/sbin/cupsd) would be stored within the /etc/apparmor.d/usr.bin.cupsd file.

![](bbox=[0.158, 0.177, 0.848, 0.24])

![](bbox=[0.158, 0.274, 0.9, 0.35])

AppArmor profiles can be enforced by AppArmor (called enforce mode) or simply used to generate warnings and log events (called complain mode). To view the AppArmor profiles configured for each mode, as well as the active processes on the system that are being managed by AppArmor, you can run the **apparmor_status** command, as shown here:

```
``` 
[root@server1 -]# apparmor_status 
apparmor module is loaded.
12 profiles are loaded.
12 profiles are in enforce mode.
/sbin/dhclient 
/usr/lib/NetworkManager/nm-dhcp-client.action 
/usr/lib/connman/scripts/dhclient-script 
/usr/lib/cups/backend/cups-pdf 
/usr/lib/libvirt/virt-aa-helper 
/usr/sbin/cups-browsed 
/usr/sbin/cupsd 
/usr/sbin/libvirtd 
/usr/sbin/mysqld 
/usr/sbin/named 
/usr/sbin/nrpd 
/usr/sbin/tcpdump 
0 profiles are in complain mode.
7 processes have profiles defined.
7 processes are in enforce mode.
/sbin/dhclient (1900) 
/usr/lib/cups-browsed (2284) 
/usr/sbin/cupsd (3195) 
/usr/sbin/libvirtd (2407) 
/usr/sbin/mysqld (2523) 
/usr/sbin/named (2276) 
/usr/sbin/tcpdump (3274) 
```
```