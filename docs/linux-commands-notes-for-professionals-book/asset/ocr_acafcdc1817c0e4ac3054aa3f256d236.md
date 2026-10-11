# **Static configuration(Temporary change) using `ifconfig` utility**

A static IP address could be added to an interface using the `ifconfig` utility as follows

```
$ `ifconfig` <interface> <ip-address>/<mask> up
```

Example:

```
$ `ifconfig` eth0 10.10.50.100/16 up
```