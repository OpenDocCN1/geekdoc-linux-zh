
## RHEL 9 Network Management

using the more intuitive tool options. The same cannot be said of the graphical tool options. It is harder to use nmcli if, for example, you have only ever used nm-connection-editor.

### 12.2 Installing and Enabling NetworkManager

NetworkManager should be installed by default for most RHEL 9 installations. Use the rpm command to find out if it needs to be installed:

```
# rpm -q NetworkManager
NetworkManager-1.14.0-14.el9.x86_64
```

If necessary, install the package as follows:

```
# dnf install NetworkManager
```

Once the package is installed, the NetworkManager daemon will need to be enabled so that it starts each time the system boots:

```
# systemctl enable NetworkManager
```

Finally, start the service running and check the status to verify that the launch was successful:

```
# systemctl start NetworkManager
# systemctl status NetworkManager
• NetworkManager.service - Network Manager
    Loaded: loaded (/usr/lib/systemd/system/NetworkManager.service; enabled; vendor >
    Drop-In: /usr/lib/systemd/system/NetworkManager.service.d
            └─NetworkManager-ovs.conf
    Active: active (running) since Tue 2019-04-09 10:07:22 EDT; 2h 48min ago
.
.
```

### 12.3 Basic nmcli Commands

The nmcli tool will have been installed as part of the NetworkManager package and can be executed from the command line using the following syntax:

```
# nmcli [Options] Object {Command | help}
```

In the above syntax, Object will be one of general, networking, radio, connection, monitor, device, or agent, which can be abbreviated to a few letters of the word (for example, con, or even just the letter c, for connection). For example, all of the following commands will output help information relating to the device object:

```
# nmcli device help
# nmcli dev help
# nmcli d help
```

To check the overall status of NetworkManager on the system, use the following command:

```
# nmcli general status
```

| STATE | CONNECTIVITY | WIFI-HW | WIFI | WWAN-HW | WWAN |
|---|---|---|---|---|---|
| connected | full | enabled | enabled | enabled | enabled |

To check the status of the devices installed on a system, the following command can be used:

```
# nmcli dev status
DEVICE      TYPE      STATE       CONNECTION
eno1        ethernet  connected   eno1
wlp0s26ulu2 wifi      connected   zoneone
virbr0      bridge    connected   virbr0
lo          loopback  unmanaged   --
virbr0-nic  tun       unmanaged   --
```

The output may also be modified by using the -p (pretty) option to make the output more human-friendly:

```
# nmcli -p dev status
====================
    Status of devices
====================
DEVICE      TYPE      STATE       CONNECTION
------------------------------------------------------------
eno1        ethernet  connected   eno1
wlp0s26ulu2 wifi      connected   zoneone
virbr0      bridge    connected   virbr0
lo          loopback  unmanaged   --
virbr0-nic  tun       unmanaged   --
```

Conversely, the -t option may be used to make the output more terse and suitable for automated processing:

```
# nmcli -t dev status
eno1:ethernet:connected:eno1
wlp0s26ulu2:wifi:connected:zoneone
virbr0:bridge:connected:virbr0
lo:loopback:unmanaged:
virbr0-nic:tun:unmanaged:
```

The status output shows that the system has two physical devices installed, one Ethernet and the other a WiFi device.

The bridge (virbr) entries are virtual devices used to provide networking for virtual machines (the topic of virtualization will be covered starting with the chapter entitled “An Overview of Virtualization Techniques”). Finally, the loopback interface is a special virtual device that allows the system to communicate with itself and is typically used to perform network diagnostics.

When working with NetworkManager, it is important to understand the difference between a device and a connection. As described above, a device is either a physical or virtual network device, while a connection is a network configuration that the device connects to.

The following command displays information about the connections configured on the system:

```
# nmcli con show
```

| NAME | UUID | TYPE | DEVICE |
|---|---|---|---|
| zoneone | 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 | wifi | wlp0s26ulu2 |
| eno1 | 99d40009-6bb1-4182-baad-a103941c90ff | ethernet | eno1 |
| virbr0 | e13e9552-1765-42d1-b739-ff981668fbee | bridge | virbr0 |
| zonetwo | f940a2d1-8c18-4a9e-bf29-817702429b8a | wifi | -- |
| zonethree | fd65c5e5-3e92-4e9e-b924-1b0b07b70032 | wifi | -- |

The above output shows that the WiFi device (wlp0s26ulu2) is connected to a wireless network named zoneone while the Ethernet device (eno1) is connected to a connection named eno1. In addition to zoneone, NetworkManager has also listed two other WiFi connections named zonetwo and zonethree, neither of which currently has a device connected.

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
3: wlp0s26ulu2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 74:da:38:ee:be:50 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.121/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s26ulu2
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
| zoneone | 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 | wifi | wlp0s26ulu2 |
| eno1 | 99d40009-6bb1-4182-baad-a103941c90ff | ethernet | eno1 |
| virbr0 | e13e9552-1765-42d1-b739-ff981668fbee | bridge | virbr0 |

To switch the WiFi device connection from zoneone to zonetwo, we can run the following command:

```
# nmcli device wifi connect zonetwo -ask
Password:
```

The -ask flag causes nmcli to prompt the user to enter the password for the WiFi network. To include the WiFi password on the command line (particularly useful if the command is being executed in a script), use the password option:

```
# nmcli device wifi connect zonetwo password <password here>
```

The nmcli tool may also be used to scan for available WiFi networks as follows:

```
# nmcli device wifi list
IN-USE  SSID      MODE   CHAN  RATE       SIGNAL  BARS  SECURITY
        zoneone   Infra  6     195 Mbit/s 80            WPA2
*       zonetwo   Infra  11    130 Mbit/s 74            WPA1 WPA2
```

A currently active connection can be deactivated as follows:

```
# nmcli con down <connection name>
```

Similarly, an inactive connection can be brought back up at any time:

```
# nmcli con up <connection name>
```

When a connection is brought down, NetworkManager automatically searches for another connection, activates it, and assigns it to the device to which the previous connection was established. To prevent a connection from being used in this situation, disable the autoconnect option as follows:

```
# nmcli con mod <connection name> connection.autoconnect no
```

The following command may be used to obtain additional information about a specific connection. This includes the current values for all the connection properties:

```
# nmcli con show eno1
connection.id:                     eno1
connection.uuid:                   99d40009-6bb1-4182-baad-a103941c90ff
connection.stable-id:              --
connection.type:                   802-3-ethernet
connection.interface-name:         eno1
connection.autoconnect:            yes
connection.autoconnect-priority:   0
connection.autoconnect-retries:    -1 (default)
connection.multi-connect:          0 (default)
connection.auth-retries:           -1
connection.timestamp:              1554833695
connection.read-only:              no
connection.permissions:            --
connection.zone:                   --
connection.master:                 --
connection.slave-type:             --
connection.autoconnect-slaves:     -1 (default)
.
.
```

All of these properties can be modified using nmcli with the modify option using the following syntax:
