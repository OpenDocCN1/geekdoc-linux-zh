suspected breach in security. For example, you might want to monitor the login status of a particular user.

+   1. Become superuser.
2. Display a user's login status by using the logins command:

```
# logins -x -l username
```

For example, to monitor login status for the user calkins, type

```
# logins -x -l calkins
```

The system displays the following information:

```
calkins 200 staff 10 Bill S. Calkins
/export/home/calkins
/bin/sh
PS 030195 10 7 -1
```

Table 4-8 describes the information output of the logins command.

Table 4-8 Output from the logins Command

| | |
|---|---|
| Calkins | The login name |
| 200 | The UID |
| staff | The primary group |
| 10 | The group ID |
| Bill S. Calkins | The comment field of the /etc/passwd file |
| /export/home/calkins | The user's home directory |
| /bin/sh | The user's default login shell |
| PS 030195 10 7 -1 | Specifies the password aging information: last date password was changed, number of days required between changes, number of days allowed before a change is required, and warning period |

You'll want to monitor user logins to ensure their passwords are secure. A potential security problem is to have users without passwords (in other words, users who use a carriage return for a password). Periodically check user logins by using the following method:

+   1. Become superuser.
2. Display users who have no passwords by using the logins command:

```
# logins -p
```

The system responds with a list of users who do not have passwords.