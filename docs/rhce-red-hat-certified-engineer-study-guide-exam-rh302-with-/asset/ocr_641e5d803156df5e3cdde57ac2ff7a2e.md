# The chfn Command

The chfn command lets you change the full name associated with a user account. The form of the command is

```
chfn usernwhere user is the login name of the account to be modified. The command will prompt for the following information, known as the gecos information:
```

+   - Name
- Office
- Office phone
- Home phone

If you don't want to specify a value for a prompted field, simply press Enter. You can also use the chfn command in non-interactive mode. See its man page for this and other information.

# The chsh Command

The chsh command lets you change the command interpreter associated with a user account. The form of the command is

```
chsh -s shell userwhere shell1 specifies the path of the desired command interpreter and user specifies the login name of the user account to be modified. Only approved command interpreters listed in /etc/shell1 can be specified.
```

For more information on the chsh command, see its man page. You should now complete Exercise 10.4, which asks you to perform a variety of user administration tasks via the Linux command line.

| EXERCISE 10.4 |
| Administering User Accounts via the Command Line |

Some Linux users know only a single way to perform a given task. When a system is broken or misconfigured, some ways of performing a task may not be available to you; for example, if X is not working, Xbased tools will not be available. This exercise tests your ability to perform user administration tasks using the command line. At this point, you can look back to the relevant procedures, but you won't have the benefit of books or notes while taking the RHCE exam.