# **CREATE /var/yp/securenets TO ENHANCE SECURITY**

To enhance system security, create the /var/yp/securenets file, which prevents unauthorized systems from sending RPC requests to the NIS server and retrieving NIS maps. Notably **securenets** prevents unauthorized users from retrieving the **shadow** map, which contains encrypted passwords. When **securenets** does not exist or is *empty*, an NIS server accepts requests from any system.

Each line of **securenets** lists a netmask and IP address. NIS accepts requests from systems whose IP addresses are specified in **securenets** and ignores and logs requests from other addresses. You must include the (local) server system as **localhost** (127.0.0.1) in **securenets**. A simple **securenets** file follows:

```
$ cat /var/yp/securenets
# you must accept requests from localhost
255.255.255.255           127.0.0.1
#
# accept requests from IP addresses 192.168.0.1 - 192.168.0.62
255.255.255.192           192.168.0.0
#
# accept requests from IP addresses starting with 192.168.14
255.255.255.0             192.168.14.0
```

# **EDIT /var/yp/Makefile TO SPECIFY MAPS**

The *make* utility, controlled by /var/yp/Makefile, uses *makedb* to create the NIS maps that hold the information that NIS distributes. When you run *ypinit* on the master server, *ypinit* calls *make*: You do not need to run *make* manually. Edit /var/yp/Makefile to set options and specify which maps to create. The following sections discuss /var/yp/Makefile in more detail.

# **VARIABLES**

Following is a list of variables you can set in /var/yp/Makefile. The values following the words Fedora/RHEL are the values set in the file distributed by Fedora/RHEL.

+   B Do not change. Fedora/RHEL: not set
+   NO*PUSH* Specifies that *yperserv* is not to copy (push) maps to slave servers. Set to TRUE if you do not have any slave NIS servers; set to FALSE to cause NIS to copy maps to slave servers. Fedora/RHEL: TRUE
+   MINUID, MINGID Specifies the lowest UID and GID numbers to include in NIS maps. In the /etc/passwd and /etc/group files, lower ID numbers belong to **root** and system accounts and groups. To enhance security, NIS does not distribute password and group information about these users and groups. Set MINUID to the lowest UID number you want to include in the NIS maps and set MINGID to the lowest GID number you want to include. Fedora/RHEL: 500/500