# gawk

Searches for and processes patterns in a file

gawk [options] [program] [file-list]
gawk [options] –f program-file [file-list]

The gawk (GNU awk) utility is a pattern-scanning and processing language that searches one or
more files to see whether they contain records (usually lines) that match specified patterns and then
performs actions, such as writing the record to standard output or incrementing a counter, each time
it finds a. You can use gawk to generate reports or filter text. It works equally with num-
bers and text; when you mix the two, gawk usually comes up with the right answer.

The authors of awk (Alfred V. Aho, Peter J. Weinberger, and Brian W. Kernighan), on which gawk
is based, designed awk to be easy to use, and to this end they sacrificed execution speed.

The gawk utility takes many of its constructs from the C programming language and includes the
following features:

+   * Flexible format
* Conditional execution
* Looping statements
* Numeric variables
* String variables
* Regular expressions
* Relational expressions
* C's printf

The gawk utility takes its input from files you specify on the command line or from standard input.

# Arguments

The program is a gawk program that you include on the command line. The program-file
is the name of the file that holds the gawk program. Putting the program on the com-
mand line allows you to write simple, short gawk programs without having to create
a separate program-file. To prevent the shell from interpreting the gawk commands
shell commands, it is a good idea to enclose the program within single quotation
marks. Putting the program in a file reduces typing and the chance for errors when
t program is long or complex. See the –f option and “Discussion” following.

The file-list contains pathnames of the ordinary files that gawk processes. These
files are the input files.