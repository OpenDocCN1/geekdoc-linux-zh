With gawk, you assign a variable a value using the assignment operator (=):

```
var1 = 10
```

This assigns the value 10 (numeric, not string) to the variable var1. With gawk, you don't have to declare variable types before you use them as you must with most other languages. This makes it easy to work with variables in gawk.

> **NOTE**
Don't confuse the assignment operator, =, which assigns a value, with the comparison operator, ==, which compares two values. This is a common error that takes a little practice to overcome.

The gawk language lets you use variables within actions:

```
$1 == "Plastic" { count = count + 1 }
```

This pattern-action pair checks to see if the first column is equal to the string "Plastic," and if it is, increments the value of count by one. Somewhere above this line we should set a preliminary value for the variable count (usually in the BEGIN section), or we will be adding one to something that isn't a recognizable number.

> **NOTE**
Actually, gawk assigns all variables a value of zero when they are first used, so you don't really have to define the value before you use it. It is, however, good programming practice to initialize the variable anyway.

Here's a more complete example:

```
BEGIN { count = 0 }
$5 == "UNIX" { count = count + 1 }
END { printf "%d occurrences of UNIX were found", count }
```

In the BEGIN section, the variable count is set to zero. Then, the gawk pattern-action pair is processed, with every occurrence of "UNIX" adding one to the value of count. After the entire file has been processed, the END statement displays the total number.

Variables can be used in combination with columns and values, so all of the following statements are legal: