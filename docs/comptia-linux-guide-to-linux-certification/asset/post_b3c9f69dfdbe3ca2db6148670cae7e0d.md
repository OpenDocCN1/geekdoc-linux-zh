
The files listed previously and discussed throughout this chapter are for example purposes only. The Hands-on Projects use different files.

![](img/c27875544958897d817484d558c208c8_119_0.png)

The `ls` command displays all the files in the current directory in columnar format; however, you can also pass an argument to the `ls` command indicating the directory to be listed if the current directory listing is not required. In the following example, the files are listed underneath the /home/bob directory without changing the current directory.

```
[root@server1 ~]# pwd
 /root
 [root@server1 ~]# ls /home/bob
 assignment1 file1 letter letter2 project1
 [root@server1 ~]#
```

When running the `ls` command, you will notice that files of different types are often represented as different colors; however, the specific colors used to represent files of certain types might vary from terminal to terminal and distribution to distribution. As a result, do not assume color alone indicates the file type.

![](img/c27875544958897d817484d558c208c8_119_1.png)

Windows uses the `dir` command to list files and directories; to simplify the learning of Linux for Windows users, there is a `dir` command in Linux, which is simply a pointer or shortcut to the `ls` command.

![](img/c27875544958897d817484d558c208c8_119_2.png)

Recall from the previous chapter that you can use switches to alter the behavior of commands. To view a list of files and their type, use the -F switch to the `ls` command:

```
[root@server1 ~]# pwd
 /root
 [root@server1 ~]# ls -F
 current@ myprogram* project project12 project2 project4
 Desktop/ myscript/ project1 project13 project3 project5
 [root@server1 ~]#
```

The `ls -F` command appends a special character at the end of each filename displayed to indicate the type of file. In the preceding output, note that the filenames current, Desktop, myprogram, and myscript have special characters appended to their names. The @ symbol indicates a linked file, the * symbol indicates an executable file, the / indicates a subdirectory, the = character indicates a socket, and the | character indicates a named pipe. All other file types do not have a special character appended to them and could be text files, binary data files, or special device files.

It is common convention to name directories starting with an uppercase letter, such as the D in the Desktop directory shown in the preceding output. This allows you to quickly determine which names refer to directories when running the `ls` command without any options that specify file type.

![](img/c27875544958897d817484d558c208c8_119_3.png)

Although the `ls -F` command is a quick way of getting file type information in an easy-to-read format, at times you need to obtain more detailed information about each file. The `ls -l` command can be used to provide a long listing for each file in a certain directory.

```
[root@server1 ~]# pwd
/root
[root@server1 ~]# ls -l
total 548
lrwxrwxrwx 1 root root 9 Apr 7 09:56 current -> project12
drwx------ 3 root root 4096 Mar 29 10:01 Desktop
-rwxr-xr-x 1 root root 519964 Apr 7 09:59 myprogram
-rwxr-xr-x 1 root root 20 Apr 7 09:58 myscript
-rw-r--r-- 1 root root 71 Apr 7 09:58 project
-rw-r--r-- 1 root root 71 Apr 7 09:59 project1
-rw-r--r-- 1 root root 71 Apr 7 09:59 project12
-rw-r--r-- 1 root root 0 Apr 7 09:56 project13
-rw-r--r-- 1 root root 71 Apr 7 09:59 project2
-rw-r--r-- 1 root root 90 Apr 7 10:01 project3
-rw-r--r-- 1 root root 99 Apr 7 10:01 project4
-rw-r--r-- 1 root root 108 Apr 7 10:01 project5
[root@server1 ~]#
```

Each file listed in the preceding example has eight components of information listed in columns from left to right:

- 1. A file type character
    - The d character represents a directory.
    - The l character represents a symbolically linked file (discussed in Chapter 4).
    - The b or c characters represent special device files (discussed in Chapter 5).
    - The n character represents a named pipe.
    - The s character represents a socket.
    - The - character represents all other file types (text files, binary data files).
- 2. A list of permissions on the file (also called the mode of the file)
- 3. A hard links count (discussed in Chapter 5)
- 4. The owner of the file (discussed in Chapter 5)
- 5. The group owner of the file (discussed in Chapter 5)
- 6. The file size
- 7. The most recent modification time of the file
- 8. The filename (Some files are shortcuts or pointers to other files and indicated with an arrow ->, as with the file called “current” in the preceding output; these are known as symbolic links and are discussed in Chapter 5.)

