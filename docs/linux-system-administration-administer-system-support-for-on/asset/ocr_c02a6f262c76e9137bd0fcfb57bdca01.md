```
# Ident service is used for net authentication
auth\tstream\ttcp\twait\troot\t/usr/sbin/in.identd\tin.identd -t -l
#
# These are to start Samba, an smb server that can export file systems to
# Pathworks, Lanmanager for DOS, Windows for Workgroups, Windows95, Lanmanager
# for Windows, Lanmanager for OS/2, Windows NT, etc.
# If you're running smbd and nmbd from daemons in /etc/rc.d/rc.samba, and then
you
# shouldn't uncomment these lines.
#
# netbios-ssn\t\tstream\ttcp\tnowait\troot\t\t/usr/sbin/smbd\tsmbd
# netbios-ns\t\tdgram\tudp\twait\troot\t\t/usr/sbin/nmbd\tnmbd
#
# Sun-RPC based services.
# <service name/version><sock_type><rpc/proto><flags><user><server><args>
#
#
# rstatd/1-3\tdgram\trpc/udp\twait\troot\t/usr/sbin/tcpd\trpc.rstatd
# rusersd/2-3\tdgram\trpc/udp\twait\troot\t/usr/sbin/tcpd\trpc.rusersd
# wall d/1\t\tdgram\trpc/udp\twait\troot\t/usr/sbin/tcpd\trpc.rwalld
#
# End of inetd.conf.
```

![](bbox=[0.15, 0.53, 0.24, 0.6])

> Be sure to comment out network daemons that don't need to be running. If you run a network daemon and there's a logging capability, log the connection. Network connections can be capitalized on to gain root access if you're using ones that have known exploits. Additionally, the more ports you have open, the easier a denial of service attack is.

# # Network Files

Slackware contains some indispensable network files. These files define services, hosts, and configurations on network daemons and other network services.

Because IP addresses are divided up by hosts and networks, there are two files called **/etc/hosts** and **/etc/networks**. The **/etc/hosts** file is one way Slackware translates IP addresses into network names.

# ## The hosts File

The format of a listing in the **/etc/hosts** file looks like this:

```
IP address:Network Name:Alias
```