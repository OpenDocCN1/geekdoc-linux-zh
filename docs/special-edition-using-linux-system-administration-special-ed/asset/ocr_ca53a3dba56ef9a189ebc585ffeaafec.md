+   - **Entries to control access from indirect queries:** Indirect queries are those queries received from a desktop which xdm should redirect to another xdm system to handle. Entries take the form:
+   
+     `<host name or host name pattern> <list of alternate xdm hosts>`
+   
+     Any desktop that matches the hostname or pattern will be redirected to one of the alternate xdm hosts. The list of alternate xdm hosts is separated by spaces.

+   - **Entries to display a chooser to desktops:** The chooser allows desktops to select from a list of available xdm servers and then log in to one of the servers. Entries take the form:
+   
+     `<host name or host name pattern> CHOOSER <list of xdm hosts>`
+   
+     Any desktop that matches the hostname or pattern will be presented with the chooser. The list of xdm hosts will be listed in the chooser. In place of a list of xdm hosts, you can use the keyword `BROADCAST`, which will cause xdm to broadcast on the network to discover all available xdm servers which will handle requests from the connecting desktop and present those in the chooser’s list.

+   - **Entries to define macros:** Macros allow you to define a name for a list of hosts and then use that macro name anywhere a list of hosts is required in other Xaccess entries. Entries take the form:
+   
+     `%<macro name> <list of hosts>`
+   
+     For instance, if you define a macro named `%mymacro` and assign it the list of hosts `host1 host2 host3` then you can use `%macro` in other Xaccess entries to indicate the three hosts.

This means that the simplest Xaccess file contains a single entry:

```
```text
*
```
```

With this entry, any host requesting service through XDMCP will be presented with a login window and users can proceed to log in and use the server. In an environment with a single X application server, this will be sufficient because users only have the choice to log in to one server.

You might have more than one X application server and might want to allow users the choice to log in to any of the servers. To do so, use the following two entries in your Xaccess file to cause xdm to display a chooser list with all xdm servers to the user:

```
```text
*
* CHOOSER BROADCAST
```
```

A more complex Xaccess file might look like the following:

```
```text
fin*
per* per-x-server
mis* CHOOSER BROADCAST
```
```