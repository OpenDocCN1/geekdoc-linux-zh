
## sed 选项

| Option | Action |
| :--- | :--- |
| a | Adds after the specified line |
| b | Adds before the specified line |
| d | Deletes the specified line |
| c | Replaces the specified line with the following |

The d and c options enable you to specify a range of lines. The c option replaces lines by first inserting the text before the lines and then deleting the lines. Because these commands are used to manipulate larger sections of text, they are usually used only in `sed` scripts.

You also can use `sed` to insert another file into the original file by using r, as in

```
/term/r IncludeFile
```

This would place the contents of IncludeFile immediately following the line containing term. You always must specify an address when using r.

## sort

The `sort` command is used to put lists in alphabetic or numeric order. In addition, it can merge one or more text files. The syntax for `sort` is

```
sort [options] [filelist]
```

`sort` takes its input from the files you specify or the standard input. Its output is sent to the standard output unless you use the `-o` option followed by a filename, which writes the output to that file.

The default action is to sort a file in alphabetic order. To sort a file in numeric order, use the -n option. This means that periods as well as plus and minus signs are interpreted in arithmetic order.

`sort` considers any leading blanks to be part of the field. Use the -b option to cause `sort` to ignore white space. Other options that you should know are listed in Table 8.2.

### Table 8.2. **sort Options and What They Do**

| Option | Action |
| :--- | :--- |
| -c | Checks to see that the file is sorted correctly |
| -d | Ignores all non-alphanumeric characters |
| -f | Considers all lowercase characters as uppercase |
| -i | Ignores non-printing characters |
| -m | Merges listed files |
| -r | Performs a reverse sort |

If you use `-c` with `sort`, it checks to see only whether the file is already sorted. If it is not, an error message is returned and `sort` exits. When using the `-m` with `sort`, the files to be merged must first be individually sorted.

`sort` does not change the original file. The results of using `sort` either go to the standard output or are saved to a file you designate. You can use `-o` with `sort` to designate the file to be used for the out file. This enables you to sort a file and save it to the same name.

## cut

The `cut` utility selects characters from the input and sends them to the standard output. It can be used to select tab delimited fields, too. Each character or field is referred to by the number of its position.

If the output of the `ls -l` command is

```
drwxrwxr-x    2 root     root       1024 Sep   9  07:41  graphics
-rw-r--r--     2 root     root       58575 May  20  13:40  install.txt
drwx------     2 haddenn  haddenn    1024 May   1  04:36  mail
-rw-r------     1 haddenn  haddenn    1633 May  16  09:07  mbox
-rw-rw-r--      1 haddenn  haddenn       40 May  20  22:22  mywords
drwx------     2 haddenn  haddenn    1024 May   8  15:18  nemail
-rw-rw-r--      0 Sep    4  16:53  script
drwxr-x---     2 haddenn  haddenn    1024 May   7  20:55  temp
```

and if you wanted to see only characters 2nd10 (permissions), you could issue the following command:

```
ls -l | cut -c2-10
```

The `-c` option lists the characters to be displayed, and the `|` (pipe) tells `cut` to get its input from the `ls -l` command. The output would be

```
rwxrwxr-x
rw-r--r--
drwx------
rw-r------
rw-rw-r--
drwx------
rw-rw-r--
drwxr-x---
```

You can use the `-d` option to define which character should be used as a delimiter when counting fields and the `-f` option to let cut know which fields to return. If you had a comma-delimited file and want to see all the names listed in the sixth field, you would type

```
cut -d, -f6 MyFile
```

cut does not change the original file, but instead outputs a section of that file based on character or field count. You can redirect the output to another file using the > pipe and specifying a filename.

## expand

The expand utility is used to change tabs to a specified number of spaces. The syntax for expand is

```
expand [options] file
```

By default, each tab is considered to be eight spaces. Use the `-t` to designate another value or provide a list of integers to define where each tab is to be placed. You can use the `-i` option to convert only tabs at the beginning of the line.

## fmt

The fmt utility is used to perform simple text editing. fmt’s main purpose is to try to make all the lines the same length by joining or splitting lines. Its syntax is

```
fmt [option] filename
```

fmt does not change the original file, but instead sends its results to the standard output. If you want to format a file so that each line is 70 characters long, issue the following command:

```
fmt -70 MyFile
```

This prints the file to the screen with each line approximately 70 characters long. If a line length is not specified, fmt defaults to 75 characters.

fmt attempts to split lines at the end of a sentence if possible. Also, it will not break lines after the first word or before the last word of a sentence.

You can prevent fmt from joining lines by using the -s option. If you want to have only one space between words and two spaces between sentences, use the -u option. If you want to format only specific lines, use the -p <prefix> option. This will cause fmt to format only those lines beginning with prefix.

Blank lines, indentations, and spacing are preserved. You can redirect the output to a file just like other commands.

## head

The head command lets you look at the beginning of one or more files. Use the -n option to designate how many lines to display. If the number of lines to display is not specified, head displays the first 10 lines. Its syntax is

```
head [option] filename(s)
```

You also can use c, b, or l after the number to designate characters, blocks, or lines. If nothing is designated after the number, 1 is assumed. To see the first 25 characters of a file you would type

```
head -25c FileName
```

In addition, you can use the -c option to print the designated beginning bytes. This can be in 512-byte blocks (b), 1KB blocks (k), or 1MB blocks (m).

If you pass a list of files to head to display, it will precede the display with the name of the file. To prevent this behavior use the -q option. If you always want to see the name of the file, even when displaying only one file, use the -v option.

## join

The join utility displays one line for each pair of input lines. The output is the join field followed by the remaining fields from file1 and then the remaining fields from file2. Its syntax is

```
join [options] file1 file2
```

Each of the two files to be joined should first be sorted alphabetically unless the -t option is used. By default, the join field is the first field in each line.

Table 8.3 lists the options that are used with the join command.

### Table 8.3 Options Used with the join Command

| Option | Action |
| :--- | :--- |
| -a | Also prints a line for each unpairable line |
| -e string | Replaces missing fields with string |
| -1, -j1 field | Joins on field of file1 |
| -2, -j2 field | Joins on field of file2 |
| -t character | Uses character as field separator |
| --help | Prints help and exits |
| --version | Prints version and exits |

## nl

The nl utility adds line numbers to a file and displays it to standard output. Its syntax is

```
nl [options] filename
```

nl divides its input into logical pages, each of which consists of a header, body, and footer. Any one of these sections can be empty and each can be numbered differently. Line numbering is reset to 1 at the beginning of each logical page. You can override this behavior by using the -p option or using the -v option to designate what number to start with on each page.

If multiple files are sent to nl, it sends its output as a single file to standard output, unless you specify otherwise. Line numbering is not reset at the beginning of each file.

The input page must contain a delimiter on a separate line to indicate the beginning of each logical page. The customary delimiters are

```
':'       start of header
'='       start of body
'\''      start of footer
```

You can change the delimiters by using the -i option. The line containing a section delimiter is displayed as a blank line.
