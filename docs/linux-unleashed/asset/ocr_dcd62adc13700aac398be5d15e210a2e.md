```
count = count + $6
count = $5 - 8
count = $5 + var1
```

Variables can also be part of a pattern. The following are both valid as pattern-action pairs:

```
$2 > max_value {print "Max value exceeded by ", $2 - max_value}
$4 - var1 < min_value {print "Illegal value of ", $4}
```

Two special operators are used with variables to increment and decrement by one, because these are common operations. Both of these special operators are borrowed from the C language:

| `count++` | Increments count by one |
| --- | --- |
| `count--` | Decrements count by one |

# # Built-In Variables

The gawk language has a few built-in variables that are used to represent things such as the total number of records processed. These are useful when you want to get totals. Table 25.7 shows the important built-in variables.

TABLE 25.7. THE IMPORTANT BUILT-IN VARIABLES.
| Variable | Description |
| :--- | :--- |
| NR | The number of records read so far |
| FNR | The number of records read from the current file |
| FILENAME | The name of the input file |
| FS | Field separator (default is whitespace) |
| RS | Record separator (default is newline) |
| OFMT | Output format for numbers (default is %g) |
| OFS | Output field separator |
| ORS | Output record separator |
| NF | The number of fields in the current record |