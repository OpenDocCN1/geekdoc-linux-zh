+   6.  In the Name section, type **WEB** for the Name field.
+   7.  In the Remote section, check the checkbox Manually select remote IP address on which to allow connections and type **11.30.11.21** for the IP address.
+   8.  In the Remote section, type **80** for the Port field.
+   9.  In the Local section, type **localhost** for the Hostname field.
+   10. In the Local section, type **80** in the Port field.
+   11. Select OK.

Figure 6.19 shows the result of the preceding steps. Once the SSH connection is made with the remote port-forwarding settings, the internal Web client should open the Web browser and point to the following URL: http://11.30.11.21:80. Also, on the SSH server itself, the following URL can be used: http://127.0.0.1:80. This will display the Web site on web-jum4nj1.com to both the internal Web client and the SSH server on the encrypted SSH connection.

![](bbox=[0.14, 0.45, 0.6, 0.75])

**Figure 6.19**  The Remote port-forwarding configuration with SecureCRT.