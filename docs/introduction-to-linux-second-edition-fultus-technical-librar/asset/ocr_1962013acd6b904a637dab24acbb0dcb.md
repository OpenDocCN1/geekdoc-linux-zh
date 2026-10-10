# Introduction to Linux

An example of a standalone network service on your home computer might be the **named** (name daemon), a caching name server. Standalone services have their own processes running, you can check any time using `ps`:

```
bob:~> **ps aux** | **grep** named
named 908 0.0 1.0 14876 5108 ? S Mar14 0:07 named -u named
```

However, there are some services that you can use on your PC, even if there is no server process running for that service. Examples could be the FTP service, the secure copy service or the finger service. Those services have the Internet Daemon (inetd) listening in their place.

# **10.3.1.2 (x)inetd**

On your home PC, things are usually a bit calmer. You may have a small network, for instance, and you may have to transfer files from one PC to another from time to time, using FTP or Samba (for connectivity with MS Windows machines). In those cases, starting all the services which you only need occasionally and having them run all the time would be a waste of resources. So in smaller setups, you will find the necessary daemons dependent on a central program, that listen on all the ports of the services for which it is responsible.

This super-server, the Internet services daemon, is started up at system initialization time. There are two common implementations: **inetd** and **xinetd** (the extended Internet services daemon). One or the other is usually running on every Linux system:

```
bob:~> **ps -ef** | **grep** inet
root 926 1 0 Mar14 7 00:00:00 xinetd -ipv6 -stayalive -reuse \
 -pidfile /var/run/xinetd.pid
```

The services for which the Internet daemon is responsible, are listed in its configuration file, `/etc/inetd.conf`, for **inetd**, and in the directory `/etc/xinetd.d` for **xinetd**. Commonly managed services include file share and print services, SSH, FTP, telnet, the Samba configuration daemon, talk and time services.

As soon as a connection request is received, the central server will start an instance of the required server. Thus, in the example below, when user *bob* starts an FTP session to the local host, an FTP daemon is running as long as the session is active:

```
bob:~> **ps aux** | **grep** ftp
bob 793 0.1 0.2 3960 1076 pts/6 S 16:44 0:00 ncftp localhost
ftp 794 0.7 0.5 5588 2608 ? SN 16:44 0:00 ftpd:
localhost.localdomain: anonymous@bob@his.server.com: IDLE
```

Of course, the same happens when you open connections to remote hosts: either a daemon answers directly, or a remote **(x)inetd** starts the service you need and stops it when you quit.