
## Question 2
Which of the following statements most accurately describe the characteristics of environment and shell variables?

- a. An environment variable applies to all users. A shell variable remains constant as you move from shell to shell.
- b. An environment variable applies to all shells. A shell variable may change, or may not even exist, as you move from shell to shell.
- c. An environment variable applies to all users. A shell variable may change, or may not even exist, as you move from shell to shell.
- d. An environment variable applies to all shells. A shell variable remains constant as you move from shell to shell.

Answer b is correct. Although environment variables apply to all shells, a shell variable changes from shell to shell (unless you export that variable). Because environment variables may not apply to all users, answers a and c are incorrect. Shell variables are not normally constant from shell to shell; therefore, answer d is incorrect.

## Question 3
You have a large number of files in your home directory including the figures that you need for your seventh presentation. These figures are in binary format. Based on your company policy, you've organized your figures in the following format: fig07-xx, where xx is the figure number. You want to see if you have figures 10 through 19. You don't want to see any other figures in the list. Which of the following commands will list just the figures that you want?

- a. ls -ltr fig07-*
- b. ls -ltr fig07-[10-19]
- c. ls -ltr fig07-1?
- d. ls -ltr fig07-1*

Answer c is correct. The question mark is a wildcard for the one character position. Because the asterisk is a wildcard for any number of characters, answer a is incorrect. The bracketed search terms only work for one character at a time; you would need ls -ltr fig07-1[0-9] for this to work. Therefore, answer b is incorrect. Because the asterisk includes any number of characters, answer d could include fig07-1, fig07-1000, and so on. Therefore, answer d is also incorrect.

## Question 4
You started a program in a command-line interface, and because you're not in a graphical user interface, you can't just click a button to start another shell. The program seems like it's going to run for a long time. You want it to keep running, but you need to check your email. What can you do? [Check all correct answers]

- a. Press Ctrl+C, and when you see the command-line interface, type the bg command to move the process into the background.
- b. Press Ctrl+Z, and when you see the command-line interface, type the bg command to move the process into the background.
- c. Press Ctrl+Alt+F2, and when you see the login screen, log in again. Your program will keep running in another virtual console. If F2 doesn't work, try F1, F3, or F4.
- d. Press Ctrl+Z, and when you see the command-line interface, restart the program using an ampersand (&) at the end. This resumes the process in the background. You will then see a command-line interface where you can run another program.

Answers b and c are correct. The Ctrl+Z command suspends a running process, and the bg command restarts the process in the background. You can use the Ctrl+Alt+Fx (x is a number from 1 to 6) command to start another virtual console. The program continues to run in your original console. Because the Ctrl+C command stops a running program, answer a is incorrect. Because your program is still running, you do not need to start it again. Although you could use an ampersand (&) if you hadn't already started your program, using it at this time means you would have to start your program again. Therefore, answer d is incorrect.

## Question 5
You've created a program called filemanager, which uses the files listed in the current directory. You just want to use file names, and you don't want to use any hidden file names. Which of the following commands is the most efficient way to feed data to the filemanager program?

- a. ls -l filemanager
- b. ls -a filemanager
- c. ls > filemanager
- d. ls | filemanager

Answer d is correct. The plain ls command outputs just the file names in the current directory. With the pipe (|), this information becomes standard input (stdin) for the filemanager program. The ls -l command outputs permissions, owners, and so on. Therefore, answer a is incorrect. The ls -a command outputs hidden files. Therefore, answer b is incorrect. Because ls -a command would overwrite your filemanager program with your current file list, answer c is incorrect.

## Question 6
There are three different standard I/O channels. Which of the following methods is an allowable way to redirect these channels?

- a. Stdin can be redirected from a file. If you have a number of input terms in the text file crabgrass and a script named runner, you can execute the runner << crabgrass command.
- b. Stdout can be redirected to a file. If you have a number of input terms in the text file crabgrass and a script named runner, you can direct the output to a third file with the runner crabgrass 2> otherfile command.
- c. Stderr can be redirected to a file. If you have a number of input terms in the text file crabgrass and a script named runner, you can direct the error to a third file with the runner crabgrass >> logfile command.
- d. Stdin can be redirected from a file. Stdout can also be redirected to another file. If you have a number of input terms in the text file crabgrass and a script named runner, you can execute the runner < crabgrass > otherfile command.

Answer d is correct. You can direct standard input (stdin) from a file with the left arrow (<) switch. You can direct standard output (stdout) to a file with the right arrow (>) switch. You cannot redirect with a double left arrow (<<); therefore, answer a is incorrect. Because stdout cannot be redirected with the error redirect arrow (2>), answer b is incorrect. If you're redirecting standard error (stderr), you need to use 2>>, and not the double right arrow (>>). Therefore, answer c is incorrect.

## Question 7
A user wants to open a text file from an MS-DOS directory named big memo.txt. Whenever he tries to open the file, he sees the following message:

```
big: No such file or directory
```

This user needs your help. Which of the following commands do you tell this user to run? This file is part of the /disks/c/data directory.

- a. vi /disks/c/data/big memo.txt
- b. vi /disks/c/data/big\ memo.txt
- c. vi /disks/c/data/big/ memo.txt /
- d. vi /disks/c/data/bigmemo.txt

Answer b is correct. The backslash (\ ) keeps the shell from interpreting characters such as the question mark (?), asterisk (*), and space. The backslash in answer b allows the vi editor to see these characters for what they are, instead of interpreting them as wildcards or new files. Because there is no backslash that "escapes" the space in answers a and c, these answers are both incorrect. Because there is no space after the backslash, answer d opens the bigmemo.txt file; therefore, this answer is incorrect.

## Question 8
Which of the following commands lists the files in your directory with inode numbers? The output should allow you to differentiate between regular files, directories, and executable files. It should also list the most newly revised file last.

- a. ls -ltr
- b. ls -iTr
- c. ls -iFr
- d. ls -dir

Answer c is correct. The switches in this command give you inode numbers (-i), help you differentiate between regular files, directories, and executable files (-F), and set up the order so that the oldest file is first and the newest file is last (-r). A long listing does not give you inode numbers; therefore, answer a is incorrect. Nothing in answer b allows you to differentiate between files and directories, so it is also incorrect. Because answer d only gives you the inode number of the current directory, it is also incorrect.

## Question 9
Which of the following values of umask corresponds to read and execute permissions for the file owner, write and execute permissions for other members of the owner's group, and execute permissions for other users on a Linux computer?

- a. 531
- b. 731
- c. 246
- d. 642

Answer c is correct. The umask is the value that you subtract from full read (r), write (w), and execute (x) permissions for each type of user. Read and execute permissions (4 +1) correspond to the number 5, so the first number of umask is (7-5=) 2. Write and execute permissions (2 +1) correspond to the number 3, so the second number of umask is (7-3=) 4. Execute permissions correspond to the number 1, so the third number of umask is (7-1=) 6.
