```
# seconds.
#chap-interval <n>
# With this option, pppd will accept the peer's idea of our local IP
# address, even if the local IP address was specified in an option.
#ipcp-accept-local
# With this option, pppd will accept the peer's idea of its (remote)
# IP address, even if the remote IP address was specified in an
# option.
#ipcp-accept-remote
```

# What Options Should I Use? (No PAP/CHAP

Well, as in all things, that depends (sigh). The options specified here should work with most servers.

However, if it does not work, read the template file (/etc/ppp/ options.tpl) and the pppd man pages and speak to the sysadmin/user support people who run the server to which you are connecting.

You should also note that the connect scripts presented here also use some command line options to pppd to make things a bit easier to change.

```
# /etc/ppp/options (NO PAP/CHAP)
#
# Prevent pppd from forking into the background
# -detach
#
# use the modem control lines
modem
#
# use uucp style locks to ensure exclusive access to the serial
device
lock
#
# use hardware flow control
crcts
#
# create a default route for this connection in the routing table
defaultroute
#
# do NOT set up any 'escaped' control sequences
asyncmap 0
#
# use a maximum transmission packet size of 552 bytes
mtu 552
#
# use a maximum receive packet size of 552 bytes
mru 552
#
#------END OF SAMPLE /etc/ppp/options (no PAP/CHAP)
```