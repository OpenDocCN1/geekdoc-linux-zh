# 16.10.7.4 The in_nolocal Attribute

As you (hopefully) recall, a cluster alias provides an additional IP address through which access to cluster services may be gained. You may want to restrict access to a service such that the clients must use a cluster alias to get access to the service. Attaching the in_nolocal attribute to a service indicates that there should be no access to the service unless the alias is used. This means that use of any of the member’s local IP interface addresses (or node names) will not provide access to any service with the in_nolocal attribute.

The following example first shows successful client access to a service using a cluster alias, and then shows an unsuccessful attempt due to the in_nolocal attribute having been applied to the tftp service.

From the client system:

```
# rah sheridan grep tftp /etc/clus_services
 tftp 69/udp in_multi;in_nolocal
```

Get some tftp activity going using the cluster alias. Works like a charm.

```
# tftp babylon5 -g /tftp/big1 /dev/null &
[1] 5182
```

```
# rah molari ps -A | grep tftp | grep -v grep
1049867 ?? S 0:00.00 tftpd /tftp
```

Try to get some tftp activity going using a member name. No luck because of the in_nolocal attribute.

```
# tftp sheridan -g /tftp/big1 /dev/null &
[1] 5202
```

```
# rah sheridan ps -A | grep tftp | grep -v grep
```

# 16.10.7.5 The out_alias Attribute

When communication takes place between nodes in a network, the nodes will identify themselves in the IP header with an IP address that is in use on the sending node. This would normally be the IP address associated with a local interface and not the IP address associated with a cluster alias. In the case where various authentication mechanisms may be in place, these mechanisms may function better if the sending node’s (actually a cluster member’s) IP address is the IP address associated with

```
# rah molari ps -A | grep tftp | grep -v grep
1049745 ?? S 0:01.70 tftpd /tftp
```