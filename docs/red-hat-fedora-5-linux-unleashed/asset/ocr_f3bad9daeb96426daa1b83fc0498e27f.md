The first entry is for the loopback entry. The second is for the name of the machine. The third is another machine on the network. If no naming service is in use on the network, the only host that myhost will recognize by name is yourhost. (IP addresses on the network can still be used.)

If your network is using a naming service, the last line is not needed and can be deleted. However, if myhost connects to yourhost frequently, it might be good to leave the entry so that myhost does not need to consult the naming service each time. This can save time and reduce the strain on the network or the name service server. Edit this file if you need to change your hostname or IP address or if you aren't using a naming service and a host has been added to your network.

# Service Settings in /etc/services

The /etc/services file maps port numbers to services. The first few lines look similar to this (the /etc/services file can be quite long, more than 500 lines):

```
# Each line describes one service, and is of the form:
#
# service-name port/protocol [aliases ...] [# comment]

tcpmux 1/tcp # TCP port service multiplexer
tcpmux 1/udp # TCP port service multiplexer
rje 5/tcp # Remote Job Entry
rje 5/udp # Remote Job Entry
echo 7/tcp
echo 7/udp
discard 9/tcp sink null
discard 9/udp sink null
systat 11/tcp users
```

Typically, there are two entries for each service because most services can use either TCP or UDP for their transmissions. Usually after /etc/services is initially configured, you will not need to change it.

# Using /etc/nsswitch.conf After Changing Naming Services

This file was initially developed by Sun Microsystems to specify the order in which services are accessed on the system. A number of services are listed in the /etc/nsswitch.conf file, but the most commonly modified entry is the hosts entry. A portion of the file can look like this:

```
passwd: files
shadow: files
group: files

#hosts: db files nisplus nis dns
hosts: files dns
```