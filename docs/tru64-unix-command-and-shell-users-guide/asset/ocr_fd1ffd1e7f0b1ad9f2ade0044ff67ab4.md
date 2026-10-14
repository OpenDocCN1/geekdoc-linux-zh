# Controlling Access to Your Files and Directories

This chapter shows you how to control access to your system as well as your files and directories. After reading this chapter, you will be able to:

+   - Understand password, group, and system security issues
+   - Understand file and directory permissions
+   - Display and set file and directory permissions
+   - Change owners and groups
+   - Change your identity to access files
+   - Understand superuser concepts
+   - Find information about enhancements to security that may be installed on your system

A good way to learn about the topics in this chapter is to do the examples so that the information on your screen is consistent with the information in this book.

Before you can work through the examples, you must be logged in and your login directory should contain:

+   - The files file1, file2, file3, record1, and record6
+   - The subdirectory reports that contains the file1, file2, file3, and notes files and the subdirectory newstatus
+   - The project subdirectory that contains the files file1, file2, file3, and notes as well as the subdirectory status

If you are using files with different names, make the appropriate substitutions as you work through the examples.

# 5.1 Understanding Password and Group Security Files

Before a user can log in successfully, the user must be made known to the system by the creation of a user account. Adding a user account is a routine but critical activity that is usually performed by the system administrator.

When a user account is created, information about the new user is added to the following two files: