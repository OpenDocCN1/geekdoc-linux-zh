
The Python binary is installed into `/usr/bin/python`; if you run that, you will enter the Python interactive interpreter where you can type commands and have them executed immediately. Although PHP also has an interactive mode (use `php -a` to activate it), it is neither as powerful nor as flexible as Python's.

As with Perl, PHP, and other scripting languages, you can also execute Python scripts by adding a *shebang* line to the start of your scripts that points to `/usr/bin/python` and then setting the file to be executable.

The third and final way to run Python scripts is through `mod_python`, which is installed by default when you select the Web Server application group from the Add/Remove Software dialog.

For the purposes of this introduction, we will be using the interactive Python interpreter because it provides immediate feedback on commands as you type them.

## Getting Interactive

We will be using the interactive interpreter for this chapter, so it is essential that you are comfortable using it. To get started, open a terminal and run the command `python`. You should see this:

```
[paul@caitlin ~]$ python
Python 2.3.4 (#1, Oct 26 2004, 16:42:40)
[GCC 3.4.2 20041017 (Red Hat 3.4.2-6.fc3)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

The `>>>` is where you type your input, and you can set and get a variable like this:

```
>>> python = 'great'
>>> python
great
>>>
```

On line one, the variable `python` is set to the text `great`, and on line two that value is read back from the variable simply by typing the name of the variable you want to read. Line three shows Python printing the variable; on line four, you are back at the prompt to type more commands. Python remembers all the variables you use while in the interactive interpreter, which means you can set a variable to be the value of another variable.

When you are done, press **Ctrl+D** to exit. At this point, all your variables and commands are forgotten by the interpreter, which is why complex Python programs are always saved in scripts.

## The Basics of Python

Python is a language wholly unlike most others, and yet it is so logical that most people can pick it up very quickly. You have already seen how easily you can assign strings, but in Python nearly everything is that easy—as long as you remember the syntax!

### Numbers

The way Python handles numbers is more precise than some other languages. It has all the normal operators—such as + for addition, - for subtraction, / for division, and * for multiplication—but it adds % for modulus (division remainder), ** for raise to the power, and // for floor division. It is also very specific about which type of number is being used, as this example shows:

```
>>> a = 5
>>> b = 10
>>> a * b
50
>>> a / b
0
>>> b = 10.0
>>> a / b
0.5
>>> a // b
0.0
```

The first division returns 0 because both a and b are integers (whole numbers), so Python calculates the division as an integer, giving 0. By converting b to 10.0, Python considers it to be a floating-point number and so the division is now calculated as a floating-point value, giving 0.5. Even with b being floating-point, using //—floor division—rounds it down.

Using **, you can easily see how Python works with integers:

```
>>> 2 ** 30
1073741824
>>> 2 ** 31
2147483648L
```

The first statement raises 2 to the power of 30 (that is, $2 \times 2 \times 2 \times 2 \times 2 \times \ldots$), and the second raises 2 to the power of 31. Notice how the second number has a capital L on the end of it—this is Python telling you that it is a long integer. The difference between long integers and normal integers is slight but important: Normal integers can be calculated using simple instructions on the CPU, whereas long integers—because they can be as big as you need them to be—need to be calculated in software and therefore are slower.

When specifying big numbers, you need not put the L at the end—Python will figure it out for you. Furthermore, if a number starts off as a normal number and then exceeds its boundary, Python automatically converts it to a long integer. The same is not true the other way around: If you have a long integer and then divide it by another number so that it could be stored as a normal integer, it remains a long integer:

```python
>>> num = 9999999999999999999999999999999999999999L
>>> num = num / 100000000000000000000000000000000000
>>> num
9999L
```

You can convert between number types using typecasting, like this:

```python
>>> num = 10
>>> int(num)
10
>>> float(num)
10.0
>>> long(num)
10L
>>> floatnum = 10.0
>>> int(floatnum)
10
>>> float(floatnum)
10.0
>>> long(floatnum)
10L
```

You need not worry whether you are using integers or long integers; Python handles it all for you, so you can concentrate on getting the code right.

## More on Strings

Python stores strings as an immutable sequence of characters—a jargon-filled way of saying "It is a collection of characters that, once set, cannot be changed without creating a new string." Sequences are important in Python. There are three primary types, of which strings are one, and they share some properties. Mutability makes much sense when you learn about lists in the next section.

As you saw in the previous example, you can assign a value to strings in Python with just an equal sign, like this:

```python
>>> mystring = 'hello'
>>> myotherstring = 'goodbye';
>>> mystring
'hello'
>>> myotherstring
'goodbye'
>>> test = "Are you really Bill O'Reilly?"
>>> test
'Are you really Bill O'Reilly?'
```

The first example encapsulates the string in single quotation marks and the second and third in double quotation marks. However, printing the first and second strings shows them both in single quotation marks because Python does not distinguish between the two. The third example is the exception—it uses double quotation marks because the string itself contains a single quotation mark. Here, Python prints the string with double quotation marks because it knows the string contains the single quotation mark.

Because the characters in a string are stored in sequence, you can index into them by specifying the character you are interested in. Like most other languages, these indexes are zero-based, which means you need to ask for character 0 to get the first letter in a string. For example:

```
>>> string = "This is a test string"
>>> string
'This is a test string'
>>> string[0]
'T'
>>> string[0], string[3], string[20]
('T', 's', 'g')
```

The last line shows how, with commas, you can ask for several indexes at the same time. You could print the entire first word using this:

```
>>> string[0], string[1], string[2], string[3]
('T', 'h', 'i', 's')
```

However, for that purpose you can use a different concept: slicing. A *slice* of a sequence draws a selection of indexes. For example, you can pull out the first word like this:

```
>>> string[0:4]
'This'
```

The syntax there means "take everything from position 0 (including 0) and end at position 4 (excluding it)." So, [0:4] copies the items at indexes 0, 1, 2, and 3. You can omit either side of the indexes, and it will copy either from the start or to the end:

```
>>> string[:4]
'This'
>>> string[5:]
'is a test string'
>>> string[11:]
'est string'
```

You can also omit both numbers, and it will give you the entire sequence:

```
>>> string
'This is a test string'
```

Later you will learn precisely why you would want to do that, but for now there are a number of other string intrinsics that will make your life easier. For example, you can use the + and * operators to concatenate (join) and repeat strings, like this:

```
>>> mystring = 'Python'
>>> mystring * 4
'PythonPythonPythonPython'
>>> mystring = mystring + ' rocks! '
>>> mystring * 2
'Python rocks! Python rocks! '
```

In addition to working with operators, Python strings come with a selection of built-in methods. You can change the case of the letters with capitalize() (uppercases the first letter and lowercases the rest), lower() (lowercases them all), title() (uppercases the first letter in each word), and upper() (uppercases them all). You can also check whether strings match certain cases with islower(), istitle(), and isupper(); that also extends to isalnum() (returns true if the string is letters and numbers only) and isdigit() (returns true if the string is all numbers).

This example demonstrates some of these in action:

```
>>> string
'This is a test string'
>>> string.upper()
'THIS IS A TEST STRING'
>>> string.lower()
'this is a test string'
>>> string.isalnum()
False
>>> string = string.title()
>>> string
'This Is A Test String'
```

Why did isalnum() return false—your string contains only alphanumeric characters, doesn't it? Well, no. There are spaces in there, which is what is causing the problem. More importantly, we were calling upper() and lower() and they were not changing the contents of the string—they just returned the new value. So, to change our string from This is a test string to This Is A Test String, we actually have to assign it back to the string variable.
