```
[global]
security = user
```

The third way is to store the user password on an NT Domain Controller. This allows a Samba server to be a regular file server in a Domain, and have clients log into the Domain. This does not mean that /etc/passwd is no longer used, just that instead of storing the user account (passwd etc) information in the smbpasswd data file, it now resides in the Domain Controller.

```
[global]
security = domain
```

or

```
[global]
security = server
```

There are two other ways of working a Samba server into your environment using the winbind daemon and LDAP. I will discuss these later. These involve replacement of both the /etc/passwd and the smbpasswd files and some chicanery with the nss switch.

**3.8.13.1 User Accounts.** Every user that connects to the Samba server must have a user account. Never forget that underneath Samba is a UNIX box, and the access rules for Linux provide a foundation for Samba. There are many ways to provide user accounts, /etc/passwd, NIS, winbind, and LDAP.

**3.8.13.1.1 Local Authentication.** This is the simplest of all authentication methods. Of the popular distributions I have used have had a default Samba configuration file that used the /etc/passwd and /etc/group to keep track of user accounts. The Windows encrypted passwords are stored in the smbpasswd file. On Red Hot, this is /etc/samba/smbpasswd.

Each user needs access to the Samba server will need an account in /etc/passwd, which can be added with useradd options username. To create the necessary smbpasswd entry,

```
smbpasswd -a username

command will to be run.
An example would be:
```

```
useradd -g users -d /dev/null -s /dev/null -n -u 500 bob
smbpasswd -a bob
```

This is the most secure user account you can create (I think). There is no home directory, nor is there a default shell. This user can access only the Samba shares that the SysAdmin permits them to.