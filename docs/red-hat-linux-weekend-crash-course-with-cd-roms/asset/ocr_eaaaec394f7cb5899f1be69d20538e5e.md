| Command Name | Description |
|---|---|
| rm | Deletes files. The syntax is rm filename. (Use with caution because the file gets deleted.) |
| rmdir | Deletes directories. Type rmdir ~/temp to remove the directory named temp in your home directory (see the mkdir command). |
| pwd | Displays the current directory. Type pwd to see the current directory name. |
| Finding Files | |
| find | Finds files based on specified criteria such as name, size, and so on. Type find /usr -name "README*" -print to try this command. |
| Processing Files | |
| cat | Displays a file on standard output (can concatenate several files into one big file). Type cd to go to your home directory and then type cat .bash_profile to see the contents of that file. |
| grep | Searches for regular expressions within a text file. Type cd to go to your home directory and then type grep BASH .b* to see the result of searching for the string BASH in some files. |
| more | Displays a text file one page at a time. Type more /etc/inittab to see the contents one page at a time. (Press the Spacebar to advance or type q to quit.) |
| Managing Processes | |
| printenv | Displays the current environment variables. Type printenv to see the list of environment variables. |
| Managing Users | |
| passwd | Changes the password. Type passwd and follow the prompts to change your password. |
| su | Becomes another user or root (when invoked without any argument). Type su and enter the root password when prompted. Be careful what you do because now you are the super user. Type exit to return to normal user. |

The following sections cover new commands (by category) not covered in the earlier sessions.