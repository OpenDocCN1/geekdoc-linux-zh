
## EXPLANATION

With the -b option, grep prints the byte offset from the input file before each line of output.

Instead of using the datafile for these next two examples, we'll use a file called negative to demonstrate the -e and -x options.

```
% cat negative
-40 is cold.
This is line 1.
This is line 2.5
-alF are options to the ls command
```

## EXAMPLE 4.65

```
1 % grep -e "-aIF" negative
-aIF are options to the ls command
```

```
2 % grep --regexp=-40 negative
-40 is cold.
```

## EXPLANATION

- 1. With the -e option, grep treats all characters in the pattern equally, so that leading dashes are not mistaken for options.
- 2. The alternate way to represent -e is --regexp=pattern, where pattern is the regular expression; in this example the regular expression is -40.

## EXAMPLE 4.66

```
% grep -x -e "-40 is cold." negative
-40 is cold.
```

## EXPLANATION

With the -x option, grep will not match a line unless the search pattern is identical to the entire line. The -e is used to allow a dash as the first character in the search string.

The remaining examples in this section use the following datafile.

| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
|---|---|---|---|---|---|---|
| western | WE | Sharon Gray | 5.3 | .97 | 5 | 23 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| southern | SO | Suan Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Patricia Hemenway | 4.0 | .7 | 4 | 17 |
| eastern | EA | TB Savage | 4.4 | .84 | 5 | 20 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |

## EXAMPLE 4.67

```
1 % cat repatterns
western
north

2 % grep -f repatterns datafile
northwest  NW  Charles Main  3.0  .98  3  34
western    WE  Sharon Gray    5.3  .97  5  23
northeast  NE  AM Main Jr.    5.1  .94  3  13
north      NO  Margot Weber   4.5  .89  5  9
```

## EXPLANATION

1 The file repatterns is displayed. It contains grep's search patterns that will be matched against lines in an input file. Western and north are the patterns grep will use in its search.

2 With the -f option followed by a filename (in this example, repatterns), grep will get its search patterns from that file and match them against lines in datafile. Grep searched for and printed all lines containing patterns western and north.

## EXAMPLE 4.68

```
1 % grep '[0-9]' datafile db
datafile:northwest NW  Charles Main  3.0  .98  3  34
datafile:western WE    Sharon Gray    5.3  .97  5  23
datafile:southwest SW  Lewis Dalsass  2.7  .8   2  18
datafile:southern SO   Suan Chin      5.1  .95  4  15
datafile:southeast SE  Patricia Hemenway 4.0 .7  4  17
datafile:eastern EA    TB Savage      4.4  .84 5  20
datafile:northeast NE  AM Main Jr.    5.1  .94 3  13
datafile:north NO      Margot Weber   4.5  .89 5  9
datafile:central CT    Ann Stephens   5.7  .94 5  13
db:123
```

## EXAMPLE 4.68 (CONTINUED)

```
2 % grep -h '[0-9]' datafile db
northwest   NW   Charles Main   3.0   .98   3   34
western     WE   Sharon Gray    5.3   .97   5   23
southwest   SW   Lewis Dalsass  2.7   .8    2   18
southern    SO   Suan Chin      5.1   .95   4   15
southeast   SE   Patricia Hemenway 4.0   .7    4   17
eastern     EA   TB Savage      4.4   .84   5   20
northeast   NE   AM Main Jr.    5.1   .94   3   13
north       NO   Margot Weber   4.5   .89   5    9
central     CT   Ann Stephens   5.7   .94   5   13
```

## EXPLANATION

- 1. If more than one file is listed, grep prepends each line of its output with the filename. Filenames are datafile and db.
- 2. With the -h option, grep suppresses the header information; i.e., does not print the filenames.

## EXAMPLE 4.69

```
% grep -q Charles datafile  or
% grep --quiet Charles datafile
% echo $status
0
```

## EXPLANATION

The quiet option suppresses any output from grep. It is used when the exit status is all that is needed. If the exit status is zero, grep found the pattern.
