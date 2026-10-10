simple example). If we have a third-order b-tree, then at most we would have three keys to check for each search. Of course, we could only reference three values with this simple structure!

In order to grow the scope of our b-tree's usefulness, we have to grow the depth of the tree. Once a b-tree expands beyond its order, additional bnodes are created and the depth of the tree is increased.

Only bnodes at the lowest level of the tree contain key-value data. The bnodes at all other levels contain key-pointer data. This means that in order to find a specific value, we must conduct a search of a bnode at each level of the tree. Each search, on average, requires half as many compare operations as there are keys in the bnode (the order). This means that the average search length is defined as (order/2) × depth. Optimization is achieved by adjusting both the order and the depth of the b-tree.

# Example: Growing the b-tree

From Figure 3-7, consider a very simple example of a third-order b-tree. The original bnode has keys: 1, 2, 3. Everything fits in a single bnode, so the depth is simply 1.

When we add a fourth key, 4, to the tree, it fills the bnode to capacity and causes the growth of the tree. If the number of keys in a bnode exceeds the order, then it is time to split the node and grow the tree.

To grow this simple tree, we create two new bnode structures and move half of the existing key-value pairs to each. Notice that the data is packed into the first two entries of each of the new bnodes, which allows for room to grow.

Next, we must adjust the depth value in the broot data structure that defines the tree. The original bnode must also be reconfigured. First, it is cleared, and a single key is created.

Let's take a closer look at the bnode structure. Notice that there are actually more value slots than there are key slots. This allows for two pointers to be created in relation to each key entry. The pointer down and to the left is used if you are seeking a key of a lower value. The pointer down and to the right is used if you are looking for one that is greater than or equal to the key.

Let's try locating a value given a key = 2:

Follow the broot pointer to the first-level bnode.

Search for a key = 2. Because there is no perfect match, we look for a key that is > 2 and follow the pointer down and to the left of that key to the next bnode.

Search for a key = 2. A match here will yield the appropriate value. We know that this is a value and not another pointer, since the broot structure told us we had a depth of two!