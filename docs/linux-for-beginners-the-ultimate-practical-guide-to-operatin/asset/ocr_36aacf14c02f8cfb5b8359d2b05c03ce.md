# # CHAPTER 13. Exercises

As we have already learned above, the creation of a directory is pretty easy. In the same manner, removing or deleting a directory from the Linux system is also very simple. One thing that you have to bear in mind, however, once you remove or delete a directory from the Linux system, there is no way to undo that task. Therefore, the best thing is whenever you are running any command on Linux; the first thing is to be careful with what you do. If it means double checking the command before running it, the better. The command we are going to use to remove or delete a directory is rmdir which stands for remove directory. The things that you have to take note of here is that rmdir command supports the -p and -v options in the same manner as mkdir command. Additionally, the directory has to be empty before t is removed. We will learn how to get around this later.

+   1. `rmdir linux_tutorial/beginner/commands`
+   2. `ls linux_tutorial/beginner`

# ## How to create a blank file

Many commands that are involved in data manipulation within a file have a superb feature that they will create a file automatically when we refer to it, and we find that it does not exist. As a matter of fact, we can manipulate this feature to create a blank file using the touch command. In other words, you type the command touch followed by the command line option and the file name.

+   1. `pwd`
+   2. `/home/Gary/linux_tutorial`
+   3. `ls`
+   4. `beginner`
+   5. `touch practice_exercise1`
+   6. `ls practice_exercise1 commands`