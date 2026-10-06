The POSIX shell does not support the typeset keyword or the zsh's declare keyword.

The POSIX shell does not support the select command.

The POSIX shell does not support the two-argument form of the cd command.

The POSIX shell does not automatically define and maintain the value of the PWD environment variable.

The POSIX shell has a different syntax for doing integer arithmetic. It does not use the let keyword. Arithmetic expressions are initiated by the symbols (($ and are terminated by )). Within the parentheses you must refer to shell variables by using a $ sign. For example, the following brief POSIX shell dialog will display the value 7:

```
$ x=3
$ y=4
$ z=$($x + $y)
$ echo $z
```

The equivalent zsh or ksh sequence would be

```
$ x=3
$ y=4
$ let z="x + y"
$ echo $z
```

+   In zsh or ksh you can also use double parentheses for arithmetic instead of let, but the syntax is different. Two ways to write the let statement in zsh or ksh are

```
z=$((x + y))
```

and

```
((z=x + y))
```

+   You can define shell functions in the POSIX shell, just as you can in zsh or ksh. However, both zsh and ksh support multiple syntaxes to define functions. The POSIX shell supports only one of these; it does not support the function keyword, and it requires braces ({}) even if the function body is a single command. The following function definition style is valid in the POSIX shell, zsh, and ksh: