When you have successfully used dig to contact a DNS server, you can get a bit fancier with what you ask that server to do. Here, for example, is the command I type to try a reverse lookup with the IP address 192.168.0.2:

```
host 192.168.0.2 localhost
```

This command displays the following output:

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:

2.0.168.192.in-addr.arpa domain name pointer wxp.naba.net
```

# Understanding Network Information Service (NIS)

Network Information Service (NIS) was developed by Sun Microsystems as a way to share information among all computers in a local area network. The types of information NIS most commonly uses include the following:

+   ♦ User names and passwords from files such as `/etc/passwd` and `/etc/shadow`
+   ♦ Group information from the `/etc/group` file

Normally, each system has its own copy of information in respective files, and any changes require updating the files on each system individually. Using NIS, you can maintain a single set of configuration files for a collection of computers in an NIS server. All other computers running NIS clients can then access the files. For example, if your user name and password are in the NIS password database, you will be able to log in on all computers on the network running NIS client programs.

![](bbox=[0.15, 0.78, 0.22, 0.9])

NIS was originally called Sun Yellow Pages (YP), but the name Yellow Pages is a registered trademark of British Telecom in the United Kingdom, so Sun Microsystems had to change the name. To this day, however, many NIS commands — and the NIS package names — begin with the letters yp.

# How NIS works

If you want to use NIS in a network, you must set up at least one computer as an NIS server. You can have multiple NIS servers in a network, each serving a different collection of computers. You can also have a master NIS