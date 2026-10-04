# Chapter 5. Using Lists and Arrays

If you are familiar with compiled languages such as C or Pascal, you may want to consider why you use particular constructs in your programs instead of others. In some cases, you may do so because of the machine and language architecture, rather than because the problem and the data structure match. In some cases you'll find that the Tcl data types are better suited than the more familiar constructs.

When programming in compiled languages such as C or Pascal, there are several reasons for using linked lists:

+   - Linked lists provide an open-ended data structure; you don't need to declare the number of entries at compile time.
- Data can be added to or deleted from linked lists quickly.
- Entries in a linked list can be easily rearranged.
- Linked lists can be used as container classes for other data.

All of these features are supported by the Tcl list. In fact, the internal implementation of the Tcl list allows data items to be swapped with fewer pointer changes than exchanging entries in a linked list. This allows commands such as `sort` to run very efficiently.

The important reason for using linked lists is that you have data that can be conceptualized as a list of items. The Tcl list is ideal for this purpose, and as a programmer you can spend your time developing the algorithm for handling your data, instead of developing a linked list subroutine package.

A binary tree is frequently used in C or Pascal to search for data efficiently. In Tcl, the indices of an associative array are stored in a very efficient hash table. Rather than implementing a binary tree for data access purposes, you can use an associative array and get the speed of a good hash algorithm for free. Depending on the depth of your tree, the hash search is very likely to be faster than a binary search, without the overhead of balancing the tree.

Tcl is most commonly used for applications that are not speed critical, and the speed of the list or array is generally adequate. If your application grows and becomes bound by Tcl data constructs, you can extend the interpreter with other faster data representations. Extending the interpreter will be covered in Chapter 12.