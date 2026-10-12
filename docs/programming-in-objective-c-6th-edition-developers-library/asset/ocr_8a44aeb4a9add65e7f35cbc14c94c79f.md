# **Pointers to Functions**

Of a slightly more advanced nature, but presented here for the sake of completeness, is the notion of a pointer to a function. When working with pointers to functions, the C compiler needs to know not only that the pointer variable points to a function, but also the type of value returned by that function as well as the number and types of its arguments. To declare a variable f to be of type “pointer to function that returns an i and that takes no arguments,” the declaration

can be written. The parentheses around \* are required because otherwise the C compiler treats the preceding statement as the declaration of a function called f that returns a pointer to an i (because the function call operator ( has higher precedence than the pointer indirection operator \*).

To set your function pointer pointing to a specific function, you simply assign the name of the function to it. So, if 1 is a function that returns an i and that takes no arguments, the statement

stores a pointer to this function inside the function pointer variable f. Writing a function name without a subsequent set of parentheses is treated in an analogous way to writing an array name without a subscript. The C compiler automatically produces a pointer to the specified function. An ampersand is permitted in front of the function name, but it’s not required.

If the 1 function has not been previously defined in the program, it is necessary to declare the function before the preceding assignment can be made. So, a statement such as

is needed before a pointer to this function can be assigned to the variable f.

You can call the function that is indirectly referenced through a pointer variable by applying the function call operator to the pointer, listing any arguments to the function inside the parentheses. For example,

calls the function pointed to by f, storing the returned value inside the variable ⊕.

One common application for pointers to functions is in passing them as arguments to other functions. The standard C library uses this, for example, in the function q, which performs a “quicksort” on an array of data elements. This function takes as one of its arguments a pointer to a function that is called whenever q needs to compare two elements in the array being sorted. In this manner, q can be used to sort arrays of any type, as the actual comparison of any two elements in the array is made by a user-supplied function, and not by the q function itself. **Appendix B, “The Standard C Library,”** goes into more detail about q and contains an actual example of its use.