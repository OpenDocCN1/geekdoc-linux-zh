```
Another_Directory  picture.jpg  text.txt
```

But there is much more information available for each file, including its type, size, ownership and more. To see this information you must ask `ls` for a "long form" listing, using the `-l` parameter:

```
$ ls -l
total 536
drwxrwxr-x 2 carol carol   4096 Dec 10 15:57 Another_Directory
-rw------- 1 carol carol  539663 Dec 10 10:43 picture.jpg
-rw-rw-r-- 1 carol carol    1881 Dec 10 15:57 text.txt
```

Each column on the output above has a meaning. Let us have a look at the columns relevant for this lesson.

+   - The `first` column on the listing shows the file type and permissions. For example, on `drwxrwxr-x`:
+      - The first character, `d`, indicates the file type.
+      - The next three characters, `rwx`, indicate the permissions for the `owner` of the file, also referred to as `user` or `u`.
+      - The next three characters, `rwx`, indicate the permissions for the `group` owning the file, also referred to as `g`.
+      - The last three characters, `r-x`, indicate the permissions for anyone else, also known as `others` or `o`.

> It is also common to hear the `others` permission set referred to as `world` permissions, as in "Everyone else in the world has these permissions".

+   - The `third` and `fourth` columns show ownership information: respectively the user and group that own the file.
+   - The `seventh` and last column shows the file name.

The `second` column indicates the number of hard links pointing to that file. The `fifth` column shows the filesize. The `sixth` column shows the date and time the file was last modified. But these columns are not relevant for the current topic.

# What about Directories?

If you try to query information about a directory using `ls -l`, it will show you a listing of the directory's contents instead: