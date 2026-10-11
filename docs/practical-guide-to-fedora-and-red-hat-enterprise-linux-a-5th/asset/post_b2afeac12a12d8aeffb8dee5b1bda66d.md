
# diff: COMPARES TWO FILES

```
$ diff -u colors.1 colors.2
--- colors.1 Tue Nov 25 15:45:32 2008
+++ colors.2 Tue Nov 25 15:24:46 2008
@@ -1,6 +1,5 @@
 red
+blue
 green
 yellow
-pink
-purple
 orange
```

Figure 5-8 **diff** displaying the unified output format

The diff (difference) utility compares two files and displays a list of the differences between them. This utility does not change either file, so it is useful when you want to compare two versions of a letter or a report or two versions of the source code for a program.

The diff utility with the **-u** (unified output format) option first displays two lines indicating which of the files you are comparing will be denoted by a plus sign (**+**) and which by a minus sign (**-**). In Figure 5-8, a minus sign indicates the **colors.1** file; a plus sign indicates the **colors.2** file.

The **diff -u** command breaks long, multiline text into *hunks*. Each hunk is preceded by a line starting and ending with two at signs (**@@**). This hunk identifier indicates the starting line number and the number of lines from each file for this hunk. In Figure 5-8, the hunk covers the section of the **colors.1** file (indicated by a minus sign) from the first line through the sixth line. The **+1,5** then indicates that the hunk covers **colors.2** from the first line through the fifth line.

Following these header lines, **diff -u** displays each line of text with a leading minus sign, a leading plus sign, or nothing. A leading minus sign indicates that the line occurs only in the file denoted by the minus sign. A leading plus sign indicates that the line comes from the file denoted by the plus sign. A line that begins with neither a plus sign nor a minus sign occurs in both files in the same location. Refer to the diff info page for more information.

# file: TESTS THE CONTENTS OF A FILE

You can use the **file** utility to learn about the contents of any file on a Linux system without having to open and examine the file yourself. In the following example, **file** reports that **letter_e.bz2** contains data that was compressed by the **bzip2** utility (page 162):

```
$ file letter_e.bz2
   letter_e.bz2: bzip2 compressed data, block size = 900k
```

Next file reports on two more files:

```
$ file memo zach.jpg
memo:    ASCII text
zach.jpg: JPEG image data, ... resolution (DPI), 72 x 72
```

Refer to the file man page for more information.

# | (PIPE): COMMUNICATES BETWEEN PROCESSES

Because pipes are integral to the functioning of a Linux system, they are introduced here for use in examples. Pipes are covered in detail beginning on page 238.

A *process* is the execution of a command by Linux (page 314). Communication between processes is one of the hallmarks of both UNIX and Linux. A *pipe* (written as a vertical bar, |, on the command line and appearing as a solid or broken vertical line on keyboards) provides the simplest form of this kind of communication. Simply put, a pipe takes the output of one utility and sends that output as input to another utility. Using UNIX/Linux terminology, a pipe takes standard output of one process and redirects it to become standard input of another process. (For more information refer to “Standard Input and Standard Output” on page 230.) Most of what a process displays on the screen is sent to standard output. If you do not redirect it, this output appears on the screen. Using a pipe, you can redirect the output so that it becomes instead standard input of another utility. For example, a utility such as head can take its input from a file whose name you specify on the command line following the word head, or it can take its input from standard input. Thus, you can give the command shown in Figure 5–5 on page 155 as follows:

```
$ cat months | head
Jan
Feb
Mar
Apr
May
Jun
Jul
Aug
Sep
Oct
```

The next command displays the number of files in a directory. The wc (word count) utility with the -w option displays the number of words in its standard input or in a file you specify on the command line:

```
$ ls | wc -w
14
```

You can use a pipe to send output of a program to the printer:

```
$ tail months | lpr
```

![](img/f28adb66a7398a382f0505e0ba74a872_199_0.png)

**Figure 5-9** echo copies the command line (but not the word echo) to the screen

# FOUR MORE UTILITIES

The echo and date utilities are two of the most frequently used members of the large collection of Linux utilities. The script utility records part of a session in a file, and unix2dos makes a copy of a text file that can be read on either a Windows or a Macintosh machine.

# ECHO: DISPLAYS TEXT

The echo utility copies anything you put on the command line after echo to the screen. Some examples appear in Figure 5-9. The last example shows what the shell does with an unquoted asterisk (*) on the command line: It expands the asterisk into a list of filenames in the directory.

