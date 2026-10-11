# ## Additional Network Security Considerations

While most daemons are started from inetd and /etc/rc.d, there are also a number of places within your server that you should be watching. These include mostly configuration files for network services, which should be audited in the event that a service is unintentionally started. For example, special attention should be paid to rhosts authentication, the portmapper daemon, and services started as chroot. The next three sections of this chapter describe each of these topics in detail.

# ### Disabling rhosts authentication

Although most current Linux distributions no longer come configured for this type of authentication, a few older systems may still be vulnerable. First and foremost, make sure that your inetd.conf file does not include support for the rlogin daemon. The command

```
```
[ramon]$ grep rlogin /etc/inetd.conf
```
```

should not return anything. If you do have rlogin enabled, simply delete (or comment out) the offending line and restart the inetd daemon. The r series of remote access commands (rsh, rlogin, rcp) are riddled with security holes and should not be used.

In addition, look for the /etc/hosts.equiv file, or an .rhosts file in any home directory. If there is one, remove or rename it immediately. If this file contains a host name definition (or IP address), users on that host will be able to rlogin to your server without being prompted for a password if you accidentally leave rlogin running. This is the ultimate vulnerability, and it’s the main reason why the r commands should never be used.

Use the following command as the root user to periodically weed out all .rhosts files from users’ home directories:

```
```
[ramon]$ sudo find /home -name ".rhosts" -exec rm {} \;
```
```

# ### The portmap Daemon and RPC Services

The portmapper (portmap) is the network service that enables remote procedure call (RPC) facilities such as Network File Systems (NFS) for file sharing and Network Information Services (NIS or “yellow pages”) for name resolution. Started from /etc/rc.d, the portmap daemon listens to local RPC servers, which register their port numbers with the portmap services. (Unlike regular inetd-driven services, RPC programs don’t bind to a fixed TCP/UDP port.) Remote clients that wish to use an RPC service contact the portmap first, which then returns the port number where the RPC daemon can be reached.

RPC-based services can be extremely vulnerable to malicious attacks, especially when the intruder registers a bogus RPC service remotely and asks portmap to listen for requests to