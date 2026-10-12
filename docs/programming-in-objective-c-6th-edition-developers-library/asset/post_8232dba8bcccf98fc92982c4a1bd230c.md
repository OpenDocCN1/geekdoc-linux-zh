
The plus sign—or the increment operator—is used to add 1 to its operand. Because addition by 1 is such a common operation in programs, a special operator was created solely for this purpose. Therefore, the expression `++n` is equivalent to the expression `n + 1`. Although it might appear that `n + 1` is more readable, you will soon become familiar with the function of this operator and will even learn to appreciate its succinctness.

Of course, no programming language that offered an increment operator to add 1 would be complete without a corresponding operator to subtract 1. The name of this operator is the decrement operator, and it is symbolized by the double minus sign. So, an expression in C that reads

```c
b - 1
```

can be equivalently expressed using the decrement operator as

```c
--b
```

Some programmers prefer to put the `++` or `--` after the variable name, as in `n++` or `b--`. This is a matter of personal preference for the example shown in the `if` statement. However, as you’ll learn in Chapter 10, “Pointers,” the pre- or post-nature of the operator does come into play when used in more complex expressions.

## Aligning Output

One slightly disturbing thing you might have noticed in Program 4.3’s output is the fact that the 10th triangular number does not quite line up under the previous triangular numbers. This is because the number 10 takes up two print positions, whereas the previous values of n, 1 through 9, took up only one print position. Therefore, the value 55 is effectively “pushed over” one extra position in the display. This minor annoyance can be corrected if you substitute the following `printf` statement in place of the corresponding statement from Program 4.3.

```c
printf("%3d %4d\n", n, t);
```

To verify that this change does the trick, here is the output from the modified program (we’ll call it Program 4.3A).

### Program 4.3A Output

```
T  n
1  1
2  3
3  6
4  10
5  15
6  21
7  28
8  36
9  45
10 55
```

The primary change made to the `printf` statement was the inclusion of a field width specification. The characters `%3d` tell the `printf` routine that not only do you want to display the value of an integer at that particular point, but you also want the size of the integer to be displayed to take up three columns in the display. Any integer that would normally take up less than three columns (that is, the integers 0 through 99) are displayed with a *leading space*. This is known as *right justification*.

Thus, by using a field width specification, you guarantee that at least the specified number of columns are used for displaying the value of n and, therefore, you ensure that the values of t are lined up.

If the value that is to be displayed requires more columns than are specified by the field width, `printf` simply ignores the field width specification and uses as many columns as are necessary to display the value.

Field width specifications can also be used for displaying values other than integers. You will see some examples of this in programs that are coming up shortly.

## Program Input

**Program 4.2** calculates the 200th triangular number—and nothing more. If you want to calculate the 50th or the 100th triangular number instead, you have to go back and change the program so that the `for` loop is executed the correct number of times. You also have to change the `printf` statement to display the correct message.

An easier solution might be if you could somehow have the program ask which triangular number you want to calculate. Then, after you provide your answer, the program could calculate the desired triangular number for you. Such a solution can be effected in C by using a routine called `scanf`. The `scanf` routine is very similar in concept to the `printf` routine. Whereas the `printf` routine is used to display values at the terminal, the `scanf` routine enables you to type values *into* the program. **Program 4.4** asks the user which triangular number should be calculated, proceeds to calculate that number, and then displays the results.

## Program 4.4 Asking the User for Input

Click here to view code image

```c
#include <stdio.h>

int main(void) {
    int c, t = 0, n;

    printf("Which triangular number do you want me to compute?\n");
    scanf("%d", &n);
    for (c = 1; c <= n; c++) {
        t += c;
        printf("... %d\n", t);
    }
    return 0;
}
```

In **Program 4.4** output, the number typed in by the user (100) is set in bold type to distinguish it from the output displayed by the program.

## Program 4.4 Output

According to the output, the number 100 was typed in by the user. The program then proceeded to calculate the 100th triangular number and displayed the result of 5050 at the terminal. The user could have instead typed in the number 10, or 30, if he desired to calculate those particular triangular numbers.

The first `printf` statement in Program 4.4 is used to prompt the user to type in a number. Of course, it is always nice to remind the user what it is you want entered. After the message is printed, the `scanf` routine is called. The first argument to `scanf` is the format string and is very similar to the format string used by `printf`. In this case, the format string doesn’t tell the system what types of values are to be displayed but rather what types of values are to be read in from the terminal. Like `printf`, the `%` characters are used to specify an integer value.

The second argument to the `scanf` routine specifies where the value that is typed in by the user is to be stored. The `&` character before the variable n is necessary in this case. Don’t worry about its function here, though. Chapter 10 discusses this character, which is actually an operator, in great detail. Always remember to put the leading `&` in front of the variable name in the `scanf` function call. If you forget, it causes unpredictable results and might cause your program to terminate abnormally.

Given the preceding discussion, you can now see that the `scanf` call from Program 4.4 specifies that an integer value is to be read from the terminal and stored in the variable n. This value represents the particular triangular number that the user wants to calculate.

After this number has been typed in (and the “Return” or “Enter” key on the keyboard pressed to signal that typing of the number is completed), the program then proceeds to calculate the requested triangular number. This is done in the same way as in Program 4.2—the only difference being that instead of using 200 as the limit, n is used.

> **Note**
> Pressing the Enter key on a keyboard with a numeric keypad may not cause the number you enter to be sent to the program. Use the Return key on your keyboard instead.

After the desired triangular number has been calculated, the results are displayed, and execution of the program is then complete.

## Nested for Loops

Program 4.4 gives the user the flexibility to have the program calculate any triangular number that is desired. However, if the user has a list of five triangular numbers to be calculated, she can simply execute the program five times, each time typing in the next triangular number from the list to be calculated.

Another way to accomplish this same goal, and a far more interesting method as far as learning about C is concerned, is to have the program handle the situation. This can best be accomplished by inserting a loop in the program to simply repeat the entire series of calculations five times. You know by now that the `for` statement can be used to set up such a loop. Program 4.5 and its associated output illustrate this technique.

### Program 4.5 Using Nested for Loops

Click here to view code image

### Program 4.5 Output

Click here to view code image

The program consists of two levels of `for` statements. The outermost `for` statement

```c
for (c = 1; c <= 5; c++)
```

specifies that the program loop is to be executed precisely five times. This can be seen because the value of c is initially set to 1 and is incremented by 1 until it is no longer less than or equal to 5 (in other words, until it reaches 6).

Unlike the previous program examples, the variable c is not used anywhere else within the program. Its function is solely as a loop counter in the `for` statement. Nevertheless, because it is a variable, it must be declared in the program.

The program loop actually consists of all the remaining program statements, as indicated by the braces. It might be easier for you to comprehend the way this program operates if you conceptualize it as follows:
