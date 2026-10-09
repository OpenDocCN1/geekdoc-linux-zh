# You can use system-config-firewall to create iptables rules

The **iptables** and **iptables-services** packages do not provide firewall rules. You can use the instructions in this section to configure **iptables** from the command line. Alternatively, you can use **system-config-firewall** (**system-config-firewall** package), a GUI configuration tool for **iptables** rules.

# Prerequisites

You can run the **iptables** service or the **firewalld** service, but not both at the same time. To run **iptables**, make sure the following packages are installed:

+   - **iptables**
+   - **iptables-services**

**Disable firewalld**

Disable the **firewalld** service. The mask command is similar to **disable**, but it makes it impossible to start the service.

```
# systemctl mask firewalld.service
ln -s '/dev/null' '/etc/systemd/system/firewalld.service'
```

**Enable iptables and ip6tables**

Run **systemctl** to cause the **iptables** and **ip6tables** services to start each time the system enters multiuser mode:

```
# systemctl enable iptables.service
# systemctl enable ip6tables.service
```

The **systemctl** utility will not start the **iptables.service** unit unless there is a set of rules for it to load from the **/etc/sysconfig/iptables** file. See “**system-config-firewall**: Generate a Set of Rules” on page 923 for more information about this file. The following file sets up a basic firewall that allows outbound traffic and rejects all incoming traffic except that which is in response to outbound traffic. Copy this sample file to the file named **iptables** to get started.

```
# cat /etc/sysconfig/iptables
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```

You can save and reload **iptables** rules as explained in “Saving rules” on page 914.

**Stop firewalld**

Stop the firewalld service.

```
# systemctl stop firewalld.service
```

**Start iptables and ip6tables**

Next, run **systemctl** to start the **iptables** and **ip6tables** services.

```
# systemctl start iptables.service
# systemctl start ip6tables.service
```