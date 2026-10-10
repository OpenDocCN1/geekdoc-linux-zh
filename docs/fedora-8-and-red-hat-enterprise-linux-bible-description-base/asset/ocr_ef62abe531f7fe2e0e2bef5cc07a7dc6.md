desktop. Figure 18-6 shows an example of the My Network Places window with shares available from the local Windows XP system (named Bluestreak) and the Samba server in Linux (named Waldo).

![](bbox=[0.14, 0.18, 0.82, 0.48])

**Figure 18-6:** View your Linux Samba server from the My Network Places window.

The My Network Places window shows the computers that Windows found on your network. If your server appears on the screen (in my case, the server's name is Waldo), double-click it. Otherwise, you may need to double-click Entire Network, and then open the workgroup that your server is a part of to find your server. The server should show two kinds of resources:

+   - **Printers and Faxes** — A name and an icon should represent each printer and fax shared from the server. To access a printer or fax, double-click it. Windows will have you set up the printer or fax for your computer. After that, you can use the printer or fax as you would any local printer or fax.

+   - **Directories** — A name and folder icon should represent shared directories from the server. Open the directory to see the files and folders in that directory.

Double-click a folder to view the contents of that folder. At this point, you may receive a request to enter a password. Type the password and click OK. You should be able to view the contents of the folder, and its subfolders, at this time.

> **TIP:** If you plan to use the directory often, you may want to assign a drive letter to it. Right-click the folder icon, then select Map Network Drive. Select a drive from the list and, if you like, choose Reconnect at login to have it available when you log on. Then click OK.