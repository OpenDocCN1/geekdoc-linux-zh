
function then proceeds to calculate the value of the 20th triangular number and display the answer at the terminal.

For an example of a function that takes more than one argument, rewrite the greatest common divisor program (Program 4.7) in function form. The two arguments to the function are the two numbers whose greatest common divisor (gcd) you want to calculate. See Program 7.5.

## Program 7.5 Revising the Program to Find the Greatest Common Divisor

```c
/*  Code from image */
int
greatest(int u, int v)
{
    int t;
    printf("Original values of u and v are %d and %d\n", u, v);
    while (v != 0) {
        t = u % v;
        u = v;
        v = t;
    }
    printf("Greatest common divisor is %d\n", u);
}
```

## Program 7.5 Output

```
Click here to view code image
```

The function `greatest` is defined to take two integer arguments. The function refers to these arguments through their formal parameter names `u` and `v`. After declaring the variable `t` to be of type `int`, the program displays the values of the arguments `u` and `v`, together with an appropriate message. The function then calculates and displays the greatest common divisor of the two integers.

You might be wondering why there are two `printf` statements inside the function `greatest`. You must display the values of `u` and `v` before you enter the `while` loop because their values are changed inside the loop. If you wait until after the loop has finished, the values displayed for `u` and `v` do not at all resemble the original values that were passed to the routine. Another solution to this problem is to assign the values of `u` and `v` to two variables before entering the `while` loop. The values of these two variables can then be displayed together with the value of `u` (the greatest common divisor) using a single `printf` statement after the `while` loop has completed.

### Returning Function Results

The functions in Programs 7.4 and 7.5 perform some straightforward calculations and then display the results of the calculations at the terminal. However, you might not always want to have the results of your calculations displayed. The C language provides you with a convenient mechanism whereby the results of a function can be *returned* to the calling routine. This is not new to you because you’ve used it in all previous programs to return from `main`. The general syntax of this construct is straightforward enough:

```c
return expression;
```

This statement indicates that the function is to return the value of *expression* to the calling routine. Parentheses are placed around *expression* by some programmers as a matter of programming style, but their use is optional.

An appropriate `return` statement is not enough. When the function declaration is made, you must also declare the *type of value the function returns*. This declaration is placed immediately *before* the function’s name. Each of the previous examples in this book defined the function `main` to return an integer value, which is why the keyword `int` is placed directly before the function name. On the other hand, a function declaration that starts like this:

```c
float
kickit(float kick);
```

begins the definition of a function `kickit`, which takes one float argument called `kick` and which *returns* a floating-point value. Similarly,

```c
int
gcd(int, int);
```

defines a function `gcd` with integer arguments `u` and `v` that returns an integer value. In fact, you can modify Program 7.5 so that the greatest common divisor is not displayed by the function `greatest` but is instead returned to the `main` routine, as shown in Program 7.6.

## Program 7.6 Finding the Greatest Common Divisor and Returning the Results

```c
/*  Code from image */
#include <stdio.h>

int
gcd(int, int);

int
main(void)
{
    int x, y, z;
    printf("Enter two integers: ");
    scanf("%d%d", &x, &y);
    z = gcd(x, y);
    printf("Greatest common divisor: %d\n", z);
    return 0;
}

int
gcd(int u, int v)
{
    int t;
    while (v != 0) {
        t = u % v;
        u = v;
        v = t;
    }
    return u;
}
```

## Program 7.6 Output

```
Click here to view code image
```

After the value of the greatest common divisor has been calculated by the `gcd` function, the statement

```c
return u;
```

is executed. This has the effect of returning the value of `u`, which is the value of the greatest common divisor, back to the calling routine.

You might be wondering what you can do with the value that is returned to the calling routine. As you can see from the `main` routine, in the first two cases, the value that is returned is stored in the variable `z`. More precisely, the statement

```c
z = gcd(x, y);
```

says to call the function `gcd` with the arguments `x` and `y` and to store the value that is returned by this function in the variable `z`.

The result that is returned by a function does not have to be assigned to a variable, as you can see by the last statement in the `main` routine. In this case, the result returned by the call

```c
gcd(x, y)
```

is passed directly to the `printf` function, where its value is displayed.

A C function can only return a single value in the manner just described. Unlike some other languages, C makes no distinction between subroutines (procedures) and functions. In C, there is only the function, which can optionally return a value. If the declaration of the type returned by a function is omitted, the C compiler assumes that the function returns an `int`—if it returns a value at all. Some C programmers take advantage of the fact that functions are assumed to return an `int` by default and omit the return type declaration. This is poor programming practice and should be avoided. When a function returns a value, make certain you declare the type of value returned in the function’s header, if only for the sake of improving the program’s readability. In this manner, you can always identify from the function header not only the function’s name and the number and type of its arguments, but also if it returns a value and the returned value’s type.

