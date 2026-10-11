error message for up to one second, allowing the client to close the file causing the violation in the meantime.

Unix by default does not have this behaviour.

There should be no reason to turn off this parameter, as it is designed to enable Samba to more correctly emulate Windows.

# delete group script (G) Default: *No default*

This is the full pathname to a script that will be run *AS ROOT* smbd(8) when a group is requested to be deleted. It will expand any *%g* to the group name passed. This script is only useful for installations using the Windows NT domain administration tools.

# deleteprinter command (G) Default: *No default*

Example: *deleteprinter command = /usr/bin/removeprinter*

With the introduction of MS-RPC based printer support for Windows NT/2000 clients in Samba 2.2, it is now possible to delete printer at run time by issuing the DeletePrinter() RPC call.

For a Samba host this means that the printer must be physically deleted from underlying printing system. The *deleteprinter command* defines a script to be run which will perform the necessary operations for removing the printer from the print system and from *smb.conf*.

The [sub]acmfopion] / [subcomfopion] is automatically called with only one parameter: *printer name*.

Once the *deleteprinter command* has been executed, **smbd** will reparse the **smb.conf** to associated printer no longer exists. If the sharename is still valid, then **smbd** will return an ACCESS_DENIED error to the client.

# delete readonly (S) Default: *delete readonly = no*

This parameter allows readonly files to be deleted. This is not normal DOS semantics, but is allowed by UNIX.

This option may be useful for running applications such as rcs, where UNIX file ownership prevents changing file permissions, and DOS semantics prevent deletion of a read only file.

# delete share command (G) Default: *No default*

Example: *delete share command = /usr/local/bin/delshare*