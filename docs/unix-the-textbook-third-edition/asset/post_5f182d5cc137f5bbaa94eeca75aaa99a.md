
```
% cc -c compute.c power.c
% ls
compute.c compute.o power.c  power.o
% cc compute.o power.o -o power -lm
%
```

The dependency relationship of the two source files is quite simple in this case. To create the executable file power, we need two object modules: power.o and compute.o. If either of the two files power.c or compute.c is updated, the executable needs to be recreated. Figure 17.4 shows this first cut on the dependency relationship.

The make rule corresponding to this dependency relationship is, therefore, the following. Note that the math library has to be linked because the compute function in the compute.c file uses the pow function in this library.

```
power:      power.o compute.o
            cc power.o compute.o -o power -lm
```

We also know that the object file power.o is built from the source file power.c and that the object file compute.o is built from the source file compute.c. Figure 17.5 shows the second cut on the dependency relationship.

Thus, the make rules for creating the two object files are

```
power.o:    power.c
            cc -c power.c
```

![](img/02e070097d401d3bf7de4bf1c470b267_736_0.png)

FIGURE 17.4 First cut on the make dependency tree.

![](img/02e070097d401d3bf7de4bf1c470b267_736_1.png)

FIGURE 17.5 Second cut on the make dependency tree.

```
compute.o: compute.c
	cc -c compute.c
```

The final makefile is shown as

```
% cat makefile
power:
	power.o compute.o
	cc power.o compute.o -o power -lm
power.o: power.c
	cc -c power.c
compute.o: compute.c
	cc -c compute.c
%
```

We then execute the make utility with the preceding makefile:

```
% make
cc power.o compute.o -o power -lm
%
```

In the following in-chapter exercise, you will use the make utility to create the executable code for a C source code that is partitioned into two files.

## EXERCISE 17.4

Create the two source files power.c and compute.c and follow the steps just discussed to create the executable file power by using the make utility.

We now change the structure of this software and divide it into six files called main.c, compute.c, input.c, compute.h, input.h, and main.h. The contents of these files are shown in the following session. Note that the compute.h and input.h files contain declarations (prototypes) of the compute and input functions but not their definitions; the definitions are in the compute.c and input.c files. The main.h file contains two prompts to be displayed to the user. Figure 17.6 shows the new dependency tree.

```
% cat compute.h
/* Declaration/Prototype of the "compute" function */
double compute(double, double);
% cat input.h
/* Declaration/Prototype of the "input" function */
double input (char *);
% cat main.h
/* Declaration of prompts to users */
#define PROMPT1 "Enter the value of x: "
#define PROMPT2 "Enter the value of y: "
```

![](img/02e070097d401d3bf7de4bf1c470b267_738_0.png)

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

To generate the executable for the software, you need to generate the object files for the three source files and link them into a single executable. The following commands are needed to accomplish this task. Note that, as before, you need to link the math library while linking the compute.o file to generate the executable in the power file.

```
% cc -c main.c input.c compute.c
% cc main.o input.o compute.o -o power -lm
%
```

The makefile corresponding to this dependency relationship is

```
% cat makefile
power:		main.o input.o compute.o
	cc main.o input.o compute.o -o power -lm
main.o:		main.c main.h input.h compute.h
	cc -c main.c
input.o:		input.c input.h
	cc -c input.c
compute.o:	compute.c compute.h
	cc -c compute.c
%
```

The execution of the make command results in the execution of the rules associated with all targets in the makefile.

```
% make
cc main.o input.o compute.o -o power -lm
%
```

In the following in-chapter exercise, you will use the make utility to create an executable for a multimodule C source.

## EXERCISE 17.5

Create the three source and header files just discussed, and then use the make command to create the executable in the file power. Use the preceding makefile to perform your task.

If the make rules are in a file other than makefile (or Makefile), you need to run the make command with the -f option, as in make -f my.makefile.

The make rules as shown in the preceding makefile contains some redundant commands that can be removed. The make utility has a predefined rule that invokes the cc -c xxx.c -o xxx.o command for every rule, as in

```
xxx.o: xxx.c zzz.h
	cc -c xxx.c
```
