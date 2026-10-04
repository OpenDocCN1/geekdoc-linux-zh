# 6.6 Making a Tcl Object

```
set key [lindex $cmdArgs 1]
set val [lindex $cmdArgs 2]
\
else {[length $cmdArgs] == 2} {
    set option "-node"
    set key [lindex $cmdArgs 0]
    set val [lindex $cmdArgs 1]
} else {
    error "$node set ?-node ?-tree key value"
}
if {[string match option "-node"} {
    return [treeSetNode $node $key $val]
}
selse {[string match option "-tree"} {
    return [treeSetTreeValue $node $key $val]
} else {
    error "$node set ?-node ?-tree key value"
}
}
{get} {
# return the Key/Value pair associated with this node.
# May be:
# get -node key
# get -tree-key
# get -best-key -- return node, value
# or tree value if no node exists
# get key -- treat as best.
if {[length $cmdArgs] == 2} {
    set option [lindex $cmdArgs 0]
    set key .[lindex $cmdArgs 1]
    set val [lindex $cmdArgs 2]
}
else {[length $cmdArgs] == 1} {
    set option "-best"
    set key [lindex $cmdArgs 0]
    set val [lindex $cmdArgs 1]
} else {
    error "$node set ?-node ?-tree key value"
}
}}
```