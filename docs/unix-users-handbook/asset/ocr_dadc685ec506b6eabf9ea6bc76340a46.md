The reference array_m[0][4] is referencing the first row, last col-umn, or the element in the upper right corner, 9.

# Passing Arrays to Functions

It is possible to pass the value of an element or an entire array as an argument to a function.

To pass in a single element, a function call and function defini-tion would look as follows:

```
```c
#include <stdio.h>
void print_grade(int);        /* function prototype */
main()
{

    int grades[5] = {100, 98, 97, 87, 99}; /* declare array */
...
    print_grade( grades[0] );
    /* send the first element of the array grades into
       the function as an argument */
...
    return;
}
...
void print_grade( int a_grade)
{
    printf("The grade is %d.\n", a_grade);
}
```
```

The output of the program would be:

The grade is 100.

To access a whole array inside a function, it is only necessary to list the array name without any square brackets ([ ]) or subscripts. To