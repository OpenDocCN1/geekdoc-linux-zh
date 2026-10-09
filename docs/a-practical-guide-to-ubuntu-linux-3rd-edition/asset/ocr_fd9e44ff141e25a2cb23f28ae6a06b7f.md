The readonly and export builtins are synonyms for the commands declare -r and declare -x, respectively. You can declare a variable without assigning a value to it, as the preceding declaration of the variable person4 illustrates. This declaration makes person4 available to all subshells (i.e., makes it global). Until an assignment is made to the variable, it has a null value.

You can list the options to declare separately in any order. The following is equivalent to the preceding declaration of person3:

```
$ declare -x -r person3=helen
```

Use the + character in place of - when you want to remove an attribute from a variable. You cannot remove the readonly attribute. After the following command is given, the variable person3 is no longer exported but it is still readonly.

```
$ declare +x person3
```

You can use typeset instead of declare.

Without any arguments or options, declare lists all shell variables. The same list is output when you run set (page 998) without any arguments.

+   Listing variable attributes

If you use a declare builtin with options but no variable names as arguments, the command lists all shell variables that have the indicated attributes set. For example, the command declare -r displays a list of all readonly shell variables. This list is the same as that produced by the readonly command without any arguments. After the declarations in the preceding example have been given, the results are as follows:

```
```
$ declare -r
declare -ar BASH_VERSIONINFO=([0]=''3' [1]=''2' [2]=''39' [3]=''1' ... )
declare -ir EUID=''500''
declare -ir PPID=''936''
declare -r SHELLOPTS="braceexpand:emacs:hashall:histexpand:history:..."
declare -ir UID=''500''
declare -r person2=''zach''
declare -rx person3=''helen''
```
```

The first five entries are keyword variables that are automatically declared as readonly. Some of these variables are stored as integers (-i). The -a option indicates that BASH_VERSIONINFO is an array variable; the value of each element of the array is listed to the right of an equal sign.

+   Integer

By default the values of variables are stored as strings. When you perform arithmetic on a string variable, the shell converts the variable into a number, manipulates it, and then converts it back to a string. A variable with the integer attribute is stored as an integer. Assign the integer attribute as follows:

```
$ declare -i COUNT
```

# KEYWORD VARIABLES

Keyword variables either are inherited or are declared and initialized by the shell when it starts. You can assign values to these variables from the command line or