![](bbox=[0.18, 0.07, 0.77, 0.24])

**Figure 7.17** Local port-forwarding connections listening on port 3389, 5631, 5632, and 5901.

# *Secure Management with Windows Terminal Services and SSH*

Once the SSH server has been established, you can attempt to log in to the Windows terminal server. To log in to the Windows terminal server, enter the following commands:

+   1.  Select Start ▷ Programs ▷ Terminal Services Client.
+   2.  Enter **127.0.0.1** for the Server.
+   3.  Select Connect.

Once the Terminal Services client connects to the loopback address on port 3389, the SSH connection will forward that request to the Windows terminal server over the encryption SSH tunnel. After the connection reaches the Windows terminal server, you should see the login display and be prompted for your password, as shown in Figure 7.18.

Notice that the loopback interface is holding the connection by the designation of **127.0.0.1** in the upper left-hand corner in Figure 7.18. In order to log in, use your Windows terminal server or domain password given to you by your Windows administrator. After you have entered the correct password, you will view the desktop and have access to the operating system as if you were in front of the computer itself. You should load extra copy-and-paste utilities from Microsoft at the following Web address:

> www.microsoft.com/windows/2000/techinfo/reskit/tools/hotfixes/rdclip-o.asp