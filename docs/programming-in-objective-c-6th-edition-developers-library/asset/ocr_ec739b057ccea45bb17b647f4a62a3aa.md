can be used to invoke a function that multiplies each element in the matrix by the value of the m                                                                       . This implies, of course, that the function itself can change the values contained inside array. The discussion of this topic    for single-dimensional arrays also applies here: An assignment made to any element of the formal parameter array inside the function makes a permanent change to the array that was passed to the function.

When declaring a single-dimensional array as a formal parameter inside a function, you learned that the actual dimension of the array is not needed; simply use a pair of empty brackets to inform the C compiler that the parameter is, in fact, an array. This does not totally apply in the case of multidimensional arrays. For a two-dimensional array, the number of rows in the array can be omitted, but the declaration *must* contain the number of columns in the array. So the declarations

> Click here to view code image

```
i                    
and
i                    
```

are both valid declarations for a formal parameter array called a                                                                             containing 100 rows by 50 columns; but the declarations

```
i                    
and
i                    
```

are not because the number of columns in the array *must* be specified.

In [Program 7.13](#), you define a function s                                                                        , which multiplies a two-dimensional integer array by a scalar integer value. Assume for purposes of this example that the array is dimensioned 3 × 5. The m                                                                                                                                .2 routine calls the s                              .2 routine twice. After each call, the array is passed to the d                .2 routine to display the contents of the array. Pay careful attention to the nested f         .2 loops that are used in both s        .2 and d         .2 to sequence through each element of the two-dimensional array.

# Program 7.13 Using Multidimensional Arrays and Functions

> Click here to view code image

```
#
i                    
{
```