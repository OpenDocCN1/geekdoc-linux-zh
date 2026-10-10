+   10. If the user should belong to more than one group, enter groups in addition to
+   the one you entered in Step 7 in the Member Groups field, separated by commas.
+   This field may be left blank if the user should belong to only one group.
+   11. You may change the user’s home directory by editing the Home Directory
+   field, but in most cases the default based on the username should work fine.
+   12. Enter a default shell for the user. The system checks this against a list of
+   acceptable shells (stored in /etc/shells). If you enter an invalid shell,
+   sysinstall complains when you select OK.
+   13. Position your text cursor on OK and press ENTER. FreeBSD now creates a new
+   account using the information you’ve provided and returns you to the User and
+   Group Management menu (Step 4). You can then repeat Steps 4–13 if you want
+   to add more users, or select Cancel twice and then Exit Install to get out of
+   sysinstall.

This procedure for adding users works well in most cases. It presents prompts for
what should go in each field and can quickly add a few users. Like many FreeBSD
administration tasks, though, sysinstall presents a menu-based face for other tools.

# ## Using adduser

Sometimes sysinstall isn’t adequate. For instance, if you need to add many users,
you may prefer to write a script to do the job, and sysinstall doesn’t interact well
with scripts. You might also prefer not to wade through sysinstall’s menus. In such
cases, a simpler but more powerful tool exists: adduser. This program prompts you
for information in a fairly rigid order using standard input and output, so you can
call it from a script using redirection, as described in Chapter 5, if you want to create
accounts in a semiautomated way.

The first time you run adduser, the program tries to access its configuration file,
/etc/adduser.conf, but this file doesn’t exist on a standard installation. The
program therefore runs through most of its options, as described shortly, to obtain
default values. You can press ENTER to accept the defaults for most of these. If you
decide to change them later, you can edit adduser.conf or delete the file and run
adduser again to generate new defaults.

After you’ve generated adduser.conf, or when you run the program, it begins
prompting for information. The first information is related to the username and user
identity:

```
```
# adduser
Use option `--verbose' if you want to see more warnings and
questions or try to repair bugs.

Enter username [a-z0-9_-]: marie
Enter full name []: Marie Curie
```
```