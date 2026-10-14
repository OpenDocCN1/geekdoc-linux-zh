
```
{
    cin >> s;
}
```

Compile and run the program with the following commands, and then as shown, enter a string, which is displayed on the last line after you press Enter:

```
$ g++ getstr.cpp
$ ./a.out
Enter a string: abcdefg
You entered: abcdefg
```

The sample program prototypes a function to input a string into a global char buffer. The function's prototype shows how to declare a pointer parameter:

void getstr(char *s);

Parameter s is a pointer to a char. Due to an age-old C specification, pointers and arrays are programmatically equivalent, and therefore, it's common to use a pointer to pass the input char array to getstr(). To use the function, the program declares input as follows and passes it to the function for filling with the user's input:

```
char input[128];
...
getstr(input);
```

## FUNCTION RETURN VALUES

As you have seen in this book's listings, functions can return nothing, or they can return a value of any valid C++ type. The following sections explain more about function return values. As a practical example, a sample listing in this section shows how to create an elapsed event timer using the standard GNU C library's time functions.

## RETURNING SIMPLE VALUES

As you have seen in many of this book's sample programs, functions might return nothing, or they might return a value of any valid C++ data type such as int or double. To indicate that a function returns nothing, precede its declaration by void:

```
void f();
```

Although allowed, this technique is rarely useful, and you normally save a function's return value in a variable, or use it in a statement as in the following examples:

```
double saved_value = f();
cout << "Value == " << f() << endl;
```

Return values are essential in constructing modular programs. As a practical demonstration, Listing 10.6, stopwatch.cpp, uses the system clock to create a timer, accurate to 1/10 second (depending, of course, on the system clock's accuracy), independent of the computer processor speed.

### LISTING 10.6 STOPWATCH.CPP

```
#include <iostream.h>
#include <sys/times.h>    // need times() function
#include <time.h>        // need CLOCKS_PER_SEC
#include <math.h>        // need fabs() function

// Function prototypes
clock_t mark_time();
double elapsed_time(clock_t start_time, clock_t end_time);

// Main program
int main()
{
    clock_t start, stop;  // Variables for mark_time() function

    cout << "Press enter to start timing...";
    cin.get();
    start = mark_time();  // Mark starting time
    cout << "Press enter to stop timing...";
    cin.get();
    stop = mark_time();   // Mark stopping time
    cout << "Elapsed time was "
         << elapsed_time(start, stop)
         << " seconds" << endl;
    return 0;
}

// Returns current processor time (mark)
clock_t mark_time()
{
    return times(NULL);
}

// Calculate elapsed time in seconds
double elapsed_time(clock_t start_time, clock_t end_time)
{
    double t = fabs(end_time - start_time);  // Processor elapsed time
    return t / (CLOCKS_PER_SEC / 10000);     // Elapsed time in seconds
}
```

Compile and run stopwatch.cpp. When prompted, press Enter to start the elapsed timer, wait a few seconds, and then press Enter again to stop timing and display the results as shown in the following test run:

persist outside the function's scope. In other words, functions may not return references to local variables or parameters. A function declared as

```
double &ref();
```

returns a reference to a double object, presumably one that is declared elsewhere. In cases where you don't want to give the function's caller the right to change a referred-to value, declare the function const like this:

```
const double &ref();
```

You may use reference functions on each side of an assignment operator. A statement such as the following stores 3.14159 in whatever double object to which the ref() function refers:

```
ref() = 3.14159;
```

The ref() function itself might be written along these lines:

```
double d;
double &ref()
{
    return d; // Return reference to d
}
```

Because ref() merely returns a reference to the global variable d, the reference function is in a sense a synonym for that object. If d is hidden away in a library module, all references to it are controlled by forcing the data's users to call ref(). This hides the inner nature of the global data and also can aid debugging.

The foregoing sample code is, however, merely for illustration. Similar but more complex programming is invaluable for hiding a data structure's internal representation while providing safe access to its information. For example, a reference function might return a value selected from an array. Reference functions also play a major role in object-oriented programming, the subject of Part III of this book.

## RETURNING POINTERS TO DATA

As with pointer parameters, this chapter wouldn't be complete without mentioning also that functions may return pointer values. But see Chapter 11, "Managing Memory with Pointers," for more information on this subject.

## OTHER FUNCTIONALITIES

Following are some additional topics about functions, including some features available only in C++.
