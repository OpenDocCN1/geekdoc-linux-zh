Use the **xrdb** utility to add resources for the application to the resource database.

# The Sequence of Events When CDE Starts

The following section is a blow-by-blow account of what happens when a user logs into CDE. In this particular account, assume a distributed topology like a diskless cluster. The account begins with the boot of the hub system and nodes in step 1. By step 4, X servers are running on each node and login screens are being displayed. By step 6, the user is logged in. By step 11, the session manager is busy re-creating the user’s session.

+   1. The **dtlogin** executable is started as part of the **init** process that occurs during the system boot sequence on the hub machine and each cluster node.
+   2. **dtlogin** reads **/usr/dt/config/Xconfig** to get a list of resources with which to configure the login process. This is where **dtlogin** first learns about files like **Xaccess**, **Xservers**, **Xresources**, **Xstartup**, **Xsession**, and **Xreset** and gets the values of a number of appearance and behavior resources.
+   3. **dtlogin** reads two files in **/usr/dt/config**:
+   	* **Xservers** or the file identified by the **Dtlogin\*servers** resource setting in **Xconfig**.
+   	* **Xresources** or the file identified by the **Dtlogin\*resources** resource setting in **Xconfig**.
+   4. **dtlogin** starts an X server and a child **dtlogin** for each local display.
+   5. Each child **dtlogin** invokes **dtgreet**, the login screen.
+   6. When a login and password are validated, a child **dtlogin** sets certain environment variables to default values.
+   7. The child **dtlogin** runs **/usr/dt/config/Xstartup**.
+   8. The child **dtlogin** runs **/usr/dt/config/Xsession**.