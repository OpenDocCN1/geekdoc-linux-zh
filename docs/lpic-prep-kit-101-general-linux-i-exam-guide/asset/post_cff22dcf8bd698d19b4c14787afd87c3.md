
## sed

The syntax for `sed` is:

```bash
sed [-n] [-e command] [-f command_file] filename [>newfile]
```

We will look at each of the options in this section.

Chapter 4 discussed using `sed` to search for text in a file; however, it can do much more than that. `sed` commands can be entered at the command line, as in the following:

```bash
sed s/term1/term2/ FileName
```

More commonly, however, you will use a file containing the commands in conjunction with `sed`, as in the following:

```bash
sed -f ConfFile FileName
```

where `ConfFile` contains the command:

```bash
s/term1/term2
```

One of the simplest `sed` commands is substitution. In the previous example, `sed` replaces the first occurrence of the first term in each line with the second term. If `term1` occurs more than once in a line, only the first occurrence is replaced. To replace every occurrence of `term1` with `term2`, you would use `g` at the end, as in:

```bash
s/term1/term2/g
```

The `g` tells `sed` to perform a global search and replace. You can limit the replacement to a specific occurrence by specifying which occurrence you want to act upon, as in the following:

```bash
s/3/term1/term2/
```

This would replace only the third occurrence of `term1` with `term2`. You also can designate specific lines to process by referring to the line by number:

```bash
1s/term1/term2/
1,3s/term1/term2/
```

The first example will process only line 1, whereas the second processes lines 1–3. Be sure to note the placement of the numbers. If the number is first, it denotes line number, but if it is after the `s` (command) then it denotes the number of its occurrence. The following is an example of this:

```bash
s/2/term1/term2/
```

This would replace the second occurrence of `term1` with `term2`.

You also can use the `$` instead of a line number to specify the last line. If you do not know the line number, you can use patterns instead to locate the line. The command:

```bash
/StartWord/,/StopWord/s/term1/term2/
```

processes the file starting with the first line containing `StartWord` and ending with the first line containing `StopWord`. After `StopWord` has been found, `sed` looks for another occurrence of `StartWord`. If it is found, `sed` will process all commands on all lines until `StopWord` is found again. This process continues until the end of the file is reached.

If you want to process all lines except those specified, follow the address with `!`. You also can use a `\n` to specify a newline character within the pattern. However, it will not match a newline at the end of a pattern.

By default, `sed` prints each line of the file after it has finished processing the line. However, if you want to see only the lines that have been changed, use `p`. This causes `sed` to print only each line that has been changed. Of course, `sed` will print the same line for each change it made. So if it makes three changes to one line, it will print the same line three times (once after making each change).

```bash
s/term1/term2/gp
```

If you want to do the same thing from the command line, use the `-n` option with `sed`, as in:

```bash
sed -n s/term1/term2/gp FileName
```

Both of the previous two examples would change every instance of `term1` to `term2` and print the changed line(s) to standard output. If you want to use both `-n` and `-f`, be sure that `-n` precedes the `-f`. You also could use `-nf` or `-fn`.

If you want to redirect the changed lines to a file, you can use the `w` option (if you are saving your commands to a script file). The following is an example of this:

```bash
s/term1/term2/w OutFile
```

When typing the commands on the command line, you can redirect the output to a file by using a pipe, such as `>`.

In addition, you can use `sed` to add, delete, or change lines of a text file. Table 8.1 shows the commands you can use when you want to work on an entire line.

### Table 8.1 Use These sed Options to Add, Delete, or Replace Text

| Option | Action |
| :--- | :--- |
| a | Adds after the specified line |
| i | Inserts before the specified line |
| d | Deletes the specified line |
| c | Replaces the specified line with the following |

The `a` and `c` options enable you to specify a range of lines. The `c` option replaces lines by first inserting the text before the lines and then deleting the lines. Because these commands are used to manipulate larger sections of text, they are usually used only in `sed` scripts.

You also can use `sed` to insert another file into the original file by using `r`, as in:

```bash
/term/r IncludeFile
```

