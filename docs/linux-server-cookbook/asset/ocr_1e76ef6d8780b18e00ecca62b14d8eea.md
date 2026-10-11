```
agonzalez@ubuntu:~$ ls -l example.txt
-rw-rw-r-- 1 agonzalez agonzalez 37 Jul  3 19:27 example.txt
agonzalez@ubuntu:~$ groups
agonzalez adm cdrom sudo dip plugdev lxd
agonzalez@ubuntu:~$ chown :root example.txt
chown: changing group of 'example.txt': Operation not permitted
agonzalez@ubuntu:~$ chown -v :sudo example.txt
changed ownership of 'example.txt' from agonzalez:agonzalez to :sudo
```

![](bbox=[0.34, 0.235, 0.7, 0.255])

+   - Change recursively the user and group owner for a directory as administrator.

```
root@ubuntu:/tmp# chown -R -v agonzalez:agonzalez snap/
changed ownership of 'snap/lxd/22911' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd/22923' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd/common' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd/current' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd' from root:root to agonzalez:agonzalez
changed ownership of 'snap/' from root:root to agonzalez:agonzalez
```

![](bbox=[0.35, 0.44, 0.7, 0.455])

The command **chgrp** is used to change only the group owner for files and directories. The syntax is **chgrp [options] group file(s)/dir(s)**. Options are the same as for **chown** command.

# ## Command chmod

This command is used to change the permission for files and directories. It allows us to specify the permissions using the symbolic or the octal representation. As described previously about permissions, the symbolic representation has the following syntax: **u=permission,g=permission,o=permission**, and the octal representation can contain three digits or four digits in case there is a need to specify special permission.

The command *chmod* can be used to replace current permissions using the character equal ( =) or manipulate current permission by adding more rights using the character (+) or removing permissions using the character minus (-). The command *chmod* allows to add permission using the character plus (+) or delete permissions (-) instead of the symbol equal (=). As well, *chmod* allows to specify only the permission to be modified and not all the components. And it is possible to use the letter “*a*” to set, add or remove permission for all the components.