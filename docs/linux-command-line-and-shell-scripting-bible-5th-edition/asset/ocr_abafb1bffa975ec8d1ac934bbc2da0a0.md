# Part III: Advanced Shell Scripting

```
> This is another inserted line.
> ' data6.txt
This is an inserted line.
This is another inserted line.
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
```

Both of the specified lines are added to the data stream.

# Changing lines

The change (`c`) command allows you to change the contents of an entire line of text in the data stream. It works the same way as the insert and append commands in that you must specify the new line separately from the rest of the `sed` command:

```
$ sed '2c\
> This is a changed line of text.
> ' data6.txt
This is line number 1.
This is a changed line of text.
This is the 3rd line.
This is the 4th line.
$
```

In the preceding example, the `sed` editor changes the text in line number 2. You can also use a text pattern for the address:

```
$ sed '/3rd line/c\
> This is a changed line of text.
> ' data6.txt
This is line number 1.
This is line number 2.
This is a changed line of text.
This is the 4th line.
$
```

The text pattern change (`c`) command changes any line of text in the data stream that it matches.

```
$ cat data8.txt
I have 2 Infinity Stones
I need 4 more Infinity Stones
I have 6 Infinity Stones!
I need 4 Infinity Stones
I have 6 Infinity Stones...
I want 1 more Infinity Stone
$

$ sed '/have 6 Infinity Stones/c\
> Snap! This is changed line of text.
> ' data8.txt
```