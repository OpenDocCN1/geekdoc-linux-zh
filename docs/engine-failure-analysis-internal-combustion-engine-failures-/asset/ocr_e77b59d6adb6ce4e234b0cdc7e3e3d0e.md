# EXAMPLE

| This Command | Does the Following |
| --- | --- |
| sum *.txt | Displays the checksum and blocks the count for all the .txt files in the working directory. |

# tac

**tac** [ *option* ] [ *filename* ]

Display *filename* in reverse line order, starting from the last line (the opposite of cat).

See also *rev*.

# OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -b, --before | Attach the separator before instead of after |
| --help | Show the available options |
| -r, --regex | Interpret the separator as a regular expression |
| -s, --separator=string | Use string as the separator instead of newline |
| --version | Show the version number |

# tail

**tail** [ *option* ] [ *filename* ]

Print the last ten lines of each file to the standard output. You can specify more than one *filename* in a space-separated list or by using a shell pattern (see the section “Shell Patterns” in Chapter 4). The utility prints the name of each file before the text. If you omit the *file-name*, the utility accepts input from the standard input.