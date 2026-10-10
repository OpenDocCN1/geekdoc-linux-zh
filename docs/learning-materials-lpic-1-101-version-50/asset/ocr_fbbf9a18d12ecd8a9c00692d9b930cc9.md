# # Summary

In this lesson, you learned:

+   - What links are.
+   - The difference between *symbolic* and *hard* links.
+   - How to create links.
+   - How to move, rename or remove these links.

The following commands were discussed on this lesson:

+   - `ln`: The “link” command. By itself, this command creates a hard link. With the `-s` switch a *symbolic* or *soft* link can be created. Remember that hard links can only reside on the same partition and filesystem, and symbolic links can traverse partitions and filesystems (even network attached storage).
+   - The `-i` parameter to `ls`, which allows one to view the inode number for a file.