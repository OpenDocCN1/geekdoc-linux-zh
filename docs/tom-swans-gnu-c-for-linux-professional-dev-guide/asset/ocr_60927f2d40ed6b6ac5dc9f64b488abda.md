it is more common to surround even a single statement in braces:

do {
    statement;
} while (condition);

Inside the braces, you may insert as many statements as you need:

do {
    statement1;
    statement2;
    ...
} while (expression);

To demonstrate do-while, Listing 9.6, dwcount.cpp, is similar to the wcount.cpp program but uses a do-while loop to count from 1 to 10.

# LISTING 9.6 DWCOUNT.CPP

```
#include <iostream.h>

int counter;

int main()
{
    cout << "Counting with do-while" << endl;
    counter = 1;
    do {
        cout << "counter == " << counter << endl;
        counter++;
    } while (counter <= 10);
    return 0;
}
```

As you can with while loops, it is often possible to combine the use and increment of the control variable. For example, the do-while loop in dwcount.cpp can be shortened to the following:

```
do {
    cout << "counter == " << counter << endl;
} while (++counter <= 10);
```

In this case, however, the operator must be applied before counter is evaluated. In other words, the expression ++counter equals the incremented value of the variable; and, therefore, the loop executes one final time when that value is 10. If the statement used counter++ as the condition, the loop would count from 1 to 11. (The expression, however, could also be changed to (counter++ <= 10).) Here again, an off-by-one error is easy to make, and the longer version, which costs nothing in performance, is clear and understandable.