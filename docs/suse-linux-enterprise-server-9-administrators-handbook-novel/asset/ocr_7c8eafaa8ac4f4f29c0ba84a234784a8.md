# LISTING 8.2
The Default `/etc/ntp.conf` File (continued)

```
##
server 127.127.1.0  # local clock (LCL)
fudge 127.127.1.0  stratum 10  # LCL is unsynchronized

##
## Outside source of synchronized time
##
## server xx.xx.xx.xx      # IP address of server

##
## Miscellaneous stuff
##

driftfile /var/lib/ntp/drift/ntp.drift  #path for drift file

logfile /var/log/ntp       # alternate log file
# logconfig=syncstatus + sysevents
# logconfig=all

# statsdir /tmp/        # directory for statistics files
# filegen peerstats  file peerstats type day enable
# filegen loopstats  file loopstats type day enable
# filegen clockstats file clockstats type day enable

#
# Authentication stuff
#
# keys /etc/ntp.keys              # path for keys file
# trustedkey 1 2 3 4 5 6 14 15  # define trusted keys
# requestkey 15                  # key (15) for accessing server variables
# controlkey 15                  # key (6) for accessing server variables
```

You can make a simple client configuration by adding the list of NTP time servers that you want `ntpd` to contact:

```
##
## Outside source of synchronized time
##
server 10.1.1.1 prefer          # IP of local time server
server time.nrc.ca              # DNS name of Ottawa server
server dense.utcc.utoronto.ca   # University of Toronto
#server ntp-1.nrc.ca            # Pennsylvania state
#server timeb.cs.columbia.edu   # New York state
#server tick.ijr.us             # New Jersey state
```