
## Exercises

- **8.1 [2]** You can use the `-U` option to get `ls` to output a directory’s entries without sorting them. Even so, after `ls -laU >filelist`, the entry for *filelist* in the output file gives length zero. What could be the reason?

- **8.2 [2]** Compare the output of the commands `ls /tmp` and `ls /tmp >ls-tmp.txt` (where, in the second case, we consider the content of the *ls-tmp.txt* to be the output). Do you notice something? If so, how could you explain the phenomenon?

![](img/44bdd771e9c9b1353d2401c2892b2459_105_0.png)

- **8.3 [2]** Why isn’t it possible to replace a file by a new version in one step, for example using `grep xyz file >file`?

- **8.4 [1]** And what is wrong with `cat foo >foo`, assuming a non-empty file foo?

- **8.5 [2]** In the shell, how would you output an error message such that it goes to standard error output?

### 8.1.3 Command Pipelines

Output redirection is frequently used to store the result of a program in order to continue processing it with a different command. However, this type of intermediate storage is not only quite tedious, but you must also remember to get rid of the intermediate files once they are no longer required. Therefore, Linux offers a way of linking commands directly via pipes: A program’s output automatically becomes another program’s input.

This direct connection of several commands into a pipeline is done using the `|` operator. Instead of first redirecting the output of `ls -laR` to a file and then looking at that file using `less`, you can do the same thing in one step without an intermediate file:

```
$ ls -laR | less
total 7
drwxr-xr-x   12 joe   users        1024 Aug 26 18:55   ./
drwxr-xr-x    5 root  root         1024 Aug 13 12:52   ../
drwxr-xr-x    3 joe   users        1024 Aug 20 12:30   photos/
-rw-r--r--    1 joe   users          449 Sep  6 13:50   filelist
-rw-r--r--    1 joe   users        15811 Aug 13 12:33   pingu.gif
-rw-r--r--    1 joe   users        14373 Aug 13 12:33   hobby.txt
-rw-r--r--    2 joe   users         3316 Aug 20 15:14   chemistry.txt
```

These command pipelines can be almost any length. Besides, the final result can be redirected to a file:

```
$ cut -d: -f1 /etc/passwd | sort | pr -2 >userlst
```

This command pipeline takes all user names from the first comma-separated column of /etc/passwd file, sorts them alphabetically and writes them to the userlst file in two columns. The commands used here will be described in the remainder of this chapter.

Sometimes it is helpful to store the data stream inside a command pipeline at a certain point, for example because the intermediate result at that stage is useful for different tasks. The `tee` command copies the data stream and sends one copy to standard output and another copy to a file. The command name should be obvious if you know anything about plumbing (see Figure 8.2).

The `tee` command with no options creates the specified file or overwrites it if it exists; with `-a` ("append"), the output can be appended to an existing file.

```
$ ls -laF | tee list | less
total 7
drwxr-xr-x 12 joe users 1024 Aug 26 18:55 ./
drwxr-xr-x 5 root users 1024 Aug 13 12:52 ../
drwxr-xr-x 3 joe users 1024 Aug 20 12:30 photos/
-rw-r-- 1 joe users 449 Sep 6 13:50 content
-rw-r-- 1 joe users 15811 Aug 13 12:33 pingu.gif
-rw-r-- 1 joe users 14373 Aug 13 12:33 hobby.txt
-rw-r-- 2 joe users 3316 Aug 20 15:14 chemistry.txt
```

In this example the content of the current directory is written both to the *list* file and the screen. (The *list* file does not show up in the `ls` output because it is only created afterwards by `tee`.)

## Exercises

- **8.6 [!]** How would you write the same intermediate result to several files at the same time?

### 8.2 Filter Commands

One of the basic ideas of Unix—and, consequently, Linux—is the “toolkit principle”. The system comes with a great number of system programs, each of which performs a (conceptually) simple task. These programs can be used as “building blocks” to construct other programs, to save the authors of those programs from having to develop the requisite functions themselves. For example, not every program contains its own sorting routines, but many programs avail themselves of the `sort` command provided by Linux. This modular structure has several advantages:

