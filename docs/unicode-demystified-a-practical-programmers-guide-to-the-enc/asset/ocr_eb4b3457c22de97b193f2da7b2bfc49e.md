The next example finds all cars priced at or under $3,000:

```
$ gawk $5 <= 3000' cars
plym fury 77 73 2500
chevy nova 79 60 3000
fiat 600 65 115 450
toyota tercel 82 180 750
chevy impala 65 85 1550
```

When you use double quotation marks, gawk performs textual comparisons, using the ASCII (or other local) collation sequencing as the basis of the comparison. Following, gawk shows that the strings 450 and 750 fall in the range that lies between the strings 2000 and 9000:

```
$ $5 >= "2000" && $5 < "9000"' cars
plym fury 77 73 2500
chevy nova 79 60 3000
chevy nova 80 50 3500
fiat 600 65 115 450
honda accord 81 30 6000
toyota tercel 82 180 750
```

When you need a numeric comparison, do not use quotation marks. The next example gives the correct results. It is the same as the previous example but without the quotation marks:

```
$ gawk $5 >= 2000 && $5 < 9000' cars
plym fury 77 73 2500
chevy nova 79 60 3000
chevy nova 80 50 3500
honda accord 81 30 6000
```

Next, the range operator () selects a group of lines. The first line it selects is the one specified by the pattern before the comma. The last line is the selected by the pattern after the comma. If no line matches the pattern, gawk selects every line up to the end of the file. The next example selects all lines, starting with the line that contains vol and concluding with the line that contains:

```
$ gawk '/vol/, /fiat/' cars
novo gl 78 102 9850
ford ltd 83 15 10500
chevy nova 80 50 3500
fiat 600 65 115 450
```

After the range operator finds its first group of lines, it starts the process, looking for a line that matches the pattern before the comma. In the following example gawk finds three groups of lines that fall between chevy and ford. Although the fifth line in the file contains ford, gawk does not select it because at the time it is processing the fifth line; it is searching for chevy: