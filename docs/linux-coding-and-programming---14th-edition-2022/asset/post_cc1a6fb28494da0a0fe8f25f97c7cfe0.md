
## Creating Bash Scripts – Part 2

Previously we looked at creating your first Bash script, Hello World, and adding a system variable. Now you can expand these and see what you can do when you start to play around with creating your own unique variables.

### VARIABLES

Just as in every other programming language a Bash script can store and call certain variables from the system, either generic or user created.

- **STEP 1** Let's start by creating a new script called hello.sh; `xed hello.sh`. In it enter: `#!/bin/bash`, then, `echo Hello $1`. Save the file and exit Xed. Back in the Terminal make the script executable with: `chmod +x hello.sh`.

![](img/d501697c83491ed0bb4b382b0d28ef0a_69_0.png)

- **STEP 2** As the script is now executable, run it with `./hello.sh`. Now, as you probably expected a simple 'Hello' is displayed in the Terminal. However, if you then issue the command with a variable, it begins to get interesting. For example, try `./hello.sh David`.

![](img/d501697c83491ed0bb4b382b0d28ef0a_69_2.png)

- **STEP 3** The output now will be Hello David. This is because Bash automatically assigns variables for the user, which are then held and passed to the script. So the variable '$1' now holds 'David'. You can change the variable by entering something different: `./hello.sh Mint`.

![](img/d501697c83491ed0bb4b382b0d28ef0a_69_1.png)

- **STEP 4** You can even rename variables. Modify the hello.sh script with the following: `firstName=$1`, `surname=$2`, `echo Hello $firstname $surname`. Putting each statement on a new line. Save the script and exit back into the Terminal.

![](img/d501697c83491ed0bb4b382b0d28ef0a_69_3.png)

- **STEP 5** When you run the script now you can use two custom variables: `./hello.sh David Hayward`. Naturally change the two variables with your own name; unless you’re also called David Hayward. At the moment we’re just printing the contents, so let’s expand the two-variable use a little.

![](img/d501697c83491ed0bb4b382b0d28ef0a_70_0.png)

- **STEP 6** Create a new script called `addition.sh`, using the same format as the hello.sh script, but changing the variable names. Here we’ve added `firstnumber` and `secondnumber`, and changed the echo command to output some simple arithmetic by placing an integer expression, `echo $((($firstnumber+$secondnumber)))`. Save the script, and make it executable (`chmod +x addition.sh`).

![](img/d501697c83491ed0bb4b382b0d28ef0a_70_1.png)

- **STEP 7** When you now run the addition.sh script we can enter two numbers: `./addition.sh 1 2`. The result will hopefully be 3, with the terminal displaying ‘The sum is 3’. Try it with a few different numbers and see what happens. See also if you can alter the script and rename it to multiplication, and subtraction.

![](img/d501697c83491ed0bb4b382b0d28ef0a_70_2.png)

- **STEP 8** Let’s expand things further. Create a new script called `greetings.sh`. Enter the scripting as below in the screenshot, save it and make it executable with the `chmod` command. You can see that there are a few new additions to the script now.

![](img/d501697c83491ed0bb4b382b0d28ef0a_70_3.png)

- **STEP 9** We’ve added a `-n` to the echo command here which will leave the cursor on the same line as the question, instead of a new line. The `read` command stores the user’s input as the variables `firstname` and `surname`, to then read back later in the last echo line. And the `clear` command clears the screen.

![](img/d501697c83491ed0bb4b382b0d28ef0a_70_4.png)

- **STEP 10** As a final addition, let’s include the date variable we used in the last section. Amend the last line of the script to read: `echo Hello $firstname $surname, how are you on this fine day $(date +%A)?`. The output should display the current day of the week, calling it from a system variable.

![](img/d501697c83491ed0bb4b382b0d28ef0a_70_5.png)

## Creating Bash Scripts – Part 3

