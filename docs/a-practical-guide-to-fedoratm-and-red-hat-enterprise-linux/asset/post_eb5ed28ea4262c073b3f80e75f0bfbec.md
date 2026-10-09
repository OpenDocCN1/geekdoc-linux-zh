
The **-#** *n* option prints *n* copies of each file. Depending on which shell you are using, you might need to escape the **#** by preceding it with a backslash to keep the shell from interpreting it as a special character. The following command prints two copies of **memo** on the printer named **laser**.

```bash
$ lpr -Plaser -#2 memo
```

## RELATED UTILITIES

- **lpq** The **lpq** utility displays information about jobs in a print queue. When called without arguments, **lpq** lists all print jobs queued for the default printer. Use the **-P** *printer* option with **lpq** to look at other print queues—even those for printers connected to remote systems. With the **-l** (lowercase “el”) option, **lpq** displays more information about each job. If you specify a username as an argument, **lpq** displays only the print jobs belonging to that user.

The next example shows a number of print jobs queued for the default printer. Max owns all the jobs, and the first one is being printed (it is active). Jobs 635 and 639 were created by sending input to **lpr’s** standard input; job 638 was created by giving **ncut.icn** as an argument to the **lpr** command. The last column gives the size of each print job.

```text
$ lpq
deskjet is ready and printing
Rank  Owner  Job  Files  Total Size
active  max    635  (stdin)  38128 bytes
1st     max    638  ncut.icn  3587 bytes
2nd     max    639  (stdin)  3960 bytes
```

- **lprm** One item displayed by **lpq** is the job number for each print job in the queue. To remove a job from the print queue, give the job number as an argument to **lprm**.

Unless you are working with **root** privileges, you can remove only your own jobs. Even a user working with **root** privileges might not be able to remove a job from a queue for a remote printer. Without an argument, **lprm** removes the active printer job (i.e., the job that is now printing) from the queue, if you own that job. The next command removes job 638 from the default print queue:

```bash
$ lprm 638
```

## MV: RENAMES OR MOVES A FILE

The **mv** (move) utility, which renames or moves one or more files, has three forms. The first renames a single file with a new filename that you supply. The second renames one or more files so that they appear in a specified directory. The third renames a directory. The **mv** utility physically moves (copies and deletes) the original file if it is not possible to rename it (that is, if you move the file from one filesystem to another). See page 224 for a description of the related **cp** (copy) utility.

**mv can destroy a file**

Just as **cp** can destroy a file, so can **mv**. Also like **cp**, **mv** has a **-i** (interactive) option. See the caution box on page 224.

### ARGUMENTS

The first form of *mv* takes two arguments: the pathname of the ordinary file you want to rename and/or move and the new pathname of the file. The first of the following commands renames **memo** in the working directory to **memo.copy**. The second command moves **memo** from the working directory to the **copies** directory and renames it **memo.130808**.

```bash
$ mv memo memo.copy
$ mv memo copies/memo.130808
```

The second form of *mv* takes two or more arguments; all but the last are the pathnames of ordinary files you want to move and the last specifies the new parent directory for the files. The files you move will have the same simple filenames as each of the original files but new absolute pathnames. The following command moves **memo1**, **memo2**, and **memo3** from the working directory and **memoX** from the */tmp* directory to the (existing) **memo.copy** subdirectory of the working directory.

```bash
$ mv memo1 memo2 memo3 /tmp/memoX memo.copy
```

The third form of *mv* takes two arguments: the pathname of an existing directory that you want to move and/or rename, and the new pathname for the directory, which does not exist. (If the directory exists, the command is the second form of *mv* and moves the file to the directory without changing the file’s name.) The first of the following commands renames the **memo.copy** directory in the working directory **memo.old**. The second moves the **feb** subdirectory of **memos** to the directory named **archive** and renames it **1302**.

```bash
$ mv memo.copy memo.old
$ mv memos/feb archive/1302
```

### OPTIONS

