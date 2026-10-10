This first line in this file specifies that TCP/IP networking is enabled, but the second turns IP forwarding off. These settings are appropriate for a single-user workstation that is connected to a LAN or the external Internet. The HOSTNAME line specifies the name of this computer as it is defined for TCP/IP purposes. The GATEWAY line contains the IP address of the gateway device, if any, that is used to access the external Internet. This line is not needed if you are accessing the Internet by means of a modem.

# **/etc/hosts**

One of several essential TCP/IP configuration files, /etc/hosts indicates the IP addresses of the computer's loopback interface and that of the default network interface. A typical /etc/hosts file looks like the following:

```
```
127.0.0.1     localhost.localdomain   localhost
192.168.100.10 lorthlorien.mydomain.org lorthlorien
```
```

For each line, the first column indicates the IP address (such as 127.0.0.1). The second indicates the fully qualified domain name (FQDN) of the host that is being defined (for the loopback interface, localhost.localdomain is the default). The third column indicates aliases that can be used to refer to this host.

If you are setting up a small, internal network and do not wish to run a DNS server, you can configure your network by adding to this file all the IP addresses, FQDNs, and aliases of the machines on your network. The following defines a network with five hosts in addition to the local host:

```
```
127.0.0.1     localhost.localdomain   localhost
192.168.100.10 lorthlorien.mydomain.org lorthlorien
192.168.100.11 rivendell.mydomain.org rivendell
192.168.100.12 gondor.mydomain.org   gondor
192.168.100.13 mordor.mydomain.org   mordor
192.168.100.14 laserjet.mydomain.org laserjet
```
```