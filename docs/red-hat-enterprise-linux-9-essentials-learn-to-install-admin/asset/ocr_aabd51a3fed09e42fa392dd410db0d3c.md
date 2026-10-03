# RHEL 9 Network Management

| NAME | UUID | TYPE | DEVICE |
|---|---|---|---|
| zoneone | 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 | wifi | wlp0s26u1u2 |
| enol | 99d40009-6bb1-4182-baad-a103941c90ff | ethernet | enol |
| virbr0 | e13e9552-1765-42d1-b739-ff981668fbee | bridge | virbr0 |
| zonetwo | f940a2d1-8c18-4a9e-bf29-817702429b8a | wifi | -- |
| zonethree | fd65c5e5-3e92-4e9e-b924-1b0b07b70032 | wifi | -- |

The above output shows that the WiFi device (wlp0s26u1u2) is connected to a wireless network named zoneone while the Ethernet device (eno1) is connected to a connection named eno1. In addition to zoneone, NetworkManager has also listed two other WiFi connections named zonetwo and zonethree, neither of which currently has a device connected.

To find out the IP address allocated to a connection, the ip tool can be used with the address option:

```
# ip address
```

The above command can also be abbreviated:

```
# ip a
```

```
. 
. 
3: wlp0s26u1u2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 74:da:38:ee:be:50 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.121/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s26u1u2
        valid_lft 57584sec preferred_lft 57584sec
. 
.
```

The ip command will output information for all the devices detected on the system. For example, the above output shows that the WiFi device has been assigned an IP address of 192.168.1.121.

If we only wanted to list active connections, the nmcli command could have been used with the -a option:

```
# nmcli con show -a
```

| NAME | UUID | TYPE | DEVICE |
|---|---|---|---|
| zoneone | 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 | wifi | wlp0s26u1u2 |
| enol | 99d40009-6bb1-4182-baad-a103941c90ff | ethernet | enol |
| virbr0 | e13e9552-1765-42d1-b739-ff981668fbee | bridge | virbr0 |

To switch the WiFi device connection from zoneone to zonetwo, we can run the following command:

```
# nmcli device wifi connect zonetwo -ask
Password:
```

The -ask flag causes nmcli to prompt the user to enter the password for the WiFi network. To include the WiFi password on the command line (particularly useful if the command is being