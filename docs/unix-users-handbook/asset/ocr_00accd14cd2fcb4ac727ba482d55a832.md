To reference an element in the array, the index number is used. To refer to a specific element, use the array name followed by the index number between square brackets ( [ ] ). The index number is referred to as a subscript when accessing information in an array. The code fragment below is declaring an array called grades and placing a value into the first and third elements of the array:

```
```c
int grades[ 5 ];
...
grades[ 0 ] = 100;
grades[ 2 ] = 87;
```
```

Loops are very useful when dealing with arrays. If a program has populated the array called grades with five student test scores, the sum of the grades in the array can be found with the following for loop:

```
```c
for ( x = 0; x < 5; x ++ ) /* loop five times */
    sum += grades[x]; /* short hand for sum = sum + grades[x] */
```
```

The for loop traverses the array, starting with the first element, grades[0]. The loop occurs five times, once for each element in the array. The x variable is used as a subscript to reference the elements in the array.

One of the more common errors in C is when the index is out of range. If x <= 5 were used in the conditional expression of the loop, it would have looped a 6th time and tried to access grades[5], which does not exist. This error would not show up at compile time; it would be seen only during the execution of the program. You may get unpredictable results, or it could result in a segmentation violation and core dump.

An array can be initialized with values at the time it is declared by using: