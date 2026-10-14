# MUTUALLY RECURSIVE FUNCTIONS

Because they call themselves directly, functions such as factorial() in the preceding section are said to be inclusively recursive. Another form of recursion occurs when one function calls another, which eventually ends up calling the first function again. If you position three mirrors so that mirror 1 reflects mirror 2, which reflects mirror 3, which again reflects mirror 1, you’d have a graphic illustration of mutual recursion. Kids call them kaleidoscopes.

Mutual recursion is useful for writing co-routines. These are functions that depend on one another but don’t necessarily require one function to be called before the other. Listing 10.11, onfirst.cpp, demonstrates mutual recursion in a somewhat frivolous way. Named for Abbott and Costello’s famous and comically recursive “Who’s on First?” routine, onfirst.cpp displays the alphabet. Before continuing, can you figure out how?

# LISTING 10.11 ONFIRST.CPP

```
#include <iostream.h>

// Function prototypes
void A(char c);
void B(char c);

int main()
{
    A('Z');
    cout << endl;
    return 0;
}

void A(char c)
{
    if (c > 'A')
        B(c);
    cout << c;
}

void B(char c)
{
    A(--c);
}
```

Compile and run the program using the following commands. As shown here, the program displays the alphabet in uppercase:

```
$ g++ onfirst.cpp
$ ./a.out
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```