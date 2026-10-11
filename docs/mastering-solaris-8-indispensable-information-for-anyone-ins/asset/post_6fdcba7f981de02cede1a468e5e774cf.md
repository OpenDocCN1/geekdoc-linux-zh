
## The Korn shell performs command substitution by using a string within parentheses. The string is treated as a command and is executed within a subshell. The text and parentheses will be replaced by standard output of the command. Here is an example of command substitution:

```bash
#!/bin/ksh
ls -l $(find . -name README -print)
```

When double sets of parentheses are used together, ksh treats them as enclosures for arithmetic expressions. You can use an arithmetic expression enclosed between `(( ))` and preceded by `$` in place of any numeric value. See the following example:

```bash
#!/bin/ksh
echo "There are $((52*7)) days in the year."
```

The Korn shell does not expand the filename within the `$(( ))`, so it is easy to use operators such as the asterisk for mathematical expressions. Because these operators signify an arithmetic expression, if you want to use a parenthesized subshell within `$()`, you must place a space between the `$(` and the next `(`.

The enclosed brackets `[ ]` are used synonymously with the `test` built-in or utility.

> **TIP** To find out whether a command is a built-in or a system utility in ksh, use the built-in `type <command>`.

The Korn shell has more built-ins than either the Bourne or C shell, and most were covered in the two previous chapters. In this chapter, built-ins that were not covered previously will be discussed. The Korn shell includes built-ins for option processing, control flow, input/output, and control of the user’s environment.

The Korn shell commands that are not simple are referred to as control structures or control flow commands. Control flow commands are used for shell programming and may be useful in interactive work. Korn shell control structures that control the process flow are `if...then`, `for...in`, `while`, `case`, `until`, and `select`. You can use the same syntax you use in the Bourne shell for these test commands. You can also use the `test` built-in, the `[[` built-in, or any other command as the test command. The syntax for the `[[` built-in is as follows:

```bash
[[ <conditions> ]]
```

The result for this built-in is a return status, just like the results for the `test` built-in. The Bourne shell uses `-a` as a logical AND with two expressions, whereas the Korn shell uses `&&` for the same effect. The `sh` also uses `-o` for logical OR for two expressions while the Korn shell uses `||`. Table 19.4 lists more Korn shell test options.

### TABLE 19.4: KORN SHELL TEST OPTIONS

| Test | Result |
| :--- | :--- |
| `-o <option>` | True if the option named `<option>` is set or on |
| `(<expression>)` | True if `<expression>` is true |
| `! <expression>` | True if `<expression>` is false |
| `<expression1> && <expression2>` | True if `<expression1>` and `<expression2>` are both true |
| `<expression1> || <expression2>` | True if either `<expression1>` or `<expression2>` is true |

The `[[` will probably be used the most as the test command for control structures. It also allows an arithmetic test when inside double parentheses instead of square brackets. The double parentheses are not preceded by a `$` sign. This test yields only a true or false. All of the logical Korn arithmetic operators may be used. Consider the following examples:

```bash
if [[ $(( $(#FORM) + 21 )) -lt $[PWD] ]]
then
...
fi
```

or

```bash
if (( $(#FORM) + 21 )) < $[PWD] )
then
...
fi
```

or

```bash
if (( $(#FORM) + 21 < $[PWD] ))
then
...
fi
```

The comparison operators that are similar to arithmetic operators may be familiar to you. The Korn shell treats the tokens `[[` and `((` as special symbols instead of commands. You do not need to follow them with a SPACE.

## Shell Variable Expansion

The Korn shell expands all the shell variables used by the Bourne shell and adds its own to the mix. You may want to review the discussion of variable expansion in the previous two chapters. Many of the conventions will be the same. The Korn shell expands an unset name to a null string just as the Bourne shell (`sh`) does.

The same modifiers (`=`, `:`, `?`) are used to assign default values. The Korn shell makes use of a set of pattern-matching string operators used to manipulate path names and other strings. You can delete prefixes or suffixes that match patterns from strings. Table 19.5 displays these pattern-matching operators.

