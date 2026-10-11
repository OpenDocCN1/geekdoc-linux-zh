The following steps walk you through each line of this program:

+   1. The first line (#! /bin/bash) tells Linux to run the bash shell.
+   2. Clear wipes the screen clean.
+   3. The program uses the function keyword display to define a function.
+   4. Between the French braces, you tell Linux to display two lines of text on-screen.
+   5. Following the closing French brace, you call the function by using the name of the function (display), and Linux then displays the text on-screen.

# Passing Arguments to a Function

Passing arguments sounds like avoiding a heated discussion with the guy who cut you off on the highway. But the term passing arguments really refers to a way to give changing information to a function.

Suppose, for example, that you write a function that validates an ID and password. The function contains the commands and information necessary to perform the validation — all except for two pieces. The missing pieces are the ID and the password, which are different each time that the program calls the function.

The ID and password can pass as arguments to the function if you call the function in your program. Linux assigns the ID and password to variables whenever you call the function. These variables are $1 and $2. Each number refers to the next argument passing to the program. You can't substitute the number in these variables with another name such as var1 because Linux expects to see numbers.

So you can use the variable in place of the information in the function definition. Say that the ID is the first argument passing to the function and the password is the second argument. You can, therefore, use $1 in the function definition whenever you want to refer to the ID and use $2 to refer to the password.

The program looks as follows:

```
#! /bin/bash
clear
function verify
{
    if [ $1 -eq "Bob" ] && [ $2 -eq "555" ]

```