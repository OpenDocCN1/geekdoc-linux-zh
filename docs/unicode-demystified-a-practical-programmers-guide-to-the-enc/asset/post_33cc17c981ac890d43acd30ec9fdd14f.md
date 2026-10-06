
# Communication Utilities

| utility | description |
| :--- | :--- |
| mail | Sends and receives electronic mail—page 1241 |
| pine | Sends and receives electronic mail and news—page 1278 |

# Utilities That Display and Alter Status

| utility | description |
| :--- | :--- |
| cd | Changes to another working directory—page 1100 |
| chgrp | Changes the group associated with a file—page 1102 |
| chmod | Changes the access mode of a file—page 1103 |
| chown | Changes the owner of a file—page 1108 |
| date | Displays or sets the time and date—page 1141 |
| df | Displays disk space usage—page 1147 |
| du | Displays information on disk usage—page 1155 |
| file | Displays the classification of a file—page 1163 |
| finger | Displays information about users—page 1171 |
| kill | Terminates a process—page 1224 |
| nice | Changes the priority of a command—page 1263 |
| nohup | Runs a command that keeps running after you log out—page 1264 |
| ps | Displays process status—page 1268 |
| sleep | Creates a process that sleeps for a specified interval—page 1234 |
| stty | Displays or sets terminal parameters—page 1335 |
| top | Dynamically displays process status—page 1356 |
| umask | Establishes the file-creation permissions mask—page 1366 |
| w | Displays information on system users—page 1370 |

# Utilities That Are Programming Tools

| utility | description |
| :--- | :--- |
| configure | Configures source code automatically—page 1120 |
| gcc | Compiles C and C++ programs—page 1210 |
| make | Keeps a set of programs current—page 1247 |
| patch | Updates source code—page 1272 |

# Source Code Management (RCS, CVS) Utilities

| utility | description |
| :--- | :--- |
| ci | Creates or records changes in an RCS file—page 1110 |
| co | Retrieves an unencoded revision of an RCS file—page 1115 |
| cvs | Manages concurrent access to files in a hierarchy—page 1134 |
| rcs | Creates or changes the attributes of an RCS file—page 1295 |
| rlog | Prints a summary of the history of an RCS file—page 1298 |

# Miscellaneous Utilities

| utility | description |
| :--- | :--- |
| at | Executes a shell script at a time you specify—page 1093 |
| cal | Displays a calendar—page 1096 |
| crontab | Maintains crontab files—page 1129 |
| echo | Displays a message—page 1157 |
| expr | Evaluates an expression—page 1159 |
| utility | description |
| :--- | :--- |
| which | Shows where in your path command is located—page 1373 |
| who | Displays names of users—page 1375 |
| fsck | Checks and repairs a filesystem—page 1176 |
| Mtools | Uses DOS-style commands on files and directories—page 1256 |
| tee | Copies standard input to standard output and one or more files—page 1348 |
| test | Evaluates an expression—page 1352 |
| tr | Replaces specified characters—page 1362 |
| tty | Displays the terminal pathname—page 1365 |
| xargs | Converts standard output of one command into arguments for other—page 1377 |

The following sample shows the format that is used throughout Part III. These descriptions of the utilities are similar to the man page descriptions (pages 42 and 1252); however, most users find the descriptions in this book easier to read and understand. These descriptions emphasize the most useful features of the utilities and often leave out the more obscure features. For information about the less commonly features, refer to the man and info pages.

# sample

Very brief description of what the utility does
Following the syntax-line is one or more paragraphs that describe the utility. The syntax-line shows how to run the utility from a command line. Options and arguments enclosed in brackets [] are not required. Type words that appear in this sans serif italic typeface as. Words that you must substitute when you type appear in this bold typeface. Hyphenated words listed as arguments identify single arguments (for example, source-file) or groups of arguments (for example, directory-list). This section describes the arguments you can use when you run the utility. The argument itself, as shown in the preceding syntax-line, is printed in bold italic.

This section lists the common options you can use with the command. Otherwise, you must precede options with a hyphen. Most commands accept a single hyphen before multiple options. The following are some options:

