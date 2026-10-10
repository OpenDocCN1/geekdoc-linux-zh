
## Viewing File Information

  It's not uncommon to look through a directory and see files that you're not familiar with, or perhaps even forget why they're there. Linux has a couple of handy commands that can help you out with that.

  The file command can provide basic information about the file type of a specified file, as shown in Listing 3.31.

### Listing 3.31: Using the file command

```bash
$ file mytest
mytest: Bourne-Again shell script, ASCII text executable
$
```

  The output from the file command shows that Linux recognizes the mytest file as a shell script file, in ASCII text format, and as an executable file.

  If you'd like to see information about when a file was created, modified, or last accessed, use the stat command, as shown in Listing 3.32.

### Listing 3.32: Using the stat command

```bash
$ stat mytest
  File: mytest
  Size: 1016 Blocks: 8 IO Block: 4096 regular file
Device: 805h/2053d Inode: 1054186 Links: 1
Access: (0764/-rwxrw-r--)
Uid: ( 1000/ rich)
Gid: ( 1000/ rich)
Access: 2021-11-06 09:18:23.856584608 -0500
Modify: 2021-10-31 11:25:22.048406517 -0500
Change: 2021-10-31 11:25:22.048406517 -0500
Birth: -
$
```

  As seen in Listing 3.32, the output from the stat command provides basic information about the file, such as the file's name, size, inode number, and the physical device it's stored on. But it also provides some harder-to-find information, such as the last time the file was accessed and modified.

## Exploring File Differences

  A handy command to explore text file differences is the diff command. It allows you to make comparisons between two files, line by line. The basic syntax for the command is:

```bash
diff [OPTION]... FILES
```

  With the `diff` utility you can perform a variety of comparisons. In addition, you can format the output to make the results easier for viewing. Table 3.7 shows a few commonly used options.

**TABLE 3.7 The `diff` command's commonly used options**

| Short | Long | Description |
| :--- | :--- | :--- |
| `-e` | `--ed` | Create an ed script, which can be used to make the first file compared the same as the second file compared. |
| `-q` | `--brief` | If files are different, issue a simple message expressing this. |
| `-r` | `--recursive` | Compare any subdirectories within the original directory tree, and consecutively compare their contents and the subdirectories as well (recursive). |
| `-s` | `--report-identical-files` | If files are the same, issue a simple message expressing this. |
| `-Wn` | `--width n` | Display a width maximum of *n* characters for output. |
| `-y` | `--side-by-side` | Display output in two columns. |

  To simply see if differences exist between two text files, you enter the `diff` command with the `-q` switch followed by the filenames. An example is shown in Listing 3.33. To help you see the exact file differences, the `pr` command is employed first to display both files side by side in a column format.

### Listing 3.33: Quickly comparing files using the `diff` `-q` command

```bash
$ pr -mtw 35 numbers.txt random.txt
   42
   2A
   2A              Flat Land
   52              Schroddinger's Cat
   0010 1010       0010 1010
   *               0000 0010
   $
$ diff -q numbers.txt random.txt
Files numbers.txt and random.txt differ
$
```

  For just a quick view of differences between files, modify the `diff` command's output to display the files in a column format. Use the `-y` (or `--side-by-side`) option along with the `-w` (or `--width`) switch for an easier display to read, as shown in Listing 3.34. The pipe symbol (|) designates the second file's lines, which are different from those in the first file.

### Listing 3.34: Using the `diff` command for quick file differences

```bash
$ diff -yW 35 numbers.txt random.txt
42            42
2A            | Flat Land
52            | Schrodinger's
0010 1010     0010 1010
*             | 0000 0010
$
```

  The `diff` utility provides more than just differences; it also denotes what needs to be appended, changed, or deleted to make the first file identical to the second. To see the exact differences between the files and any needed modifications, remove the `-q` switch. An example is shown in Listing 3.35.

### Listing 3.35: Employing the `diff` command

```bash
$ diff numbers.txt random.txt
2,3c2,3
< 2A
< 52
---
> Flat Land
> Schrodinger's Cat
5c5
< *
---
> 0000 0010
$
```

  The `diff` command's output can be a little confusing. In Listing 3.35, the first output line displays `2,3c2,3`. This output tells you that to make the first file, `numbers.txt`, just like the second file, `random.txt`, you will need to change the `numbers.txt` file's lines 2 through 3 to match the `random.txt` file's lines 2 through 3. The output's next six lines show each file's text content that does not match, separated by a dashed line. Next, the `5c5` designates that line 5 in `numbers.txt` needs to be changed to match line 5 in the `random.txt` file.

![](img/c0a399aca0d18f8822d714ad0a173123_139_0.png)

> **NOTE**
>
> The `diff` command is rather powerful. Not only can it tell you the differences between text file lines, but it can also create a script for you to use. The script allows you to modify the first compared text file and turn it into a twin of the second text file. This function is demonstrated in the next chapter.

  The letter `c` in the `diff` utility's output denotes that changes are needed. You may also see an `a` for any needed additions or `d` for any needed deletions.

## Using Simple Pinpoint Commands

  Commands that quickly locate (pinpoint) files are very useful. They allow you to determine if a particular utility is installed on your system, locate a needed configuration file, find helpful documentation, and so on. The beauty of the commands covered here is that they are simple to use.

  The `which` command shows you the full path name of a shell command passed as an argument. Listing 3.36 shows examples of using this utility.

### Listing 3.36: Using the `which` command

```bash
$ which diff
/usr/bin/diff
$
$ which shutdown
/usr/sbin/shutdown
$
$ which line
/usr/bin/which: no line in (/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/Christine/.local/bin:/home/Christine/bin)
$
$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:
/home/Christine/.local/bin:/home/Christine/bin
$
```

  In the first example in Listing 3.36, the `which` command is used to find the `diff` command's program location. The command displays the full path name of `/usr/bin/diff`. The `shutdown` utility is located in a `sbin` directory. However, the `line` program is not installed on this system, and the `which` utility displays all the directories it searched to find the program. It uses the `PATH` environment variable, whose contents are also displayed in Listing 3.36, to determine which directories to search.

![](img/c0a399aca0d18f8822d714ad0a173123_140_0.png)

> **NOTE**
>
> Environment variables are configuration settings that modify your process's environment. When you type in a command [program] name, the `PATH` variable sets the directories Linux will search for the program binary. It is also used by other commands, such as the `which` utility. Note that directory names are separated by a colon (`:`) in the `PATH` list.

  The `which` command is also handy for quickly determining if a command is using an alias. Listing 3.37 shows an example of this.

### Listing 3.37: Using the `which` command to see a command alias

```bash
$ which ls
alias ls='ls --color=auto'
        /usr/bin/ls

$ unalias ls

$ which ls
/usr/bin/ls
$
```

  When the `which` utility is used on the `ls` command in Listing 3.37, it shows that cur-

  Another simple pinpoint command is the `whereis` utility. This utility allows you to not

### Listing 3.38: Employing the `whereis` command

```bash
$ whereis diff
diff: /usr/bin/diff /usr/share/man/man1/diff.1.gz
/usr/share/man/man1p/diff.1p.gz

$ whereis line
line:
$
```

  The first command issued in Listing 3.38 searches for program binaries, source code files,

  A handy and simple utility to use in finding files is the `locate` program. This utility

```bash
locate [OPTION]... PATTERN...
```

  Notice in the syntax that the `locate` utility uses a pattern list to find files. Thus, you can
