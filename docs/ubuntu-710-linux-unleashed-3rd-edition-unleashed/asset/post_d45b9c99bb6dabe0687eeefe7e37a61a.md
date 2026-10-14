
# CHAPTER 24

## Working with Python

As PHP has come to dominate the world of web scripting, Python is increasingly dominating the domain of command-line scripting. Python’s precise and clean syntax makes it one of the easiest languages to learn, and it allows programmers to code more quickly and spend less time maintaining their code. Although PHP is fundamentally similar to Java and Perl, Python is closer to C and Modula-3, and so it might look unfamiliar at first.

Most of the other languages have a group of developers at their cores, but Python has Guido van Rossum—creator, father, and Benevolent Dictator For Life (BDFL). Although Guido spends less time working on Python now, he still essentially has the right of veto changes to the language, which has enabled it to remain consistent over the many years of its development. The end result is that, in Guido’s own words, “Even if you are in fact clueless about language design, you can tell that Python is a very simple language.”

The following pages constitute a “quick-start” tutorial to Python designed to give you all the information you need to put together basic scripts and to point you toward resources that can take you further.

### Python on Linux

Ubuntu comes with Python installed by default, as do many other versions of Linux and UNIX—even Mac OS X comes with Python preinstalled. Part of this is due to convenience because it is such a popular scripting language and it saves having to install it later if the user wants to run a script.

The Python binary is installed into /usr/bin/python; if you run that, you enter the Python interactive interpreter where you can type commands and have them executed immediately. Although PHP also has an interactive mode (use php -a to activate it), it is neither as powerful nor as flexible as Python's.

As with Perl, PHP, and other scripting languages, you can also execute Python scripts by adding a shebang line (#!) to the start of your scripts that point to /usr/bin/python and then setting the file to be executable.

The third and final way to run Python scripts is through mod_python, which you can install through synaptic.

For the purposes of this introduction, we use the interactive Python interpreter because it provides immediate feedback on commands as you type them.

### IN THIS CHAPTER

- Python on Linux
- The Basics of Python
- Functions
- Object Orientation
- The Standard Library and the Vaults of Parnassus
- Reference

immediately. Although PHP also has an interactive mode (use php -a to activate it), it is neither as powerful nor as flexible as Python's.

As with Perl, PHP, and other scripting languages, you can also execute Python scripts by adding a shebang line (#!) to the start of your scripts that point to /usr/bin/python and then setting the file to be executable.

The third and final way to run Python scripts is through mod_python, which you can install through synaptic.

For the purposes of this introduction, we use the interactive Python interpreter because it provides immediate feedback on commands as you type them.

### Getting Interactive

We will be using the interactive interpreter for this chapter, so it is essential that you are comfortable using it. To get started, open a terminal and run the command python. You should see this:

```
[paul@caitlin ~]$ python
Python 2.4.3 (#2, Apr 27 2006, 14:43:58)
[GCC 4.0.3 (Ubuntu 4.0.3-1ubuntu5)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

The >>> is where you type your input, and you can set and get a variable like this:

```
>>> python = 'great'
>>> python
'great'
>>>
```

On line one, the variable python is set to the text great, and on line two that value is read back from the variable simply by typing the name of the variable you want to read. Line three shows Python printing the variable; on line four you are back at the prompt to type more commands. Python remembers all the variables you use while in the interactive interpreter, which means you can set a variable to be the value of another variable.

When you are done, press Ctrl+D to exit. At this point, all your variables and commands are forgotten by the interpreter, which is why complex Python programs are always saved in scripts!

## The Basics of Python

Python is a language wholly unlike most others, and yet it is so logical that most people can pick it up quickly. You have already seen how easily you can assign strings, but in Python nearly everything is that easy—as long as you remember the syntax!

### Numbers

The way Python handles numbers is more precise than some other languages. It has all the normal operators—such as + for addition, - for subtraction, / for division, and * for multiplication—but it adds % for modulus (division remainder), ** for raise to the power, and // for floor division. It is also specific about which type of number is being used, as this example shows:

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

The first division returns 0 because both a and b are integers (whole numbers), so Python calculates the division as an integer, giving 0. By converting b to 10.0, Python considers it to be a floating-point number, and so the division is now calculated as a floating-point value, giving 0.5. Even with b being floating point, using //—floor division—rounds it down.

Using **, you can easily see how Python works with integers:

```
>>> 2 ** 30
1073741824
>>> 2 ** 31
2147483648L
```

The first statement raises 2 to the power of 30 (that is, 2 × 2 × 2 × 2 × 2 ...), and the second raises 2 to the power of 31. Notice how the second number has a capital L on the end of it—this is Python telling you that it is a long integer. The difference between long integers and normal integers is slight but important: Normal integers can be calculated using simple instructions on the CPU, whereas long integers—because they can be as big as you need them to be—need to be calculated in software and therefore are slower.

When specifying big numbers, you need not put the L at the end—Python figures it out for you. Furthermore, if a number starts off as a normal number and then exceeds its boundaries, Python automatically converts it to a long integer. The same is not true the
