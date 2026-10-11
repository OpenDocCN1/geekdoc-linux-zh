
If the condition of the while loop is always true, the program again executes all the instructions in the loop. Your program doesn’t stop until you or the administrator who’s responsible for your computer stops the program. Again, this situation is the infamous endless loop.

No cool programmer wants to put an endless loop in a program. You can avoid this situation by making sure that at least one instruction in the while loop changes the true or false value of the condition that the while loop uses. The following example shows how to do so:

```
#!/bin/bash
declare raining="1"
while [ "$raining" -eq "1" ]
do
    clear
    echo " "
    echo "Is it raining? "
    echo " "
    echo "1. Yes "
    echo "2. No "
    echo " "
    echo "Enter your selection: "
    read raining
done
echo "It stopped raining."
```

- `#!/bin/bash`: The `bash` tells the program that this part is a bash shell script.
- `declare`: The `declare` tells the computer to create a string variable by the name of `raining` and assign it the value `1`.
- `while`: The `while` tells the program to check whether the value of `$raining` is `1`. If so, the program executes the following instructions.
- `clear`: The `clear` tells the program to clear the screen.
- `echo`: The `echo` stuff displays a menu.
- `read`: The `read` waits for the user to make a selection and then assigns the selection to the `raining` variable.

The program returns to the top of the while loop and checks to see whether the value of `$raining` is `1`. If the value didn’t change, the instructions execute again.

If the value isn’t 1, the instructions don’t execute again. The program jumps to the last instruction in the program and displays it stopped raining. on-screen.

## Part IV: Loops and Loops

![](img/05279073f26be7df99b3c487360dec6a_141_0.png)

### Test your programming knowledge

- 1. How can the program break out of a while loop?
  - a. Use a file hidden in a birthday cake.
  - b. Make the condition false.
  - c. Make the condition true.
  - d. Use explosives.
- 2. How can a while loop run endlessly?
  - a. Your computer goes crazy.
  - b. Your program always changes the condition to false.
  - c. Your program never changes the condition to false.
  - d. The accelerator gets stuck.

Answers: 1) b. See “Avoiding Endless while Loops.” 2) c. See “Avoiding Endless while Loops.”

Of course, the user can enter a character other than 1 or 2. If that happens, the program treats the value as if the user is selecting 2. The value is no longer 1, so the program follows the same instructions as if the rain isn’t falling.

![](img/05279073f26be7df99b3c487360dec6a_141_1.png)

Always indent instructions that you place in a while loop. If you don’t, you usually must spend hours trying to understand what you told the program to do. (Although your program has no trouble reading your code whether you indent it or not.) Always indent lines of instructions so that you group similar instructions together.

## Chapter 11
### The for in Loop

- In This Chapter
  - Using the for in loop
  - Using the for in loop in a program
  - Using wordlists

Say that you want to print the same letter to each of your friends inviting them to the big bash you're throwing because you just won the lottery. You want to personalize these invitations. You could write a program to print the text, but each time the program runs, you find yourself entering the name of your next friend.

Of course, you avoid this problem by using the `for in` loop. The `for in` loop enables you to store all your friends' names in a list, and then your program uses each name in printing the invitation. It’s like having a mail-merge feature built into your own program.

So, whenever you want your programming code to execute a series of instructions as long as a condition is true, use the `while` loop. Your computer keeps executing instructions that you place inside a `while` loop until one of the instructions in your code changes the condition to false.

If you know how many times that you want the instructions to execute, however, use the `for in` loop instead.

Just in case you can't wait, here's what a `for in` loop looks like:

```
For VariableName in wordlist
 do
    instruction
done
```

The `wordlist` is a list of string values that you assign to the variable; I explain this wordlist stuff later in the chapter, so don't worry for now. (Remember that a string is any combination of letters and numbers.) The instruction inside the loop can use the variable.

You can stuff as many instructions as you need inside the loop. Your biggest challenge is your ability to keep track of the programming instructions that you enter. Use your common sense as a guide.

