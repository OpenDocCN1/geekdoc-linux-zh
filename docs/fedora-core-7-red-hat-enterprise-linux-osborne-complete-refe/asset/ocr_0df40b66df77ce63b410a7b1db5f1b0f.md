# Sharing Windows Printers

To share a printer, locate the printer in the Printers window and right-click it, selecting the Sharing As option. This opens the Sharing panel, where you can click the Shared As button and enter the name under which the printer will be known by other hosts. For example, on the Windows client named lizard, to have a printer called Epson Stylus Color shared as myepson, the Sharing panel for this printer would have the Shared As button selected and the name myepson entered. Then when the user double-clicks the lizard icon in the Computers Near Me window, the printer icon labeled myepson will appear.

For a Linux system to use this printer, it will have be first configured as a remote Windows printer on that Linux system. You can do this easily with system-config-printer (Printing on the System | Administration menu). You can also use the CUPS Print Configuration tool.

To configure your remote printer, you give the printer a name by which it is known on your Linux system, the Windows client computer name, and the name of the printer as it is accessed on the Windows client, along with the username for access (usually **guest**). Once configured, your printing commands can access it using just the printer name, as they would any other printer. For example, the **myepson** printer installed on the Windows client has to also be installed for CUPS on the Linux system operating as the Samba server. For the CUPS print server, you can use system-config-printer to configure your Windows printer. You can give the printer the same name, if you wish. In the New Printer window, you select the Windows Printer via Samba entry in the Select Connection panel. In the facing panel you enter the SMB share name, such as //lizard/myepson. You can also use the share browser below this entry to locate your printer. Here you also select the workgroup used. Once selected, the SMB share name will be entered for you. For Authentication, enter **guest** for the user.

Once it is installed, you can restart the CUPS server. Then an **lpr** command can access the remote Windows printer directly. The next example prints the **mydoc** file on the Windows client's Epson printer:

```
lpr -P myepson mydoc
```

# Windows Clients

To access Samba resources from a Windows system, you will need to make sure that your Windows system has enabled TCP/IP networking. This may already be the case if your Windows client is connected to a Microsoft network. If you need to connect a Windows system directly to a TCP/IP network that your Linux Samba server is running on, you should check that TCP/IP networking is enabled at that Windows system. This involves making sure that the Microsoft Network client and the TCP/IP protocol are installed, and that your network interface card (NIC adapter) is configured to use TCP/IP. The procedures differ slightly on Windows 2000 and XP, and Windows 95, 98, and ME.

Once connected, your Samba shares and printers will appear in the Windows Network window. On Windows XP you can select My Network Places and it will list the Samba shares on your Linux Samba server. If you open View Workgroup Computers, it will list your Samba server (along with any other Samba or Windows systems in your workgroup). The Samba server will have the name given it in the **server string** option along with the netbios name (the host name). Follow the instructions on your particular Windows system for accessing remote shared resources such as printers and directories.