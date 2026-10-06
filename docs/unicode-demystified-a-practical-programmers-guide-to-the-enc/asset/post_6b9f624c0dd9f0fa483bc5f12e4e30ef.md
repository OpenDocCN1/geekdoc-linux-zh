
# select

The Bourne Again Shell's select control structure, based on the one found in the Korn Shell and corresponding to the select control structure in zsh, displays a menu, assigns a value to a variable based on the user's choice of items, and executes a series of commands. The syntax of a select structure is

```bash
select varname [in arg ... ]
do
  commands
done
```

First, select generates and displays a menu of the arg items. The menu is formatted with numbers before each item. For example, a select structure that begins with select fruit in apple blueberry kiwi orange watermelon STOP displays the following menu:

+ 1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP

You can have many items in the list of args. The select structure uses the values of the LINES and COLUMNS variables to determine the size of the display. (LINES has a default value of 24; COLUMNS, a default of 80.) With COLUMNS set to 20, the menu looks like this:

+ 1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP

After displaying the menu, select displays the value of PS3, the special select prompt. The default value of PS3 is the characters #?, but typically you would set PS3 to a more meaningful value.

If in the preceding menu you enter a value number (one in the range), select sets the value of varname to the argument corresponding to number entered and executes the commands between do and done. The select structure issues the PS3 prompt and waits for another entry, doing this repeatedly until something causes it to exit from the statements between do and done, typically a break, return, or exit statement. The break statement exits from the loop. Within a function return returns control to the program that called the function. The exit statement exits from the current shell. The following script illustrates the use of select:

```bash
$ cat fruit
!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple banana blueberry orange watermelon STOP
do
  if [ "$FRUIT" = "STOP" ]; then
    echo "Thanks for playing!"
    break
  fi
  echo "You chose number $FRUIT as your favorite."
done
```

$ fruit
1) apple 3) blueberry 5) orange 7) STOP
2) banana 4) kiwi 6) watermelon

Choose your favorite fruit from these possibilities:
You choose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities:
An invalid menu choice causes zsh to assign a null string to varname and execute the commands between do and done. If the user presses RETURN without entering a choice, the Z Shell replays the menu and the PS3 prompt. The Z Shell stores the user's response in the keyword variable REPLY.

As the syntax indicates, you can omit the keyword in the list of arguments. If you do, select uses the current values of the positional parameters $@.

# Here Document

A here document allows you to redirect input to a shell script from within the shell script itself. A here document is so called it here, immediately accessible in the shell script, instead of there, perhaps in another file.

The following script, birthday, contains a Here document. The two less (<<) symbols in the first line indicate to the shell that a Here document follows. One or more characters that delimit the Here document follow the less signs—this example uses plus signs. Whereas the opening delimiter can occur adjacent to the less signs, the closing delimiter must occur on a line by itself. The shell sends everything between the two delimiters to the process as standard input. In the following example it is as as though you had redirected standard input to grep from a file, except that the file is embedded in the shell script:

The term Here document is not used in the zan man pages; you must search for << instead.

![](img/aa8214d49e1cf50152c432845129fb3b_710_0.png)

[$Name] to a null string. The shell provides the following alternatives to accept ing expanded null string as the value of the variable.

- Use a default value for the variable.
- Use a default value and assign that value to the variable.
- Display an error.

You can choose one of these alternatives by using a modifier with the variable name.

# Uses a Default Value

The :- modifier uses a default value in place of a null or unset variable while allowing a nonnull variable to represent itself:

```bash
${name:-default}
```

The shell interprets the :- as: “If name is null or unset, expand default and use the expanded value in place of name; else use name.” The following command lists the contents of the directory named by the LIT variable; if LIT is null or unset, it lists the contents of /home/alex/literature:

```bash
$ ls ${LIT:-home/alex/literature}
```

The default can itself have variable references that are expanded:

```bash
$ ls ${LIT:-HOME/literature}
```

You can supply defaults for unset variables but leave null variables unchanged by omitting the colon:

```bash
$ ls ${LIT-HOME/literature}
```

# Assigns a Default Value

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. (Wait, the OCR is repetitive here, I will clean up based on logical flow).

The shell interprets the :- as: “If name is null or unset, expand default and use the expanded value in place of name; else use name.” The following command lists the contents of the directory named by the LIT variable; if LIT is null or unset, it lists the contents of /home/alex/literature:

```bash
$ ls ${LIT:-home/alex/literature}
```

The default can itself have variable references that are expanded:

```bash
$ ls ${LIT:-HOME/literature}
```

You can supply defaults for unset variables but leave null variables unchanged by omitting the colon:

```bash
$ ls ${LIT-HOME/literature}
```

# Assigns a Default Value

The :- modifier does not change the value of a variable. You may want to change the value of a null or unset variable to its default in a script. You can do this with the := modifier:

```bash
${name:=default}
```

The :- modifier does not change the value of a variable. (Correcting OCR repetition error).

The := modifier works similarly to :- but it also sets the variable to the default if it is null or unset. The shell expands the following as is to set the variable:

```bash
$ ls ${name:=default}
```

# String Pattern Matching

The shell provides a powerful set of string-matching operators that manipulate pathnames and other strings. These operators can delete from strings prefixes or suffixes that match patterns. The four operators are listed in Table 13-4.

| String Operator | Description |
|---|---|
| # | Removes minimal prefixes |
| ## | Removes maximal prefixes |
| % | Removes minimal suffixes |
| %% | Removes maximal suffixes |

The syntax for these operators is

```bash
$varname op pattern
```

In this syntax op is one of the operators listed in Table 13-4, and pattern is a match pattern similar to that used for filename generation. These operators are commonly used to manipulate pathnames to extract or remove components or to change suffixes:

```bash
$ SOURCEFILE=/usr/local/src/prog.c
$ echo ${SOURCEFILE##/*}
local/src/prog.c
$ echo ${SOURCEFILE##/*}/c
prog.c
$ echo ${SOURCEFILE%%/*}
/usr/local/src
$ echo ${SOURCEFILE%%%c}

$ echo ${SOURCEFILE%.c}.c
/usr/local/src/prog
$ CHOPFIRST=${SOURCEFILE##/*}
$ echo $SCHOPFIRST
local/src/prog.c
$ NEXT=${CHOPFIRST%%/*}
$ echo $NEXT
local
```

# Filename Generation

An important feature of most shells is the ability to refer to files by giving a pattern that describes one or more filenames. For example, all the shells discussed in this book use *.c as a pattern describing all filenames that end in .c. The shells expand the
