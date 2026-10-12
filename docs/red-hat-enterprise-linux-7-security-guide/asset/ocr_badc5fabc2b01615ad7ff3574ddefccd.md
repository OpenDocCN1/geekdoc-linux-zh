```
~/# firewall-cmd --add-forward-port=port=<port-number>:proto=tcp|udp|sctp|dccp:toport=<port-number>
```

To redirect a port to another port at a different IP address:

+   1. Add the port to be forwarded:

```
~/# firewall-cmd --add-forward-port=port=<port-number>:proto=tcp|udp:toport=<port-number>:toaddr=<IP/mask>
```

+   2. Enable masquerade:

```
~/# firewall-cmd --add-masquerade
```

# Example 5.1. Redirecting TCP Port 80 to Port 88 on the Same Machine

To redirect the port:

+   1. Redirect the port 80 to port 88 for TCP traffic:

```
~/# firewall-cmd --add-forward-port=port=80:proto=tcp:toport=88
```

+   2. Make the new settings persistent:

```
~/# firewall-cmd --runtime-to-permanent
```

+   3. Check that the port is redirected:

```
~/# firewall-cmd --list-all
```

# 5.9.2. Removing a Redirected Port

To remove a redirected port:

```
~/# firewall-cmd --remove-forward-port=port=<port-number>:proto=
<tcp|udp>:toport=<port-number>:toaddr=<IP/mask>
```

To remove a forwarded port redirected to a different address:

+   1. Remove the forwarded port:

```
~/# firewall-cmd --remove-forward-port=port=<port-number>:proto=
<tcp|udp>:toport=<port-number>:toaddr=<IP/mask>
```

+   2. Disable masquerade:

```
~/# firewall-cmd --remove-masquerade
```