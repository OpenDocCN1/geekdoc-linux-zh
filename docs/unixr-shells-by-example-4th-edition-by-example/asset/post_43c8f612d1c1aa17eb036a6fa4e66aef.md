
## EXAMPLE 3.16

```
% sed 's/[0-9][0-9]/&./' datafile
```

| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34.5 |
| western | WE | Sharon Gray | 5.3 | .97 | 5 | 23.5 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18.5 |
| southern | SO | Suan Chin | 5.1 | .95 | 4 | 15.5 |
| southeast | SE | Patricia Hemenway | 4.0 | .7 | 4 | 17.5 |
| eastern | EA | TB Savage | 4.4 | .64 | 5 | 20.5 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13.5 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13.5 |

### EXPLANATION

The ampersand (&) in the replacement string represents exactly what was found in the search string. Each line that ends in two digits will be replaced by itself, and .5 will be appended to it.

a To represent a literal ampersand in the replacement string, it must be escaped \&.

## EXAMPLE 3.17

```
% sed -n 's/Hemenway/Jones/gp' datafile
```

southeast SE Patricia Jones 4.0 .7 4 17

### EXPLANATION

All occurrences of Hemenway are replaced with Jones, and only the lines that changed are printed. The -n option combined with the p command suppresses the default output. The g stands for global substitution across the line.

## EXAMPLE 3.18

```
% sed -n 's/\(Mar\)/got/\1ianne/p' datafile
```

north NO Marianne Weber 4.5 .89 5 9

### EXPLANATION

The pattern Mar is enclosed in parentheses and saved as tag 1 in a special register. It will be referenced in the replacement string as \1. Margot is then replaced with Marianne.

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

## EXAMPLE 5.19

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

### EXPLANATION

The character after the s command is the delimiter between the search string and the replacement string. The delimiter character is a forward slash by default, but can be changed. Whatever character follows the s command (with the exception of the newline character or backslash) is the new delimiter. This technique can be useful when searching for patterns containing a forward slash, such as pathnames or birthdays.

## 5.9.4 Range of Selected Lines: The Comma

A range of lines starts at one address in a file and ends at another address in the file. The address range can be line numbers (such as 5,10), regular expressions (such as /Dick/,/Joe/), or a combination of both (such as /north/, $). The range is inclusive—it consists of the line with the starting condition, all lines in between, and the line ending the condition of the range. If the ending condition is never reached, it ends when the file ends. If the ending condition is reached, and then the condition for starting again applies, the range starts over.

## EXAMPLE 5.20

```
% sed -n '/west/,/east/p' datafile
```

northwest NW Charles Main 3.0 .98 3 34
western WE Sharon Gray 5.3 .97 5 23
southwest SW Lewis Dalsass 2.7 .8 2 18
southern SO Suan Chin 5.1 .95 4 15
southeast SE Patricia Hemenway 4.0 .7 4 17

### EXPLANATION

All lines in the range of patterns between west and east are printed. If west were to appear on a line after east, the lines from west to the next east or to the end of file, whichever comes first, would be printed. The arrows mark the range.

## EXAMPLE 5.21

```
% sed -n '5,/northeast/p' datafile
```

southeast SE Patricia Hemenway 4.0 .7 4 17
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13

### EXPLANATION

Prints the lines from line 5 through the first line that begins with northeast.

## EXAMPLE 5.22

```
% sed '/west/,/east/s/$/++VACA++/' datafile
```

northwest NW Charles Main 3.0 .98 3 34++VACA++
western WE Sharon Gray 5.3 .97 5 23++VACA++
southwest SW Lewis Dalsass 2.7 .8 2 18++VACA++
southern SO Suan Chin 5.1 .95 4 15++VACA++
southeast SE Patricia Hemenway 4.0 .7 4 17++VACA++
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
central CT Ann Stephens 5.7 .94 5 13

### EXPLANATION

For lines in the range between the patterns east and west, the end-of-line ($) is replaced with the string ++VACA++. The newline is moved over to the end of the new string. The arrows mark the range.
