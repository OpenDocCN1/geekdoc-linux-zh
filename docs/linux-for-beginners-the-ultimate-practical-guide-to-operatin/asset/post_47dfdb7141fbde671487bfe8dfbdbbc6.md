
The directory will be changed to 'httpd' but relative to the '/home' directory. The full working directory will be '/home/httpd'. Now type the following command:

```
cd ..
```

This command will change the working directory to the parent directory of the current directory. In our case, we will move from '/home/httpd' to the '/home' directory. Type the following command:

```
cd ~
```

This command changes the directory to the user's home directory '/home/((username))'. The “username” will be the name you have used on the computer. The symbol “~” is called the tilde and it is used in Linux to represent the user's home directory.

## Copying Files

The command 'cp,' which stands for “copy files” is used for copying files. Note that the file is not deleted from its initial location and a duplicate of the same is made at the specified location. Type the following command:

```
cp first me
```

The command above will make a duplicate of the file first at the same directory but with a new name, that is 'me'. If the file 'me' exists in the directory, it will be overwritten and you will not be warned before this command is executed. Consider the command below:

```
cp -i first me
```

Notice that in the above command we have added the “-i” option. If the file 'me' exists in the directory, you will be notified before it is overwritten. Next, try the following command:

```
cp -i /d/file
```

With the above command, the file '/d/file' will be copied into the same current directory and then named 'file'. Note that we have used the “-i” option so if it already exists we will be notified before it is overwritten.

You might also need to copy all the files contained in a particular directory to another directory. This can be achieved as follows:

```
cp -dpr sourcedirectory destinationdirectory
```

All the files in the directory ‘sourcedirectory’ will be copied to the directory ‘destinationdirectory’. Notice that we have used the option ‘-dpr’. This means the following:

- -d – means that links will be preserved
- -p – file attributes will be preserved
- -r – copying will be done recursively

It is good to specify those options if needed while copying all the files from a directory, otherwise, the default settings will be applied which might produce an unwanted result.

To show the amount of space on a disk used on each of the mounted file systems, use the command ‘df’.

## ‘Less’ Command

The less command is the same as the more command. The difference comes in that with this command the user can page up or down through the file. Consider the example below:

```
less first
```

The above command will display the contents of the file ‘first’.

## ‘Ln’ Command

This command creates a symbolic link to a certain file. Write and run the following command:

```
ln -s first slink
```

The command above will create a symbolic link named ‘slink’ which will link to the file ‘first’. The command `ls -i first slink` will show that the two files are different and have different “inodes”.

## ‘Locate’ Command

This is used for searching in the database. Run the following command:

```
slocate -u
```

A database named ‘slocate’ will be created. This will take some time to complete, so be patient. Before you will be able to search for a file, this command must be run first. However, on most systems, ‘cron’ will run this command on a periodical basis. Again, run the following command:

```
locate whois
```

This command will look for files in your system whose name contains the string “whois”.

## ‘Logout’ Command

The command is used to logout the user who is currently logged into the system. Just go to the terminal and type this command:

```
logout
```

You will then be logged out and returned to the login screen.

## ‘Ls’ Command

‘Ls’ stands for list. It is used for listing files in a directory. However, it comes with many options which need to be known as well, otherwise, you will become confused. If you need to list all the files in the current directory except those starting with “.” then just type in the command:

```
ls
```

![](img/e3fe187ed34a3465fc5a2628f88b7166_12_0.png)

The figure above is the Desktop directory and it contains the files shown. Note that only the file names will be listed. You might need to show more details about the files in the directory such as the ownership permissions, their size, time and date stamp, etc. This can be achieved with the following command:

```
ls -al
```

As shown above, the command ‘ls -al’ is more extensive compared to the previous command. You can use it if you want more details about the file.

## ‘More’ Command

Send contents of a file one page at a time to the screen. It can also work on piped output. Let us list the contents of the file ‘/etc/profile’ to the screen. This is an in-built file, meaning that it comes with the operating system and it contains the profiles for the users of the system:

```
more /etc/profile
```

![](img/e3fe187ed34a3465fc5a2628f88b7166_13_0.png)

Note that the contents of the file will be displayed one page at a time. This is because the content is too big to be displayed on a single page. Consider the command below:

```
ls –all | more
```

The command will list all files in the directory and output will be piped through ‘more’. If the output from the directory can’t fit in one page, it will be listed on an additional page.

## ‘Mv’ Command

This command stands for “move” and is used for renaming or moving files. Consider the command below:

```
mv –i first first2
```

The file will be moved from ‘first’ to ‘first2’, meaning it will be renamed to ‘first2’ rather than ‘first’.

```
mv /d/first
```

The above command will move the file ‘first’ from the directory ‘d’ to the current working directory. Now you have seen how the ‘mv’ command is a powerful tool.

Now that we have been talking of working directories, what are they exactly? And how can we know in which directory they currently are? Just type the command:

```
pwd
```

After pressing the enter key, you notice that the output is a directory. This shows the directory which you are currently in. The abbreviation ‘pwd’ stands for “print working directory” and is used for the purpose to show the current working directory.

## ‘Shutdown’ Command

This command is used for shutting down the system. The purpose of this command is to halt the current process and shut down the system immediately. To do this use the following code:

```
shutdown -h now
```

The next command is used to reboot the system, meaning that it will immediately shut down and restart the system. To do this use the command below:

```
shutdown -r now
```

## ‘Whereis’ Command

This command is used for showing the manual, source, and binary files for a command. Consider the command below:

```
whereis ls
```

This command will show the manual and binary files for the command ‘ls’. To see the list of commands which have been on your system previously, use the command ‘history’:

Above is the list of commands which have been run on my system. You can try on your system and observe the output.

## ‘Sudo’ Command

This stands for “superuser do”. It has the purpose of allowing a permitted user to execute commands as a “superuser”. This is usually defined in the ‘sudoers’ list. It has the importance of ensuring security by making sure that sensitive commands are only executed by the correct people. Another command, the ‘su’ command enables you to log in to the system as a superuser. The purpose of ‘sudo’ is to borrow privileges from the superuser. This explains the difference between these two commands, the ‘su’ and the ‘sudo’ commands. The ‘sudo’ command is normally used in commands which will change the system files, such as when updating or upgrading the OS. This shows how secure the command is compared to the ‘su’ command.

## ‘Mkdir’ Command

This command stands for “make directory”. It creates a new directory and names its path. If this path is already in existence, an error saying that the folder cannot be created will be outputted. Consider the figure shown below:

I have made a directory named “m”. Once I list the available directories after creating the directory, I find that it has been created. Notice that I have run the command as ‘sudo’. Without this, the command won’t run. This is for security purposes. Once you use the ‘sudo’ command for the first time, you will be prompted to provide the password for the superuser to do so. It is good to note that you can only create a directory inside a folder and you must have a “write permission” on that folder. Otherwise, you will be unable to do so.

## ‘Uname’ Command

It stands for “Unix name”. With this command, you can get detailed information about the operating system, kernel and the machine. Consider the figure below:

Information about the OS, the kernel, and the machine have been shown.

- Ubutnu - the name of the kernel of the machine
- SMP - the machine’s node name
