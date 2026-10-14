+   Programming statements (such as if-then statements)
+   Functions

You can access the bash calculator from the shell prompt using the bc command:

```
$ bc
bc 1.06
Copyright 1991-1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type 'warranty.'
12 * 5.4
64.8
3.156 * (3 + 5)
25.248
quit
$
```

The example starts out by entering the expression 12 * 5.4. The bash calculator returns the answer. Each subsequent expression entered into the calculator is evaluated and the results are displayed. To exit the bash calculator, you must enter quit.

The floating point arithmetic is controlled by a built-in variable called scale. You must set this value to the desired number of decimal places you want in your answers, or you won't get what you were looking for:

```
$ bc -q
3.44 / 5
0
scale=4
3.44 / 5
.6880
quit
$
```

The default value for the scale variable is zero. Before the scale value is set, the bash calculator provides the answer to zero decimal places. After setting the scale variable value to four, the bash calculator displays the answer to four decimal places. The -q command-line parameter suppresses the lengthy welcome banner from the bash calculator.

Besides normal numbers, the bash calculator also understands variables:

```
$ bc -q
var1=10
var1 * 4
40
var2 = var1 / 5
print var2
2
quit
$
```

Once a variable value is defined, you can use the variable throughout the bash calculator session. The print statement allows you to print variables and numbers.