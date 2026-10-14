# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

# Chapter 12
Working with Files on the Shell

# In This Chapter

+   - How to Manage and Organize Your Files Using a Shell
+   - How to Read Files

# Working with Files and Folders

In Chapter 11, “Shells and Consoles,” you learned how to log in and out and how to navigate the file system using a shell. In this chapter you’ll continue your exploration of the UNIX shell and learn how to manipulate files and directories using one.

# Creating a New Empty File: touch

Most of the time you’ll create files as the result of working with some application or shell program. For didactic purposes, I am going to introduce a command that allows you to create empty files here. This ability to generate files as if by magic will make your exploration a little more interesting.

If you need to create an empty file, you can easily do so with the touch command. The purpose of touch is to modify the access and creation times of files, but as a side effect it creates files if they don’t already exist.

To create a file, enter the command touch followed by a filename: