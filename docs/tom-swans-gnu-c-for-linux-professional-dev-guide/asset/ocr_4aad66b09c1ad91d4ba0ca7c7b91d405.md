```
return b;
}

// Main program
int main()
{
    int x, y, z; // Input and result variables

    cout << "X? ";
    cin >> x;
    cout << "Y? ";
    cin >> y;
    z = max(x, y);
    cout << "max(a, b) == " << z << endl;
    return 0;
}
```

The inline function max() is declared and implemented before its use in the program. This tells the compiler to expand any calls to the function by replacing those calls with the function’s statements. To compile a program with inline functions, and to have the compiler expand them, in GNU C++ you must compile with at least the first level of optimizations using the -O option. To compile the sample inline.cpp program and expand its inline max() function, use this command:

```
$ g++ -O inline.cpp
```

Running the program produces output such as

```
$ ./a.out
X? 34
Y? 96
max(a, b) == 96
```

Although the program appears to call max(), it actually executes that function’s statements as though they were written in main(). There is nothing special about an inline function’s statements. Anything that can go in a normal function can go in one declared inline.

Usually, inline functions are stored in header files, but you can write them in your program’s source code files as shown here. Just be sure to implement inline functions in full before the program uses them.

# FUNCTION OVERLOADING

All programmers face the demandingly creative job of thinking up new function names. Sure, you can invent any old name for a function—the compiler greets a function named f29q() with the same enthusiasm as it greets one named batting_average(). Humans, however, tend to better comprehend the latter name.

In a large program, coming up with good function names is no joking matter. Consider a graphics program that has to draw umpteen shapes. Each drawing function needs a unique name, leading to programs strewn with functions such as draw_ellipse(), draw_circle(), draw_square(), and draw_line(). The code probably also has numerous variables named