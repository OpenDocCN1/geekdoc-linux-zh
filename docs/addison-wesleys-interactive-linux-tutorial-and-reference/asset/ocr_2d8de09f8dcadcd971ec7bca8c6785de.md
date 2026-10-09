+   6. Remove read permission to *newdir* for others.
+   a. Type **chmod o-r newdir**.
+   Who, what, which.
+   b. Press <Enter>
+   c. List your home directory, and check your work. You should see permissions for *newdir* as shown in Figure 8-4.

```
drwxrwx--x  1  ronsm  1024  Nov 8  16:00  newdir
drwxrwxr-x  1  ronsm  1024  Mar  1  12:23  practice
```

Figure 8-4 Results of Removing Read Permission
from *newdir* for Others

+   7. Remove execute permission for the group and others from **newdir**.
+   a. Type **chmod go-x newdir**
+   Who, what, which.
+   b. Press <Enter>
+   c. List your home directory, and check your work. You should see permissions for **newdir** as shown in Figure 8-5.

```
drwxrw----  1  ronsm  1024  Nov 8  16:00  newdir
drwxrwxr-x  1  ronsm  1024  Mar  1  12:23  practice
```

Figure 8-5 Results of Removing Execute Permission
from *newdir* for Group and Others

+   8. Change the group's permissions for *newdir* to read and execute; add read permission for others to **newdir**.
+   a. Type **chmod g=rx,o+r newdir**
+   Who, what, which.
+   b. Press <Enter>
+   c. List your home directory, and check your work. You should see permissions for **newdir** as shown in Figure 8-6.