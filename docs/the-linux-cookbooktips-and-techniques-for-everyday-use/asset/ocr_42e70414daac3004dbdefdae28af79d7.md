```
Print the user name associated with the current effective user id.
Same as id -un.

--help      display this help and exit
--version   output version information and exit

Report bugs to sh-utils-bugs@gnu.ai.mit.edu
$
```

This command outputs some usage information about the whoami tool, including a short description and a list of possible options.

*NOTE:* Not all tools take the `--help` option; some tools take a `-h` or `-?` option instead, which performs the same function.

# 3.8.4 Reading a Page from the System Manual

In the olden days, the hardcopy reference manual that came with most Unix systems also existed electronically on the system itself; each software program that came with the system had its own manual page (often called a "man page") that described it. This is still true on Linux-based systems today, except they don't always come with a hardcopy manual.

Use the man tool to view a page in the system manual. As an argument to man, give the name of the program whose manual page you want to view (so to view the manual page for man, you would type man man).

+   - To view the manual page for w, type:

```
$ man w RET
```

This command displays the manual page for w: