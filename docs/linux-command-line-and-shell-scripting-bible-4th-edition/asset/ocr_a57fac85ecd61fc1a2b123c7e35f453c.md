# Working with Data Files

When you have a large amount of data, it's often difficult to handle the information and make it useful. As you saw with the du command in the previous section, it's easy to get data overload when working with system commands.

The Linux system provides several command-line tools to help you manage large amounts of data. This section covers the basic commands that every system administrator — as well as any everyday Linux user — should know to make their lives easier.

# Sorting data

One popular function that comes in handy when working with large amounts of data is the sort command. The sort command does what it says — it sorts data.

By default, the sort command sorts the data lines in a text file using standard sorting rules for the language you specify as the default for the session:

```
$ cat file1
one
two
three
four
five
$ sort file1
five
four
one
three
two
$
```

Pretty simple. However, things aren't always as easy as they appear. Take a look at this example:

```
$ cat file2
1
2
100
45
```