# 7.3 A Tree Object Package with Namespaces

The code that implements this is:

# Example 7.3.2-1

```
package provide treeObject 1.0
############################################################
# proc newTreeObject { --
# Creates a new Tree object, and returns an object for
# Arguments:
#   NONE
# NOTE: This procedure is in global scope.
#
proc newTreeObject {
    set treeId [treeObject::tree::treeCreate]
    proc treeId {args}
        return \[treeObject::TreeObjProc $treeId \$args]
    "
    return $treeId
}
# These procedures are defined within the treeObject namespace
#
namespace eval treeObject {
#
# The tree package is required. This causes the Tcl
# interpreter to search the pkgIndex.tcl files and
# set the fields in auto_index
package require tree 1.0
#
# In order to import the tree procedures, we need to force
# the package to load.
```