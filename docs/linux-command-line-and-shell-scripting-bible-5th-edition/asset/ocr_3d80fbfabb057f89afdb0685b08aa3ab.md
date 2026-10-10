# Part IV: Working with Alternative Shells

The shell startup files also execute if you use the tcsh shell for a shell script:

```
$ cat test2
#!/bin/tcsh
# test run a script
echo "This is a test"
$ ./*test2
This is the /etc/csh/cshrc file
This is the /home/test/.tcshrc file
This is a test
$
```

Notice that before the output of the shell script appears, you see the echo statements from the tcsh shell startup files.

The startup files don't replace the login files but add to them. If you have both set, when you log in with a new login shell, you'll see that not only do the login shell files execute, but the startup shell files do as well:

```
$ ssh rich@localhost
Password:
Last login: Fri Sep 5 18:55:26 from localhost.localhost
This is the /etc/csh.cshrc file
This is the /etc/csh.login file
This is the /home/test/.tcshrc file
This is the .login file
$
```

Notice the order in which the shell executes the default files:

+   1.  The all-user startup file
+   2.  The all-user login file
+   3.  The private startup file
+   4.  The private login file

This order is important to remember if you're setting environment variables. If any of these files set the same environment variable values, the last value set wins.

# Logout files

Besides the login and startup files, the tcsh shell also has the ability to execute commands in files when you log out from an interactive or login shell session. These files can be in the following locations:

+   *   `/etc/csh.logout`
+   *   `$HOME/.logout`

As you probably figured out by now, every user on the system executes the commands in the /etc/csh.logout file at logout, while each individual user has a unique $HOME/.logout file. The tcsh shell will execute any commands in these files before logging out of the current shell.