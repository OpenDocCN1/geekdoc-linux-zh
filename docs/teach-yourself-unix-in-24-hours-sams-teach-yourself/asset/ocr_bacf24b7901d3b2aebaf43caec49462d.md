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

![](bbox=[0.065, 0.883, 0.131, 0.966])