in on another IP address will then be denied NIS services. The following line from `ypserv.conf` grants access to anyone logging in from an IP address in the range of 192.168.0.1 to 192.168.0.255 (specified as 192.168.0.1 with a network mask [page 483] of /24):

```
$ cat /etc/ypserv.conf
...
192.168.0.1/24 : * : * : none
```

# /var/yp/securenets: Enhances Security

To enhance system security, you can create the `/var/yp/securenets` file, which prevents unauthorized systems from sending RPC requests to the NIS server and retrieving NIS maps. Notably `securenets` prevents unauthorized users from retrieving the `shadow` map, which contains encrypted passwords. When `securenets` does not exist or is empty, an NIS server accepts requests from any system.

Each line of `securenets` lists a netmask and an IP address. NIS accepts requests from systems whose IP addresses are specified in `securenets`; it ignores and logs requests from other addresses. You must include the (local) server system as `localhost` (127.0.0.1) in `securenets`. A simple `securenets` file follows:

```
$ cat /var/yp/securenets
# you must accept requests from localhost
255.255.255.255 127.0.0.1
#
# accept requests from IP addresses 192.168.0.1 - 192.168.0.62
255.255.255.192 192.168.0.0
#
# accept requests from IP addresses starting with 192.168.14
255.255.255.0 192.168.14.0
```

# /var/yp/Makefile: Creates Maps

The `make` utility, which is controlled by `/var/yp/Makefile`, uses `makedb` to create the NIS maps that hold the information distributed by NIS. When you run `ypinit` (page 784) on the master server, `ypinit` calls `make`. You do not need to run `make` manually. Edit `/var/yp/Makefile` to set options and specify which maps to create. The following sections discuss `/var/yp/Makefile` in more detail.

# VARIABLES

Following is a list of variables you can set in `/var/yp/Makefile`. The values following Fedora/RHEL are the values set in the file distributed by Fedora/RHEL.

+   B Do not change.
+   Fedora/RHEL: not set

+   NOPUSH Specifies that `ypserv` is not to copy (push) maps to slave servers. Set to `TRUE` if you do not have any slave NIS servers; set to `FALSE` to cause NIS to copy maps to slave servers.
+   Fedora/RHEL: TRUE