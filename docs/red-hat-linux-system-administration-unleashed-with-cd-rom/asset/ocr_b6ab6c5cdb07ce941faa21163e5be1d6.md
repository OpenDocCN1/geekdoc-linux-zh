# LISTING 26.1 continued

```
# <service_name> <sock_type> <proto> <flags> <user> <server_path> <args>
#
#
# These are standard services.
ftp stream tcp nowait root /usr/local/etc/ftp-gw /usr/local/etc/ftp-gw
telnet stream tcp nowait root /usr/local/etc/tn-gw /usr/local/etc/tn-gw
ssh stream tcp nowait root /usr/local/etc/plug-gw plug-gw sshd
ssh-a stream tcp nowait root /usr/local/etc/netacl sshd
#
# Ident service is used for net authentication
auth stream tcp nowait root /usr/local/etc/plug-gw /usr/sbin/in.identd
#
# End of inetd.conf.
```

The plug-gw file is as follows:

```
#
# Secure Shell and identd gateway
#
plug-gw: -port ssh * -plug-to <ssh_server> -port ssh
plug-gw: -port 113 * -plug-to <mail_server> -port 113
```

The plug-gw section of netperm-table tells the firewall to forward connection on port 22 over to the secure shell server's ssh port (that is, port 22). For identd, any identd connections are sent over to the mail server because it is the most logical place to run identd.

Now let's take a closer look at the ssh-a line. This is a special port being reserved for administrative secure shell into the firewall machine. For example, sshd normally runs off of port 22. However, for this example, sshd will run on port 38. In order for inetd to understand this, the /etc/services file will need the entry:

```
ssh tcp/38   ssh # Administrative Secure Shell added.
```

Setting up a proxy server requires much more work than a simple packet filter firewall. However, a proxy server goes a very long way toward making the network more accessible and the firewall more tolerable for the users. Now that we have discussed how to set up proxy services across a firewall, we can turn our attention toward setting up the firewall itself.