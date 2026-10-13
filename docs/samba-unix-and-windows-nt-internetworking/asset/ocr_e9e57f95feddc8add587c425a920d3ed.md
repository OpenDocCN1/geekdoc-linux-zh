Now you can reboot the machine. To finish up, you'll need to update the NetBIOS Name List and Broadcast List for name service by running MPTS configuration and selecting Adapters and Protocol Services → Configure → LAN Adapters and Protocols. Highlight IBM OS/2 NETBIOS OVER TCP/IP and select Edit. On the NetBIOS over TCP/IP panel, bring up the Edit/Change menus for the NetBIOS and broadcast lists. Finally, register the name list changes by invoking IBMCOM/RFCADDR.

# Macintosh

The DAVE toolkit distributed by Thursby Software Systems, Inc., brings the CIFS/SMB world onto the Macintosh desktop. DAVE implements all services defined by the CIFS protocol, as well as WINS support and Windows domain logins. A DAVE client can act as both CIFS/SMB client and CIFS/SMB server. Other features include support for WinPopup messages and network printing.

DAVE clients access CIFS/SMB services using the standard Macintosh chooser interface (Figure 13.6). From the chooser, users can interact with Windows workgroup and domain services just as they would if they resided in a local Appletalk network. Windows clients interact with resources residing on a Macintosh server using standard browse interfaces like Network Neighborhood.

![](bbox=[0.22, 0.48, 0.82, 0.71])

Figure 13.6: DAVE CIFS/SMB chooser interface

DAVE is compatible with Windows 9x, Windows NT and Windows 2000. For more information, refer to the Thursby Web page: http://www.thursby.com.

# Summary

+   - Samba supports UNIX client access to remote CIFS/SMB servers via the `smbclient`, `smbwrapper`, `smbtar`, and `smbprint` routines.