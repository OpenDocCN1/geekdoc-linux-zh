# CHAPTER 6 THE LINUX FILESYSTEM

![](bbox=[0.328, 0.098, 0.807, 0.342])

**Figure 6-1** A family tree

# # THE HIERARCHICAL FILESYSTEM

Family tree *A hierarchical structure* (page 1151) frequently takes the shape of a pyramid. An example of this type of structure is found by tracing a family's lineage: A couple has a child, who may in turn have several children, of whom may have more children. This hierarchical structure is called a *family tree (Figure 6-1)*

Directory Like the family tree it resembles, the Linux filesystem is called a *tree*. It consists of a set of connected files. This structure allows you to organize files so you can easily find any particular one. On a standard Linux system, each user starts with one directory, to which the user can add subdirectories to any desired level. By creating multiple levels of subdirectories, a user can expand the structure as needed.

Subdirectories Typically each subdirectory is dedicated to a single subject, such as a person, project, or event. For example, Figure 6-2 shows a secretary's subdirectory named correspond. This directory contains three subdirectories: **business**, **memo**, and **personal**. The *business* directory contains files that store each letter the secretary types. If you expect many letters to go one client, as is the case with *milk_co*, you can dedicate a subdirectory to that client.

One major strength of the Linux filesystem is its ability to adapt to users' needs. You can take advantage of this strength by strategically organizing your files so they are most convenient and useful for you.

# # DIRECTORY FILES AND ORDINARY FILES

Like a family tree, the tree representing the filesystem is usually pictured upside down, with its *root* at the top. Figures 6-2 and 6-3 show that the tree “grows”