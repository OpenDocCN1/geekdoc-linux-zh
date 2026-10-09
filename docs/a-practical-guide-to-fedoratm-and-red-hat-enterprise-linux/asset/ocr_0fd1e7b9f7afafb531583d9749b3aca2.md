# smbpasswd AND pdbedit: Work with Samba Users and Passwords

Samba can use Linux passwords or Samba passwords to authenticate users. The **passdb backend** (page 842) parameter in the **smb.conf** (page 839) configuration file controls which type of passwords Samba uses. Setting **passdb backend** to tdbsam (default) causes Samba to use Samba passwords. Samba stores the passwords in a Trivial Database (tdb.sourceforge.net). Setting **passdb backend** to smbpsswd causes Samba to use Linux passwords that are stored in the text file named /etc/samba/smbpasswd. This section discusses how to use **smbpasswd** to work with Samba passwords and how to use **pdbedit** to display Samba users.

With the -L option, **pdbedit** displays a list of Samba users; when you install Samba, no Samba users are defined:

```
```
# pdbedit -L
#
```
```

The Samba user named **nobody** does not have to exist for the Windows user named **guest** to log in as the Anonymous user. See “The user named **guest**” in the preceding section for more information.

As installed, no users have Samba passwords (there are no Samba users). You can add Samba users and optionally passwords only for users listed in **/etc/passwd**. Working with **root** privileges, use **smbpasswd** with the -a option to add a Samba user and password for a Linux user (a user listed in /etc/passwd):

```
```
# smbpasswd -a sam
New SMB password:
Retype new SMB password:
Added user sam.
```
```

The **pdbedit** utility shows the Samba user you just added, although it does not display password information:

```
```
# pdbedit -L
sam:1000:Sam the Great
```
```

Once a user has a Samba password, he can use **smbpasswd** without any arguments to change his password. The **smbpasswd** utility will display a nondescriptive error message if the new password is too simple or if the two passwords you enter do not match.

```
```
$ smbpasswd
Old SMB password:
New SMB password:
Retype new SMB password:
Password changed for user sam
```
```

If a user has different usernames on the Linux and Windows systems, you must map the Windows username to a Linux username (see “User maps” on page 830). Except for the Windows user specified by the **guest** account (page 842), make sure all Linux users who will log in using Samba have Samba passwords.