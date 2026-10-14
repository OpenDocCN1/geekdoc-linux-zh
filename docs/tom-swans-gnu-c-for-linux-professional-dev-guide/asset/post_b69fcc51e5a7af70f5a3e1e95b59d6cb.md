
ellipse, circle, square, and line, and the resulting source code appears to have developed a bad stammer:

```
draw_ellipse(ellipse);
draw_circle(circle);
draw_square(square);
draw_line(line);
```

Wouldn’t it be great if you could use the same function name—let’s call it draw()—to draw all shapes? Then, you could simply write:

```
draw(ellipse);
draw(circle);
draw(square);
draw(line);
```

This is the kind of clarity that function overloading provides. In C++, multiple functions may have the same names as long as they differ in at least one parameter data type. The functions are “overloaded” because, although named the same, they perform distinct actions. The four draw() functions in this hypothetical graphics program are still separate, and they are written just as other nonoverloaded functions. However, the C++ compiler recognizes them by the way they are used, not only by their names.

A sample program demonstrates how function overloading can help simplify a program’s source code. Listing 10.9, overload.cpp, uses an overloaded function named square() to display the square product of three variables, each of a different data type.

```
// LISTING 10.9   OVERLOAD.CPP
#include <iostream.h>

// Overloaded-function prototypes
int square(int a);
double square(double a);
long double square(long double a);

int main()
{
    // Declare and initialize some variables
    int x = 10;
    double y = 20.5;
    long double z = 30.75;

    // Display the variables' square products
    cout << square(x) << endl;
    cout << square(y) << endl;
    cout << square(z) << endl;
    return 0;
}

// Returns the square of an int
int square(int a)
{
    return a * a;
}
```

```
// Returns the square of a double
double square(double a)
{
    return a * a;
}

// Returns the square of a long double
long double square(long double a)
{
    return a * a;
}
```

Running the program displays the square of three different types of variables, showing onscreen the following text:

```
$ g++ overload.cpp
$ ./a.out
100
420.25
945.562
```

The program prototypes three overloaded square() functions. Each function has the same name but declares a different type of parameter. The parameter names don't matter; only their types must be different.

Overloaded functions can clarify a program's meaning. They also help automatically select the correct function to call. In the sample program, this statement calls the correct function for whatever the argument type (y in this case) happens to be:

```
cout << square(y) << endl;
```

Contrast that with the conventional method of creating differently named functions. If, for example, the program has a square_int() function, the following statement may or may not do what the programmer intends:

```
cout << square_int(y) << endl; // ???
```

Such code makes the programmer responsible for passing objects of the correct type to square_int(). By overloading the square() function, the compiler makes the correct choice for you. Of course, it's up to you to overload functions that perform more or less the same jobs. If you haphazardly give many functions the same name, your program will be as comprehensible as a book written with only one word.

> Note
> Overloaded functions are essential ingredients in object-oriented programming, introduced in Part III, "Object-Oriented Programming"

## RECURSIVE FUNCTIONS

The concept of recursion strikes many as more theoretical than practical, but it is actually a common, everyday event. When you peer into a mirror with another mirror behind, you see an endless series of images infinitely recurring themselves. Imagine is a recursion of light from the one before.

In programming, recursion occurs when a function calls itself—like dialing your own number, but, although in C++, you don’t get a busy signal. The return addresses of such calls are stacked in memory like reflections in facing mirrors, until some event causes the recursion to unwind. Some algorithms are naturally recursive. For example, the factorial of a value equals that value times the product of its preceding sequential values. The factorial of 5 equals 1 * 2 * 3 * 4 * 5, or 120—equal to 5 times the factorial of 4. From this observation, you can write a recursive factorial function such as in Listing 10.10, fact.cpp.

```
// LISTING 10.10   FACT.CPP
#include <iostream.h>

double factorial(int number);

int main()
{
    int input = 8;
    cout << "Factorial of " << input << " = ";
    cout << factorial(input) << endl;
    return 0;
}

double factorial(int number)
{
    if (number > 1)
        return number * factorial(number - 1);
    return 1;
}
```

Compile and run the demonstration program with these commands:

```
$ g++ fact.cpp
$ ./a.out
Factorial of 8 = 40320
```

To understand the factorial() function, consider the essential fact that the factorial of n equals n times the factorial of (n - 1). In other words, the factorial of 4 equals 4 * 3 * 2 * 1. The factorial of 3 equals 3 * 2 * 1. So, the factorial of 4 must equal 4 times the factorial of 3. The factorial() function uses recursion to implement this self-defining algorithm. The statement

```
d = factorial(8);
```

sets d equal to 40,320 (8 * 7 * ... * 1).
