# 5. Files and Directories

This chapter discusses the basic tools for manipulating files and directories—tools that are among the most essential on a Linux system.

A file is a collection of data that is stored on disk and that can be manipulated as a single unit by its name.

A directory is a file that acts as a folder for other files. A directory can also contain other directories (called subdirectories in this context); a directory that contains another directory is called the parent directory of the child directory it contains.

You might think of a regular file as a folder in a file cabinet drawer. The folder has a name, it holds the information that is put into it, and that information can be rearranged; you can recall the file at any time, and you can destroy it. The drawers of the the file cabinet then would be directories, and every file must be kept in one.

There the metaphor ends. The folders can be copied identically, and phantom folders can exist whose contents point to the contents of one of your real folders, so that when you look inside the phantom you are looking in the contents of a folder somewhere else. You can have as many directories as you like, and unlike physical file cabinets, you can have drawers inside other drawers, which in turn can have their own drawers on and on. In fact, there is a “master” drawer, the root directory, which contains inside it all other drawers—each drawer must in turn be kept inside some other drawer.

It is also helpful to think of the directories on a system like a tree with all its branches, because directories form a branching hierarchy—and the tree metaphor is used frequently to describe them: a directory tree includes a directory and all of its files, including the contents of all subdirectories. (Each directory is a “branch” in the “tree.”) A slash character alone (/) is the name of the root directory at the base of the directory tree hierarchy; think of it as forming the roots and trunk from which all other files or directories are supported and from which they all inevitably branch out.

An abridged version of the root directory tree is shown in Figure 5-1.

To represent a directory’s place in the file hierarchy, specify all of the directories between it and the root directory, using a slash (/) as the delimiter to separate directories. So the directory dict as it appears in the preceding illustration would be represented as /usr/dict.