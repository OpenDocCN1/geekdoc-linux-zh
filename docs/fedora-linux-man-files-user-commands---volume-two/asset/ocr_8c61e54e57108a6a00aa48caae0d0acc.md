# TYPICAL USE OF GIT CREDENTIAL

An application using git-credential will typically use git credential following these steps:

+   1. Generate a credential description based on the context.

For example, if we want a password for we might generate the following credential description (don’t forget the blank line at the end; it tells git credential that the application finished feeding all the information it has):

```
protocol=https host=example.com path=foo.git
```

+   2. Ask git-credential to give us a username and password for this description. This is done by running git credential fill, feeding the description from step (1) to its standard input. The complete credential description (including the credential per se, i.e. the login and password) will be produced on standard output, like:

```
protocol=https host=example.com username=bob password=secr3t
```

In most cases, this means the attributes given in the input will be repeated in the output, but Git may also modify the credential description, for example by removing the path attribute when the protocol is HTTP(s) and credential.useHttpPath is false.

If the git credential knew about the password, this step may not have involved the user actually typing this password (the user may have typed a password to unlock the keychain instead, or no user interaction was done if the keychain was already unlocked) before it returned password=secr3t.

+   3. Use the credential (e.g., access the URL with the username and password from step (2)), and see if it’s accepted.

+   4. Report on the success or failure of the password. If the credential allowed the operation to complete successfully, then it can be marked with an “approve” action to tell git credential to reuse it in its next invocation. If the credential was rejected during the operation, use the “reject” action so that git credential will ask for a new password in its next invocation. In either case, git credential should be fed with the credential description obtained from step (2) (which also contain the ones provided in step (1)).