```
```c
void *vp, *root;
struct employee *e;
... fill tree with data ...

vp = tfind(& key, root, emp_name_id_compare);
if (vp != NULL) { /* it’s there, use it */
    e = *((struct employee **) vp);      Retrieve stored data from tree
    /* use info in *e ... */
}
```
```

How can a pointer to a node double as a pointer to a pointer to the data? Well, consider how a binary tree’s node would be implemented. Each node maintains at least a pointer to the user’s data item and pointers to potential left and right subchildren. So, it has to look approximately like this:

```
```c
struct binary_tree {
    void *user_data;                   Pointer to user’s data
    struct binary_tree *left;          Left subchild or NULL
    struct binary_tree *right;         Right subchild or NULL
    ... possibly other fields here ...
} node;
```
```

C and C++ guarantee that fields within a struct are laid out in increasing address order. Thus, it’s true that `& node.left < & node.right`. Furthermore, the address of the struct is also the address of its first field (in other words, ignoring type issues, `& node == & node.user_data`).

Conceptually, then, here’s what `‘e = *((struct employee **) vp)’` means:

+   1. `vp` is a `void *`, that is, a generic pointer. It is the address of the internal tree node, but it’s also the address of the part of the node (most likely another `void *`) that points to the user’s data.
+   2. `‘(struct employee **) vp’` casts the address of the internal pointer to the correct type; it remains a pointer to a pointer, but now to `struct employee`. Remember that casts from one pointer type to another don’t change any values (bit patterns); they only change how the compiler treats the values for type considerations.
+   3. `‘*((struct employee **) vp)’` indirections through the newly minted `struct employee **`, returning a usable `struct employee *` pointer.
+   4. `‘e = *((struct employee **) vp)’` stores this value in `e` for direct use later.

The concept is illustrated in Figure 14.2.