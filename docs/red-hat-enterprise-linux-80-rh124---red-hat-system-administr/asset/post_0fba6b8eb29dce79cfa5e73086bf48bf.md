
# CHAPTER 7 | Managing Local Users and Groups

```
[user02@host ~]$ sudo tail /var/log/secure
[sudo] password for user02:
user02 is not in the sudoers file. This incident will be reported.
[user02@host ~]$
```

One additional benefit of using sudo is that all commands executed are logged by default to /var/log/secure.

```
[user01@host ~]$ sudo tail /var/log/secure
...output omitted.
Feb 6 28:45:46 host sudo[2577]: user01 : TTY=pts0 ; PWD=/home/user01 ; USER=root COMMAND=/sbin/sudo -L user02
...output omitted.
```

In Red Hat Linux 7 and Red Enterprise Linux 8, all members of the wheel group can use sudo to run commands as any user, including root. The user is prompted for their password. This is a change from Red Hat Linux 6 and earlier, where users who were members of the wheel group did not get this administrative access by default.

> WARNING
RHEL 6 does not grant the wheel group any privileges by default. Sites that have been using this group for a non-standard purpose might be surprised when RHEL 7 and RHEL 8 automatically grant all members of wheel full sudo privileges. This could lead to unauthorized users getting administrative access to RHEL 7 and RHEL 8 systems.

Historically, Unix-like systems use membership in the wheel group to grant or control superuser access.

# Getting an Interactive Root Shell with Sudo

If there is a non-administrative user account on the system that can use sudo to run the command, you can run sudo -s from that to get an interactive root shell. This works because sudo will run su as root, and root does not need to enter a password to use sudo.

Another way to access the root account with sudo is to use the sudo -i command. This will switch to the root account and run user's default shell (usually bash) and associated shell login scripts. If you just want to run the shell, you can use the sudo -s command.

For example, an administrator might get an interactive shell as root on an AWS EC2 instance by using SSH public-key authentication to log in as the normal user ec2-user, and then by running sudo -i to get the root user's shell.

```
[ec2-user@host ~]$ sudo -i
[password] for ec2-user:
[root@host ~]#
```

The sudo -s command and sudo -i do not behave exactly the same. This will be discussed briefly at the end of the section.

# Configuring Sudo

The main configuration file for sudo is /etc/sudoers. To avoid problems if multiple administrators try to edit it at the same time, it should only be edited with the special visudo command.

For example, the following line from the /etc/sudoers enables sudo access for members of group wheel.

```
%wheel=(ALL) ALL
```

In this line, %wheel is the user or group who rules the access. A % specifies that any one who might have this file, wheel can run any command. The ALL=(ALL) specifies that wheel can run commands as any user on the system.

By default, /etc/sudoers also includes the contents of files in the /etc/sudoers.d directory as part of the configuration file. This allows an administrator to add sudo access for a user simply by putting an appropriate file in that directory.

> NOTE
Using supplementary files under the /etc/sudoers.d directory is convenient and simple. You can enable or disable sudo access simply by copying a file into the directory or removing it from the directory.

In this case, you will create and remove files in the /etc/sudoers.d directory to configure sudo access for users and groups.

To enable full sudo access for the user01, you could create /etc/sudoers.d/user01 with the following content:

```
user01 ALL=(ALL) ALL
```

To enable full sudo access for the group group01, you could create /etc/sudoers.d/group01 with the following content:

```
%group01 ALL=(ALL) ALL
```

It is also possible to set sudo allow a user to run commands as another user without entering their password:

```
ansible ALL=(ALL) NASSWD:ALL
```

While there are obvious security risks to granting this level of access to a user or group, it is frequently used with cloud instances, virtual machines, and provisioning systems to help configure servers. The account must be carefully protected and might require SSH public-key authentication in order for a user to access the remote system securely. For example, the official for Red Hat Enterprise Linux ships with the root and ec2-user passwords locked. user can also run any command as root without a password because the last line of /etc/sudoers file is set as follows:

```
ec2-user ALL=(ALL) NOPASSWD:ALL
```

The requirement to enter a password for sudo can be re-enabled or changes may be made to tighten security.

> NOTE
In this course, you will frequently see sudo su instead of sudo -i. Both commands work, but there are some subtle differences between them. The sudo su command sets up the root user exactly like a normal login because it ignores the settings. The sudo -i command actually sets up the root user's environment differently than a normal login. This affects where the shell will look. You can make sudo -i behave like su by editing /etc/sudoers with visudo. Find the line

```
Defaults secure_path = /sbin:/bin:/bin
```

and replace it with the following lines:

| Defaults:secure_path = /usr/local/bin:/bin |
| Defaults:root secure_path = /usr/local/bin:/sbin |

For most purposes, this is not a major difference. However, for consistency of PATH settings on systems, the authors mostly use sudo in examples.

> REFERENCES
su(1), sudo(8), visudo(8) and sudoers(5) man pages
info libc (GNU Library Reference Manual) - Section 3.2: The Process (Note that the glibc-devel package must be installed for this node to be available.)

# GUIDED EXERCISE: GAINING SUPERUSER ACCESS

In this exercise, you will practice switching to the root account and running commands as root.

# OUTCOMES

You should be able to:
- Use sudo to switch to root and access the interactive shell as root without knowing the password of the superuser.
- Explain how su and sudo -i affect the shell environment through running or not running login scripts.
- Use sudo to run other commands as root.

# BEFORE YOU BEGIN

Log in to workstation using student as the password. On workstation, run lab users-sudo start to start the exercise. This script creates the necessary user accounts and sets up the environment correctly.

```
[student@workstation ~]$ lab users-sudo start
```

- 1. From workstation, open an SSH session to servera as student.
```
[student@workstation ~]$ ssh student@servera
...output omitted...
[student@servera ~]$
```

- 2. Explore the shell environment of student. View the current user and group information and display the current working directory. Also view the environment variables that specify the user's home directory and the locations of the user's executables.

- 2.1. Run id to view the current user and group information.
```
[student@servera ~]$ id
uid=1000(student) gid=1000(student) groups=1000(wheel)
context=unconfined_u:unconfined_r:unconfined_t:s0-sc0:0.c023
```

- 2.2. Run pwd to display the current working directory.
```
[student@servera ~]$ pwd
/home/student
```

- 2.3. Print the values of the HOME and PATH variables to determine the home directory and user executables, respectively.
```
[student@server ~]$ echo HOME
/home/student
[student@server ~]$ echo PATH
/home/student/.local/bin:/home/student/bin:/usr/local/bin:/usr/local:/usr/bin:/usr/sbin
```

- 3. Switch to root in a non-login shell and explore the new shell environment.

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
context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c123
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
[root@server #]$ echo PATH
/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/bin
```

If you have some experience with Linux and the su without the (-) option to become root would cause you to keep the PATH of student. That did not happen. As you will see in the next step, this is not the usual PATH for root either. What happened? The difference is that you did not use su, you ran su as root because you did not pass the password of supper. The sudo command initially overrides the PATH variable from the initial environment for security reasons. Any command that runs after the initial override can still update the PATH, that runs in the following steps.

3.5. Exit the root user's shell to return to the student user's shell.

```
[root@server #]$ exit
exit
```
