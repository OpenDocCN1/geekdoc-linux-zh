
where command is an ed-style command applied to each line of the specified file. If no file is specified, standard input is assumed.

As sed applies the indicated command or commands to each line of the input, it writes the results to standard output.

Let's have a look. First, the intro file again:

```
$ cat intro
```

The Unix operating system was pioneered by Ken Thompson and Dennis Ritchie at Bell Laboratories in the late 1960s. One of the primary goals in the design of the Unix system was to create an environment that promoted efficient program development.

```
$
```

Suppose you want to change all occurrences of "Unix" in the text to "UNIX." This can be easily done in sed as follows:

```
$ sed 's/Unix/UNIX/' intro # Substitute Unix with UNIX
```

The UNIX operating system was pioneered by Ken Thompson and Dennis Ritchie at Bell Laboratories in the late 1960s. One of the primary goals in the design of the UNIX system was to create an environment that promoted efficient program development.

```
$
```

Get into the habit of enclosing your sed command in single quotes. Later, you'll know when the quotes are necessary and it's better to use double quotes.

The sed command s/Unix/UNIX/ is applied to every line of intro. Whether or not the line is modified, it writes to standard output. Since it's in the data stream also note that sed makes no changes to the original file.

To make the changes, you must redirect the output from sed into a temporary file and replace the original file with the newly one created:

```
$ sed 's/Unix/UNIX/' > temp # Make the changes
mv temp intro # And now make them permanent
```

```
$
```

Always make sure the correct changes were made to the file before you overwrite the original, a cat of temp would have been short before the mv temp overwrite the original data file.

If your text included more than one occurrence of "Unix" on the line, the above sed would changed just the first occurrence to "UNIX." By appending the global option g to the end of the substitute command s, you can ensure that multiple occurrences on a line will be changed.

In this case, the sed command would read

```
$ sed 's/Unix/UNIX/g' intro > temp
```

Now suppose you wanted to extract the usernames from the output of who. You already know how to do that with the cut command:

```
$ who | cut -c18
root
ruth
steve
pat
$
```

Alternatively, you can use sed to delete all the characters from the first space (which marks the end of the username) through the end of the line using a regular expression:

```
$ who | sed 's/.*//'
root
ruth
steve
pat
$
```

The sed command substitutes a blank space followed by any characters up to the end of the line (.*) with nothing (/); that is, it deletes the characters from the first blank to the end of line for each input.

## -n Option

By default, sed writes each line of input to standard output, whether or not it gets changes. Sometimes, you'll want to use sed to extract specific lines from a file. That's what the -n flag is: it tells sed that you don't want to print any lines by default. Paired with -t, you use the p command to print whichever lines match your pattern or pattern. For example, to print just the first two lines from a file:

```
$ sed -n '1,2p' intro # Just print the first 2 lines
```

The UNIX operating system was pioneered by Ken Thompson and Dennis Ritchie at Bell Laboratories.

If, instead of lines, you precede the p command with a sequence of characters enclosed in slashes, sed prints just the lines from standard input that match pattern. The following example shows how sed can be used to display the lines that contain a particular string:

```
$ sed -n '/UNIX/p' intro # Just print lines containing UNIX
```

## Deleting Lines

To delete lines, use the d command. By specifying a line number or range of numbers, you can delete specific lines from the input. In the following example, sed is used to delete the first two lines of text:

```
$ sed '1,2d' intro
```

Remember that default sed writes all lines of the input to standard output, remaining lines—that is, lines not deleted—simply written to output. By preceding d command with a pattern, you can use sed to delete all lines that contain that text. In the following example, sed is used to delete all lines containing UNIX:

```
$ sed '/UNIX/4d' intro
```

### Table 3.2 sed Examples

| Command | Description |
| :--- | :--- |
| sed '5d' | Delete line 5 |
| sed '/Test/d' | Delete all lines containing Test |
| sed -n '20,25p' | Print only lines 20 through 25 of text |
| sed '1,10s/unix/UNIX/g' intro | Change unix to UNIX wherever it appears in the first 10 lines of intro |
| sed '/jan/s/-1/5/' | Change the first jan to 5 in all lines containing jan |
| sed 's/...//' | Delete the first three characters of each line |
| sed 's/...$$' | Delete the last 3 characters from each line |
| sed -n '1' | Print all lines showing non-printing characters as \nn (where nn is octal value of the character), and tab characters as \t |

## tr

The tr filter is used to translate characters from standard input. The general form of the command is

```
tr from-chars to-chars
```

where from-chars and to-chars are one or more characters or a set of characters. Any character in from-chars encountered on the input be translated into the corresponding character in to-chars. The result of the translation is written to standard output.

In its simplest form, tr can be used to translate one character into another. Recall the form earlier in this chapter:

```
$ cat intro
```

The Unix operating system was pioneered by Ken Thompson and Dennis Ritchie at Bell Laboratories in the late 1960s. One of the primary goals in the design of the Unix system was to create an environment that promoted efficient program development.

The following shows how tr can be used to translate all e's to s's:

```
$ tr e < intro
```

The Unix operating system was pioneered by Ken Thompson and Dennis Ritchie at Bell Laboratories in the late 1960s. One of the primary goals in the design of the UNIX system was to create an environment promoted efficient program development.

The input to be redirected from the file intro because tr always expects its input to come from standard input. The results of the translation are written to standard output, leaving the original file untouched. Showing a more practical example, recall the pipeline that you used to extract the usernames and home directories of everyone on the system:

```
$ cut -f1,6 /etc/passwd
```

```
root:
cron:
bin:
ucp:/usr/spool/ucp
asg:
steve:/users/steve
other:
$
```

You can translate the colons into tab characters to produce a more readable output simply by adding an appropriate tr command to the end of the pipeline:

```
$ cut -d: -f1,6 /etc/passwd | tr : ' '
root
	cron
	bin
	ucp/usr/spool/ucp
	asg
	steve/users/steve
	other
$
```

Enclosed between the single quotes is a tab character (even though you can't see it—take our word for it). It must be enclosed in quotes to keep it from being parsed and discarded by the shell as extraneous whitespace.

Working with characters that aren't printable? The octal representation of a character can be given to tr in the format \nnn where `nnn` is the octal value of the character. This isn't used too often, but can be handy to remember.

For example, the octal value of the character is 11, so another way to accomplish the colon-to-tab transformation is to use the `tr` command

```
tr : '\11'
```

Table 3.3 lists characters that you'll often want to specify in octal format.

### Table 3.3 Octal Values of Some ASCII Characters

| Character | Octal value |
| :--- | :--- |
| Bell | 7 |
| Backspace | 10 |
| Tab | 11 |
| Newline | 12 |
| Linefeed | 12 |
| Formfeed | 14 |
| Carriage Return | 15 |
| Escape | 33 |

In the following example, `tr` takes the output from `date` and translates all spaces into newline characters. The result is that each field of output appears on a different line:

```
$ date | tr ' '\12' # Translate spaces to newlines
Sun
```
