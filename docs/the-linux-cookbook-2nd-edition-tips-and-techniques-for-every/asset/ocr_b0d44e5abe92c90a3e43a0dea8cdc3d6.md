There are several methods for doing this, each with its own output format. All of them are capable of outputting in hexadecimal (or "hex" for short); these outputs are sometimes called hex dumps.

# METHOD #1

The hexdump filter dumps its input in any one of a number of formats, showing a number of characters from the file per line, and preceded with a number indicating the location in the file of the first character in that line.

To display text in hex, first use the tr filter to eliminate carriage returns from the input, and pass this text to hexdump with the -C option, which displays its input in hexadecimal, with one byte per character. 16 characters of the input are displayed on each line, separated by spaces, and a column is written on the left-hand side showing the offset value of the file, in hexadecimal.

⇒ To peruse the contents of the file ‘tarpon’ in hexadecimal, type:

```
$ tr -d '\r' < tarpon | hexdump -C | less [RET]
```

# METHOD #2

Use od, "octal dump," to make a literal and unambiguous dump of some text. It works as a filter or takes the name of a file as an argument, and can output in octal, hexadecimal, or other formats

Use the -t option to specify the format type of the output, and give "x1" as an argument to specify that the display should be in hexadecimal, with one byte per integer (with an argument of "x2," a hex integer is displayed for every two bytes of input).

⇒ To peruse the contents of the file details in hex, type:

```
$ od -t x1 details | less [RET]
```

This command outputs the values of each literal character of the file details in hexadecimal, 16 characters per line, separated by spaces. Each line is preceded by an offset value (in octal) indicating the offset in the file of the first character in that line. To change the offset display from octal to decimal, use the -A option and give "d" as an argument (or give "x" if you want hex).

To display the printable characters in a new column on the right-hand side of the screen, add a "z" to the end of your argument to the -t option. Each line of the column will be prefaced with a greater-than sign (>) and end with a less-than sign (<).