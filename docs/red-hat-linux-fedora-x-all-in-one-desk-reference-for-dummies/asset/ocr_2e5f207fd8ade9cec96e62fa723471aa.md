# Understanding the /etc/passwd File 429

To modify any information in a user account, use the usermod command. For example, if I want my username, naba, to have root as the primary group,
type the following:

```
usermod -g root naba
```

To find out about the useradd, userdel, and usermod commands,
type man useradd, man userdel, or man usermod in a terminal window.

# ## Understanding the /etc/passwd File

The /etc/passwd file is a list of all user accounts. It is a text file and any user
read it — no special privileges needed. Each line in /etc/passwd has
seven fields, separated by colons (:).

Here is a typical entry from the /etc/passwd file:

```
naba:500:10:Naba Barkakati:/home/naba:/bin/bash
```

Figure 2-4 explains the meaning of the seven fields in this entry.

Figure 2-4:
This typical
/etc/
passwd
entry
illustrates
the meaning
of the
varous
fields.

![](bbox=[0.235, 0.592, 0.845, 0.802])

As the example shows, the format of each line in /etc/passwd looks like this:

```
username:password:UID:GID:GECOS:homedir:shell
```