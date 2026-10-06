# Chapter 3 Tools of the Trade

| Notation | Meaning | Matches |
| --- | --- | --- |
| \min,max\| | At min and at max occurrences of previous regular expression | \{1,5\} [0-9]\{3,9\} [0-9]\{3\} [0-9]\{3,\} | At least 1 and at most 5 x's Anywhere from 3 to 9 successive Exactly 3 digits At least 3 digits |
| \(...)\ | Save characters matched between parentheses in register (1-9) | ^\(\) ^\(.)\1 ^\(.)\(\(\) | First character on the line; stores it in register 1 First and second characters on the line if they're the same First and second characters on the line; stores first character in register 1 and second character in register 2 |

# cut

This teaches you about a useful command as cut. This command comes in handy when you need to extract (that, as "cut out") various fields from a data file or the output of a command. The general format of the cut command is

```
cut -chars file
```

where chars specifies characters (by position) you want to extract from each line of file. This can consist of a single number, as in -5 to extract the fifth character from each line of input; a comma-separated list of numbers, as in -c1,13,50 to extract characters 1, 13, and 50; or a dash-separated range of numbers, as in -c20-50 to extract characters 20 through 50, inclusive. To extract characters to the end of the line, you can omit the number of range

```
cut -c5- data
```

extracts characters 5 through the end of the line from each line of data and writes the result to standard output.

If file is not specified, cut reads its input from standard input, meaning that you can use cut as a filter in the pipeline.

Let's take another look at the output from the who command:

```
$ who
root console Feb 24 08:54
steve tty02 Feb 24 12:55
george tty08 Feb 24 09:15
dawn tty10 Feb 24 15:55
$
```