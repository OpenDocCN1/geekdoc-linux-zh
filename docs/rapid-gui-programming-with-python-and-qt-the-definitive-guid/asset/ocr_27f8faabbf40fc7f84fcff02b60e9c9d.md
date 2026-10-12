```
self.columns = max(self.columns, len(items))
branch.insertChild(LeafNode(items, branch))
if callReset:
    self.reset()
```

To add a record there must be more fields than the level of nesting. The logic we use is similar to what we saw in Chapter 14 when we populated a QTreeWidget's internal model. For each field that is to be a branch we look for an existing branch with the same key. If we find one, we make it the current root branch; otherwise, we create a new branch, insert it as a child of the current root branch, and make the new branch the current root branch. As the loop progresses, we gradually walk down the tree, creating any branches that are needed, until we reach the lowest branch.

Once the loop has gone over all the branches that are necessary, creating any that did not previously exist, we can create a list of the non-nesting fields and add them as a child leaf node of the current (lowest-level) branch.

To put things in concrete terms, using the Server Info application as an example, here's what happens. When the first record is read we have a new country, new state, new city, new provider, and so on, so no suitable branches will exist. First a country branch will be created, then a state branch, and then a city branch, and finally a leaf containing the remaining provider, server, and IP address fields. If the next record read is for the same country, but for a new state, it will find the existing country node and use it as the parent node for the new state. Similarly, if a record has a country and state for which branches have already been created, these will be used. But whenever a new branch is needed the code in the loop's body will create it.

When new records are added on an ad hoc basis, we call reset() to notify any views that a significant change has taken place; but when loading from a file we pass False and call reset() in the calling code once all the records have been read.

```
def asRecord(self, index):
    leaf = self.nodeFromIndex(index)
    if leaf is not None and isinstance(leaf, LeafNode):
        return leaf.asRecord()
    return []
```

This method provides a list of the user's chosen “path”. It makes sense only for leaf nodes, since only a leaf node can represent a complete path. Returning None for nonleaf nodes would have been an equally good design choice. Notice that we use the nodeFromIndex() method to retrieve the node for a given model index: We will discuss how this works shortly.

```
def rowCount(self, parent):
    node = self.nodeFromIndex(parent)
    if node is None or isinstance(node, LeafNode):
```