For the file named “project” in the previous example, you can see that this file is a regular file because the long listing of it begins with a - character, the permissions on the file are rw-r--r--, the hard link count is 1, the owner of the file is root user, the group owner of the file is the root group, the size of the file is 71 bytes, and the file was modified last on April 7th at 9:58 a.m.

![](img/c27875544958897d817484d558c208c8_121_0.png)

> If SELinux is enabled on your system, you may also notice a period (.) immediately following the permissions on a file or directory that is managed by SELinux. SELinux will be discussed later in Chapter 14.

![](img/c27875544958897d817484d558c208c8_121_1.png)

> On most Linux systems, a shortcut to the `ls` command can be used to display the same columns of information as the `ls -l` command. Some users prefer to use this shortcut, commonly known as an alias, which is invoked when a user types `ll` as a command prompt. This is known as the `ll` command.

The `ls -F` and `ls -l` commands are valuable to a user who wants to display file types; however, neither of these commands can display all file types using special characters. To display the file type of any file, you can use the `file` command; simply give the `file` command an argument specifying what file to analyze. You can also pass multiple files as arguments or use the * metacharacter to refer to all files in the current directory. An example of using the `file` command in the root user’s home directory is:

```
[root@server1 ~]# pwd
/root
[root@server1 ~]# ls
current    myprogram    project    project12    project2    project4
Desktop    myscript    project1    project13    project3    project5
[root@server1 ~]# file Desktop
Desktop: directory
[root@server1 ~]# file project Desktop
project: ASCII text
Desktop: directory
[root@server1 ~]# file *
Desktop: directory
current: symbolic link to project12
myprogram: ELF 32-bit LSB executable, Intel 80386, version 1, dynamically linked (uses shared libs), stripped
myscript: Bourne-Again shell script text executable
project: ASCII text
project1: ASCII text
project12: ASCII text
project13: empty
project2: ASCII text
project3: ASCII text
project4: ASCII text
project5: ASCII text
[root@server1 ~]#
```

As shown in the preceding example, the `file` command can also identify the differences between types of executable files. The `myscript` file is a text file that contains executable commands (also known as a shell script), whereas the myprogram file is a 32-bit executable compiled program. The file command also identifies empty files such as project13 in the previous example.

Some filenames inside each user's home directory represent important configuration files or program directories. Because these files are rarely edited by the user and can clutter up the listing of files, they are normally hidden from view when using the ls and file commands. Recall that filenames for hidden files start with a period character (.). To view them, simply pass the -a option to the ls command. Some hidden files that are commonly seen in the root user's home directory are shown next:

```
[root@server1 ~]# ls
current myprogram project project12 project2 project4
Desktop myscript project1 project13 project3 project5
[root@server1 ~]# ls -a
. .gimp-2.8 project
.. .gnome project1
.bash_history .gnome-desktop project12
.bash_logout .gnome_private project13
.bash_profile .gtkrc project2
.bashrc .ICEauthority project3
.cshrc .kde project4
current .mcop project5
.DCOPServer_server1_0 .MCOP-random-seed .sane
Desktop .mcoprc .sawfish
.first_start_kde .mozilla .tcsfrc
.galeon myprogram .Xauthority
.gconf myscript .Xresources
.gconfd .nautilus .xsession-errors
[root@server1 ~]#
```

As discussed earlier, the (.) character refers to the current working directory and the (..) character refers to the parent directory relative to your current location in the directory tree. Each of these pointers is seen as a special (or fictitious) file when using the ls -a command, as each starts with a period.

You can also specify several options simultaneously for most commands on the command line and receive the combined functionality of all the options. For example, to view all hidden files and their file types, you could type:

```
[root@server1 ~]# ls -aF
./. .gimp-2.8/ project/
../ .gnome/ project1
.bash_history .gnome-desktop/ project12
.bash_logout .gnome_private/ project13
.bash_profile .gtkrc project2
.bashrc .ICEauthority project3
.cshrc .kde/ project4
current@ .mcop/ project5
.DCOPServer_server1_0@ .MCOP-random-seed .sane/
Desktop/ .mcoprc .sawfish/
```
