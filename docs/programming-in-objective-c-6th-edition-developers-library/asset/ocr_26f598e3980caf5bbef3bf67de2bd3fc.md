# ## Working with Variables

Early computer programmers had the onerous task of having to write their programs in the binary language of the machine they were programming. This meant that computer instructions had to be hand-coded into binary numbers by the programmer before they could be entered into the machine. Furthermore, the programmer had to explicitly assign and reference any storage locations inside the computer’s memory by a specific number or memory address.

Today’s programming languages allow you to concentrate more on solving the particular problem at hand than worrying about specific machine codes or memory locations. They enable you to assign symbolic names, known as *variable names*, for storing program computations and results. A variable name can be chosen by you in a meaningful way to reflect the type of value that is to be stored in that variable.

In Chapter 2, “Compiling and Running Your First Program,” you used several variables to store integer values. For example, you used the variable `s` in Program 2.4 to store the result of the addition of the two integers 50 and 25.

The C language allows data types other than just integers to be stored in variables as well, provided the proper declaration for the variable is made *before* it is used in the program. Variables can be used to store floating-point numbers, characters, and even *pointers* to locations inside the computer’s memory.

The rules for forming variable names are quite simple: They must begin with a letter or underscore (_) and can be followed by any combination of letters (upper- or lowercase), underscores, or the digits 0–9. The following is a list of valid variable names.

+   s  
+   p  
+   i  
+   j  
+   n  
+   -

On the other hand, the following variable names are not valid for the stated reasons:

| Column 1 | Column 2 |
| :--- | :--- |
| `sum$value` | $ is not a valid character. |
| `piece flag` | Embedded spaces are not permitted. |
| `3Spencer` | Variable names cannot start with a number. |
| `int` | int is a reserved word. |

`i` cannot be used as a variable name because its use has a special meaning to the C compiler. This use is known as a reserved name or reserved word. In general, any name that has special significance to the C compiler cannot be used as a variable name. Appendix A provides a complete list of such reserved names.

You should always remember that upper- and lowercase letters are distinct in C. Therefore, the variable names `s`, `S`, `,`, and `S` each refer to a different variable.

Your variable names can be as long as you want, although only the first 63 characters might be significant, and in some special cases (as described in Appendix A), only the first 31 characters might be significant. It’s typically not practical to use variable names that are too long—just because of all the extra typing you have to do. For example, although the following line is valid

Click here to view code image