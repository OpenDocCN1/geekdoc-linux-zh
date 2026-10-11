# ### Setting pppd Options

The `/etc/ppp/options` file is used to set options that govern pppd. The package ships with a template file, named `options.tpl`, but Red Hat and others don't include it. The `/etc/ppp/options` file shown in Listing 4.2 will do for most purposes.

# Listing 4.2  The pppd Options File

```
# /etc/ppp/options
#
# Prevent pppd from forking into the background
-detach
#
# use the modem control lines
modem
# use uucp style locks to ensure exclusive access to the serial device
lock
# use hardware flow control
crtscts
# create a default route for this connection in the routing table
defaultroute
# do NOT set up any "escaped" control sequences
asyncmap 0
# use a maximum transmission packet size of 552 bytes
mtu 552
# use a maximum receive packet size of 552 bytes
mru 552
#
# force pppd to use your ISP user name as your 'host name' during the
# authentication process
name username
#
# If you are using ENCRYPTED secrets in the /etc/ppp/pap-secrets
# file, then uncomment the following line.
#-papcrypt
```

The exam doesn't make much of the contents of this file, focusing more on the steps needed to make a connection.

# ### Authentication Options

PPP doesn't restrict who can connect from a client to a server because it's not designed to. Without authentication mechanisms such as PAP and CHAP, getting access to a machine over PPP is easy.

Linux supports the following protocols for authentication:

> **Password Authentication Protocol (PAP)** —This protocol provides clear text authentication.
>
> **Challenge Handshake Authentication Protocol (CHAP)** —With this protocol, passwords are never sent unencrypted.