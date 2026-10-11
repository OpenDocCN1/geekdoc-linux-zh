# Chapter 13 • Internationalization and Localization



The field width is a decimal digit string, providing a minimum width. The default is to use as many characters as necessary based on the rest of the specification. Values smaller than the field width are padded with spaces on the left (or on the right, if the `,` flag was given).

The left precision consists of a # character and a decimal digit string. It indicates the minimum number of digits to appear to the left of the decimal point character. ${ }^{4}$ If the converted value is smaller than this, the result is padded with the numeric fill character. The default is a space, but the = flag can be used to change it. Grouping characters are not included in the count.

Finally, the right precision consists of a `,` character and a decimal digit string. This indicates how many digits to round the value to before it is formatted. The default is provided by the $\mathrm{frac\_digits}$ and int_frac_digits fields in the struct lconv. If this value is 0 , no decimal point character is printed.

strfmon() returns the number of characters placed into the buffer, not including the terminating zero byte. If there’s not enough room, it returns $-1$ and sets errno to E2BIG.

Besides strfmon(), POSIX (but not ISO C) provides a special flag—the single-quote character, ’—for the printf() formats %i, %d, %u, %f, %F, %g, and %G. In locales that supply a thousands separator, this flag adds the locale’s thousands separator. The following simple program, ch13-quoteflag.c, demonstrates the output:

```
/* ch13-quoteflag.c -- demonstrate printf's quote flag */
#include <stdio.h>
#include <locale.h>
int main(void)
{
    setlocale(LC_ALL, ""); /* Have to do this, or it won't work */
    printf("%i'g\n", 1234567);
    return 0;
}
```

Here’s what happens for two different locales: one that does not supply a thousands separator and one that does:

> The technical term used in the standards is radix point, since numbers in different bases may have fractional parts as well. However, for monetary values, it seems pretty safe to use the term “decimal point.”