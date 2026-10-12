The man command allows you to view the online manuals. The syntax for this command is as follows:

```
man [-k] [section] keyword
```

The keyword is usually the name of the program, utility, or function. The default action is to search in all of the available sections following a predefined order and to show only the first page found, even if the keyword exists in several sections.

Because commands may appear in several sections, the first page found might not be the man page you are looking for. The command printf is a good example.

Say you are writing a program and would like to know more about the ANSI C library function printf(). Just by typing

```
man printf
```

you get information about printf. However, the man pages for this printf are for the shell command printf. Obviously, this is the wrong information. A reasonable solution is to list all of the sections covering printf (if it exists in multiple sections) and to select the correct one. You can search the keywords of the man pages with the -k option:

```
man -k printf
fprintf    printf (3)    - formatted output conversion
fprintf    printf (3)    - print formatted output
printf     printf (1)    - write formatted output
printf     printf (3)    - formatted output conversion
printf     printf (3)    - print formatted output
```

The printf you are interested in in this example is a library function that can be found in section 3 (from Table B-4) or, more specifically, in section 3b or 3s (as you can see from the preceding output). To specify a particular section of a man page, you pass it to man at the command line to find the correct information you are looking for:

```
man 3b printf
```