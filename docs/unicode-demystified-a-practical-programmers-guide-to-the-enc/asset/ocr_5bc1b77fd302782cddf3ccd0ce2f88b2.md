```
$ ls -l whoson
-rw-r-- 1 alex group      40 May 24 11:30 whoson
$ chmod u+x whoson
$ ls -l whoson
-rwx--r-- 1 alex group      40 May 24 11:30 whoson
```

```
$ whoson
Sat May 24 11:40:49 PST 2003
Users Currently Logged In
ny pts/7 May 23 18:17
hls pts/1 May 24 09:59
scott pts/12 May 24 06:29 (bravo.tcorp.com)
alex pts/4 May 24 09:08
```

**Figure 12-1** Using chmod to make a shell script executable

When you create a file such as whoson, you cannot execute it by giving its name as a command because you do not have execute permission for the file.
The shell does not recognize whoson as an executable file and issues an error message when you try to execute it. You can execute it by giving the filename as an argument to `bash whoson`. When you do this, bash takes the argument to a shell script and executes it. In this case bash is executable, and whoson is an argument that bash executes so you do not need to have permission to execute whoson.
You can do the same with tosh and zsh.

You can use chmod (pages 119 and 1103) to change the access privileges associated with a file. Figure 12-1 shows it with the -l option indicating the access privileges of whoson before and after chmod gives the owner execute permission.
The first ls shows a hyphen (–) as the fourth character, indicating that the owner does not have permission to execute the file. Then chmod u+x causes chmod to add (+) execute permission (x) for the owner (u). The u stands for *user*, indicating it means the owner of the file who may be the user of the file at any time. The second argument is the name of the file. The second ls shows an x in the fourth position, indicating that the owner has execute permission.

If other users are going to execute the file, you must also change group and/or public privileges. Any user must have execute access to a file to use the file's name as a command. If the file is a shell script (a shell command file), the user trying to execute the file must also have read access to the file. You do not need read access to a binary executable (compiled program). Finally, the shell executes when its name is given as a command. For more information refer to “Access Permissions” (page 118) and to ls and chmod in Part III.

Now you know how to write and execute simple shell scripts. The sections “Separating and Grouping Commands” (following) and “Redirecting Standard Error” (page 552) describe features that are useful when you are running commands either on a command line or from within a script. The section “Job Control” (page 554) explains the relationships between commands and GNU/Linux system processes.