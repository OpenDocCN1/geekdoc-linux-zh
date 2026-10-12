```
#icmdir yp.radiostation.de
#directory yp.icecast.org
touch_freq 5
```

```
########## Server IP/port configuration (IMPORTANT) ############
#hostname 192.168.1.1
port 8000
server_name icecast.ksl.com
```

```
################### Main Server Logfile ####################
logfile icecast.log
accessfile access.log
usagefile usage.log
logfiledebuglevel 0
consoledebuglevel 0
```

```
################### Reverse Lookups ####################
# Set this to 1 if you want ip:s to be looked up (using reverse lookup)
# or 0 if you just want the ip:s (which is slightly faster)
reverse_lookups 0
```

```
################### Console mode ####################
# Use 0 if you want stdin to become a local admin console with log tailing
# Use 1 if you want stdin to become a local admin console
# Use 2 if you just want the console to become a log window
# Use 3 if you want the icecast server to be launched in the background (not available for Win32)
console_mode 0
```

```
################### Client Timeout ####################
# (How to deal with clients when no encoder is connected)
# A negative value means keep them forever
# 0 (zero) means kick them out instantly
# X > 0 means keep them X seconds
client_timeout 30
```