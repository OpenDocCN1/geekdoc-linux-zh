# CHAPTER 17 | Comprehensive review

# # SOLUTION

# # MANAGING USERS AND GROUPS,
PERMISSIONS AND PROCESSES

In this review, you will manage user and group accounts, set permissions on files and
directories, and manage processes.

# ## OUTCOMES

You should be able to:

+   - Manage users and groups.
- Set permissions on files and directories.
- Remove processes that are consuming much CPU.

# ## BEFORE YOU BEGIN

Log in to workstation student using student as the password.

On workstation, run lab rhsa-rh124-review2 start to start the comprehensive
review this script consumes the maximum CPU resources and creates
necessary files to set the environment correctly.

```
$student@workstation ~]$ lab rhsa-rh124-review2 start
```

# ## INSTRUCTIONS

Accomplish the following tasks on server2 to complete the exercise.

+   - Terminate the process that is currently using the most CPU time.
- Create a new group called database that has the GID database 50000.
- Create a new user duser1 that uses the group database as one of its secondary
groups. The initial password of duser1 should be redhat. Configure the user
duser1 to force a password change after 10 days since the date of the password change. duser1 should be able to
change its password after 10 days since the date of the password change. The password of
duser1 should expire in 30 days since the date of the password change.
- Configure the user duser1 to use sudo to run any command as the superuser.
- Configure the user duser1 to have a default account.
- The permissions on /home/student/grading/review2 would allow the group
members of database and the user student to access the directory and create contents
it it. All other users should read and execute permissions on the directory. Also,
ensure that users are only allowed to delete files they from /home/student/
grading/review2 and not files belonging to others.

1. Terminate the process that is currently using the most CPU time.