
## Managing Files and Directories

As mentioned earlier, using a Linux system involves navigating several directories and manipulating the files inside them. Thus, an efficient Linux user must understand how to create directories as needed, copy or move files from one directory to another, and delete files and directories. These tasks are commonly referred to as file management tasks.

Following is an example of a directory listing while the user is logged in as the root user:

```
[root@server1 root]# pwd
/root

[root@server1 root]# ls -F
current@  myprogram*  project  project12  project2  project4
Desktop/  myscript  project1  project13  project3  project5
[root@server1 root]#
```

As shown in the preceding output, only one directory (Desktop), two executable files (myprogram and myscript), and several project-related files (project*) exist. Although this directory structure is not cluttered and appears in an easy-to-read format on the terminal screen, typical home directories on a Linux system contain many more files; a typical Linux user might have over 100 files in his home directory. As a result, it is good practice to organize these files into subdirectories based on file purpose. Because several project files are in the root user's home directory in the preceding output, you could create a subdirectory called proj_files to contain the project-related files and decrease the size of the directory listing. To do this, you use the **mkdir (make directory) command**, which takes arguments specifying the absolute or relative pathnames of the directories to create. To create a proj_files directory underneath the current directory, you can use the mkdir command with a relative pathname:

```
[root@server1 root]# mkdir proj_files
[root@server1 root]# ls -F
current@  myprogram*  project  project12  project2  project4  proj_files/
Desktop/  myscript*  project1  project13  project3  project5
[root@server1 root]#
```

Now, you can move the project files into the proj_files subdirectory by using the **mv (move) command**. The mv command requires two arguments at minimum: **the source file/directory and the target file/directory**. If several files are to be moved, simply specify several source arguments; the last argument then becomes the target directory. Both the source(s) and destination can be absolute or relative pathnames, and the source can contain wildcards if several files are to be moved. For example, to move all of the project files to the proj_files directory, you could type mv with the source argument project* (to match all files starting with the letters "project") and the target argument proj_files (relative pathname to the destination directory), as shown in the following output:

```
[root@server1 root]# mv project* proj_files
[root@server1 root]# ls -F
current@  Desktop/  myprogram*  myscript*  proj_files/
[root@server1 root]# ls -F proj_files
project project1 project12 project13 project2 project3 project4 project5
[root@server1 root]#
```

In the preceding output, the current directory listing does not show the project files anymore, yet the listing of the proj_files subdirectory indicates that they were moved successfully.

![](img/09bf13b782f71165e17bb3839040c96a_181_0.png)

If the target is the name of a directory, the mv command moves those files to that directory. If the target is a filename of an existing file in a certain directory and there is one source file, the mv command overwrites the target with the source. If the target is a filename of a nonextant file in a certain directory, the mv command creates a new file with that filename in the target directory and moves the source file to that file.

Another important use of the mv command is to rename files, which is simply moving a file to the same directory but with a different filename. To rename the myscript file from earlier examples to myscript2, you can use the following mv command:

```
[root@server1 root]# ls -F
current@ Desktop/ myprogram* myscript* proj_files/
[root@server1 root]# mv myscript myscript2
[root@server1 root]# ls -F
current@ Desktop/ myprogram* myscript2* proj_files/
[root@server1 root]#
```

Similarly, the mv command can rename directories. If the source is the name of an existing directory, it is renamed to whatever directory name is specified as the target.

The mv command works similarly to a "cut and paste" operation in which the file is copied to a new directory and deleted from the source directory. There might be times, however, when the file in the source directory should be maintained; this is referred to as copying a file and can be accomplished using the cp (copy) command. Much like the mv command, the cp command takes two arguments at minimum. The first argument specifies the source file/directory to be copied and the second argument specifies the target file/directory. If several files need to be copied to a destination directory, simply specify several source arguments and the final argument on the command line becomes the target directory. Each argument can be an absolute or relative pathname and can contain wildcards or the special metacharacters "." (specifies the current directory) and ".." (specifies the parent directory). For example, to make a copy of the file /etc/hosts in the current directory (/root), you can specify the absolute pathname to the /etc/hosts file (/etc/hosts) and the relative pathname indicating the current directory (.):

