You can list the options to declare separately in any order. The following is equivalent to the declaration of person3:

```
$ declare -x -r person3=helen
```

Also, you can use the + character in place of - if you want to remove an attribute from a variable. After the following command is given, making an assignment to the variable person3 does not result in an error:

```
$ declare +r person3
```

If the declare builtin is given with options but no variable names as arguments, the command list lists all shell variables that have the indicated attributes set. For example, the option -r with declare gives a list of all readonly shell variables. After the declarations in the preceding example have been given, the results are as:

```
$ declare -r
declare -ar BASH_VERSINFO='([0]="2" [1]="05b" [2]="0" [3]="1" ... )'
declare -ir UID="936"
declare -ir SHELLOPTS="braceexpand:emacs:hashall:histexpand:history:..."
declare -ir UID="500"
declare -ir person2="jenny"
declare -rx person3="helen"
```

The first five entries are keyword variables that are automatically declared readonly. Some of these variables are also stored as integers, the option -i indicates. the -a option indicates that BASH_VERSINFO is stored as an array variable; the value of each element of the array is to the right of the equal sign. If you had used readonly to make a keyword variable readonly, the keyword variable would also appear in the list. Another way to get the same list of shell variables is by using readonly with no arguments.

Without any arguments or options, the declare lists all the shell variables. The same list is output when you run set (page 584) without any arguments. Another name for declare is typeset. You may see it often in shell scripts, including complex scripts that come with the GNU/Linux system.

read: Accepts User Input