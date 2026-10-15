
Many utilities and filters use patterns to locate and select specific text in your file. Sometimes, you may need to use patterns in a more flexible and powerful way, searching for several different variations on a given pattern. You can include a set of special characters in your pattern to enable a flexible search. A pattern that contains such special characters is called a regular expression. Regular expressions can be used in most filters and utilities that employ pattern searches such as sed, awk, grep, and egrep.

> Tip Although many of the special characters used for regular expressions are similar to the shell file expansion characters, they are used in a different way. Shell file expansion characters operate on filenames. Regular expressions search text.

You can save the output of a filter in a file or send it to a printer. To do so, you need to use redirection or pipes. To save the output of a filter to a file, you redirect it to a file using the redirection operation, >. To send output to the printer, you pipe the output to the lpr utility, which then prints it. In the next command, the cat command pipes its output to the lpr command, which then prints it.

```
$ cat complist | lpr
```

All filters accept input from the standard input. In fact, the output of one filter can be piped as the input for another filter. Many filters also accept input directly from files, however. Such filters can take filenames as their arguments and read data directly from those files.

## Searching Files: grep

The grep and egrep filters search the contents of files for a pattern. They then inform you of what file the pattern was found in and print the lines in which it occurred in each file. Preceding each line is the name of the file in which the line is located. grep can search for only one pattern, whereas fgrep can search for more than one pattern at a time.

The grep filter takes two types of arguments. The first argument is the pattern to be searched for; the second argument is a list of filenames, which are the files to be searched. You enter the filenames on the command line after the pattern. You can also use special characters, such as the asterisk, to generate a file list.

```
$ grep pattern filenames-list
```

If you want to include more than one word in the pattern search, you enclose the words within single quotation marks. This is to quote the spaces between the words in the pattern. Otherwise, the shell would interpret the space as a delimiter or argument on the command line, and grep would try to interpret words in the pattern as part of the file list. In the next example, grep searches for the pattern “text file”:

```
$ grep 'text file' preface
A text file in Unix
text files, changing or
```

If you use more than one file in the file list, grep will output the name of the file before the matching line. In the next example, two files, preface and intro, are searched for the pattern "data". Before each occurrence, the filename is output.

```
$ grep data preface intro
preface: data in the file.
intro: new data
```

As mentioned earlier, you can also use shell file expansion characters to generate a list of files to be searched. In the next example, the asterisk file expansion character is used to generate a list of all files in your directory. This is a simple way of searching all of a directory's files for a pattern.

```
$ grep data *
```

The special characters are often useful for searching a selected set of files. For example, if you want to search all your C program source code files for a particular pattern, you can specify the set of source code files with *.c. Suppose you have an unintended infinite loop in your program and you need to locate all instances of iterations. The next example searches only those files with a .c extension for the pattern "while" and displays the lines of code that perform iterations.

```
$ grep while *.c
```

## Regular Expressions

Regular expressions enable you to match possible variations on a pattern, as well as patterns located at different points in the text. You can search for patterns in your text that have different ending or beginning letters, or you can match text at the beginning or end of a line. The regular expression special characters are the circumflex, dollar sign, asterisk, period, and brackets: ^, $, *, ., []. The circumflex and dollar sign match on the beginning and end of a line. The asterisk matches repeated characters, the period matches single characters, and the brackets match on classes of characters. See Table 8-8 for a listing of the regular expression special characters.

| Character | Match | Operation |
| --- | --- | --- |
| ^ | Start of a line | References the beginning of a line |
| $ | End of a line | References the end of a line |
| . | Any character | Matches on any one possible character in a pattern |
| * | Repeated characters | Matches on repeated characters in a pattern |
| [] | Classes | Matches on classes of characters (a set of characters) in the pattern |

TABLE 8-8 Regular Expression Special Characters
