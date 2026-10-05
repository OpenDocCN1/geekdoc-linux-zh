# GUIDED EXERCISE

# MANAGING DEFAULT PERMISSIONS AND FILE ACCESS

In this exercise, you will control the permissions on new files created in a directory using umask settings and the setgid permission.

# OUTCOMES

You should be able to:

+   * Create a shared directory where new files are automatically owned by the operators group.
* Experiment with various umask settings.
* Adjust default permissions for specific users.
* Confirm your adjustment is correct.

# BEFORE YOU BEGIN

Log in to workstation as student using student as the password.

On workstation, run the lab perms-default start command. The command runs a script that determines if servera is reachable on the network. The script also creates the operators group and the operator1 user on servera.

```
[student@workstation ~]$ lab perms-default start
```

+   1. Use the ssh command to log in to servera as the student user.

```
[student@workstation ~]$ ssh student@servera
[student@servera ~]$
```

+   2. Use the su command to switch to the operator1 user using redhat as the password.

```
[student@servera ~]$ su - operator1
Password: redhat
[operator1@servera ~]$
```

+   3. Use the umask command to list the operator1 user's default umask value.

```
[operator1@servera ~]$ umask
0002
```