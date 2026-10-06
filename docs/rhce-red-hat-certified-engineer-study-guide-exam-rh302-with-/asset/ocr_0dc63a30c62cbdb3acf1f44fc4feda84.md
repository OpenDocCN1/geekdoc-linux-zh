# 578 Chapter 23 • Understanding Secondary Network Services

# does not have the prefer keyword, this driver is never
# used for synchronization, unless no other other
# synchronization source is available. In case the local
# host is controlled by some external source, such as an
# external oscillator or another protocol, the prefer
# keyword would cause the local host to disregard all
# synchronization sources, unless the kernel modifications
# are in use and declare an unsynchronized condition.

```
server 128.173.14.71 # vt.edu
server 140.247.60.28 # harvard.edu
server 165.227.1.1 # scruz.net
server 131.216.16.9 # unlvdu
server 127.127.1.0 # local clock
fudge 127.127.1.0 stratum 10
```

```
restrict default ignore
restrict 199.184.237.129
restrict 128.173.14.71
restrict 140.247.60.28
restrict 165.227.1.1
restrict 131.216.16.9
restrict 192.168.0.0 mask 255.255.255.0
restrict 127.0.0.0 mask 255.255.255.0
```

# Drift file. Put this in a directory which the daemon can
# write to. No symbolic links allowed, either, since the
# daemon updates the file by creating a temporary in the
# same directory and then rename()ing it to the file.

```
driftfile /etc/ntp/drift
#multicastclient # listen on default
2224.0.1.1
#broadcastdelay 0.008
```

# Authentication delay. If you use, or plan to use
# someday, the authentication facility you should make the
# programs in the auth_stuff directory and figure out what
# this number should be on your machine.

authenticate no

# Keys file. If you want to doodle your server at run
# time, make a keys file (mode 600 for sure) and define the
# key number to be used for making requests.

Copyright©2000 SYBEX, Inc., Alameda, CA www.sysex.com