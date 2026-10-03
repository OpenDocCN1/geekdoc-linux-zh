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