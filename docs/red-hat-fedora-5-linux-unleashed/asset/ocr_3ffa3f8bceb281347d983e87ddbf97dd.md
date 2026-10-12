The format for a case statement for tcsb is as follows:

```
```
switch (str)
case str1:str2:
	Statements
	breaksw
case str3:str4:
	Statements
	breaksw
default:
	Statements
	breaksw
endsw
```
```

You can specify a number of discrete values—such as str1, str2, and so on—for each condition, of you can specify a value with a wildcard. The last condition should be default and is executed if none of the other conditions is met. For each of the specified conditions, all the associated statements until breaksw are executed.

The example that echos the month when a number is given, shown earlier for pdksh and bash, can be written in tcsb as follows:

```
```
#!/bin/tcsb

set month = 5
switch ( $month )
case 1: echo "Month is January";  breaksw
case 2: echo "Month is February"; breaksw
case 3: echo "Month is March";    breaksw
case 4: echo "Month is April";    breaksw
case 5: echo "Month is May";      breaksw
case 6: echo "Month is June";     breaksw
case 7: echo "Month is July";     breaksw
case 8: echo "Month is August";   breaksw
case 9: echo "Month is September"; breaksw
case 10: echo "Month is October";  breaksw
case 11: echo "Month is November"; breaksw
case 12: echo "Month is December"; breaksw
default: echo "Oops! Month is October!"; breaksw
endsw
```
```

You need to end the statements under each condition with breaksw. If you do not, the statements under the next condition will also be executed.

# The break and exit Statements

You should be aware of two other statements: the break statement and the exit statement.