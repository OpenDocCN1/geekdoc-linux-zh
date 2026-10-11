it follows the tree branch by branch until the path to file or desired directory stands completed. Take the example of a directory on your system in which most of the system's programs are installed.

```
[gha@localhost ~]$ cd /usr/downloads
[gha@localhost downloads]$ pwd
/usr/downloads
[gha@localhost downloads]$ ls
```

This command will list the files in that directory. The ls command is one of the  widely  used  commands  in  a  Linux  operating  system.  With  this command's help, you can see the contents of a directory and determine the number of files and directory attributes. As you have seen, you can enter the ls command to see the list of files and subdirectories that are contained inside a current working directory.

```
[gha@localhost ~]$ ls /usr
bin games include lib lib64 libexec local sbin share src tmp
```

You can list the home directory of the user and the /usr by using the following command.

```
[gha@localhost ~]$ ls ~ /usr
/root:
b ench.py hello.c

/usr:
bin games include lib lib64 libexec local sbin share src tmp
```

You can add -l to the ls command to change the format of the display and reveal more details. By adding -l to the same ls command, you can change the output to a longer format.

# ## Options and Arguments Commands

Most Linux commands are made up of one character preceded by a dash. However, some are longer, with two dashes followed by a word, such as those in the GNU support project. Some commands even allow two or more shorter options to be tagged to one another. In the example you see below, we will give the ls command two options – the first (l) will reduce the long output, while the second (t) sorts the results by modification time.

Let us see the result of the -l command.

```
[gha@localhost ~]$ ls -l
total 8
```