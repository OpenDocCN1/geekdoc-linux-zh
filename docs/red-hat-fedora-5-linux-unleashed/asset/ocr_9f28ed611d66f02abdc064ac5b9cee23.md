# Control Via Restricted Shells

Using restricted shells is actually the opposite of granting additional privileges to users. These might be situations in which you want to restrict a user to a very specific subset of privileges permitted to other users. If you have a desire to severely restrict what a user can do (for reasons of security, distribution of a turnkey system, or custom system installation), you can provide him with a restricted shell. To run a restricted bash shell, you would use the -r option. It is easy to try yourself, just enter the following at your prompt:

```
S bash -r
```

Then try to do something that you could do before as a regular user, such as listing the files in your home directory:

```
S ls -a
```

You then see:

```
bash: ls: No such file or directory
```

The cd command, redirection, using ! in command names, and several other commands and options are also disabled in the restricted shell. (The man page for bash details specific restrictions; the appropriate information is at the very end of the very long man page.) Do not rely on a restricted shell as your only means of controlling user activity; although using restricted shells applies some tight restrictions, a very determined user might find a way to contourd the restrictions. Always use appropriate permission and password controls as well.

# The User Login Process

It is useful to know what happens during the process when a user attempts to log in— if for nothing else than troubleshooting for that one user in the accounting department who cannot get logged on to run the payroll program and get the payroll checks printed on time. Understanding this process also involves understanding the purpose of the default user installation files that are found in /etc/skel. This section helps illuminate the login process for you.

The login process is used for entering, or "signing on" to a system and is summarized in steps as follows:

+   1. Login prompts for a username.

+   2. If the /etc/nologin file exists and the user is not root, a warning message is issued and the login process is halted. The /etc/nologin file is typically used when the system will be shut down shortly and new logins should be restricted.

+   3. The /etc/usertty file is examined to see whether any restrictions are specified for the user. As a security measure, root logons can be restricted to specific terminals and regular users can have the same restrictions placed on them as necessary.