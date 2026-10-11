type in the filename as if it were a regular command. When a shell script is written, it creates a special array variable, `argv`, that contains the elements of its arguments.

# ## Command-Line Shortcuts

The C shell provides some shortcuts by means of the keyboard. If you type the `Esc` key preceded by a partial command or filename, the C shell will attempt to complete the filename. However, if you have more than one filename that matches, the common letters are completed and the C shell will beep a signal. In the C shell, you need to run the command `set filec` to enable file-name completion. The `Ctrl+K` key will erase the previous word.

# ## Variable Control Structures

The C shell uses most of the control structures found in the Bourne shell but the syntax is somewhat different. The effects, however, are the same. Refer to Chapter 18, “The Bourne Shell,” and Chapter 19, “The Korn Shell,” for more comprehensive descriptions of the control structures.

The syntax for the `if` control structure is as follows:

```
```
if (expression) simple-command
```
```

Because the `if` structure works only with simple commands, do not use lists of commands or pipes. Those require the `if...then` control structure to execute.

The `goto` built-in transfers control to the statement that begins with `label`. Here is an example of a `goto` statement:

```
```
$ cat goto_1
#!/bin/csh

#  test for 2 args

if ($#argv == 2) goto myargs
echo 'Usage: goto_1 arg1 arg2'
exit 1
myargs
```
```

The `if...then...else` control structure has three separate forms:

Form 1

```
```
if (expression) then
    commands
endif
```
```

Form 2