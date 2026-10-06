# Chapter 16 Programming Tools.

```
/* convert tabs in standard input to spaces in */
/* standard output while maintaining columns */

#include <stdio.h>
#define TABSIZE 8

/* prototype for function stop */
int findstop(int *ptr);

int main() {
    int c;      /* character read from stdin */
    int pos = 0; /* column position of character */
    int inc;     /* column increment to tab stop */

    while ((c = getchar()) != EOF) {
        switch(c) {
            case '\t': /* c is a tab */
                inc = findstop(&pos);
                for (; inc > 0; inc--)
                    putchar(' ');
                break;
            case '\n': /* c is a newline */
                putchar(c);
                pos = 0;
                break;
            default: /* c is anything else */
                putchar(c);
                pos++;
                break;
        }
    }
    return 0;

```

# Comments

# Preprocessor Directives

# Function Prototype

# Main Function

Figure 16-1 A simple C program (tabs.c—the line numbers are not part of the source code)

```
/* compute size of increment to next tab stop */
int findstop(int *col) {
    int retval;
    retval = (TABSIZE - (*col % TABSIZE));
    /* increment argument (current column position) to next tabstop */
    *col = retval;
    return retval;
} /* main gets many blanks for filling
```

occurs in your program. If you replace the #define TABSIZE in Figure 16-1 with the following directive, the program will place TAB stops every four columns rather than every eight:

```
#define TABSIZE 4
```

Symbolic constants are one type of macro—the mapping of a symbolic name to replacement text. Macros are handy when the replacement text is needed at multiple-points throughout the source code or when the definition of the macro is subject