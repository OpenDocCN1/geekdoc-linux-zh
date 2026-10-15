
| % cat datafile |  |  |  |  |  | |
|---|---|---|---|---|---|---|
| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| western | WE | Sharon Gray | 53 | .97 | 5 | 23 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| southern | SO | Suan Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Patricia Hemenway | 4.0 | .7 | 4 | 17 |
| eastern | EA | TB Savage | 4.4 | .84 | 5 | 20 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |

## EXAMPLE 4.42

```
% egrep '3+' datafile
% grep -E '3+' datafile
% grep '\3+' datafile
```

| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| western | WE | Sharon Gray | 5.3 | .97 | 5 | 23 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |

## EXPLANATION

Prints all lines containing one or more 3s.

## EXAMPLE 4.43

```
% egrep '2\.?[0-9]' datafile
% grep -E '2\.?[0-9]' datafile
% grep '2\.?[0-9]' datafile
```

| western | WE | Sharon Gray | 5.3 | .97 | 5 | 23 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| eastern | EA | TB Savage | 4.4 | .84 | 5 | 20 |

## EXPLANATION

Prints all lines containing a 2, followed by zero or one period, followed by a number in the range between 0 and 9.

## EXAMPLE 4.44

```
% egrep '(no)+' datafile
% grep -E '(no)+' datafile
% grep '(no)+' datafile
```

| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |

## EXPLANATION

Prints lines containing one or more occurrences of the pattern group no.

## EXAMPLE 4.45

```
% grep -E '\W\+|\w+[ABC]' datafile
```

northwest    NW    Charles Main    3.0    .98    3    34
southern      SO    Suan Chin        5.1    .95    4    15
northeast     NE    AM Main Jr.      5.1    .94    3    13
central       CT    Ann Stephens     5.7    .94    5    13

## EXPLANATION

Prints all lines containing one or more alphanumeric word characters (\w+), followed by one or more nonalphanumeric word characters (\W+), followed by one letter in the set ABC.

## EXAMPLE 4.46

```
% egrep '(Sh|u)' datafile
% grep -E '(Sh|u)' datafile
% grep 'S(h|u)' datafile
```

western    WE    Sharon Gray    5.3    .97    5    23
southern   SO    Suan Chin      5.1    .95    4    15

## EXPLANATION

Prints all lines containing S, followed by either h or u; i.e., Sh or Su.

## EXAMPLE 4.47

```
% egrep 'Sh|u' datafile
% grep -E 'Sh|u' datafile
% grep 'Sh|u' datafile
```

Prints all lines containing the expression Sh or u.

## 4.9.2 Anomalies with Regular and Extended Variants of grep

The variants of GNU grep supported by Linux are almost, but not the same, as their UNIX namesakes. For example, the version of egrep, found in Solaris or BSD UNIX, does not support three metacharacter sets: \{ \} for repetition, \( \) for tagging characters, and \< \>, the word anchors. Under Linux, these metacharacters are available with grep and grep -E, but egrep does not recognize \< \>. The following examples illustrate these differences, just in case you are running bash or tcsh under a UNIX system other than Linux, and you want to use grep and its family in your shell scripts.

The examples in this section use the following datafile, repeated periodically for your convenience.

| % cat datafile | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| northwest | WE | Sharon Gray | 53 | .97 | 5 | 23 |
| western | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| southwest | SO | Suan Chin | 5.1 | .95 | 4 | 15 |
| southern | SE | Patricia Hemenway | 4.0 | .7 | 4 | 17 |
| southeast | EA | TB Savage | 4.4 | .84 | 5 | 20 |
| eastern | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| northeast | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| north | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |
| central |  |  |  |  |  |  |

## EXAMPLE 4.48

```
(Linux GNU grep)
1 % grep '\<north\>' datafile  # Must use backslashes

2 % grep '\<north\>' datafile
north NO Margot Weber 4.5 .89 5 9

3 % grep -E '\<north\>' datafile
north NO Margot Weber 4.5 .89 5 9

4 % egrep '\<north\>' datafile
north NO Margot Weber 4.5 .89 5 9

(Solaris egrep)
5 % egrep '\<north\>' datafile
<no output; not recognized>
```
