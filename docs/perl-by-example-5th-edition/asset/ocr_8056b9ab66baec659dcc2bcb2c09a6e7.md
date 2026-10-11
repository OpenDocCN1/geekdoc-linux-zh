# EXPLANATION

1   The array @list1 is assigned a list of numbers between 1 and 100.
2   The array @list2 is assigned the list of numbers 5, 10, 15, and 20.
3   The addempt subroutine is called. Two arguments are passed. The backslash preceding each of the arrays causes references to be passed.
4   The subroutine addempt is declared and defined.
5   The references are passed to the @__ array and assigned to my variables $arr1 and $arr2, respectively.
6   The my variable $total is declared.
7, 8, 9   The address or values of the references are printed.
10  The foreach loop is entered. @$arr1 and @$arr2 dereference the references, creating a list of array elements to be processed, one at a time.
11  Each time through the loop, $total accumulates the sum of $total + $num.
12  The sum is returned to where the subroutine was called on line 3. Since the subroutine was called as an argument to the print function, the results will be printed after they are returned from the subroutine.

# ### 12.1.6 The ref Function

The *ref* function is used to test for the existence of a reference. It returns a non-empty string if its argument is a reference and with no argument, $_ is used. The string returned is the type of data the reference points to; for example, *SCALAR* is returned if the reference points to a scalar, and *ARRAY* is returned if it points to an array. If the argument is not a reference, the empty string is returned. Table 12.1 lists the values returned by the *ref* function.

# **Table 12.1**  Return Values \* from the *ref* Function

| What Is Returned | Meaning |
| :--- | :--- |
| REF | Reference to reference |
| SCALAR | Reference to scalar |
| ARRAY | Reference to array |
| HASH | Reference to hash |
| CODE | Reference to subroutine |
| GLOB | Reference to typeglob |

\* For a complete list, see *perldoc -l ref*.