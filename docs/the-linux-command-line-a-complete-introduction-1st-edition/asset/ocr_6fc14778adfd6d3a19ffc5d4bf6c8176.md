In this example, we employ the -l option (for page length) and the -w option (page width) to define a "page" that is 65 characters wide and 15 lines long. pr paginates the contents of the distros.txt file, separates each page with several lines of whitespace, and creates a default header containing the file modification time, filename, and page number. The pr program provides many options to control page layout. We'll take a look at more of them in Chapter 22.

# printf—Format and Print Data

Unlike the other commands in this chapter, the printf command is not used for pipelines (it does not accept standard input), nor does it find frequent application directly on the command line (it's used mostly in scripts). So why is it important? Because it is so widely used.

printf (from the phrase print formatted) was originally developed for the C programming language and has been implemented in many programming languages, including the shell. In fact, in bash, printf is a built-in.

printf works like this:

```
printf "format" arguments
```

The command is given a string containing a format description, which is then applied to a list of arguments. The formatted result is sent to standard output. Here is a trivial example:

```
[me@linuxbox ~]$ printf "I formatted the string: %s\n" foo
I formatted the string: foo
```

The format string may contain literal text (like I formatted the string:); escape sequences (such as \n, a newline character); and sequences beginning with the % character, which are called conversion specifications. In the example above, the conversion specification %s is used to format the string foo and place it in the command's output. Here it is again:

```
[me@linuxbox ~]$ printf "I formatted '%s' as a string.\n" foo
I formatted 'foo' as a string.
```

As we can see, the %s conversion specification is replaced by the string foo in the command's output. The s conversion is used to format string data. There are other specifiers for other kinds of data. Table 21-4 lists the commonly used data types.

# Table 21-4: Common printf Data-Type Specifiers

| Specifier | Description |
|-----------|-------------|
| d | Format a number as a signed decimal integer. |
| f | Format and output a floating point number. |

(continued)