To set a new `umask`, type `umask` followed by the numerical value of the mask. Here is how you go about it:

+   1.  **Figure out what permission settings you want for new files.**
+   
+       For example, if you want new files that can be read and written only by the owner and by nobody else, the permission setting looks like this:
+   
+       ```
+       rw-------
+       ```
+   2.  **Convert the permissions into a numerical value by using the conversion method that assigns 4 to the first field, 2 to the second, and 1 to the third.**
+   
+       Thus, for files that are readable and writable only by their owner, the permission setting is 600.
+   3.  **Subtract the desired permission setting from 666 to get the value of the mask.**
+   
+       For a permission setting of 600, the mask becomes 666 - 600 = 066.
+   4.  **Use the umask command to set the file-creation mask:**
+   
+       ```
+       umask 066
+       ```

![](bbox=[0.12, 0.5, 0.2, 0.59])

> A default `umask` of 022 is good for system security because it translates to files that have read and write permission for the owner and read permissions for everyone else. The bottom line is that you don't want a default `umask` that results in files that are writable by the whole wide world.

# ## Checking for set user ID permission

Another permission setting can be a security hazard. This permission setting, called the set user ID (or `setuid` for short), applies to executable files. When the `setuid` permission is enabled, the file executes under the user ID of the file’s owner. In other words, if an executable program is owned by `root` and the `setuid` permission is set, no matter who executes that program, it runs as if `root` is executing it. This permission means that the program can do a lot more (for example, read all files, create new files, and delete files) than what a normal user program can do. Another risk is that if a `setuid` program file has some security hole, crackers can do a lot more damage through such programs than through other vulnerabilities.

You can find all `setuid` programs with a simple `find` command:

```
```bash
find / -type f -perm +4000 -print
```
```