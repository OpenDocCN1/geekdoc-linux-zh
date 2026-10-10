![](bbox=[0.18, 0.1, 0.8, 0.42])

Figure 6-10 The b-tree

The base of the tree is its **broot**. It sets the rules for the tree's usage and directs us to the first level **bnode** in the tree. This first **bnode** is sometimes called the root **bnode** — try not to confuse the two structure names.

The **bnode** structures are ranked and ordered according to the tree's depth (defined in the **broot**) and form the tree's **branches**. To continue with the tree model, the **chunk** structures could be thought of as the leaves on the branches. Each chunk contains **vfd** | **dbd** structure pairs; these **vfd** | **dbds** are the fruit of a successful search of the tree.

# Broot, Bnodes, and Chunks

Let's examine the b-tree structures in Listings 6.9 and 6.10.

Listing 6.9 q4> fields struct broot

```
We start off with a pointer to the root (first) bnode and
record the depth of the b-tree
0 0 4 0 * b_root
4 0 4 0 int b_depth
Next we find the number of pages mapped and the number of swap
pages reserved for this tree
8 0 4 0 int b_npages
12 0 4 0 int b_rpages
The page list pointer directs us to this region's page list,
and nfrag points to the next available chunk (required if we
need to grow the tree)
16 0 4 0 * b_list
20 0 4 0 int b_nfrag
```