
# DELETING A NETWORK CONNECTION

The **nmcli con name** deletes the connection name **name** from the system, disconnecting it from the device and removing the file **/etc/sysconfig/network-scripts/ifcfg-name**.

```
[root@host ~]# nmcli con static-ens3
```

# WHO CAN MODIFY NETWORK SETTINGS?

The root user can make any necessary network configuration changes with **nmcli**.

Regular users who are logged in on the local console can also make many network configuration changes to the system. They have to log in at their system's keyboard to either a text-virtual console or the graphical desktop environment to get this control. The logic behind that is if someone is physically present at the computer, it's likely being used as a workstation or laptop and they may need to configure, activate, and deactivate either or wired network interfaces at. By contrast, if the system is in the datacenter, generally the only users logging into the machine itself should be administrators.

Regular users who log in using **ssh** do not have access to change network permissions without becoming root.

You can use the **nmcli gen permissions** command to see what your current permissions are.

# SUMMARY OF COMMANDS

The following table is a list of key **nmcli** commands discussed in this section.

| COMMAND | PURPOSE |
| :--- | :--- |
| nmcli dev status | Show the NetworkManager status of all network interfaces. |
| nmcli con show | List all connections. |
| nmcli con show name | List the current settings for the connection *name*. |
| nmcli con add con-name name | Add a new connection *name*. |
| nmcli con mod name | Modify the connection *name*. |
| nmcli con reload | Reload the configuration files (useful after they have been edited by hand). |
| nmcli con up name | Activate the connection *name*. |
| nmcli dev dis dev | Deactivate and disconnect the current connection on the network interface *dev*. |
| nmcli con del name | Delete the connection *name* and its configuration file. |

# REFERENCES

> NetworkManager(8), nmcli(1), nmcli-examples(5), nm-settings(5), hostnamectl(1), resolv.conf(5), hostname(5), ip(8), and ip-address(8) man pages

# GUIDED EXERCISE

# CONFIGURING NETWORKING FROM THE COMMAND LINE

In this exercise, you will configure network settings using **nmcli**.

# OUTCOMES

You should be able to convert a system from DHCP to static configuration.

# BEFORE YOU BEGIN

Log in as the `student` user on workstation using `student` the password.

From workstation, run the **lab net-config start** command. The command runs a script that determines if the host, servera, is reachable on the network.

```
[student@workstation ~]$ lab net-config start
```

- 1. Use the ssh command to log in `servera` as the `student` user. The systems are configured to use SSH keys for authentication.

```
[student@workstation ~]$ ssh student@servera
[student@servera ~]$
```

- 2. These instructions are written assuming that your network interface with the MAC address 52:54:00:00:00:fa0 is named ens3. Use **ip link** to check this, and if your system has a different interface name, use that for the rest of the exercise.

```
[student@servera ~]$ ip link
1: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
len 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens3:<BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fcod_type state UP default qlen 1000
link/ether 52:54:00:00:00:fa brd ff:ff:ff:ff:ff:ff
```

- 3. View network settings using **nmcli**.

- 3.1. Show all connections.

```
[student@servera ~]$ nmcli con show
```

| NAME | UUID | TYPE | DEVICE |
| :--- | :--- | :--- | :--- |
| ens3 | 03da038a-3257-4272-a478-53055cc0128 | ethernet | ens3 |

| Wired connection 1 91d515af-5367-384b-a012-6bdd2e390f66 ethernet

- 3.2. Display only the active connection.
Your network interface name should appear under DEVICE, and the name of the connection active for that device is on the same line under NAME. This exercise assumes that the active connection is ens3, matching the network interface name.
If the name of the active connection is different, use instead of ens3 for the rest of this exercise.

```
$student@servera~$ nmcli con show --active
NAME UUID DEVICE
ens3 03d0a38a-3257-a472-a478-53055cc90128 ethernet ens3
```

- 3.3. Display all settings for the active connection.

```
$student@servera~$ nmcli con show "ens3"
connection.id:
ens3
connection.uuid:
03d0a38a-3257-a472-a478-53055cc90128
connection.stable-id:
-
connection.type:
802-3-ethernet
connection.autoconnect:
yes
..output omitted...
ipv4.method:
manual
ipv4.dns:
172.25.250.254
ipv4.dns-search:
lab.example.com,example.com
"
ipv4.priority:
0
ipv4.addresses:
172.25.250.10/24
172.25.250.254
ipv4.gateway:
..output omitted...
GENERAL.NAME:
GENERAL.NAME:\ens3
GENERAL.UUID:
03d0a38a-3257-a472-a478-53055cc90128
GENERAL.DEVICE:
ens3
GENERAL.STATE:
activated
GENERAL.DEFAULT:
yes
GENERAL.DEFAULT6:
no
GENERAL.SPEC-OBJECT:
-
GENERAL.VPN:
no
GENERAL.DBUS-PATH:
/org/freesktop/NetworkManager/ActiveConnection/2
GENERAL.CON-PATH:
/org/freesktop/NetworkManager/Settings/2
GENERAL.ZONE:
-
GENERAL.MASTER-PATH:
-
IP4.ADDRESS[1]:
172.25.250.10/24
172.25.250.254
IP4.GATEWAY:
dst = 172.25.250.24, nh = 0.0.0.0, mt = 100
IP4.ROUTE[1]:
IP4.ROUTE[2]:ndst = 0.0.0.0/0, nh = 172.25.250.254, mt = 100
IP4.DNS[1]:
172.25.250.254
```
