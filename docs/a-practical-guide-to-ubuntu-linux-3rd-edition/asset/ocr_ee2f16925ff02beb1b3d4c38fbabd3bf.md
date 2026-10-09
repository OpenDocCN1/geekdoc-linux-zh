where *op* is one of the operators listed in Table 27-7 and *pattern* is a match pattern similar to that used for filename generation. These operators are commonly used to manipulate pathnames to extract or remove components or to change suffixes:

```
$ SOURCEFILE= /usr/local/src/prog.c
echo ${SOURCEFILE#/s/}
/usr/local/src/prog.c
echo ${SOURCEFILE##/*}
prog.c
echo ${SOURCEFILE%/*}
/usr/local/src
echo ${SOURCEFILE%%/*}

$ echo ${SOURCEFILE%.c}
/usr/local/src/prog
$ CHOPFIRST=${SOURCEFILE#/*}
$ echo $CHOPFIRST
local/src/prog.c
$ NEXT=${CHOPFIRST%/*}
$ echo $NEXT
local

```

Here the string-length operator, ${#*name*}, is replaced by the number of characters in the value of *name*:

```
$ echo $SOURCEFILE
/usr/local/src/prog.c
$ echo ${#SOURCEFILE}
21

```

# # OPERATORS

Arithmetic expansion and arithmetic evaluation in *bash* use the same syntax, precedence, and associativity of expressions as in the C language. Table 27-8 lists operators in order of decreasing precedence (priority of evaluation); each group of operators has equal precedence. Within an expression you can use parentheses to change the order of evaluation.

Table 27-8 Operators
| Type of operator/operator | Function |
| :------------------------- | :---------------------- |
| Post | |
| *var*++ | Postincrement |
| *var*−− | Postdecrement |
| Pre | |
| ++*var* | Preincrement |
| −−*var* | Predecrement |