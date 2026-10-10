To show these built-in variables in use, here is a sample program called mypgm2:

```
#!/bin/sh

#my test program
echo "Number of parameters is $#"
echo "Program name is $0"
echo "Parameters as a single string is $*"
```

If you execute mypgm2 from the command line in bash as follows

$ bash mypgm2 Andrew Hudson

you get the following result:

```
Number of parameters is 2
Program name is mypgm2
Parameters as a single string is Sanjiv Guha
```

# # Special Characters

Some characters have special meaning to Linux shells; these characters represent commands, denote specific use for surrounding text, or provide search parameters. Special characters provide a sort of shorthand by incorporating these rather complex meanings into a simple character. Table 33.1 shows some special characters.

TABLE 33.1 Special Shell Characters

| Character | Explanation |
| :--- | :--- |
| $ | Indicates the beginning of a shell variable name |
| \| | Pipes standard output to next command |
| # | Starts a comment |
| & | Executes a process in the background |
| ? | Matches one character |
| * | Matches one or more characters |
| > | Output redirection operator |
| < | Input redirection operator |
| ' | Command substitution (the backquote or backtick—the key above the Tab key on most keyboards) |
| >> | Output redirection operator (to append to a file) |
| << | Wait until following end-of-input string (here operator) |
| [ ] | Range of characters |
| [a-z] | All characters a through z |
| [a,z] or [az] | Characters a or z |
| Space | Delimiter between two words |