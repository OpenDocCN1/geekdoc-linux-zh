![](bbox=[0.18, 0.12, 0.92, 0.45])

Figure 1.2 The main Linux directory tree structure.

```
$ cd /
```

thus giving the pathname of the required destination directory as a parameter. In order to obtain a list of the names of the files and directories that are contained in the current directory you use the ls command. Using the ls command on the root directory of a typical Linux system gives an output such as:

```
$ ls
bin dev home mnt sbin var
boot dos lib proc tmp vmlinuz
cdrom etc lost+found root usr
```

The most important branches of the Linux directory hierarchy are shown in Figure 1.2. You should use the pwd, cd and ls commands to explore this directory hierarchy on your own machine. If at any point you want to get back to your home directory you can obviously use the cd command and give the appropriate pathname as a command line parameter. But, if you just enter the cd command without specifying a destination directory this is a short cut that will also take you straight back to your home directory. The main branches of the Linux directory hierarchy, as shown in Figure 1.2, contain files which have the general functions given in Table 1.1.

# 1.4 The Password File

Under Linux, the password file is one of the central data files in the system. It ties together quite a lot of what you have seen so far. The password file contains a list of all the users who have login names; it specifies where the home directories are for