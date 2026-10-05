
FIGURE 11-1:
The Python shell, just after it opens.

The bottom box is the Python shell, and the three arrows are called the prompt, and indicate that Python is ready for you to enter a command. You can test this by entering the license() command, which shows you a history of Python, before displaying the terms and conditions of using it. If you don't want to get bogged down in legalese, by typing q and then pressing Enter when prompted.

You can increase the size of the shell to make it easier to read the output. Click and drag the bottom border of the editor box to adjust the amount of space dedicated to each of the two boxes. Use the button in the top right of the Thonny title bar to maximize the window too. (See Chapter 4.)

One of the most basic commands in any programming language is the one that tells the computer to put some text on the screen. In Python, this command is print(), and you can use it like this:

```python
>>> print("hello world")
hello world
>>>
```

A simple program like this one that displays a greeting on the screen is often called a “hello world” program. It's the starting point for learning most program-languages.

The brackets are used to enclose whatever you want to output to the screen. The quotes are used to mark the start and end of the text you want to show.

As you type, you might notice that Thonny highlights your text using different colors. Gray is used to highlight a section that still needs a closing bracket, and green is used to highlight a section that still needs a closing quote mark. This highlighting is a feature of Thonny that helps Python beginners avoid common mistakes. Don't press Enter if your code is still highlighted: You've left something out.

Whatever you type in the quotes after the print() command is "printed" on the screen, and Python then returns you to the prompt so that you can enter another command.

Like the Linux shell, Python is case-sensitive — it won't work if you use capital letters where you shouldn't. The command print() must be entered in lowercase; otherwise, Python tells you a name error, because what you entered hasn't been defined. You can mess around with the word in quotes as much as you like, however: This is the text that you want to appear onscreen. Take a look at these examples:

![](img/df9a01bf057d58c2401b5edabd6e8829_225_0.png)

```python
>>> PRINT("Hello Leo!
```

If you make a mistake entering something, you can press Ctrl-C to get back to the prompt and start over. In particular, if you make a mistake with brackets, Python might expect you to enter a multiline command and not give you a result or a prompt when you press Enter. The way out is to press Ctrl-C.

# Using the shell to calculate sums

You can also use the shell to carry out calculations. Table 11-1 shows you the mathematical operators you can use. Just put the sum after the print() command, like this:

```python
>>> print(5 + 5)
10
>>> print(9 - 4)
5
>>> print(7 * 7)
49
>>> print(10 / 2)
5.0
```

# Mathematical Operators in Python

| Operator | Description |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| // | Division, discarding any decimal portion |
| % | Modulo, which shows the remainder after division |

TABLE 11-1

![](img/df9a01bf057d58c2401b5edabd6e8829_226_0.png)

Don't use quotes around the sum in the print() command. What would happen if you did? Python would put on the screen literally whatever characters you asked it to, like this:

```python
>>> print("5 + 5")
5 + 5
```

If you want to force a rounding effect to remove any decimal portion from your answer after dividing a number, you can use the floor division (//) operator, like this:

```python
>>> print(10 / 3)
3.3333333333333335
>>> print(10 // 3)
3
```

An operator might not have come across before is modulo: It uses the % sign and tells you the remainder after a division. Here are some examples:

```python
>>> print(10 % 3)
1
>>> print(10 % 2)
0
```

You can use the modulo operator to tell whether one number is divisible by another (the modulo is 0, if so).

These sums are quite basic, but you can enter more advanced sums by stringing together numbers and operators. In algebra, you use parentheses to surround the bits of the sum that belongs together and should be carried out. You still need to put parentheses around the whole sum for the print() command. For example:

```python
>>> print((10/3))
6.666666666666667
>>> print(10 / (3*2))
1.6666666666666667
```

![](img/df9a01bf057d58c2401b5edabd6e8829_227_0.png)

You can also do mathematics in the shell by entering the sums without a print() command, but it's essential to use the command when you're creating programs, as you see shortly.

The spaces we've used around the mathematical operators are optional. They help with readability, and in that last example, help to show which parts of the sum belong together.

# Creating the Times Tables Program

In this section, we show how to make a program that generates multiplication tables. For example, if the user requests a multiplication table for the number 7, the program outputs the sequence 7, 14, 21, and so on. The program is only a few lines long, but it teaches you how to create programs, using variables to ask the user for information, and create loops — sections of program that repeat. You build on your understanding of the print() command to do all this, and if you've read Chapters 9 and 10 (on Scratch), some of the ideas should be familiar to you.

214 PART 4 Programming the Raspberry Pi

# Creating and running your first Python program

The problem with entering instructions in the shell is that you have to enter them each time you use them. The commands are carried out straightaway, too, which limits the sophistication of the kinds of things you can do. You can solve these problems by creating a program, a set of repeatable instructions that you can save as a file and use again.

To create a program, you use the editor, which is the box above the shell that says <untitled> on its tab.

When you enter commands in the editor, they're not carried out straightaway. The editor acts like a simple text editor; it enables you to enter your list of commands (or program) and gives you control over when commands are carried out.

Enter the following commands in the editor, using Enter to start a new line:

```python
# simple times table program
print("This program calculates times tables")
print("It is from Raspberry Pi For Dummies")
```

The window should now look like Figure 11-2. The two print() commands should look familiar to you, though the first line is new. In Python, after a hash mark (#) on the same line is ignored by the computer. The hash mark indicates a comment, used to add notes to programs so that you can understand them.

Before you can run your program, you must save it. If you've made changes since the last time it was saved, your program will be automatically saved for you. It overwrites the previous version of the program. On the File menu is an option to save a copy of the program or to save it a different filename (Save As), which can be useful if there is a chance you might want to revert to an earlier version.

To save your program, click the File menu at the top of the Thonny window and choose Save. You can also use the icons on the menu bar: the paper file opening a new file, and the arrow pointing to the filing cabinet representing saving.

The term used for starting a program is running it, so you click the Run menu and then Run Script. Alternatively, the keyboard shortcut to run the program is F5, or you can click the button in the menu bar that looks like a triangular "play" icon. When you run the program, you see those lines of text printed on the screen.

![](img/df9a01bf057d58c2401b5edabd6e8829_229_0.png)

Figure 11-2: Using the editor.

Congratulations! You've just written your first Python program!

![](img/df9a01bf057d58c2401b5edabd6e8829_229_1.png)

# Using variables

The next step in the program is to ask the user which multiplication table to generate. You store this number in a variable. A variable is a way of storing a number or piece of text so that you can refer to it later. (We talk more about variables in Chapter 10, where it plays a role in Scratch discussion.)

For example, you might have a variable that stores your bank balance. It might go up (ka-ching!) or it might go down (sadly, more often), but you can always refer to it as your bank balance. Variables are one of the basic building blocks of programming, and not just in Python.