- It makes life easier for programmers, who do not need to develop (or incorporate) new sorting routines all the time.

- If `sort` receives a big fix or performance improvement, all programs using `sort` benefit from it, too—and in most cases do not even need to be changed.

Tools that take their input from standard input and write their output to standard output are called “filter commands” or “filters” for short. Without input redirection, a filter will read its input from the keyboard. To finish off keyboard input for such a program, you must enter the key sequence `Ctrl` + `d`, which is interpreted as “end of file” by the terminal driver.

> Note that the last applies to keyboard input *only*. Files on the disk may of course contain the `Ctrl` + `d` character (ASCII 4), without the system believing that the file ended at that point. This as opposed to a certain very popular operating system, which traditionally has a somewhat quaint notion of the meaning of the Control-Z (ASCII 26) character even in text files . . .

Many “normal” commands, such as the aforementioned `grep`, operate like filters if you do not specify input file names for them to work on.

In the remainder of the chapter you will become familiar with a selection of the most important such commands. Some commands have crept in that are not technically genuine filter commands, but all of them form important building blocks for pipelines.

### Table 8.2: Options for cat (selection)

| Option | Result |
| :--- | :--- |
| -b | (engl. number non-blank lines) Numbers all non-blank lines in the output, starting at 1. |
| -E | (engl. end-of-line) Displays a $ at the end of each line (useful to detect otherwise invisible space characters). |
| -n | (engl. number) Numbers all lines in the output, starting at 1. |
| -s | (engl. squeeze) Replaces sequences of empty lines by a single empty line. |
| -T | (engl. tabs) Displays tab characters as “^I”. |
| -v | (engl. visible) Makes control characters c visible as “^c”, characters a with character codes greater than 127 as “M-a”. |
| -A | (engl. show all) Same as -vET. |

### 8.3 Reading and Writing Files

#### 8.3.1 Outputting and Concatenating Text Files—cat

The cat (“concatenate”) command is really intended to join several files named on the command line into one. If you pass just a single file name, the content of that file will be written to standard output. If you do not pass a file name at all, cat reads its standard input—this may seem useless, but cat offers options to number lines, make line ends and special characters visible or compress runs of blank lines into one (Table 8.2).

![](img/44bdd771e9c9b1353d2401c2892b2459_107_0.png)

It goes without saying that only text files lead to sensible screen output with cat. If you apply the command to other types of files (such as the binary file /bin/cat), it is more than probable—on a text terminal at least—that the shell prompt will consist of unreadable characters once the output is done. In this case you can restore the normal character set by (blindly) typing reset. If you redirect cat output to a file this is of course not a problem.

![](img/44bdd771e9c9b1353d2401c2892b2459_107_1.png)

The “Useless Use of cat Award” goes to people using cat where it is extraneous. In most cases, commands do accept filenames and don’t just read their standard input, so cat is not required to pass a single file to them on standard input. A command like “cat data.txt | grep foo” is unnecessary if you can just as well write “grep foo data.txt”. Even if grep could only read its standard input, “grep foo < data.txt” would be shorter and would not involve an additional cat process.

### Exercises

- **8.7 [2]** How can you check whether a directory contains files with “weird” names (e. g., ones with spaces at the end or invisible control characters in the middle)?

#### 8.3.2 Beginning and End—head and tail

Sometimes you are only interested in part of a file: The first few lines to check whether it is the right file, or, in particular with log files, the last few entries. The head and tail commands deliver exactly that—by default, the first ten and the last ten lines of every file passed as an argument, respectively (or else as usual the first or last ten lines of their standard input). The -n option lets you specify a different number of lines: “head -n 20” returns the first 20 lines of its standard input, “tail -n 5 data.txt” the last 5 lines of file data.txt.
