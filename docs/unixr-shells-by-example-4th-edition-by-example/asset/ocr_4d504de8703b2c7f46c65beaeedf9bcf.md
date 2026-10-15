The remaining examples in this section use the following datafile, repeated periodically for your convenience.

| region | code | name | 3.0 | .98 | 3 | 4 |
|--------|------|------|------|------|------|------|
| northwest | NW | Joel Craig | 3.0 | .98 | 3 | 4 |
| southwest | WE | Sharon Kelly | 5.3 | .97 | 5 | 23 |
| southeast | SO | May Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Derek Johnson | 4.0 | .7 | 4 | 17 |
| eastern | EA | Susan Beal | 4.4 | .84 | 5 | 20 |
| northeast | NE | TJ Nichols | 5.1 | .94 | 3 | 13 |
| north | NO | Val Shultz | 4.5 | .89 | 5 | 9 |
| central | CT | Sheri Watson | 5.7 | .94 | 5 | 13 |

# 6.16.6 The printf Function

```
EXAMPLE 6.122
% nawk '{printf "$%6.2f\n", $6 * 100}' datafile

$ 98.00
$ 97.00
$ 95.00
$ 70.00
$ 84.00
$ 94.00
$ 89.00
$ 94.00
```

The printf function formats a floating-point number to be right-justified (the default) with a total of 6 digits, one for the decimal point, and two for the decimal numbers to the right of the period. The number will be rounded up and printed.