```
(Linux):$ alias abc='echo $*' following
(Linux):$ abc one two three
following one two abc
(Linux):$ unalias abc
(Linux):$ function abc () { echo $* } following
(Linux):$ abc one two three
one two three following
```

**Listing 10.65** A simple shell function.

Variables used in shell functions are global, provided they have not been declared as local variables by means of the keyword local. The bash recognizes from the round parentheses that a shell function is being defined, so the keyword function does not need to be specified.

#  10.8.4 Variable substitution

Variables are expanded by means of the dollar sign ($). Instead of the variable name, the contents of the variable are substituted. The variable name can optionally be enclosed in curly brackets to mark the end of the name. However, the shell is also capable of influencing the expansion of variables.

+   ${variable:-word}
If the variable is not set or if it is empty, the value of the word is substituted. First, however, the shell carries out tilde expansion, variable expansion, command substitution, and arithmetic calculations.

+   ${variable:=word}
In addition to the functions indicated above, the variable variable is assigned the word after expansion of word.

+   ${variable?:word}
If the variable is not set or if it is empty, the text resulting from the expansion of the word is written to the standard error output. Otherwise, the value of the variable is substituted.

+   ${variable:+word}
If the variable is not set or if it is empty, nothing is substituted. Otherwise, the result of the expansion of word is substituted.