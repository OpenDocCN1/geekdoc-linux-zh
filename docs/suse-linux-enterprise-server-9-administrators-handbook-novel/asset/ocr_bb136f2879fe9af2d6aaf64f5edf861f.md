— if you click Abort, any changes made (including new users “added”) will be discarded.

# TIP

You can select Expert Options, Write Changes Now to save the changes made thus far, without exiting the module.

The procedure for updating and deleting a user is similar: Instead of Add, select Edit or Delete after highlighting the desired user.

# TIP

If you change a user’s UID, YaST will normally change all file ownerships in the user's home directory. If for some reason YaST fails to do this automatically, you can use the `chown -R username /home/username` command to change the ownerships.

# TIP

When a user's UID is changed using YaST, only the ownership permissions for files in the home directory are adjusted. Changes to the permissions on files that may be located elsewhere on the system are not made.

To find all files on a system owned by a particular user, you can use the find command:

```
find / -uid id_number -print
```

find is a very powerful and useful program that can perform specific functions (via the exec switch) on found files. For instance, the following command will change all files belonging to UID 1000 to UID 1002:

```
find / -uid 1000 -exec chown 1002 {} \;
```

Being familiar with it will add a great tool to your bag of tricks. See `man find` for more information.

When you use YaST, you can manage most aspects of the user account within the single application, except you cannot use YaST to enable or disable a user account—you must do this using command-line tools. In addition, because YaST is a menu-driven utility, it does not lend itself to batch creation or modification of user accounts easily. Therefore, we highlight the multistep user-creation process necessary when using the command-line tools.