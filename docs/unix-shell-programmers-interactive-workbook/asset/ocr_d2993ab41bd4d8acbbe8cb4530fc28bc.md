# 308 Lab 6.2: Arrays and Compound Variables

However, there is nothing about hello, even if you put it in quotes, that makes it unequivocally a string; it could be the name of another variable whose value you want to use as a subscript.

Assign the value 5 to a variable named TGIF.

+   i) How can you use the value of TGIF to print the value of the sixth element of days?
Answer:Your interaction should look something like the following:

```
[6088]: TGIF=5
[6089]: print ${days[TGIF]}
Friday
[6090]:
```

Friday is the value of days[5].

The only difference between hello in the previous question and TGIF in this question is that line 6088 assigns a value to TGIF before using it as a subscript, whereas hello was never assigned a value.

The shell “knows” that there must be a number inside the square brackets, so if you give it a string, it automatically checks to whether the string can be used as the name of a variable and, if so, whether the variable's value can be used as a number. You don't have to use a dollar sign to tell the shell to evaluate the variable.

> What you write inside the square brackets of a subscript is called an arithmetic expression.The rules for writing arithmetic expressions are covered in Exercise 6.1.2.

![](bbox=[0.141, 0.633, 0.235, 0.693])

Print the value of days using @ as the subscript.

+   j) What did the shell print?
Answer:Your interaction should look like the following:

```
[6090]: print ${days[@]}
Sunday Monday Tuesday Wednesday Thursday Friday
Saturday
[6091]:
```

Just as the sign @ (@ refers to a list of all the parameters passed to a function or script when used as a variable name inside a function or script, it