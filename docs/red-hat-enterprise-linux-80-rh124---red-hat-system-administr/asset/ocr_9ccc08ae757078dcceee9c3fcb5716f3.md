# 2.3. Print the values of the HOME and PATH variables to determine the home directory and user executables, respectively.

```
[student@server ~]$ echo HOME
/home/student
[student@server ~]$ echo SPATH
/home/student/.local/bin:/home/student/bin:/usr/local/bin:/usr/local:/usr/bin:/usr/sbin
```

+   3. Switch to root in a non-login shell and explore the new shell environment.

3.1. Run su at the shell prompt to become the root user.

```
[student@server ~]$ sudo su
[sudo] password for student: student
[root@server #]
```

3.2. Run id to view the current user and group information.

```
[root@server #]$ id
uid=0(root) gid=0(root) groups=0(root)
context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

3.3. Run pwd to display the working directory.

```
[root@server #]$ pwd
/home/student
```

3.4. Print the values of the HOME and PATH variables to determine the home directory and user executables, respectively.

```
[root@server #]$ echo HOME
/root
[root@server #]$ echo SPATH
/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/bin
```

If you have some experience with Linux and the su without the (-) option to become root would cause you to keep the PATH of student student. That did not happen. As you will see in the next step, this is not the usual PATH for root either.
What happened? The difference is that you did not use su, you ran su as root because you did not pass the password of the supper. The sudo command initially overrides the PATH variable from the initial environment for security reasons. Any command that runs after the initial override can still update the PATH, that runs in the following steps.

3.5. Exit the root user's shell to return to the student user's shell.

```
[root@server #]$ exit
exit
```