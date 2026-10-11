
## od

The `od` utility is used to dump the contents of a file and is useful for viewing files with non-printing characters such as binaries. By default, its output is in 2-byte octal numbers. Its syntax is:

```
od [options] file
```

The output from a file might look like the following:

```
0000000 066101 064160 043141 066151 066145 071551 065164 064506
0000020 025254 064554 072163 061412 072141 027064 074164 005164
0000040 066054 031171 062012 074541 005163 064544 072143 063012
0000060 066151 071545 066412 073571 064550 064143 071412 063157
0000100 062164 074541 000012
0000105
```

In this example, the first column is the offset of each line, and then each two bytes are represented by a three-digit octal number.

## paste

The `paste` utility joins the corresponding lines from the named files and sends the output to the display. The output separates the joined lines with a tab. Its syntax is:

```
paste [options] filename
```

Use the `-d` option to have the joined lines separated by another character, rather than separating them with a tab.

You also can use the `-s` option. This causes `paste` to output one file followed by a newline character and then output the next file. With this option, the lines are not joined together but the files are pasted one after the other.

The `paste` utility often is used in conjunction with `cut` to rearrange columns. First, you would use `cut` to get each column in a separate file, and then use `paste` to join them in the order you want.

## pr

The `pr` utility is used to break files into pages. Its syntax is:

```
pr [options] file
```

The `pr` utility is most frequently used to send a file to a printer. The standard page length is 66 lines but can be changed with the `-l` option. You can use the `-f` option to generate a form feed at the end of each page, instead of filling the page with newline characters.

You also can have the output formatted in columns by using the `-columns` option to specify the number of columns to use. Use the `-m` option to print the listed files in parallel—each in a separate column.

The file name is printed as the header unless you use the `-h headertext` option. This will cause the `headertext` to be printed centered at the top of the page.

To prevent `pr` from changing the layout of your file, use the `-t` option. This will suppress printing of headers and footers. The `-T` option does the same as `-t`, but it also removes any form feeds contained in the file.

## split

The `split` utility is used to divide files into equally sized pieces. Its syntax is:

```
split [options] [input_file] [output_file]
```

The default size of each output file is 1,000 lines. You can change this by using the `-l` option to define how many lines to put in each output file.

`output_file` gives the syntax for prefixing each piece of the original file. If none is given, then `split` uses `x`. This is added to the filenames, which are `aa`, `ab`, `ac`, and so on, as in:

```
split FileName dog
```

If `FileName` is 3,780 lines long, `split` would divide the file into four files, which would be called `adog`, `bdog`, `cdog`, and `ddog`. If no output file is given, the files would be `aax`, `abx`, `acx`, and `adx`.

Files also can be divided by the number of bytes in each output file by using the option `-b`. `split` multiplies the number by 512KB. You can use `-k`, which multiplies by 1,024, or use `-m`, which multiplies by 1,048,576. For example:

```
split -b 2 FileName
```

would divide `FileName` into 1024-byte blocks.

## tac

`tac` displays a file line-by-line, starting with the last line and ending with the first one. Think of `tac` as being a reverse `cat`—just like its spelling. Its syntax is:

```
tac filename
```

If multiple files are passed to `tac`, each one is separated by a newline. You can specify the separator to use by using the `-s` option. By default, the separator appears after the file. Use the `-b` option to place the separator before the file.

## tail

`tail` displays the last lines of a file and is especially helpful in reading long log files in which the newest messages are at the end. Its syntax is:

```
tail [options] file
```

You can designate how many lines to display by using the `-n` option. If the number of lines is not specified, `tail` defaults to 10. `tail` also enables you to designate where to start displaying the file by using the `+n` option, which starts displaying a file at line number `n` and then displays to the end of the file.

You can tell `tail` which item to count instead of which lines. Use `b` for blocks and `c` for characters. To show the last 30 characters of a file, you would type:

```
tail -30c filename
```

You can display by blocks, too. Use `b` for 512-byte blocks, `k` for 1KB blocks, and `m` for 1MB blocks.

The `-f` option keeps a file open and displays each new line that is added. This is helpful when you are troubleshooting and want to watch the error logs. Press Ctrl+C to end the display.

When you pass multiple files to `tail`, it heads each display with the filename. To suppress this, use the `-q` option.

