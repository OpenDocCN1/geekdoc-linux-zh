# ## Using Function Return Values

In addition to accepting arguments, functions may also return a value. This means you can make function calls part of arithmetic operations and assignments. For example, suppose you have a function called `triple`. It is designed to take an int argument and return that value multiplied by three. You could use the function call in a manner such as:

```
y = triple(x);
```

The function receives the value in `x`, triples it, and then returns this value. The statement above stores the return value in a variable called `y`. Here is what the `triple` function might look like:

```
int triple(int num)
{
	return(num * 3);
}
```

The function is defined as an int function. This means that it returns an int value. You may place a call to this function anywhere in your program where an int is expected. The function takes a single argument, which is also an int. In the function the argument is stored in the variable `num`. There is only one line in the function's block of code:

```
return(num*3);
```

This is the return statement. It is used to return a value back to the calling part of the program. In this example the value of `num * 3` is returned. The next sample program demonstrates the function:

```
#include <stdio.h>
int triple(int num);
int main()
{
	int x = 6, y;
	y = triple(x);
	printf("%d tripled is %d\n", x, y);
}
int triple(int num)
{
	return (num * 3);
}
```

The program output is shown in Figure 10-7.