
## S

- character strings, 218-226
  - containing structures, 183-185
  - functions, 169-177
  - illustrating, 165, 186-187
  - initializing, 178-179
  - pointers, 239-251
  - setting, gdb (GNU Debugger), 407-408
  - storing dates, 164-169
  - storing time, 175-177
  - using in expressions, 166-169
  - variants, 189
- switch statement, 83-86, 463-464
- system ("mkdir/usr/tmp/data") function, 494
- system include files, 313-314

## T

- tables, prime numbers, generating, 86-87
- test() function, 254
- testing character strings for equality, 202-204
- tests, compound relational, if statements, 72-74
- text editors, 7
- top-down programming, 137
- triangular numbers, 43-44
- trigraph sequences, preprocessor, 464
- type cast operator, 38-39, 450
- type definitions, 319
- type modifiers, 442
  - printf() function, 347
- type qualifiers, 379-380
- typedef statement, 441
  - extending data types, 323-325

## U

- unary minus operators, 33-39
- unions, 375-378, 439-440
- universal character names, 428
- Unix, 7
- Unix utilities, 343-344
- unsigned char data type, 433
- unsigned int constant, 27-28
- unsigned int data type, 433
- unsigned long int strtol (s, end, base) function, 484
- unsigned long long int strtoul (s, end, base) function, 484
- unsigned specifier, 278

### utilities

- csvs, 343
- make, 341-342
- Unix, 343-344

## V

- values, variables, displaying, 15-17
- variable-length arrays, 115-117, 436
- variable-length character strings, 197-214
- variables, 21, 29-30
  - auto, 456
  - automatic local, 124-126, 155-158
  - _Bool, 24-26
  - Boolean, 86-90
  - char, 24
  - declaring, for loops, 56
  - displaying values of, 15-17
  - extern, 456
  - external, 334-337
  - versus static, 337-339
  - global, functions, 151-155
  - omitted, 456
  - pointers, defining, 234-237
  - register, 456
  - static, 155-158, 456
  - versus external, 337-339
  - storage classes, 456
  - volatile, 442
  - working with, gdb (GNU Debugger), 400-401
- variants
  - for loops, 55-56
  - structures, 189
- vim text editor, 7
- Visual Studio, 506
- void *calloc (n, size) function, 484
- void *malloc (size) function, 485
- void *memchr (m1, c, n) function, 476
- void *memcmp (m1, m2, n) function, 476
- void *memcpy (m1, m2, n) function, 476
- void *memmove (m1, m2, n) function, 476
- void *memset (m1, c, n) function, 476
- void *realloc (pointer, size) function, 485
- void clearerr (filePtr) function, 477
- void data type, 433
- void exit (n) function, 493
- void free (pointer) function, 485
- void perror (message) function, 481
- void qsort (arr, n, size, comp_fn) function, 493-494
- void rewind (filePtr) function, 481
- void srand (seed) function, 494
- volatile qualifier, 379
- volatile variable, 442

## W-Z

- while statement, 56-60, 464
- wide character constants, 431
- wide character string constants, 432
- width modifiers, printf() function, 347
- writing functions, 120

```c
#include <stdio.h>

int main (void)
{
	printf ("Programming is fun.\n");

	return 0;
}
```

```c
int main(int argc, char *argv[])
```

```c
#include <stdio.h>

int main (void)
{
    printf ("Programming is fun.\n");
    printf ("And programming in C is even more fun.\n");
    
    return 0;
}
```

Programming is fun.
And programming in C is even more fun.

```c
#include <stdio.h>

int main (void)
{
		printf ("Testing...\n..1\n...2\n....3\n");

		return 0;
}
```

```c
#include <stdio.h>

int main (void)
{
    int sum;

    sum = 50 + 25;
    printf ("The sum of 50 and 25 is %i\n", sum);

    return 0;
}
```

The sum of 50 and 25 is 75

```c
#include <stdio.h>

int main (void)
{
    int value1, value2, sum;

    value1 = 50;
    value2 = 25;
    sum = value1 + value2;
    printf ("The sum of %i and %i is %i\n", value1, value2, sum);

    return 0;
}
```

The sum of 50 and 25 is 75

