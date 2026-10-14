# 2.8.2 Getting a Description of a Program

Use whatis to get a one-line description of a program. Give as an argument the name of the tool or application you want described.

⇒ To get a description of the who tool, type:

```
$ whatis who [RET]
```

NOTES: The whatis tool gets its descriptions from the manual page of a given program; manual pages are described later in this section, in Recipe 2.8.4 [Reading a Page from the System Manual], page 46.

# 2.8.3 Listing the Usage of a Tool

Many tools have a long-style option, --help, that outputs usage information about the tool, including the options and arguments the tool takes.

⇒ To list the possible options for whoami, type:

```
$ whoami --help [RET]
Usage: whoami [OPTION]...
Print the user name associated with the current effective user id.
Same as id -un.

--help     display this help and exit
--version  output version information and exit

Report bugs to <bug-sh-utils@gnu.org>.
$
```

This command outputs some usage information about the whoami tool, including a short description and a list of possible options.

NOTES: Not all tools take the --help option; some tools take a -h or -? option instead, which performs the same function.

# 2.8.4 Reading a Page from the System Manual

In the olden days, the hardcopy reference manual that came with most UNIX systems also existed electronically on the system itself; each software program that came with the system had its own manual page (often called a “man page”) that described it. This is still true on Linux-based systems today, except they usually don’t come with a hardcopy manual.