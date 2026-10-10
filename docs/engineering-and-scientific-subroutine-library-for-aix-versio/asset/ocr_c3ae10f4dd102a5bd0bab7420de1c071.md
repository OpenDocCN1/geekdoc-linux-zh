# IBSrch, SBSRCh, and DBSrch

where:
 x is a sequence of length *n*, containing the search elements.
 *y* is a sequence of length *m* to be searched. It must be sorted into ascending order.
 INDX is the array of length *n* of indices.
 RC is the array of length *n* of return codes.

See reference [77]. If *n* is 0, no search is performed. If *m* is 0, then:
 INDX(i) = 1 and RC(i) = 1 for *i* = 1, *n*

It is important to note that a negative stride for sequence *y* reverses the direction of the search, because the order of the sequence elements is reversed in the array. For more details on sorting sequences, see "Function" on page 879.

# Error Conditions

Computational Errors: None

Input-Argument Errors:
 1. *n* < 0
 2. *m* < 0
 3. *iOPT* ≠ 0 or 1

# Example 1

This example shows a search where sequences *x* and *y* have positive strides, and where the optional return codes are returned as part of the output.

# Call Statement and Input:

```
```
                X        INCX        N
        |        |        |
CALL IBSRCH( X , 2 , 5 , Y , 1 , 10 , INDX , RC , 1 )
```
```
        X    = (-3, . , 125, . , 30, . , 20, . , 70)
        Y    = (10, 20, 30, 40, 50, 60, 80, 90, 100)
```
```

# Output:

```
```
        INDX   = (1, 11, 3, 2, 8)
        RC     = (1, 1, 0, 0, 1)
```
```

# Example 2

This example shows the same calling sequence as in Example 1, except that it includes the IOPT argument, specified as 1. This is equivalent to using the calling sequence in Example 1 and gives the same results.

# Call Statement and Input:

```
```
                X        INCX        N
        |        |        |
CALL IBSRCH( X , 2 , 5 , Y , 1 , 10 , INDX , RC , 1 )
```
```

# Example 3

This example shows a search where sequence *x* has a negative stride, and sequence *y* has a positive stride. The optional return codes are not requested, because IOPT is specified as 0.

# Call Statement and Input:

```
```
                X        INCX        N
        |        |        |
CALL IBSRCH( X , -2 , 5 , Y , 1 , 10 , INDX , RC , 0 )
```
```