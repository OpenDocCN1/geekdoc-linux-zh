
# Simple Math with UNIX

Having both an internal clock and an internal calendar, UNIX seems to have much of what you need in an office. One piece that's missing now, however, is a simple desktop calculator. UNIX offers two different types of calculator, although neither can be called simple.

Mathematicians talk about infix and postfix notation as two different ways to write an expression, the former having the operation embedded in the operators, and the latter having all the operators listed, followed by the operation required. Table 2.1 lists some examples of a mathematical expression in both formats.

Table 2.1. Comparing infix and postfix notation.

| Infix | Postfix |
| --- | --- |
| 75*0.85 | 75 0.85 * |
| (37*1.334)+44 | 37 1.334 * 44 + |
| cos(3)/4 | 3.45 cos 4 / |

You're probably familiar with the infix notation, which is the form used in math textbooks throughout the world. Lists of calculators can work this way, too; you'd press the keys 1 + 1 = to find out 1 plus 1 equals 2.

Some calculators offer the postfix alternative, also known as (reverse) Polish notation, invented by Polish mathematician and logician Jan Kwiatkowski. Notably, for many years Hewlett-Packard has been making calculators that work with RPN notation. On an HP calculator, you'd press the keys Enter = to find out that 1 plus 1 equals 2.

Notice that, although parentheses were required in the second equation in the table when using infix notation, parentheses weren't necessary to force a specific order of evaluation with postfix. Remember that in math you always work from the inside of the parentheses outward, so (3 * 4) + 8 is solved by multiplying 3 by 4, then adding 8, and that process is exactly what RPN mimics.

UNIX offers two calculator programs, one with infix notation and one with postfix notation.

# Task 2.9: Using the bc Infix Calculator

The first calculator to learn is bc, the UNIX infix-notation calculator.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_49_0.png)

# Getting onto the System and Using the Command Line

1. To use the infix calculator, enter the following command:

```
% bc
```
Nothing happens—prompt, nothing. The reason is that bc, like its RPN cousin, waits for you to enter commands. The quit command lets you leave the program. You can see how it works by seeing how I solve the first and second mathematical equations of Table 2.1:
```
% bc
75 * 0.85
63.75
(37*1.334)+44
93.358
quit
```

2. Unfortunately, bc is, in many ways, a typical UNIX command. Consider what happens when I enter help, hoping for some clue on how to use the bc program:

```
% bc
help
syntax error on line 1, type
```

3. This is not very helpful. If you get stuck in a command, there are two sure ways to escape. Control-a (holding down the Control—also called Ctrl—key on your keyboard and simultaneously pressing the a key) indicates that you have no further input, which often causes programs to quit. If that fails, Control-e kills the program, that forces it to quit immediately.
The bc command has a number of powerful and useful options, as shown in Table 2.2.

Table 2.2. Helpful bc commands.

| Notation | Description of Function |
|---|---|
| sqrt(n) | Square root of n |
| % | Remainder |
| ^ | To the power of (3^5 is 3 to the power of 5) |
| s(n) | Sine(n) |
| c(n) | Cosine(n) |
| e(n) | Exponential(n) |
| l(n) | Log(n) |

4. If you wanted to calculate the sine of 4.5243 to the third power, you could do it with bc. You need to be sure, however, that the system knows you're working with higher math functions by specifying the command -l math (or, in some cases just -l):

```
% bc -l
s ( 4.5243 ^ 3 )
-.99770433540886100879
quit
```

If you try on your calculator, you probably won't get a result quite as precise as this. The bc and dc commands both work with extended precision, allowing for highly accurate results.

# Task 2.10: Using the dc Postfix Calculator

By contrast, the dc command works with the postfix notation, and each number operation must be on its own line. Further, the result of an operation isn't automatically shown; you have to enter p to see the most recently calculated result.

1. To use dc for the calculations shown previously, enter the following characters shown in bold. The result follows each completed entry.

```
% dc
75
0.85
-
p
63.75
37
1.334
-
44
+
p
83.358
quit
```

2. The set of commands available in dc are different because dc addresses a different set of mathematical equations. The dc command is particularly useful if you need to work in a non-decimal base. (For example, some older computer systems worked in octal, a base-8 numbering system. The number 210 in octal, therefore, represents 2 * 8 * 8 + 1 * 8 + 0, or 136 in decimal.) Table 2.3 summarizes some of the most useful commands available in dc.

Table 2.3. Helpful commands in dc.

| Notation | Description of Function |
|---|---|
| v | Square root |
| i | Set radix (numeric base) for input |
| o | Set radix for output |
| p | Print top of stack |
| f | All values in the stack are printed |

3. For example, I used dc to verify that 210 (octal) is indeed equal to 136 (decimal):

```
% dc
8
i
210
p
136
```

# Summary

This hour focused on giving you the skills required to log in to UNIX, figure out who you are and what groups you're in, change your password, and log out again. You also learned how to list the other users of the system, find out what UNIX commands they're using, check the date and time, and even show a calendar view of any month or year. Finally, you learned the power of two similar utilities, bc and dc, the two UNIX calculators.

# Workshop

The Workshop summarizes the key terms you learned and poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

- **account name**: This is the official one-word by which the UNIX system connects you: is taylor. See also **account** in Hour 1.)
- **domain name**: UNIX systems on the Internet, or any other network, are assigned a domain within which they exist. This is typically the company (for example, sun.com for Sun Microsystems) or institution (for example, isu.edu for Louisiana State University). The domain name is always the first host address, except the host name.
- **flags**: Arguments given to a UNIX command that are intended to alter its behavior are called flags. They're always preceded by a single dash. For example, the command line -i /tmp has -i as the command itself, -i as the flag to the command, and /tmp as the argument.
- **heuristic**: A set of well-defined steps or a procedure for accomplishing a specific task.
- **host name**: UNIX computers have all unique names assigned by the local administration team. The computers you use are limbo, well, netcom, and mentor, for example. Enter hostname to see what your system is called.
- **login**: A synonym for account name, this can also refer to the actual process of connecting to the UNIX system and entering your account name and password to your account.
- **user ID**: A synonym for account name.
