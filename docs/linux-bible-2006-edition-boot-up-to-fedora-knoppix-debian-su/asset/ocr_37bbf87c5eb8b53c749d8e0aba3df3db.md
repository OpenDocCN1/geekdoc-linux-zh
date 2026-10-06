# Part II ✦ Running the Show

Each line in the /etc/passwd file represents a single user account record. Each field is separated from the next by a colon:) character. The field's position in the sequence determines what it is. As you can see, the login name is first. Again, the password field contains an x because we use a shadow password file to store encrypted password data. The user ID is selected by 502. The group ID is 100, which corresponds to the users group in /etc/group file. The comment field was correctly set to Mary Smith, the home directory was automatically assigned as /home/mary, and the command shell was assigned as /bin/tcsh, exactly as specified with the useradd options.

By leaving out many of the options (as I in the first useradd example), defaults are assigned in most cases. For example, by not using -u -G wheel,sales, in Red Linux a group named mary would have been created and assigned to the new user. Other Linux systems assign users -s /bin/tcsh causes /bin/bash to be assigned to the group by default. Likewise,

The /etc/group file holds information about the different groups on your Linux systems and the users they belong to. Groups are useful for enabling multiple users to share the same files while denying access to others. Peek at the /etc/group file, and you found something like this:

```
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8
kmem:x:9:
wheel:x:10:root,joe.mary

nbody:x:99
users:x:100
chris:x:500
shee:x:501
sales:x:601:bob.jane,jane,mary
```

Each line in the group file contains the name of a group, the group ID number associated with it, and a list of users in that group. By default, each user is added to or her own group, beginning with GID 500. Note that mary was added to the wheel and sales groups instead of her own group.

It is actually rather significant that mary was added to the wheel. By doing this, you grant her the capability to use the sudo command to run commands as the root user (provided that sudo is configured as described later in this chapter).