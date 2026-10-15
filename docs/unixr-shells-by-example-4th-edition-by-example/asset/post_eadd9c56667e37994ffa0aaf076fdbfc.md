
# Table 4.4 egrep's Regular Expression Metacharacters (continued)

| Metacharacter | Function | Example | What It Matches |
|---|---|---|---|
| [^ ] | Matches one character not in the set | '[A-KM-Z]ove' | Matches lines not containing A through K or M through Z, followed by ove. |
| New with egrep |  |  |  |
| + | Matches one or more of the characters preceding the + sign | '[a-z]+ove' | Matches one or more lowercase letters, followed by ove. Would find move, approve, love, behove, etc. |
| ? | Matches zero or one of the preceding characters | 'l?ove' | Matches for an l followed by either one or not any occurrences of the letter o. Would find love or live. |
| a|b | Matches either a or b | 'love|hate' | Matches for either expression, love or hate. |
| () | Groups characters | 'love(able|ly)' '(ov)+' | Matches for lovable or lovely. Matches for one or more occurrences of ov. |

## 4.5.1 egrep Examples

The following examples illustrate only the way the new extended set of regular expression metacharacters is used with egrep. The grep examples presented earlier illustrate the use of the standard metacharacters, which behave the same way with egrep. Egrep also uses the same options at the command line as grep.

The following datafile is used in the examples in this section.

```
% cat datafile
northwest NW Charles Main 3.0 .98 3 34
western WE Sharon Gray 5.3 .97 5 23
southwest SW Lewis Dalsass 2.7 .8 2 18
southern SO Suan Chin 5.1 .95 4 15
southeast SE Patricia Hemenway 4.0 .7 4 17
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
central CT Ann Stephens 5.7 .94 5 13
```

## EXAMPLE 4.30

% egrep '\NW\|EA' datafile
northwest      NW    Charles Main    3.0  .98  3  34
eastern         EA    TB Savage        4.4  .84  5  20

## EXPLANATION

Prints the line if it contains either the expression NW or the expression EA.

## EXAMPLE 4.31

% egrep '3+' datafile
northwest      NW    Charles Main    3.0  .98  3  34
western        WE    Sharon Gray      5.3  .97  5  23
northeast      NE    AM Main Jr.      5.1  .94  3  13
central        CT    Ann Stephens     5.7  .94  5  13

## EXPLANATION

Prints all lines containing one or more occurrences of the number 3; e.g., 3, 33, 33333333.

## EXAMPLE 4.32

% egrep '\2\.?[0-9]' datafile
western        WE    Sharon Gray      5.3  .97  5  23
southwest      SW    Lewis Dalsass    2.7  .8   2  18
eastern        EA    TB Savage        4.4  .84  5  20

## EXPLANATION

Prints all lines containing a 2, followed by one period or no period at all, followed by a number; e.g., matches 2.5, 25, 29, 2.3, etc.

## EXAMPLE 4.33

% egrep '(no)+' datafile
northwest      NW    Charles Main    3.0  .98  3  34
northeast      NE    AM Main Jr.      5.1  .94  3  13
north          NO    Margot Weber     4.5  .89  5  9

## EXPLANATION

Prints lines containing one or more consecutive occurrences of the pattern group no; e.g., no, nono, nonononono, etc.

## EXAMPLE 4.34

```
% egrep 'S(h|u)' datafile
western      WE   Sharon Gray   5.3  .97  5  23
southern     SO   Suan Chin     5.1  .95  4  15
```

## EXPLANATION

Prints all lines containing S, followed by either h or u; e.g., Sharon or Suan.

## EXAMPLE 4.35

```
% egrep 'Sh|u' datafile
western      WE   Sharon Gray     5.3  .97  5  23
southern     SO   Suan Chin       5.1  .95  4  15
southwest    SW   Lewis Dalsass   2.7  .8   2  18
southeast    SE   Patricia Hemenway 4.0  .7   4  17
```

## EXPLANATION

Prints all lines containing the expression Sh or u; e.g., Sharon or southern.

## 4.5.2 egrep Review

Table 4.5 contains examples of egrep commands and what they do.

# Table 4.5 Review of egrep

| Command | What It Does |
|---|---|
| egrep '^A+' file | Prints lines beginning with one or more spaces. |
| egrep '^A*' file | Prints lines beginning with zero or more spaces.ᵃ |
| egrep '(Tom|Dan) Savage' file | Prints lines containing Tom Savage or Dan Savage. |
| egrep '(ab)+' file | Prints lines with one or more occurrences of ab. |
| egrep '^X[0-9]?' file | Prints lines beginning with X followed by zero or one single digit. |
| egrep 'fun.,$' * | Prints lines ending in fun. from all files.ᵃ |
| egrep '[A-Z]+' file | Prints lines containing one or more capital letters. |
| egrep '[0-9]' file | Prints lines containing a number.ᵃ |
