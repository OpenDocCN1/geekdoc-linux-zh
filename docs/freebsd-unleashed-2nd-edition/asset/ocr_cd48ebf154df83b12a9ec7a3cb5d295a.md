program line by line, we'll just cover the concepts that are new and/or important to the operation of the program:

+   Line 6—This line assigns a reasonably accurate value of pi to a variable called pi. I point this out because it shows good programming practice. We could just as easily have typed the number 3.14159265 each time we needed to use pi in the program. But assigning the number to a variable serves two primary purposes. First, it simply makes the program more readable. Second, it makes the program much easier to maintain. If we later decided that we needed more precision for the value of pi, we would only have to change one number where we assign the value to the variable pi. If we had used the actual number each time in the program when we needed it, we would have to find and change each occurrence of pi when we decided we need more precision.

+   Line 16—As shown earlier, the read command gathers data from STDIN. In this case, we gather the value typed by the user and store it in the variable radius.

+   Line 20—Line 20 uses command substitution and a pipe to compute the circumference of the circle and store the value in the variable circumference. Because bc does not accept expressions directly on the command line, we need to use the echo command to echo the expression we want computed and then pipe the output of echo to bc.

+   Line 21—This line is similar to line 20. The caret (^) in the expression is the bc exponent operator. In this case, it raises the value stored in $radius by the power of 2 (you may recall from geometry that the area of a circle is obtained by squaring the radius and then multiplying by pi). We do not need to use parentheses to change the order of operation because, as you may recall from algebra, exponents have higher precedence than multiplication. Therefore, we can be assured that the exponent will be evaluated before the multiplication is done.

+   Lines 25 and 26—These lines display the results to the user. I used printf here because it gives me a nicer layout than echo. The use of the hardware tabs with \t causes the numbers to line up in a nice column.

This is only a very simple use of bc. bc is quite powerful and can do much more than the examples you've seen here. See the man page for bc if you are interested in learning more about its capabilities, both inside shell scripts and in standalone programs.

# # Loops

Sometimes you might want an operation to repeat until a certain condition becomes true (or until a certain condition is no longer true). This is where looping statements come into play. The Bourne shell supports three different looping constructs for these situations. These are the while loop, the until loop, and the for loop. We will look at each one separately.