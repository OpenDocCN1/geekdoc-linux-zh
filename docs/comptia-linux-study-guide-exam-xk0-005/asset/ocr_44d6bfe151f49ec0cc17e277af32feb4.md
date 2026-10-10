# Tunneling Your X11 Connection

Another method that provides remote GUI interactions within a secure tunnel is X11 forwarding. X11 forwarding allows you to interact with various X11-based graphical utilities on a remote system through an encrypted network connection. This method is also enacted using the OpenSSH service.

First you need to see if X11 forwarding is permitted. This setting is in the OpenSSH configuration file, /etc/ssh/sshd_config. The directive X11Forwarding should be set to yes in the remote system's configuration file. If the directive is set to no, then you must modify it to employ X11 forwarding. In Listing 8.3, a check is performed on the configuration file for this directive on a CentOS distribution.

# Listing 8.3 Checking the AllowTCPForwarding directive

```
```
grep "X11Forwarding yes" /etc/ssh/sshd_config
X11Forwarding yes
# 
```
```

Once you have made any necessary configuration file modifications, the command to use is ssh -X user@remote-host. Similar to earlier ssh command uses, user is the user account that resides on the remote-host system. remote-host has the GUI utilities you wish to employ and can be designated via an IP address or a hostname. Figure 8.10 shows connecting from a remote Fedora client to a CentOS server and using a graphical utility on that server.

# FIGURE 8.10 Forwarding X11

![](bbox=[0.15, 0.56, 0.85, 0.94])