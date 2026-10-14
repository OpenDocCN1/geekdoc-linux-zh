The encryption method is set in the variable CRYPT. By default, it is set to DES. For local files (such as /etc/shadow), the method is changed to Blowfish later in the /etc/default/passwd file using the variable CRYPT_FILES. Another possible encryption method is MD5. YaST also uses the /etc/default/passwd file.

+   - **userdel**—This command lets you delete an existing user account. If you include the option `-r`, the user’s home directory is deleted as well. Before using `userdel -r`, you should determine the user’s UID (`id user`). The UID enables you to locate files outside the user’s home directory (such as `/var/mail/$USER`) that are assigned to the user. To delete these files, enter the command:

```
find / -uid user_ID --exec rm{}\;
```

+   - **usermod**—Modify settings (such as UID, standard shell, home directory, and primary group) for an existing user account. The `usermod` options are basically the same as those for the `useradd` command. The following are examples:
+     - Change the home directory:
+       `usermod --d /data/geeko --m geeko`
+     - Change the UID:
+       `usermod --u 1001 geeko`

You can use the `id` command in a terminal window to display information about a user’s UID and which groups the user is assigned to. For example, entering `id gecko` provides information about the user geeko:

```
geeko@dal0:~> id
uid=1000(geeko) gid=100(users)
groups=16(dialout),33(video),100(users)
geeko@dal0:~>
```

This information includes the following:

+   - *User ID*—uid=1000(geeko)
+   - *Current default (effective) group*—gid=100(users)
+   - *All groups of which geeko is a member*—groups=16(dialout), 33(video), 100(users)

# Manage Groups from the Command Line

You can use the following commands to perform the same group management tasks available with YaST (and some tasks not available with YaST):

![](bbox=[0.101, 0.85, 0.29, 0.925])

You need to be logged in as root (or switch to root by entering `su -`) to use these commands.