```c
/* This program adds two integer values
and displays the results           */

#include <stdio.h>

int main (void)
{
    // Declare variables
    int   value1, value2, sum;

    // Assign values and calculate their sum
    value1 = 50;
    value2 = 25;
    sum = value1 + value2;

    // Display the result
    printf ("The sum of %i and %i is %i\n", value1, value2, sum);

    return 0;
}
```

The sum of 50 and 25 is 75

```c
#include <stdio.h>

int main (void)
{
    int sum;
    /* COMPUTE RESULT
    sum = 25 + 37 - 19
    /* DISPLAY RESULTS */
    printf ("The answer is %i\n", sum);
    return 0;
}
```

```c
#include <stdio.h>
int main (void)
{
    int answer, result;

    answer = 100;
    result = answer - 10;
    printf ("The result is %i\n", result + 5);

    return 0;
}
```

```c
printf ("Color is %#x\n", rgbColor);
```

```c
#include <stdio.h>

int main (void)
{
    int         integerVar = 100;
    float       floatingVar = 331.79;
    double      doubleVar = 8.44e+11;
    char        charVar = 'W';

    _Bool       boolVar = 0;

    printf ("integerVar = %i\n", integerVar);
    printf ("floatingVar = %f\n", floatingVar);
    printf ("doubleVar = %e\n", doubleVar);
    printf ("doubleVar = %g\n", doubleVar);
    printf ("charVar = %c\n", charVar);

    printf ("boolVar = %i\n", boolVar);

    return 0;
}
```

integerVar = 100

floatingVar = 331.790009

doubleVar = 8.440000e+11

doubleVar = 8.44e+11

charVar = W

boolVar = 0;

```c
long int numberOfPoints = 131071100L;
```

```c
long long int maxAllowedStorage;
```

```c
theAmountOfMoneyWeMadeThisYear = theAmountOfMoneyLeftAtTheEndOfTheYear - theAmountOfMoneyAtTheStartOfTheYear;
```

```c
moneyMadeThisYear = moneyAtEnd - moneyAtStart;
```

```c
// Illustrate the use of various arithmetic operators

#include <stdio.h>

int main(void)
{
	int a = 100;
	int b = 2;
	int c = 25;
	int d = 4;
	int result;

	result = a - b;		// subtraction
	printf("a - b = %i\n", result);

	result = b * c;		// multiplication
	printf("b * c = %i\n", result);

	result = a / c;		// division
	printf("a / c = %i\n", result);

	result = a + b * c;	// precedence
	printf("a + b * c = %i\n", result);

	printf("a * b + c * d = %i\n", a * b + c * d);

	return 0;
}
```

```c
// More arithmetic expressions

#include <stdio.h>

int main (void)
{
int a = 25;
int b = 2;

float c = 25.0;
float d = 2.0;

printf ("6 + a / 5 * b = %i\n", 6 + a / 5 * b);
printf ("a / b * b = %i\n", a / b * b);
printf ("c / d * d = %f\n", c / d * d);
printf ("-a = %i\n", -a);

return 0;
}
```

```c
// The modulus operator

#include <stdio.h>

int main (void)
{
    int a = 25, b = 5, c = 10, d = 7;

    printf("a = %i, b = %i, c = %i, and d = %i\n", a, b, c, d);
    printf("a %% b = %i\n", a % b);
    printf("a %% c = %i\n", a % c);
    printf("a %% d = %i\n", a % d);
    printf ("a / d * d + a %% d = %i\n",
            a / d * d + a % d);

    return 0;
}
```

a = 25, b = 5, c = 10, and d = 7
a % b = 0
a % c = 5
a % d = 4
a / d * d + a % d = 25

```c
// Basic conversions in C

#include <stdio.h>

int main (void)
{
    float    f1 = 123.125, f2;
    int    i1, i2 = -150;
    char       c = 'a';

    i1 = f1;               // floating to integer conversion
    printf ("%f assigned to an int produces %i\n", f1, i1);

    f1 = i2;               // integer to floating conversion
    printf ("%i assigned to a float produces %f\n", i2, f1);

    f1 = i2 / 100;           // integer divided by integer
    printf ("%i divided by 100 produces %f\n", i2, f1);

    f2 = i2 / 100.0;         // integer divided by a float
    printf ("%i divided by 100.0 produces %f\n", i2, f2);

    f2 = (float) i2 / 100;     // type cast operator
    printf ("(float) %i divided by 100 produces %f\n", i2, f2);

    return 0;
}
```
