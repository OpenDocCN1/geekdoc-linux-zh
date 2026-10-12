can be used. The statement

Click here to view code image

defines the `s` variable `t` and sets its value to 3:29:55 a.m. As with other variables, if `t` is a local structure variable, it is initialized each time the function is entered. If the structure variable is made static (by placing the keyword `s` in front of it), it is only initialized once at the start of program execution. In either case, the initial values listed inside the curly braces must be constant expressions.

As with the initialization of an array, fewer values might be listed than are contained in the structure. So the statement

Click here to view code image

sets `t` to 1 and `t` to 1 but gives no initial value to `t`. In such a case, its default initial value is undefined.

You can also specify the member names in the initialization list. In that case, the general format is

This method enables you to initialize the members in any order, or to only initialize specified members. For example,

Click here to view code image

sets the `t` variable to the same initial values as shown in the previous example. The statement

Click here to view code image

sets just the `y` member of the `d` structure variable `t` to 2.

# Compound Literals

You can assign one or more values to a structure in a single statement using what is known as *compound literals*. For example, assuming that `t` has been previously declared as a `s d` variable, the assignment of the members of `t` as shown in *Program 8.1* can also be done in a single statement as follows:

Click here to view code image

t

Note that this statement can appear anywhere in the program; it is not a declaration statement. The type cast operator is used to tell the compiler the type of the expression, which in this case is `s`, and is followed by the list of values that are to be assigned to the members of the structure, in order. These values are listed in the same way as if you were initializing a structure variable.

You can also specify values using the _.member_ notation like this:

Click here to view code image