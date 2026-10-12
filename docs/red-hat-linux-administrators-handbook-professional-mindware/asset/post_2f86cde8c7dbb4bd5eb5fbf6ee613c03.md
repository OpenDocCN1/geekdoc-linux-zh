
## grep

**Syntax:** `grep [options] pattern [file...]`

The grep command allows you to search for one or more files for particular character patterns. Every line of each file that contains the pattern is displayed at the terminal. The grep command is useful when you have lots of files and want to find out which ones contain particular words or phrases.

Using the `-v` option, you can display the inverse of a pattern. Perhaps you want to select the lines in `data.txt` that do *not* contain the word `the`:

```
grep -vw 'the' data.txt
```

If the `-w` option was not specified, then any word containing the would match, such as toge[the]r. The `-w` option specifies that the pattern must be a whole word. The `-i` option ignores the difference between upper- and lowercase letters when searching for the pattern.

## head

**Syntax:** `head [-count | -n number] filename`

The head command displays the first few lines of a file. By default, the first ten lines of a file are displayed. However, you can use the preceding options to specify a different number of lines. The following example illustrates how to view the first two lines of the text file doc.txt:

```
head -2 doc.txt
# Outline of future projects
# Last modified:  02/02/01
```

## ln

**Syntax:** `ln [-s] sourcefile target`

The ln command creates two types of links: hard and soft. A link can best be thought of as another name for a file. After a link is created, it is indistinguishable from the original file. A file that has hard links to it will not be removed from the hard disk until all links are removed. Hard links are created without the `-s` option:

```
ln ./www ./public_html
```

However, a hard link does have limitations: it can link neither to another directory nor to a file on another file system. But, by using the `-s` option, you can create a soft link, which eliminates these restrictions:

```
ln -s /dev/fs02/jack/www /dev/fs01/foo/public_html
```

The preceding creates a soft link between the directory www on file system 2 and a newly created file public_html on file system 1.

## locate

**Syntax:** `locate keyword`

The locate command finds the path of a particular file or command. locate will find an exact or substring match. For example:

```
locate foo
/usr/lib/texmf/tex/latex/misc/footnpag.sty
/usr/share/automake/footer.am
/usr/share/games/fortunes/food
/usr/share/games/fortunes/food.dat
/usr/share/gimp/patterns/moonfoot.pat
```

The output that locate produces will contain the keyword foo in the absolute path or will not have any output at all.

## ls

**Syntax:** `ls [-laRl] file or directory`

The ls command allows you to list files (and subdirectories) in a directory. It is one of the most commonly used programs. When used with the `-1` option, the ls command displays only the file and directory names in the current directory. When the `-l` option is used, a long listing containing file/directory permission information, size, modification date, and so on is displayed. Using the `-a` option enables you to view all files and directories (including the ones that have a leading period in their names) within the current directory. The `-R` option allows the command to recursively display contents of the subdirectories (if any).

## mkdir

**Syntax:** `mkdir directory ...`

