# # Answers to Explorational Exercises

+   1. Identify the hardware architecture and Linux kernel version being used on your computer in an easy-to-read output format.
+   
+   Run `man uname`, read through the “Description” section, and identify the command arguments that will display only the exact results you want. Note how `-v` will give you the kernel version and `-i` will provide hardware platform.

```
```
$ man uname
$ uname -v
$ uname -i
```
```

+   2. Print out the last twenty lines of the dynamic history database and the `.bash_history` file to compare them.

```
```
$ history 20
$ tail -n 20 .bash_history
```
```

+   3. Use the `apropos` tool to identify the `man` page where you will find the command you will need to display the size of an attached physical block device in bytes rather than megabytes or gigabytes.
+   
+   One way, would be to run `apropos` with the string `block`, read through the results, note that `lsblk` lists block devices (and would, therefore, be the most likely tool for our needs), run `man lsblk`, scroll through the “Description” section and note that `-b` will display a device size in bytes. Finally, run `lsblk -b` to see what comes out.

```
```
$ apropos block
$ man lsblk
$ lsblk -b
```
```