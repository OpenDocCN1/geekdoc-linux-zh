produces the output

```
219 hosts
18 users
237 total
```

# Combining Options

The options to wc can be grouped together and specified in any order. For example, to obtain a count of the number of lines and words in the file fruits, we can use any of the following commands:

```
$ wc -w -l fruits
$ wc -l -w fruits
$ wc -lw fruits
$ wc -lw fruits
```

The output from each of these commands is identical:

```
8 18 fruits
```

The output lists the number of words in the files, followed by the number of lines in the file. The filename is specified at the end of the line. When multiple files are specified, the information for each file is listed along with the appropriate total values.

# Manipulating Files

In the preceding sections, you looked at listing files and viewing their content. In this section, you will look at copying, renaming, and removing files using the cp, mv, and rm commands.

# Copying Files (cp)

The cp command (short for copy) is used to make a copy of a file. The basic syntax of the command is

```
cp src dest
```