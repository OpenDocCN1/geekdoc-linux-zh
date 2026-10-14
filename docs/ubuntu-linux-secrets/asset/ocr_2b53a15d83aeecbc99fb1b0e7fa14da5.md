will also show different types of entries in different colors. The LS_COLORS environment variable controls this feature.

The basic list isn’t all that exciting. Fortunately, you can modify the way the ls command displays data. You can use parameters with a command to modify the default behavior of the program. Command-line parameters are preceded by a dash to distinguish them from data.

For example, if you don’t use color to distinguish the different types of entries, use the `-F` parameter with the `ls` command to add symbols to the file and directory names to easily distinguish files from directories. Using the `-F` parameter produces the following output:

```
```text
$ ls -F
4rich/ Documents/ Music/ Public/ store.zip Videos/
backup.zip Download/ myprog* store/ Templates/
Desktop/ Drivers/ Pictures/ store.2 test
$
```
```

The `-F` parameter now flags the directories with a forward slash to help identify them in the list. Similarly, it flags executable files (like the myprog file in the example) with an asterisk to help you easily identify the files that can be run on the system.

The output of the basic `ls` command can be misleading. It shows the files and directories contained in the current directory, but not necessarily all of them. Linux often uses hidden files to store configuration information. In Linux, hidden files have filenames that start with a period. These files don’t appear in the default `ls` list (thus, they are called hidden).

To display hidden files along with normal files and directories, use the `-a` parameter. Figure 19-5 shows an example of using the `-a` parameter with the `ls` command.

![](bbox=[0.177, 0.532, 0.716, 0.832])

**Figure 19-5:** Using the `-a` parameter with the `ls` command.