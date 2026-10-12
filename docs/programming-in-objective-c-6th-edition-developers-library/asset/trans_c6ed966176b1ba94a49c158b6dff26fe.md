

今天的日期是 15 年 9 月 25 日。

```c
// Function to use structures containing pointers
#include <stdio.h>
int main (void)
{
    struct intPtrs
    {
        int  *p1;
        int  *p2;
    };

    struct intPtrs  pointers;
    int  i1 = 100, i2;

    pointers.p1 = &i1;
    pointers.p2 = &i2;
    *pointers.p2 = -97;

    printf ("i1 = %i, *pointers.p1 = %i\n", i1, *pointers.p1);
    printf ("i2 = %i, *pointers.p2 = %i\n", i2, *pointers.p2);
    return 0;
}
```

i1 = 100, *pointers.p1 = 100
i2 = -97, *pointers.p2 = -97

```c
struct entry
{
    int           value;
    struct entry  *next;
};
```

```c
// Function to use linked lists
#include <stdio.h>
int main (void)
{
    struct entry
    {
        int value;
        struct entry *next;
    };
    struct entry n1, n2, n3;
    int i;

    n1.value = 100;
    n2.value = 200;
    n3.value = 300;

    n1.next = &n2;
    n2.next = &n3;

    i = n1.next->value;
    printf ("%i ", i);

    printf ("%i\n", n2.next->value);

    return 0;
}
```

```c
struct entry *list_pointer = &n1;
```

```c
// Program to traverse a linked list
#include <stdio.h>
int main (void)
{
    struct entry
    {
        int             value;
        struct entry    *next;
    };
    struct entry        n1, n2, n3;
    struct entry        *list_pointer = &n1;

    n1.value = 100;
    n1.next  = &n2;
    n2.value = 200;
    n2.next  = &n3;
    n3.value = 300;
    n3.next  = (struct entry *) 0; // Mark list end with null pointer

    while (list_pointer != (struct entry *) 0) {
        printf ("%i\n", list_pointer->value);
        list_pointer = list_pointer->next;
    }
    return 0;
}
```

```c
list_pointer = list_pointer->next;
```

```c
charPtr = &d;    // not valid
```

foo.c:10: warning: assignment of read-only variable 'charPtr'

```c
*charPtr = 'Y';     // not valid
```

foo.c:11: warning: assignment of read-only location

```c
const char * const *charPtr = &c;
```

```c
void print_list (struct entry *pointer)
{
...
}
```

```c
// Program to illustrate using pointers and functions

#include <stdio.h>

void test (int *int_pointer)
{
    *int_pointer = 100;
}

int main (void)
{
    void test (int *int_pointer);
    int i = 50, *p = &i;

    printf ("Before the call to test i = %i\n", i);
    test (p);
    printf ("After the call to test i = %i\n", i);
    return 0;
}
```

Before the call to test i = 50
After the call to test i = 100

```c
// More on pointers and functions

#include <stdio.h>

void exchange (int * const pint1, int * const pint2)
{
    int temp;

    temp = *pint1;
    *pint1 = *pint2;
    *pint2 = temp;
}

int main (void)
{
    void exchange (int * const pint1, int * const pint2);
    int i1 = -5, i2 = 66, *p1 = &i1, *p2 = &i2;

    printf ("i1 = %i, i2 = %i\n", i1, i2);

    exchange (p1, p2);
    printf ("i1 = %i, i2 = %i\n", i1, i2);

    exchange (&i1, &i2);
    printf ("i1 = %i, i2 = %i\n", i1, i2);

    return 0;
}
```

i1 = -5, i2 = 66
i1 = 66, i2 = -5
i1 = -5, i2 = 66

```c
void exchange(int * const pint1, int * const pint2)
```

```c
#include <stdio.h>

struct entry
{
    int  value;
    struct entry  *next;
};

struct entry  *findEntry (struct entry  *listPtr, int match)
{
    while (listPtr != (struct entry *) 0)
        if (listPtr->value == match)
            return listPtr;
        else
            listPtr = listPtr->next;

    return (struct entry *) 0;
}

int main (void)
{
    struct entry  *findEntry (struct entry  *listPtr, int match);
    struct entry  n1, n2, n3;
    struct entry  *listPtr, *listStart = &n1;

    int search;

    n1.value = 100;
    n1.next  = &n2;

    n2.value = 200;
    n2.next  = &n3;

    n3.value = 300;
    n3.next  = 0;

    printf ("Enter value to locate: ");
    scanf ("%i", &search);

    listPtr = findEntry (listStart, search);

    if (listPtr != (struct entry *) 0)
        printf ("Found %i.\n", listPtr->value);
    else
        printf ("Not found.\n");

    return 0;
}
```

