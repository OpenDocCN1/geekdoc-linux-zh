# Configure BIND to Not Display Version Information

Edit the BIND configuration file, named.conf, and override the version number:

```
options { version "Not available"; }
```

You might also want to configure BIND with specific ACLs and limit queries from specific hosts. See the BIND documentation for details. More information about BIND can be found at http://www.isc.org/products/BIND/.

# Finger: 79 (TCP)

Finger is a user information lookup program. Fingering a remote host will provide information such as usernames, IP addresses, idle time, and real names of the individuals logged on the host at the time.

# Enumerate Remote Users by Using the Finger Command

If the remote host is running a finger daemon, the command-line finger tool can be used to query the host:

```
finger @host
```

Example:

```
[bash]$ finger @192.168.1.1
Login    Name          TTY     Idle   When     Where
bob      Bob             pts/1    8     Wed 14:26   bobaddress.bobsisp.org
rob      Robert Smith    pts/4   51     Wed 12:46   dhcp.robshomeisp.org
tang     Thomas Tang     pts/3   1:08   Wed 10:07   somecasanexample.com
```

It is also possible to finger a specific username. Querying for a specific username will yield some information about the user even if the user is not logged on at the time:

```
finger username@host
```

Example:

```
[bash]$ finger root@192.168.1.1
Login name:  root        In real life: Sys Admin
Directory: /        Shell: /usr/local/bin/tcsh
Last login Jan 11 14:26:51 on tty2
```