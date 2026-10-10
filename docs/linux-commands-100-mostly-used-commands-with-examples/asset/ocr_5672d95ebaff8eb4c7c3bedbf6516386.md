# 32. ifconfig or ip: Configure network interfaces.

`ifconfig` Command:

The `ifconfig` command is used to configure network interfaces on a Linux system. It allows you to view and configure the IP address, netmask, broadcast address, and other parameters of a network interface. However, `ifconfig` has been deprecated in many modern Linux distributions in favor of the more powerful `ip` command.

**Examples:**

1. **Viewing Network Interfaces:**

```
```
ifconfig
```
```

This command displays information about all network interfaces on the system.

2. **Viewing Information for a Specific Interface:**

```
```
ifconfig eth0
```
```

Replace "eth0" with the name of your network interface. This command displays detailed information about the specified interface.

3. **Assigning an IP Address:**