# 6.6.3 Defining the Object's Method

The TreeObjProc is the largest part of the tree object package. This procedure takes two arguments: the name of the node to manipulate (which is set when the node's procedure is defined) and a list of arguments. The first entry in the list will be a subcommand that defines tree.tcl procedure to evaluate, and the rest of the list will be arguments that will be passed to the tree procedure.

All of the procedures that were defined in the tree example in Chapter 5 are supported in TreeObjProc.

```
############################################################
# proc TreeObjProc (node methodArgs) --
# Primary method for tree objects.
# Parses the subcommand and calls the appropriate
# tree.tcl proc.
#n# Arguments:
# node: The internal name for this node.
# methodArgs: A list, the first member is the subcommand
name, subsequent (optional) members are
arguments to be passed to the tree.tcl
command.
#n# Results:
# Calls other procedures which may produce output,
# create new objects, delete objects, etc.
proc TreeObjProc {node methodArgs} {
    set subCommand [lindex $methodArgs 0]
    set cmdArgs [range $methodArgs 1 end]
    switch $subCommand {
    set {
        # Set the Key/Value pair associated with this node.
        # could be set -node key value
        # set -tree key value
        # set key value -- Default to node.
        if {[length $cmdArgs] == 3} {
            set option [lindex $cmdArgs 0]
        }
    }}
```