As noted earlier, a function declaration that is preceded by the keyword `void` explicitly informs the compiler that the function does not return a value. A subsequent attempt at using the function in an expression, as if a value were returned, results in a compiler error message. For example, because the `celsius` function of Program 7.4 did not return a value, you placed the keyword `void` before its name when defining the function. Subsequently attempting to use this function as if it returned a value, as in

```c
celsius(fahr)
```

results in a compiler error.

In a sense, the `void` data type is actually defining the *absence* of a data type. Therefore, a function declared to be of type `void` has no value and cannot be used as if it does have a value in an expression.

In Chapter 5, “Making Decisions,” you wrote a program to calculate and display the absolute value of a number. Now, write a function that takes the absolute value of its argument and then returns the result. Instead of using integer values as you did in Program 5.1, write this function to take a floating value as an argument and to return the answer as type `float`, as shown in Program 7.7.

## Program 7.7 Calculating the Absolute Value

```c
/*  Code from image */
#include <stdio.h>

float
abs(float x)
{
    if (x < 0.0)
        return -x;
    else
        return x;
}

int
main(void)
{
    float f, r;
    int i;
    f = -1.0;
    r = abs(f);
    printf("f = %.1f, abs(f) = %.1f\n", f, r);
    r = abs(f) + abs(f);
    printf("abs(f) + abs(f) = %.1f\n", r);
    i = -4;
    r = abs((float)i) / 2.0;
    printf("abs(i) / 2 = %.1f\n", r);
    f = -6.0;
    r = abs(f) / 4;
    printf("abs(f) / 4 = %.1f\n", r);
    return 0;
}
```

## Program 7.7 Output

```
Click here to view code image
```

The `abs` function is relatively straightforward. The formal parameter called `x` is tested against zero. If it is less than zero, the value is negated to take its absolute value. The result is then returned back to the calling routine with an appropriate `return` statement.

You should note some interesting points with respect to the `main` routine that tests out the `abs` function. In the first call to the function, the value of the variable `f`, initially set to −1, is passed. Inside the function itself, this value is assigned to the variable `x`. Because the result of the `if` test is TRUE, the statement that negates the value of `x` is executed, thereby setting the value of `x` to 1. In the next statement, the value of `x` is returned to the `main` routine where it is assigned to the variable `r` and is then displayed.

When the value of `x` is changed inside the `abs` function, this in no way affects the value of the variable `f`. When `f` was passed to the `abs` function, its value was automatically copied into the formal parameter `x` by the system. Therefore, any changes made to the value of `x` inside the function affect only the value of `x` and not the value of `f`. This is verified by the second `printf` call, which displays the unchanged value of `f`. Make certain you understand that it's not possible for a function to directly change the value of any of its arguments—it can only change copies of them.

The next two calls to the `abs` function illustrate how the result returned by a function can be used in an arithmetic expression. The absolute value of `f` is added to the absolute value of `f` and the sum is assigned to the variable `r`.

The fourth call to the `abs` function introduces the notion that the type of argument that is passed to a function should agree with the type of argument as declared inside the function. Because the function `abs` expects a floating value as its argument, the integer variable `i` is first cast to type `float` before the call is made. If you omit the cast operation, the compiler does it for you anyway because it knows the `abs` function is expecting a floating argument. (This is verified by the fifth call to the `abs` function.) However, it's clearer what's going on if you do the casting yourself rather than relying on the system to do the conversion for you.

The final call to the `abs` function shows that the rules for evaluation of arithmetic expressions also pertain to values returned by functions. Because the value returned by the `abs` function is declared to be of type `float`, the compiler treats the division operation as the division of a floating-point number by an integer. As you recall, if one operand of a term is of type `float`, the operation is performed using floating arithmetic. In accordance with this rule, the division of the absolute value of −6.0 by 4 produces a result of 1.5.

Now that you've defined a function that computes the absolute value of a number, you can use it in any future programs in which you might need such a calculation performed. In fact, the next program (Program 7.8) is just such an example.

## Functions Calling Functions Calling...

With most cell phones having calculator apps on them, it’s usually no big deal to find the square root of a particular number should the need arise. But years ago, students were taught manual techniques that could be used to arrive at an approximation of the square root of a number. One such approximation method that lends itself most readily to solution by a computer is known as the Newton-Raphson Iteration Technique. In Program 7.8, you write a square root function that uses this technique to arrive at an approximation of the square root of a number.
