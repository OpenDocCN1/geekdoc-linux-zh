that PAM modules cannot support the challenge/response authentication mechanism needed in the presence of SMB password encryption.

# **only user (S)** Default: *only user = no*

This is a boolean option that controls whether connections with usernames not in the *user* list will be allowed. By default this option is disabled so that a client can supply a username to be used by the server. Enabling this parameter will force the server to only use the login names from the *user* list and is only really useful in *security = share level* security.

Note that this also means Samba won't try to deduce usernames from the service name. This can be annoying for the [*homes*] section. To get around this you could use *user = %S* which means your *user* list will be just the service name. which for home directories is the name of the user.

# **oplock break wait time (G)** Default: *oplock break wait time = 0*

This is a tuning parameter added due to bugs in both Windows 9x and WinNT. If Samba responds to a client too quickly when that client issues an SMB that can cause an oplock break request, then the network client can fail and not respond to the break request. This tuning parameter (which is set in milliseconds) is the amount of time Samba will wait before sending an oplock break request to such (broken) clients.

> **WARNING**
> 
> DO NOT CHANGE THIS PARAMETER UNLESS YOU HAVE READ AND UNDERSTOOD THE SAMBA OPLOCK CODE.

# **oplock contention limit (S)** Default: *oplock contention limit = 2*

This is a *very* advanced smbd(8) tuning option to improve the efficiency of the granting of oplocks under multiple client contention for the same file.

In brief it specifies a number, which causes smbd(8) not to grant an oplock even when requested if the approximate number of clients contending for an oplock on the same file goes over this limit. This causes smbd to behave in a similar way to Windows NT.