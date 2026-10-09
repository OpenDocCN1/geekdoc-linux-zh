2 respectively. Furthermore, these descriptors are associated with the terminal from which the process was started. The purpose of redirstions and pipes is to redirect these descriptors to a different location. For example, instead of having the output of a process go to the screen, you can redirect it to a text file.

# **Redirections**   Suppose that you want to run a specific program and cannot remember the name of the program. It would be helpful to see a list of all the programs available, but so many files are listed it is difficult to view them satisfactorily. One way to view the files at your leisure is to copy the directory contents to a file and then view the file.

To redirect standard input or output, use the redirection symbols greater than (> ) or less than (<). You should think of the redirection symbols as showing the direction to redirect. The > is used to redirect output, or away from the command. The < is used to redirect input, or into the command.

The > symbol redirects the output that would normally go to the screen to wherever you point. For example, if you wanted to redirect a directory listing (ls -l) to a file called myfile, you would type the command ls -l > myfile.

The < symbol redirects the input that would normally come from the keyboard to come from a file instead. For example, if you wanted to count the number of lines in the file myfile, you could either count the lines by hand or use the word count (wc) program to count them for you. To use wc, type wc -l < myfile.

The -l option says to count lines, and the < myfile redirects input to the wc command from the file myfile.

> For more information on wc refer to the man pages.

Now suppose that you are the user jsmith and want a list of all programs in the /sbin directory. Follow the next few steps:

+   Log in to the CLI as jsmith.
After you are logged in, change directories to /sbin with the cd command: cd /sbin
List a long list directory, directing the output to a file called myfiles instead of to the screen: ls -l > myfiles
View the contents of myfiles with the following command: view myfiles.

> The view command is a subset of the vim (Vi MImproved) command. The standard editor for Linux CLI is vi (often referred to as virtually impossible). The new and improved version of vi is vim. Using the command view opens a file with vim in read-only mode. You can then use the up/down arrow keys to browse the file. Use man vim for a complete description.

# **Pipes**   A pipe is in some ways an input/output redirection. It is used to send the output of one command to the input of another program. Suppose that you want to know how many JPEG images are in your pictures directory.