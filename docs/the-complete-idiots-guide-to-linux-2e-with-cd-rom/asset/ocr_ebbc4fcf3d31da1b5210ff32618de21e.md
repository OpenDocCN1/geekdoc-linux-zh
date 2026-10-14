To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

# Chapter 17
Command Toolbox: Useful Shell Commands and Shortcuts

# In This Chapter

+   - User Utilities
+   - Finding Files
+   - Text and File Utilities
+   - Splitting Files into Smaller Files: split
+   - Accessing a Computer Through the Network: telnet
+   - Working on the Console: setfont
+   - UNIX Printing Primer
+   - UNIX Text Processing

This chapter introduces a number of basic tools and command line programs that you can use while working on the shell. There are many more tools available, but these are some of the more basic ones. You have already learned a few in each category. Although this chapter is not comprehensive, it will give you an idea of what you will find. Many more tools are available—so many, in fact, that it could be the topic for an entire book.

# User Utilities

Every once in a while during the course of your work, you will want to change your password, change your shell, find files, search files, and so on. Here are some commands to help you.

# Changing Your Password: passwd

Use the passwd command to change your password. Because the command is interactive, it will ask you for your current password (to ensure that some other user doesn’t change your password while you are away from your computer) and then for a new password. After successful confirmation of your password, it is accepted by the system. Note that passwords are never echoed to the screen to avoid being spied by nearby eyes, as in the following code: