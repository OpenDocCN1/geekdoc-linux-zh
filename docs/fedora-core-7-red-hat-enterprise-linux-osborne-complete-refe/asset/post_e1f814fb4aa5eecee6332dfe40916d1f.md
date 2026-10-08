
Samba also provides its own Samba password PAM module, `pam_smbpass.so`. With this module, you provide PAM authentication support for Samba passwords, enabling the use of Windows hosts on a PAM-controlled network. The module could be used for authentication and password management in your PAM **samba** file. The following entries in the PAM **samba** file would implement PAM authentication and passwords using the Samba password database:

```
auth required pam_smbpass.so nodelay
password required pam_smbpass.so nodelay
```

Be sure to enable PAM in the **smb.conf** file:

```
obey pam restrictions = yes
```

### Samba Passwords: smbpasswd

With user-level security, access to Samba server resources by a Windows client is allowed only to users on that client. Each user on the Windows client has to have a corresponding account on the Samba server. A user logs in to his or her Windows account and then, when accessing a Samba share or printer, has to log in using the Windows account name specified for Samba server access. The user name and password used to access the Samba server has to be registered in the Samba password database.

Note: If you are using the older smbpasswd file, you can use the `mkssmbpasswd.sh` script to generate an smbpasswd file made up of all the users listed in your `/etc/passwd` file. You pipe the contents of the passwd file to `mkssmbpasswd.sh` and then use redirection (`>`) to create the file.

### Adding and Changing Passwords

You use the `smbpasswd` command to add, or later change, passwords. To add or change a password for a particular user, you use the `smbpasswd` command with the username:

```bash
# smbpasswd dylan
New SMB Password: new-password
Repeat New SMB Password: new-password
```

Users can use `smbpasswd` to change their own password. The following example shows how you would use `smbpasswd` to change your Samba password. If the user has no Samba password, that user can just press the ENTER key.

```bash
$ smbpasswd
Old SMB password: old-password
New SMB Password: new-password
Repeat New SMB Password: new-password
```

Should you want to use no passwords, you can use smbpasswd with the `-n` option. The **smb.conf** file will have to have the **null passwords** option set to yes.

Note: If you are using the older smbpaswords file, be sure that Samba is configured to use encrypted passwords. Set the **encrypt passwords** option to **yes** and specify the SMB password file.

## Managing Samba Users: smbpasswd and pdbedit

The easiest way to manage Samba users is to use the system-config-samba tool. Click Preferences to select Samba Users. In this window you can then add, edit, or remove Samba users. In the SWAT tool you would use the Password panel.

To manage users you can either use the `smbpasswd` command or the `pdbedit` tool. The `smbpasswd` command with the `-a` option will add a user and the `-x` option will remove one.

```
smbpasswd -a aleina
```

To enable or disable users you would use the `-e` and `-d` options.

The smbpasswd command will operate on both the older smbpsswd file or the newer ttdbsam backend database files. For just the ttdbsam backend database files you can use `pdbedit` instead. To add a user you would use the `-a` option and to remove a user you use the `-x` option.

```
pdbedit -a larisa
```

This is a command line tool with options for adding and removing users, as well as features like changing password and setting the home directory. You can also import or export the user entries to or from other backend databases.

The `pdbedit` command lets you display more information about users. To display users from the backend database you could use the `-L` option. Add the `-v` option for detailed information. For a particular user add the user name.

```
pdbedit -Lv richard
```

For domain policies like minimum password length or retries, you use the `-P` option.

```
pdbedit -P
```

You use the `-i` and `-e` options to import and export database entries. The following will import entries from the old `smbpasswd` file to the new `tdbsam` backend database.

```
pdbedit -i smbpasswd -e tdbsam
```

If your system is using LDAP-enabled Samba database, then use the smbldap tools to manage users and groups.

## Configuring Samba with system-config-samba

The system-config-samba tool provides a simple means to configure your Samba server, adding Samba users and specifying Samba shares. It will also automatically configure all the printers on your Linux system as Samba shared printers, allowing you to use them from a connected Windows system. You can start system-config-samba from the Samba entry in the Server Settings menu, accessible from the System Setting menu. The system-config-samba tool will list all the shares for your server. You can use buttons at the top to manage your shares, adding new ones or deleting current ones. If you delete, the actual directories are not removed; they just lose their status as shared directories.

### Server Configuration with system-config-samba

To configure your Samba server, select Server Settings from the Preferences menu. This opens a window with two panels, Basic and Security. On the Basic panel, you enter the Samba server workgroup name. This will be the same name used as the workgroup by all your Windows systems. For example, if you are using the group name, WORKGROUP, for your Windows systems, you would enter WORKGROUP here. The description is the name you want displayed for your Samba server on your Windows systems. On the Security panel, you specify the authentication mode, the password encryption option, and the name of the guest account, along with the authentication server.

- As explained in detail later, the authentication mode specifies the access level, which can be user, share, server, or domain. User-level access restricts access by user password, whereas share access opens access to any guest.
- Normally, you would elect to encrypt passwords, rather than have them passed over your network in plain text.
- The Guest user is the name of the account used to allow access to shares or printers that you want open to any user, without having to provide a password. The pop-up menu will list all your current users, with nobody as the selected default.

### Adding Samba Users with system-config-samba

With system-config-samba, you can add users and shares easily. User-level access restricts Windows users to those that are assigned corresponding account on the Samba server. Samba maintains its own password listing for users. To provide a user Samba access, you need to register the user as a Samba user, giving them a Samba password. Select Samba Users from the Preferences menu to open the Samba Users window, clicking the Add User button. Here you enter the Unix Username, the Windows Username, and the Samba Password. There is an additional box for confirming the Samba password. The Unix Username is a pop-up window listing all the users on your Samba server.

### Specifying Samba Shares with system-config-samba

Click Add to add a share, or select Add Share from the File menu. On the Basic panel, you can then enter the directory on the Samba server that you want to share, specifying the full pathname. The Browse button lets you search and select a directory. You can also set permissions to either read-only or read/write. On the Access panel, you can restrict access to certain users or allow access to all users. All Samba users on your system will be listed with check boxes where you can select those you want to give access.

## The Samba smb.conf Configuration File

You configure the Samba daemon using the `smb.conf` file located in the `/etc/samba` directory. The file is separated into two basic parts: one for global options and the other for shared services. A shared service, also known as *shares*, can either be filespace services (used by clients as an extension of their native file systems) or printable services (used by clients to access print services on the host running the server). The filespace service is a directory to which clients are given access; they can use the space in it as an extension of their local file system. A printable service provides access by clients to print services, such as printers managed by the Samba server.
