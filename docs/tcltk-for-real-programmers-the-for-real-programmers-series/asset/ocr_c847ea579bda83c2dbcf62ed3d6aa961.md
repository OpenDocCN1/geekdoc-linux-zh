# Chapter 6. Procedure Techniques

```
set methods {set, get, add, delete \
    destroyTree childList, parent, valueList, \
    base, dump, \
    siblingCommand search}
error "Bad method: subCommand\n use $methods"

}
return " "
```

There are a few points to note about this code.

The TreeObjProc procedure uses rename to delete the procedure associated with a node when the node is deleted. Once a node is deleted, there is no longer a procedure call with that name.

The subcommand strings are shorter and simpler than the procedures defined in tree.tcl. The tree.tcl package needs to use long names starting with a unique string to avoid conflicts with other packages that may be loaded. (Imagine how many packages might have a procedure named “process-Data.\) Within the TreeObjProc, however, there are no conflicts with other Tcl commands or procedures, so simple subcommand names can be used.

The set and get commands use an option (-tree or -node) to declare whether the set should be attached to a single node or to the complete tree. In the tree.tcl script, setting a value in the tree and setting one in a node are two separate procedures. By default, the set and get commands set the Key/Value pair for a node. The following example uses the default action for these commands.

Here’s the example from Chapter 5 rewritten to use the TreeObj class instead of the tree functions.

# Example 6.6.3-1

Example Script

```
#!/bin/sh
\
exec tclsh "$0" "$@"

source ../tree/treeObj.tcl
```