
# String Variables

allow numeric strings but treat them as text strings, and the @ built-in works with numeric variables. The C shell recognizes the $ as a variable when it precedes a word but will not substitute if the $ is preceded by a \ . If, however, you put a variable within double quotation marks, a substitution will occur even with a quoted dollar sign.

> **TIP** Using the setenv built-in is similar to using the export built-in in the Bourne shell. It assigns a value to a variable and places it in the calling environment of the child processes.

Once the C shell identifies the value of a variable, it substitutes the value when it finds the variable on a command line or in a script.

The C shell declares and assigns string variables somewhat differently than the Bourne or Korn shell does. String variables in the C shell are set by the `set` or `setenv` built-in. Unlike the other shells, the C shell allows space around the equal signs (=). The following example displays the use of the `set` built-in:

```
% set file = Tanya
% echo $file
Tanya

% set

argv	(	)
	home/barrie
file	Tanya
path	(	/usr/bin)
prompt		%
shell	/bin/csh
status	0
term	vtx400
user	barrie
```

The variable `file` is declared on the first line. It is then displayed on the second line. The `set` command, without arguments, displays a list of the shell's local variables and their values. If you give a `set` command and the name of a variable that has no value, the variable will assume a null string. You can use the `unset` built-in to remove a declared variable in the same way. The `setenv` built-in separates the variable name from the string by one or more spaces and does not use an equal sign (=).

# Numeric Variables

In the C shell, the `@` built-in assigns a value to a numeric variable. The `@` built-in and the `@` set built-in are used similarly, although the `@` built-in must have a numeric argument. Use of the `@` command without arguments produces a list of all shell variables, just as the `set` command does.

**TIP**
If you give a nonnumeric value to the `@` built-in, you will get an error message!

The `@` built-in evaluates most of the operators found in the C programming language. Table 20.3 includes a list of expressions evaluated by the `@` built-in.

**TABLE 20.3: NUMERIC EXPRESSIONS**

| Expression | Function |
|:-----------|:---------|
| + | Add |
| - | Subtract |
| * | Multiply |
| / | Divide |
| % | Remainder |
| ( ) | Change evaluation order |
| ~ | One's complement |
| ! | Logical negation |
| ++ | Postfix increment |
| -- | Postfix decrement |
| >> | Shift right |
| << | Shift left |
| && | Logical AND |
| \|\| | Logical OR |
| & | AND |
| ^ | XOR |
| \| | OR inclusive |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |
| != | Not equal to, compare |
| == | Equal to, compare |

There are some simple rules in the use of expressions. The C shell will evaluate a missing argument as 0. All results will be decimal numbers. Each element of an expression must be separated from others with a space with the exception of &, (<or>), and |. Operators act on numeric arguments except for != and ==. The postfix increment (++) and decrement (--) can be used only in an expression that contains a single variable name.

## Numeric Arrays

The `set` built-in is used to declare an array of numeric variables before using the `@` command to assign values. When you're working with arrays, you can use the `set` built-in to assign values to their elements as simply as you can assign a value to a single numeric value. You must, however, specify the element or index of the array. Here is the syntax:

```
@ <variable-name>[index]operator expression
```

The index must be either a numeric constant or a variable, not an expression. The first element has the index of 1.

If your specified index is too large for the array, you will get the error message `@: Subscript out of range`. Even though a numeric array behaves as simple numeric variables, you must use `set` to declare it. This brief example shows how to set the array:

```
% set speeds = (0 0 0 0 0)
% @ speeds[2] = 15
% @ speeds[3] = ($speeds[2] + 4)
% echo $speeds[3]
19
```

## Switch Variables

The C shell has variables that act as switches with no significant values. A declared variable causes the shell to take action and an undeclared variable does not. The variables can be set in the `.cshrc` file, on a command line, or in a script. The `echo` variable can be set, or if you call `csh` with the `-x` option, `csh` sets the variable.

