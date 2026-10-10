|x -x file|Checks if file exists and is executable.|
					|-o file|Checks if file exists and is owned by the current user.|
					|-G file|Checks if file exists and the default group is the same as the current user.|
					|file1 -nt file2|Checks if file1 is newer than file2.|
					|file1 -ot file2|Checks if file1 is older than file2.|
				

These conditions give you the ability to check filesystem files within shell scripts. They are often used in scripts that access files. Because they're used so often, let's look at each of these individually.

# # Checking directories

The -d test checks to see if a specified directory exists on the system. This is usually a good thing to do if you're trying to write a file to a directory or before you try to change to a directory location:

```
$catjump_point.sh#!/bin/bash#Lookbeforeyouleap#jump_directory=/home/Torfa#if[-d$jump_directory]thenecho“The$jump_directory directoryexists.”cd$jump_directorylselseecho“The$jump_directory directorydoesNOTexist.”fi$./jump_point.shThe/home/Torfa directorydoesNOTexist.$
```

The -d test condition checks to see if the jump_directory variable's directory exists. If it does, it proceeds to use the cd command to change to the current directory and performs a directory listing. If it does not, the script emits a warning message and exits the script.