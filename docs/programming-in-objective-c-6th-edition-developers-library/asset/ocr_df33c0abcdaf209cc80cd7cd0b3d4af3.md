computer system that uses the ASCII format mentioned previously, the character ` is actually represented internally as the number 48, the character `' as the number 49, and so on.

If c is a digit character, the phrase I       is displayed. Otherwise, if c is not alphabetic and is not a digit, the final € clause is executed and displays the phrase “It's a special character.” Execution of the program is then complete.

You should note that even though S       is used here to read just a single character, the Enter (or Return) key must still be pressed after the character is typed to send the input to the program. In general, whenever you're reading data from the terminal, the program doesn't see any of the data typed on the line until the Enter key is pressed.

For your next example, suppose you want to write a program that allows the user to type in simple expressions of the form

n

The program evaluates the expression and displays the results at the terminal, to two decimal places of accuracy. The operators that you want to have recognized are the normal operators for addition, subtraction, multiplication, and division. Program 5.8 makes use of a large i statement with many € clauses to determine which operation is to be performed.

# Program 5.8 Evaluating Simple Expressions

![](bbox=[0.0, 0.43, 0.3, 0.46])

```

/

#

i
{






}
```

# Program 5.8 Output

![](bbox=[0.0, 0.81, 0.3, 0.83])

```

T
123.5 + 59.3
1
```

# Program 5.8 Output (Rerun)

![](bbox=[0.0, 0.94, 0.3, 0.96])

```






```