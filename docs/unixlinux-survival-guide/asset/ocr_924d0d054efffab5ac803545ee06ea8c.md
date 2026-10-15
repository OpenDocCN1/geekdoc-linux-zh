```
#finger stream tcp6 nowait nobody /usr/sbin/in.fingerd
in.fingerd
...
# RWALLD - rwall daemon (allows others to post messages to users)
#walld/1 tli rpc/datagram_v wait root
/usr/lib/netserv/rwall/rpc.rwalld rpc.rwalld
...
# FTPD - FTP server daemon
#ftp stream tcp6 nowait root /usr/sbin/in.ftpd
in.ftpd -a
...
```

These are three examples for deactivated services in /etc/inetd.conf. You just need to put the # sign at the beginning of the line and that line will be considered a comment from now on. If you restart either inetd or xinetd, then the services will not be available. If xinetd is used, then /etc/inetd.conf is one of two ways to configure the system. The program usually uses the file /etc/xinetd.conf for global settings and the configuration files in /etc/xinetd.d to configure the different services. These services can be turned off or on in the respective configuration file by using either disable = yes or disable = no. If there should be an active connection, then restarting the daemon is not enough to terminate this connection; you need to stop all waiting daemons by hand. Making sure that all services started by xinetd are really off is one of the rare situations that warrants a reboot if possible. The finger service hails from the time when most of the population on the old ARPAnet was trustworthy; it is rarely used these days and should be shut down. The name rwall comes from write to all and is a quick way of notifying all users on a given system. Again, if you do not know it or make use of it, it should be turned off. Shutting down the last service, ftpd, could pose a problem. Even if the machine is not used as a server, chances are at least some users use the protocol to transfer files to and from their accounts. If that should be the case, it is your job to convince the users to use scp instead because ftp transfers passwords and everything else as clear text. System administrators should always make sure that the systems do not react to requests for services that should not be available in the first place. A quick nmap scan might reveal interesting ports that could be turned off.

One type of incident makes news more often than it should—breaking into a system through the use of accounts of former users. What holds true for unused ports holds equally true for unused user accounts: if you do not use it, turn it off. It is amazing how simple it is to gather information about possible user accounts, especially accounts that are not in use anymore. It takes just a bit of social engineering to get hold of this information. It is not even bad intention most of the time. Look at this subject from another perspective: what happens to paper that is not used anymore? Will it be shredded to make it harder to gain information from it?