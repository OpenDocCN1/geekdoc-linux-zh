![](bbox=[0.12, 0.12, 0.88, 0.45])

FIGURE 17.6 The make dependency tree for the sample C software.

```
% cat compute.c
#include <math.h>
#include "compute.h"
double compute (double x, double y)
{
    return (pow ((double) x, (double) y));
}
```

```
% cat input.c
#include <stdio.h>
#include "input.h"
double input(char *s)
{
    float x;
    printf ("%s", s);
    scanf ("%f", &x);
    return (x);
}
```

```
% cat main.c
#include <stdio.h>
#include "main.h"
#include "compute.h"
#include "input.h"
int main()
{
    double x, y;
    printf ("The program takes x and y from stdin and displays x^y.\n");
    x = input (PROMPT1);
    y = input (PROMPT2);
    printf ("x^y is: %6.3f\n", compute(x,y));
}
```