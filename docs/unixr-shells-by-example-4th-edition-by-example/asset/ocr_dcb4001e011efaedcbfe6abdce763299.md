% cat datafile
northwest NW Joel Craig 3.0 .98 3 4
western WE Sharon Kelly 5.3 .97 5 23
southwest SW Chris Foster 2.7 .8 2 18
southern SO May Chin 5.1 .95 4 15
southeast SE Derek Johnson 4.0 .7 4 17
eastern EA Susan Beal 4.4 .84 5 20
northeast NE TJ Nichols 5.1 .94 3 13
north NO Val Shultz 4.5 .89 5 9
central CT Sheri Watson 5.7 .94 5 13

# EXAMPLE 6.114

```
% nawk '{$9 = $6 * $7; print $9}' datafile
2.94
4.85
1.6
3.8
2.8
4.2
2.82
4.45
4.7
```

# EXPLANATION

The result of multiplying the sixth field ($6) and the seventh field ($7) is stored in a new field, $9, and printed. There were eight fields; now there are nine.

# EXAMPLE 6.115

```
% nawk '{$10 = 100; print NF, $9, $0}' datafile
10 northwest NW Joel Craig 3.0 .98 3 4 100
10 western WE Sharon Kelly 5.3 .97 5 23 100
10 southwest SW Chris Foster 2.7 .8 2 18 100
10 southern SO May Chin 5.1 .95 4 15 100
10 southeast SE Derek Johnson 4.0 .7 4 17 100
10 eastern EA Susan Beal 4.4 .84 5 20 100
10 northeast NE TJ Nichols 5.1 .94 3 13 100
10 north NO Val Shultz 4.5 .89 5 9 100
10 central CT Sheri Watson 5.7 .94 5 13 100
```

# EXPLANATION

A tenth field ($10) is assigned 100 for each record. This is a new field. The ninth field ($9) does not exist, so it will be considered a null field. The number of fields is printed (NF), followed by the value of $9, the null field, and the entire record ($0). The value of the tenth field is 100.