## tr

The `tr` utility can be used to replace one string with another or to delete a string in a file. `tr` sends its output to standard display. Its syntax is:

```
tr [options] string1 [string2]
```

The most common use of `tr` is to perform a search and replace operation in which you specify the string to search for and the string to use as a replacement—for example, changing lowercase to uppercase. To change the word `monday` to `Monday` in the file `FileName`, type the following:

```
cat FileName | tr 'monday' 'Monday'
```

If you specify only one string and use the `-d` option, `tr` deletes the specified string. You can use the `-s` option with only one string and `tr` will replace multiple occurrences with only one. For example, if you type:

```
cat myfile | tr -s 'a-z'
```

`tr` changes the word `Hallo*een*` to `\* Halloween \*` when displaying `myfile` to your screen. `tr` also can be used to encrypt your file using the rotate 13 method. This replaces the first letter of the alphabet with the 13th, the second with the 14th, and so on. An example is:

```
tr '[A-M]\[N-Z]\[a-m]\[n-z]' '[N-Z]\[A-M]\[n-z]\[a-m]'
```

As you can see, you can use ranges of characters enclosed in square brackets as part of your string. Notice that single quotes are needed because of the special characters.

## wc

The `wc` utility will tell you the number of words, lines, or characters in a file. Its syntax is:

```
wc [options] {filename(s)}
```

If you specify multiple files, the number of words, lines, and characters will be displayed for each file followed by the sum total of words, lines, and characters.

You can use the `-o` option to display only the number of characters, `-w` to display the number of words, and `-1` to display the number of lines.

So, if you called `wc` with `days` and `mywhich` listed as filenames, the output would be:

```
6    8     69 days
5    17     181 mywhich
11   25     169 total
```

To display the number of lines in `days` without showing the file's name, you could type:

```
wc -1 < days
```

## Input and Output

Almost every command can get information passed to it by way of standard input (*stdin*). This usually is via the terminal, such as when you type a command. However, input can also come from a file.

In addition, each command has two types of output: standard output (*stdout*) and standard error (*stderr*). *stdout* is the results of the command, whereas *stderr* is where any error messages are sent. By default, both of these are directed to the display, but either or both of these streams can be redirected to a file.

The shell manages how standard input and standard output are handled. By default, your shell directs standard output and standard error from the command to the device file, which is associated with your terminal and causes it to appear on your display. In the same manner, the shell directs standard input from your terminal, or keyboard, to the command.

Consider the command `cat`. If you type only `cat <enter>`, the standard input comes from the keyboard and the standard output goes to the display. In other words, what you type appears on your display.

After you press Ctrl-d, you signal to the `cat` command that the input is finished. `cat` then returns control to the shell and your prompt returns. If, however, you type `cat MyFile`, the input is the file `MyFile` and the output again goes to your display.

### Redirection and Pipes

*Redirection* is the method of altering the source for standard input or where to send output. The `>` can be used to define where to send standard output and `<` can be used to redirect standard input.

What if you type `cat file1 > file2`? This is an example of using redirection. The input comes from `file1`, the output goes to `file2`, and nothing appears on your display.

This affects only standard output. If any errors had occurred, those messages would have been sent to your display and not to `file2`. To redirect both the *stdout* and *stderr*, use the greater than sign (`>`) followed by the ampersand (`&`), as in the following:

```
cat file1 file2 >& error-msg
```

This example will send both the standard output and any error messages to the file called `error-msg`. If you are using the `bash` shell, you also can use:

```
cat file1 file2 &> error-msg
```

to do the same thing.

The shell assigns the number 0 to the standard input, the number 1 to the standard output, and the number 2 to the standard error output. You can use these numbers when using redirection. To save the error messages and discard the regular output, type:

```
cat file1 file2 2> error-msg
```

If you wanted to redirect both standard output and standard error, you could type:

```
cat file1 file2 1> MyFile 2> error-msg
```

When redirecting output to a file, any existing file with the same name will be overwritten. If you do not want to overwrite the existing file, use `>>` to append the new information to the existing file.

Sometimes you might not want to save the output of a command, whether it be standard output or standard error. This can be accomplished by redirecting the output to the `/dev/null` device. The output then disappears without a trace, as in the following:

```
cat file1 file2 >& /dev/null
```
