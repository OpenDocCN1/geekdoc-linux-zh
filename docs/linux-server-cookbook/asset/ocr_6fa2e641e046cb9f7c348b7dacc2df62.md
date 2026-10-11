The options for this command are the same as for command **chown** (refer to *table 5.11*). **Figures 5.15, 5.16**, and **5.17** show different examples using the command **chmod**:

+   - Specify permission for the user to read and write, the group only to read, and no permission: to others.

```
agonzalez@ubuntu:~$ chmod -v u=rw,g=r,o= example.txt
mode of 'example.txt' changed from 0664 (rw-rw-r--) to 0640 (rw-r----);
```

![](bbox=[0.32, 0.27, 0.72, 0.29])

+   - Remove read permission for group owner:

```
agonzalez@ubuntu:~$ chmod -v g-r example.txt
mode of 'example.txt' changed from 0640 (rw-r-----) to 0600 (rw-------
```

![](bbox=[0.32, 0.37, 0.72, 0.39])

+   - Specify the permission to user and group to read and write, and read for others using octal representation:

```
agonzalez@ubuntu:~$ chmod -v 644 example.txt
mode of 'example.txt' changed from 0600 (rw-------) to 0644 (rw-r--r--
```

![](bbox=[0.32, 0.5, 0.72, 0.52])

To understand the *execution* permission for files and directories, *figures 5.18* and *5.19* feature different examples:

+   - Add execution permission to a file to be able to be executed:

```
agonzalez@ubuntu:~$ stat -c "%a %A" appl
664 -rw-rw-r--
agonzalez@ubuntu:~$ ./appl
-bash: ./appl: Permission denied
agonzalez@ubuntu:~$ chmod -v u+x appl
mode of 'appl' changed from 0664 (rw-rw-r--) to 0764 (rwxrw-r--
agonzalez@ubuntu:~$ ./appl
Example application
```

![](bbox=[0.3, 0.77, 0.74, 0.79])

+   - Remove execution permission to a directory to not allow access to files inside: