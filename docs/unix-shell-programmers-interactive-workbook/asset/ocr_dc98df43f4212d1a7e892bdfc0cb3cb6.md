# 490 Lab : The read and printf Commands

There is a lot of material in here, so let's summarize the main features of the function before learning about how the individual parts work:

+   1. There is a while loop at the heart of this function that uses the value returned by a read command to decide whether to continue executing.
2. The value of a variable named IFS is saved when the function starts and restored to its original value before the function exits. The value of IFS is changed inside the loop and in two different places inside the loop.
3. Inside the loop, the value of the input buffer from the first read is read again by piping the output of a print command to a second read command.

![](bbox=[0.148, 0.365, 0.246, 0.445])

A read command has an exit status of false if it tries to read beyond the end of the input file and true otherwise, so "while...done" is a common programming idiom for reading all the lines in a file.

Now run the following two command lines to compare the output of mywc and the version of wc that is available on your computer:

```
wc < wtest
mywc < wtest
```

e) How does the output of these two commands compare?

The shell uses the variable IFS as its Internal Field Separator, the character(s) it uses for doing token splitting. By default, it is the "whitespace" characters, space, tab, and new line, but you can change it if you wish. In particular, if you give IFS an empty string as its value, the shell will not do field splitting when executing read commands.

![](bbox=[0.148, 0.81, 0.246, 0.89])

The shell also uses IFS when it does field splitting during command substitution, parameter expansion, and for the words after in, for, and select.