
| Conversion | Description |
|---|---|
| s | A null-terminated string. You may specify a precision to restrict output to that many characters. |
| u | An unsigned decimal. |
| x | An unsigned hexadecimal using the digits 0, ..., 9 and the lowercase letters a, b, c, d, e, and f. |
| X | Same as x, but uses the uppercase letters A, B, C, D, E, and F. |

## A sprintf() EXAMPLE

Learning to put all the myriad elements together for a sprintf() statement might seem to take doctorate-level mental gymnastics. There are so many options, letters, and symbols in a formatting string that it's easy to get hung up trying to format output to look as you want. Following are some sample statements that will help you learn how to use sprintf().

One of the most common uses for sprintf() is to format date values. Suppose that your program declares variables to hold the day, month, and year like this:

```
int month = 2;
int day = 16;
int year = 2001;
```

Using sprintf(), the program can format and display the date as a string using statements such as

```
sprintf(buffer, "Date: %2d-%2d-%4d", day, month, year);
cout << buffer << endl;
```

That writes the following string to the standard output:

```
Date: 16-02-2001
```

In the sprintf() statement, the formatting command %2d specifies a precision of 2 and that the value is decimal (an integer). Using a precision value with the conversion letter d pads values with leading zeros within the specified width so that the month value 2 is written as 02. The command %4d writes the full date value 2001. (No Y2K problem here.)

The following sample program in Listing 8.8, sprintfex.cpp, gives additional examples for using sprintf() to format integer and floating point values.

### LISTING 8.8 SPRINTEFEX.CPP

```
#include <iostream.h>
#include <stdio.h>

#define BUFSIZE 128    // Size of formatting buffer

char buffer[BUFSIZE];  // Holds sprintf() output

// A few sample variables:
int xint = 123;
long xlong = 12345678L;
char xchar = 'e';
char *xstring = "This is pretty cool!";
double xdouble = 3.14159;
long double xlongdouble = xdouble * xdouble;

int main()
{
cout << "Sample printf() statements" << endl;
cout << "VARIABLE          RESULT" << endl;
sprintf(buffer, "xint (decimal) == %d", xint);
cout << buffer << endl;
sprintf(buffer, "xint (hex)      == %x", xint);
cout << buffer << endl;
sprintf(buffer, "xint (octal)    == %o", xint);
cout << buffer << endl;
sprintf(buffer, "xlong            == %ld", xlong);
cout << buffer << endl;
sprintf(buffer, "xchar            == %c", xchar);
cout << buffer << endl;
sprintf(buffer, "xstring          == %s", xstring);
cout << buffer << endl;
sprintf(buffer, "xdouble          == %lf", xdouble);
cout << buffer << endl;
sprintf(buffer, "xlongdouble(1)   == %Le", xlongdouble);
cout << buffer << endl;
sprintf(buffer, "xlongdouble(2)   == %Lf", xlongdouble);
cout << buffer << endl;
return 0;
}
```

Following is the program's output. Compare these lines with each statement's sprintf() formatting commands:

```
$ g++ sprintfex.cpp
$ ./a.out
Sample printf() statements
VARIABLE          RESULT
xint (decimal) == 123
xint (hex)      == 0x7b
xint (octal)    == 0173
xlong           == 12345678
xchar           == e
xstring         == This is pretty cool!
xdouble         == 3.141590
xlongdouble(1)  == 9.869588e+00
xlongdouble(2)  == 9.869588
```

## LUCKY PENNIES

Years ago, in my brief career as a computer store sales clerk, I had a raging argument with a customer who insisted his computer didn’t work. The fellow had written some accounting software using floating point variables, and he brought his system in repeatedly to demonstrate that it "lost pennies." I was unable to convince him that the trouble was not in his system but in his method. Floating point values in a computer’s memory are approximations, I said, and they are not appropriate for storing monetary values. Despite my explanations, the store manager ended up giving the customer his money back, even though his computer worked perfectly well.

Lucky for you and me, GNU C++ provides long and long long (double wide) integers that are perfect for storing monetary values down to the last penny. Simply represent all your monetary amounts as long or long long values and assume two decimal places. In other words, the binary values represent pennies. A long value of 32176 formatted monetarily equals $321.76.

Adding the decimal place is merely a matter of string formatting, not floating point mathematics. To demonstrate one method for inserting a decimal point into integer values, Listing 8.9, money.cpp, prompts for and formats long integer values entered at a program prompt.

### LISTING 8.9 MONEY.CPP

```
#include <iostream.h>
#include <stdio.h>    // Need sprintf()
#include <string.h>   // Need memmove()

long value;          // Value in binary
char buffer[32];     // Value in string form

main()
{
    // Prompt for value to convert
    cout << "Value? ";
    cin >> value;

    // Convert value to string form in buffer
    sprintf(buffer, "%ld", value);
    cout << "Unformatted: " << buffer << endl;

    // Move last two characters of buffer down one
    int dest = strlen(buffer) - 1;
    int src = strlen(buffer) - 2;
    memmove(&buffer[dest], &buffer[src], 3);  // Including null!

    // Insert decimal point and display results
    buffer[src] = '.';
    cout << "Formatted:   " << buffer << endl;

    return 0;
}
```
