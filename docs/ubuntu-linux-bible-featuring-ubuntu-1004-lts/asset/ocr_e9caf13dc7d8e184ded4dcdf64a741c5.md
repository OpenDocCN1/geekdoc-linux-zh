You must least enter the name or IP address of the Windows server that hosts the share you want to connect to. If you are going to access this directory frequently, you can create a permanent entry for it in the Places menu by checking “Add Bookmark” and entering a name for the bookmark on the Places menu. You can also identify the name of the user that you want to connect as, the name of the Windows domain or workgroup you want to connect as, and the share you want to connect to, but all of this is optional—you will be prompted for anything that you do not specify here when you attempt to connect. Click Connect to create a desktop icon for the Windows share that you have defined.

Simply creating a desktop icon for a Windows share doesn't actually establish the connection. To do that, double-click on the appropriate desktop icon to open it. You will see a dialog that prompts you for any required information that you have not specified yet, as shown in Figure 26-9.

# Figure 26-9

Completing authentication information for a Windows share

![](bbox=[0.039, 0.423, 0.865, 0.549])

Once you enter any remaining information about the share that you want to connect to and the server upon which it resides, a Nautilus File Manager window appears that displays the contents of the default directory associated with the user that you are logged in as, as shown in Figure 26-10.

Once the Nautilus File Manager displays, copying files in either direction you use the standard Nautilus and GNOME desktop conventions, as discussed in Chapter 5.

Once you are accessing the Windows share, close the Nautilus File Manager window. To discard the desktop icon, right-click on the icon for the Windows share and select “Unmount Volume” from the pop-up menu to sever the connection and discard the icon. Desktop icons for SMB shares will be automatically removed when you log out. If you want to create a permanent desktop icon, see the sidebar entitled “Creating Permanent Desktop Icons for Services and Locations,” earlier in this chapter, for more information.