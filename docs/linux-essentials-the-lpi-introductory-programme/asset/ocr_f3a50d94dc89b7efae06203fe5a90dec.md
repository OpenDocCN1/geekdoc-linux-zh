is equivalent to

```
```
$ . assignment
```
```

Like program files for external commands, the files to be read using source or . are searched in the directories given by the PATH variable.

# ## 9.6 The Shell As A Programming Language

Being able to execute shell commands from a file is a good thing, to be sure. However, it is even better to be able to structure these shell commands such that they do not have to do the same thing every time, but---for example---can obtain command-line parameters. The advantages are obvious: In often-used procedures you save a lot of tedious typing, and in seldom-used procedures you can avoid mistakes that might creep in because you accidentally leave out some important step. We do not have space here for a full explanation of the shell as a programming language, but fortunately there is enough room for a few brief examples.

**Command-line parameters** When you pass command-line parameters to a shell script, the shell makes them available in the variables $1, $2, .... Consider the following example:

```
```
$ cat hello
#!/bin/bash
echo Hello $1, are you free $2?
$ ./hello Joe today
Hello Joe, are you free today?
$ ./hello Sue tomorrow
Hello Sue, are you free tomorrow?
```
```

The $* contains all parameters at once, and the number of parameters is in $#:

```
```
$ cat parameter
#!/bin/bash
echo $# parameters: $*
$ ./parameter
0 parameters:
$ ./parameter dog
1 parameters: dog
$ ./parameter dog cat mouse tree
4 parameters: dog cat mouse tree
```
```

**Loops** The for command lets you construct loops that iterate over a list of words (separated by white space):

```
```
$ for i in 1 2 3
> do
>     echo And $i!
> done
And 1!
And 2!
And 3!
```
```

Here, the i variable assumes each of the listed values in turn as the commands between do and done are executed.

This is even more fun if the words are taken from a variable: