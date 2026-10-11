The file contains 2 types of entries:

+   * **search.** The domain name in this option is used to complete incomplete host names. For example, if you look up the host name da3, the name is automatically completed to the fully qualified domain name da3.digitalailines.com.

+   * **nameserver.** Every entry starting with nameserver is followed by an IP address of a name server. You can configure up to 3 name servers. If the first name server fails, the next one is used.

# Files Holding the Network Configuration

The following table lists the files used to store the network configuration on RHEL and SUSE Linux Enterprise Server 10. The content of the files is not exactly identical, but the table should nevertheless help you to find the information you are looking for.

| Table 3-1 | RHEL | SLES 10 |
| :--- | :--- | :--- |
| | /etc/sysconfig/networking/devices/ifcfg-ethx, hard-linked to /etc/sysconfig/networking/profiles/default/ifcfg-ethx, and to /etc/sysconfig/network-scripts/ifcfg-ethx. | /etc/sysconfig/network/ifcfg-eth\*-id-macaddress |
| | /etc/sysconfig/networking/profiles/default/hosts, hard-linked to /etc/hosts | /etc/hosts |
| | /etc/sysconfig/networking/profiles/default/resolv.conf, hard-linked to /etc/resolv.conf | /etc/resolv.conf |
| | /etc/nsswitch.conf | /etc/nsswitch.conf |
| | /etc/sysconfig/network | /etc/HOSTNAME |
| | /etc/sysconfig/network-scripts/ | /etc/sysconfig/network/scripts/ |