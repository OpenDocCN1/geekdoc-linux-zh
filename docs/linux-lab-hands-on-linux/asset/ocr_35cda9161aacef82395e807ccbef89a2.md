![](bbox=[0.25, 0.14, 0.85, 0.45])

▶ **Program 2: Writing a program in C that read character from stdin and displaying output on the screen.**

Let us now perform the following steps to work on C program under Linux environment:

+   1. Open Text Edit by selecting **Applications→Accessories→Text Editor** (Figure 1).
+   2. Type the following program (appears in Listing 1) in the Text Editor window (Figure 10).

# ▶ Listing 1

```
/*Reading Reading and wrtiting to stdin and stdout */
#include <stdio.h>
int main (int argc, char *argv[])
{
	int k, l = 0;
	printf ("INPUT: ");
	while ((k=getchar()) !='\n')
	{ l++;
		putchar(k);
	}
	printf("\nThe number of characters read (including the newline): %d\n", l+l);
	return 0;
}
```