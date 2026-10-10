```
```
userdel $user_account          #delete user account
echo
echo "User account, $user_account, has been removed"
echo
#
exit
$   ```
```

That was lots of work! However, the `delete_User.sh` script is a great time-saver and helps you avoid lots of nasty problems when deleting local user accounts.

# ## Running the script

Because it is intended to function as an interactive script, the `Delete_User.sh` script should not be placed in the `cron` table. However, it is still important to ensure that it works as expected.

Before the script is tested, the appropriate permissions are set on the script's file:

```
```
$ chmod u+x Delete_User.sh
$
$ ls -og Delete_User.sh
-rwxr-xr-x 1 6111 Aug 12 14:18 Delete_User.sh
$   ```
```

> > **NOTE**
> >
> > To run this type of script, you must either be logged in as the root user account or use the `sudo` command to run the script with super user privileges.

The script is tested by removing an account, `consultant`, that was set up for a company's temporary consultant on this system:

```
```
$ sudo ./Delete_User.sh
[sudo] password for christine:
Step #1 - Determine User Account name to Delete

Please enter the username of the user
account you wish to delete from system: consultant
Is consultant the user account   ```
```