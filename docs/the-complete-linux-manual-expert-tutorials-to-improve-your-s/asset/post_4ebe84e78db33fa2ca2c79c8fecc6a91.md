
## STEP 5

Additional functions can be added to Python through modules. Python has a vast range of modules available that can cover numerous programming duties. They add functions and can be imported as and when required. For example, to use advanced Mathematics functions enter:

```
import math
```

Once entered, you have access to all the Math module functions.

### STEP 6

To use a function from a module enter the name of the module followed by a full stop, then the name of the function. For instance, using the Math module, since you’ve just imported it into Python, you can utilise the square root function. To do so, enter:

```
math.sqrt(16)
```

You can see that the code is presented as module.function(data).

![](img/f80199d101da92d953f18eaa6205b48e_110_0.png)

![](img/f80199d101da92d953f18eaa6205b48e_110_1.png)

## FORGING FUNCTIONS

There are many different functions you can import created by other Python programmers and you will undoubtedly come across some excellent examples in the future; you can also create your own with the def command.

### STEP 1

Choose File > New File to enter the editor, let’s create a function called Hello, that greets a user. Enter:

```
def Hello():
print("Hello")

Hello()
```

Press F5 to save and run the script. You can see Hello in the Shell, type in Hello() and it returns the new function.

### STEP 3

To modify it further, delete the Hello("David") line, the last line in the script and press Ctrl+S to save the new script. Close the Editor and create a new file (File > New File). Enter the following:

```
from Hello import Hello

Hello("David")
```

Press F5 to save and execute the code.

![](img/f80199d101da92d953f18eaa6205b48e_110_2.png)

![](img/f80199d101da92d953f18eaa6205b48e_110_3.png)

### STEP 2

Let’s now expand the function to accept a variable, the user’s name for example. Edit your script to read:

```
def Hello(name):
print("Hello", name)

Hello("David")
```

This will now accept the variable name, otherwise it prints Hello David. In the Shell, enter: name=("Bob"), then: Hello(name). Your function can now pass variables through it.

### STEP 4

What you’ve just done is import the Hello function from the saved Hello.py program and then used it to say hello to David. This is how modules and functions work: you import the module then use the function. Try this one, and modify it for extra credit:

```
def add(a, b):
result = a + b
return result
```

![](img/f80199d101da92d953f18eaa6205b48e_110_4.png)

![](img/f80199d101da92d953f18eaa6205b48e_110_5.png)

## Conditions and Loops

Conditions and loops are what make a program interesting; they can be simple or rather complex. How you use them depends greatly on what the program is trying to achieve; they could be the number of lives left in a game or just displaying a countdown.

## TRUE CONDITIONS

Keeping conditions simple to begin with makes learning to program a more enjoyable experience. Let’s start then by checking if something is TRUE, then doing something else if it isn’t.

### STEP 1

Let’s create a new Python program that will ask the user to input a word, then check it to see if it’s a four-letter word or not. Start with File > New File, and begin with the input variable:

```
word=input("Please enter a four-letter word: ")
```

![](img/f80199d101da92d953f18eaa6205b48e_111_0.png)

### STEP 3

Now you can use an if statement to check if the word_length variable is equal to four and print a friendly confirmation if it applies to the rule:

```
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
    print (word, "is a four-letter word. Well done.")
```

The double equal sign (==) means check if something is equal to something else.

![](img/f80199d101da92d953f18eaa6205b48e_111_1.png)

### STEP 2

Now we can create a new variable, then use the len function and pass the word variable through it to get the total number of letters the user has just entered.

```
word=input("Please enter a four-letter word: ")
word_length=len(word)
```

![](img/f80199d101da92d953f18eaa6205b48e_111_2.png)

### STEP 4

The colon at the end of IF tells Python that if this statement is true do everything after the colon that’s indented. Next, move the cursor back to the beginning of the Editor:

```
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
    print (word, "is a four-letter word. Well done.")
else:
    print (word, "is not a four-letter word.")
```

![](img/f80199d101da92d953f18eaa6205b48e_111_3.png)

### STEP 5

Press F5 and save the code to execute it. Enter a four-letter word in the Shell to begin with, you should have the returned message that it's the word is four letters. Now press F5 again and rerun the program but this time enter a five-letter word. The Shell will display that it's not a four-letter word.

![](img/f80199d101da92d953f18eaa6205b48e_112_0.png)

### STEP 6

Now expand the code to include another conditions. Eventually, it could become quite complex. We've added a condition for three-letter words:

```
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
    print (word, "is a four-letter word. Well done.")
elif word_length == 3:
    print (word, "is a three-letter word. Try again.")
else:
    print (word, "is not a four-letter word.")
```

![](img/f80199d101da92d953f18eaa6205b48e_112_1.png)

## LOOPS

A loop looks quite similar to a condition but they are somewhat different in their operation. A loop will run through the same block of code a number of times, usually with the support of a condition.

### STEP 1

Let's start with a simple While statement. Like IF, this will check to see if something is TRUE, then run the indented code:

```
x = 1
while x < 10:
    print (x)
    x = x + 1
```

![](img/f80199d101da92d953f18eaa6205b48e_112_2.png)

### STEP 3

The For loop is another example. For is used to loop over a range of data, usually a list stored as variables inside square brackets. For example.

```
words=["Cat", "Dog", "Unicorn"]
for word in words:
    print (word)
```

![](img/f80199d101da92d953f18eaa6205b48e_112_3.png)

### STEP 2

The difference between if and while is when while gets to the end of the indented code, it goes back and checks the statement is still true. In our example x is less than 10. With each loop it prints the current value of x, then adds one to that value. When x does eventually equal 10 it stops.

![](img/f80199d101da92d953f18eaa6205b48e_112_4.png)

### STEP 4

The For loop can also be used in the countdown example by using the range function:

```
for x in range (1, 10):
    print (x)
```

The x=x+1 part isn't needed here because the range function creates a list between the first and last numbers used.

![](img/f80199d101da92d953f18eaa6205b48e_112_5.png)

## Python Modules

We’ve mentioned modules previously, (the Math module) but as modules are such a large part of getting the most from Python, it’s worth dedicating a little more time to them. In this instance we’re using the Windows version of Python 3.

## MASTERING MODULES

Think of modules as an extension that’s imported into your Python code to enhance and extend its capabilities. There are countless modules available and as we’ve seen, you can even make your own.

### STEP 1

Although good, the built-in functions within Python are limited. The use of modules, however, allows us to make more sophisticated programs. As you are aware, modules are Python scripts that are imported, such as import math.

### STEP 3

The result is an error in the IDLE Shell, as the Pygame module isn’t recognised or installed in Python. To install a module we can use PIP (Pip Installs Packages). Close down the IDLE Shell and drop into a command prompt or Terminal session. At an elevated admin command prompt, enter:

```
pip install pygame
```

![](img/f80199d101da92d953f18eaa6205b48e_113_0.png)

![](img/f80199d101da92d953f18eaa6205b48e_113_1.png)

### STEP 2

Some modules, especially on the Raspberry Pi, are included by default, the Math module being a prime example. Sadly, other modules aren’t always available. A good example on non-PI platforms is the Pygame module, which contains many functions to help create games. Try: import pygame.

### STEP 4

The PIP installation requires an elevated status due it installing components at different locations. Windows users can search for CMD via the Start button and right-click the result then click Run as Administrator. Linux and Mac users can use the Sudo command, with sudo pip install package.

![](img/f80199d101da92d953f18eaa6205b48e_113_2.png)

![](img/f80199d101da92d953f18eaa6205b48e_113_3.png)
