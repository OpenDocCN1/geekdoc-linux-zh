
## 7.6.5 Printing the Values of Variables: The echo Command

The echo command prints its arguments to standard output and is used primarily in Bourne and C shells. The Korn shell has a built-in print command. There are different versions of the echo command; for example, the Berkeley (BSD) echo is different from the System V echo. Unless you specify a full pathname, you will use the built-in version of the echo command. The built-in version will reflect the version of UNIX you are using. The System V echo allows the use of numerous escape sequences, whereas the BSD version does not. Table 7.4 lists the BSD echo option and escape sequences.

### Table 7.4 BSD echo Option and System V Escape Sequences

| Option | Meaning |
|---|---|
| BSD | |
| -n | Suppress newline at the end of a line of output |
| System V | |
| \b | Backspace |
| \c | Print the line without a newline |
| \f | Form feed |
| \n | Newline |
| \r | Return |
| \t | Tab |
| \v | Vertical tab |
| \\ | Backslash |

### EXAMPLE 7.24

```
1 $ echo The username is $LOGNAME.
   The username is ellie.
2 $ echo "\tHello there\c"   # System V
   Hello there$
3 $ echo -n "Hello there"   # BSD
   Hello there$
```

### EXPLANATION

- 1. The echo command prints its arguments to the screen. Variable substitution is performed by the shell before the echo command is executed.
- 2. The System V version of the echo command supports escape sequences similar to those of the C programming language. The $ is the shell prompt.
- 3. The -n option to the echo command indicates that the BSD version of the echo command is being used. The line is printed without the newline. The escape sequences are not supported by this version of echo.

## 7.6.6 Variable Expansion Modifiers

Variables can be tested and modified by using special modifiers. The modifier provides a shortcut conditional test to check if a variable has been set, and then assigns a value to the variable based on the outcome of the test. See Table 7.5 for a list of Bourne shell variable modifiers.

### Table 7.5 Bourne Shell Variable Modifiers

| Modifier | Value |
|---|---|
| ${variable:-word} | If variable is set and is non-null, substitute its value; otherwise, substitute word. |
| ${variable:=word} | If variable is set or is non-null, substitute its value; otherwise, set it to word. The value of variable is substituted permanently. Positional parameters may not be assigned in this way. |
| ${variable:+word} | If parameter is set and is non-null, substitute word; otherwise, substitute nothing. |
| ${variable:?word} | If variable is set and is non-null, substitute its value; otherwise, print word and exit from the shell. If word is omitted, the message parameter null or not set is printed. |

Using the colon with any of the modifiers (-, =, +, ?) checks whether the variable is not set or is null; without the colon, a variable set to null is considered to be set.

### EXAMPLE 7.25

```
(Assigning temporary default values)
1  $ fruit=peach
2  $ echo ${fruit:-plum}
   peach
3  $ echo ${newfruit:-apple}
   apple
4  $ echo $newfruit

5  $ echo $EDITOR      # More realistic example

6  $ echo ${EDITOR:-/bin/vi}
   /bin/vi
7  $ echo $EDITOR

8  $ name=
   $ echo ${name:-Joe}

9  $ echo ${name:-Joe}
   Joe
```

### EXPLANATION

- 1 The variable fruit is assigned the value peach.
- 2 The special modifier will check to see if the variable fruit has been set. If it has, the value is printed; if not, plus is substituted for fruit and its value is printed.
- 3 The variable newfruit has not been set. The value apple will be temporarily substituted for newfruit.
- 4 The setting was only temporary. The variable newfruit is not set.
- 5 The variable EDITOR has not been set.
- 6 The :- modifier substitutes EDITOR with /bin/vi.
- 7 The EDITOR was never set. Nothing prints.
- 8 The variable name is set to null. By not prefixing the modifier with a colon, the variable is considered to be set, even if to null, and the new value Joe is not assigned to name.
- 9 The colon causes the modifier to check that a variable is either not set or is set to null. In either case, the value Joe will be substituted for name.

### EXAMPLE 7.26

(Assigning permanent default values)

```
1 $ name=
2 $ echo ${name:=Patty}
Patty
3 $ echo $name
Patty
4 $ echo ${EDITOR:=/bin/vi}
/bin/vi
5 $ echo $EDITOR
/bin/vi
```

### EXPLANATION

- 1 The variable name is assigned the value null.
- 2 The special modifier := will check to see if the variable name has been set. If it has been set, it will not be changed; if it is either null or not set, it will be assigned the value to the right of the equal sign. Patty is assigned to name because the variable is set to null. The setting is permanent.
- 3 The variable name still contains the value Patty.
- 4 The value of the variable EDITOR is set to /bin/vi.
- 5 The value of the variable EDITOR is displayed.
