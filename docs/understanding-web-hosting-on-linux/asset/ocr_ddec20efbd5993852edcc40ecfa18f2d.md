# Conditional Statements

Conditional statements are used for program flow control. There are basically four conditional statements the if statement, the while loop (which can also function as a do/until), the for loop, and the switch statement

Here is the basic structure of the if statement:

```
if (boolean expression) {
  // statement here
} else {
  // statements here
}
```

Here is an example of the if statement:

```
if(amount >= 100.00) {
  discount = .10;
} else {
  discount = .00;
}
```

There are two forms of the while loop. The first is similar to the DOW or DOWxx loop in RPG. The statements or block following the while is executed while the condition in the expression is true:

```
while (boolean expression) {
  // statements here
}
```

Here is an example of this kind of while statement:

```
int counter = 0;
while (counter < 100) {
  counter = counter + 1;
}
```

The second form of the while loop is similar to an RPG DOU or DOUxx loop. The block of code is executed at least once, and the loop continues until the condition is not true:

```
do {
  // statements here
} while (boolean expression)
```

Here is an example:

```
int counter = 0;
do {
  counter++;
} while (counter < 100)
```

The for loop is probably the most popular form of loop structure. You will see it used often in Java applications. Here is its basic structure: