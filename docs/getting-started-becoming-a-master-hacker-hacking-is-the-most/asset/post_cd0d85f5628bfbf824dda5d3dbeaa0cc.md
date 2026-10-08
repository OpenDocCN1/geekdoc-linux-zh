
## Comments

Like any programming language, Python has the capability to add comments. Comments are simply text that is added to your code to help explain what you are trying to do. These comments are NOT executed by the interpreter. The Python interpreter sees the comments and simply skips over them until it comes to another line of executable code.

Comments are not required in your scripts but are highly advisable. Imagine coming back to your script six months or six years from now and trying to determine what you were trying to accomplish. Moreover, imagine another programmer trying to decipher your code five years from now. In both cases, comments are mighty helpful and will save you both significant time and frustration.

Python uses the “#” symbol to designate a single line of comment. When you want to write multiline comments, you can use three double quotation marks (`'''`) to begin the comment and three double quotation marks at the end.

As you can see below, I have enhanced our secondpythonscript.py with some comments that help explain what we were trying to do with this code.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_538_0.png)

```python
#!/usr/bin/python3
"""
This script is designed to teach different variable types
These comments are here to help us later understand
why and how we wrote this code. You will not regret
taking the time to add comments!
"""

HackersAriseStringVariable = "Getting Started Becoming a Master Hacker"
```

When we execute the script again, nothing changes as the Python interpreter simply skips over the comments and executes only the non-commented lines.

## Functions

Functions in Python (like other programming languages) are bits of code that perform a designated action. They are like mini-programs within your script. For instance, the print() statement we used above is a function that displays whatever you pass to it in the script. There are a large number of functions in Python that you can import and use. Most are available in your default installation of Python, but there are numerous others available in the downloadable libraries in Python.

Here is a brief sampling of available functions.

- `abs()` - returns the absolute value of a number
- `ascii()` - returns a string containing a printable representation of an object
- `bool()` - returns a Boolean value
- `dict()` - creates a new dictionary
- `help()` - invokes the built-in help
- `hash()` - returns the hash value of an object
- `max()` - returns the largest value
- `hex()` - converts an integer to hexadecimal
- `min()` - returns the smallest value
- `round()` - returns a rounded number
- `len()` - returns the length of the object
- `sum()` - sums the items of an iterable and returns the total

```bash
root@kali-2019:~# ./secondpythonscript.py
Getting Started Becoming a Master Hacker
12
3.1415
3
root@kali-2019:~#
```

You can also create your own functions, but before you do so, make certain that it has not already been created. You can check the official Python documentation at [https://docs.python.org](https://docs.python.org).

To create your own function, use the def statement followed by the name you want to use for the function. For instance, if we wanted to create a function named “new_function,” we would enter: `def new_function`.

## Lists

Most programming languages use what they refer to as arrays to store multiple separate objects. These arrays are lists of values that can be retrieved, deleted, replaced, and manipulated when referenced by an index `[]`. In Python, arrays are known as lists.

It’s worth noting here that Python—like many other programming languages—begins counting with 0.

The first element is element 0, the second element is element 1, and so forth. This means that if you wanted to access the fourth element in a list, you would do so with `list[3]`.

Lists in Python are iterable. This means that the list can provide successive elements when you run all the way through it (see Loops). This is useful because quite often when we use lists, we are looking through the list for a particular value such as a password list.

Let’s imagine you want to display the third element in our list in our secondpythonscript.py (we created a list named HackersAriseList). We can access that element and print it by calling the list’s name followed by the index of the element in square brackets.

Let’s test this now on our script. On Line 27 of our script, change the index in the square brackets to `[2]`.

Now, run the script again.

`kali > ./secondpythonscript.py`

As you can see, this time, the script prints the number 3 from our list!

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_541_0.png)

```python
#!/usr/bin/python3

import socket

s = socket.socket()

s.connect(('192.168.1.101', 22))

answer = s.recv(1024)

print(answer)

s.close()
```

## Modules

A module is simply a section of code saved into a separate file so that you can use it as many times as you need without having to reenter all the code again and again. If you want to use a module, you need to import it. As we discussed earlier, using standard and third-party modules is one of the key strengths of Python, and these particular modules are why hackers prefer Python. So, if we wanted to use the ftp module, we would import it.

```python
import ftplib
```

Later in this chapter we will use this module and the socket module in our ftp password cracking script.

**Network Communications in Python**

Before we move on to more advanced Python concepts, let’s use what we learned so far to write a couple of scripts that may be useful to hackers and information security professionals.

**Building a TCP Client**

In this script, we’ll create a simple TCP network connection in Python using a very practical and widely used module named “socket.” Socket is among those many modules in Python that can be used for a multitude of tasks. Here we will be using the socket module to create our simple TCP connection.

Let’s build the script seen below, and then we will analyze it here. This script goes out and grabs the banner presented by the SSH protocol on port 22. A banner, as we saw earlier in Chapter 4 with Shodan, is an “announcement” that an application makes when someone or something connects to it. Hackers can use this technique for reconnaissance to determine what application, and even what version of the application, is running on a port. This is exactly what Shodan does. It grabs the banner from every port and IP address and puts the banner information into a database, indexes it, and allows us to search by that information.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_543_0.png)

In the first step, we need to import the socket module we referenced earlier. Once it has been imported, we can then use its functions and tools. In this script, we will use the socket module to create a connection over the network for us. A socket is a module that enables two computer nodes to communicate with each other. It uses the familiar server/client architecture.

In the next step, we create a variable and associate it with the socket class from the socket module (Remember my earlier discussion on classes?). We do this so we don’t have to reference the full `socket.socket()` syntax each time we want to use it. Now we can simply use the variable name, making our coding simpler and more efficient.

Next, we use the `connect()` method from the socket module to make a network connection to a particular IP address and port. Remember that methods are functions available for a particular object. In Python, the syntax is `object.method`. In this case, we are connecting to IP address 192.168.1.101 (use the IP address of your Metasploitable 2 system) and port 22.

Once you make the connection, there are a number of things we can do. In this script, we use the receive method `recv` to read 1024 bytes of data from our socket (TCP connection) and store that information in a variable called `answer`. The receive method takes the banner information and places it into the variable.

Once the variable has the banner information, we will want to print it with the `print()` function. On the final line of the script, we close the socket.

Now, save this script as `SSH BannerGrab.py` and give yourself permission to execute it with `chmod` (`chmod 755 SSHBannerGrab.py`). Let’s now run this script, and if the target system has SSH running on port 22, it will make a TCP connection, receive the banner, place the banner into a variable and print the contents of the variable as seen below.

We have just created our first reconnaissance Python script!

As you can see, this script not only told us what application is running on port 22, but also the version of the application (7.3p1) and the operating system (Debian-1). In many
