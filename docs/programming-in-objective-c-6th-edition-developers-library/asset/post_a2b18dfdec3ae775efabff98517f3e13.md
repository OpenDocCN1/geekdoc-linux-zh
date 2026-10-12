
## Program 7.15 Output

N 100
B 8
C

## Program 7.15 Output (Rerun)

N 1983
B 0
C

Notice how the wise choice of function names makes the operation of Program 7.15 clear. Spelled out directly in the `main` routine is the function of the program: to get a number and a base, convert the number, and then display the converted number. The much-improved readability of this program over the equivalent one from Chapter 6 is a direct result of the structuring of the program into separate functions that perform small, well-defined tasks. Note that you do not even need comment statements inside the `main` routine to describe what the program is doing—the function names speak for themselves.

The primary use of global variables is in programs in which many functions must access the value of the same variable. Rather than having to pass the value of the variable to each individual function as an argument, the function can explicitly reference the variable instead. There is a drawback with this approach. Because the function explicitly references a particular global variable, the generality of the function is somewhat reduced. So, every time that function is to be used, you must ensure that the global variable exists, by its particular name.

For example, the `conv` function of Program 7.15 succeeds in converting only a number that is stored in the variable `n` to a base as specified by the value of the variable `b`. Furthermore, the variable `d` and the array `c` must be defined. A far more flexible version of this function would allow the arguments to be passed to the function.

Although the use of global variables can reduce the number of arguments that need to be passed to a function, the price that must be paid is reduced function generality and, in some cases, reduced program readability. This issue of program readability stems from the fact that if you use global variables, the variables that are used by a particular function are not evident simply by examining the function's header. Also, a call to the particular function does not indicate to the reader what types of parameters the function needs as inputs or produces as outputs.

Some programmers adopt the convention of prefixing all global variable names with the letter “g”. For example, their variable declarations for Program 7.15 might look like this:

The reason for adopting such a convention is that it becomes easier to pick out a global variable from a local one when reading through a program. For example, the statement `gn = gc + 1;` implies that `gn` is a global variable and `gc` is a global one. This tells the reader of this line about the scope of these variables and where to look for their declarations.

One final thing about global variables. They do have default initial values: zero. So, in the global declaration `int g[100];`, all 100 elements of the `g` array are set to zero when the program begins execution. So remember that although global variables have default initial values of zero, local variables have no default initial value and so must be explicitly initialized by the program.

## Automatic and Static Variables

When you normally declare a local variable inside a function, as in the declaration of the variables `count` and `error` in your `setup` function, you are declaring automatic local variables. Recall that the keyword `auto` can, in fact, precede the declaration of such variables, but is optional because it is the default case. An automatic variable is, in a sense, actually created each time the function is called. In the preceding example, the local variables `error` and `count` are created whenever the `setup` function is called. As soon as the `setup` function is finished, these local variables “disappear.” This process happens automatically, hence the name automatic variables.

Automatic local variables can be given initial values, as is done with the values of `error` and `count`, previously. In fact, any valid C expression can be specified as the initial value for a simple automatic variable. The value of the expression is calculated and assigned to the automatic local variable each time the function is called. And because an automatic variable disappears after the function completes execution, the value of that variable disappears along with it. In other words, the value an automatic variable has when a function finishes execution is guaranteed not to exist the next time the function is called.

If you place the word `static` in front of a variable declaration, you are in an entirely new ballgame. The word `static` in C refers not to an electric charge, but rather to the notion of something that has no movement. This is the key to the concept of a static variable—it does not come and go as the function is called and returns. This implies that the value a static variable has upon leaving a function is the same value that variable will have the next time the function is called.

Static variables also differ with respect to their initialization. A static, local variable is initialized only once at the start of overall program execution—and not each time that the function is called. Furthermore, the initial value specified for a static variable must be a simple constant or constant expression. Static variables also have default initial values of zero, unlike automatic variables, which have no default initial value.

In the function `add`, which is defined as follows:

```c
int add(int x, int y) {
    static int calls = 0;
    calls++;
    return x + y;
}
```

the value of `calls` is initialized to 0 only once when program execution begins. To set its value to 100 each time the function is executed, an explicit assignment statement is needed.

Of course, reinitializing `calls` this way defeats the purpose of using a static variable in the first place.

Program 7.16 should help make the concepts of automatic and static variables a bit clearer.

## Program 7.16 Illustrating Static and Automatic Variables

Inside the `counter` function, two local variables are declared. The first variable, called `auto_var`, is an automatic variable of type `int` with an initial value of 1. The second variable, called `static_var`, is a static variable, also of type `int` and also with an initial value of 1. The function calls the `print` routine to display the values of these two variables. After this, the variables are each incremented by 1, and execution of the function is then complete.

The `main` routine sets up a loop to call the `counter` function five times. The output from Program 7.16 points out the difference between the two variable types. The value of the automatic variable is listed as 1 for each line of the display. This is because its value is set to 1 each time the function is called. On the other hand, the output shows the value of the static variable steadily increasing from 1 through 5. This is because its value is set equal to 1 only once—when program execution begins—and because its value is retained from one function call to the next.

The choice of whether to use a static variable or automatic variable depends upon the intended use of the variable. If you want the variable to retain its value from one function call to the next (for example, consider a function that counts the number of times that it is called), use a static variable. Also, if your function uses a variable whose value is set once and then never changes, you might want to declare the variable `static`, as it saves the inefficiency of having the variable reinitialized each time that the function is called. This efficiency consideration is even more important when dealing with arrays.

From the other direction, if the value of a local variable must be initialized at the beginning of each function call, an automatic variable seems the logical choice.

## Recursive Functions

The C language supports a capability known as recursive function. Recursive functions can be effectively used to succinctly and efficiently solve problems. They are commonly used in applications in which the solution to a problem can be expressed in terms of successively applying the same solution to subsets of the problem. One example might be in the evaluation of expressions containing nested sets of parenthesized expressions. Other common applications involve the searching and sorting of data structures called trees and lists.

Recursive functions are most commonly illustrated by an example that calculates the factorial of a number. Recall that the factorial of a positive integer n, written n!, is simply the product of the successive integers 1 through n. The factorial of 0 is a special case and is defined equal to 1. So 5! is calculated as follows:

5! = 5 × 4 × 3 × 2 × 1

And 6! is calculated like so:

6! = 6 × 5 × 4 × 3 × 2 × 1

Comparing the calculation of 6! to the calculation of 5!, observe that the former is equal to 6 times the latter; that is, 6! = 6 × 5!. In the general case, the factorial of any positive integer n greater than zero is equal to n multiplied by the factorial of n - 1:

n! = n × (n - 1)!

The expression of the value of n! in terms of the value of (n-1)! is called a recursive definition because the definition of the value of a factorial is based on the value of another factorial. In fact, you can develop a function that calculates the factorial of an integer n according to this recursive definition. Such a function is illustrated in Program 7.17.
