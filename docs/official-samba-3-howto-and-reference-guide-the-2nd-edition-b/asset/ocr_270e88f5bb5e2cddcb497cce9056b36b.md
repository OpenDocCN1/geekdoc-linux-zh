Home Directory: \BERSERKER\samba

HomeDir Drive:

Logon Script:

Profile Path: \BERSERKER\profile

-w This option sets the `smbpasswd(5)` listing format. It will make pdbedit list the users in the database, printing out the account fields in a format compatible with the `smbpasswd` file format. (See the `smbpasswd(5)` for details)

Example: `pdbedit -L -w`

```
sorce:500:508818B733CE64B4BEAD3B435B51404EE:
	D2A2418EFC466A8A0F6B1DBB5C3DB80C:
	[UX]		J:LCT-00000000:
samba:45:0F29255F7B67A7A9AAD3B435B51404EE:
	BC281CE3F53B6A5146629CD4751D3490:
	[UX]		J:LCT-3BF41E8D:
```

-u username This option specifies the username to be used for the operation requested (listing, adding, removing). It is *required* in add, remove and modify operations and *optional* in list operations.

-f fullname This option can be used while adding or modifying a user account. It will specify the user's full name.

Example: `-f "Simo Sorce"`

-h homedir This option can be used while adding or modifying a user account. It will specify the user's home directory network path.

Example: `-h \BERSERKER\sorce"`

-D drive This option can be used while adding or modifying a user account. It will specify the windows drive letter to be used to map the home directory.

Example: `-d "H:"`

-S script This option can be used while adding or modifying a user account. It will specify the user's logon script path.

Example: `-S \BERSERKER\netlogon\sorce.bat"`