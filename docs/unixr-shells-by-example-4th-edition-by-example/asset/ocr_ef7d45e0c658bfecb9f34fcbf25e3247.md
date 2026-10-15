| % cat datafile |  |  |  |  |  |
|---|---|---|---|---|---|
| northwest | NW | Joel Craig | 3.0 | .98 | 3 | 4 |
| western | WE | Sharon Kelly | 5.3 | .97 | 5 | 23 |
| southwest | SW | Chris Foster | 2.7 | .8 | 2 | 18 |
| southern | SO | May Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Derek Johnson | 4.0 | .7 | 4 | 17 |
| eastern | EA | Susan Beal | 4.4 | .84 | 5 | 20 |
| northeast | NE | TJ Nichols | 5.1 | .94 | 3 | 13 |
| north | NO | Val Shultz | 4.5 | .89 | 5 | 9 |
| central | CT | Sheri Watson | 5.7 | .94 | 5 | 13 |

# EXAMPLE 6.74

```
% awk '/southern/{print $5 + 10.56}' datafile
15.66
```

# EXPLANATION

If the record contains the regular expression southern, 10.56 is added to the value of the fifth field ($5) and printed.

# EXAMPLE 6.75

```
% awk '/southern/{print $8 - 10}' datafile
5
```

# EXPLANATION

If the record contains the regular expression southern, 10 is subtracted from the value of the eighth field ($8) and printed.

# EXAMPLE 6.76

```
% awk '/southern/{print $8 / 2}' datafile
7.5
```

# EXPLANATION

If the record contains the regular expression southern, the value of the eighth field ($8) is divided by 2 and printed.