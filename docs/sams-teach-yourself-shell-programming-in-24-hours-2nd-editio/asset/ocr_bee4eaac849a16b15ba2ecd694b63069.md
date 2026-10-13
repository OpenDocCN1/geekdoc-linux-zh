# Variable Substitution

In the previous chapter, you learned about a basic form of variable substitution, namely how to retrieve the value of a variable using the $ meta-character. In addition to this, the shell provides several other advanced forms of variable substitution that enable shell programs to manipulate the value of a variable based on its state.

There are two broad categories of advanced variable substitution:

+   - Actions taken when a variable has a value
+   - Actions taken when a variable does not have a value

The actions can range from one time value substitution to aborting the script. These categories are broken into four forms of variable substitution. These forms are summarized in Table 9.2.

Table 9.2 Advanced Variable Substitution

| Name | Syntax | Description |
|---|---|---|
| Default Value Substitution | `${param:-word}` | If param is null or unset, word is substituted for param. The value of param does not change. |
| Default Value Assignment | `${param:=word}` | If param is null or unset, param is set to the value of word. |
| Null Value Error | `${param:?msg}` | If param is null or unset, msg is printed to STDERR and the shell exits. |
| Substitute When Set | `${param:+word}` | If param is set, word is used instead of the value of param. The value of param does not change. |

# Default Value Substitution

The first form of advanced variable substitution allows a default value to be substituted when the variable's value is null. The syntax is as follows:

`${param:-word}`

Here param is the name of the variable and word is the default value. Substitution is performed only when param is unset. Furthermore, word is not assigned to param; the shell just replaces the expression with word. The following example illustrates the behavior:

```
$ unset MYFRUIT
$ FRUIT=${MYFRUIT:-APPLE}
$ echo MYFRUIT is $MYFRUIT, FRUIT is $FRUIT
MYFRUIT is , FRUIT is APPLE
```