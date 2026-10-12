# The #if and #elif Preprocessor Statements

The `#` preprocessor statement offers a more general way of controlling conditional compilation. The `#` statement can be used to test whether a constant expression evaluates to nonzero. If the result of the expression is nonzero, subsequent lines up to a `#` , `#` , or `#` are processed; otherwise, they are skipped. As an example of how this might be used, assume you define the name `O` , which is set to `1` if the operating system is Macintosh OS, to `2` if the operating system is Windows, to `3` if the operating system is Linux, and so on. You could write a sequence of statements to conditionally compile statements based upon the value of `O` as follows:

Click here to view code image

```
```
#       
#       
#       
#       
#       
```
```

With most compilers, you can assign a value to the name `O` on the command line using the `--` option discussed earlier. The command line

```
```
g
```

```

compiles `p` with the name `O` defined as `2`. This causes the program to be compiled to run under Windows.

The special operator

```
```
d
```
```

can also be used in `#` statements. The set of preprocessor statements

```
```
#       
#       
```
```

and

```
```
#       
#       
```
```

does the same thing. The statements

Click here to view code image

```
```
#       
#       
#       
#       
#       
```
```

define `B` as " if either `W` or `W` is defined and as " otherwise.

# The #undef Statement

On some occasions, you might need to cause a defined name to become undefined. This is done with the `#` statement. To remove the definition of a particular n , you write