# Chapter 3. Introduction to the Tcl Language

Notice that the * symbol in the variable name pi*2 does not mean multiply in this case. Since the * is embedded in a word, it is simply another character in a variable name. The last example shows how spaces can be embedded in a variable name. This is not a recommended style.

# 3.1.5 Command Results

If a Tcl command fails to execute for a syntactic reason (incorrect arguments, etc.), it will generate an error, display a message about the cause of the error, and stop evaluating the current Tcl script.

If a command can be evaluated successfully, it may return data. That data can be assigned to a variable, used in a conditional statement like an if, or passed to another command.

Enclosing a Tcl command in square brackets causes the command to be evaluated immediately, and the command's return value is available for the script to process. This is the same as putting a command inside backquotes in Unix shell programming.

For example, the set command always returns the value of the variable being set. When x is assigned the value of "apple" in the following example, evaluating the set command returns "apple". When set x "pear" is then evaluated within the square brackets, it returns "pear", which is then assigned as the value for y.

# Example 3.1.5-1

```
# The set command returns the contents of the variable.
% set x "apple"
apple
% set y [set x "pear"]
pear
% puts $y
pear
```

In the previous example, the quotes around the word apple are not required by the Tcl interpreter. However, it's good practice to place strings within quotes.