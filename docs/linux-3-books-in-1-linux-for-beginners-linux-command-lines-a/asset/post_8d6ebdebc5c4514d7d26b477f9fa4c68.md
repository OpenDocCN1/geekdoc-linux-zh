
tasks in the Linux operating system using the Bash shell. You can also use the Bash shell to perform tasks that would be rather complicated, even on the graphical interface.

The Bash shell, as mentioned earlier, can be accessed through the terminal in Ubuntu. The keyboard works as the input device for the terminal, and the monitor works as the output device to show you the result of your commands. There are virtual consoles available on Linux to access the Bash shell as well. This helps you to have multiple virtual consoles on a single physical machine, and multiple users can log in via the multiple virtual consoles.

## Shell Basics

There are three parts to the command that you enter on the shell prompt in Linux.

1. *Command that you want to run*
2. *Options that will define the behavior of the command*
3. *Arguments that are the command's targets*

The command defines the program that you want to execute. The command can be followed by options or no options at all. The options will define how a command will behave and how it will function. You can use a dash or two dashes to specify an option. The dashes are appended to options so that options can be distinguished from arguments.

Example -a or --all

Arguments also follow the command, and you can have a single argument or multiple arguments. Arguments are the targets on which the command gets executed upon.

A basic command looks like this.

*usermod -L John*

The command in this example is *usermod*

The option is *-L*

The argument is John

This command is used to lock the password of the user John on the Linux system.

It is useful to know which options go with which commands to be efficient on the command line. The --help option with any command will give you a list of options that can be used with that particular command. It is not important to know every option by heart. The list also gives you a description of what the option does.

Let us see an example of this with the grep command. The grep command is used to search through a string or a file. If the file has a string that matches the one specified by you in your grep command, the output shows every line of the file that contains the specified string.

```
[student@desktop ~]$ grep --help

Usage: grep [OPTION]... PATTERN [FILE]...

Search for PATTERN in each FILE or standard input.

PATTERN is, by default, a basic regular expression (BRE).

Example: grep -i 'hello world' menu.h main.c

Regex Selection and Interpretation:
-E, --extended-regexp         PATTERN is an extended regular expression (ERE)
-F, --fixed-strings           PATTERN is a set of newline-separated fixed strings
-G, --basic-regexp           PATTERN is a basic regular expression (BRE)
-P, --perl-regexp           PATTERN is a Perl regular expression
-e, --regexp=PATTERN        use PATTERN for matching
-f, --file=FILE             obtain PATTERN from FILE
-i, --ignore-case			ignore case distinctions
-w, --word-regexp			force PATTERN to match only whole words
-x, --line-regexp			force PATTERN to match only whole lines
-z, --null-data			a data line ends in 0 byte, not newline

Miscellaneous:
-s, --no-messages			suppress error messages
-v, --invert-match			select non-matching lines
-V, --version			display version information and exit
--help			display this help text and exit

Output Control:
-m, --max-count=NUM		stop after NUM matches
-b, --byte-offset			print the byte offset with output lines
-n, --line-number			print line number with output lines
--line-buffered			flush output on every line
-H, --with-filename		print the file name for each match
-h, --no-filename			suppress the file name prefix on output
--label=LABEL			use LABEL as the standard input file name
-o, --only-matching		show only the part of a line matching PATTERN
-q, --quiet, --silent	suppress all normal output
--binary-files=TYPE	assume that binary files are TYPE; TYPE is 'binary', 'text', or 'without-match'
-a, --text			equivalent to --binary-files=text
-I                equivalent to --binary-files=without-match
-d, --directories=ACTION  how to handle directories; ACTION is 'read', 'recurse', or 'skip'
-D, --devices=ACTION     how to handle devices, FIFOs, and sockets; ACTION is 'read' or 'skip'
-r, --recursive           like --directories=recurse
-R, --dereference-recursive likewise, but follow all symlinks
--include=FILE_PATTERN  search only files that match FILE_PATTERN
--exclude=FILE_PATTERN  skip files and directories matching FILE_PATTERN
--exclude-from=FILE   skip files matching any file pattern from FILE
--exclude-dir=PATTERN  directories that match PATTERN will be skipped.
-L, --files-without-match print only names of FILES containing no match
-l, --files-with-matches  print only names of FILES containing matches
-c, --count               print only a count of matching lines per FILE
-T, --initial-tab         make tabs line up (if needed)
-Z, --null                print 0 byte after FILE name

Context Control:
-B, --before-context=NUM print NUM lines of leading context
-A, --after-context=NUM print NUM lines of trailing context
-C, --context=NUM  print NUM lines of output context
-NUM  same as --context=NUM
--group-separator=SEP use SEP as a group separator
--no-group-separator use empty string as a group separator
--color[=WHEN],
--colour[=WHEN]   use markers to highlight the matching strings; WHEN is 'always', 'never', or 'auto'
-U, --binary    do not strip CR characters at EOL (MSDOS/Windows)
-u, --unix-byte-offsets  report offsets as if CRs were not there (MSDOS/Windows)

'egrep' means 'grep -E'. 'fgrep' means 'grep -F'.

Direct invocation as either 'egrep' or 'fgrep' is deprecated.

When FILE is -, read standard input. With no FILE, read . if a command-line -r is given, - otherwise. If fewer than two FILES are given, assume -h.
Exit status is 0 if any line is selected, 1 otherwise;
if any error occurs and -q is not given, the exit status is 2.

Report Bugs to: bug-grep@gnu.org
GNU Grep home page: <http://www.gnu.org/software/grep/>
General help using GNU software: <http://www.gnu.org/gethelp/>
```

You may find the command line a bit difficult to understand initially, but you will enjoy it more than the graphical interface once you get used to the command line.

Let us try to understand the essential syntax of the command line.

- Options are wrapped using square brackets []
- If a command is followed by …, it indicates the list of items belonging to the same type
- If you have specified multiple items and separated them using a pipe | it indicates that only of them should be used
- Variables are specified using angle brackets <>. If you see <filename> in the syntax, you know you have to replace it with the actual filename

Let us go through an example.

```
[student@desktop ~]$ date --help
date [OPTION]... [+FORMAT]
```

This indicates that the command is **date**, and it takes the options represented by **[OPTION]**. It also takes another option **[FORMAT]** prefixed with a + sign.

## Executing Commands

The bash shell’s primary function is to interpret the commands input by a user and convert them into system-specific instructions for the Linux operating system. We already know that a string you end on the shell prompt is made up of three parts, command, options, and arguments. Every word that is entered on the command prompt needs to be separated by using a blank space. The Linux system already has a script file where the function of the command you type is defined. You can manipulate this script by passing options and arguments to your command.
