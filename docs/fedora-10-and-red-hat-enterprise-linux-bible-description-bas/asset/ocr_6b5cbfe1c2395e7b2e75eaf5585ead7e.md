# Using Samba directories from Windows

While using a Windows system, to see the file and print services available from your Linux Samba server (as well as from other computers on the network), open the Network and Sharing window in Windows Vista. Selections at the bottom of that let let see all the files and folders you and others are sharing.

For other Windows systems, open My Network Places window (for Windows XP) or Network Neighborhood (Windows 98 and other Windows systems). To open the window, select Start -> My Network Places from the Windows XP desktop. Figure 18-6 shows an example of the My Network Places window with shares available from the local Windows XP system (named Bluestream) and the Samba server in linux (named Waldo).

![](bbox=[0.132, 0.31, 0.846, 0.597])

**Figure 18-6:** View your Samba server from the My Network Places window.

My Network Places window shows the computers that Windows found on your network. If your server appears on the screen (in my case, the server's name is Waldo), double-click it. Otherwise, you may need to double-click Entire Network, and then open the group that your server is a part of to find your server. The server shows two kinds of resources:

+   **Printers and Faxes** — A name and an icon should represent each printer and fax shared from the server. To access a printer or fax, double-click it. Windows will have you set the printer or fax for your computer. After that, you can use the printer or fax as you would any local printer or fax.

+   **Directories** — A name and folder icon should represent shared directories from the server. Open the directory to see the files and folders in that directory.