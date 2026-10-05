
In the example of a bank balance, you can create a variable in Python for bank balance called balance by just giving it a value, like this:

```python
balance = 500
```

(If you want to try this, enter the commands in the shell. This isn't part of our Times Tables program.) You can vary the value later (which is why it's called a variable) by just giving it a new value:

```python
balance = 250
```

More often, you'll want to do sums with the balance, such as taking some money off the total when money is withdrawn or adding money to it when a deposit is received. To do that, change the variable's value to a number that's calculated from its current value. Here's an example:

```python
balance = balance - 250
```

This example takes the value of the balance variable, knocks 250 off, and then puts the answer back into the balance variable. You can display the value of a variable onscreen using the print() command with the variable name:

```python
print(balance)
```

Programmers often use a shorthand form when they're adding numbers to, or subtracting them from, a variable. The shorthand is += for addition and -= for subtraction. Here's an example:

```python
balance = 500
balance += 20
print(balance)
```

If you run this tiny program, or enter these instructions in the shell, Python prints 52 on the screen.

Here's another example:

```python
balance = 500
balance -= 70
print(balance)
```

This program subtracts 70 from the initial balance of 500, so it shows 430 onscreen. This shorthand is an elegant and concise way to express the idea of changing a variable's value, and you'll see it used widely in Python.

## Accepting user input

Before we go any further, we should clarify one piece of jargon: function. A function is a set of commands that do a particular job, and lots of them are built in Python. You've already seen one of them: `print()`. Later on, you'll learn how to make your own, too. (See "Creating your functions," later in this chapter.) To use a function, enter its name, followed by parentheses. If you want to send any information to work with, you put that inside the parentheses, as you already have with print().

When the program runs, we ask the user which multiplication table to generate and store that in a variable that we call tableum. To do that, we set up the tableum variable using a built-in function input(), which asks the user, waits for the user to enter something, and then puts whatever is entered into the variable.

Here's how the input() function works:

| `tableum = input("Which multiplication table shall I generate for you?")` |

![](img/df9a01bf057d58c2401b5edabd6e8829_231_0.png)

We've inserted a space after the question mark and before the closing quotation mark, otherwise, the cursor would appear next to the question mark. Extra space separating the question and the user's answer makes things clear and more professional.

Add the preceding line of code to your program and run it, and you'll see that the program displays the question in the shell and displays a cursor and waits for you to enter a number. The program doesn't anything else yet, however, because you haven't told it to do anything with the number you enter.

## Printing words, variables, and numbers together

It's time to make your program do something with its user input. Start by having the program print a title for the multiplication table the user has requested. This requires something we haven't discussed before: the capability to print text and variables on the same line of text. The print() function can be used to print more than one line in a, if they're separated by commas, so you can combine text and the variable tableum, like this:

```python
print("\nHere is your", tableum, "times table:")
```

The first two characters here, `\n`, have a special meaning. They're known as an escape sequence, and they're used to start a new line. Here they create a bit of space between the question asking for input and the resulting heading.

Any characters that appear between the quote marks are printed onscreen. If you put the variable name `tableName` between quotes, you'll see the word tableenum instead of the name you used.

You now need to print a line for each entry in the tables, from 1 to 12. As you know, you can use variables in sums, and when you print sums, you can display the table like this:

```python
print("1 times", tableName, "is", tableName)
print("2 times", tableName, "is", tableName + 2)
print("3 times", tableName, "is", tableName + 3)
print("4 times", tableName, "is", tableName + 4)
```

What happens when you run it? You might be surprised:

| 7 times is 7 |
| 2 times is 77 |
| 3 times is 777 |
| 4 times is 7777 |

That's not the result you were looking for! The problem is that the variable tableName is being treated as a string, or a group of letters and other characters, rather than a number. This is what happens by default with the input() function. The user could enter anything when prompted. To fix that, you need to convert the string to an integer using the int() function.

```python
tableName = int(tableName)
```

Now when you run it, you will get the correct results:

| 1 times is 1 |
| 2 times is 2 |
| 3 times is 3 |
| 4 times is 4 |

This shorthand is an elegant and concise way to express the idea of changing a variable's value, and you'll see it used widely in Python.