### TABLE 19.5: STRING OPERATORS

| String Operator | Description |
| :--- | :--- |
| `#` | Removes minimal matching prefixes |
| `##` | Removes maximal matching prefixes |
| `%` | Removes minimal matching suffixes |
| `%%` | Removes maximal matching suffixes |

Here is the syntax for string operators:
`$(<variable> op string)`

The abbreviation `<op>` can be used for any one of the operators listed in Table 19.5 and `<string>` is a matching pattern of characters used for filenames. Use these operators to extract components, remove patterns, or change suffixes. The following example demonstrates how this is done:

```bash
$ STOREFILE=/usr/local/src/dept.c
$ echo ${STOREFILE#/}
local/src/dept.c
$ echo ${STOREFILE##/}
dept.c
$ echo ${STOREFILE%/}
/usr/local/src
$ echo ${STOREFILE%%/}
/usr/local/src/dept.c
$ echo ${STOREFILE%/C}
/usr/local/src/dept.c
$ CUTFIRST=${SOURCEFILE#/}
$ echo $CUTFIRST
local/src/dept.c
$ NEXT=$[CUTFIRST%/*]
$ echo $NEXT
local
```

## Array Variables

The Korn shell allows you to assign an array of values to a variable by using the `set` built-in. The syntax for an array variable is as follows:

```bash
set -A <name> factor1 factor2
```

The following example demonstrates how you would use an array variable. The first element of the array is the subscript 0:

```bash
$ set -A NAMES barrie kay rose peter joe
$ echo $NAMES
barrie
$ echo ${NAMES[2]}
rose
```

> **TIP** Because the subscripting is zero based, the subscript 2 displays the third element of the array.

You can display all the elements by using an asterisk, as in this example:

```bash
$ echo ${NAMES[*]}
barrie kay rose peter joe
```

The use of double quotation marks changes the outcome of the array. If quotation marks are used with subscripts `[*]` and `[@]`, the shell will extract the array differently. The `@` will cause the array to duplicate itself. The `*` will produce a single element that holds all of the other elements of the array separated by an internal field separator, which is usually a space.

The following example illustrates that `*` is used to fill array A with elements of the NAMES variable and `@` is used to fill array B. The `set` built-in displays the values of the A and B arrays without using an argument:

```bash
$ set -A A "${NAMES[*]}"
$ set -A B "${NAMES[@]}"
$ set | head -5
A='barry kay rose peter joe'
B[0]=barry
B[1]=kay
B[2]=rose
B[3]=peter
```

## Korn Shell Control Structures

Control structures are sophisticated commands that control the flow of processes throughout the program. Many employ a form of Boolean logic to test a condition and, after determining whether the condition is true or false, produce a result to output. The use of `if...then` statements, `while...do` statements, and so on provide a means of control that is very specific. These statements create an internal looping mechanism until the appropriate condition is met, thereby breaking the loop and returning control of the function to the program that called it. Control structures are powerful tools for building a program or script that needs to conform to certain conditions.

## The Select Control Structure

The Korn shell uses the `select` control structure to display a menu, assign a value to a variable, and execute a series of commands. The syntax for the `select` structure is as follows:

```bash
select <variable> [in args...]
do
    commands
done
```

A menu of the args items is displayed. The menu is formatted with preceding numbers.

The args list can be very long or it can be short. The `select` structure uses the values of the `LINES` (default 24) and `COLUMNS` (default 80) variables to determine the size of the display. Ordinarily, a page of the green barred computer output paper can support 24 lines and 80 columns, hence the default numbers. The `select` structure will then display the value of `PS3` (default `?#`), which is the special select prompt. You can set the value to something more meaningful to you.

If the user selects a valid number from the menu, then the `select` structure sets the value of `<variable>` to the argument with the number the user entered and executes the commands between `do` and `done`. The `select` structure will then reuse the `PS3` prompt and wait for the user's response. It will repeat this sequence until it is forced
