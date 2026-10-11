# OPTIONS

Following is a list of *options* and their default *values*:

files Specifies the maximum number of map files that *ypserv* caches. Set to 0 to turn off caching. Default is 30.

trusted_master On a slave server, the name/IP address of the master server that new maps will be accepted from. Default is no master server, meaning no new maps are accepted.

xfer_check_port YES (default) requires the master server to run on a *privileged port* (page 1100). NO allows it to run on any port.

# ACCESS RULES

Access rules, which specify which hosts and domains can access which maps, have the following format:

> *host*:*domain*:*map*:*security*

where *host* and *domain* specify the IP address and NIS domain this rule applies to; *map* is the name of the map that this rule applies to; and *security* is either **none** (always allow access), **port** (allow access from a privileged port), or **deny** (never allow access).

The following lines appear in the *ypserv.conf* file supplied with Fedora/RHEL:

```
$ cat /etc/ypserv.conf
```
# Not everybody should see the shadow passwords, not secure, since
# under MSDOG everybody is root and can access ports < 1024 !!!
*       : *        : shadow.byname : port
: *      : passwd.adjunct.byname : port
```
```

These lines restrict the *shadow.byname* and *passwd.adjunct.byname* (the *passwd* map with shadow [asterisk] entries) maps to access from ports numbered less than 1024. As the comment points out, however, anyone using a DOS or early Windows system on the network can read the maps because they can access ports numbered less than 1024.

The following example describes a LAN with some addresses that you want to grant NIS access from and some that you do not; perhaps you have a wireless segment or some public network connections that you do not want to expose to NIS. You can list the systems or an IP subnet that you want to grant access to in *ypserv.conf*. Any-one logging in on another IP address will then be denied NIS services. The following line from *ypserv.conf* grants access to anyone logging in from an IP address in the range of 192.168.0.1 to 192.168.0.255 (specified as 192.168.0.1 with a subnet mask [page 443] of /24):

```
$ cat /etc/ypserv.conf
```
192.168.0.1/24 : * : * : none
```
```