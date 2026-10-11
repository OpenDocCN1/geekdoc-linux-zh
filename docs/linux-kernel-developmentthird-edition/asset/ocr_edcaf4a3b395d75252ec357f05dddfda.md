```
/*
 * Find the right place in the rbtree:
 */
while (*link) {
    parent = *link;
    entry = rb_entry(parent, struct sched_entity, run_node);
    /* We dont care about collisions. Nodes with
     * the same key stay together.
     */
    if (key < entry_key(cfs_rq, entry)) {
        link = &parent->rb_left;
    } else {
        link = &parent->rb_right;
        leftmost = 0;
    }
}

/*
 * Maintain a cache of leftmost tree entries (it is frequently
 * used):
 */
if (leftmost)
    cfs_rq->rb_leftmost = &sse->run_node;

rb_link_node(&sse->run_node, parent, link);
rb_insert_color(&sse->run_node, &cfs_rq->tasks_timeline);
}
```

Let’s look at this function. The body of the while() loop traverses the tree in search of a matching key, which is the inserted process’s vruntime. Per the rules of the balanced tree, it moves to the left child if the key is smaller than the current node’s key and to the right child if the key is larger. If it ever moves to the right, even once, it knows the inserted process cannot be the new leftmost node, and it sets leftmost to zero. If it moves only to the left, leftmost remains one, and we have a new leftmost node and can update the cache by setting rb_leftmost to the inserted process. The loop terminates when we compare ourselves to a node that has no child in the direction we move; link is then NULL and the loop terminates. When out of the loop, the function calls rb_link_node() on the parent node, marking the inserted process the new child. The function rb_insert_color() updates the self-balancing properties of the tree; we discuss the coloring in Chapter 6.