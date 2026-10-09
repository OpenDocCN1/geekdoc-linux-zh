# Configuring the DHCP Server

We will setup a simple DHCP configuration to provide clients with network information. The DHCP server can be configured using the default configuration file /etc/dhcpd.conf.

The DHCP server package comes with a sample dhcpd configuration file, called dhcpd.conf.sample. We will use this file as a starting point to configure DHCP configuration, take a backup of your existing dhcpd.conf file and then copy the sample file in its place:

```
# cp /etc/dhcpd.conf /etc/dhcpd.conf.backup
# cp /usr/share/doc/dhcp-3.0pl1/dhcpd.conf.sample /etc/dhcpd.conf
```

Now open the /etc/dhcpd.conf file, using gedit or another text editor, and we'll edit it so it contains all the required options. A simple dhcp configuration file looks like this:

```
ddns-update-style interim;
ignore client-updates;
subnet 192.168.0.0 netmask 255.255.255.0 {
    option routers                        192.168.0.1;
    option subnet-mask                    255.255.255.0;
    option domain-name                    "linux4biz.net";
    option domain-name-servers            192.168.0.1;
    range dynamic-bootp                   192.168.0.128 192.168.0.254;
    default-lease-time                    21600;
    max-lease-time                        43200;
}
```

You can use # characters to comment out the lines you don't need, or simply delete them to keep the file tidy. Let's have a look at the settings in this example:

+   - The first two lines of the configuration file instruct the DHCP server not to accept dynamic DNS updates.
+   - The next line defines a subnet and netmask that will is used to supply the DHCP information. After that we defined all the options:

| Option | Description |
| :--- | :--- |
| routers | Specifies the default gateway |
| subnet-mask | Specifies the default netmask |
| domain-name | Specifies the default domain-name |
| domain-name-servers | Specifies the name-servers for our network |