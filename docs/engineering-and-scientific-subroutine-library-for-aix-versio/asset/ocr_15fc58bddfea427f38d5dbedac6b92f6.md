# Chapter 13. Sorting and Searching

The sorting and searching subroutines are described in this chapter.

# Overview of the Sorting and Searching Subroutines

The sorting and searching subroutines operate on three types of data: integer, short-precision real, and long-precision-real ( Table 155). The sorting subroutines perform sorts with or without index designations. The searching subroutines perform either a binary or sequential search.

# Table 155. List of Sorting and Searching Subroutines

| Descriptive Name | Integer Subroutine | Short- Precision Subroutine | Long- Precision Subroutine | Page |
| :--- | :--- | :--- | :--- | :--- |
| Sort the Elements of a Sequence | ISORT | SSORT | DSORT | 879 |
| Sort the Elements of a Sequence and Note the Original Element Positions | ISORTX | SSORTX | DSORTX | 881 |
| Sort the Elements of a Sequence Using a Stable Sort and Note the Original Element Positions | ISORTS | SSORTS | DSORTS | 884 |
| Binary Search for Elements of a Sequence X in a Sorted Sequence Y | IBSRCH | SBSRCH | DBSRCH | 887 |
| Sequential Search for Elements of a Sequence X in the Sequence Y | ISSRCH | SSSRCH | DSSRCH | 891 |

# Use Considerations

It is important to understand the concept of stride for sequences when using these subroutines. For example, in the sort subroutines, a negative stride causes a sequence to be sorted into descending order in an array. In the search subroutines, a negative stride reverses the direction of the search. See “How Stride Is Used for Vectors” on page 58.

# Performance and Accuracy Considerations

+   1. The binary search subroutines provide better performance than the sequential search subroutines because of the nature of the searching algorithms. However, the binary search subroutines require that, before the subroutine is called, the sequence to be searched is sorted into ascending order. Therefore, if your data is already sorted, a binary search subroutine is faster. On the other hand, if your data is in random order and the number of elements being searched for is small, a sequential search subroutine is faster than doing a sort and binary search.
+   2. When doing multiple invocations of the binary search subroutines, you get better overall performance from the searching algorithms by doing fewer invocations and specifying larger search element arrays for argument x.
+   3. If you do not need the results provided in array RC by these subroutine, you get better performance if you do not request it. That is, specify 0 for the iopt argument.