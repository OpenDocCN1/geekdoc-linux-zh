# Quoting with the :x Modifier.

If you are creating an array and any of the words in the list contain metacharacters, :x prevents the shell from interpreting the metacharacters when performing variable substitution.

# EXAMPLE 9.60

```
1 % set things = ".c a?? file[1-5]"
% echo $things
.c a?? file[1-5]
2 % set newthings = ( $things )
set: No match.
3 % set newthings = ( $things:x )
4 % echo $newthings
3
5 % echo "$newthings[1] $newthings[2] $newthings[3]"
.c a?? file[1-5]
6 % grep $newthings[2]:q filex
The question marks in a?? would be used for filename expansion
it is not quoted
```

# EXPLANATION

+   1 The variable things is assigned a string. Each string contains a wildcard. The number of elements in the variable is one, one string.
+   2 When attempting to create an array out of the string things, the C shell tries to expand the wildcard characters to perform filename substitution within things and produces a No match.
+   3 The :x extension prevents the shell from expanding the wildcards in the things variable.
+   4 The array newthings consists of three elements.
+   5 To print the elements of the array, they must be quoted or, again, the shell will try to expand the wildcards.
+   6 The :q quotes the variable just as though the variable were surrounded by double quotes. The grep program will print any lines containing the pattern a?? in file filex.

# 9.13 New Features of the Interactive TC Shell

The TC shell is a public domain enhanced version of its predecessor, the Berkeley UNIX C shell. If you are using Linux, you will have this available to you rather than the traditional C shell. Although tcsh is included in most Linux distributions, it can also be ported to a number of other operating systems, including Solaris, Windows NT, HP-UX, QNX, and more. There are an assortment of new features in the TC shell. The remainder of this chapter covers these additional features, most of them shortcuts, including command-line editing, fancy prompts, programmable completions (filenames, commands, and variables), spelling correction, and so forth.