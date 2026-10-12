# # Basic Windows 9x Logon Authentication

In the following sample *smb.conf*, the server’s hostname is **mainserver**, the workgroup is **MYGROUP**, the Windows 9x clients all use encrypted passwords, and there is no WINS server or domain controller other than the Samba server:

```
```text
[global]
netbios_name=mainserver
workgroup=MYGROUP
encrypt_passwords=yes

wins_support=yes
preferred_master=yes
domain_master=yes
domain_logons=yes

[homes]
writeable=yes
```
```

Restart Samba and you now have a server capable of assuming the logon authentication duties for Windows 9x clients. The next step is to set up the clients and users.

Each potential user must have a valid UNIX account and a valid **smbpasswd** entry. Assuming the user has a valid UNIX account, setting up the **smbpasswd** entry is simply a matter of doing the following as *root*:

```
```bash
# smbpasswd -a slitt
```
```

The preceding adds an **smbpasswd** entry for user *slitt* by prompting for the password and a password confirmation. The password should be the same as used on the client.

Now that the user is taken care of, modify the client computer to authenticate against Samba instead of locally. On the Windows 9x client, right-click any Network Neighborhood icon and choose *Properties* to pull up the *Network Dialog Box*. Select the *Configuration* tab, and highlight *Client for Microsoft Networks* in the *The Following Network Components Are Installed* drop-down list, and click the *Properties* button to bring up the *Client for Microsoft Networks Properties* dialog box.

Check the *Logon to Windows NT Domain* checkbox, type the workgroup name of the Samba server (which should match the client) in the *Windows NT Domain* text box, and check the *Logon and Restore Network Connections* radio button. Click OK all the way out of all dialog boxes, and answer affirmatively when asked if you want to restart the computer.

Upon restart, the Windows logon screen contains a third field, the *domain*. In the domain field, type in the workgroup name for the Samba server (which should already match the client workgroup name on the identification tab of the Network dialog box). If all is well, you’re logged in.