The same motivations previously cited for using static variables also apply to the case of static functions.

Figure 14.1 summarizes communication between different modules. Here two modules are depicted, \(\mathfrak{m}\) and \(\mathfrak{m}\).

```
double x;
static double result;

static void doSquare(void)
{
double square(void);

x = 2.0;
result = square();
}
int main(void)
{
doSquare();
printf("%g\n", result);

return 0;
}
```

```
extern double x;

double square(void)
{

return x * x;
}
```

mod1.c  mod2.c
Figure 14.1 Communication between modules.

\(\mathfrak{m}\) defines two functions: \(\mathfrak{d}\) and \(\mathfrak{m}\). The way things are set up here, \(\mathfrak{m}\) calls \(\mathfrak{d}\), which in turn calls \(\mathfrak{s}\). This last function is defined in the module \(\mathfrak{m}\).

Because \(\mathfrak{d}\) is declared \(\mathfrak{s}\), it can only be called from within \(\mathfrak{m}\), and by no other module.

\(\mathfrak{m}\) defines two global variables: \(\mathfrak{x}\) and \(\mathfrak{r}\), both of type \(\mathfrak{d}\). \(\mathfrak{x}\) can be accessed by any module that is linked together with \(\mathfrak{m}\). On the other hand, the keyword \(\mathfrak{s}\) in front of the definition of \(\mathfrak{r}\) means that it can only be accessed by functions defined inside \(\mathfrak{m}\) (namely \(\mathfrak{m}\) and \(\mathfrak{d}\)).

When execution begins, the \(\mathfrak{m}\) routine calls \(\mathfrak{d}\). This function assigns the value \(\mathfrak{z}\) to the global variable \(\mathfrak{x}\) and then calls the function \(\mathfrak{s}\). Because \(\mathfrak{s}\) is defined in another source file (inside \(\mathfrak{m}\)), and because it doesn't return an \(\mathfrak{i}\), \(\mathfrak{d}\) properly includes an appropriate declaration at the beginning of the function.

The \(\mathfrak{s}\) function returns as its value the square of the value of the global variable \(\mathfrak{x}\). Because \(\mathfrak{s}\) wants to access the value of this variable, which is defined in another source file (in \(\mathfrak{m}\)), an appropriate \(\mathfrak{\Theta}\) declaration appears in \(\mathfrak{m}\) (and, in this case, it makes no