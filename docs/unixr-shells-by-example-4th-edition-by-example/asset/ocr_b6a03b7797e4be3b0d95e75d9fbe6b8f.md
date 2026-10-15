# Table 4.4 egrep's Regular Expression Metacharacters (continued)

| Metacharacter | Function | Example | What It Matches |
|---|---|---|---|
| [^ ] | Matches one character not in the set | '[A-KM-Z]ove' | Matches lines not containing A through K or M through Z, followed by ove. |
| New with egrep |  |  |  |
| + | Matches one or more of the characters preceding the + sign | '[a-z]+ove' | Matches one or more lowercase letters, followed by ove. Would find move, approve, love, behove, etc. |
| ? | Matches zero or one of the preceding characters | 'l?ove' | Matches for an l followed by either one or not any occurrences of the letter o. Would find love or live. |
| a|b | Matches either a or b | 'love|hate' | Matches for either expression, love or hate. |
| () | Groups characters | 'love(able|ly)' '(ov)+' | Matches for lovable or lovely. Matches for one or more occurrences of ov. |

# 4.5.1 egrep Examples

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