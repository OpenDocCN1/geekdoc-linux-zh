> Putting a significantly large number of elements into a balanced binary tree does not change the speed of the tree

If a binary tree is balanced, its search, insert and delete operations take about log(n) steps, where n is the total number of elements the tree has. Additionally, the height of a balanced binary tree is approximately log2(n), which means a tree with 1000 elements has a height of about 14, which is remarkably small. The height of a tree with 100,000 elements will be about 17, and the height of a balanced tree with 1,000,000 elements will be 20. Putting a significantly large number of elements into a balanced binary tree does not change the speed of the tree in an extreme way. You can reach any node in 1,000,000 nodes in under 30 steps.
The adjacent diagram shows a graphical representation of a small binary tree. You can see that all values are found in the sub-tree with the value of 22 are smaller than all values in the sub-tree with 18 as its root. In other words, all keys in a child of a binary tree are ordered by design. The good thing is you do not have to take special care with them; putting an element in its right place keeps them ordered. As you will find out, deleting an element from a tree is not always trivial because of the way trees are constructed.
The depth of the example tree is 8 to reach either element 7 or 10. You will need to pass over 8 nodes (16 > 2 > 13 > 4 > 11 > 9 > 10). It is easy just by looking at the presented tree with the same elements but with 15 as the root node would look totally different! See the two illustrations on page 54 for an example of how the same elements can form two different kinds of trees. You should also be aware that exist trees with nodes more than two children.

# Creating a binary tree

As it has with linked lists, you will need a special structure to hold the data of a tree. For a binary tree, each node should be able to reference two nodes. Therefore, the C structure shown below for describing the nodes of a binary tree is:

```
struct node {
  int val;
  struct node *right;
  struct node *left;
};
```

![](bbox=[0.448, 0.163, 0.915, 0.883])

Above Each node can connect to a maximum of one node above and below