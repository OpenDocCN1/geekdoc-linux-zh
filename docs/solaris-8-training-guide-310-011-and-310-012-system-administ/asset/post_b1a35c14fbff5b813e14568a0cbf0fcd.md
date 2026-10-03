
## TABLE 20.1
### roleadd Options

| Option | Description |
|---|---|
| `-c <comment>` | Any text string to provide a brief description of the role. |
| `-d <dir>` | The home directory of the new role account. |
| `-m` | Creates the new role's home directory if it does not already exist. |
| `-s <shell>` | Specifies the user's shell on login. The default is /bin/sh. |
| `-A <authorization>` | Both of these options respectively assign authorizations and profiles to the role. |
| `-P <profile>` | Authorizations and profiles are described later in this section. |

The other options are the same options that were described for the useradd command, outlined in Chapter 5, “Setting Up User Accounts.”

When creating a role account with the roleadd command, you need to specify an authorization and profile to the role. An authorization is a user right that grants access to a restricted function. It is a unique string that identifies what is being authorized as well as who created the authorization.

Certain privileged programs check the authorizations to determine whether users can execute restricted functionality. Following are the predefined authorizations from the /etc/security/auth_attr file that apply to the tasks to be delegated:

```
solaris.admin.usermgr.pswd:::Change User Passwords::help=UserMgrPswd.html
solaris.system.shutdown:::Shutdown the System::help=SysShutdown.html
solaris.admin.fsmgr.write:::Mount/Share File Systems::help=FsMgrWrite.html
```

All authorizations are stored in the auth_attr database, so the system administrator needs to use one or more of the authorizations that are stored in that file. For the Acme Corp. example, the system administrator needs to specify the authorizations named, as shown here:

```
solaris.admin.usermgr.pswd
solaris.system.shutdown
solaris.admin.fsmgr.write
```

Therefore, the system administrator would issue the roleadd command as follows:

```
roleadd -m -d /export/home/adminusr -c "Admin Assistant" \
-A solaris.admin.usermgr.pswd,solaris.system.shutdown, \
solaris.admin.fsmgr.write adminusr
```

A role account named adminusr with the required directory structures has been created. The next step is to set the password for the adminusr role account by typing the following:

```
passwd adminusr
<enter the new password twice>
```

Now we need to set up Neil's account so he can access the new role account named adminusr. With the usermod command, we assign the role to the user account using the -R option as follows:

```
usermod -R adminusr neil
```

To access the administrative functions, Neil needs to first log in using his regular user account named neil. Neil can check which roles he has been granted by typing the following:

```
roles
```

The system responds with the roles that have been granted to the user account neil as follows:

```
adminusr
```

Neil then needs to su to the adminusr account by typing the following:

```
su adminusr
<enter the password for adminusr>
```

Now, Neil can modify user passwords, shut down the system, and mount and share file systems. Any other user trying to su to the adminusr account gets this message:

```
$ su adminusr
Password:
Roles can only be assumed by authorized users
su: Sorry
$
```

If later on, the system administrator wants to assign additional authorizations to the role account named adminusr, he would do so using the rolemod command. The rolemod command modifies a role's login information on the system. The syntax for the rolemod command is as follows:

```
rolemod [-u uid] [-o] [-g group] [-G group] [-d dir] [-m] \
[-s shell] [-c comment] [-l new_name] [-f inactive] \
[-e expire] [-A Authorization] [-P profile] <role account>
```

Options to the rolemod command are described in Table 20.2.

## TABLE 20.2
### rolemod Options

| Option | Description |
|---|---|
| -A <authorization> | One or more comma-separated authorizations as defined in the auth_attr database. This replaces any existing authorization setting. |
| -c <comment> | Specifies a comment string. <comment> can be any text string. It is generally a short description of the login, and is currently used as the field for the user's full name. This information is stored in the user's /etc/passwd entry. |
| -d <dir> | Specifies the new home directory of the role. It defaults to <base_dir>/login, in which <base_dir> is the base directory for new login home directories, and login is the new login. |
| -e <expire> | Specifies the expiration date for a role. After this date, no user can access this role. The <expire> option argument is a date entered using one of the date formats included in the template file /etc/datemsk. For example, you can enter 12/30/01 or December 30, 2001. A value of " " defeats the status of the expired date. |
| -f <inactive> | Specifies the maximum number of days allowed between uses of a login ID before that login ID is declared invalid. Normal values are positive integers. |
| -g <group> | Specifies an existing group's integer ID or character-string name. It redefines the role's primary group membership. |
| -G <group> | Specifies an existing group's integer ID or character string name. It redefines the role's supplementary group membership. Duplicates between groups with the -g and -G options are ignored. |

## TABLE 20.2 continued
### rolemod OPTIONS

| Option | Description |
|---|---|
| -l <new_logname> | Specifies the new login name for the role. The <new_logname> argument is a string no more than eight bytes long, consisting of characters from the set of alphabetic characters, numeric characters, period (.), underline (_), and hyphen (-). The first character should be alphabetic, and the field should contain at least one lowercase alphabetic character. A warning message is written if these restrictions are not met. A future Solaris release might refuse to accept login fields that do not meet these requirements. The <new_logname> argument must contain at least one character and must not contain a colon (:) or NEWLINE (\n). |
| -m | Moves the role's home directory to the new directory specified with the -d option. If the directory already exists, it must have permissions read/write/execute by group, in which group is the role's primary group. |
| -o | Allows the specified UID to be duplicated (non-unique). |
| -P <profile> | Replaces any existing profile setting. One or more comma-separated execution profiles are defined in the auth_attr database. |
| -s <shell> | Specifies the full pathname of the program that is used as the role's shell on login. The value of shell must be a valid executable file. |
| -u <uid> | Specifies a new UID for the role. It must be a non-negative decimal integer. The UID associated with the role's home directory is not modified with this option; a role does not have access to its home directory until the UID is manually reassigned using the chown command. |

To add the ability to purge log files, you need to add solaris.admin.logsvc.purge to the list of authorizations for adminusr. To do this, issue the rolemod command as follows:

```
rolemod -A \
solaris.admin.usermgr.pswd,solaris.system.shutdown, \
solaris.admin.fsmgr.write,solaris.admin.logsvc.purge \
adminusr
```

If you want to remove a role account, use the roledel command as follows:

```
roledel [-r] <role account name>
```

The -r option removes the role's home directory from the system. For example, to remove the adminusr role account, issue the following command:

```
roledel -r adminusr
```

The next section discusses each of the RBAC databases in detail, describing the entries made when I executed the roleadd and usermod commands.

> NOTE
The rolemod command does not add to the existing authorizations; it replaces any existing authorization setting.

## RBAC COMPONENTS

RBAC relies on the following four databases to provide users access to privileged operations:

- user_attr (extended user attributes database). Associates users and roles with authorizations and profiles.
- auth_attr (authorization attributes database). Defines authorizations and their attributes and identifies the associated help file.
- prof_attr (rights profile attributes database). Defines profiles, lists the profile's assigned authorizations, and identifies the associated help file.
- exec_attr (profile attributes database). Defines the privileged operations assigned to a profile.

These four databases interact with each other.
