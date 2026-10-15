The remaining examples in this section use the following datafile.

| % cat datafile |  |  |  |  |  |
|---|---|---|---|---|---|
| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| western | WE | Sharon Gray | 5.3 | .97 | 5 | 23 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| southern | SO | Suan Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Patricia Hemenway | 4.0 | .7 | 4 | 17 |
| eastern | EA | TB Savage | 4.4 | .84 | 5 | 20 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |

# EXAMPLE 4.67

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

# EXPLANATION

1 The file repatterns is displayed. It contains grep's search patterns that will be matched against lines in an input file. Western and north are the patterns grep will use in its search.

2 With the -f option followed by a filename (in this example, repatterns), grep will get its search patterns from that file and match them against lines in datafile. Grep searched for and printed all lines containing patterns western and north.

# EXAMPLE 4.68

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