Apache includes a Perl utility called dbmmanage (usually installed in /usr/sbin) that you can use to create the DBM database initially and to populate the database with new users and groups. The command-line usage of dbmmanage is as follows:

```
dbmmanage filename [ command [ username [pw [group1[,group2] [encpasswd ] ]

In the dbmmanage command line, command can be one of the following:
```

+   * add: This command adds an entry for username to filename using the encrypted password encpasswd or the group(s) in the list of group1 [,group2].
+   * adduser: This command prompts for a password and adds an entry for username to filename.
+   * check: This command prompts for a password and then checks if username is in filename and if its password matches the one specified.
+   * delete: This command deletes the username entry from filename.
+   * import: This command reads the username:password entries (one per line) from the standard Linux input and appends them to filename. The password must already be encrypted.
+   * update: This command is equivalent to the adduser command, except that it ensures that username already exists in filename.
+   * view: This command displays the complete contents of the DBM database file.

For example, to create the DBM user database file /etc/httpd/conf/user-list-DBM and add a new user named alice, enter the following command:

```
[ramon]$ sudo dbmmanage /etc/httpd/conf/user-list-DBM adduser alice
New password:
Re-type new password:
User alice added with password encrypted to vqQ/X7Z7hYLXQ using crypt

To view your newly created entry, enter the following command:
[ramon]$ sudo dbmmanage /etc/httpd/conf/user-list-DBM view
alice:vqQ/X7Z7hYLXQ

To delete the database entry for alice, enter the following command:
[ramon]$ sudo dbmmanage /etc/httpd/conf/user-list-DBM delete alice
alice deleted
```