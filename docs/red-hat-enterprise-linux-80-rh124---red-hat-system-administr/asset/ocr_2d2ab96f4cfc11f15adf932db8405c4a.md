7. Delete the operator3 user along any personal data of the user. Confirm that the user is successfully deleted.

7.1. Remove the operator3 user from the system.

```
[root@servera ~]# userdel -r operator3
```

7.2. Confirm that operator3 is successfully deleted.

```
[root@servera ~]# tail /etc/passwd
...output omitted...
operator1:x:1001:1001:Operator One:/home/operator1:/bin/bash
operator2:x:1002:1002:Operator Two:/home/operator2:/bin/bash
```

Notice that the preceding output does not display the user account information of operator3.

7.3. Exit the root user's shell to return to the student user's shell.

```
[root@servera ~]# exit
logout
[student@servera ~]$
```

7.4. Log off from servera.

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation ~]$
```

# Finish

On workstation, run lab users-manage finish to complete this exercise. This script ensures that the environment is clean.

```
[student@workstation ~]$ lab users-manage finish
```

This concludes the guided exercise.