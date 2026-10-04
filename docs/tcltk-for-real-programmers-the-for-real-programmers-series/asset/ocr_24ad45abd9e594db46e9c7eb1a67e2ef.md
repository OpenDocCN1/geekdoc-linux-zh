The preceding example is very similar to the example in Chapter 5, since most of the code deals with the file system, not with the tree. However, it's a bit easier to follow with the shorter subcommand names used instead of the long tree procedures.

There are two problems with this tree object.

+   1. The associative array Tree_InternalArray sits at the global scope, where any code can access it easily.

+   2. The script that wishes to use the treeObject needs to know the directory where treeObj.tcl is stored, and treeObj.tcl needs to be able to find treeObj.tcl.

Chapter 7 will discuss the namespace and package commands. The examples show how to use the namespace command to hide the Tree_InternalArray in a private namespace and how to use the package command to create a package that can be used without the script needing to know the location of the files it loads.

# 6.7 Bottom Line

+   * A procedure can be defined as taking an undefined number of arguments by placing the args argument last in the argument list.

+   * A procedure argument with a default value is defined by declaring the argument as a list. The second list element is the default value.

+   * When a Tcl procedure is evaluated, it creates a local scope for variables. This local scope stacks below the scope of the code that invoked the procedure.

+   * A Tcl script can access all of the scopes above it in the procedure call stack.

+   * Tcl procedures can be constructed and evaluated in a running procedure.

+   * Data items can be treated as objects by creating a procedure with the same name as the data item and using that procedure to manipulate the data item.