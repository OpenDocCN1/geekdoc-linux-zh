Then issue the following command:

```
$ chmod +x testif.sh; ./testif.sh
```

The `chmod` command sets execution permissions for the shell script; in other words, it makes the script executable. The next chapter, on file systems, contains detailed information on setting various permissions for files. The `./testif.sh` command executes the script. We see the following output:

```
x and y are not equal
```

As an aside, it is not necessary to type a shell script into a file. We could type it in at the command line itself:

```
$ x=10; y=5
$ if [ "$x" -eq "$y" ]
> then
> echo x and y are equal
> else
> echo x and y are not equal
> fi
x and y are not equal
$
```

> Note that the shell prompt changes into a $ > $ sign since the shell expects more input.

The if then ... else ... fi statement has the following syntax:

```
if expression
  then
    statement 1
    statement 2
    ...
    statement n
  else
    statement 1'
    statement 2'
    ...
    statement n'
fi
```

If the value of the expression turns out to be true, the statements from statement 1 to statement n are executed. If it evaluates to false, the statements from statement 1' to statement n' are executed. The expression can be formed using operators, in this case the `-eq` operator. The -eq operator tests for equality of numbers. It evaluates to true if two numbers are equal and false if they are not.