Now we'll use the print function in awk to plug the words from each input line into a template, like this:

```
awk '(print "Hit the",$1,"with your",$2)' words.data
Hit the nail with your hammer
Hit the pedal with your foot
Hit the clown with your pie
```

Say some of the data in your input file is numeric, as in the grades.data file shown here:

```
Rogers 87 100 95
Lambchop 66 89 76
Barney 12 36 27
```

You can perform calculations like this:

```
awk '(print "Avg for",$1,"is",($2+$3+$4)/3)' grades.data
Avg for Rogers is 94
Avg for Lambchop is 77
Avg for Barney is 25
```

So far, we haven't specified any value for pattern in these examples, but if you want to exclude lines from being processed, you can enter something like this:

```
awk '/clown/ {print "See the",$2,"at the",$3}' words.data
See the clown at the circus
```

Here, we told awk to consider only the input lines that start with clown. Note also that there is no space between the pattern and the print specifier. If you put a space there, awk will think the input file is '{print and will not work. But all this is just the tip of the awk iceberg—entire books have been written on this command. If you are a programmer, try the man awk command.

# THE FIND COMMAND

The find command locates files in many different ways. Unlike the rest of the commands in this chapter, find does not look at the contents of a file—it only helps you find files that meet certain criteria, such as name, size, age, and type. The general form of the find command is