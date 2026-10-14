+   - NIS allows you to set a multitude of other options in the file `/etc/sysconfig/ypbind`.
+   - The final step in activating the NIS server is to launch `ypbind`. This is what actually starts the NIS client.
+   - To activate your changes, either restart your system or enter:
+   
+     ```
+     earth:  # rcnetwork restart
+     earth:  # rcypbind restart
+     ```

# NIS Master and Slave Server

An NIS Server needs package ypserver, series n, and a running portmap. If your portmapper has the tcp-wrapper built in, make sure `/etc/hosts.allow` and `/etc/hosts.deny` are set up correctly. NIS is mainly used for `/etc/passwd`, `/etc/shadow`, and `/etc/group`, but `/etc/hosts` and `/etc/services` can also be shared over the network. The client and the server machines need a common domain name. It does not need to be a DNS domain name. Pick any name you like. Write the name into the file `/etc/defaultdomain`.