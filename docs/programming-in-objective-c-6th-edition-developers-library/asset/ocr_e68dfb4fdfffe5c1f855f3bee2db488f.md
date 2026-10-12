sets p to point n elements farther in the array, no matter what type of element is contained in the array.

The increment and decrement operators + and - are particularly handy when dealing with pointers. Applying the increment operator to a pointer has the same effect as adding one to the pointer, while applying the decrement operator has the same effect as subtracting one from the pointer. So, if t is defined as a c pointer and is set pointing to the beginning of an array of c s called t, the statement
+
sets t pointing to the next character in t, which is t. In a similar fashion, the statement
-
sets t pointing to the previous character in t, assuming, of course, that t was not pointing to the beginning of t prior to the execution of this statement.

It is perfectly valid to compare two pointer variables in C. This is particularly useful when comparing two pointers in the same array. For example, you can test the pointer v to see if it points past the end of an array containing 100 elements by comparing it to a pointer to the last element in the array. So, the expression
v
is TRUE (nonzero) if v is pointing past the last element in the v array, and is FALSE (zero) otherwise. Recall from previous discussions that you can replace the preceding expression with its equivalent
v
because v used without a subscript is a pointer to the beginning of the v array.
(Remember, it's the same as writing & . )

Program 10.11 illustrates pointers to arrays. The a function calculates the sum of the elements contained in an array of integers.

# Program 10.11 Working with Pointers to Arrays

Click here to view code image

```
/
#
i
{
}
i
{
```