To make a directory, use the `mkdir` command. Only two restrictions apply when choosing a directory name: filenames can be up to 255 characters long, and directory names can contain any character except `\`

The following example creates three directories, all in the current directory, provided write permission is granted in the current directory:

```
mkdir dir1 dir2 dir3
```

## mv

**Syntax:** `mv [-i-f] sourcefile targetfile`

Use the `mv` command to move or rename directories and files. The command will perform a move or a rename, depending on whether or not the `targetfile` is an existing directory. To illustrate, suppose you want to rename an existing directory currently called `foo` to the new name of `foobar`:

```
mv foo foobar
```

Because `foobar` does not already exist as a directory, `foo` will be renamed to `foobar`. If the following command is issued

```
mv doc.txt foobar
```

and `foobar` is an existing directory, a move will be performed. The file `doc.txt` will now reside in the directory `foobar`.

The `-f` option removes existing destination files and never prompts the user. The `-i` option prompts the user whether to overwrite each destination file that already exists. If the response does not begin with `y` or `Y`, the file is skipped.

## pico

**Syntax:** `pico [filename]`

`pico` is a full-screen text editor that is very user-friendly and highly suitable for users who have migrated to Linux from an MS Windows or DOS environment.

## pwd

**Syntax:** `pwd`

The pwd command prints the current working directory. The directories displayed will be the absolute path. None of the directories displayed will be hard or soft symbolic links.

## rm

**Syntax:** `rm [-rif] directory/file`

To remove a file or directory, use the `rm` command. Here are some examples:

```
rm doc.txt
rm ./doc.txt
rm /tmp/foo.txt
```

To remove multiple files with `rm`, use wildcards or type each file individually. For example,

```
rm doc1.txt doc2.txt doc3.txt
```

is equivalent to

```
rm doc[1-3].txt
```

`rm` is a powerful command that can cause chaos if used incorrectly. For instance, suppose you have stored on your computer a thesis that you've worked hard on for the last six months. You decide to `rm` all of your docs, mistakenly thinking that you are in another directory from the one in which your thesis is stored. After finding out a backup file does not exist (and you are no longer in denial), you wonder whether you could have prevented this mistake somehow.

The `rm` command's `-i` option enables `rm` to be interactive. It tells `rm` to ask your permission before removing each file. For example, if you enter

```
rm -i *.doc
rm: remove thesis.doc (yes/no)? n
```

the `-i` option gives you a parachute, asking you whether to pull the cord (answer no, the default) or suffer the consequences (answer yes). The `-f` option is completely the opposite. The `-f` (force) option tells rm to remove all the files you specify regardless of the file permissions. Use the `-f` option only when you are 100 percent sure you are removing the correct file(s).

To remove a directory and all of the files and directories within it, use the `-r` option. `rm -r` will remove an entire subtree:

```
rm -r documents
```

If you are not sure of what you are doing, combine the `-r` option with the `-i` option:

```
rm -ri documents
```

The preceding example asks for your permission before removing each file and directory.

## sort

**Syntax:** `sort [-rndu] [-o outfile] [infile/sortedfile]`

The obvious task this command performs is to sort. However, sort also merges files. sort reads files that contain previously sorted data and merges them into one large sorted file.

To save the sorted results, use the `-o` option: `sort -o sorted.txt a.txt` will save the sorted a.txt file in sorted.txt. To use sort to merge existing sorted files into one file and save the output in sorted.txt, use the following:

```
sort -o sorted.txt a.txt b.txt c.txt
```

The `-r` option for this command reverses the sort order. Therefore, a file that contains the letters of the alphabet on a line will be sorted from z to a if the `-r` option is used.

The `-d` option sorts files based on dictionary order. sort considers only letters, numerals, and spaces and ignores other characters.

The `-u` option looks for identical lines and suppresses all but one. Therefore, sort produces only unique lines.

## stat

**Syntax:** `stat file`

This program displays various statistics on a file or directory. For example,

```
stat foo.txt
```

displays the following output:

```
File: "foo.txt"
  Size: 4447232      Filetype: Regular File
  Mode: (0644/-rw-r----)  Uid: (  0/root)   Gid: (  0/root)

Device: 3,0   Inode: 16332     Links: 1

Access: Mon Mar  1 21:39:43 2000 (00000.02:32:30)
Modify: Mon Mar  1 22:14:26 2000 (00000.01:57:47)
Change: Mon Mar  1 22:14:26 2000 (00000.01:57:47)
```

As you can see, this output displays the file access, modification, change date, size, owner and group information, permission mode, and so on.

## strings

**Syntax:** `strings filename`

The strings command prints character sequences that are at least four characters long. This utility is used mainly to describe the contents of non-text files.

## tail

**Syntax:** `tail [-count | -n number] filename`

The tail command displays the end of a file. By default, tail displays the last 10 lines of a file. To display the last 50 lines of the file doc.txt, issue this command:

```
tail -50 doc.txt
```
