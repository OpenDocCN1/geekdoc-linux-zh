
The numerator is 1, and the denominator is 3.

The value of the fraction is 1/3.

`-(void) setNumerator: (int) num;`

```cpp
#include <iostream>

class Fraction
{
  private:
    int numerator;
    int denominator;

  public:
    void setNumerator (int num);
    void setDenominator (int denom);
    int  Numerator (void);
    int  Denominator (void);
    void print (Fraction f);
};

void Fraction::setNumerator (int num)
{
    numerator = num;
}

void Fraction::setDenominator (int denom)
{
    denominator = denom;
}

int Fraction::Numerator (void)
{
    return numerator;
}

int Fraction::Denominator (void)
{
    return denominator;
}

void Fraction::print (Fraction f)
{
    std::cout << "The value of the fraction is " << numerator << '/'
              << denominator << '\n';
}

int main (void)
{
    Fraction    myFract;

    myFract.setNumerator (1);
    myFract.setDenominator (3);

    myFract.print (myFract);

    return 0;
}
```

The value of the fraction is 1/3.

`void Fraction::setNumerator(int num)`

```cpp
std::cout << "The value of the fraction is " << numerator << '/'
        << denominator << '\n';
```

```csharp
using System;

class Fraction
{
    private int numerator;
    private int denominator;

    public int Numerator
    {
        get
        {
            return numerator;
        }

        set
        {
            numerator = value;
        }
    }

    public int Denominator
    {
        get
        {
            return denominator;
        }
        set
        {
            denominator = value;
        }
    }

    public void print ()
    {
        Console.WriteLine("The value of the fraction is {0}/{1}",
            numerator, denominator);
    }
}

class example
{
    public static void Main()
    {
        Fraction myFract = new Fraction();

        myFract.Numerator = 1;
        myFract.Denominator = 3;

        myFract.print ();
    }
}
```

The value of the fraction is 1/3.

`Fraction myFract = new Fraction();`

```
type name = initial_value, name = initial_value, ... ;
```

```c
double _Complex c1 = 5 + 10.5 * I;
```

```
type   name[n]   = { initExpression, initExpression, ... };
```

```c
int x = 1233;      
int a[] = { [9] = x + 1, [3] = 3, [2] = 2, [1] = 1 };
```

```
type name[d1][d2]...[dn] = initializationList;
```

