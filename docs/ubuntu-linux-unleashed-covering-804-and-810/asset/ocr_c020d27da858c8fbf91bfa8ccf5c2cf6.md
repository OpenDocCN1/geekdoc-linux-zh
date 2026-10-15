![](bbox=[0.079, 0.092, 0.773, 0.49])

FIGURE 16.3  Configure Samba to allow access from specific hosts or subnets on your LAN.

When finished, click the Commit Changes button to save the global access settings. The next step is to create a Samba user and set the user's password. Click the Password icon on the main SWAT page (refer to Figure 16.2). The Server Password Management page opens, as shown in Figure 16.4. Type a username in the User Name field; then type a password in the New Password and Re-type New Password fields.

> **NOTE**
> 
> You must supply a username of an existing system user, but the password used for Samba access does not have to match the existing user's password.

When finished, click the Add New User button. SWAT then creates the username and password and displays Added user *username* (where *username* is the name you entered). The new Samba user should now be able to gain access to the home directory from any allowed host if the Samba (smb) server is running.

For example, if you have set up Samba on a host named *mini* that has a user named *andrew*, the user can access the home directory on *mini* from any remote host (if allowed by the Globals settings), perhaps by using the smbclient command like so:

```
```bash
$ smbclient //mini/andrew -U andrew
```
```