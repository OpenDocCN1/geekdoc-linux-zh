# Appendix B Debugging the Linux Kernel

**Example** B–1 shows an example for the graphic representation of data structures in ddd. This example uses a fragment from a concrete variant of data structures to represent some of the routing tables described in Chapter 16.

The entry point is a global array, fn_tables, the 254th element of which is the fib_table structure of the routing table main. The fn_hash_structure (reachable as (struct fn_hash *) fib_tables[254]->tb data) is appended to the main table. The fn_hash_structure has a number of pointers to fn_zone structures for prefix lengths 0 through 31 in its fn_zones array. The figure represents the data structure for the prefix with length 8. An explicit type conversion is required to display the hash table referenced size cannot be derived from the pointer type, fz_hash. Specifically, we have to give the expression that describes this pointer a leading (struct fib_node [16]) * to make the hash table visible, as shown in the figure. The eighth element of the hash table is null and refers to a fib_node structure for the prefix 10.0.0/8 (where the prefix length can be derived from the fn_zone structure further up). The figure also represents the associated fib_info structure, and the fib_prefs element of that structure contains the source address 10.0.0.1 in hexadecimal representation (in network byte order) and the hooked fib_nh structure.

![](bbox=[0.178, 0.403, 0.9, 0.893])

FIGURE B–1
Example using ddd: Checking routing-table data structures (See Chapter 16).