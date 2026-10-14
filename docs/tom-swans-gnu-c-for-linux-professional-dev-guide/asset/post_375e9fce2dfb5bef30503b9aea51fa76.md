
## PARAMETERS AND ARGUMENTS

A function's parameters provide it with input data. For example, the kilos() function in this chapter declares a parameter named miles of type double:

```
double kilos(double miles);
```

A statement such as the following passes a value to kilos() for conversion:

```
cout << kilos(100) << " kilometers" << endl;
```

The value 100 is called an argument. It is passed to the function's miles parameter. Inside the function, miles equals 100—the value of the argument. A parameter such as miles resembles a local variable in that its scope extends only to its declaring function. In this example, the scope of the miles parameter extends only to the kilos() function. Only statements in the function can refer to miles.

There are three types of function parameters: value, reference, and pointer. The following sections explain how to create and use these types of parameters.

> **Note**  
> Although the following sections explain pointer parameters briefly, their intricacies are best handled with other topics introduced in Chapter 11, "Managing Memory with Pointers."

### VALUE PARAMETERS

A value parameter is so called because only a copy of its value is passed to the function. Declare a value parameter the same way you declare a variable, but place the declaration inside the function header's parentheses:

```
void f(int i);
```

The prototype for function f() declares a single value parameter, int i. Statements that call f() pass arguments by value to parameter i, as in these samples:

```
f(10); // Pass 10 to i
f(x); // Pass value of x to i
```

To package this formula as a function, a program can prototype it like this:

```
double cost(double time, double power, double rate);
```

The cost() function returns a double value. It declares three value parameters of type double separated by commas—time, power, and rate. The completed function implements the cost formula:

```
double cost(double time, double power, double rate)
{
    return rate * (power * 0.001 * time);
}
```

Elsewhere in the program, statements can pass arguments to the function for processing. A simple statement computes the cost of running a 100-watt appliance for 10 hours at a kwh rate of 0.0687:

```
double result = cost(10.0, 100.0, 0.0687);
```

Listing 10.3, electric.cpp, puts the cost() function into action. In addition to demonstrating value function parameters, the program also shows a general-purpose method for creating a row-and-column reference table.

### LISTING 10.3 ELECTRIC.CPP

```
#include <iostream.h>
#include <stdio.h>    // Need sprintf()

#define MAXROW 12    // Number of rows in table
#define MAXCOL 8     // Number of columns in table

// Function prototypes

double cost(double time, double power, double rate);
void printTable(double startHours, double hourlyIncrement,
    double startWatts, double wattsIncrement, double costPerKwh);

int main()
{
    double startHours    = 100;
    double hourlyIncrement = 10;
    double startWatts    = 4;
    double wattsIncrement  = 2;
    double costPerKwh    = 0.0687;
    printTable(startHours, hourlyIncrement,
        startWatts, wattsIncrement, costPerKwh);
    return 0;
}

// Return cost of electricity given time, power, and rate
double cost(double time, double power, double rate)
{
    return rate * (power * 0.001 * time);
}
// Print table using the cost() function
void printTable(double startHours, double hourlyIncrement,
    double startWatts, double wattsIncrement, double costPerKwh)
{
    int row, col;        // Local variables
    double hours, watts;    // Local variables
    char buffer[24];        // Formatted output buffer

    // Print top line of table
    cout << endl << "Hrs/Watts";
    watts = startWatts;
    for (col = 1; col <= MAXCOL; col++) {
        sprintf(buffer, "%8.0f", watts);
        cout << buffer;
        watts += wattsIncrement;
    } // for

    // Print table rows
    hours = startHours;
    for (row = 1; row <= MAXROW; row++) {
        sprintf(buffer, "%6.1f ", hours);
        cout << buffer;
        watts = startWatts;
        for (col = 1; col <= MAXCOL; col++) {
            sprintf(buffer, "%8.2f", cost(hours, watts, costPerKwh));
            cout << buffer;
            watts += wattsIncrement;
        } // for
        hours += hourlyIncrement;
    } // for
    cout << endl << endl << "Cost of electricity @ ";
    sprintf(buffer, "%8.4f", costPerKwh);
    cout << buffer << " per KWH" << endl << endl;
}
```

Compile and run the program to display a table that shows the cost of running an appliance of a certain power in watts for a given number of hours. Modify main()'s local variables to display a table with a different range of values. (Alternatively, you might add statements to prompt users for input—I took the easy way out to save space in the printed listing here.) Enter these commands to display the table shown in Figure 10.1.

```
$ g++ electric.cpp
$ ./a.out
```
