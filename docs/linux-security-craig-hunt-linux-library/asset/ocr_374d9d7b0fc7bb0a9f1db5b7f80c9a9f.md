![](bbox=[0.73, 0.13, 0.87, 0.26])

# # Network Services Configuration

Part 1, “System Security,” described the concepts that you need to master in order to secure your Linux installation and configuration before connecting your server to the public network. It explored the process of choosing a Linux distribution, configuring password authentication, and ensuring the confidentiality and availability of the data kept on the filesystems. In addition, it showed you how to ensure the integrity of system utilities and configuration files.

Part 2, “Network Security,” takes the discussion one step away from the system itself and deals with the issues associated with connecting a Linux server to a network. Native support for a wide range of TCP/IP services has always been one of the strongest qualities of the Linux operating system. Configuring these services with security in mind, however, is an increasingly difficult challenge for system administrators as new network services are demanded of their servers.

This chapter begins Part 2 by discussing network services configuration on a Linux server. It includes a detailed description of

+   * The issues associated with the inetd daemon
+   * The /etc/rc.d startup files
+   * TCP Wrappers, a tool for enforcing access control on network daemons
+   * The commands that are available to show network activity on your server

Let’s start by introducing a simple set of rules to apply when configuring Linux network daemons.