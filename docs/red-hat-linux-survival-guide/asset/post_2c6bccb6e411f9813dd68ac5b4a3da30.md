
## diff

Syntax: diff [-iqb] file1 file2

You use the diff command to determine differences between files and/or directories. The diff command is different from the cmp command in the way it compares the files. The diff command is used to report differences between two files, line by line. The cmp command reports differences between two files character by character, instead of line by line. As a result, it is more useful than diff for comparing binary files. By default, diff does not produce any output if the files are identical.

For text files, cmp is useful mainly when you want to know only whether two files are identical.

To illustrate the difference between considering changes character by character and considering them line by line, think of what happens if you add a single newline character to the beginning of a file. If you compare that file with an otherwise identical file that lacks the newline at the beginning, diff reports that a blank line has been added to the file, and cmp reports that the two files differ in almost every character.

The normal output format consists of one or more hunks of differences; each hunk shows one area where the files differ. Normal format hunks look like this:

```
change-command
< from-file-line
< from-file-line. . .
--
> to-file-line
> to-file-line. . .
```

There are three types of change commands. Each consists of a line number or comma-separated range of lines in the first file, a single character indicating the kind of change to make, and a line number or comma-separated range of lines in the second file. All line numbers are the original line numbers in each file. The types of change commands are:

- ‘l a r’ — Add the lines in range r of the second file after line l of the first file. For example, ‘8a12,15’ means append lines 12–15 of file 2 after line 8 of file 1; or, if changing file 2 into file 1, delete lines 12–15 of file 2.
- ‘f c t’ — Replace the lines in range f of the first file with lines in range t of the second file. This is like a combined add and delete but more compact. For example, ‘5,7c8,10’ means change lines 5–7 of file1 to read as lines 8–10 of file2; or, if changing file2 into file1, change lines 8–10 of file2 to read as lines 5–7 of file1.
- ‘r d l’ — Delete the lines in range r from the first file; line l is where they would have appeared in the second file had they not been deleted. For example, ‘5,7d3’ means delete lines 5–7 of file 1; or, if changing file 2 into file 1, append lines 5–7 of file 1 after line 3 of file 2.

For example, a.txt contains

```
a
b
c
d
e
```

and b.txt contains

```
c
d
e
f
g
```

The diff command produces the following output:

```
1,2d0
< a
< b
5a4,5
> f
> g
```

The diff command produces output that shows how the files are different and what you need to do for the files to be identical. First, notice how ‘c’ is the first common character between the two files. The first line reads 1,2d0. This is interpreted as deleting lines 1 and 2 of the first file, lines a and b. Next, the third line reads 5a4,5. The ‘a’ signifies append. If you append lines 4 through 5 of the second file to line 5 of the first file, the files are identical.

The diff command has some common options. The -i option ignores changes in case. diff considers upper- and lowercase characters equivalent. The -q option gives a summary of information. Simply put, the -q option reports if the files differ at all.

```
```
diff -q a.txt b.txt
Files a.txt and b.txt differ
```
```

The -b option ignores changes in whitespace. The phrase “the foo” is equivalent to “the foo” if you use the -b option.

## du

Syntax: du [-ask] filenames

This command summarizes disk usage. If you specify a directory, du reports the disk usage for that directory and any directories it contains. If you do not specify a filename or directory, du assumes the current directory. du -a breaks down the total and shows the size of each directory and file. The -s option will just print the total. Another useful option is the -k option. This option prints all file sizes in kilobytes. Here are some examples of the various options:

```
```
du -a
247    ./util-linux_2.9e-0.1.deb
130    ./libncurses4_4.2-2.deb
114    ./slang1_1.2.2-2.deb
492    .

du -s
492    .
```
```

## fgrep

The fgrep command is designed to be a fast-searching program (as opposed to grep). However, it can search only for exact characters, not for general specifications. The name fgrep stands for “fixed character grep.”

These days, computers and memory are so fast that there is rarely a need for fgrep.

## file

Syntax: file filename

The file command determines the file's type. If the file is not a regular file, this command identifies its file type. It identifies the file types directory, FIFO, block special, and character special as such. If the file is a regular file and the file is zero-length, this command identifies it as an empty file.

If the file appears to be a text file, file examines the first 512 bytes and tries to determine its programming language. If the file is an executable a.out, file prints the version stamp, provided it is greater than 0.

```
file main.c
main.c:          c program text
```

## find

Syntax: find [path] [-type fdl] [-name pattern] [-atime [+ -]number of days] [-exec command {} \;] [-empty]

The find command finds files and directories. For example:

```
find . -type d
```

The find command returns all subdirectory names under the current directory. The -type option is typically set to d (for directory) or f (for file) or l (for links). Following are a few of the things you can do with find:

- Find all text files (ending with .txt extension) in the current directory, including all its subdirectories:
  ```
  find . -type f -name "*.txt"
  ```
- Search all text files (ending with the .txt extension) in the current directory, including all its subdirectories for the keyword “magic,” and return their names (because -l is used with grep):
  ```
  find . -type f -name "*.txt" -exec grep -l 'magic' {} \;
  ```
- Find all GIF files that have been accessed in the past 24 hours (one day) and display their details using the ls -l command.
- Display all empty files in the current directory hierarchy.

```
find . -name "*.gif" -atime -1 -exec ls -l {} \;
```

```
find . -type f -empty
```

## grep

Syntax: grep [-viw] pattern file(s)

The grep command allows you to search for one or more files for particular character patterns. Every line of each file that contains the pattern is displayed at the terminal. The grep command is useful when you have lots of files and you want to find out which ones contain particular words or phrases.

Using the -v option, you can display the inverse of a pattern. Perhaps you want to select the lines in data.txt that do not contain the word “the,” you could use the following :

```
grep -vw 'the' data.txt
```

If you do not specify the -w option, any word containing “the” matches, such as “toge[the]r.” The -w option specifies that the pattern must be a whole word. Finally, the -i option ignores the difference between uppercase and lowercase letters when searching for the pattern.

Much of the flexibility of grep comes from the fact that you can specify not only exact characters but also a more general search pattern. To do this, use what you describe as “regular expressions.”

![](img/9eb7e89292d2f85707b4d49102c865b7_561_0.png)

See Chapter 9 for details on regular expression.

## head

**Syntax:** `head [-count | -n number] filename`

This command displays the first few lines of a file. By default, it displays the first ten lines of a file. However, you can use the preceding options to specify a different number of lines. The following example illustrates how to view the first two lines of the text file doc.txt.

```
head -2 doc.txt
# Outline of future projects
# Last modified: 02/02/99
```

## ln

**Syntax:** `ln [-s] sourcefile target`

ln creates two types of links: hard and soft. Think of a link as two names for the same file. After you create a link, you cannot distinguish it from the original file. You cannot remove a file that has hard links from the hard drive until you remove all links. You create hard links without the -s option.

```
ln ./www ./public_html
```

However, a hard link does have limitations. A hard link cannot link to another directory, and a hard link cannot link to a file on another file system. Using the -s option, you can create a soft link, which eliminates these restrictions. For example, the following command creates a soft link between the directory www on file system 2 and a newly created file public_html on file system 1:

```
ln -s /dev/fs02/jack/www /dev/fs01/foo/public_html
```

## locate

**Syntax:** `locate keyword`

The locate command finds the path of a particular file or command. locate finds an exact or substring match. For example:
