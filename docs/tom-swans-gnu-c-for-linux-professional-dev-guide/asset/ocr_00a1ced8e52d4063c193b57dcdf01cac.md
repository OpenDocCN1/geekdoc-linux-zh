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

# LISTING 10.3 ELECTRIC.CPP

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
```