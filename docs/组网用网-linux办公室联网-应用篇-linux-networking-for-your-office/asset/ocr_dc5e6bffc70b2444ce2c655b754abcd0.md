+   - Issue the command:
+     cat "0" /proc/sys/net/ipv4/ip_forward
+     This will disable forwarding in the kernel.

+   - Uncheck the Enable routing check button in the linuxconf Config, Networking, Client tasks, Routing and gateways, Defaults screen, shown in Figure 21.4. This has the same effect as the preceding command.

![](bbox=[0.19, 0.29, 0.68, 0.68])

# FIGURE 21.4

When you disable routing, Linux refuses to pass a packet from one network to another.

# Configuring the SOCKS Clients

On the client side, you must also create a configuration file, called /etc/lib socks5.conf. This file contains lines of the form:

```
proxy cmd dest-host dest-port [userlist [proxylist]]
```

The meanings of each of these items is similar to the meanings of equivalent items in the /etc/socks5.conf file. For instance, the following line allows any user to connect to the proxy server gingko.biloba.com:

```
socks5 - - - gingko.biloba.com
```

You can create more complex configurations that pass different protocols through different proxy servers, provide services only to certain users, and so on. Once you’ve created the configuration file, you can use SOCKS-aware client programs.