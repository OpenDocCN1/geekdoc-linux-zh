# 4.9.2 Anomalies with Regular and Extended Variants of grep

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

# EXAMPLE 4.48

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