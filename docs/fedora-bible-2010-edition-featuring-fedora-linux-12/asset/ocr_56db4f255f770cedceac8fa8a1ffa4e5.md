mary would have been created and assigned to the new user. Likewise, excluding `-s /bin/tcsh` causes `/bin/bash` to be assigned as the default shell.

The `/etc/group` file holds information about the different groups on your Fedora system and the users who belong to them. Groups are useful for allowing multiple people to share access to the same files while denying access to others. If you peek at the `/etc/group` file, you should find something similar to this:

```
```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8:
kmem:x:9:
whee1:x:10:root,joe,mary

no body:x:99:
users:x:100:
chris:x:500
share:x:501
sales:x:601:bob,jane,joe,mary
```
```

Each line in the group file contains the name of a group, the group ID number associated with it, and a list of users in that group. By default, each user is added to his or her own group, beginning with GID 500. Note that *mary* was added to the *whee1* and *sales* groups instead of having her own group.

It is actually rather significant that *mary* was added to the *whee1* group. By doing this, you can easily grant her the ability to use the `sudo` command to run commands as the root user, provided that the *whee1* line is uncommented from the `/etc/sudoers` file (as described in Chapter 9), which it is not by default. (The *whee1* group is used by convention as a sudoers group. You can define other such groups as well.)

In this example, we used the `-g` option to assign *mary* to the *users* group. If you leave off the `-g` parameter, the default behavior is for `useradd` to create a new group with the same name and ID number as the user; this group is assigned as the new user’s primary group. For example, look at the following `useradd` command:

```
```bash
# useradd -m -G wheel,sales -s /bin/tcsh -c "Mary Smith" mary
```
```

It would result in an `/etc/passwd` entry like this:

```
```plain
mary:x:502:502:Mary Smith:/home/mary:/bin/tcsh
```
```