In the previous pages we looked at some very basic Bash scripting, which involved outputting text to the screen, getting a user's input, storing it and outputting that to the screen; as well as including a system variable using the Date command. Now let's combine what you've achieved so far and introduce Loops.

### IF, THEN, ELSE

With most programming structures there will come a time where you need to loop through the commands you've entered to create better functionality, and ultimately a better program.

- **STEP 1** Let's look at the If, Then and Else statements now, which when executed correctly, compare a set of instructions and simply work out that if something is present, THEN do something, ELSE do something different. Create a new script called `greeting2.sh` and enter the text in the screenshot below into it.

![](img/d501697c83491ed0bb4b382b0d28ef0a_71_0.png)

- **STEP 2** `greeting2.sh` is a copy of `greeting.sh` but with a slight difference. Here we've added a loop starting at the if statement. This means, if the variable entered is equal to David the next line, THEN, is the reaction to what happens, in this case it will output to the screen 'Awesome name', followed by the variable (which is David).

![](img/d501697c83491ed0bb4b382b0d28ef0a_71_1.png)

- **STEP 3** The next line, ELSE, is what happens if the variable doesn't equal 'David'. In this case it simply outputs to the screen the now familiar 'Hello...'. The last line, the FI statement, is the command that will end the loop. If you have an if command without a FI command, you get an error.

![](img/d501697c83491ed0bb4b382b0d28ef0a_71_2.png)

- **STEP 4** You can obviously play around with the script a little, changing the name variable that triggers a response, or maybe even issuing a response where the first name and surname variables match a specific variable.

![](img/d501697c83491ed0bb4b382b0d28ef0a_71_3.png)

### MORE LOOPING

You can loop over data using the FOR, WHILE and UNTIL statements. These can be handy if you’re batch naming, copying or running a script where a counter is needed.

- **STEP 1** Create a new script called count.sh. Enter the text in the screenshot below, save it and make it executable. This creates the variable 'count' which at the beginning of the script equals zero. Then start the WHILE loop, which WHILE count is less than (the LT part) 100 will print the current value of count in the echo command.

![](img/d501697c83491ed0bb4b382b0d28ef0a_72_0.png)

- **STEP 2** Executing the count.sh script will result in the numbers 0 to 99 listing down the Terminal screen; when it reaches 100 the script will end. Modifying the script with the FOR statement, makes it work in much the same way. To use it in our script, enter the text from the Screenshot into the count.sh script.

![](img/d501697c83491ed0bb4b382b0d28ef0a_72_1.png)

- **STEP 3** The addition we have here is: `for count in {0..100}; do`, which means FOR the variable 'count' IN the numbers from zero to one hundred, then start the loop. The rest of the script is the same. Run this script, and the same output should appear in the Terminal.

![](img/d501697c83491ed0bb4b382b0d28ef0a_72_2.png)

- **STEP 4** The UNTIL loop works much the same way as the WHILE loop only, more often than not, in reverse. So our counting to a hundred, using UNTIL, would be: `until [ $count -gt 100 ]; do`. The difference being, UNTIL count is greater than (the gt part) one hundred, keep on looping.

![](img/d501697c83491ed0bb4b382b0d28ef0a_72_3.png)

- **STEP 5** You’re not limited to numbers zero to one hundred. You can, within the loop, have whatever set of commands you like and execute them as many times as you want the loop to run for. Renaming a million files, creating fifty folders etc. For example, this script will create ten folders named folder1 through to folder10 using the FOR loop.

![](img/d501697c83491ed0bb4b382b0d28ef0a_72_4.png)

- **STEP 6** Using the FOR statement once more, we can execute the counting sequence by manipulating the `(0..100)` part. This section of the code actually means `[START..END..INCREMENT]`, if there’s no increment then it’s just a single digit up to the END. For example, we could get the loops to count up to 1000 in two’s with: `for count in {0..1000..2}; do`.

![](img/d501697c83491ed0bb4b382b0d28ef0a_72_5.png)
