```
switch -exact --$option {
  -node} {
    return [treeGetValue $node $key]
  }
  -tree} {
    return [treeGetValue $node $key]
  }
  -best} {
    set fail [catch \
      {treeGetValue $node $key} returnVal]
    if {!$fail} {
      return $returnVal
    }
    return [treeGetValue $node $key]
  }
  default {
    error "$node set -node? -node? key value"
  }
}
```

```
(add) {
# Add a child node to this node.
set newNode [treeCreateChild $node]
proc newNode {args} "\
  return \[TreeObjProc $newNode \$args]"
return $newNode
}
```

```
(delete) {
# remove this node
# and remove the proc from the proc hash table
# If cmdArgs == "-r", delete recursively.
if {[cmdArgs "-r"]} {
  foreach child [$node childList] {
    $child delete -r
    catch {rename $child ""}
  }
# delete this node.
treeDeleteNode $node
rename $node ""
}
```