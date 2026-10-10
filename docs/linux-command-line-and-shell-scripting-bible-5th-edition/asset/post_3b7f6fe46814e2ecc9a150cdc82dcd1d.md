
You can use an address range in the change command, but the results may not be what you expect:

```
$ cat data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
$ sed '2,3c\
> This is a changed line of text.
> ' data6.txt
This is line number 1.
This is a changed line of text.
This is the 4th line.
$
```

Instead of changing both lines with the text, the sed editor uses the single line of text to replace both lines.

## Transforming characters

The transform (y) command is the only sed editor command that operates on a single character. The transform command uses the format:

```
[address]y/ inchars/ outchars/
```

The transform command performs a one-to-one mapping of the inchars and outchars values. The first character in inchars is converted to the first character in outchars. The second character in inchars is converted to the second character in outchars. This mapping continues throughout the length of the specified characters. If inchars and outchars are not the same length, the sed editor produces an error message.

Here's a simple example of using the transform (y) command:

```
$ cat data9.txt
This is line 1.
This is line 2.
This is line 3.
This is line 4.
This is line 5.
This is line 1 again.
This is line 3 again.
This is the last file line.
$
$ sed 'y/123/789/' data9.txt
This is line 7.
This is line 8.
This is line 9.
This is line 4.
This is line 5.
This is line 7 again.
This is line 9 again.
This is the last file line.
$
```

As you can see from the output, each instance of the characters specified in the *inchars* pattern has been replaced by the character in the same position in the *outchars* pattern.

The transform (y) command is a global command; that is, it performs the transformation on any character found in the text line automatically, without regard to the occurrence:

```
$ echo "Test #1 of try #1." | sed 'y/123/678/'
Test #6 of try #6.
$
```

The sed editor transformed both instances of the matching character 1 in the text line. You can’t limit the transformation to a specific occurrence of the character.

## Printing revisited

The “Introducing more substitution options” section showed you how to use the p flag with the substitution (s) command to display lines that the sed editor changed. In addition, three commands can be used to print information from the data stream:

- The print (p) command to print a text line
- The equals sign (=) command to print line numbers
- The list (l) command to list a line

The following sections look at these three printing commands in the sed editor.

## Printing lines

Like the p flag in the substitution (s) command, the print (p) command prints a line in the sed editor output. On its own, this command doesn’t offer much excitement:

```
$ echo "This is a test." | sed 'p'
This is a test.
This is a test.
$
```

All it does is print the data text that you already know is there. The most common use for the print command is printing lines that contain matching text from a text pattern:

```
$ cat data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
$ sed -n "/3rd\ line/\ p" data6.txt
This is the 3rd line.
$
```

By using the -n option on the command line, you can suppress all the other lines and print only the line that contains the matching text pattern.

You can also use this as a quick way to print a subset of lines in a data stream:

```
$ sed -n "/2,3\ p" data6.txt
This is line number 2.
This is the 3rd line.
$
```

You can also use the print (p) command when you need to see a line before it gets altered, such as with the substitution (s) or change (c) command. You can create a script that displays the line before it's changed:

```
$ sed -n "/3\{
> p
> s/line/test/p
> \} " data6.txt
This is the 3rd line.
This is the 3rd test.
$
```

This sed editor command searches for lines that contain the number 3 and executes two commands. First, the script uses the p command to print the original version of the line; then it uses the s command to substitute text, along with the p flag to print the resulting text. The output shows both the original line text and the new line text.

## Printing line numbers

The equals sign (=) command prints the current line number for the line within the data stream. Line numbers are determined by using the newline character in the data stream. Each time a newline character appears in the data stream, the sed editor assumes that it terminates a line of text:

```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
$ sed "=\" data1.txt
1
The quick brown fox jumps over the lazy dog.
2
The quick brown fox jumps over the lazy dog.
3
The quick brown fox jumps over the lazy dog.
$
```

The sed editor prints the line number before the actual line of text. The p command comes in handy if you're searching for a specific text pattern in the data stream:

```
$ cat data7.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.

This is line number 1 again; we want to keep it.
This is more text we want to keep.
Last line in the file; we want to keep it.
$
$ sed -n '/text/{
> =
> p
> }' data7.txt
6
This is more text we want to keep.
$
```

By using the `-n` option, you can have the sed editor display both the line number and text for the line that contains the matching text pattern.

## Listing lines

The list (l) command allows you to print both the text and nonprintable characters in a data stream. Any nonprintable characters are shown using either their octal values, preceded by a backslash, or the standard C-style nomenclature for common nonprintable characters, such as `\t` for tab characters:

```
$ cat data10.txt
This  line  contains   tabs.
This line does contain tabs.
$
$ sed -n 'l' data10.txt
This\tline\tcontains\ttabs.$
This line does contain tabs.$
$
```

The tab character locations are shown with the `\t`. The dollar sign at the end of each line indicates the newline character. If you have a data stream that contains an escape character, the list (l) command displays it (using the octal code if necessary):

```
$ cat data11.txt
This line contains an escape character.
$
$ sed -n 'l' data11.txt
This line contains an escape character. \a$
$
```

The data11.txt file contains an escape control code, which generates a bell sound. When the cat command is used to display the text file, the escape control code isn’t shown; only the sound is generated (if the computer’s sound is turned on). However, using the list command, the escape control code used is displayed.

## Using files with sed

The substitution (s) command contains flags that allow you to work with files. There are also regular sed editor commands that let you do that without having to substitute text.

### Writing to a file

The write (w) command is used to write lines to a file. Here’s the format for the write command:

```
[address]w filename
```

The filename can be specified as either a relative or absolute pathname, but in either case, the person running the sed editor must have write permissions for the file. The address can be any type of addressing method used in sed, such as a single line number, a text pattern, or a range of line numbers or text patterns.

Here’s an example that prints only the first two lines of a data stream to a text file:

```
$ sed '1,2w test.txt' data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
$ cat test.txt
This is line number 1.
This is line number 2.
$
```

Of course, if you don’t want the lines to display on STDOUT, you can use the -n option for the sed command.

This is a great tool to use if you need to create a data file from a master file on the basis of common text values, such as those in a mailing list:

```
$ cat data12.txt
Blum, R     Browncoat
McGuiness, A Alliance
Bresnahan, C Browncoat
Harken, C   Alliance
$
$ sed -n '/Browncoat/w Browncoats.txt' data12.txt
$
$ cat Browncoats.txt
Blum, R     Browncoat
Bresnahan, C Browncoat
$
```

The sed editor writes to a destination file only the data lines that contain the text pattern.
