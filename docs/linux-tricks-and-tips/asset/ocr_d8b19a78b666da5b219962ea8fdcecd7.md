# Conditions and Loops

![](bbox=[0.07, 0.13, 0.15, 0.16])

Press F5 and save the code to execute it. Enter a four-letter word in the Shell to begin with; you should have the returned message that it’s the word is four letters. Now press F5 again and rerun the program but this time enter a five-letter word. The Shell will display that it’s not a four-letter word.

![](bbox=[0.51, 0.13, 0.58, 0.16])

Now expand the code to include another conditions. Eventually, it could become quite complex. We’ve added a condition for three-letter words:

```
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
    print(word, "is a four-letter word. Well done.")
elif word_length == 3:
    print(word, "is a three-letter word. Try again.")
else:
    print(word, "is not a four-letter word.")
```

![](bbox=[0.07, 0.26, 0.93, 0.4])

# LOOP S

A loop looks quite similar to a condition but they are somewhat different in their operation. A loop will run through the same block of code a number of times, usually with the support of a condition.

![](bbox=[0.06, 0.51, 0.14, 0.54])

Let’s start with a simple While statement. Like IF, this will check to see if something is TRUE, then run the indented code:

```
x = 1
while x < 10:
    print(x)
    x = x + 1
```

![](bbox=[0.51, 0.51, 0.58, 0.54])

The For loop is another example. For is used to loop over a range of data, usually a list stored as variables inside square brackets. For example:

```
words=["Cat", "Dog", "Unicorn"]
for word in words:
    print(word)
```

![](bbox=[0.07, 0.63, 0.49, 0.71])

![](bbox=[0.51, 0.63, 0.93, 0.71])

![](bbox=[0.06, 0.74, 0.14, 0.77])

The difference between if and while is when while gets to the end of the indented code, it goes back and checks the statement is still true. In our example x is less than 10. With each loop it prints the current value of x, then adds one to that value. When x does eventually equal 10 it stops.

![](bbox=[0.51, 0.74, 0.58, 0.77])

The For loop can also be used in the countdown example by using the range function:

```
for x in range(1, 10):
    print(x)
```

The x=x+1 part isn’t needed here because the range function creates a list between the first and last numbers used.

![](bbox=[0.07, 0.86, 0.49, 0.95])

![](bbox=[0.51, 0.86, 0.93, 0.95])