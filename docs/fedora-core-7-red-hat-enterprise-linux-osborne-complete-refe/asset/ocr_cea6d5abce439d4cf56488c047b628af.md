The /etc/hosts.allow and /etc/hosts.deny files are used to restrict access to services provided by your server to hosts on your network or on the Internet (if accessible). For example, you can use the hosts.allow file to permit access by certain hosts to your FTP server. Entries in the hosts.deny file would explicitly deny access to certain hosts. For NFS, you can provide the same kind of security by controlling access to specific NFS daemons.

> *Note You can further secure your NFS transmissions by having them operate over TCP instead of UDP. Use the tcp option to mount your NFS file systems (UDP is the default). However, performance does degrade for NFS when it uses TCP.*

# Portmapper Service

The first line of defense is to control access to the portmapper service. The portmapper tells hosts where the NFS services can be found on the system. Restricting access does not allow a remote host to even locate NFS. For a strong level of security, you should deny access to all hosts except those that are explicitly allowed. In the hosts.deny file, you would place the following entry, denying access to all hosts by default. ALL is a special keyword denoting all hosts.

```
portmap:ALL
```

In the hosts.allow file, you would then enter the hosts on your network, or any others that you would want to permit access to your NFS server. Again, you would specify the portmapper service and then list the IP addresses of the hosts you are permitting access. You can list specific IP addresses or a network range using a netmask. The following example allows access only by hosts in the local network, 192.168.0.0, and to the host 10.0.0.43. You can separate addresses with commas:

```
portmap: 192.168.0.0/255.255.255.0, 10.0.0.43
```

The portmapper is also used by other services such as NIS. If you close all access to the portmapper in hosts.deny, you will also need to allow access to NIS services in hosts.allow, if you are running them. These include ypbind and ypserv. In addition, you may have to add entries for remote commands like ruptime and rusers, if you are supporting them.

In addition, it is also advisable to add the same level of control for specific NFS services. In the hosts.deny file, you would add entries for each service, as shown here:

```
mountd:ALL
rquotad:ALL
statd:ALL
lockd:ALL
```

Then, in the hosts.allow file, you can add entries for each service:

```
mountd: 192.168.0.0/255.255.255.0, 10.0.0.43
rquotad: 192.168.0.0/255.255.255.0, 10.0.0.43
statd: 192.168.0.0/255.255.255.0, 10.0.0.43
lockd: 192.168.0.0/255.255.255.0, 10.0.0.43
```