The *-f* (--force) option causes *mv* **not** to prompt you if a move would overwrite an existing file that you do not have write permission for. You must have write permission for the directory holding the existing file.

The *-i* (--interactive) option prompts for confirmation if *mv* would overwrite a file. If your response begins with a **y** or **Y**, *mv* overwrites the file; otherwise, *mv* does not move the file. The following example copies all files named **memoX** followed by a single character to the **memo.copy** directory, prompting you if it would overwrite a file.

```bash
$ mv -i memo? memo.copy
mv: overwrite 'memo.copy/memo3'? y
```

If *mv* would not overwrite a file, it does not prompt even with this option.

The *-v* (--verbose) option lists files as they are moved.

```bash
$ mv -v memo? memo.copy
'memo1' -> 'memo.copy/memo1'
'memo2' -> 'memo.copy/memo2'
'memo3' -> 'memo_copy/memo3'
'memo4' -> 'memo_copy/memo4'
'memo5' -> 'memo_copy/memo5'
```

## LEXT sort: SORTS AND/OR MERGES FILES

The `sort` utility sorts and/or merges one or more text files. It orders the output using the collating sequence specified by the LC_COLLATE locale variable (page 368). This section explains how to use `sort` to order a file by lines. See the `sort` man page for information on sorting on fields.

Without the -o option, `sort` sends its output to standard output. This utility sorts and merges files unless you use the -m (merge only) or -c (check only) option.

### ARGUMENTS

The arguments are the pathnames of one or more ordinary files that contain the text to be sorted. Without arguments, `sort` takes its input from standard input. The following example shows `sort` processing a file named days that holds the days of the week, one per line, in calendar order. The `sort` utility outputs the contents of the file in alphabetical order.

```bash
$ sort days
Friday
Monday
Saturday
Sunday
Thursday
Tuesday
Wednesday
```

The next example merges and sorts the days and months files.

```bash
$ sort days months
April
August
December
February
Friday
...
```

### OPTIONS

- **Check** The -c (-check) option checks whether the file is properly sorted. The `sort` utility does not display anything if everything is in order. It displays a message if the file is not in sorted order and returns an exit status of 1. The following example shows that the fourth line of days, which contains **Thursday**, is the first line of the file that is not in alphabetical order.

```bash
$ sort -c days
sort: days:4: disorder: Thursday
```

- **Dictionary** The -d (-dictionary-order) option ignores all characters that are not alphanumeric characters or blanks. For example, `sort` does not consider punctuation with this option. The *LC_CTYPE* locale variable (page 368) affects the outcome when you specify this option.

- The *-i* (`--ignore-case`) option considers all lowercase letters to be uppercase letters.

- The *-I* (`--ignore-nonprinting`) option ignores nonprinting characters. This option is overridden by the *-d* option. The *LC_CTYPE* locale variable (page 368) affects the outcome when you specify this option.

- The *-m* (`--merge`) option assumes that each of the multiple input files is in sorted order and merges them without verifying they are sorted.

- The *-n* (`--numeric-sort`) option orders in arithmetic sequence; it does not order lines in the machine collating sequence. With this option, minus signs and decimal points take on their arithmetic meaning. The following example shows the difference between sorting a numeric file without using the *-n* option and with it.

```bash
$ sort num
09.0
10.5
1.24
-5
9

$ sort -n num
-5
1.24
09.0
9
10.5
```

- The *-o* *filename* (`--output=filename`) option sends output to *filename* instead of standard output; *filename* can be the same as one of the names of the files that *sort* is sorting. The following command sends the output to the *days.sort* file.

```bash
$ sort -o days.sort days
```

- The *-r* (`--reverse`) option reverses the sense of the sort (e.g., z precedes a). The following examples order *days* in reverse alphabetic order and *num* in reverse arithmetic order.

```bash
$ sort -r days
Wednesday
Tuesday
Thursday
Sunday
Saturday
Monday
Friday

$ sort -rn num
10.5
9
09.0
1.24
-5
```
