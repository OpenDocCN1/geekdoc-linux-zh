```
```cpp
// LISTING 9.11  FORSCOPE.CPP
#include <iostream.h>

int main()
{
    for (int i = 1; i <= 10; i++)
        cout << "i = " << i << endl;
    cout << "Final value of i == " << i << endl;   // ???
    return 0;
}
```
```

Compiling the forscope.cpp test program with GNU C++ using the following commands produces two warning messages:

```
```text
$ g++ forscope.cpp
forscope.cpp: In function 'int main()':
forscope.cpp:7: warning: name lookup of 'i' changed for new ANSI 'for' scoping
forscope.cpp:5: warning: using obsolete binding at 'i'
```
```

The compiler issues the warnings because the program’s for loop declares an it inside the loop, and the new ANSI C++ rules state that in such cases is available only to statements inside the loop itself. However, the test program refers to i outside the loop as was permitted in past ANSI C++ drafts. To accommodate older programs that rely on the obsolete specifications, GNU C++ treats the condition as a warning rather than an error, and it completes the compilation. Other C++ compilers might refuse to compile this program at all.

To limit the scope of variables to the for loop that declares them, in GNU C++, compile with the option **-ffor-scope**. With this option, forscope.cpp does not compile. To use the older specification that places the for loop variable in the outer scope, use the **-fno-for-scope** option. Do that only if you are compiling older programs that assume the nonstandard rule. With that option, forscope.cpp compiles without any warnings or errors.

# SUMMARY

Without intervention, a C or C++ program’s statements execute one after the other like water flowing down a river. C and C++ provide conditional and repetitive flow-control statements that alter this normal path. Conditional statements include if, if-else, switch, and conditional expressions. Repetitive statements include while, do-while, and for. In addition, this chapter explained how to use break, continue, and goto statements, and it explained the controversial subject of declaring control variables inside for loops.

For more information on subjects introduced in this chapter, turn to the following chapters:

+   - Chapter 6, “Creating Data Objects”
+   - Chapter 7, “Applying Fundamental Operators”
+   - Chapter 10, “Creating and Calling Functions”