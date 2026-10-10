
Another indented line is within the else code block, and both lines will run if the user does not correctly input “Python”. This program does indeed compare strings, so quotations must surround the text.

## Conditional Operators

Double equal signs (==) are only one of the many operators that can be used to create a conditional expression. This small list shows other operators in Python.

- `>` - Greater than
- `<` - Less than
- `==` - Equal to
- `>=` - Greater than or equal to
- `<=` - Less than or equal to
- `!=` - Not equal to

If statements evaluate whether the expression in the parenthesis is true; the above operators allow for some interesting expressions.

```python
age = int(input("How old are you? "))

if (age <= 18):
    print ("Starting early! Good for you!")
else:
    print ("Ah, a good age to learn.")

print ("Thank you for downloading this book.")
```

A clever use of indentations is used here. If the user’s age is 18 or under, it will congratulate them then skip the else statement and finally print out the thank you message. If the user is above 18 it will display the else message and then also thank them. No matter which conditional runs, the user will still receive the thank you message. The indentation makes all the difference about what code lines will actually run within a decision structure, and you must pay close attention to avoid a logic error.

For situations that require more than just two potential outcomes, the keyword "elif" can be used.

```python
age = int(input("How old are you? "))
if (age <= 18 and age > 0):
    print ("Starting early! Good for you!")
elif (age >= 80):
    print ("Never too late to learn!")
elif (age > 18 and age < 80):
    print ("Ah, a good age to learn.")
else:
    print ("That seems like an invalid age.")
    quit()

print ("Thank you for downloading this book.")
```

Elif is a keyword that can be used to split the decision making process into multiple branching paths. Between if and else statements, any number of elif conditionals can be used. Also, another new keyword is used above- "and". Our first comparison checks to see if age is less than or equal to 18 AND greater than 0. Therefore that conditional will only evaluate to true if the age value satisfies both requirements. Pretend the user input 75. The first statement evaluates, and 75 is indeed greater than 0, but it is not also less than 18, so that statement is skipped. Then, the first elif is evaluated. Age is not greater than 80, so that statement is skipped as well. Thirdly, age is definitely between 18 and 80, so the console prints "Ah, a good age to learn" and then skips the else statement altogether.

Remembering that only one statement in a decision “tree” can ever run, we can see that any elif that activates essentially runs its code block and then breaks from the decision structure. Else is used as a “catch-all” type expression in our above program. Any invalid input, such as “-1” would be picked up by else and displayed as such. Good programming form comes from catching potential user errors like this, and as an aspiring programmer you should always be expecting the user to incorrectly input values whenever the chance arises.

“And” is a comparison operator that forces both parts of an expression to be true. Another operator, “or”, is used to force only one part of the expression to evaluate to true.

```python
elif (age == 25 or age == 50 or age == 75):
    print ("Happy quarterly birthday!")
```

If we were to put this elif within the above program (under the first if), we would see that only one part of the expression must be true for the whole comparison to be true. The user’s age could be 25, 50, or 75 and the application would say “Happy quarterly birthday”. Using “and” instead of “or” would be impossible, because the age cannot be 25 and 50 and 75 all at the same time. The keywords that we use for comparisons are helpful and greatly useful, but if used incorrectly they can lead to logic errors.

## Example Program 2 – project2.py

```python
print("Python Quiz!")

answered = 0

correct = 0

print()

print("What version of python are we using?")
print("A: 1, B: 2, C: 3")
user_answer = input("Enter A, B, or C: ")

answered += 1

print()

if (user_answer == "C" or user_answer == "c"):
    correct += 1
    print ("Correct")
else:
    print ("Incorrect")

print()

print("How many 'else' statements can be in a decision tree?")
print("A: 1, B: Infinite, C: None")
user_answer = input("Enter A, B, or C: ")

answered += 1

print()

if (user_answer == "A" or user_answer == "a"):
    correct += 1
    print ("Correct")
else:
    print ("Incorrect")

print()

print("What does '=' do in Python?")
print("A: Compare, B: Assign, C: Both")
user_answer = input("Enter A, B, or C: ")

answered += 1

print()

if (user_answer == "B" or user_answer == "b"):
    correct += 1
    print ("Correct")
else:
    print ("Incorrect")

print()
print ("You got {} out of {} correct.".format(correct, answered))

if (correct == 3):
    print ("Congratulations! Good score.")
elif (correct == 2):
    print ("Good work, but study hard!")
else:
    print ("Go back and read over the section again, I'm sure you'll get it.")
```

Homework program:

- Use if statements to create a calculator program that prompts the user for two numbers and an operator.

## Loops

Just as conditional statements activate if an expression evaluates to true, looping conditionals also compare values in an expression. But while if, elif, and else statements are linear in nature, other conditionals have the ability to repeatedly run blocks of code. "Loops" are conditional statements that can be run several times through the course of a program, and they allow for expanded functionality within Python programs. A "while" loop is such a conditional.

```python
answer = 0
while (answer != 2):
    answer = int(input("What is 4 / 2? "))
print ("Correct!")
```

So long as the specified condition evaluates to true, the “while” code block will continuously run. We can see a perfect example of this through the program above. We create a new variable “answer” and repeatedly compare it to 2. While answer is not equal to 2, the program will ask the user for the correct answer. Inputting something other than 2 will just loop back around to the while statement, again prompting for the correct answer. If while finally does evaluate to true (because answer equals 2) the loop will break and the program will resume by printing “Correct”.

The program can be enhanced further by “nesting” conditionals. A single indentation indicates a code block set aside for our while statement, but we can go for a second level of indentation to add an additional comparison.

```python
answer = 0
while (answer != 2):
    answer = int(input("What is 4 / 2? "))
    if (answer != 2):
        print ("Incorrect...")
print ("Correct!")
```

This program uses “nested” functions to incorporate if statements within while statements. The sheer amount of possibilities gained from this are virtually endless. Note how there are indentation levels that determine which code blocks can run within which functions. Every intended block, both 1 and 2 indent levels, will run when the while loop activates. It is a hard-to-master concept, but one that surely increases functionality.

Another common loop is the “for” loop. For is different from while in that a for loop runs through a range of numbers or a set of values instead of checking a conditional.

```python
for user_variable in range (1, 5):
    print (user_variable)
```

For takes the specified variable "user_variable" and uses the supplied range. The variable will be initialized at 1, and it will be iterated every time the function loops. By observing the output we can see how this works.

1
2
3
4

User_variable is printed out, then incremented to 2. It is printed again and incremented as 3. Once more time for 4. But it reaches 5 and stops, which is why 5 does not get printed out.
Because the keyword "range" was used, the for loop will always start at the first number and stop at the second. Leaving it out will have the for loop cycle through the values given.

```python
for user_variable in (1, 5):
    print(user_variable)
```

For example, only "range" is left out here, but the output is very different.
