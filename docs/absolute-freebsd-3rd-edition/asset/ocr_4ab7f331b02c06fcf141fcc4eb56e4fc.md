Creating new users on some Unix systems requires you to manually edit /etc/passwd, rebuild the password database, edit /etc/group, create a home directory, set permissions on that home directory, install dotfiles, and so on. This makes handling your local customizations routine—if you set everything by hand, you can manage your local account setup easily. The adduser(8) program provides a set of sensible defaults. For sites with different requirements, /etc/adduser.conf lets you set those requirements as defaults while retaining the high degree of automation. To create adduser.conf file, run adduser -c and answer the questions.

+   1. Uid (Leave empty for default):  
+   2. Login group []:  
+   3. Enter additional groups []: staff  
+   4. Login class [default]: staff  
+   5. Shell (sh csh tcsh nologin) [sh]: tcsh  
+   6. Home directory [/home/]: /nfs/u1/home  
+   7. Use password-based authentication? [yes]:  
+   8. Use an empty password? (yes/no) [no]:  
+   9. Use a random password? (yes/no) [no]: yes  
+   10. Lock out the account after creation? [no]: no

You might want to start numbering UIDs somewhere other than 1,000. If you want higher initial UIDs, enter it in the uid space 1. Don't start below 1,000.

The login group 2 is the default user group. An empty login group means the user account defaults to having its own unique user group (the FreeBSD default).

You can specify any additional user groups 3 that new accounts belong to by default, as well as the login class 4. I set both of these to staff so that all new users get added to that group and assigned that class.

Choose a default shell 5 for your users.

Your home directory location 6 might vary from the standalone FreeBSD standard. In this example, I've specified a typical style of NFS-mounted home directories used when many users have accounts on many machines.