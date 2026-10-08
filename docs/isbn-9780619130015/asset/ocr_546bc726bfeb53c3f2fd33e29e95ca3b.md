Here is an example.

```
void print_square(int val)
{
    printf("\nThe square is %d", val*val);
}
```

This function takes an int argument. When it receives the argument, the function stores the argument in the variable val. The printf statement causes the value of the expression val*val to print. Here is a complete program that uses the function:

```
#include <stdio.h>
void print_square(int val);

main()
{
    int num = 5;
    print_square(num);
}
```

```
void print_square(int val)
{
    printf("\nThe square is %d\n", val*val);
}
```

The output of the program is shown in Figure 10-6.

![](bbox=[0.19, 0.58, 0.79, 0.9])

Figure 10-6: Demonstration of a function argument