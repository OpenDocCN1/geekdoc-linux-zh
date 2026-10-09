```
# /etc/hosts.equiy before this file, so the definitions in it take
# precedence.
#
# The format of this file is as follows:
#
# [!-]hostnamé
#
# The hostname can be preceded by a '-' character to deny access. If you
# are using NIS, the hostname may be in the form:
#
#+@netgroup
# -@netgroup
#
# where "netgroup" is an NIS netgroup defined in the netgroup map. The
# '+' form allows access to any host in the netgroup, while the '-' form
# denies access to any host in the netgroup.
#
# Lines beginning with a '#' character and blank lines are ignored.
#
# Examples:
#
# host
# -host
#+@group
# -@group
wilma
dino
booboo
banbam
daffy@mydomain.com
```

Communication with remote `lpr` daemons is handled by the **writersrv** subsystem.
If you have trouble communicating with a remote system that is responding to other network services, make certain that the **writersrv** subsystem is running and that it is listening to a socket.

```
# lsarc -s writersrv  ----------------- Verify subsystem is operative
# ps -ef | grep writesrv -------------- Verify process is running
# netstat -a | grep writersrv -------- Verify socket connection is listening
```

# Configuring a Print Server

Since your machine now has a local printer attached to a print queue, it is an easy process to make this server into a print server. The only things that need to be done on the print server side are to add the client machines into the `/etc/hosts.lp` file and to start the `lpd` daemon. You can add entries into the `/etc/hosts.lp` file as hostnames, or you can use the IP address. I prefer not to hard-code any IP addresses