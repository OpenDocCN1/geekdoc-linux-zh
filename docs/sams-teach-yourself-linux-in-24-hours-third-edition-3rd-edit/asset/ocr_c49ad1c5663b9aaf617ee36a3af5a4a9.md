shows an example. In this example, the owner has full access to the file (read, write, and execute). The group, owner, and other users have read and execute permissions on the file.

FIGURE 12.3
The owner has read, write, and execute permissions on the file.

![](bbox=[0.27, 0.24, 0.88, 0.55])

# Changing File Ownership

To change the ownership of a file (that is, the user owner and the group owner), use the chown and chgrp commands. Let's look at two files that user rusty has created and placed in the sales group directory:

```
-rw-r--r-- 1 rusty rusty 747293 Jul 4 04:04 packages
-rw-r--r-- 1 rusty rusty 155 Jul 7 01:01 tealist
```

For both files, the group ownership needs to be changed to the sales group. To do this, rusty would cd to the sales directory and use the chgrp command as follows:

```
[rusty@localhost sales]$ chgrp sales packages
[rusty@localhost sales]$ chgrp sales tealist
```

If rusty wants to transfer the tealist file into the hands of user mona, rusty would change the owner with the following command:

```
[rusty@localhost sales]$ chown mona tealist
```

The listing would then appear as follows:

```
-rw-r--r-- 1 rusty sales 747293 Jul 4 04:04 packages
-rw-r--r-- 1 mona sales 155 Jul 7 01:01 tealist
```