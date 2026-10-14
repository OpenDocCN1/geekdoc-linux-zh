If you want to allow users to browse to their home folder, change the browseable setting to yes.

+   6. Remove the comment from the read only line, and change the setting to no. This allows your users to write files to their home folder:
+   ```
+   read only = no
+   ```

+   7. Remove the comment from the valid users line. This setting restricts users to connecting only to their own home folder:
+   ```
+   valid users = %S
+   ```

+   8. Remove the comments from the printing and printcap name lines for the CUPS server entry. This enables your Samba server to share any printers defined in the CUPS server:
+   ```
+   printing = cups
+   printcap name = cups
+   ```

+   9. Save the new smb.conf file and exit the editor.

Now you have the Samba server configuration set for your network environment. The next step is to create the Samba account passwords for your users.

# Defining Samba Passwords

The default Samba configuration in Ubuntu uses the Ubuntu user account system to track users in the Samba configuration. However, there’s one problem with this setup. When a user attempts to connect to the Samba server with his or her userID, Windows servers and clients pass the password using an encryption scheme. Samba must know what the encrypted password is to be able to authenticate the user login request.

To do that, the Samba software maintains a separate password file that contains the user passwords encrypted by the Windows encryption algorithm. You must set the Samba user passwords separate from the Ubuntu passwords for this to work.

The tool used to encrypt Samba passwords is called smbpasswd. You must use the smbpasswd program to define each Ubuntu user account that’s going to access the Samba server. To define a user account password for the first time, you must use the -a parameter:

```
rich@testbox:~$ sudo smbpasswd -a test
New SMB password:
Retype new SMB password:
Added user test.
rich@testbox:~$
```

This creates a Samba password for the new user account. If you need to change the password for the account, you don’t need the -a parameter:

```
rich@testbox:~$ sudo smbpasswd test
New SMB password:
Retype new SMB password:
rich@testbox:~$
```

You’ll need to do this for all Ubuntu users who want to connect to their home folder as a Windows shared drive via the network.