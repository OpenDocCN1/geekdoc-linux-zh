# 244 Chapter 11 More on Parameters

```
e
$ echo ${var#test}    Remove test from left
case
$ echo ${var#teas}      No match
testcase
$
```

There are many practical uses for these constructs. For example, the following tests to see whether the filename stored inside the variable file ends in the two characters .o:

```
if [ ${file.*o ] = $file ]; then
  # file ends in .o
  ...
```

Another example, here's a shell program that works just like the Unix system's basename command:

```
$ cat my
echo ${1##*/}
$
```

The program displays its argument with all the characters to the last / removed:

```
$ basename /usr/spool/uucpublic
uucpublic
$ basename $HOME
steve
$ basename memos
memos
$
```

But wait, there are more constructs:

# ${#variable}

Need to figure out how many characters are stored in a variable? That's just what this construct offers:

```
$ text='The shell'
$ echo ${#text}
9
$
```

> Tip
Each of the parameter constructs described in this chapter is summarized in Appendix A,
Table A.3.