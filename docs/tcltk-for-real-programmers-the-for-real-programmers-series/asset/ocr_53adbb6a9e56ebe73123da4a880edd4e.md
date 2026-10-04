Chapter 5. Using Lists and Arrays

```
puts "root has these children: [treeGetChildList $root]\n"
#
# Create a node4 as a child of node3
#
set node4 [treeCreateChild $node3]

puts "the parent of node4 is: [treeGetParent $node4]"
puts "node3 has these children: [treeGetChildList $node3]\n"

puts "Tree_InternalArray has these indices:"

foreach index [lsort [array names Tree_InternalArray]] {
    puts "$index"
}
```

# Script Output

```
root is: tree0.2 node2 -- node3 is: tree0.3
t parent of node2 is: tree0.1
root has these children: tree0.2 tree0.3
```

```
the parent of node4 is: tree0.3
node3 has these children: tree0.4
```

```
Tree_InternalArray has these indices:
root
tree0.1
tree0.1.children
tree0.2
tree0.2.parent
tree0.3
tree0.3.children
tree0.3.parent
tree0.4
tree0.4.parent
tree0.base
```

134