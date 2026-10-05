# Graphics, Multimedia, and Productivity Tools
PART IV

# echo SPATH

If the directory where the file myenv is located is not in the current search path, you must add the directory name in the search path. Now you can execute the file myenv from the command line as if it were a Linux command:

# ./myenv

> Note
The first line in your shell program should start with a pound sign (#), which tells the shell that the line is a comment. Following the pound sign, you must have an exclamation point (!), which tells the shell to run the command following the exclamation point and to use the rest of the file as input for that command. This is common practice for all shell scripting. For example, if you write a shell script for bash, the first line of your script would contain !/bin/bash.

A second way to execute myenv under a particular shell (such as bash), is as follows:

# bash myenv

This invokes a new shell and passes the filename myenv as a parameter to execute the file. You can also execute myenv from the command line as follows:

| Command Line | Environment |
| . myenv | pdksh and bash |
| # source myenv | tsh |

The dot (.) is a way of telling the shell to execute the file myenv. In this case, you do not have to ensure that the execute permission of the file has been set. Under tsh, you have to use the source command instead of the dot (.)

After you execute the command myenv, you should be able to use dir from the command line to get a list of files from the current directory and 11 to get a list of files with various attributes displayed. However, the only way to use the new commands in myenv with the bash shell is to push them into your login or profile file. The default shell for SuSE Linux users is bash, so these commands can be made available for everyone on your system by putting them in the file profile under the /etc directory.