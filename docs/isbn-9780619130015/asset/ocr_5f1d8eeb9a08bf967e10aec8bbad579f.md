tells the compiler to use the ifstream class to perform file input and output operations. The identifier file follows the class name. This statement is similar to the following C statement:

```
FILE *file;
```

Further, the file.fail() function is a part of the ifstream class and reports an invalid condition with the file access. The endl stream manipulator causes the screen output to skip a line.

The file.getline() function reads in a line from the file and stores it in the buffer record_in for subsequent processing. The file.good flag is a component of ifstream class and is used to determine if the record accessed contains data.

Now that you have an understanding of how C++ is similar to C, next you'll see how C++ provides additional enhancements.

# ## How C++ Enhances C Functions

C++ created a way to define a function so that it can handle multiple sets of criteria, called **function overloading**. Whereas C functions are quite flexible, function overloading adds considerably to their overall use by expanding the function definition to accept varying kinds and numbers of parameters. During compilation, the C++ compiler determines which function to call based on the number and types of parameters the calling statement passes to the function. For example, in the next exercise you overload a function to access the system date in two different ways.

> **To use function overloading:**

**1** Use the editor of your choice to type the contents of datestuf.C:

```
// Program name: datestuf.C
// Purpose: shows you two ways to access the system date.
#include <iostream.h>
#include <time.h>

void display_time(const struct tm *tim)
{
    cout << "1. It is now " << asctime(tim);
}

void display_time(const time_t *tim)
{
    cout << "2. It is now " << ctime(tim);
}
```