```
[root@server1 root]# cp /etc/hosts .
[root@server1 root]# ls -F
current@ Desktop/ hosts myprogram* myscript2* proj_files/
[root@server1 root]#
```

You can also make copies of files in the same directory. To make a copy of the host file called hosts2 in the current directory, type the following command:

```
[root@server1 root]# cp hosts hosts2
[root@server1 root]# ls -F
current/  Desktop/  hosts  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]#
```

One notable difference between the mv and cp commands, aside from their purpose, is that they work on directories differently. The mv command simply renames a directory, whereas the cp command creates a whole new copy of the directory and its contents. To copy a directory full of files in Linux, you must tell the cp command that the copy will be **recursive** (involve files and subdirectories too) by using the -r option. The following example demonstrates copying the proj_files directory and all of its contents to the /home/user1 directory without and with the -r option:

```
[root@server1 root]# ls -F
current/  Desktop/  hosts  myprogram*  myscript2*  proj_files/
[root@server1 root]# ls -F /home/user1
Desktop/
[root@server1 root]# cp proj_files /home/user1
cp: omitting directory `proj_files'
[root@server1 root]# ls -F /home/user1
Desktop/
[root@server1 root]# cp -r proj_files /home/user1
[root@server1 root]# ls -F /home/user1
Desktop/  proj_files/
[root@server1 root]#
```

When copying or moving files, if the target is a file that exists, the mv and cp commands warn the user that the target file will be overwritten and ask whether to continue. This is not a feature of the command as normally invoked, but is a feature of the default configuration in Red Hat Linux because the BASH shell in Red Hat Linux contains aliases to the cp and mv commands.

> **NOTE**
> 
> Aliases are special variables in memory that point to commands; they are fully discussed in Chapter 8, "Working with the BASH Shell."

When you type mv, you are really running the mv command with the -i option, which interactively prompts the user to choose whether to overwrite the existing file if the target file already exists when the command is executed; this is called **interactive mode**. Similarly, when you type the `cp` command, the `cp -i` command is run to perform the same function. To see the aliases present in your current shell, simply type `alias`, as shown in the following output:

```
[root@server1 root]# alias
alias cp='cp -i'
alias l='\ls -d . --color=tty'
alias ll='\ls -l --color=tty'
alias ls='\ls --color=tty'
alias mc='../usr/share/mc/bin/mc-wrapper.sh'
alias mv='mv -i'
alias rm='rm -i'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
[root@server1 root]#
```

If you want to override this interactive option, use the `-f` (force) option to override the choice, as shown in the following example in which the root user tries to rename the hosts file to the hosts2 file that already exists without and with the `-f` option to the `mv` command:

```
[root@server1 root]# ls -F
current@  Desktop/  hosts  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]# mv hosts hosts2
mv: overwrite 'hosts2'? n
[root@server1 root]# mv -f hosts hosts2
[root@server1 root]# ls -F
current@  Desktop/  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]#
```

Creating directories, copying, and moving files are file management tasks that preserve or create data on the hard disk. To remove files or directories, you must use either the `rm` command or the `rmdir` command.

The `rm` (remove) command takes a list of arguments specifying the absolute or relative pathnames of files to remove. As with most commands, wildcards can be used to simplify specifying multiple files to remove. After a file has been removed from the filesystem, it cannot be recovered. As a result, the `rm` command is aliased in Red Hat Linux to the `rm` command with the `-i` option, which interactively prompts the user to choose whether to continue with the deletion. Like the `cp` and `mv` commands, the `rm` command also accepts the `-f` option to override this choice and immediately delete the file. An example demonstrating the use of the `rm` and `rm -f` commands to remove the current and hosts2 files is shown in the following example:

```
[root@server1 root]# ls -F
current@  Desktop/  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]# rm current
rm: remove 'current'? y
```
