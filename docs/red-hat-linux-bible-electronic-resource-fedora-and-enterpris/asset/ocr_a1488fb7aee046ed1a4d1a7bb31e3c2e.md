To begin, open the `/etc/squid/squid.conf` file (as the root user). You will see a lot of information describing the values that you can set in this file. Most of the tags that you need to configure Squid are used to set up cache and provide host access to your proxy server.

> **TIP:** Don't change the *squid.conf.default* file! If you really mess up your *squid.conf* file, you can start again by making another copy of this file to *squid.conf*. If you want to recall exactly what change you have made so far, type the following from the `/etc/squid` directory:
> 
> ```
> # diff squid.conf squid.conf.default | less
> ```
> 
> This will show you the differences between your actual *squid.conf* and the version you started with.

# ## Configuring access control in squid.conf

To protect your computing resources from being used by anyone, Squid requires that you define which host computers have access to your HTTP (Web) services. By default, all hosts are denied access to Squid HTTP services except for the local host. With the `acl` tag, you can create access lists. Then, with the `http_access` tag, you can authorize access to HTTP (Web) services for the access lists you create.

The form of the access control list tag (`acl`) is:

```
```
acl name type string
acl name type file
```
```

The name is any name you want to assign to the list. A `string` is a string of text, and `file` is a file of information that applies to the particular `type` of `acl`. Valid `acl` types include `dst`, `src`, `dstdomain`, `srccdomain`, `url_path_pattern`, `url_pattern`, `time`, `port`, `proto`, `method`, `browser`, and `user`.

Several access control lists are set up by default. You can use these assigned `acl` names to assign permissions to HTTP or ICP services. You can also create your own `acl` names to assign to those services. Here are the default `acl` names from the `/etc/squid/squid.conf` file that you can use or change:

```
```
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
acl SSL_ports port 443 563
acl Safe_ports port 80		# http
acl Safe_ports port 21		# ftp
acl Safe_ports port 443 563	# https, snews
acl Safe_ports port 70		# gopher
acl Safe_ports port 210		# wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280		# gss-http
acl Safe_ports port 488		# gss-http
acl Safe_ports port 591		# filemaker
acl Safe_ports port 777		# multiling http
acl CONNECT method CONNECT
```
```