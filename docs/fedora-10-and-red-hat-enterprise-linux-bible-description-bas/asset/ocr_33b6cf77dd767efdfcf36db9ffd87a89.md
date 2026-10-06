# Chapter 11: Setting Up and Supporting Users 467

+   - Creates a home directory based on the user's name and places it in the /home directory.
- Copies any files located within the /etc/skel to the new home directory. This usually includes only two of the available useradd options.

```
# useradd -m -g users,sales -s /bin/tch -c "Mary Smith"
```

In this case, the useradd command is told to create a home directory for the user (-m), makes users the primary group (-g), adds her to the groups wheel and sales (-G), and sets tch as primary shell (-s). Note that the wheel and sales groups must already exist for this to work. This results in a line similar to the following being added to the /etc/passwd

```
mary:x502:100:Mary Smith:/home/mary:/bin/tch
```

In the /etc/passwd file, each line represents a single user account record. Each field is separated from another by a colon (:). The field's position in the sequence determines what it is. As you can see, the login name is first. The password field contains an x because Fedora is using a shadow password file to store encrypted password data. The User ID selected by the user command was 502. The primary group ID is 100, which corresponds to the users group in the /etc/group file. The comment field was correctly set to Mary Smith, the home directory was automatically assigned as /home/mary, and the command shell was assigned as /bin/tch exactly as specified with the useradd options.

By leaving out some of the options (as I did in the first user example), defaults are assigned in most cases. For example, by not using -g users or -G wheel,sales, a group named mary would have been created and assigned to the new user. Likewise, excluding -s /bin/tch /bin/bash would be assigned as the default shell.

The /etc/group file holds information about the different groups on your Fedora or RHEL system and the users who belong to them. Groups are useful for allowing multiple people to share access to the same files without denying access to others. If you peek at /etc/group, you find something similar to:

```
bin:x:2:root,daemon
daaemon:x:2:root,daemon
sys:x:3:root,adm
adm:x:4:root,adm,daemon
tty:x:5
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8
kmem:x:9
wheel:x:10:root,joe,mary
```