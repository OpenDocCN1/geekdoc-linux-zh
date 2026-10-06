# Special Installations 191

```
mouse genericps/2
timezone US/Pacific
xconfig --server "SVGA" --monitor "viewsonic17gs"
auth --usershadow --enablemd5
lilo --location mbr --linear
%packages
setup
filesystem
nbasesystem
...and so on...
%post
```

# Editing the Configuration File

The configuration file requires some revision before it can be used. Notice that the network line is commented out. You should remove the comment character (#) and revise the IP number, netmask, and gateway. If you want the system to obtain its network configuration via BOOTP or DHCP, specify the following directive:

```
network --bootproto BOOTP
```

or

```
network --bootproto DHCP
```

Table 8.4 describes the other directives shown in the same configuration and a few additional directives you may find useful. Consult the kickstart documentation on the documentation CD-ROM, especially The Official Red Linux Reference Guide, to learn more about these and other kick-directives.

# TABLE 8.4 Kickstart Directives

| Directive | Meaning |
| auth --usershadow --enablemd5 | Specifies that shadow passwords and MD5 encryption are to be used. |
| cdrom | Specifies that the installation media is on a local CD-ROM. |
| clearpart --all | Specifies that all existing partitions should be deleted. |