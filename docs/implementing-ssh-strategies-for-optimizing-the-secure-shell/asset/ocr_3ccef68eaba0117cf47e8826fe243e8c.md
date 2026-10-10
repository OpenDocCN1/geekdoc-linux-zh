Since pcAnywhere requires two ports, you will have to add a second local port forward.

+   37. Select Add to display the Port Forwarding options.
+   38. Enter **pcAnywhere2** Server for the Name field.
+   39. In the Local subsection, make sure “Manually select local IP address on which to allow connections” is unchecked.
+   40. In the Local subsection, enter **5632** for the Port field.
+   41. In the Remote subsection, make sure “Destination host is different from the SSH server” is checked.
+       a. Enter **10.1.0.200** for the Hostname field.
+   42. In the Remote subsection, enter port **5632** for the Port field.
+   43. You can leave the Application subsection blank.
+   44. Select OK.

The result should look like Figure 7.15.

![](bbox=[0.18, 0.41, 0.63, 0.78])

**Figure 7.15** Local port-forwarding settings.

After the SSH client has been completely installed, the management clients are ready for the secure management architecture.