# 5.5 Tree Package Implementation

parent The parent to receive this child node.

child The new child node to be added to the parent.

The following example shows the three procedures that are used to create a new child: the public entry point and the two internal procs. In this example, the internal procs are called to show the steps in creating a child node.

Since all of the interaction between the programmer and the Tree package is done with handles returned by the Tree package, the application programmer will never need to know the internal naming conventions of the Tree package. In this example the array indices are displayed to show how the package works.

# Example 5.5.3-1

```
############################################################ --
# proc treeCreateChild (parent)
# Creates a child of a given parent
#
# Arguments:
#    parent: The parent node to contain this new node
# Results:
#    Creates a new node.
#    Adds the child to the parent node.
#    Returns the handle for the new node
#
```

```
proc treeCreateChild (parent) {
    global Tree_InternalArray

    TreeGetNameParts $parent primary idNum

    set child [TreeCreateNode $primary.base]

    TreeAddChild $parent $child
    return $child
}
```

```
################################################************
# proc treeCreateNode (rootname) --
# Create a new node (unattached) in this tree
# Arguments:
```