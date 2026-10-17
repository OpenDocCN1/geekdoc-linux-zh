
```
/* Program to evaluate simple expressions of the form
number operator number
*/
#include <stdio.h>
int main (void)
{
    float value1, value2;
    char operator;

    printf ("Type in your expression.\n");
    scanf ("%f %c %f", &value1, &operator, &value2);

    if ( operator == '+' )
        printf ("%.2f\n", value1 + value2);
    else if ( operator == '-' )
        printf ("%.2f\n", value1 - value2);
    else if ( operator == '*' )
        printf ("%.2f\n", value1 * value2);
    else if ( operator == '/' )
        printf ("%.2f\n", value1 / value2);

    return 0;
}
```

Type in your expression.

123.5 + 59.3

182.80

Type in your expression.

198.7 / 26

7.64

Type in your expression.

```
89.3 * 2.5
223.25
```

```
/* Program to evaluate simple expressions of the form
value   operator   value    */
#include <stdio.h>

int main (void)
{
   float value1, value2;
   char  operator;

   printf ("Type in your expression.\n");
   scanf ("%f %c %f", &value1, &operator, &value2);

   if ( operator == '+' )
      printf ("%.2f\n", value1 + value2);
   else if ( operator == '-' )
      printf ("%.2f\n", value1 - value2);
   else if ( operator == '*' )
      printf ("%.2f\n", value1 * value2);
   else if ( operator == '/' )
      if ( value2 == 0 )
         printf ("Division by zero.\n");
      else
         printf ("%.2f\n", value1 / value2);
   else
      printf ("Unknown operator.\n");

   return 0;
}
```

Type in your expression.

**123.5 + 59.3**

182.80

Type in your expression.

198.7 / 0

Division by zero.

Type in your expression.

```
125 $ 28
```

Unknown operator.

```
switch ( expression )
{

case value1:

program statement
program statement
...
break;

case value2:

program statement
program statement
...
break;

...

case valuen:

program statement
program statement
...
break;

default:

program statement
program statement
...
break;
}
```

```
if ( expression == value1 )
{
    program statement
    program statement
    ...
}
else if ( expression == value2 )
{
    program statement
    program statement
    ...
}
...
else if ( expression == valuen )
{
    program statement
    program statement
    ...
}
else
{
    program statement
    program statement
    ...
}
```

```
/** Program to evaluate simple expressions of the form
value   operator   value   **/

#include <stdio.h>

int main (void)
{
   float   value1, value2;
   char    operator;

   printf ("Type in your expression.\n");
   scanf ("%f %c %f", &value1, &operator, &value2);

   switch (operator)
   {
      case '+':
         printf ("%.2f\n", value1 + value2);
         break;
      case '-':
         printf ("%.2f\n", value1 - value2);
         break;
      case '*':
         printf ("%.2f\n", value1 * value2);
         break;
      case '/':
         if ( value2 == 0 )
            printf ("Division by zero.\n");
         else
            printf ("%.2f\n", value1 / value2);
         break;
      default:
         printf ("Unknown operator.\n");
         break;
   }

   return 0;
}
```

Type in your expression.

```
178.99 - 326.8
```

```
-147.81
```

```
switch (operator)
{
  ...
  case '*':
  case 'x':
      printf ("%.2f\n", value1 * value2);
      break;
  ...
}
```

```
// Program to generate a table of prime numbers

#include <stdio.h>

int main (void)
{
 int p, d;
 _Bool isPrime;

 for ( p = 2; p <= 50; ++p ) {
 isPrime = 1;

 for ( d = 2; d < p; ++d )
 if ( p % d == 0 )
 isPrime = 0;

 if ( isPrime != 0 )
 printf ("%i ", p);
 }

 printf ("\n");
 return 0;
}
```

if ( 100 )

    printf ("This will always be printed.\n");

while ( char != 'e' && count != 80 )

// 用于生成素数表的程序

#include <stdio.h>

#include <stdbool.h>

int main (void)

{

   int     p, d;

   bool    isPrime;

   for ( p = 2; p <= 50; ++p ) {

       isPrime = true;

       for ( d = 2; d < p; ++d )

           if ( p % d == 0 )

               isPrime = false;

       if ( isPrime != false )

           printf ("%i  ", p);

   }

   printf ("\n");

   return 0;

}
