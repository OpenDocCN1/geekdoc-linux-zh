If the service is marked `“guest only = yes”` and the server is running with share-level security (`“security = share”`, steps 1 to 5 are skipped.

+   1.  If the client has passed a username/password pair and that username/password pair is validated by the UNIX system's password programs, the connection is made as that user-name. This includes the `\server\service%username` method of passing a username.
+   
+   2.  If the client has previously registered a username with the system and now supplies a correct password for that username, the connection is allowed.
+   
+   3.  The client's NetBIOS name and any previously used usernames are checked against the supplied password. If they match, the connection is allowed as the corresponding user.
+   
+   4.  If the client has previously validated a username/password pair with the server and the client has passed the validation token, that username is used.
+   
+   5.  If a user = field is given in the smb.conf file for the service and the client has supplied a password, and that password matches (according to the UNIX system's password checking) with one of the usernames from the user = field, the connection is made as the username in the user = line. If one of the usernames in the user = list begins with a @, that name expands to a list of names in the group of the same name.
+   
+   6.  If the service is a guest service, a connection is made as the username given in the guest account = for the service, irrespective of the supplied password.

# EXPLANATION OF EACH PARAMETER

**abort shutdown script (G)** Default: *No default*

*Example: abort shutdown script = /sbin/shutdown -c*

This a full path name to a script called by smbd(8) that should stop a shutdown procedure issued by the *shutdown script*.

If the connected user possesses the *SeRemoteShutdownPrivilege*, right, this command will be run as user.

**acl compatibility (S)** Default: *acl compatibility = Autowin2k*

*Example: acl compatibility = win2k*

This parameter specifies what OS ACL semantics should be compatible with. Possible values are *nt4* for Windows NT 4, *win2k* for Windows 2000 and above and *auto*. If you specify *auto*, the value for this parameter will be based upon the version of the client. There should be no reason to change this parameter from the default.