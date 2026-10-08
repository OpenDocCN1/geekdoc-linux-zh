Here, printf substitutes the value in the integer variable age for the %d. The next example prints the values of three int variables:

```
printf("The values are %d %d %d", num1, num2, num3);
```

This message will contain the values of num1, num2, and num3, in that order. You can also pass arithmetic expressions to printf:

```
printf("You have worked %d minutes", hours*60);
```

In fact, you can pass any valid C expression to printf. However, be sure you use an appropriate format specifier. Table 10-5 shows a list of valid format specifiers.

| Format Specifier | Meaning |\n| :--- | :--- |\n| %c | Single character |\n| %d | Signed decimal integer |\n| %e | Floating-point number, e notation |\n| %E | Floating-point number, E notation |\n| %f | Floating-point number, decimal notation |\n| %g | Causes %f or %e to be used, whichever is shorter |\n| %G | Causes %f or %E to be used, whichever is shorter |\n| %i | Signed decimal integer |\n| %o | Unsigned octal integer |\n| %p | Pointer |\n| %s | Character string |\n| %u | Unsigned decimal integer |\n| %x | Unsigned hex integer using digits 0-f |\n| %X | Unsigned hex integer using digits 0-F |\n| %% | Print a percent sign |

Table 10-5: Format specifiers

You have learned enough C programming basics to write a simple program.