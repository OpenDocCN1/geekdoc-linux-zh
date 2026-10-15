```
% cat datafile
northwest  NW  Charles Main  3.0  .98  3  34
western    WE  Sharon Gray   5.3  .97  5  23
southwest  SW  Lewis Dalsass 2.7  .8   2  18
southern   SO  Suan Chin     5.1  .95  4  15
southeast  SE  Patricia Hemenway 4.0  .7   4  17
eastern    EA  TB Savage     4.4  .84  5  20
northeast  NE  AM Main Jr.   5.1  .94  3  13
north      NO  Margot Weber  4.5  .89  5  9
central    CT  Ann Stephens  5.7  .94  5  13
```

# EXAMPLE 5.19

```
% sed 's#3#88#g' datafile
northwest  NW  Charles Main  88.0  .98  88  884
western    WE  Sharon Gray   5.88  .97  5  288
southwest  SW  Lewis Dalsass 2.7  .8   2  18
southern   SO  Suan Chin     5.1  .95  4  15
southeast  SE  Patricia Hemenway 4.0  .7   4  17
eastern    EA  TB Savage     4.4  .84  5  20
northeast  NE  AM Main Jr.   5.1  .94  88  188
north      NO  Margot Weber  4.5  .89  5  9
central    CT  Ann Stephens  5.7  .94  5  188
```

# EXPLANATION

The character after the s command is the delimiter between the search string and the replacement string. The delimiter character is a forward slash by default, but can be changed. Whatever character follows the s command (with the exception of the newline character or backslash) is the new delimiter. This technique can be useful when searching for patterns containing a forward slash, such as pathnames or birthdays.

# 5.9.4 Range of Selected Lines: The Comma

A range of lines starts at one address in a file and ends at another address in the file. The address range can be line numbers (such as 5,10), regular expressions (such as /Dick/,/Joe/), or a combination of both (such as /north/, $). The range is inclusive—it consists of the line with the starting condition, all lines in between, and the line ending the condition of the range. If the ending condition is never reached, it ends when the file ends. If the ending condition is reached, and then the condition for starting again applies, the range starts over.