If you want **ethtool** to modify any settings, list the options here; if no options are listed, **ethtool** is not called.

The file **/etc/sysconfig/network/ifcfg.template** contains a template that you can use as a base for device configuration files. It also has comments explaining the various options.

# **Configure a Device Dynamically with DHCP**

If you want to configure a device by using a **DHCP** server, you set the **BOOTPROTO** option to **dhcp** as shown in the following:

```
BOOTPROTO='dhcp'
```

When the device is configured by using **DHCP**, you don't need to set any options for the network address configuration in the file. If there are any settings, they are overwritten by the settings of the DHCP server.

# **Start and Stop Configured Interfaces**

To apply changes to a configuration file, you need to stop and restart the corresponding interface. You can do this with the commands **ifdown** and **ifup**.

For example, entering **ifdown eth0** disables the device eth0. **ifup eth0** enables eth0 again.

When the device is restarted, the new configuration is read from the configuration file.

> Configuring the interfaces with IP addresses, routes, etc. with the ip tool requires an existing device setup, including a correctly loaded kernel module. This is usually done at boot time by /sbin/hwup, using the configuration contained in files in the directory /etc/sysconfig/hardware/. Information is available in the manual page for hwup.