Although you can edit the * /etc/passwd * file directly and then run * passwd * to add a user to the system, it’s not considered elegant by any means. One of the reasons to use the commands outlined here is that you might not be the only person accessing these files at a given time.

# ## Adding Users with useradd

The */usr/sbin/useradd* command is used to automate user additions, whereas the */usr/sbin/adduser* script is a friendlier front-end (so the author claims) that simplifies the process. On some distributions, the *adduser* file can be a link to the *useradd* program.

![](bbox=[0.08, 0.34, 0.18, 0.41])

> The exam focuses on the *useradd* command and doesn’t include the *adduser* script.

Rather than show the syntax for the command, let’s add a user to show how it works.

To add a user with the defaults, you would type

```
```bash
useradd snuffy
```
```

On a Red Hat machine, this creates the user *snuffy* with the next available UID, the GID set to a newly created group with that username as the group name, the same value as the UID for the GID, and a copy of the */etc/skel* directory properly set up as the directory */home/snuffy*.

On a Debian machine, this same command creates the user *snuffy* with the next available UID, the GID set to the users (100) group, and no created home directory.

To set up the same user on the Debian system, you’d have to specify the *-m* option to create the user’s home directory. A more complex example is to create a user named *ulogin* with a particular home directory, a specific UID, a specialized *skel* or template directory, the user’s group set as the primary group, and the user’s full given name as the comment. To do this you would type

```
```bash
useradd -m -d /home2/ulogin -u 2112 -k /etc/skel_mktg -g 100 -c "Ursula K. Login" ulogin
```
```

This creates the user with all the specialized information. On a Red Hat machine the */bin/bash* shell is auto-supplied, whereas on a Debian machine