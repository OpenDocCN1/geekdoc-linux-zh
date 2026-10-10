![](bbox=[0.15, 0.06, 0.88, 0.53])

Figure 3-9 Skip List

# Example

From Figure 3-9, let's assume that we need to locate the structure with the attribute 9678. In the list nexus structure, we see that the highest level active pointer is at `next` [2], so we follow it. This structure has an attribute value of 5255, so we need to continue our search at this level.

We arrive back at the starting point structure, so we backtrack to the 5255 structure, drop down a level to `next` [1], and continue.

We now arrive at the structure with the 9678 attribute—it's a match! Our search is over.

In the example, it took only three searches. A simple binary search would have taken four searches.

# Pros

The skip list offers an interesting approach for searching that often results in a reduction of search times when compared to a simple binary method. Adding and removing members to and from the list is reasonably quick.