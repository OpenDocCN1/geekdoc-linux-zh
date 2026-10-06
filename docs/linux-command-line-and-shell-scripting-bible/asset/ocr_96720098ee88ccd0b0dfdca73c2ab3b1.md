# B Quick Guide to sed and gawk

The format of the read command is:

```
[address]r filename
```

The filename parameter specifies either an absolute or relative pathname for the file that contains data. You can't use a range of addresses for the read command. You can only specify a single line number or text pattern address. The sed editor inserts the text from the file after the address.

```
$ sed '3r data' data2
```

The sed editor inserts the complete text from the data file into the data2 file, starting at line 3 of the data2 file.

# the gawk program

The gawk program is the GNU version of the original awk program in Unix. The awk program takes stream editing one step further than the sed editor by providing a programming language instead of just editor commands. This section describes the basics of the gawk program as a quick reference to its abilities.

# The gawk command format

The basic format of the gawk program is:

```
gawk options program file
```

Table B-2 shows the options available with the gawk program.

| Option | Description |
|---|--- |
| -F fs | Specify a file separator for delineating data fields in a line. |
| -f file | Specify a filename to read the program from. |
| -v var=value | Define a variable and default value used in the gawk program. |
| -mf N | Specify the maximum number of fields to process in the data file. |
| -mr N | Specify the maximum record size in the data file. |
| -W keyword | Specify the compatibility mode or warning level for gawk. Use help to list all the available keywords. |