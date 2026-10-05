7. Change the password policy for the consultant2 account to require a new password every 15 days.

```
[student@server ~]$ sudo chage -M 15 consultant2
...output omitted...
```

8. Additionally, force the consultant1, consultant2, and consultant3 users to change their passwords on the first login.

+   8.1. Set the last day of the password change to 0 so that the users are forced to change the password when they log in to system for the first time.

```
[student@server ~]$ sudo chage -d 0 consultant1
...output omitted...
[student@server ~]$ sudo chage -d 0 consultant2
...output omitted...
[student@server ~]$ sudo chage -d 0 consultant3
...output omitted...
```

+   8.2. Log off from server.

```
[student@server ~]$ exit
logout
Connection to server closed.
```

# Evaluation

On workstation, run the lab users-review grade command to confirm success of this exercise.

```
[student@workstation ~]$ lab users-review grade
```

# Finish

On workstation, run the lab users-review finish to complete this lab. This script deletes the user accounts and files created throughout the lab to ensure that the environment is clean.

```
[student@workstation ~]$ lab users-review finish
```

This concludes the lab.