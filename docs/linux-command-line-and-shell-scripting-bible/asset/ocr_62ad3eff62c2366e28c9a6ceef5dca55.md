# The foreach statement

The tcsh shell doesn't use the for statement, but it does contain a foreach statement for iterating the values in an array variable or a list. The format of the foreach statement is:

```
foreach varl (wordlist)
  statements
end
```

The parameter wordlist can be an array variable, or a list of values separated by spaces:

```
$ cat test7
#!/bin/tcsh
# testing the foreach statement

echo "The directories in your PATH are:"
foreach dir ($path)
  echo $dir
end
$ ./test7
The directories in your PATH are:
/usr/local/bin
/bin
/usr/bin
/usr/X11R6/bin
$
```

This is a great way to iterate through array variables, especially if you don't know how many elements are in the array.

# The while statement

The while statement in tcsh allows you to loop until a specified expression evaluates to a FALSE condition. The format of the while command is:

```
while (expression)
  statements
end
```

The expression used in the while statement is the same format as for the if statement, as well as the special =~ and !~ string comparison symbols:

```
$ cat test8
#!/bin/tcsh
# determining the factorial of a value
```

```
set value=$1
set factorial = 1
```