Whenever you connect to the Internet through a dial-up connection, the outside world not only becomes transparent to you—that is, you can now browse and view other sites—but you also become transparent to others. If your ports are not correctly closed or if you do not have the necessary security patches in place, anyone with a functioning packet sniffer or port scanner can quickly compromise your Linux machine. You should take the following precautionary measures:

+   1.  Place the following in your /etc/hosts.deny file. If you do not have this file, create it. You probably already have tcp_wrappers installed, as it installs by default with the latest Red Hat releases, and this file requires tcp_wrappers in order to work.
+       
+       ALL: ALL

+   2.  Type the following in your /etc/hosts.allow file:
+       
+       ALL: LOCAL

The first file denies all users from outside your system to all ports and processes on your local machine. The second file allows only the localhost access to the needed ports. You may add any additional IP addresses, hostnames, or services to the latter file and allow other users to access your home machine.

> I sometimes add the IP address for my machine at work to my home machine's hosts.allow file. This way I dial up at home and do work on my home machine while at work.

In your /etc/resolv.conf file, add the following lines. You'll have to change them based upon your own ISP and its name servers. Talk to your ISP's support staff if you don't have viable IP addresses of a name server that you can access.

```
search my_isp.com

domain my_isp.com

nameserver 192.168.0.254

nameserver 192.168.0.253
```

Be sure to replace the variables in this example with the correct numbers and names associated with your own Linux connection.