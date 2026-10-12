```
# workgroup = NT-Domain-Name or Workgroup-Name
    workgroup = MYGROUP

# server string is the equivalent of the NT
# Description field
    server string = Samba Server

# This option is important for security.
# It allows you to restrict connections to machines
# which are on your local network. The following
# example restricts access to two C class networks and
# the "loopback" interface. For more examples of
# the syntax see
# the smb.conf man page
;   hosts allow = 192.168.1. 192.168.2. 127.

# if you want to automatically load your printer list rather
# than setting them up individually then you'll need this
    printcap name = /etc/printcap
    load printers = yes

# It should not be necessary to spell out the print system type unless
# yours is non-standard. Currently supported print systems include:
# bsd, sysv, plp, lprng, aix, hpux, qnx
    printing = lprng

# Uncomment this if you want a guest account, you must add this to /etc/passwd
# otherwise the user "nobody" is used
;   guest account = pcguest

# this tells Samba to use a separate log file for each machine
# that connects
    log file = /var/log/samba/%m.log
```