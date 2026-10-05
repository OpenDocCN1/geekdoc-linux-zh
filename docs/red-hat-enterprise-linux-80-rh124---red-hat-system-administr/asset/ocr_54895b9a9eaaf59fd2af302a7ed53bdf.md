# CONFIGURING NETWORKING FROM THE COMMAND LINE

# OBJECTIVES

After completing this section, you should be able to manage network settings and devices using the nmcli command.

# DESRIBING NETWORKMANAGER CONCEPTS

NetworkManager is a daemon that monitors and manages network settings. In addition to the daemon, there is a GNOME Notification Area app providing network status information. Command-line and graphical tools talk to NetworkManager and save configuration files in the /etc/sysconfig/network-scripts directory.

+   - A device is a network interface.
- A connection is a collection of settings that can be configured for a device.
- Only one connection can be active for one device at a time. Multiple connections may exist for different devices or allow connection to be altered for the same device. If you need to temporarily change network settings, instead of changing the configuration of a connection, you can change which connection is active for a device. For example, a device for a wireless network interface on a laptop might use different connections for the wireless network at a work site and for the wireless network at home.
- Each connection has a name or ID that identifies it.

# VIEWING NETWORKING INFORMATION

The nmcli dev status displays the status of all network devices:

```
[user@host ~$] nmcli dev status
DEVICE TYPE STATE CONNECTION
eno1 ethernet connected eno1
ens3 ethernet connected static-ens3
eno2 ethernet disconnected
lo loopback unmanaged
```

The nmcli con show displays a list of all connections. To list only connections, add the --active option.

```
[user@host ~$] nmcli con show -active
NAME UUID DEVICE
eno2 ff79d670-d833-42ed-9329-f8b5f81cd 802-3-ethernet --
static-ens3 72ca57a2-f780-40da-b146-99f71c431c2e 802-3-ethernet ens3
eno1 87bd5c56-1f5d-4a29-a869-7baadf546dfa 802-3-ethernet eno1
static-ens3 72ca57a2-f780-40da-b146-99f71c431c2e 802-3-ethernet ens3
```