# 5.6 Using the Tree Package

```
# Loop through the names in fileList

foreach name $fileList {
    set node [treeCreate $treeNode]
    treeSetNodeValue $node name $name
    treeSetNodeValue $node type [file type $name]
}
```

```
# Create a tree structure
set root [treeCreate]
# Add the initial directory and its directory entries
# to the treeTo
addDirToTree $root [file natename /]
```

```
# If any children are directories, add their entries to the
# tree as new nodes
foreach entry [treeGetChildList $root] {
    if [[treeNodeValue $entry type] == "directory"]
        addDirToTree $entry [treeNodeValue $entry name]
}
```

```
# Print out the tree in the form:
# Dir1
# Dir1/Entry1
# Dir1/Entry2
# Dir2
# Dir2/Entry3
# Dir2/Entry4
```

```
foreach entry [treeGetChildList $root] {
    puts "[treeGetNodeValue $entry name]"
    if [[treeNodeValue $entry type] == "directory"] {
        foreach sub [treeGetChildList $entry] {
```