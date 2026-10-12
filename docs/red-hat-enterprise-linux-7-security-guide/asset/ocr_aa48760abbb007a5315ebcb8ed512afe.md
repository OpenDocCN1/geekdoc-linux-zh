In case of the IPv6 protcol the firewalld daemon applies to Reverse Path Forwarding by default. The setting can be checked in the `/etc/firewalld/firewalld.conf` file. You can change the firewall behavior by setting the `IPv6_rpfilter` option.

If you need a custom configuration of Reverse Path Forwarding, you can perform it *without* the *firewalld* daemon by using the `ip6tables` command as follows:

```
`ip6tables -t raw -I PREROUTING -m rpfilter --invert -j DROP`
```

This rule should be inserted near the beginning of the raw/PREROUTING chain, so that it applies to all traffic, in particular before the stateful matching rules. For more information about the `iptables` and `ip6tables` services, see Section 5.13, “Setting and Controlling IP sets using iptables”.

# Enabling Packet Forwarding

To enable packets arriving from outside of a system to be forwarded to another external host, IP forwarding must be enabled in the kernel. Log in as **root** and change the line which reads `net.ipv4.ip_forward = 0` in the `/etc/sysctl.conf` file to the following:

```
`net.ipv4.ip_forward = 1`
```

To load the changes from the `/etc/sysctl.conf` file, enter the following command:

```
`/sbin/sysctl -p`
```

To check if IP forwarding is turned on, issue the following command as **root**:

```
`/sbin/sysctl net.ipv4.ip_forward`
```

If the above command returns a `1`, then IP forwarding is enabled. If it returns a `0`, then you can turn it on manually using the following command:

```
`/sbin/sysctl -w net.ipv4.ip_forward=1`
```

# 4.4.3.2. Additional Resources

The following are resources which explain more about Reverse Path Forwarding.

+   - **Installed Documentation**
+   
+   `/usr/share/doc/kernel-doc-version/Documentation/networking/ip-sysctl.txt` - This file contains a complete list of files and options available in the directory. Before accessing the kernel documentation for the first time, enter the following command as **root**:
+   
+   ``` ~]# yum install kernel-doc ```
+   - **Online Documentation**
+   
+   See RFC 3704 for an explanation of Ingress Filtering for Multihomed Networks.