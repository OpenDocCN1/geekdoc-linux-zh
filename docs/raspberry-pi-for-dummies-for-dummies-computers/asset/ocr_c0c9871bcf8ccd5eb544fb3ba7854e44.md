In the example of a bank balance, you can create a variable in Python for bank balance called balance by just giving it a value, like this:

```
balance = 500
```

(If you want to try this, enter the commands in the shell. This isn't part of our Times Tables program.) You can vary the value later (which is why it's called a variable) by just giving it a new value:

```
balance = 250
```

More often, you'll want to do sums with the balance, such as taking some money off the total when money is withdrawn or adding money to it when a deposit is received. To do that, change the variable's value to a number that's calculated from its current value. Here's an example:

```
balance = balance - 250
```

This example takes the value of the balance variable, knocks 250 off, and then puts the answer back into the balance variable. You can display the value of a variable onscreen using the print() command with the variable name:

```
print(balance)
```

Programmers often use a shorthand form when they're adding numbers to, or subtracting them from, a variable. The shorthand is += for addition and -= for subtraction. Here's an example:

```
balance = 500
balance += 20
print(balance)
```

If you run this tiny program, or enter these instructions in the shell, Python prints 52 on the screen.

Here's another example:

```
balance = 500
balance -= 70
print(balance)
```

This program subtracts 70 from the initial balance of 500, so it shows 430 onscreen. This shorthand is an elegant and concise way to express the idea of changing a variable's value, and you'll see it used widely in Python.