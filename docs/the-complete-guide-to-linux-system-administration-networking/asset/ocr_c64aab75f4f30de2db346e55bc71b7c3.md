![](bbox=[0.17, 0.13, 0.83, 0.65])

# Figure 9-6 The Service Configuration utility

# Configuring System Services

The initialization scripts in /etc/rc.d/init.d are provided when you install Linux. If you install a new software package for an Internet server or a system service or daemon, a script is typically placed in the correct directory and configured to activate the service at start-up time.

The initialization scripts in /etc/rc.d/init.d typically use configuration information located in the /etc/sysconfig directory and its subdirectories. The files in /etc/sysconfig are named for services, with each file containing name-value pairs that define configuration options for that service. For example, the /etc/sysconfig/network file on a Fedora system might look like this:

```
NETWORKING=yes
HOSTNAME=incline.xmission.com
GATEWAY=192.168.100.5
```

These lines are used by the script /etc/rc.d/init.d/network to control how networking is set up. (Information on specific network device configurations, such as IP addresses for Ethernet cards, is located in the network-scripts subdirectory of /etc/sysconfig.)

You can edit the files in /etc/sysconfig directly, but because the content of these files is often not intuitive, you can avoid configuration problems by relying on utilities designed to configure specific services, when available, as described in other areas of this book. For example, you can use the system-config-network utility to configure the /etc/sysconfig/