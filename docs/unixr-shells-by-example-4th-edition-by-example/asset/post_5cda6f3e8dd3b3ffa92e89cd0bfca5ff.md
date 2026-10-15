
# EXAMPLE 12.30

```
(The Command Line)
1  $ array[0]=tom
   $ array[1]=dan
   $ array[2]=bill
2  $ print ${array[0]}    # Curly braces are required.
   tom
3  $ print ${array[1]}
   dan
4  $ print ${array[2]}
   bill
5  $ print ${array[*]}    # Display all elements.
   tom dan bill
6  $ print ${#array[*]}   # Display the number of elements.
   3
```

## EXPLANATION

+   1 The first three elements of the array are assigned values. The index starts at 0.
+   2 The value of the first array element, tom, is printed. Make sure you remember to surround the variable with curly braces. $array[0] would print tom[0].
+   3 The value of the second element of the array, dan, is printed.
+   4 The value of the third element of the array, bill, is printed.
+   5 All elements in the array are printed.
+   6 The number of elements in the array is printed. An array can be declared with typeset if you know the size and type.

# EXAMPLE 12.31

```
(At The Command Line)
1  $ typeset -i ints[4]   # Declare an array of four integers.
2  $ ints[0]=50
   $ ints[1]=75
   $ ints[2]=100
3  $ ints[3]=happy
   ksh: happy: bad number
```

## EXPLANATION

+   1 The typeset command creates an array of 4 integers.
+   2 Integer values are assigned to the array.
+   3 A string value is assigned to the fourth element of the array, and the Korn shell sends a message to standard error.

## 12.7.1 Creating Arrays with the set Command

You can assign the values of an array using the set command. The first word after the -A option is the name of the array; the rest of the words are the elements of the array.

# EXAMPLE 12.52

(The Command Line)

```
1  $ set -A fruit apples pears peaches
2  $ print ${fruit[0]}
   apples
3  $ print ${fruit[*]}
   apples pears peaches
4  $ fruit[1]=plums
5  $ print ${fruit[*]}
   apples plums peaches
```

## EXPLANATION

+   1. The set command with the -A option creates an array. The name of the array, fruit, follows the -A option. Each of the elements of the fruit array follow its name.
+   2. Subscripts start at 0. Curly braces are required around the variable for it to be evaluated properly. The first element of the array is printed.
+   3. When the asterisk is used as a subscript, all elements of the array are displayed.
+   4. The second element of the array is reassigned the value plums.
+   5. All elements of the array are displayed.

# 12.8 Functions

Korn shell functions are similar to those used in the Bourne shell, and are used to modularize your program. A function is a collection of one or more commands that can be executed simply by entering the function's name, similar to a built-in command. Here is a review of some of the important rules about using functions.

+   1. The Korn shell executes built-in commands first, then functions, and then executables. Functions are read into memory once when they are defined, not every time they are referenced.
+   2. A function must be defined before it is used; therefore, it is best to place function definitions at the beginning of the script.
+   3. The function runs in the current environment; it shares variables with the script that invoked it, and lets you pass arguments by setting them as positional parameters. The present working directory is that of the calling script. If you change the directory in the function, it will be changed in the calling script.
+   4. In the Korn shell, you can declare local variables in the function using the typeset command. Ksh functions can be exported to subshells.

+   5. The return statement returns the exit status of the last command executed within the function or the value of the argument given, and cannot exceed a value of 255.

+   6. To list functions and definitions, use the preset alias, functions.

+   7. Traps are local to functions and will be reset to their previous value when the function exits (not so with the Bourne shell).

+   8. Functions can be recursive, that is, call themselves. Recursion should be handled carefully. The Korn shell will warn you otherwise with the message, recursion too deep.

+   9. Functions can be autoloaded; they are defined only if referenced. If never referenced, they are not loaded into memory.

+   10. Versions of the Korn shell that are more recent than 1988 also support discipline functions, passing variables by reference, and compound variables. A built-in command is no longer found before a function of the same name. In older versions it was necessary to use a combination of aliases and functions to write a function that would override a built-in command.

## 12.8.1 Defining Functions

A function must be defined before it can be invoked. Korn shell functions are defined with the keyword function preceding the function name. The curly braces must have space on the inside of each brace. (Please see "Functions" on page 372 for the older-style Bourne shell function definition; these are still compatible in Korn shell scripts.)

## FORMAT

```
function function_name { commands; commands; }
```

# EXAMPLE 12.53

```
function usage { print "Usage $0 [-y] [-g]" ; exit 1; }
```

## EXPLANATION

The function name is usage. It is used to print a diagnostic message and exit the script if the script does not receive the proper arguments, either -y or -g.

## 12.8.2 Listing and Unsetting Functions

To list local function definitions, type typeset -f. To list exported function definitions, type typeset -fx. To unset a function, type unset -f function_name. See the typeset command, Table 12.11 on page 714.

> 3. David G. Korn and Morris I. Bolsky, The Korn Shell Command and Programming Language (Englewood Cliffs, NJ: Prentice-Hall, Inc., 1988), p. 77.
