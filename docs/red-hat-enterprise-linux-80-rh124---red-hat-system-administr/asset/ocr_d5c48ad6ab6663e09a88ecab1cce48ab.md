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
| nmcli dev status | Show the NetworkManager status of all network interfaces. |
| nmcli con show | List all connections. |
| nmcli con show name | List the current settings for the connection *name*. |
| nmcli con add con-name name | Add a new connection *name*. |
| nmcli con mod name | Modify the connection *name*. |
| nmcli con reload | Reload the configuration files (useful after they have been edited by hand). |
| nmcli con up name | Activate the connection *name*. |
| nmcli dev dis dev | Deactivate and disconnect the current connection on the network interface *dev*. |
| nmcli con del name | Delete the connection *name* and its configuration file. |