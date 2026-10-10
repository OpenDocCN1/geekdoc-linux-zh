![](bbox=[0.08, 0.06, 0.92, 0.45])

fwbuilder will generate a script configuring the firewall according to the rules that you have defined. Its modular architecture gives it the ability to generate scripts targeting different systems including iptables for Linux, ipf for FreeBSD, and pf for OpenBSD.

# 7.4.4. Installing the Rules at Each Boot

In order to implement the firewall rules each time the machine is booted, you will need to register the configuration script in an up directive of the /etc/network/interfaces file. In the following example, the script is stored under /usr/local/etc/arrakis.fw.

```
```
auto eth0
iface eth0 inet static
  address 192.168.0.1
  network 192.168.0.0
  netmask 255.255.0.255
  broadcast 192.168.0.255
  up /usr/local/etc/arrakis.fw
```
```