### When to Use a for in Loop

No hard-and-fast rules exist to tell you when to use a **for in** loop. You just need to use your best judgment. (I guess you didn’t need to go to MIT after all.)

The following list describes the times when you can use a **for in** loop:

- You need to do the same thing to more than one string value.
- You want to use a series of string values in a certain sequence.

Say, for example, that you want your program to give your five employees an increase in salary. Aren’t you a nice person? The necessary steps are as follows:

1. Look up the employee’s salary in the payroll file.
2. Calculate the new salary.
3. Save the new salary to the payroll file.

You place the name of each employee in the list that you associate with the **for in** loop. The program then uses the name of each employee in sequence to find the employee’s record, perform the necessary math, and place the employee’s record back into the file.

### How the for in Loop Works

Here’s something to do if you’re ready to show off your new programming talents to your friends. Write a program that greets each one of them personally after you gather them around your computer. You can accomplish this task in either of a couple ways.

You can, for example, type the following code:

```
echo "Hello, Mary."
echo "Hello, Joe."
echo "Hello, Sue."
```

This program simply repeats the same instruction three times. Each time it changes the name to greet another one of your friends.

The following code also displays a **Hello** message to each of your three buddies:

```
let counter = 1
while [ "$counter" -lt 5 ]
do
	if [ "$counter" -eq 1 ]
	then
		echo "Hello, Mary."
	fi
	if [ "$counter" -eq 2 ]
	then
		echo "Hello, Joe."
	fi
	if [ "$counter" -eq 3 ]
	then
		echo "Hello, Sue."
	fi
	let counter=$counter + 1
done
```

Here's what's happening.

- Each time instructions within the **while** loop execute, the computer checks the value of *counter*.
- Depending on the value of *counter*, a particular welcome message appears.
- The last instruction in the **while** loop (`let counter=counter + 1`) tells the computer to add 1 to the value of *counter* and then assign this new value to *counter*. This instruction enables the computer to display all the messages.

After these instructions execute, the computer checks the value of *counter* to see whether the value is less than 5. If the value of *counter* is less than 5, the instructions execute another time. If the value of *counter* is greater than 5, the loop ends.

The preceding program took 16 lines of code to accomplish the same result as the following **for** in loop. I probably could have written in longhand in less time than it takes to simply read the code in the preceding example.

Use the following code to display a greeting to each of your three pals by using the **for** in loop:

```
for friend in Mary Joe Sue
do
	echo "Hello, $friend."
done
```

In the first line of the preceding for in loop, you follow `for friend in` with the names of your friends, which you place after the word `in`. This creates a wordlist (see the following section) and designates the names as values, which you then assign to the variable.

Notice the space between `$friend` and the following period. If you don't include this space, the program looks for a variable by the name of `friend.` (with a period) and not `friend` (without a period).

Here's what happens as this program runs:

- Your computer takes the first value and assigns it to `friend`.
- Then the greeting appears on the computer screen.
- Your computer goes back and assigns the next value to `friend`.

This sequence continues until your computer runs out of values, in which case it's greeted all your friends; then the for in loop ends.

So, you've cut down the amount of instructions that you need to type from the 16 lines using the while loop to three lines by using the for in loop. You've also made your program a lot easier to read by using the for in loop.

### Using a Wordlist

The values that you assign to the variable are known as the wordlist. A wordlist is a list of string values (a mixture of characters and numbers) that you sequentially assign to a variable, one at a time.

By the way, you can use a wordlist with other statements besides the for in loop. (I think, however, that following a routine showing how you typically use a wordlist is a better way to demonstrate its use.)

Some points to remember about a wordlist:

- Values that you assign to a wordlist must be a string value.
- You must separate each value by a space.
- You need to place values within quotation marks if a space is part of the value.

Following's an example of how to use values that contain spaces:

```
for friend in "Mary Jones" "Joe Smith" "Sue Jones"
do
	echo "Hello, $friend ."
done
```
