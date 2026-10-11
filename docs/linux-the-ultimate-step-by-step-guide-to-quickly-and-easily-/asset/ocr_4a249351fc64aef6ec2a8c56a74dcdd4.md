![](bbox=[0.24, 0.05, 0.76, 0.31])

# # Change and Set Hostname Command

On a CentOS Linux 7 server, you can use any one of the following tools to manage hostnames:

+   - hostnamectl: Control the system hostname. This is the recommended method.
+   - nmtui: Control the system hostname using text user interface (TUI).
+   - nmcli: Control the system hostname using CLI part of NetworkManager.

# ## Method #1: hostnamectl

Let us see how to use the hostnamectl command.

To verify new settings, enter:

```
# hostnamectl status
```

# ## How do I see the host names?

Sample outputs:

| Static hostname: | server1.cyberciti.biz |
| :--- | :--- |
| Pretty hostname: | Senator Padmé Amidala's Laptop |
| Transient hostname: | r2-d2 |
| Icon name: | computer |
| Chassis: | n/a |
| Machine ID: | b5470b10ccfd49ed8e4a3b0e953a53c3 |
| Boot ID: | f79de79e2dac4670bddffe528e826b61f |
| Virtualization: | oracle |
| Operating System: | CentOS Linux 7 (Core) |
| CPE OS Name: | cpe:/o:centos:centos:7 |
| Kernel: | Linux 3.10.0-229.1.2.el7.x86_64 |
| Architecture: | x86_64 |