- toc This is an example of a simple option preceded by a single dash and not followed by any arguments. The toc appearing as the first word of the description is a cue, a suggestion of what the option stands for. It stands for toc or table of contents.
- program-file Includes an argument. The argument is set in bold italic in both the left and the description right. Substitute another word (filename, string of characters, or other value) for any arguments you use in this serif typeface (such as -f) as is.
- make-directories This is an example of an option that has a long and short version. You can tell that -d at the beginning of the description is a cue to what the option means because it is preceded by a hyphen and does not look like.

# Discussion
This optional section contains a discussion about how to use the utility and any quirks it may have.

# Notes
This section contains miscellaneous notes: some important and others interesting.

# Examples
This section contains examples of a tutorial and is more casual than the preceding sections.

# aspell

Checks a file for spelling errors

aspell action [options] filename
The aspell utility checks words in a document against a standard dictionary. You can use aspell utility interactively: it displays each misspelled word in context, together with a menu that gives you the choice of accepting the word, choosing one of aspell's suggested replacements, inserting the word into your personal dictionary, and entering a new word. You can also use aspell so that it reads from standard input and writes to standard output. This mode is suitable when you want to redirect from standard input or output or simply want a list of misspelled words, per line. For more information refer to /usr/share/doc/aspell* on your system (with manuals in the man-html and man-text subdirectories) and to the aspell home page at aspell.sourceforge.net.

aspell Not Like Other Utilities Regarding Its Input
Unlike many other utilities, aspell does not accept input from standard input when you do not specify a filename on the command line. Instead, aspell specifies where it gets its input.

# Action
You can specify aspell action using the long form (not preceded with a hyphen) or the short form (preceded with a hyphen)—not all actions have short forms. You must choose one and only one of the actions when you run aspell.

- check -c Runs aspell as an interactive spell checker. Input comes from a single filename on the command line. own- config Displays aspell's configuration: both the default and current values. Output goes to standard output. Send the output through a pipe to less to read the whole document.
- help -h Displays an extensive page of help. Output goes to standard output. Send the output through a pipe to less for easier viewing.
- list -l Runs aspell noninteractively. Input comes from standard input. Output goes to standard output.

1. The aspell manual uses the term commands where its usage message uses the term action. This book uses action.

The filename is the name of the file you want to check. The aspell utility accepts this argument only when you use the check (-c) action.

# Arguments
The default values of many of the options are determined when aspell is compiled (see the config action). You can specify options on the command line, in ASPELL_CONF shell variable, or in your personal configuration file (~/.aspell.conf). Superuser can create a global configuration file (/etc/aspell.conf). Put one option per line in a configuration file; separate options with a semicolon (;) in ASPELL_CONF. Options on the command line override those in ASPELL_CONF, which override those in your personal configuration file, which override in the global configuration file. Specify an option using the long or short form (not all options have short forms). The short form is valid only on the command line: it cannot be used in ASPELL_CONF or a configuration file.

# aspell Options and Leading Hyphens
The way you specify options differs, depending on whether you are specifying them on the command line or in the ASPELL_CONF variable or a configuration file.

On the command line: Prefix long options with two hyphens (for example, --ignore-case or --ignore-case). Short options are always prefixed with a single hyphen and are allowed only on the command line.

In ASPELL_CONF or a configuration file: Drop the leading hyphens (for example, ignore-case or ignore-case).

In the following list, the Boolean options turn a feature on (enable the feature) or off (disable the feature). Precede a Boolean option with no- to turn it off. For example, --ignore-case turns this feature on, and --dont-ignore-case turns it off. Value options assign a value to a feature. Follow the option by a SPACE and an appropriate value (string or integer). For all options in a configuration file or in ASPELL_CONF variable, use the long form, without leading hyphens.

- --backup Creates a backup file named filename.bak (default is --backup).
- --Wn N ignores equal to or shorter than n characters (default is 1).
- --ignore-case Ignores the case of letters in words being checked (default is --dont-ignore-case).
- --strip-accents Removes accent marks from all the words in the dictionary before checking words (default is --dont-strip-accents).

# Options
