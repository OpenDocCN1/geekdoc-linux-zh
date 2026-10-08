![](bbox=[0.03, 0.07, 0.12, 0.18])

What happens if you craft a new shell script or any new file? What permission settings exist? You want to execute the shell script, so you will need execute permission for the file. You can use **umask** to define the defaults for all your new files and directories.

By default, most systems start with a permission of 777 for directories and 666 for files. This means that everyone has complete access to all directories you create and everyone has read and write access to all files you create. These defaults are modified with the value of **umask**.

You can view your **umask** in the following two ways:

```
martyp $ **umask**
002
martyp $ **umask -S**
u=rwx,g=rwx,o=r-x
martyp $
```

The first example displays the octal value of **umask**, which we'll cover shortly, and the second example shows the symbolic value of **umask**. The *-S* does not work on all UNIX variants.

The **umask** is used to *disable* access. You start with a **umask** and use the fields to disable some level of access. The **umask** command uses three octal fields. The fields are the sum of the access codes for user, group, and other, as shown in Figure 7-5.

![](bbox=[0.12, 0.68, 0.92, 0.88])