
# Get started with Python

![](img/e016e192a91ffc1a9e47474690a590742f_8_0.png)

# Hello World

Let’s get stuck in, and what better way than with the programmer’s best friend, the ‘Hello World’ application! Start by opening a terminal. Its current working directory will be your home directory. It’s probably a good idea to make a directory for the files we’ll be creating in this tutorial, rather than having them loose in your home directory. You can create a directory called Python using the command `mkdir Python`. You’ll then want to change into that directory using the command `cd Python`.

The next step is to create an empty file using the command `touch` followed by the filename. Our expert used the command `touch hello_world.py`. The final and most important part of setting up the file is making it executable. This allows us to run code inside the hello_world.py file. We do this with the command `chmod +x hello_world.py`. Now that we have our file set up, we can go ahead and open it up in nano, or any text editor of your choice. Gedit is a great editor with syntax highlighting support that should be available on any distribution. You’ll be able to install it using your package manager if you don’t have it already.

```bash
[liam@liam-Laptop ~]$ mkdir Python
[liam@liam-Laptop ~]$ cd Python/
[liam@liam-Laptop Python]$ touch hello_world.py
[liam@liam-Laptop Python]$ chmod +x hello_world.py
[liam@liam-Laptop Python]$ nano hello_world.py
```

Our Hello World program is very simple, it only needs two lines. The first line begins with a ‘shebang’ (the symbol #! – also known as a hashbang) followed by the path to the Python interpreter. The program loader uses this line to work out what the rest of the lines need to be interpreted with. If you’re running this in an IDE like IDLE, you don’t necessarily need to do this.

The code that is actually read by the Python interpreter is only a single line. We’re passing the value Hello World to the print function by placing it in brackets immediately after we’ve called the print function. Hello World is enclosed in quotation marks to indicate that it is a literal value and should not be interpreted as source code. As expected, the print function in Python prints any value that gets passed to it from the console.

You can save the changes you’ve just made to the file in nano using the key combination `Ctrl+O`, followed by `Enter`. Use `Ctrl+X` to exit nano.

```python
#!/usr/bin/env python2
print("Hello World")
```

You can run the Hello World program by prefixing its filename with `./` – in this case you’d type: `./hello_world.py`.

```bash
[liam@liam-Laptop Python]$ ./hello_world.py
Hello World
```

> **TIP**
> If you were using a graphical editor such as gedit, then you would only have to do the last step of making the file executable. You should only have to mark the file as executable once. You can freely edit the file once it is executable.

# Variables and data types

A variable is a name in source code that is associated with an area in memory that you can use to store data, which is then called upon throughout the code. The data can be one of many types, including:

| **Integer** | Stores whole numbers |
| :--- | :--- |
| **Float** | Stores decimal numbers |
| **Boolean** | Can have a value of True or False |
| **String** | Stores a collection of characters. “Hello World” is a string |

As well as these main data types, there are sequence types (technically, a string is a sequence type but is so commonly used we’ve classified it as a main data type):

| **List** | Contains a collection of data in a specific order |
| :--- | :--- |
| **Tuple** | Contains a collection of immutable data in a specific order |

A tuple would be used for something like a co-ordinate, containing an x and y value stored as a single variable, whereas a list is typically used to store larger collections. The data stored in a tuple is immutable because you aren’t able to change values of individual elements in a tuple. However, you can do so in a list.

It will also be useful to know about Python’s dictionary type. A dictionary is a mapped data type. It stores data in key-value pairs. This means that you access values stored in the dictionary using that value’s corresponding key, which is different to how you would do it with a list. In a list, you would access an element of the list using that element’s index (a number representing the element’s position in the list).

Let’s work on a program we can use to demonstrate how to use variables and different data types. It’s worth noting at this point that you don’t always have to specify data types in Python. Feel free to create this file in any editor you like. Everything will work just fine as long as you remember to make the file executable. We’re going to call ours `variables.py`.

![](img/e016e192a91ffc1a9e474690a590742f_9_0.png)

# Interpreted vs compiled languages

An interpreted language such as Python is one where the source code is converted to machine code and then executed each time the program runs. This is different from a compiled language such as C, where the source code is only converted to machine code once – the resulting machine code is then executed each time the program runs.

The following line creates an integer variable called hello_int with the value of 21. Notice how it doesn't need to go in quotation marks.

The same principle is true of Boolean values.

We create a tuple in the following way.

And a list in this way.

You could also create the same list in the following way.

We might as well create a dictionary while we're at it. Notice how we've aligned the colons below to make the code tidy.

Notice that there will now be two exclamation marks when we print the element.

At this point, it's worth explaining that any text in a Python file that follows a `#` character will be ignored by the interpreter. This is so you can write comments in your code.

```python
#!/usr/bin/env python2

# We create a variable by writing the name of the variable we want followed
# by an equals sign, which is followed by the value we want to store in the
# variable. For example, the following line creates a variable called
# hello_str, containing the string 'Hello World'.
hello_str = "Hello World"

hello_int = 21

hello_bool = True

hello_tuple = (21, 32)

hello_list = ["Hello", "this", "is", "a", "list"]

# This list now contains 5 strings. Notice that there are no spaces
# between these strings so if you were to join them up to make a sentence
# you'd have to add a space between each element.

hello_list = list()
hello_list.append("Hello")
hello_list.append("this")
hello_list.append("is")
hello_list.append("a")
hello_list.append("list")

# The first line creates an empty list and the following lines use the append
# function of the list type to add elements to the list. This way of using a
# list isn't really very useful when working with strings you know of in
# advance, but it can be useful when working with dynamic data such as user
# input. This list will overwrite the first list without any warning as we
# are using the same variable name as the previous list.

hello_dict = {"first_name": "Liam",
              "last_name": "Fraser",
              "eye_colour": "Blue"}

# Let's access some elements inside our collections
# We'll start by changing the value of the last string in our hello_list and
# add an exclamation mark to the end. The "list" string is the 5th element
# in the list. However, indexes in Python are zero-based, which means the
# first element has an index of 0.

print(hello_list[4])
hello_list[4] += "!"
# The above line is the same as
hello_list[4] = hello_list[4] + "!"
print(hello_list[4])
```

> “Any text in a Python file that follows a # character will be ignored”

![](img/e016e192a91ffc1a9e474690a590742f_10_0.png)

Remember that tuples are immutable, although we can access the elements of them like so:

```python
print(str(hello_tuple[0]))
# We can't change the value of those elements like we just did with the list
# Notice the use of the str function above to explicitly convert the integer
# value inside the tuple to a string before printing it.
```

Let's create a sentence using the data in our hello_dict:

```python
print(hello_dict["first_name"] + " " + hello_dict["last_name"] + " has " + hello_dict["eye_colour"] + " eyes.")
```

A tidier way of doing this would be to use Python's string formatter:

```python
print("{} {} has {} eyes.".format(hello_dict["first_name"], hello_dict["last_name"], hello_dict["eye_colour"]))
```

## Control structures

In programming, a control structure is any kind of statement that can change the path that the code execution takes. For example, a control structure that decided to end the program if a number was less than 5 would look something like this:

```python
#!/usr/bin/env python2

import sys # Used for the sys.exit function

int_condition = 5

if int_condition < 6:
    sys.exit("int_condition must be >= 6")
else:
    print("int_condition was >= 6 – continuing")
```

The path that the code takes will depend on the value of the integer int_condition. The code in the 'if' block will only be executed if the condition is true. The import statement is used to load the Python system library; the latter provides the exit function, allowing you to exit the program, printing an error message. Notice that indentation (in this case four spaces per indent) is used to indicate which statement a block of code belongs to.

'If' statements are probably the most commonly used control structures. Other control structures include:

- **'For'** statements, which allow you to iterate over items in collections, or to repeat a piece of code a certain number of times.
- **'While'** statements, a loop that continues while the condition is true.

We're going to write a program that accepts user input from the user to demonstrate how control structures work. We're calling it **construct.py**.

The 'for' loop is using a local copy of the current value, which means any changes inside the loop won't make any changes affecting the list. On the other hand however, the 'while' loop is directly accessing elements in the list, so you could change the list there should you want to do so. We will talk about variable scope in some more detail later on. The output from the above program is as follows:

```bash
[liam@liams-laptop Python]$ ./construct.py
How many integers? 3
Please enter integer 1: 1
You must enter an integer
Please enter integer 1: 5
Please enter integer 2: 2
Please enter integer 3: 6
Using a for loop
5
2
6
Using a while loop
5
2
6
```

## Indentation in detail

As previously mentioned, the level of indentation dictates which statement a block of code belongs to. Indentation is mandatory in Python, whereas in other languages, sets of braces are used to organise code blocks. For this reason, it is essential that you use a consistent indentation style. Four spaces are typically used to represent a single level of indentation in Python. You can use tabs, but tabs are not well defined, especially if you happen to open a file in more than one editor.

> “The 'for' loop uses a local copy, so changes in the loop won't affect the list”

## More about a Python list

A Python list is similar to an array in other languages. A list or tuple in Python can contain data of multiple types, which is not usually the case with arrays in other languages. For this reason, we recommend that you only store data of the same type in a list. This should almost always be the case anyway due to the nature of the way data in a list would be processed.
