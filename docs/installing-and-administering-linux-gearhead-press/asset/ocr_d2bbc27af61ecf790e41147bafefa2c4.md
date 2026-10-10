```
$ chmod numeric filename<Enter>
```

With numeric (also called octal) notation, you specify absolute file or directory permissions. You do not need to know the existing values beforehand. This situation contrasts with symbolic notation, which requires you to know the existing permissions before adding, subtracting, or redefining new permissions with respect to the existing permissions.

A scenario might help to explain the numeric notation concept. As we go through it, please refer to Figure 6.1.

Let’s say that you have created a file called *newfile* and you want the owner and the group to be able to read and write to it, but you only want it to be readable by all other system users.

First, to enable the owner to read and write to the file, you add the *x* and *w* permissions to the three leftmost permission bits (in other words, the owner’s permission bits).

Each permission you set within the nine permission bits is represented by a binary value 1. Each lack of a permission is represented by a 0. For example, rw-r--r--  translates to 110100100 in binary.

Use Figure 6.1 to translate the binary notation to numeric (octal). In Figure 6.1, we see that the owner’s *r* and *w* permission bits would have values of 400 and 200, respectively. Second, to set the same permissions for the group, you add 40 (*r*) and 20 (*w*). Finally, to set the read permission for all other system users, you add 4 (*r*). The numeric result comes from simple addition: 400 + 200 + 40 + 20 + 4 = 664

So, to translate the permission mode from a symbolic (alphabetical) form to a numeric form, you add the numbers that correspond to the individual permissions required and then specify that number as an argument to the chmod command.

![](bbox=[0.14, 0.7, 0.88, 0.9])