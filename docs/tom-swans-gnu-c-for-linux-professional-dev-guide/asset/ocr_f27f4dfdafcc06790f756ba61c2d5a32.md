This code demonstrates a general-purpose method that's useful for performing any action at regular intervals—in this case, starting a new line at a specified column. This is a common task inside for statements and repetitive loops. Beginners often incorrectly program the job like this:

```
if (columns++ == NUMCOLS) {
    cout << endl;
    columns = 0;    // ???
}
```

That does not work because of a subtle logical error. On the first iteration of the for loop, because of the if statement's expression columns++, columns equals 1 before the program reaches the output statement. Setting columns back to zero after starting a new line causes an additional column to be printed on lines two and beyond. Even though columns is initially zero because it is a global variable, it must be reset to 1, not 0, in the preceding if statement:

```
columns = 1;
```

This is another good example of a common off-by-one error. To avoid this sort of trouble, when you need to perform an action at regular intervals, rather than test whether a variable such as columns equals NUMCOLS and then reset that value to zero, it's easier and more intuitive to use the modulo operator as shown in the ascii.cpp listing.

# The break Statement

It's sometimes useful to interrupt a while, do-while, or for loop in progress. To do that, use a break statement—for example, if inside the loop, a statement detects an error. In general, break is typically used as follows to test an additional condition:

```
while (condition1) {
    statement;
    if (condition2)
        break;
}
```

The loop executes the statement normally while condition1 is true. However, if condition2 becomes true, the break statement immediately ends the while loop, and the program continues with the next statement. For example, the statement might set an error flag to true, in which case break ends the loop. Listing 9.8, breaker.cpp, demonstrates the effect of a break statement.

```
LISTING 9.8    BREAKER.CPP
#include <iostream.h>

int count;

int main()
{
    count = 1;
    while (count <= 100)  {

```