Once `echo` is declared, the shell will display each command before it executes them. The `ignoreeof` variable is a special tool that keeps you from exiting the shell accidentally with `Ctrl+D`. Once this variable is set, you must use `exit` or `logout` to exit the shell.

The `noclobber` variable is another safeguard that prevents you from accidentally overwriting a file when you redirect output, although you can still append to it. It will not let you create a file when you append output to a nonexistent file. If you want to override `noclobber`, you can append an exclamation point to the symbol used for redirecting the output (`>!` and `>>!`).

The `x>ofile` command redirects standard output from `x` to `opfile` and will overwrite a file called `opfile` if it exists, but only if you do not declare the `noclobber` variable. If you do declare the `noclobber` variable, the `x>opfile` command redirects standard output from process `x` to `opfile`. It will display an error message if `opfile` exists and it will not overwrite the file.

By the same token, if the `x>>opfile` command is given and not declared, it will redirect standard output from process `x` to `opfile`. It will append new output to the end of `opfile` if it exists, or it will create `opfile` if it does not. If the `x>>noclobber` is declared, it will redirect standard output from process `x` to `opfile` and append new output to the end if the file exists. The shell will give an error message if `opfile` does not exist and will not create the file.

The `noglob` variable, when declared, does not expand ambiguous filenames. It allows you to use `*`, `?`, `~`, and `[ ]` in a script or on the command line without quoting. The `nomatch` variable, when set, causes the shell to pass an ambiguous reference that doesn't match a filename to the command being called. The C shell will not expand the file reference. If not set, `nomatch` causes the shell to generate a `No match` error message and the command is not executed.

The `notify` variable, when set, causes the shell to send a message to your terminal letting you know that a background job has finished. Finally, the `verbose` variable is declared by the C shell when you call the shell with the `-v` option. You can also declare it by using the `set` command. The `verbose` argument will display each command after a history substitution.

## Creating Scripts

Writing and executing scripts in the C shell is similar to the same activities in both the Bourne and Korn shells. The differences lie in the methods of declaring values and assigning them to variables. The syntax for this is as follows (unlike in sh, space on either side of the equal sign are optional in csh):

```
set <variable>=value
```

Many of the control structures have a different syntax. You can run scripts while using any one of the shells, but the first line must read `#!/bin/csh`. If the first character is anything other than `#`, `csh` will call `sh` to execute the script.

You should give yourself execution permission with the `chmod u+x <filename>` command. The script file can contain any commands that can be typed in. You can type in the filename as if it were a regular command. When a shell script is written, it creates a special array variable, `argv`, that contains the elements of its arguments.

## Command-Line Shortcuts

The C shell provides some shortcuts by means of the keyboard. If you type the `Esc` key preceded by a partial command or filename, the C shell will attempt to complete the filename. However, if you have more than one filename that matches, the common letters are completed and the C shell will beep a signal. In the C shell, you need to run the command `set filec` to enable file-name completion. The `Ctrl+K` key will erase the previous word.

## Variable Control Structures

The C shell uses most of the control structures found in the Bourne shell but the syntax is somewhat different. The effects, however, are the same. Refer to Chapter 18, “The Bourne Shell,” and Chapter 19, “The Korn Shell,” for more comprehensive descriptions of the control structures.

The syntax for the `if` control structure is as follows:

```
if (expression) simple-command
```

Because the `if` structure works only with simple commands, do not use lists of commands or pipes. Those require the `if...then` control structure to execute.

The `goto` built-in transfers control to the statement that begins with `label`. Here is an example of a `goto` statement:

```
$ cat goto_1
#!/bin/csh

#  test for 2 args

if ($#argv == 2) goto myargs
echo 'Usage: goto_1 arg1 arg2'
exit 1
myargs
```

The `if...then...else` control structure has three separate forms:

Form 1

```
if (expression) then
    commands
endif
```

Form 2
