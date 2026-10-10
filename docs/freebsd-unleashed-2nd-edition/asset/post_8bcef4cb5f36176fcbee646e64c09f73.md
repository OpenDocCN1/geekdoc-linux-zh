
## Listing 12.6 Continued

```bash
36. done
37. # We get to this point when the player guesses the correct number.
38. echo
39. echo "Correct!"
40. echo
41. echo "You guessed the number in $guess_count guesses."
42. echo
```

Here's a sample run:

```text
Number guessing game written in bourne shell script.

Enter upper limit for guess: 10
I've thought of a number between 1 and 10.

Please guess a number between 1 and 10: 5

Your guess was too low. Please try again.
Please guess a number between 1 and 10: 8

Your guess was too high. Please try again.
Please guess a number between 1 and 10: 7

Correct!

You guessed the number in 3 guesses.
```

Most of the concepts in this program should be familiar to you by now:

- Line 3 simply clears the screen.
- Line 4 initializes a variable guess_count to store the number of guesses the player has made and sets the initial value to 1.
- Lines 23 and 30 increment the value of the variable guess_count by 1 for each incorrect guess made.
- Line 10 uses command substitution with the jot command to assign a single random number between 1 and whatever the player entered as the upper limit for the guess to the variable rand_number.
- Line 17 starts an infinite loop.
- Line 19 checks to see whether the number the player entered is greater than the random number that the program picked. If it is, the player is informed of that, the `guess_count` variable is incremented by 1, and the player is asked to pick another number. After the player has picked another number, it is stored in the variable guess and the `while` loop starts over.
- If the number the player guessed is not greater than the random number the computer picked, the `elif` statement is evaluated to check whether the number is lower. If it is, the player is informed of this, the `guess_count` variable is incremented by 1, and the player is asked to try again. After the player has entered a new number, the `while` loop starts over.
- Finally, if neither condition is true, the `else` statement is executed (we did not need to perform a test here because if the number is neither higher nor lower, it must be equal). The `else` statement here simply breaks out of the infinite loop, and program flow passes to the first statement after the `done` statement.
- The statements at the end of the program simply tell the user he guessed the correct number and then inform the user how many guesses it took him to get the correct answer by displaying the value of `guess_count`.

Like loop tests, `if` tests also support the logical AND (`&&`) and logical OR (`||`) tests to perform conditions if and only if both conditions are true, or if one of any number of conditions are true.

### case Statements

If you need to test the same variable for multiple conditions, there is a more efficient and cleaner way of doing it than with `if` statements. The `case` statement takes a variable as an argument and then uses statement blocks to determine what to do, depending on the value of the variable. Listing 12.7 uses `case` statements to create a random quote generator.

## Listing 12.7 Using case to Generate Random Quotes

```bash
#!/bin/sh
# Random quote generator.
quote_num=`jot -r 1 15`
case "$quote_num" in
    1)
        echo
        echo "\"Until he extends his circle of compassion to include"
        echo "all living things, man will not himself find peace.\""
        echo "\" -- Albert Schweitzer"
        echo ;
    2)
        echo
        echo "With regard to excellence, it is not enough to know, but"
        echo "we must try to have and use it."
        echo "-- Aristotle"
        echo ;;
    3)
        echo
        echo "Imagination is more important than knowledge. Knowledge"
        echo "is limited. Imagination encircles the whole world."
        echo "-- Albert Einstein"
        echo ;;
    4)
        echo
        echo "It is not the strongest of the species that survive, nor"
        echo "the most intelligent, but the one most responsive to change."
        echo "-- Charles Darwin"
        echo ;;
esac
```

Once again, we use *jot* in line 3 to generate a random number between 1 and 4. The case block begins on line 4. The syntax is *case variable in*, where *variable* is the name of the variable that the tests should be performed on. Line 5 begins the first test. Everything to the left of the parenthesis indicates the condition that case tests for. Like the *if* statement, *case* stops at the first match it comes to, executes the statements that go with that match, and then jumps down to *esac* (which is “*case*” spelled backward). The end of the statements that go along with each condition is marked with a double semicolon. The double semicolon can be on a line by itself, or it can be placed on the same line as the last statement, as is done in the previous example.

The case statement also accepts shell wildcards. Here’s an example:

```bash
case "$myvar" in
    a) #statements to do for a
       ;;
    b) #statements to do for b
       ;;
    *) #statements to do for anything else
       ;;
esac
```

The previous code will check to see whether *$myvar* is equal to *a* or *b*, and perform the appropriate statements if it is. If it is not, the last test is a wildcard that will match anything. So, if *$myvar* is not equal to *a* or *b*, the last group of statements will be performed.

Other wildcards supported by case include ?, which works the same way it does in the shell (as you saw in Chapter 7), and the pipe character (|), which allows case to accept a range of options. For example, Y | y) will accept either Y or y as a match for a test. You can also enclose multiple characters in brackets to match a range of characters. For example, [Yy]|[Ee]|[Ss]) will accept either y or yes as a match in any combination of upper- or lowercase letters.

## CGI Programming

You've probably seen Web sites that have features such as random quotes that display on the page at each load or a random picture that changes each time the page is reloaded. The program presented previously that used case to display the quotes is one way to do this. This is called a CGI program, and it is a way for the Web server to run external programs and then send the output of those programs over the Internet to a browser. Chapter 25, "Configuring a Web Server," covers more of CGI programming.

## Logical AND/OR Conditionals

Using logical AND/OR conditionals are basically a short-hand way of doing if statements in some cases. They use the exit status of the first command to determine whether to run the second command. Here's an example:

```bash
tar cvfz backup.tar.gz documents/2000/ && rm -r documents/2000
```

This command basically says, "If the first operation is successful, perform the second operation. If the first operation is not successful, do not perform the second operation." In other words, "You have to perform A and B. If A cannot be performed, do not perform B." In this case, it will attempt to archive all the files in the directory documents/2000 into a file called backup.tar.gz. If the archive operation is successful (the tar command exits with 0), the operation after && will also be performed, which removes the directory documents/2000. If the archive operation is unsuccessful (the tar command exits with some number other than 0), the operation after && will not be performed (obviously, we do not want to remove the directory if we were unable to successfully archive it).

The || is the OR operator. It basically says, "If you cannot perform A, perform B. But do not perform B if A is successful." Here is an example:

```bash
tar cvfz backup.tar.gz documents/2000/ || echo "Archive operation failed."
```

In this case, if the archive operation is successful (tar exits with 0), the statement after || will not be executed. If, however, the archive operation fails (tar returns an exit status other than 0), the statement after || will be executed, and an error message will be printed to the screen.
