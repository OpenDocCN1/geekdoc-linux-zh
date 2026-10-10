Configuring access control in squid.conf

To protect your computing resources from being used by anyone, Squid requires that you define which host computers have access to your HTTP (Web) services. By default, all hosts are denied access to Squid HTTP services except for the local host. With the `acl` tag, you can create access lists. Then, with the `http_access` tag, you can authorize access to HTTP (Web) services for the access lists you create.

The form of the access control list tag (`acl`) is:

```
```
acl name type string
acl name type file
```
```

The `name` is any name you want to assign to the list. `A string` is a string of text, and `file` is a file of information that applies to the particular `type` of `acl`. Valid `acl` types include `dst`, `src`, `dstdomain`, `srcdomain`, `url_path_pattern`, `url_pattern`, `time`, `port`, `proto`, `method`, `browser`, and `user`.

Several access control lists are set up by default. You can use these assigned `acl` names to assign permissions to HTTP or ICP services. You can also create your own `acl` names to assign to those services. Here are some of the default `acl` names from the `/etc/squid/squid.conf` file that you can use or change:

```
```
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object

acl localhost src 127.0.0.1/255.255.255.255
acl localhost src 10.0.0.0/8 # RFC1918 possible internal network
acl localnet src 172.16.0.0/12 # RFC1918 possible internal network
acl localnet src 192.168.0.0/16 # RFC1918 possible internal network
acl SSL_ports port 443 563
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 563 # https, snews
acl Safe_ports port 70 # gopher
acl Safe_ports port 210 # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280 # http-mgmt
acl Safe_ports port 488 # gss-http
acl Safe_ports port 591 # filmmaker
acl Safe_ports port 777 # multi-ling http
acl CONNECT method CONNECT
```
```

When Squid tries to determine which class a particular computer falls in, it goes from top to bottom. In the first line, all host computers (address/netmask are all zeros) are added to the `acl` group `all`. In the second line, you create a manager group called `manager` that has access to your `cache_object` (the capability to get content from the cache). The group `localhost` is assigned to your loopback address. Secure socket layer (SSL) ports are