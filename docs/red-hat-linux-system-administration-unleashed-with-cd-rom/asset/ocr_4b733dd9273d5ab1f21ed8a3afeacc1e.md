+   - n—Changes the mode in which host addresses are output. The following modes are supported:
+     - **IP Address**—A numeric IP address.
+     - **Symbolic Hostname**—A symbolic hostname as specified in the `/etc/hosts` file or resolved from a DNS server.
+     - **MAC Address**—An ethernet MAC address.
+     - **Board Manufacturer**—A text identifier specifying the manufacturer of the network interface hardware used by each network host.
+   - p—Changes the mode in which traffic information is output. The following modes are supported:
+     - **Percentage**—Shows traffic information as a percentage of the total traffic sent.
+     - **Absolute**—Shows traffic information as an absolute value representing the amount of data sent.
+     - **Throughput**—Shows traffic information throughput information in an amount of data sent per second format.
+   - 1—Changes the type of hosts that ntop outputs information for. The following types are supported:
+     - **local**—Displays network information for hosts that are classified as inside a local network.
+     - **remote**—Displays network information for hosts that are classified as inside a remote network.
+   - d—Sets ntop to sort hosts according to idle time or the amount of data sent/received.
+   - t—Sets ntop to sort hosts according to the data being sent or received.
+   - y—Sets ntop to sort hosts according to their associated protocol identifiers.
+   - `<space>`—Toggles showing of additional network traffic information in additional columns.

The second execution mode that is supported by ntop is Web mode; it allows program output to be monitored by multiple local or remote users through a Web browser. The ntop Web mode is illustrated in Figure 16.7.

When used in Web mode, ntop can be manipulated by selection of one of several different traffic views from the left frame of the HTML browser display window. These offer additional information not available in the ntop interactive mode. Table 16.3 lists the views available.