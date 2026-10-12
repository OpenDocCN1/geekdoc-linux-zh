Client for Microsoft Networks is checked. From the WINS Configuration tab, click Enable WINS Resolution, type the IP address for your Linux server, and click Add. Then click OK.

> **TIP:** If you want to allow the client to share its own files and printers, you can click **File and Print Sharing**. Then you can select to turn on file access and/or printer access from the pop-up window that appears.

Other information that you need to add relates to the client computer’s identity and access. On the Network window, click the Identification tab. On that tab, enter a name for the client computer, the name of the workgroup and a description of the computer. Next, click the Access Control tab. From there, select either User-level or Share-level access control (to match the type of control set up on the server). Click OK when you are done. (At this point, you may need to reboot Windows.)

To see the file and print services available from your Red Hat Linux Samba server (as well as from other computers on the network), open the Network Neighborhood window. To open the window, double-click the Network Neighborhood icon on the Windows 95 desktop. Figure 18-6 shows an example of the Network Neighborhood window for a small LAN.

The Network Neighborhood window shows the computers that Windows found on your network. If your server appears on the screen (in my case, the server’s name is pine), double-click on it. Otherwise, you may need to double-click on Entire Network, then open the workgroup that your server is a part of to find your server. The server should show two kinds of resources:

![](bbox=[0.07, 0.54, 0.6, 0.8])

Figure 18-6: View your Red Hat Linux Samba server from the Network Neighborhood window.

+   * **Printers** — A name and a printer icon should represent each printer shared from the server. To access a printer, double-click on it. Windows will have you set up the printer for your computer. After that, you can print with it as you would any local printer.