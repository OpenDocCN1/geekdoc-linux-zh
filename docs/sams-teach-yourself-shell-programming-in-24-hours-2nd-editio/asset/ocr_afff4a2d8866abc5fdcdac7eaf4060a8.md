awk comes from the last names of its creators Alfred Aho, Peter Weinberger, and Brian Kernighan. awk was added to UNIX Version 7 in 1978 and has been an indispensable part of it ever since.

There are three versions of awk:

+   - Original awk
+   - New nawk
+   - The POSIX/GNU version gawk

Original awk has remained almost the same since its first introduction to UNIX in 1978. It was intended to be a small programming language for filtering text and producing reports. By the mid-1980s, people were using awk for large programs, so its authors decided to extend it. This version, called nawk (short for new awk), was released to the public in 1987 and became a part of SunOS 4.1.x. nawk was supposed to replace awk, but this has not yet happened. Most commercial UNIX versions such as HP-UX and Solaris still ship with both awk and nawk. BSD systems also ship with awk rather than nawk.

In 1992 the Institute of Electrical and Electronics Engineers (IEEE) standardized awk as part of its Portable Operating Systems Interface standard (POSIX). gawk, the GNU version of awk, is based on the POSIX standard. All Linux systems ship with gawk.

The examples in this chapter work with any version of awk.

# Basic Syntax

The basic syntax of an awk command is

```
awk 'script' files
```

Here, files is a list of one or more files, and script is one or more commands of the form:

```
/pattern/ { actions }
```

Here pattern is a regular expression, and actions are one or more of the commands covered later in this chapter. If pattern is omitted, awk performs the actions for each input line.

Let's get started by looking at a simple task: printing the lines in a file. In order to print the file fruit_prices.txt (from the previous chapter), you can use the following command:

```
$ awk '{ print ; }' fruit_prices.txt
Fruit Price/lbs Quantity
Banana $0.80 100
```