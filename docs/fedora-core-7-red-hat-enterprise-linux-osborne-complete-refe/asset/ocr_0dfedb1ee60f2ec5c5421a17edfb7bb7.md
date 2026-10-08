# ## Searching Files: grep

The **grep** and **fgrep** filters search the contents of files for a pattern. They then inform you of what file the pattern was found in and print the lines in which it occurred in each file. Preceding each line is the name of the file in which the line is located. The **grep** command can search for only one pattern, whereas **fgrep** can search for more than one pattern at a time.

The **grep** filter takes two types of arguments. The first argument is the pattern to be searched for; the second argument is a list of filenames, which are the files to be searched. You enter the filenames on the command line after the pattern. You can also use special characters, such as the asterisk, to generate a file list.

```
$ grep pattern filenames-list
```

If you want to include more than one word in the pattern search, you enclose the words within single quotation marks. This is to quote the spaces between the words in the pattern. Otherwise, the shell would interpret the space as a delimiter or argument on the command line, and **grep** would try to interpret words in the pattern as part of the file list. In the next example, **grep** searches for the pattern “text file”:

```
$ grep 'text_file' preface
A text_file in Linux
text_files, changing or
```

If you use more than one file in the file list, **grep** will output the name of the file before the matching line. In the next example, two files, **preface** and **intro**, are searched for the pattern “data”. Before each occurrence, the filename is output.

```
$ grep data preface intro
preface: data in the file.
intro: new data
```

As mentioned earlier, you can also use shell file expansion characters to generate a list of files to be searched. In the next example, the asterisk file expansion character is used to generate a list of all files in your directory. This is a simple way of searching all of a directory’s files for a pattern.

```
$ grep data *
```

The special characters are often useful for searching a selected set of files. For example, if you want to search all your C program source code files for a particular pattern, you can specify the set of source code files with * .c. Suppose you have an unintended infinite loop in your program and you need to locate all instances of iterations. The next example searches only those files with a .c extension for the pattern “while” and displays the lines of code that perform iterations:

```
$ grep while * .c
```

# ## Regular Expressions

Regular expressions enable you to match possible variations on a pattern, as well as patterns located at different points in the text. You can search for patterns in your text that have different ending or beginning letters, or you can match text at the beginning or end of a line.