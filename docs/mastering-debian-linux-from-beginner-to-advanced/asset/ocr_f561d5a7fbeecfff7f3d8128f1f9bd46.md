+   • netmask: The subnet mask
+   • gateway: The IP address of your router or default gateway
+   • dns-nameservers: The IP addresses of the DNS servers you want to use

# ### Configuring DNS

DNS (Domain Name System) resolution can be configured in two main ways:

+   1. In the `/etc/network/interfaces` file (as shown above)
+   2. In the `/etc/resolv.conf` file

# **Using /etc/resolv.conf**

The `/etc/resolv.conf` file is used to configure the system's DNS resolver. Here's an example configuration:

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

However, be aware that this file may be overwritten by DHCP or other network management tools. For a more permanent solution, you can use the `resolvconf` package or Network Manager.

# ## Using Network Manager

If you're using a desktop environment, you might prefer to use Network Manager for easier network configuration. Network Manager provides a graphical interface for managing network connections and can be configured to handle static IP and DNS settings.

To configure a static IP using Network Manager: