# EXAMPLE 6.119

```
% awk 'END{print "The total number of records is " NR}' datafile
```

The total number of records is 9

# EXPLANATION

After awk has finished processing the input file, the statements in the END block are executed. The string The total number of records is is printed, followed by the value of NR, the number of the last record.

# EXAMPLE 6.120

```
% awk '/north/{count++}END{print count}' datafile
```

3

# EXPLANATION

If the record begins with the regular expression north, the user-defined variable count is incremented by one. When awk has finished processing the input file, the value stored in the variable count is printed.

# 6.16.5 awk Script with BEGIN and END

The following datafile2 is used for Example 6.121.

```
% cat datafile2
Joel Craig:northwest:NW:3.0:.98:3:4
Sharon Kelly:western:WE:5.3:.97:5:23
Chris Foster:southwest:SW:2.7:.8:2:18
May Chin:southern:SO:5.1:.95:4:15
Derek Johnson:southeast:SE:4.0:.7:4:17
Susan Beal:eastern:EA:4.4:.84:5:20
TJ Nichols:northeast:NE:5.1:.94:3:13
Val Shultz:north:NO:4.5:.89:5:9
Sheri Watson:central:CT:5.7:.94:5:13
```