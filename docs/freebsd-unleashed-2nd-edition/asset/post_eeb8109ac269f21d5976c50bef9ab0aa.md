
## Listing 12.3 Breaking Out of a Loop

```bash
#!/bin/sh
# The following program loops indefinitely.
while true
do
    echo "This line will print forever... But..."
    break
done
echo
echo "The break statement in the loop causes the loop"
echo "to terminate immediately and go the first statement"
echo "after the loop."
```

Here's the output of this program:

```text
This line will print forever... But...

The break statement in the loop causes the loop
to terminate immediately and go to the first statement
after the loop.
bash$
```

In a more complex implementation, you could have a loop that waits for some kind of input to be entered from the user's console or from the network; the loop could test continuously for the existence of a file or the value of a variable, and if that condition becomes true, a break could end the loop. Usually it is considered more elegant to write loops whose exit conditions are constructed to react properly on the right kind of input and to avoid a break when possible. In sufficiently complex programs, however, a break can be just what you need to get out of a jam.

## The continue Statement

The continue statement causes the loop to immediately jump back to the top and re-evaluate the test condition. Any remaining statements in the loop are not executed. Listing 12.4 is another example that uses the "endless loop" program with a slight modification.

## Listing 12.4 Restarting a Loop Before It Has Ended

```bash
#!/bin/sh
# The following program loops indefinitely.
while true
do
    echo "This line will print forever."
    continue
    echo "But this line will never print even though it is inside"
    echo "the loop because the preceding continue statement"
    echo "causes the loop to jump back to the top and re-evaluate"
    echo "the test."
done
echo "This line will never print since the program will"
echo "never get past the loop."
exit 0 # The program will never exit cleanly since it will
# never get to this point.
```

This program will indefinitely output *"This line will print forever."* The rest of the echo statements inside the loop will never be printed because the continue statement before them causes the loop to immediately jump back to the top and re-evaluate the test condition.

## Conditional Statements

Conditional statements execute if and only if a certain condition or conditions are true. They generally come in three forms: *if* statements, *case* statements, and logical AND/OR statements. These are very fundamental and useful constructs in programming; flow control depends on them (executing certain blocks of code depending on the outcome of a condition), as does the ability of a program to behave correctly upon receiving certain expected arguments (which would be handled by case statements).

### if Statements

*if* statements test numerical expressions. If the condition is true, the statements inside the *if* block are executed. If the condition is false, one of two things can happen:

-   Nothing. The statements inside the *if* block are not executed, and the program continues as if they were not even there.
-   If an *else* statement is included inside the *if* block, the statements will be executed if the condition is false. In other words, this can be used to write "Do this if the condition is true, or do this if the condition is false, but do not do both" type of controls in programs.

For example, the following program uses an *if* statement to test the number of command-line arguments given to the program. If the command-line arguments are one or more, the program performs the operations inside the *then* block. If no command-line arguments were supplied, the program exits without doing anything:

```bash
#!/bin/sh
# ifprog: Demonstrate one way to use if statements.
if [ $# -ge 1 ]
then
    echo "You supplied $# command line arguments."
fi
echo
echo "Program exiting..."
echo
```

And here are two sample runs:

**Run 1:**

```bash
bash$ ./ifprog file1 file2 file3
You supplied 3 command line arguments.

Program exiting...
bash$
```

**Run 2:**

```bash
bash$ ./ifprog

Program exiting...
bash$
```

The `if` statement in line 3 checks to see whether the number of command-line arguments supplied is one or greater (using the magic variable `$#`, which stores the number of command-line arguments). If it is, the statements between `then` and `fi` are executed. ("`fi`" is `if` spelled backward. It marks the end of the `if` block.) If it isn't, the statements inside the `if` block are skipped and the program jumps to the first statement past `fi`, which in this case simply informs the user that the program is exiting.

### Using an else Statement

We could make this program more user friendly by including an `else` statement that tells the user how to properly use the program rather than simply having it exit without doing anything, as it currently does. Listing 12.5 shows the revised example. Note that the operand in line 3 is a number one, not a lowercase L.

## Listing 12.5 A More Friendly Version of the Previous Program

```bash
#!/bin/sh
# ifprog: Demonstrate one way to use if statements.
if [ $# -ge 1 ]
then
    echo "You supplied $# command line arguments."
else
    echo "Usage: $0 file1 file2..."
    echo
    exit 1
fi
echo
echo "Program exiting..."
echo
```

Now, if the number of command-line arguments is less than one, the program will perform the else statements and give the user a usage message (remember that `$0` contains the name of the command that was invoked). Notice also line 9, which tells the program to exit immediately and sets the exit status to 1 (which indicates the program terminated with errors). Statements 10–14 will never get executed if the program runs the else statements.

The then part of the if statement is required. The else part is optional. As you have seen, the then part of the if statement performs an action if the expression tested by if evaluates to true. Sometimes, however, you might want to perform an action only if the expression evaluates to false and to do nothing if the expression evaluates to true. You can do this by using a colon as a placeholder. Here’s an example:

```bash
if [ $myvar -gt 5 ]
then
    # Do nothing and continue after end of if block
else
    # Statements to execute if condition is false go here.
fi
```

## Using an elif Statement

Sometimes you might want to test for two or more different conditions and perform a different action, depending on the results. The elif statement accomplishes this.

elif is an abbreviation for “else if.” When elif statements are used, the program will go through the if statement. If it evaluates to true, its actions will be performed and then program flow will jump to the first statement after the end of the if block (where fi is located). If it evaluates to false, the first elif is checked. If it is true, the statements inside it are executed and flow jumps to the end of the if block. If it is false, the second elif statement is evaluated, and so on. Basically, evaluations are done until the program reaches an expression that evaluates to true. If none of the conditions evaluate to true, either nothing happens or the statements inside `else`, if present, are executed.

Listing 12.6 uses much of what you have learned up to this point, including `if`, `elif`, and `else` to play a simple number-guessing game. Note that line 10 uses `jot`, a little command-line random-number-generating tool. The arguments in this case to its `-r` option are the number of results to return (1), the lower bound (1), and the upper bound (`$up_limit`).

## Listing 12.6 A Simple Number-Guessing Game

```bash
#!/bin/sh
# Number guessing game
clear
guess_count=1 # Initialize the guess counter to 1
echo
echo "Number guessing game written in bourne shell script."
echo
echo -n "Enter upper limit for guess: "
read up_limit
rnd_number=`jot -r 1 1 $up_limit` # Get a random number
echo
echo "I've thought of a number between 1 and $up_limit."
echo
echo -n "Please guess a number between 1 and $up_limit: "
read guess
# Check the guess against the random number.
while true
do
    if [ $guess -gt $rnd_number ]
    then
        echo
        echo "Your guess was too high. Please try again."
        guess_count=`expr $guess_count + 1`
        echo -n "Please guess a number between 1 and $up_limit: "
        read guess
    elif [ $guess -lt $rnd_number ]
    then
        echo
        echo "Your guess was too low. Please try again."
        guess_count=`expr $guess_count + 1`
        echo -n "Please guess a number between 1 and $up_limit: "
        read guess
    else
        break
    fi
```
