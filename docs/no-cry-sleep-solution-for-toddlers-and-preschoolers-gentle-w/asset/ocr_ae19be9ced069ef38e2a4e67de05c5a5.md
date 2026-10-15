To both export added entries and re-export changed ones, you can combine the -r and -a options.

```
exportfs -r -a -v
```

# Manually Exporting File Systems

You can also use the exportfs command to manually export file systems instead of using entries for them in the /etc/exports file. Export entries will be added to the /var/lib/nfs/xtab file directly. With the -o option, you can list various permissions, and then follow them with the host and file system to export. The host and file system are separated by a colon. For example, to manually export the /home/myprojects directory to golf.mytrek.com with the permissions ro and insecure, you would use the following:

```
exportfs -o rw,insecure golf.mytrek.com:/home/myprojects
```

You can also use exportfs to unexport a directory that has already been exported, either manually or by the /etc/exports file. Just use the -u option with the host and the directory exported. The entry for the export will be removed from the /var/lib/nfs/xtab file. The following example will unexport the /home/foodstuff directory that was exported to lizard.mytrek.com:

```
exportfs -u lizard.mytrek.com:/home/foodstuff
```

# NFS Security: /etc/hosts.allow and /etc/hosts.deny

The /etc/hosts.allow and /etc/hosts.deny files are used to restrict access to services provided by your server to hosts on your network or on the Internet (if accessible). For example, you can use the hosts.allow file to permit access by certain hosts to your FTP server. Entries in the hosts.deny file would explicitly deny access to certain hosts. For NFS, you can provide the same kind of security by controlling access to specific NFS daemons.

> NOTE You can further secure your NFS transmissions by having them operate over TCP instead of UDP. Use the tcp option to mount your NFS file systems (UDP is the default). However, performance does degrade for NFS when it uses TCP.

# Portmapper Service

The first line of defense is to control access to the portmapper service. The portmapper tells hosts where the NFS services can be found on the system. Restricting access does not allow a remote host to even locate NFS. For a strong level of security, you should deny access to all hosts except those that are explicitly allowed. In the hosts.deny file, you would place the following entry, denying access to all hosts by default. ALL is a special keyword denoting all hosts.

```
portmap:ALL
```

In the hosts.allow file, you would then enter the hosts on your network, or any others that you would want to permit access to your NFS server. Again, you would specify the portmapper service, then list the IP addresses of the hosts you are permitting access. You can list specific IP addresses or a network range using a netmask. The following example