4. Make the new settings persistent:

```
~/# firewall-cmd --runtime-to-permanent
```

# 5.11.4. Configuring the ICMP Filter using GUI

To enable or disable an **ICMP** filter, start the **firewall-config** tool and select the network zone whose messages are to be filtered. Select the **ICMP Filter** tab and select the check box for each type of **ICMP** message you want to filter. Clear the check box to disable a filter. This setting is per direction and the default allows everything.

To edit an **ICMP** type, start the **firewall-config** tool and select **Permanent** mode from the menu labeled **Configuration**. Additional icons appear at the bottom of the **Services** window. Select **Yes** in the following dialog to enable masquerading and to make forwarding to another machine working.

To enable inverting the **ICMP Filter**, click the **Invert Filter** check box on the right. Only marked **ICMP** types are now accepted, all other are rejected. In a zone using the **DROP** target, they are dropped.

# 5.12. SETTING AND CONTROLLING IP SETS USING FIREWALLD

To see the list of IP set types supported by **firewalld**, enter the following command as **root**.

```
~/# firewall-cmd --get-ipset-types
hash:ip hash:ip,mark hash:ip,port hash:ip,port,ip hash:ip,port,net
hash:mac hash:net hash:net,iface hash:net,net hash:net,port
hash:net,port,net
```

# 5.12.1. Configuring IP Set Options with the Command-Line Client

IP sets can be used in **firewalld** zones as sources and also as sources in rich rules. In **Red Hat Enterprise Linux 7**, the preferred method is to use the IP sets created with **firewalld** in a direct rule.

To list the IP sets known to **firewalld** in the permanent environment, use the following command as **root**:

```
~/# firewall-cmd --permanent --get-ipsets
```

To add a new IP set, use the following command using the permanent environment as **root**:

```
~/# firewall-cmd --permanent --new-ipset=test --type=hash:net
success
```

The previous command creates a new IP set with the name **test** and the **hash:net** type for **IPv4**. To create an IP set for use with **IPv6**, add the `--option=family=inete6` option. To make the new setting effective in the runtime environment, reload **firewalld**. List the new IP set with the following command as **root**:

```
~/# firewall-cmd --permanent --get-ipsets
test
```