
# bfs 105

Merry merry king of the bush is is he
Laugh, kookaburra, laugh
Glad your life must be.

Kookaburra sits in the old gum tree
Eating all the gumdrops he can see
Laugh, kookaburra, laugh
Leave some there for me.

# Files

/tmp/bd*
Temporary file used for comparison.

While biff is comparing files, it creates temporary files in the /tmp directory. When the comparison is done, the files are automatically removed. The following example shows two temporary files.

```
caste% ls /tmp/bd*
bdcG4GX bdowl1VW
caste%
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwesu |
| CSI | Enabled |

# See Also

diff(1), attributes(5), largefile(5)

# Diagnostics

Use help for explanations.

# bfs — Big File Scanner

# Synopsis

```
/usr/bin/bfs [-] filename
```

# 106

# bfs

# Description

The bfs command is similar to ed(1) except that it is read-only and processes much larger files. Files can be up to 1024 Kbytes and 32-Kbyte lines, with up to 512 characters, including newline, per line (255 for 16-bit machines). bfs is usually more efficient than ed(1) for scanning a file because the file is not copied to a buffer. It is most useful for identifying sections of a large file where you use split(1) to divide the file into more manageable pieces for editing.

Normally, the size of the file being scanned is the size of any file with the (w) write. The optional - suppresses printing of sizes. You can turn on prompting for input with if you type P and press Return, as in ed(1). You can turn prompting off by typing another P and pressing Return. Note that when prompting is turned on, messages are displayed in errors.

All expressions described under ed(1) are supported. You can surround regular expressions with two symbols like / and > indicates downward search without wrap-around, and < indicates only the letters a through z for mark names, and all 26 are remembered.

# bfs Commands

The e, v, k, p, q, w, !, and n commands are as described under ed(1). Commands such as --, +, +==-12, and =f are accepted. Note that 1,10b and 1,10 both print the first 10 lines. The f command prints the name of the file being scanned; there is no referenced file name. The w command is independent of output diversion, truncation, or crunch (see the xo, xt, and xc commands, below). Additional commands that are listed below.

- + - label Position a label in a command file. Terminate the label by newline, and ignore blanks before the (:) and the start of the label. You can also use this command to insert comments into a command file, because labels need not be referenced.

- (, )/regular expression/label

Jump (either upward or downward) to label if the command succeeds. It fails under any of the following conditions:

+ - Either address is not between 1 and $.
- The second address is less than the first.
- The regular expression does not match at least one line in the specified range, including the first and last lines.

On success, dot (.) moves to the matched line and jump to label. This command is the only one that does not issue an error message on bad addresses, so it can be used to test whether addresses are bad before other commands are executed. Note that the command xb/label is an unconditional jump.

The xb command is allowed only if it is from some place other than a terminal. If it is read from a pipe, you can jump downward.

- xbz label Test the last return code from the execution of a UNIX system command (!command) or non-zero value to the specified label. The two examples below both search for the next five lines containing the string

# 107

# bfs

Example 1:

```
xv55
: 1
/size/
xv5!expr %5 - 1
!!if 0%5 != 0 exit 2
xbn 1
```

Example 2:

```
xv45
: 1
/size/
xv4!expr %4 - 1
!!if 0%4 = 0 exit 2
xbz 1
```

- xc[switch] If switch1, crunch output from the p and null commands; if switch is 0, don't crunch output. Without an argument, xc reverses switch. Initially, switch is set for no crunching. Crun output reduces strings of tags and blanks to one blank and suppresses blank lines.

- xf file Take further commands from the named file. When an end-of-file is reached, an interrupt signal is received, or an error occurs, resume reading the file containing the xf. You can nest the x commands to a depth of 10.

- xn List the marks currently in (you set marks with the k command).

- xo [file] Divert output from the p and null commands to the named file, which, if necessary, is created 666 (readable and writable by everyone) unless your umask setting (umask(1)) dictates otherwise. If fileis missing, divert output to the standard output. Note that each diversion causes truncation or creation of the file.

- xt number Truncate output from the p and null commands to, at most, number characters. The initial number is 255.

- xv[digit] [spaces] Set the variable name to specify the digit following xv. The commands xv510 or xv55 assign the value 100 to the variable 5. The command xv61,100p assigns the value 1,100p to the variable 6. To reference a variable, put a % in front of the variable name. For example, using the above assignments for variables 5 and 6, the following commands all print the first 100.

```
1,%5p
1,%5
%6
```

- g/%5/p globally searches for the characters 100 and prints each line containing a match.

# 108

# bfs

To escape the special meaning of %, precede it with a backslash (\). For example, you can use g/".*\\[cds]/p to match and list %c, %d, and %s formats (for example, print f-like statements) of characters, decimal integers, and strings.

Another feature of the xv command is that you can store the first line of output from a UNIX system command in a variable. The only requirement is that the first character of value be an !. For example, the following lines put the current line into variable 35, print it, and increment the variable 36 by 1.

```
.w junk
xv5!cat junk
!rm junk
!echo "%5"
xv6!expr %6 + 1
```

To escape the special meaning of ! as the first character of value, precede it with a \. The following statement stores the value !date in variable 7.

```
xv7!date
```

# Operands

filename

Any file to 1024 Kbytes and 32-Kbyte lines, with up to 512 characters, including newline, per line (255 for 16-bit machines). filename can be a section of a larger file that has been divided into manageable sections for editing by the use of csplit(1).

# Examples

The following example returns the total number of characters in the core file and exits with Control-D.

```
castle% bfs core
1890
^D
castle%
```

The following example returns the total number of characters in the bibliography file, assigns the value 100 to a variable 5, prints lines 1–100 of the file, and exits with Control-D. The example shows only the first few of 100.

```
castle% bfs bibliography
4471
xv100
1,%5p
%A Janice Winsor
%T Opening the Dream Door
%P 153
%I Merrill-West Publishing
^D
castle%
```

The following example uses the - option to suppress printing of the total number of characters in the bibliography file. It then assigns the value dreams to the variable 1, displays the value of the variable, searches for all lines in the file that contain the word dreams, and exits with Control-D.

```
```
caste% bfs - bibliography

xvdreams
echo "%1"
dreams
g/%1/p
%K dreams, psychic development dreams, psychic development
dreams as an example, Janice Winsor makes practical suggestions
Processes for remembering and accessing dreams are taught in an
^Dncaste%
```
```

The following example returns the total number of characters in the bibliography file, assigns the value date to a variable 7, displays the value of the variable, and exits with Control-D.

```
```
caste% bfs bibliography
4471
x7:date
echo "%7"
Thursday March 18 08:36:52 WST 1999
^D
caste%
```
```

# Exit Status

| 0 | Successful completion without any file or command errors |
| >0 | An error occurred |

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwesu |

# See Also

```
csplit(1), ed(1), umask(1), attributes(5)
```

# Diagnostics

Message is ? for errors in commands if prompting is turned off. Self-explanatory error messages are displayed when prompting is on.
