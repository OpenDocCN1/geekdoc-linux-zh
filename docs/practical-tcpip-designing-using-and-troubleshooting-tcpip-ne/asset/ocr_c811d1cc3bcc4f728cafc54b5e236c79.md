# ## Appendix 8 Windows-NT route command managepage

### Name
**route** — display or modify this machine’s routing tables

### Synopsis
**route [-f] [-p] *command destination mask netmask gateway metric value if interface*

+   - **Options**
+     - **-f** flush all “gateway” entries (i.e. not entries for directly connected networks). This may be used on its own or in conjunction with a *command*.
+     - **-p** used with the **add** command to make the specified route permanent (persist across reboots of the system). By default routes added are not persistent.

### Commands

+   - **print [ *destination* [ *mask netmask* ] ]**
+     with no arguments, prints the entire routing table. With arguments *destination* or *destination mask netmask*, prints matching routes.
+   - **add *destination gateway* [ *metric value* ] [ *if interface* ]**
+   - **add *destination* [ *mask netmask* ] *gateway* [ *metric value* ] [ *if interface* ]**
+     creates a static route to *destination* via router *gateway*. If the **mask** arguments are given, the route is for a range of addresses specified by the combination of *destination* and *netmask*; otherwise it’s for the single host with address *destination*. You can explicitly specify the network interface although usually that isn’t necessary.
+     The **metric** arguments can indicate a preference between routes that would otherwise be equally applicable; the higher the **metric** value, the less preferred the route.
+   - **delete *destination* [ *mask netmask* ] [ *gateway* ]**
+     delete all matching routes. If a deleted route was persistent it is deleted permanently, i.e. the deletion is persistent too.
+   - **change *destination* [ *mask netmask* ] *gateway* [ *metric value* ] [ *if interface* ]**
+     modify the specified route. Only one of the arguments should differ from the existing values, so that **route** can identify the entry you wish to change.

+   - **Notes**
+     1. when you specify a range with *destination mask netmask*, the *destination* must be the network address (the lowest IP number in the specified range); otherwise you get an error, e.g. to create a route for the 16 addresses 10.1.2.22/240, the correct command is:
+        ```
+        route add 10.1.2.16 mask 255.255.255.240 192.0.2.77
+        ```
+        whereas
+        ```
+        route add 10.1.2.22 mask 255.255.255.240 192.0.2.77
+        ```
+        complains “The route addition failed: 87”
+     2. *destination* and *gateway* can be specified as host names instead of IP numbers
+     3. you can use wildcards in *destination*: * matches any string of characters, and ? matches any one character.