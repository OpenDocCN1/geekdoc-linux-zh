input can be almost anything, and the code has to be defensive. For example,
without the list enclosing the $answer user could type in [proc apples
a} {return 1}] to force the program to generate a correct response.

# 6.6.2 Creating a Tree Object

The tree subroutines discussed in Chapter 5 returned an index into the global associative array Tree_InternalArray. This index is used as a handle to identify the node being referenced.

This handle name can also be defined as a procedure name, just as the variable names were used in the previous example.

Rather than adding code to convert the handle into a procedure each time we add a new node, we can write a new procedure (newTreeObject) that will:

+   1. Call the treeCreate procedure to create a new tree.
2. Define a procedure with the same name as the handle treeCreate returned.
3. Return that name for the program to use as a procedure for manipulating the tree.

In the previous example, we created a procedure that had a single purpose. We can also make a procedure that will perform any of several actions based on a subcommand name. In the next examples, that procedure will be named TreeObjProc, which will be discussed after describing the newTreeObject procedure.

The following code shows the newTreeObject procedure.

Example 6.6.2-1

```
####################################################################
# proc newTreeObject {} --
# Creates a new Tree object, and returns an object for
#   accessing the base node.
# Arguments:
#   None

proc newTreeObject {} {}
```