The echo utility is a good tool for learning about the shell and other Linux programs. Some examples on page 244 use echo to illustrate how special characters, such as the asterisk, work. Throughout Chapters 7, 9, and 27, echo helps explain how shell variables work and how you can send messages from shell scripts to the screen. Refer to the echo info page for more information.

# DATE: DISPLAYS THE TIME AND DATE

The date utility displays the current date and time:

![](img/f28adb66a7398a382f0505e0ba74a872_199_1.png)

The following example shows how you can choose the format and select the contents of the output of date:

![](img/f28adb66a7398a382f0505e0ba74a872_199_2.png)

Refer to the date info page for more information.

## script: Records a Shell Session

The `script` utility records all or part of a login session, including your input and the system's responses. This utility is useful only from character-based devices, such as a terminal or a terminal emulator. It does capture a session with `vim`; however, because `vim` uses control characters to position the cursor and display different typefaces, such as bold, the output will be difficult to read and may not be useful. When you `cat` a file that has captured a `vim` session, the session quickly passes before your eyes.

By default `script` captures the session in a file named `typescript`. To use a different filename, follow the `script` command with a SPACE and the new filename. To append to a file, use the `-a` option after `script` but before the filename; otherwise `script` overwrites an existing file. Following is a session being recorded by `script`:

```
$ script
  Script started, file is typescript
$ date
Sun Jan 20 10:28:56 PST 2008
$ who am i
alex    pts/4        Jan  8 22:15
$ apropos vim
vim (1)                - Vi I'mproved, a programmers text editor
vimdiff (1)            - edit two or three versions of a file with ...
vimtutor (1)           - the vim tutor
$ exit
  Script done, file is typescript
$
```

Use the `exit` command to terminate a script session. You can then view the file you created with `cat`, `less`, `more`, or an editor. Following is the file that was created by the preceding `script` command:

```
$ cat typescript
  Script started on Sun Jan 20 10:28:44 2008
$ date
Sun Jan 20 10:28:56 PST 2008
$ who am i
alex    pts/4        Jan  8 22:15
$ apropos vim
vim (1)                - Vi I'mproved, a programmers text editor
vimdiff (1)            - edit two or three versions of a file with ...
vimtutor (1)           - the vim tutor
$ exit
  Script done on Sun Jan 20 10:29:58 2008
$
```

If you will be editing the file with `vim`, `emacs`, or another editor, you can use `dos2unix` to eliminate from the `typescript` file the `^M` characters that appear at the ends of the lines. Refer to the `script` man page for more information.

# unix2dos: CONVERTS LINUX AND MACINTOSH FILES TO WINDOWS FORMAT

If you want to share a text file that you created on a Linux system with someone on a Windows or Macintosh system, you need to convert the file before the person on the other system can read it easily. The `unix2dos` utility converts a Linux text file so that it can be read on a Windows or Macintosh system. Give the following command to convert a file named `memo.txt` (created with a text editor) to a DOS-format file:

```
$ unix2dos memo.txt
```

Without any options `unix2dos` overwrites the original file. You can now email the file as an attachment to someone on a Windows or Macintosh system.

You can use the `dos2unix` utility to convert Windows or Macintosh files so they can be read on a Linux system:

```
$ dos2unix memo.txt
```

See the `unix2dos` and `dos2unix` man pages for more information.

You can also use `tr` to change a Windows or Macintosh text file into a Linux text file. In the following example, the `-d` option causes `tr` to remove RETURNs (represented by `\r`) as it makes a copy of the file:

```
$ cat memo | tr -d '\r' > memo.txt
```

The greater than (>) symbol redirects the standard output of `tr` to the file named `memo.txt`. For more information refer to "Redirecting Standard Output" on page 232. Converting a file the other way without using `unix2dos` is not as easy.

# COMPRESSING AND ARCHIVING FILES

Large files use a lot of disk space and take longer than smaller files to transfer from one system to another over a network. If you do not need to look at the contents of a large file very often, you may want to save it on a CD, DVD, or another medium and remove it from the hard disk. If you have a continuing need for the file, retrieving a copy from a CD may be inconvenient. To reduce the amount of disk space you use without removing the file entirely, you can compress the file without losing any of the information it holds. Similarly a single archive of several files packed into a larger file is easier to manipulate, upload, download, and email than multiple files. You may frequently download compressed, archived files from the Internet. The utilities described in this section compress and decompress files and pack and unpack archives.
