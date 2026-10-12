
The portion of the loop referred to in the preceding as Calculate the requested triangular number actually consists of setting the value of the variable t to 0 plus the `for` loop that calculates the triangular number. Thus, you see that you have a `for` statement that is actually contained within another `for` statement. This is perfectly valid in C, and nesting can continue even further to any desired level.

The proper use of indentation becomes even more critical when dealing with more sophisticated program constructs, such as nested `for` statements. You can easily determine which statements are contained within each `for` statement. (To see how unreadable a program can be if correct attention isn’t paid to formatting, see exercise 5 at the end of this chapter.)

## for Loop Variants

Some syntactic variations are permitted in forming the `for` loop. When writing a `for` loop, you might discover that you have more than one variable that you want to initialize before the loop begins or more than one expression that you want to evaluate each time through the loop.

### Multiple Expressions

You can include multiple expressions in any of the fields of the `for` loop, provided that you separate such expressions by commas. For example, in the `for` statement that begins

Click here to view code_image

the value of i is set to 0 and the value of j is set to 0 before the loop begins. The two expressions i = and j are separated from each other by a comma, and both expressions are considered part of the init_expression field of the loop. As another example, the `for` loop that starts

Click here to view code_image

sets up two index variables, i and j; the former initialized to 0 and the latter to 1 before the loop begins. Each time after the body of the loop is executed, the value of i is incremented by 1, whereas the value of j is decremented by 10.

### Omitting Fields

Just as the need might arise to include more than one expression in a particular field of the `for` statement, the need might arise to omit one or more fields from the statement. This can be done simply by omitting the desired field and marking its place with a semicolon. The most common application for the omission of a field in the `for` statement occurs when there is no initial expression that needs to be evaluated. The init_expression field can simply be "left blank" in such a case, as long as the semicolon is still included:

Click here to view code_image

This statement might be used if j were already set to some initial value before the loop was entered. A `for` loop that has its looping_condition field omitted effectively sets up an infinite loop; that is, a loop that is theoretically executed forever. Such a loop can be used provided there is some other means used to exit from the loop (such as executing a `return`, `break`, or `goto` statement as discussed elsewhere in this book).

### Declaring Variables

You can also declare variables as part of your initial expression inside a `for` loop. This is done using the normal ways you've defined variables in the past. For example, the following can be used to set up a `for` loop with an integer variable c both defined and initialized to the value 1:

Click here to view code_image

The variable c is only known throughout the execution of the `for` loop and cannot be accessed outside the loop. As another example, the following `for` loop

Click here to view code_image

defines two integer variables and sets their values accordingly.

## The while Statement

The `while` statement further extends the C language's repertoire of looping capabilities. The syntax of this frequently used construct is as follows:

Click here to view code_image

The expression specified inside the parentheses is evaluated. If the result of the evaluation is TRUE, the program statement that immediately follows is executed. After execution of this statement (or statements if enclosed in braces), the expression is once again evaluated. If the result of the evaluation is TRUE, the program statement is once again executed. This process continues until the expression finally evaluates as FALSE, at which point the loop is terminated. Execution of the program then continues with the statement that follows the program statement.

As an example of its use, Program 4.6 sets up a `while` loop, which merely counts from 1 to 5.

Click here to view code_image

The program initially sets the value of `c` to 1. Execution of the `while` loop then begins. Because the value of `c` is less than or equal to 5, the statement that immediately follows is executed. The braces serve to define both the `print` statement and the statement that increments `c` as the body of the `while` loop. From the output of the program, you can readily observe that this loop is executed precisely 5 times, or until the value of `c` reaches 6.

You might have realized from this program that you could have readily accomplished the same task by using a `for` statement. In fact, a `for` statement can always be translated into an equivalent `while` statement, and vice versa. For example, the general `for` statement

Click here to view code_image

can be equivalently expressed in the form of a `while` statement as

Click here to view code_image

After you become familiar with the use of the `while` statement, you will gain a better feel as to when it seems more logical to use a `while` statement and when to use a `for` statement.

In general, a loop executed a predetermined number of times is a prime candidate for implementation as a `for` statement. Also, if the initial expression, looping expression, and the looping condition all involve the same variable, the `for` statement is probably the right choice.

The next program provides another example of the use of the `while` statement. The program

computes the *greatest common divisor* of two integer values. The greatest common divisor (*gcd*) of two integers is the largest integer value that evenly divides the two integers. For example, the *gcd* of 10 and 15 is 5 because 5 is the largest integer that evenly divides both 10 and 15.

There is a procedure or *algorithm* that can be followed to arrive at the *gcd* of two arbitrary integers. This algorithm is based on a procedure originally developed by Euclid around 300 B.C., and can be stated as follows:

**Problem:**

Find the greatest common divisor of two nonnegative integers *u* and *v*.

**Step 1:**

If *v* equals 0, then you are done and the *gcd* is equal to *u*.

**Step 2:**

Calculate *temp* = *u* % *v*, *u* = *v*, *v* = *temp*, and go back to step 1.

Don’t concern yourself with the details of how the preceding algorithm works—simply take it on faith. Focus more here on developing the program to find the greatest common divisor than on performing an analysis of how the algorithm works.

After the solution to the problem of finding the greatest common divisor has been expressed in terms of an algorithm, it becomes a much simpler task to develop the computer program. An analysis of the steps of the algorithm reveals that step 2 is repetitively executed as long as the value of *v* is not equal to 0. This realization leads to the natural implementation of this algorithm in C with the use of a *while* statement.

*Program 4.7* finds the *gcd* of two nonnegative integer values typed in by the user.

*Program 4.7 Finding the Greatest Common Divisor*

Click here to view code_image
