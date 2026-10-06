This is a great way to create simple functions on the fly, both in your interactive shells and
your shell scripts.

> NOTE In case you're wondering, the ksh93 shell supports normal functions also. They use
the same format as functions in the bash shell, either using the function command or
using the double parentheses to define the function name.

# # Summary

This chapter introduced the Korn shell and discussed one of the most popular Korn shell implementations, the ksh93 shell. The ksh93 shell is an advanced version of the original Korn shell\and provides lots of interesting features.

The ksh93 shell allows you to typeset variables, defining what type of a variable can hold and
h to process it. By typesetting variables, you can change how the shell displays numeric
values (such as the base used) and also modify the way text is stored (such as all upper or\lower-case).

You can create both numeric and associative array variables in the ksh93 shell. Associative arrays
allow you to assign a string key to a data value. To recall the value, just refer the string key
in the array. The use of compound variables is similar in that you assign multiple values to
variable and reference the values using a subscript of the array.

The ksh93 shell also provides lots of built-in commands. One handy command is the printf
command, which allows you to use C-style printf formatting features to format your output.

One of the highlights of the ksh93 shell is its support for math features. The ksh93 shell can
perform mathematical operations using standard C-style math symbols, and even includes
anced built-in math functions, such as square root, absolute value, and the standard trig
unction. The selling feature of the ksh93 shell for many shell programmers is its full support
oflo-point values. You can process floating-point values as the integer values directly
y your shell scripts!

Finally, the chapter discussed a unique feature of the ksh93 shell, discipline functions.
functions allow you to modify how variables are set and the value they return when you reference them. By overriding the default behavior, you can assign any type of function to a variable.
Whenever you reference the variable, the ksh93 shell automatically executes the function and
assigns the appropriate values when it completes.

The next chapter finishes off tour of alternate Linux shells by examining the Z shell (zsh). The
 shell is one of the newest shells, and shows it by including lots of advanced features.