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

# EXAMPLE 6.185

```
1 % nawk 'BEGIN{name=ARGV[1];}\n$0 ~ name {print $3, $4}' "Derek" datafile
nawk: can't open Derek
source line number 1
```

```
2 % nawk 'BEGIN{name=ARGV[1]; delete ARGV[1];}\n$0 ~ name {print $3, $4}' "Derek" datafile
Derek Johnson
```

# EXPLANATION

+   1 The name "Derek" was assigned to the variable name in the BEGIN block. In the pattern-action block, nawk attempted to open "Derek" as an input file and failed.
+   2 After assigning "Derek" to the variable name, ARGV[1] is deleted. When starting the pattern-action block, nawk does not try to open "Derek" as the input file, but opens datafile instead.

# 6.26.4 Reading Input (getline)

# EXAMPLE 6.186

```
% nawk 'BEGIN{ "date" | getline d; print d}' datafile
Mon Jan 15 11:24:24 PST 2004
```

# EXPLANATION

The UNIX/Linux date command is piped to the getline function. The results are stored in the variable d and printed.