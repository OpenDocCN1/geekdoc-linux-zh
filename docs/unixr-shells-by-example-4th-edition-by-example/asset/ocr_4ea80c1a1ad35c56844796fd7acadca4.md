# EXAMPLE 6.36

```
awk 'print $1' datafile
awk: syntax error near line 1
awk: bailing out near line 1
```

# EXPLANATION

This is the awk (old awk) error message. Old awk programs were difficult to debug because almost all errors produced this same message. The curly braces are missing in the action statement.

# EXAMPLE 6.37

```
nawk '{print $0}' datafile
northwest   NW   Joel Craig   3.0   .98   3   4
western     WE   Sharon Kelly 5.3   .97   5   23
southwest   SW   Chris Foster 2.7   .8    2   18
southern    SO   May Chin     5.1   .95   4   15
southeast   SE   Derek Johnson 4.0   .7    4   17
eastern     EA   Susan Beal   4.4   .84   5   20
northeast   NE   TJ Nichols   5.1   .94   3   13
north       NO   Val Shultz   4.5   .89   5   9
central     CT   Sheri Watson 5.7   .94   5   13
```

# EXPLANATION

Each record is printed. $0 holds the current record.

# EXAMPLE 6.38

```
nawk '{print "Number of fields: "NF}' datafile
Number of fields: 8
Number of fields: 8
Number of fields: 8
Number of fields: 8
Number of fields: 8
Number of fields: 8
Number of fields: 8
Number of fields: 8
Number of fields: 8
```

# EXPLANATION

There are 8 fields in each record. The built-in awk variable NF holds the number of fields and is reset for each record.