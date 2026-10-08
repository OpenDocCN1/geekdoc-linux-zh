# login

The basic environment is initialized to:

```
HOME=your-login-directory
LOGNAME=your-login-name
PATH=/usr/bin
SHELL=last-field-of-passwd-entry
MAIL=/var/mail/your-login-name
TZ=timezone-specification
```

For Bourne and Korn shell, the shells execute /etc/profile and .profile if it exists. For C shells, the shell executes /etc/.login, /home/.cshrc, and .login. The default /etc/profile and /.login files check quotas (see quota(1M)), parse /etc/mock, and check for mail. None of the messages are printed if the file .hushlogin exists. The name of the command interpreter is set to -(dash) followed by the name of the interpreter's path name, for example, -sh

If the login-shell in the password file (see passwd(4)) is empty, then the default interpreter /usr/bin/sh is used. If this is *(asterisk), the named directory becomes the root directory. At that point, login is reexecuted at the new level, which must have its own root structure.

You can expand or modify the environment (except for PATH and SHELL) by supplying additional arguments to login, either at execution time or when login requests your login name. The arguments can take either the form xxxor=xxx;Arguments without an equal sign (=) are put into the environment as:

```
login=n
```

where n is a number that starts at 0 and incremented each new variable name is required. Variables containing an =(equal sign) are put into the environment without modification. If variables already appear in the environment, they replace the older values.

You cannot change the PATH and SHELL environment variables to prevent people who are logged in to restricted environments from spawning secondary shells that are not restricted. login allows simple-character quoting quotations. Typing a backslash(\ in front of a character quotes it and allows you to include characters as spaces and tabs.

Alternatively, you can pass the current environment using the -p option to login. This option indicates that login should pass currently defined environment variables, if possible, to the new environment. This option does not bypass any environment restrictions mentioned above. Environment variables specified on the login line take precedence if a variable is set by both methods.

To enable remote login, by edit the /etc/default/login file and insert a pound (#) before the CONSOLE=/dev/console.

# Security

users pam3PAM for authentication, account management, session management, and password management, listed by /etc/pam.conf, specifies the modules to be used for login. Below is a partial pam.conf file with entries for the login command and using the UNIX authentication, account management, session management, and password management module.

login required /usr/lib/security/pam_unix.so.1
login account required /usr/lib/security/pam_unix.so.1