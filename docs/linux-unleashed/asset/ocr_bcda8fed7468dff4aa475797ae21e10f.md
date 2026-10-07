# ## Quotes

There may be times when you'll want to use commands containing special characters that you don't want Tcl to interpret. By quoting these particular characters, you hide them from the Tcl interpreter.

Three kinds of quoting can be used in Tcl scripts. The first is quoting with double quotation marks ("). This kind of quoting is used to hide whitespace characters and command separators from the Tcl interpreter.

Whenever there are two or more words that you want Tcl to treat as a single word, you can do so by surrounding the words with quotation marks. A good example of this type of quoting is when you want to create variable names that contain more than one word or you want to assign a value that contains more than one word to a variable, as follows:

```
```
set "Monthly sales" 40000

set Header1 "Description of item"
```
```

The second kind of quoting uses the backslash character (\). This type of quoting can hide any single character from the interpreter. This form of quoting is most commonly used to hide special characters, such as $, from the Tcl interpreter. The following example illustrates the need for backslash quoting:

```
```
set Header1 "The cost is \$3.50"
```
```

In this example the Header1 variable is being assigned the value The cost is $3.50. The quotation marks are necessary to hide the fact that there are four separate words contained in the character string. The backslash in this command tells the Tcl interpreter to treat $ as a regular character instead of the variable substitution character. If the backslash had not been used in the command, the interpreter would have attempted to substitute the variable named 3.50 into the command. This would result in an error because there is no variable with that name defined.

The third type of quoting available in Tcl uses braces ({}). This quoting is more powerful than quoting using quotation marks or backslashes. Quoting using braces hides not only whitespace and command separators from the Tcl interpreter, but also any other kind of special character. This type of quoting can be used to eliminate the need for backslash quoting in character strings. The example used for backslash quoting can be written using brace quotation as follows:

```
```
set Header1 {The cost is $3.50}
```
```

The most important use of brace quoting is to defer the evaluation of special characters. This means that special characters are not processed immediately by the Tcl interpreter