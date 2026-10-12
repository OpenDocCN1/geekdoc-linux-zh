
## Communication Between Modules

Several methods can be used so that the modules contained in separate files can effectively communicate. If a function from one file needs to call a function contained inside another file, the function call can be made in the normal fashion, and arguments can be passed and returned in the usual way. Of course, in the file that calls the function, you should *always make certain to include a prototype declaration so the compiler knows the function's argument types and the type of the return value*. As noted in [Chapter 13, “Extending Data Types with the Enumerated Data Type, Type Definitions, and Data Type Conversions,”](#), in the absence of any information about a function, the compiler assumes it returns an `int` and converts `sc` arguments to `int` arguments to `d` when the function is called.

It’s important to remember that even though more than one module might be specified to the compiler at the same time on the command line, *the compiler compiles each module independently*. That means that no knowledge about structure definitions, function return types, or function argument types is shared across module compilations by the compiler. It’s totally up to you to ensure that the compiler has sufficient information about such things to correctly compile each module.

## External Variables

Functions contained in separate files can communicate through *external variables*, which are effectively an extension to the concept of the global variable discussed in [Chapter 7, “Working with Functions.”](#)

An external variable is one whose value can be accessed and changed by another module. Inside the module that wants to access the external variable, the variable is declared in the normal fashion and the keyword `extern` is placed before the declaration. This signals to the system that a globally defined variable from another file is to be accessed.

Suppose you want to define an `int` variable called `minn`, whose value you want to access and possibly modify from within a function contained in another file. In [Chapter 7,](#) you learned that if you wrote the statement

`int minn;`

at the beginning of your program, *outside* of any function, then its value could be referenced by any function within that program. In such a case, `minn` was defined as a global variable. Actually, this same definition of the variable `minn` also makes its value accessible by functions contained in other files. Specifically, the preceding statement defines the variable `minn` not just as a global variable, but also as an *external* global variable. To reference the value of an external global variable from another module, you must declare the variable to be accessed, preceding the declaration with the keyword `extern`, as follows:

`extern int minn;`

The value of `minn` can now be accessed and modified by the module in which the preceding declaration appears. Other modules can also access the value of `minn` by incorporating a similar `extern` declaration in the file.

You must obey an important rule when working with external variables. The variable has to be *defined* in some place among your source files. This is done in one of two ways. The first way is to declare the variable outside of any function, *not preceded* by the keyword `extern`, as follows:

Here, an initial value can be optionally assigned to the variable, as was shown previously. The second way to define an external variable is to declare the variable outside of any function, placing the keyword `extern` in front of the declaration, and *explicitly assigning an initial value to it*, as follows:

```c
extern int i = 5;
```

Note that these two ways are mutually exclusive. When dealing with external variables, the keyword `extern` can only be omitted in one spot throughout your source files. If you don’t omit the keyword in any one spot, in exactly one place, you must assign the variable an initial value.

Take a look at a small program example to illustrate the use of external variables. Suppose you type the following code into a file called `main.c`:

```c
#include <stdio.h>

int i;

int main()
{
    printf("%d\n", i);
    return 0;
}
```

The definition of the global variable `i` in the preceding program makes its value accessible by any module that uses an appropriate `extern` declaration. Suppose you now type the following statements into a file called `foo.c`:

```c
extern int i;

void f(void)
{
    i = 5;
}
```

Compiling the two modules `main.c` and `foo.c` together with a command like

```bash
$ gcc main.c foo.c
```

and subsequently executing the program produces the following output at the terminal:

```
5
```

This output verifies that the function `f` is able to access and change the value of the external variable `i`.

Because the value of the external variable `i` is referenced *inside* the function `f`, you could have placed the `extern` declaration of `i` inside the function itself, as follows:

```c
void f(void)
{
    extern int i;
    i = 5;
}
```

If many functions in the file need to access the value of i, it is easier to make the declaration just once at the front of the file. However, if only one function or a small number of functions need to access this variable, there is something to be said for making separate declarations in each such function: It makes the program more organized and isolates the use of the particular variable to those functions that actually use it.

When declaring an external array, it is not necessary to give its size. Thus, the declaration
e
enables you to reference a character array t that is defined elsewhere. As with formal parameter arrays, if the external array is multidimensional, all but the first dimension must be specified. Thus, the declaration
e
suffices to declare a two-dimensional external array m that contains 50 columns.

### Static Versus Extern Variables and Functions

You now know that any variable defined outside of a function is not only a global variable, but is also an external variable. Many situations arise in which you want to define a variable to be global but not external. In other words, you want to define a global variable to be local to a particular module (file). It makes sense to want to define a variable this way if no functions other than those contained inside a particular file need access to the particular variable. This can be accomplished in C by defining the variable to be static.

The statement
```c
static int m;
```
if made outside of any function, makes the value of m accessible from any subsequent point in the file in which the definition appears, but not from functions contained in other files. If you need to define a global variable whose value does not have to be accessed from another file, declare the variable to be static. This is a cleaner approach to programming: The static declaration more accurately reflects the variable’s usage and no conflicts can be created by two modules that unknowingly both use different external global variables of the same name.

As mentioned earlier in this chapter, you can directly call a function defined in another file. Unlike variables, no special mechanisms are required; that is, to call a function contained in another file, you don’t need an extern declaration for that function.

When a function is defined, it can be declared to be extern or static, the former case being the default. A static function can be called only from within the same file as the function appears. So, if you have a function called func, placing the keyword static before the function header declaration for this function makes it callable only from within the file in which it is defined:

```c
static void func(void)
{
}
```

The definition of the static function effectively becomes local to the file in which it is defined. It cannot be called from outside the file.

The same motivations previously cited for using static variables also apply to the case of static functions.

Figure 14.1 summarizes communication between different modules. Here two modules are depicted, `mod1.c` and `mod2.c`.

**mod1.c**
```c
double x;
static double result;

static void doSquare(void)
{
    double square(void);

    x = 2.0;
    result = square();
}

int main(void)
{
    doSquare();
    printf("%g\n", result);
    return 0;
}
```

**mod2.c**
```c
extern double x;

double square(void)
{
    return x * x;
}
```

Figure 14.1 Communication between modules.

`mod1.c` defines two functions: `doSquare` and `main`. The way things are set up here, `main` calls `doSquare`, which in turn calls `square`. This last function is defined in the module `mod2.c`.

Because `doSquare` is declared `static`, it can only be called from within `mod1.c`, and by no other module.

`mod1.c` defines two global variables: `x` and `result`, both of type `double`. `x` can be accessed by any module that is linked together with `mod1.c`. On the other hand, the keyword `static` in front of the definition of `result` means that it can only be accessed by functions defined inside `mod1.c` (namely `main` and `doSquare`).

When execution begins, the `main` routine calls `doSquare`. This function assigns the value 2.0 to the global variable `x` and then calls the function `square`. Because `square` is defined in another source file (inside `mod2.c`), and because it doesn't return an `int`, `doSquare` properly includes an appropriate declaration at the beginning of the function.

The `square` function returns as its value the square of the value of the global variable `x`. Because `square` wants to access the value of this variable, which is defined in another source file (in `mod1.c`), an appropriate `extern` declaration appears in `mod2.c` (and, in this case, it makes no