Enter value to locate: 200
Found 200.

Enter value to locate: 400
Not found.

Enter value to locate: 300
Found 300.

```c
struct entry *findEntry (struct entry *listPtr, int match)
```

```c
// Function to sum the elements of an integer array

#include <stdio.h>

int arraySum (int array[], const int n)
{
    int sum = 0, *ptr;
    int * const arrayEnd = array + n;

    for (ptr = array; ptr < arrayEnd; ++ptr)
        sum += *ptr;

    return sum;
}

int main (void)
{
    int arraySum (int array[], const int n);
    int values[10] = { 3, 7, -9, 3, 6, -1, 7, 9, 1, -5 };

    printf ("The sum is %i\n", arraySum (values, 10));
    return 0;
}
```

```c
for ( ...; pointer <= array + n; ... )
```

```c
// Function to sum the elements of an integer array    Ver. 2

#include <stdio.h>

int  arraySum (int  *array, const int  n)
{
    int  sum = 0;
    int  * const arrayEnd = array + n;

    for ( ; array < arrayEnd;  ++array )
        sum += *array;

    return sum;
}

int main (void)
{
    int  arraySum (int  *array, const int  n);
    int  values[10] = { 3, 7, -9, 3, 6, -1, 7, 9, 1, -5 };

    printf ("The sum is %i\n", arraySum (values, 10));

    return 0;
}
```

```c
void copyString(char to[], char from[])
{
    int i;
    for(i = 0; from[i] != '\0'; ++i )
        to[i] = from[i];
    to[i] = '\0';
}
```

```c
#include <stdio.h>

void copyString (char *to, char *from)
{
    for ( ; *from != '\0'; ++from, ++to )
        *to = *from;

    *to = '\0';
}

int main (void)
{
    void copyString (char *to, char *from);
    char string1[] = "A string to be copied.";
    char string2[50];

    copyString (string2, string1);
    printf ("%s\n", string2);

    copyString (string2, "So is this.");
    printf ("%s\n", string2);

    return 0;
}
```

A string to be copied.
So is this.

```c
copyString (string2, "So is this.");
```

```c
textPtr = "A character string.";
```

```c
text = "This is not valid.";
```

```c
char text[80] = "This is okay.";
```

```c
char *text = "This is okay.";
```

```c
char *days[] =
{ "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };
```

```c
// Function to copy one string to another. Pointer Ver. 2

#include <stdio.h>

void copyString (char *to, char *from)
{
    while ( *from )
        *to++ = *from++;

    *to = '\0';
}

int main (void)
{
    void  copyString (char *to, char *from);
    char  string1[] = "A string to be copied.";
    char  string2[50];

    copyString (string2, string1);
    printf ("%s\n", string2);

    copyString (string2, "So is this.");
    printf ("%s\n", string2);

    return 0;
}
```

A string to be copied.
So is this.

```c
// Function to count the characters in a string - Pointer version
#include <stdio.h>

int stringLength (const char *string)
{
    const char *cptr = string;

    while ( *cptr )
        ++cptr;
    return cptr - string;
}

int main (void)
{
    int stringLength (const char *string);

    printf ("%i ", stringLength ("stringLength test"));
    printf ("%i ", stringLength (""));
    printf ("%i\n", stringLength ("complete"));

    return 0;
}
```

```c
char *message = "Programming in C is fun\n";
char message2[] = "You said it\n";
char *format = "x = %i\n";
int x = 100;
```

```c
/*** set 1 ***/
printf ("Programming in C is fun\n");
printf ("%s", "Programming in C is fun\n");
printf ("%s", message);
printf (message);

/*** set 2 ***/
printf ("You said it\n");
printf ("%s", message2);
printf (message2);
printf ("%s", &message2[0]);

/*** set 3 ***/
printf ("said it\n");
printf (message2 + 4);
printf ("%s", message2 + 4);
printf ("%s", &message2[4]);

/*** set 4 ***/
printf ("x = %i\n", x);
printf (format, x);
```

| b1 | b2 | b1 & b2 |
|:---:|:---:|:---:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

w1    00000000000011001       25
w2    00000000001001101       & 77
---------------------------------
w3    00000000000001001        9

