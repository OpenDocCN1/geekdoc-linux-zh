# 216 Hardening a Unix Server

But what does 022 mean?

To answer that question, let's first do a refresh of some basics. Unix systems have two default permissions: 666 for files (meaning everyone can read and write) and 777 for directories (meaning everyone has read, write, and execute permissions). However, to apply umask, we just need to subtract 022 from the default value, which will be something like this:

666 - 022 = 644

Based on Figure 7.9, 644 equals rw-r--r--.

And as you can see in the following figure, the default permissions for files is exactly that:

```
kali@kali:-$ ls -l
total 36
-rw-r--r-- 1 kali kali  0 Nov 29 12:16 bravo
```

Figure 7.14 – Default permissions on files

# Directory permissions:

777 - 022 = 755

Based on Figure 7.9, 755 equals rwxr-xr-x.

The following figure confirms that the default permissions for directories that are 755 equalwxr-xr-x:

```
kali@kali:-$ ls -ld bravito
drxr-xr-x 2 kali kali 4096 Nov 29 16:22 bravito
```

Figure 7.15 – Default permissions on directories

Now, to change the umask value is very simple. Just type the umask command and the new value.

For example, if you want to add a more restrictive value, you can use umask 0027, which will provide the following results:

# File permissions:

666 - 027 = 640

Based on Figure 7.9, 640 equals rw-r--r--.

The result of that is that by default, others won’t be able to access those files.