# 584 Chapter 12 The Shell II: The Bourne Again Shell

In the original Bourne Shell, the positional parameters were limited to $1-$9, so shell scripts that accepted more than nine arguments were forced to shift to later arguments. The Bourne Again Shell has no limit on the number of positional parameters, so this use of shift has declined. However, repeating shift is a convenient way to loop over all the command line arguments in shell scripts that expect an arbitrary number of arguments. See page 632 for a sample shell program that uses this technique.

# set: Initialize Command Line Arguments

When you call the set builtin with one or more arguments, it uses the arguments as values for positional parameters, starting with $1 (for tsh, see footnote 8 on page 581). The following script uses set to assign values to the positional parameters $1, $2, and $3:

```
cat set_it
set this is it
echo $3 $2 $1
set $1 it is this
```

Combining the use of command substitution (page 575) with the set builtin is a convenient way to get standard output of a command in a form that can be easily manipulated in a shell script. The following script shows how to use date and set provide the date in a useful format. The first command shows the output of date. Then cat displays the contents of the dateset script. The first command in the script uses command substitution to set the positional parameters to the output of the date utility. The next command, echo $$, displays all the positional parameters resulting from the previous set. Subsequent commands display the values of parameters $1, $2, $3, and $4. The final command displays the date in a format you can use in a letter or report:

```
date
Tue Apr 30 08:46:39 PDT 2002
cat dateset
set $(date)
echo $*
echo
echo "Argument 1: $1"
echo "Argument 2: $2"
echo "Argument 3: $3"
echo "Argument 6: $6"
echo
echo "$2 $3, $6"
```