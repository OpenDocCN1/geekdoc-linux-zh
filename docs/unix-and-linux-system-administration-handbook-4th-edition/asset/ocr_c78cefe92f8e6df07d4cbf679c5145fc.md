once, such as when creating class-specific accounts. newusers expects an input file of lines just like the /etc/passwd file, except that the password field contains the initial password in clear text. Oops... better protect that file.
newusers honors the password aging parameters set in the /etc/login.defs file, but it does not copy in the default startup files as useradd does. The only startup file it provides is .xauth.

At a university, what’s really needed is a batch adduser script that can use a list of students from enrollment or registration data to generate the input for newusers, with usernames formed according to local rules and guaranteed to be locally unique, with strong passwords randomly generated, and with UIDs and GIDs increasing for each user. You’re probably better off writing your own wrapper for useradd in Perl or Python than in trying to get newusers to do what you need.

# 7.7 REMOVING USERS

When a user leaves your organization, that user’s login account and files should be removed from the system. This procedure involves the removal of all references to the login name that were added by you or your useradd program. If you remove a user by hand, you may want to use the following checklist:

+   - Remove the user from any local user databases or phone lists.
+   - Remove the user from the aliases file or add a forwarding address.
+   - Remove the user’s crontab file and any pending at jobs or print jobs.
+   - Kill any of the user’s processes that are still running.
+   - Remove the user from the passwd, shadow,¹¹ group, and gshadow files.
+   - Remove the user’s home directory.
+   - Remove the user’s mail spool.
+   - Clean up entries on shared calendars, room reservation systems, etc.
+   - Delete or transfer ownership of any mailing lists run by the deleted user.

Before you remove someone’s home directory, be sure to relocate any files that are needed by other users. You usually can’t be sure which files those might be, so it’s always a good idea to make an extra backup of the user’s home directory and mail spool before deleting them.

Once you have removed a user, you may want to verify that the user’s old UID no longer owns files on the system. To find the paths of orphaned files, you can use the find command with the -nouser argument. Because find has a way of “escaping” onto network servers if you’re not careful, it’s usually best to check filesystems individually with -xdev:

```
$ sudo find filesystem -xdev -nouser
```

Killing the deleted user’s running processes can be tricky in a distributed environment. Shared calendars and room reservation systems may have ongoing items