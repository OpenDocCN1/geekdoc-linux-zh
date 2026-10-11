You can also make copies of files in the same directory. To make a copy of the host file called hosts2 in the current directory, type the following command:

```
```
[root@server1 root]# cp hosts hosts2
[root@server1 root]# ls -F
current/  Desktop/  hosts  hosts2  myprogram*  myscript2*  proj_files/  [root@server1 root]#_ 
```
```

One notable difference between the mv and cp commands, aside from their purpose, is that they work on directories differently. The mv command simply renames a directory, whereas the cp command creates a whole new copy of the directory and its contents. To copy a directory full of files in Linux, you must tell the cp command that the copy will be **recursive** (involve files and subdirectories too) by using the -r option. The following example demonstrates copying the proj_files directory and all of its contents to the /home/user1 directory without and with the -r option:

```
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
[root@server1 root]#_ 
```
```

When copying or moving files, if the target is a file that exists, the mv and cp commands warn the user that the target file will be overwritten and ask whether to continue. This is not a feature of the command as normally invoked, but is a feature of the default configuration in Red Hat Linux because the BASH shell in Red Hat Linux contains aliases to the cp and mv commands.

> **NOTE**
> 
> Aliases are special variables in memory that point to commands; they are fully discussed in Chapter 8, "Working with the BASH Shell."

When you type mv, you are really running the mv command with the -i option, which interactively prompts the user to choose whether to overwrite the existing file if the target file already exists when the command is executed; this is called **interactive mode**. Similarly, when you