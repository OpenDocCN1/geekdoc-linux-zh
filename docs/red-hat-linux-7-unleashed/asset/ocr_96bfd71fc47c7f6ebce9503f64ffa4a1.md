If not, verify that the user and password used on the Windows client is matched by a user/password combination in **smbpasswd**. You can verify that you’re really authenticating on the server by changing the password on the server, using the **smbpasswd** command, and then verifying that client logons now fail. Naturally, the original password must then be restored.

# ## Enabling a Server-Hosted Logon Script

It’s very handy to implement a server-hosted logon script. This section outlines a simple scheme, administered only by user root.

Start by creating directory `/home/netlogon/scripts`, owner and group root, mode 755.

Add the following to the **smb.conf** [**global**] section:

```
logon script=scripts\%u.bat
```

### Caution

Danger of time waste! Much time is wasted troubleshooting logon script problems resulting from treating logon scripts as UNIX files. Symptoms resulting from this mistake are elusive to track.

Always use backslashes (never forward slashes) in the logon script parameter. Always use backslashes in commands within the logon script. Most elusive, always save the logon script as a DOS format file, with CRLF line separators.

Within the vi editor, this can be accomplished by executing the following command before writing your file:

```
:set fileformat=dos
```

At the risk of beating a dead horse, logon script problems resulting from forward slashes and UNIX style files can bite you over and over again, costing up to an hour each time. The best prevention is to be very aware of this, and check at the first sign of problems with logon scripts.

The preceding Samba parameter specifies that the logon script is a .bat file with a file-name identical to the user, located in the **scripts** directory below the special [**netlogon**] share.

Create the [**netlogon**] share as follows:

```
[netlogon]
path=/home/netlogon
writable=no
guest ok=no
oplocks=no
```