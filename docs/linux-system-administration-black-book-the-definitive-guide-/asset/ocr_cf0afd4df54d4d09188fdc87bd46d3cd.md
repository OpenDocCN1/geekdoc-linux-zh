# Setting Up IP Masquerading

To set up IP masquerading, do the following:

+   1. Log in to the command line or a terminal window as root on the machine that is fronting for the masquerade.

+   2. Referring to Table 7.4, choose which addressing class of internal-only IP addresses you want to use for the machines that are masquerading. Typically, people choose class C.

+   3. Type `"vi /etc/rc.d/rc.masq"` to open the brand-new file you will use to store your masquerading settings.

+   4. Enter the following command to build a current list of all kernel module dependencies:

```
/sbin/depmod -a
```

+   5. Now you need to decide what services you want users behind the masquerading server to be able to use. These services and their modules are listed in Table 7.13.

+   6. For each service you want to include, enter a line in the format `"/sbin/modprobe module"`.

+   7. Enter the following line to set your default forwarding policy to refuse data, which is just a good security measure:

```
/sbin/iptables -P forward DENY
```

+   8. Enter a line similar to the following to forward only the information for the class C local-only IP address you chose:

```
/sbin/iptables -A forward -s privateIPclassC/24 -j MASQ
```

+   9. Press the Esc key and then type `"ZZ"` to save and close the file.

+   10. Type `"chmod 700 /etc/rc.d/rc.masq"` to change the permissions for this file.

+   11. Type `"vi /etc/sysconfig/network"` to open the network boot initialization file.

Table 7.13 Modules needed to masquerade specific services.

| Service | Module |
|---|---|
| FTP | ip_masq_ftp |
| IRC | ip_masq_irc |
| RealAudio | ip_masq_raudio |

205