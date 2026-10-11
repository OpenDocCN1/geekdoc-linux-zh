is only useful for installations using the Windows NT domain administration tools. The script is free to create a group with an arbitrary name to circumvent unix group name restrictions. In that case the script must print the numeric gid of the created group on stdout.

# add machine script (G) Default: *No default*

Example: *add machine script = /usr/sbin/adduser -n -g machines -c Machine -d /var/lib/nobody -s /bin/false %u*

This is the full pathname to a script that will be run by smbd(8) when a machine is added to it’s domain using the administrator username and password method.

This option is only required when user sam back-ends tied to the Unix uid method of RID calculation such as smbpasswd. This option is only available in Samba 3.0.

# addprinter command (G) Default: *No default*

Example: *addprinter command = /usr/bin/addprinter*

With the introduction of MS-RPC based printing support for Windows NT/2000 clients in Samba 2.2, The MS Add Printer Wizard (APW) icon is now also available in the "Printers..." folder displayed a share listing. The APW allows for printers to be add remotely to a Samba or Windows NT/2000 print server.

For a Samba host this means that the printer must be physically added to the underlying printing system. The *add printer command* defines a script to be run which will perform the necessary operations for adding the printer to the print system and to add the appropriate service definition to the **smb.conf** file in order that it can be shared by smbd(8).

The *addprinter command* is automatically invoked with the following parameter (in order):

+   - *printer name*
+   - *share name*
+   - *port name*
+   - *driver name*
+   - *location*
+   - *Windows 9x driver location*

All parameters are filled in from the PRINTER_INFO 2 structure sent by the Windows NT/2000 client with one exception. The "Windows 9x driver location" parameter is included for *backwards compatibility only*. The remaining fields in the structure are generated from answers to the APW questions.