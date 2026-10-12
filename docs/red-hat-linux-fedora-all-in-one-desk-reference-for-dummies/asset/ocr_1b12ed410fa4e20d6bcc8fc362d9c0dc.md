This chgrp command changes the group ownership of composer.txt to class. After I tried this, I typed ls -l again to verify the ownership, and here's what I got:

```
-rw-rw-r-- 1 naba class 40909 07-14 20:37 composer.txt
```

You can use the chown command to change the user owner. The command has the following format:

```
chown username filename
```

For example, to change the user ownership of a file named sample.jpg to naba, type:

```
chown naba sample.jpg
```

In fact, chown can change both the user and group owner at the same time. For example, to change the user owner to naba and the group owner to class, type:

```
chown naba.class composer.txt
```

In other words, you simply append the group name to the username with a period in between, and use that as the name of the owner.