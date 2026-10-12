# General File and Directory Commands

In this section, you will learn about file- and directory-specific commands that you're likely to use on a daily basis.

# cat

**Syntax:** `cat file [>|>] [destination_file]`

The cat command displays the contents of a file to the standard output, enabling you to examine the contents of a file. The argument you pass to cat is the file you wish to view. To view the total content of a file called name, you'd use the following command (the command is shown with the sample output below it):

```
cat name
Kiwee
Joe
Ricardo
Charmaine
```

cat can also merge existing multiple files into one:

```
cat name1 name2 name3 > allnames
```

This example combines the files name1, name2, and name3 to produce the final file allnames. You establish the order of the merge by the order in which you enter the files at the command line.

Using cat, you can append a file to another file. For example, if you forgot to add the file name4 in the previous command, you can add it to the allnames file by executing the following command:

```
cat name4 >> allnames
```

# chmod

**Syntax:** `chmod [-R] permission_mode file_or_directory`