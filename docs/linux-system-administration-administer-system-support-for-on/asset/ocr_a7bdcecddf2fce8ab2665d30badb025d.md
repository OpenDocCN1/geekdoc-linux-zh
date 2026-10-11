So, your /etc/group file with the infosys and market groups may look like this:

```
root::0:root
bin::1:root,bin,daemon
daemon::2:root,bin,daemon
sys::3:root,bin,adm
adm::4:root,adm,daemon
tty:::5:
disk::6:root,adm
lp::7:lp
mem::8:
kmem::9:
wheel::10:root
floppy::11:root
mail::12:mail
news::13:news
uucp::14:uucp
man::15:man
infosys::300:judy bob russ dbadmin
market::200:wendy jane bob
users::100:mike dave kim judy bob russ dbadmin
nogroup::-2:
```

In this case, the information-systems folks can access anything in the user groups. Because bob is the marketing-information systems specialist, he has access to both information systems and marketing. The users mike, dave, and kim just belong to the user group.

If root needs to change someone's group access, root uses the chgrp command. Also, if root wants to change all the files in a directory, he or she just needs to use the -R option to make it recursive.

```
# chgrp infosys /usr/local/maintenance
```

You can add a group with the groupadd command.

```
# groupadd test
```

This adds an entry to the /etc/group file with a group with the next group identification number (in this case, 101). Notice there is no password.

```
root::0:root
bin::1:root,bin,daemon
daemon::2:root,bin,daemon
sys::3:root,bin,adm
adm::4:root,daemon
```