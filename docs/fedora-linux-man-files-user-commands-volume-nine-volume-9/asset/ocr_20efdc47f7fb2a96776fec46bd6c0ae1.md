If specified, this parater suppresses the normal password prompt from the client to the user. This is useful when accessing a service that does not require a password. Unless a password is specified on the command line or this parater is specified, the client will request a password.

If a password is specified on the command line and this option is also defined the password on the command line will be silently ignored and no password will be used.

-k|---kerberos
Try to authenticate with kerberos. Only useful in an Active Directory environnt.

-C|--use-ccache
Try to use the credentials cached by winbind.

-A|--authentication-file=filena
This option allows you to specify a file from which to read the userna and password used in the connection. The format of the file is
userna = <value> password = <value> domain = <value>
Make certain that the permissions on the file restrict access from unwanted users.

-U|--user=userna[%password]
Sets the SMB userna or userna and password.
If %password is not specified, the user will be prompted. The client will first check the **USER** environnt variable, then the **LOGNAME** variable and if either exists, the string is uppercased. If these environmental variables are not found, the userna **GUEST** is used.
A third option is to use a credentials file which contains the plaintext of the userna and password. This option is mainly provided for scripts where the admin does not wish to pass the credentials on the command line or via environnt variables. If this thod is used, make certain that the permissions on the file restrict access from unwanted users. See the -A for more details.
Be cautious about including passwords in scripts. Also, on many systems the command line of a running process may be seen via the ps command. To be safe always allow rpcclient to prompt for a password and type it in directly.

-S|---signing on/off/required
Set the client signing state.