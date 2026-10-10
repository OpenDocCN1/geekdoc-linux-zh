
In Listing 4.6, notice that the file has different numbers listed in an unsorted order. The second example attempts to numerically order the file, using the `sort` command with no options. This yields incorrect results. However, the third example uses the `sort -n` command, which properly orders the file numerically.

There are several useful options for the `sort` command. Commonly used switches are shown in Table 4.3.

### TABLE 4.3 The `sort` command's commonly used options

| Short | Long | Description |
| :- | :- | :- |
| -c | --check | Check if file is already sorted. Produces no output if file is sorted. If file is not sorted, it displays the file name, the line number, the keyword `disorder`, and the first unordered line's text. |
| -f | --ignore-case | Consider lowercase characters as uppercase characters when sorting. |
| -k n1 [,n2] | --key=n1 [,n2] | Sort the file using the data in the *n1* field. May optionally specify a second sort field by following *n1* with a comma and specifying *n2*. Field delimiters are spaces by default. |
| -M | --month-sort | Display text in month of the year order. Months must be listed as standard three-letter abbreviations, such as JAN, FEB, MAR, and so on. |
| -n | --numeric-sort | Display text in numerical order. |
| -o *file* | --output=*file* | Create a new sorted file named *file*. |
| -r | --reverse | Display text in reverse sort order. |

The sort utility is handy for formatting a small text file to help you understand the data it contains. Another useful command for formatting small text files is one we've already touched on: the `cat` command.

The `cat` command's original purpose in life was to concatenate files for display. That is where it gets its name. However, it is typically used to display a single file. Listing 4.7 is an example of concatenating two files to display their text contents one after the other.

### Listing 4.7: Using the cat command to concatenate files

```
$ cat numbers.txt random.txt
42
2A
52
0010 1010
*
42
Flat Land
Schrodinger's Cat
0010 1010
0000 0010
$
```

Both files displayed in Listing 4.7 have the number 42 as their first line. This is the only way you can tell where one file ends and the other begins, because the `cat` utility does not denote a file's beginning or end in its output. Unfortunately, often the `cat` utility's useful formatting options go unexplored. Table 4.4 has a few commonly used switches.

### TABLE 4.4 The cat command's commonly used options

| Short | Long | Description |
| :--- | :--- | :--- |
| -A | --show-all | Equivalent to using the option -vET combination. |
| -E | --show-ends | Display a $ when a newline linefeed is encountered. |
| -n | --number | Number all text file lines and display that number in the output. |
| -s | --squeeze-blank | Do not display repeated blank empty text file lines. |
| -T | --show-tabs | Display a ^I when a Tab character is encountered. |
| -v | --show-nonprinting | Display nonprinting characters when encountered using either ^ and/or M- notation. |

Being able to display nonprinting characters with the `cat` command is handy. If a text file is causing some sort of odd problem when you're processing it, you can quickly see if any nonprintable characters are embedded. Listing 4.8 contains an example of this method.

### Listing 4.8: Using the `cat` command to display nonprintable characters

```
$ cat bell.txt

$ cat -v bell.txt
^G
$
```

In Listing 4.8, the first `cat` command displays the file, and it appears to simply contain a blank line. However, by employing the `-v` option, you can see that a nonprintable character exists within the file. The `^G` is in caret notation and indicates that the nonprintable Unicode character **BEL** is embedded in the file. This character causes a bell sound when the file is displayed.

Another handy set of utilities for formatting text are the `pr` and `printf` commands. The `pr` utility was covered in Chapter 3, “Managing Files, Directories, and Text,” so let's explore the `printf` command. Its entire purpose in life is to format and display text data. It has the following basic syntax:

`printf FORMAT [ARGUMENT]...`

The basic idea is that you provide text formatting via **FORMAT** for the *ARGUMENT*. A simple example is shown in Listing 4.9.

### Listing 4.9: Employing the `printf` command

```
$ printf "%s\n" "Hello World"
Hello World
$ 
```

In Listing 4.9, the `printf` command uses the `"%s\n"` as the formatting description. It is enclosed within quotation marks to prevent unexpected results. The `"%s` tells `printf` to print the string of characters listed in the *ARGUMENT*, which in this example is **Hello World**. The `"\n` portion of the **FORMAT** tells the `printf` command to print a newline character after printing the string. This allows the prompt to display on a new line, instead of at the displayed string's end.

> While the `pr` utility can handle formatting entire text files, the `printf` command is geared toward formatting the output of a single text line. You must incorporate other commands and write a Bash shell script for it to process a whole text file with it.

The formatting characters for the `printf` command are not too difficult once you have reviewed them. A few common ones are listed in Table 4.5.

## Determining Word Count

Besides formatting data, gathering statistics on various text files can also be helpful when you are managing a server. The easiest and most common utility for determining counts in a text file is the `wc` utility. The command's basic syntax is as follows:

```
wc [OPTION]... [FILE]...
```

### TABLE 4.5 The printf command's commonly used FORMAT settings

| FORMAT | Description |
| :----- | :----- |
| %c | Display the first ARGUMENT character. |
| %d | Display the ARGUMENT as a decimal integer number. |
| %f | Display the ARGUMENT as a floating-point number. |
| %s | Display the ARGUMENT as a character string. |
| \% | Display a percentage sign. |
| \" | Display a double quotation mark. |
| \\ | Display a backslash. |
| \f | Include a form feed character. |
| \n | Include a newline character. |
| \r | Include a carriage return. |
| \t | Include a horizontal tab. |

In Listing 4.10 the `printf` command is used to print a floating-point number, which has three digits after the decimal point. Only two are desired, so the `%.2f` format is used.

### Listing 4.10: Using the printf command to format a floating-point number

```
$ printf "%.2f\n" 98.532
98.53
$
```

Formatting text data can be useful in uncovering information. Be sure to play around with all these commands to get some worthwhile experience.

When you issue the **wc** command with no options and pass it a filename, the utility will display the file’s number of lines, words, and bytes in that order. Listing 4.11 shows an example.

### Listing 4.11: Employing the wc command

```
$ wc random.txt
5 9 52 random.txt
$
```

There are a few useful and commonly used options for the **wc** command. These are shown in Table 4.6.

### TABLE 4.6 The wc command’s commonly used options

| Short | Long | Description |
| :--- | :--- | :--- |
| -c | --bytes | Display the file’s byte count. |
| -L | --max-line-length | Display the byte count of the file’s longest line. |
| -l | --lines | Display the file’s line count. |
| -m | --chars | Display the file’s character count. |
| -w | --words | Display the file’s word count. |

An interesting **wc** option for troubleshooting configuration files is the -L switch. Generally speaking, configuration file line length will be under 150 bytes, though there are exceptions. Thus, if you have just edited a configuration file and that service is no longer working, check the file’s longest line length. A longer-than-usual line length indicates you might have accidentally merged two configuration file lines. An example is shown in Listing 4.12.

### Listing 4.12: Using the wc command to check line length

```
$ wc -L /etc/nsswitch.conf
72 /etc/nsswitch.conf
$
```

In Listing 4.12, the file’s line length shows a normal maximum line length of 72 bytes. This **wc** command switch can also be useful if you have other utilities that cannot process text files exceeding certain line lengths.
