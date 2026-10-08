![](bbox=[0.035, 0.075, 0.11, 0.17])

# route

The information displayed with **netstat** is the routing tables for your system. Some are automatically created with the **ifconfig** command when your system is booted or when the network interface is initialized. Routes to networks and hosts that are not directly connected to your system are entered with the **route** command.

![](bbox=[0.035, 0.175, 0.11, 0.27])

Your system administrator can make routing changes on the fly, as I did to change the Flags from U to UG:

![](bbox=[0.035, 0.275, 0.11, 0.37])

```
$ /usr/sbin/route add default 128.185.61.1 3
```

First is the **route** command. Second, we specify that we wish to add a route; the other option is to delete a route. Third, we specify the destination, in this case, the default. This could be a specific host name, a network name, an IP address, or default that signifies the wildcard gateway route that is shown in our example. Fourth is the gateway through which the destination is reached. In the above example, the IP address was used, but this could also be a host name. The 3 corresponds to the count that is used to specify whether the gateway is the local host or a remote gateway. If the gateway is the local host, then a count of 0 is used. If the gateway is a remote host, which is the case in the example, a count of >0 is used. This corresponds to UG for Flags. This manually changed the network routing table by adding a default route with the appropriate Flags. Issuing this command fixed the problem I encountered trying to get system1 to talk to the systems on the other side of the router (remember Figure 9-10?).

Before issuing **/usr/sbin/route** with the **add** option, you can first use the **delete** option to remove the existing default route, which is not working.

**route** commands usually appear in one of the system’s startup files so that every time the system boots, **route** commands are issued. This ensures that the right connectivity information is in place every time the system starts.