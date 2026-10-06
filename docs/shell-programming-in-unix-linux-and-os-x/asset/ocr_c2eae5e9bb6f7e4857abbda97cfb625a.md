Leading whitespace characters are removed from any line that's read. The backslash characters are also interpreted by the shell when it reads the line. You can use the -r option of read to prevent it from interpreting the backslash character. If we change the

while read to

in number to

while read -r line

the output will look like:

```
$ number
Here are some backslashes: \*
1: Here are some backslashes: \\*
$
```

In Chapter 11 you'll learn how to preserve the leading whitespace characters and also how to have some control over the parsing of the input data.

# The printf Command

echo is quite adequate for displaying simple messages, sometimes you'll want to print formatted output: for example, lining up columns of data. Unix systems provide the printf command for these tasks. Those of you familiar with the C or C++ programming language will notice many similarities with their function of the name.

The general format of the printf command is

```
printf "format" arg1 arg2 ...
```

where format is a string that details how the subsequent values are to be displayed. Since the printf string is an argument and likely to contain special characters, spaces, it's always a good idea to include it in quotes.

Characters preceded by a percent sign are called format specifications and tell printf how the corresponding argument should be displayed. Each percent sign in the format string there should be a corresponding argument, except for the percent specification %%, which causes a single percent to be displayed.

```
$ printf "Hello world!\n"
Hello world!
$
```

Let's start with a simple example of printf:

```
$ printf "This is a number: %d\n" 10
This is a number: 10
$
```