The fourth line from the bottom of the example on the preceding page shows that this query took 496 milliseconds (about one-half of a second). When you run the same query again, it runs more quickly because the DNS cache has saved the information locally in memory:

```
```
$ dig www.ubuntu.com
...
;; Query time: 1 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Mon Apr 5 16:45:46 2010
;; MSG SIZE rcvd: 112
```
```

# ## CONFIGURING A DNS SERVER

This section discusses the `/etc/bind/named.conf` file, zone files, implementation of a DNS cache, and running DNS inside a chroot jail.

# ### named.conf: The named Configuration File

Configuration information for **named** is kept in `/etc/bind/named.conf`. By default, the zone files reside in `/etc/bind`. If you are running **named** in a chroot jail, these files are kept in `/var/lib/named/etc/bind`, with a link in `/etc/bind` (page 847).

# #### Try not to modify named.conf

> > **tip** The Ubuntu **bind9** package breaks the **named.conf** file distributed with BIND into four files: **named.conf**, **named.conf.default-zones**, **named.conf.local**, and **named.conf.options**. There are two motivations for breaking this file apart. First, it makes the configuration files easier to understand. Second, it enables you to configure **named** without modifying **named.conf**. This setup allows the **bind9** package to be upgraded, including changes to **named.conf**, without requiring you to modify the local configuration.

When you configure **named**, try to put your changes in the **named.conf.options** and **named.conf.local** files. For more complex setups it may be easier to modify **named.conf** and carry those changes forward when **bind9** is upgraded.

# #### IP-list

In the descriptions for breaking this section, **IP-list** is a semicolon-separated list of IP addresses, where each IP address is optionally followed by a slash and a subnet mask length (page 462). Prefix an *IP-list* with an exclamation point (!) to negate it. Built-in names you can use in *IP-list* include **any**, **none**, and **localhost**. You must enclose these built-in names within double quotation marks.

# #### COMMENTS

Within **named.conf**, specify a comment by preceding it with a hashmark (\#) as in a Perl or shell program, preceding it with a double slash (//) as in a C++ program, or