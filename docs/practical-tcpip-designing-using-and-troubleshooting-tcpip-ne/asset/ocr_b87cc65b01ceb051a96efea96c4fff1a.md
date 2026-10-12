In some of the examples we have used unusual spacing to highlight differences between similar lines.

+   1. Print all routes to any 10.2.x.x network
+      `route print 10.2.*`
+   2. Print any route using 10.1.1.22 as a gateway
+      `route print * 10.1.1.22`
+   3. Print only routes to 10.2.x.x networks using 10.1.1.22 as a gateway
+      `route print 10.2.* 10.1.1.22`

![](bbox=[0.18, 0.27, 0.72, 0.45])

+   4. Create a default route:
+      `route add 0.0.0.0 mask 0.0.0.0 10.1.1.254`
+   5. Create a route saying that we can get to the range of addresses specified by 10.2.2.0/24 (i.e. 10.2.2.0, netmask 255.255.255.0) by using the router 10.1.1.22:
+      `route add 10.2.2.0 mask 255.255.255.0 10.1.1.22`
+   6. Create a route to the range 10.0.0.0 netmask 255.0.0.0 via the same router:
+      `route add 10.0.0.0 mask 255.255.0.0 10.1.1.22`

As with Linux, using the **route** command is error-prone because of its syntax; however, the Windows error messages, explained below, are even worse than Linux's. The tools on our Web site make it easier to construct the correct commands.

Note that when you have multiple NICs in your machine, Control Panel > Network settings aren’t actioned immediately – you have to reboot.

# ## Making your settings permanent

By default, routes **added** with the **route** command do not persist across reboots. If you use the “**-P**” option in the command when you create the route, it is considered a _persistent_ route and will remain in effect after rebooting. Anything you do to a persistent route also persists, so you don’t have to use “**-P**” with **change** or **delete**.