This would place the contents of `IncludeFile` immediately following the line containing `term`. You always must specify an address when using `r`.

## sort

The `sort` command is used to put lists in alphabetic or numeric order. In addition, it can merge one or more text files. The syntax for `sort` is:

```bash
sort [options] [filelist]
```

`sort` takes its input from the files you specify or the standard input. Its output is sent to the standard output unless you use the `-o` option followed by a filename, which writes the output to that file.

The default action is to sort a file in alphabetic order. To sort a file in numeric order, use the `-n` option. This means that periods as well as plus and minus signs are interpreted in arithmetic order.

`sort` considers any leading blanks to be part of the field. Use the `-b` option to cause `sort` to ignore white space. Other options that you should know are listed in Table 8.2.

### Table 8.2 sort Options and What They Do

| Option | Action |
| :--- | :--- |
| -c | Checks to see that the file is sorted correctly |
| -d | Ignores all non-alphanumeric characters |
| -f | Considers all lowercase characters as uppercase |
| -i | Ignores non-printing characters |
| -m | Merges listed files |
| -r | Performs a reverse sort |

If you use `-c` with `sort`, it checks to see only whether the file is already sorted. If it is not, an error message is returned and `sort` exits. When using the `-m` with `sort`, the files to be merged must first be individually sorted.

`sort` does not change the original file. The results of using `sort` either go to the standard output or are saved to a file you designate. You can use `-o` with `sort` to designate the file to be used for the output file. This enables you to sort a file and save it to the same name.

## cut

The `cut` utility selects characters from the input and sends them to the standard output. It can be used to select tab-delimited fields, too. Each character or field is referred to by the number of its position.

If the output of the `ls -l` command is:

```bash
drwxwxr-x   2 root     root     1024 Sep  9 07:41 graphics
-rw-r--r--   1 root     root     58575 May 20 13:40 install.txt
drwX-------   2 haddan   haddan     1024 May  1 04:36 mail
-rw-------   1 haddan   hadden     1633 May 16 09:07 mbox
-rw-rw-r--   1 haddan   haddan       40 May 20 22:22 mywords
drwX-------   2 haddan   haddan     1024 May  8 15:18 nsmail
-rw-rw-r--   1 haddan   hadden        0 Sep  4 10:53 script
drwxr-xr-x   2 haddan   haddan     1024 May  7 20:55 temp
```

and if you wanted to see only characters 2 through 10 (permissions), you could issue the following command:

```bash
ls -l | cut -c2-10
```

The `-c` option lists the characters to be displayed, and the `|` (pipe) tells `cut` to get its input from the `ls -l` command. The output would be:

```bash
rwxrwxr-x
rw-r--r--
rwx-------
rw---------
rw-rw-r--
rwx-------
rw-rw-r--
rwxr-xr-x
```

You can use the `-d` option to define which character should be used as a delimiter when counting fields and the `-f` option to let `cut` know which fields to return. If you had a comma-delimited file and want to see all the names listed in the sixth field, you would type:

```bash
cut -d, -f6 MyFile
```

`cut` does not change the original file, but instead outputs a section of that file based on character or field count. You can redirect the output to another file using the `>` pipe and specifying a filename.

## expand

The `expand` utility is used to change tabs to a specified number of spaces. The syntax for `expand` is:

```bash
expand [options] file
```

By default, each tab is considered to be eight spaces. Use the `-t` to designate another value or provide a list of integers to define where each tab is to be placed. You can use the `-i` option to convert only tabs at the beginning of the line.

## fmt

The `fmt` utility is used to perform simple text editing. `fmt`'s main purpose is to try to make all the lines the same length by joining or splitting lines. Its syntax is:

```bash
fmt [option] filename
```

`fmt` does not change the original file, but instead sends its results to the standard output. If you want to format a file so that each line is 70 characters long, issue the following command:

```bash
fmt -70 MyFile
```

This prints the file to the screen with each line approximately 70 characters long. If a line length is not specified, `fmt` defaults to 75 characters.

`fmt` attempts to split lines at the end of a sentence if possible. Also, it will not break lines after the first word or before the last word of a sentence.
