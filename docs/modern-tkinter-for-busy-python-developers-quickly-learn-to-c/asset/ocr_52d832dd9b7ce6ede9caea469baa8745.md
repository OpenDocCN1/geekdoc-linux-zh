![](bbox=[0.13, 0.08, 0.37, 0.23])

![](bbox=[0.37, 0.08, 0.62, 0.23])

![](bbox=[0.62, 0.08, 0.87, 0.23])

# Treeview Widgets

Treeview widgets are created using the `tkk.Treeview` function:

```
tree = ttk.Treeview(parent)
```

Horizontal and vertical scrollbars can be added in the usual manner, if desired.

# Adding Items to the Tree

To do anything useful with the treeview, you'll need to add one or more items to it. Each item represents a single node in the tree, whether a leaf node or an internal node. Items are referred to by a unique id; this can be assigned by the programmer when the item is first created, or the widget can automatically choose an id for the item.

Items are created by inserting them into the tree, using the treeview's “insert” method. To insert an item, you need to know where in the tree to insert it, which means specifying the parent item as well as what position in the list of the parent's children the new item should be inserted at.

The treeview widget automatically creates a root node (which is not displayed), having the id of “{}” (i.e. the empty string), which can serve as the parent of the first level of items you add. Positions within the list of the parent's children are specified by index (0 being the first, with the special “end” index meaning inserting after all existing children).

Normally, you'll also specify the name of each item, which is displayed in the tree. There are other options to add an image beside the name, specify whether the node is open or closed, and so on.

```
```python
# Inserted at the root, program chooses id:
tree.insert('', 'end', 'widgets', text='Widget Tour')

# Same thing, but inserted as first child:
tree.insert('', 0, 'gallery', text='Applications')

# Treeview chooses the id:
id = tree.insert('', 'end', text='Tutorial')

# Inserted underneath an existing node:
tree.insert('widgets', 'end', text='Canvas')
tree.insert(id, 'end', text='Tree')
```
```

Inserting the item returns the id of the newly created item.