```c
static int matrix[4][3] =
{ 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

```c
int matrix[4] [3] = { [0][0] = 1, [1][1] = 5, [2][2] = 9 };
```

```c
struct point end = { .y = 500, .x = 200 };
```

```c
struct entry
{
   char *word;
   char *def;
} dictionary[1000] = {
   {"a",        "first letter of the alphabet" },
   {"aardvark", "a burrowing African mammal" },
   {"aback",    "to startle" } 
};
```

```c
struct entry
{
    char    *word;
    char    *def;
} dictionary[1000] = {
    [0].word = "a",             [0].def = "first letter of the alphabet",
    [1].word = "aardvark",     [1].def = "a burrowing African mammal",
    [2].word = "aback",         [2].def = "to startle"
};
```

```c
struct  entry
{
char  *word;
char  *def;
} dictionary[1000] = {
{ {.word = "a",             .def = "first letter of the alphabet" },
{.word = "aardvark", .def = "a burrowing African mammal"} ,
{.word = "aback",      .def = "to startle"}
};
```

```c
struct date tomorrow = today;
```

```c
union shared swap2 = { .w[0] = 0x0, .w[1] = 0xffffffff; }
```

```
enum name { enum_1, enum_2, ... } variableList;
```

```c
if ( dataFlag ||  checkData (myData) )
...
```

```c
if (index >= 0 && index < n && a[index] == 0)
... 
```

```c
(struct point) {.x = 0, .y = 0}
```

```c
origin = (struct point) {.x = 0, .y = 0};
```

```c
moveToPoint ((struct  point) {.x = 0, .y = 0});
```

```c
intPtr = (int [100]) { [0] = 1, [50] = 50, [99] = 99 };
```

```c
returnType   name ( type1 param1, type2 param2, ... )
{
      variableDeclarations


    programStatement
    programStatement
    ...
    return expression;
}
```

```c
int printf (char *format, ...)
{
 ... 
}
```

```c
returnType name (type1 param1, type2 param2, ... );
```

```c
long double  power (double x, int n);
```

```c
long double power (double, int);
```

```
for ( expression_1; expression_2; expression_3 )
    programStatement
```

```c
for ( int i = 0; i < 100; ++i)
...
```

```c
#define name(param_1, param_2, ..., param_n) text
```

```c
#define myPrintf(...) printf("DEBUG: " __VA_ARGS__);
```

```c
myPrintf("i = %i, j = %i\n", i, j);
```

```c
#define printint(x) printf(#x" = %d\n",x)
```

```c
printf("count" " = %i\n", count);
```

```c
printf ("count = %i\n", count);
```

```c
str (The string "\t" contains a tab)
```

"The string \"\t\" contains a tab"

```c
#define printx(n)   printf ("%i\n", x ## n );
```

```c
#define printx(n) printf ("x" # n " = %i\n", x ## n );
```

```c
#define DATABASE_DEFS    < /usr/data/database.h>
...
#include DATABASE_DEFS
```

```c
memcpy ((void *) data2, (void *) data1, sizeof (data1));
```

```c
char *fgets (buffer, i, filePtr)
```

```c
FILE *fopen (fileName, accessMode)
```

```c
int fprintf (filePtr, format, argl, arg2, ..., argn)
```

```c
size_t fread (buffer, size, n, filePtr)
```

```c
numread = fread (text, sizeof (char), 80, in_file);
```

```c
FILE *freopen (fileName, accessMode, filePtr)
```

```c
if ( freopen ("inputData", "r", stdin) == NULL ) {
   ...
}
```

```c
int fscanf (filePtr, format, arg1, arg2, ..., argn)
```

```c
int fseek (filePtr, offset, mode)
```

```c
size_t fwrite (buffer, size, n, filePtr)
```

```c
#include <stdlib.h>
#include <stdio.h>

if ( (in = fopen ("data", "r")) == NULL ) {
    perror ("data file read");
    exit (EXIT_FAILURE);
}
```

```c
int printf (format, arg1, arg2, ..., argn)
```

```c
int rename (fileName1, fileName2)
```

```c
int scanf (format, arg1, arg2, ..., argn)
```

```c
int sprintf (buffer, format, argl, arg2, ..., argn)
```

```c
int version = 2;
char fname[125];
...
sprintf (fname, "/usr/data%i/2015", version);
```

```c
int sscanf (buffer, format, arg1, arg2, ..., argn)
```

```c
char buffer[] = "July 16, 2014", month[10];
int day, year;
...
sscanf (buffer, "%s %d, %d", month, &day, &year);
```

```c
#include <stdio.h>
#include <stdlib.h>

if ( sscanf (argv[1], "%f", &fval) != 1 ) {
    fprintf (stderr, "Bad number: %s\n", argv[1]);
    exit (EXIT_FAILURE);
}
```

```c
#include <stdlib.h>
 ...
char  buffer[] = "  123.456xyz", *end;
double value;
 ...
value = strtod (buffer, &end);
```

```c
long int strtol (s, end, base)
```

```c
long long int strtoll (s, end, base)
```

```c
unsigned long int strtoul (s, end, base)
```

```c
unsigned long long int strtoull (s, end, base)
```

```c
void *realloc (pointer, size)
```

```c
void qsort (arr, n, size, comp_fn)
```

```c
#include <stdlib.h>

int main(void)
{
    int data[1000], comp_ints(void *, void *);
    qsort (data, 1000, sizeof(int), comp_ints);
}

int comp_ints(void *p1, void *p2)
{
    int i1 = * (int *) p1;
    int i2 = * (int *) p2;
    return i1 - i2;
}
```

```c
system (`mkdir /usr/tmp/data`);
```

```sh
gcc [options] file [file ...]
```

```c
while ( c = getchar ( ) != EOF )
...
if ( x & 0xF ==  y )
...
```

```c
#define reciprocal(x) 1 / x
...
w = reciprocal(a + b);
```

```c
total_earning = (cash + (investments * inv_interest) + (savings * sav_interest));
printf("Your total money to date is %.2f, total_earning);
```
