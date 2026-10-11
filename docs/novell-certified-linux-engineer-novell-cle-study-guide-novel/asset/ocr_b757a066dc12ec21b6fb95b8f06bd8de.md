16. In the top frame, click **Save**.

17. Using a filename of your choice, save the file to the drive mapped to the Samba share on your NNLS server.

18. Close your browser window.

19. On your server, copy the file from your Windows workstation to the `/var/opt/novell/http/htdocs/ippdocs` directory on your NNLS server.

With that, the iPrint system is ready to go! Let's now discuss how to install iPrint printers on Windows workstations.

# ## Configuring iPrint Printers on Windows Workstations

# ### Test Objective Covered:

+   1. Print with iPrint.

With the iPrint Client installed, the Driver Store configured, the iPrint Manager implemented, the Printer Agents configured, and the iPrint maps created, you're ready to start configuring iPrint printers on client Windows workstations.

This is done using the map HTML file you created and copied to your iPrint server. To access this map and install the printers it contains, you need to do the following:

> **WARNING**
> These steps are written using Windows XP Professional. If your organization uses a different version of Windows, the steps may be slightly different.

+   1. Verify that the iPrint Client has been installed on your Windows workstation. To do this, you can do the following:
+      a. Select **Start, Control Panel, Add or Remove Programs**.
+      b. Verify that the Novell iPrint Client is displayed in the list of installed programs, as shown in Figure 9.27.
+      c. Close the **Add or Remove Programs** and **Control Panel** windows.