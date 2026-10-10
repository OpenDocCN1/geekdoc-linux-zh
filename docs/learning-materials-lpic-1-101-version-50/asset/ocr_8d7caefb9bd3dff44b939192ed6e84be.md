![](bbox=[0.59, 0.08, 0.92, 0.19])

# # 104.6 Lesson 1

|  |  |
| --- | --- |
| Certificate: | LPIC-1 |
| Version: | 5.0 |
| Topic: | 104 Devices, Linux Filesystems, Filesystem Hierarchy Standard |
| Objective: | 104.6 Create and change hard and symbolic links |
| Lesson: | 1 of 1 |

# ## Introduction

On Linux some files get a special treatment either because of the place they are stored in, such as temporary files, or the way they interact with the filesystem, like links. In this lesson you will learn what links are and how to manage them.

# ## Understanding Links

As already mentioned, on Linux everything is treated as a file. But there is a special kind of file, called a link, and there are two types of links on a Linux system:

# ### Symbolic links

Also called soft links, they point to the path of another file. If you delete the file the link points to (called target) the link will still exist, but it “stops working”, as it now points to “nothing”.

# ### Hard links

Think of a hard link as a second name for the original file. They are not duplicates, but instead