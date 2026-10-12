Click here to view code image

would do the trick. However, recall that if the preceding statement were used, the decimal portion of the result of the division would be lost. This is because an integer division would be performed because both the numerator and the denominator of the division operation are integers.

Two different solutions are possible for this problem. One is to declare either n or g to be of type f. This then guarantees that the division is carried out without the loss of the decimal places. The only problem with this approach is that the variables n and g are used by the program to store only integer values.

Declaring either of them to be of type f only obscures their use in the program and is generally not a very clean way of doing things.

The other solution, as used by the program, is to actually convert the value of one of the variables to a floating-point value for the purposes of the calculation. The type cast operator (f) is used to convert the value of the variable g to type f for purposes of evaluation of the expression. Because the value of g is cast into a floating-point value before the division takes place, the division is treated as the division of a floating value by an integer. Because one of the operands is now a floating-point value, the division operation is carried out as a floating-point operation. This means, of course, that you obtain those decimal places that you want in the average.

After the average has been calculated, it is displayed at the terminal to two decimal places of accuracy. If a decimal point followed by a number (known collectively as a precision modifier) is placed directly before the format character f (or e) in a p format string, the corresponding value is displayed to the specified number of decimal places, rounded. So in Program 5.2, the precision modifier. is used to cause the value of a to be displayed to two decimal places.

After the program has displayed the number of failing grades, execution of the program is complete.

Note that if the user of the program enters 0 as the number of test grades to be recorded, the program will generate some odd results, like NaN (Not a Number) or something else; it will vary by system however, depending on how your computer deals with division by 0. You may wonder why someone would bother running a program to record test scores if there are no test scores to enter, but this is the type of possible error-checking you can add to your program.

# ## The if-else Construct

If someone asks you whether a particular number is even or odd, you most likely make the determination by examining the last digit of the number. If this digit is either 0, 2, 4, 6, or 8, you readily state that the number is even. Otherwise, you claim that the number is odd.

An easier way for a computer to determine whether a particular number is even or odd is affected not by examining the last digit of the number to see if it is 0, 2, 4, 6, or 8, but by simply determining whether the number is evenly divisible by 2. If it is, the number is even; else it is odd.

You have already seen how the modulus operator % is used to compute the remainder of one integer divided by another. This makes it the perfect operator to use in determining whether an integer is evenly divisible by 2. If the remainder after division by 2 is zero, it is even; else it is odd.

Look at Program 5.3—a program that determines whether an integer value typed in by the user is even or odd and that displays an appropriate message at the terminal.