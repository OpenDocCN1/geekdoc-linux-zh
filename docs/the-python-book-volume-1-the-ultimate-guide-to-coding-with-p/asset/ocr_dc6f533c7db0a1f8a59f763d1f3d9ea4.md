![](bbox=[0.639, 0.029, 1.0, 0.068])

![](bbox=[0.099, 0.197, 0.62, 0.369])

# 04 Setting it up

Having detailed comments in your code is important because it allows you to note down things you find confusing and document complex procedures. If another programmer has to work with your code in the future, they’ll be extremely grateful. Start by adding a comment with a description of what the program will do and your name. All comment lines start with a hash (#) and are not interpreted as code by the Python interpreter. We import the sys library so we can use the sys.exit function to close the program later on. We also import everything from the decimal library because we want to make use of the decimal type.

# 01 Staying organised

We don’t want to have messy folders on our new Pi, so let’s go to the file manager and organise ourselves. Open the file manager by clicking the icon next to the menu icon on the bottom left of the screen. Create a new folder by right-clicking and selecting New>Folder, then type a name and click OK. We created a folder called Python, and inside that we created a folder called Hello World v2.

![](bbox=[0.368, 0.377, 0.619, 0.527])

![](bbox=[0.099, 0.508, 0.352, 0.681])

# 03 Saving your work

It’s always a good idea to keep saving your work with Ctrl+S as you program, because it would be a shame to lose anything you’ve been working on. To save your file for the first time, either press Ctrl+S or go to the File menu and select Save. Give the file a sensible name and save it in the tidy folder structure you created before. It’s a good habit to be well organised when programming, because it makes things much easier when your projects become bigger and more complicated.

# 02 Starting Geany

Start Geany by going to the LXDE menu and going to Programs. From here, select Geany. Once you’re in the Geany interface, create a new Python file from a template by selecting ‘New (with template)>main.py’. Delete everything in this template apart from the first line: #!/usr/bin/env python. This line is important because it means you can run the code from the command line and the Bash shell will know to open it with the Python interpreter.

```
```python
#!/usr/bin/env python

# An advanced Hello World program
# Programming in Python via
# for Linux User and Developer

# Import the sys library for
import sys
# Import everything from the
from decimal import *
```
```

# 05 Variables

A variable is data that is stored in memory and can be accessed via a name. Our program is going to start by asking for your first name, store that in a variable and then print out a welcome message. We’re going to add a comment that explains this and create a variable called firstName. Notice how we’ve capitalised the first letter of the second word to make it easier to read. We want the firstName variable to hold the value returned by a function called raw_input, that will ask the user for input. The question is passed into the print function within brackets, and because this is a string it is enclosed within quotation marks. A string type is basically a collection of characters. Note the extra space we’ve added after the colon because the user types their input straight after this question.

```
```python
# Get the user's first name and output a message
# The string in quotation marks will be displayed
```
```

```
```python
print('Welcome ' + firstName + '\n')
```
```

# 06 Printing a message

Now that we have a value in firstName, we need to output a welcome message to the screen. We print to the screen in Python using the print function. The print function is followed by a pair of brackets which enclose the values to print. When using the addition operator with strings, they are joined together. Note how firstName doesn’t need to be enclosed by quotation marks because it is the name of a variable. If it was enclosed in quotation marks, the text firstName would be output. We finish off by adding a ‘\n’ character (new line character) to our output to leave one blank line before we start our next example.

> > When using the addition operator
> > with strings, they are joined together