This chapter covers many of the various tools used for managing files. Basic commands used for creating, moving, and deleting files are covered. Also covered in this chapter are commands used for dealing with directories that contain files. A variety of tools used for locating and compressing files are explained in this chapter. You will also learn about the tools used for managing quotas and permissions, two areas where users and files are closely connected. Finally, you will learn how file links are used and where the standard location of many of the files on a Linux system is. File management is a major part of working with a Linux system, so thoroughly understanding the material covered in this chapter is important.

# # Managing Files

# ## 1.3 GNU and Unix Commands

+   * Perform Basic File Management. Use the basic unix commands to copy and move files and directories. Perform advanced file management operations such as copying multiple files recursively and moving files that meet a wildcard pattern. Use simple and advanced wildcard specifications to refer to files.

When working with a Linux system, you need to be familiar with basic commands used for file management. In this section we cover the most commonly used tasks, including moving around the file system and working with directories and files.

![](bbox=[0.13, 0.6, 0.19, 0.66])

> > You will need to know the purpose of each command along with the commonly used options and functionality.

When working with files on a Linux system, you should keep in mind a few practices and restrictions. Hidden files begin with a period. Filenames can begin with a number, but they can't contain slashes, question marks, asterisks, or other reserved characters. File extensions aren't always required but can be useful for keeping track of file types.

The following sections examine some of the basic commands used when dealing with files and directories.

# ## Changing directories

Directories on a Linux system are arranged in a tree structure. The / directory, known as the root directory, contains a number of system directories. Each of these directories can contain further directories and so on as the tree branches outward. Figure 6-1 shows this directory structure. The system directories and their locations are covered later in this chapter.