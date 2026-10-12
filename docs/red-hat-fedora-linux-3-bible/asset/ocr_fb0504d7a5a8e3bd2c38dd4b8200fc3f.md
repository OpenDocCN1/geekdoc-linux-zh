# Chapter 11: Setting Up and Supporting Users

access to the same files while denying access to others. If you peek at the `/etc/group` file, you should find something similar to this:

```
```text
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8:
kmem:x:9:
wheel:x:10:root,joe,mary
...
...

nobody:x:99:
users:x:100:
chris:x:500
sherex:x:501
sales:x:601:bob,jane,joe,mary
```
```

Each line in the group file contains the name of a group, the group ID number associated with it, and a list of users in that group. By default, each user is added to his or her own group, beginning with GID 500. Note that mary was added to the wheel and sales groups instead of having her own group.

It is actually rather significant that mary was added to the wheel group. By doing this, you grant her the ability to use the sudo command to run commands as the root user (provided that sudo was configured as described in Chapter 10).

In this example, we used the `-g` option to assign mary to the users group. If you leave off the `-g` parameter, the default behavior is for useradd to create a new group with the same name and ID number as the user, which is assigned as the new user’s primary group. For example, look at the following useradd command:

```
`# useradd -m -G wheel,sales -s /bin/tcsh -c "Mary Smith" mary`
```

It would result in a /etc/passwd line like this:

```
`mary:x:502:502:Mary Smith:/home/mary:/bin/tcsh`
```

It would also result in a new group line like this:

```
`mary:x:502:`
```