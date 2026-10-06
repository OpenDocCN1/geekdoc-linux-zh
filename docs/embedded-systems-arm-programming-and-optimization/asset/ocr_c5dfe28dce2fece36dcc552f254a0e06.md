# 1.6 Assembly Optimization #1: Sorting 19

```
int bubble_sort (int *data,int n) {
    int i,j,temp;
    for (i=0;i<n-1;i++) {
        for (j=0;j<n-1;j++) {
            if (data[j]>data[j+1]) {
                temp=data[j];
                data[j]=data[j+1];
                data[j+1]=temp;
            }
        }
    }
    return 1;
}
```

Next, convert the assembly implementation into a function. To do this, remove ".equ" and ".comm" directives, change the name of the exported symbol to "bubble_sort_asm", and add a new directive that specifies this as a function:

+   - global bubble_sort_asm
- arch armv7-a
- type bubble_sort_asm, %function

The function arguments, the pointer to the array and its size, will arrive in registers r0 and r1, respectively. As such, replace the instruction "ldr r1, =N" which initializes the size of the array. Also, change the instruction that initializes the register for the array in the outer loop body from "ldr r2,data" to "mov r2,r0".

Lastly, return the value in register r0 just before returning to the caller:

```
exito: mov r0,#r1
    bx lr
```

Now write a driver that will call both functions. The driver will also be responsible for allocating the arrays and verifying the results:

```
#include <stdio.h>
#include <stdlib.h>
#define N 32768
```