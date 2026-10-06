In a situation where the fields are separated by tabs, you should use the -f option to
cut instead:

```
$ cut -f1 phonebook
Alice Cheba
Barbara Swingle
Jeff Goldberg
Liz Stachiw
Susan Goldino
Tony Iannino
$
```

Recall that you don't have to specify the delimiter character with the -d option because
cut defaults to a tab character delimiter.

How do you know in advance whether fields are delimited by blanks or tabs? One way is to
out out is by trial and error, as shown previously. Another way is to type the command
sed -n 1 file

at your terminal. If a tab character separates the fields, \t will be displayed instead of the tab:

```
$ sed -n 1 phonebook
Alice Cheba\t973-555-2015
Barbara Swingle\t201-555-9257
Jeff Goldberg\t201-555-3378
Liz Stachiw\t212-555-2298
Susan Goldberg\t201-555-7776
Tony Iannino\t973-555-1295
$
```

The output verifies that each name is separated from each phone number by a tab character.
The stream editor sed is covered in more detail a later in this chapter.

# paste

The paste command is the inverse of cut: Instead of breaking lines apart, it puts them
together. The general format of the paste command is

```
paste files
```

where corresponding lines from each of the specified files are "pasted" or merged together
form single lines that are written to standard output. The dash character - can also be
used in the files sequence to specify that input is from standard input.

Suppose that you have a list of names in a file called names:

```
$ cat names
Tony
Emanuel
Lucy
```