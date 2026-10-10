
expr is not limited to comparing numbers. It can also compare strings. For example, `expr "The quick brown fox jumped over the lazy dog" = "The quick brown fox jumped over the lazy dg"` will evaluate to 0 (the expression is false unless the strings are exactly equal).

Although expr is great for simple shell scripting, as mentioned previously, its capabilities are rather limited. If you need to do floating-point math, work with complex expressions that change the order of operations, and so on, you can use a command called bc. bc is a programming language in itself for working with math. It is possible to embed expressions into your shell program and feed them to bc. The program in Listing 12.2 uses bc to compute both the circumference and the area of a circle. Note that the argument to bc is -l, the lowercase letter L. It defines the standard math library for bc.

### LISTING 12.2 Using bc to Compute the Circumference and Area of a Circle

```bash
#!/bin/sh

# The Following program computes both the circumference and the area
# of a circle.

pi="3.14159265"          # Assign the value of pi to a variable.

# Tell the user what the program does and ask them for the radius of
# the circle.

echo
echo "This program computes both the circumference and the area of"
echo "a circle."
echo
echo -n "Please enter the radius of the circle: "
read radius

# Now we will use bc to compute the answers and store them in variables.

circumference=`echo "$radius*3pi" | bc -l`
area=`echo "$radius*2*3pi" | bc -l`

# Last, we display the answers to the user and exit.

printf "\n\nThe circumference is:\t$circumference\n"
printf "The area is:\t\t$area\n"
```

Most of the concepts used in this program have already been explained in the sections “Variables” and “Interacting with the User.” Therefore, rather than go through the program line by line, we'll just cover the concepts that are new and/or important to the operation of the program:

- Line 6—This line assigns a reasonably accurate value of pi to a variable called pi. I point this out because it shows good programming practice. We could just as easily have typed the number 3.14159265 each time we needed to use pi in the program. But assigning the number to a variable serves two primary purposes. First, it simply makes the program more readable. Second, it makes the program much easier to maintain. If we later decided that we needed more precision for the value of pi, we would only have to change one number where we assign the value to the variable pi. If we had used the actual number each time in the program when we needed it, we would have to find and change each occurrence of pi when we decided we need more precision.
- Line 16—As shown earlier, the read command gathers data from STDIN. In this case, we gather the value typed by the user and store it in the variable radius.
- Line 20—Line 20 uses command substitution and a pipe to compute the circumference of the circle and store the value in the variable circumference. Because bc does not accept expressions directly on the command line, we need to use the echo command to echo the expression we want computed and then pipe the output of echo to bc.
- Line 21—This line is similar to line 20. The caret (^) in the expression is the bc exponent operator. In this case, it raises the value stored in $radius by the power of 2 (you may recall from geometry that the area of a circle is obtained by squaring the radius and then multiplying by pi). We do not need to use parentheses to change the order of operation because, as you may recall from algebra, exponents have higher precedence than multiplication. Therefore, we can be assured that the exponent will be evaluated before the multiplication is done.
- Lines 25 and 26—These lines display the results to the user. I used printf here because it gives me a nicer layout than echo. The use of the hardware tabs with \t causes the numbers to line up in a nice column.

This is only a very simple use of bc. bc is quite powerful and can do much more than the examples you've seen here. See the man page for bc if you are interested in learning more about its capabilities, both inside shell scripts and in standalone programs.

## Loops

Sometimes you might want an operation to repeat until a certain condition becomes true (or until a certain condition is no longer true). This is where looping statements come into play. The Bourne shell supports three different looping constructs for these situations. These are the while loop, the until loop, and the for loop. We will look at each one separately.

### The while Loop

The while loop repeats the statements inside the loop as long as the condition that is being tested is true. Depending on your point of view, it could also be said that the while loop repeats the statements inside the loop until the condition that is being tested becomes false. If the condition is already false the first time it is evaluated, the loop will never be executed. For example, the following program uses a while loop to count to 20 and display the numbers on the screen:

```bash
#!/bin/sh
# Count from 1 to 20
i=1
while [ $i -le 20 ]
do
    echo $i
    i=`expr $i + 1`
done
```

This program introduces a few new concepts:

- Line 3—This line simply assigns the variable i the initial value of 1. i is a variable that is universally understood to be a loop-control counter; as with its usage in summation in mathematics, i typically stands for increment. This is one case where you can get away with not using a descriptive variable name.
- Line 4—The while command contains the condition to test enclosed in brackets. The bracket is actually a shorthand notation for a command called test. You will use this command a lot in shell scripting.

Unfortunately, the test command uses a somewhat strange syntax. -le in this example means "is less than or equal to." So this means the loop will repeat as long as the variable i is less than or equal to 20. For mathematical evaluations, Table 12.2 shows all the operators that this command supports.

| Option | Action |
| :--- | :--- |
| -eq | True, if operand one is equal to operand two |
| -ne | True, if operand one is not equal to operand two |
| -gt | True, if operand one is greater than operand two |
| -ge | True, if operand one is greater than or equal to operand two |
| -lt | True, if operand one is less than operand two |
| -le | True, if operand one is less than or equal to operand two |

- Line 5—The do statement indicates that everything after this should be done for each iteration of the loop. All statements located between the do statement and the done statement are considered part of the loop.
- Line 6—Prints the current value of the variable i.
- Line 7—Uses command substitution with the expr command to increment the value of i by 1 and then assign the new value back into i.
- Line 8—Indicates the end of the loop. At this point, the program jumps back up to the while statement, and the test condition is evaluated again. If i is still less than or equal to 20, the statements inside the loop are repeated again. If i is greater than 20, the loop exits and control passes to the first statement after the done statement (in this case, line 9, which simply exits the program with a 0, or successful status).

Notice that the statements inside the loop are indented. This makes it easy to pick out the statements that are part of the loop when quickly scanning the program’s source code. The shell ignores the indentation, so you could have written this program without using it. I recommend you always indent loops, though, to make them easier to find when quickly scanning program source code.

> **TIP**
> The space between the bracket ([ ) and the condition to be tested is mandatory, as is the space immediately before the final bracket ( ]). Failing to include either one will cause an error. For example,
>
> ```bash
> [ $varA -gt 5 ]
> ```
>
> will work, but
>
> ```bash
> [$varA -gt 5]
> ```
>
> will cause an error.

### The until Loop

The until loop is the opposite of the while loop. It performs the operations inside the loop as long as the condition being tested is not true. When the condition being tested becomes true, the loop exits. If the condition is already true the first time it is evaluated, the loop will never be executed.

The while loop and the until loop are very similar. Usually, you can use either one in a program and achieve the same results simply by modifying the condition that is tested for. For example, the counting program that used the while loop can be rewritten to use an until loop by making only two changes in line 4:

- `until [ $i -gt 20 ]`
