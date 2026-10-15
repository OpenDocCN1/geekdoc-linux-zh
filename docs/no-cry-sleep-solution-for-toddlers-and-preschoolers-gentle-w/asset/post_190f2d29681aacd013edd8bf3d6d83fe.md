
```text
$ ls -F
weather reports/ letters/
```

The ls command also takes as an argument any directory name or directory pathname. This enables you to list the files in any directory without first having to change to that directory. In the next example, the ls command takes as its argument the name of a directory, reports. Then the ls command is executed again, only this time the absolute pathname of reports is used.

```text
$ ls reports
monday tuesday
$ ls /home/chris/reports
monday tuesday
$
```

## Moving Through Directories

The cd command takes as its argument the name of the directory to which you want to change. The name of the directory can be the name of a subdirectory in your working directory or the full pathname of any directory on the system. If you want to change back to your home directory, you only need to enter the cd command by itself, without a filename argument.

```text
$ cd props
$ pwd
/home/dylan/props
```

## Referencing the Parent Directory

A directory always has a parent (except, of course, for the root). For example, in the preceding listing, the parent of thankyou is the letters directory. When a directory is created, two entries are made: one represented with a dot (.), and the other represented by double dots (..). The dot represents the pathname of the directory, and the double dots represent the pathname of its parent directory. Double dots, used as an argument in a command, reference a parent directory. The single dot references the directory itself.

You can use the single dot to reference your working directory, instead of using its pathname. For example, to copy a file to the working directory retaining the same name, the dot can be used in place of the working directory's pathname. In this sense, the dot is another name for the working directory. In the next example, the user copies the weather file from the chris directory to the reports directory. The reports directory is the working directory and can be represented with the single dot.

```text
$ cd reports
$ cp /home/chris/weather .
```

The .. symbol is often used to reference files in the parent directory. In the next example, the cat command displays the weather file in the parent directory. The pathname for the file is the .. symbol followed by a slash and the filename.

```text
$ cat ../weather
raining and warm
```

TIP: You can use the cd command with the .. symbol to step back through successive parent directories of the directory tree from a lower directory.

## File and Directory Operations: find, cp, mv, rm, and ln

As you create more and more files, you may want to back them up, change their names, erase some of them, or even give them added names. Linux provides you with several file commands that enable you to search for files, copy files, rename files, or remove files (see Table 10-5 later in this chapter). If you have a large number of files, you can also search them to locate a specific one. The commands are shortened forms of full words, consisting of only two characters. The cp command stands for "copy" and copies a file, mv stands for "move" and renames or moves a file, rm stands for "remove" and erases a file, and ln stands for "link" and adds another name for a file, often used as a shortcut to the original. One exception to the two-character rule is the find command, which performs searches of your filenames to find a file.

## Searching Directories: find

Once you have a large number of files in many different directories, you may need to search them to locate a specific file, or files, of a certain type. The find command enables you to perform such a search. The find command takes as its arguments directory names followed by several possible options that specify the type of search and the criteria for the search. find then searches within the directories listed and their subdirectories for files that meet these criteria. The find command can search for a file by name, type, owner, and even the time of the last update.

```text
$ find directory-list -option criteria
```

The -name option has as its criteria a pattern and instructs find to search for the filename that matches that pattern. To search for a file by name, you use the find command with the directory name followed by the -name option and the name of the file.

```text
$ find directory-list -name filename
```

The find command also has options that merely perform actions, such as outputting the results of a search. If you want find to display the filenames it has found, you simply include the -print option on the command line along with any other options. The -print option instructs find to output to the standard output the names of all the files it locates (you can also use the -ls option to list files in the long format). In the next example, the user searches for all the files in the reports directory with the name monday. Once located, the file, with its relative pathname, is printed.

```text
$ find reports -name monday -print
reports/monday
```

The find command prints out the filenames using the directory name specified in the directory list. If you specify an absolute pathname, the absolute pathname of the found files will be output. If you specify a relative pathname, only the relative pathname is output. In the
